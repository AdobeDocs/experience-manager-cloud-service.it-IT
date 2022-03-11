---
title: Experience Manager [!DNL AEM Forms] Architettura as a Cloud Service
description: Comprendere l'architettura [!DNL AEM Forms] as a Cloud Service per scoprire gli aspetti relativi a scalabilità, resilienza e prestazioni della piattaforma.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 6%

---


# [!DNL AEM] Architettura as a Cloud Service {#architecture}

[!DNL AEM Forms] L’architettura di distribuzione as a Cloud Service viene standardizzata per tutti i clienti con l’obiettivo di liberare completamente i clienti da considerazioni di architettura. Ad esempio, mentre la nuova architettura as a Cloud Service AEM si basa ancora sul concetto di micro-kernel per la persistenza, i clienti non devono preoccuparsi di quale micro-kernel scegliere. I micro-kernel utilizzati sia dal lato dell’autore che da quello della pubblicazione sono univoci per [!DNL AEM Cloud Service] altrimenti non sono disponibili per i clienti per le installazioni on-premise.

AEM as a Cloud Service ha un&#39;architettura dinamica con un numero variabile di istanze AEM. Fornisce ambienti di sviluppo, stage, produzione e dimostrazione. Fornisce strumenti per gestire le istanze AEM (Cloud Manager), mantenere gli utenti e le autenticazioni (Admin Console e sistema IMS (gestione delle identità Adobi)), configurare la memorizzazione in cache (Flast CDN) e l’ambiente di sviluppo nativo per il cloud. Per ulteriori informazioni sull&#39;architettura consulta: [Introduzione all&#39;architettura di [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=en).

## Cloud Manager{#cloud-manager}

Cloud Manager è un componente essenziale per [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). Ogni nuovo tenant del [!DNL AEM Forms] Per l’accesso a Cloud Manager, as a Cloud Service viene eseguito il provisioning per la prima volta. Cloud Manager è il punto di ingresso singolo per le operazioni e l’utente tipo di sviluppatori dei nostri clienti. È il luogo da cui è possibile gestire i programmi e gli ambienti AEM. Cloud Manager si è evoluto come portale self-service in cui è possibile creare e configurare i componenti principali dell’AEM as a Cloud Service:

* Creazione e gestione di programmi
* Creazione e gestione degli ambienti AEM all’interno dei programmi
* Creazione e gestione delle pipeline per la distribuzione del codice cliente e della configurazione in un ambiente specifico
* Ricevere notifiche su importanti eventi del ciclo di vita per questi componenti (ad esempio aggiornamenti dei prodotti) Per ulteriori informazioni su Cloud Manager, consulta [Comprendere Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) e [Introduzione a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it).

## Utenti e autenticazione {#users-and-authentication}

AEM as a Cloud Service include il supporto Admin Console per le istanze AEM e l’autenticazione basata su Adobe Identity Management System (IMS). Admin Console consente agli amministratori di gestire tutti gli utenti di Experience Cloud da una posizione centralizzata. Gli utenti e i gruppi possono essere assegnati a profili di prodotto associati a istanze di AEM as a Cloud Service, per consentire loro di accedere a tale istanza. Per ulteriori informazioni sugli utenti, l&#39;autenticazione e l&#39;accesso a un&#39;istanza di AEM as a Cloud Service, vedi [Supporto IMS per [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

Vari utenti sono coinvolti in un [!DNL AEM Forms] progetto. Dopo l&#39;accesso al [!DNL AEM Forms] as a Cloud Service istanza, puoi [aggiungere utenti in admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=it) per gli utenti tipo applicabili all’organizzazione o al progetto e [assegnare gli utenti a gruppi incorporati](forms-groups-privileges-tasks.md) per fornire loro i privilegi richiesti.

Per apprendere varie [!DNL AEM Forms] specifici gruppi di utenti e privilegi disponibili su [!DNL AEM Forms] come istanza di Cloud Services, vedi [Configurazione, utente, ruoli e gruppi](forms-groups-privileges-tasks.md).

## Esperienza per sviluppatori {#developer-experience}

