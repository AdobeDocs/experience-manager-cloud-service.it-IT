---
title: Creazione e gestione delle visualizzazioni in Screens as a Cloud Service
description: Questa pagina descrive come creare e gestire le visualizzazioni in Screens as a Cloud Service.
exl-id: 0f9faa4b-b50e-40f8-a8ed-280f8bd0a9b8
source-git-commit: 9e0ab778e97658bc8d7669b1f582f3bcddd47915
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 8%

---

# Creazione e gestione delle visualizzazioni in Screens as a Cloud Service {#create-displays-screens-cloud}

Dopo aver pubblicato il canale, è ora di creare la visualizzazione nel provider di servizi Screens.

Una visualizzazione è un raggruppamento virtuale di schermate solitamente posizionate una accanto all’altra. La visualizzazione è solitamente permanente per quanto riguarda l’installazione. Questo sarà l’oggetto con il quale gli autori di contenuti lavoreranno e al quale faranno sempre riferimento come visualizzazione logica piuttosto che le controparti fisiche.

## Obiettivo {#objective}

Questo documento spiega come creare e gestire le visualizzazioni nel provider di servizi Screens. Dopo la lettura dovresti:

* Come creare ed eliminare le visualizzazioni
* Informazioni su come organizzare le visualizzazioni in cartelle

## Passaggi per creare una visualizzazione {#create-display}

Segui i passaggi riportati di seguito per creare la visualizzazione dal provider di servizi Screens:

1. Passa a Screens Services Provider dalla tua istanza AEM Cloud Service.
1. Seleziona **Display** dal pannello di navigazione a sinistra e fai clic su **Crea** dall’angolo in alto a destra dello schermo.

   ![immagine](/help/screens-cloud/assets/display/disp-1.png)

1. Seleziona **Visualizzazione** dalla barra delle azioni.

   ![immagine](/help/screens-cloud/assets/display/disp-2.png)

1. Inserisci il titolo come **LoopingChannelDisplay** in **Nome visualizzato** e fai clic su **Crea**.

   ![immagine](/help/screens-cloud/assets/display/disp3.png)

1. Visualizzazione con titolo come **LoopingChannelDisplay** sarà ora visibile nell’elenco di visualizzazione.

   ![immagine](/help/screens-cloud/assets/display/disp-4.png)

### Eliminazione di una visualizzazione {#deleting-display}

È possibile eliminare una visualizzazione da Screens Services Provider.

Seleziona la visualizzazione e fai clic su **Elimina** dal fondo del pannello, come illustrato nella figura riportata di seguito.

![immagine](/help/screens-cloud/assets/display/disp-5.png)

## Passaggi per organizzare le visualizzazioni in cartelle {#organize-display}

## Come attivare/disattivare la barra delle cartelle {#toggle-rail}

Puoi cambiare la barra della cartella dalla visualizzazione di tutte le cartelle a cartelle specifiche:

1. Passa alla visualizzazione Inventario visualizzata facendo clic sul pulsante evidenziato di seguito:

   ![immagine](/help/screens-cloud/assets/display/display-inventory.png)

1. Viene visualizzata la barra laterale della cartella.

   ![immagine](/help/screens-cloud/assets/display/toggle-rail.png)

1. Seleziona **Nascondi cartelle** per chiuderlo di nuovo.

## Come creare una nuova cartella {#create-folder}

Puoi creare cartelle per organizzare meglio le visualizzazioni.

1. Passa alla visualizzazione Inventario visualizzata.
1. Assicurati di non essere attualmente in una cartella. Dovresti vedere quanto segue:

   ![immagine](/help/screens-cloud/assets/display/verify-view.png)

   Nota: **Tutte le visualizzazioni** deve essere selezionato nella barra laterale della cartella e la navigazione nel breadcrumb deve essere visualizzata solo **Display**.

1. Fai clic sul pulsante &quot;Crea&quot; in alto a destra e seleziona la **Cartella** opzione .

   ![immagine](/help/screens-cloud/assets/display/Createfolder.png)

1. Inserisci il titolo della nuova cartella e fai clic su **Crea**.

   ![immagine](/help/screens-cloud/assets/display/Createfolder2.png)

## Come creare una nuova cartella nidificata {#nested-folder}

1. Passa alla visualizzazione Inventario visualizzata.

1. Seleziona la cartella principale desiderata dalla barra laterale della cartella o sfogliando nella vista Inventario.
1. Verificare che la cartella principale desiderata sia selezionata.

   ![immagine](/help/screens-cloud/assets/display/Nestedview.png)

   * La cartella deve essere selezionata nella barra laterale della cartella.
   * Nella navigazione breadcrumb deve essere visualizzato il nome della cartella corrente accanto a **Display**.

1. Fai clic su  **Crea**  in alto a destra e seleziona la **Cartella** opzione .

   ![immagine](/help/screens-cloud/assets/display/Createfolder.png)

1. Inserisci il titolo della nuova cartella e fai clic su **Crea**.

   ![immagine](/help/screens-cloud/assets/display/Createfolder2.png)

## Come spostare il contenuto in una nuova cartella {#move-folder}

È possibile spostare i contenuti nelle nuove cartelle per organizzare meglio i display.

1. Passa alla visualizzazione Inventario visualizzata.

1. Seleziona la cartella principale desiderata dalla barra laterale della cartella o dalla vista Inventario.

1. Verificare di aver selezionato la cartella padre desiderata.

![immagine](/help/screens-cloud/assets/display/movetofolder.png)

**Nota**: La cartella deve essere selezionata nella barra laterale della cartella. Inoltre, la navigazione breadcrumb deve mostrare il nome della cartella corrente accanto a **Display**.

## Eliminare il contenuto da una cartella {#delete-folder}

Tutte le operazioni relative alle cartelle sono accessibili tramite la barra delle azioni di selezione nella vista Inventario.

1. Passa alla cartella principale o selezionala dalla barra laterale.

1. Nella vista Inventario, seleziona la cartella figlio desiderata da eliminare e accertati che sia vuota.

1. Fai clic sul pulsante **Elimina** nella barra delle azioni di selezione. Se la cartella non è vuota, l’azione verrà disabilitata.


## Novità {#whats-next}

Dopo aver appreso come creare e gestire le visualizzazioni per il progetto, dovresti continuare il percorso as a Cloud Service Screens esaminando il documento [Assegnazione di un canale a una visualizzazione in Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/assigning-channels-to-display.html?lang=en).
