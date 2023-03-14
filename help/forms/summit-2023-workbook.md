---
title: Creare Forms coinvolgenti utilizzando componenti core e headless
seo-title: Build Engaging Forms Using Core Components and Headless
description: Creare Forms coinvolgenti utilizzando componenti core e headless
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
source-git-commit: 8f3ffc72507be1d28bc437041579578d6a479e23
workflow-type: tm+mt
source-wordcount: '2453'
ht-degree: 1%

---


# Creare Forms coinvolgenti utilizzando componenti core e headless

## Panoramica di Lab

In questo laboratorio pratico imparerai:

Come utilizzare AEM Forms per creare facilmente moduli adattivi utilizzando i componenti core più recenti che sono coerenti con AEM Sites, abilitare esperienze di acquisizione dati omnicanale distribuendo i moduli adattivi come moduli headless su web, dispositivi mobili e chat. Inoltre, scopri le best practice su stile, personalizzazioni e sviluppo front-end.

## Punti chiave da eliminare

* **Agilità aziendale**: in qualità di utente aziendale, posso creare facilmente esperienze modulo per più canali.

* **Potere per sviluppatori front-end**: in qualità di sviluppatore front-end, posso controllare l’esperienza dell’utente finale utilizzando moduli headless.

* **Velocità sviluppatore**: in qualità di sviluppatore, posso personalizzare facilmente e in modo coerente i componenti Sites e Forms.

## Prerequisiti

Sandbox AEM Forms as Cloud Service

## Lezione 1

### Obiettivo

Acquisisci familiarità con l’ambiente as a Cloud Service di AEM Forms.

### Contesto della lezione

In questa lezione, imparerai a conoscere l’ambiente as a Cloud Service di AEM Forms navigando nell’interfaccia utente di.

### Esercizio

1. Apri il browser e immetti l’URL dell’ambiente di authoring del Cloud Service. Esempio:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Accedi all’ambiente di authoring del Cloud Service in base alle credenziali condivise. Esempio: Username: [L716+001@summitlab.us](mailto:L716%2B001@summitlab.us)
Password: 
**Adobe 123!**

1. Dopo aver effettuato l’accesso, passa all’interfaccia utente di AEM Forms. Clic **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Clic **Forms e documenti**. Ignora eventuali popup relativi a preferenze o informazioni.

   ![](/help/forms/assets/screenshot2028113929.png)

   Vengono visualizzati tutti i moduli disponibili.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lezione 2

### Obiettivo

Crea un modulo adattivo utilizzando i Componenti core più recenti, configura e invia il modulo.

## Contesto della lezione

In questa lezione, in qualità di utente aziendale, creerai un modulo adattivo per più canali come web, dispositivi mobili e chat utilizzando l’authoring di moduli adattivi con componenti OOTB di base standardizzati per l’acquisizione dei dati.

## Esercizio

