---
title: Centro notifiche
description: Sfruttare il Centro di notifica per intervenire in modo comodo su incidenti e altre informazioni importanti
hidefromtoc: true
source-git-commit: 55ecd685afa28226974f3415b550bd2e8d05e2e6
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Centro notifiche {#notification-center}

>[!NOTE]
>Questa funzione non è stata rilasciata.

Una volta configurata, AEM come Cloud Service invia notifiche su informazioni importanti per le quali i clienti devono intervenire. Esempi di notifiche includono una coda bloccata o un set di credenziali in scadenza. L’intero set di tipi di notifica può essere visualizzato nel [tabella seguente](#current-notification-types)e si espanderà nel tempo. Le notifiche vengono ricevute sia via e-mail che come nuova voce sotto il widget di notifica, a cui si accede facendo clic sull&#39;icona della campana nell&#39;angolo in alto a destra in tutto il Adobe Experience Cloud. È possibile configurare le impostazioni di notifica.

Quando viene ricevuta una notifica, è possibile fare clic per aprire AEM Centro notifiche di as a Cloud Service con una finestra a comparsa che mostra il contesto aggiuntivo che illustra l&#39;azione consigliata da un cliente di intraprendere.

Oltre a visualizzare informazioni sulla notifica appena selezionata, il Centro notifiche funge da hub dove è possibile visualizzare e gestire il set di notifiche correnti e precedenti. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Esistono due categorie di notifiche di alto livello:

1. Incidenti : si è verificato un evento, che in genere richiede una risoluzione rapida. Ad esempio, la risoluzione di una coda bloccata
1. Proattivo : l’Adobe include una raccomandazione per un’azione che un cliente dovrebbe intraprendere nel prossimo futuro. Ad esempio, per interrompere il riferimento a un’interfaccia utente obsoleta.

Consulta la sezione [tabella seguente](#current-notification-types) per le notifiche attualmente supportate.

Dalla schermata Centro notifiche è possibile selezionare un programma e un ambiente specifici, che hanno l&#39;effetto di filtrare tale ambito.

## Configurazione {#configuration}

Puoi seguire i passaggi seguenti per configurare la ricezione delle notifiche:

1. Crea i seguenti profili di prodotto, come descritto [nel presente articolo](/help/journey-onboarding/notification-profiles.md), assegnazione degli ID Adobe appropriati dalla tua organizzazione a tali profili.
1. Determina le impostazioni di configurazione delle notifiche. [In questa pagina](https://experience.adobe.com/preferences/notification-section), assicurati che l’Experience Manager di abbonamento sia abilitato e che l’ **Altro** casella di controllo selezionata. Inoltre, si consiglia di impostare la sezione E-mail su **Notifiche istantanee** in modo da ricevere le notifiche immediatamente dopo un incidente.

>[!NOTE]
>Gli abbonamenti funzionano a livello di organizzazione e gli abbonati ricevono notifiche per tutti i programmi e gli ambienti all’interno di tali programmi.

## Flusso utente dettagliato {#detailed-user-flow}

Facendo clic sull&#39;e-mail si accede al Centro notifiche, con una finestra a comparsa che mostra il contesto per la notifica su cui hai fatto clic e, in alcuni casi, collegamenti a informazioni aggiuntive che descrivono come intraprendere azioni correttive.

![Dettagli dell&#39;incidente](/help/operations/assets/incident-details.png)

Fai clic su **Ulteriori informazioni** questo collegamento indirizza l’utente a questo articolo, in cui è possibile fare riferimento alla notifica nella tabella seguente, che fornisce indicazioni sull’azione da intraprendere.

Nel Centro notifiche è disponibile un elenco di altre notifiche recenti. È consigliabile utilizzare l’elenco Azioni per confermare una notifica al fine di segnalare all’Adobe che l’organizzazione è a conoscenza dell’attività e di risolvere in seguito la notifica quando è stata eseguita un’azione correttiva.

![Elenco notifiche](/help/operations/assets/notification-list.png)

Nella maggior parte dei casi, la notifica dovrebbe fornire tutto il contesto necessario per risolvere il problema. Tuttavia, in caso di domande ad Adobe sull’Assistenza, puoi fare clic sul pulsante **Contatta il supporto** nel popup di notifica. Viene visualizzato un modulo dal quale è possibile descrivere la domanda e inviarla per creare il ticket di assistenza, che includerà anche un riferimento alla notifica specifica in modo che un tecnico del supporto Adobe abbia il contesto pertinente.

![Contatta il supporto 1](/help/operations/assets/contact-support1.png)

![Contatta il supporto 2](/help/operations/assets/contact-support2.png)

Come tutti i ticket di supporto, verrà visualizzato nel [Scheda Casi di assistenza Adobe Admin Console](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html), in cui puoi tenere traccia di e aggiungere altri commenti.

![Supporto Admin Console](/help/operations/assets/admin-console-support.png)

## Tipi di notifica correnti {#current-notification-types}

Nella tabella seguente sono elencati i tipi di notifica attualmente supportati

| Tipo di notifica | Profilo prodotto correlato | Azione correttiva |
|---|---|---|
| Coda di replica bloccata | Incidente | Sblocca la coda seguendo le istruzioni contenute in [Documentazione di replica](/help/operations/replication.md#troubleshooting) |
| Scadenza del certificato S2S | Proattivo | Scopri come aggiornare una credenziale nel [Generazione dei token di accesso per la documentazione delle API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
