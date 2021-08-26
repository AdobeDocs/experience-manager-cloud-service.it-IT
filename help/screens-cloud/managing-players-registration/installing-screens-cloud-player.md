---
title: Installazione e configurazione dei lettori in Screens come Cloud Service
description: Questa pagina descrive come installare e configurare i lettori in Screens come Cloud Service.
source-git-commit: 1fc06f987bb40d940bbec9c37e6d58c2c1ca9266
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---


# Installazione e configurazione dei lettori in Screens come Cloud Service {#installing-players-screens-cloud}

Questa sezione descrive come installare i lettori AEM Screens registrati nelle istanze di AEM on-premise. Inoltre, è necessario eseguire una reimpostazione di fabbrica del lettore esistente e quindi registrare il nuovo lettore su AEM Screens come Cloud Service.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come impostare il lettore prima di registrare i giocatori. Dopo aver letto dovrebbe essere in grado di capire:

* da dove installare i lettori
* come aggiornare il lettore alla modalità Cloud

## Passaggi per impostare il lettore in modalità Cloud {#cloud-mode-setup}

Dopo aver scaricato l&#39;ultimo lettore da [AEM Screens Player Downloads](https://download.macromedia.com/screens/), ora sei pronto per aggiornare il lettore alla modalità Cloud.

Per aggiornare il lettore, effettua le seguenti operazioni:

1. Apri AEM Screens player.

   >[!NOTE]
   >Puoi scegliere di testare con dispositivi hardware dedicati o con un&#39;estensione web sul tuo lettore.

1. Fai clic sulla scheda **Configurazione** e fai clic sul pulsante **To Factory** sotto l&#39;opzione **Reset**.

   ![immagine](/help/screens-cloud/assets/player/installplayer-2.png)

1. Fai clic su **Conferma** per ripristinare il lettore.

1. Sempre dalla scheda **Configurazione** e fai clic sul pulsante **Cambia in modalità cloud** sotto l&#39;opzione **Attiva modalità di esecuzione**.

   ![immagine](/help/screens-cloud/assets/player/installplayer-1.png)

1. Fai clic su **Conferma** per annullare la registrazione del lettore quando si passa alla modalità cloud.

## Monitoraggio della riproduzione di base {#playback-monitoring}

Il lettore riporta varie metriche di riproduzione con ciascuna `ping` che per impostazione predefinita corrisponde a 30 secondi. In base alle metriche, puoi rilevare vari casi edge come esperienza bloccata, schermata vuota e problemi di pianificazione. Questo consente di comprendere e risolvere i problemi del dispositivo, e quindi di accelerare un&#39;indagine e le misure correttive.

Il monitoraggio della riproduzione di base in un lettore AEM Screens consente di:

* Monitorare in remoto se un lettore riproduce correttamente il contenuto

* Migliorare la reattività alle schermate vuote o alle esperienze interrotte nel campo

* Riduci il rischio di mostrare all’utente finale un’esperienza non funzionante

### Informazioni sulle proprietà {#understand-properties}

Le seguenti proprietà sono incluse in ogni `ping`:

| Proprietà | Descrizione |
|---|---|
| id {string} | identificatore del lettore |
| activeChannel {string} | in corso la riproduzione del percorso del canale, o null se non è pianificato nulla |
| activeElements {string} | stringa separata da virgole, elementi attualmente visibili in tutti i canali di riproduzione a sequenza (multipli in caso di layout a più zone) |
| isDefaultContent {boolean} | true se il canale di riproduzione è considerato un canale predefinito o di fallback (ovvero, ha priorità 1 e nessuna pianificazione) |
| hasContentChanged {boolean} | true se il contenuto è cambiato negli ultimi 5 minuti, false in caso contrario |
| lastContentChange {string} | timestamp dell’ultima modifica del contenuto |

>[!NOTE]
>Facoltativamente, è possibile abilitare una proprietà più avanzata dalle preferenze del lettore (Abilita monitoraggio riproduzione), ovvero:
>|Proprietà|Descrizione|
>|—|—|
>|isContentRendering {boolean}|true se la GPU può confermare che sta riproducendo il contenuto effettivo (in base all&#39;analisi dei pixel)|

### Limitazioni  {#limitations}

Di seguito sono elencate alcune limitazioni al monitoraggio della riproduzione di base:

* Poiché il lettore riporta il proprio stato di riproduzione al server, è necessaria una connessione attiva.

* La proprietà `isContentRendering` che controlla che la GPU sia attualmente ad uso intensivo di risorse, deve essere abilitata per impostazione predefinita e richiede un esplicito consenso alle preferenze del lettore. Si consiglia di non utilizzarlo in combinazione con i video.

* Supportato per i canali di sequenza.

## Novità {#whats-next}

Ora, dopo aver installato e configurato il lettore in modalità Cloud, dovresti continuare a usare Screens come percorso di Cloud Service esaminando il documento [Registrazione dei lettori in Screens come Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) da Screens Services Provider.