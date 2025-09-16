---
title: App di esempio SecurBank per l’editor universale
description: Scopri l’editor universale tramite un’esperienza pratica utilizzando l’app SecurBank, progettata per mostrare la potenza, la flessibilità e l’usabilità dell’editor universale per accelerare la creazione dei contenuti.
exl-id: 97e1395f-b51e-4cee-b1d0-2466a08f96af
feature: Developing
role: Admin, Architect, Developer
source-git-commit: c4dcb1cecb756f746ecb856fcfd65d73833a5ee0
workflow-type: ht
source-wordcount: '902'
ht-degree: 100%

---

# App di esempio SecurBank per l’editor universale {#securbank}

Scopri l’editor universale tramite un’esperienza pratica utilizzando l’app SecurBank, progettata per mostrare la potenza, la flessibilità e l’usabilità dell’editor universale per accelerare la creazione dei contenuti.

## Prerequisiti {#prerequisites}

* Per installare l’app SecurBank, devi farti assegnare al [profilo prodotto](/help/journey-onboarding/assign-profiles-aem.md) **amministratore AEM** 
* Per lo sviluppo locale devi avere installato [Node.js](https://nodejs.org) versione 20 o successiva.

## Installazione di SecurBank {#installation}

L’installazione dell’app SecurBank è immediata, ma poiché interessa molte aree di AEM as a Cloud Service sono necessari diversi passaggi. Di seguito è riportata una panoramica dei passaggi principali.

1. [Crea un programma sandbox in Cloud Manager](#create-sandbox-program).
1. [Clona l’archivio Git del programma e aggiornalo con il contenuto del progetto SecurBank AEM](#clone-and-update).
1. [Esegui la pipeline per distribuire il progetto SecurBank AEM](#run-pipeline).
1. [Recupera le credenziali di Cloud Manager per lo sviluppo di app web locali](#retrieve-credentials).
1. [Scarica e configura l’app web SecurBank](#download-web-app).
1. [Esegui l’app web SecurBank](#run-web-app).

Le sezioni seguenti descrivono in dettaglio le singole attività richieste.

### Crea un programma sandbox in Cloud Manager. {#create-sandbox-program}

Sarà necessario un nuovo programma Cloud Manager in cui installare SecurBank.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Crea un nuovo programma sandbox per l’app SecurBank.

   * Utilizza le opzioni predefinite per selezionare **Soluzioni e componenti aggiuntivi**.
   * Per informazioni dettagliate su come creare un programma sandbox, consulta il documento [Creazione di programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).

### Clona l’archivio Git del programma e aggiornalo con il contenuto del progetto SecurBank AEM. {#clone-and-update}

1. Una volta creato il programma, aprilo e nella scheda **Archivi** tocca o fai clic sul pulsante **Accedi a dati archivio** per aprire la finestra di dialogo **Informazioni archivio** e visualizzare le credenziali necessarie per accedere all’archivio Git per l’ambiente sandbox.

   * Per informazioni dettagliate su come accedere alle informazioni dell’archivio, consulta il documento [Accesso agli archivi](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. Utilizzando le credenziali nella finestra di dialogo **Informazioni archivio**, clona l’archivio nel computer locale.

1. Individuare la cartella del clone locale, aprirla ed eliminare tutto il contenuto ad eccezione dei file nascosti/punti.

1. Recupera il codice del progetto SecurBank AEM più recente da GitHub all’indirizzo [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank) facendo clic su **Codice** e quindi su **Scarica ZIP** nel menu a discesa.

1. Decomprimi il contenuto del file zip sul file system locale e spostalo nella cartella del clone locale del programma sandbox che hai provveduto a vuotare.

1. Utilizzando il terminale, passa alla cartella del progetto clonato, esegui il commit di tutti i contenuti e inviali a Git.

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### Esegui la pipeline per distribuire il progetto SecurBank AEM. {#run-pipeline}

Dopo aver eseguito il commit del progetto AEM per SecurBank nell’archivio sandbox, è possibile distribuirlo con una pipeline.

1. Torna alla scheda **Panoramica** del programma sandbox in Cloud Manager ed esegui la pipeline non di produzione full stack.

   * Deseleziona tutte le opzioni per l’esecuzione della pipeline.
   * Per ulteriori informazioni sull’esecuzione delle pipeline, consulta il documento [Gestione delle pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines).

### Recupera le credenziali di Cloud Manager per lo sviluppo di app web locali. {#retrieve-credentials}

Prima di poter eseguire l’app SecurBank, devi avere le credenziali di Cloud Manager per collegarvi l’app.

1. Mentre la pipeline è in esecuzione, torna alla scheda **Panoramica** in Cloud Manager, tocca o fai clic sul pulsante con i puntini di sospensione accanto al nome dell’ambiente e seleziona **Developer Console**.

1. In Developer Console, seleziona la scheda **Integrazioni**, quindi la scheda **Token locale** e tocca o fai clic su **Ottieni token di sviluppo locale**.

1. Con il token di accesso viene prodotto un file JSON. Copia solo il token stesso (il JSON rimanente non è necessario) in una posizione sicura per utilizzarlo in un passaggio futuro prima di chiudere Developer Console e tornare a Cloud Manager.

1. In Cloud Manager, nella scheda **Panoramica**, fai clic con il pulsante destro del mouse sull’URL dell’ambiente per copiarlo e salvarlo in un percorso sicuro per l’utilizzo in un passaggio futuro.

### Scarica e configura l’app web SecurBank. {#download-web-app}

Ora puoi scaricare e configurare l’app web SecurBank.

1. Recupera il codice app SecurBank più recente da GitHub alle [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events) facendo clic sull’indirizzo **Codice** e quindi su **Scarica ZIP** nel menu a discesa.

1. Decomprimi il contenuto del file zip sul file system locale.

1. Avvia l’editor di codice che preferisci e apri il file dell’ambiente nascosto nel progetto dell’app SecurBank all’indirizzo `summit-2024-l425-ue-z-final-with-events/react-app/.env`.

1. Apportare le modifiche seguenti al file `.env` e salvarle.

   * Per `REACT_APP_HOST_URI` incolla il valore dell’URL dell’ambiente copiato in precedenza.
   * Per `REACT_APP_DEV_TOKEN` incolla il valore del token di sviluppo locale copiato in precedenza.

### Esegui l’app web SecurBank. {#run-web-app}

Quanto hai configurato tutto, sia in Cloud Manager che in locale, puoi eseguire l’app web SecurBank.

1. Nella riga di comando del computer locale, passare alla cartella `react-app` del progetto di app SecurBank scaricato e decompresso.

1. Nella cartella `react-app` installare l’app SecurBank con il comando `node -i`.

1. Una volta installata, avviare l’app SecurBank con il comando `npm start`.

1. Se l’installazione e l’avvio sono stati completati correttamente, vedrai:

* La seguente uscita nel terminale

  ```text
  Compiled successfully!
  
  You can now view securbank in the browser.
  
    Local:            https://localhost:3000
    On Your Network:  https://192.168.1.15:3000
  
  Note that the development build is not optimized.
  To create a production build, use npm run build.
  
  webpack compiled successfully
  ```

   * e una finestra del browser aperta per l’URL `https://localhost:3000`.

      * Tieni presente che ciò è a scopo di sviluppo e, in quanto tale, non viene fornito alcun certificato valido. Pertanto, potrebbe essere necessario informare il browser per consentirgli di accedere alla pagina.

Congratulazioni. Ora l’app SecurBank è in esecuzione correttamente nel browser.

Se il contenuto non viene ancora visualizzato, verifica che la pipeline **Distribuzione a Dev** già eseguita sia stata completata correttamente.

![App SecurBank nel browser](assets/securbank.png)

{{ue-headless-auth}}

