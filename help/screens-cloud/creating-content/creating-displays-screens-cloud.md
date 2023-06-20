---
title: Creazione e gestione di visualizzazioni in Schermi as a Cloud Service
description: Questa pagina descrive come creare e gestire le visualizzazioni in Screens as a Cloud Service.
exl-id: 0f9faa4b-b50e-40f8-a8ed-280f8bd0a9b8
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 3%

---

# Creazione e gestione di visualizzazioni in Schermi as a Cloud Service {#create-displays-screens-cloud}

Dopo aver pubblicato il canale, è ora possibile creare la visualizzazione nel provider di servizi Screens.

Un display è un raggruppamento virtuale di schermi che sono generalmente posizionati uno accanto all’altro. Il display è di solito permanente rispetto a un&#39;installazione. Il contenuto di questo oggetto è ciò con cui gli autori lavorano e a cui fanno sempre riferimento come visualizzazione logica piuttosto che come controparti fisiche.

## Obiettivo {#objective}

Questo documento spiega come creare e gestire le visualizzazioni nel provider di servizi Screens. Dopo la lettura dovresti:

* Come creare ed eliminare le visualizzazioni
* Come organizzare gli schermi in cartelle

## Passaggi per creare una visualizzazione {#create-display}

Per creare la visualizzazione dal provider di servizi Screens, effettua le seguenti operazioni:

1. Dalla tua istanza di AEM Cloud Service, accedi al provider di servizi Screens.
1. Seleziona **Display** dal pannello di navigazione a sinistra e fai clic su **Crea** dall&#39;angolo in alto a destra dello schermo.

   ![immagine](/help/screens-cloud/assets/display/disp-1.png)

1. Seleziona **Visualizzazione** dalla barra delle azioni.

   ![immagine](/help/screens-cloud/assets/display/disp-2.png)

1. Inserisci il titolo come **LoopChannelDisplay** in **Nome visualizzato** e fai clic su **Crea**.

   ![immagine](/help/screens-cloud/assets/display/disp3.png)

1. La visualizzazione con titolo **LoopChannelDisplay** sarà ora visibile nell’elenco di visualizzazione.

   ![immagine](/help/screens-cloud/assets/display/disp-4.png)

### Eliminazione di una visualizzazione {#deleting-display}

È possibile eliminare una visualizzazione dal provider di servizi Screens.

Seleziona la visualizzazione e fai clic su **Elimina** dalla parte inferiore del pannello, come illustrato nella figura riportata di seguito.

![immagine](/help/screens-cloud/assets/display/disp-5.png)

## Passaggi per organizzare le visualizzazioni in cartelle {#organize-display}

## Come attivare/disattivare la barra delle cartelle {#toggle-rail}

Puoi passare dalla barra delle cartelle alla visualizzazione di tutte le cartelle a cartelle specifiche:

1. Passare alla visualizzazione del magazzino visualizzato facendo clic sul pulsante evidenziato di seguito:

   ![immagine](/help/screens-cloud/assets/display/display-inventory.png)

1. Viene visualizzata la barra laterale della cartella.

   ![immagine](/help/screens-cloud/assets/display/toggle-rail.png)

1. Seleziona **Nascondi cartelle** per chiuderlo di nuovo.

## Come creare una nuova cartella {#create-folder}

Puoi creare cartelle per organizzare meglio le visualizzazioni.

1. Passare alla visualizzazione delle scorte.
1. Assicurati di non essere attualmente in una cartella, dovresti vedere quanto segue:

   ![immagine](/help/screens-cloud/assets/display/verify-view.png)

   Nota: **Tutte le visualizzazioni** deve essere selezionato nella barra laterale delle cartelle e la navigazione breadcrumb deve mostrare solo **Display**.

1. Fai clic sul pulsante &quot;Crea&quot; in alto a destra e seleziona la **Cartella** opzione.

   ![immagine](/help/screens-cloud/assets/display/Createfolder.png)

1. Inserisci il titolo della nuova cartella e fai clic su **Crea**.

   ![immagine](/help/screens-cloud/assets/display/Createfolder2.png)

## Come creare una nuova cartella nidificata {#nested-folder}

1. Passare alla visualizzazione delle scorte.

1. Seleziona la cartella principale desiderata dalla barra laterale della cartella o navigando nella vista inventario.
1. Verifica che sia selezionata la cartella principale desiderata.

   ![immagine](/help/screens-cloud/assets/display/Nestedview.png)

   * La cartella deve essere selezionata nella barra laterale della cartella.
   * La navigazione delle breadcrumb deve mostrare il nome della cartella corrente accanto a **Display**.

1. Clic  **Crea**  in alto a destra e seleziona la **Cartella** opzione.

   ![immagine](/help/screens-cloud/assets/display/Createfolder.png)

1. Inserisci il titolo della nuova cartella e fai clic su **Crea**.

   ![immagine](/help/screens-cloud/assets/display/Createfolder2.png)

## Come spostare il contenuto in una nuova cartella {#move-folder}

Puoi spostare il contenuto nelle nuove cartelle per organizzare meglio le visualizzazioni.

1. Passare alla visualizzazione delle scorte.

1. Seleziona la cartella principale desiderata dalla barra laterale della cartella o selezionandola dalla vista inventario.

1. Verifica di aver selezionato la cartella principale desiderata.

![immagine](/help/screens-cloud/assets/display/movetofolder.png)

**Nota**: la cartella deve essere selezionata nella barra laterale della cartella. Inoltre, la navigazione delle breadcrumb deve mostrare il nome della cartella corrente accanto a **Display**.

## Come eliminare il contenuto da una cartella {#delete-folder}

Tutte le operazioni della cartella sono accessibili tramite la barra delle azioni di selezione nella vista inventario.

1. Passa alla cartella principale o selezionala dalla barra laterale.

1. Nella vista inventario, seleziona la cartella secondaria che desideri eliminare e assicurati che sia vuota.

1. Clic **Elimina** nella barra delle azioni di selezione. L’azione è disabilitata se la cartella non è vuota.


## Passaggio successivo {#whats-next}

Ora che hai imparato a creare e gestire le visualizzazioni per il progetto, devi continuare il percorso Screens as a Cloud Service esaminando il documento [Assegnazione di un canale a una visualizzazione in Schermi as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/assigning-channels-to-display.html?lang=en).
