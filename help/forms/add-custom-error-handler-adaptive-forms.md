---
title: Aggiungere gestori di errori personalizzati in Forms adattivo per Forms adattivo AEM
description: AEM Forms fornisce gestori predefiniti di errori e operazioni riuscite per un modulo che utilizza l’endpoint REST configurato per richiamare un servizio esterno. Puoi aggiungere un gestore degli errori predefinito e personalizzato in un modulo adattivo AEM.
keywords: Aggiungi un gestore degli errori personalizzato, aggiungi un gestore degli errori predefinito, aggiungi un gestore degli errori nel modulo, utilizza il servizio invoke dell’editor delle regole per aggiungere un gestore degli errori personalizzato, configura l’editor delle regole per aggiungere un gestore degli errori personalizzato, aggiungi un gestore degli errori personalizzato utilizzando l’editor delle regole
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Foundation Components
exl-id: 198a26a9-d6bb-457d-aab8-0a5d15177c48
role: User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 1%

---

# Aggiungere gestori di errori personalizzati nel Forms adattivo dell’AEM {#error-handlers-in-adaptive-form}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

AEM Forms fornisce gestori predefiniti di successo e di errori per l’invio di moduli. Fornisce inoltre funzionalità per personalizzare le funzioni del gestore degli errori. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel backend per codici di errore specifici o informare il cliente che il servizio non è disponibile. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un servizio esterno viene richiamato utilizzando le API, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull’evento di successo o errore per l’invio. Le informazioni vengono passate come parametri al gestore pertinente per eseguire la funzione. Un gestore degli errori consente di gestire e visualizzare gli errori o i problemi di convalida rilevati.

![flusso di lavoro gestore errori per informazioni su come aggiungere un gestore errori personalizzato nei moduli](/help/forms/assets/error-handler-workflow.png)

Il modulo adattivo convalida gli input forniti nei campi in base a criteri di convalida predefiniti e verifica la presenza di vari errori restituiti dall’endpoint REST configurato per richiamare un servizio esterno. È possibile impostare i criteri di convalida in base all’origine dati utilizzata con il modulo adattivo. Ad esempio, se utilizzi i servizi web RESTful come origine dati, puoi definire i criteri di convalida in un file di definizione Swagger.

Se i valori di input soddisfano i criteri di convalida, vengono inviati all’origine dati, altrimenti nel modulo adattivo viene visualizzato un messaggio di errore tramite un gestore degli errori. Simile a questo approccio, Forms adattivo si integra con gestori di errori personalizzati per eseguire le convalide dei dati. Se i valori di input non soddisfano i criteri di convalida, i messaggi di errore vengono visualizzati a livello di campo nel modulo adattivo. Ciò si verifica quando il messaggio di errore di convalida restituito dal server è nel formato di messaggio standard.


## Utilizzo dei gestori di errori {#uses-of-error-handler}

I gestori di errori vengono utilizzati per vari scopi. Di seguito sono elencati alcuni degli utilizzi delle funzioni di gestione degli errori:
* **Esegui convalida**: la gestione degli errori inizia con la convalida degli input dell&#39;utente in base a regole o criteri predefiniti. Quando gli utenti compilano un modulo adattivo, il gestore degli errori convalida l’input per garantire che soddisfi il formato, la lunghezza o qualsiasi altro vincolo richiesto.

* **Invia feedback in tempo reale**: quando viene rilevato un errore, il gestore degli errori visualizza un feedback immediato all&#39;utente, ad esempio messaggi di errore in linea sotto i campi del modulo corrispondenti. Questo feedback consente agli utenti di identificare e correggere gli errori senza dover inviare il modulo e attendere una risposta.


* **Messaggi di errore visualizzati**: quando un invio di un modulo adattivo rileva un errore di convalida, il gestore degli errori visualizza un messaggio di errore appropriato. I messaggi di errore devono essere chiari, concisi ed evidenziati nei campi specifici che richiedono attenzione.

* **Evidenzia il campo errato**: per attirare l&#39;attenzione dell&#39;utente sui campi errati specifici, il gestore degli errori evidenzia o distingue visivamente i campi corrispondenti. Viene eseguita modificando il colore di sfondo, aggiungendo un&#39;icona o un bordo o qualsiasi altro segnale visivo che consenta agli utenti di individuare e risolvere rapidamente gli errori.


## Formato della risposta di errore/errore {#failure-response-format}

Un modulo adattivo visualizza gli errori a livello di campo se i messaggi di errore di convalida del server sono nel seguente formato standard.
Il codice riportato di seguito illustra la struttura di risposta dei guasti esistente:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


