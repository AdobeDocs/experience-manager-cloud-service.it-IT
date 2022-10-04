---
title: Implementazione del codice
description: Scopri come distribuire il codice utilizzando le pipeline di Cloud Manager in AEM as a Cloud Service.
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: cb08fcbd6c1060466ca9e6b4639774d43b70c83c
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 2%

---


# Implementazione del codice {#deploy-your-code}

Scopri come distribuire il codice in Produzione utilizzando le pipeline di Cloud Manager in AEM as a Cloud Service.

![Diagramma della pipeline di produzione](./assets/configure-pipeline/production-pipeline-diagram.png)

La distribuzione del codice in Stage e poi in Produzione avviene tramite una pipeline di produzione. L’esecuzione della pipeline di produzione è suddivisa in due fasi logiche.

1. Implementazione in ambiente stage
   * Il codice viene generato e distribuito nell’ambiente Stage per test funzionali automatizzati, test dell’interfaccia utente, audit dell’esperienza e test di accettazione da parte degli utenti (UAT).
1. Implementazione in ambiente di produzione
   * Una volta convalidata la build sullo stage e approvata per la promozione su Produzione, lo stesso artefatto di build viene distribuito nell’ambiente di produzione.

_Solo il tipo di pipeline Full Stack Code supporta la scansione del codice, il test delle funzioni, il test dell’interfaccia utente e il controllo dell’esperienza._

## Implementazione del codice con Cloud Manager in AEM as a Cloud Service {#deploying-code-with-cloud-manager}

Una volta che [configurato la pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) tra cui archivio, ambiente e ambiente di test, puoi distribuire il codice.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

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

>[!NOTE]
>
>La cache del Dispatcher viene cancellata su ogni distribuzione. Viene successivamente riscaldato prima che i nuovi nodi di pubblicazione accetti il traffico.

## Esegui nuovamente una distribuzione di produzione {#Reexecute-Deployment}

La riesecuzione del passaggio di distribuzione di produzione è supportata per le esecuzioni in cui il passaggio di distribuzione di produzione è stato completato. Il tipo di completamento non è importante: la distribuzione potrebbe essere annullata o non riuscita. Detto questo, si prevede che il caso d’uso principale sia quello in cui la fase di distribuzione della produzione non è riuscita per motivi transitori. La nuova esecuzione crea una nuova esecuzione utilizzando la stessa pipeline. Questa nuova esecuzione consiste in tre fasi:

1. Passaggio di convalida : si tratta essenzialmente della stessa convalida che si verifica durante una normale esecuzione della pipeline.
1. Passaggio della build: nel contesto di una nuova esecuzione, il passaggio della build sta copiando gli artefatti e non esegue effettivamente un nuovo processo di compilazione.
1. Passaggio di distribuzione di produzione : utilizza la stessa configurazione e le stesse opzioni del passaggio di distribuzione di produzione in una normale esecuzione della pipeline.

Il passaggio di compilazione può essere etichettato in modo leggermente diverso nell’interfaccia utente per indicare che sta copiando gli artefatti, non sta ricostruendo.

![Ridistribuzione](assets/Re-deploy.png)

Limiti:

* La riesecuzione del passaggio di distribuzione di produzione sarà disponibile solo all’ultima esecuzione.
* La riesecuzione non è disponibile per le esecuzioni dell’aggiornamento push. Se l’ultima esecuzione è un’esecuzione di aggiornamento push, non è possibile eseguirla nuovamente.
* Se l’ultima esecuzione è un’esecuzione di aggiornamento push, non è possibile eseguirla nuovamente.
* Se l’ultima esecuzione non è riuscita in un qualsiasi punto prima della fase di distribuzione della produzione, non è possibile eseguire nuovamente l’esecuzione.

### Esegui nuovamente l’API {#Reexecute-API}

### Identificazione di un’esecuzione di nuova esecuzione

Per identificare se un’esecuzione è un’esecuzione di nuova esecuzione, è possibile esaminare il campo trigger. Il suo valore sarà *RE_EXECUTE*.

### Attivazione di una nuova esecuzione

Per attivare una nuova esecuzione, è necessario effettuare una richiesta PUT al collegamento HAL &lt;(<https://ns.adobe.com/adobecloud/rel/pipeline/reExecute>)> sullo stato del passaggio di distribuzione di produzione. Se questo collegamento è presente, l’esecuzione può essere riavviata da quel passaggio. Se è assente, l’esecuzione non può essere riavviata da quel passaggio. Nella versione iniziale, questo collegamento sarà sempre presente solo nel passaggio di distribuzione della produzione, ma le versioni future potrebbero supportare l’avvio della pipeline da altri passaggi. Esempio:

```Javascript
 {
  "_links": {
    "https://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```


Sintassi del collegamento HAL _href_  il valore di cui sopra non è destinato ad essere utilizzato come punto di riferimento. Il valore effettivo deve sempre essere letto dal collegamento HAL e non generato.

Invio di un *PUT* la richiesta a questo endpoint darà luogo a un *201* in caso di esito positivo, l’organo di risposta sarà la rappresentazione della nuova esecuzione. È simile all’avvio di un’esecuzione regolare tramite l’API .
