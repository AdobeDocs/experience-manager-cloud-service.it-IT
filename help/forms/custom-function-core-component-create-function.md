---
title: Creare e aggiungere funzioni personalizzate in un modulo adattivo
description: AEM Forms supporta funzioni personalizzate che consentono agli utenti di creare e utilizzare le proprie funzioni all’interno dell’editor di regole.
keywords: Aggiungi una funzione personalizzata, utilizza una funzione personalizzata, crea una funzione personalizzata, utilizza la funzione personalizzata nell’editor di regole.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: e7ab4233-2e91-45c6-9377-0c9204d03ee9
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 2%

---

# Creare una funzione personalizzata per un modulo adattivo basato su componenti core

I Forms adattivi basati sui componenti core offrono esperienze utente dinamiche regolando il contenuto e il comportamento in base all’input dell’utente. Le funzioni personalizzate consentono agli sviluppatori di estendere le funzionalità, garantendo che i moduli soddisfino requisiti specifici. Integrando funzioni personalizzate, gli sviluppatori possono implementare logiche complesse, automatizzare i processi e introdurre interazioni univoche in linea con requisiti aziendali specifici o aspettative degli utenti. Essa garantisce che i moduli non solo si adattino a condizioni diverse, ma forniscano anche una soluzione più precisa ed efficace per casi d’uso diversi.
Questo articolo illustra i passaggi necessari per creare funzioni personalizzate per Adaptive Forms utilizzando i componenti core.

## Considerazioni

* `parameter type` e `return type` non supportano `None`.

* Le funzioni non supportate nell&#39;elenco delle funzioni personalizzate sono:
   * Funzioni del generatore
   * Funzioni Async/Await
   * Definizioni dei metodi
   * Metodi di classe
   * Parametri predefiniti
   * Parametri rimanenti

* Le funzioni ECMAScript più recenti sono disponibili come accesso anticipato (EA), mentre fino a ECMAScript 2019 è supportato nella disponibilità generale.

## Prerequisiti per creare una funzione personalizzata

Prima di iniziare ad aggiungere una funzione personalizzata al Forms adattivo, verifica di disporre dei seguenti elementi:

**Software:**

* **Editor di testo normale (IDE)**: mentre qualsiasi editor di testo normale può funzionare, un ambiente di sviluppo integrato (IDE) come Microsoft Visual Studio Code offre funzionalità avanzate per semplificare la modifica.

* **Git:** Questo sistema di controllo della versione è necessario per la gestione delle modifiche al codice. Se non lo hai installato, scaricalo da https://git-scm.com.


## Creare una funzione personalizzata

