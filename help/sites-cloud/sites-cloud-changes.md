---
title: Notevoli modifiche ai siti AEM nel servizio AEM Cloud
description: 'Notevoli modifiche ai siti AEM nel servizio AEM Cloud '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Notevoli modifiche ai siti AEM come servizio cloud {#notable-changes}

AEM Sites as a Cloud Service offre funzionalità di gestione dell&#39;esperienza come parte di AEM nativo del cloud come piattaforma di servizio cloud. Oltre ai vantaggi di base di AEM come servizio cloud, come la scalabilità nativa del cloud, il tempo di attività e sempre aggiornato, AEM Sites as a Cloud Service offre anche una serie di modifiche e aggiunte specifiche a Siti.

>[!NOTE]
>Questo documento evidenzia le modifiche importanti apportate a AEM Sites. Per le modifiche generali ad AEM in Cloud vedi:
>
>* [Notevoli modifiche ad Adobe Experience Manager (AEM) come servizio Cloud](/help/release-notes/aem-cloud-changes.md)


Le modifiche e le aggiunte in AEM Sites come servizio cloud sono le seguenti:

* [Operazioni asincrone sulle pagine](#asynchronous-page-operations)
* [Nuovo sito di riferimento ed esercitazione](#new-reference-site-and-tutorial)

## Operazioni asincrone sulle pagine {#asynchronous-page-operations}

Nel servizio AEM Cloud, le operazioni che tradizionalmente hanno bloccato l&#39;interfaccia utente sono state suddivise in attività più piccole eseguite in background.

* Spostare le pagine
* Pagine di rollout

L’iniziatore di tali azioni può controllarne lo stato in una nuova interfaccia in `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>L&#39;utente del sistema non deve apportare alcuna modifica per utilizzare questa nuova funzione. Qui si tratta semplicemente di un cambiamento di comportamento rispetto alle versioni locali precedenti di AEM.

## Nuovo sito di riferimento ed esercitazione {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), un nuovo sito di riferimento di AEM, è stato aggiornato e pubblicato in modo da riflettere le procedure ottimali per la creazione di un sito Web con AEM e il set completo di funzionalità, componenti e modelli di implementazione disponibili in AEM. Il nuovo sito di riferimento e l&#39; [esercitazione](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) che lo accompagna riguardano argomenti fondamentali come la configurazione del progetto, i componenti core, i modelli modificabili, le librerie client e lo sviluppo di componenti con Adobe Experience Manager Sites.

In precedenza, We.Retail veniva installato per impostazione predefinita con AEM (tranne quando veniva avviato in modalità di produzione).  Ora, per impostazione predefinita, un sito di riferimento non verrà installato.  Viene invece fornito [git repo](https://github.com/adobe/aem-guides-wknd/) e [l&#39;esercitazione](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) con il codice del sito di riferimento WKND aggiornato.

## Funzionalità non disponibili in Runtime {#capabilities-not-available-at-runtime}

AEM come servizio cloud è sempre attivo e sempre aggiornato. Per ottenere questo risultato, è necessario separare l’archivio AEM da contenuti immutabili e modificabili e impedire l’accesso a contenuti immutabili in fase di esecuzione. Per ulteriori dettagli sul contenuto modificabile e immutabile, vedere Aree [variabile e non modificabili del repository](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

A causa dell&#39;impossibilità di accedere a contenuti immutabili in fase di esecuzione, le seguenti operazioni di AEM Sites non sono disponibili in fase di esecuzione:

* Traduzione dizionario i18n
* Modalità Sviluppatore nell’Editor pagina di AEM Sites

Queste funzionalità possono essere utilizzate tramite istanze di sviluppatori locali e autonome di AEM come servizio cloud, per aggiornare contenuto e codice in AEM come repository GIT di Servizi cloud, ma non in istanze runtime ospitate.
