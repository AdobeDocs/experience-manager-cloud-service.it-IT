---
title: Integrare Edge Delivery Services con Adobe Managed CDN in Cloud Manager
description: null
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: 71ea3b810d4145d5581c29e26db9bc157c425a15
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# Integrare Edge Delivery Services con Adobe Managed CDN in Cloud Manager {#integrate-adbe-cdn-with-edservices-in-cm}

Adobe Managed CDN (AMC-D) si integra in modo nativo con Edge Delivery Services per offrire esperienze performanti e distribuite a livello globale per i siti Adobe Experience Manager (AEM).

Insieme, offrono i seguenti vantaggi:

* Una rete CDN chiavi in mano di livello enterprise gestita da Adobe.
* Un moderno livello di consegna edge che accelera le richieste, ottimizza la memorizzazione in cache e protegge dagli attacchi più comuni.
* Un flusso di lavoro Cloud Manager unificato per la gestione dei domini, i certificati SSL e le distribuzioni basate su pipeline.

<!--
Adobe's Edge Delivery Services (EDS) can take advantage of an Adobe managed CDN. EDS is a framework that optimizes website delivery for speed, simplicity, and scalability by pushing content closer to the user through edge nodes. It is not a replacement for a CDN, but rather a way to enhance content delivery, especially when you use the Adobe managed CDN. It offers you the following benefits:

* Adobe-Managed CDN: EDS can use an Adobe-managed CDN, offering features like self-service CDN management and automatic certificate renewal. 
* EDS and AEM: EDS is a feature of AEM as a Cloud Service and works alongside the AEM authoring environment. 
* Performance enhancement: EDS, in conjunction with an Adobe Managed CDN, improves website performance by caching content at edge locations closer to users, reducing latency. 
* Flexibility: EDS provides flexibility in content delivery, allowing your organization to choose between the Adobe-managed CDN or their own CDN setup, based on their needs and existing infrastructure. 
Self-Service CDN Management:
Adobe-managed CDN within EDS enables self-service configuration and management tasks like SSL certificate setup. 
 
Use Cases:
EDS with CDN integration is beneficial for various scenarios, including e-commerce storefronts and websites requiring high performance and scalability. -->

## Opzioni di implementazione di Edge Delivery Services in Adobe Managed CDN in Cloud Manager {#deployment-options}

Questo argomento illustra i due modi in cui è possibile implementare Edge Delivery Services su Adobe Managed CDN in Cloud Manager e, altrettanto importante, consente di decidere quale opzione è più adatta al proprio caso d’uso.

Edge Delivery Services può essere configurato utilizzando una delle due opzioni seguenti. Ciascuno di essi dispone di funzionalità diverse.

|  | Opzione di implementazione | Documento chiave | Funzionalità | Ideale per |
| --- | --- | --- | --- | --- |
| Opzione 1 | *Con* un ambiente AEM as a Cloud Service (AEMaaCS) esistente | [Configurare un proxy da un ambiente esistente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment) | La pipeline di configurazione è generalmente disponibile per gli ambienti AEMaaCS | Team che già eseguono Sites in Cloud Manager e desiderano un miglioramento rapido delle prestazioni a basso rischio. |
| Opzione 2 | *Senza* un ambiente AEMaaCS esistente; noto come &quot;ambiente Edge&quot; autonomo. | [Imposta un sito Edge Delivery senza un ambiente esistente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment) | La pipeline di configurazione è attualmente disponibile solo per gli ambienti Edge tramite il programma Beta limitato.<br>Consulta [Aggiungi pipeline di configurazione Edge Delivery](help/implementing/cloud-manager/release-notes/current.md##add-eds-pipeline). | Nuove build o migrazioni che desiderano abbracciare l’architettura Edge Delivery completa e il routing granulare. |

<!-- Ultimately this URL above will need to be updated on GA -->

| Opzione | Riepilogo | Ideale per | Documenti chiave |
| --- | --- | --- | --- |
| Proxy CDN gestito di Adobe | Adobe Managed CDN esegue il front-end di un ambiente AEM Sites esistente. La pipeline Sites corrente rimane l’&quot;origine&quot;, mentre AMC-D gestisce il caching dei bordi e la terminazione TLS. | Team che già eseguono Sites in Cloud Manager e desiderano un miglioramento rapido delle prestazioni a basso rischio. | Configurare un proxy AMC-D |
| Pipeline di configurazione con originSelectors | Una pipeline di configurazione Edge Delivery dedicata pubblica il contenuto statico e dinamico direttamente al server Edge di. `originSelectors` instrada il traffico tra AMC-D e i livelli di authoring/pubblicazione di AEM. | Nuove build o migrazioni che desiderano abbracciare l’architettura Edge Delivery completa e il routing granulare. | Configurare la pipeline di Edge Delivery |

>[!TIP]
>
>Non sei sicuro del percorso da scegliere? Consulta [Scegliere un modello di distribuzione](#choose-deployment-model) di seguito per le linee guida per le decisioni.

## Scegli un modello di distribuzione {#choose-deployment-model}

Entrambi i modelli possono coesistere all’interno dello stesso programma Cloud Manager, consentendo migrazioni graduali.

| Se... | Quindi utilizza... |
| :--- | :--- |
| Necessità di un rollout rapido e con modifiche minime e hosting di Sites già in Cloud Manager | Proxy AMC-D |
| Pianifica la ristrutturazione del contenuto per Edge Delivery o desidera un indirizzamento dettagliato tra più origini | Configura pipeline di consegna Edge + `originSelectors` |

## Prerequisiti {#prerequisites}

1. Onboarding del sito in Cloud Manager: richiesto per entrambi i modelli di distribuzione. Segui Onboarding in un sito AEM.

2. Porta il tuo Git (BYOG) (facoltativo): se archivi il codice del sito al di fuori di Adobe Git, completa l’onboarding di BYOG.

3. Licenza Edge Delivery: assicurati che il programma sia concesso in licenza per Edge Delivery Services.


