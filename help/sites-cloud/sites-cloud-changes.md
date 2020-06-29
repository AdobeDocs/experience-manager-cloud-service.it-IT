---
title: Modifiche di rilievo apportate ad AEM Sites in AEM Cloud Service
description: 'Modifiche di rilievo apportate ad AEM Sites in AEM Cloud Service '
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 16%

---


# Modifiche di rilievo apportate ad AEM Sites as a Cloud Service {#notable-changes}

I AEM Sites come Cloud Service offrono funzionalità di gestione dell&#39;esperienza come parte di AEM nativo del cloud come piattaforma Cloud Service. Oltre ai vantaggi di base di AEM come Cloud Service, come la scalabilità nativa del cloud, il tempo di attività e sempre aggiornato, AEM Sites come Cloud Service fornisce anche una serie di modifiche e aggiunte specifiche a Siti.

>[!NOTE]
>Questo documento evidenzia le modifiche rilevanti apportate ai AEM Sites. Per le modifiche generali ad AEM come Cloud Service e ad altri moduli, vedi:
>
>* [Introduzione ad Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* Una [panoramica di AEM come Cloud Service - Novità e differenze](/help/overview/what-is-new-and-different.md)
>* [Architettura](/help/core-concepts/architecture.md) di Adobe Experience Manager as a Cloud Service
>* [Notevoli modifiche ad AEM come Cloud Service (Note sulla versione)](/help/release-notes/aem-cloud-changes.md)
>* [Modifiche di rilievo apportate ad AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
>* [Presentazione dei AEM Assets come Cloud Service](/help/assets/overview.md)
>* [Esercitazioni su Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)


Le modifiche e le aggiunte in AEM Sites come Cloud Service sono le seguenti:

* [Operazioni asincrone sulle pagine](#asynchronous-page-operations)
* [Nuovo sito di riferimento ed esercitazione](#new-reference-site-and-tutorial)

## Operazioni asincrone sulle pagine {#asynchronous-page-operations}

Nel servizio AEM Cloud, le operazioni che tradizionalmente hanno bloccato l&#39;interfaccia utente sono state suddivise in attività più piccole che vengono eseguite in background.

* Spostare le pagine
* Pagine di rollout

L’iniziatore di tali azioni può controllarne lo stato in una nuova interfaccia in `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>L&#39;utente del sistema non deve apportare alcuna modifica per utilizzare questa nuova funzione. Qui si tratta semplicemente di un cambiamento di comportamento rispetto alle versioni locali precedenti di AEM.

## Nuovo sito di riferimento ed esercitazione {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), un nuovo sito di riferimento di AEM, è stato aggiornato e pubblicato in modo da riflettere le procedure ottimali per la creazione di un sito Web con AEM e il set completo di funzionalità, componenti e modelli di implementazione disponibili in AEM. Il nuovo sito di riferimento e [l’esercitazione](https://docs.adobe.com/content/help/it-IT/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) che lo accompagna riguardano argomenti fondamentali come la configurazione del progetto, i componenti core, i modelli modificabili, le librerie client e lo sviluppo di componenti con  Siti di Adobe Experience Manager.

In precedenza, We.Retail veniva installato per impostazione predefinita con AEM (tranne quando veniva avviato in modalità di produzione).  Ora, per impostazione predefinita, un sito di riferimento non verrà installato.  Viene invece fornito [git repo](https://github.com/adobe/aem-guides-wknd/) e [l&#39;esercitazione](https://docs.adobe.com/content/help/it-IT/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) con il codice del sito di riferimento WKND aggiornato.

## Funzionalità non disponibili in Runtime {#capabilities-not-available-at-runtime}

AEM come Cloud Service è sempre attivo e sempre aggiornato. Per ottenere questo risultato, è necessario separare l’archivio AEM da contenuti immutabili e modificabili e impedire l’accesso a contenuti immutabili in fase di esecuzione. Per ulteriori dettagli sul contenuto modificabile e immutabile, vedere Aree [variabile e non modificabili del repository](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

A causa dell&#39;impossibilità di accedere al contenuto immutabile in fase di esecuzione, le seguenti operazioni sui AEM Sites non sono disponibili in fase di esecuzione:

* Traduzione dizionario i18n
* Modalità Sviluppatore nell’Editor pagina AEM Sites

Queste funzionalità possono essere utilizzate tramite istanze di sviluppatori locali e autonome di AEM come Cloud Service, per aggiornare contenuto e codice in AEM come repository Cloud Service GIT, ma non in istanze di runtime ospitate.
