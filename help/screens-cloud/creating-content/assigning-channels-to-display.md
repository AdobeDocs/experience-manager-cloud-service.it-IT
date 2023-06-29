---
title: Assegnazione di un canale a una visualizzazione in Schermi as a Cloud Service
description: Questa pagina descrive come assegnare un canale a una visualizzazione in Screens as a Cloud Service.
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---

# Assegnazione di un canale a una visualizzazione in Schermi as a Cloud Service {#assign-channel-displays-screens-cloud}

Al termine della configurazione del progetto, devi assegnare il canale a una visualizzazione per visualizzarne il contenuto.

## Obiettivo {#objective}

Questo documento spiega come assegnare un canale a una visualizzazione, una volta che la visualizzazione è pronta e hai aggiunto contenuti al canale e lo hai pubblicato. Dopo aver letto, dovresti essere in grado di capire come assegnare un canale a una visualizzazione dal provider di servizi Screens.

## Prerequisiti {#prerequisites}

Prima di eseguire i passaggi seguenti per assegnare un canale a una visualizzazione, è necessario aver completato l’apprendimento:

* Creazione e gestione delle visualizzazioni
* Creazione e gestione dei canali

## Passaggi per assegnare un canale a una visualizzazione {#assign-channel-to-display}

Per assegnare un canale a una visualizzazione, segui i passaggi seguenti:

1. Passa a Screens Services Provider e seleziona **Display** dal pannello di navigazione a sinistra.

1. Clic **Assegna canale** sul display.

   ![immagine](/help/screens-cloud/assets/display/assignchannel-1.png)

1. Compila i campi seguenti da **Assegna un canale** .

   ![immagine](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. Seleziona il nome del canale dal menu a discesa.
   1. Scegli la priorità.

      >[!NOTE]
      >La priorità viene utilizzata per ordinare le assegnazioni nel caso in cui più corrispondano ai criteri di riproduzione. Quello con il valore più alto ha sempre la precedenza sui valori più bassi. Ad esempio, se sono presenti due canali A e B. A ha una priorità di 1 e B ha una priorità di 2, quindi viene visualizzato il canale B, in quanto ha una priorità più alta di A.

   1. Seleziona la data di inizio e la data di fine da **Attivazione**.

1. Clic **+ Aggiungi ricorrenza** per aggiungere una pianificazione di ricorrenza per il canale.

   ![immagine](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >Puoi aggiungere più pianificazioni ricorrenti al tuo canale. Le pianificazioni di ricorrenza introducono il DayParting, che consente di impostare una pianificazione globale con più canali in esecuzione in orari specifici del giorno e di riutilizzare quella configurazione per tutti i display contemporaneamente.

   È possibile impostare le seguenti opzioni:

   * **Nome**: titolo dello Schedule ricorrente.
   * **Ripeti**: scegli se la pianificazione viene eseguita su base giornaliera, settimanale, mensile o annuale.
   * **Inizio**: ora di inizio della pianificazione.
   * **Fine**: ora di fine della pianificazione. Puoi impostarla in base all’ora o alla durata.
   * **Ora**: la pianificazione termina a un’ora specificata.
   * **Durata**: la pianificazione viene eseguita per una particolare durata di tempo in ore o minuti.

1. Fai clic su **Crea**. Potete vedere che a quel display è assegnato un canale, come mostrato nella figura seguente.

   ![immagine](/help/screens-cloud/assets/display/assignchannel-3.png)


## Passaggio successivo {#whats-next}

Ora che hai assegnato il canale a una visualizzazione, devi continuare il percorso Screens as a Cloud Service esaminando il documento [Installazione e configurazione di Screens Player per AEM as a Cloud Service](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
