---
title: Funzioni obsolete e rimosse
description: Note sulla versione specifiche per le funzioni obsolete e rimosse in Adobe Experience Manager as a Cloud Service.
translation-type: ht
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

---


# Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe valuta costantemente le funzionalità dei prodotti, per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti. Inoltre, poiché Adobe Experience Manager as a Cloud Service offre un modello di distribuzione nativo per il cloud, alcune funzionalità e funzioni sono state sostituite da controparti native per il cloud.

Per comunicare l’imminente rimozione/sostituzione delle funzionalità AEM, si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Le funzionalità obsolete rimangono comunque disponibili, ma non vengono più aggiornate.
1. Le funzionalità annunciate come obsolete vengono rimosse nella versione principale successiva, non appena possibile. La data effettiva per la rimozione viene annunciata.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzioni e le funzionalità contrassegnate come obsolete in Experience Manager as a Cloud Service. In genere, le funzioni pianificate per la rimozione in una versione futura vengono prima impostate come obsolete e ne viene indicata un’alternativa.

Consigliamo ai clienti di verificare se utilizzano la funzione o funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Funzionalità | Funzione obsoleta | Sostituzione |
| ------------ | ------------------ | ----------- |
| Assets | Flusso di lavoro di `DAM Asset Update` per elaborare le immagini acquisite. | Per l’inserimento delle risorse si utilizzano ora i [microservizi per le risorse](/help/assets/asset-microservices-overview.md). |
| Assets | Le risorse vengono caricate direttamente in AEM. Consulta l’articolo sulle [API di caricamento risorse dichiarate obsolete](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Utilizza il [caricamento binario diretto](/help/assets/add-assets.md). Per informazioni di carattere tecnico, consulta l’articolo sulle [API di caricamento diretto](/help/assets/developer-reference-material-apis.md#overview-binary-upload). |
| Assets | [Alcuni passaggi](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) del flusso di lavoro `DAM Asset Update` non sono supportati, inclusa la chiamata di strumenti della riga di comando come ImageMagick. | [I microservizi per le risorse](/help/assets/asset-microservices-overview.md) sostituiscono numerosi flussi di lavoro. Per l’elaborazione personalizzata, utilizza i [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| Assets | Transcodifica FFmpeg dei video. | Per generare le miniature FFmpeg, utilizza i [microservizi per le risorse](/help/assets/asset-microservices-overview.md). Per la transcodifica FFmpeg, utilizza [Dynamic Media](/help/assets/manage-video-assets.md). |

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzioni e le funzionalità che sono state rimosse da AEM con Experience Manager as a Cloud Service.

| Area | Funzione | Sostituzione |
| ------------ | ------------------ | ----------- |
| Interfaccia | Alcune finestre di dialogo dell’interfaccia classica rimangono al momento disponibili solo per alcune funzionalità, come Verifica collegamenti, Pulizia delle versioni e alcune configurazioni di Cloud Service, ma l’accesso all’interfaccia classica in generale è stato rimosso nell’interfaccia dei prodotti AEM. | Interfaccia standard |
| Dynamic Media | Le integrazioni precedenti con [Dynamic Media Classic (Scene7)](https://helpx.adobe.com/it/experience-manager/6-5/sites/administering/using/scene7.html) e la [modalità ibrida di Dynamic Media](https://helpx.adobe.com/it/experience-manager/6-5/assets/using/config-dynamic.html) non sono disponibili in AEM as a Cloud Service. | Utilizza la versione di [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) fornita con Experience Manager as a Cloud Service. |
| Sites | Portal Director e componente Portlet | Queste funzionalità sono diventate obsolete in AEM 6.4 e ora sono state rimosse da AEM. |
| Sites | Importazione progettazione | Questa funzionalità è stata rimossa perché le sezioni non modificabili dell’archivio AEM non sono accessibili in fase di esecuzione. |
| Assets | [La condivisione di AEM Assets con il servizio di base Marketing Cloud Assets e i servizi Creative Cloud](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) non è disponibile. | Per l’integrazione con Creative Cloud, utilizza [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html). |
