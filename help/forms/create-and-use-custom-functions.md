---
title: Creare e aggiungere funzioni personalizzate in un modulo adattivo
description: AEM Forms supporta funzioni personalizzate che consentono agli utenti di creare e utilizzare le proprie funzioni all’interno dell’editor di regole.
keywords: Aggiungi una funzione personalizzata, utilizza una funzione personalizzata, crea una funzione personalizzata, utilizza la funzione personalizzata nell’editor di regole.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
mini-toc-levels: 4
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
source-git-commit: 4cd7924e99809146e111f6b3309db0a8292e61b1
workflow-type: tm+mt
source-wordcount: '3510'
ht-degree: 0%

---


<span class="preview"> Questo articolo contiene `Override form submission success and error handlers` come funzione pre-release. La funzione di pre-release è accessibile solo tramite [canale preliminare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features).

# Funzioni personalizzate in Forms adattivo (componenti core)

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | Questo articolo |

## Introduzione

AEM Forms supporta funzioni personalizzate che consentono agli utenti di definire funzioni JavaScript per l’implementazione di regole di business complesse. Queste funzioni personalizzate estendono le funzionalità dei moduli facilitando la manipolazione e l’elaborazione dei dati immessi per soddisfare requisiti specifici. Consentono inoltre di modificare dinamicamente il comportamento delle forme in base a criteri predefiniti.

>[!NOTE]
>
> Assicurati che [componente core](https://github.com/adobe/aem-core-forms-components) è impostato sulla versione più recente per utilizzare le funzioni più recenti.

### Utilizzo di funzioni personalizzate {#uses-of-custom-function}

L’utilizzo di funzioni personalizzate in Adaptive Forms offre i seguenti vantaggi:
* **Trattamento dei dati**: le funzioni personalizzate consentono di elaborare i dati immessi nei campi dei moduli.
* **Convalida dei dati**: le funzioni personalizzate ti consentono di eseguire controlli personalizzati sugli input dei moduli e fornire messaggi di errore specifici.
* **Comportamento dinamico**: le funzioni personalizzate consentono di controllare il comportamento dinamico dei moduli in base a condizioni specifiche. Ad esempio, è possibile visualizzare/nascondere campi, modificare i valori dei campi o modificare dinamicamente la logica del modulo.
* **Integrazione**: puoi utilizzare funzioni personalizzate da integrare con API o servizi esterni. Consente di recuperare dati da origini esterne, inviare dati agli endpoint Rest esterni o eseguire azioni personalizzate basate su eventi esterni.

Le funzioni personalizzate sono essenzialmente librerie client aggiunte nel file JavaScript. Una volta creata, una funzione personalizzata diventa disponibile nell’editor di regole per la selezione da parte dell’utente in un modulo adattivo. Le funzioni personalizzate sono identificate dalle annotazioni JavaScript nell’editor di regole.

### Annotazioni JavaScript supportate per la funzione personalizzata {#js-annotations}

Le annotazioni JavaScript vengono utilizzate per fornire metadati per il codice JavaScript. Include commenti che iniziano con simboli specifici, ad esempio /** e @. Le annotazioni forniscono informazioni importanti su funzioni, variabili e altri elementi nel codice. Il modulo adattivo supporta le seguenti annotazioni JavaScript per le funzioni personalizzate:

#### Nome

Il nome viene utilizzato per identificare la funzione personalizzata nell’editor di regole di un modulo adattivo. Per denominare una funzione personalizzata vengono utilizzate le sintassi seguenti:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` è il nome della funzione. Gli spazi non sono consentiti.
  `<Function Name>` è il nome visualizzato della funzione nell’editor di regole di un modulo adattivo.
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
   * numero[]: rappresenta una matrice di valori numerici.
   * booleano[]: rappresenta una matrice di valori booleani.
   * data: rappresenta un singolo valore di data.
   * data[]: rappresenta una matrice di valori di data.
   * array: rappresenta una matrice generica contenente valori di vari tipi.
   * object: rappresenta un oggetto modulo passato a una funzione personalizzata anziché passare direttamente il relativo valore.
   * ambito: rappresenta l&#39;oggetto globals, che contiene variabili di sola lettura quali istanze di moduli, istanze di campi di destinazione e metodi per l&#39;esecuzione di modifiche di moduli all&#39;interno di funzioni personalizzate. Viene dichiarato come ultimo parametro nelle annotazioni JavaScript e non è visibile nell’editor di regole di un modulo adattivo. Il parametro scope accede all&#39;oggetto del modulo o del componente per attivare la regola o l&#39;evento necessario per l&#39;elaborazione del modulo. Per ulteriori informazioni sull&#39;oggetto Globals e su come utilizzarlo, [fai clic qui](/help/forms/create-and-use-custom-functions.md#support-field-and-global-objects).

Il tipo di parametro non fa distinzione tra maiuscole e minuscole e non sono consentiti spazi nel nome del parametro.

`<Parameter Description>` contiene dettagli sullo scopo del parametro. Può avere più parole.

**Parametri facoltativi**
Per impostazione predefinita, tutti i parametri sono obbligatori. È possibile definire un parametro come facoltativo aggiungendo `=` dopo il tipo di parametro o che racchiude il nome del parametro in  `[]`. I parametri definiti come facoltativi nelle annotazioni JavaScript vengono visualizzati come facoltativi nell’editor di regole.
Per definire una variabile come parametro facoltativo, è possibile utilizzare una delle sintassi seguenti:

* `@param {type=} Input1`

Nella riga di codice precedente, `Input1` è un parametro facoltativo senza alcun valore predefinito. Per dichiarare un parametro facoltativo con valore predefinito:
`@param {string=<value>} input1`

`input1` come parametro facoltativo con il valore predefinito impostato su `value`.

* `@param {type} [Input1]`

Nella riga di codice precedente, `Input1` è un parametro facoltativo senza alcun valore predefinito. Per dichiarare un parametro facoltativo con valore predefinito:
`@param {array} [input1=<value>]`
`input1` è un parametro facoltativo di tipo array con il valore predefinito impostato su `value`.
Assicuratevi che il tipo di parametro sia racchiuso tra parentesi graffe {} e il nome del parametro è racchiuso tra parentesi quadre [].

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

L&#39;illustrazione seguente viene visualizzata utilizzando `OptionalParameterFunction` funzione personalizzata nell’editor di regole:

![Parametri facoltativi o obbligatori ](/help/forms/assets/optional-default-params.png)

Puoi salvare la regola senza specificare un valore per i parametri richiesti, ma la regola non viene eseguita e visualizza un messaggio di avviso come:

![avviso di regola incompleto](/help/forms/assets/incomplete-rule.png)

Quando l’utente lascia vuoto il parametro opzionale, il valore &quot;Undefined&quot; (Non definito) viene passato alla funzione personalizzata per il parametro opzionale.

Per ulteriori informazioni su come definire parametri opzionali nei JSDocs, [fai clic qui](https://jsdoc.app/tags-param).

#### Tipo restituito

Il tipo restituito specifica il tipo di valore restituito dalla funzione personalizzata dopo l&#39;esecuzione. Le seguenti sintassi vengono utilizzate per definire un tipo restituito in una funzione personalizzata:

* `@return {type}`
* `@returns {type}`
  `{type}` rappresenta il tipo restituito della funzione. I tipi restituiti consentiti sono:
   * string (stringa): rappresenta un singolo valore di stringa.
   * number: rappresenta un singolo valore numerico.
   * booleano: rappresenta un singolo valore booleano (true o false).
   * stringa[]: rappresenta una matrice di valori stringa.
   * numero[]: rappresenta una matrice di valori numerici.
   * booleano[]: rappresenta una matrice di valori booleani.
   * data: rappresenta un singolo valore di data.
   * data[]: rappresenta una matrice di valori di data.
   * array: rappresenta una matrice generica contenente valori di vari tipi.
   * object: rappresenta direttamente l&#39;oggetto modulo anziché il relativo valore.

  Il tipo restituito non fa distinzione tra maiuscole e minuscole.

#### Privata

La funzione personalizzata dichiarata come privata non viene visualizzata nell’elenco delle funzioni personalizzate nell’editor delle regole di un modulo adattivo. Per impostazione predefinita, le funzioni personalizzate sono pubbliche. Sintassi per dichiarare la funzione personalizzata come privata `@private`.


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

Crea una libreria client per chiamare funzioni personalizzate nell’editor di regole. Per ulteriori informazioni, consulta [Utilizzo delle librerie lato client](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

I passaggi per creare funzioni personalizzate sono i seguenti:
1. [Creare una libreria client](#create-client-library)
1. [Aggiungere una libreria client a un modulo adattivo](#use-custom-function)

### Creare una libreria client {#create-client-library}

Puoi aggiungere funzioni personalizzate aggiungendo una libreria client. Per creare una libreria client, effettua le seguenti operazioni:

1. [Clonare l’archivio as a Cloud Service di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).
1. Creare una cartella in `[AEM Forms as a Cloud Service repository folder]/apps/` cartella. Ad esempio, crea una cartella denominata come `experience-league`.
1. Accedi a `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` e creare un `ClientLibraryFolder`. Ad esempio, crea una cartella della libreria client come `customclientlibs`.
1. Aggiungi una proprietà `categories` con valore di tipo stringa. Ad esempio, assegna il valore `customfunctionscategory` al `categories` proprietà per `customclientlibs` cartella.

   >[!NOTE]
   >
   > Puoi scegliere un nome qualsiasi per `client library folder` e `categories` proprietà.

1. Crea una cartella denominata `js`.
1. Accedi a `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` cartella.
1. Aggiungi un file JavaScript, ad esempio: `function.js`. Il file contiene il codice per la funzione personalizzata.
1. Salva il `function.js` file.
1. Accedi a `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` cartella.
1. Aggiungi un file di testo come `js.txt`. Il file contiene:

   ```javascript
       #base=js
       functions.js
   ```

1. Salva il `js.txt` file.
1. Aggiungi, esegui il commit e invia le modifiche nell’archivio utilizzando i seguenti comandi:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. [Eseguire la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) per distribuire la funzione personalizzata.

Una volta eseguita correttamente la pipeline, la funzione personalizzata aggiunta nella libreria client diventa disponibile nel [Editor di regole per moduli adattivi](/help/forms/rule-editor-core-components.md).

### Aggiungere una libreria client a un modulo adattivo{#use-custom-function}

Dopo aver implementato la libreria client nell’ambiente Forms CS, utilizzane le funzionalità nel modulo adattivo. Per aggiungere la libreria client al modulo adattivo

1. Apri il modulo in modalità di modifica. Per aprire un modulo in modalità di modifica, selezionare un modulo e selezionare **[!UICONTROL Modifica]**.
1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri **[!UICONTROL Base]** e seleziona il nome del **[!UICONTROL categoria libreria client]** dall’elenco a discesa (in questo caso, seleziona `customfunctionscategory`).

   ![Aggiunta della libreria client della funzione personalizzata](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > È possibile aggiungere più categorie specificando un elenco separato da virgole all’interno del **[!UICONTROL Categoria libreria client]** campo.

1. Clic **[!UICONTROL Fine]**.

È possibile utilizzare la funzione personalizzata in [editor di regole di un modulo adattivo](/help/forms/rule-editor-core-components.md) utilizzando [Annotazioni JavaScript](##js-annotations).

## Utilizzo di una funzione personalizzata in un modulo adattivo

In un modulo adattivo, puoi utilizzare [funzioni personalizzate nell’editor di regole](/help/forms/rule-editor-core-components.md). Aggiungiamo il seguente codice al file JavaScript (`Function.js` file) per calcolare l&#39;età in base alla data di nascita (AAAA-MM-GG). Creare una funzione personalizzata come `calculateAge()` prende la data di nascita come dato di partenza e restituisce l’età:

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

Nell’esempio precedente, quando l’utente immette la data di nascita nel formato (AAAA-MM-GG), la funzione personalizzata `calculateAge` viene richiamato e restituisce l’età.

![Funzione personalizzata Calcola età nell’editor di regole](/help/forms/assets/custom-function-calculate-age.png)

Visualizziamo in anteprima il modulo per osservare come le funzioni personalizzate vengono implementate tramite l’editor di regole:

![Funzione personalizzata Calcola età nell’anteprima del modulo dell’editor di regole](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Puoi consultare quanto segue [funzione personalizzata](/help/forms/assets//customfunctions.zip) cartella. Scarica e installa questa cartella nell’istanza AEM utilizzando [Gestione pacchetti](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).


### Impostare le opzioni dell’elenco a discesa utilizzando le funzioni personalizzate

L’editor di regole nei Componenti core non supporta **Imposta opzioni di** per impostare le opzioni dell’elenco a discesa in fase di esecuzione. Tuttavia, è possibile impostare le opzioni dell’elenco a discesa utilizzando le funzioni personalizzate.

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

Nel codice di cui sopra, `setEnums` viene utilizzato per impostare `enum` proprietà e `setEnumNames` viene utilizzato per impostare `enumNames` proprietà dell’elenco a discesa.

Creiamo una regola per `Next` , che imposta il valore dell’opzione dell’elenco a discesa quando l’utente fa clic sul pulsante `Next` pulsante:

![Opzioni elenco a discesa](/help/forms/assets/drop-down-list-options.png)

Fai riferimento all’illustrazione seguente per dimostrare dove sono impostate le opzioni dell’elenco a discesa facendo clic sul pulsante Visualizza:

![Opzioni elenco a discesa nell’editor delle regole](/help/forms/assets/drop-down-option-rule-editor.png)



### Supporto delle funzioni asincrone nelle funzioni personalizzate {#support-of-async-functions}

Le funzioni personalizzate asincrone non vengono visualizzate nell’elenco dell’editor di regole. Tuttavia, è possibile richiamare funzioni asincrone all’interno di funzioni personalizzate create utilizzando espressioni di funzioni sincrone.

![Sincronizza e asincronizza funzione personalizzata](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

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

Nell&#39;esempio precedente, la funzione asyncFunction è un `asynchronous function`. Esegue un&#39;operazione asincrona eseguendo una `GET` richiesta a `https://petstore.swagger.io/v2/store/inventory`. Attende la risposta utilizzando `await`, analizza il corpo della risposta come JSON utilizzando `response.json()`, quindi restituisce i dati. Il `callAsyncFunction` è una funzione personalizzata sincrona che richiama `asyncFunction` e visualizza i dati di risposta nella console. Anche se il `callAsyncFunction` è sincrona, chiama la funzione asyncFunction asincrona e gestisce il relativo risultato con `then` e `catch` istruzioni.

Per vedere come funziona, aggiungiamo un pulsante e creiamo una regola per il pulsante che richiama la funzione asincrona al clic di un pulsante.

![creazione regola per funzione asincrona](/help/forms/assets/rule-for-async-funct.png)

Fai riferimento all’illustrazione della finestra della console seguente per dimostrare che quando l’utente fa clic su `Fetch` , la funzione personalizzata `callAsyncFunction` viene richiamato, che a sua volta chiama una funzione asincrona `asyncFunction`. Inspect nella finestra della console per visualizzare la risposta al pulsante, fai clic su:

![Finestra della console](/help/forms/assets/async-custom-funct-console.png)

Approfondiamo le funzioni personalizzate.

## Varie funzioni per funzioni personalizzate

È possibile utilizzare funzioni personalizzate per aggiungere caratteristiche personalizzate ai moduli. Queste funzioni supportano varie funzionalità, ad esempio l’utilizzo di campi specifici, l’utilizzo di campi globali o la memorizzazione in cache. Questa flessibilità consente di personalizzare i moduli in base ai requisiti aziendali.

### Oggetti di ambito Field e Global nelle funzioni personalizzate {#support-field-and-global-objects}

Gli oggetti Field fanno riferimento ai singoli componenti o elementi di un modulo, ad esempio campi di testo e caselle di controllo. L&#39;oggetto Globals contiene variabili di sola lettura quali l&#39;istanza del modulo, l&#39;istanza del campo di destinazione e i metodi per apportare modifiche al modulo nelle funzioni personalizzate.

>[!NOTE]
>
> Il `param {scope} globals` deve essere l’ultimo parametro e non viene visualizzato nell’editor di regole di un modulo adattivo.

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

Scopri in che modo le funzioni personalizzate utilizzano gli oggetti campo e globali con l’aiuto di un `Contact Us` utilizzando casi d’uso diversi.

![Modulo per contattarci](/help/forms/assets/contact-us-form.png)

#### Visualizzare un pannello utilizzando la regola SetProperty

Aggiungi il seguente codice nella funzione personalizzata come spiegato in [create-custom-function](#create-custom-function) , per impostare il campo modulo come `Required`.

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
> * Puoi configurare le proprietà del campo utilizzando le proprietà disponibili in `[form-path]/jcr:content/guideContainer.model.json`.
> * Modifiche apportate al modulo utilizzando `setProperty` Il metodo dell&#39;oggetto Globals è asincrono e non viene riflesso durante l&#39;esecuzione della funzione personalizzata.

In questo esempio, la convalida del `personaldetails` facendo clic sul pulsante. Se non vengono rilevati errori nel pannello, viene visualizzato un altro pannello, `feedback` visibile al clic del pulsante.

Creiamo una regola per `Next` , che convalida il `personaldetails` e rende `feedback`  visibile quando l’utente fa clic su `Next` pulsante.

![Imposta proprietà](/help/forms/assets/custom-function-set-property.png)

Fare riferimento all&#39;illustrazione seguente per dimostrare dove `personaldetails` viene convalidato facendo clic sul pulsante `Next` pulsante. Nel caso in cui tutti i campi all’interno di `personaldetails` sono convalidati, `feedback` diventa visibile.

![Anteprima modulo proprietà](/help/forms/assets/set-property-form-preview.png)

Se sono presenti errori nei campi di `personaldetails` a livello di campo facendo clic sul pulsante `Next` e `feedback` il pannello rimane invisibile.

![Anteprima modulo proprietà](/help/forms/assets/set-property-panel.png)


#### Convalida un campo.

Aggiungi il seguente codice nella funzione personalizzata come spiegato in [create-custom-function](#create-custom-function) per convalidare il campo.

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
> Se non viene passato alcun argomento nel `validate()` funzione, convalida il modulo.

In questo esempio, un pattern di convalida personalizzato viene applicato al `contact` campo. Gli utenti devono inserire un numero di telefono che inizia con `10` seguito da `8` cifre. Se l’utente immette un numero di telefono che non inizia con `10` o contiene più o meno di `8` cifre, viene visualizzato un messaggio di errore di convalida al clic del pulsante:

![Pattern di convalida dell’indirizzo e-mail](/help/forms/assets/custom-function-validation-pattern.png)

Il passaggio successivo consiste nel creare una regola per `Next` pulsante che convalida `contact` sul pulsante, fai clic su.

![Pattern di convalida](/help/forms/assets/custom-function-validate.png)

Fai riferimento all’illustrazione seguente per dimostrare che se l’utente immette un numero di telefono che non inizia con `10`, a livello di campo viene visualizzato un messaggio di errore:

![Pattern di convalida dell’indirizzo e-mail](/help/forms/assets/custom-function-validate-error-message.png)

Se l’utente immette un numero di telefono valido e tutti i campi nel campo `personaldetails` vengono convalidati, il `feedback` Il pannello viene visualizzato sullo schermo:

![Pattern di convalida dell’indirizzo e-mail](/help/forms/assets/validate-form-preview-form.png)



#### Reimpostare un pannello

Aggiungi il seguente codice nella funzione personalizzata come spiegato in [create-custom-function](#create-custom-function) per ripristinare il pannello.

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
> Se non viene passato alcun argomento nel `reset()` funzione, convalida il modulo.

In questo esempio, la proprietà `personaldetails` il pannello viene ripristinato facendo clic su `Clear` pulsante. Il passaggio successivo consiste nel creare una regola per `Clear` che ripristina il pannello facendo clic sul pulsante.

![Pulsante Cancella](/help/forms/assets/custom-function-reset-field.png)

Vedere l&#39;illustrazione seguente per mostrare che se l&#39;utente fa clic su `clear` pulsante, il pulsante `personaldetails` ripristini pannello:

![Reimposta modulo](/help/forms/assets/custom-function-reset-form.png)



#### Per visualizzare un messaggio personalizzato a livello di campo e contrassegnare il campo come non valido

È possibile utilizzare `markFieldAsInvalid()` per definire un campo come non valido e impostare un messaggio di errore personalizzato a livello di campo. Il `fieldIdentifier` il valore può essere `fieldId`, o `field qualifiedName`, o `field dataRef`. Il valore dell’oggetto denominato `option` può essere `{useId: true}`, `{useQualifiedName: true}`, o `{useDataRef: true}`.
Le sintassi utilizzate per contrassegnare un campo come non valido e impostare un messaggio personalizzato sono:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Aggiungi il seguente codice nella funzione personalizzata come spiegato in [create-custom-function](#create-custom-function) per abilitare un messaggio personalizzato a livello di campo.

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

Il passaggio successivo consiste nel creare una regola per `comments` campo:

![Contrassegna campo come non valido](/help/forms/assets/custom-function-invalid-field.png)

Vedere la dimostrazione riportata di seguito per mostrare che l&#39;immissione di feedback negativo nel `comments` Il campo attiva la visualizzazione di un messaggio personalizzato a livello di campo:

![Contrassegna campo come modulo di anteprima non valido](/help/forms/assets/custom-function-invalidfield-form.png)

Se l’utente immette più di 15 caratteri nella casella di testo dei commenti, il campo viene convalidato e il modulo viene inviato:

![Contrassegna campo come modulo di anteprima valido](/help/forms/assets/custom-function-validfield-form.png)



#### Modificare i dati acquisiti prima dell&#39;invio

La seguente riga di codice:
`globals.functions.submitForm(globals.functions.exportData(), false);` viene utilizzato per inviare i dati del modulo dopo la manipolazione.
* Il primo argomento è costituito dai dati da inviare.
* Il secondo argomento indica se il modulo deve essere convalidato prima dell&#39;invio. È `optional` e impostato come `true` per impostazione predefinita.
* Il terzo argomento è il seguente: `contentType` dell’invio, che è anche facoltativo con il valore predefinito come `multipart/form-data`. Gli altri valori possono essere `application/json` e `application/x-www-form-urlencoded`.

Aggiungi il seguente codice nella funzione personalizzata come spiegato in [create-custom-function](#create-custom-function) per inviare i dati manipolati sul server:

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

In questo esempio, se l’utente lascia il `comments` casella di testo vuota, il `NA` viene inviato al server al momento dell’invio del modulo.

Ora, crea una regola per `Submit` pulsante che invia i dati:

![Inviare dati](/help/forms/assets/custom-function-submit-data.png)

Fai riferimento all’illustrazione della `console window` di seguito per dimostrare che se l’utente abbandona `comments` casella di testo vuota, quindi il valore come `NA` viene inviato nel server:

![Invia dati nella finestra della console](/help/forms/assets/custom-function-submit-data-form.png)

È inoltre possibile esaminare la finestra della console per visualizzare i dati inviati al server:

![Dati di Inspect nella finestra della console](/help/forms/assets/custom-function-submit-data-console-data.png)



#### Ignora messaggi di errore e di completamento dell’invio del modulo

Aggiungi la seguente riga di codice come spiegato in [create-custom-function](#create-custom-function) , per personalizzare il messaggio di invio o di errore per l’invio dei moduli e visualizzare i messaggi di invio dei moduli in una casella modale:

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

In questo esempio, quando l’utente utilizza `customSubmitSuccessHandler` e `customSubmitErrorHandler` funzioni personalizzate, i messaggi di esito positivo e negativo vengono visualizzati in una finestra modale. La funzione JavaScript `showModal(type, message)` viene utilizzato per creare e visualizzare in modo dinamico una finestra di dialogo modale su uno schermo.

Ora, crea una regola per l’invio corretto del modulo:

![Invio modulo completato](/help/forms/assets/form-submission-success.png)

Fai riferimento all’illustrazione seguente per dimostrare che, quando il modulo viene inviato correttamente, il messaggio di successo viene visualizzato in una finestra modale:

![Messaggio di esito positivo invio modulo](/help/forms/assets/form-submission-success-message.png)

Allo stesso modo, creiamo una regola per gli invii di moduli non riusciti:

![Invio del modulo non riuscito](/help/forms/assets/form-submission-fail.png)

Fai riferimento all’illustrazione seguente per dimostrare che quando l’invio del modulo non riesce, il messaggio di errore viene visualizzato in un modale:

![Messaggio di errore invio modulo](/help/forms/assets/form-submission-fail-message.png)

Per visualizzare l’invio dei moduli riuscito o non riuscito in modo predefinito, `Default submit Form Success Handler` e `Default submit Form Error Handler` funzioni pronte all’uso.

Nel caso in cui il gestore di invio personalizzato non riesca a eseguire le operazioni previste nei progetti o moduli AEM esistenti, fare riferimento a [risoluzione dei problemi](#troubleshooting) sezione.

<!--


#### Use Case:  Perform actions in a specific instance of the repeatable panel 

Rules created using the visual rule editor on a repeatable panel apply to the last instance of the repeatable panel. To write a rule for a specific instance of the repeatable panel, we can use a custom function.

Let's create a form to collect information about travelers heading to a destination. A traveler panel is added as a repeatable panel, where the user can add details for 5 travelers using the Add button.

Add the following line of code as explained in the [create-custom-function](#create-custom-function) section, to perform actions in a specific instance of the repeatable panel, other than the last one:

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
 
In this example, the `hidePanelInRepeatablePanel` custom function performs action in a specific instance of the repeatable panel. In the above code, `travelerinfo` represents the repeatable panel. The `repeatablePanel[1].traveler, {visible: false}` code hides the panel in the second instance of the repeatable panel. 
Let us add a button labeled `Hide` to add a rule to hide a specific panel.

![Hide Panel rule](/help/forms/assets/custom-function-hidepanel-rule.png)

Refer to the video below to demonstrate that when the `Hide` is clicked, the panel in the second repeatable instance hides:




#### **Usecase**: Pre-fill the field with a value when the form loads

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to load the pre-filled value in a field when the form is initialized:

```javascript
/**
 * @name importData
 * @param {scope} globals
 */
function importData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount',200000]]));
} 
```

In the aforementioned code, the `importData` function updates the value in the `amount` textbox field when the form loads.

Let us create a rule for the `Submit` button, where the value in the `amount` textbox field changes to specified value when the form loads:

![Import Data Rule](/help/forms/assets/custom-function-import-data.png)

Refer to the screenshot below, which demonstrates that when the form loads, the value in the amount textbox is pre-filled with a specified value:

![Import Data Rule](/help/forms/assets/cg)



#### **Usecase**: Set focus on the specific field

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to set focus on the specified field when the `Submit` button is clicked.:

```javascript
/**
 * @name setFocus
 * @param {object} field
 * @param {scope} globals
 */
