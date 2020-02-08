---
title: Informazioni sulla risorsa
description: Scopri come la funzione Asset Insights consente di tenere traccia delle valutazioni degli utenti e delle statistiche di utilizzo delle immagini utilizzate nei siti Web di terze parti, nelle campagne di marketing e nelle soluzioni creative di Adobe.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Informazioni sulla risorsa{#asset-insights}

<!-- TBD: Add uicontrol tags  -->

La funzione Asset Insights consente di tenere traccia delle valutazioni degli utenti e delle statistiche di utilizzo delle immagini utilizzate nei siti Web di terze parti, nelle campagne di marketing e nelle soluzioni creative di Adobe. Consente di ricavare informazioni sulle loro prestazioni e popolarità.

Assets Insights acquisisce i dettagli dell’attività dell’utente, ad esempio il numero di volte in cui un’immagine viene valutata, di cui è stato fatto clic e di impression (numero di volte in cui un’immagine viene caricata sul sito Web). Assegnano dei punteggi alle immagini in base a queste statistiche. Puoi usare le statistiche sui punteggi e sulle prestazioni per selezionare le immagini più comuni da includere nei cataloghi, nelle campagne di marketing e così via. È anche possibile formulare criteri per l&#39;archiviazione e il rinnovo delle licenze basati su tali statistiche.

Per acquisire le statistiche di utilizzo per le immagini da un sito Web, è necessario includere nel codice del sito Web il codice da incorporare per l’immagine.

Per consentire a Informazioni sulle risorse di visualizzare le statistiche di utilizzo per le risorse, configura prima la funzione per recuperare i dati di reporting da Adobe Analytics. Per informazioni dettagliate, consultate [Configurare approfondimenti](#configure-asset-insights)risorse.

>[!NOTE]
>
>Le informazioni approfondite sono supportate e fornite solo per le immagini.

## Visualizzare le statistiche per un’immagine {#viewing-statistics-for-an-image}

Potete visualizzare i punteggi di Asset Insights dalla pagina dei metadati.

1. Nell’interfaccia utente di Assets, seleziona l’immagine e tocca **[!UICONTROL Proprietà]** dalla barra degli strumenti.
1. Dalla pagina Proprietà, tocca **[!UICONTROL Approfondimenti]**.
1. Consultate i dettagli di utilizzo della risorsa nella scheda **[!UICONTROL Insights]** (Approfondimenti). La sezione **[!UICONTROL Punteggio]** descrive le risorse totali utilizzate e le risorse disponibili per le prestazioni di una risorsa.

   La valutazione dell&#39;utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   Il punteggio **[!UICONTROL Impression]** indica quante volte la risorsa viene caricata sul sito Web. Il numero visualizzato in **[!UICONTROL Clic]** indica quante volte è possibile fare clic sulla risorsa.

1. Consultate la sezione Statistiche **[!UICONTROL di]** utilizzo per sapere di quali entità faceva parte la risorsa e di quali soluzioni creative ha utilizzato di recente. Maggiore è l’utilizzo, maggiori saranno le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le intestazioni seguenti:

   * **Risorsa**: Il numero di volte in cui la risorsa faceva parte di una raccolta o di una risorsa composta
   * **Web e dispositivi mobili**: Il numero di volte in cui la risorsa faceva parte di siti Web e app
   * **Social**: Il numero di volte in cui la risorsa è stata utilizzata nelle soluzioni, come Adobe Social e Adobe Campaign
   * **E-mail**: Numero di volte in cui la risorsa è stata utilizzata nelle campagne e-mail
   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Poiché la funzione Asset Insights in genere raccoglie i dati delle soluzioni da Adobe Analytics in modo periodico, la sezione Soluzioni potrebbe non visualizzare i dati più recenti. Il periodo di tempo per il quale i dati vengono visualizzati dipende dalla pianificazione dell&#39;operazione di recupero eseguita da Asset Insights per recuperare i dati Analytics.

1. Per visualizzare graficamente le statistiche sulle prestazioni della risorsa in un periodo di tempo, selezionare il periodo nella sezione Statistiche **** prestazioni. I dettagli, compresi clic e impression, vengono visualizzati come linee di tendenza di un grafico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A differenza dei dati nella sezione Soluzioni, nella sezione Statistiche prestazioni vengono visualizzati i dati più recenti.

1. Per ottenere il codice da incorporare per la risorsa che includete nei siti Web per ottenere i dati sulle prestazioni, toccate o fate clic su **[!UICONTROL Ottieni codice]** da incorporare sotto la miniatura della risorsa. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Visualizzare le statistiche aggregate per le immagini {#viewing-aggregate-statistics-for-images}

Puoi visualizzare simultaneamente un punteggio di tutte le risorse all’interno di una cartella utilizzando la Visualizzazione **** approfondimenti.

1. Nell’interfaccia utente Risorse, passa alla cartella contenente le risorse per le quali vuoi visualizzare informazioni.
1. Toccate o fate clic sull&#39;icona Layout dalla barra degli strumenti, quindi scegliete Visualizzazione **[!UICONTROL approfondimenti]**.
1. Nella pagina vengono visualizzati i punteggi di utilizzo delle risorse. Confronta le valutazioni delle varie risorse e trai informazioni approfondite.

## Pianificazione processo in background {#scheduling-background-job}

Asset Insights recupera periodicamente i dati di utilizzo delle risorse dalle suite di rapporti di Adobe Analytics. Per impostazione predefinita, Asset Insights esegue un processo in background ogni 24 ore alle 2 del mattino fino ai dati di recupero. Tuttavia, potete modificare sia la frequenza che l’ora configurando il servizio **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** Service dalla console Web.

1. Toccate il logo AEM e passate a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console **** Web.
1. Apri la configurazione del servizio di sincronizzazione dei processi **[!UICONTROL di]** Adobe CQ DAM Asset Performance Report.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specificate la frequenza di pianificazione desiderata e l&#39;ora di inizio del processo nell&#39;espressione utilità di pianificazione delle proprietà. Salva le modifiche.

## Configurare approfondimenti risorse {#configure-asset-insights}

Risorse Adobe Experience Manager (AEM) recupera i dati di utilizzo relativi alle risorse AEM utilizzate da siti Web di terze parti da Adobe Analytics. Per abilitare Asset Insights per recuperare questi dati e generare approfondimenti, configura prima la funzione da integrare con Adobe Analytics.

>[!NOTE]
>
>Le informazioni approfondite sono supportate e fornite solo per le immagini.

1. In AEM, fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Fate clic sulla scheda Configurazione **** Insights.
1. Nella procedura guidata, selezionate un centro dati e fornite le credenziali, incluso il nome dell&#39;organizzazione, il nome utente e il segreto condiviso.

   ![Configurare Adobe Analytics per Assets Insights in AEM](assets/insights_config2.png)
   *Figura:Configurare Adobe Analytics per Assets Insights in AEM*

1. Tocca o fai clic su **[!UICONTROL Autenticazione]**. Dopo l’autenticazione delle credenziali da parte di AEM, dall’elenco Suite **[!UICONTROL di]** rapporti, scegliete una suite di rapporti di Adobe Analytics da cui recuperare i dati da Asset Insights. Fate clic su **[!UICONTROL Aggiungi]**.
1. Dopo che AEM ha impostato la suite di rapporti, toccate **[!UICONTROL Fine]**.

### Tracciatore pagina {#page-tracker}

Dopo aver configurato l’account Adobe Analytics, viene generato il codice Page Tracker. Per abilitare Assets Insights per tenere traccia delle risorse AEM utilizzate in siti Web di terze parti, includi il codice di tracciamento delle pagine nel codice del sito Web. Utilizzate l&#39;utilità Tracker pagina in Risorse AEM per generare il codice tracciatore pagina. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. In AEM, fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Nella pagina **[!UICONTROL Navigazione]** , fai clic sulla scheda **[!UICONTROL Insights Page Tracker]** (Tracciatore pagina approfondimenti).
1. Fate clic su **[!UICONTROL Scarica]** per scaricare il codice tracciatore pagina.

<!--

## Using demo package for Asset Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Asset Insights to capture data from and generate insights for a sample web page.

1. Configure Asset Insights using the instructions in [Configure Asset Insights](#configure-asset-insights).
1. Download the sample AEM Assets package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in AEM itself.

-->
