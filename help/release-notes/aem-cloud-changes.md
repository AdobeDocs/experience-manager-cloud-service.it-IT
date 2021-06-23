---
title: Modifiche di rilievo apportate ad Adobe Experience Manager (AEM) as a Cloud Service
description: Modifiche di rilievo apportate ad Adobe Experience Manager (AEM) as a Cloud Service
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: cff7454e2b6a1d55accef31d20d85378f08dfe0c
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 82%

---

# Modifiche di rilievo apportate ad Adobe Experience Manager (AEM) as a Cloud Service {#notable-changes-aem-cloud}

AEM Cloud Service include molte nuove funzioni e opportunità per gestire i progetti AEM. Tuttavia, esistono diverse differenze tra la versione on-premise di AEM Sites o Adobe Managed Services e AEM Cloud Service. In questo documento sono illustrate le principali differenze.

>[!CONTEXTUALHELP]
>id="aem_cloud_notable_changes"
>title="Modifiche di rilievo in AEM come Cloud Service"
>abstract="In questa scheda, puoi visualizzare il contenuto che ti aiuterà a comprendere le differenze tra AEM on-premise o in Adobe Managed Services, rispetto a AEM come Cloud Service."
>additional-url="https://video.tv.adobe.com/v/330543" text="Evoluzione del AEM come Cloud Service"


>[!NOTE]
>In questo documento sono illustrate le modifiche di rilievo apportate ad AEM a livello generale. Per ulteriori informazioni e modifiche specifiche relative alla soluzione, vedi:
>
>* [Introduzione ad Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* [Novità e differenze](/help/overview/what-is-new-and-different.md) tra Adobe Experience Manager as a Cloud Service e le versioni precedenti
* [Architettura](/help/core-concepts/architecture.md) di Adobe Experience Manager as a Cloud Service
* [Modifiche di rilievo apportate ad AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
* [Modifiche di rilievo apportate ad AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)


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

Oltre alle modifiche nella cartella `/home` sul livello di pubblicazione, le modifiche dirette all’archivio di pubblicazione non sono consentite AEM Cloud Service. Nelle versioni precedenti di AEM on-premise o AEM su AMS, è possibile apportare modifiche al codice direttamente nell’archivio di pubblicazione. Alcune limitazioni possono essere attenuate nei seguenti modi:

* Per i contenuti e la configurazione basata su contenuti: apporta le modifiche all’istanza di authoring e pubblicale.
* Per il codice e la configurazione: apporta le modifiche nell’archivio GIT ed esegui la pipeline CI/CD per distribuirle.

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

Il caricamento, l’elaborazione e il download delle risorse sono ottimizzati in Experience Manager Assets come Cloud Service. Ora è più efficiente, consente di eseguire caricamenti e download più veloci e scalare i contenuti. Inoltre, influisce sul codice personalizzato esistente e su alcune operazioni. Vedere le [modifiche a [!DNL Assets]](/help/assets/assets-cloud-changes.md).
