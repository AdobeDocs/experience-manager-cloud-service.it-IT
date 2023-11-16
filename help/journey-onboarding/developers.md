---
title: Attività dei ruoli Sviluppatore e Responsabile dell’implementazione
description: Quando l’amministratore di sistema ha configurato le risorse cloud necessarie, gli utenti con ruolo Sviluppatore e Responsabile dell’implementazione possono accedere a Git per sviluppare applicazioni e distribuirle con le pipeline.
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 90%

---


# Attività dei ruoli Sviluppatore e Responsabile dell’implementazione {#developer-deployment-manager}

In questa parte facoltativa del [percorso di onboarding,](overview.md) scopri come sviluppatori e responsabili dell’implementazione possono accedere a git per sviluppare applicazioni e distribuirle con le pipeline.

## Percorso affrontato finora {#story-so-far}

Hai fatto molta strada nel tuo percorso di onboarding. Congratulazioni. L’amministratore di sistema ha completato il percorso di onboarding configurando le risorse cloud necessarie e concedendo l’accesso nel documento [Assegnazione dei profili di prodotto di AEM.](assign-profiles-aem.md)

Ora gli utenti con i ruoli Sviluppatore e Responsabile dell’implementazione possono iniziare a creare applicazioni personalizzate, mentre gli utenti AEM possono iniziare a creare contenuti. In questo senso, il percorso di onboarding è completo e ora è possibile utilizzare il nuovo sistema AEM as a Cloud Service illustrato in questo documento.

## Pubblico {#audience}

Il presente documento è redatto dalla prospettiva degli utenti con ruolo **Sviluppatore** e **Responsabile dell’implementazione**.

Anche l’amministratore di sistema può eseguire queste attività, ma in genere questi ruoli sono gestiti da utenti diversi.

## Obiettivo {#objective}

Questo documento è supplementare al percorso di onboarding per illustrare le attività di base degli utenti con ruolo Sviluppatore e Responsabile dell’implementazione dopo che l’amministratore di sistema ha effettuato l’onboarding di tutti gli utenti e creato le risorse cloud necessarie.

Dopo aver letto questo documento, dovresti:

* Sapere come accedere e gestire gli archivi Git di Cloud Manager come utente con ruolo Sviluppatore.
* Sapere come configurare le pipeline e distribuire il codice in Cloud Manager come utente con ruolo Responsabile dell’implementazione.

## Ruoli Sviluppatore e Responsabile dell’implementazione {#roles}

Una volta che l’amministratore di sistema ha completato le principali attività di onboarding relative alla creazione di utenti e alla configurazione delle risorse cloud, gli utenti con maggiore necessità di accedere al sistema sono in genere sviluppatori e responsabili dell’implementazione. Questo perché si tratta degli utenti responsabili della generazione delle applicazioni personalizzate con AEM as a Cloud Service.

* **Sviluppatori**: questi utenti accedono agli archivi Git di Cloud Manager e gestiscono il codice per le applicazioni AEM personalizzate.
* **Responsabili dell’implementazione**: questi utenti utilizzano Cloud Manager per creare ed eseguire pipeline per la distribuzione del codice dagli archivi Git negli ambienti AEM in esecuzione.

A seconda delle esigenze dell’organizzazione, gli stessi utenti possono avere entrambi i ruoli.

## Prerequisiti {#prerequisites}

Prima di iniziare le attività descritte in questo documento come utente con ruolo Sviluppatore o Responsabile dell’implementazione, assicurati che l’amministratore di sistema abbia completato tutti i passaggi di questo percorso di onboarding. Ciò significa che:

* L’amministratore di sistema ha assegnato sviluppatori e responsabili dell’implementazione ai rispettivi profili di prodotto.
* Gli sviluppatori sono stati inoltre assegnati ai profili di prodotto **Utenti AEM** o **Amministratori AEM** per poter utilizzare AEM.
* Le risorse cloud sono state configurate.

## Accesso a Git {#accessing-git}

