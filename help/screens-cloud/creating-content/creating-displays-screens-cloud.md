---
title: Creazione e gestione di visualizzazioni in Screens as a Cloud Service
description: Questa pagina descrive come creare e gestire le visualizzazioni in Screens as a Cloud Service.
exl-id: 0f9faa4b-b50e-40f8-a8ed-280f8bd0a9b8
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 3%

---

# Creazione e gestione di visualizzazioni in Screens as a Cloud Service {#create-displays-screens-cloud}

Dopo aver pubblicato il canale, è ora possibile creare la visualizzazione nel provider di servizi Screens.

Un display è un raggruppamento virtuale di schermi che sono generalmente posizionati uno accanto all’altro. Il display è di solito permanente rispetto a un&#39;installazione. Il contenuto di questo oggetto è ciò con cui gli autori lavorano e a cui fanno sempre riferimento come visualizzazione logica piuttosto che come controparti fisiche.

## Obiettivo {#objective}

Questo documento spiega come creare e gestire le visualizzazioni nel provider di servizi Screens. Dopo la lettura dovresti:

* Come creare ed eliminare le visualizzazioni
* Come organizzare gli schermi in cartelle

## Passaggi per creare una visualizzazione {#create-display}

Per creare la visualizzazione dal provider di servizi Screens, attenersi alla procedura descritta di seguito.

1. Dall’istanza di AEM Cloud Service, accedi a Screens Services Provider.
1. Seleziona **Visualizzazioni** dal pannello di navigazione a sinistra e fai clic su **Crea** nell&#39;angolo superiore destro dello schermo.

   ![immagine](/help/screens-cloud/assets/display/disp-1.png)

1. Seleziona **Visualizzazione** dalla barra delle azioni.

   ![immagine](/help/screens-cloud/assets/display/disp-2.png)

1. Immetti il titolo come **LoopingChannelDisplay** in **Nome visualizzato** e fai clic su **Crea**.

   ![immagine](/help/screens-cloud/assets/display/disp3.png)

1. La visualizzazione con titolo **LoopingChannelDisplay** sarà ora visibile nell&#39;elenco di visualizzazione.

   ![immagine](/help/screens-cloud/assets/display/disp-4.png)

### Eliminazione di una visualizzazione {#deleting-display}

È possibile eliminare una visualizzazione dal provider di servizi Screens.

Seleziona la visualizzazione e fai clic su **Elimina** nella parte inferiore del pannello, come illustrato nella figura seguente.

![immagine](/help/screens-cloud/assets/display/disp-5.png)

## Passaggi per organizzare le visualizzazioni in cartelle {#organize-display}

## Come attivare/disattivare la barra delle cartelle {#toggle-rail}

Puoi passare dalla barra delle cartelle alla visualizzazione di tutte le cartelle a cartelle specifiche:

1. Passare alla visualizzazione del magazzino visualizzato facendo clic sul pulsante evidenziato di seguito:

   ![immagine](/help/screens-cloud/assets/display/display-inventory.png)

1. Viene visualizzata la barra laterale della cartella.

   ![immagine](/help/screens-cloud/assets/display/toggle-rail.png)

1. Seleziona **Nascondi cartelle** per chiuderlo nuovamente.

## Come creare una cartella {#create-folder}

Puoi creare cartelle per organizzare meglio le visualizzazioni.

1. Passare alla visualizzazione delle scorte.
1. Assicurati di non essere attualmente in una cartella, dovresti vedere quanto segue:

   ![immagine](/help/screens-cloud/assets/display/verify-view.png)

   Nota: **Tutte le visualizzazioni** devono essere selezionate nella barra laterale della cartella e la navigazione delle breadcrumb deve mostrare solo **visualizzazioni**.

1. Fai clic sul pulsante Crea in alto a destra e seleziona l&#39;opzione **Cartella**.

   ![immagine](/help/screens-cloud/assets/display/Createfolder.png)

1. Inserisci il titolo della nuova cartella e fai clic su **Crea**.

   ![immagine](/help/screens-cloud/assets/display/Createfolder2.png)

## Come creare una cartella nidificata {#nested-folder}

1. Passare alla visualizzazione delle scorte.

1. Seleziona la cartella principale desiderata dalla barra laterale della cartella o navigando nella vista inventario.
1. Verifica che sia selezionata la cartella principale desiderata.

   ![immagine](/help/screens-cloud/assets/display/Nestedview.png)

   * La cartella deve essere selezionata nella barra laterale della cartella.
   * Nella navigazione delle breadcrumb deve essere visualizzato il nome della cartella corrente accanto a **Visualizzazioni**.

1. Fai clic su **Crea** in alto a destra e seleziona l&#39;opzione **Cartella**.

   ![immagine](/help/screens-cloud/assets/display/Createfolder.png)

1. Inserisci il titolo della nuova cartella e fai clic su **Crea**.

   ![immagine](/help/screens-cloud/assets/display/Createfolder2.png)

## Come spostare il contenuto in una nuova cartella {#move-folder}

Puoi spostare il contenuto nelle nuove cartelle per organizzare meglio le visualizzazioni.

1. Passare alla visualizzazione delle scorte.

1. Seleziona la cartella principale desiderata dalla barra laterale della cartella o selezionandola dalla vista inventario.

1. Verifica di aver selezionato la cartella principale desiderata.

![immagine](/help/screens-cloud/assets/display/movetofolder.png)

**Nota**: la cartella deve essere selezionata nella barra laterale della cartella. Inoltre, nella navigazione delle breadcrumb deve essere visualizzato il nome della cartella corrente accanto a **Visualizzazioni**.

## Come eliminare il contenuto da una cartella {#delete-folder}

Tutte le operazioni della cartella sono accessibili tramite la barra delle azioni di selezione nella vista inventario.

1. Passa alla cartella principale o selezionala dalla barra laterale.

1. Nella vista inventario, seleziona la cartella secondaria che desideri eliminare e assicurati che sia vuota.

1. Fai clic sull&#39;azione **Elimina** nella barra delle azioni di selezione. L’azione è disabilitata se la cartella non è vuota.


## Passaggio successivo {#whats-next}

Dopo aver appreso come creare e gestire le visualizzazioni per il progetto, è necessario continuare con l&#39;percorso di Screens as a Cloud Service esaminando il documento [Assegnazione del canale a una visualizzazione in Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/assigning-channels-to-display.html?lang=it).
