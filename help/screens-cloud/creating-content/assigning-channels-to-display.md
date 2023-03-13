---
title: Assegnazione di un canale a una visualizzazione in Schermi as a Cloud Service
description: Questa pagina descrive come assegnare un canale a una visualizzazione in Screens as a Cloud Service.
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 19%

---

# Assegnazione di un canale a una visualizzazione in Schermi as a Cloud Service {#assign-channel-displays-screens-cloud}

Una volta completata la configurazione del progetto, devi assegnare il canale a una visualizzazione per visualizzare il contenuto.

## Obiettivo {#objective}

Questo documento spiega come assegnare un canale a una visualizzazione, una volta che la visualizzazione è pronta e hai aggiunto contenuti al canale e lo hai pubblicato. Dopo aver letto, dovresti essere in grado di capire come assegnare un canale a una visualizzazione dal provider di servizi Screens.

## Prerequisiti {#prerequisites}

Prima di eseguire i passaggi seguenti per assegnare un canale a una visualizzazione, è necessario aver completato l’apprendimento:

* Creazione e gestione delle visualizzazioni
* Creazione e gestione dei canali

## Passaggi per assegnare un canale a una visualizzazione {#assign-channel-to-display}

Segui la procedura seguente per assegnare un canale a una visualizzazione:

1. Passa a Screens Services Provider e seleziona **Display** dal pannello di navigazione a sinistra.

1. Fai clic su **Assegna canale** sul display.

   ![immagine](/help/screens-cloud/assets/display/assignchannel-1.png)

1. Compila i campi seguenti da **Assegna un canale** .

   ![immagine](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. Seleziona il nome del canale dal menu a discesa.
   1. Scegli la priorità.

      >[!NOTE]
      >La priorità viene usata per ordinare le assegnazioni nel caso in cui più utenti corrispondano ai criteri di riproduzione. Quella con il valore più alto avrà sempre la precedenza su quella con i valori più bassi. Ad esempio, se ci sono due canali A e B, A ha una priorità di 1 e B ha una priorità di 2, viene quindi visualizzato il canale B, che ha una priorità maggiore di A.
   1. Seleziona la data di inizio e la data di fine da **Attivazione**.

1. Fai clic su **+ Aggiungi ricorrenza** per aggiungere una pianificazione di ricorrenza per il canale.

   ![immagine](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >Puoi aggiungere più pianificazioni ricorrenti al tuo canale. La pianificazione della ricorrenza introduce la funzione DayParting, che consente di impostare una pianificazione globale con più canali in esecuzione in momenti specifici della giornata e di riutilizzare tale configurazione per tutti gli schermi contemporaneamente.

   È possibile impostare le seguenti opzioni:

   * **Nome**: titolo dello Schedule ricorrente.
   * **Ripeti**: scegli se la pianificazione viene eseguita su base giornaliera, settimanale, mensile o annuale.
   * **Inizio**: ora di inizio della pianificazione.
   * **Fine**: ora di fine della pianificazione. È possibile impostare l’IT in base all’ora o alla durata.
   * **Ora**: la pianificazione termina a un’ora specificata.
   * **Durata**: la pianificazione viene eseguita per una particolare durata di tempo in ore o minuti.

1. Fai clic su **Crea** e ora vedrete che a quel display è assegnato un canale, come mostrato nella figura seguente.

   ![immagine](/help/screens-cloud/assets/display/assignchannel-3.png)


## Passaggio successivo {#whats-next}

Ora che hai assegnato il canale a una visualizzazione, devi continuare il percorso Screens as a Cloud Service esaminando il documento [Installazione e configurazione di Screens Player per AEM as a Cloud Service](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
