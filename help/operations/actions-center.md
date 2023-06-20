---
title: Centro azioni
description: Sfruttare il Centro azioni per intervenire in modo comodo sugli incidenti e su altre informazioni importanti
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 27%

---

# Centro azioni {#actions-center}

>[!NOTE]
>Questa funzione non è stata rilasciata.

Il Cloud Service AEM invia notifiche e-mail al Centro operativo quando si verificano incidenti critici che richiedono un’azione immediata, nonché raccomandazioni proattive per le ottimizzazioni. Alcuni esempi includono una coda bloccata o un set di credenziali in scadenza; l&#39;intero set di tipi di notifica Centro operativo può essere visualizzato nel [tabella seguente](#supported-notification-types), che si espanderà nel tempo.

Quando viene ricevuta una notifica e-mail del Centro azioni, è possibile fare clic su di essa per aprire il Centro azioni di AEM as a Cloud Service con un pop-up contenente un contesto aggiuntivo che spiega l’azione che un cliente deve intraprendere.

Oltre a visualizzare informazioni sulla notifica e-mail con clic, il Centro azioni funge da hub in cui è possibile visualizzare e gestire il set di notifiche correnti e precedenti. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Nel Centro azioni sono disponibili due categorie di notifiche di alto livello:

1. Problemi operativi: si è verificato un evento, che in genere richiede una risoluzione rapida. Ad esempio, la risoluzione di una coda bloccata.
1. Consigli proattivi: Adobe suggerisce un’azione che il cliente dovrebbe intraprendere nel prossimo futuro. Ad esempio, per interrompere il riferimento a un’interfaccia utente obsoleta.

Consulta la [tabella seguente](#supported-notification-types) per le notifiche attualmente supportate in Centro azioni.

Dal Centro azioni è possibile selezionare un programma e un ambiente specifici, che ha l&#39;effetto di filtrare per tale ambito.

## Configurazione {#configuration}

Per configurare la ricezione delle notifiche e-mail del Centro operativo, crea i profili di prodotto descritti [in questo articolo](/help/journey-onboarding/notification-profiles.md), ovvero Notifica per incidente - Cloud Service e Notifica proattiva - Cloud Service. Assegna inoltre gli ID Adobe appropriati dalla tua organizzazione a tali profili. Questo consente a un amministratore di determinare quali utenti sono idonei a ricevere queste notifiche e-mail.

>[!NOTE]
>Le notifiche e-mail del Centro Azioni funzionano a livello di organizzazione, in modo che gli abbonati ricevano notifiche per tutti i programmi e gli ambienti all’interno di tali programmi.

## Flusso utente dettagliato {#detailed-user-flow}

Facendo clic sull’e-mail si accede al Centro azioni, con un pop-up che mostra il contesto della notifica su cui si è fatto clic e, in alcuni casi, collegamenti a informazioni aggiuntive che descrivono come intraprendere azioni correttive.

![Dettagli problema](/help/operations/assets/incident-details.png)

Facendo clic su **Ulteriori informazioni** link porta l’utente a questo articolo, dove è possibile fare riferimento al tipo di notifica nel [tabella dei tipi di notifica supportati](#supported-notification-types) di seguito, che fornisce indicazioni sulle azioni da intraprendere.

Nel Centro azioni è possibile visualizzare un elenco di altre notifiche recenti. Utilizzando l’elenco Azioni, è consigliabile confermare una notifica per segnalare all’Adobe che l’organizzazione è a conoscenza dell’attività e risolvere successivamente la notifica quando è stata intrapresa un’azione correttiva.

![Elenco notifiche](/help/operations/assets/notification-list.png)

Nella maggior parte dei casi, il popup deve fornire tutto il contesto necessario per risolvere il problema. Tuttavia, in caso di domande come ad Adobe Supporto, puoi fare clic sul pulsante **Contatta il supporto** nel popup. Verrà visualizzato un modulo in cui è possibile descrivere la domanda e inviarla per creare un ticket di supporto, che includerà anche un riferimento alla notifica specifica in modo che un Adobe di tecnici del supporto possa avere il contesto appropriato.

![Contatta supporto 1](/help/operations/assets/contact-support1.png)

![Contatta supporto 2](/help/operations/assets/contact-support2.png)

Come tutti i ticket di supporto, questo verrà visualizzato nella [scheda Casi di supporto Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/support-for-enterprise.html), in cui puoi tenerne traccia e aggiungere ulteriori commenti.

![Supporto Admin Console](/help/operations/assets/admin-console-support.png)

## Quali notifiche appaiono? {#which-notification}

L’AEM as a Cloud Service ha diversi tipi di notifiche, ma nel Centro azioni viene visualizzato solo un sottoinsieme, come illustrato nella tabella seguente.

| Tipo di notifica | Descrizione | Come configurare | Viene visualizzato nel Centro azioni |
|---|---|---|---|
| Problemi operativi | Problemi critici che richiedono un intervento immediato | Utente assegnato al profilo di prodotto &quot;Notifica per incidente - Cloud Service&quot; | X |
| Consigli proattivi | Ottimizzazioni da pianificare | Utente assegnato al profilo di prodotto &quot;Notifica proattiva - Cloud Service&quot; | X |
| Stati della pipeline di Cloud Manager | Informazioni sullo stato delle pipeline | Utente con ruoli Proprietario business, Gestore programma o Gestore distribuzione, casella di controllo “Altri” selezionata in [Preferenze Experience Cloud](https://experience.adobe.com/preferences), come [descritto qui](/help/implementing/cloud-manager/notifications.md). |   |

## Tipi di notifica supportati {#supported-notification-types}

Nella tabella seguente sono elencati i tipi di notifica attualmente supportati in Centro azioni.

| Tipo di notifica | Profilo prodotto correlato | Azione correttiva |
|---|---|---|
| Coda di replica bloccata | Problema | Sblocca la coda seguendo le istruzioni contenute nella [Documentazione di replica](/help/operations/replication.md#troubleshooting) |
| Certificato S2S in scadenza | Proattiva | Scopri come aggiornare una credenziale nella [Documentazione sulla generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |

