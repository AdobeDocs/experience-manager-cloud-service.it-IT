---
title: Informazioni sulla risorsa
description: Monitora le valutazioni degli utenti e le statistiche di utilizzo di immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe.
contentOwner: AG
feature: Informazioni sulla risorsa, rapporti sulle risorse
role: Business Practitioner
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
translation-type: tm+mt
source-git-commit: a42138cd009a85a92e74d98dd808578014361e1d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 9%

---

# Informazioni sulla risorsa {#asset-insights}

Asset Insights tiene traccia delle valutazioni utente e delle statistiche di utilizzo delle immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe. Fornisce informazioni sulle prestazioni e sulla popolarità delle immagini.

Assets Insights acquisisce i dettagli dell’attività dell’utente, ad esempio il numero di volte in cui un’immagine viene valutata, su cui è stato fatto clic e le impression (numero di volte in cui un’immagine viene caricata sul sito web). Assegna punteggi alle immagini in base a queste statistiche. Puoi utilizzare i punteggi e le statistiche sulle prestazioni per selezionare le immagini più comuni da includere nei cataloghi, nelle campagne di marketing e così via. Puoi anche formulare politiche di archiviazione e rinnovo delle licenze basate su queste statistiche.

Affinché Assets Insights possa acquisire le statistiche di utilizzo per le immagini da un sito web, devi includere il codice di incorporamento per l’immagine nel codice del sito web.

Per consentire a Asset Insights di visualizzare le statistiche di utilizzo per le risorse, configura innanzitutto la funzione per recuperare i dati di reporting da Adobe Analytics. Per informazioni dettagliate, consulta [Configurare Asset Insights](#configure-asset-insights).

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

## Visualizzare le statistiche di un&#39;immagine {#viewing-statistics-for-an-image}

Puoi visualizzare i punteggi di Asset Insights dalla pagina dei metadati.

1. Dall’interfaccia utente di Assets, seleziona l’immagine e tocca **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Dalla pagina Proprietà, tocca **[!UICONTROL Informazioni]**.
1. Controlla i dettagli di utilizzo della risorsa nella scheda **[!UICONTROL Informazioni]** . La sezione **[!UICONTROL Punteggio]** descrive l’utilizzo totale delle risorse e le origini delle prestazioni di una risorsa .

   Il punteggio di utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   Il punteggio **[!UICONTROL Impression]** è il numero di volte in cui la risorsa viene caricata sul sito web. Il numero visualizzato in **[!UICONTROL Clic]** indica il numero di volte in cui la risorsa viene selezionata.

1. Consulta la sezione **[!UICONTROL Statistiche di utilizzo]** per sapere di quali entità faceva parte la risorsa e di quali soluzioni creative l’ha utilizzata di recente. Maggiore è l’utilizzo, maggiori sono le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le seguenti intestazioni:

   * **[!UICONTROL Risorsa]**: Il numero di volte in cui la risorsa faceva parte di una raccolta o di una risorsa composta.
   * **[!UICONTROL Web e dispositivi mobili]**: Il numero di volte in cui la risorsa faceva parte di siti web e app.
   * **[!UICONTROL Social]**: Il numero di volte in cui la risorsa è stata utilizzata nelle soluzioni, come Adobe Social e Adobe Campaign.
   * **[!UICONTROL E-mail]**: Il numero di volte in cui la risorsa è stata utilizzata nelle campagne e-mail.

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Poiché la funzione Asset Insights in genere recupera i dati delle soluzioni da Adobe Analytics in modo periodico, la sezione Soluzioni potrebbe non visualizzare i dati più recenti. Il periodo di tempo per il quale vengono visualizzati i dati dipende dalla pianificazione dell’operazione di recupero eseguita da Asset Insights per il recupero dei dati di Analytics.

1. Per visualizzare graficamente le statistiche sulle prestazioni della risorsa in un arco di tempo, seleziona il periodo nella sezione **[!UICONTROL Statistiche di prestazioni]**. I dettagli, compresi clic e impression, vengono visualizzati come linee di tendenza di un grafico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A differenza dei dati nella sezione Soluzioni , la sezione Statistiche di prestazioni visualizza i dati più recenti.

1. Per ottenere il codice di incorporamento della risorsa inclusa nei siti web per ottenere i dati sulle prestazioni, tocca o fai clic su **[!UICONTROL Ottieni codice di incorporamento]** sotto la miniatura della risorsa. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Visualizza le statistiche aggregate per le immagini {#viewing-aggregate-statistics-for-images}

Dalla **[!UICONTROL Visualizzazione approfondimenti]** puoi visualizzare simultaneamente un punteggio di tutte le risorse presenti all’interno di una cartella.

1. Nell’interfaccia utente di Assets, passa alla cartella contenente le risorse per le quali desideri visualizzare le informazioni.
1. Tocca o fai clic sull’icona Layout nella barra degli strumenti, quindi scegli **[!UICONTROL Visualizzazione approfondimenti]**.
1. Nella pagina vengono visualizzati i punteggi di utilizzo delle risorse. Confronta le valutazioni delle varie risorse e trai informazioni approfondite.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Asset Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Asset Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## Configurare Asset Insights {#configure-asset-insights}

[!DNL Experience Manager Assets] recupera i dati di utilizzo relativi alle risorse digitali utilizzate da siti web di terze parti da  [!DNL Adobe Analytics]. Per abilitare Asset Insights al recupero di questi dati e alla generazione di informazioni, configura innanzitutto la funzionalità di integrazione con [!DNL Adobe Analytics].

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Fai clic sulla scheda **[!UICONTROL Configurazione approfondimenti]**.
1. Nella procedura guidata, seleziona un centro dati e fornisci le tue credenziali, tra cui il nome dell’organizzazione, il nome utente e il segreto condiviso.

   ![Configurare Adobe Analytics per Assets Insights in  [!DNL Experience Manager]](assets/insights_config2.png)

   *Figura: Configurare Adobe Analytics per Assets Insights in[!DNL Experience Manager]*

1. Tocca o fai clic su **[!UICONTROL Autentica]**. Dopo che [!DNL Experience Manager] autentica le credenziali, dall’elenco **[!UICONTROL Suite di rapporti]** scegli una suite di rapporti Adobe Analytics dalla quale desideri che Asset Insights recuperi i dati. Fate clic su **[!UICONTROL Aggiungi]**.
1. Dopo che [!DNL Experience Manager] imposta la suite di rapporti, tocca **[!UICONTROL Fine]**.

### Tracciamento pagina {#page-tracker}

Dopo aver configurato l’account Adobe Analytics, viene generato il codice di tracciamento pagina . Per abilitare Asset Insights a tracciare le risorse [!DNL Experience Manager] utilizzate in siti web di terze parti, includi il codice di tracciamento della pagina nel codice del sito web. Utilizza l’utilità Tracciamento pagina in Assets per generare il codice di tracciamento pagina. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Nella pagina **[!UICONTROL Navigazione]**, fai clic sulla scheda **[!UICONTROL Tracciamento pagina approfondimenti]**.
1. Fai clic su **[!UICONTROL Scarica]** per scaricare il codice di tracciamento della pagina.

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
