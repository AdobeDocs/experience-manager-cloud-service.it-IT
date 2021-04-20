---
title: Rapporti su utilizzo e condivisione
description: Rapporti sulle risorse in [!DNL Adobe Experience Manager Assets] per comprendere l’utilizzo, l’attività e la condivisione delle risorse digitali.
contentOwner: AG
feature: Asset Reports,Asset Management
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 8%

---


# Rapporti sulle risorse {#asset-reports}

Il reporting delle risorse consente di valutare l’utilità della distribuzione [!DNL Adobe Experience Manager Assets]. Con [!DNL Assets] puoi generare vari rapporti per le risorse digitali. I rapporti forniscono informazioni utili sull’utilizzo del sistema, sul modo in cui gli utenti interagiscono con le risorse e sulle risorse <!-- downloaded and --> condivise.

Utilizza le informazioni contenute nei rapporti per derivare le metriche di successo chiave per misurare l’adozione di [!DNL Assets] all’interno dell’azienda e da parte dei clienti.

Il framework di reporting [!DNL Assets] utilizza [!DNL Sling] processi per elaborare in modo asincrono le richieste di report in modo ordinato. È scalabile per archivi di grandi dimensioni. L’elaborazione asincrona dei rapporti aumenta l’efficienza e la velocità con cui vengono generati i rapporti.

L’interfaccia di gestione dei rapporti è intuitiva e include opzioni e controlli a grana fine per accedere ai rapporti archiviati e visualizzare gli stati di esecuzione dei rapporti (con esito positivo, non riuscito e in coda).

Quando viene generato un rapporto, riceverai una notifica tramite <!-- through an email (optional) and --> una notifica nella casella in entrata. Puoi visualizzare, scaricare o eliminare un rapporto dalla pagina di elenco dei rapporti, in cui vengono visualizzati tutti i rapporti generati in precedenza.

## Genera report {#generate-reports}

[!DNL Experience Manager Assets] genera i seguenti rapporti standard:

* Carica
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

[!DNL Adobe Experience Manager] gli amministratori possono generare e personalizzare facilmente questi rapporti per la tua implementazione. Un amministratore può seguire questi passaggi per generare un rapporto:

1. Nell&#39;interfaccia [!DNL Experience Manager] fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.

   ![Pagina degli strumenti per navigare nel rapporto delle risorse](assets/navigation.png)

1. Nella pagina [!UICONTROL Rapporti su risorse], fai clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Crea rapporto]**, scegli il rapporto che desideri creare e fai clic su **[!UICONTROL Avanti]**.

   ![Seleziona tipo di rapporto](assets/choose_report.png)

