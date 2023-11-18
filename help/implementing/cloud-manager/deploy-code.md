---
title: Distribuzione del codice
description: Scopri come distribuire il codice con le pipeline di Cloud Manager in AEM as a Cloud Service.
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 91%

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
* **Test di build e dell’unità**: questo passaggio esegue un processo di compilazione containerizzato.
   * Per ulteriori informazioni sull’ambiente di build, consulta il documento [Dettagli sull’ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md).
* **Analisi del codice**: questo passaggio valuta la qualità del codice dell’applicazione.
   * Per ulteriori informazioni sul processo di test, consulta il documento [Test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md).
* **Genera immagini**: questo processo è responsabile della trasformazione in immagini Docker e configurazioni di Kubernetes dei pacchetti di contenuti e dispatcher generati dalla fase di build.
* **Implementazione nell’ambiente di staging**: l’immagine viene implementata nell’ambiente di staging in preparazione alla [fase di test nell’ambente di staging.](#stage-testing)

![Implementazione nell’ambiente di staging](assets/stage-deployment.png)

## Fase di test nell’ambiente di staging {#stage-testing}

La fase di **test nell’ambiente di staging** prevede i seguenti passaggi.

* **Test funzionali del prodotto**: la pipeline di Cloud Manager esegue i test per l’ambiente di staging.
   * Per ulteriori dettagli, consulta [Test funzionali del prodotto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing).

* **Test funzionali personalizzato**: questo passaggio nella pipeline viene sempre eseguito e non può essere saltato. Se la build non produce JAR di test, il test viene superato per impostazione predefinita.
   * Per ulteriori dettagli, consulta [Test funzionali personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing).

* **Test dell’interfaccia utente personalizzati**: questo passaggio è una funzione facoltativa che esegue automaticamente i test dell’interfaccia utente creati per le applicazioni personalizzate.
   * I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in termini di linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium).
   * Per ulteriori dettagli, consulta [Test dell’interfaccia utente personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing).

* **Audit dell’esperienza**: questo passaggio nella pipeline viene sempre eseguito e non può essere saltato. Quando si esegue una pipeline di produzione, viene incluso un passaggio di audit dell’esperienza dopo i test funzionali personalizzati che eseguiranno i controlli.
   * Le pagine configurate vengono inviate al servizio e valutate.
   * I risultati sono informativi e mostrano i punteggi e cosa è cambiato tra il punteggio corrente e quello precedente.
   * Questo approfondimento e è utile per determinare l’eventuale introduzione di una regressione con la distribuzione corrente.
   * Per ulteriori informazioni, consulta la sezione dedicata alla [lettura dei risultati dell’audit dell’esperienza](/help/implementing/cloud-manager/experience-audit-testing.md).

![Test nell’ambiente di staging](assets/stage-testing.png)

## Fase di implementazione nell’ambiente di produzione {#deployment-production}

Il processo di implementazione nelle topologie di produzione è leggermente diverso per ridurre l’impatto sui visitatori di un sito AEM.

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

Tutte le distribuzioni di Cloud Service seguono un processo continuo per garantire l’operatività continua. Per ulteriori informazioni, consulta [Funzionamento delle implementazioni continue](/help/implementing/deploying/overview.md#how-rolling-deployments-work).

>[!NOTE]
>
>La cache del Dispatcher viene cancellata su ogni distribuzione. Subisce successivamente un processo di riscaldamento prima che i nuovi nodi di pubblicazione accettino il traffico.

## Eseguire nuovamente una distribuzione di produzione {#reexecute-deployment}

In rari casi, i passaggi di distribuzione nell’ambiente di produzione possono non riuscire per motivi transitori. In questi casi, la riesecuzione del passaggio di distribuzione nell’ambiente di produzione è supportata fino a quando il passaggio di distribuzione nell’ambiente di produzione è stato completato, indipendentemente dal tipo di completamento (ad esempio, annullato o non riuscito). La riesecuzione crea una nuova esecuzione utilizzando la stessa pipeline costituita da tre passaggi.

1. Passaggio di convalida: si tratta essenzialmente della stessa convalida che si verifica durante una normale esecuzione della pipeline.
1. Passaggio di compilazione: nel contesto di una riesecuzione, il passaggio di compilazione copia gli artefatti e non esegue effettivamente un nuovo processo di compilazione.
1. Passaggio di distribuzione della produzione: questa opzione utilizza la stessa configurazione e le stesse opzioni del passaggio di distribuzione di produzione in una normale esecuzione della pipeline.

In tali circostanze, in cui è possibile eseguire una riesecuzione, la pagina di stato della pipeline di produzione fornisce l’opzione **Riesegui** accanto a quella consueta di **Scarica registro build**.

![Opzione Riesegui nella finestra di panoramica sulla pipeline](assets/re-execute.png)

>[!NOTE]
>
>In una riesecuzione, il passaggio di compilazione viene etichettato nell’interfaccia utente, per rispecchiare la copia degli artefatti non la ricompilazione.

### Limitazioni {#limitations}

* La riesecuzione del passaggio di distribuzione nell’ambiente di produzione è disponibile solo per l’ultima esecuzione.
* La riesecuzione non è disponibile per le esecuzioni degli aggiornamenti push.
   * Se l’ultima esecuzione è un aggiornamento push, non è possibile eseguirla nuovamente.
* Se l’ultima esecuzione non è riuscita in un qualsiasi punto precedente al passaggio di distribuzione nell’ambiente di produzione, non è possibile eseguirla nuovamente.

### Riesecuzione dell’API {#reexecute-API}

Oltre a essere disponibile nell’interfaccia utente, è possibile utilizzare l’[API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Pipeline-Execution) per attivare le riesecuzioni e identificare le esecuzioni attivate come riesecuzioni.

#### Attivazione di una riesecuzione {#reexecute-deployment-api}

Per attivare una nuova esecuzione, effettua una richiesta PUT al collegamento HAL `https://ns.adobe.com/adobecloud/rel/pipeline/reExecute` nello stato del passaggio di distribuzione nell’ambiente di produzione.

* Se tale collegamento è presente, l’esecuzione può essere riavviata da quel passaggio.
* Se assente, l’esecuzione non può essere riavviata da quel passaggio.

Questo collegamento è disponibile solo per il passaggio di distribuzione nell’ambiente di produzione.

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

La sintassi del valore href del collegamento HAL è solo un esempio. Il valore effettivo deve sempre essere letto dal collegamento HAL e non generato.

L’invio di una richiesta PUT a questo endpoint genera una risposta 201 in caso di esito positivo; il corpo della risposta è la rappresentazione della nuova esecuzione. È simile all’avvio di un’esecuzione normale tramite l’API.

#### Identificazione di un’esecuzione rieseguita {#identify-reexecution}

Le riesecuzioni possono essere identificate dal valore `RE_EXECUTE` nel `trigger` campo.
