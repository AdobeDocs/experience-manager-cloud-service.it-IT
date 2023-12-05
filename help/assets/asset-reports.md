---
title: Report sull'utilizzo e la condivisione
description: Rapporti sulle risorse in [!DNL Adobe Experience Manager Assets] che ti aiutano a comprendere l’utilizzo, l’attività e la condivisione delle risorse digitali.
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: ef617b01-0019-4379-8d58-c03215d7e28f
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 8%

---

# Rapporti sulle risorse {#asset-reports}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

La generazione di rapporti sulle risorse consente di valutare l’utilità della [!DNL Adobe Experience Manager Assets] distribuzione. Con [!DNL Assets], puoi generare vari rapporti per le risorse digitali. I rapporti forniscono informazioni utili sull’utilizzo del sistema, sul modo in cui gli utenti interagiscono con le risorse e su quali risorse vengono <!-- downloaded and --> condiviso.

Utilizza le informazioni contenute nei rapporti per derivare le metriche di successo chiave con cui misurare l’adozione di [!DNL Assets] all&#39;interno dell&#39;azienda e dai clienti.

Il [!DNL Assets] utilizzo del framework di reporting [!DNL Sling] processi per elaborare in modo asincrono le richieste di rapporti in modo ordinato. È scalabile per archivi di grandi dimensioni. L’elaborazione asincrona dei rapporti aumenta l’efficienza e la velocità con cui vengono generati.

L’interfaccia di gestione dei rapporti è intuitiva e include opzioni e controlli dettagliati per accedere ai rapporti archiviati e visualizzare gli stati di esecuzione dei rapporti (operazione riuscita, non riuscita e in coda).

Quando viene generato un rapporto, ricevi una notifica tramite <!-- through an email (optional) and --> una notifica casella in entrata. Puoi visualizzare, scaricare o eliminare un rapporto dalla pagina dell’elenco dei rapporti, in cui vengono visualizzati tutti i rapporti generati in precedenza.

## Generare rapporti {#generate-reports}

[!DNL Experience Manager Assets] genera automaticamente i seguenti rapporti standard:

* Carica
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicare
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

[!DNL Adobe Experience Manager] gli amministratori possono generare e personalizzare facilmente questi rapporti per la tua implementazione. Per generare un rapporto, l’amministratore può effettuare le seguenti operazioni:

1. In entrata [!DNL Experience Manager] , fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.

   ![Pagina Strumenti per passare al rapporto delle risorse](assets/navigation.png)

1. Il giorno [!UICONTROL Rapporti su risorse] pagina, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Dalla sezione **[!UICONTROL Crea rapporto]** , scegli il rapporto da creare e fai clic su **[!UICONTROL Successivo]**.

   ![Seleziona tipo di rapporto](assets/choose_report.png)

