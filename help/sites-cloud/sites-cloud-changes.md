---
title: Modifiche di rilievo apportate ad AEM Sites in AEM Cloud Service
description: 'Modifiche di rilievo apportate ad AEM Sites in AEM Cloud Service '
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 21%

---


# Modifiche di rilievo apportate ad AEM Sites as a Cloud Service {#notable-changes}

 AEM Sites come Cloud Service fornisce funzionalità di gestione dell&#39;esperienza come parte del AEM nativo del cloud come piattaforma di Cloud Service. Oltre ai vantaggi principali di AEM come Cloud Service, come la scalabilità nativa del cloud, il tempo di attività e sempre aggiornato,  AEM Sites come Cloud Service fornisce anche una serie di modifiche e aggiunte specifiche a Siti.

>[!NOTE]
>In questo documento vengono evidenziate le modifiche rilevanti apportate  AEM Sites. Per le modifiche generali alla AEM come Cloud Service e altri moduli, vedere:
>
>* [Introduzione ad Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* [Panoramica di AEM as a Cloud Service: novità e differenze](/help/overview/what-is-new-and-different.md)
>* [Architettura](/help/core-concepts/architecture.md) di Adobe Experience Manager as a Cloud Service
>* [Modifiche di rilievo apportate ad AEM as a Cloud Service (Note sulla versione)](/help/release-notes/aem-cloud-changes.md)
>* [Modifiche di rilievo apportate ad AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
>* [Presentazione  AEM Assets come Cloud Service](/help/assets/overview.md)
>* [Tutorial su Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)


Le modifiche e le aggiunte  AEM Sites come Cloud Service sono le seguenti:

* [Operazioni asincrone sulle pagine](#asynchronous-page-operations)
* [Nuovo sito di riferimento ed esercitazione](#new-reference-site-and-tutorial)

## Operazioni asincrone sulle pagine {#asynchronous-page-operations}

Nel servizio AEM Cloud, le operazioni che tradizionalmente hanno bloccato l&#39;interfaccia utente sono state suddivise in attività più piccole che vengono eseguite in background.

* Spostare le pagine
* Pagine di rollout

L’iniziatore di tali azioni può controllarne lo stato in una nuova interfaccia in `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>L&#39;utente del sistema non deve apportare alcuna modifica per utilizzare questa nuova funzione. Si nota qui semplicemente come un cambiamento di comportamento rispetto alle versioni locali di AEM precedenti.

## Nuovo sito di riferimento ed esercitazione {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), un nuovo sito di riferimento AEM, è stato aggiornato e pubblicato in modo da riflettere le procedure ottimali per la creazione di un sito Web con AEM, e il set completo di funzionalità, componenti e modelli di distribuzione disponibili in AEM. Il nuovo sito di riferimento e l’ [esercitazione](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) che lo accompagna riguardano argomenti fondamentali come la configurazione del progetto, i componenti core, i modelli modificabili, le librerie client e lo sviluppo di componenti con  Adobe Experience Manager Sites.

In precedenza, We.Retail era installato per impostazione predefinita con AEM (tranne quando avviato in modalità di produzione).  Ora, per impostazione predefinita, un sito di riferimento non verrà installato.  Viene invece fornito [git repo](https://github.com/adobe/aem-guides-wknd/) e [l&#39;esercitazione](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) con il codice del sito di riferimento WKND aggiornato.

## Funzionalità non disponibili in Runtime {#capabilities-not-available-at-runtime}

AEM come Cloud Service è sempre attivo e sempre aggiornato. Per ottenere questo risultato è necessario separare l&#39;archivio AEM in contenuto immutabile e modificabile e impedire l&#39;accesso a contenuto immutabile in fase di esecuzione. Per ulteriori dettagli sul contenuto modificabile e immutabile, vedere Aree [variabile e non modificabili del repository](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

A causa dell&#39;impossibilità di accedere al contenuto immutabile in fase di esecuzione, le seguenti operazioni  AEM Sites non sono disponibili in fase di esecuzione:

* Traduzione dizionario i18n
* Modalità Sviluppatore in  AEM Sites Page Editor

Tali funzionalità possono essere utilizzate tramite istanze di sviluppatori locali e autonome di AEM come Cloud Service, per aggiornare contenuto e codice nella AEM come repository GIT di Cloud Service, ma non in istanze di runtime ospitate.
