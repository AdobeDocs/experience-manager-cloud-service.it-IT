---
title: Questo articolo illustra vari casi d’uso per una funzione personalizzata in un modulo adattivo basato su componenti core.
description: L’articolo delinea vari casi d’uso per una funzione personalizzata in un modulo adattivo basato su componenti core. Le funzioni personalizzate vengono utilizzate nell’editor di regole per creare regole personalizzate per il modulo.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: df92b91e-f3b0-4a08-bd40-e99edc9a50a5
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 0%

---

# Esempi di sviluppo e utilizzo di funzioni personalizzate

L’articolo fornisce esempi dettagliati di funzioni personalizzate per un modulo adattivo basato su componenti core, fornendo informazioni utili sulla loro effettiva implementazione in vari scenari. Le funzioni personalizzate vengono utilizzate nell’editor di regole di un’AEM Forms, consentendo agli sviluppatori di definire e controllare la logica che regola il comportamento dei moduli.
Questo articolo esplora diverse implementazioni di funzioni personalizzate, mostrando come possono essere utilizzate per adattare i moduli in modo da soddisfare requisiti specifici e migliorare le funzionalità generali.

## Popolare le opzioni dell’elenco a discesa utilizzando le funzioni personalizzate

L&#39;editor di regole nei componenti core non supporta la proprietà **Imposta opzioni** per popolare dinamicamente le opzioni dell&#39;elenco a discesa in fase di esecuzione. Tuttavia, puoi popolare le opzioni dell’elenco a discesa utilizzando funzioni personalizzate, che ti consentono di recuperare le opzioni in base a una logica specifica. Le funzioni personalizzate forniscono maggiore flessibilità e controllo su come e quando vengono compilate le opzioni a discesa, migliorando l’esperienza utente.

Per popolare le opzioni dell&#39;elenco a discesa utilizzando una funzione personalizzata, aggiungere il codice seguente come descritto nella sezione [create-custom-function](/help/forms/custom-function-core-component-create-function.md):


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

## Mostra un pannello utilizzando la regola `SetProperty`

Scopri in che modo le funzioni personalizzate utilizzano gli oggetti campo e globali con l&#39;aiuto di un modulo `Contact Us`.

![Modulo per contattarci](/help/forms/assets/contact-us-form.png)

Aggiungere il codice seguente nella funzione personalizzata come descritto nella sezione [create-custom-function](/help/forms/custom-function-core-component-create-function.md) per impostare il campo modulo come `Required`.

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

## Convalida il campo

Scopri in che modo le funzioni personalizzate utilizzano gli oggetti campo e globali per convalidare il campo con l&#39;aiuto di un modulo `Contact Us`.

Aggiungi il seguente codice nella funzione personalizzata come descritto nella sezione [create-custom-function](/help/forms/custom-function-core-component-create-function.md) per convalidare il campo.

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

## Reimpostare un pannello

Scopri in che modo le funzioni personalizzate utilizzano gli oggetti campo e globali per reimpostare il campo con l&#39;aiuto di un modulo `Contact Us`.

Aggiungi il seguente codice nella funzione personalizzata, come descritto nella sezione [create-custom-function](/help/forms/custom-function-core-component-create-function.md), per ripristinare il pannello.

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

## Per visualizzare un messaggio personalizzato a livello di campo e contrassegnare il campo come non valido

Scopri in che modo le funzioni personalizzate utilizzano gli oggetti campo e globali per visualizzare un messaggio personalizzato a livello di campo e contrassegnare il campo come non valido con l’aiuto di un modulo `Contact Us`.

È possibile utilizzare la funzione `markFieldAsInvalid()` per definire un campo come non valido e impostare un messaggio di errore personalizzato a livello di campo. Il valore `fieldIdentifier` può essere `fieldId`, `field qualifiedName` o `field dataRef`. Il valore dell&#39;oggetto denominato `option` può essere `{useId: true}`, `{useQualifiedName: true}` o `{useDataRef: true}`.
Le sintassi utilizzate per contrassegnare un campo come non valido e impostare un messaggio personalizzato sono:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Aggiungi il seguente codice nella funzione personalizzata, come descritto nella sezione [create-custom-function](/help/forms/custom-function-core-component-create-function.md), per abilitare un messaggio personalizzato a livello di campo.

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

## Invia dati modificati al server

Scopri in che modo le funzioni personalizzate utilizzano oggetti campo e globali per inviare dati manipolati sul server con l&#39;aiuto di un modulo `Contact Us`.

La seguente riga di codice:
`globals.functions.submitForm(globals.functions.exportData(), false);` viene utilizzato per inviare i dati del modulo dopo la manipolazione.

* Il primo argomento è costituito dai dati da inviare.
* Il secondo argomento indica se il modulo deve essere convalidato prima dell&#39;invio. È `optional` ed è impostato come `true` per impostazione predefinita.
* Il terzo argomento è `contentType` dell&#39;inoltro, che è anche facoltativo con il valore predefinito `multipart/form-data`. Gli altri valori possono essere `application/json` e `application/x-www-form-urlencoded`.

