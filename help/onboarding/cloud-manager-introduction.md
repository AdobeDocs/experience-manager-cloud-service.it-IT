---
title: Introduzione a Cloud Manager
description: Scopri in che modo Cloud Manager supporta il progetto AEM tramite programmi, ambienti e pipeline.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 96%

---


# Introduzione a Cloud Manager {#intro-cloud-manager}

Cloud Manager è un componente essenziale di AEM as a Cloud Service e funge da punto di ingresso singolo per il team. Le pipeline CI/CD appositamente progettate offrono funzionalità di test approfondite e la massima qualità del codice per garantire esperienze eccezionali. Per consentire ai clienti di avviare rapidamente i progetti, Cloud Manager fornisce tutto ciò che serve per iniziare in autonomia, inclusa la possibilità di creare risorse e ambienti cloud e di accedere agli archivi Git. Queste funzioni supportano le configurazioni di sviluppo di livello Enterprise per consentire ai team di confermare modifiche frequenti, offrire rapidamente esperienze digitali eccezionali e accelerare il time to value.

L’amministratore di sistema è responsabile della configurazione del team Cloud Manager, che include le persone che creano le risorse cloud e il team di sviluppo. Per ulteriori informazioni su come impostare e scalare il team di sviluppo Enterprise e scoprire come AEM as a Cloud Service può supportare il processo di sviluppo, consulta il documento [Configurazione del team di sviluppo Enterprise per AEM as a Cloud Service](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md).

## Accesso alla pagina Panoramica di Cloud Manager {#navigate-cloud-manager}

Per accedere a Cloud Manager, segui la procedura riportata di seguito.

