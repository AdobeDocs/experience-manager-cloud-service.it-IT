---
title: Funzioni obsolete e rimosse
description: Note sulla versione specifiche delle funzioni obsolete e rimosse di Adobe Experience Manager come servizio Cloud.
translation-type: tm+mt
source-git-commit: b31ae32285080075d2531edd2c4976cf801d1c89

---


# Deprecated and removed features {#deprecated-and-removed-features}

Adobe valuta costantemente le capacità dei prodotti, per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne per migliorare il valore complessivo dei clienti, sempre in considerazione della compatibilità con le versioni precedenti. Inoltre, poiché Adobe Experience Manager come servizio Cloud fornisce un modello di distribuzione nativo per il cloud, alcune funzionalità e funzionalità sono state sostituite da controparti native per il cloud.

Per comunicare l’imminente rimozione/sostituzione delle funzionalità AEM, si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Le funzionalità obsolete continuano a essere disponibili ma non vengono ulteriormente migliorate.
1. Le funzionalità annunciate come obsolete vengono rimosse nella release principale successiva, non appena possibile. Viene annunciata la data di destinazione effettiva per la rimozione.

Questo processo offre ai clienti almeno un processo di pubblicazione per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Deprecated features {#deprecated-features}

In questa sezione sono elencate le funzionalità contrassegnate come obsolete in Experience Manager come servizio Cloud. In genere, le funzioni pianificate per essere rimosse in una versione futura sono impostate per prime su obsoleta, con un&#39;alternativa fornita.

Consigliamo ai clienti di verificare se utilizzano la funzione/funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Area | Funzione | Sostituzione |
| ------------ | ------------------ | ----------- |
| Assets | L&#39;assimilazione e l&#39;elaborazione delle risorse non utilizzano più `DAM Asset Update` il flusso di lavoro | L’assimilazione delle risorse utilizza ora i microservizi [delle](/help/assets/asset-microservices-overview.md) risorse. |
| Assets | Caricare le risorse direttamente in AEM - consultate API di caricamento delle risorse [obsolete](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) | [Il caricamento](/help/assets/add-assets.md) binario diretto viene utilizzato in Experience Manager come servizio cloud. Per informazioni tecniche, consultate API di caricamento [diretto](/help/assets/developer-reference-material-apis.md#overview-binary-upload). |
| Assets | [Alcuni passaggi](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) `DAM Asset Update` del flusso di lavoro non sono supportati, inclusa la chiamata di strumenti della riga di comando come ImageMagick | [I microservizi](/help/assets/asset-microservices-overview.md) delle risorse sostituiscono molti flussi di lavoro. Per l’elaborazione personalizzata, utilizzate i flussi di lavoro [di](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)post-elaborazione. |

## Removed features {#removed-features}

In questa sezione sono elencate le funzionalità e le funzionalità rimosse da AEM con Experience Manager come servizio Cloud.

| Area | Funzione | Sostituzione |
| ------------ | ------------------ | ----------- |
| Interfaccia | Alcune finestre di dialogo dell’interfaccia classica rimangono al momento disponibili per alcune funzionalità, come Controllo collegamenti, Rimozione versioni e alcune configurazioni del servizio cloud, ma l’accesso all’interfaccia classica in generale è stato rimosso dall’interfaccia utente del prodotto AEM. | Interfaccia standard |
| Dynamic Media | Le precedenti integrazioni con [Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/scene7.html) e la modalità [](https://helpx.adobe.com/experience-manager/6-5/assets/using/config-dynamic.html) Dynamic Media Hybrid non sono disponibili in AEM come servizio cloud. | Utilizzate [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) fornito con Experience Manager come servizio Cloud. |
| Sites | Direttore del portale e componente Portlet | Queste funzionalità erano obsolete in AEM 6.4 e ora sono state rimosse da AEM. |
| Sites | Importazione progettazione | Questa funzionalità è stata rimossa perché le sezioni immutabili dell’archivio AEM non sono accessibili in fase di esecuzione. |
| Assets | [La condivisione di AEM Assets con il servizio di base Marketing Cloud Assets e i servizi](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) Creative Cloud non è disponibile. | Per l’integrazione con Creative Cloud, utilizzate [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html). |
