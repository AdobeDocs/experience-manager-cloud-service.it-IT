---
title: Informazioni su Assets
description: Monitora le valutazioni utente e le statistiche sull’utilizzo delle immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe.
contentOwner: AG
feature: Asset Insights,Asset Reports
role: User,Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 10%

---

# Informazioni su Assets {#asset-insights}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/asset-insights.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

La funzionalità Assets Insights consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate nei siti web di terze parti, nelle campagne di marketing e nelle soluzioni creative di Adobe. Consente di fornire informazioni approfondite sulle prestazioni e sulla popolarità delle immagini.

Assets Insights acquisisce i dettagli dell’attività dell’utente, ad esempio il numero di volte in cui un’immagine viene valutata, cliccata e impression (numero di volte in cui un’immagine viene caricata sul sito web). Assegna punteggi alle immagini in base a queste statistiche. Puoi utilizzare i punteggi e le statistiche sulle prestazioni per selezionare le immagini più comuni da includere in cataloghi, campagne di marketing e così via. È inoltre possibile formulare criteri di archiviazione e rinnovo delle licenze in base a tali statistiche.

Affinché Assets Insights possa acquisire le statistiche di utilizzo delle immagini provenienti da un sito web, devi includere il codice di incorporamento dell’immagine nel codice del sito web.

