---
title: Creare un modulo utilizzando l’authoring basato su documenti per AEM Forms Edge Delivery Service
description: Crea moduli perfetti, velocemente. ⚡ AEM Forms Edge Delivery + authoring basato su documenti = velocità straordinaria e moduli compatibili con SEO per utenti e motori di ricerca più felici.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 20%

---


# Creare un modulo utilizzando l’authoring basato su documenti per AEM Forms Edge Delivery Service

Nell’era digitale di oggi, la creazione di moduli facili da usare è essenziale per qualsiasi organizzazione. L’authoring basato su documenti di AEM Forms Edge Delivery consente di creare moduli utilizzando strumenti familiari come Word o Google Docs.Questi moduli inviano i dati direttamente a un file Microsoft Excel o Google Sheets, consentendo di utilizzare ecosistemi dinamici e API affidabili di Google Sheets, Microsoft Excel e Microsoft Sharepoint per elaborare facilmente i dati inviati o avviare un flusso di lavoro aziendale esistente.

Questa guida illustra i seguenti aspetti:

* Preparazione del foglio di calcolo: scopri come impostare un file Excel o Google Sheets per la raccolta dati e aggiungervi campi modulo.
* Inviare dati al foglio: scopri come inviare dati al foglio utilizzando le richieste di POST.
* Pubblicazione del modulo: integra il modulo nella pagina AEM Sites o pubblicalo come pagina indipendente.

Sia che siate principianti o professionisti, questa guida vi permette di costruire forme belle e funzionali che gli utenti amano. Sblocchiamo la creazione efficiente dei moduli - immergetevi subito!

## Prima di iniziare

`WIP`

## Prepara il foglio di calcolo per ricevere i dati

1. Crea una cartella di lavoro di Microsoft Excel o un foglio di Google ovunque sotto la directory del progetto di consegna AEM Edge su Microsoft OneDrive o Google Drive. Questo documento utilizza un foglio Google denominato `contact-us.xlsx`, si trova nella directory principale di un progetto Adobe Experience Manager (AEM).

1. Assicurati che l’utente AEM (ad esempio helix@adobe.com) configurato per il progetto disponga delle autorizzazioni di modifica per il foglio.

1. Aprire la cartella di lavoro creata e modificare il nome del foglio predefinito in &quot;in ingresso&quot;.

   >[!NOTE]
   >
   > Se il foglio &quot;in entrata&quot; non esiste, il AEM non invierà alcun dato a questa cartella di lavoro.

1. Visualizza l’anteprima del foglio nella barra laterale.

   >[!NOTE]
   >
   >Anche se il foglio è stato visualizzato in anteprima in precedenza, è necessario visualizzarlo nuovamente dopo aver creato il foglio &quot;in ingresso&quot; per la prima volta.

1. Preparare il foglio aggiungendo intestazioni corrispondenti ai dati che si stanno inserendo. Nell&#39;esempio seguente vengono visualizzati i campi per un modulo &quot;contact-us&quot;:

   ![Campi per un modulo contattaci](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   Puoi eseguire questa operazione manualmente o utilizzando una richiesta POST al percorso del modulo nel servizio di amministrazione dell’AEM. Il servizio di amministrazione esamina i dati nel corpo del POST e genera le intestazioni, le tabelle e i fogli necessari per acquisire i dati in modo efficace e sfruttare al massimo il servizio Forms.

   Per informazioni su come formattare la richiesta POST per la configurazione del foglio, consulta [Documentazione API di amministrazione](https://www.hlx.live/docs/admin.html#tag/form). Inoltre, osserva l’esempio fornito di seguito:

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

La richiesta POST di cui sopra fornisce dati di esempio, inclusi i campi modulo e i rispettivi valori di esempio. Questi dati vengono utilizzati dal servizio di amministrazione per configurare il modulo.

Mentre il servizio di amministrazione consiglia di configurare il foglio, se preferisci creare le intestazioni manualmente, consulta il documento intitolato [Impostazione manuale foglio Forms](https://www.hlx.live/docs/manual-forms-sheet-setup).

Quando invii la richiesta POST al servizio di amministrazione, osserverai le seguenti modifiche nella cartella di lavoro:

* Un nuovo foglio denominato &quot;shared-default&quot; viene aggiunto alla cartella di lavoro di Excel o al foglio di Google. I dati presenti nel foglio &quot;shared-default&quot; vengono recuperati quando si effettua una richiesta di GET al foglio. Questo foglio funge da posizione ottimale per utilizzare le formule dei fogli di calcolo per riepilogare i dati in arrivo e favorirne il consumo in altri contesti.

  In nessun caso il foglio &quot;shared-default&quot; deve contenere informazioni personali identificabili o dati sensibili che l&#39;utente non ha familiarità con l&#39;essere accessibile al pubblico.

* Un foglio denominato &quot;Slack&quot; viene aggiunto alla cartella di lavoro di Excel o al foglio di Google. In questo foglio puoi configurare le notifiche automatiche per un canale di Slack designato ogni volta che dei nuovi dati vengono acquisiti nel foglio di calcolo. Attualmente, AEM supporta le notifiche esclusivamente all&#39;organizzazione dello Slack di progettazione AEM e all’organizzazione di supporto aziendale Adobe.

   1. Per impostare le notifiche di Slack, immetti &quot;teamId&quot; dell’area di lavoro di Slack e &quot;channel name&quot; o &quot;ID&quot;. Puoi anche chiedere al bot di Slack (con il comando di debug) il “teamId” e l’“ID canale”. È preferibile utilizzare “ID canale” invece di “nome canale”, in quanto non è influenzato dalle ridenominazioni del canale.

      >[!NOTE]
      >
      > I moduli più vecchi non avevano la colonna “teamId”. Il “teamId” era incluso nella colonna del canale, separato da “#” o “/”.

   1. Immettere il titolo desiderato e in campi immettere i nomi dei campi da visualizzare nella notifica di Slack. Ogni intestazione deve essere separata da una virgola (ad esempio nome, e-mail).

Il foglio è ora configurato per ricevere i dati e puoi inviare richieste di POST direttamente ad esso utilizzando hlx.page, hlx.live o il tuo dominio di produzione.


## Inviare dati al foglio {#send-data-to-your-sheet}

Una volta che il foglio è impostato per ricevere i dati, puoi inviare le richieste di POST direttamente ad esso utilizzando hlx.page, hlx.live o il tuo dominio di produzione, per inviare i dati.

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> L’URL non deve avere l’estensione .json. Devi pubblicare il foglio per far sì che le operazioni POST funzionino su .live o sul dominio di produzione.

### Formattazione dei dati per EDS Forms

Esistono alcuni modi diversi per formattare i dati del modulo nel corpo del POST.

* Matrice di coppie nome:valore:

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
              { "name": "message", "value": "I have some questions about your products." },
              { "name": "phone", "value": "123-456-7890" },
              { "name": "company", "value": "Example Inc." },
              { "name": "country", "value": "United States" },
              { "name": "preferred_contact_method", "value": "Email" },
              { "name": "newsletter_subscribe", "value": true }
              ]
          }'
  
* Oggetto con coppie chiave:valore

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

* `x-www-form-urlencoded` corpo (`content-type` l’intestazione deve essere impostata su `application/x-www-form-urlencoded`) &#39;nome=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



