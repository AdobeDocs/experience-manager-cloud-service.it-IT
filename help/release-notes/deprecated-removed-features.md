---
title: Funzioni obsolete e rimosse
description: Note sulla versione specifiche per le funzioni obsolete e rimosse in  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: 459e6cbf91f9b7f995bd1fd9c8758962c41c9341
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 98%

---

# Funzioni obsolete e rimosse {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Funzioni obsolete e rimosse in AEM as a Cloud Service"
>abstract="AEM as a Cloud Service dispone di un modello di distribuzione nativo per il cloud. Alcune funzionalità sono state sostituite da controparti native per il cloud e questa scheda mostra tali funzioni."


Adobe valuta costantemente le funzionalità dei prodotti, per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti. Inoltre, poiché [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] offre un modello di distribuzione nativo per il cloud, alcune funzionalità sono state sostituite da controparti native per il cloud.

Per comunicare l’imminente rimozione/sostituzione delle funzionalità [!DNL Experience Manager], si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Le funzionalità obsolete rimangono comunque disponibili, ma non vengono più aggiornate.
1. Le funzionalità annunciate come obsolete vengono rimosse nella versione principale successiva, non appena possibile. La data effettiva per la rimozione viene annunciata.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzionalità contrassegnate come obsolete in [!DNL Experience Manager] as a [!DNL Cloud Service]. In genere, le funzioni pianificate per la rimozione in una versione futura vengono impostate come obsolete e ne viene indicata un’alternativa.

Consigliamo ai clienti di verificare se utilizzano la funzione/funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Funzionalità | Funzione obsoleta | Sostituzione |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | Proprietà di Frammenti di esperienza per **Stato social media**. | La funzione verrà rimossa presto. |
| [!DNL Sites] | Frammenti di contenuto semplici basati su modelli. | [Frammenti di contenuto strutturati basati su modelli](/help/assets/content-fragments/content-fragments-models.md) ora. |
| [!DNL Assets] | Flusso di lavoro di `DAM Asset Update` per elaborare le immagini acquisite. | Per l’inserimento delle risorse si utilizzano ora i [microservizi per le risorse](/help/assets/asset-microservices-overview.md). |
| [!DNL Assets] | Carica le risorse direttamente in [!DNL Experience Manager]. Consulta [API di caricamento risorse dichiarate obsolete](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Utilizza il [caricamento binario diretto](/help/assets/add-assets.md). Per informazioni di carattere tecnico, consulta l’articolo sulle [API di caricamento diretto](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Alcuni passaggi](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) del flusso di lavoro `DAM Asset Update` non sono supportati, inclusa la chiamata di strumenti della riga di comando come [!DNL ImageMagick]. | [I microservizi per le risorse](/help/assets/asset-microservices-overview.md) sostituiscono numerosi flussi di lavoro. Per l’elaborazione personalizzata, utilizza i [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Transcodifica FFmpeg dei video. | Per generare le miniature FFmpeg, utilizza i [microservizi per le risorse](/help/assets/asset-microservices-overview.md). Per la transcodifica FFmpeg, utilizza [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | Interfaccia utente di replica ad albero nella scheda “Distribuisci” dell’agente di replica (rimozione dopo il 30 settembre 2021) | [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o approcci al [flusso di lavoro della struttura dei contenuti di pubblicazione](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | Né la scheda Distribuzione nella schermata di amministrazione dell’agente di replica, né l’API di replica possono essere utilizzate per replicare pacchetti di contenuti superiori a 10 MB (limite applicato a partire dal 12 settembre 2022). | [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o approcci al [flusso di lavoro della struttura dei contenuti di pubblicazione](/help/operations/replication.md#publish-content-tree-workflow) |


| [!DNL Foundation] | Né la scheda Distribuizione nella schermata di amministrazione dell’agente di replica né l’API di replica possono essere utilizzate per replicare pacchetti di contenuti superiori a 10 MB. È invece possibile utilizzare [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o il [flusso di lavoro della struttura dei contenuti di pubblicazione](/help/operations/replication.md#publish-content-tree-workflow) |

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità che sono state rimosse da [!DNL Experience Manager] con [!DNL Experience Manager] as a [!DNL Cloud Service].

| Area | Funzione obsoleta | Sostituzione | Data di rimozione prevista |
| ------------ | ------------------ | ----------- | ------------------- |
| Interfaccia utente | L’interfaccia utente classica viene rimossa dall’interfaccia utente del prodotto. Sono disponibili alcune finestre di dialogo dell’interfaccia utente classica per alcune funzionalità, come Verifica collegamenti, Pulizia versione e alcune configurazioni di Cloud Service. I prossimi [aggiornamenti dei prodotti](/help/release-notes/home.md) potrebbero rimuovere ulteriormente la disponibilità dell’interfaccia utente classica. | Interfaccia standard | Rimosso |
| [!DNL Dynamic Media] | Le integrazioni precedenti con [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=it#integration) e la [modalità ibrida di Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=it#dynamic) non sono disponibili in [!DNL Experience Manager] as a [!DNL Cloud Service]. | Utilizza la versione di [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) fornita con [!DNL Experience Manager] as a [!DNL Cloud Service]. | Rimosso |
| [!DNL Sites] | Portal Director e componente Portlet | Queste funzionalità sono diventate obsolete in [!DNL Experience Manager] 6.4 e ora sono state rimosse da [!DNL Experience Manager]. | Rimosso |
| [!DNL Sites] | Importazione progettazione | Questa funzionalità è stata rimossa perché le sezioni non modificabili dell’archivio [!DNL Experience Manager] non sono accessibili in fase di esecuzione. | Rimosso |
| [!DNL Assets] | La condivisione di [!DNL Assets] con il servizio di base Experience Cloud Assets e i servizi Creative Cloud non è disponibile. | Per l’integrazione con [!DNL Adobe Creative Cloud], utilizza [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html). | Rimosso |
| [!DNL Foundation] | Supporto per le origini dati Apache Sling (OSGi bundle org.apache.sling.datasource) | N/D | Rimosso |
| [!DNL Foundation] | Supporto per i modelli di script JST (OSGi bundle org.apache.sling.scripting.jst) | N/D | Rimosso |
| [!DNL Foundation] | Supporto per Apache Felix Http Whiteboard | OSGi Http Whiteboard | Marzo 2022 |
| [!DNL Foundation] | Supporto per com.adobe.granite.oauth.server | Integrazione Adobe IMS | Marzo 2023 |


## API Java {#java-api}

Consulta [questa pagina](/help/release-notes/deprecated-apis.md) per eventuali API Java obsolete o rimosse, che vengono talvolta introdotte.

## Configurazione OSGI {#osgi-configuration}

Consulta [questo articolo](/help/implementing/deploying/osgi-configuration-api.md) per eventuali restrizioni alla configurazione delle proprietà OSGI, alcune delle quali possono essere introdotte nel tempo.
