---
title: Modifiche di rilievo apportate ad AEM Sites in AEM Cloud Service
description: Modifiche di rilievo apportate ad AEM Sites in AEM Cloud Service
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 17%

---

# Modifiche di rilievo apportate ad AEM Sites as a Cloud Service {#notable-changes}

AEM Sites as a Cloud Service fornisce funzionalità di gestione delle esperienze come parte del AEM nativo del cloud come piattaforma di Cloud Service. Oltre ai vantaggi principali di AEM come Cloud Service, come la scalabilità nativa per il cloud, il uptime e sempre aggiornato, AEM Sites as a Cloud Service fornisce anche una serie di modifiche e aggiunte specifiche per Sites.

>[!NOTE]
>Questo documento evidenzia le modifiche di rilievo apportate ad AEM Sites. Per le modifiche generali a AEM come Cloud Service e ad altri moduli, consulta:
>
>* [Introduzione ad Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* [Panoramica di AEM as a Cloud Service: novità e differenze](/help/overview/what-is-new-and-different.md)
* [Architettura](/help/core-concepts/architecture.md) di Adobe Experience Manager as a Cloud Service
* [Modifiche di rilievo apportate ad AEM as a Cloud Service (Note sulla versione)](/help/release-notes/aem-cloud-changes.md)
* [Modifiche di rilievo apportate ad AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Introduzione ad AEM Assets as a Cloud Service](/help/assets/overview.md)
* [Tutorial su Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=it)


Le modifiche e le aggiunte in AEM Sites come Cloud Service sono le seguenti:

* [Operazioni pagina asincrone](#asynchronous-page-operations)
* [Nuovo sito di riferimento e tutorial](#new-reference-site-and-tutorial)

## Operazioni pagina asincrone {#asynchronous-page-operations}

Nel servizio AEM Cloud, le operazioni che tradizionalmente hanno bloccato l’interfaccia utente sono state suddivise in attività più piccole che vengono eseguite in background.

* Sposta pagine
* Pagine di rollout

L’iniziatore di tali azioni può controllarne lo stato in una nuova interfaccia utente in `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
L’utente del sistema non deve apportare alcuna modifica per utilizzare questa nuova funzione. Si nota qui semplicemente come un cambiamento di comportamento rispetto alle versioni on-premise precedenti di AEM.

## Nuovo sito di riferimento e tutorial {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), un nuovo sito di riferimento AEM, è stato aggiornato e pubblicato per riflettere le best practice per la creazione di un sito web con AEM e l’insieme completo di funzionalità, componenti e modelli di distribuzione disponibili in AEM. Il nuovo sito di riferimento e l&#39; [tutorial di accompagnamento](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) riguardano argomenti fondamentali come la configurazione del progetto, i componenti core, i modelli modificabili, le librerie client e lo sviluppo di componenti con Adobe Experience Manager Sites.

In precedenza, We.Retail veniva installato per impostazione predefinita con AEM (tranne quando avviato in modalità di produzione).  Ora, un sito di riferimento non verrà installato per impostazione predefinita.  Vengono invece forniti i [git repo](https://github.com/adobe/aem-guides-wknd/) e [tutorial di accompagnamento](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) con il codice del sito di riferimento WKND aggiornato.

## Funzionalità non disponibili in Runtime {#capabilities-not-available-at-runtime}

AEM come Cloud Service è sempre attivo e sempre aggiornato. Per raggiungere questo obiettivo è necessaria la separazione dell’archivio AEM in contenuto immutabile e mutabile e il divieto di accesso a contenuto immutabile in fase di esecuzione. Per ulteriori dettagli sul contenuto variabile e immutabile, consulta [Aree variabili rispetto alle Aree immutabili del Repository](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

A causa dell’inaccessibilità del contenuto immutabile in fase di runtime, le seguenti operazioni di AEM Sites non sono disponibili in fase di runtime:

* Traduzione dizionario i18n
* Modalità sviluppatore nell’Editor pagina di AEM Sites

Queste funzionalità possono essere utilizzate tramite istanze di sviluppatori locali indipendenti di AEM come Cloud Service, per aggiornare contenuto e codice nel AEM come archivio GIT di Cloud Service, ma non in istanze di runtime in hosting.
