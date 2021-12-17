---
title: Comprendere l’installazione del componente aggiuntivo Demo di riferimento
description: Scopri Cloud Manager e come viene utilizzato per installare il componente aggiuntivo.
source-git-commit: 52d65251744ce0ae5cf7a7e0a45b39d8fe78f13a
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---


# Comprendere l’installazione del componente aggiuntivo Demo di riferimento {#understand-installation}

Scopri Cloud Manager e come viene utilizzato per installare il componente aggiuntivo.

>[!TIP]
>
>Se hai già esperienza con Cloud Manager o desideri passare direttamente alla configurazione e all’utilizzo del componente aggiuntivo, puoi passare a [Creare un programma e una pipeline](create-program.md)
>
>Per scoprire come Cloud Manager e AEM collaborano per creare ambienti demo e come configurarli e utilizzarli, continua a leggere il documento corrente.

## Obiettivo {#objective}

Questo documento consente di comprendere come funziona il processo di installazione del componente aggiuntivo Demo di riferimento, illustrando come funzionano i diversi pezzi insieme. Dopo la lettura è necessario:

* Conoscenza di base di Cloud Manager.
* Scopri come le pipeline forniscono contenuto e configurazione a AEM.
* Scopri come i modelli possono creare nuovi siti precompilati con contenuti dimostrativi con pochi clic.

Questo documento si concentra sulla comprensione di questi elementi fondamentali del componente aggiuntivo Demo di riferimento AEM prima di passare al passaggio successivo del percorso in cui si inizia l&#39;installazione.

Anche se si consiglia di procedere passo dopo percorso, se hai già esperienza con Cloud Manager o desideri passare direttamente alla configurazione e all’utilizzo del componente aggiuntivo, puoi saltare a [Creare un programma e una pipeline](create-program.md)

## Ruolo responsabile {#responsible-role}

Questo percorso si applica a un amministratore di sistema che è membro del **Proprietario business** in Cloud Manager per la tua organizzazione.

## Requisiti e prerequisiti {#requirements-prerequisites}

Sono necessari requisiti minimi per conoscere e iniziare a utilizzare il componente aggiuntivo Demos di riferimento.

### Conoscenza {#knowledge}

* Conoscenza di base di Cloud Manager

### Strumenti {#tools}

* Essere membro di **Proprietario business** ruolo in Cloud Manager per la tua organizzazione

## Informazioni su Cloud Manager {#cloud-manager}

Cloud Manager è un componente essenziale di AEM as a Cloud Service e funge da punto di ingresso singolo per la piattaforma.

Cloud Manager viene utilizzato per amministrare le risorse cloud che supportano i progetti AEM, inclusi gli ambienti e gli strumenti necessari. Ai fini del presente percorso, non è necessaria una comprensione completa di Cloud Manager. Tuttavia, è necessario avere familiarità con alcuni concetti di base.

>[!TIP]
>
>Per informazioni approfondite su Cloud Manager, consulta [Risorse aggiuntive](#additional-resources) sezione di questo articolo per collegamenti a ulteriori informazioni.

### Programmi {#programs}

Quando accedi a Cloud Manager hai accesso a uno o più **programmi**. Un programma può essere definito in molti modi diversi, ma è più semplice pensarlo come associato ai siti e alle esperienze associate a un’identità di marchio.

Se accedi a Cloud Manager come rappresentante **WKND Travel and Adventure Enterprises**, è possibile creare un **Vita notturna WKND** programma e **Progetti di cortile WKND** programma. Entrambi questi programmi avrebbero ambienti AEM per la gestione dei siti associati.

### Sandbox {#sandboxes}

I programmi possono essere programmi di produzione o programmi sandbox.

* **Un programma di produzione** viene creato per consentire il traffico live quando il programma è pronto per essere live.
* **Un programma sandbox** viene creato per la formazione, le demo in esecuzione, l’abilitazione, i POC, ecc. e non è destinato al traffico live.

Per installare il componente aggiuntivo Demos di riferimento AEM, è necessario creare un nuovo programma sandbox.

>[!NOTE]
>
>Il componente aggiuntivo Demos di riferimento AEM è disponibile solo nei programmi sandbox.

## Flusso di installazione e utilizzo {#installation-flow}

Ora che conosci alcuni concetti fondamentali di Cloud Manager, l’installazione del componente aggiuntivo AEM Reference Demos è concettualmente semplice.

1. Accedi a Cloud Manager.
1. Crea un nuovo programma di AEM sandbox, attivando il componente aggiuntivo Demos di riferimento AEM come opzione per il programma.
1. Il contenuto e la configurazione demo vengono distribuiti nel programma. Il contenuto demo contiene:
   * Modelli di sito utilizzati per creare vari siti AEM utilizzando le funzioni di AEM, precompilati con esempi di best practice.
   * Strumenti di configurazione per gestire il contenuto demo.
1. Accedi a AEM nel tuo nuovo programma sandbox e utilizza lo strumento di creazione rapida del sito e crea siti demo in base ai modelli.
1. Utilizza gli strumenti di configurazione per gestire tali siti demo e modelli, inclusa l’eliminazione di tali siti quando non più necessario.

## Modelli di sito AEM {#site-templates}

I modelli di sito AEM sono pacchetti che contengono contenuto e struttura predefiniti per un sito. I modelli di sito possono essere personalizzati per soddisfare le esigenze di progetti specifici, in modo che, quando AEM amministratori creano nuovi siti, possano scegliere tra modelli applicabili ai propri casi aziendali.

Il componente aggiuntivo Demos di riferimento AEM include più modelli per varie esigenze di test e dimostrazione. Dopo aver creato il programma e implementato la pipeline per installare il componente aggiuntivo, è possibile accedere AEM e creare siti in base a molti modelli dimostrativi

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso aggiuntivo Demos di riferimento AEM, devi:

* Conoscenza di base di Cloud Manager.
* Scopri come le pipeline forniscono contenuto e configurazione a AEM.
* Scopri come i modelli possono creare nuovi siti precompilati con contenuti dimostrativi con pochi clic.

Sviluppare questa conoscenza e continuare il percorso di creazione siti rapida AEM revisione successiva del documento [Creare un programma e una pipeline,](create-program.md) dove verrà illustrato come impostare un nuovo programma e una nuova pipeline per distribuire il componente aggiuntivo.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso Creazione rapida siti esaminando il documento [Creare un programma e una pipeline,](create-program.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso.

* [Informazioni su programmi e tipi di programmi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html) - Inizia qui per comprendere le differenze tra i programmi live e sandbox.
* [Modelli di sito](/help/sites-cloud/administering/site-creation/site-templates.md) - Per ulteriori informazioni sulla struttura dei modelli di sito e sulla relativa modalità di creazione, consulta questo documento.
* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
