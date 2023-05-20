---
title: Post-pubblicazione
description: Scopri come monitorare i problemi e migliorare le prestazioni
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 39%

---

# Post-pubblicazione {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Risoluzione dei problemi relativi ad AEM"
>abstract="Esamina le best practice per lo sviluppo continuo e gestisci i registri insieme a strumenti come la console per sviluppatori e CRXDE Lite per aiutarti a risolvere eventuali problemi relativi ad AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=it" text="Accesso e gestione dei registri"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=it#aem-as-a-cloud-service-development-tools" text="Strumenti di sviluppo in AEM as a Cloud Service"

Questa è l’ultima parte del percorso, dove imparerai a monitorare i problemi e a migliorare le prestazioni una volta completata la migrazione. Assicurati che i file temporanei vengano eliminati, rivedi le best practice per lo sviluppo continuo e gestisci i registri.

## Percorso affrontato finora {#story-so-far}

Nel passaggio precedente del percorso, hai imparato a eseguire la migrazione e [Go-live](/help/journey-migration/go-live.md) una volta che il codice e il contenuto erano pronti per essere trasferiti all’AEM as a Cloud Service.

## Obiettivo {#objective}

Questo documento descrive gli strumenti disponibili per la risoluzione dei problemi relativi agli ambienti AEM as a Cloud Service:

* **Console per sviluppatori**
* **CRXDE Lite**
* **Gestione dei registri**

## Console per sviluppatori {#developer-console}

Il debug degli ambienti per sviluppatori as a Cloud Service all’AEM è disponibile nella Console per sviluppatori per ambienti di sviluppo, stage e produzione.

Per ulteriori informazioni sugli strumenti di sviluppo, consulta [Implementazione per AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools).

## CRXDE Lite {#crxde-lite}

Come utente, puoi accedere a CRXDE Lite nell’ambiente di sviluppo ma non in quello di stage o produzione.

>[!IMPORTANT]
>Scrittura in archivi immutabili come `/libs` e `/apps` in fase di runtime genera errori. Inoltre, non hai accesso agli strumenti per sviluppatori per gli ambienti di staging e produzione.

Per informazioni su come sviluppare l’applicazione AEM utilizzando CRXDE Lite, consulta l’articolo sullo [sviluppo con CRXDE Lite](/help/implementing/developing/tools/crxde.md).

## Gestione dei registri {#managing-logs}

Gli utenti possono accedere a un elenco dei file di registro disponibili per l’ambiente selezionato.

Per informazioni su come accedere ai registri e gestirli attraverso l’interfaccia o l’API tramite Cloud Manager, consulta [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md).

## Contattare il supporto tecnico {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Guida e supporto"
>abstract="Per eventuali domande o dubbi, contatta il Team di supporto AEM."
>additional-url="https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html" text="Supporto per Experience Cloud"

Se hai domande sull’accesso al Cloud Service, contatta il rappresentante del tuo Adobe o [Supporto per Experience Cloud](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html) per ulteriori dettagli.

## Apprendimenti documento {#document-learnings}

Una volta completata la migrazione, devi documentare le conoscenze acquisite durante questo processo. Alcune domande che potrebbero essere utili per il processo di documentazione sono:

* Cosa ha funzionato bene e cosa no?
* Quali erano i punti dolenti maggiori?
* Recommendations in caso di migrazione futura.

Dovresti quindi condividere questi insegnamenti post-migrazione con le parti interessate e i team all’interno della tua organizzazione.

## Il percorso è terminato - Davvero? {#journey-ends}

Congratulazioni. Hai completato il Percorso di migrazione as a Cloud Service dell’AEM. Devi sapere come:

* Introduzione al passaggio a AEM as a Cloud Service
* Determinare se l’implementazione è pronta per essere spostata su AEM as a Cloud Service
* Prepara il codice e il contenuto cloud
* Eseguire la migrazione
* Monitora i problemi e migliora le prestazioni