1. Crea un endpoint di invio per il modulo:

   1. Apri <https://requestbin.com/> in una nuova scheda del browser.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Clic **Creare un raccoglitore pubblico** e copia l’URL dell’endpoint.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Creare un modulo adattivo tramite l’interfaccia della procedura guidata:

   1. Nella scheda del browser utilizzata nella lezione 1, passa ad AEM Forms come interfaccia web di Cloud Service e passa a Forms e Documenti.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Clic **Crea** e seleziona Modulo adattivo.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Seleziona la **Vuoto con i Componenti core** modello dalla schermata di selezione del modello, come illustrato di seguito:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Fai clic su **Stile** e seleziona la scheda **wknd-theme** tema come mostrato di seguito:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Fai clic su **Invio** e seleziona la scheda **Invia a endpoint REST** e specificare il raccoglitore pubblico nel
      **URL per la richiesta POST** come mostrato di seguito:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Fai clic su **Crea**. Specificare un nome e un titolo per il modulo. Ad esempio: **contatto**. Fai clic su **Crea**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. Viene aperto l’editor di moduli adattivi. Ignorare eventuali finestre a comparsa o finestre di dialogo per informazioni o preferenze. Fai clic sul browser Componenti nella barra a sinistra e aggiungi **Piè di pagina** nella parte inferiore del modulo vuoto.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. Aggiungi il **Intestazione** nella parte superiore del modulo.
      ![](/help/forms/assets/screenshot2028122029.png)

   1. Aggiungi un **Titolo** al centro del modulo.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Aggiungi un **Input testo** dopo il componente titolo.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Aggiungi un **Input numero** componente.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Aggiungi un **Pulsante Invia** al modulo.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Fai clic su **Titolo** in modo che **menu a comparsa** viene visualizzato. Fai clic su **Icona Modifica** nel menu per modificare l’etichetta.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Invio `Contact Us` come testo del titolo.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Fai clic su **Input testo** in modo da visualizzare il menu a comparsa. Fai clic su **Icona Modifica** nel menu per modificare l’etichetta.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Invio **Nome e cognome** come etichetta campo.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Fai clic su **Input numero** in modo da visualizzare il menu a comparsa. Fai clic su **Icona Modifica** nel menu per modificare l’etichetta.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Inserisci il **Numero di telefono** come etichetta del campo.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Aggiungi convalide al modulo:

   1. Fai clic su **Numero di telefono** in modo da visualizzare il menu a comparsa. Fai clic su **Icona chiave inglese** nel menu per configurare il campo.
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Apri **scheda convalide**, contrassegna il campo **Obbligatorio** e fai clic su **Fine**. Viene visualizzato il messaggio di operazione riuscita.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Clic **Anteprima** per visualizzare l&#39;anteprima del modulo dal punto di vista dell&#39;utente finale.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Compila il modulo con dati fittizi
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Invia il modulo
      ![](/help/forms/assets/screenshot2028125729.png)

   1. Nella scheda Cestino richieste, seleziona i dati inviati.
      ![](/help/forms/assets/screenshot2028125829.png)

Per il resto dell&#39;esercizio, utilizzare un modulo di registrazione precreato.

