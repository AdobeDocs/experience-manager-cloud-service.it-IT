---
title: Centro notifiche
description: Utilizzare il Centro notifiche per intervenire in modo comodo sugli incidenti e su altre informazioni importanti
hidefromtoc: true
source-git-commit: a5977c667d831c47d41cd86b68e9196fbe726899
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Centro notifiche {#notification-center}

>[!NOTE]
>Questa funzione non è stata rilasciata.

Una volta configurata, AEM come Cloud Service invia notifiche su informazioni importanti per le quali i clienti devono intervenire. Esempi di notifiche includono una coda bloccata o un set di credenziali in scadenza. L’intero set di tipi di notifica può essere visualizzato nel [tabella seguente](#current-notification-types)e si espanderà nel tempo. Le notifiche vengono ricevute tramite e-mail e come nuova voce sotto il widget di notifica, a cui si accede facendo clic sull’icona a forma di campana nell’angolo in alto a destra in tutto Adobe Experience Cloud. È possibile configurare le impostazioni di notifica.

Quando viene ricevuta una notifica, è possibile fare clic su di essa per aprire il Centro notifiche dell’as a Cloud Service AEM con una finestra a comparsa contenente un contesto aggiuntivo che spiega l’azione consigliata da parte di un cliente.

Oltre a visualizzare informazioni sulla notifica con clic, il Centro notifiche funge da hub in cui è possibile visualizzare e gestire il set di notifiche correnti e precedenti. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Esistono due categorie di notifiche di alto livello:

1. Incidenti: si è verificato un evento che in genere richiede una risoluzione immediata. Ad esempio, la risoluzione di una coda bloccata
1. Proattivo: Adobe consiglia un’azione che il cliente deve intraprendere nel prossimo futuro. Ad esempio, per interrompere il riferimento a un’interfaccia utente obsoleta.

Consulta la [tabella seguente](#current-notification-types) per le notifiche attualmente supportate.

Dalla schermata Centro notifiche, puoi selezionare un programma e un ambiente specifici, che ha l’effetto di filtrare per tale ambito.

## Configurazione {#configuration}

Per configurare la ricezione delle notifiche, segui i passaggi indicati di seguito:

1. Crea i seguenti profili di prodotto, come descritto [in questo articolo](/help/journey-onboarding/user-groups.md), assegnando gli ID Adobe appropriati dalla tua organizzazione a tali profili.
1. Determina le impostazioni di configurazione delle notifiche. [In questa pagina](https://experience.adobe.com/preferences/notification-section), accertarsi che l&#39;abbonamento Experience Manager sia abilitato e che **Altro** è selezionata. Inoltre, si consiglia di impostare la sezione E-mail su **Notifiche istantanee** in modo da ricevere notifiche immediatamente dopo il verificarsi di un incidente.

>[!NOTE]
>Gli abbonamenti funzionano a livello di organizzazione, pertanto gli abbonati riceveranno notifiche per tutti i programmi e gli ambienti all’interno di tali programmi.

## Flusso utente dettagliato {#detailed-user-flow}

Facendo clic sull’e-mail si accede al Centro notifiche, con un pop-up che mostra il contesto della notifica su cui si è fatto clic e, in alcuni casi, collegamenti a informazioni aggiuntive che descrivono come intraprendere azioni correttive.

![Dettagli dell’incidente](/help/operations/assets/incident-details.png)

Facendo clic su **Ulteriori informazioni** link porta l’utente a questo articolo, dove nella tabella seguente è possibile fare riferimento alla notifica, che fornisce indicazioni sull’azione da intraprendere.

Nel Centro notifiche puoi visualizzare un elenco di altre notifiche recenti. Si consiglia di utilizzare l&#39;elenco Azioni per confermare una notifica per segnalare all&#39;Adobe che l&#39;organizzazione è a conoscenza dell&#39;operazione e per risolvere la notifica in seguito quando è stata intrapresa un&#39;azione correttiva.

![Elenco notifiche](/help/operations/assets/notification-list.png)

Nella maggior parte dei casi, la notifica deve fornire tutto il contesto necessario per risolvere il problema. Tuttavia, in caso di domande come ad Adobe Supporto, puoi fare clic sul pulsante **Contatta il supporto** nel popup di notifica. Verrà visualizzato un modulo in cui è possibile descrivere la domanda e inviarla per creare il ticket di supporto, che includerà anche un riferimento alla notifica specifica in modo che un Adobe di tecnici del supporto abbia il contesto pertinente.

![Contatta l’assistenza 1](/help/operations/assets/contact-support1.png)

![Contatta l’assistenza 2](/help/operations/assets/contact-support2.png)

Come tutti i ticket di supporto, verrà visualizzato nel [Scheda Casi di supporto di Adobe Admin Console](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html), dove è possibile tracciarlo e aggiungere ulteriori commenti.

![Supporto Admin Console](/help/operations/assets/admin-console-support.png)

## Tipi di notifica correnti {#current-notification-types}

La tabella seguente elenca i tipi di notifica attualmente supportati

| Tipo di notifica | Profilo prodotto correlato | Azione correttiva |
|---|---|---|
| Coda di replica bloccata | Caso | Sblocca la coda seguendo le istruzioni in [Documentazione sulla replica](/help/operations/replication.md#troubleshooting) |
| Certificato S2S in scadenza | Proattivo | Scopri come aggiornare le credenziali in [Documentazione sulla generazione di token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
