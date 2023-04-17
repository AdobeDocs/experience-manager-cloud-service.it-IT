---
title: Centro notifiche
description: Sfruttare il Centro notifiche per intervenire opportunamente su problemi e altre informazioni importanti
hidefromtoc: true
source-git-commit: 55ecd685afa28226974f3415b550bd2e8d05e2e6
workflow-type: ht
source-wordcount: '638'
ht-degree: 100%

---


# Centro notifiche {#notification-center}

>[!NOTE]
>Questa funzione non è stata rilasciata.

Una volta configurato, AEM as Cloud Service invia notifiche su informazioni importanti per le quali i clienti dovrebbero intervenire. Esempi di notifiche sono, ad esempio, una coda bloccata o un set di credenziali in scadenza. L’intero set di tipi di notifica può essere visualizzato nella [tabella seguente](#current-notification-types) e si espanderà nel tempo. Le notifiche vengono ricevute sia via e-mail che come nuova voce nel widget di notifica, a cui si accede facendo clic sull’icona della campana nell’angolo in alto a destra di Adobe Experience Cloud. È possibile configurare le impostazioni di notifica.

Quando viene ricevuta una notifica, è possibile fare clic per aprire il centro notifche di AEM as a Cloud Service con una finestra a comparsa, nella quale viene mostrato un contesto aggiuntivo che spiega l’azione consigliata al cliente.

Oltre a visualizzare informazioni sulla notifica appena cliccata, il centro notifiche funge da hub dove è possibile visualizzare e gestire il set di notifiche attuali e precedenti. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Esistono due categorie di notifiche di alto livello:

1. Problemi: si è verificato un evento, che in genere richiede una risoluzione rapida. Ad esempio, la risoluzione di una coda bloccata
1. Proattiva: Adobe suggerisce un’azione che il cliente dovrebbe intraprendere nel prossimo futuro. Ad esempio, per interrompere il riferimento a un’interfaccia utente obsoleta.

Consulta la [tabella seguente](#current-notification-types) per le notifiche attualmente supportate.

Dalla schermata del centro notifiche è possibile selezionare un programma e un ambiente specifici, tramite i quali è possibile filtrare per quell’ambito.

## Configurazione {#configuration}

Puoi seguire i passaggi seguenti per configurare la ricezione delle notifiche:

1. Crea i seguenti profili di prodotto assegnando gli Adobe ID appropriati dell’organizzazione, come descritto [nel presente articolo](/help/journey-onboarding/notification-profiles.md).
1. Determina le impostazioni di configurazione delle notifiche. [In questa pagina](https://experience.adobe.com/preferences/notification-section), assicurati che l’abbonamento a Experience Manager sia abilitato e che la casella di controllo **Altri** sia selezionata. Inoltre, si consiglia di impostare la sezione e-mail su **Notifiche istantanee** in modo da ricevere le notifiche immediatamente dopo il verificarsi di un problema.

>[!NOTE]
>Gli abbonamenti funzionano a livello di organizzazione e gli abbonati ricevono notifiche per tutti i programmi e gli ambienti all’interno di tali programmi.

## Flusso utente dettagliato {#detailed-user-flow}

Facendo clic sull’e-mail si accede al centro notifiche, con una finestra a comparsa che mostra il contesto per la notifica su cui hai fatto clic e, in alcuni casi, collegamenti a informazioni aggiuntive che descrivono come intraprendere un’azione correttiva.

![Dettagli problema](/help/operations/assets/incident-details.png)

Cliccando sul collegamento a **Ulteriori informazioni** l’utente potrà consultare questo articolo, in cui è possibile fare riferimento alla notifica nella tabella seguente, la quale fornisce indicazioni sull’azione da intraprendere.

Nel centro notifiche è disponibile un elenco di altre notifiche recenti. È consigliabile utilizzare l’elenco Azioni per confermare una notifica al fine di segnalare ad Adobe che l’organizzazione è a conoscenza dell’attività e per risolvere in seguito la notifica dopo aver intrapreso un’azione correttiva.

![Elenco notifiche](/help/operations/assets/notification-list.png)

Nella maggior parte dei casi, la notifica dovrebbe fornire tutto il contesto necessario per risolvere il problema. Tuttavia, se hai bisogno di porre domande al supporto Adobe, puoi fare clic sul collegamento **Contatta supporto** nel popup di notifica. Viene visualizzato un modulo dal quale è possibile descrivere la domanda e inviarla per creare il ticket di supporto, che includerà anche un riferimento alla notifica specifica in modo che un tecnico del supporto Adobe abbia il contesto pertinente.

![Contatta supporto 1](/help/operations/assets/contact-support1.png)

![Contatta supporto 2](/help/operations/assets/contact-support2.png)

Come tutti i ticket di supporto, questo verrà visualizzato nella [scheda Casi di supporto Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/support-for-enterprise.html), in cui puoi tenerne traccia e aggiungere ulteriori commenti.

![Supporto Admin Console](/help/operations/assets/admin-console-support.png)

## Tipi di notifica correnti {#current-notification-types}

Nella tabella seguente sono elencati i tipi di notifica attualmente supportati

| Tipo di notifica | Profilo prodotto correlato | Azione correttiva |
|---|---|---|
| Coda di replica bloccata | Problema | Sblocca la coda seguendo le istruzioni contenute nella [Documentazione di replica](/help/operations/replication.md#troubleshooting) |
| Certificato S2S in scadenza | Proattiva | Scopri come aggiornare una credenziale nella [Documentazione sulla generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
