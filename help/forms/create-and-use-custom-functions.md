---
title: Creare e aggiungere funzioni personalizzate in un modulo adattivo
description: AEM Forms supporta funzioni personalizzate che consentono agli utenti di creare e utilizzare le proprie funzioni all’interno dell’editor di regole.
keywords: Aggiungi una funzione personalizzata, utilizza una funzione personalizzata, crea una funzione personalizzata, utilizza la funzione personalizzata nell’editor di regole.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: 46fbed98a806f62dd1882eb0085d4338c5cd51a7
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 1%

---


# Funzioni personalizzate in Forms adattivo (componenti core)

## Introduzione

AEM Forms supporta funzioni personalizzate che consentono agli utenti di definire funzioni JavaScript per l’implementazione di regole di business complesse. Queste funzioni personalizzate estendono le funzionalità dei moduli facilitando la manipolazione e l’elaborazione dei dati immessi per soddisfare requisiti specifici. Consentono inoltre di modificare dinamicamente il comportamento delle forme in base a criteri predefiniti.
In Adaptive Forms, puoi utilizzare funzioni personalizzate all’interno del [editor di regole di un modulo adattivo](/help/forms/rule-editor-core-components.md) per creare regole di convalida specifiche per i campi modulo.

Comprendiamo l’utilizzo della funzione personalizzata, in cui gli utenti immettono l’indirizzo e-mail e desideri che l’indirizzo e-mail inserito segua un formato specifico (contiene il simbolo &quot;@&quot; e un nome di dominio). Crea una funzione personalizzata come &quot;ValidateEmail&quot; che accetta l’indirizzo e-mail come input e restituisce true se è valido, altrimenti restituisce false.

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

Nell’esempio precedente, quando l’utente tenta di inviare il modulo, viene richiamata la funzione personalizzata &quot;ValidateEmail&quot; per verificare se l’indirizzo e-mail inserito è valido.

### Utilizzo di funzioni personalizzate {#uses-of-custom-function}

L’utilizzo di funzioni personalizzate in Adaptive Forms offre i seguenti vantaggi:

* **Manipolazione dei dati**: le funzioni personalizzate manipolano ed elaborano i dati immessi nei campi dei moduli.
* **Convalida dei dati**: le funzioni personalizzate ti consentono di eseguire controlli personalizzati sugli input dei moduli e fornire messaggi di errore specifici.
* **Comportamento dinamico**: le funzioni personalizzate consentono di controllare il comportamento dinamico dei moduli in base a condizioni specifiche. Ad esempio, è possibile visualizzare/nascondere campi, modificare i valori dei campi o modificare dinamicamente la logica del modulo.
* **Integrazione**: puoi utilizzare funzioni personalizzate da integrare con API o servizi esterni. Consente di recuperare dati da origini esterne, inviare dati agli endpoint Rest esterni o eseguire azioni personalizzate basate su eventi esterni.

## Note JS supportate

Assicurati che la funzione personalizzata che scrivi sia accompagnata dai `jsdoc` sopra di esso.

Supportato `jsdoc` tag:

* **Privato**
Sintassi: `@private`
Una funzione privata non è inclusa come funzione personalizzata.

* **Nome**
Sintassi: `@name funcName <Function Name>`
In alternativa `,` puoi utilizzare: `@function funcName <Function Name>` **o** `@func` `funcName <Function Name>`.
  `funcName` è il nome della funzione (non sono consentiti spazi).
  `<Function Name>` è il nome visualizzato della funzione.

* **Parametro**
Sintassi: `@param {type} name <Parameter Description>`
In alternativa, puoi utilizzare: `@argument` `{type} name <Parameter Description>` **o** `@arg` `{type}` `name <Parameter Description>`.
Mostra i parametri utilizzati dalla funzione. Una funzione può avere più tag di parametri, uno per ogni parametro in ordine di occorrenza.
  `{type}` rappresenta il tipo di parametro. I tipi di parametri consentiti sono:

   1. stringa
   2. numero
   3. booleano
   4. ambito
   5. stringa[]
   6. numero[]
   7. booleano[]
   8. data
   9. data[]
   10. array
   11. oggetto

  `scope` fa riferimento a uno speciale oggetto globals fornito da forms runtime. Deve essere l’ultimo parametro e non è visibile all’utente nell’editor di regole. È possibile utilizzare l&#39;ambito per accedere a un modulo leggibile e a un oggetto proxy di campo per leggere le proprietà, l&#39;evento che ha attivato la regola e un set di funzioni per manipolare il modulo.

  `object` Il tipo viene utilizzato per passare un oggetto campo leggibile nel parametro a una funzione personalizzata invece di passare il valore.

  Tutti i tipi di parametri sono classificati in una delle categorie precedenti. Nessuno non è supportato. Accertati di selezionare uno dei tipi riportati sopra. I tipi non fanno distinzione tra maiuscole e minuscole. Il nome del parametro non può contenere spazi.  La descrizione del parametro può contenere più parole.

* **Parametro facoltativo**
Sintassi: `@param {type=} name <Parameter Description>`
In alternativa, puoi utilizzare: `@param {type} [name] <Parameter Description>`
Per impostazione predefinita, tutti i parametri sono obbligatori. Per contrassegnare un parametro come facoltativo, aggiungi `=` nel tipo del parametro o inserendo il nome del parametro tra parentesi quadre.
Ad esempio, dichiariamo `Input1` come parametro facoltativo:
   * `@param {type=} Input1`
   * `@param {type} [Input1]`

