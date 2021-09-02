---
title: Scopri cosa è Cloud Manager
description: Leggi questa pagina per saperne di più su Cloud Manager, sui programmi e sugli ambienti di Cloud Manager.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 4d1d6357e26e8c3ffbadfcae99f7ae7a091db1d3
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Introduzione a Cloud Manager {#intro-cloud-manager}

Cloud Manager è un componente essenziale di AEM come Cloud Service e funge da punto di ingresso unico per il tuo team.

Per supportare i clienti con configurazioni di sviluppo aziendali, AEM as a Cloud Service si integra completamente con Cloud Manager e le sue pipeline CI/CD appositamente progettate, che sono dotate per garantire test approfonditi e la massima qualità del codice per fornire esperienze eccezionali.

Per garantire che i clienti possano iniziare rapidamente con AEM come Cloud Service, Cloud Manager fornisce tutto il necessario per iniziare a utilizzare i servizi self-service, inclusa la possibilità di creare risorse e ambienti cloud. In questo modo, i tuoi sviluppatori AEM possono accedere all’archivio Git tramite Cloud Manager. Utilizzando Cloud Manager, i team di sviluppo possono lavorare spesso per eseguire modifiche in modo autonomo.

L’amministratore di sistema sarà responsabile della configurazione del team Cloud Manager, che includerà singoli utenti che creeranno le risorse cloud e gli sviluppatori. Per informazioni sul supporto di Cloud Manager nell&#39;installazione di Enterprise Team Development, consulta [Configurazione di sviluppo team per AEM come Cloud Service](/help/implementing/cloud-manager/enterprise-team-dev-setup.md) .

## Navigazione alla pagina Panoramica di Cloud Manager {#navigate-cloud-manager}

Segui i passaggi seguenti per passare a Cloud Manager:

1. Passa direttamente alla pagina di accesso di Cloud Manager da [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

   >[!NOTE]
   >Aggiungi un segnalibro a questa pagina per riferimenti futuri e per aiutarti a passare direttamente alla pagina di destinazione di Cloud Manager.

1. Seleziona il programma dalla pagina **Programmi e prodotti di Cloud Manager** per avviare la pagina **Panoramica**.

## Programmi di Cloud Manager {#cloud-manager-programs}

I programmi Cloud Manager rappresentano set di ambienti Cloud Manager che supportano set logici di iniziative aziendali, in genere corrispondenti a un contratto a livello di servizio (SLA, Service Level Agreement) acquistato. Ad esempio, un programma può rappresentare le risorse AEM per supportare i siti Web pubblici globali, mentre un altro programma rappresenta una DAM centrale interna. Guarda questo [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en) per ulteriori informazioni sull’utilizzo dei programmi Cloud Manager.

Un utente può creare un programma **Sandbox** o **Produzione**.

* Viene creato un *programma di produzione* per abilitare il traffico live al momento appropriato in futuro.
Per ulteriori informazioni, consulta [Introduzione ai programmi di produzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/introduction-production-programs.html?lang=en) .

* Un *programma sandbox* viene generalmente creato per scopi di formazione, esecuzione di demo, abilitazione, POC o documentazione. Non è destinato a trasportare traffico live e avrà restrizioni che un programma di produzione non intende. Includerà Sites e Assets e verrà fornito automaticamente con un ramo Git che include codice di esempio, un ambiente di sviluppo e una pipeline non di produzione.
Per ulteriori informazioni, consulta [Introduzione ai programmi sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/introduction-sandbox-programs.html?lang=en) .

## Ambienti Cloud Manager {#cloud-manager-environments}

Gli ambienti cloud verranno creati, aperti e visualizzati tramite Cloud Manager. Possono essere un ambiente di produzione, stage o ambiente di sviluppo. Ambienti diversi supportano scopi diversi e possono essere utilizzati utilizzando pipeline CI/CD diverse. Gli ambienti sono composti di servizi quali:

* [AEM Author Services](#author-services)
* [AEM Publish Services](#publish-services)
* [Servizi Dispatcher](#dispatcher-services)

   >[!NOTE]
   > Per ulteriori informazioni sugli ambienti disponibili, consulta il video [Utilizzo di Adobe Cloud Manager Environments](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager) . Inoltre, consulta [Manage Environments](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en) per ulteriori informazioni sui tipi di ambiente che un utente può creare e su come l’utente può creare un ambiente.

### AEM Author Service {#author-services}

AEM Author Service è incluso in un ambiente in cui il contenuto del sito e le risorse digitali vengono create, gestite e aggiornate. In genere, solo gli utenti interni hanno accesso al servizio Author ed è dietro una schermata di accesso. Il servizio Authoring è progettato sia come ambiente di authoring che di anteprima.

### Servizio di pubblicazione AEM {#publish-services}

AEM Publish Service è incluso in un ambiente che ospita l’esperienza dell’utente finale, come un sito web. Questo è il servizio che i visitatori del sito visualizzeranno e con cui interagiranno. In genere, il servizio di pubblicazione è disponibile al pubblico.

### Servizio Dispatcher AEM {#dispatcher-services}

Dispatcher è un modulo `Apache HTTP Web server` che fornisce un livello di sicurezza e prestazioni che si trova davanti al servizio di pubblicazione AEM.
