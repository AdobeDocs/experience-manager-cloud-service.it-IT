---
title: Funzioni obsolete e rimosse
description: Note sulla versione specifiche per le funzioni obsolete e rimosse in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
translation-type: tm+mt
source-git-commit: e6ad571b7428f6fb7a11907e752ba670a722057c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 45%

---


# Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe valuta costantemente le funzionalità dei prodotti, per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti. Inoltre, poiché [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] fornisce un modello di distribuzione nativo per il cloud, alcune funzionalità e funzionalità sono state sostituite da controparti native per il cloud.

Per comunicare l’imminente rimozione/sostituzione delle funzionalità [!DNL Experience Manager], si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Le funzionalità obsolete rimangono disponibili, ma non vengono ulteriormente migliorate.
1. Le funzionalità annunciate come obsolete vengono rimosse nella versione principale successiva, non appena possibile. La data effettiva per la rimozione viene annunciata.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzioni e le funzionalità contrassegnate come obsolete in [!DNL Experience Manager] come [!DNL Cloud Service]. In genere, le funzioni da rimuovere in una versione futura vengono inizialmente rese obsolete e viene fornita un’alternativa.

Consigliamo ai clienti di verificare se utilizzano la funzionalità nella distribuzione corrente e di pianificare la modifica della loro implementazione in modo da utilizzare l’alternativa fornita.

| Funzionalità | Funzione obsoleta | Sostituzione |
| ------------ | ------------------ | ----------- |
| [!DNL Assets] | Flusso di lavoro di `DAM Asset Update` per elaborare le immagini acquisite. | Per l’inserimento delle risorse si utilizzano ora i [microservizi per le risorse](/help/assets/asset-microservices-overview.md). |
| [!DNL Assets] | Carica le risorse direttamente in [!DNL Experience Manager]. Consulta [API di caricamento risorse obsolete](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Utilizza il [caricamento binario diretto](/help/assets/add-assets.md). Per informazioni di carattere tecnico, consulta l’articolo sulle [API di caricamento diretto](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Alcuni passaggi](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) del flusso di lavoro `DAM Asset Update` non sono supportati, inclusa la chiamata di strumenti della riga di comando come ImageMagick. | [I microservizi per le risorse](/help/assets/asset-microservices-overview.md) sostituiscono numerosi flussi di lavoro. Per l’elaborazione personalizzata, utilizza i [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Transcodifica FFmpeg dei video. | Per generare le miniature FFmpeg, utilizza i [microservizi per le risorse](/help/assets/asset-microservices-overview.md). Per la transcodifica FFmpeg, utilizza [Dynamic Media](/help/assets/manage-video-assets.md). |

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità rimosse da [!DNL Experience Manager] con [!DNL Experience Manager] come [!DNL Cloud Service].

| Area | Funzione obsoleta | Sostituzione |
| ------------ | ------------------ | ----------- |
| Interfaccia utente | L’interfaccia classica viene rimossa dall’interfaccia utente del prodotto. Sono disponibili alcune finestre di dialogo dell’interfaccia classica per alcune funzionalità, come Verifica collegamenti, Pulizia versione e alcune configurazioni di Cloud Service. I prossimi [aggiornamenti dei prodotti](/help/release-notes/home.md) potrebbero rimuovere ulteriormente la disponibilità dell&#39;interfaccia classica. | Interfaccia standard |
| [!DNL Dynamic Media] | Le integrazioni precedenti con [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) e [Dynamic Media Hybrid Mode](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) non sono disponibili in [!DNL Experience Manager] come [!DNL Cloud Service]. | Utilizza [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) fornito con [!DNL Experience Manager] come [!DNL Cloud Service]. |
| [!DNL Sites] | Portal Director e componente Portlet | Queste funzionalità sono state dichiarate obsolete in [!DNL Experience Manager] 6.4 e sono state rimosse da [!DNL Experience Manager]. |
| [!DNL Sites] | Importazione progettazione | Questa funzionalità è stata rimossa perché le sezioni immutabili dell’archivio [!DNL Experience Manager] non sono accessibili in fase di esecuzione. |
| [!DNL Assets] | [[!DNL Assets] La condivisione di con il servizio di base Marketing Cloud Assets e i servizi Creative Cloud](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) non è disponibile. | Per l’integrazione con [!DNL Adobe Creative Cloud], utilizza [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html). |
