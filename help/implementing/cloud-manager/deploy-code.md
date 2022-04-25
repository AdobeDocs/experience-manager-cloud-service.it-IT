---
title: Implementazione del codice
description: Scopri come distribuire il codice utilizzando le pipeline di Cloud Manager in AEM as a Cloud Service.
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: feee55b2d1814b14121030b2ec3c0cb286e87044
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 1%

---


# Implementazione del codice {#deploy-your-code}

Scopri come distribuire il codice utilizzando le pipeline di Cloud Manager in AEM as a Cloud Service.

## Implementazione del codice con Cloud Manager in AEM as a Cloud Service {#deploying-code-with-cloud-manager}

Una volta che [configurato la pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) tra cui archivio, ambiente e ambiente di test, puoi distribuire il codice.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione appropriata.

1. Fai clic sul programma per il quale vuoi distribuire il codice.

1. Fai clic su **Distribuzione** dall&#39;invito all&#39;azione sul **Panoramica** per avviare il processo di distribuzione.

   ![CTA](assets/deploy-code1.png)

1. La **Esecuzione della pipeline** viene visualizzato lo schermo. Fai clic su **Crea** per avviare il processo.

   ![Schermata di esecuzione della pipeline](assets/deploy-code2.png)

Il processo di compilazione distribuisce il codice in tre fasi.

1. [Implementazione fase](#stage-deployment)
1. [Test della fase](#stage-testing)
1. [Distribuzione di produzione](#production-deployment)

>[!TIP]
>
>Puoi rivedere i passaggi da vari processi di distribuzione visualizzando i registri o rivedendo i risultati per i criteri di test.

## Fase di distribuzione {#stage-deployment}

La **Implementazione fase** fase. comporta questi passaggi.

* **Convalida**  - Questo passaggio assicura che la pipeline sia configurata per l’utilizzo delle risorse attualmente disponibili. Ad esempio, verificare che il ramo configurato esista e che gli ambienti siano disponibili.
* **Build &amp; Unit Testing** - Questo passaggio esegue un processo di compilazione containerizzato.
   * Vedi il documento [Dettagli dell’ambiente di generazione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) per informazioni dettagliate sull’ambiente di creazione.
* **Scansione del codice** - Questo passaggio valuta la qualità del codice dell&#39;applicazione.
   * Vedi il documento [Test della qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) per informazioni dettagliate sul processo di test.
* **Creare immagini** - Questo processo è responsabile della trasformazione dei pacchetti di contenuti e dispatcher prodotti dalla fase di creazione in immagini Docker e configurazioni Kubernetes.
* **Distribuisci su Stage** - L&#39;immagine viene distribuita nell&#39;ambiente di staging in preparazione della [Fase di prova.](#stage-testing)

![Implementazione fase](assets/stage-deployment.png)

## Fase di prova {#stage-testing}

La **Test della fase** La fase comporta questi passaggi.

* **Test funzionale del prodotto** - La pipeline di Cloud Manager esegue i test eseguiti sull’ambiente stage.
   * Fare riferimento al documento [Test funzionale del prodotto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) per ulteriori dettagli.

* **Test funzionale personalizzato** - Questo passaggio nella pipeline viene sempre eseguito e non può essere ignorato. Se la build non produce JAR di test, il test viene superato per impostazione predefinita.
   * Fare riferimento al documento [Test funzionale personalizzato](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) per ulteriori dettagli.

* **Test personalizzati dell&#39;interfaccia utente** - Questa fase è una funzionalità facoltativa che esegue automaticamente i test dell’interfaccia utente creati per le applicazioni personalizzate.
   * I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium).
   * Fare riferimento al documento [Test personalizzati dell&#39;interfaccia utente](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) per ulteriori dettagli.

* **Audit delle esperienze** - Questo passaggio nella pipeline viene sempre eseguito e non può essere ignorato. Quando viene eseguita una pipeline di produzione, viene incluso un passaggio di controllo dell’esperienza dopo un test funzionale personalizzato che eseguirà i controlli.
   * Le pagine configurate vengono inviate al servizio e valutate.
   * I risultati sono informativi e mostrano i punteggi e il cambiamento tra il punteggio corrente e quello precedente.
   * Questa informazione è utile per determinare se vi è una regressione che verrà introdotta con la distribuzione corrente.
   * Fare riferimento al documento [Informazioni sui risultati di Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md) per ulteriori dettagli.

![Test della fase](assets/stage-testing.png)

## Fase di distribuzione della produzione {#deployment-production}

Il processo di distribuzione nelle topologie di produzione è leggermente diverso al fine di ridurre l’impatto sui visitatori di un sito AEM.

Le distribuzioni di produzione seguono generalmente gli stessi passaggi descritti in precedenza, ma in modo continuo.

1. Distribuisci pacchetti AEM per l’authoring.
1. Scollega dispatcher1 dal load balancer.
1. Distribuisci pacchetti AEM a publish1 e il pacchetto dispatcher a dispatcher1, svuota la cache del dispatcher.
1. Rimetti dispatcher1 nel load balancer.
1. Una volta che dispatcher1 è tornato in servizio, scollega dispatcher2 dal load balancer.
1. Distribuisci pacchetti AEM a publish2 e il pacchetto dispatcher a dispatcher2, svuota la cache del dispatcher.
1. Rimetti dispatcher2 nel load balancer.

Questo processo continua fino a quando la distribuzione non raggiunge tutti gli editori e i dispatcher nella topologia.

![Fase di implementazione della produzione](assets/production-deployment.png)

## Timeout {#timeouts}

I seguenti passaggi si interrompono se rimangono in attesa del feedback degli utenti:

| Incremento | Timeout |
|--- |--- |
| Test della qualità del codice | 14 giorni |
| Test di sicurezza | 14 giorni |
| Test delle prestazioni | 14 giorni |
| Domanda di approvazione | 14 giorni |
| Pianificazione distribuzione produzione | 14 giorni |
| Supporto CSE | 14 giorni |

## Processo di distribuzione {#deployment-process}

Tutte le distribuzioni di Cloud Service seguono un processo continuo per garantire tempi di inattività pari a zero. Fare riferimento al documento [Funzionamento delle implementazioni continue](/help/implementing/deploying/overview.md#how-rolling-deployments-work) per saperne di più.