---
title: Installazione e configurazione dei lettori in Screens as a Cloud Service
description: Questa pagina descrive come installare e configurare i lettori in Screens as a Cloud Service.
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: 3367977496d3edad0f6f1e27e98eac95c791e870
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# Installing and Configuring Players in Screens as a Cloud Service {#installing-players-screens-cloud}

This section describes how to install AEM Screens players that are registered to on-premise AEM instances. Additionally, you must do a factory reset of the existing player and then register the new player against AEM Screens as a Cloud Service.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come impostare il lettore prima di registrare i giocatori. Dopo aver letto dovrebbe essere in grado di capire:

* da dove installare i lettori
* come aggiornare il lettore alla modalità Cloud

## Passaggi per impostare il lettore in modalità Cloud {#cloud-mode-setup}

Dopo aver scaricato l&#39;ultimo lettore da [Download di AEM Screens Player](https://download.macromedia.com/screens/),ora puoi aggiornare il lettore in modalità Cloud.

Per aggiornare il lettore, effettua le seguenti operazioni:

1. Apri AEM Screens player.

   >[!NOTE]
   >Puoi scegliere di testare con dispositivi hardware dedicati o con un&#39;estensione web sul tuo lettore.

1. Fai clic sul pulsante **Configurazione** e fai clic su **A fabbrica** pulsante sotto **Reimposta** opzione .

   ![immagine](/help/screens-cloud/assets/player/installplayer-2.png)

1. Fai clic su **Conferma** per ripristinare il lettore.

1. Di nuovo dal **Configurazione** e fai clic su **Cambia in modalità cloud** pulsante sotto **Attiva/disattiva modalità di esecuzione** opzione .

   ![immagine](/help/screens-cloud/assets/player/installplayer-1.png)

1. Fai clic su **Conferma** quando si passa alla modalità cloud, il lettore viene cancellato dalla registrazione.

## Basic Playback Monitoring {#playback-monitoring}

Il lettore riporta varie metriche di riproduzione con ciascuna `ping` il valore predefinito è 30 secondi. Based on these metrics, we can detect various edge cases such as stuck experience, blank screen, and scheduling issues. This lets us understand and troubleshoot issues on the device, and thus expedites an investigation and corrective measures with you.

Il monitoraggio della riproduzione di base in un lettore AEM Screens consente di:

* Monitoraggio remoto, se un lettore riproduce correttamente il contenuto.

* Migliorare la reattività alle schermate vuote o alle esperienze interrotte nel campo .

* Riduce il rischio di mostrare all’utente finale un’esperienza non funzionante.

### Informazioni sulle proprietà {#understand-properties}

Le seguenti proprietà sono incluse in ogni `ping`:

| Proprietà | Descrizione |
|---|---|
| id {string} | identificatore del lettore |
| activeChannel {string} | in corso la riproduzione del percorso del canale, o null se non è pianificato nulla |
| activeElements {string} | stringa separata da virgole, elementi attualmente visibili in tutti i canali di riproduzione a sequenza (multipli in caso di layout a più zone) |
| isDefaultContent {boolean} | true se il canale di riproduzione è considerato un canale predefinito o di fallback (ovvero, ha priorità 1 e nessuna pianificazione) |
| hasContentChanged {boolean} | true se il contenuto è cambiato negli ultimi 5 minuti, false in caso contrario |
| lastContentChange {string} | timestamp of the last content change |

>[!NOTE]
>Facoltativamente, è possibile abilitare una proprietà più avanzata dalle preferenze del lettore (Abilita monitoraggio riproduzione), ovvero:
>|Proprietà|Descrizione|
>|---|---|
>|isContentRendering {boolean}|true se la GPU può confermare che sta riproducendo il contenuto effettivo (in base all&#39;analisi dei pixel)|

### Limitazioni  {#limitations}

Di seguito sono elencate alcune limitazioni al monitoraggio della riproduzione di base:

* Il lettore segnala il proprio stato di riproduzione al server, quindi richiede una connessione attiva.

* La `isContentRendering` che controlla che la GPU sia attualmente troppo intensa per essere abilitata per impostazione predefinita e richiede l&#39;esplicito consenso dalle preferenze del lettore. Si consiglia di non utilizzarlo insieme ai video in produzione.

* Questa funzione è supportata solo per i canali di sequenza e non copre ancora il caso d’uso dei canali interattivi (SPA).

* Le metriche non sono ancora completamente esposte ai nostri clienti, stiamo lavorando sodo per abilitare un meccanismo di reporting e avvisi simile a dashboard in un futuro prossimo.

## Novità {#whats-next}

Ora, dopo aver installato e configurato il lettore in modalità Cloud, dovresti continuare il tuo percorso as a Cloud Service Screens esaminando il documento, [Registrazione dei lettori in Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) da Screens Services Provider.