1. Accedi alla pagina di accesso di Cloud Manager all’indirizzo [`https://my.cloudmanager.adobe.com`.](https://my.cloudmanager.adobe.com/).

1. Dalla pagina **Programmi e prodotti** di Cloud Manager, seleziona il programma per aprire la pagina **Panoramica**.

Puoi accedere alla pagina Programmi e prodotti di Cloud Manager anche dalla pagina Home di Adobe Experience Cloud, seguendo la procedura riportata di seguito.

1. Accedi a Adobe Experience Cloud all’indirizzo [`https://experience.adobe.com`](https://experience.adobe.com), quindi accedi con il tuo Adobe ID.

1. Assicurati di aver selezionato l’organizzazione corretta facendo riferimento al nome visualizzato nella parte superiore destra della barra degli strumenti.

1. Seleziona **Experience Manager**.

1. Il giorno **Cloud Manager** , fare clic su **Launch**

## Autorizzazioni basate sui ruoli in Cloud Manager {#role-based-permissions}

| Autorizzazione | Descrizione | Proprietario business | Responsabile dell’implementazione | Program Manager (Responsabile programma) | Sviluppatore |
|--- |--- |--- |--- |--- |--- |
| Aggiunta di un programma<br>Modifica di un programma | Aggiunta di un nuovo programma<br>Aggiunta o rimozione di soluzioni o componenti aggiuntivi | x |  |  |  |
| Creazione di un ambiente | Creazione degli ambienti di produzione + staging e sviluppo | x | x |  |  |
| Aggiornamento ambiente | Aggiornamento degli ambienti di produzione + staging e sviluppo | x | x |  |  |
| Eliminazione ambiente di sviluppo | Eliminazione degli ambienti di sviluppo | x | x |  |  |
| Configurazione della pipeline | Configurazione e modifica delle pipeline |  | x |  |  |
| Esecuzione delle pipeline | Avvio delle pipeline | x | x |  |  |
| Esecuzione delle pipeline | Rifiuto/approvazione degli errori del gate di qualità a 3 livelli | x | x | x |  |
| Esecuzione delle pipeline | Approvazione per la pubblicazione | x | x | x |  |
| Esecuzione delle pipeline | Pianificazione delle distribuzioni nell’ambiente di produzione | x | x | x |  |
| Eliminazione delle pipeline | Autorizzazione all’eliminazione delle pipeline |  | x |  |  |
| Annullamento dell’esecuzione | Annullamento dell’esecuzione corrente |  | x |  |  |
| Generazione del token di accesso personale | Accesso a Git |  | x |  | x |
| Crea un RDE | Crea un ambiente di sviluppo rapido | x |  |  | x |
| Reimposta un RDE | Ripristina un ambiente di sviluppo rapido | x |  |  | x |
| Creare/modificare i set di contenuti | Creare o modificare un set di contenuti per la copia del contenuto |  | x |  |  |
| Avvia/annulla copia contenuto | Avviare o annullare un processo di copia del contenuto |  | x |  |  |

>[!NOTE]
>
>È possibile assegnare più ruoli a un singolo utente. Ad esempio, assegnando a un utente entrambi i ruoli **Proprietario business** e **Responsabile distribuzione**, si assegna la somma delle rispettive autorizzazioni.

## Programmi di Cloud Manager {#cloud-manager-programs}

I programmi di Cloud Manager rappresentano set di ambienti di Cloud Manager che supportano raggruppamenti logici di iniziative aziendali. Tali raggruppamenti corrispondono in genere al contratto del livello di servizio (SLA) acquistato. Ad esempio, un programma può rappresentare le risorse AEM per supportare il sito web pubblico di un’organizzazione, mentre un altro programma può rappresentare un DAM interno.


Per ulteriori informazioni sull’uso dei programmi di Cloud Manager, guarda questo [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=it).

L’utente può creare un programma **sandbox** o un programma **di produzione**.

* Un **programma di produzione** viene creato per abilitare il traffico in tempo reale nel momento futuro adeguato.
   * Per ulteriori dettagli, consulta [Introduzione ai programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).

* Un **programma sandbox** viene generalmente creato a scopi di formazione, esecuzione di demo, abilitazione, creazione di POC o documentazione.
   * Non è concepito per trasmettere il traffico in tempo reale e presenta delle limitazioni non riscontrate nei programmi di produzione.
   * Un programma sandbox include Sites e Assets e viene fornito automaticamente con un ramo Git che include il codice di esempio, un ambiente di sviluppo e una pipeline non di produzione.
   * Per ulteriori dettagli, consulta [Introduzione ai programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md).

## Ambienti di Cloud Manager {#cloud-manager-environments}

Gli ambienti cloud vengono creati, aperti e visualizzati tramite Cloud Manager. Questi ambienti possono essere di produzione, staging o sviluppo. Ambienti diversi hanno scopi diversi e possono essere utilizzati con diverse pipeline CI/CD. Gli ambienti sono composti di servizi quali:

* [Servizi di authoring di AEM](#author-services)
* [Servizi di pubblicazione AEM](#publish-services)
* [Servizi Dispatcher](#dispatcher-services)

>[!TIP]
>
> Per una panoramica degli ambienti disponibili, fai riferimento al video [Utilizzo degli ambienti di Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=it).
>
>Per ulteriori informazioni su quali tipi di ambienti si possono creare e su come farlo, consulta il documento [Gestire gli ambienti](/help/implementing/cloud-manager/manage-environments.md).

### Servizio di authoring di AEM {#author-services}

Il servizio di authoring di AEM è incluso negli ambienti in cui si creano, gestiscono e aggiornano i contenuti del sito e le risorse digitali. In genere solo gli utenti interni hanno accesso al servizio di authoring, che è protetto da una schermata di accesso. Il servizio di authoring funge da ambiente di creazione e da ambiente di anteprima.

### Servizio di pubblicazione AEM {#publish-services}

Il servizio di pubblicazione AEM è incluso negli ambienti che ospitano l’esperienza dell’utente finale, come un sito web. Si tratta del servizio che i visitatori del sito vedono e con cui interagiscono. In genere, il servizio di pubblicazione è disponibile per tutti gli utenti.

### Servizio Dispatcher AEM {#dispatcher-services}

Il dispatcher è un modulo di `Apache HTTP Web server` che fornisce un livello di sicurezza e prestazioni aggiuntive per il servizio di pubblicazione AEM.
