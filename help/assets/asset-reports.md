---
title: Rapporti sull’utilizzo e la condivisione
description: Rapporti sulle risorse in [!DNL Adobe Experience Manager Assets] per comprendere l'utilizzo, l'attività e la condivisione delle risorse digitali.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3ee2e53268ea77949057ac18fcb4a8f8b1e01cb2
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 7%

---


# Rapporti su risorse {#asset-reports}

Il reporting delle risorse consente di valutare l&#39;utilità della distribuzione [!DNL Adobe Experience Manager Assets]. Con [!DNL Assets] potete generare vari rapporti per le risorse digitali. I rapporti forniscono informazioni utili sull’utilizzo del sistema, su come gli utenti interagiscono con le risorse e quali risorse vengono scaricate e condivise.

Utilizzate le informazioni contenute nei report per derivare le metriche di successo chiave per misurare l&#39;adozione di [!DNL Assets] all&#39;interno dell&#39;azienda e da parte dei clienti.

Il framework di report [!DNL Assets] utilizza i processi [!DNL Sling] per elaborare in modo asincrono le richieste di report in modo ordinato. È scalabile per archivi di grandi dimensioni. L&#39;elaborazione asincrona dei report aumenta l&#39;efficienza e la velocità con cui vengono generati i report.

L&#39;interfaccia di gestione dei report è intuitiva e include opzioni e controlli di granulometria per accedere ai report archiviati e visualizzare gli stati di esecuzione dei report (operazione riuscita, non riuscita e in coda).

Quando viene generato un rapporto, riceverete una notifica da <!-- through an email (optional) and --> una notifica in entrata. Puoi visualizzare, scaricare o eliminare un rapporto dalla pagina di elenco dei rapporti, dove vengono visualizzati tutti i rapporti generati in precedenza.

## Genera report {#generate-reports}

[!DNL Experience Manager Assets] genera i seguenti rapporti standard:

* Carica
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicazione
* Utilizzo disco
* File
* Condivisione collegamenti

[!DNL Adobe Experience Manager] gli amministratori possono generare e personalizzare facilmente questi rapporti per la vostra implementazione. Per generare un rapporto, un amministratore può effettuare le seguenti operazioni:

1. Nell&#39;interfaccia [!DNL Experience Manager] fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.

   ![Pagina degli strumenti per navigare nel rapporto delle risorse](assets/navigation.png)

1. Nella pagina [!UICONTROL Report risorse], fate clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Crea rapporto]**, scegliere il rapporto che si desidera creare e fare clic su **[!UICONTROL Avanti]**.

   ![Selezionare il tipo di rapporto](assets/choose_report.png)

<!-- TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

>[!NOTE]
>
>Per impostazione predefinita, i frammenti di contenuto e le condivisioni di collegamenti sono inclusi nel rapporto Risorse [!UICONTROL Scarica]. Selezionate l&#39;opzione appropriata per creare un rapporto delle condivisioni di collegamenti o per escludere i frammenti di contenuto dal rapporto di download.

>[!NOTE]
>
>Il rapporto [!UICONTROL Download] visualizza i dettagli solo delle risorse che vengono scaricate dopo la selezione individuale o che vengono scaricate tramite la funzione Azione rapida. Tuttavia, non include i dettagli delle risorse che si trovano all’interno di una cartella scaricata.