1. Configura i dettagli del rapporto come titolo, descrizione, miniatura e percorso della cartella nell&#39;archivio CRX in cui è memorizzato il rapporto. Per impostazione predefinita, il percorso della cartella è `/content/dam`. È possibile specificare un percorso diverso.

   ![Pagina per aggiungere i dettagli del rapporto](assets/report_configuration.png)

   Scegli l’intervallo di date per il rapporto. Puoi scegliere di generare il rapporto ora o in una data e in un’ora future.

   >[!NOTE]
   >
   >Se scegli di pianificare il rapporto in un secondo momento, accertati di specificare la data e l’ora nei campi Data e ora. Se non si specifica alcun valore, il motore di report lo considera come un report da generare immediatamente.

   I campi di configurazione possono variare a seconda del tipo di rapporto creato. Ad esempio, il rapporto **[!UICONTROL Utilizzo del disco]** fornisce opzioni per includere le rappresentazioni delle risorse nel calcolo dello spazio su disco utilizzato dalle risorse. È possibile scegliere di includere o escludere le risorse nelle sottocartelle per il calcolo dell’utilizzo del disco.

   >[!NOTE]
   >
   >Il rapporto **[!UICONTROL Utilizzo spazio su disco]** non include campi intervallo di date, poiché indica solo l’utilizzo attuale dello spazio.

   ![Pagina dei dettagli del rapporto Utilizzo disco](assets/disk_usage_configuration.png)

   Quando crei il rapporto **[!UICONTROL File]**, puoi includere o escludere le sottocartelle. Tuttavia, non puoi includere rappresentazioni di risorse per questo rapporto.

   ![Pagina dei dettagli del rapporto File](assets/files_report.png)

   Il rapporto **[!UICONTROL Condivisione collegamenti]** visualizza gli URL delle risorse condivise con utenti esterni da [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> Le colonne non sono personalizzabili.

   Il rapporto **[!UICONTROL Condivisione collegamenti]** non include opzioni per le sottocartelle e i rendering, in quanto pubblica semplicemente gli URL condivisi visualizzati in `/var/dam/share`.

   ![Pagina dei dettagli del rapporto Condivisione collegamenti](assets/link_share.png)

1. Fare clic su **[!UICONTROL Avanti]** nella barra degli strumenti.

1. Nella pagina **[!UICONTROL Configura colonne]**, alcune colonne sono selezionate per essere visualizzate nel rapporto per impostazione predefinita. Puoi selezionare più colonne. Annulla la selezione di una colonna per escluderla nel rapporto.

   ![Selezionare o annullare la selezione delle colonne del rapporto](assets/configure_columns.png)

   Per visualizzare un nome di colonna personalizzato o un percorso di proprietà, configura le proprietà per il binario di risorsa sotto il nodo `jcr:content` in CRX. In alternativa, aggiungilo tramite il selettore del percorso della proprietà.

   ![Selezionare o annullare la selezione delle colonne del rapporto](assets/custom_columns.png)

1. Fai clic su **[!UICONTROL Crea]** nella barra degli strumenti. Un messaggio notifica l’avvio della generazione del rapporto.
1. Nella pagina [!UICONTROL Rapporti su risorse], lo stato di generazione del rapporto si basa sullo stato corrente del processo di rapporto, ad esempio [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued] o [!UICONTROL Scheduled]. Lo stesso stato viene visualizzato nella casella in entrata delle notifiche.Per visualizzare la pagina del rapporto, fare clic sul collegamento del rapporto. In alternativa, seleziona il rapporto e fai clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.

   ![Un rapporto generato](assets/report_page.png)

   Fai clic su **[!UICONTROL Scarica]** dalla barra degli strumenti per scaricare il rapporto in formato CSV.

## Aggiungi colonne personalizzate ai rapporti {#add-custom-columns}

Puoi aggiungere colonne personalizzate ai seguenti rapporti per visualizzare più dati per le tue esigenze personalizzate:

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
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicazione
* File

Per aggiungere colonne personalizzate a questi rapporti, effettua le seguenti operazioni:

1. In [!DNL Manager interface], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.
1. Nella pagina [!UICONTROL Rapporti su risorse], fai clic su **[!UICONTROL Crea]** nella barra degli strumenti.

1. Dalla pagina **[!UICONTROL Crea rapporto]**, scegli un rapporto da creare. Fai clic su **[!UICONTROL Avanti]**.

1. Configura i dettagli del rapporto come titolo, descrizione, miniatura, percorso della cartella e intervallo di date, a seconda delle necessità. Fai clic su **[!UICONTROL Avanti]**.

1. Selezionare le informazioni applicabili dall&#39;elenco **[!UICONTROL Colonne predefinite]**. Per visualizzare una colonna personalizzata, specificane il nome **[!UICONTROL Colonne personalizzate]**.

   ![Specifica il nome della colonna del report personalizzata](assets/custom_columns-1.png)

1. Aggiungi il percorso della proprietà sotto il nodo `jcr:content` in CRXDE utilizzando il selettore del percorso della proprietà. In alternativa, digitare il percorso nel campo percorso della proprietà.

   ![Mappa il percorso della proprietà dai percorsi in jcr:content](assets/property_picker.png)

   Per aggiungere altre colonne personalizzate, fai clic su **[!UICONTROL Aggiungi]** e ripeti i passaggi precedenti.

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

* Se il [!UICONTROL Rapporto sull&#39;utilizzo del disco] non viene generato e se utilizzi [!DNL Dynamic Media], assicurati che tutte le risorse procedano correttamente. Per risolvere il problema, rielabora le risorse e genera di nuovo il rapporto.

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
