---
title: Modifiche di rilievo apportate ad Adobe Experience Manager (AEM) as a Cloud Service
description: Modifiche di rilievo apportate ad Adobe Experience Manager (AEM) as a Cloud Service.
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 100%

---

# Modifiche di rilievo apportate ad Adobe Experience Manager as a Cloud Service {#notable-changes-aem-cloud}

Adobe Experience Manager (AEM) Cloud Service include molte nuove funzioni e opportunità per gestire i progetti AEM. Tuttavia, ci sono alcune differenze tra AEM Sites on-premise o Adobe Managed Service e AEM Cloud Service. Questo documento illustra le principali differenze.

>[!CONTEXTUALHELP]
>id="aem_cloud_notable_changes"
>title="Modifiche importanti in AEM as a Cloud Service"
>abstract="In questa scheda, puoi visualizzare contenuti utili a comprendere le differenze tra AEM on-premise o in Adobe Managed Services rispetto ad AEM as a Cloud Service."
>additional-url="https://video.tv.adobe.com/v/330543" text="Evoluzione di AEM as a Cloud Service"


>[!NOTE]
>Questo documento illustra le modifiche di rilievo apportate ad AEM a livello generale. Per ulteriori informazioni e modifiche specifiche relative alla soluzione, consulta:
>
>* [Introduzione ad Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* [Novità e differenze](/help/overview/what-is-new-and-different.md) tra Adobe Experience Manager as a Cloud Service e le versioni precedenti
>* [Architettura](/help/overview/architecture.md) di Adobe Experience Manager as a Cloud Service
>* [Modifiche di rilievo apportate ad AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
>* [Modifiche di rilievo apportate ad AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)

Le principali differenze riguardano le seguenti aree:

* [/apps e /libs non sono modificabili in fase di esecuzione](#apps-libs-immutable)

* [I bundle e le configurazioni OSGi devono essere trattati come codice](#osgi)

* [Non sono consentite modifiche all’archivio di pubblicazione](#changes-to-publish-repo)

* [Non sono consentite modalità di esecuzione personalizzate](#custom-runmodes)

* [Rimozione degli agenti di replica e delle relative modifiche](#replication-agents)

* [Rimozione dell’interfaccia classica](#classic-ui)

* [Distribuzione lato pubblicazione](#publish-side-delivery)

* [Gestione e distribuzione delle risorse](#asset-handling)

## /apps e /libs non sono modificabili in fase di esecuzione {#apps-libs-immutable}

Tutti i contenuti e le sottocartelle in `/apps` e `/libs` sono di sola lettura. Non è possibile apportarvi modifiche mediante funzioni o codice personalizzato. Verrà restituito un errore per segnalare che il contenuto è di sola lettura e che l’operazione di scrittura non è stata completata. Ciò ha un impatto su diverse aree di AEM:

* Non sono consentite modifiche in `/libs`.
   * Questa non è una nuova regola, ma non veniva applicata nelle precedenti versioni on-premise di AEM.
* Le sovrapposizioni per le aree in `/libs` in cui è consentita la sovrapposizione sono ancora consentite all’interno di `/apps`.
   * Tali sovrapposizioni devono provenire da Git tramite la pipeline CI/CD.
* Le informazioni di progettazione dei modelli statici memorizzate in `/apps` non possono essere modificate tramite l’interfaccia utente.
   * In alternativa, si consiglia di usare i modelli modificabili.
   * Se è ancora necessario usare i modelli statici, le informazioni di configurazione devono provenire da Git tramite la pipeline CI/CD.
* Le configurazioni di rollout di blueprint MSM e MSM personalizzato devono essere installate da Git tramite la pipeline CI/CD.
* Le modifiche di traduzione I18N devono provenire da Git tramite la pipeline CI/CD.

## I bundle e le configurazioni OSGi devono essere trattati come codice {#osgi}

Le modifiche ai bundle e alle configurazioni OSGi devono essere introdotte tramite la pipeline CI/CD.

* I bundle OSGi nuovi o aggiornati devono essere introdotti tramite Git mediante la pipeline CI/CD.
* Le modifiche alle configurazioni OSGi possono provenire solo da Git tramite la pipeline CI/CD.

La console Web, utilizzata nelle versioni precedenti di AEM per modificare i bundle e le configurazioni OSGi, non è disponibile in AEM Cloud Service. 

## Non sono consentite modifiche all’archivio di pubblicazione {#changes-to-publish-repo}

A parte le modifiche nella cartella `/home` sul livello di pubblicazione, le modifiche dirette all’archivio di pubblicazione non sono consentite in AEM Cloud Service. Nelle versioni precedenti di AEM on-premise o AEM su AMS, era possibile apportare modifiche al codice direttamente nell’archivio di pubblicazione. Alcune limitazioni possono essere attenuate nei seguenti modi:

* Per i contenuti e la configurazione basata su contenuti: apporta le modifiche all’istanza di authoring e pubblicale
* Per il codice e la configurazione: apporta le modifiche nell’archivio GIT ed esegui la pipeline CI/CD per distribuirle.

## Non sono consentite modalità di esecuzione personalizzate {#custom-runmodes}

In AEM Cloud Service non sono possibili modalità di esecuzione aggiuntive o personalizzate. Per un elenco delle modalità di esecuzione disponibili per AEM Cloud Service, consulta [Distribuzione in AEM as a Cloud Service.](/help/implementing/deploying/overview.md#runmodes)

## Rimozione degli agenti di replica e delle relative modifiche {#replication-agents}

In AEM Cloud Service il contenuto viene pubblicato utilizzando la [Distribuzione dei contenuti Sling](https://sling.apache.org/documentation/bundles/content-distribution.html). Gli agenti di replica utilizzati nelle versioni precedenti di AEM non vengono più utilizzati o forniti. Questa limitazione potrebbe interessare le seguenti aree dei progetti AEM esistenti:

* Flussi di lavoro personalizzati che, ad esempio, inviano contenuti agli agenti di replica dei server di anteprima
* Personalizzazione degli agenti di replica per la trasformazione dei contenuti.
* Utilizzo della replica inversa per riportare i contenuti dall’ambiente di pubblicazione a quello di authoring.

Inoltre, i pulsanti di pausa e disattivazione sono stati rimossi dalla console di amministrazione dell’agente di replica.

## Rimozione dell’interfaccia classica {#classic-ui}

L’interfaccia classica non è più disponibile in AEM Cloud Service.

## Distribuzione lato pubblicazione {#publish-side-delivery}

L’accelerazione HTTP, compresa la gestione del traffico e la rete CDN per i servizi di authoring e pubblicazione, è inclusa per impostazione predefinita in AEM Cloud Service.

Per la transizione dei progetti da AMS o da un’installazione on-premise, Adobe consiglia vivamente di utilizzare la rete CDN incorporata, per la quale sono ottimizzate le funzioni incluse in AEM Cloud Service.

## Gestione e distribuzione delle risorse {#asset-handling}

Il caricamento, l’elaborazione e il download delle risorse sono ottimizzati in [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. AEM [!DNL Assets] è ora più efficiente, consente una maggiore scalabilità e offre velocità di caricamento e download molto più elevate. Inoltre, influisce sul codice personalizzato esistente e su alcune operazioni. Per un elenco delle modifiche e per il livello di parità con le funzioni di [!DNL Experience Manager] 6.5, vedi le [modifiche apportate a [!DNL Assets]](/help/assets/assets-cloud-changes.md).