* **Tipo restituito**
Sintassi: `@return {type}`
In alternativa, puoi utilizzare `@returns {type}`.
Aggiunge informazioni sulla funzione, ad esempio l&#39;obiettivo.
{type} rappresenta il tipo restituito della funzione. I tipi restituiti consentiti sono:

   1. stringa
   2. numero
   3. booleano
   4. stringa[]
   5. numero[]
   6. booleano[]
   7. data
   8. data[]
   9. array
   10. oggetto

Tutti gli altri tipi di reso sono classificati in una delle categorie precedenti. Nessuno non è supportato. Accertati di selezionare uno dei tipi riportati sopra. I tipi restituiti non fanno distinzione tra maiuscole e minuscole.

## Considerazioni durante la creazione di funzioni personalizzate {#considerations}

Per elencare le funzioni personalizzate nell’editor delle regole, puoi dichiararle in uno dei seguenti formati:

* **Istruzione function con o senza commenti jsdoc**

Puoi creare una funzione personalizzata con o senza commenti jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
<!--

* **Arrow function with mandatory jsdoc comment**

Some of the examples to create Arrow functions are:
```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} a some parameter description
    * @param {string} b another parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
```

    * @param {string=} b another parameter description
      /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;-->

* **Espressione di funzione con commento jsdoc obbligatorio**

Per elencare le funzioni personalizzate nell’editor di regole di un modulo adattivo, crea funzioni personalizzate nel formato seguente:

```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} input1 parameter description
    * @param {string} input2 another parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

<!--
* @param {string=} input2 another parameter description
The functions that are not supported in the custom function list are:
* Generator functions
* Async/Await functions 
* Method definitions
* Class methods
* Default parameters
* Rest parameters -->

>[!NOTE]
>
> Puoi controllare la `error.log` per eventuali errori, ad esempio se le funzioni personalizzate non sono elencate nell’editor di regole.

<!--The `error.log` file also displays the methods and parameters that are not supported for custom functions. -->


## Creare una funzione personalizzata {#create-custom-function}

Crea una libreria client per chiamare funzioni personalizzate nell’editor di regole. Per ulteriori informazioni, consulta [Utilizzo delle librerie lato client](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

I passaggi per creare funzioni personalizzate sono i seguenti:
1. [Creare una libreria client](#create-client-library)
1. [Aggiungere una libreria client in un modulo adattivo](#use-custom-function)

### Creare una libreria client {#create-client-library}

Puoi aggiungere funzioni personalizzate aggiungendo la libreria client. Per creare una libreria client, effettua le seguenti operazioni:

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

   >[!NOTE]
   >
   > Se il file JavaScript contenente il codice per le funzioni personalizzate presenta un errore, le funzioni personalizzate non sono elencate nell’editor di regole di un modulo adattivo. È inoltre possibile controllare `error.log` file per l’errore.

   <!-- 
    >* AEM Adaptive Form supports the caching of custom functions. If the JavaScript is modified, the caching becomes invalidated, and it is parsed. You can see a message as `Fetched following custom functions list from cache` in the `error.log` file.  -->

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

1. [Esegui la pipeline.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline)

Una volta eseguita correttamente la pipeline, la funzione personalizzata aggiunta nella libreria client diventa disponibile nel [Editor di regole per moduli adattivi](/help/forms/rule-editor-core-components.md).

### Aggiungere una libreria client in un modulo adattivo{#use-custom-function}

Dopo aver implementato la libreria client nell’ambiente Forms CS, utilizzane le funzionalità nel modulo adattivo. Per aggiungere la libreria client al modulo adattivo

1. Apri il modulo in modalità di modifica. Per aprire un modulo in modalità di modifica, selezionare un modulo e selezionare **[!UICONTROL Modifica]**.
1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri **[!UICONTROL Base]** e seleziona il nome del **[!UICONTROL categoria libreria client]** dall’elenco a discesa (in questo caso, seleziona `customfunctionscategory`).

   ![Aggiunta della libreria client della funzione personalizzata](/help/forms/assets/clientlib-custom-function.png)

1. Clic **[!UICONTROL Fine]** .

Ora puoi creare una regola per utilizzare funzioni personalizzate nell’editor di regole.

<!--

Create a rule to use custom function in the rule editor. 

### Support for the optional parameters in custom functions{#support-for-optional-parameter}

AEM supports including optional parameters in JSDocs. These parameters are displayed as optional in the rule editor. There are two ways to add optional parameters in JSDocs:
*  `@param {string=abc} b -- some description for b which is optional`

    In the above line of code, `b` is an optional parameter with the default value set to `abc`. 
    Alternatively, you can define `b` as an optional parameter without assigning any default value as `@param {string=} b -- some description for b which is optional`

* `@param {array} [z=[def,xyz]] - - some description for z which is optional`

    In the above line of code, `z` is an optional parameter of array type with the default value set to `[def , xyz]`. 
    Alternatively, you can define `z` as an optional parameter without assigning any default value as `@param {array} [z=] - - some description for z which is optional`

>[!NOTE]
>
> Ensure that the parameter name is enclosed in square brackets [] and the parameter type is enclosed in curly brackets {}. 

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

In the rule editor of an Adaptive Form, the parameters are displayed as `required`. By default the parameters are `required`, if not defined as optional in JSDocs.

  ![Optional or required parameters](/help/forms/assets/optional-default-params.png) 

  You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

  ![incomplete rule warning message](/help/forms/assets/incomplete-rule.png) 
  
  The rule is executed even if you do not specify a value for optional parameters. Undefined values are passed for optional parameters on executing the rule.

  ### Support for field and globals objects in custom functions {#support-field-and-global-objects}

  needs to be discussed

  -->

## Consulta anche {#see-also}

{{see-also}}





