---
title: Preparare il foglio di calcolo per accettare i dati
description: Creare moduli potenti più rapidamente utilizzando fogli di calcolo e campi blocco di moduli adattivi.
feature: Edge Delivery Services
exl-id: 0643aee5-3a7f-449f-b086-ed637ae53b5a
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 100%

---

# Impostare i Fogli Google o i file Microsoft Excel per iniziare ad accettare i dati


Una volta che hai [creato e visualizzato in anteprima il modulo](/help/edge/docs/forms/create-forms.md), è il momento di abilitare il foglio di calcolo corrispondente per iniziare a ricevere i dati. Operazioni disponibili:

- [Abilitare manualmente il foglio di calcolo per accettare i dati](#manually-enable-the-spreadsheet-to-accept-data)
- [Utilizza le API amministratore per abilitare un foglio di calcolo ad accettare i dati](#use-admin-apis-to-enable-a-spreadsheet-to-accept-data)

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


## Utilizza le API amministratore per abilitare un foglio di calcolo ad accettare i dati

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

## modifiche automatiche al foglio dopo che è stato abilitato per l’accettazione dei dati.

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



Quindi, puoi [personalizzare il messaggio di ringraziamento](/help/edge/docs/forms/thank-you-page-form.md).