1. Configura i dettagli del rapporto come titolo, descrizione, miniatura e percorso della cartella. Per impostazione predefinita, il percorso della cartella è `/content/dam`. Puoi specificare un percorso diverso per eseguire il rapporto su una cartella specifica.

   ![Pagina per aggiungere i dettagli del rapporto](assets/report_configuration.png)

   Scegli l’intervallo di date per il rapporto. Puoi scegliere di generare il rapporto ora o in una data e un’ora future.

   >[!NOTE]
   >
   >Se si sceglie di pianificare il rapporto in un secondo momento, assicurarsi di specificare la data e l&#39;ora nei campi Data e ora. Se non specifichi alcun valore, il motore di report lo tratta come un report che deve essere generato immediatamente.

   I campi di configurazione possono variare in base al tipo di rapporto creato. Ad esempio, il **[!UICONTROL Utilizzo disco]** Il rapporto fornisce opzioni per includere le rappresentazioni delle risorse durante il calcolo dello spazio su disco utilizzato dalle risorse. Puoi scegliere di includere o escludere le risorse nelle sottocartelle per il calcolo dell’utilizzo del disco.

   >[!NOTE]
   >
   >Il rapporto **[!UICONTROL Utilizzo spazio su disco]** non include campi intervallo di date, poiché indica solo l’utilizzo attuale dello spazio.

   ![Pagina Dettagli del report Utilizzo disco](assets/disk_usage_configuration.png)

   Quando crei il **[!UICONTROL File]** rapporto, puoi includere/escludere sottocartelle. Tuttavia, per questo rapporto non puoi includere rappresentazioni di risorse.

   ![Pagina Dettagli del rapporto File](assets/files_report.png)

   Il **[!UICONTROL Condivisione collegamenti]** Il rapporto mostra gli URL delle risorse condivise con utenti esterni da [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> Le colonne non sono personalizzabili.

   Il **[!UICONTROL Condivisione collegamenti]** , non include opzioni per sottocartelle e rappresentazioni, in quanto pubblica semplicemente gli URL condivisi visualizzati in `/var/dam/share`.

   ![Pagina dei dettagli del rapporto Condivisione collegamenti](assets/link_share.png)

1. Clic **[!UICONTROL Successivo]** dalla barra degli strumenti.

1. In **[!UICONTROL Configura colonne]** , alcune colonne vengono selezionate per essere visualizzate nel rapporto per impostazione predefinita. Puoi selezionare più colonne. Annulla la selezione di una colonna per escluderla nel rapporto.

   ![Seleziona o annulla la selezione delle colonne del rapporto](assets/configure_columns.png)

   Per visualizzare il nome di una colonna personalizzata o il percorso di una proprietà, configura le proprietà del binario della risorsa in `jcr:content` in CRX. In alternativa, aggiungilo tramite il selettore del percorso delle proprietà.

   ![Seleziona o annulla la selezione delle colonne del rapporto](assets/custom_columns.png)

1. Clic **[!UICONTROL Crea]** dalla barra degli strumenti. Un messaggio notifica che la generazione del rapporto è stata avviata.
1. Il giorno [!UICONTROL Rapporti su risorse] pagina, lo stato di generazione del rapporto si basa sullo stato corrente del processo di rapporto, ad esempio, [!UICONTROL Completato], [!UICONTROL Non riuscito], [!UICONTROL In coda], o [!UICONTROL Pianificato]. Lo stesso stato viene visualizzato nella casella in entrata delle notifiche.Per visualizzare la pagina del report, fare clic sul collegamento al report. In alternativa, seleziona il rapporto e fai clic su **[!UICONTROL Visualizza]** dalla barra degli strumenti.

   ![Un rapporto generato](assets/report_page.png)

   Clic **[!UICONTROL Scarica]** dalla barra degli strumenti per scaricare il rapporto in formato CSV.

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
* [!DNL Brand Portal] pubblicare
* File

Per aggiungere colonne personalizzate a questi rapporti, effettua le seguenti operazioni:

1. In [!DNL Manager interface], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.
1. Il giorno [!UICONTROL Rapporti su risorse] pagina, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti.

1. Dalla sezione **[!UICONTROL Crea rapporto]** , scegli un rapporto da creare. Fai clic su **[!UICONTROL Avanti]**.

1. Configura i dettagli del rapporto come titolo, descrizione, miniatura, percorso della cartella e intervallo di date, a seconda dei casi. Fai clic su **[!UICONTROL Avanti]**.

1. Seleziona le informazioni applicabili dall’elenco di **[!UICONTROL Colonne predefinite]**. Per visualizzare una colonna personalizzata, specifica il nome della colonna in **[!UICONTROL Colonne personalizzate]**.

   ![Specifica il nome per la colonna personalizzata del rapporto](assets/custom_columns-1.png)

1. Aggiungi il percorso della proprietà sotto `jcr:content` in CRXDE utilizzando il selettore del percorso delle proprietà. In alternativa, digita il percorso nel campo percorso proprietà.

   ![Mappare il percorso proprietà dai percorsi in jcr:content](assets/property_picker.png)

   Per aggiungere altre colonne personalizzate, fai clic su **[!UICONTROL Aggiungi]** e ripetere i passaggi precedenti.

1. Clic **[!UICONTROL Crea]** dalla barra degli strumenti. Un messaggio notifica l’avvio della generazione del rapporto.

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## Informazioni sulla risoluzione dei problemi {#tips-troubleshoot}

* Se il [!UICONTROL Rapporto utilizzo disco] non genera e se utilizzi [!DNL Dynamic Media], assicurati che tutte le risorse vengano elaborate correttamente. Per risolvere il problema, rielabora le risorse e genera nuovamente il rapporto.

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