È possibile accedere e gestire gli archivi Git con la gestione self-service dell’account Git di Cloud Manager.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, accedi alla scheda **Pipeline** e individua il pulsante **Accedi a dati archivio** per accedere e gestire il tuo archivio Git.

   ![Pulsante Accedi a dati archivio nella scheda Ambienti](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Fai clic su **Visualizza informazioni archivio** per aprire una finestra di dialogo e visualizzare:

   * L’URL dell’archivio Git di Cloud Manager.
   * Il nome utente di Git.
   * La password di Git, il cui valore viene visualizzato quando fai clic sul pulsante **Genera password**.

   ![Informazioni sull’archivio](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Con queste credenziali l’utente può clonare una copia locale dell’archivio, apportare qui le modifiche e, una volta terminato, riconfermarle nell’archivio del codice remoto in Cloud Manager.

## Configurazione della pipeline {#setup-pipeline}

Dopo che gli sviluppatori hanno aggiunto il codice personalizzato agli archivi Git, l’utente con il ruolo Responsabile dell’implementazione può creare ed eseguire pipeline per distribuire tale codice negli ambienti AEM.

Per creare la prima pipeline di distribuzione non di produzione, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Accedi alla scheda **Pipeline** dalla pagina Home di Cloud Manager. Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline non di produzione**.

   ![Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. Dalla scheda **Configurazione** della finestra di dialogo **Aggiungi pipeline non di produzione**, seleziona il tipo di pipeline non di produzione che desideri aggiungere. Per questo esempio, seleziona **Pipeline di distribuzione**.

   ![Finestra di dialogo Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Per identificare la pipeline, fornisci un **nome della pipeline non di produzione** con le seguenti informazioni aggiuntive.

1. Per **Trigger distribuzione**, seleziona **Manuale** in modo che la pipeline venga eseguita solo quando avviata dall’utente.

1. Fai clic su **Continua**.

1. Dalla scheda **Codice sorgente** della finestra di dialogo **Aggiungi pipeline non di produzione**, seleziona il tipo di codice da elaborare con la pipeline. Per questo esempio, seleziona **Codice full stack**.

1. Nella scheda **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Ambienti di distribuzione idonei**: seleziona l’ambiente in cui eseguire la distribuzione della pipeline.
   * **Archivio**: definisce l’archivio Git dal quale la pipeline deve recuperare il codice.
   * **Ramo Git**: definisce il ramo della pipeline selezionata dal quale recuperare il codice.
      * Digitando i primi caratteri del nome del ramo, la funzione di completamento automatico del campo troverà i rami corrispondenti per supportare nella selezione.

   ![Pipeline full stack](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Fai clic su **Salva**.

Hai appena creato la tua prima pipeline. Ora gli utenti con il ruolo Responsabile dell’implementazione possono avviare la pipeline dall’interfaccia utente di Cloud Manager.

## Distribuzione {#deploy}

Ora che il team di sviluppo ha aggiunto il codice personalizzato agli archivi Git e che disponi di una pipeline creata per distribuire tale codice, puoi eseguire la pipeline per trasferire effettivamente il codice dall’archivio Git all’ambiente.

![Scheda Pipeline in Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Accedi a **Pipeline** scheda da **Panoramica del programma** e fai clic sul pulsante con i puntini di sospensione a fianco della pipeline creata nella sezione precedente, quindi seleziona **Esegui** dal menu.

1. L’esecuzione della pipeline viene avviata ed è indicata dalla colonna **Stato**.

Per visualizzare i dettagli dell’esecuzione, fai nuovamente clic sul pulsante con i puntini di sospensione e seleziona **Visualizza dettagli**.

Congratulazioni. Hai distribuito il codice dall’archivio Git a un ambiente non di produzione.

## Passaggio successivo {#whats-next}

Ora che hai letto questo documento, dovresti:

* Sapere come accedere e gestire gli archivi Git di Cloud Manager come utente con ruolo Sviluppatore.
* Sapere come configurare le pipeline e distribuire il codice in Cloud Manager come utente con ruolo Responsabile dell’implementazione.

Hai completato con successo il tuo percorso come utente Sviluppatore o Responsabile dell’implementazione acquisendo non solo competenze lavorative su Cloud Manager, ma anche su ambienti di lavoro, archivi e pipeline. Tuttavia, c’è altro da scoprire sui potenti strumenti CI/CD di AEM as a Cloud Service. Per ulteriori informazioni, consulta la sezione [Risorse aggiuntive](#additional-resources).

Se ti interessa scoprire come accedere e utilizzare AEM as a Cloud Service come autore di contenuti, continua con la sezione finale del percorso di onboarding [Attività degli utenti AEM.](aem-users.md)

>[!TIP]
>
>Ora che hai completato l’onboarding, [scopri come aggiungere facilmente il componente aggiuntivo AEM Reference Demos](/help/journey-sites/demos-add-on/overview.md) a un ambiente sandbox con una configurazione di AEM minima e come testare le potenti funzioni di AEM con esempi dettagliati basati sulle best practice.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate risorse aggiuntive e opzionali utili per andare oltre il contenuto del percorso di onboarding.

* [Accesso agli archivi](/help/implementing/cloud-manager/managing-code/accessing-repos.md): scopri come accedere e gestire l’archivio Git con la gestione self-service dell’account Git di Cloud Manager.
* [Utilizzo di Git con Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md): scopri come utilizzare gli archivi Git di Cloud Manager e come integrare un archivio Git personalizzato e gestito dal cliente on-premise con Cloud Manager.
* [Configurazione dell’ambiente di sviluppo locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=it): questo tutorial illustra i passaggi necessari per la configurazione di un ambiente di sviluppo locale per Adobe Experience Manager (AEM) con l’SDK di AEM as a Cloud Service.
* [Guida introduttiva di AEM Sites: tutorial WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it): questo tutorial in più sezioni è concepito per sviluppatori e sviluppatrici che utilizzano per la prima volta Adobe Experience Manager (AEM). Questo tutorial illustra l’implementazione di un sito AEM per un brand di lifestyle fittizio, WKND. Il tutorial tratta elementi fondamentali come la configurazione del progetto, i componenti core, i modelli modificabili, le librerie lato client e lo sviluppo di componenti con Sites di Adobe Experience Manager.
* [Guida introduttiva dell’SPA nell’AEM con React](/help/implementing/developing/hybrid/getting-started-react.md) - Questo articolo presenta un esempio di applicazione per l’SPA, spiega come viene creata e come iniziare a utilizzare il proprio SPA in modo rapido utilizzando il framework React.
* [Guida introduttiva dell’SPA nell’AEM con l’uso di Angular](/help/implementing/developing/hybrid/getting-started-angular.md) - Questo articolo presenta un esempio di applicazione per l’SPA, spiega come viene creata e come iniziare subito a utilizzare il proprio SPA utilizzando il framework Angular.
* [Percorso di sviluppo headless](/help/journey-headless/developer/overview.md): inizia qui il tuo percorso guidato per sviluppare applicazioni headless con AEM.
