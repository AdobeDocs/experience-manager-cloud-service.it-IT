---
title: Installazione e configurazione dei lettori in Screens as a Cloud Service
description: Questa pagina descrive come installare e configurare i lettori in Screens as a Cloud Service.
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: af7793ca7ad3d11bfff980a4d00f537fd0871755
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# Installazione e configurazione dei lettori in Screens as a Cloud Service {#installing-players-screens-cloud}

Questa sezione descrive come installare lettori AEM Screens registrati in istanze AEM on-premise. Inoltre, devi eseguire un ripristino di fabbrica del lettore esistente e quindi registrare il nuovo lettore rispetto all’as a Cloud Service AEM Screens.

## Obiettivo {#objective}

Questo documento spiega come configurare il lettore prima di registrarlo. Dopo aver letto, dovresti essere in grado di capire quanto segue:

* dove installare i lettori da
* come aggiornare il lettore alla modalità Cloud

## Passaggi per impostare il lettore sulla modalità cloud {#cloud-mode-setup}

Dopo aver scaricato l&#39;ultimo lettore da [Download del lettore AEM Screens](https://download.macromedia.com/screens/), puoi aggiornare il lettore in modalità cloud.

Per aggiornare il lettore, segui i passaggi seguenti:

1. Apri AEM Screens Player.

   >[!NOTE]
   >Puoi scegliere di eseguire il test con dispositivi hardware dedicati o con un’estensione web sul tuo lettore.

1. Fare clic sulla scheda **Configurazione** e fare clic sul pulsante **In fabbrica** sotto l&#39;opzione **Ripristina**.

   ![immagine](/help/screens-cloud/assets/player/installplayer-2.png)

1. Fai clic su **Conferma** per ripristinare il lettore.

1. Di nuovo dalla scheda **Configurazione** e fai clic sul pulsante **Passa a modalità cloud** in **Attiva/disattiva modalità di esecuzione**.

   ![immagine](/help/screens-cloud/assets/player/installplayer-1.png)

1. Fai clic su **Conferma** per richiedere conferma quando si passa alla modalità cloud e si annulla la registrazione del lettore.

## Monitoraggio della riproduzione di base {#playback-monitoring}

Il lettore riporta diverse metriche di riproduzione per ogni `ping` per impostazione predefinita, 30 secondi. In base a queste metriche, Adobe è in grado di rilevare vari casi limite, come esperienza bloccata, schermata vuota e problemi di pianificazione. Questo rilevamento ci consente di comprendere e risolvere i problemi del dispositivo e quindi di accelerare un&#39;indagine e le misure correttive con te.

Il monitoraggio della riproduzione di base in un lettore AEM Screens consente di:

* Monitora in remoto se un lettore riproduce correttamente il contenuto.

* Migliora la reattività a schermate vuote o esperienze bloccate nel campo.

* Riduce il rischio di mostrare all’utente un’esperienza non funzionante.

### Informazioni sulle proprietà {#understand-properties}

In ogni `ping` sono incluse le seguenti proprietà:

| Proprietà | Descrizione |
|---|---|
| id {string} | l’identificatore del lettore |
| activeChannel {string} | percorso del canale attualmente in riproduzione o null se non è pianificato nulla |
| activeElements {string} | stringa separata da virgole, attualmente elementi visibili in tutti i canali della sequenza di riproduzione (più se era presente un layout multizona) |
| isDefaultContent {boolean} | true se il canale di riproduzione è considerato un canale predefinito o di fallback (ovvero, ha priorità 1 e nessuna pianificazione) |
| hasContentChanged {boolean} | true se il contenuto è cambiato negli ultimi 5 minuti, false in caso contrario |
| lastContentChange {string} | timestamp dell’ultima modifica al contenuto |

>[!NOTE]
>
>Facoltativamente, puoi abilitare una proprietà più avanzata dalle preferenze del lettore (Abilita monitoraggio della riproduzione):
>
>| Proprietà | Descrizione |
>|---|---|
>| isContentRendering {boolean} | true se la GPU può confermare che sta riproducendo il contenuto effettivo (in base all&#39;analisi dei pixel) |

### Limitazioni {#limitations}

Di seguito sono elencate alcune limitazioni al monitoraggio di base della riproduzione:

* Il lettore segnala il proprio stato di riproduzione al server, pertanto richiede una connessione attiva.

* La proprietà `isContentRendering` che controlla che la GPU richieda un uso eccessivo di risorse per essere abilitata per impostazione predefinita e richiede il consenso esplicito dalle preferenze del lettore. Si consiglia di non utilizzarlo con i video in produzione.

* Questa funzione è supportata solo per i canali di sequenza e non copre ancora il caso di utilizzo dei canali interattivi (SPA).

* Le metriche non sono ancora completamente esposte ai clienti; Adobe sta lavorando per abilitare a breve un meccanismo di reporting e avviso simile a quello delle dashboard.

## Passaggio successivo {#whats-next}

Ora che hai installato e configurato il lettore in modalità Cloud, continua con l’percorso Screens as a Cloud Service. Consulta [Registrazione dei lettori in Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) dal provider di servizi Screens.