Crea una libreria client per chiamare funzioni personalizzate nell’editor di regole. Per ulteriori informazioni, vedere [Utilizzo di librerie lato client](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=it#developing).

I passaggi per creare funzioni personalizzate sono i seguenti:

1. [Creare una libreria client](#create-client-library)
1. [Aggiungere una libreria client a un modulo adattivo](#use-custom-function)

### Creare una libreria client {#create-client-library}

Puoi aggiungere funzioni personalizzate aggiungendo una libreria client. Per creare una libreria client, effettua le seguenti operazioni:

**Clona l&#39;archivio**

Clona il tuo [archivio as a Cloud Service di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=it#accessing-git):

1. Apri la riga di comando o la finestra del terminale.

1. Passa alla posizione desiderata sul computer in cui desideri memorizzare l’archivio.

1. Esegui il comando seguente per clonare l’archivio:

   `git clone [Git Repository URL]`

Con questo comando viene scaricato l&#39;archivio e viene creata una cartella locale dell&#39;archivio clonato nel computer. In questa guida questa cartella viene indicata come [directory del progetto AEMaaCS].

**Aggiungi una cartella della libreria client**

Per aggiungere una nuova cartella della libreria client alla directory di progetto [AEMaaCS], eseguire la procedura seguente:

1. Apri la [directory del progetto AEMaaCS] in un editor.

   ![struttura cartella funzioni personalizzata](/help/forms/assets/custom-library-folder-structure.png)

1. Individuare `ui.apps`.
1. Aggiungi nuova cartella. Aggiungere ad esempio una cartella denominata `experience-league`.
1. Passare alla cartella `/experience-league/` e aggiungere `ClientLibraryFolder`. Creare ad esempio una cartella della libreria client denominata `customclientlibs`.

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**Aggiungi file e cartelle alla cartella Libreria client**

Aggiungi quanto segue alla cartella della libreria client aggiunta:

* file .content.xml
* file js.txt
* cartella js

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. In `.content.xml` aggiungi le seguenti righe di codice:

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > È possibile scegliere qualsiasi nome per la proprietà `client library folder` e `categories`.

1. In `js.txt` aggiungi le seguenti righe di codice:

   ```javascript
         #base=js
       function.js
   ```

1. Nella cartella `js`, aggiungi il file javascript come `function.js` che include le funzioni personalizzate:

   ```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */
   
    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();
   
    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();
   
    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }
   
    return age;
    }
   ```

1. Salva i file.

![struttura cartella funzioni personalizzata](/help/forms/assets/custom-function-added-files.png)

**Includi la nuova cartella nel file filter.xml**:

1. Passa al file `/ui.apps/src/main/content/META-INF/vault/filter.xml` nella directory del progetto [AEMaaCS].

2. Apri il file e aggiungi la seguente riga alla fine:

   `<filter root="/apps/experience-league" />`
3. Salva il file.

![filtro funzione personalizzato xml](/help/forms/assets/custom-function-filterxml.png)

**Distribuisci la cartella della libreria client appena creata nell&#39;ambiente AEM**

Distribuisci la directory del progetto AEM as a Cloud Service [AEMaaCS] nell&#39;ambiente Cloud Service. Per eseguire l’implementazione nell’ambiente Cloud Service:

1. Eseguire il commit delle modifiche

   1. Aggiungi, esegui il commit e invia le modifiche nell’archivio utilizzando i seguenti comandi:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. Distribuisci il codice aggiornato:

   1. Attiva una distribuzione del codice tramite la pipeline full stack esistente. In questo modo viene automaticamente generato e distribuito il codice aggiornato.

Se non hai già configurato una pipeline, consulta la guida su [come impostare una pipeline per AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=it#setup-pipeline).

Una volta eseguita correttamente la pipeline, la funzione personalizzata aggiunta nella libreria client diventa disponibile nell&#39;[editor di regole per moduli adattivi](/help/forms/rule-editor-core-components.md).

### Aggiungere una libreria client a un modulo adattivo{#use-custom-function}

Dopo aver implementato la libreria client nell’ambiente Forms CS, utilizzane le funzionalità nel modulo adattivo. Per aggiungere la libreria client al modulo adattivo

1. Apri il modulo in modalità di modifica. Per aprire un modulo in modalità di modifica, selezionare un modulo e selezionare **[!UICONTROL Modifica]**.
1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri la scheda **[!UICONTROL Base]** e seleziona il nome della **[!UICONTROL categoria di librerie client]** dall&#39;elenco a discesa (in questo caso, seleziona `customfunctionscategory`).

   ![Aggiunta della libreria client della funzione personalizzata](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > È possibile aggiungere più categorie specificando un elenco separato da virgole nel campo **[!UICONTROL Categoria libreria client]**.

1. Fai clic su **[!UICONTROL Fine]**.

Puoi utilizzare la funzione personalizzata nell&#39;editor di regole [ di un modulo adattivo](/help/forms/rule-editor-core-components.md) utilizzando le [annotazioni di JavaScript](##js-annotations).

## Utilizzo di una funzione personalizzata in un modulo adattivo

In un modulo adattivo, puoi utilizzare [funzioni personalizzate all&#39;interno dell&#39;editor di regole](/help/forms/rule-editor-core-components.md). Aggiungiamo il codice seguente al file JavaScript (`Function.js` file) per calcolare l&#39;età in base alla data di nascita (AAAA-MM-GG). Creare una funzione personalizzata come `calculateAge()` che utilizza come input la data di nascita e restituisce l&#39;età:

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

Nell&#39;esempio precedente, quando l&#39;utente immette la data di nascita nel formato (AAAA-MM-GG), la funzione personalizzata `calculateAge` viene richiamata e restituisce l&#39;età.

![Calcola la funzione personalizzata Agae nell&#39;editor di regole](/help/forms/assets/custom-function-calculate-age.png)

Visualizziamo in anteprima il modulo per osservare come le funzioni personalizzate vengono implementate tramite l’editor di regole:

![Funzione personalizzata Calcola età nell&#39;anteprima modulo editor regole](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> È possibile fare riferimento alla seguente cartella [funzione personalizzata](/help/forms/assets//customfunctions.zip). Scarica e installa questa cartella nella tua istanza di AEM utilizzando [Gestione pacchetti](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).

## Funzioni delle funzioni personalizzate

Le funzioni personalizzate in AEM Forms offrono una soluzione solida per estendere e personalizzare le funzionalità dei moduli. Puoi utilizzare le funzioni personalizzate per soddisfare le esigenze specifiche della tua organizzazione.

Queste funzioni supportano varie funzionalità, tra cui l’utilizzo di campi specifici, l’utilizzo di campi globali, le operazioni asincrone e l’incorporazione di meccanismi di caching. Questa flessibilità assicura che i moduli possano adattarsi a requisiti complessi e fornire un’esperienza utente efficiente e personalizzata. Sfruttando queste funzioni avanzate, puoi migliorare le interazioni dei moduli e ottimizzare le prestazioni, rendendo i moduli AEM più funzionali e reattivi.

Approfondiamo le funzioni personalizzate.

### Supporto asincrono nelle funzioni personalizzate {#support-of-async-functions}

Puoi implementare funzioni asincrone nell’editor di regole utilizzando funzioni personalizzate. Per istruzioni su come eseguire questa operazione, consulta l&#39;articolo [Utilizzo di funzioni asincrone in un modulo adattivo](/help/forms/using-async-funct-in-rule-editor.md).

### Supporto di oggetti di ambito Field e Global nelle funzioni personalizzate {#support-field-and-global-objects}

Gli oggetti Field fanno riferimento ai singoli componenti o elementi di un modulo, ad esempio campi di testo e caselle di controllo. L&#39;oggetto Globals contiene variabili di sola lettura quali l&#39;istanza del modulo, l&#39;istanza del campo di destinazione e i metodi per apportare modifiche al modulo nelle funzioni personalizzate.

>[!NOTE]
>
> `param {scope} globals` deve essere l&#39;ultimo parametro e non viene visualizzato nell&#39;editor di regole di un modulo adattivo.

Per ulteriori informazioni sugli oggetti ambito, vedere l&#39;articolo [Oggetti ambito nelle funzioni personalizzate](/help/forms/custom-function-core-component-scope-function.md).

### Supporto della memorizzazione in cache nella funzione personalizzata

Forms adattivo implementa il caching per le funzioni personalizzate per migliorare il tempo di risposta durante il recupero dell’elenco delle funzioni personalizzate nell’editor di regole. Nel file `Fetched following custom functions list from cache` viene visualizzato il messaggio `error.log`.

![funzione personalizzata con supporto cache](/help/forms/assets/custom-function-cache-error.png)

Se le funzioni personalizzate vengono modificate, la memorizzazione in cache viene invalidata e analizzata.

## Risoluzione di problemi

* Se il file JavaScript contenente il codice per le funzioni personalizzate presenta un errore, le funzioni personalizzate non sono elencate nell’editor delle regole di un modulo adattivo. Per verificare l&#39;elenco delle funzioni personalizzate, è possibile individuare l&#39;errore nel file `error.log`. In caso di errore, l’elenco delle funzioni personalizzate appare vuoto:

  ![file di log degli errori](/help/forms/assets/custom-function-list-error-file.png)

  In caso di errore, la funzione personalizzata viene recuperata e visualizzata nel file `error.log`. Nel file `Fetched following custom functions list` viene visualizzato il messaggio `error.log`:

  ![file di registro errori con funzione personalizzata appropriata](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Passaggio successivo

Vediamo ora vari [esempi di funzioni personalizzate per un modulo adattivo basato su componenti core](/help/forms/custom-function-core-components-use-cases.md).

## Consulta anche

{{see-also-rule-editor}}
