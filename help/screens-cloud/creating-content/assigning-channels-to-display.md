---
title: Assegnazione di un canale a una visualizzazione in Screens come Cloud Service
description: Questa pagina descrive come assegnare un canale a una visualizzazione in Screens come Cloud Service.
hide: true
hidefromtoc: true
index: false
source-git-commit: c65eeaf74ddfd81d37eb7090b84c8bf6f876dc72
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 19%

---


# Assegnazione di un canale a una visualizzazione in Screens come Cloud Service {#assign-channel-displays-screens-cloud}

Una volta completata la configurazione del progetto, devi assegnare il canale a una visualizzazione per visualizzare il contenuto.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come assegnare un canale a una visualizzazione, una volta che la visualizzazione è pronta, hai aggiunto il contenuto al tuo canale e lo hai pubblicato. Dopo aver letto, dovresti essere in grado di capire come assegnare un canale a una visualizzazione da Screens Services Provider.

## Prerequisiti {#prerequisites}

Prima di eseguire i passaggi seguenti per assegnare un canale a una visualizzazione, è necessario aver terminato l&#39;apprendimento:

* Creazione e gestione delle visualizzazioni
* Creazione e gestione dei canali

## Passaggi per assegnare un canale a una visualizzazione {#assign-channel-to-display}

Segui la procedura seguente per assegnare un canale a una visualizzazione:

1. Passa a Provider servizi Screens e seleziona **Display** dal pannello di navigazione a sinistra.

1. Fai clic su **Assegna canale** alla visualizzazione.

   ![immagine](/help/screens-cloud/assets/display/assignchannel-1.png)

1. Compilare i campi seguenti dalla finestra di dialogo **Assegna un canale**.

   ![immagine](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. Seleziona il nome del canale dal menu a discesa.
   1. Scegli la priorità.

      >[!NOTE]
      >La priorità viene usata per ordinare le assegnazioni nel caso in cui più utenti corrispondano ai criteri di riproduzione. Quella con il valore più alto avrà sempre la precedenza su quella con i valori più bassi. Ad esempio, se ci sono due canali A e B, A ha una priorità di 1 e B ha una priorità di 2, viene quindi visualizzato il canale B, che ha una priorità maggiore di A.
   1. Seleziona la data di inizio e la data di fine da **Activation**.

1. Fai clic su **+ Aggiungi ricorrenza** per aggiungere una pianificazione delle ricorrenze per il tuo canale.

   ![immagine](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >Puoi aggiungere più pianificazioni ricorrenti al tuo canale. La pianificazione della ricorrenza introduce DayParting, che consente di impostare una pianificazione globale con più canali in esecuzione in momenti specifici della giornata, e di riutilizzare tale impostazione per tutti i display contemporaneamente.

   Puoi impostare le seguenti opzioni:

   * **Nome**: Titolo della pianificazione della ricorrenza.
   * **Ripeti**: Scegli se la pianificazione viene eseguita su Giornaliero, Settimanale, Mensile o Annuale.
   * **Avvia**: Ora di inizio della pianificazione.
   * **Fine**: L&#39;orario finale della tua pianificazione. Puoi impostarlo per ora o durata.
   * **Ora**: La pianificazione termina a un&#39;ora specificata.
   * **Durata**: La pianificazione viene eseguita per una particolare durata in ore o minuti.

1. Fai clic su **Crea** e ora vedrai l&#39;assegnazione di un canale per quella visualizzazione, come mostrato nella figura seguente.

   ![immagine](/help/screens-cloud/assets/display/assignchannel-3.png)


## Novità {#whats-next}

Ora, dopo aver assegnato il canale a una visualizzazione, dovresti continuare a usare Screens come percorso di Cloud Service esaminando il documento **Installazione e configurazione di Screens Player per AEM come Cloud Service**.
