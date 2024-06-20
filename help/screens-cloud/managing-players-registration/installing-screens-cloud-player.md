---
title: Installazione e configurazione dei lettori in Schermi as a Cloud Service
description: Questa pagina descrive come installare e configurare i lettori in Screens as a Cloud Service.
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# Installazione e configurazione dei lettori in Schermi as a Cloud Service {#installing-players-screens-cloud}

Questa sezione descrive come installare lettori AEM Screens registrati in istanze AEM on-premise. Inoltre, devi eseguire un ripristino di fabbrica del lettore esistente e quindi registrare il nuovo lettore su AEM Screens as a Cloud Service.

## Obiettivo {#objective}

Questo documento spiega come configurare il lettore prima di registrarlo. Dopo aver letto, dovresti essere in grado di capire quanto segue:

* dove installare i lettori da
* come aggiornare il lettore alla modalità Cloud

## Passaggi per impostare il lettore sulla modalità cloud {#cloud-mode-setup}

Dopo aver scaricato l’ultimo lettore da [Download di AEM Screens Player](https://download.macromedia.com/screens/), ora puoi aggiornare il lettore alla modalità Cloud.

Per aggiornare il lettore, segui i passaggi seguenti:

1. Apri AEM Screens Player.

   >[!NOTE]
   >Puoi scegliere di eseguire il test con dispositivi hardware dedicati o con un’estensione web sul tuo lettore.

1. Fai clic su **Configurazione** e fai clic su **In fabbrica** pulsante sotto **Reimposta** opzione.

   ![immagine](/help/screens-cloud/assets/player/installplayer-2.png)

1. Clic **Conferma** per ripristinare il lettore.

1. Di nuovo dal **Configurazione** e fai clic su **Passa a modalità cloud** pulsante sotto **Attiva/disattiva modalità di esecuzione** opzione.

   ![immagine](/help/screens-cloud/assets/player/installplayer-1.png)

1. Clic **Conferma** che viene richiesto quando si passa alla modalità cloud, annulla la registrazione del lettore.

## Monitoraggio della riproduzione di base {#playback-monitoring}

Il lettore riporta diverse metriche di riproduzione per ciascuno di essi `ping` il valore predefinito è 30 secondi. In base a queste metriche, Adobe è in grado di rilevare vari casi limite, come esperienza bloccata, schermata vuota e problemi di pianificazione. Questo rilevamento ci consente di comprendere e risolvere i problemi del dispositivo e quindi di accelerare un&#39;indagine e le misure correttive con te.

Il monitoraggio della riproduzione di base in un lettore AEM Screens consente di:

* Monitora in remoto se un lettore riproduce correttamente il contenuto.

* Migliora la reattività a schermate vuote o esperienze bloccate nel campo.

* Riduce il rischio di mostrare all’utente un’esperienza non funzionante.

### Informazioni sulle proprietà {#understand-properties}

Le seguenti proprietà sono incluse in ogni `ping`:

| Proprietà | Descrizione |
|---|---|
| id {string} | l’identificatore del lettore |
| activeChannel {string} | percorso del canale attualmente in riproduzione o null se non è pianificato nulla |
| activeElements {string} | stringa separata da virgole, attualmente elementi visibili in tutti i canali della sequenza di riproduzione (più se era presente un layout multizona) |
| isDefaultContent {boolean} | true se il canale di riproduzione è considerato un canale predefinito o di fallback (ovvero, ha priorità 1 e nessuna pianificazione) |
| hasContentChanged {boolean} | true se il contenuto è cambiato negli ultimi 5 minuti, false in caso contrario |
| lastContentChange {string} | timestamp dell’ultima modifica al contenuto |

>[!NOTE]
>Facoltativamente, puoi abilitare una proprietà più avanzata dalle preferenze del lettore (Abilita monitoraggio della riproduzione):
>|Proprietà|Descrizione|
>|—|—|
>|isContentRendering {boolean}|true se la GPU può confermare che sta riproducendo il contenuto effettivo (in base all&#39;analisi dei pixel)|

### Limitazioni {#limitations}

Di seguito sono elencate alcune limitazioni al monitoraggio di base della riproduzione:

* Il lettore segnala il proprio stato di riproduzione al server, pertanto richiede una connessione attiva.

* Il `isContentRendering` che controlla che la GPU richieda un uso eccessivo di risorse per essere abilitata per impostazione predefinita e che richieda il consenso esplicito dalle preferenze del lettore. Si consiglia di non utilizzarlo con i video in produzione.

* Questa funzione è supportata solo per i canali di sequenza e non copre ancora il caso di utilizzo dei canali interattivi (SPA).

* Le metriche non sono ancora completamente esposte ai clienti; Adobe sta lavorando per abilitare a breve un meccanismo di reporting e avviso simile a quello delle dashboard.

## Passaggio successivo {#whats-next}

Ora che hai installato e configurato il lettore in modalità Cloud, continua il percorso Screens as a Cloud Service. Consulta [Registrazione dei lettori in Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) da Screens Services Provider.
