---
title: Creare e aggiungere funzioni personalizzate in un modulo adattivo
description: AEM Forms supporta funzioni personalizzate che consentono agli utenti di creare e utilizzare le proprie funzioni all’interno dell’editor di regole.
keywords: Aggiungi una funzione personalizzata, utilizza una funzione personalizzata, crea una funzione personalizzata, utilizza la funzione personalizzata nell’editor di regole.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '4333'
ht-degree: 0%

---


# Funzioni personalizzate in Forms adattivo (componenti core)

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | Questo articolo |

## Introduzione

AEM Forms supporta funzioni personalizzate che consentono agli utenti di definire funzioni JavaScript per l’implementazione di regole aziendali complesse. Queste funzioni personalizzate estendono le funzionalità dei moduli facilitando la manipolazione e l’elaborazione dei dati immessi per soddisfare requisiti specifici. Consentono inoltre di modificare dinamicamente il comportamento delle forme in base a criteri predefiniti.

>[!NOTE]
>
> Verificare che il [componente core](https://github.com/adobe/aem-core-forms-components) sia impostato sulla versione più recente per utilizzare le funzionalità più recenti.

### Utilizzo di funzioni personalizzate {#uses-of-custom-function}

L’utilizzo di funzioni personalizzate in Adaptive Forms offre i seguenti vantaggi:
* **Elaborazione dei dati**: le funzioni personalizzate consentono di elaborare i dati immessi nei campi dei moduli.
* **Convalida dei dati**: le funzioni personalizzate consentono di eseguire controlli personalizzati sugli input dei moduli e di fornire messaggi di errore specifici.
* **Comportamento dinamico**: le funzioni personalizzate consentono di controllare il comportamento dinamico dei moduli in base a condizioni specifiche. Ad esempio, è possibile visualizzare/nascondere campi, modificare i valori dei campi o modificare dinamicamente la logica del modulo.
* **Integrazione**: è possibile utilizzare funzioni personalizzate da integrare con API o servizi esterni. Consente di recuperare dati da origini esterne, inviare dati agli endpoint Rest esterni o eseguire azioni personalizzate basate su eventi esterni.

Le funzioni personalizzate sono essenzialmente librerie client aggiunte al file JavaScript. Una volta creata, una funzione personalizzata diventa disponibile nell’editor di regole per la selezione da parte dell’utente in un modulo adattivo. Le funzioni personalizzate sono identificate dalle annotazioni di JavaScript nell’editor di regole.

### Annotazioni di JavaScript supportate per la funzione personalizzata {#js-annotations}

Le annotazioni JavaScript vengono utilizzate per fornire metadati per il codice JavaScript. Include commenti che iniziano con simboli specifici, ad esempio /** e @. Le annotazioni forniscono informazioni importanti su funzioni, variabili e altri elementi nel codice. Il modulo adattivo supporta le seguenti annotazioni di JavaScript per le funzioni personalizzate:

#### Nome

Il nome viene utilizzato per identificare la funzione personalizzata nell’editor di regole di un modulo adattivo. Per denominare una funzione personalizzata vengono utilizzate le sintassi seguenti:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` è il nome della funzione. Gli spazi non sono consentiti.
  `<Function Name>` è il nome visualizzato della funzione nell&#39;editor di regole di un modulo adattivo.
Se il nome della funzione è identico al nome della funzione stessa, è possibile omettere `[functionName]` dalla sintassi.

#### Parametro

Il parametro è un elenco di argomenti utilizzati dalle funzioni personalizzate. Una funzione può supportare più parametri. Le seguenti sintassi vengono utilizzate per definire un parametro in una funzione personalizzata:

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`.
  `{type}` rappresenta il tipo di parametro.  I tipi di parametri consentiti sono:

   * string (stringa): rappresenta un singolo valore di stringa.
   * number: rappresenta un singolo valore numerico.
   * booleano: rappresenta un singolo valore booleano (true o false).
   * stringa[]: rappresenta una matrice di valori stringa.
   * number[]: rappresenta una matrice di valori numerici.
   * booleano[]: rappresenta una matrice di valori booleani.
   * data: rappresenta un singolo valore di data.
   * data[]: rappresenta una matrice di valori di data.
   * array: rappresenta una matrice generica contenente valori di vari tipi.
   * object: rappresenta un oggetto modulo passato a una funzione personalizzata anziché passare direttamente il relativo valore.
   * ambito: rappresenta l&#39;oggetto globals, che contiene variabili di sola lettura quali istanze di moduli, istanze di campi di destinazione e metodi per l&#39;esecuzione di modifiche di moduli all&#39;interno di funzioni personalizzate. Viene dichiarato come ultimo parametro nelle annotazioni di JavaScript e non è visibile nell’editor di regole di un modulo adattivo. Il parametro scope accede all&#39;oggetto del modulo o del componente per attivare la regola o l&#39;evento necessario per l&#39;elaborazione del modulo. Per ulteriori informazioni sull&#39;oggetto Globals e su come utilizzarlo, [fare clic qui](/help/forms/create-and-use-custom-functions.md#support-field-and-global-objects).

Il tipo di parametro non fa distinzione tra maiuscole e minuscole e non sono consentiti spazi nel nome del parametro.

`<Parameter Description>` contiene dettagli sullo scopo del parametro. Può avere più parole.

**Parametri facoltativi**
Per impostazione predefinita, tutti i parametri sono obbligatori. È possibile definire un parametro come facoltativo aggiungendo `=` dopo il tipo di parametro o racchiudendo il nome del parametro in `[]`. I parametri definiti come facoltativi nelle annotazioni di JavaScript vengono visualizzati come facoltativi nell’editor di regole.
Per definire una variabile come parametro facoltativo, è possibile utilizzare una delle sintassi seguenti:

* `@param {type=} Input1`

Nella riga di codice precedente, `Input1` è un parametro facoltativo senza alcun valore predefinito. Per dichiarare un parametro facoltativo con valore predefinito:
`@param {string=<value>} input1`

`input1` come parametro facoltativo con il valore predefinito impostato su `value`.

* `@param {type} [Input1]`

Nella riga di codice precedente, `Input1` è un parametro facoltativo senza alcun valore predefinito. Per dichiarare un parametro facoltativo con valore predefinito:
`@param {array} [input1=<value>]`
`input1` è un parametro facoltativo di tipo array con il valore predefinito impostato su `value`.
Assicurarsi che il tipo di parametro sia racchiuso tra parentesi graffe {} e che il nome del parametro sia racchiuso tra parentesi quadre.

Considera il seguente frammento di codice, in cui input2 è definito come parametro opzionale:

```javascript
        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

Nell&#39;illustrazione seguente viene visualizzato l&#39;utilizzo della funzione personalizzata `OptionalParameterFunction` nell&#39;editor di regole:

![Parametri facoltativi o obbligatori ](/help/forms/assets/optional-default-params.png)

Puoi salvare la regola senza specificare un valore per i parametri richiesti, ma la regola non viene eseguita e visualizza un messaggio di avviso come:

![avviso regola incompleto](/help/forms/assets/incomplete-rule.png)

Quando l’utente lascia vuoto il parametro opzionale, il valore &quot;Undefined&quot; (Non definito) viene passato alla funzione personalizzata per il parametro opzionale.

Per ulteriori informazioni su come definire parametri facoltativi in JSDocs, [fai clic qui](https://jsdoc.app/tags-param).

#### Tipo restituito

Il tipo restituito specifica il tipo di valore restituito dalla funzione personalizzata dopo l&#39;esecuzione. Le seguenti sintassi vengono utilizzate per definire un tipo restituito in una funzione personalizzata:

* `@return {type}`
* `@returns {type}`
  `{type}` rappresenta il tipo restituito della funzione. I tipi restituiti consentiti sono:
   * string (stringa): rappresenta un singolo valore di stringa.
   * number: rappresenta un singolo valore numerico.
   * booleano: rappresenta un singolo valore booleano (true o false).
   * stringa[]: rappresenta una matrice di valori stringa.
   * number[]: rappresenta una matrice di valori numerici.
   * booleano[]: rappresenta una matrice di valori booleani.
   * data: rappresenta un singolo valore di data.
   * data[]: rappresenta una matrice di valori di data.
   * array: rappresenta una matrice generica contenente valori di vari tipi.
   * object: rappresenta direttamente l&#39;oggetto modulo anziché il relativo valore.

  Il tipo restituito non fa distinzione tra maiuscole e minuscole.

#### Privata

La funzione personalizzata dichiarata come privata non viene visualizzata nell’elenco delle funzioni personalizzate nell’editor delle regole di un modulo adattivo. Per impostazione predefinita, le funzioni personalizzate sono pubbliche. La sintassi per dichiarare la funzione personalizzata come privata è `@private`.


## Linee guida per la creazione di funzioni personalizzate

Per elencare le funzioni personalizzate nell’editor di regole, puoi utilizzare uno dei seguenti formati:

### Istruzione function con o senza commenti jsdoc

Puoi creare una funzione personalizzata con o senza commenti jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
Se l’utente non aggiunge annotazioni JavaScript alla funzione personalizzata, questa viene elencata nell’editor di regole in base al nome della funzione. Tuttavia, si consiglia di includere annotazioni JavaScript per migliorare la leggibilità delle funzioni personalizzate.

### Funzione freccia con annotazioni o commenti JavaScript obbligatori

È possibile creare una funzione personalizzata con una sintassi della funzione freccia:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

Se l’utente non aggiunge annotazioni JavaScript alla funzione personalizzata, la funzione personalizzata non viene elencata nell’editor di regole di un modulo adattivo.

### Espressione di funzione con annotazioni o commenti JavaScript obbligatori

Per elencare le funzioni personalizzate nell’editor di regole di un modulo adattivo, crea funzioni personalizzate nel formato seguente:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

Se l’utente non aggiunge annotazioni JavaScript alla funzione personalizzata, la funzione personalizzata non viene elencata nell’editor di regole di un modulo adattivo.

## Creare una funzione personalizzata {#create-custom-function}

Crea una libreria client per chiamare funzioni personalizzate nell’editor di regole. Per ulteriori informazioni, vedere [Utilizzo di librerie lato client](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

I passaggi per creare funzioni personalizzate sono i seguenti:
1. [Creare una libreria client](#create-client-library)
1. [Aggiungere una libreria client a un modulo adattivo](#use-custom-function)


### Prerequisiti per creare una funzione personalizzata

Prima di iniziare ad aggiungere una funzione personalizzata al Forms adattivo, verifica di disporre dei seguenti elementi:

**Software:**

* **Editor di testo normale (IDE)**: mentre qualsiasi editor di testo normale può funzionare, un ambiente di sviluppo integrato (IDE) come Microsoft Visual Studio Code offre funzionalità avanzate per semplificare la modifica.

* **Git:** Questo sistema di controllo della versione è necessario per la gestione delle modifiche al codice. Se non lo hai installato, scaricalo da https://git-scm.com.

### Creare una libreria client {#create-client-library}

Puoi aggiungere funzioni personalizzate aggiungendo una libreria client. Per creare una libreria client, effettua le seguenti operazioni:

**Clona l&#39;archivio**

Clona il tuo [archivio as a Cloud Service di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git):

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

1. Apri il file e aggiungi la seguente riga alla fine:

   `<filter root="/apps/experience-league" />`
1. Salva il file.

![filtro funzione personalizzato xml](/help/forms/assets/custom-function-filterxml.png)

**Distribuisci la cartella della libreria client appena creata nell&#39;ambiente AEM**

Distribuisci la directory del progetto AEM as a Cloud Service [AEMaaCS] nell&#39;ambiente di Cloud Service. Per eseguire l’implementazione nell’ambiente di Cloud Service:

1. Eseguire il commit delle modifiche

   1. Aggiungi, esegui il commit e invia le modifiche nell’archivio utilizzando i seguenti comandi:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. Distribuisci il codice aggiornato:

   1. Attiva una distribuzione del codice tramite la pipeline full stack esistente. In questo modo viene automaticamente generato e distribuito il codice aggiornato.

Se non hai già configurato una pipeline, consulta la guida su [come impostare una pipeline per AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline).

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
> È possibile fare riferimento alla seguente cartella [funzione personalizzata](/help/forms/assets//customfunctions.zip). Scarica e installa questa cartella nella tua istanza AEM utilizzando [Gestione pacchetti](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).


### Impostare le opzioni dell’elenco a discesa utilizzando le funzioni personalizzate

L&#39;editor di regole nei Componenti core non supporta la proprietà **Imposta opzioni di** per impostare le opzioni dell&#39;elenco a discesa in fase di esecuzione. Tuttavia, è possibile impostare le opzioni dell’elenco a discesa utilizzando le funzioni personalizzate.

Osserva il codice seguente per scoprire come impostare le opzioni dell’elenco a discesa utilizzando le funzioni personalizzate:

```javascript
    /**
    * @name setEnums
    * @returns {string[]}
    **/
    function setEnums() {
    return ["0","1","2","3","4","5","6"];   
    }

    /**
    * @name setEnumNames
    * @returns {string[]}
    **/
    function setEnumNames() {
    return ["Sunday","Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
    }
```

Nel codice riportato sopra, `setEnums` viene utilizzato per impostare la proprietà `enum` e `setEnumNames` per impostare la proprietà `enumNames` dell&#39;elenco a discesa.

Creiamo una regola per il pulsante `Next`, che imposta il valore dell&#39;opzione dell&#39;elenco a discesa quando l&#39;utente fa clic sul pulsante `Next`:

![Opzioni elenco a discesa](/help/forms/assets/drop-down-list-options.png)

Fai riferimento all’illustrazione seguente per dimostrare dove sono impostate le opzioni dell’elenco a discesa facendo clic sul pulsante Visualizza:

![Opzioni elenco a discesa nell&#39;Editor regole](/help/forms/assets/drop-down-option-rule-editor.png)



### Supporto delle funzioni asincrone nelle funzioni personalizzate {#support-of-async-functions}

Le funzioni personalizzate asincrone non vengono visualizzate nell’elenco dell’editor di regole. Tuttavia, è possibile richiamare funzioni asincrone all’interno di funzioni personalizzate create utilizzando espressioni di funzioni sincrone.

![Sincronizza e sincronizza funzione personalizzata](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> Il vantaggio di chiamare funzioni asincrone nelle funzioni personalizzate è che le funzioni asincrone consentono l’esecuzione simultanea di più attività, con il risultato di ogni funzione utilizzata all’interno delle funzioni personalizzate.

Osserva il codice seguente per scoprire come richiamare funzioni asincrone utilizzando funzioni personalizzate:

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

Nell&#39;esempio precedente, la funzione asyncFunction è un `asynchronous function`. Esegue un&#39;operazione asincrona effettuando una richiesta `GET` a `https://petstore.swagger.io/v2/store/inventory`. Attende la risposta utilizzando `await`, analizza il corpo della risposta come JSON utilizzando `response.json()`, quindi restituisce i dati. La funzione `callAsyncFunction` è una funzione personalizzata sincrona che richiama la funzione `asyncFunction` e visualizza i dati di risposta nella console. Sebbene la funzione `callAsyncFunction` sia sincrona, chiama la funzione asyncFunction asincrona e gestisce il risultato con `then` e `catch` istruzioni.

Per vedere come funziona, aggiungiamo un pulsante e creiamo una regola per il pulsante che richiama la funzione asincrona al clic di un pulsante.

![creazione regola per funzione asincrona](/help/forms/assets/rule-for-async-funct.png)

Fare riferimento all&#39;illustrazione della finestra della console seguente per dimostrare che quando l&#39;utente fa clic sul pulsante `Fetch`, viene richiamata la funzione personalizzata `callAsyncFunction`, che a sua volta chiama una funzione asincrona `asyncFunction`. Inspect nella finestra della console per visualizzare la risposta al pulsante, fai clic su:

![Finestra della console](/help/forms/assets/async-custom-funct-console.png)

Approfondiamo le funzioni personalizzate.

## Varie funzioni per funzioni personalizzate

È possibile utilizzare funzioni personalizzate per aggiungere caratteristiche personalizzate ai moduli. Queste funzioni supportano varie funzionalità, ad esempio l’utilizzo di campi specifici, l’utilizzo di campi globali o la memorizzazione in cache. Questa flessibilità consente di personalizzare i moduli in base ai requisiti aziendali.

### Oggetti di ambito Field e Global nelle funzioni personalizzate {#support-field-and-global-objects}

Gli oggetti Field fanno riferimento ai singoli componenti o elementi di un modulo, ad esempio campi di testo e caselle di controllo. L&#39;oggetto Globals contiene variabili di sola lettura quali l&#39;istanza del modulo, l&#39;istanza del campo di destinazione e i metodi per apportare modifiche al modulo nelle funzioni personalizzate.

>[!NOTE]
>
> `param {scope} globals` deve essere l&#39;ultimo parametro e non viene visualizzato nell&#39;editor di regole di un modulo adattivo.

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

Scopriamo in che modo le funzioni personalizzate utilizzano oggetti campo e globali con l&#39;aiuto di un modulo `Contact Us` utilizzando casi d&#39;uso diversi.

![Modulo per contattarci](/help/forms/assets/contact-us-form.png)

+++ **Caso d&#39;uso**: mostra un pannello utilizzando la regola `SetProperty`

Aggiungere il codice seguente nella funzione personalizzata come descritto nella sezione [create-custom-function](#create-custom-function) per impostare il campo modulo come `Required`.

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * È possibile configurare le proprietà del campo utilizzando le proprietà disponibili in `[form-path]/jcr:content/guideContainer.model.json`.
> * Le modifiche apportate al modulo utilizzando il metodo `setProperty` dell&#39;oggetto Globals sono di natura asincrona e non vengono applicate durante l&#39;esecuzione della funzione personalizzata.

In questo esempio, la convalida del pannello `personaldetails` viene eseguita facendo clic sul pulsante. Se non vengono rilevati errori nel pannello, un altro pannello, il pannello `feedback`, diventa visibile al clic del pulsante.

Creiamo una regola per il pulsante `Next`, che convalida il pannello `personaldetails` e rende visibile il pannello `feedback` quando l&#39;utente fa clic sul pulsante `Next`.

![Imposta proprietà](/help/forms/assets/custom-function-set-property.png)

Fare riferimento all&#39;illustrazione seguente per dimostrare dove viene convalidato il pannello `personaldetails` facendo clic sul pulsante `Next`. Se tutti i campi all&#39;interno di `personaldetails` sono convalidati, il pannello `feedback` diventa visibile.

![Imposta anteprima modulo proprietà](/help/forms/assets/set-property-form-preview.png)

Se nei campi del pannello `personaldetails` sono presenti errori, questi vengono visualizzati a livello di campo facendo clic sul pulsante `Next` e il pannello `feedback` rimane invisibile.

![Imposta anteprima modulo proprietà](/help/forms/assets/set-property-panel.png)

+++

+++ **Caso d&#39;uso**: convalidare il campo.

Aggiungi il seguente codice nella funzione personalizzata come descritto nella sezione [create-custom-function](#create-custom-function) per convalidare il campo.

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> Se nella funzione `validate()` non viene passato alcun argomento, il modulo viene convalidato.

In questo esempio, al campo `contact` viene applicato un pattern di convalida personalizzato. Gli utenti devono immettere un numero di telefono che inizia con `10` seguito da `8` cifre. Se l&#39;utente immette un numero di telefono che non inizia con `10` o che contiene più o meno di `8` cifre, viene visualizzato un messaggio di errore di convalida al clic del pulsante:

![Modello di convalida indirizzo e-mail](/help/forms/assets/custom-function-validation-pattern.png)

Il passaggio successivo consiste nel creare una regola per il pulsante `Next` che convalida il campo `contact` al clic del pulsante.

![Modello di convalida](/help/forms/assets/custom-function-validate.png)

Fare riferimento all&#39;illustrazione seguente per dimostrare che se l&#39;utente immette un numero di telefono che non inizia con `10`, viene visualizzato un messaggio di errore a livello di campo:

![Modello di convalida indirizzo e-mail](/help/forms/assets/custom-function-validate-error-message.png)

Se l&#39;utente immette un numero di telefono valido e tutti i campi nel pannello `personaldetails` sono convalidati, il pannello `feedback` viene visualizzato sullo schermo:

![Modello di convalida indirizzo e-mail](/help/forms/assets/validate-form-preview-form.png)

+++

+++ **Caso d&#39;uso**: reimpostare un pannello

Aggiungi il seguente codice nella funzione personalizzata, come descritto nella sezione [create-custom-function](#create-custom-function), per ripristinare il pannello.

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> Se nella funzione `reset()` non viene passato alcun argomento, il modulo viene convalidato.

In questo esempio, il pannello `personaldetails` viene ripristinato facendo clic sul pulsante `Clear`. Il passaggio successivo consiste nel creare una regola per il pulsante `Clear` che ripristini il pannello al clic del pulsante.

![Cancella pulsante](/help/forms/assets/custom-function-reset-field.png)

Vedere l&#39;illustrazione seguente per mostrare che se l&#39;utente fa clic sul pulsante `clear`, il pannello `personaldetails` viene ripristinato:

![Reimposta modulo](/help/forms/assets/custom-function-reset-form.png)

+++

+++ **Caso d&#39;uso**: per visualizzare un messaggio personalizzato a livello di campo e contrassegnare il campo come non valido

È possibile utilizzare la funzione `markFieldAsInvalid()` per definire un campo come non valido e impostare un messaggio di errore personalizzato a livello di campo. Il valore `fieldIdentifier` può essere `fieldId`, `field qualifiedName` o `field dataRef`. Il valore dell&#39;oggetto denominato `option` può essere `{useId: true}`, `{useQualifiedName: true}` o `{useDataRef: true}`.
Le sintassi utilizzate per contrassegnare un campo come non valido e impostare un messaggio personalizzato sono:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Aggiungi il seguente codice nella funzione personalizzata, come descritto nella sezione [create-custom-function](#create-custom-function), per abilitare un messaggio personalizzato a livello di campo.

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

In questo esempio, se l&#39;utente immette meno di 15 caratteri nella casella di testo dei commenti, viene visualizzato un messaggio personalizzato a livello di campo.

Il passaggio successivo consiste nel creare una regola per il campo `comments`:

![Contrassegna il campo come non valido](/help/forms/assets/custom-function-invalid-field.png)

Vedere la dimostrazione seguente per visualizzare che l&#39;immissione di un feedback negativo nel campo `comments` attiva la visualizzazione di un messaggio personalizzato a livello di campo:

![Contrassegna il campo come modulo di anteprima non valido](/help/forms/assets/custom-function-invalidfield-form.png)

Se l’utente immette più di 15 caratteri nella casella di testo dei commenti, il campo viene convalidato e il modulo viene inviato:

![Contrassegna il campo come modulo di anteprima valido](/help/forms/assets/custom-function-validfield-form.png)

+++

+++ **Caso d&#39;uso**: invio dei dati modificati al server

La seguente riga di codice:
`globals.functions.submitForm(globals.functions.exportData(), false);` viene utilizzato per inviare i dati del modulo dopo la manipolazione.
* Il primo argomento è costituito dai dati da inviare.
* Il secondo argomento indica se il modulo deve essere convalidato prima dell&#39;invio. È `optional` ed è impostato come `true` per impostazione predefinita.
* Il terzo argomento è `contentType` dell&#39;inoltro, che è anche facoltativo con il valore predefinito `multipart/form-data`. Gli altri valori possono essere `application/json` e `application/x-www-form-urlencoded`.

Aggiungi il seguente codice nella funzione personalizzata, come descritto nella sezione [create-custom-function](#create-custom-function), per inviare i dati manipolati sul server:

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

In questo esempio, se l&#39;utente lascia vuota la casella di testo `comments`, `NA` viene inviato al server al momento dell&#39;invio del modulo.

Creare una regola per il pulsante `Submit` che invia i dati:

![Invia dati](/help/forms/assets/custom-function-submit-data.png)

Fare riferimento all&#39;illustrazione di `console window` seguente per dimostrare che se l&#39;utente lascia vuota la casella di testo `comments`, il valore `NA` viene inviato nel server:

![Invia dati nella finestra della console](/help/forms/assets/custom-function-submit-data-form.png)

È inoltre possibile esaminare la finestra della console per visualizzare i dati inviati al server:

![Dati Inspect nella finestra della console](/help/forms/assets/custom-function-submit-data-console-data.png)

+++

+++ **Caso d&#39;uso**: ignorare i gestori di errori e operazioni riuscite di invio del modulo

Aggiungi la seguente riga di codice come descritto nella sezione [create-custom-function](#create-custom-function) per personalizzare l&#39;invio o il messaggio di errore per l&#39;invio dei moduli e visualizzare i messaggi di invio dei moduli in una casella modale:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

In questo esempio, quando l&#39;utente utilizza le funzioni personalizzate `customSubmitSuccessHandler` e `customSubmitErrorHandler`, i messaggi di esito positivo e negativo vengono visualizzati in un modale. La funzione JavaScript `showModal(type, message)` viene utilizzata per creare e visualizzare in modo dinamico una finestra di dialogo modale su uno schermo.

Ora, crea una regola per l’invio corretto del modulo:

![Invio modulo completato](/help/forms/assets/form-submission-success.png)

Fai riferimento all’illustrazione seguente per dimostrare che, quando il modulo viene inviato correttamente, il messaggio di successo viene visualizzato in una finestra modale:

![Messaggio di invio modulo completato](/help/forms/assets/form-submission-success-message.png)

Allo stesso modo, creiamo una regola per gli invii di moduli non riusciti:

![Invio modulo non riuscito](/help/forms/assets/form-submission-fail.png)

Fai riferimento all’illustrazione seguente per dimostrare che quando l’invio del modulo non riesce, il messaggio di errore viene visualizzato in un modale:

![Messaggio di invio modulo non riuscito](/help/forms/assets/form-submission-fail-message.png)

Per visualizzare l&#39;invio dei moduli completato e non riuscito in modo predefinito, sono disponibili le funzioni `Default submit Form Success Handler` e `Default submit Form Error Handler` pronte all&#39;uso.

Nel caso in cui il gestore di invio personalizzato non riesca a eseguire le operazioni previste nei progetti o moduli AEM esistenti, consulta la sezione [risoluzione dei problemi](#troubleshooting).

+++

+++ **Caso d&#39;uso**: esecuzione di azioni in un&#39;istanza specifica del pannello ripetibile

Le regole create utilizzando l’editor di regole visive in un pannello ripetibile si applicano all’ultima istanza del pannello ripetibile. Per scrivere una regola per una specifica istanza del pannello ripetibile, possiamo utilizzare una funzione personalizzata.

Creiamo un altro modulo per raccogliere informazioni sui viaggiatori che si dirigono verso una destinazione. Un pannello viaggiatore viene aggiunto come pannello ripetibile, in cui l&#39;utente può aggiungere dettagli per 5 viaggiatori utilizzando il pulsante `Add Traveler`.

![Informazioni viaggiatore](/help/forms/assets/traveler-info-form.png)

Aggiungi la seguente riga di codice come descritto nella sezione [create-custom-function](#create-custom-function) per eseguire azioni in un&#39;istanza specifica del pannello ripetibile, diversa dall&#39;ultima:

```javascript
/**
* @name hidePanelInRepeatablePanel
* @param {scope} globals
*/
function hidePanelInRepeatablePanel(globals)
{    
    var repeatablePanel = globals.form.travelerinfo;
    // hides a panel inside second instance of repeatable panel
    globals.functions.setProperty(repeatablePanel[1].traveler, {visible : false});
}  
```

In questo esempio, la funzione personalizzata `hidePanelInRepeatablePanel` esegue un&#39;azione in un&#39;istanza specifica del pannello ripetibile. Nel codice precedente, `travelerinfo` rappresenta il pannello ripetibile. Il codice `repeatablePanel[1].traveler, {visible: false}` nasconde il pannello nella seconda istanza del pannello ripetibile.

Aggiungiamo un pulsante con etichetta `Hide` e una regola per nascondere la seconda istanza di un pannello ripetibile.

![Nascondi regola pannello](/help/forms/assets/custom-function-hidepanel-rule.png)

Fare riferimento al video seguente per dimostrare che quando si fa clic su `Hide`, il pannello nella seconda istanza ripetibile si nasconde:

>[!VIDEO](https://video.tv.adobe.com/v/3429554?quality=12&learn=on)

+++

+++ **Usecase**: precompila il campo con un valore al caricamento del modulo

Aggiungi la seguente riga di codice, come spiegato nella sezione [create-custom-function](#create-custom-function), per caricare il valore precompilato in un campo quando il modulo viene inizializzato:

```javascript
/**
 * Tests import data
 * @name testImportData
 * @param {scope} globals
 */
function testImportData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount','10000']]));
} 
```

Nel codice sopra indicato, la funzione `testImportData` compila il campo della casella di testo `Booking Amount` al caricamento del modulo. Supponiamo che il modulo di prenotazione richieda un importo minimo di prenotazione pari a `10,000`.

Creiamo una regola al momento dell&#39;inizializzazione del modulo, in cui il valore nel campo della casella di testo `Booking Amount` viene precompilato con un valore specificato al caricamento del modulo:

![Importa regola dati](/help/forms/assets/custom-function-import-data.png)

Fai riferimento alla schermata seguente, che dimostra che quando il modulo viene caricato, il valore nella casella di testo `Booking Amount` è precompilato con un valore specificato:

![Importa modulo regola dati](/help/forms/assets/custom-function-prefill-form.png)

+++

+++ **Usecase**: imposta lo stato attivo sul campo specifico

Aggiungere la seguente riga di codice, come spiegato nella sezione [create-custom-function](#create-custom-function), per attivare il campo specificato quando si fa clic sul pulsante `Submit`.:

```javascript
/**
 * @name testSetFocus
 * @param {object} emailField
 * @param {scope} globals
 */
    function testSetFocus(field, globals)
    {
        globals.functions.setFocus(field);
    }
```

Aggiungiamo una regola al pulsante `Submit` per impostare lo stato attivo sul campo della casella di testo `Email ID` quando si fa clic su di esso:

![Imposta regola stato attivo](/help/forms/assets/custom-function-set-focus.png)

Fare riferimento alla schermata seguente, che dimostra che quando si fa clic sul pulsante `Submit`, lo stato attivo è impostato sul campo `Email ID`:

![Imposta regola stato attivo](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> È possibile utilizzare il parametro facoltativo `$focusOption` se si desidera concentrarsi sul campo successivo o precedente relativo al campo `email`.

+++

+++ **Usecase**: aggiungi o elimina un pannello ripetibile utilizzando la proprietà `dispatchEvent`

Aggiungi la seguente riga di codice, come spiegato nella sezione [create-custom-function](#create-custom-function), per aggiungere un pannello quando fai clic sul pulsante `Add Traveler` utilizzando la proprietà `dispatchEvent`:

```javascript
/**
 * Tests add instance with dispatchEvent
 * @name testAddInstance
 * @param {scope} globals
 */
function testAddInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel,'addInstance');
}
```

Aggiungiamo una regola al pulsante `Add Traveler` per aggiungere il pannello ripetibile quando viene fatto clic:

![Aggiungi regola pannello](/help/forms/assets/custom-function-add-panel.png)

Fare riferimento al file GIF riportato di seguito, a dimostrazione che quando si fa clic sul pulsante `Add Traveler`, il pannello viene aggiunto utilizzando la proprietà `dispatchEvent`:

![Aggiungi pannello](/help/forms/assets/custom-function-add-panel.gif)

Analogamente, aggiungere la seguente riga di codice, come spiegato nella sezione [create-custom-function](#create-custom-function), per eliminare un pannello quando si fa clic sul pulsante `Delete Traveler` utilizzando la proprietà `dispatchEvent`:

```javascript
/**
 
 * @name testRemoveInstance
 * @param {scope} globals
 */
function testRemoveInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 
```

Aggiungiamo una regola al pulsante `Delete Traveler` per eliminare il pannello ripetibile quando viene selezionato:

![Elimina regola pannello](/help/forms/assets/custom-function-delete-panel.png)

Fare riferimento al file GIF riportato di seguito, a dimostrazione che quando si fa clic sul pulsante `Delete Traveler`, il pannello del viaggiatore viene eliminato utilizzando la proprietà `dispatchEvent`:

![Elimina pannello](/help/forms/assets/custom-function-delete-panel.gif)

+++

## Supporto della memorizzazione in cache per la funzione personalizzata

Forms adattivo implementa il caching per le funzioni personalizzate per migliorare il tempo di risposta durante il recupero dell’elenco delle funzioni personalizzate nell’editor di regole. Nel file `error.log` viene visualizzato il messaggio `Fetched following custom functions list from cache`.

![funzione personalizzata con supporto cache](/help/forms/assets/custom-function-cache-error.png)

Se le funzioni personalizzate vengono modificate, la memorizzazione in cache viene invalidata e analizzata.

## Risoluzione dei problemi {#troubleshooting}

* Se il gestore di invio personalizzato non funziona come previsto nei progetti o moduli AEM esistenti, effettua le seguenti operazioni:
   * Verificare che la versione dei componenti core [sia aggiornata a 3.0.18 e versioni successive](https://github.com/adobe/aem-core-forms-components). Tuttavia, per i progetti e i moduli AEM esistenti, vi sono ulteriori passi da seguire:

   * Per il progetto AEM, l&#39;utente deve sostituire tutte le istanze di `submitForm('custom:submitSuccess', 'custom:submitError')` con `submitForm()` e distribuire il progetto tramite la pipeline Cloud Manager.

   * Per i moduli esistenti, se i gestori di invio personalizzati non funzionano correttamente, l&#39;utente deve aprire e salvare la regola `submitForm` sul pulsante **Invia** utilizzando l&#39;editor di regole. Questa azione sostituisce la regola esistente di `submitForm('custom:submitSuccess', 'custom:submitError')` con `submitForm()` nel modulo.


* Se il file JavaScript contenente il codice per le funzioni personalizzate presenta un errore, le funzioni personalizzate non sono elencate nell’editor delle regole di un modulo adattivo. Per verificare l&#39;elenco delle funzioni personalizzate, è possibile individuare l&#39;errore nel file `error.log`. In caso di errore, l’elenco delle funzioni personalizzate appare vuoto:

  ![file di log degli errori](/help/forms/assets/custom-function-list-error-file.png)

  In caso di errore, la funzione personalizzata viene recuperata e visualizzata nel file `error.log`. Nel file `error.log` viene visualizzato il messaggio `Fetched following custom functions list`:

  ![file di registro errori con funzione personalizzata appropriata](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Considerazioni

* `parameter type` e `return type` non supportano `None`.

* Le funzioni non supportate nell&#39;elenco delle funzioni personalizzate sono:
   * Funzioni del generatore
   * Funzioni Async/Await
   * Definizioni dei metodi
   * Metodi di classe
   * Parametri predefiniti
   * Parametri rimanenti

## Consulta anche {#see-also}

{{see-also}}


