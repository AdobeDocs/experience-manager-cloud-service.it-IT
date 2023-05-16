---
title: Informazioni sulle risorse
description: Monitora le valutazioni degli utenti e le statistiche di utilizzo di immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe.
contentOwner: AG
feature: Asset Insights,Asset Reports
role: User,Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 10%

---

# Informazioni sulle risorse {#asset-insights}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/asset-insights.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

La funzionalità Approfondimenti risorse consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe. Fornisce informazioni sulle prestazioni e sulla popolarità delle immagini.

Assets Insights acquisisce i dettagli dell’attività dell’utente, ad esempio il numero di volte in cui un’immagine viene valutata, su cui è stato fatto clic e le impression (numero di volte in cui un’immagine viene caricata sul sito web). Assegna punteggi alle immagini in base a queste statistiche. Puoi utilizzare i punteggi e le statistiche sulle prestazioni per selezionare le immagini più comuni da includere nei cataloghi, nelle campagne di marketing e così via. Puoi anche formulare politiche di archiviazione e rinnovo delle licenze basate su queste statistiche.

Affinché Assets Insights possa acquisire le statistiche di utilizzo per le immagini da un sito web, devi includere il codice di incorporamento per l’immagine nel codice del sito web.

Per consentire a Assets Insights di visualizzare le statistiche di utilizzo per le risorse, configura prima la funzione per recuperare i dati di reporting da [!DNL Adobe Analytics]. Per maggiori dettagli, vedi [Configurare Assets Insights](#configure-asset-insights). Per utilizzare questa funzione, acquista [!DNL Adobe Analytics] licenza separatamente.

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

## Visualizzare le statistiche per un’immagine {#viewing-statistics-for-an-image}

Puoi visualizzare i punteggi di Assets Insights dalla pagina dei metadati.

1. Dall’interfaccia utente Assets, seleziona l’immagine e fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti.
1. Dalla pagina Proprietà , fai clic su **[!UICONTROL Informazioni approfondite]**.
1. Esamina i dettagli di utilizzo della risorsa nella sezione **[!UICONTROL Informazioni approfondite]** scheda . La **[!UICONTROL Punteggio]** la sezione descrive l’utilizzo totale delle risorse e le origini delle prestazioni di una risorsa .

   Il punteggio di utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   La **[!UICONTROL Impressioni]** punteggio è il numero di volte in cui la risorsa viene caricata sul sito web. Numero visualizzato sotto **[!UICONTROL Clic]** è il numero di volte in cui viene fatto clic sulla risorsa.

1. Consulta la sezione **[!UICONTROL Statistiche di utilizzo]** per sapere di quali entità faceva parte la risorsa e quali soluzioni creative l’ha utilizzata di recente. Maggiore è l’utilizzo, maggiori sono le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le seguenti intestazioni:

   * **[!UICONTROL Risorsa]**: Il numero di volte in cui la risorsa faceva parte di una raccolta o di una risorsa composta.
   * **[!UICONTROL Web e dispositivi mobili]**: Il numero di volte in cui la risorsa faceva parte di siti web e app.
   * **[!UICONTROL Social]**: Il numero di volte in cui la risorsa è stata utilizzata in altre soluzioni, ad esempio [!DNL Adobe Campaign].
   * **[!UICONTROL E-mail]**: Il numero di volte in cui la risorsa è stata utilizzata nelle campagne e-mail.

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Poiché la funzione Assets Insights in genere recupera i dati delle soluzioni da [!DNL Adobe Analytics] periodicamente, la sezione Soluzioni potrebbe non visualizzare i dati più recenti. Il periodo di tempo per il quale vengono visualizzati i dati dipende dalla pianificazione dell’operazione di recupero eseguita da Assets Insights per il recupero dei dati di Analytics.

1. Per visualizzare graficamente le statistiche sulle prestazioni della risorsa in un arco di tempo, seleziona il periodo nella sezione **[!UICONTROL Statistiche di prestazioni]**. I dettagli, compresi clic e impression, vengono visualizzati come linee di tendenza di un grafico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A differenza dei dati nella sezione Soluzioni , la sezione Statistiche di prestazioni visualizza i dati più recenti.

1. Per ottenere il codice di incorporamento della risorsa inclusa nei siti web per ottenere i dati sulle prestazioni, fai clic su **[!UICONTROL Ottieni codice di incorporamento]** sotto la miniatura della risorsa. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Visualizzare le statistiche aggregate per le immagini {#viewing-aggregate-statistics-for-images}

Dalla **[!UICONTROL Visualizzazione approfondimenti]** puoi visualizzare simultaneamente un punteggio di tutte le risorse presenti all’interno di una cartella.

1. Nell’interfaccia utente Assets, individua la cartella contenente le risorse di cui desideri visualizzare le informazioni.
1. Fai clic sul pulsante **[!UICONTROL Layout]** dalla barra degli strumenti, quindi scegliere **[!UICONTROL Visualizzazione approfondimenti]**.
1. Nella pagina vengono visualizzati i punteggi di utilizzo delle risorse. Confronta le valutazioni delle varie risorse e trai informazioni approfondite.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## Configurare Assets Insights {#configure-asset-insights}

[!DNL Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti web di terze parti da [!DNL Adobe Analytics]. Per abilitare Assets Insights al recupero di questi dati e alla generazione di informazioni, configura innanzitutto la funzione con cui eseguire l’integrazione [!DNL Adobe Analytics].

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.

1. Per informazioni sull’accesso al servizio Web Analytics, vai a **[!UICONTROL Analytics]** > **[!UICONTROL Amministratore]** > **[!UICONTROL Strumenti di amministrazione]** > **[!UICONTROL Impostazioni aziendali]** > **[!UICONTROL Servizi Web]** e copia il **[!UICONTROL Segreto condiviso]** chiave.

   Nella procedura guidata, seleziona la **[!UICONTROL Centro dati]** e fornire il nome visualizzato del **[!UICONTROL Azienda]**, Servizi Web **[!UICONTROL Nome utente]** e incolla **[!UICONTROL Segreto condiviso]** chiave.

   Fai clic su **[!UICONTROL Autentica]**.

   ![Configurare Adobe Analytics per Assets Insights in [!DNL Experience Manager]](assets/analytics-insight-config.png)

   *Figura: Configurare Adobe Analytics per Assets Insights in[!DNL Experience Manager]*

1. Se l’autenticazione viene eseguita correttamente, le suite di rapporti vengono elencate nel menu a discesa . Selezionare Adobe Analytics **[!UICONTROL Suite di rapporti]** da dove desideri che Assets Insights recuperi i dati. Fai clic su **[!UICONTROL Aggiungi]**.

1. Dopo [!DNL Experience Manager] imposta la suite di rapporti, fai clic su **[!UICONTROL Fine]**.

Per ulteriori informazioni, consulta [Servizi Web Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html#api-access-information).

### Tracciamento pagina {#page-tracker}

Dopo aver configurato l’account Adobe Analytics, viene generato il codice di tracciamento pagina . Per abilitare Assets Insights per tenere traccia delle [!DNL Experience Manager] risorse utilizzate in siti web di terze parti, includi il codice di tracciamento della pagina nel codice del sito web. Utilizza l’utilità Tracciamento pagina in Assets per generare il codice di tracciamento pagina. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Fai clic su **[!UICONTROL Scarica]** per scaricare il codice di tracciamento della pagina.

<!--
Add page tracker code, CQDOC-18045, 30/07/2021
-->
Il seguente frammento di codice di esempio visualizza il codice Tracciamento pagina incluso in una pagina web di esempio:

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
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
