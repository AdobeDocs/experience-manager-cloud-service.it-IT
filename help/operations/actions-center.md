---
title: Centro azioni
description: Sfruttare il Centro azioni per intervenire opportunamente su problemi e altre informazioni importanti
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: 083aa4b893b58102b3a0bf68c4dd3b4c003b48f6
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 90%

---

# Centro azioni {#actions-center}

>[!NOTE]
>Questa funzione non è stata rilasciata.

Il Cloud Service AEM invia notifiche e-mail al Centro operativo quando si verificano incidenti critici che richiedono un’azione immediata e raccomandazioni proattive per le ottimizzazioni. Gli esempi includono una coda bloccata o un set di credenziali in scadenza; il set completo dei tipi di notifica del Centro azioni può essere visualizzato nella [tabella seguente](#supported-notification-types), che verrà ampliata nel tempo.

Quando viene ricevuta una notifica e-mail del Centro azioni, è possibile fare clic su di essa per aprire il Centro azioni di AEM as a Cloud Service con una finestra a comparsa, nella quale viene mostrato un contesto aggiuntivo che spiega al cliente l’azione da intraprendere.

Oltre a visualizzare informazioni sulla notifica e-mail appena cliccata, il Centro azioni funge da hub dove è possibile visualizzare e gestire il set di notifiche attuali e precedenti. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

Nel Centro azioni sono visualizzate due categorie di notifiche di alto livello:

1. Problemi operativi: si è verificato un evento, che in genere richiede una risoluzione rapida. Ad esempio, la risoluzione di una coda bloccata.
1. Consigli proattivi: Adobe suggerisce un’azione che il cliente dovrebbe intraprendere nel prossimo futuro. Ad esempio, per interrompere il riferimento a un’interfaccia utente obsoleta.

Consulta la [tabella seguente](#supported-notification-types) per le notifiche attualmente supportate nel Centro azioni.

Dalla schermata del Centro azioni è possibile selezionare un programma e un ambiente specifici, tramite i quali è possibile filtrare per quell’ambito.

## Configurazione {#configuration}

Per configurare la ricezione delle notifiche e-mail del Centro azioni, crea i profili di prodotto descritti [in questo articolo](/help/journey-onboarding/notification-profiles.md), ovvero Notifica per problema - Cloud Service e Notifica proattiva - Cloud Service. Assegna inoltre gli ID Adobe appropriati dalla tua organizzazione a tali profili. Questo consente all’amministratore di determinare quali utenti sono qualificati per ricevere queste notifiche e-mail.

>[!NOTE]
>Le notifiche e-mail del Centro azioni funzionano a livello di organizzazione e gli abbonati quindi ricevono notifiche per tutti i programmi e gli ambienti all’interno degli stessi.

## Flusso utente dettagliato {#detailed-user-flow}

Facendo clic sull’e-mail si accede al Centro azioni, con una finestra a comparsa che mostra il contesto per la notifica su cui hai fatto clic e, in alcuni casi, collegamenti a informazioni aggiuntive che descrivono come intraprendere un’azione correttiva.

![Dettagli problema](/help/operations/assets/incident-details.png)

Facendo clic sul collegamento a **Ulteriori informazioni** l’utente potrà consultare questo articolo, in cui è possibile fare riferimento alla [tabella dei tipi di notifica supportati](#supported-notification-types) seguente, la quale fornisce indicazioni sull’azione da intraprendere.

Nel Centro azioni è disponibile un elenco di altre notifiche recenti. Utilizzando l’elenco Azioni, è consigliabile confermare una notifica per segnalare all’Adobe che l’organizzazione è a conoscenza dell’attività e risolvere successivamente la notifica quando è stata intrapresa un’azione correttiva.

![Elenco notifiche](/help/operations/assets/notification-list.png)

Nella maggior parte dei casi, la finestra a comparsa dovrebbe fornire tutto il contesto necessario per risolvere il problema. Tuttavia, se hai bisogno di porre domande al supporto Adobe, puoi fare clic sul collegamento **Contatta supporto** nel popup di notifica. Viene visualizzato un modulo dal quale è possibile descrivere la domanda e inviarla per creare un ticket di supporto, che includerà anche un riferimento alla notifica specifica in modo che un tecnico del supporto Adobe abbia il contesto pertinente.

![Contatta supporto 1](/help/operations/assets/contact-support1.png)

![Contatta supporto 2](/help/operations/assets/contact-support2.png)

Come tutti i ticket di supporto, questo verrà visualizzato nella [scheda Casi di supporto Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/support-for-enterprise.html), in cui puoi tenerne traccia e aggiungere ulteriori commenti.

![Supporto Admin Console](/help/operations/assets/admin-console-support.png)

## Quali notifiche appaiono? {#which-notification}

AEM as a Cloud Service dispone di diversi tipi di notifiche, ma nel Centro azioni viene visualizzato solo un sottoinsieme, come illustrato nella tabella seguente.

| Tipo di notifica | Descrizione | Come configurare | Compare nel Centro azioni |
|---|---|---|---|
| Problemi operativi | Problemi critici che richiedono un intervento immediato | Utente assegnato al profilo di prodotto “Notifica per problema - Cloud Service” | X |
| Consigli proattivi | Ottimizzazioni da pianificare | Utente assegnato al profilo di prodotto “Notifica proattiva - Cloud Service” | X |
| Stati della pipeline di Cloud Manager | Informazioni sullo stato delle pipeline | Utente con ruoli Proprietario business, Gestore programma o Gestore distribuzione, casella di controllo “Altri” selezionata in [Preferenze Experience Cloud](https://experience.adobe.com/preferences), come [descritto qui](/help/implementing/cloud-manager/notifications.md). |   |

## Tipi di notifica supportati {#supported-notification-types}

Nella tabella seguente sono elencati i tipi di notifica attualmente supportati nel Centro azioni. Le notifiche sono attualmente limitate agli ambienti di produzione.

| Tipo di notifica | Profilo prodotto correlato | Azione correttiva |
|---|---|---|
| Coda di replica bloccata | Problema | Sblocca la coda seguendo le istruzioni contenute nella [Documentazione di replica](/help/operations/replication.md#troubleshooting) |
| Certificato S2S in scadenza | Proattiva | Scopri come aggiornare una credenziale nella [Documentazione sulla generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |

