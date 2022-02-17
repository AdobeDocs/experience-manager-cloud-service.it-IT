---
title: Distribuire il tema personalizzato
description: Scopri come distribuire il tema del sito utilizzando la pipeline.
source-git-commit: 97c7590fd7b77e78cf2d465454fac80906d37803
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 1%

---


# Distribuire il tema personalizzato {#deploy-your-customized-theme}

Scopri come distribuire il tema del sito utilizzando la pipeline.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di creazione di siti rapidi AEM, [Personalizzare il tema del sito,](customize-theme.md) hai imparato come è costruito il tema, come personalizzarlo e come testarlo utilizzando AEM contenuto live, e ora devi:

* Comprendere la struttura di base del tema del sito e come modificarlo.
* Scopri come testare le personalizzazioni dei temi utilizzando contenuti AEM reali tramite proxy locale.
* Scopri come eseguire il commit delle modifiche nell’archivio Git AEM.

Ora puoi effettuare il passaggio finale e utilizzare la pipeline per distribuirli.

## Obiettivo {#objective}

Questo documento spiega come distribuire il tema utilizzando la pipeline. Dopo la lettura è necessario:

* Scopri come attivare una distribuzione della pipeline.
* Scopri come controllare lo stato della distribuzione.

## Ruolo responsabile {#responsible-role}

Questa parte del percorso si applica allo sviluppatore front-end.

## Avvia la pipeline {#start-pipeline}

Dopo aver eseguito il commit delle modifiche di personalizzazione del tema nell’archivio Git AEM, puoi eseguire [la pipeline creata dall’amministratore](pipeline-setup.md) per distribuire le modifiche.

1. Accesso a Cloud Manager [come hai fatto per recuperare le informazioni di accesso Git](retrieve-access.md) E accedi al tuo programma. Sulla **Panoramica** verrà visualizzata una scheda per **Tubi**.

   ![Panoramica di Cloud Manager](assets/cloud-manager-overview.png)

1. Tocca o fai clic sui puntini di sospensione accanto alla pipeline da avviare. Dal menu a discesa, seleziona **Esegui**.

   ![Esegui pipeline](assets/run-pipeline.png)

1. In **Esegui pipeline** finestra di dialogo di conferma, tocca o fai clic su **Sì**.

   ![Conferma esecuzione pipeline](assets/pipeline-confirm.png)

1. Nell’elenco delle pipeline, la colonna di stato indica che la pipeline è in esecuzione.

   ![Stato di esecuzione della pipeline](assets/pipeline-running.png)

## Controllare lo stato della pipeline {#pipeline-status}

Puoi controllare lo stato della pipeline per visualizzarne i dettagli in qualsiasi momento.

1. Tocca o fai clic sui puntini di sospensione accanto alla pipeline.

   ![Visualizzare i dettagli della pipeline](assets/view-pipeline-details.png)

1. La finestra dei dettagli della pipeline mostra il raggruppamento dell’avanzamento della pipeline.

   ![Dettagli della pipeline](assets/pipeline-details.png)