function setFocus(field, globals)
{
    globals.functions.setFocus(field);
}
```

Let us add a rule to the `Submit` button to set focus on the `email` field when it is clicked:

![Set Focus Rule](/help/forms/assets/custom-function-set-focus.png)

Refer to the screenshot below, which demonstrates that when the `Submit` button is clicked, the focus is set on the `email` field:

![Set Focus Rule](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> You can use the optional `$focusOption` parameter, if you want to focus on the next or previous field relative to the `email` field.

+++

+++ **Usecase**: Add or delete repeatable panel using the `dispatchEvent` property

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to add a panel when the `Add Traveler` button is clicked using the `dispatchEvent` property:

```javascript
/**
 
 * @name addInstance
 * @param {scope} globals
 */
function addInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'addInstance');
} 

```

Let us add a rule to the `Add Traveler` button to add the repeatable panel when it is clicked:

![Add Panel Rule](/help/forms/assets/custom-function-add-panel.png)

Refer to the screenshot below, which demonstrates that when the `Add Traveler` button is clicked, the traveler panel is added using the `dispatchEvent` property:

![Add Panel](/help/forms/assets/customg)

Similarly, add a button labeled `Delete Traveler` to delete a panel. Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to delete a panel when the `Delete Traveler` button is clicked using the `dispatchEvent` property:

```javascript

