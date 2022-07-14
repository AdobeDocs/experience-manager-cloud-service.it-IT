---
title: Attività di Developer Manager e Deployment Manager
description: Una volta che l’amministratore di sistema ha configurato le risorse cloud necessarie, scopri come gli sviluppatori e i responsabili della distribuzione possono accedere a Git per sviluppare applicazioni e utilizzare le pipeline per distribuirle.
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 2%

---


# Attività di Developer Manager e Deployment Manager {#developer-deployment-manager}

In questa parte facoltativa del [percorso di bordo,](overview.md) scoprirai come gli sviluppatori e i responsabili della distribuzione possono accedere a git per sviluppare applicazioni e utilizzare le pipeline per distribuirle.

## La storia finora {#story-so-far}

Hai fatto molta strada nel tuo percorso di onboarding! Congratulazioni! L&#39;amministratore di sistema ha completato il percorso di onboarding configurando le risorse cloud necessarie e concedendo l&#39;accesso nel documento [Assegnazione AEM profili di prodotto.](assign-profiles-aem.md)

A questo punto gli sviluppatori e i responsabili di implementazione possono iniziare a creare applicazioni personalizzate, mentre gli utenti AEM possono iniziare a creare contenuti. In questo senso, l&#39;onboarding è completo e ora è il momento di utilizzare il nuovo sistema as a Cloud Service AEM, che verrà illustrato in questo documento.

## Pubblico {#audience}

Il presente documento è pertanto redatto dal punto di vista della **sviluppatore** e **gestione distribuzione**.

Anche l’amministratore di sistema può eseguire queste stesse attività, ma in genere questi ruoli sono gestiti da utenti diversi.

## Obiettivo {#objective}

Questo documento è un complemento al percorso di onboarding per illustrare le attività di base di uno sviluppatore e di un gestore di distribuzione dopo che l’amministratore di sistema ha effettuato l’onboarding di tutti gli utenti e creato le risorse cloud necessarie.

Dopo aver letto questo documento, dovresti:

* In qualità di sviluppatore, scopri come accedere e gestire gli archivi Git di Cloud Manager.
* In qualità di gestore dell’implementazione, puoi configurare le pipeline e distribuire il codice in Cloud Manager.

## Sviluppatori e gestori di distribuzione {#roles}

Una volta che l’amministratore di sistema ha completato le principali attività di onboarding relative alla creazione di utenti e alla configurazione di risorse cloud, gli utenti in genere più ansiosi di accedere al sistema sono gli sviluppatori e i manager di implementazione. Questo perché sono gli utenti responsabili della creazione delle applicazioni personalizzate oltre a AEM as a Cloud Service.

* **Sviluppatori** - Questi utenti accedono agli archivi Git di Cloud Manager e gestiscono il codice per le tue applicazioni personalizzate AEM.
* **Manager di distribuzione** - Questi utenti utilizzano Cloud Manager per creare ed eseguire pipeline che distribuiscono il codice dagli archivi Git agli ambienti AEM in esecuzione.

A seconda delle esigenze organizzative, gli stessi utenti possono avere entrambi i ruoli.

## Prerequisiti {#prerequisites}

Prima di iniziare le attività descritte in questo documento come sviluppatore o responsabile della distribuzione, assicurati che l’amministratore di sistema abbia completato tutti i passaggi di questo percorso di onboarding. Ciò significa che:

* L’amministratore di sistema ha assegnato gli sviluppatori e i manager di implementazione ai rispettivi profili di prodotto.
* Gli sviluppatori devono essere inoltre assegnati a **Utenti AEM** o **Amministratori AEM** profili di prodotto per utilizzare anche AEM.
* Risorse cloud configurate.

## Accesso a Git {#accessing-git}

