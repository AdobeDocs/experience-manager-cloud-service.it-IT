---
title: Modifiche di rilievo apportate ad Adobe Experience Manager (AEM) as a Cloud Service
description: Modifiche di rilievo apportate ad Adobe Experience Manager (AEM) as a Cloud Service
translation-type: ht
source-git-commit: e76de9b84931dced6383570e384ffdb6fb334daf

---


# Modifiche di rilievo apportate ad Adobe Experience Manager (AEM) as a Cloud Service {#notable-changes-aem-cloud}

AEM Cloud Service include molte nuove funzioni e opportunità per gestire i progetti AEM. Tuttavia, esistono diverse differenze tra la versione on-premise di AEM Sites o Adobe Managed Services e AEM Cloud Service. In questo documento sono illustrate le principali differenze.

>[!NOTE]
>In questo documento sono illustrate le modifiche di rilievo apportate ad AEM a livello generale. Per informazioni sulle modifiche specifiche delle soluzioni, consulta:
>
>* [Modifiche di rilievo apportate ad AEM Sites in AEM Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
>* [Modifiche di rilievo apportate ad AEM Assets in AEM Cloud Service](/help/assets/assets-cloud-changes.md)


Le principali differenze riguardano le seguenti aree:

* [/apps e /libs non sono modificabili in fase di esecuzione](#apps-libs-immutable)
* [I bundle e le impostazioni OSGi devono essere basati su archivio](#osgi)
* [Non sono consentite modifiche all’archivio di pubblicazione](#changes-to-publish-repo)
* [Non sono consentite modalità di esecuzione personalizzate](#custom-runmodes)
* [Rimozione degli agenti di replica](#replication-agents)
* [Rimozione dell’interfaccia classica](#classic-ui)
* [Distribuzione lato pubblicazione](#publish-side-delivery)
* [Gestione e distribuzione delle risorse](#asset-handling)

## /apps e /libs non sono modificabili in fase di esecuzione {#apps-libs-immutable}

Tutti i contenuti e le sottocartelle in `/apps` e `/libs` sono di sola lettura. Non è possibile apportarvi modifiche mediante funzioni o codice personalizzato. Verrà restituito un errore per segnalare che il contenuto è di sola lettura e che l’operazione di scrittura non è stata completata. Questa modifica interessa diverse aree di AEM:

* Non sono consentite modifiche in `/libs`.
   * Questa non è una nuova regola, ma non veniva applicata nelle versioni on-premise precedenti di AEM.
* Le sovrapposizioni per le aree in `/libs` in cui è consentita la sovrapposizione sono ancora consentite in `/apps`.
   * Tali sovrapposizioni devono provenire da Git tramite la pipeline CI/CD.
* Le informazioni di progettazione dei modelli statici memorizzate in `/apps` non possono essere modificate tramite l’interfaccia.
   * In alternativa, puoi sfruttare i modelli modificabili.
   * Se i modelli statici sono ancora necessari, le informazioni di configurazione devono provenire da Git tramite la pipeline CI/CD.
* Le configurazioni di rollout di blueprint MSM e MSM personalizzato devono essere installate da Git tramite la pipeline CI/CD.
* Le modifiche per la traduzione I18N devono provenire da Git tramite la pipeline CI/CD.

## I bundle e le impostazioni OSGi devono essere basati su archivio {#osgi}

La console web, utilizzata nelle versioni precedenti di AEM per modificare le impostazioni OSGi, non è disponibile in AEM Cloud Service, di conseguenza le modifiche apportate al sistema OSGi devono essere introdotte tramite la pipeline CI/CD.

* Le modifiche alle impostazioni OSGi possono essere apportate solo tramite la persistenza Git sotto forma di impostazioni OSGi basate su JCR.
* I bundle OSGi nuovi o aggiornati devono essere introdotti tramite Git nell’ambito del processo di creazione della pipeline CI/CD.

## Non sono consentite modifiche all’archivio di pubblicazione {#changes-to-publish-repo}

Le modifiche dirette nell’archivio di pubblicazione non sono consentite in AEM Cloud Service. Nelle versioni precedenti di AEM on-premise o di AEM in AMS era possibile apportare modifiche al codice direttamente nell’archivio di pubblicazione, ad esempio per creare utenti, aggiornare il profilo utente e creare nodi. Questo non è più possibile, ma puoi ovviare a questa limitazione nei seguenti modi:

* Per i contenuti e la configurazione basata su contenuti: apporta le modifiche all’istanza di authoring e pubblicale.
* Per il codice e la configurazione: apporta le modifiche nell’archivio GIT ed esegui la pipeline CI/CD per distribuirle.
* Per dati correlati all’utente, quali invii di moduli o dati del profilo: usa il servizio Unified Profile di Experience Cloud Platform o un altro archivio di informazioni sulle sessioni di terze parti.

## Non sono consentite modalità di esecuzione personalizzate {#custom-runmodes}

Con AEM Cloud Service sono disponibili le seguenti modalità di esecuzione:

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

In AEM Cloud Service il contenuto viene pubblicato utilizzando il modulo [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html). Gli agenti di replica utilizzati nelle versioni precedenti di AEM non vengono più utilizzati o forniti. Questa limitazione potrebbe interessare le seguenti aree dei progetti AEM esistenti:

* Flussi di lavoro personalizzati che, ad esempio, inviano contenuti agli agenti di replica dei server di anteprima
* Personalizzazione degli agenti di replica per la trasformazione dei contenuti
* Utilizzo della replica inversa per riportare i contenuti dall’ambiente di pubblicazione a quello di authoring

## Rimozione dell’interfaccia classica {#classic-ui}

L’interfaccia classica non è più disponibile in AEM Cloud Service.

## Distribuzione lato pubblicazione {#publish-side-delivery}

L’accelerazione HTTP, compresa la gestione del traffico e la rete CDN per i servizi di authoring e pubblicazione, è inclusa per impostazione predefinita in AEM Cloud Service.

Per la transizione dei progetti da AMS o da un’installazione on-premise, Adobe consiglia vivamente di utilizzare la rete CDN integrata, per la quale sono ottimizzate le funzioni incluse in AEM Cloud Service.

## Gestione e distribuzione delle risorse {#asset-handling}

Il caricamento, il trattamento e il download delle risorse sono stati ottimizzati in AEM Cloud Service in modo da ottimizzarne la scalabilità e velocizzare le operazioni di upload e download. Tuttavia, questo comportamento potrebbe influire su eventuale codice personalizzato esistente.

* Il flusso di lavoro predefinito **DAM Asset Update** incluso nelle versioni precedenti di AEM non è più disponibile.
* I componenti del sito web che forniscono un binario **senza trasformazione** devono utilizzare il download diretto.
   * Il servlet GET di Sling è stato modificato in modo da eseguire questa operazione per impostazione predefinita.
* I componenti del sito web che forniscono un binario **con trasformazione**, ad esempio il ridimensionamento tramite servlet, continuano a funzionare normalmente.
* Le risorse incluse in Gestione pacchetti devono essere rielaborate manualmente tramite l’azione **Rielabora risorse** nell’interfaccia di Assets.
