---
title: Configurare la pipeline
description: Crea una pipeline front-end per gestire la personalizzazione del tema del sito.
exl-id: 0d77d1a6-98f3-4961-9283-f52c1b5b2a7b
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 94%

---

# Configurare la pipeline {#set-up-your-pipeline}

Crea una pipeline front-end per gestire la personalizzazione del tema del sito.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di creazione rapida sito di AEM, [Creare sito da modello,](create-site.md) hai imparato a utilizzare un modello di sito per creare rapidamente un sito AEM che può essere ulteriormente personalizzato utilizzando gli strumenti front-end e ora dovresti:

* Comprendere come ottenere i modelli di sito di AEM.
* Scopri come creare un sito utilizzando un modello.
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

La pipeline front-end porta queste personalizzazioni impegnate e le distribuisce in un ambiente AEM, in genere in ambienti di produzione o di non produzione.

In questo modo, lo sviluppo front-end può funzionare separatamente e parallelamente a qualsiasi sviluppo back-end full-stack su AEM, che dispone di proprie pipeline di distribuzione.

>[!NOTE]
>
>Le pipeline front-end possono distribuire solo risorse JavaScript, CSS e statiche per personalizzare lo stile del sito AEM. Il contenuto del sito, ad esempio pagine o risorse, non può essere distribuito in una pipeline.

## Accesso a Cloud Manager {#login}

1. Accedi ad Adobe Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Cloud Manager elenca i vari programmi disponibili. Seleziona quello che desideri gestire. Se hai iniziato a lavorare con AEM as a Cloud Service da poco, probabilmente avrai a disposizione solo un programma.

   ![Selezione di un programma in Cloud Manager](assets/cloud-manager-select-program.png)

Viene visualizzata una panoramica del programma. La pagina avrà un aspetto diverso ma simile a questo esempio.

![Panoramica di Cloud Manager](assets/cloud-manager-overview.png)

Prendi nota del nome del programma a cui hai effettuato l’accesso o di cui hai copiato l’URL. È necessario fornirlo allo sviluppatore front-end in un secondo momento.

## Creare una pipeline front-end {#create-front-end-pipeline}

Dopo aver effettuato l’accesso a Cloud Manager, puoi creare una pipeline per la distribuzione front-end.

1. In **Pipeline** nella pagina Cloud Manager, seleziona la sezione **Aggiungi** pulsante.

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

## Novità {#what-is-next}

Dopo aver completato questa parte del percorso di creazione rapida sito di AEM, è necessario:

* Comprendere cos’è una pipeline front-end.
* Scoprire come impostare una pipeline front-end in Cloud Manager.

Sviluppa questa conoscenza e continua il percorso di creazione rapida sito di AEM rivedendo il documento [Concedere l’accesso allo sviluppatore front-end,](grant-access.md) dove puoi integrare gli sviluppatori front-end in Cloud Manager in modo che possano accedere all’archivio Git del sito AEM e alla pipeline.

## Risorse aggiuntive {#additional-resources}

Sebbene sia raccomandato passare alla parte successiva del percorso Creazione rapida sito esaminando il documento [Personalizzare il tema del sito,](customize-theme.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento. Non è necessario che tali risorse continuino sul percorso.

* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=it) - Per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
* [Archivi di Cloud Manager](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md): per ulteriori informazioni su come impostare e gestire archivi Git per il progetto AEMaaCS, consulta questo documento.
* [Configurare la pipeline CI/CD - Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md): ulteriori informazioni sulla configurazione delle pipeline, sia full stack che front end, in questo documento.
