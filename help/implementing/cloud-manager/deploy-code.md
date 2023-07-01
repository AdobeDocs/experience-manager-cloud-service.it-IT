---
title: Distribuzione del codice
description: Scopri come distribuire il codice con le pipeline di Cloud Manager in AEM as a Cloud Service.
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 89%

---


# Distribuzione del codice {#deploy-your-code}

Scopri come distribuire il codice nell’ambiente di produzione con le pipeline di Cloud Manager in AEM as a Cloud Service.

![Diagramma della pipeline di produzione](./assets/configure-pipeline/production-pipeline-diagram.png)

La distribuzione del codice nell’ambiente di staging e successivamente nell’ambiente di produzione avviene tramite una pipeline di produzione. L’esecuzione della pipeline di produzione è suddivisa in due fasi logiche.

1. Distribuzione nell’ambiente di staging
   * Il codice viene generato e distribuito nell’ambiente di staging per test funzionali automatizzati, test dell’interfaccia utente, audit dell’esperienza e test di accettazione utente (UAT).
1. Distribuzione nell’ambiente di produzione
   * Dopo aver convalidato la build nell’ambiente di staging e averla approvata per la promozione all’ambiente di produzione, l’artefatto di build viene distribuito nell’ambiente di produzione.

_Solo la pipeline del codice full stack supporta il controllo del codice, i test funzionali, i test dell’interfaccia utente e l’audit dell’esperienza._

## Distribuzione del codice con Cloud Manager in AEM as a Cloud Service {#deploying-code-with-cloud-manager}

Dopo aver [configurato la pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) includendo archivio, ambiente e ambiente di test, tutto è pronto per la distribuzione del codice.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic sul programma per il quale desideri distribuire il codice.

1. Per avviare il processo di distribuzione, dall’invito all’azione presente nella schermata **Panoramica**, fai clic su **Distribuisci**.

   ![Invito all’azione](assets/deploy-code1.png)

1. Si apre la schermata **Esecuzione delle pipeline**. Per avviare il processo, fai clic su **Genera**.

   ![Schermata di esecuzione della pipeline](assets/deploy-code2.png)

Il processo di build distribuisce il codice in tre fasi.

