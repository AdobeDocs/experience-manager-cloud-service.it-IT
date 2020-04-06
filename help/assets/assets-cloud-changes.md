---
title: Notevoli modifiche in Risorse Adobe Experience Manager come servizio cloud
description: Notevoli modifiche alle risorse Adobe Experience Manager nel servizio AEM Cloud rispetto a Experience Manager 6.5
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager come servizio Cloud offre molte nuove funzionalità e possibilità per gestire i progetti AEM. Tuttavia, esistono diverse differenze tra Experience Manager Assets in sede o in Adobe Managed Service rispetto a Experience Manager come servizio Cloud. In questo documento sono illustrate le principali differenze.

>[!NOTE]
>
>Questo documento evidenzia le modifiche importanti specifiche di Experience Manager Assets come servizio Cloud. Vedi le [modifiche generiche a Experience Manager come servizio](/help/release-notes/aem-cloud-changes.md)Cloud.

Le principali differenze rispetto a Experience Manager 6.5 si trovano nelle seguenti aree:

* [Acquisizione delle risorse](#asset-ingestion)
* [Rimozione dell’interfaccia classica](#classic-ui)

## Acquisizione delle risorse {#asset-ingestion}

Il caricamento delle risorse è stato ottimizzato per essere più efficiente e consentire un ridimensionamento migliore dell’assimilazione delle risorse e caricamenti più rapidi. Sono state aggiornate le funzionalità dei prodotti (interfacce utente Web, client desktop). Tuttavia, questo può avere un impatto su alcuni codici personalizzati esistenti.

* Experience Manager utilizza il principio di accesso binario diretto per caricare e scaricare e i microservizi di risorse per l’elaborazione delle risorse. Consultate [panoramica dell’assimilazione delle risorse](/help/assets/asset-microservices-overview.md)
   * Caricamento delle risorse [con accesso binario diretto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)
   * Per informazioni tecniche, consultate Protocollo di caricamento binario [diretto e API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)
* Il flusso di lavoro predefinito **[!UICONTROL DAM Asset Update]** incluso nelle versioni precedenti di AEM non è più disponibile. Al contrario, i microservizi delle risorse forniscono un servizio scalabile e facilmente disponibile che copre la maggior parte dell’elaborazione predefinita delle risorse (rappresentazioni, estrazione dei metadati, estrazione del testo per l’indicizzazione)
   * Consultate [Configurazione e utilizzo dei microservizi delle risorse](/help/assets/asset-microservices-configure-and-use.md)
   * Per impostare i passaggi personalizzati del flusso di lavoro nell&#39;elaborazione, è possibile utilizzare i flussi di lavoro [di](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) post-elaborazione
* Le risorse incluse in Gestione pacchetti devono essere rielaborate manualmente tramite l’azione **[!UICONTROL Rielabora risorse]** nell’interfaccia di Assets.

Le rappresentazioni standard generate con i microservizi delle risorse vengono memorizzate in modo compatibile con le versioni precedenti nei nodi dell’archivio delle risorse (stesse convenzioni di denominazione).

## Sviluppare e testare microservizi per risorse {#developing-testing-asset-microservices}

Asset microservices è un servizio cloud nativo con provisioning e collegamento automatico a Experience Manager nei programmi cliente e negli ambienti gestiti in Cloud Manager. Gli sviluppatori che lavorano per estendere Experience Manager o che eseguono la personalizzazione possono utilizzare il contenuto esistente (o le risorse con rappresentazioni generate in un ambiente cloud) per testare e convalidare il codice utilizzando, visualizzando e scaricando le risorse.

Per eseguire una convalida end-to-end del codice e del processo, compresi l’assimilazione e l’elaborazione delle risorse, implementa le modifiche del codice in un ambiente di sviluppo cloud utilizzando la pipeline e verifica con l’esecuzione completa dell’elaborazione dei microservizi di risorse.

## Rimozione dell’interfaccia classica {#classic-ui}

L&#39;interfaccia classica non è più disponibile in Experience Manager come servizio Cloud.
