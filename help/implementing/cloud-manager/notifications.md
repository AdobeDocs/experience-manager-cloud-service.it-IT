---
title: Notifiche
description: Scopri come ricevere informazioni sulle distribuzioni delle pipeline utilizzando il sistema di notifica Adobe Experience Cloud.
exl-id: c1c740b0-c873-45a8-9518-a856db2be75b
source-git-commit: 451b5a089645004c58c2674fd1fb13afbe1201cf
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 1%

---


# Notifiche {#notifications}

Scopri in che modo Cloud Manager ti notifica di eventi importanti.

## Notifiche in Cloud Manager {#cloud-manager-notifications}

[!UICONTROL Cloud Manager] invia notifiche quando una pipeline di produzione viene avviata e completata (con successo o senza successo) all’inizio di una distribuzione di produzione.

Queste notifiche vengono inviate tramite [!UICONTROL Experience Cloud] sistema di notifica agli utenti nel **Proprietario business**, **Responsabile del programma** e **Gestione distribuzione** ruoli.

Le notifiche vengono visualizzate in una barra laterale in [!UICONTROL Cloud Manager] e in tutto l&#39;Adobe [!UICONTROL Experience Cloud]. L’icona della campana nell’intestazione viene contrassegnata quando si dispone di nuove notifiche.

![Icona Notifiche](assets/notifications-bell-badged.png)

Fai clic sull’icona della campana per aprire la barra laterale e visualizzare le notifiche. La **Notifiche** nella barra laterale sono elencate le notifiche più recenti, ad esempio le conferme di distribuzione. Le notifiche riguardano i tuoi ambienti.

![Barra laterale Notifiche](assets/notifications-activities.png)

La **Annunci** La scheda include Adobi di annunci di prodotti. Gli annunci riguardano il prodotto.

![Barra laterale Notifiche](assets/notificaitons-announcements.png)

Fai clic su una notifica o un annuncio per visualizzarne i dettagli. Le notifiche collegate ad attività come le distribuzioni di pipeline ti portano ai dettagli di quell’attività, ad esempio la finestra di esecuzione della pipeline.

Fai clic sul pulsante **Visualizza tutto** nella parte inferiore del pannello per visualizzare tutti gli annunci presenti nella casella in entrata.

Fai clic sul pulsante **Contrassegna tutto come letto** nella parte inferiore del pannello per contrassegnare tutte le notifiche non lette come lette e cancellare il contrassegno dell&#39;icona della campana.

## Configurazione delle notifiche {#configuration}

Puoi personalizzare le modalità di ricezione delle notifiche e le notifiche ricevute.

Fai clic sull’icona dell’ingranaggio nella parte superiore della barra laterale delle notifiche.

![Icona delle impostazioni di notifica](assets/notifications-configuration.png)

Viene aperta la **Preferenze di Experience Cloud** , che consente di definire gli abbonamenti alle notifiche e le modalità di ricezione delle notifiche.

### Sottoscrizioni {#subscriptions}

Gli abbonamenti definiscono per quali prodotti ricevi le notifiche e quali notifiche.

![Abbonamenti alle notifiche](assets/notifications-subscriptions.png)

Per impostazione predefinita, riceverai tutte le notifiche per tutti i prodotti. Fai clic su **Personalizza** accanto a un prodotto per definire i tipi di notifiche ricevute per quel prodotto.

![Personalizzazione della sottoscrizione delle notifiche](assets/notifications-subscriptions-customize.png)

### Priorità {#priority}

Gli avvisi prioritari saranno contrassegnati con un **ALTO** e può essere configurato per essere ricevuto esclusivamente come avvisi. In **Priorità** è possibile definire quali categorie si qualificano come notifiche prioritarie.

![Priorità di notifica](assets/notifications-priority.png)

Utilizza l’elenco a discesa per aggiungere all’elenco delle categorie idonee come priorità. Fai clic sulla X accanto ai nomi delle categorie per rimuoverli.

### Avvisi {#alerts}

Gli avvisi vengono visualizzati nell’angolo in alto a destra della finestra per alcuni secondi. Utilizza la **Avvisi** per definire le notifiche per le quali ricevi gli avvisi.

![Avvisi di notifica](assets/notifications-alerts.png)

È possibile definire il comportamento degli avvisi.

* **Mostra avvisi per** - Definisce i tipi di notifiche che attivano gli avvisi
* **Gli avvisi dovrebbero rimanere sullo schermo fino a quando non li ignoro** - Controlla se gli avvisi devono persistere a meno che non vengano attivamente ignorati
* **Durata** - Definisce per quanto tempo l&#39;avviso deve rimanere sullo schermo se non si è scelto di rimanere sullo schermo.

### E-mail {#emails}

Le notifiche sono disponibili nell’interfaccia utente web di Adobe [!UICONTROL Experience Cloud] soluzioni. Puoi anche optare per l’invio di queste notifiche tramite e-mail nella **E-mail** sezione .

![E-mail di notifica](assets/notifications-emails.png)

Per impostazione predefinita non vengono inviate e-mail. Puoi scegliere di ricevere e-mail come:

* Istantanea
* Giornaliero
* Settimanale

Quando **Notifiche istantanee** viene selezionato , le e-mail vengono inviate immediatamente per ogni notifica. Per **Riepilogo giornaliero** e **Digest settimanale** puoi scegliere quando inviare il riassunto giornaliero e in quale giorno e quando inviare il riassunto settimanale.