Puoi accedere e gestire gli archivi git utilizzando la gestione degli account git self-service di Cloud Manager.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Tubi** scheda da **Panoramica del programma** e trova la **Accesso alle informazioni sul repository** per accedere e gestire il tuo archivio Git.

   ![Pulsante Accedi alle informazioni sui repository nella scheda Ambienti](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Fai clic sul pulsante **Visualizza informazioni repository** per aprire una finestra di dialogo da visualizzare:

   * URL dell’archivio Git di Cloud Manager.
   * Nome utente git.
   * La password git, il cui valore viene visualizzato quando **Genera password** fai clic su .

   ![Informazioni sul repository](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Utilizzando queste credenziali, l’utente può clonare una copia locale dell’archivio, apportare modifiche all’archivio locale e, quando è pronto, eseguire il commit di eventuali modifiche al codice nell’archivio del codice remoto in Cloud Manager.

## Configurazione della pipeline {#setup-pipeline}

Dopo che gli sviluppatori hanno aggiunto il codice personalizzato agli archivi git, il gestore della distribuzione può creare ed eseguire pipeline per distribuire tale codice negli ambienti AEM.

Segui questi passaggi per creare la tua prima pipeline di distribuzione non di produzione.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Accedere al **Tubi** scheda dalla schermata principale di Cloud Manager. Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline non di produzione**.

   ![Aggiungere una pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. Sulla **Configurazione** della scheda **Aggiungi pipeline non di produzione** selezionate il tipo di pipeline non di produzione con cui desiderate aggiungere. Per questo esempio, seleziona **Pipeline di distribuzione**.

   ![Finestra di dialogo Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Fornisci un **Nome della pipeline non di produzione** per identificare la pipeline con le seguenti informazioni aggiuntive.

1. Per **Trigger distribuzione** select **Manuale** in modo che la pipeline venga eseguita solo all’avvio.

1. Fai clic su **Continua**.

1. Sulla **Codice sorgente** della scheda **Aggiungi pipeline non di produzione** È necessario selezionare il tipo di codice che la pipeline deve elaborare. Per questo esempio, seleziona **Codice Stack Completo**.

1. Sulla **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Ambienti di distribuzione idonei** - È necessario scegliere l’ambiente in cui distribuire la pipeline.
   * **Archivio** - Questa opzione definisce da quale git repo la pipeline deve recuperare il codice.
   * **Ramo Git** - Questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice.
      * Immetti i primi caratteri del nome del ramo e la funzione di completamento automatico di questo campo troverà i rami corrispondenti per aiutarti a selezionare.

   ![pipeline a stack completo](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Fai clic su **Salva**.

Ora hai creato la tua prima pipeline! Gli utenti con il ruolo di gestione distribuzione possono ora avviare la pipeline dall’interfaccia utente di Cloud Manager.

## Implementare {#deploy}

Ora che gli sviluppatori hanno aggiunto il loro codice personalizzato agli archivi Git e hai una pipeline creata per distribuire tale codice, è ora di eseguire la pipeline per spostare effettivamente quel codice da Git al tuo ambiente.

![Scheda pipeline in Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Tubi** scheda da **Panoramica del programma** fate clic sul pulsante dei puntini di sospensione accanto alla pipeline creata nella sezione precedente e selezionate **Esegui** dal menu.

1. L’esecuzione della pipeline inizia ed è indicata dalla **Stato** colonna.

Per visualizzare i dettagli dell&#39;esecuzione, fai nuovamente clic sul pulsante con i puntini di sospensione e seleziona **Visualizza dettagli**.

Congratulazioni! Il codice è stato ora distribuito dall’archivio Git a un ambiente non di produzione.

## Novità {#whats-next}

Dopo aver letto questo documento, devi:

* In qualità di sviluppatore, scopri come accedere e gestire gli archivi Git di Cloud Manager.
* In qualità di gestore dell’implementazione, puoi configurare le pipeline e distribuire il codice in Cloud Manager.

Hai lavorato a terra come sviluppatore o manager di implementazione con conoscenze di lavoro non solo su Cloud Manager, ma anche su ambienti di lavoro, archivi e pipeline! Ma c&#39;è di più per conoscere AEM potenti strumenti CI/CD di as a Cloud Service. Consulta la sezione [Risorse aggiuntive](#additional-resources) per ulteriori dettagli.

Se sei interessato a come gli autori dei contenuti accedono e utilizzano AEM as a Cloud Service, continua sulla parte finale del percorso di onboarding, [Attività utente AEM.](aem-users.md)

>[!TIP]
>
>Ora che sei onboarding, puoi [scopri come aggiungere facilmente il componente aggiuntivo Demos di riferimento AEM](/help/journey-sites/demos-add-on/overview.md) in un ambiente sandbox con una configurazione AEM minima ed essere in grado di testare le potenti funzioni di AEM con esempi avanzati basati sulle best practice.

## Risorse aggiuntive {#additional-resources}

* [Accesso agli archivi](/help/implementing/cloud-manager/managing-code/accessing-repos.md) - Scopri come accedere e gestire l’archivio Git utilizzando la gestione autonoma dell’account Git di Cloud Manager.
* [Utilizzo di Git con Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) - Scopri come utilizzare gli archivi Git di Cloud Manager e come integrare il tuo archivio Git gestito dai clienti on-premise con Cloud Manager.
* [Configurazione ambiente di sviluppo locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=it) - Questa esercitazione descrive come configurare un ambiente di sviluppo locale per Adobe Experience Manager (AEM) utilizzando l’SDK as a Cloud Service AEM.
* [Guida introduttiva ad AEM Sites - Tutorial WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it) - Questa esercitazione in più parti è stata progettata per gli sviluppatori che non hanno mai utilizzato Adobe Experience Manager (AEM). Questa esercitazione illustra l’implementazione di un sito AEM per un brand di lifestyle fittizio WKND. L’esercitazione tratta argomenti fondamentali come la configurazione del progetto, i componenti core, i modelli modificabili, le librerie lato client e lo sviluppo dei componenti con Adobe Experience Manager Sites.
* [Guida introduttiva a SPA in AEM con React](/help/implementing/developing/hybrid/getting-started-react.md) - Questo articolo presenta un esempio di applicazione SPA, spiega come viene messa insieme e ti permette di iniziare a lavorare con il tuo SPA rapidamente utilizzando il framework React.
* [Guida introduttiva a SPA in AEM Utilizzo di Angular](/help/implementing/developing/hybrid/getting-started-angular.md) - Questo articolo presenta un esempio di applicazione SPA, spiega come viene assemblato, e ti permette di iniziare a lavorare con il tuo SPA rapidamente utilizzando il framework di Angular.
* [Percorso per sviluppatori headless](/help/journey-headless/developer/overview.md) - Inizia qui un corso guidato per lo sviluppo di applicazioni headless con AEM.