/**
 
 * @name removeInstance
 * @param {scope} globals
 */
function removeInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 

```
Let us add a rule to the `Delete Traveler` button to delete the repeatable panel when it is clicked:

![Delete Panel Rule](/help/forms/assets/custom-function-delete-panel.png)

Refer to the screenshot below, which demonstrates that when the `Delete Traveler` button is clicked, the traveler panel is deleted using the `dispatchEvent` property:

![Delete Panel](/help/forms/assets/customg)
-->

## Supporto della memorizzazione in cache per la funzione personalizzata

Forms adattivo implementa il caching per le funzioni personalizzate per migliorare il tempo di risposta durante il recupero dell’elenco delle funzioni personalizzate nell’editor di regole. Un messaggio come `Fetched following custom functions list from cache` viene visualizzato nel `error.log` file.

![funzione personalizzata con supporto cache](/help/forms/assets/custom-function-cache-error.png)

Se le funzioni personalizzate vengono modificate, la memorizzazione in cache viene invalidata e analizzata.

## Risoluzione dei problemi {#troubleshooting}

* Se il gestore di invio personalizzato non funziona come previsto nei progetti o moduli AEM esistenti, effettua le seguenti operazioni:
   * Assicurati che [versione dei componenti core aggiornata a 3.0.18 e successive](https://github.com/adobe/aem-core-forms-components). Tuttavia, per i progetti e i moduli AEM esistenti, vi sono ulteriori passi da seguire:

   * Per il progetto AEM, l’utente deve sostituire tutte le istanze di `submitForm('custom:submitSuccess', 'custom:submitError')` con `submitForm()` e implementa il progetto tramite la pipeline di Cloud Manager.

   * Per i moduli esistenti, se i gestori di invio personalizzati non funzionano correttamente, l’utente deve aprire e salvare il `submitForm` regola sul **Invia** tramite l&#39;editor di regole. Questa azione sostituisce la regola esistente da `submitForm('custom:submitSuccess', 'custom:submitError')` con `submitForm()` nel modulo.


* Se il file JavaScript contenente il codice per le funzioni personalizzate presenta un errore, le funzioni personalizzate non sono elencate nell’editor di regole di un modulo adattivo. Per verificare l&#39;elenco delle funzioni personalizzate, è possibile passare alla `error.log` file per l’errore. In caso di errore, l’elenco delle funzioni personalizzate appare vuoto:

  ![file registro errori](/help/forms/assets/custom-function-list-error-file.png)

  In caso di errore, la funzione personalizzata viene recuperata e visualizzata in `error.log` file. Un messaggio come `Fetched following custom functions list` viene visualizzato nel `error.log` file:

  ![file di log degli errori con la funzione personalizzata corretta](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Considerazioni

* Il `parameter type` e `return type` non supportano `None`.

* Le funzioni non supportate nell&#39;elenco delle funzioni personalizzate sono:
   * Funzioni del generatore
   * Funzioni Async/Await
   * Definizioni dei metodi
   * Metodi di classe
   * Parametri predefiniti
   * Parametri rimanenti

## Consulta anche {#see-also}

{{see-also}}


