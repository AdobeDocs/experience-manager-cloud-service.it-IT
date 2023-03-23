---
title: Post-pubblicazione
description: Scopri come monitorare i problemi e migliorare le prestazioni
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 25%

---

# Post-pubblicazione {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Risoluzione dei problemi AEM"
>abstract="Rivedi le best practice per lo sviluppo continuo e gestisci i registri insieme a strumenti come Developer Console e CRXDE Lite per aiutarti a risolvere i problemi relativi a AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="Accesso e gestione dei registri"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM strumenti di sviluppo as a Cloud Service"

Questa è l’ultima parte del percorso e imparerai come monitorare i problemi e migliorare le prestazioni una volta completata la migrazione. È necessario garantire la pulizia dei file temporanei, esaminare le best practice per lo sviluppo continuo e gestire i registri.

## Percorso affrontato finora {#story-so-far}

Nel passaggio precedente del percorso, hai imparato a eseguire la migrazione e [Vai in diretta](/help/journey-migration/go-live.md) una volta che il codice e il contenuto erano pronti per essere spostati in AEM as a Cloud Service.

## Obiettivo {#objective}

Questo documento descrive gli strumenti disponibili per la risoluzione dei problemi AEM ambienti as a Cloud Service:

* **Console per sviluppatori**
* **CRXDE Lite**
* **Gestione dei registri**

## Console per sviluppatori {#developer-console}

Il debug AEM ambienti di sviluppatori as a Cloud Service è disponibile in Developer Console per ambienti di sviluppo, stage e produzione.

Per ulteriori informazioni sugli strumenti di sviluppo, consulta [Implementazione per AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools).

## CRXDE Lite {#crxde-lite}

Come utente, puoi accedere a CRXDE Lite nell’ambiente di sviluppo ma non in quello di stage o produzione.

>[!IMPORTANT]
>Scrittura in archivi immutabili quali `/libs` e `/apps` in fase di runtime genera errori. Inoltre, non puoi accedere agli strumenti per sviluppatori per gli ambienti di staging e produzione.

Per informazioni su come sviluppare l’applicazione AEM utilizzando CRXDE Lite, consulta l’articolo sullo [sviluppo con CRXDE Lite](/help/implementing/developing/tools/crxde.md).

## Gestione dei registri {#managing-logs}

Gli utenti possono accedere a un elenco dei file di registro disponibili per l’ambiente selezionato.

Per informazioni su come accedere ai registri e gestirli attraverso l’interfaccia o l’API tramite Cloud Manager, consulta [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md).

## Contattare il supporto {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Aiuto e supporto"
>abstract="Rivolgiti al nostro team di supporto AEM per ottenere chiarimenti o per risolvere eventuali problemi."
>additional-url="https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html" text="Supporto per Experience Cloud"

Per domande sull&#39;accesso al Cloud Service, contatta il tuo rappresentante Adobe o [Supporto per Experience Cloud](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html) per ulteriori dettagli.

## Imparazioni dei documenti {#document-learnings}

Una volta completata la migrazione, devi documentare le conoscenze acquisite durante questo processo. Alcune domande che potrebbero essere utili per il processo di documentazione sono:

* Cosa ha funzionato bene e cosa non ha funzionato?
* Quali erano i punti dolenti principali?
* Recommendations in caso di migrazione futura.

A questo punto, condividi questi insegnamenti post-migrazione con le parti interessate e i team all’interno della tua organizzazione.

## Il percorso è terminato - Davvero? {#journey-ends}

Congratulazioni. Hai completato il AEM Percorso di migrazione as a Cloud Service! Devi comprendere come:

* Guida introduttiva al passaggio a AEM as a Cloud Service
* Determina se la distribuzione è pronta per essere spostata in AEM as a Cloud Service
* Preparare il codice e il cloud dei contenuti
* Eseguire la migrazione
* Monitoraggio dei problemi e miglioramento delle prestazioni
