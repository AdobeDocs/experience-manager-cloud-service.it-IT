---
title: Centro azioni
description: Sfruttare il Centro operativo per intervenire in modo comodo in caso di incidenti e altre informazioni importanti
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
feature: Operations
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 45%

---

# Centro azioni {#actions-center}

AEM as a Cloud Service invia notifiche e-mail del Centro azioni quando si verificano incidenti critici che richiedono un’azione immediata, e consigli proattivi per le ottimizzazioni. Gli esempi includono una coda bloccata o un set di credenziali in scadenza; il set completo dei tipi di notifica del Centro azioni può essere visualizzato nella [tabella seguente](#supported-notification-types), che verrà ampliata nel tempo.

Quando viene ricevuta una notifica e-mail del Centro azioni, è possibile fare clic su di essa per aprire il Centro azioni di AEM as a Cloud Service con un pop-up contenente un contesto aggiuntivo che spiega l’azione che un cliente deve intraprendere.

Oltre a visualizzare informazioni sulla notifica e-mail appena cliccata, il Centro azioni funge da hub dove è possibile visualizzare e gestire il set di notifiche attuali e precedenti. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

Nel Centro azioni sono visualizzate due categorie di notifiche di alto livello:

1. Problemi operativi: si è verificato un evento, che in genere richiede una risoluzione tempestiva. Ad esempio, la risoluzione di una coda bloccata.
1. Consigli proattivi: Adobe suggerisce un’azione che il cliente dovrebbe intraprendere nel prossimo futuro. Ad esempio, per interrompere il riferimento a un’interfaccia utente obsoleta.

Consulta la [tabella seguente](#supported-notification-types) per le notifiche attualmente supportate nel Centro azioni.

Dalla schermata del Centro azioni è possibile selezionare un programma e un ambiente specifici, tramite i quali è possibile filtrare per quell’ambito.

## Configurazione {#configuration}

Per configurare la ricezione delle notifiche e-mail del Centro operativo, creare i profili prodotto come descritto in [Profili di notifica](/help/journey-onboarding/notification-profiles.md), ovvero Notifica per incidente - Cloud Service e Notifica proattiva - Cloud Service. Assegna inoltre gli ID Adobe appropriati dalla tua organizzazione a tali profili. Questo consente all’amministratore di determinare quali utenti sono qualificati per ricevere queste notifiche e-mail.

>[!NOTE]
>Le notifiche e-mail del Centro azioni funzionano a livello di organizzazione e gli abbonati quindi ricevono notifiche per tutti i programmi e gli ambienti all’interno degli stessi.

## Flusso utente dettagliato {#detailed-user-flow}

Facendo clic sull’e-mail si accede al Centro azioni, con un pop-up che mostra il contesto della notifica su cui si è fatto clic e, in alcuni casi, collegamenti a informazioni aggiuntive che descrivono come intraprendere azioni correttive. È inoltre possibile accedere direttamente al Centro operativo all&#39;indirizzo [https://experience.adobe.com/aem/actions-center](https://experience.adobe.com/aem/actions-center/), dove è possibile selezionare il programma e l&#39;ambiente appropriati.

![Dettagli problema](/help/operations/assets/incident-details.png)

Facendo clic sul collegamento a **Ulteriori informazioni** l’utente potrà consultare questo articolo, in cui è possibile fare riferimento alla [tabella dei tipi di notifica supportati](#supported-notification-types) seguente, la quale fornisce indicazioni sull’azione da intraprendere.

Nel Centro azioni è disponibile un elenco di altre notifiche recenti. È consigliabile utilizzare l’elenco Azioni per confermare una notifica per segnalare ad Adobe che l’organizzazione è a conoscenza dell’attività e per risolvere in seguito la notifica dopo aver intrapreso un’azione correttiva.

![Elenco notifiche](/help/operations/assets/notification-list.png)

Nella maggior parte dei casi, il pop-up deve fornire tutto il contesto necessario per risolvere il problema. Tuttavia, in caso di domande sul supporto Adobe, puoi fare clic sul collegamento **Contatta il supporto** nel pop-up. Viene visualizzato un modulo dal quale è possibile descrivere la domanda e inviarla per creare un ticket di supporto, che includerà anche un riferimento alla notifica specifica in modo che un tecnico del supporto Adobe abbia il contesto pertinente.

![Contatta supporto 1](/help/operations/assets/contact-support1.png)

![Contatta supporto 2](/help/operations/assets/contact-support2.png)

Come tutti i ticket di supporto, questo verrà visualizzato nella [scheda Casi di supporto Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/support-for-enterprise.html), in cui puoi tenerne traccia e aggiungere ulteriori commenti.

![Supporto Admin Console](/help/operations/assets/admin-console-support.png)

## Quali notifiche appaiono? {#which-notification}

AEM as a Cloud Service dispone di diversi tipi di notifiche, ma nel Centro azioni viene visualizzato solo un sottoinsieme, come illustrato nella tabella seguente.

| Tipo di notifica | Descrizione | Come configurare | Compare nel Centro azioni |
|---------------------------------|-----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| Problemi operativi | Problemi critici che richiedono un intervento immediato | Utente assegnato al profilo di prodotto “Notifica per problema - Cloud Service” | X |
| Consigli proattivi | Ottimizzazioni da pianificare | Utente assegnato al profilo di prodotto “Notifica proattiva - Cloud Service” | X |
| Stati della pipeline di Cloud Manager | Informazioni sullo stato delle pipeline | Utente con ruoli Proprietario business, Responsabile del programma o Responsabile della distribuzione, casella di controllo &quot;Altri&quot; selezionata in [Preferenze Experience Cloud](https://experience.adobe.com/preferences), vedi [Notifiche](/help/implementing/cloud-manager/notifications.md). |                           |

## Tipi di notifica supportati {#supported-notification-types}

Nella tabella seguente sono elencati i tipi di notifica attualmente supportati in Centro azioni. Le notifiche sono attualmente limitate agli ambienti di produzione.

| Tipo di notifica | Profilo prodotto correlato | Azione correttiva |
|---------------------------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Coda di replica bloccata | Problema | Sblocca la coda seguendo le istruzioni contenute nella [Documentazione di replica](/help/operations/replication.md#troubleshooting) |
| Query GraphQL persistente non valida | Problema | Correggere la query GraphQL non valida facendo riferimento alla [documentazione sulla risoluzione dei problemi relativi alle query GraphQL persistenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/persisted-queries-troubleshoot.html?lang=it) |
| Picco di traffico all’origine | Problema | Proteggi l’origine configurando regole del filtro del traffico del limite di velocità che si attivano a soglie inferiori all’avviso di picco di traffico predefinito all’origine.  Consulta la sezione [Blocco di attacchi DoS e DDoS tramite le regole del traffico](/help/security/traffic-filter-rules-including-waf.md#blocking-dos-and-ddos-attacks-using-traffic-filter-rules) della documentazione sulle regole del filtro del traffico, che fa riferimento a un&#39;esercitazione. |
| Regole dei filtri di traffico CDN attivate | Problema | Se la regola del filtro del traffico corrispondente riflette un attacco e il sito non blocca tale traffico, proteggi il sito configurando una regola del filtro del traffico in modalità di blocco. Consulta la sezione [Protezione dei siti Web con regole del filtro del traffico (incluse le regole di WAF)](/help/security/traffic-filter-rules-including-waf.md#tutorial-protecting-websites) della documentazione sulle regole del filtro del traffico, che fa riferimento a un&#39;esercitazione. |
| Errori di inoltro registro Splunk | Problema | Verifica che l’endpoint Splunk funzioni e sia raggiungibile dall’ambiente AEM Cloud Service. Per ulteriori informazioni sull&#39;inoltro del registro, visitare la [documentazione sull&#39;inoltro del registro Splunk](/help/implementing/developing/introduction/logging.md#splunk-logs). Se hai bisogno di assistenza per la risoluzione dei problemi o se devi apportare modifiche alla configurazione di registrazione, genera un ticket di supporto con Adobe. |
| Le pagine contengono un numero elevato di nodi | Proattiva | Riduci il numero totale di nodi all’interno di una pagina. Consulta la [documentazione sulla complessità delle pagine](https://experienceleague.adobe.com/it/docs/experience-manager-pattern-detection/table-of-contents/pcx) | |
| Numero elevato di istanze del flusso di lavoro in esecuzione | Proattiva | Termina i flussi di lavoro in esecuzione che non sono più necessari. Scopri come [configurare un processo di eliminazione](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/operations/maintenance) |               |
| Certificato S2S in scadenza | Proattiva | Scopri come aggiornare una credenziale nella [Documentazione sulla generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) | Numero elevato di connessioni | Proattiva | Scopri il connection pooling in [Connection pooling insieme alla documentazione delle reti avanzate](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking) |
| Mappatura utenti servizio obsoleti | Proattiva | Scopri come utilizzare il nuovo formato di mappatura utente del servizio Sling, come indicato in [Best practice per la mappatura utente del servizio Sling e la definizione utente del servizio](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/best-practices-for-sling-service-user-mapping-and-service-user-definition) |
| Numero elevato di connessioni | Proattiva | Scopri il connection pooling nella [documentazione sulle reti avanzate](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking) |  |
| Utenti aggiunti direttamente al gruppo personalizzato | Proattiva | Gli utenti devono essere aggiunti ai gruppi IMS pertinenti e questi gruppi IMS devono essere aggiunti come membri dei gruppi AEM. Allinea con [Best practice IMS](/help/security/ims-support.md) | |
| Contenuto JCR mancante | Proattiva | Aggiungi un nodo di contenuto JCR mancante. Consulta la [documentazione di Assets Content Validator](https://experienceleague.adobe.com/it/docs/experience-manager-pattern-detection/table-of-contents/acv) | |
| Flussi di lavoro completati non eliminati | Proattiva | Riduci al minimo il numero di istanze del flusso di lavoro e migliora le prestazioni eliminando le istanze del flusso di lavoro che hanno più di 90 giorni. Scopri come [configurare le attività di manutenzione](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/operations/maintenance) | |
| Tipo di risorsa Sling mancante nella pagina | Proattiva | Aggiungi nodo di tipo di risorsa Sling mancante. Consulta la [documentazione di Assets Content Validator](https://experienceleague.adobe.com/it/docs/experience-manager-pattern-detection/table-of-contents/acv) | |
| Query lenta | Proattiva | Correggi le query lente definendo le definizioni di indice corrette come suggerito dalla [Scheda di riferimento rapido per le query JCQ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/JCR_query_cheatsheet-v1.1.pdf?lang=it) | |
| Query senza indice | Proattiva | Evita di eseguire query che non utilizzano un indice - [collegamento alla documentazione sull&#39;indicizzazione](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/operations/indexing) | |
| Avviso libreria obsoleta | Proattiva | Sostituisci i pacchetti obsoleti con le versioni più recenti consigliate, come descritto nell&#39;[articolo obsoleto](/help/release-notes/deprecated-removed-features.md), per mantenere l&#39;applicazione sicura e performante | |
| Avviso configurazione obsoleta | Proattiva | Sostituisci le configurazioni obsolete con le versioni più recenti consigliate, come descritto nell&#39;[articolo obsoleto](/help/release-notes/deprecated-removed-features.md), per mantenere l&#39;applicazione sicura e performante |