Aggiungi il seguente codice nella funzione personalizzata, come descritto nella sezione [create-custom-function](/help/forms/custom-function-core-component-create-function.md), per inviare i dati manipolati sul server:

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

![Verifica i dati nella finestra della console](/help/forms/assets/custom-function-submit-data-console-data.png)

## Ignora gestori di errori e operazioni riuscite per l’invio del modulo

Scopri in che modo le funzioni personalizzate utilizzano gli oggetti campo e globali per sostituire i gestori di invio con l&#39;aiuto di un modulo `Contact Us`.

Aggiungi la seguente riga di codice come descritto nella sezione [create-custom-functionas](/help/forms/custom-function-core-component-create-function.md) per personalizzare l&#39;invio o il messaggio di errore per l&#39;invio dei moduli e visualizzare i messaggi di invio dei moduli in una casella modale:

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

Nel caso in cui il gestore di invio personalizzato non riesca a eseguire le operazioni previste nei moduli o nei progetti AEM esistenti, consulta la sezione [risoluzione dei problemi](#troubleshooting).

## Eseguire azioni in un&#39;istanza specifica del pannello ripetibile

Le regole create utilizzando l’editor di regole visive in un pannello ripetibile si applicano all’ultima istanza del pannello ripetibile. Per scrivere una regola per una specifica istanza del pannello ripetibile, possiamo utilizzare una funzione personalizzata.

Creiamo un altro modulo come `Booking Form` per raccogliere informazioni sui viaggiatori che si dirigono verso una destinazione. Un pannello viaggiatore viene aggiunto come pannello ripetibile, in cui l&#39;utente può aggiungere dettagli per 5 viaggiatori utilizzando il pulsante `Add Traveler`.

![Informazioni viaggiatore](/help/forms/assets/traveler-info-form.png)

Aggiungi la seguente riga di codice come descritto nella sezione [create-custom-function](/help/forms/custom-function-core-component-create-function.md) per eseguire azioni in un&#39;istanza specifica del pannello ripetibile, diversa dall&#39;ultima:

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

## Precompila il campo con un valore al caricamento del modulo

Scopri in che modo le funzioni personalizzate utilizzano gli oggetti campo e globali per precompilare il campo con l&#39;aiuto di `Booking Form`.

Aggiungi la seguente riga di codice, come spiegato nella sezione [create-custom-function](/help/forms/custom-function-core-component-create-function.md), per caricare il valore precompilato in un campo quando il modulo viene inizializzato:

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

## Imposta lo stato attivo sul campo specifico

Scopri in che modo le funzioni personalizzate utilizzano gli oggetti campo e globali per impostare lo stato attivo su un campo specifico con l&#39;aiuto di `Booking Form`.

Aggiungere la seguente riga di codice, come spiegato nella sezione [create-custom-function](/help/forms/custom-function-core-component-create-function.md), per attivare il campo specificato quando si fa clic sul pulsante `Submit`.:

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

## Aggiungere o eliminare un pannello ripetibile utilizzando la proprietà `dispatchEvent`

Scopri in che modo le funzioni personalizzate utilizzano gli oggetti field e global per aggiungere o eliminare un pannello ripetibile utilizzando la proprietà `dispatchEvent` con l&#39;aiuto di un `Booking Form`.

Aggiungi la seguente riga di codice, come spiegato nella sezione [create-custom-function](/help/forms/custom-function-core-component-create-function.md), per aggiungere un pannello quando fai clic sul pulsante `Add Traveler` utilizzando la proprietà `dispatchEvent`:

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

## Problema noto

* Le funzioni personalizzate non supportano i valori letterali delle espressioni regolari di JavaScript. L’utilizzo di valori letterali regex in una funzione personalizzata genera errori durante l’esecuzione. Ad esempio:
  `const pattern = /^abc$/;`

  Per garantire la compatibilità, utilizza il costruttore RegExp nelle funzioni personalizzate.

  `const pattern = new RegExp("^abc$");`
Effettua il refactoring delle espressioni regolari per utilizzare il costruttore RegExp per garantire un’esecuzione coerente e affidabile.

## Risoluzione di problemi

* Se il gestore di invio personalizzato non funziona come previsto nei progetti o moduli AEM esistenti, effettua le seguenti operazioni:
   * Verificare che la versione dei componenti core [sia aggiornata a 3.0.18 e versioni successive](https://github.com/adobe/aem-core-forms-components). Tuttavia, per i progetti e i moduli AEM esistenti, sono disponibili ulteriori passaggi da seguire:

   * Per il progetto AEM, l&#39;utente deve sostituire tutte le istanze di `submitForm('custom:submitSuccess', 'custom:submitError')` con `submitForm()` e distribuire il progetto tramite la pipeline Cloud Manager.

   * Per i moduli esistenti, se i gestori di invio personalizzati non funzionano correttamente, l&#39;utente deve aprire e salvare la regola `submitForm` sul pulsante **Invia** utilizzando l&#39;editor di regole. Questa azione sostituisce la regola esistente di `submitForm('custom:submitSuccess', 'custom:submitError')` con `submitForm()` nel modulo.

## Consulta anche

{{see-also-rule-editor}}