Dove:

* `errorCausedBy` descrive il motivo dell&#39;errore.
* `errors` menziona l&#39;espressione SOM dei campi che non hanno soddisfatto i criteri di convalida insieme al messaggio di errore di convalida.
* Il campo `originCode` aggiunto dall&#39;AEM contiene il codice di stato http restituito dal servizio esterno.
* Il campo `originMessage` è stato aggiunto dall&#39;AEM e contiene i dati di errore non elaborati restituiti dal servizio esterno.

Con i miglioramenti delle funzioni e i successivi aggiornamenti delle versioni di AEM Forms, la struttura di risposta dei guasti esistente è stata modificata in un nuovo formato basato su RFC7807, compatibile con le versioni precedenti della struttura di risposta dei guasti esistente:

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<SOM expression of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * Verificare che la struttura della risposta di errore includa **fieldName** o **dataRef**.
> * Assicurati che l&#39;intestazione **ContentType** sia **application/problem+json**.

Dove:
* `type (required)` specifica il tipo di errore. Può corrispondere a uno dei seguenti valori:
   * `SERVER_SIDE_VALIDATION` indica un errore dovuto alla convalida lato server.
   * `FORM_SUBMISSION` indica un errore durante l&#39;invio del modulo
   * `SERVICE_INVOCATION` indica un errore durante una chiamata di un servizio di terze parti.
   * `FAILURE` indica un errore generale.
   * `VALIDATION_ERROR` indica un errore a causa di un errore di convalida.

* `title (optional)` fornisce un titolo o una breve descrizione dell&#39;errore.
* `detail (optional)` fornisce ulteriori dettagli sull&#39;errore, se necessario.
* `instance (optional)` rappresenta un&#39;istanza o un identificatore associato all&#39;errore e consente di tenere traccia o identificare l&#39;occorrenza specifica dell&#39;errore.
* `validationErrors (required)` contiene informazioni sugli errori di convalida. Include i campi seguenti:
   * `fieldname` fa riferimento all&#39;espressione SOM dei campi che non hanno soddisfatto i criteri di convalida.
   * `dataRef` rappresenta il percorso JSON o XPath dei campi che non hanno superato la convalida.
   * `details` contengono il messaggio di errore di convalida con il campo errato.
* Campo `originCode (optional)` aggiunto dall&#39;AEM e contenente il codice di stato http restituito dal servizio esterno
* Il campo `originMessage (optional)` è stato aggiunto dall&#39;AEM e contiene i dati di errore non elaborati restituiti dal servizio esterno.

### Formato risposta errore di esempio {#sample-error-response-format}

Alcune delle opzioni per visualizzare le risposte di errore sono:

