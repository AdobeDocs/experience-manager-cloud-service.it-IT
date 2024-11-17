---
title: Report sull'utilizzo e la condivisione
description: Rapporti sulle risorse in [!DNL Adobe Experience Manager Assets] che ti aiutano a comprendere l'utilizzo, l'attività e la condivisione delle risorse digitali.
contentOwner: AG
feature: Asset Reports, Asset Management
role: Admin, User
exl-id: ef617b01-0019-4379-8d58-c03215d7e28f
source-git-commit: 6a03eb1a4ac8284299c1ffcf27d6a6c8a8b9abc4
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 10%

---

# Rapporti sulle risorse {#asset-reports}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Il reporting delle risorse consente di valutare l&#39;utilità della distribuzione di [!DNL Adobe Experience Manager Assets]. Con [!DNL Assets] puoi generare diversi rapporti per le risorse digitali. I report forniscono informazioni utili sull&#39;utilizzo del sistema, sulle modalità di interazione degli utenti con le risorse e sulle risorse condivise <!-- downloaded and -->.

Utilizza le informazioni contenute nei rapporti per derivare le metriche di successo chiave con cui misurare il livello di adozione di [!DNL Assets] all&#39;interno della tua azienda e da parte dei clienti.

Il framework di reporting [!DNL Assets] utilizza [!DNL Sling] processi in modo asincrono per elaborare le richieste di report in modo ordinato. È scalabile per archivi di grandi dimensioni. L’elaborazione asincrona dei rapporti aumenta l’efficienza e la velocità con cui vengono generati.

L’interfaccia di gestione dei rapporti è intuitiva e include opzioni e controlli dettagliati per accedere ai rapporti archiviati e visualizzare gli stati di esecuzione dei rapporti (operazione riuscita, non riuscita e in coda).

Quando viene generato un report, viene inviata una notifica tramite <!-- through an email (optional) and --> alla casella in entrata. Puoi visualizzare, scaricare o eliminare un rapporto dalla pagina dell’elenco dei rapporti, in cui vengono visualizzati tutti i rapporti generati in precedenza.

## Generare rapporti {#generate-reports}

[!DNL Experience Manager Assets] genera i seguenti rapporti standard:

* Carica
* Download
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicazione
* Utilizzo disco
* File
* Condivisione collegamenti

<!-- Removed download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Disk Usage
* Files
* Link Share
-->

Gli amministratori di [!DNL Adobe Experience Manager] possono generare e personalizzare facilmente questi rapporti per la tua implementazione. Per generare un rapporto, l’amministratore può effettuare le seguenti operazioni:

1. Nell&#39;interfaccia [!DNL Experience Manager], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Rapporti]**.

   ![Pagina Strumenti per passare al report risorse](assets/navigation.png)

1. Nella pagina [!UICONTROL Rapporti risorse], fai clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Crea report]**, scegli il report che desideri creare e fai clic su **[!UICONTROL Avanti]**.

   >[!NOTE]
   >
   >Iscriviti a un **profilo di prodotto Amministratore AEM** per creare un report **Scarica**. Consulta [Assegnazione dei profili di prodotto AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem) per acquisire il diritto a un profilo di prodotto Amministratore AEM.

   ![Seleziona tipo di report](assets/choose_report.png)

