---
title: Modifiche di rilievo apportate ad AEM Sites in AEM Cloud Service
description: Comprendi come scrivere e amministrare AEM Sites as a Cloud Service, nonché conoscere le modifiche significative apportate ad AEM Sites in AEM Cloud Service.
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 3761019b42ddc4b3a6cc904afe91b47eb3d99ac6
workflow-type: ht
source-wordcount: '526'
ht-degree: 100%

---


# Modifiche di rilievo apportate ad AEM Sites as a Cloud Service {#notable-changes}

AEM Sites as a Cloud Service fornisce funzionalità di gestione delle esperienze come parte della piattaforma nativa per il cloud AEM as a Cloud Service. Oltre ai vantaggi principali di AEM as a Cloud Service, come la scalabilità nativa per il cloud, il tempo di attività e l’aggiornamento costante, AEM Sites as a Cloud Service fornisce anche alcune modifiche e aggiunte specifiche per Sites.

>[!NOTE]
>Questo documento evidenzia le modifiche di rilievo apportate ad AEM Sites. Per le modifiche generali di AEM as a Cloud Service e altri moduli, vedi:
>
>* [Introduzione ad Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* [Panoramica di AEM as a Cloud Service: novità e differenze](/help/overview/what-is-new-and-different.md)
>* [Architettura](/help/overview/architecture.md) di Adobe Experience Manager as a Cloud Service
>* [Modifiche di rilievo apportate ad AEM as a Cloud Service (Note sulla versione)](/help/release-notes/aem-cloud-changes.md)
>* [Modifiche di rilievo apportate ad AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
>* [Introduzione ad AEM Assets as a Cloud Service](/help/assets/overview.md)
>* [Tutorial su Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=it)

Le modifiche e le aggiunte in AEM Sites as a Cloud Service sono le seguenti:

* [Operazioni pagina asincrone](#asynchronous-page-operations)
* [Nuovo sito di riferimento e tutorial](#new-reference-site-and-tutorial)

## Operazioni pagina asincrone {#asynchronous-page-operations}

In AEM Cloud Service, le operazioni che tradizionalmente bloccavano l’interfaccia utente sono state suddivise in attività più piccole che vengono eseguite in background.

* Sposta pagine
* Rollout pagine

<!--
The initiator of such actions can check their status in a new UI at `/mnt/overlay/dam/gui/content/asyncjobs.html`.
-->

Puoi visualizzare lo stato dei processi asincroni dalla [dashboard Operazioni in background](/help/operations/asynchronous-jobs.md).

>[!NOTE]
>
>L’utente del sistema non deve apportare alcuna modifica per utilizzare questa nuova funzione. Questa nota indica semplicemente un cambiamento di comportamento rispetto alle versioni on-premise precedenti di AEM.

## Nuovo sito di riferimento e tutorial {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), un nuovo sito di riferimento AEM, è stato aggiornato e pubblicato per riflettere le best practice per la creazione di un sito web con AEM ed è dotato dell’insieme completo di funzionalità, componenti e modelli di distribuzione disponibili in AEM. Il nuovo sito, insieme al [tutorial di accompagnamento](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it), tratta argomenti fondamentali come la configurazione del progetto, i componenti core, i modelli modificabili, le librerie client e lo sviluppo di componenti con Adobe Experience Manager Sites.

In precedenza, We.Retail veniva installato per impostazione predefinita con AEM (tranne quando avviato in modalità di produzione). In AEM as a Cloud Service, per impostazione predefinita non viene installato un sito di riferimento. Invece, vengono forniti [archivio git](https://github.com/adobe/aem-guides-wknd/) e [tutorial di accompagnamento](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it) con il codice del sito di riferimento WKND aggiornato.

## Funzionalità non disponibili in fase di esecuzione {#capabilities-not-available-at-runtime}

AEM as a Cloud Service è sempre attivo e sempre aggiornato. Per raggiungere questo obiettivo è necessaria la separazione dell’archivio AEM in contenuto immutabile e mutabile e il divieto di accesso al contenuto immutabile in fase di esecuzione. Per maggiori dettagli sul contenuto mutabile o immutabile vedi [Aree variabili e immutabili dell’archivio](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

A causa dell’inaccessibilità del contenuto immutabile in fase di esecuzione, non sono disponibili le seguenti operazioni di AEM Sites:

* Traduzione dizionario i18n
* Modalità sviluppatore nell’Editor pagina di AEM Sites

Queste funzionalità possono essere utilizzate tramite istanze sviluppatore locali indipendenti di AEM as a Cloud Service, per aggiornare contenuto e codice nell’archivio GIT di AEM as a Cloud Service, ma non nelle istanze di esecuzione in hosting.