+++  In base alla proprietà fieldName del modulo adattivo


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "guide[0].guide1[0].guideRootPanel[0].textbox1686647736683[0]",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```

  Per visualizzare l&#39;espressione SOM di qualsiasi campo in un modulo adattivo, tocca il campo e seleziona **[!UICONTROL Visualizza espressione SOM]**.

  ![Espressione personalizzata di un campo modulo adattivo per visualizzare la risposta di errore nel gestore errori personalizzato](/help/forms/assets/custom-error-handler-somexpression.png)

+++


+++ In base alla proprietà dataRef del modulo adattivo

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "/Pet/id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

  ![Riferimento dati di un campo modulo adattivo per visualizzare la risposta di errore nel gestore errori personalizzato](/help/forms/assets/custom-errorhandler-dataref.png)

Puoi visualizzare il valore di dataRef nella finestra **[!UICONTROL Proprietà]** di un componente modulo.

+++


## Aggiungi gestore errori tramite l’Editor regole {#add-error-handler-using-rule-editor}

Utilizzando l&#39;azione Invoke Service[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=it#invoke) dell&#39;editor di regole , puoi definire i criteri di convalida in base all&#39;origine dati utilizzata con il modulo adattivo. Se si utilizzano i servizi Web RESTful come origine dati, è possibile definire i criteri di convalida in un file di definizione Swagger. Utilizzando le funzioni di gestore degli errori e l’editor di regole in Adaptive Forms, puoi gestire e personalizzare in modo efficace la gestione degli errori. Definisci le condizioni utilizzando l’Editor regole e configura le azioni da eseguire quando la regola viene attivata. Il modulo adattivo convalida gli input immessi nei campi in base a criteri di convalida predefiniti. Se i valori di input non soddisfano i criteri di convalida, i messaggi di errore vengono visualizzati a livello di campo in un modulo adattivo.

>[!NOTE]
>
> * Per utilizzare i gestori di errori con l’azione Richiama servizio dell’Editor regole, configura Forms adattivo con un modello dati del modulo (FDM).
> * Se la risposta di errore si trova nello schema standard, viene fornito un gestore degli errori predefinito per visualizzare i messaggi di errore sui campi. È inoltre possibile chiamare il gestore degli errori predefinito dalla funzione del gestore degli errori personalizzato.

Utilizzando l’editor di regole, puoi:
* [Aggiungi funzione gestore errori predefinita](#add-default-errror-handler)
* [Aggiungi funzione di gestione degli errori personalizzata](#add-custom-error-handler-function)


### Aggiungi funzione gestore errori predefinita {#add-default-errror-handler}

È supportato un gestore degli errori predefinito per visualizzare i messaggi di errore sui campi se la risposta di errore si trova nello schema standard o in un errore di convalida lato server.
Per informazioni su come utilizzare un gestore di errori predefinito utilizzando l&#39;azione Richiama servizio[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=it#invoke) dell&#39;editor di regole, utilizzare un modulo adattivo semplice con due campi, **ID animale domestico** e **Nome animale** e utilizzare un gestore di errori predefinito nel campo **ID animale** per verificare la presenza di vari errori restituiti dall&#39;endpoint REST configurato per richiamare un servizio esterno, ad esempio `200 - OK`,`404 - Not Found`, `400 - Bad Request`.  Per aggiungere un gestore degli errori predefinito tramite l’azione Richiama servizio dell’editor di regole, esegui i passaggi seguenti:

1. Apri un modulo adattivo in modalità di creazione, seleziona un componente modulo e seleziona **[!UICONTROL Editor regole]** per aprire l&#39;editor regole.
1. Seleziona **[!UICONTROL Crea]**.
1. Crea una condizione nella sezione **When** della regola. Ad esempio, **Quando[il nome del campo ID animale domestico]** viene modificato. Selezione modificata dall&#39;elenco a discesa **Seleziona stato**.
1. Nella sezione **Then**, seleziona **[!UICONTROL Richiama servizio]** dall&#39;elenco a discesa **Seleziona azione**.
1. Seleziona un **Servizio post** e le associazioni dati corrispondenti dalla sezione **Input**. Ad esempio, per convalidare **ID animale**, selezionare un **servizio post** come **GET/animale domestico/{petId}** e selezionare **ID animale** nella sezione **Input**.
1. Selezionare le associazioni dati dalla sezione **Output**. Seleziona **Nome animale** nella sezione **Output**.
1. Seleziona **[!UICONTROL Gestore errori predefinito]** dalla sezione **Gestore errori**.
1. Fai clic su **[!UICONTROL Fine]**.

![aggiungere un gestore errori predefinito per i controlli di convalida dei campi in un modulo](/help/forms/assets/default-error-handler.png)

Come risultato di questa regola, i valori immessi per **ID animale** controllano la convalida per **Nome animale** utilizzando il servizio esterno richiamato dall&#39;endpoint REST. Se i criteri di convalida basati sull’origine dati non riescono, i messaggi di errore vengono visualizzati a livello di campo.

![visualizza il messaggio di errore predefinito quando aggiungi un gestore degli errori predefinito in un modulo per gestire le risposte agli errori](/help/forms/assets/default-error-message.png)

### Aggiungi funzione di gestione degli errori personalizzata

È possibile aggiungere una funzione di gestione degli errori personalizzata per eseguire alcune delle azioni seguenti:

* gestisce le risposte di errore che utilizzano risposte di errore non standard o standard. È importante notare che queste risposte di errore non standard non sono conformi allo schema [standard di risposte di errore](#failure-response-format).
* invia eventi di analytics a qualsiasi piattaforma di analytics. Ad esempio, Adobe Analytics.
* visualizza la finestra di dialogo modale con messaggi di errore.

Oltre alle azioni citate, i gestori degli errori personalizzati possono essere utilizzati per eseguire funzioni personalizzate che soddisfano requisiti utente specifici.

Il gestore degli errori personalizzati è una funzione (libreria client) progettata per rispondere agli errori restituiti da un servizio esterno e fornire una risposta personalizzata agli utenti finali. Qualsiasi libreria client con annotazione `@errorHandler` è considerata una funzione di gestore degli errori personalizzata. Questa annotazione consente di identificare la funzione di gestione degli errori specificata nel file `.js`.
Per capire come creare e utilizzare un gestore di errori personalizzato utilizzando l&#39;azione Richiama servizio[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=it#invoke) dell&#39;editor di regole, prendiamo ad esempio il modulo adattivo con due campi, **ID animale domestico** e **Nome animale**, e utilizziamo un gestore di errori personalizzato nel campo **ID animale** per verificare la presenza di vari errori restituiti dall&#39;endpoint REST configurato per richiamare un servizio esterno, ad esempio `200 - OK`,`404 - Not Found`, `400 - Bad Request`.

Per aggiungere e utilizzare un gestore di errori personalizzato in un modulo adattivo, effettua le seguenti operazioni:
1. [Aggiungi funzione personalizzata per gestore errori](#1-add-the-custom-function-for-the-error-handler)
2. [Utilizza l’Editor regole per configurare un gestore degli errori personalizzato](#use-custom-error-handler)

#### 1. Aggiungi la funzione personalizzata per il gestore degli errori

Per informazioni su come aggiungere funzioni personalizzate, fai clic su [Crea funzioni personalizzate in un modulo adattivo basato su componenti core](/help/forms/custom-function-core-component-create-function.md#create-a-custom-function).

<!-- To create a custom error function, perform the following steps:

1. [Clone your AEM Forms as a Cloud Service Repository](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=it#accessing-git). 
2. Create a folder under the `[AEM Forms as a Cloud Service repository folder]/apps/` folder. For example, create a folder named as `experience-league`
3. Navigate to `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` and create a `ClientLibraryFolder` as `clientlibs`.
4. Create a folder named `js`.
5. Navigate to the `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` folder. -->

1. Aggiungere il codice seguente per il gestore degli errori personalizzato nel file JavaScript, ad esempio `function.js`. Il file contiene il codice per il gestore degli errori personalizzato.
Aggiungiamo il seguente codice al file JavaScript per visualizzare la risposta e le intestazioni, ricevute dall’endpoint del servizio REST, nella console del browser.

   ```javascript
       /**
       * Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers)
       {
           console.log("Custom Error Handler processing start...");
           console.log("response:"+JSON.stringify(response));
           console.log("headers:"+JSON.stringify(headers));
           guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers);
           console.log("Custom Error Handler processing end...");
       }
   ```

   >[!NOTE]
   >
   > * Per chiamare il gestore errori predefinito dal gestore errori personalizzato, viene utilizzata la seguente riga del codice di esempio: `guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers) `
   > * Nel file `.content.xml`, aggiungi le proprietà `allowProxy` e `categories` per utilizzare la libreria client del gestore degli errori personalizzata in un modulo adattivo.
   >
   >   * `allowProxy = [Boolean]true`
   >   * `categories= customfunctionsdemo`
   >       Ad esempio, in questo caso, [custom-errorhandler-name] viene fornito come `customfunctionsdemo`.


1. Aggiungi, esegui il commit e invia le modifiche nell’archivio.

<!--

<!--
1. Save the `function.js` file.
1. Navigate to the `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` folder.
2. Add a text file as `js.txt`. The file contains:

    ```javascript
        #base=js
        functions.js
    ```

3. Save the `js.txt` file.    
The created folder structure looks like:

    ![Created Client Library Folder Structure](/help/forms/assets/customclientlibrary_folderstructure.png) 
    using the below commands:
         
    ```javascript

        git add .
        git commit -a -m "Adding error handling files"
        git push
    ```
-->

1. [Eseguire la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=it#setup-pipeline).

Una volta eseguita correttamente la pipeline, il gestore degli errori personalizzato diventa disponibile nell’editor di regole del modulo adattivo. Ora vediamo come configurare e utilizzare un gestore di errori personalizzato utilizzando il servizio Invoke dell’editor di regole in AEM Forms.

#### 2. Utilizza l’Editor regole per configurare un gestore degli errori personalizzato {#use-custom-error-handler}

Prima di implementare il gestore di errori personalizzato in un modulo adattivo, accertati che il nome della libreria client nella **[!UICONTROL Categoria libreria client]** sia allineato al nome specificato nell&#39;opzione delle categorie del file `.content.xml`.

![Aggiunta del nome della libreria client nella configurazione del contenitore di moduli adattivi](/help/forms/assets/client-library-category-name.png)

In questo caso, il nome della libreria client viene fornito come `customfunctionsdemo` nel file `.content.xml`.

Per utilizzare un gestore degli errori personalizzato utilizzando l&#39;azione Richiama servizio **dell&#39;editor di regole:**

1. Apri un modulo adattivo in modalità di creazione, seleziona un componente modulo e seleziona **[!UICONTROL Editor regole]** per aprire l&#39;editor regole.
1. Seleziona **[!UICONTROL Crea]**.
1. Crea una condizione nella sezione **When** della regola. Ad esempio, quando **[il nome del campo ID animale domestico]** viene modificato, selezionare **è cambiato** dall&#39;elenco a discesa **Seleziona stato**.
1. Nella sezione **Then**, seleziona **[!UICONTROL Richiama servizio]** dall&#39;elenco a discesa **Seleziona azione**.
1. Seleziona un **Servizio post** e le associazioni dati corrispondenti dalla sezione **Input**. Ad esempio, per convalidare **ID animale**, selezionare un **servizio post** come **GET/animale domestico/{petId}** e selezionare **ID animale** nella sezione **Input**.
1. Selezionare le associazioni dati dalla sezione **Output**. Selezionare ad esempio **Nome animale** nella sezione **Output**.
1. Seleziona **[!UICONTROL Gestore errori personalizzato]** dalla sezione **[!UICONTROL Gestore errori]**.
1. Fai clic su **[!UICONTROL Fine]**.

![aggiungi un gestore degli errori personalizzato in un modulo per gestire le risposte di errore](/help/forms/assets/custom-error-handler.png)

Come risultato di questa regola, i valori immessi per **ID animale** controllano la convalida per **Nome animale** utilizzando il servizio esterno richiamato dall&#39;endpoint REST. Se i criteri di convalida basati sull’origine dati non riescono, i messaggi di errore vengono visualizzati a livello di campo.

![aggiungi un gestore degli errori personalizzato in un modulo per gestire le risposte agli errori](/help/forms/assets/custom-error-handler-message.png)

Apri la console del browser e controlla la risposta e l’intestazione, ricevute dall’endpoint del servizio REST, per il messaggio di errore di convalida.


La funzione del gestore degli errori personalizzato è responsabile dell’esecuzione di azioni aggiuntive, ad esempio la visualizzazione di una finestra di dialogo modale o l’invio di un evento di analisi, in base alla risposta all’errore. Una funzione di gestione degli errori personalizzata offre la flessibilità necessaria per adattare la gestione degli errori ai requisiti utente specifici.

<!-- 

## Configure Adaptive Form submission to add custom handlers {#configure-adaptive-form-submission}

If the server validation error message does not display in the standard format, you can enable asynchronous submission and add a custom error handler on Adaptive Form submission to convert the message into a standard format.

### Configure asynchronous Adaptive Form submission {#configure-asynchronous-adaptive-form-submission}

Before adding custom handler, you must configure the adaptive form for asynchronous submission. Execute the following steps:

1. In adaptive form authoring mode, select the Form Container object and select ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model (FDM)]** and select the appropriate data model, if you are using RESTful web service based [form data model (FDM)](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST Service endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Select ![Save](assets/save_icon.png) to save the properties.

### Add custom error handler on Adaptive Form submission {#add-custom-error-handler-af-submission}

AEM Forms provides out-of-the-box success and error handlers for form submissions. Handlers are client-side functions that execute based on the server response. When an Adaptive Form is submitted, the data is transmitted to the server for validation, which returns a response to the client with information about the success or error event for the submission. The information is passed as parameters to the relevant handler to execute the function.

Execute the following steps to add custom error handler on Adaptive Form submission:

1. Open an Adaptive Form in authoring mode, select any form object, and select  to open the rule editor.
1. Select **[!UICONTROL Form]** in the Form Objects tree and select **[!UICONTROL Create]**.
1. Select **[!UICONTROL Error in Submission]** from the Event drop-down list.
1. Write a rule to convert custom error structure to the standard error structure and select **[!UICONTROL Done]** to save the rule.

The following is a sample code to convert a custom error structure to the standard error structure:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys (errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

The `var som_map` lists the SOM expression of the Adaptive Form fields that you want to transform into the standard format. You can view the SOM expression of any field in an adaptive form by tapping the field and selecting **[!UICONTROL View SOM Expression]**.

Using this custom error handler, the adaptive form converts the fields listed in `var som_map` to standard error message format. As a result, the validation error messages display at field-level in the adaptive form.

 -->


## Consulta anche {#see-also}

{{see-also}}
* [Creare e utilizzare gestori di errori personalizzati in Adaptive Forms (Componenti core)](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)

<!--

>[!MORELIKETHIS]
>
>* [Create style or themes for your forms](/help/forms/using-themes-in-core-components.md)
>* [Create or add an Adaptive Form to AEM Sites page](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

-->
