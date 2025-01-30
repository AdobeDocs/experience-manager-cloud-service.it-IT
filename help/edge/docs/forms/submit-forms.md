---
title: Preparare il foglio di calcolo per accettare i dati
description: Creare moduli potenti più rapidamente utilizzando fogli di calcolo e campi blocco di moduli adattivi.
feature: Edge Delivery Services
exl-id: 0643aee5-3a7f-449f-b086-ed637ae53b5a
role: Admin, Architect, Developer
source-git-commit: 552779d9d1cee2ae9f233cabc2405eb6416c41bc
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 97%

---

# Impostare i Fogli Google o i file Microsoft Excel per iniziare ad accettare i dati


Una volta che hai [creato e visualizzato in anteprima il modulo](/help/edge/docs/forms/create-forms.md), è il momento di abilitare il foglio di calcolo corrispondente per iniziare a ricevere i dati. È possibile

* [Abilitare manualmente il foglio di calcolo per accettare i dati](#manually-enable-the-spreadsheet-to-accept-data)
* [Utilizza le API di amministrazione per abilitare un foglio di calcolo ad accettare i dati](#use-admin-apis-to-enable-a-spreadsheet-to-accept-data)

![Ecosistema di authoring basato sul documento](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)


<!--

>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->

## Abilitare manualmente il foglio di calcolo per accettare i dati

Per abilitare il foglio di calcolo ad accettare i dati,

1. Apri il foglio di calcolo contenente il modulo e aggiungi un nuovo foglio, rinominandolo `incoming`. Ad esempio, il modulo di [interrogazione](/help/edge/assets/enquiry.xlsx) della cartella di lavoro Microsoft Excel.

   >[!WARNING]
   >
   > Se il foglio `incoming` non è presente, AEM non invia alcun dato al foglio di calcolo.

1. In questo foglio inserisci una tabella denominata “intake_form”. Seleziona il numero di colonne necessarie per far corrispondere i nomi dei campi modulo. Poi, nella barra degli strumenti, vai su Inserisci > Tabella e fai clic su OK.

1. Modifica il nome della tabella in “intake_form”. In Microsoft Excel, per modificare il nome della tabella, selezionala e fai clic su Progettazione tabella.

1. Successivamente, aggiungi i nomi dei campi modulo come intestazioni della tabella. Per verificare che i campi siano esattamente gli stessi, puoi copiarli e incollarli dal foglio “shared-aem”.  Nel foglio “shared-aem” seleziona e copia gli ID modulo elencati nella colonna “Nome”, ad eccezione del campo Invia.

1. Nel foglio “in entrata”, seleziona Incolla speciale > Trasponi righe in colonne per copiare gli ID dei campi come intestazioni di colonna in questo nuovo foglio. Conserva solo i campi di cui è necessario acquisire i dati, gli altri possono essere ignorati.

   Ogni valore nella colonna `Name` del foglio `shared-aem`, escluso il pulsante Invia, può essere utilizzato come intestazione nel foglio `incoming`. Ad esempio, prendi in considerazione l’immagine seguente che illustra le intestazioni per un modulo di “interrogazione”:

   ![Campi per un modulo contattaci](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. Utilizza l’estensione [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima gli aggiornamenti del modulo. Il foglio è ora pronto per accettare gli invii dei moduli in entrata.

   >[!NOTE]
   >
   >Anche se hai già visualizzato l’anteprima del foglio, devi visualizzarla nuovamente dopo aver creato il foglio `incoming` per la prima volta.


Una volta aggiunti i nomi dei campi al foglio `incoming`, il modulo diventa pronto per accettare gli invii. Puoi visualizzare in anteprima il modulo e, tramite questo, inviare i dati al foglio.

Una volta configurato il foglio per la ricezione dei dati, puoi [visualizzare in anteprima il modulo](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) <!--or [use POST requests](#use-admin-apis-to-send-data-to-your-sheet)--> o iniziare a inviare i dati al foglio.

>[!WARNING]
>
>  I fogli “shared-aem” non devono mai contenere informazioni personali identificabili o dati sensibili che l’utente non intende rendere accessibili pubblicamente.


## Utilizza le API di amministrazione per abilitare un foglio di calcolo ad accettare i dati

Puoi inoltre inviare una richiesta POST al modulo per abilitarlo ad accettare dati e per configurare le intestazioni per il foglio `incoming`. Dopo aver ricevuto la richiesta POST, il servizio analizza il corpo della richiesta e genera in modo autonomo le intestazioni e i fogli essenziali, necessari per l’acquisizione dei dati.

Per utilizzare le API di amministrazione per abilitare un foglio di calcolo ad accettare i dati:


1. apri la cartella di lavoro creata e cambia il nome del foglio predefinito in `incoming`.

   >[!WARNING]
   >
   > Se il foglio `incoming` non esiste, AEM non invierà alcun dato alla cartella di lavoro.

1. Visualizza l’anteprima del foglio nella barra laterale.

   >[!NOTE]
   >
   >Anche se hai già visualizzato l’anteprima del foglio, devi visualizzarla nuovamente dopo aver creato il foglio `incoming` per la prima volta.

1. Invia la richiesta POST per generare le intestazioni appropriate nel foglio `incoming` e aggiungi i fogli `shared-default` nel foglio di calcolo, se questo non esiste già.

   Per informazioni su come formattare la richiesta POST per la configurazione del foglio, consulta [Documentazione API di amministrazione](https://www.aem.live/docs/admin.html?lang=it#tag/authentication/operation/profile). Osserva l’esempio fornito di seguito:

   **Richiesta**

   ```JSON
   POST 'https://admin.aem.page/form/{owner}/{repo}/{branch}/contact-us.json' \
   --header 'Content-Type: application/json' \
   --data '{
       "data": {
           "Email": "john@wknd.com",
           "Name": "John",
           "Subject": "Regarding Product Inquiry",
           "Message": "I have some questions about your products.",
           "Phone": "123-456-7890",
           "Company": "Adobe Inc.",
           "Country": "United States",
           "PreferredContactMethod": "Email",
           "SubscribeToNewsletter": true
       }
   }'
   ```


   **Risposta**

   ```JSON
   HTTP/2 200 
   content-type: application/json
   x-invocation-id: 1b3bd30a-8cfb-4f85-a662-4b1f7cf367c5
   cache-control: no-store, private, must-revalidate
   accept-ranges: bytes
   date: Sat, 10 Feb 2024 09:26:48 GMT
   via: 1.1 varnish
   x-served-by: cache-del21736-DEL
   x-cache: MISS
   x-cache-hits: 0
   x-timer: S1707557205.094883,VS0,VE3799
   strict-transport-security: max-age=31557600
   content-length: 138
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country",      "PreferredContactMethod","SubscribeToNewsletter"]}%
   ```

   Puoi utilizzare strumenti come curl o Postman per eseguire questa richiesta POST, come dimostrato di seguito:

   ```JSON
   curl -s -i -X POST 'https://admin.aem.page/form/wkndform/wefinance/main/contact-us.json' \
       --header 'Content-Type: application/json' \
       --data '{
           "data": {
               "Email": "john@wknd.com",
               "Name": "John",
               "Subject": "Regarding Product Inquiry",
               "Message": "I have some questions about your products.",
               "Phone": "123-456-7890",
               "Company": "Wknd Inc.",
               "Country": "United States",
               "PreferredContactMethod": "Email",
               "SubscribeToNewsletter": true
       }
   }'
   ```

   la richiesta POST di cui sopra fornisce dati di esempio, inclusi i campi modulo e i rispettivi valori di esempio. Questi dati vengono utilizzati dal servizio di amministrazione per configurare il modulo.

   Il modulo è ora abilitato per l’accettazione dei dati. Nel foglio di calcolo puoi inoltre osservare le seguenti modifiche:

## Il foglio viene modificato automaticamente dopo che è stato abilitato per accettare i dati.

Una volta che il foglio è impostato per ricevere i dati, nel foglio di calcolo si osservano le seguenti modifiche:

Un foglio denominato “Slack” viene aggiunto alla cartella di lavoro di Excel o al foglio di Google. In questo foglio puoi configurare le notifiche automatiche per un canale di Slack designato ogni volta che dei nuovi dati vengono acquisiti nel foglio di calcolo. Attualmente, AEM supporta le notifiche esclusivamente all&#39;organizzazione dello Slack di progettazione AEM e all’organizzazione di supporto aziendale Adobe.

1. Per impostare le notifiche di Slack, immetti il “teamId” dell’area di lavoro di Slack e il “nome del canale” o l’“ID”. Puoi anche chiedere al bot di Slack (con il comando di debug) il “teamId” e l’“ID canale”. È preferibile utilizzare “ID canale” invece di “nome canale”, in quanto non è influenzato dalle ridenominazioni del canale.

   >[!NOTE]
   >
   > I moduli più vecchi non avevano la colonna “teamId”. Il “teamId” era incluso nella colonna del canale, separato da “#” o “/”.

1. Immetti il titolo desiderato e in campi immetti i nomi dei campi da visualizzare nella notifica di Slack. Ogni intestazione deve essere separata da una virgola (ad esempio nome, e-mail).

   >[!WARNING]
   >
   >  I fogli “shared-default” non devono mai contenere informazioni personali identificabili o dati sensibili che l’utente non intende rendere accessibili pubblicamente.



<!--
## Send data to your sheet {#send-data-to-your-sheet}

After the sheet is set to receive data, you can [preview the form using Adaptive Forms Block](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) or [use Admin APIs](#use-admin-apis-to-send-data-to-your-sheet) to start sending data to the sheet.

### Use Admin APIs to send data to your sheet

You can send POST requests directly to your form using aem.page, aem.live, or your production domain, to send data. 


```JSON

POST https://branch–repo–owner.aem.(page|live)/email-form
POST https://my-domain.com/email-form

```

>[!NOTE] 
>
> The URL should not have the .json extension. You must publish the sheet for POST operations to function on `.live` or on the production domain.

#### Formatting the form data

There are a few different ways that you can format the form data in the POST body. You can use: 

* array of `name:value` pairs: 
    
    ```JSON
    
    {
      "data": [
        { "name": "name", "value": "Clark Kent" },
        { "name": "email", "value": "superman@example.com" },
        { "name": "subject", "value": "Regarding Product Inquiry" },
        { "name": "message", "value": "I have some questions about your products." },
        { "name": "phone", "value": "123-456-7890" },
        { "name": "company", "value": "Example Inc." },
        { "name": "country", "value": "United States" },
        { "name": "preferred_contact_method", "value": "Email" },
        { "name": "newsletter_subscribe", "value": true }
      ]
    }

    ```

    For example

    ```JSON

    curl -s -i -X POST 'https://main--wefinance--wkndform.aem.page/contact-us' \
        --header 'Content-Type: application/json' \
        --data '{
        "data": [
            { "name": "name", "value": "Clark Kent" },
            { "name": "email", "value": "superman@example.com" },
            { "name": "subject", "value": "Regarding Product Inquiry" },
            { "name": "message", "value": "I have some questions about your        products." },
            { "name": "phone", "value": "123-456-7890" },
            { "name": "company", "value": "Example Inc." },
            { "name": "country", "value": "United States" },
            { "name": "preferred_contact_method", "value": "Email" },
            { "name": "newsletter_subscribe", "value": true }
        ]
    }'

    ```



* an object with `key:value` pairs:

    ```JSON

        {
          "data": {
            "name": "Jessica Jones",
            "email": "jj@example.com",
            "subject": "Regarding Product Inquiry",
            "message": "I have some questions about your products.",
            "phone": "123-456-7890",
            "company": "Example Inc.",
            "country": "United States",
            "preferred_contact_method": "Email",
            "newsletter_subscribe": true
          }
        }

    ```

    For example,

    ```JSON

    curl -s -i -X POST 'https://admin.aem.page/form/wkndform/wefinance/main/contact-us.json' \
    --header 'Content-Type: application/json' \
    --data '{
        "data": {
            "Email": "khushwant@wknd.com",
            "Name": "khushwant",
            "Subject": "Regarding Product Inquiry",
            "Message": "I have some questions about your products.",
            "Phone": "123-456-7890",
            "Company": "Adobe Inc.",
            "Country": "United States",
            "PreferredContactMethod": "Email",
            "SubscribeToNewsletter": true
        }
    }'

    ```

* URL encoded (`x-www-form-urlencoded`) body (with `content-type` header set to `application/x-www-form-urlencoded`)

    ```Shell

    'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'

    ```

    For example, if your project's repository is named "wefinance", it's located under the account owner "wkndform", and you're using the "main" branch.,

    ```Shell

    curl -s -i -X POST \
      -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
      https://main--wefinance--wkndform.aem.live/contact-us

    ```
-->

Quindi, puoi [personalizzare il messaggio di ringraziamento](/help/edge/docs/forms/thank-you-page-form.md).

## Consulta anche

{{see-more-forms-eds}}