La nuova architettura che supporta AEM as a Cloud Service apporta alcune modifiche fondamentali all’esperienza complessiva degli sviluppatori. Uno degli obiettivi principali per le modifiche all’esperienza di sviluppo è quello di consentire la migrazione a AEM as a Cloud Service il prima possibile, con poche modifiche al codice personalizzato esistente.

## Sviluppo cloud {#cloud-development}

Di seguito sono riportate le linee guida per eseguire in modo scorrevole il codice esistente nell’ambiente AEM as a Cloud Service:

* Memorizza il codice e le configurazioni nell’archivio Git del programma Cloud Manager associato. La gestione e l&#39;integrazione del codice con CI/CD è un gioco da ragazzi.
* Rendere il codice e la configurazione dell&#39;applicazione compatibili con la linea di base [!DNL AEM Forms] immagini. L’utilizzo delle API più recenti consente di creare applicazioni più veloci e sicure.
* Utilizza la pipeline di Cloud Manager associata all’ambiente Cloud Manager per creare e distribuire le applicazioni. Consente di apportare le funzioni e i bug più recenti corretti per [!DNL AEM Forms] as a Cloud Service al tuo ambiente.
* Verifica che le tue applicazioni personalizzate trasmettano tutti i gate di qualità del codice, sicurezza e prestazioni applicati nella pipeline. Consente di creare applicazioni sicure e con prestazioni migliori che consentono di migliorare la customer experience. Puoi sempre utilizzare l’interfaccia utente di Cloud Manager per saltare alcuni controlli.
Questo processo viene comunemente definito sviluppo cloud-first. [!DNL AEM Forms] as a Cloud Service fornisce anche un SDK per supportare lo sviluppo rapido prima che le modifiche al codice in sospeso e alla configurazione vengano tentate nel cloud.
Alcune interfacce che prima facevano parte del AEM QuickStart non sono più disponibili per gli utenti dell&#39;ambiente as a Cloud Service AEM. Ad esempio, la console Web in cui vengono gestiti i bundle OSGI e la relativa configurazione associata. Il browser dell’archivio dei contenuti di CRXDE Lite diventa accessibile solo per i tipi di ambiente non di produzione. È disponibile un sottoinsieme delle funzionalità della console Web necessarie agli sviluppatori, in particolare per scopi di diagnostica e di stato, tramite una nuova console per sviluppatori.
Inoltre, uno dei requisiti più comuni per gli sviluppatori è l’accesso rapido ai file di registro dei vari ambienti. Con [!DNL AEM Cloud Service], i file di registro dei diversi nodi in Author, Publish sono resi disponibili tramite Cloud Manager, sotto forma di file che possono essere scaricati o tramite API per la creazione di code ai registri. A causa della netta separazione di codice e contenuto, gli sviluppatori possono sfruttare un particolare processo per aggiornare il contenuto come parte di una distribuzione. I casi d’uso tipici per i contenuti modificabili sono:
* Contenuto standard &quot;predefinito&quot; che fa parte del progetto del cliente (ad esempio cartelle, modelli, flussi di lavoro...)
* Definizioni degli indici di ricerca
* ACL e autorizzazioni
* Utenti e gruppi di utenti del servizio
Imposta l&#39;ambiente di sviluppo, [Configurare la pipeline CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html)e impara [distribuire il codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) sull&#39;ambiente.

## Sviluppo locale {#local-development}

Quando configuri e configuri un [!DNL AEM Forms] Ambiente as a Cloud Service, puoi configurare ambienti di sviluppo, staging e produzione. Inoltre, crea e configura un ambiente di sviluppo locale per iterazioni e sviluppo rapidi. Puoi scaricare e configurare AEM SDK e [!DNL AEM Forms] archivio di funzionalità aggiuntive per configurare un [!DNL Forms] Ambiente di sviluppo as a Cloud Service.  Per istruzioni dettagliate, vedi [Configurare un ambiente di sviluppo locale](setup-local-development-environment.md).

## Debugging {#debugging}

AEM as a Cloud Service viene eseguito su un&#39;infrastruttura cloud self-service, scalabile. Richiede agli sviluppatori AEM di comprendere ed eseguire il debug di vari facet di AEM as a Cloud Service, dalla generazione e distribuzione fino a ottenere i dettagli dell&#39;esecuzione delle applicazioni AEM. Per informazioni dettagliate, consulta [Debug AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en).
