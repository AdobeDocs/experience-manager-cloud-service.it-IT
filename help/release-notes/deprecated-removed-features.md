---
title: Funzioni obsolete e rimosse
description: Note sulla versione specifiche per le funzioni obsolete e rimosse in [!DNL Adobe Experience Manager] come [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: d55e2aec4718e752cfc0dfa610abf1a1d36a583f
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 34%

---

# Funzioni obsolete e rimosse {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Funzioni obsolete e rimosse in AEM as a Cloud Service"
>abstract="AEM as a Cloud Service dispone di un modello di distribuzione nativo per il cloud. Alcune funzionalità sono state sostituite da controparti native per il cloud e questa scheda mostra tali funzioni."


Adobe valuta costantemente le funzionalità dei prodotti, per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti. Inoltre, come [!DNL Adobe Experience Manager] come [!DNL Cloud Service] fornisce un modello di distribuzione nativo per il cloud, alcune funzionalità e funzionalità sono state sostituite da controparti native per il cloud.

Comunicare l&#39;imminente rimozione/sostituzione di [!DNL Experience Manager] , si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Le funzionalità obsolete rimangono disponibili, ma non vengono ulteriormente migliorate.
1. Le funzionalità annunciate come obsolete vengono rimosse nella versione principale successiva, non appena possibile. La data effettiva per la rimozione viene annunciata.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzioni e le funzionalità contrassegnate come obsolete in [!DNL Experience Manager] come [!DNL Cloud Service]. In genere, le funzioni da rimuovere in una versione futura vengono inizialmente rese obsolete e viene fornita un’alternativa.

Consigliamo ai clienti di verificare se utilizzano la funzionalità nella distribuzione corrente e di pianificare la modifica della loro implementazione in modo da utilizzare l’alternativa fornita.

| Funzionalità | Funzione obsoleta | Sostituzione |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | Proprietà dei frammenti esperienza per **Stato social media**. | La funzione verrà rimossa presto. |
| [!DNL Sites] | Frammenti di contenuto semplici basati su modelli. | [Frammenti di contenuto strutturati basati su modelli](/help/assets/content-fragments/content-fragments-models.md) ora. |
| [!DNL Assets] | Flusso di lavoro di `DAM Asset Update` per elaborare le immagini acquisite. | Per l’inserimento delle risorse si utilizzano ora i [microservizi per le risorse](/help/assets/asset-microservices-overview.md). |
| [!DNL Assets] | Caricare le risorse direttamente in [!DNL Experience Manager]. Vedi [API di caricamento risorse obsolete](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Utilizza il [caricamento binario diretto](/help/assets/add-assets.md). Per informazioni di carattere tecnico, consulta l’articolo sulle [API di caricamento diretto](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Alcuni passaggi](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) del flusso di lavoro `DAM Asset Update` non sono supportati, inclusa la chiamata di strumenti della riga di comando come [!DNL ImageMagick]. | [I microservizi per le risorse](/help/assets/asset-microservices-overview.md) sostituiscono numerosi flussi di lavoro. Per l’elaborazione personalizzata, utilizza i [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Transcodifica FFmpeg dei video. | Per generare le miniature FFmpeg, utilizza i [microservizi per le risorse](/help/assets/asset-microservices-overview.md). Per la transcodifica FFmpeg, utilizza [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | Interfaccia utente di replica ad albero nella scheda &quot;Distribute&quot; dell’agente di replica (rimozione dopo il 30 settembre 2021) | [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o [flusso di lavoro della struttura dei contenuti di pubblicazione](/help/operations/replication.md#publish-content-tree-workflow) approcci |

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità rimosse da [!DNL Experience Manager] con [!DNL Experience Manager] come [!DNL Cloud Service].

| Area | Funzione obsoleta | Sostituzione | Data di rimozione di Target |
| ------------ | ------------------ | ----------- | ------------------- |
| Interfaccia utente | L’interfaccia classica viene rimossa dall’interfaccia utente del prodotto. Sono disponibili alcune finestre di dialogo dell’interfaccia classica per alcune funzionalità, come Verifica collegamenti, Pulizia versione e alcune configurazioni di Cloud Service. Prossima [aggiornamenti dei prodotti](/help/release-notes/home.md) potrebbero rimuovere ulteriormente la disponibilità dell’interfaccia classica. | Interfaccia standard | Rimosso |
| [!DNL Dynamic Media] | Integrazioni precedenti con [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) e [Modalità ibrida Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) non sono disponibili in [!DNL Experience Manager] come [!DNL Cloud Service]. | Utilizzo [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) forniti [!DNL Experience Manager] come [!DNL Cloud Service]. | Rimosso |
| [!DNL Sites] | Portal Director e componente Portlet | Queste funzionalità sono state dichiarate obsolete in [!DNL Experience Manager] 6.4 e sono stati rimossi da [!DNL Experience Manager]. | Rimosso |
| [!DNL Sites] | Importazione progettazione | Questa funzionalità è stata rimossa come sezioni immutabili del [!DNL Experience Manager] archivio non accessibile in fase di runtime. | Rimosso |
| [!DNL Assets] | [!DNL Assets]La condivisione di con il servizio di base Marketing Cloud Assets e i servizi Creative Cloud non è disponibile. | Per l’integrazione con [!DNL Adobe Creative Cloud], utilizza [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html). | Rimosso |
| [!DNL Foundation] | Supporto per le origini dati Apache Sling (OSGi bundle org.apache.sling.datasource) | N/D | Rimosso |
| [!DNL Foundation] | Supporto per i modelli di script JST (OSGi bundle org.apache.sling.scripting.jst) | N/D | Rimosso |
| [!DNL Foundation] | Supporto per la lavagna bianca Http Apache Felix | Whiteboard Http OSGi | Marzo 2022 |

## API Java {#java-api}

Vedi [questa pagina](/help/release-notes/deprecated-apis.md) per eventuali API Java obsolete o rimosse, che vengono talvolta introdotte.

## Configurazione OSGI {#osgi-configuration}

Vedi [articolo](/help/implementing/deploying/osgi-configuration-api.md) per eventuali restrizioni alla configurazione delle proprietà OSGI, alcune delle quali possono essere introdotte nel tempo.
