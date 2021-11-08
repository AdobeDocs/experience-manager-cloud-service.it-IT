---
title: Imposta la pipeline
description: Crea una pipeline front-end per gestire la personalizzazione del tema del sito.
source-git-commit: 2d575036c8e84e282a6599015360dcd25e4c8aa9
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---


# Imposta la pipeline {#set-up-your-pipeline}

Crea una pipeline front-end per gestire la personalizzazione del tema del sito.

>[!CAUTION]
>
>Lo strumento di creazione rapida del sito è attualmente un&#39;anteprima tecnica. Esso è messo a disposizione a fini di prova e valutazione e non è destinato all&#39;uso della produzione se non concordato con il sostegno Adobe.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di creazione di siti rapidi AEM, [Crea sito da modello,](create-site.md) hai imparato a utilizzare un modello di sito per creare rapidamente un sito AEM che può essere ulteriormente personalizzato utilizzando gli strumenti front-end e ora devi:

* Scopri come ottenere AEM modelli di sito.
* Scopri come creare un nuovo sito utilizzando un modello.
* Scopri come scaricare il modello dal tuo nuovo sito per fornire allo sviluppatore front-end.

Questo articolo si basa su questi elementi fondamentali per consentire l’impostazione di una pipeline front-end, che lo sviluppatore front-end utilizzerà successivamente nel percorso per distribuire personalizzazioni front-end.

## Obiettivo {#objective}

Questo documento consente di comprendere le pipeline front-end e come crearne una per gestire la distribuzione del tema personalizzato del sito. Dopo la lettura è necessario:

* Comprendere cos’è una pipeline front-end.
* Scopri come impostare una pipeline front-end in Cloud Manager.

## Ruolo responsabile {#responsible-role}

Questa parte del percorso si applica all’amministratore di Cloud Manager.

## Requisiti {#requirements}

* Devi avere accesso a Cloud Manager.
* Devi essere membro del **Gestione distribuzione** in Cloud Manager.
* In Cloud Manager deve essere configurato un archivio git per l’ambiente AEM.
   * In generale, questo vale già per qualsiasi progetto attivo. Tuttavia, in caso contrario, consulta la documentazione Archivio Cloud Manager disponibile nella sezione [Risorse aggiuntive](#additional-resources) sezione .

## Che cos’è una pipeline front-end {#front-end-pipeline}

Lo sviluppo front-end comporta la personalizzazione di risorse JavaScript, CSS e statiche che definiscono lo stile del sito AEM. Lo sviluppatore front-end lavorerà nei propri ambienti locali per effettuare queste personalizzazioni. Una volta pronte, le modifiche vengono salvate nell’archivio Git AEM. Ma sono impegnati solo nel codice sorgente. Non sono ancora in diretta.

La pipeline front-end porta queste personalizzazioni impegnate e le distribuisce in un ambiente AEM, in genere in ambienti di produzione o non di produzione.

In questo modo, lo sviluppo front-end può funzionare separatamente e parallelamente a qualsiasi sviluppo back-end full-stack su AEM, che dispone di proprie pipeline di distribuzione.

>[!NOTE]
>
>Le pipeline front-end possono distribuire solo risorse JavaScript, CSS e statiche per personalizzare lo stile del sito AEM. Il contenuto del sito, come pagine o risorse, non può essere distribuito in una pipeline.

## Accesso a Cloud Manager {#login}

1. Accedi ad Adobe Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Cloud Manager elenca i vari programmi disponibili. Tocca o fai clic su quello che desideri gestire. Se inizi con AEM as a Cloud Service, probabilmente avrai a disposizione solo un programma.

   ![Selezione di un programma in Cloud Manager](assets/cloud-manager-select-program.png)

Viene visualizzata una panoramica del programma. La pagina avrà un aspetto diverso ma simile a questo esempio.

![Panoramica di Cloud Manager](assets/cloud-manager-overview.png)

Prendi nota del nome del programma a cui hai effettuato l’accesso o che hai copiato l’URL. In seguito, dovrai fornire questa funzionalità allo sviluppatore front-end.

## Creare una pipeline front-end {#create-front-end-pipeline}

Dopo aver effettuato l’accesso a Cloud Manager, puoi creare una pipeline per la distribuzione front-end.

1. In **Tubi** della pagina Cloud Manager, tocca o fai clic sul pulsante **Aggiungi** pulsante .

   ![Tubi](assets/pipelines-add.png)

1. Nel menu a comparsa visualizzato sotto la finestra di dialogo **Aggiungi** pulsante seleziona **Aggiungi pipeline non di produzione** ai fini del presente percorso.

1. Sulla **Configurazione** della scheda **Aggiungi pipeline non di produzione** che apre:
   * Seleziona **Pipeline di distribuzione**.
   * Fornisci alla pipeline un nome nel **Nome della pipeline non di produzione** campo .

   ![Aggiungere la configurazione della pipeline](assets/add-pipeline-configuration.png)

1. Tocca o fai clic su **Continua**.

1. Sulla **Codice sorgente** scheda:
   * Seleziona **Codice front-end** come tipo di codice da distribuire.
   * Assicurati che l’ambiente corretto sia selezionato in **Ambienti di distribuzione idonei**.
   * Selezionare la risposta corretta **Archivio**.
   * Definisci quali **Ramo Git** la pipeline deve essere associata a .
   * Definisci la **Posizione codice** se lo sviluppo front-end si trova sotto un particolare percorso nell’archivio selezionato. Il valore predefinito è la directory principale dell’archivio, ma spesso lo sviluppo front-end e il back-end si trovano in percorsi diversi.

   ![Informazioni sul codice sorgente per l’aggiunta della pipeline](assets/add-pipeline-source-code.png)

1. Tocca o fai clic su **Salva**.

La nuova pipeline viene creata e visibile nel **Tubi** della finestra di Cloud Manager. Quando toccate i puntini di sospensione dopo il nome della pipeline, vengono visualizzate le opzioni che consentono di modificare o visualizzare i dettagli in base alle necessità.

![Opzioni pipeline](assets/new-pipeline.png)

>[!TIP]
>
>Se conosci le pipeline in AEMaaCS e vuoi saperne di più sulle differenze tra i diversi tipi di pipeline, compresi ulteriori dettagli sulla pipeline front-end, consulta Configura pipeline CI/CD - Cloud Services collegati nel [Risorse aggiuntive](#additional-resources) di seguito.

## Novità {#what-is-next}

Dopo aver completato questa parte del percorso di creazione siti rapidi AEM, è necessario:

* Comprendere cos’è una pipeline front-end.
* Scopri come impostare una pipeline front-end in Cloud Manager.

Sviluppare questa conoscenza e continuare il percorso di creazione siti rapida AEM revisione successiva del documento [Concedere l’accesso allo sviluppatore front-end,](grant-access.md) dove puoi integrare gli sviluppatori front-end in Cloud Manager in modo che possano accedere all’archivio Git del sito AEM e alla pipeline.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso Creazione rapida siti esaminando il documento [Personalizzare il tema del sito,](customize-theme.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso.

* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
* [Repository di Cloud Manager](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) - Per ulteriori informazioni su come impostare e gestire archivi Git per il progetto AEMaaCS, consulta questo documento.
* [Configurare la pipeline CI/CD - Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) - Ulteriori informazioni sulla configurazione delle tubazioni, sia full stack che front end, in questo documento.