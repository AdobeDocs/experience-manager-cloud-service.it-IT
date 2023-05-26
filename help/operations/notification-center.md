---
title: Centro notifiche
description: Sfruttare il Centro notifiche per intervenire opportunamente su problemi e altre informazioni importanti
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: 3aa753fb5cc5130ced7e9baafde63e8825394dce
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 95%

---

# Centro notifiche {#notification-center}

>[!NOTE]
>Questa funzione non è stata rilasciata.

AEM as a Cloud Service invia notifiche quando si verificano incidenti critici che richiedono un’azione immediata, nonché consigli proattivi per le ottimizzazioni. Gli esempi includono una coda bloccata o un set di credenziali in scadenza; l’insieme completo dei tipi di notifica può essere visualizzato nella [tabella seguente](#supported-notification-types), che verrà ampliata nel tempo.

Queste notifiche possono essere configurate per essere ricevute sia via e-mail che sotto il widget di notifica, a cui si accede facendo clic sull’icona della campana nell’angolo in alto a destra in tutto Adobe Experience Cloud.

Quando viene ricevuta una notifica, è possibile fare clic per aprire il centro notifche di AEM as a Cloud Service con una finestra a comparsa, nella quale viene mostrato un contesto aggiuntivo che spiega al cliente l’azione da intraprendere.

Oltre a visualizzare informazioni sulla notifica appena cliccata, il centro notifiche funge da hub dove è possibile visualizzare e gestire il set di notifiche attuali e precedenti. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Nel centro notifiche sono visualizzate due categorie di notifiche di alto livello:

1. Problemi operativi: si è verificato un evento, che in genere richiede una risoluzione rapida. Ad esempio, la risoluzione di una coda bloccata.
1. Consigli proattivi: Adobe suggerisce un’azione che il cliente dovrebbe intraprendere nel prossimo futuro. Ad esempio, per interrompere il riferimento a un’interfaccia utente obsoleta.

Consulta la [tabella seguente](#supported-notification-types) per le notifiche attualmente supportate.

Dalla schermata del centro notifiche è possibile selezionare un programma e un ambiente specifici, tramite i quali è possibile filtrare per quell’ambito.

## Configurazione {#configuration}

Segui i passaggi più avanti per configurare la ricezione delle notifiche:

1. Crea i seguenti profili di prodotto, come descritto [in questo articolo](/help/journey-onboarding/notification-profiles.md), assegnando loro anche gli Adobe ID appropriati dell’organizzazione. Questo consente all’amministratore di determinare quali utenti sono qualificati per ricevere queste notifiche.
1. Ogni utente assegnato identificato nel passaggio precedente può configurare come desidera ricevere le notifiche. Il giorno [Pagina Preferenze Experience Cloud](https://experience.adobe.com/preferences/notification-section), assicurati che la sottoscrizione Experience Manager sia abilitata e che **Incidenti operativi** e **Consigli proattivi** le caselle di controllo sono selezionate sia per le colonne in-app che per quelle e-mail (vedi immagine qui sotto). Inoltre, si consiglia di impostare la sezione e-mail su **Notifiche istantanee** in modo da ricevere le notifiche immediatamente dopo il verificarsi di un problema.

![Configurare le sottoscrizioni](/help/operations/assets/configure-subscriptions.png)

>[!NOTE]
>Gli abbonamenti funzionano a livello di organizzazione e gli abbonati ricevono notifiche per tutti i programmi e gli ambienti all’interno degli stessi.

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

## Quali notifiche appaiono? {#which-notification}

AEM as a Cloud Service dispone di diversi tipi di notifiche, ma nel centro notifiche viene visualizzato solo un sottoinsieme, come illustrato nella tabella seguente.

| Tipo di notifica | Descrizione | Come configurare | Compare nel centro notifiche |
|---|---|---|---|
| Problemi operativi | Problemi critici che richiedono un intervento immediato | Utente assegnato al profilo di prodotto “Notifica prolema: Cloud Service”, casella di controllo “Problemi operativi” selezionata in [Preferenze Experience Cloud](https://experience.adobe.com/preferences) | X |
| Consigli proattivi | Ottimizzazioni da pianificare | Utente assegnato al profilo di prodotto “Notifica proattiva: Cloud Service”, casella di controllo “Consigli proattivi” selezionata in [Preferenze Experience Cloud](https://experience.adobe.com/preferences) | X |
| Stati della pipeline di Cloud Manager | Informazioni sullo stato delle pipeline | Utente con ruoli Proprietario business, Gestore programma o Gestore distribuzione, casella di controllo “Altri” selezionata in [Preferenze Experience Cloud](https://experience.adobe.com/preferences) |  |

## Tipi di notifica supportati {#supported-notification-types}

Nella tabella seguente sono elencati i tipi di notifica attualmente supportati.

| Tipo di notifica | Profilo prodotto correlato | Azione correttiva |
|---|---|---|
| Coda di replica bloccata | Problema | Sblocca la coda seguendo le istruzioni contenute nella [Documentazione di replica](/help/operations/replication.md#troubleshooting) |
| Certificato S2S in scadenza | Proattiva | Scopri come aggiornare una credenziale nella [Documentazione sulla generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |

