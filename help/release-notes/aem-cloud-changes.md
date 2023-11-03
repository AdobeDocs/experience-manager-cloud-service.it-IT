---
title: Modifiche di rilievo apportate ad Adobe Experience Manager (AEM) as a Cloud Service
description: Modifiche di rilievo apportate ad Adobe Experience Manager (AEM) as a Cloud Service.
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: 30edc83364dd9666b94f54048abc8b7f92ad6ce3
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 49%

---

# Modifiche di rilievo apportate a Adobe Experience Manager as a Cloud Service {#notable-changes-aem-cloud}

Il Cloud Service Adobe Experience Manager (AEM) offre molte nuove funzioni e possibilità per la gestione dei progetti AEM. Tuttavia, esistono alcune differenze tra AEM Sites on-premise o in Adobe Managed Service e AEM Cloud Service. In questo documento sono illustrate le principali differenze.

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

* [I bundle e le configurazioni OSGi devono essere trattate come codice](#osgi)

* [Non sono consentite modifiche all’archivio di pubblicazione](#changes-to-publish-repo)

* [Non sono consentite modalità di esecuzione personalizzate](#custom-runmodes)

* [Rimozione degli agenti di replica e delle relative modifiche](#replication-agents)

* [Rimozione dell’interfaccia classica](#classic-ui)

* [Distribuzione lato pubblicazione](#publish-side-delivery)

* [Gestione e distribuzione delle risorse](#asset-handling)

## /apps e /libs non sono modificabili in fase di esecuzione {#apps-libs-immutable}

Qualsiasi contenuto e sottocartella in `/apps` e `/libs` è di sola lettura. Non è possibile apportare modifiche a una funzione o a un codice personalizzato. Verrà restituito un errore per segnalare che il contenuto è di sola lettura e che l’operazione di scrittura non è stata completata. Ciò ha un impatto su diversi settori dell&#39;AEM:

* Non sono consentite modifiche in `/libs`.
   * Questa non è una nuova regola, ma non è stata applicata nelle precedenti versioni on-premise dell’AEM.
* Sovrapposizioni per aree in `/libs` che possono essere sovrapposti sono ancora consentiti in `/apps`.
   * Tali sovrapposizioni devono provenire da Git tramite la pipeline CI/CD.
* Informazioni di progettazione del modello statico memorizzate in `/apps` non può essere modificato tramite l’interfaccia utente.
   * In alternativa, si consiglia di usare i modelli modificabili.
   * Se i modelli statici sono ancora necessari, le informazioni di configurazione devono provenire da Git tramite la pipeline CI/CD.
* Le configurazioni di rollout di blueprint MSM e MSM personalizzato devono essere installate da Git tramite la pipeline CI/CD.
* Le modifiche di traduzione I18N devono provenire da Git tramite la pipeline CI/CD.

## I bundle e le configurazioni OSGi devono essere trattate come codice {#osgi}

Le modifiche ai bundle e alle configurazioni OSGi devono essere introdotte tramite la pipeline CI/CD.

* I bundle OSGi nuovi o aggiornati devono essere introdotti tramite Git tramite la pipeline CI/CD.
* Le modifiche alle configurazioni OSGi possono provenire solo da Git tramite la pipeline CI/CD.

La console Web, utilizzata nelle versioni precedenti di AEM per modificare i bundle e le configurazioni OSGi, non è disponibile in AEM Cloud Service. 

## Non sono consentite modifiche all’archivio di pubblicazione {#changes-to-publish-repo}

A parte le modifiche nella cartella `/home` sul livello di pubblicazione, le modifiche dirette all’archivio di pubblicazione non sono consentite in AEM Cloud Service. Nelle versioni precedenti di AEM on-premise o AEM su AMS, era possibile apportare modifiche al codice direttamente nell’archivio di pubblicazione. Alcune limitazioni possono essere attenuate nei seguenti modi:

* Per i contenuti e la configurazione basata su contenuti: apporta le modifiche all’istanza di authoring e pubblicale.
* Per il codice e la configurazione: apporta le modifiche nell’archivio GIT ed esegui la pipeline CI/CD per distribuirle.

## Non sono consentite modalità di esecuzione personalizzate {#custom-runmodes}

In AEM Cloud Service non sono possibili modalità di esecuzione aggiuntive o personalizzate. Per un elenco delle modalità di esecuzione disponibili in AEM Cloud Service, consulta il documento [Distribuzione a AEM as a Cloud Service.](/help/implementing/deploying/overview.md#runmodes)

## Rimozione degli agenti di replica e delle relative modifiche {#replication-agents}

In AEM Cloud Service il contenuto viene pubblicato utilizzando il modulo [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html). Gli agenti di replica utilizzati nelle versioni precedenti dell’AEM non vengono più utilizzati o forniti, il che potrebbe interessare le seguenti aree dei progetti AEM esistenti:

* Flussi di lavoro personalizzati che, ad esempio, inviano contenuti agli agenti di replica dei server di anteprima
* Personalizzazione degli agenti di replica per la trasformazione dei contenuti.
* Utilizzo della replica inversa per riportare il contenuto dalla pubblicazione all’authoring.

Inoltre, i pulsanti di pausa e disattivazione vengono rimossi dalla console di amministrazione dell’agente di replica.

## Rimozione dell’interfaccia classica {#classic-ui}

L’interfaccia classica non è più disponibile in AEM Cloud Service.

## Distribuzione lato pubblicazione {#publish-side-delivery}

L’accelerazione HTTP, compresa la gestione del traffico e la rete CDN per i servizi Author e Publish, è disponibile per impostazione predefinita in AEM Cloud Service.

Per i progetti che passano da AMS a un’installazione on-premise, Adobe consiglia vivamente di utilizzare la rete CDN integrata, perché le funzioni all’interno di AEM Cloud Service sono ottimizzate per la rete CDN fornita.

## Gestione e distribuzione delle risorse {#asset-handling}

Il caricamento, l’elaborazione e il download delle risorse sono ottimizzati in [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. AEM [!DNL Assets] ora è più efficiente, consente una maggiore scalabilità e velocizza le operazioni di caricamento e download. Inoltre, influisce sul codice personalizzato esistente e su alcune operazioni. Per un elenco delle modifiche e per il livello di parità con le funzioni di [!DNL Experience Manager] 6.5, vedi le [modifiche apportate a [!DNL Assets]](/help/assets/assets-cloud-changes.md).
