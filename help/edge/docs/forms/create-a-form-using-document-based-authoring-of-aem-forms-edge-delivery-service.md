---
title: Creare un modulo utilizzando l’authoring basato su documenti di AEM Forms Edge Delivery Service
description: Crea moduli perfetti, velocemente. ⚡ authoring basato su documento di AEM Forms Edge Delivery = velocità sorprendente e moduli compatibili con SEO per utenti e motori di ricerca più soddisfatti.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 100%

---


# Creare un modulo utilizzando l’authoring basato su documenti di AEM Forms Edge Delivery Service

Nell’era digitale di oggi, la creazione di moduli facili da usare è essenziale per qualsiasi organizzazione. L’authoring basato su documenti di AEM Forms Edge Delivery consente di creare moduli usando strumenti conosciuti come Word o Google Docs. Questi moduli inviano i dati direttamente a un file Microsoft Excel o Fogli Google, consentendo di utilizzare un ecosistema dinamico e API affidabili di Fogli Google, Microsoft Excel e Microsoft SharePoint per elaborare facilmente i dati inviati o avviare un flusso di lavoro aziendale esistente.

Questa guida illustra i seguenti passaggi:

* Preparazione del foglio di calcolo: scopri come impostare un file Excel o Fogli Google per la raccolta dati e aggiungervi campi modulo.
* Invio dati al foglio: scopri come inviare dati al foglio utilizzando le richieste POST.
* Pubblicazione del modulo: integra il modulo nella pagina AEM Sites o pubblicalo come pagina indipendente.

Destinata a principianti e a professionisti, questa guida permette di creare moduli di bell’aspetto e funzionali che gli utenti gradiranno. Sveliamo la creazione di moduli efficienti: iniziamo subito!

## Prima di iniziare

`WIP`

## Preparare il foglio di calcolo per la ricezione dei dati

1. Crea una cartella di lavoro di Microsoft Excel o un foglio di Google ovunque all’interno della directory del progetto Edge Delivery AEM su Microsoft OneDrive o Google Drive. Questo documento utilizza un foglio Google denominato `contact-us.xlsx`, che si trova nella directory principale di un progetto di Adobe Experience Manager (AEM).

1. Assicurati che l’utente AEM (ad esempio helix@adobe.com) configurato per il progetto disponga delle autorizzazioni di modifica per il foglio.

1. Apri la cartella di lavoro creata e cambia il nome del foglio predefinito in “incoming”.

   >[!NOTE]
   >
   > Se il foglio “incoming” non esiste, AEM non invierà alcun dato alla cartella di lavoro.

1. Visualizzare l’anteprima del foglio nella barra laterale.

   >[!NOTE]
   >
   >Anche se hai già visualizzato l’anteprima del foglio, devi visualizzarla nuovamente dopo aver creato il foglio “incoming” per la prima volta.

1. Prepara il foglio aggiungendo le intestazioni corrispondenti ai dati che stai inserendo. Nell’esempio seguente vengono visualizzati i campi per un modulo “contattaci”:

   ![Campi per un modulo contattaci](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   Puoi eseguire questa operazione manualmente o utilizzando una richiesta POST al percorso del modulo nel servizio amministrazione di AEM. Il servizio di amministrazione esamina i dati nel corpo della richiesta POST e genera le intestazioni, le tabelle e i fogli appropriati e necessari per acquisire i dati in modo efficace e sfruttare al massimo il servizio Forms.

   Per informazioni su come formattare la richiesta POST per la configurazione del foglio, consulta la [documentazione API di amministrazione](https://www.hlx.live/docs/admin.html#tag/form). Inoltre, osserva l’esempio fornito di seguito:

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
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country","PreferredContactMethod","SubscribeToNewsletter"]}%
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

La richiesta POST menzionata in precedenza fornisce dati di esempio, inclusi i campi modulo e i rispettivi valori di esempio. Questi dati vengono utilizzati dal servizio di amministrazione per configurare il modulo.

Mentre il servizio di amministrazione consiglia di configurare il foglio, se preferisci creare le intestazioni manualmente, consulta il documento intitolato [Impostazione manuale del foglio per moduli](https://www.hlx.live/docs/manual-forms-sheet-setup).

Quando invii la richiesta POST al servizio di amministrazione, nella cartella di lavoro vedrai le modifiche seguenti:

* Un nuovo foglio denominato “shared-default” viene aggiunto alla cartella di lavoro Excel o al foglio di Google. I dati presenti nel foglio “shared-default” vengono recuperati quando si effettua una richiesta GET al foglio. Questo foglio funge da posizione ottimale per utilizzare le formule dei fogli di calcolo in modo da riepilogare i dati in arrivo e favorirne l’utilizzo in altri contesti.

  I fogli “shared-default” non devono mai contenere informazioni personali identificabili o dati sensibili che l’utente non intende rendere accessibili pubblicamente.

* Un foglio denominato “slack” viene aggiunto alla cartella di lavoro Excel o al foglio di Google. In questo foglio puoi configurare le notifiche automatiche per un canale di Slack designato ogni volta che dei nuovi dati vengono acquisiti nel foglio di calcolo. Attualmente, AEM supporta le notifiche esclusivamente all&#39;organizzazione dello Slack di progettazione AEM e all’organizzazione di supporto aziendale Adobe.

   1. Per impostare le notifiche Slack, immetti il “teamId” dell’area di lavoro Slack e il “nome del canale” o l’“ID”. Puoi anche chiedere al bot di Slack (con il comando di debug) il “teamId” e l’“ID canale”. È preferibile utilizzare “ID canale” invece di “nome canale”, in quanto non è influenzato dalle ridenominazioni del canale.

      >[!NOTE]
      >
      > I moduli più vecchi non avevano la colonna “teamId”. Il “teamId” era incluso nella colonna del canale, separato da “#” o “/”.

   1. Immetti il titolo desiderato e in campi immetti i nomi dei campi da visualizzare nella notifica Slack. Ogni intestazione deve essere separata da una virgola (ad esempio nome, e-mail).

Il foglio è ora configurato per ricevere i dati e puoi inviare richieste POST direttamente ad esso utilizzando hlx.page, hlx.live o il tuo dominio di produzione.


## Inviare dati al foglio {#send-data-to-your-sheet}

Una volta che il foglio è configurato per ricevere i dati, puoi inviare le richieste POST direttamente ad esso utilizzando hlx.page, hlx.live o il tuo dominio di produzione, per l’invio dei dati.

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> L’URL non deve avere l’estensione .json. È necessario pubblicare il foglio per far funzionare le operazioni POST su .live o sul dominio di produzione.

### Formattazione dei dati per moduli EDS

Esistono diversi modi per formattare i dati del modulo nel corpo POST.

* Array di coppie nome-valore:

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

  Ad esempio

  ```JSON
      curl -s -i -X POST 'https://main--portal--wkndforms.hlx.page/contact-us' \
          --header 'Content-Type: application/json' \
          --data '{
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
          }'
  
* Oggetto con coppie chiave-valore

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

* corpo `x-www-form-urlencoded` (`content-type` l’intestazione deve essere impostata su `application/x-www-form-urlencoded`)
‘firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com’



