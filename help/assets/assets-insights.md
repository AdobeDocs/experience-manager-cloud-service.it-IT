---
title: Approfondimenti Assets
description: Tieni traccia delle valutazioni utente e delle statistiche di utilizzo delle immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe.
contentOwner: AG
feature: Asset Insights, Asset Reports
role: User, Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 13%

---

# Approfondimenti Assets {#asset-insights}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/asset-insights.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

La funzionalità Assets Insights consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate nei siti web di terze parti, nelle campagne di marketing e nelle soluzioni creative di Adobe. Consente di fornire informazioni approfondite sulle prestazioni e sulla popolarità delle immagini.

Assets Insights acquisisce i dettagli dell’attività dell’utente, ad esempio il numero di volte in cui un’immagine viene valutata, cliccata e impression (numero di volte in cui un’immagine viene caricata sul sito web). Assegna punteggi alle immagini in base a queste statistiche. Puoi utilizzare i punteggi e le statistiche sulle prestazioni per selezionare le immagini più comuni da includere in cataloghi, campagne di marketing e così via. È inoltre possibile formulare criteri di archiviazione e rinnovo delle licenze in base a tali statistiche.

Affinché Assets Insights possa acquisire le statistiche di utilizzo delle immagini provenienti da un sito web, devi includere il codice di incorporamento dell’immagine nel codice del sito web.

Per consentire a Assets Insights di visualizzare le statistiche di utilizzo delle risorse, configura innanzitutto la funzione per recuperare i dati di reporting da [!DNL Adobe Analytics]. Per ulteriori dettagli, vedere [Configurare Assets Insights](#configure-asset-insights). Per utilizzare questa funzionalità, acquistare la licenza di [!DNL Adobe Analytics] separatamente.

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

## Visualizzare le statistiche di un’immagine {#viewing-statistics-for-an-image}

Puoi visualizzare i punteggi di Assets Insights dalla pagina dei metadati.

1. Dall&#39;interfaccia utente di Assets, selezionare l&#39;immagine e quindi fare clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Dalla pagina Proprietà, fai clic su **[!UICONTROL Informazioni]**.
1. Rivedi i dettagli di utilizzo della risorsa nella scheda **[!UICONTROL Informazioni]**. La sezione **[!UICONTROL Punteggio]** descrive l&#39;utilizzo totale delle risorse e l&#39;andamento delle prestazioni di una risorsa.

   Il punteggio di utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   Il punteggio **[!UICONTROL Impression]** è il numero di volte in cui la risorsa viene caricata sul sito Web. Il numero visualizzato in **[!UICONTROL Clic]** è il numero di volte in cui si fa clic sulla risorsa.

1. Rivedi la sezione **[!UICONTROL Statistiche di utilizzo]** per sapere di quali entità faceva parte la risorsa e quali soluzioni creative l&#39;hanno utilizzata di recente. Maggiore è l’utilizzo, maggiori sono le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le seguenti intestazioni:

   * **[!UICONTROL Risorsa]**: il numero di volte in cui la risorsa faceva parte di una raccolta o di una risorsa composta.
   * **[!UICONTROL Web e dispositivi mobili]**: il numero di volte in cui la risorsa faceva parte di siti Web e app.
   * **[!UICONTROL Social]**: il numero di volte in cui la risorsa è stata utilizzata in altre soluzioni, ad esempio [!DNL Adobe Campaign].
   * **[!UICONTROL E-mail]**: il numero di volte in cui la risorsa è stata utilizzata nelle campagne e-mail.

   ![statistiche_di_utilizzo](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Poiché la funzione Assets Insights in genere recupera i dati delle soluzioni da [!DNL Adobe Analytics] in modo periodico, è possibile che nella sezione Soluzioni non vengano visualizzati i dati più recenti. Il periodo di tempo per il quale vengono visualizzati i dati dipende dalla pianificazione dell’operazione di recupero eseguita da Assets Insights per recuperare i dati di Analytics.

1. Per visualizzare graficamente le statistiche sulle prestazioni della risorsa in un arco di tempo, seleziona il periodo nella sezione **[!UICONTROL Statistiche di prestazioni]**. I dettagli, compresi clic e impression, vengono visualizzati come linee di tendenza di un grafico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A differenza dei dati nella sezione Soluzioni, la sezione Statistiche di prestazioni visualizza i dati più recenti.

1. Per ottenere il codice di incorporamento per la risorsa inclusa nei siti Web per ottenere i dati sulle prestazioni, fai clic su **[!UICONTROL Ottieni codice di incorporamento]** sotto la miniatura della risorsa. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Visualizzare le statistiche di aggregazione per le immagini {#viewing-aggregate-statistics-for-images}

Dalla **[!UICONTROL Visualizzazione approfondimenti]** puoi visualizzare simultaneamente un punteggio di tutte le risorse presenti all’interno di una cartella.

1. Nell’interfaccia utente di Assets, passa alla cartella contenente le risorse per le quali desideri visualizzare le informazioni approfondite.
1. Fare clic sull&#39;opzione **[!UICONTROL Layout]** nella barra degli strumenti, quindi scegliere **[!UICONTROL Visualizzazione approfondimenti]**.
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

[!DNL Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti Web di terze parti da [!DNL Adobe Analytics]. Per consentire ad Assets Insights di recuperare questi dati e generare approfondimenti, configura innanzitutto la funzione da integrare con [!DNL Adobe Analytics].

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.

1. Per informazioni sull&#39;accesso al servizio Web Analytics, vai a **[!UICONTROL Analytics]** > **[!UICONTROL Admin]** > **[!UICONTROL Strumenti di amministrazione]** > **[!UICONTROL Impostazioni società]** > **[!UICONTROL Servizi Web]** e copia la chiave **[!UICONTROL Segreto condiviso]**.

   Nella procedura guidata, seleziona il **[!UICONTROL Centro dati]** e fornisci il nome visualizzato della **[!UICONTROL Società]**, dei servizi Web **[!UICONTROL Nome utente]**, quindi incolla la chiave **[!UICONTROL Segreto condiviso]**.

   Fare clic su **[!UICONTROL Autentica]**.

   ![Configurazione di Adobe Analytics per approfondimenti su Assets in [!DNL Experience Manager]](assets/analytics-insight-config.png)

   *Figura: Configurare Adobe Analytics per Assets Insights in[!DNL Experience Manager]*

1. Una volta completata l’autenticazione, nell’elenco a discesa verranno elencate le suite di rapporti. Seleziona la **[!UICONTROL suite di rapporti]** di Adobe Analytics da cui desideri che Assets Insights recuperi i dati. Fare clic su **[!UICONTROL Aggiungi]**.

1. Dopo che [!DNL Experience Manager] ha configurato la tua suite di rapporti, fai clic su **[!UICONTROL Fine]**.

Per ulteriori informazioni, vedere [Servizi Web Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html?lang=it#api-access-information).

### Tracciamento pagina {#page-tracker}

Dopo aver configurato l’account Adobe Analytics, viene generato il codice di tracciamento pagina. Per consentire ad Assets Insights di tenere traccia delle risorse [!DNL Experience Manager] utilizzate nei siti web di terze parti, includi il codice di tracciamento della pagina nel codice del sito web. Utilizza l’utility Tracciamento pagina in Assets per generare il codice di tracciamento della pagina. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Fai clic su **[!UICONTROL Scarica]** per scaricare il codice di tracciamento della pagina.

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
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