1. [Implementazione nell’ambiente di staging](#stage-deployment)
1. [Test nell’ambiente di staging](#stage-testing)
1. [Implementazione nell’ambiente di produzione](#production-deployment)

>[!TIP]
>
>Puoi rivedere i passaggi da vari processi di distribuzione visualizzando i registri o rivedendo i risultati per i criteri di test.

## Fase di implementazione nell’ambiente di staging {#stage-deployment}

La fase di **implementazione nell’ambiente di staging** prevede i passaggi riportati di seguito.

* **Convalida**: questo passaggio garantisce che la pipeline sia configurata per utilizzare le risorse attualmente disponibili. Ad esempio, i test per verificare che il ramo configurato esista e che gli ambienti siano disponibili.
* **Test della build e unit test**: questo passaggio esegue un processo di build in contenitori.
   * Consulta [Dettagli dell’ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) per informazioni dettagliate sull’ambiente di build.
* **Controllo del codice**: questo passaggio valuta la qualità del codice dell’applicazione.
   * Consulta [Test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) per informazioni dettagliate sulla procedura di test.
* **Genera immagini**: questo processo è responsabile della trasformazione in immagini Docker e configurazioni di Kubernetes dei pacchetti di contenuti e dispatcher generati dalla fase di build.
* **Implementazione nell’ambiente di staging**: l’immagine viene implementata nell’ambiente di staging in preparazione alla [fase di test nell’ambente di staging.](#stage-testing)

![Implementazione nell’ambiente di staging](assets/stage-deployment.png)

## Fase di test nell’ambiente di staging {#stage-testing}

La fase di **test nell’ambiente di staging** prevede i seguenti passaggi.

* **Test funzionali del prodotto**: la pipeline di Cloud Manager esegue i test per l’ambiente di staging.
   * Consulta [Test funzionali del prodotto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) per ulteriori dettagli.

* **Test funzionali personalizzato**: questo passaggio nella pipeline viene sempre eseguito e non può essere saltato. Se la build non produce JAR di test, il test viene superato per impostazione predefinita.
   * Consulta [Test funzionali personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) per ulteriori dettagli.

* **Test dell’interfaccia utente personalizzati**: questo passaggio è una funzione facoltativa che esegue automaticamente i test dell’interfaccia utente creati per le applicazioni personalizzate.
   * I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in termini di linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium).
   * Consulta [Test dell’interfaccia utente personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) per ulteriori dettagli.

* **Audit dell’esperienza**: questo passaggio nella pipeline viene sempre eseguito e non può essere saltato. Quando si esegue una pipeline di produzione, viene incluso un passaggio di audit dell’esperienza dopo i test funzionali personalizzati che eseguiranno i controlli.
   * Le pagine configurate vengono inviate al servizio e valutate.
   * I risultati sono informativi e mostrano i punteggi e cosa è cambiato tra il punteggio corrente e quello precedente.
   * Questa informazione è utile per determinare se c’è una regressione introdotta con la distribuzione corrente.
   * Consulta [I risultati dell’audit dell’esperienza](/help/implementing/cloud-manager/experience-audit-testing.md) per ulteriori dettagli.

![Test nell’ambiente di staging](assets/stage-testing.png)

## Fase di implementazione nell’ambiente di produzione {#deployment-production}

Il processo di distribuzione nelle topologie di produzione è leggermente diverso per ridurre al minimo l’impatto sui visitatori di un sito AEM.

Le implementazioni nell’ambiente di produzione seguono generalmente la stessa procedura descritta in precedenza, ma in modo continuo.

1. Distribuire i pacchetti AEM nel servizio Author.
1. Scollegare dispatcher1 dal load balancer.
1. Distribuire i pacchetti AEM in publish1 e il pacchetto dispatcher in dispatcher1; svuotare la cache del dispatcher.
1. Ripristinare dispatcher1 nel load balancer.
1. Dopo aver ripristinato il servizio di dispatcher1, scollegare dispatcher2 dal load balancer.
1. Distribuire i pacchetti AEM in publish2 e il pacchetto dispatcher in dispatcher2; svuotare la cache del dispatcher.
1. Ripristinare dispatcher2 nel load balancer.

Questo processo continua fino al completamento della distribuzione in tutti gli elementi Publish e Dispatcher nella topologia.

![Fase di distribuzione nell’ambiente di produzione](assets/production-deployment.png)

## Timeout {#timeouts}

Per i seguenti passaggi è previsto un timeout in caso di attesa del feedback dell’utente:

| Passaggio | Timeout |
|--- |--- |
| Test di qualità del codice | 14 giorni |
| Test di sicurezza | 14 giorni |
| Test delle prestazioni | 14 giorni |
| Domanda di approvazione | 14 giorni |
| Pianificazione della distribuzione nell’ambiente di produzione | 14 giorni |
| Supporto CSE | 14 giorni |

## Processo di distribuzione {#deployment-process}

Tutte le distribuzioni di Cloud Service seguono un processo continuo per garantire l’operatività continua. Consulta [Funzionamento delle distribuzioni continue](/help/implementing/deploying/overview.md#how-rolling-deployments-work) per ulteriori informazioni.

>[!NOTE]
>
>La cache del Dispatcher viene cancellata su ogni distribuzione. Subisce successivamente un processo di riscaldamento prima che i nuovi nodi di pubblicazione accettino il traffico.

## Riesecuzione di una distribuzione nell’ambiente di produzione {#Reexecute-Deployment}

La riesecuzione del passaggio di distribuzione nell’ambiente di produzione è supportata per le esecuzioni in cui il suddetto passaggio è stato completato. Il tipo di completamento non è importante: la distribuzione può essere stata annullata o non riuscita. Detto ciò, il caso d’uso principale è quello in cui il passaggio di distribuzione nell’ambiente di produzione non è riuscito per motivi transitori. La riesecuzione crea una nuova esecuzione utilizzando la stessa pipeline. La nuova esecuzione consiste di tre passaggi:

1. Passaggio di convalida: si tratta essenzialmente della stessa convalida prevista durante una normale esecuzione della pipeline.
1. Fase di build: nel contesto di una nuova esecuzione, la fase di build copia gli artefatti senza eseguire effettivamente un nuovo processo di build.
1. Passaggio di distribuzione nell’ambiente di produzione: utilizza la stessa configurazione e le stesse opzioni del passaggio di distribuzione nell’ambiente di produzione previste per una normale esecuzione della pipeline.

La fase di build può essere etichettata in modo leggermente diverso nell’interfaccia utente per indicare la copia degli artefatti e non un nuovo processo di build.

![Ridistribuzione](assets/Re-deploy.png)

Limiti:

* La riesecuzione del passaggio di distribuzione nell’ambiente di produzione è disponibile solo per l’ultima esecuzione.
* La riesecuzione non è disponibile per le esecuzioni degli aggiornamenti push. Se l’ultima esecuzione è un aggiornamento push, non è possibile eseguirla nuovamente.
* Se l’ultima esecuzione è un aggiornamento push, non è possibile eseguirla nuovamente.
* Se l’ultima esecuzione non è riuscita in un qualsiasi punto precedente al passaggio di distribuzione nell’ambiente di produzione, non è possibile eseguirla nuovamente.

### Riesecuzione dell’API {#Reexecute-API}

### Identificazione di un’esecuzione rieseguita

Per identificare se un’esecuzione è stata rieseguita, verifica il campo trigger. Il suo valore è *RI_ESEGUI*.

### Attivazione di una nuova esecuzione

Per attivare una nuova esecuzione è necessario effettuare una richiesta PUT al collegamento HAL &lt;(<https://ns.adobe.com/adobecloud/rel/pipeline/reExecute>)> dello stato del passaggio di distribuzione nell’ambiente di produzione. Se questo collegamento è presente, l’esecuzione può essere riavviata da quel passaggio. Se assente, l’esecuzione non può essere riavviata da quel passaggio. Nella versione iniziale, il collegamento sarà sempre presente solo nel passaggio di distribuzione nell’ambiente di produzione, ma le versioni future potrebbero supportare l’avvio della pipeline da altri passaggi. Esempio:

```JavaScript
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


La sintassi del valore _href_ del collegamento HAL di cui sopra non è concepita per essere utilizzata come punto di riferimento. Il valore effettivo deve sempre essere letto dal collegamento HAL e non generato.

Invio di un *PUT* la richiesta a questo endpoint restituisce un *201* response if success (risposta in caso di esito positivo); il corpo della risposta è la rappresentazione della nuova esecuzione. È simile all’avvio di un’esecuzione normale tramite l’API.
