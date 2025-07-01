---
title: Caricare risorse nell’archivio
description: Carica le risorse in [!DNL Assets view], visualizza lo stato di caricamento e risolvi eventuali problemi.
role: User
exl-id: 01af3b66-dba8-4b09-aadf-ba4ae09b824f
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 31c9e742d8bdf69c12788794670817864c9c027a
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 89%

---

# Caricare le risorse {#add-assets}

Per aggiungere nuove risorse con cui lavorare, carica alcune risorse dal file system locale. <!-- TBD: Many of the [common file formats are supported](/help/assets/supported-file-formats-assets-view.md). -->

Per caricare una o più risorse o una cartella contenente risorse, puoi utilizzare i seguenti metodi:

* Trascina risorse o cartelle nell’interfaccia utente e segui le istruzioni visualizzate.
* Fai clic sull&#39;opzione **[!UICONTROL Aggiungi Assets]** nella barra degli strumenti e aggiungi alcuni file alla finestra di dialogo di caricamento.

<!-- TBD: Update this GIF
![Asset and nested folder upload demo](assets/do-not-localize/upload-assets.gif) -->

Puoi utilizzare uno di questi metodi per caricare le risorse dopo aver creato una cartella. Per creare una cartella vuota, fai clic su **[!UICONTROL Crea cartella]** nella barra degli strumenti. [!DNL Assets view] offre una potente funzionalità di ricerca full-text ma puoi anche utilizzare le cartelle per organizzare meglio le risorse.

Dopo aver selezionato i file, viene visualizzata una finestra di dialogo di conferma per aggiungere altri file o rimuovere i file già selezionati. Per aggiungere altri file a una selezione, fai clic su **[!UICONTROL Sfoglia]** e seleziona **[!UICONTROL Sfoglia file]** o **[!UICONTROL Sfoglia cartelle]**. Aggiungi più file o cartelle dalla stessa cartella o da una cartella diversa.

Una volta messi in coda tutti i file, fai clic su **[!UICONTROL Carica]**.

![Caricare file e cartelle](assets/upload-browse-files-folders.png)

*Figura: Prima di caricare le risorse selezionate, si possono aggiungere o rimuovere le risorse dalla coda.*

>[!TIP]
>
>Se carichi una struttura di cartelle nella vista Assets, non è necessario creare un file .ZIP con la struttura di cartelle, puoi caricare direttamente le strutture di cartelle. Un file .ZIP caricato nella vista Assets viene memorizzato come una risorsa ZIP e non viene estratto automaticamente dopo il caricamento.

## Visualizzare lo stato e l’avanzamento del caricamento {#upload-progress}

Quando carichi più risorse o cartelle nidificate in [!DNL Assets view], alcune possono non essere caricate per vari motivi, ad esempio se sono duplicate o in caso di problemi di rete.

Per tenere traccia dell’avanzamento del caricamento, fai clic sull’opzione **[!UICONTROL Avanzamento caricamento]** nella barra degli strumenti. Un pannello mostra l’avanzamento del caricamento di tutte le risorse.

Per visualizzare un sottoinsieme di risorse in base all’avanzamento o allo stato del caricamento, utilizza il filtro nella barra laterale **[!UICONTROL Avanzamento caricamento]**. I vari filtri consentono di visualizzare tutte le risorse; i caricamenti completati, in corso e in pausa; e le risorse in coda da caricare, duplicate e il cui caricamento non è riuscito.

![Filtrare l’avanzamento del caricamento in base allo stato](assets/filter-upload-progress.png)

*Figura: Filtrare le risorse da caricare in base allo stato o all’avanzamento del caricamento.*

Non appena caricate, le risorse vengono elaborate da [!DNL Assets view] per generare miniature ed elaborare i metadati. Per molte risorse, l’elaborazione richiede un po’ di tempo. Se non vedi una miniatura e sulla miniatura segnaposto compare un messaggio di elaborazione, controlla nuovamente la cartella dopo qualche minuto. Durante l’elaborazione, [!DNL Assets view] genera anche le rappresentazioni, aggiunge tag avanzati e indicizza i dettagli della risorsa che verranno usati per le ricerche.

