---
title: Notevoli modifiche ad Adobe Experience Manager (AEM) come servizio Cloud
description: Notevoli modifiche ad Adobe Experience Manager (AEM) come servizio Cloud
translation-type: tm+mt
source-git-commit: e76de9b84931dced6383570e384ffdb6fb334daf

---


# Notevoli modifiche ad Adobe Experience Manager (AEM) come servizio Cloud {#notable-changes-aem-cloud}

Il servizio AEM Cloud offre molte nuove funzioni e possibilità per gestire i progetti AEM. Tuttavia, esistono diverse differenze tra AEM Sites in sede o in Adobe Managed Service rispetto al servizio AEM Cloud. Questo documento evidenzia le differenze importanti.

>[!NOTE]
>Questo documento evidenzia le modifiche importanti apportate ad AEM nel suo insieme. Per modifiche specifiche alla soluzione, vedi:
>
>* [Notevoli modifiche ad AEM Sites nel servizio AEM Cloud](/help/sites-cloud/sites-cloud-changes.md)
>* [Notevoli modifiche a Risorse AEM nel servizio AEM Cloud](/help/assets/assets-cloud-changes.md)


Le principali differenze si riscontrano nei seguenti settori:

* [/apps e /libs sono immutabili in fase di esecuzione](#apps-libs-immutable)
* [I bundle e le impostazioni OSGi devono essere basati su repository](#osgi)
* [Le modifiche all&#39;archivio di pubblicazione non sono consentite](#changes-to-publish-repo)
* [Modalità di esecuzione personalizzate non consentite](#custom-runmodes)
* [Rimozione degli agenti di replica](#replication-agents)
* [Rimozione dell’interfaccia classica](#classic-ui)
* [Distribuzione lato pubblicazione](#publish-side-delivery)
* [Gestione e distribuzione delle risorse](#asset-handling)

## /apps e /libs sono immutabili in fase di esecuzione {#apps-libs-immutable}

Qualsiasi contenuto e sottocartelle in `/apps` e `/libs` è di sola lettura. Eventuali funzioni o codici personalizzati che prevedono di apportare modifiche non riusciranno a farlo. Viene restituito un errore che indica che il contenuto è di sola lettura e che l&#39;operazione di scrittura non è stata completata. Questo ha un impatto in diverse aree di AEM:

* Non `/libs` sono consentite modifiche.
   * Questa non è una nuova regola, ma non è stata applicata nelle versioni locali precedenti di AEM.
* Le sovrapposizioni per le aree in `/libs` cui è consentita la sovrapposizione sono ancora consentite all&#39;interno `/apps`.
   * Tali sovrapposizioni devono provenire da Git attraverso la pipeline CI/CD.
* Le informazioni di progettazione dei modelli statici memorizzate in `/apps` non possono essere modificate tramite l&#39;interfaccia utente.
   * È consigliabile utilizzare i modelli modificabili.
   * Se i modelli statici sono ancora richiesti, le informazioni di configurazione devono provenire da Git tramite la pipeline CI/CD.
* Le configurazioni MSM Blueprint e MSM rollout personalizzate devono essere installate da Git tramite la pipeline CI/CD.
* I18n cambiamenti di traduzione devono provenire da Git attraverso la pipeline CI/CD.

## I bundle e le impostazioni OSGi devono essere basati su repository {#osgi}

La console Web, utilizzata nelle versioni precedenti di AEM per modificare le impostazioni OSGi, non è disponibile in AEM Cloud Service. Pertanto, le modifiche al sistema OSGi devono essere introdotte attraverso la pipeline CI/CD.

* Le modifiche alle impostazioni OSGi possono essere apportate solo tramite la persistenza Git come impostazioni OSGi basate su JCR.
* I pacchetti OSGi nuovi o aggiornati devono essere introdotti tramite Git nell’ambito del processo di creazione della pipeline CI/CD.

## Le modifiche all&#39;archivio di pubblicazione non sono consentite {#changes-to-publish-repo}

Le modifiche dirette all&#39;archivio di pubblicazione non sono consentite su AEM Cloud Service. Nelle versioni precedenti di AEM o AEM locale su AMS, era possibile apportare modifiche al codice direttamente nell’archivio di pubblicazione, ad esempio per creare utenti, aggiornare il profilo utente e creare nodi. Questo non è più possibile e può essere attenuato nei seguenti modi:

* Per la configurazione basata su contenuto e contenuto: apportate le modifiche all’istanza di creazione e pubblicatele.
* Per codice e configurazione: apportare le modifiche nel repository GIT ed eseguire la pipeline CI/CD per distribuirla.
* Per dati relativi all&#39;utente quali l&#39;invio del modulo o i dati del profilo: usa il servizio di profilo unificato dalla piattaforma Experience Cloud o da un altro archivio di informazioni sulle sessioni di terze parti.

## Modalità di esecuzione personalizzate non consentite {#custom-runmodes}

Per il servizio AEM Cloud sono disponibili le seguenti modalità di esecuzione:

* `author`
* `publish`
* `prod`
* `author.prod`
* `publish.prod`
* `stage`
* `author.stage`
* `publish.stage`
* `dev`
* `author.dev`
* `publish.dev`

In AEM Cloud Service non sono possibili modalità di esecuzione aggiuntive o personalizzate.

## Rimozione degli agenti di replica {#replication-agents}

Nel servizio AEM Cloud, il contenuto viene pubblicato utilizzando [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html). Gli agenti di replica utilizzati nelle versioni precedenti di AEM non vengono più utilizzati o forniti, il che potrebbe interessare le seguenti aree dei progetti AEM esistenti:

* Flussi di lavoro personalizzati che inviano contenuti agli agenti di replica dei server di anteprima, ad esempio.
* Personalizzazione degli agenti di replica per trasformare il contenuto
* Utilizzo della replica inversa per riportare i contenuti dalla pubblicazione all&#39;autore

## Rimozione dell’interfaccia classica {#classic-ui}

L&#39;interfaccia classica non è più disponibile nel servizio AEM Cloud.

## Distribuzione lato pubblicazione {#publish-side-delivery}

L’accelerazione HTTP, compresa la CDN e la gestione del traffico per i servizi di creazione e pubblicazione, è fornita per impostazione predefinita in AEM Cloud Service.

Per la transizione di un progetto da AMS o da un’installazione locale, Adobe consiglia vivamente di sfruttare la rete CDN integrata, perché le funzioni del servizio AEM Cloud sono ottimizzate per la rete CDN fornita.

## Gestione e distribuzione delle risorse {#asset-handling}

Il caricamento, il trattamento e il download delle risorse sono stati ottimizzati in AEM Cloud Service in modo da renderne più efficiente il ridimensionamento e velocizzare i caricamenti e i download. Tuttavia, questo potrebbe avere un impatto su alcuni codici personalizzati esistenti.

* Il flusso di lavoro predefinito Aggiornamento **risorse** DAM nelle versioni precedenti di AEM non è più disponibile.
* I componenti del sito Web che forniscono un binario **senza trasformazione** devono utilizzare il download diretto.
   * Il servlet Sling GET è stato modificato per impostazione predefinita.
* I componenti del sito Web che forniscono un binario **con trasformazione** (ad esempio, ridimensiona tramite servlet) possono continuare a funzionare correttamente.
* Per le risorse incluse in Gestione pacchetti è necessaria la rielaborazione manuale tramite l’azione **Rielabora risorsa** nell’interfaccia Risorse.
