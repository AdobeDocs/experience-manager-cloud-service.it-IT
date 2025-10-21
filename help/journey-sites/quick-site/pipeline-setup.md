---
title: Configurare la pipeline
description: Crea una pipeline front-end per gestire la personalizzazione del tema del sito.
exl-id: 0d77d1a6-98f3-4961-9283-f52c1b5b2a7b
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: display, noCatalog
source-git-commit: 0a458616afad836efae27e67dbe145fc44bee968
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 100%

---


# Configurare la pipeline {#set-up-your-pipeline}

{{traditional-aem}}

Crea una pipeline front-end per gestire la personalizzazione del tema del sito.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso di creazione rapida di siti AEM, [Crea sito da modello](create-site.md), hai imparato a utilizzare un modello per siti per creare rapidamente un sito AEM che può essere ulteriormente personalizzato utilizzando gli strumenti front-end e hai appreso a:

* Ottenere i modelli di sito AEM.
* Creare un sito utilizzando un modello.
* Scopri come scaricare il modello dal tuo nuovo sito per fornirlo allo sviluppatore front-end.

Questo articolo si basa su questi elementi fondamentali per consentire l’impostazione di una pipeline front-end, che lo sviluppatore front-end utilizzerà successivamente nel percorso per distribuire personalizzazioni front-end.

## Obiettivo {#objective}

Questo documento consente di comprendere le pipeline front-end e come crearne una per gestire la distribuzione del tema personalizzato del sito. Dopo la lettura dovresti:

* Comprendere cos’è una pipeline front-end.
* Scoprire come impostare una pipeline front-end in Cloud Manager.

## Ruolo responsabile {#responsible-role}

Questa parte del percorso si applica all’amministratore di Cloud Manager.

## Requisiti  {#requirements}

* Devi avere accesso a Cloud Manager.
* Devi essere membro del **Responsabile della distribuzione** in Cloud Manager.
* In Cloud Manager deve essere configurato un archivio git per l’ambiente AEM.
   * In generale, questo vale già per qualsiasi progetto attivo. Tuttavia, in caso contrario, consulta la documentazione sugli Archivi di Cloud Manager disponibile nella sezione [Risorse aggiuntive](#additional-resources).

## Che cos’è una pipeline front-end {#front-end-pipeline}

Lo sviluppo front-end comporta la personalizzazione di risorse JavaScript, CSS e statiche che definiscono lo stile del sito AEM. Lo sviluppatore front-end lavorerà nei propri ambienti locali per effettuare queste personalizzazioni. Una volta pronte, le modifiche vengono salvate nell’archivio Git AEM. Ma sono impegnati solo nel codice sorgente. Non sono ancora in diretta.

La pipeline front-end porta queste personalizzazioni impegnate e le implementa in un ambiente AEM, in genere in ambienti di produzione o non di produzione.

In questo modo, lo sviluppo front-end può funzionare separatamente e parallelamente a qualsiasi sviluppo back-end full-stack su AEM, che dispone di proprie pipeline di distribuzione.

>[!NOTE]
>
>Le pipeline front-end possono distribuire solo risorse JavaScript, CSS e statiche per personalizzare lo stile del sito AEM. Il contenuto del sito, come pagine o risorse, non può essere distribuito in una pipeline.

## Accesso a Cloud Manager {#login}

1. Accedi ad Adobe Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Cloud Manager elenca i vari programmi disponibili. Seleziona il programma che desideri gestire. Se hai iniziato a lavorare con AEM as a Cloud Service da poco, probabilmente avrai a disposizione solo un programma.

   ![Selezione di un programma in Cloud Manager](assets/cloud-manager-select-program.png)

Viene visualizzata una panoramica del programma. La pagina avrà un aspetto diverso ma simile a questo esempio.

![Panoramica di Cloud Manager](assets/cloud-manager-overview.png)

Prendi nota del nome del programma a cui hai effettuato l’accesso o di cui hai copiato l’URL. In seguito, devi fornire questa funzionalità allo sviluppatore front-end.

## Creare una pipeline front-end {#create-front-end-pipeline}

Dopo aver effettuato l’accesso a Cloud Manager, puoi creare una pipeline per la distribuzione front-end.

1. Nella sezione **Pipeline** della pagina di Cloud Manager, seleziona il pulsante **Aggiungi**.

   ![Pipeline](assets/pipelines-add.png)

1. Nel menu a comparsa visualizzato sotto il pulsante **Aggiungi**, seleziona **Aggiungi pipeline di non produzione** ai fini del presente percorso.

1. Sulla scheda **Configurazione** della finestra di dialogo **Aggiungi pipeline di non produzione** che viene visualizzata:
   * seleziona **Pipeline di distribuzione**.
   * Fornisci alla pipeline un nome nel campo **Nome della pipeline di non produzione**.

   ![Aggiungi la configurazione della pipeline](assets/add-pipeline-configuration.png)

1. Seleziona **Continua**.

1. Sulla scheda **Codice sorgente**:
   * Seleziona **Codice front-end** come tipo di codice da distribuire.
   * Assicurati che l’ambiente corretto sia selezionato in **Ambienti di distribuzione idonei**.
   * Seleziona l’**Archivio** corretto.
   * Definisci quale **Ramo Git** deve essere associato alla pipeline.
   * Definisci la **Posizione del codice** se lo sviluppo front-end si trova sotto un particolare percorso nell’archivio selezionato. Il valore predefinito è la directory principale dell’archivio, ma spesso lo sviluppo front-end e il back-end si trovano in percorsi diversi.

   ![Informazioni sul codice sorgente per l’aggiunta della pipeline](assets/add-pipeline-source-code.png)

1. Seleziona **Salva**.

La nuova pipeline viene creata ed è visibile nella sezione **Pipeline** della finestra di Cloud Manager. Toccando o facendo clic sui puntini di sospensione dopo il nome della pipeline, vengono visualizzate le opzioni che consentono di modificare o visualizzare i dettagli in base alle necessità.

![Opzioni pipeline](assets/new-pipeline.png)

>[!TIP]
>
>Se conosci le pipeline in AEMaaCS e vuoi saperne di più sulle differenze tra i diversi tipi di pipeline, compresi ulteriori dettagli sulla pipeline front-end, consulta Configurare la pipeline CI/CD - Cloud Services nella sezione [Risorse aggiuntive](#additional-resources) di seguito.

## Passaggio successivo {#what-is-next}

Dopo aver completato questa parte del percorso di creazione rapida sito di AEM, è necessario:

* Comprendere cos’è una pipeline front-end.
* Come impostare una pipeline front-end in Cloud Manager.

Approfondisci questo argomento e continua il percorso di creazione rapida di un sito AEM rivedendo il documento [Concedere l’accesso allo sviluppatore front-end](grant-access.md), dove puoi effettuare l’onboarding degli sviluppatori front-end in Cloud Manager in modo che possano accedere all’archivio Git del sito AEM e alla pipeline.

## Risorse aggiuntive {#additional-resources}

Sebbene sia consigliabile passare alla parte successiva del percorso per la creazione rapida di un sito rivedendo il documento [Personalizzare il tema del sito](customize-theme.md), di seguito sono riportate alcune risorse aggiuntive e facoltative che approfondiscono alcuni concetti menzionati in questo documento. Tuttavia, queste non sono necessarie per proseguire nel percorso.

* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=it): per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
* [Archivi di Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md): per ulteriori informazioni su come impostare e gestire archivi Git per il progetto AEMaaCS, consulta questo documento.
* [Configurare la pipeline CI/CD - Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md): ulteriori informazioni sulla configurazione delle pipeline, sia full stack che front end, in questo documento.
