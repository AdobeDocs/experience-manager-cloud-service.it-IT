---
title: Introduzione a Cloud Manager
description: Scopri in che modo Cloud Manager supporta il progetto AEM tramite i suoi programmi, ambienti e pipeline.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 2d793f22e554c2a4bde8831b5053d1640ba07c70
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 5%

---

# Introduzione a Cloud Manager {#intro-cloud-manager}

Cloud Manager è un componente essenziale di AEM as a Cloud Service e funge da punto di ingresso unico per il tuo team. Le sue pipeline CI/CD appositamente progettate sono dotate di funzionalità di test approfonditi e della massima qualità del codice per offrire esperienze eccezionali. Per consentire ai clienti di avviare rapidamente i progetti, Cloud Manager fornisce tutto ciò che è necessario in modalità self-service, inclusa la possibilità di creare risorse e ambienti cloud e di accedere agli archivi Git. Queste funzioni supportano le configurazioni di sviluppo aziendale, in modo che i team possano lavorare spesso per eseguire frequenti cambiamenti, fornire rapidamente esperienze digitali eccezionali e accelerare il time-to-value.

L’amministratore di sistema è responsabile della configurazione del team Cloud Manager, che include utenti singoli che creeranno le risorse cloud e gli sviluppatori. Per ulteriori informazioni su come impostare e ridimensionare il team di sviluppo aziendale e vedere come AEM as a Cloud Service può supportare il processo di sviluppo, consulta il documento [Configurazione di sviluppo team Enterprise per AEM as a Cloud Service.](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)

## Navigazione alla pagina Panoramica di Cloud Manager {#navigate-cloud-manager}

Segui questi passaggi per passare a Cloud Manager.

1. Passa alla pagina di accesso di Cloud Manager all’indirizzo [`https://my.cloudmanager.adobe.com`.](https://my.cloudmanager.adobe.com/).

1. Seleziona il programma da Cloud Manager’s **Programmi e prodotti** per avviare **Panoramica** pagina.

Puoi inoltre accedere alla pagina Programmi e prodotti di Cloud Manager dalla home page di Adobe Experience Cloud seguendo questi passaggi.

1. Passa a Adobe Experience Cloud all&#39;indirizzo [`https://experience.adobe.com`](https://experience.adobe.com) e accedi utilizzando il tuo Adobe ID.

1. Assicurati di essere nell’organizzazione corretta facendo riferimento al nome dell’organizzazione visualizzato in alto a destra nella barra degli strumenti.

1. Seleziona **Experience Manager**.

1. Sulla **Cloud Manager** scheda, fai clic su **Launch**

## Autorizzazioni basate sul ruolo in Cloud Manager {#role-based-permissions}

| Autorizzazione | Descrizione | Business Owner (Proprietario) | Deployment Manager (Responsabile implementazione) | Program Manager (Responsabile programma) | Developer (Sviluppatore) |
|--- |--- |--- |--- |--- |--- |
| Aggiungi programma<br>Modifica programma | Aggiungi un nuovo programma<br>Aggiungere o rimuovere soluzioni o componenti aggiuntivi | x |  |  |  |
| Creare un ambiente | Creare ambienti di produzione e di staging e sviluppo | x | x |  |  |
| Ambiente di aggiornamento | Aggiornare ambienti di produzione e di staging e di sviluppo | x | x |  |  |
| Elimina ambiente di sviluppo | Eliminare gli ambienti di sviluppo | x | x |  |  |
| Configurazione della pipeline | Configurazione e modifica delle pipeline |  | x |  |  |
| Esecuzione della pipeline | Avvia pipeline | x | x |  |  |
| Esecuzione della pipeline | Rifiutare/approvare importanti errori del gate di qualità a 3 livelli | x | x | x |  |
| Esecuzione della pipeline | Fornire l&#39;approvazione dal vivo | x | x | x |  |
| Esecuzione della pipeline | Pianificare distribuzioni di produzione | x | x | x |  |
| Elimina pipeline | Consenti eliminazione pipeline |  | x |  |  |
| Annulla esecuzione | Annulla esecuzione corrente |  | x |  |  |
| Genera token di accesso personale | Accedere a Git |  | x |  | x |

>[!NOTE]
>
>Un utente può essere assegnato a più ruoli. Ad esempio, l’assegnazione di entrambi **Proprietario business** e **Gestione distribuzione** I ruoli di un utente danno all&#39;utente la somma di queste autorizzazioni.

## Programmi di Cloud Manager {#cloud-manager-programs}

I programmi Cloud Manager rappresentano set di ambienti Cloud Manager che supportano raggruppamenti logici di iniziative aziendali. Questi raggruppamenti corrispondono in genere a un contratto a livello di servizio (SLA) acquistato. Ad esempio, un programma può rappresentare le risorse AEM per supportare il sito Web pubblico di un&#39;organizzazione, mentre un altro programma rappresenta un DAM interno.


Guarda questo [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) per ulteriori informazioni sull’utilizzo dei programmi Cloud Manager.

Un utente può creare un **Sandbox** o **Produzione** programma.

* A **programma di produzione** viene creato per abilitare il traffico live al momento opportuno in futuro.
   * Fare riferimento al documento [Introduzione ai programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) per ulteriori dettagli.

* A **programma sandbox** viene generalmente creato per scopi di formazione, esecuzione di demo, abilitazione, creazione di POC o per la documentazione.
   * Non è destinato a trasportare il traffico in diretta e avrà restrizioni che un programma di produzione non lo farà.
   * Include Sites e Assets e viene fornito automaticamente con un ramo git che include codice di esempio, un ambiente di sviluppo e una pipeline non di produzione.
   * Fare riferimento al documento [Introduzione ai programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) per ulteriori dettagli.

## Ambienti Cloud Manager {#cloud-manager-environments}

Gli ambienti cloud verranno creati, aperti e visualizzati tramite Cloud Manager. Questi ambienti possono essere ambienti di produzione, staging o sviluppo. Ambienti diversi hanno scopi diversi e possono essere utilizzati con diverse pipeline CI/CD. Gli ambienti sono composti di servizi quali:

* [Servizi di authoring AEM](#author-services)
* [Servizi di pubblicazione AEM](#publish-services)
* [Servizi Dispatcher](#dispatcher-services)

>[!TIP]
>
> Fai riferimento al video [Utilizzo degli ambienti Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) panoramica degli ambienti disponibili.
>
>Consulta il documento [Gestire gli ambienti](/help/implementing/cloud-manager/manage-environments.md) per ulteriori informazioni sui tipi di ambiente che un utente può creare e su come l’utente può creare un ambiente.

### Servizio di authoring AEM {#author-services}

Un servizio di authoring AEM è incluso in ambienti in cui il contenuto del sito e le risorse digitali vengono create, gestite e aggiornate. In genere solo gli utenti interni hanno accesso al servizio di authoring e viene mantenuto dietro una schermata di accesso. Il servizio di authoring funziona sia come ambiente di authoring che come ambiente di anteprima.

### AEM Publishing Service {#publish-services}

Un servizio di pubblicazione AEM è incluso in ambienti che ospitano l’esperienza dell’utente finale, come un sito web. Questo è il servizio che i visitatori del sito visualizzeranno e con cui interagiranno. In genere, il servizio di pubblicazione è disponibile al pubblico.

### Servizio Dispatcher AEM {#dispatcher-services}

Il dispatcher è un `Apache HTTP Web server` modulo che fornisce un livello di sicurezza e prestazioni che si trova davanti al servizio di pubblicazione AEM.