>[!TIP]
>
>Nella finestra dei dettagli della pipeline, puoi toccare o fare clic su **Registro di download** per qualsiasi passaggio della pipeline a scopo di debug, in caso di errore di un passaggio. Il debug della pipeline esula dall’ambito di questo percorso. Consulta i documenti tecnici per Cloud Manager in [Risorse aggiuntive](#additional-resources) di questa pagina.

## Convalidare le personalizzazioni distribuite {#view-customizations}

Una volta completata la pipeline, puoi informare l’amministratore per convalidare le modifiche. L’amministratore:

1. Apri l’ambiente di authoring AEM.
1. Passa a [il sito creato in precedenza dall&#39;amministratore.](create-site.md)
1. Modifica una delle pagine di contenuto.
1. Visualizza le modifiche applicate.

![Modifiche applicate](assets/changes-applied.png)

## Fine del Percorso? {#end-of-journey}

Congratulazioni! È stato completato il percorso di creazione AEM siti rapidi. Ora dovresti:

* Scopri come Cloud Manager e la pipeline front-end funzionano per gestire e distribuire personalizzazioni front-end.
* Scopri come creare un sito AEM basato su un modello e come scaricare il tema del sito.
* Come integrare uno sviluppatore front-end in modo che possa accedere all’archivio Git AEM.
* Come personalizzare e testare un tema utilizzando il contenuto AEM proxy e eseguire il commit di tali modifiche in AEM git.
* Come distribuire la personalizzazione front-end utilizzando la pipeline.

Ora puoi personalizzare i temi del tuo sito AEM. Tuttavia, prima di iniziare a creare diversi flussi di lavoro utilizzando più pipeline front-end, controlla il documento [Sviluppo di siti con la pipeline front-end.](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) Sarà utile per sfruttare al massimo lo sviluppo front-end:

* Mantenere un&#39;unica fonte di verità.
* Mantenere una separazione delle preoccupazioni.

AEM è uno strumento potente e ci sono molte opzioni aggiuntive disponibili. Consulta alcune delle risorse aggiuntive disponibili nella sezione [Sezione Risorse aggiuntive](#additional-resources) per ulteriori informazioni sulle funzioni visualizzate in questo percorso.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate alcune risorse aggiuntive che approfondiscono alcuni concetti menzionati in questo documento.

* [Utilizzo della barra del sito per gestire il tema del sito](/help/sites-cloud/administering/site-creation/site-rail.md) - Scopri le potenti funzioni della barra del sito per personalizzare e gestire facilmente il tema del sito, tra cui il download delle origini tema e la gestione delle versioni del tema.
* [AEM documentazione tecnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=it) - Se hai già una conoscenza approfondita di AEM, potresti voler consultare direttamente i documenti tecnici approfonditi.
* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
* [Autorizzazioni basate sul ruolo](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - Cloud Manager dispone di ruoli preconfigurati con le autorizzazioni appropriate. Per informazioni dettagliate su questi ruoli e su come amministrarli, consulta questo documento.
* [Repository di Cloud Manager](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) - Per ulteriori informazioni su come impostare e gestire archivi Git per il progetto AEMaaCS, consulta questo documento.
* [Configurare la pipeline CI/CD - Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) - Ulteriori informazioni sulla configurazione delle tubazioni, sia full stack che front end, in questo documento.
* [Modello di sito standard AEM](https://github.com/adobe/aem-site-template-standard) - Questo è l’archivio GitHub del modello di sito standard AEM.
* [Tema sito AEM](https://github.com/adobe/aem-site-template-standard-theme-e2e) - Questo è l’archivio GitHub del tema del sito AEM.
* [npm](https://www.npmjs.com) - AEM temi utilizzati per costruire rapidamente i siti sono basati su npm.
* [webpack](https://webpack.js.org) - AEM temi utilizzati per costruire rapidamente i siti si basano su webpack.
* [Creazione e organizzazione delle pagine](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) - Questa guida descrive come gestire le pagine del sito AEM se desideri personalizzarlo ulteriormente dopo averlo creato dal modello.
* [Come lavorare con il pacchetto](/help/implementing/developing/tools/package-manager.md) - I pacchetti consentono l&#39;importazione e l&#39;esportazione del contenuto del repository. Questo documento spiega come lavorare con i pacchetti nella AEM 6.5, che si applica anche ad AEMaaCS.
* [Percorso di onboarding](/help/journey-onboarding/home.md) - Questa guida funge da punto di partenza per garantire che i team siano configurati e abbiano accesso a AEM as a Cloud Service.
* [Documentazione di Adobe Experience Manager Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it) - Esplorate la documentazione di Cloud Manager per informazioni dettagliate sulle sue funzioni.
* [Documentazione sull’amministrazione del sito](/help/sites-cloud/administering/site-creation/create-site.md) - Per ulteriori informazioni sulle funzioni dello strumento Creazione rapida di siti, consultare i documenti tecnici sulla creazione del sito.
* [Sviluppo di siti con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) - Questo documento descrive alcune considerazioni di cui tenere conto per sfruttare appieno il potenziale del processo di sviluppo front-end utilizzando la pipeline front-end.