1. Apri l’interfaccia di gestione di AEM Forms, ad esempio, `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`e seleziona il modulo di registrazione.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Fate clic su **Pubblica**. 

   ![](/help/forms/assets/screenshot2028115629.png)

   Viene visualizzato il messaggio di operazione riuscita.

   ![](/help/forms/assets/screenshot2028115729.png)

   L’URL di pubblicazione del modulo sarà simile a `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Per visualizzare il modulo pubblicato, sostituisci l’ID del programma (pXXXXXX) e l’ID dell’ambiente (eXXXXXX) nell’URL indicato sopra con gli ID dell’ambiente.

## Lezione 3

### Obiettivo

Aggiorna gli stili utilizzando le best practice per lo sviluppo front-end.

### Contesto della lezione

In questa lezione, in qualità di sviluppatore front-end, scopri come aggiornare facilmente lo stile del modulo adattivo creato in precedenza.

### Esercizio

Imposta archivio locale del tema:

1. Aprire il prompt dei comandi o la shell con i diritti di amministratore:

   ![](/help/forms/assets/screenshot2028115829.png)

1. Al prompt dei comandi utilizzare il comando seguente per passare a **c:\git** cartella

   ```Shell
   cd c:\git
   ```

1. Utilizza il comando seguente per clonare il codice front-end del tema:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Utilizza il seguente comando nell’ordine elencato per passare al **aem-forms-theme-canvas** e aprire Visual Studio Code.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Seleziona **Considera attendibili gli autori di tutti i file nella cartella principale** e fai clic su **Sì, mi fido degli autori**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Per eseguire il rendering del modulo ospitato nell’ambiente di pubblicazione del servizio cloud, rinomina il `env_template` file.  Per rinominare il file, fare clic con il pulsante destro del mouse su **env_template** e seleziona la **Rinomina** opzione.

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Imposta i seguenti valori per le variabili nel file .env e salva il file:

   * **URL_AEM**: specifica l’ambiente di pubblicazione del servizio cloud. Esempio, `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **MODULO_ADATTIVO_AEM**: specifica il percorso del modulo. Ad esempio, se il percorso del modulo è `/content/forms/af/registration`, il valore di questa variabile sarà `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)

   ![](/help/forms/assets/screenshot20228116569.png)


1. Nella finestra Prompt dei comandi eseguire il comando seguente:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Se ricevi un messaggio che richiede di aggiornare npm tramite `npm notice Run npm nstall -g npm@9.6.0`ignorare il messaggio.
   > * Non eseguire altri comandi npm se non indicato nella cartella di lavoro.


1. Eseguire il comando seguente per visualizzare l&#39;anteprima del modulo.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   Una volta eseguito il comando precedente, attendere che `webpack compiled` messaggio. Il modulo viene visualizzato in una scheda del browser.

   >[!NOTE]
   >
   >Se visualizzi una schermata vuota nel browser dopo l’esecuzione di `npm run live` comando, cambia `localhost` nell’URL del browser a 127.0.0.1 e hit **Invio**.



   ![](/help/forms/assets/screenshot2028115129.png)


1. In Visual Studio Code aprire `PROJECT\src\site\_variables.scss` file. Osserva `$error` Il colore è una tonalità di ROSSO.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Nel browser, invia il modulo per visualizzare il colore Rosso nel **Nome** campo.

   ![](/help/forms/assets/screenshot2028120829.png)

1. Imposta il **$error** colore a **#5736eb** e salva il file.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Aggiorna il browser e invia il modulo. Il colore dell&#39;errore nel campo del nome è stato modificato di conseguenza.

   ![](/help/forms/assets/screenshot2028121129.png)

1. Nel prompt dei comandi, premere **CTRL+C**, immetti **Y**, e premere **Invio** chiave per terminare il processo npm. È importante arrestare il server npm in modo che non sia in conflitto con il successivo set di esercizi.
1. Chiudere le finestre Codice di Visual Studio e Prompt dei comandi.

## Lezione 4

### Obiettivo

Esegui il rendering del modulo su web/mobile e altre interfacce come modulo headless.

### Contesto della lezione

In questa lezione, come sviluppatore front-end, scoprirai come eseguire il rendering del modulo adattivo creato in precedenza come modulo headless utilizzando il framework di progettazione dello spettro di react.

### Esercizio

Configura archivio locale utilizzando il progetto iniziale React:

1. Aprire il prompt dei comandi utilizzando i diritti di amministratore.

   ![](/help/forms/assets/screenshot2028115829.png)

1. Al prompt dei comandi utilizzare il comando seguente per passare a **c:\git** cartella

   ```Shell
   cd c:\git
   ```

1. Utilizza il seguente comando per clonare il progetto iniziale di react del modulo adattivo:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Utilizza i seguenti comandi nell’ordine elencato per passare al **react-starter-kit-aem-headless-forms** e aprire Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   Viene visualizzata la finestra Codice di Visual Studio.

   ![](/help/forms/assets/screenshot2028117429.png)

Per eseguire il rendering del modulo ospitato nell’ambiente di pubblicazione del servizio cloud:

1. Rinominare il file env_template in file env. Per rinominare, fare clic con il pulsante destro del mouse sulla **env_template** e seleziona la **Rinomina** opzione.

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Imposta i seguenti valori per le variabili nel file .env. Dopo aver aggiornato le variabili, salva il file.

   * **URL_AEM**: specifica l’URL dell’ambiente di pubblicazione del servizio cloud. Esempio, `https://publish-p105303-e986623.adobeaemcloud.com`

   * **PERCORSO_MODULO_AEM**: specifica il percorso del modulo adattivo creato nella lezione precedente. Esempio, `/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Apri la finestra dei comandi, accertati di trovarti nella directory react-starter-kit-aem-headless-forms ed esegui il seguente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. Nella finestra Prompt dei comandi eseguire il comando seguente:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   Il comando precedente avvia un server di sviluppo locale che esegue il rendering della definizione del modulo recuperata dall’AEM in modo headless utilizzando la libreria front-end react-spectrum.

   >[!NOTE]
   >
   >Se visualizzi una schermata vuota nel browser dopo l’esecuzione di `npm start` comando, cambia `localhost` nell’URL del browser a 127.0.0.1 e hit **Invio**.

   ![](/help/forms/assets/screenshot2028118229.png)

Controlliamo l’esecuzione delle regole in questo modulo headless:

1. Seleziona la **Seleziona la casella per ricevere uno sconto del 5%** opzione. L&#39;opzione successiva per applicare la carta di credito è disabilitata.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Deseleziona **Seleziona la casella per ricevere uno sconto del 5%** per abilitare l&#39;opzione della carta di credito.

   ![](/help/forms/assets/screenshot2028126329.png)

Apportiamo modifiche al modulo sul server come utente aziendale e visualizziamo automaticamente le modifiche riflesse nel modulo headless.

1. Apri l’interfaccia di gestione di AEM Forms nel browser. Ad esempio: [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Seleziona la **registrazione** modulo e clic **Modifica.** Apre il modulo nell’editor di moduli adattivi.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Seleziona la **Numero di telefono** e fare clic sul pulsante **Icona Modifica (icona a forma di matita)** nella barra degli strumenti. Se non è possibile visualizzare la barra degli strumenti popup, passare alla modalità Modifica facendo clic su **Modifica** pulsante in alto a destra, da sinistra a **Anteprima** pulsante.

   ![](/help/forms/assets/screenshot2028119629.png)

1. Cambia l’etichetta in Mobile Number (Numero cellulare). Fare clic su uno spazio vuoto nel modulo per salvare le modifiche apportate al modulo.

   ![](/help/forms/assets/screenshot2028119729.png)

Pubblichiamo il modulo aggiornato per propagare le modifiche all’ambiente di pubblicazione.

1. Nella scheda dell’interfaccia di gestione di AEM Forms, seleziona il modulo di registrazione e fai clic su **Annulla pubblicazione**. Se non vede il **Annulla pubblicazione** , andare al passaggio 3 per pubblicare direttamente le modifiche.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Clic **Annulla pubblicazione**. Clic **Chiudi** nella rispettiva finestra di dialogo.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. Dopo aver aggiornato il browser, seleziona il modulo di registrazione e fai clic su **Pubblica**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Fai clic su **Pubblica**. Clic **Chiudi** nella rispettiva finestra di dialogo.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Aggiorna la scheda del browser con il modulo headless visualizzato. Nota: l&#39;etichetta del numero di telefono è stata modificata in Numero cellulare.

   ![](/help/forms/assets/screenshot2028120529.png)

1. Aprire la finestra del prompt dei comandi utilizzata per avviare **react-starter-kit-aem-headless-forms** progetto, premere **CTRL+C**, quindi immetti **Y** e premere Invio per terminare il processo npm. È importante arrestare il server npm in modo che non sia in conflitto con il successivo set di esercizi.

1. Chiudere le finestre Codice di Visual Studio e Prompt dei comandi.


## Lezione 5

### Obiettivo

Eseguire il rendering del modulo come modulo headless tramite l’interfaccia utente Materiale di Google

### Contesto della lezione

In questa lezione, in qualità di sviluppatore front-end, imparerai a eseguire il rendering del modulo adattivo creato in precedenza come modulo headless tramite l’interfaccia utente Materiale di Google.

### Esercizio

Configurare l’archivio locale utilizzando il progetto iniziale dell’interfaccia utente materiale:

1. Aprire il prompt dei comandi utilizzando i diritti di amministratore.

   ![](/help/forms/assets/screenshot2028115829.png)


1. Al prompt dei comandi utilizzare il comando seguente per passare a **c:\git** cartella:

   ```Shell
   cd c:\git
   ```

1. Eseguire i seguenti comandi nell&#39;ordine elencato per creare una cartella denominata mui e passare alla cartella mui utilizzando i seguenti comandi:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Utilizza il seguente comando per clonare il progetto iniziale di react del modulo adattivo:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Utilizza il seguente comando nell’ordine elencato per passare al **react-starter-kit-aem-headless-forms** e aprire il codice in Visual Studio Code:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Per eseguire il rendering del modulo ospitato nell’ambiente di pubblicazione del servizio cloud:

1. Rinomina il **env_template** file in **env** file. Per rinominare, fare clic con il pulsante destro del mouse sulla **env_template** file e seleziona **Rinomina**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Imposta i seguenti valori per le variabili nel file .env. Dopo aver aggiornato le variabili, salva il file. Utilizza il **CTRL+S** cambia combinazione per salvare il file.

   * **URL_AEM**: specifica l’URL dell’ambiente di pubblicazione del servizio cloud. Ad esempio: [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **PERCORSO_MODULO_AEM**: specifica il percorso del modulo adattivo creato nella lezione precedente. Ad esempio, /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. Aprire la finestra di comando, verificare di essere **react-starter-kit-aem-headless-forms** ed eseguire il comando seguente:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. Nella finestra Prompt dei comandi eseguire il comando seguente:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   Il comando avvia un server di sviluppo locale ed esegue il rendering della definizione del modulo recuperata dall’AEM in modo headless utilizzando la libreria front-end dell’interfaccia utente dei materiali di Google.

   >[!NOTE]
   >
   >Se visualizzi una schermata vuota nel browser dopo l’esecuzione di `npm start` comando, cambia `localhost` nell’URL del browser a 127.0.0.1 e hit **Invio**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Per valutare l&#39;esecuzione della stessa logica di business in questa copia trasformata del modulo:

   Seleziona **Seleziona la casella per ricevere uno sconto del 5%**. L’opzione successiva **Desideri richiedere il modulo per la carta di credito aziendale We.Finance?** viene disabilitato.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lezione 6

### Obiettivo

Creare un aspetto alternativo del modulo headless utilizzando le varianti dei componenti dell’interfaccia utente Materiale

### Contesto della lezione

In questa lezione, in qualità di sviluppatore front-end, imparerai a creare una rappresentazione alternativa di diversi componenti utilizzando l’interfaccia utente Materiale per il modulo adattivo creato in precedenza dall’utente aziendale.

### Esercizio

Aggiorna la variante dei componenti nel progetto headless. Per modificare la variante del componente di input del testo dell&#39;interfaccia utente del materiale in `OutlinedInput`:

1. In Visual Code, passa al componente di input del testo aprendo `index.tsx` file in `src/components/textinput/index.tsx`.

1. Aggiungi `//` all&#39;inizio della riga di codice 103. Converte la riga in un commento.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Aggiungi quanto segue alla riga 104 per utilizzare una variante diversa del componente e salva il file. Utilizza il **CTRL+S** cambia combinazione per salvare il file.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   È essenziale utilizzare l’iniziale maiuscola corretta per la variante &quot;OutliningInput&quot;, altrimenti la compilazione non riuscirà. La compilazione dell&#39;ambiente di sviluppo locale viene avviata automaticamente al prompt dei comandi. Attendi di visualizzare il seguente messaggio

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Aggiorna il browser, se non si aggiorna automaticamente, per vedere che il componente di input del testo utilizza una variante diversa.

   ![](/help/forms/assets/screenshot2028127729.png)


   Questa modifica si verifica per gli utenti finali senza alcuna modifica alla definizione del modulo in AEM Forms Server ed è specifica per il canale headless in esame. Ad esempio, canale web in questo laboratorio.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Chiudere Visual Studio Code e le finestre del prompt dei comandi.