Per consentire a Assets Insights di visualizzare le statistiche di utilizzo delle risorse, configura innanzitutto la funzione per recuperare i dati di reporting da [!DNL Adobe Analytics]. Per ulteriori informazioni, consulta [Configurare Assets Insights](#configure-asset-insights). Per utilizzare questa funzione, acquista [!DNL Adobe Analytics] licenza separatamente.

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

## Visualizzare le statistiche di un’immagine {#viewing-statistics-for-an-image}

Puoi visualizzare i punteggi di Assets Insights dalla pagina dei metadati.

1. Dall’interfaccia utente Assets, seleziona l’immagine e fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti.
1. Dalla pagina Proprietà, fai clic su **[!UICONTROL Approfondimenti]**.
1. Rivedi i dettagli di utilizzo della risorsa in **[!UICONTROL Approfondimenti]** scheda. Il **[!UICONTROL Punteggio]** La sezione descrive l’utilizzo totale delle risorse e le sequenze di prestazioni di una risorsa.

   Il punteggio di utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   Il **[!UICONTROL Impression]** punteggio è il numero di volte in cui la risorsa viene caricata sul sito web. Numero visualizzato in **[!UICONTROL Clic]** è il numero di volte in cui si fa clic sulla risorsa.

1. Rivedi **[!UICONTROL Statistiche di utilizzo]** sezione per sapere di quali entità faceva parte la risorsa e quali soluzioni creative l’hanno recentemente utilizzata. Maggiore è l’utilizzo, maggiori sono le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le seguenti intestazioni:

   * **[!UICONTROL Risorsa]**: numero di volte in cui la risorsa faceva parte di una raccolta o di una risorsa composta.
   * **[!UICONTROL Web e mobile]**: numero di volte in cui la risorsa faceva parte di siti web e app.
   * **[!UICONTROL Social]**: numero di volte in cui la risorsa è stata utilizzata in altre soluzioni, ad esempio [!DNL Adobe Campaign].
   * **[!UICONTROL E-mail]**: numero di volte in cui la risorsa è stata utilizzata nelle campagne e-mail.

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Perché la funzione Assets Insights in genere recupera i dati delle soluzioni da [!DNL Adobe Analytics] periodicamente, la sezione Soluzioni potrebbe non visualizzare i dati più recenti. Il periodo di tempo per il quale vengono visualizzati i dati dipende dalla pianificazione dell’operazione di recupero eseguita da Assets Insights per recuperare i dati di Analytics.

1. Per visualizzare graficamente le statistiche sulle prestazioni della risorsa in un arco di tempo, seleziona il periodo nella sezione **[!UICONTROL Statistiche di prestazioni]**. I dettagli, compresi clic e impression, vengono visualizzati come linee di tendenza di un grafico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A differenza dei dati nella sezione Soluzioni, la sezione Statistiche di prestazioni visualizza i dati più recenti.

1. Per ottenere il codice di incorporamento della risorsa da includere nei siti Web per ottenere i dati sulle prestazioni, fai clic su **[!UICONTROL Ottieni codice di incorporamento]** sotto la miniatura della risorsa. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Visualizzare le statistiche di aggregazione per le immagini {#viewing-aggregate-statistics-for-images}

Dalla **[!UICONTROL Visualizzazione approfondimenti]** puoi visualizzare simultaneamente un punteggio di tutte le risorse presenti all’interno di una cartella.

1. Nell’interfaccia utente Assets, passa alla cartella contenente le risorse per le quali desideri visualizzare le informazioni approfondite.
1. Fai clic su **[!UICONTROL Layout]** dalla barra degli strumenti, quindi scegliere **[!UICONTROL Visualizzazione approfondimenti]**.
1. Nella pagina vengono visualizzati i punteggi di utilizzo delle risorse. Confronta le valutazioni delle varie risorse e trae informazioni.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## Configurare Assets Insights {#configure-asset-insights}

[!DNL Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti web di terze parti da [!DNL Adobe Analytics]. Per abilitare Assets Insights al recupero di tali dati e alla generazione di informazioni, configura innanzitutto la funzione da integrare con [!DNL Adobe Analytics].

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

1. In entrata [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.

1. Per informazioni sull’accesso al servizio web Analytics, vai a **[!UICONTROL Analytics]** > **[!UICONTROL Amministratore]** > **[!UICONTROL Strumenti di amministrazione]** > **[!UICONTROL Impostazioni società]** > **[!UICONTROL Servizi Web]** e copia **[!UICONTROL Segreto condiviso]** chiave.

   Nella procedura guidata, seleziona **[!UICONTROL Data center]** e forniscono il nome visualizzato del **[!UICONTROL Azienda]**, servizi web **[!UICONTROL Nome utente]**, e incolla **[!UICONTROL Segreto condiviso]** chiave.

   Clic **[!UICONTROL Autentica]**.

   ![Configurare Adobe Analytics per Informazioni su risorse in [!DNL Experience Manager]](assets/analytics-insight-config.png)

   *Figura: Configurare Adobe Analytics per Informazioni su risorse in[!DNL Experience Manager]*

1. Una volta completata l’autenticazione, nell’elenco a discesa verranno elencate le suite di rapporti. Seleziona l’Adobe Analytics **[!UICONTROL Suite di rapporti]** da dove desideri che Assets Insights recuperi i dati. Clic **[!UICONTROL Aggiungi]**.

1. Dopo [!DNL Experience Manager] configura la suite di rapporti, fai clic su **[!UICONTROL Fine]**.

Per ulteriori informazioni, consulta [Servizi Web di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html#api-access-information).

### Tracciamento pagina {#page-tracker}

Dopo aver configurato l’account Adobe Analytics, viene generato il codice di tracciamento pagina. Per abilitare Assets Insights per tenere traccia di [!DNL Experience Manager] le risorse utilizzate nei siti web di terze parti includono il codice di tracciamento della pagina nel codice del sito web. Utilizza l’utility Tracciamento pagina in Assets per generare il codice di tracciamento della pagina. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. In entrata [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Clic **[!UICONTROL Scarica]** per scaricare il codice di tracciamento della pagina.

<!--
Add page tracker code, CQDOC-18045, 30/07/2021
-->
Il seguente snippet di codice di esempio visualizza il codice di tracciamento pagina incluso in una pagina web di esempio:

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```



<!--

## Using demo package for Assets Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Assets Insights to capture data from and generate insights for a sample web page.

1. Configure Assets Insights using the instructions in [Configure Assets Insights](#configure-asset-insights).
1. Download the sample [!DNL Experience Manager Assets] package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in [!DNL Experience Manager] itself.

-->

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati da Assets](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