![Le risorse vengono elaborate al momento del caricamento e nelle relative sezioni compare la dicitura Elaborazione in corso](assets/upload-processing.png)

*Figura: Sezioni delle risorse caricate, con la dicitura “Elaborazione in corso”.*

## Rappresentazioni delle risorse {#renditions}

[!DNL Assets view] elabora le risorse caricate quasi in tempo reale e per molti tipi di file supportati genera le relative rappresentazioni. Create per le immagini, le rappresentazioni sono versioni ridimensionate dell’immagine caricata. Puoi scaricare non solo la risorsa, ma anche le sue rappresentazioni per utilizzare una versione appropriata all’utilizzo a cui è destinata. Puoi visualizzare tutte le rappresentazioni di una risorsa quando la [visualizzi in anteprima](/help/assets/navigate-assets-view.md#preview-assets).

![Rappresentazioni](assets/renditions-view-download.png)

*Figura: Visualizzare e scaricare le rappresentazioni.*

## Gestire i caricamenti non riusciti {#resolve-upload-fails}

Se il caricamento di una risorsa supportata non riesce per qualche motivo, fai clic su **[!UICONTROL Riprova]** nel riquadro [!UICONTROL Avanzamento caricamento].

![Riprovare un caricamento non riuscito](assets/upload-retry.png)

*Figura: Riprovare il caricamento di un file supportato che per qualche motivo non riesce.*

Se tenti di caricare risorse duplicate, queste non vengono caricate finché non confermi esplicitamente il caricamento. Inizialmente, le risorse duplicate vengono contrassegnate come caricamenti non riusciti. Per risolvere il problema, puoi semplicemente creare una versione, eliminare e sostituire la risorsa esistente o creare una copia duplicata rinominando la risorsa. Puoi risolvere tali errori una risorsa alla volta oppure in blocco, per tutti i duplicati non riusciti.

![Gestire le risorse duplicate una alla volta](assets/uploads-manage-duplicates.png)

*Figura: Per le risorse duplicate che non possono essere caricate per impostazione predefinita, risolvere il problema una risorsa alla volta.*

![Gestire in blocco tutti i caricamenti non riusciti](assets/upload-progress-manage-failed-uploads.png)

*Figura: Per le risorse duplicate che non possono essere caricate per impostazione predefinita, risolvi i problemi di tutte le risorse contemporaneamente.*

>[!TIP]
>
>È possibile caricare le risorse nell&#39;archivio DAM direttamente dalle applicazioni desktop [!DNL Creative Cloud].
<!--TBD
See how [[!DNL Assets view] integrates with [!DNL Adobe Asset Link]](/help/assets/integration-assets-view.md).
-->

## Eliminare risorse o cartelle {#delete-assets}

Gli utenti possono eliminare singole risorse o cartelle che non sono più necessarie. Per eliminare una risorsa o una cartella, effettua una delle seguenti operazioni:

* Utilizza l’opzione disponibile sulla miniatura di una risorsa o cartella.

  ![Opzioni sulla miniatura per gestire una risorsa](assets/options-on-thumbnail.png)

  *Figura: Le azioni per file e cartelle sono disponibili nella sezione della risorsa o cartella.*

* Seleziona una risorsa o una cartella e fai clic su **[!UICONTROL Elimina]** ![icona Elimina](assets/do-not-localize/delete-icon.png) nella barra degli strumenti.

## Passaggi successivi {#next-steps}

* [Guarda un video per caricare le risorse nella visualizzazione Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/creating.html?lang=it)

* Fornisci feedback sui prodotti utilizzando l’opzione [!UICONTROL Feedback] disponibile nell’interfaccia utente della vista Risorse

* Fornisci feedback alla documentazione utilizzando [!UICONTROL Modifica questa pagina] ![modifica la pagina](assets/do-not-localize/edit-page.png) o [!UICONTROL Segnala un problema] ![crea un problema GitHub](assets/do-not-localize/github-issue.png) disponibile sulla barra laterale destra

* Contatta il [Servizio clienti](https://experienceleague.adobe.com/it?support-solution=General&lang=it#support)