## Domande frequenti

+++ La procedura guidata per moduli adattivi è disponibile pubblicamente?

Sì, è disponibile con AEM Forms come Cloud Service.

+++


+++ I componenti core sono disponibili al pubblico?

Sì, i componenti core Adaptive Forms sono disponibili con AEM Forms come Cloud Service.

+++

+++ I moduli headless sono disponibili pubblicamente?

Sì, i moduli headless sono disponibili con AEM Forms come Cloud Service.

+++

+++ I moduli headless richiedono una licenza separata?

No, i moduli headless utilizzano la stessa metrica del valore della licenza, numero di invii di moduli.

+++

+++ I componenti core e i moduli headless sono disponibili con Forms AEM 6.5?

Sì, sia i componenti core per moduli adattivi che i moduli headless sono disponibili con AEM Forms 6.5 Service Pack 16 e versioni successive.

+++


## Passaggi successivi

Ora che hai imparato a creare moduli adattivi e a distribuirli a più canali utilizzando moduli headless, dovresti provare a mettere in atto le nuove competenze. Divertitevi e andate avanti creando e distribuendo esperienze di acquisizione dati eccezionali agli utenti finali, dove si trovano, su larga scala!

## Riferimenti

* [Introduzione ai componenti core per moduli adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [Creare un modulo adattivo utilizzando i componenti core](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [Aggiornare lo stile per AF basato su componenti core](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Moduli adattivi headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [Utilizzo del kit di avvio Headless React](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


