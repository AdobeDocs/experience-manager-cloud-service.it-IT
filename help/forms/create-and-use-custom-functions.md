---
title: Utilizzo di funzioni personalizzate in un modulo adattivo
description: AEM Forms supporta funzioni personalizzate che consentono agli utenti di creare e utilizzare le proprie funzioni all’interno dell’editor di regole.
keywords: Aggiungi una funzione personalizzata, utilizza una funzione personalizzata, crea una funzione personalizzata, utilizza la funzione personalizzata nell’editor di regole.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: 5b5b44f8dffc01a75eda464cd7759cf03028c2c6
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 2%

---


# Introduzione alle funzioni personalizzate per moduli adattivi basati su componenti core

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions-core-components) |
| AEM as a Cloud Service | Questo articolo |

AEM Forms supporta funzioni personalizzate che consentono agli utenti di definire funzioni JavaScript per l’implementazione di regole aziendali complesse. Queste funzioni personalizzate estendono le funzionalità dei moduli facilitando la manipolazione e l’elaborazione dei dati immessi per soddisfare requisiti specifici. Consentono di modificare dinamicamente il comportamento delle forme in base a criteri predefiniti. Le funzioni personalizzate consentono inoltre agli sviluppatori di applicare logiche di convalida complesse, eseguire calcoli dinamici e controllare la visualizzazione o il comportamento degli elementi del modulo in base alle interazioni dell&#39;utente o a criteri predefiniti.

>[!NOTE]
>
> Verificare che il [componente core](https://github.com/adobe/aem-core-forms-components) sia impostato sulla versione più recente per utilizzare le funzionalità più recenti.

## Utilizzo di funzioni personalizzate {#uses-of-custom-function}

L’utilizzo di funzioni personalizzate in Adaptive Forms offre i seguenti vantaggi:
* **Elaborazione dei dati**: le funzioni personalizzate consentono di elaborare i dati immessi nei campi dei moduli.
* **Convalida dei dati**: le funzioni personalizzate consentono di eseguire controlli personalizzati sugli input dei moduli e di fornire messaggi di errore specifici.
* **Comportamento dinamico**: le funzioni personalizzate consentono di controllare il comportamento dinamico dei moduli in base a condizioni specifiche. Ad esempio, è possibile visualizzare/nascondere campi, modificare i valori dei campi o modificare dinamicamente la logica del modulo.
* **Integrazione**: è possibile utilizzare funzioni personalizzate da integrare con API o servizi esterni. Consente di recuperare dati da origini esterne, inviare dati agli endpoint Rest esterni o eseguire azioni personalizzate basate su eventi esterni.

Le funzioni personalizzate sono essenzialmente librerie client aggiunte al file JavaScript. Una volta creata, una funzione personalizzata diventa disponibile nell’editor di regole per la selezione da parte dell’utente in un modulo adattivo. Le funzioni personalizzate sono identificate dalle annotazioni di JavaScript nell’editor di regole.

## Annotazioni di JavaScript supportate per la funzione personalizzata {#js-annotations}

Le annotazioni JavaScript vengono utilizzate per fornire metadati per il codice JavaScript. Include commenti che iniziano con simboli specifici, ad esempio /** e @. Le annotazioni forniscono informazioni importanti su funzioni, variabili e altri elementi nel codice. Il modulo adattivo supporta le seguenti annotazioni di JavaScript per le funzioni personalizzate:

### Nome

Il nome viene utilizzato per identificare la funzione personalizzata nell’editor di regole di un modulo adattivo. Per denominare una funzione personalizzata vengono utilizzate le sintassi seguenti:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` è il nome della funzione. Gli spazi non sono consentiti.
  `<Function Name>` è il nome visualizzato della funzione nell&#39;editor di regole di un modulo adattivo.
Se il nome della funzione è identico al nome della funzione stessa, è possibile omettere `[functionName]` dalla sintassi.

### Parametro

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
   * ambito: rappresenta l&#39;oggetto globals, che contiene variabili di sola lettura quali istanze di moduli, istanze di campi di destinazione e metodi per l&#39;esecuzione di modifiche di moduli all&#39;interno di funzioni personalizzate. Viene dichiarato come ultimo parametro nelle annotazioni di JavaScript e non è visibile nell’editor di regole di un modulo adattivo. Il parametro scope accede all&#39;oggetto del modulo o del componente per attivare la regola o l&#39;evento necessario per l&#39;elaborazione del modulo. Per ulteriori informazioni sull&#39;oggetto Globals e su come utilizzarlo, [fare clic qui](/help/forms/custom-function-core-component-scope-function.md).

Il tipo di parametro non fa distinzione tra maiuscole e minuscole e non sono consentiti spazi nel nome del parametro.

`<Parameter Description>` contiene dettagli sullo scopo del parametro. Può avere più parole.

#### Parametri facoltativi

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

### Tipo restituito

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

### Privata

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

## Problema noto

* Le funzioni personalizzate non supportano i valori letterali delle espressioni regolari di JavaScript. L’utilizzo di valori letterali regex in una funzione personalizzata genera errori durante l’esecuzione. Ad esempio:
  `const pattern = /^abc$/;`

  Per garantire la compatibilità, utilizza il costruttore RegExp nelle funzioni personalizzate.

  `const pattern = new RegExp("^abc$");`
Effettua il refactoring delle espressioni regolari per utilizzare il costruttore RegExp per garantire un’esecuzione coerente e affidabile.

## Passaggio successivo

Per creare e utilizzare una funzione personalizzata nel modulo adattivo, consulta l&#39;articolo [Creare una funzione personalizzata per un modulo adattivo basato su componenti core](/help/forms/custom-function-core-component-create-function.md).

## Consulta anche

{{see-also-rule-editor}}