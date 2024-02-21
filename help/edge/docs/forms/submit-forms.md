---
title: 'Da fogli di calcolo a Forms: masterizzazione delle convalide dei campi blocco modulo'
description: Crea moduli potenti più rapidamente utilizzando fogli di calcolo e campi blocco modulo. Questa guida consente di creare convalide personalizzate per i campi blocco EDS Forms.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---


# Attiva il modulo per l&#39;invio dei dati

Dopo aver creato e visualizzato in anteprima il modulo, attivare il foglio corrispondente per accettare i dati. Per iniziare ad accettare i dati, imposta il foglio di calcolo in modo da includere le intestazioni corrispondenti ai dati che intendi raccogliere. Tutte le intestazioni aggiunte al foglio &quot;shared-default&quot; devono essere presenti anche nel foglio &quot;incoming&quot; sotto una tabella.

Nell&#39;esempio seguente vengono visualizzati i campi per un modulo &quot;contact-us&quot;:

![Campi per un modulo per i contatti](/help/edge/assets/contact-us-form-excel-sheet-fields.png)


Una volta completata la configurazione, il modulo diventa pronto per accettare gli invii. Per consentire al foglio di calcolo di accettare i dati, è possibile utilizzare uno dei seguenti metodi:

* [Configurare manualmente un foglio di calcolo per accettare i dati](#manually-configure-a-spreadsheet-to-receive-data)

* [Utilizzare le API amministratore per consentire a un foglio di calcolo di accettare i dati](#use-admin-apis-to-enable-a-spreadsheet-to-receive-data-use-admin-apis-to-enable-a-spreadsheet-to-recieve-data)

## Configurare manualmente un foglio di calcolo per accettare i dati

Per configurare manualmente un foglio di calcolo per l&#39;accettazione dei dati:


1. Aprire la cartella di lavoro creata e modificare il nome del foglio predefinito in &quot;in ingresso&quot;.

   >[!WARNING]
   >
   > Se il foglio &quot;in entrata&quot; non esiste, il AEM non invierà alcun dato a questa cartella di lavoro.

1. Preparare il foglio aggiungendo intestazioni corrispondenti ai dati che si stanno inserendo. Nell&#39;esempio seguente vengono visualizzati i campi per un modulo &quot;contact-us&quot;:

   ![Campi per un modulo per i contatti](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. Visualizzate l&#39;anteprima del foglio nella barra laterale.

   >[!NOTE]
   >
   >Anche se il foglio è stato visualizzato in anteprima in precedenza, è necessario visualizzarlo nuovamente dopo aver creato il foglio &quot;in ingresso&quot; per la prima volta.


## Utilizzare le API amministratore per consentire a un foglio di calcolo di accettare i dati

Puoi avviare una richiesta POST al percorso del modulo all’interno del servizio di amministrazione dell’AEM. Una volta ricevuti i dati del corpo del POST, il servizio di amministrazione li analizza e genera in modo autonomo le intestazioni, le tabelle e i fogli essenziali necessari per l’acquisizione dei dati, ottimizzando la funzionalità del servizio forms.

Per utilizzare le API amministratore per consentire a un foglio di calcolo di accettare i dati:


1. Aprire la cartella di lavoro creata e modificare il nome del foglio predefinito in &quot;in ingresso&quot;.

   >[!WARNING]
   >
   > Se il foglio &quot;in entrata&quot; non esiste, il AEM non invierà alcun dato a questa cartella di lavoro.

1. Visualizzate l&#39;anteprima del foglio nella barra laterale.

   >[!NOTE]
   >
   >Anche se il foglio è stato visualizzato in anteprima in precedenza, è necessario visualizzarlo nuovamente dopo aver creato il foglio &quot;in ingresso&quot; per la prima volta.

1. Preparare il foglio aggiungendo intestazioni corrispondenti ai dati che si stanno inserendo.

   A tale scopo, invia una richiesta POST al percorso del modulo nel servizio di amministrazione dell’AEM. Il servizio di amministrazione esamina i dati nel corpo del POST e genera le intestazioni, le tabelle e i fogli appropriati, necessari per acquisire i dati in modo efficace e sfruttare al massimo il servizio Forms.

   Per informazioni su come formattare la richiesta POST per la configurazione del foglio, consultare [Documentazione di Admin API](https://www.hlx.live/docs/admin.html#tag/form). Osserva inoltre l’esempio fornito di seguito:

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

   La richiesta POST precedentemente menzionata fornisce dati di esempio, inclusi i campi del modulo e i rispettivi valori di esempio. Questi dati vengono utilizzati dal servizio di amministrazione per configurare il modulo.

   Quando si invia la richiesta POST al servizio di amministrazione, si osservano le seguenti modifiche nella cartella di lavoro:

* Un nuovo foglio denominato &quot;shared-default&quot; viene aggiunto alla cartella di lavoro di Excel o al foglio di Google. I dati presenti nel foglio &quot;shared-default&quot; vengono recuperati quando si effettua una richiesta di GET al foglio. Questo foglio funge da posizione ottimale per utilizzare le formule del foglio di calcolo per riepilogare i dati in arrivo e favorirne il consumo in altri contesti.

  I fogli &quot;shared-default&quot; non devono mai contenere informazioni personali identificabili o dati sensibili che l&#39;utente non è a suo agio nell&#39;essere accessibili pubblicamente.

* Un foglio denominato &quot;Slack&quot; viene aggiunto alla cartella di lavoro di Excel o al foglio di Google. In questo foglio puoi configurare le notifiche automatiche per un canale di Slack designato ogni volta che nuovi dati vengono acquisiti nel foglio di calcolo. Attualmente, l&#39;AEM supporta le notifiche esclusivamente all&#39;organizzazione dello Slack di progettazione AEM e all&#39;organizzazione di supporto aziendale Adobe.

   1. Per impostare le notifiche di Slack, immetti il &quot;teamId&quot; dell’area di lavoro di Slack e il &quot;nome del canale&quot; o l’&quot;ID&quot;. Puoi anche chiedere al backbot (con il comando di debug) di &quot;teamId&quot; e &quot;channel ID&quot;. È preferibile utilizzare &quot;ID canale&quot; invece di &quot;nome canale&quot;, in quanto sopravvive alle ridenominazioni del canale.

      >[!NOTE]
      >
      > I moduli più vecchi non avevano la colonna &quot;teamId&quot;. Il &quot;teamId&quot; era incluso nella colonna del canale, separato da un &quot;#&quot; o &quot;/&quot;.

   1. Immettere il titolo desiderato e in campi immettere i nomi dei campi da visualizzare nella notifica di Slack. Ogni intestazione deve essere separata da una virgola (ad esempio nome, e-mail).

Il foglio è ora configurato per la ricezione dei dati, è possibile [anteprima del modulo utilizzando il blocco moduli](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) o [utilizzare le richieste POST](#use-admin-apis-to-send-data-to-your-sheet) per iniziare a inviare dati al foglio.



## Invia dati al foglio {#send-data-to-your-sheet}

Dopo aver impostato il foglio per la ricezione dei dati, è possibile [anteprima del modulo utilizzando il blocco moduli](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) o [utilizzare le API amministratore](#use-admin-apis-to-send-data-to-your-sheet) per iniziare a inviare dati al foglio.

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

Quindi, puoi personalizzare il messaggio di ringraziamento, [configurare una pagina di ringraziamento](/help/edge/docs/forms/thank-you-page-form.md), o [imposta reindirizzamenti](/help/edge/docs/forms/thank-you-page-form.md).

## Vedi altro

* [Creare e visualizzare in anteprima un modulo](/help/edge/docs/forms/create-forms.md)
* [Abilita modulo per l’invio di dati](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare un modulo nella pagina Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Aggiungere convalide ai campi modulo](/help/edge/docs/forms/validate-forms.md)
* [Modificare i temi e lo stile del modulo](/help/edge/docs/forms/style-theme-forms.md)