1. Configurare i dettagli del rapporto come titolo, descrizione, miniatura e percorso della cartella nell&#39;archivio CRX in cui è memorizzato il rapporto. Per impostazione predefinita, il percorso della cartella è `/content/dam`. Potete specificare un percorso diverso.

   ![Pagina per aggiungere i dettagli del rapporto](assets/report_configuration.png)

   Scegli l&#39;intervallo di date per il rapporto.

   Puoi scegliere di generare il rapporto adesso o in una data e in un&#39;ora future.

   >[!NOTE]
   >
   >Se scegli di pianificare il rapporto in un secondo momento, accertati di specificare la data e l’ora nei campi Data e Ora. Se non si specifica alcun valore, il motore di report lo gestisce come un report da generare all&#39;istante.

   I campi di configurazione possono essere diversi in base al tipo di rapporto creato. Ad esempio, il rapporto **[!UICONTROL Uso del disco]** fornisce opzioni per includere le rappresentazioni delle risorse nel calcolo dello spazio su disco utilizzato dalle risorse. Potete scegliere di includere o escludere le risorse nelle sottocartelle per il calcolo dell’utilizzo del disco.

   >[!NOTE]
   >
   >Il rapporto **[!UICONTROL Utilizzo spazio su disco]** non include campi intervallo di date, poiché indica solo l’utilizzo attuale dello spazio.

   ![Pagina dei dettagli del rapporto Uso del disco](assets/disk_usage_configuration.png)

   Quando create il rapporto **[!UICONTROL File]**, potete includere o escludere sottocartelle. Tuttavia, non potete includere rappresentazioni delle risorse per questo rapporto.

   ![Pagina dei dettagli del rapporto sui file](assets/files_report.png)

   Il rapporto **[!UICONTROL Condivisione collegamenti]** visualizza gli URL delle risorse condivise con utenti esterni da [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> Le colonne non sono personalizzabili.

   Il rapporto **[!UICONTROL Condivisione collegamenti]** non include opzioni per sottocartelle e rappresentazioni, perché pubblica semplicemente gli URL condivisi visualizzati in `/var/dam/share`.

   ![Pagina dei dettagli del rapporto Condivisione collegamenti](assets/link_share.png)

1. Fare clic su **[!UICONTROL Next]** dalla barra degli strumenti.

1. Nella pagina **[!UICONTROL Configura colonne]**, per impostazione predefinita nel rapporto vengono selezionate alcune colonne. È possibile selezionare più colonne. Deselezionate una colonna selezionata per escluderla nel rapporto.

   ![Seleziona o deseleziona le colonne del rapporto](assets/configure_columns.png)

   Per visualizzare un nome di colonna o un percorso di proprietà personalizzato, configura le proprietà per il binario della risorsa sotto il nodo `jcr:content` in CRX. In alternativa, aggiungetelo tramite il selettore del percorso della proprietà.

   ![Seleziona o deseleziona le colonne del rapporto](assets/custom_columns.png)

1. Fare clic su **[!UICONTROL Crea]** dalla barra degli strumenti. Un messaggio notifica che è stata avviata la generazione del report.
1. Nella pagina [!UICONTROL Report risorse], lo stato di generazione del rapporto è basato sullo stato corrente del processo del rapporto, ad esempio [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued] o [!UICONTROL Scheduled]. Lo stesso stato viene visualizzato nella inbox delle notifiche.Per visualizzare la pagina del rapporto, fai clic sul collegamento del rapporto. In alternativa, selezionare il rapporto e fare clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.

   ![Report generato](assets/report_page.png)

   Fate clic su **[!UICONTROL Scarica]** dalla barra degli strumenti per scaricare il rapporto in formato CSV.

## Aggiungi colonne personalizzate {#add-custom-columns}

Puoi aggiungere colonne personalizzate ai report seguenti per visualizzare più dati per i tuoi requisiti personalizzati:

* Carica
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicazione
* File

Per aggiungere colonne personalizzate a questi rapporti, procedere come segue:

1. In [!DNL Manager interface], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.
1. Nella pagina [!UICONTROL Report risorse], fate clic su **[!UICONTROL Crea]** nella barra degli strumenti.

1. Dalla pagina **[!UICONTROL Crea rapporto]**, scegliere il rapporto che si desidera creare e fare clic su **[!UICONTROL Avanti]**.
1. Configura i dettagli del rapporto come titolo, descrizione, miniatura, percorso della cartella e intervallo di date, a seconda delle necessità.

1. Per visualizzare una colonna personalizzata, specificane il nome in **[!UICONTROL Colonne personalizzate]**.

   ![Specificare il nome per la colonna personalizzata del rapporto](assets/custom_columns-1.png)

1. Aggiungete il percorso della proprietà sotto il nodo `jcr:content` in CRXDE utilizzando il selettore del percorso della proprietà. In alternativa, digitare il percorso nel campo percorso della proprietà.

   ![Mappare il percorso della proprietà dai percorsi in jcr:content](assets/property_picker.png)

   Per aggiungere altre colonne personalizzate, fare clic su **[!UICONTROL Aggiungi]** e ripetere i passaggi 5 e 6.

1. Fare clic su **[!UICONTROL Crea]** dalla barra degli strumenti. Un messaggio notifica che è stata avviata la generazione del report.

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## Informazioni, suggerimenti e limitazioni per la risoluzione dei problemi {#best-practices-and-limitations}

* Se il rapporto sull&#39;uso del disco non viene generato e si utilizza [!DNL Dynamic Media], assicurarsi che tutte le risorse procedano correttamente. Per risolvere il problema, rielaborare le risorse e generare di nuovo il rapporto.
