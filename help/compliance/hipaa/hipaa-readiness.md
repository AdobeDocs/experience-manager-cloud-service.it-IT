---
title: Preparazione HIPAA per Adobe Experience Manager as a Cloud Service
description: Scopri il supporto di Experience Manager as a Cloud Service per i regolamenti HIPAA e come conformarsi quando si implementa un nuovo progetto AEM as a Cloud Service.
feature: Compliance
role: Admin, Architect, Developer, Leader
source-git-commit: 49721ac71bc2bde10eb5f25db58ee1b07c8a82e5
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 6%

---

# Preparazione HIPAA per Adobe Experience Manager as a Cloud Service {#hipaa-readiness-for-adobe-experience-manager-as-a-cloud-service}

>[!WARNING]
>
>Il contenuto di questo documento non costituisce una consulenza legale e non intende esserne una sostituzione.
>
>Consulta l’ufficio legale della tua azienda per ricevere consigli in merito alle normative HIPAA.

>[!NOTE]
>
>Per ulteriori informazioni sulla risposta di Adobe ai problemi di privacy e sulle conseguenze per i clienti di Adobe, consulta:
>
>* [Prodotti e servizi HIPAA e Adobe](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html) nel Centro affidabilità di Adobe
>* [Centro per la privacy di Adobe](https://www.adobe.com/it/privacy.html)

Per Adobe Experience Manager (AEM) as a Cloud Service, Adobe fornisce la documentazione necessaria per comprendere lo stato di preparazione all’HIPAA. Può aiutarti a conformarti a queste normative.

## Health Insurance Portability and Accountability Act (HIPAA) {#health-insurance-portability-and-accountability-act-hipaa}

### Legge sulla portabilità e responsabilità dell’assicurazione sanitaria (Health Insurance Portability and Accountability Act, HIPAA) {#the-health-insurance-portability-and-accountability-act-hipaa}

Le Regole HIPAA sulla Privacy, la Sicurezza e la Notifica di Violazione stabiliscono importanti protezioni per le informazioni sanitarie identificabili individualmente note come Protected Health Information (PHI).

In base all&#39;HIPAA, un&#39;entità coperta è un fornitore di assistenza sanitaria, un piano sanitario o un centro di assistenza sanitaria. Una società collegata è un&#39;entità che fornisce servizi a un&#39;entità coperta che comporta l&#39;accesso a PHI. Le norme HIPAA sulla privacy e sulla sicurezza richiedono che un’entità coperta ottenga garanzie scritte da un socio in affari sotto forma di un accordo di associazione commerciale (BAA) che richieda al socio in affari di salvaguardare la privacy e la sicurezza del PHI dell’entità coperta.

### Fornitura di PHI ad Adobe {#providing-phi-to-adobe}

Adobe funge da Business Associate per i servizi compatibili con HIPAA, elencati in [Servizi conformi HIPAA in AEM as a Cloud Service](#hipaa-readiness-of-services-in-aem-as-a-cloud-service).

I clienti che ottengono in licenza un servizio compatibile con HIPAA di Adobe per l&#39;elaborazione del PHI **devono** disporre della licenza corretta e di un BAA firmato con Adobe.

>[!IMPORTANT]
>
>Ai clienti non è consentito creare, ricevere, gestire o trasmettere dati PHI tramite prodotti e servizi Adobe non designati come servizi compatibili con HIPAA o senza la licenza appropriata per l’utilizzo di un servizio compatibile con HIPAA.

### Responsabilità condivise HIPAA {#hipaa-shared-responsibilities}

I servizi compatibili con HIPAA di Adobe si basano su un modello di sicurezza basato sulla responsabilità condivisa, che richiede al cliente e ad Adobe di assumersi responsabilità distinte per il mantenimento della sicurezza di PHI. In questo modello di sicurezza condivisa, Adobe si basa sul cliente per utilizzare e configurare i servizi compatibili con HIPAA.

Per ulteriori informazioni sull’esecuzione di una BAA di Adobe per i servizi conformi allo standard HIPAA, contatta il tuo rappresentante commerciale Adobe o il tuo Customer Success Manager.

>[!IMPORTANT]
>
>**Dichiarazione di non responsabilità**:
>
>Il Cliente è responsabile dell&#39;utilizzo dei Servizi compatibili con HIPAA di Adobe e della conformità dei Servizi compatibili con HIPAA di Adobe.

Per ulteriori informazioni, vedere [Prodotti e servizi HIPAA e Adobe](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html) nel Centro protezione di Adobe.

## Terminologia HIPAA {#hipaa-terminology}

Nella tabella seguente viene descritta la classificazione dei servizi AEM per l’utilizzo HIPAA.

| Preparazione HIPAA | Descrizione |
| --- | --- |
| compatibile con HIPAA | Progettato per elaborare PHI quando configurato in modo appropriato e utilizzato con una BAA. |
| Non compatibile con HIPAA | Non progettato per l’elaborazione di PHI e non deve essere utilizzato in casi d’uso correlati all’HIPAA. |

>[!NOTE]
>
>Le classificazioni di idoneità HIPAA si basano sulla funzionalità prevista di ciascun servizio e possono cambiare nel tempo.
>
>Quando pianificano le implementazioni relative all’HIPAA, i clienti devono fare riferimento alla documentazione più recente e ai termini contrattuali applicabili.

## Preparazione HIPAA dei servizi in AEM as a Cloud Service {#hipaa-readiness-of-services-in-aem-as-a-cloud-service}

La tabella seguente descrive quali servizi di AEM sono pronti per HIPAA e quali possono essere utilizzati insieme a essi. I servizi compatibili con HIPAA richiedono l&#39;acquisto di una protezione estesa per l&#39;assistenza sanitaria, come descritto in [Requisiti aggiuntivi](#additional-requirements).

| Prodotto/funzionalità | Servizio/i | Preparazione HIPAA |
| --- | --- | --- |
| AEM Sites | AEM Sites, AEM Publish, Edge Delivery Services | compatibile con HIPAA |
| AEM Sites | Editor universale | Non compatibile con HIPAA<br>[1] Può essere aggiunto a un programma di sicurezza esteso quando non viene introdotto alcun PHI. |
| AEM Sites Optimizer | Sites Optimizer | Non compatibile con HIPAA<br>[1] Può essere aggiunto a un programma di sicurezza esteso quando non viene introdotto alcun PHI. |
| AEM Assets | AEM Assets | compatibile con HIPAA |
| AEM Assets | Content Hub | Non compatibile con HIPAA<br>[1] Può essere aggiunto a un programma di sicurezza esteso quando non viene introdotto alcun PHI. |
| AEM Assets | Brand Portal | Non compatibile con HIPAA |
| AEM Assets | Dynamic Media OpenAPI | Non compatibile con HIPAA<br>[1] Può essere aggiunto a un programma di sicurezza esteso quando non viene introdotto alcun PHI. |
| AEM Assets | Scena Dynamic Media 7 | Non compatibile con HIPAA |
| AEM Forms | AEM Forms, Servizio Facade di autenticazione, Servizio Utilità PDF | compatibile con HIPAA |
| AEM CIF | Commerce Integration Framework | Non compatibile con HIPAA |
| AEM Cloud Manager | AEM Cloud Manager, Release Orchestrator, interruttori di rilascio, convalida rilascio | compatibile con HIPAA |
| AEM Cloud Manager | Distribuzione del software | Non compatibile con HIPAA<br>[1] Può essere aggiunto a un programma di sicurezza esteso quando non viene introdotto alcun PHI. |
|   |   |   |
| AEM Guides  | AEM Guides  | Non compatibile con HIPAA |
|   |   |   |
| LLM Optimizer | LLM Optimizer | Non compatibile con HIPAA<br>[1] Può essere aggiunto a un programma di sicurezza esteso quando non viene introdotto alcun PHI. |

>[!NOTE]
>
>[1]
>
>Per i servizi non compatibili con HIPAA che possono essere aggiunti a un programma di sicurezza esteso, i clienti devono assicurarsi che PHI non venga instradato a o memorizzato in tali servizi.
>
>Introdurre il PHI in un servizio che non è compatibile con HIPAA può causare la non conformità.

### Requisiti aggiuntivi {#additional-requirements}

[I servizi elencati](#hipaa-readiness-of-services-in-aem-as-a-cloud-service) come pronti per HIPAA richiedono l&#39;acquisto di una protezione estesa per l&#39;assistenza sanitaria.

Quando si acquista la soluzione Extended Security for Healthcare, è necessario che:

* i prodotti selezionati per tale programma sono pronti per HIPAA (come elencato nella tabella),
* La sicurezza estesa per l&#39;assistenza sanitaria è stata acquistata per *ogni* prodotto; in questo modo si garantisce un numero sufficiente di crediti Cloud Manager,
* La sicurezza estesa per l&#39;assistenza sanitaria viene applicata al momento della creazione del programma.

Se i requisiti sono soddisfatti, la sicurezza estesa per l&#39;assistenza sanitaria può essere applicata al momento della creazione del programma AEM. Per informazioni dettagliate, vedere [Configurazione](#setup).

>[!NOTE]
>
>Per ulteriori dettagli su provisioning e prezzi, rivolgiti al tuo rappresentante commerciale.

## Ambienti {#environments}

*HIPAA-ready* non è applicabile agli ambienti RDE (Rapid Development Environment), Dev o Stage, in quanto PHI non è consentito in questi ambienti.

Ciò significa che devi:

* utilizzare dati fittizi a scopo di sviluppo e test
* Elabora PHI solo dagli ambienti di produzione

La tabella seguente mostra dove i tipi di ambiente possono essere supportati come pronti per HIPAA.

| | RDE | Svil. | Fase  | Prod |
| --- | --- | --- | --- | --- |
| Tipo di ambiente  | No  | No  | No  | Sì  |

## Configurazione {#setup}

Quando [crei programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md), la scheda [Protezione fornisce le opzioni per attivare la protezione HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security).