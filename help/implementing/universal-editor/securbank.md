---
title: App di esempio SecurBank per l’editor universale
description: Scopri l’Editor universale con esperienza pratica utilizzando l’app SecurBank, progettata per mostrare la potenza, la flessibilità e l’usabilità dell’Editor universale per accelerare la creazione dei contenuti.
source-git-commit: 4b7612f423e4e728911920793e9e0a03757c7c9d
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 1%

---


# App di esempio SecurBank per l’editor universale {#securbank}

Scopri l’Editor universale con esperienza pratica utilizzando l’app SecurBank, progettata per mostrare la potenza, la flessibilità e l’usabilità dell’Editor universale per accelerare la creazione dei contenuti.

## Prerequisiti {#prerequisites}

* Devi essere assegnato al **Amministratore AEM** [profilo prodotto](/help/journey-onboarding/assign-profiles-aem.md) per installare l’app SecurBank.
* Devi avere [Node.js](https://nodejs.org) versione 20 o successiva installata per lo sviluppo locale.

## Installazione di SecurBank {#installation}

L’installazione dell’app SecurBank è immediata, ma poiché interessa molte aree dell’AEM as a Cloud Service, sono necessari diversi passaggi. Di seguito è riportata una panoramica dei passaggi principali.

1. [Crea un programma sandbox in Cloud Manager.](#create-sandbox-program)
1. [Clona l’archivio Git del programma e aggiornalo con il contenuto del progetto AEM di SecurBank.](#clone-and-update)
1. [Esegui la pipeline per distribuire il progetto AEM SecurBank.](#run-pipeline)
1. [Recupera le credenziali di Cloud Manager per lo sviluppo di app web locali.](#retrieve-credentials)
1. [Scarica e configura l’app web SecurBank.](#download-web-app)
1. [Esegui l’app web SecurBank.](#run-web-app)

Le sezioni seguenti descrivono in dettaglio le singole attività richieste.

### Crea un programma sandbox in Cloud Manager. {#create-sandbox-program}

Sarà necessario un nuovo programma Cloud Manager in cui installare SecurBank.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Crea un nuovo programma sandbox per l’app SecurBank.

   * Utilizza le opzioni predefinite durante la selezione **Soluzioni e componenti aggiuntivi**.
   * Per informazioni dettagliate su come creare un programma sandbox, consulta il documento [Creazione di programmi sandbox.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)

### Clona l’archivio Git del programma e aggiornalo con il contenuto del progetto AEM di SecurBank. {#clone-and-update}

1. Una volta creato il programma, aprilo e sul **Archivi** , tocca o fai clic sulla scheda **Accedi a dati archivio** per aprire **Informazioni archivio** e visualizzare le credenziali necessarie per accedere all’archivio Git per l’ambiente sandbox.

   * Per informazioni dettagliate su come accedere alle informazioni dell’archivio, consulta il documento [Accesso agli archivi.](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. Utilizzo delle credenziali in **Informazioni archivio** nella finestra di dialogo, clona l’archivio sul computer locale.

1. Individuare la cartella del clone locale, aprirla ed eliminare tutto il contenuto ad eccezione dei file nascosti/punti.

1. Recupera il codice del progetto AEM SecurBank più recente da GitHub all’indirizzo [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank) facendo clic su **Codice** e poi **Scarica ZIP** nel menu a discesa.

1. Decomprimi il contenuto del file zip sul file system locale e spostalo nella cartella ora vuota del clone locale del programma sandbox.

1. Utilizzando il terminale, passa alla cartella del progetto clonato, esegui il commit di tutti i contenuti e inviali a Git.

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### Esegui la pipeline per distribuire il progetto AEM SecurBank. {#run-pipeline}

Con il commit del progetto AEM per SecurBank nell’archivio sandbox, è possibile distribuirlo con una pipeline.

1. Torna a **Panoramica** del programma sandbox in Cloud Manager ed esegui la pipeline non di produzione full stack.

   * Deseleziona tutte le opzioni per l’esecuzione della pipeline.
   * Per ulteriori informazioni sull’esecuzione delle pipeline, consulta il documento [Gestione delle pipeline.](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)

### Recupera le credenziali di Cloud Manager per lo sviluppo di app web locali. {#retrieve-credentials}

Prima di poter eseguire l’app SecurBank, sono necessarie le credenziali di Cloud Manager per connettersi a Cloud Manager.

1. Quando la pipeline è in esecuzione, torna a **Panoramica** in Cloud Manager, tocca o fai clic sul pulsante con i puntini di sospensione accanto al nome dell’ambiente e seleziona **Console per sviluppatori**.

1. Nella Console per sviluppatori, seleziona la **Integrazioni** , quindi la scheda **Token locale** tocca o fai clic su **Ottieni token di sviluppo locale**.

1. Un file JSON viene prodotto con il token di accesso. Copia solo il token stesso (il JSON rimanente non è necessario) in una posizione sicura da utilizzare in un passaggio futuro prima di chiudere Developer Console e tornare a Cloud Manager.

1. Torna a Cloud Manager, sulla **Panoramica** , fai clic con il pulsante destro del mouse sull’URL dell’ambiente per copiarlo e salvarlo in un percorso sicuro da utilizzare in un passaggio futuro.

### Scarica e configura l’app web SecurBank. {#download-web-app}

Ora puoi scaricare e configurare l’app web SecurBank.

1. Recupera il codice app SecurBank più recente da GitHub all’indirizzo [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events) facendo clic su **Codice** e poi **Scarica ZIP** nel menu a discesa.

1. Decomprimi il contenuto del file zip sul file system locale.

1. Avvia l’editor di codice preferito e apri il file dell’ambiente nascosto nel progetto dell’app SecurBank all’indirizzo `summit-2024-l425-ue-z-final-with-events/react-app/.env`.

1. Apporta le seguenti modifiche al `.env` e salvare le modifiche.

   * Per `REACT_APP_HOST_URI` incolla il valore dell’URL dell’ambiente copiato in precedenza.
   * Per `REACT_APP_DEV_TOKEN` incolla il valore del token di sviluppo locale copiato in precedenza.

### Esegui l’app web SecurBank. {#run-web-app}

Con tutto ciò che è configurato sia in Cloud Manager che localmente, puoi eseguire l’app web SecurBank.

1. Nella riga di comando del computer locale, passare alla `react-app` cartella del progetto di app SecurBank scaricato e decompresso.

1. Nel tuo `react-app` cartella installa l’app SecurBank con `node -i` comando.

1. Una volta installata, avvia l’app SecurBank con `npm start` comando.

1. Se l&#39;installazione e l&#39;avvio sono stati completati correttamente, verranno visualizzati i seguenti elementi:

* La seguente uscita nel terminale.

  ```text
  Compiled successfully!
  
  You can now view securbank in the browser.
  
    Local:            https://localhost:3000
    On Your Network:  https://192.168.1.15:3000
  
  Note that the development build is not optimized.
  To create a production build, use npm run build.
  
  webpack compiled successfully
  ```

   * E una finestra del browser aperta per l’URL `https://localhost:3000`.

      * Tieni presente che ciò è a scopo di sviluppo e, in quanto tale, non viene fornito alcun certificato valido. Pertanto, potrebbe essere necessario informare il browser per consentirgli di accedere alla pagina.

Congratulazioni Ora l’app SecurBank è in esecuzione correttamente nel browser.

Se il contenuto non viene ancora visualizzato, verificare che **Implementa in Dev** pipeline eseguita correttamente.

![App SecurBank nel browser](assets/securbank.png)
