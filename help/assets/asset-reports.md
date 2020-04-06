---
title: Rapporti sulle risorse
description: Questo articolo descrive vari rapporti sulle risorse in Risorse AEM e come generare rapporti.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Rapporti su risorse {#asset-reports}

Il reporting delle risorse è uno strumento chiave per valutare l’utilità della distribuzione di Risorse Adobe Experience Manager (AEM). Risorse AEM consente di generare diversi rapporti sulle risorse digitali. I rapporti forniscono informazioni utili sull’utilizzo del sistema, su come gli utenti interagiscono con le risorse e quali risorse vengono scaricate e condivise.

Utilizzate le informazioni contenute nei rapporti per derivare le metriche di successo chiave per misurare l&#39;adozione di AEM Assets all&#39;interno dell&#39;azienda e da parte dei clienti.

Il framework di reporting di AEM Assets sfrutta i processi Sling per elaborare in modo asincrono le richieste di rapporti in modo ordinato. È scalabile per archivi di grandi dimensioni. L&#39;elaborazione asincrona dei report aumenta l&#39;efficienza e la velocità con cui vengono generati i report.

L&#39;interfaccia di gestione dei report è intuitiva e include opzioni e controlli di granulometria per accedere ai report archiviati e visualizzare gli stati di esecuzione dei report (operazione riuscita, non riuscita e in coda).

Quando viene generato un rapporto, riceverete una notifica via e-mail (facoltativo) e una notifica nella inbox. Puoi visualizzare, scaricare o eliminare un rapporto dalla pagina di elenco dei rapporti, dove vengono visualizzati tutti i rapporti generati in precedenza.

## Generazione di rapporti {#generate-reports}

Risorse AEM genera i seguenti rapporti standard:

* Carica
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* Pubblicazione Brand Portal
* Utilizzo disco
* File
* Condivisione collegamenti

Gli amministratori di AEM possono generare e personalizzare facilmente questi rapporti per la vostra implementazione. Per generare un rapporto, un amministratore può effettuare le seguenti operazioni:

1. Tocca o fai clic sul logo AEM, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.

   ![navigazione](assets/navigation.png)

1. Nella pagina Rapporti risorse, toccate o fate clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Dalla pagina **[!UICONTROL Crea rapporto]** , scegliete il rapporto che desiderate creare e toccate o fate clic su **[!UICONTROL Avanti]**.

   ![Choose_report](assets/choose_report.png)

   >[!NOTE]
   >
   >Prima di generare un rapporto sulle **[!UICONTROL risorse scaricate]**, accertati che il servizio di download delle risorse sia attivato. Dalla console web (`https://[aem_server]:[port]/system/console/configMgr`), apri la configurazione **[!UICONTROL Day CQ DAM Event Recorder]** e seleziona da Tipi di evento l’opzione **[!UICONTROL Risorsa scaricata (DOWNLOADED)]**, se non è già selezionata.

   >[!NOTE]
   >
   >Per impostazione predefinita, i frammenti di contenuto e le condivisioni di collegamenti sono inclusi nel rapporto Risorse scaricate. Selezionate l&#39;opzione appropriata per creare un rapporto delle condivisioni di collegamenti o per escludere i frammenti di contenuto dal rapporto di download.

1. Configurare i dettagli del rapporto come titolo, descrizione, miniatura e percorso della cartella nell&#39;archivio CRX in cui è memorizzato il rapporto. Per impostazione predefinita, il percorso della cartella è */content/dam*. Potete specificare un percorso diverso.

   ![report_configuration](assets/report_configuration.png)

   Scegli l&#39;intervallo di date per il rapporto.

   Puoi scegliere di generare il rapporto adesso o in una data e in un&#39;ora future.

   >[!NOTE]
   >
   >Se scegli di pianificare il rapporto in una data successiva, accertati di specificare la data e l&#39;ora nel campo Data e ora. Se non si specifica alcun valore, il motore di report lo gestisce come un report da generare all&#39;istante.

   I campi di configurazione possono essere diversi in base al tipo di rapporto creato.

   Ad esempio, il rapporto Uso **[!UICONTROL del]** disco offre opzioni per includere le rappresentazioni delle risorse nel calcolo dello spazio su disco utilizzato dalle risorse. Potete scegliere di includere o escludere le risorse nelle sottocartelle per il calcolo dell’utilizzo del disco.

   >[!NOTE]
   >
   >Il rapporto **[!UICONTROL Utilizzo spazio su disco]** non include campi intervallo di date, poiché indica solo l’utilizzo attuale dello spazio.

   ![disk_usage_configuration](assets/disk_usage_configuration.png)

   Quando create il rapporto **[!UICONTROL File]** , potete includere o escludere sottocartelle. Tuttavia, non potete includere rappresentazioni delle risorse per questo rapporto.

   ![files_report](assets/files_report.png)

   Il rapporto **[!UICONTROL Condivisione collegamenti]** visualizza gli URL delle risorse condivise con utenti esterni da AEM Assets. Include gli ID e-mail dell’utente che ha condiviso le risorse, gli ID e-mail degli utenti con cui le risorse sono condivise, la data di condivisione e la data di scadenza del collegamento. Le colonne non sono personalizzabili.

   Il rapporto **[!UICONTROL Condivisione collegamenti]** non include opzioni per sottocartelle e rendering, in quanto pubblica semplicemente gli URL condivisi che sono visualizzati in */var/dam/share*.

   ![link_share](assets/link_share.png)

1. Toccate o fate clic su **[!UICONTROL Avanti]** nella barra degli strumenti.

1. Nella pagina **[!UICONTROL Configura colonne]** , per impostazione predefinita nel rapporto vengono selezionate alcune colonne. È possibile selezionare ulteriori colonne. Deselezionate una colonna selezionata per escluderla nel rapporto.

   ![configure_Columns](assets/configure_columns.png)

   Per visualizzare un nome di colonna personalizzato o un percorso di proprietà, configurate le proprietà per il binario della risorsa sotto il nodo jcr:content in CRX. In alternativa, aggiungetelo tramite il selettore del percorso della proprietà.

   ![custom_Columns](assets/custom_columns.png)

1. Tap/click **[!UICONTROL Create]** from the toolbar. Un messaggio notifica che è stata avviata la generazione del report.
1. Nella pagina Rapporti risorse, lo stato di generazione del rapporto si basa sullo stato corrente del processo del rapporto, ad esempio Successo, Non riuscito, In coda o Pianificato. Lo stesso stato viene visualizzato nella inbox delle notifiche.

   Per visualizzare la pagina del rapporto, toccate o fate clic sul collegamento del rapporto. In alternativa, seleziona il rapporto e tocca o fai clic sull’icona Visualizza nella barra degli strumenti.

   ![report_page](assets/report_page.png)

   Toccate/fate clic sull’icona Scarica dalla barra degli strumenti per scaricare il rapporto in formato CSV.

## Aggiungere colonne personalizzate {#add-custom-columns}

Puoi aggiungere colonne personalizzate ai report seguenti per visualizzare più dati per i tuoi requisiti personalizzati:

* Carica
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* Pubblicazione Brand Portal
* File

1. Tocca o fai clic sul logo AEM, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.
1. Nella pagina Rapporti risorse, toccate o fate clic su **[!UICONTROL Crea]** dalla barra degli strumenti.

1. Dalla pagina **[!UICONTROL Crea rapporto]** , scegliete il rapporto che desiderate creare e toccate o fate clic su **[!UICONTROL Avanti]**.
1. Configura i dettagli del rapporto come titolo, descrizione, miniatura, percorso della cartella, intervallo di date e così via, a seconda dei casi.

1. Per visualizzare una colonna personalizzata, specificane il nome in **[!UICONTROL Colonne personalizzate]**.

   ![custom_Columns-1](assets/custom_columns-1.png)

1. Aggiungete il percorso della proprietà sotto il `jcr:content` nodo in CRXDE utilizzando il selettore del percorso della proprietà.

   ![property_picker](assets/property_picker.png)

   In alternativa, digitare il percorso nel campo percorso della proprietà.

   ![property_path](assets/property_path.png)

   Per aggiungere altre colonne personalizzate, toccate/fate clic su **[!UICONTROL Aggiungi]** e ripetete i passaggi 5 e 6.

1. Tap/click **[!UICONTROL Create]** from the toolbar. Un messaggio notifica che è stata avviata la generazione del report.

## Configurare il servizio di eliminazione {#configure-purging-service}

Per rimuovere i rapporti non più necessari, configura il servizio Rimozione rapporti DAM dalla console Web per eliminare i rapporti esistenti in base alla loro quantità e età.

1. Accedere alla console Web (Gestione configurazione) da `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri la configurazione **[!UICONTROL DAM Report Purge Service]** .
1. Specificare la frequenza (intervallo di tempo) per il servizio di eliminazione nel `scheduler.expression.name` campo. Puoi anche configurare la soglia di età e quantità per i rapporti.
1. Salva le modifiche.
