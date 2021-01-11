---
title: Informazioni sulla risorsa
description: Scopri come la funzione Asset Insights consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo di immagini utilizzate in siti Web di terze parti, campagne di marketing e  Adobe  soluzioni creative.
contentOwner: AG
translation-type: tm+mt
source-git-commit: db653daa2d3c271329812b35960f50ee22fb9943
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 9%

---


# Informazioni sulla risorsa {#asset-insights}

Asset Insights tiene traccia delle valutazioni degli utenti e delle statistiche di utilizzo delle immagini utilizzate in siti Web di terze parti, campagne di marketing e  soluzioni creative . Consente di ottenere informazioni sulle prestazioni e la popolarità delle immagini.

Assets Insights acquisisce i dettagli dell’attività dell’utente, ad esempio il numero di volte in cui un’immagine viene valutata, di cui è stato fatto clic e di impression (numero di volte in cui un’immagine viene caricata sul sito Web). Assegnano dei punteggi alle immagini in base a queste statistiche. Puoi usare le statistiche sui punteggi e sulle prestazioni per selezionare le immagini più comuni da includere nei cataloghi, nelle campagne di marketing e così via. È anche possibile formulare criteri per l&#39;archiviazione e il rinnovo delle licenze basati su tali statistiche.

Per acquisire le statistiche di utilizzo per le immagini da un sito Web, è necessario includere nel codice del sito Web il codice da incorporare per l’immagine.

Per consentire a Informazioni sulle risorse di visualizzare le statistiche di utilizzo per le risorse, configurate prima la funzione per recuperare i dati di reporting da  Adobe Analytics. Per informazioni dettagliate, consultate [Configurare le informazioni sulle risorse](#configure-asset-insights).

>[!NOTE]
>
>Le informazioni approfondite sono supportate e fornite solo per le immagini.

## Visualizzare le statistiche per un&#39;immagine {#viewing-statistics-for-an-image}

Potete visualizzare i punteggi di Asset Insights dalla pagina dei metadati.

1. Dall’interfaccia utente di Assets, seleziona l’immagine e tocca **[!UICONTROL Properties]** dalla barra degli strumenti.
1. Dalla pagina Proprietà, toccare **[!UICONTROL Insights]**.
1. Rivedete i dettagli di utilizzo della risorsa nella scheda **[!UICONTROL Insights]**. La sezione **[!UICONTROL Punteggio]** descrive il totale delle risorse utilizzate e delle prestazioni di una risorsa.

   La valutazione dell&#39;utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   Il punteggio **[!UICONTROL Impression]** indica quante volte la risorsa viene caricata sul sito Web. Il numero visualizzato in **[!UICONTROL Clic]** indica quante volte si fa clic sulla risorsa.

1. Rivedete la sezione **[!UICONTROL Statistiche di utilizzo]** per sapere di quali entità faceva parte la risorsa e quali soluzioni creative ne hanno recentemente utilizzato la risorsa. Maggiore è l’utilizzo, maggiori saranno le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le intestazioni seguenti:

   * **[!UICONTROL Risorsa]**: Il numero di volte in cui la risorsa faceva parte di una raccolta o di una risorsa composta.
   * **[!UICONTROL Web e dispositivi mobili]**: Il numero di volte in cui la risorsa faceva parte di siti Web e app.
   * **[!UICONTROL Social]**: Il numero di volte in cui la risorsa è stata utilizzata nelle soluzioni, come  Adobe Social e  Adobe Campaign.
   * **[!UICONTROL E-mail]**: Il numero di volte in cui la risorsa è stata utilizzata nelle campagne e-mail.

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Poiché la funzione Asset Insights in genere raccoglie i dati delle soluzioni da  Adobe Analytics in modo periodico, la sezione Soluzioni potrebbe non visualizzare i dati più recenti. Il periodo di tempo per il quale i dati vengono visualizzati dipende dalla pianificazione dell&#39;operazione di recupero eseguita da Asset Insights per recuperare i dati Analytics.

1. Per visualizzare graficamente le statistiche sulle prestazioni della risorsa in un arco di tempo, seleziona il periodo nella sezione **[!UICONTROL Statistiche di prestazioni]**. I dettagli, compresi clic e impression, vengono visualizzati come linee di tendenza di un grafico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A differenza dei dati nella sezione Soluzioni, nella sezione Statistiche prestazioni vengono visualizzati i dati più recenti.

1. Per ottenere il codice da incorporare per la risorsa che includete nei siti Web per ottenere i dati sulle prestazioni, toccate o fate clic su **[!UICONTROL Ottieni codice da incorporare]** sotto la miniatura della risorsa. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Visualizzare le statistiche aggregate per le immagini {#viewing-aggregate-statistics-for-images}

Dalla **[!UICONTROL Visualizzazione approfondimenti]** puoi visualizzare simultaneamente un punteggio di tutte le risorse presenti all’interno di una cartella.

1. Nell’interfaccia utente Risorse, passa alla cartella contenente le risorse per le quali vuoi visualizzare informazioni.
1. Toccate/fate clic sull&#39;icona Layout dalla barra degli strumenti, quindi scegliete **[!UICONTROL Visualizzazione approfondimenti]**.
1. Nella pagina vengono visualizzati i punteggi di utilizzo delle risorse. Confronta le valutazioni delle varie risorse e trai informazioni approfondite.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Asset Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Asset Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## Configurare approfondimenti risorse {#configure-asset-insights}

[!DNL Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti Web di terze parti da  [!DNL Adobe Analytics]. Per abilitare Asset Insights per recuperare questi dati e generare informazioni, configura innanzitutto la funzione da integrare con [!DNL Adobe Analytics].

>[!NOTE]
>
>Le informazioni approfondite sono supportate e fornite solo per le immagini.

1. In [!DNL Experience Manager], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.
1. Nella procedura guidata, selezionate un centro dati e fornite le credenziali, incluso il nome dell&#39;organizzazione, il nome utente e il segreto condiviso.

   ![Configurare  Adobe Analytics per Assets Insights in  [!DNL Experience Manager]](assets/insights_config2.png)

   *Figura: Configurare  Adobe Analytics per Assets Insights in[!DNL Experience Manager]*

1. Tocca o fai clic su **[!UICONTROL Autentica]**. Dopo che [!DNL Experience Manager] esegue l&#39;autenticazione delle credenziali, dall&#39;elenco **[!UICONTROL Suite di rapporti]**, scegliete una suite di rapporti Adobe Analytics  da dove si desidera che Asset Insights recuperi dati. Fate clic su **[!UICONTROL Aggiungi]**.
1. Dopo che [!DNL Experience Manager] ha impostato la suite di rapporti, toccate **[!UICONTROL Fine]**.

### Page Tracker {#page-tracker}

Dopo aver configurato l&#39;account Adobe Analytics , viene generato il codice Page Tracker. Per abilitare Assets Insights per tenere traccia delle risorse [!DNL Experience Manager] utilizzate in siti Web di terze parti, includi il codice di tracciamento delle pagine nel codice del sito Web. Utilizzate l&#39;utilità Tracciatore pagina in Risorse per generare il codice tracciatore pagina. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. In [!DNL Experience Manager], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Fate clic su **[!UICONTROL Scarica]** per scaricare il codice tracciatore pagina.

<!--

## Using demo package for Asset Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Asset Insights to capture data from and generate insights for a sample web page.

1. Configure Asset Insights using the instructions in [Configure Asset Insights](#configure-asset-insights).
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
