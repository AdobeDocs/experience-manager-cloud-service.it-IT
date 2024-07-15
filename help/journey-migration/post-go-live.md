---
title: Post-pubblicazione
description: Scopri come monitorare i problemi e migliorare le prestazioni
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 22%

---

# Post-pubblicazione {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Risoluzione dei problemi relativi ad AEM"
>abstract="Esamina le best practice per lo sviluppo continuo e gestisci i registri insieme a strumenti come la console per sviluppatori e CRXDE Lite per aiutarti a risolvere eventuali problemi relativi ad AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=it" text="Accesso e gestione dei registri"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=it#aem-as-a-cloud-service-development-tools" text="Strumenti di sviluppo in AEM as a Cloud Service"

Questo percorso è l’ultima parte, per consentirti di imparare a monitorare i problemi e migliorare le prestazioni al termine della migrazione. Assicurati che i file temporanei vengano eliminati, rivedi le best practice per lo sviluppo continuo e gestisci i registri.

## Percorso affrontato finora {#story-so-far}

Nel passaggio precedente del percorso, hai imparato a eseguire la migrazione e [Go-live](/help/journey-migration/go-live.md) una volta che il codice e il contenuto erano pronti per essere trasferiti ad AEM as a Cloud Service.

## Obiettivo {#objective}

Questo documento descrive gli strumenti disponibili per la risoluzione dei problemi relativi agli ambienti AEM as a Cloud Service:

* **Console per sviluppatori**
* **CRXDE Lite**
* **Gestione dei registri**

## Console di sviluppo {#developer-console}

Il debug degli ambienti per sviluppatori di AEM as a Cloud Service è disponibile in Developer Console per gli ambienti di sviluppo, stage e produzione.

Per ulteriori informazioni sugli strumenti di sviluppo, consulta [Implementazione per AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools).

## CRXDE Lite {#crxde-lite}

In qualità di utente, puoi accedere a CRXDE Lite nell’ambiente di sviluppo ma non in quello di stage o produzione.

>[!IMPORTANT]
>La scrittura in archivi immutabili come `/libs` e `/apps` in fase di runtime genera errori. Inoltre, non hai accesso agli strumenti per sviluppatori per gli ambienti di staging e produzione.

Consulta [Sviluppo con CRXDE Lite](/help/implementing/developing/tools/crxde.md) per ulteriori informazioni su come sviluppare l&#39;applicazione AEM utilizzando CRXDE Lite.

## Gestione dei registri {#managing-logs}

Gli utenti possono accedere a un elenco dei file di registro disponibili per l’ambiente selezionato.

Consulta [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md) per scoprire come accedere e gestire i registri tramite l&#39;interfaccia utente o dall&#39;API tramite Cloud Manager.

## Contattare il supporto {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Guida e supporto"
>abstract="Per eventuali domande o dubbi, contatta il Team di supporto AEM di Adobe."
>additional-url="https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html" text="Supporto per Experience Cloud"

Se hai domande sull&#39;accesso al Cloud Service, contatta il rappresentante dell&#39;Adobe o il [supporto per l&#39;Experience Cloud](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html) per maggiori dettagli.

## Apprendimenti documento {#document-learnings}

Una volta completata la migrazione, documenta le conoscenze acquisite durante questo processo. Alcune domande che potrebbero essere utili per il processo di documentazione sono:

* Cosa ha funzionato bene e cosa no?
* Quali erano i punti dolenti maggiori?
* Recommendations se è prevista una migrazione futura.

Condividi questi insegnamenti post-migrazione con le parti interessate e i team all’interno della tua organizzazione.

## Il percorso è terminato - Davvero? {#journey-ends}

Congratulazioni. Hai completato il Percorso di migrazione AEM as a Cloud Service. Devi sapere come:

* Introduzione al passaggio ad AEM as a Cloud Service
* Determinare se l’implementazione è pronta per essere spostata in AEM as a Cloud Service
* Prepara il codice e il contenuto cloud
* Eseguire la migrazione
* Monitora i problemi e migliora le prestazioni