1. Configura i dettagli del rapporto come titolo, descrizione, miniatura e percorso della cartella. Per impostazione predefinita, il percorso della cartella è `/content/dam`. Puoi specificare un percorso diverso per eseguire il rapporto su una cartella specifica.

   ![Pagina per aggiungere dettagli report](assets/report_configuration.png)

   Scegli l’intervallo di date per il rapporto. Puoi scegliere di generare il rapporto ora o in una data e un’ora future.

   >[!NOTE]
   >
   >Se si sceglie di pianificare il rapporto in un secondo momento, assicurarsi di specificare la data e l&#39;ora nei campi Data e ora. Se non specifichi alcun valore, il motore di report lo tratta come un report che deve essere generato immediatamente.

   I campi di configurazione possono variare in base al tipo di rapporto creato. Ad esempio, il report **[!UICONTROL Utilizzo disco]** fornisce opzioni per includere le rappresentazioni delle risorse durante il calcolo dello spazio su disco utilizzato dalle risorse. Puoi scegliere di includere o escludere le risorse nelle sottocartelle per il calcolo dell’utilizzo del disco.

   >[!NOTE]
   >
   >Il rapporto **[!UICONTROL Utilizzo spazio su disco]** non include campi intervallo di date, poiché indica solo l’utilizzo attuale dello spazio.

   ![Pagina dettagli del report sull&#39;utilizzo del disco](assets/disk_usage_configuration.png)

   Quando crei il report **[!UICONTROL File]**, puoi includere/escludere sottocartelle. Tuttavia, per questo rapporto non puoi includere rappresentazioni di risorse.

   ![Dettagli del report File](assets/files_report.png)

   Il report **[!UICONTROL Condivisione collegamenti]** visualizza gli URL delle risorse condivise con utenti esterni da [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> Le colonne non sono personalizzabili.

   Il report **[!UICONTROL Condivisione collegamenti]** non include opzioni per sottocartelle e rendering, in quanto pubblica semplicemente gli URL condivisi visualizzati in `/var/dam/share`.

   ![Pagina dettagli del report Condivisione collegamenti](assets/link_share.png)

1. Fai clic su **[!UICONTROL Avanti]** nella barra degli strumenti.

1. Nella pagina **[!UICONTROL Configura colonne]**, alcune colonne sono selezionate per essere visualizzate nel report per impostazione predefinita. Puoi selezionare più colonne. Annulla la selezione di una colonna per escluderla nel rapporto.

   ![Selezionare o annullare la selezione delle colonne del report](assets/configure_columns.png)

   Per visualizzare un nome di colonna o un percorso di proprietà personalizzato, configura le proprietà per il binario della risorsa nel nodo `jcr:content` in CRX. In alternativa, aggiungilo tramite un selettore del percorso della proprietà.

   ![Selezionare o annullare la selezione delle colonne del report](assets/custom_columns.png)

1. Fai clic su **[!UICONTROL Crea]** nella barra degli strumenti. Un messaggio notifica che la generazione del rapporto è stata avviata.
1. Nella pagina [!UICONTROL Report risorse], lo stato di generazione del report si basa sullo stato corrente del processo di report, ad esempio [!UICONTROL Operazione riuscita], [!UICONTROL Non riuscita], [!UICONTROL In coda] o [!UICONTROL Pianificato]. Lo stesso stato viene visualizzato nella casella in entrata delle notifiche. Per visualizzare la pagina del rapporto, fai clic sul collegamento al rapporto. In alternativa, selezionare il report e fare clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.

   <!--![A generated report](assets/report_page.png)-->
   ![stato report generato](assets/report-status.JPG)

   Fai clic su **[!UICONTROL Scarica]** nella barra degli strumenti per scaricare il rapporto in formato CSV.

   >[!NOTE]
   >
   >Puoi generare rapporti in base agli eventi generati negli ultimi 360 giorni. Experience Manager conserva i dati dell’ID utente per 30 giorni.

## Aggiungere colonne personalizzate ai rapporti {#add-custom-columns}

Puoi aggiungere colonne personalizzate ai seguenti rapporti per visualizzare più dati in base ai tuoi requisiti personalizzati:

<!-- Remove download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Files
-->

* Carica
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicazione
* File

Per aggiungere colonne personalizzate a questi rapporti, effettua le seguenti operazioni:

1. In [!DNL Manager interface], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Rapporti]**.
1. Nella pagina [!UICONTROL Rapporti risorse], fai clic su **[!UICONTROL Crea]** nella barra degli strumenti.

1. Dalla pagina **[!UICONTROL Crea report]**, scegli un report da creare. Fai clic su **[!UICONTROL Avanti]**.

1. Configura i dettagli del rapporto come titolo, descrizione, miniatura, percorso della cartella e intervallo di date, a seconda dei casi. Fai clic su **[!UICONTROL Avanti]**.

1. Selezionare le informazioni applicabili dall&#39;elenco di **[!UICONTROL Colonne predefinite]**. Per visualizzare una colonna personalizzata, specificare il nome della colonna in **[!UICONTROL Colonne personalizzate]**.

   ![Specificare il nome per la colonna personalizzata del report](assets/custom_columns-1.png)

1. Aggiungi il percorso proprietà nel nodo `jcr:content` in CRXDE utilizzando il selettore del percorso proprietà. In alternativa, digita il percorso nel campo percorso proprietà.

   ![Mappa il percorso proprietà dai percorsi in jcr:content](assets/property_picker.png)

   Per aggiungere altre colonne personalizzate, fare clic su **[!UICONTROL Aggiungi]** e ripetere i passaggi precedenti.

1. Fai clic su **[!UICONTROL Crea]** nella barra degli strumenti. Un messaggio notifica l’avvio della generazione del rapporto.

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## Informazioni sulla risoluzione dei problemi {#tips-troubleshoot}

* Se il [!UICONTROL Report sull&#39;utilizzo del disco] non viene generato e si utilizza [!DNL Dynamic Media], verificare che tutte le risorse siano elaborate correttamente. Per risolvere il problema, rielabora le risorse e genera nuovamente il rapporto.

<!-- These notes were present in generate report section above. Removing commented text from in between the instructions to preserve the numbering of the ordered list.

TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

<!-- Removed download report.
   >[!NOTE]
   >
   >By default, the Content Fragments and link shares are included in the asset [!UICONTROL Download] report. Select the appropriate option to create a report of link shares or to exclude Content Fragments from the download report.

   >[!NOTE]
   >
   >The [!UICONTROL Download] report displays details of only those assets which are downloaded after selecting individually or are downloaded using Quick Action. However, it does not include the details of the assets that are inside a downloaded folder.
-->

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
