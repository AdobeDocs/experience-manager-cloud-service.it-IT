---
title: Preparare il foglio di calcolo per accettare i dati
description: Crea moduli potenti più rapidamente utilizzando fogli di calcolo e campi blocco modulo.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# Preparare il foglio di calcolo per accettare i dati

Una volta [ha creato e visualizzato in anteprima il modulo](/help/edge/docs/forms/create-forms.md), è ora di abilitare il foglio di calcolo corrispondente per iniziare a ricevere i dati.

<!-- 
>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->

Per attivare il foglio di calcolo:

1. Aprire il foglio di calcolo contenente il modulo e aggiungere un nuovo foglio, rinominandolo `incoming`.

   >[!WARNING]
   >
   > Se il `incoming` non è presente, l’AEM non invia dati al foglio di calcolo.

1. Speculare i nomi dei campi modulo e i valori `Name` colonna nella`shared-default` alle intestazioni nel foglio `incoming` foglio.

   Ogni valore in `Name` colonna del `shared-default` , escluso il pulsante di invio, funge da intestazione nel `incoming` foglio. Ad esempio, considera l’immagine seguente che illustra le intestazioni per un modulo &quot;contact-us&quot;:

   ![Campi per un modulo per i contatti](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. Utilizza la barra laterale per visualizzare l’anteprima del foglio.

   >[!NOTE]
   >
   >Anche se avete già visualizzato l&#39;anteprima del foglio, dovete visualizzarla nuovamente dopo aver creato il `incoming` per la prima volta.


Una volta aggiunti i nomi dei campi al `incoming` foglio, il modulo diventa pronto per accettare gli invii. È possibile visualizzare in anteprima il modulo e inviare i dati al foglio utilizzando il modulo.

Nel foglio di calcolo vengono inoltre osservate le seguenti modifiche:

Un foglio denominato &quot;Slack&quot; viene aggiunto alla cartella di lavoro di Excel o al foglio di Google. In questo foglio puoi configurare le notifiche automatiche per un canale di Slack designato ogni volta che nuovi dati vengono acquisiti nel foglio di calcolo. Attualmente, l&#39;AEM supporta le notifiche esclusivamente all&#39;organizzazione dello Slack di progettazione AEM e all&#39;organizzazione di supporto aziendale Adobe.

1. Per impostare le notifiche di Slack, immetti il &quot;teamId&quot; dell’area di lavoro di Slack e il &quot;nome del canale&quot; o l’&quot;ID&quot;. Puoi anche chiedere al backbot (con il comando di debug) di &quot;teamId&quot; e &quot;channel ID&quot;. È preferibile utilizzare &quot;ID canale&quot; invece di &quot;nome canale&quot;, in quanto sopravvive alle ridenominazioni del canale.

   >[!NOTE]
   >
   > I moduli più vecchi non avevano la colonna &quot;teamId&quot;. Il &quot;teamId&quot; era incluso nella colonna del canale, separato da un &quot;#&quot; o &quot;/&quot;.

1. Immettere il titolo desiderato e in campi immettere i nomi dei campi da visualizzare nella notifica di Slack. Ogni intestazione deve essere separata da una virgola (ad esempio nome, e-mail).

   >[!WARNING]
   >
   >  I fogli &quot;shared-default&quot; non devono mai contenere informazioni personali identificabili o dati sensibili che l&#39;utente non è a suo agio nell&#39;essere accessibili pubblicamente.


## (Facoltativo) Utilizza le API amministratore per consentire a un foglio di calcolo di accettare i dati

È inoltre possibile inviare una richiesta POST al modulo per consentirgli di accettare dati e configurare intestazioni per `incoming` foglio. Dopo aver ricevuto la richiesta del POST, il servizio analizza il corpo della richiesta e genera in modo autonomo le intestazioni e i fogli essenziali necessari per l’acquisizione dei dati.

Per utilizzare le API amministratore per consentire a un foglio di calcolo di accettare i dati:


1. Aprire la cartella di lavoro creata e modificare il nome del foglio predefinito in `incoming`.

   >[!WARNING]
   >
   > Se il `incoming` Il foglio di lavoro non esiste, l&#39;AEM non invierà alcun dato alla cartella di lavoro.

1. Visualizzate l&#39;anteprima del foglio nella barra laterale.

   >[!NOTE]
   >
   >Anche se avete già visualizzato l&#39;anteprima del foglio, dovete visualizzarla nuovamente dopo aver creato il `incoming` per la prima volta.

1. Invia la richiesta POST per generare le intestazioni appropriate nel `incoming` e aggiungere il `shared-default` nel foglio di calcolo, se non esiste già.

   Per informazioni su come formattare la richiesta POST per la configurazione del foglio, consultare [Documentazione di Admin API](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile). Osserva l’esempio fornito di seguito:

   **Richiesta**

   ```JSON
   POST 'https://admin.hlx.page/form/{owner}/{repo}/{branch}/contact-us.json' \
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
   curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
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

   La richiesta POST di cui sopra fornisce dati di esempio, inclusi i campi del modulo e i rispettivi valori di esempio. Questi dati vengono utilizzati dal servizio di amministrazione per configurare il modulo.

   Il modulo è ora abilitato per l&#39;accettazione dei dati. Nel foglio di calcolo vengono inoltre osservate le seguenti modifiche:

Un foglio denominato &quot;Slack&quot; viene aggiunto alla cartella di lavoro di Excel o al foglio di Google. In questo foglio puoi configurare le notifiche automatiche per un canale di Slack designato ogni volta che nuovi dati vengono acquisiti nel foglio di calcolo. Attualmente, l&#39;AEM supporta le notifiche esclusivamente all&#39;organizzazione dello Slack di progettazione AEM e all&#39;organizzazione di supporto aziendale Adobe.

1. Per impostare le notifiche di Slack, immetti il &quot;teamId&quot; dell’area di lavoro di Slack e il &quot;nome del canale&quot; o l’&quot;ID&quot;. Puoi anche chiedere al backbot (con il comando di debug) di &quot;teamId&quot; e &quot;channel ID&quot;. È preferibile utilizzare &quot;ID canale&quot; invece di &quot;nome canale&quot;, in quanto sopravvive alle ridenominazioni del canale.

   >[!NOTE]
   >
   > I moduli più vecchi non avevano la colonna &quot;teamId&quot;. Il &quot;teamId&quot; era incluso nella colonna del canale, separato da un &quot;#&quot; o &quot;/&quot;.

1. Immettere il titolo desiderato e in campi immettere i nomi dei campi da visualizzare nella notifica di Slack. Ogni intestazione deve essere separata da una virgola (ad esempio nome, e-mail).


Il foglio è ora configurato per la ricezione dei dati, è possibile [visualizzare in anteprima il modulo utilizzando il blocco Modulo adattivo](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) o [utilizzare le richieste POST](#use-admin-apis-to-send-data-to-your-sheet) per iniziare a inviare dati al foglio.

>[!WARNING]
>
>  I fogli &quot;shared-default&quot; non devono mai contenere informazioni personali identificabili o dati sensibili che l&#39;utente non è a suo agio nell&#39;essere accessibili pubblicamente.

## Invia dati al foglio {#send-data-to-your-sheet}

Dopo aver impostato il foglio per la ricezione dei dati, è possibile [visualizzare in anteprima il modulo utilizzando il blocco Modulo adattivo](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) o [utilizzare le API amministratore](#use-admin-apis-to-send-data-to-your-sheet) per iniziare a inviare dati al foglio.

### Utilizzare le API amministratore per inviare dati al foglio

Puoi inviare le richieste di POST direttamente al tuo modulo utilizzando hlx.page, hlx.live o il tuo dominio di produzione, per inviare dati.


```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> L’URL non deve avere l’estensione .json. È necessario pubblicare il foglio per far funzionare le operazioni POST su `.live` o sul dominio di produzione.

#### Formattazione dei dati del modulo

Esistono alcuni modi diversi per formattare i dati del modulo nel corpo del POST. Puoi utilizzare:

* array di `name:value` coppie:

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

  Per esempio

  ```JSON
  curl -s -i -X POST 'https://main--portal--wkndforms.hlx.page/contact-us' \
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



* un oggetto con `key:value` coppie:

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

  Ad esempio:

  ```JSON
  curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
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

* Codifica URL (`x-www-form-urlencoded`) corpo (con `content-type` intestazione impostata su `application/x-www-form-urlencoded`)

  ```Shell
  'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'
  ```

  Ad esempio:

  ```Shell
  curl -s -i -X POST \
    -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
    https://main--portal--wkndforms.hlx.live/contact-us
  ```

Ora puoi personalizzare il messaggio di ringraziamento, [configurare una pagina di ringraziamento](/help/edge/docs/forms/thank-you-page-form.md), o [imposta reindirizzamenti](/help/edge/docs/forms/thank-you-page-form.md).

## Vedi altro

* [Creare e visualizzare in anteprima un modulo](/help/edge/docs/forms/create-forms.md)
* [Abilita modulo per l’invio di dati](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare un modulo nella pagina Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Aggiungere convalide ai campi modulo](/help/edge/docs/forms/validate-forms.md)
* [Modificare i temi e lo stile del modulo](/help/edge/docs/forms/style-theme-forms.md)
