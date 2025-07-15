---
Title: How to use forms submission service for submitting forms?
Description: Learn how to use forms submission service for submitting forms.
Keywords: Use form submission service, Submit form using form submission service
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: 37b20a97942f381b46ce36a6a3f72ac019bba5b7
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 9%

---

# Servizio di invio Forms con Edge Delivery Services Forms

<span class="preview"> Questa funzione è disponibile tramite il programma per i primi utilizzatori. Per richiedere l’accesso, invia un’e-mail con il nome dell’organizzazione e il nome dell’archivio GitHub dall’indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Ad esempio, se l’URL dell’archivio è https://github.com/adobe/abc, il nome dell’organizzazione è adobe e il nome dell’archivio è abc.</span>

Il servizio di invio di Forms consente di memorizzare i dati degli invii di moduli in qualsiasi foglio di calcolo, ad esempio OneDrive, SharePoint o Google Sheets, consentendo di accedere e gestire facilmente i dati dei moduli nella piattaforma di fogli di calcolo preferita.

![Servizio di invio Forms](/help/forms/assets/form-submission-service.png)

## Vantaggi dell&#39;utilizzo del servizio di invio Forms

Alcuni vantaggi dell’utilizzo del servizio di invio Forms con i fogli di calcolo sono:

* **Integrazione diretta**: è possibile configurare i moduli per inviare i dati direttamente a un foglio di calcolo specificato, eliminando la necessità di trasferimento manuale dei dati.
* **Struttura dati**: quando si imposta l&#39;invio, è possibile mappare i campi modulo alle colonne corrispondenti del foglio di calcolo per l&#39;archiviazione organizzata dei dati.
* **Controllo dell&#39;accesso**: è possibile sfruttare le autorizzazioni esistenti per controllare gli utenti che possono accedere e modificare i dati del modulo inviati, a seconda del servizio foglio di calcolo scelto.

## Prerequisiti

Di seguito sono riportati i prerequisiti per l’utilizzo del servizio Forms Submission:

* Assicurati che nel progetto AEM sia presente il blocco di moduli adattivi più recente.
* Assicurati che l’archivio Git sia aggiunto al inserisco nell&#39;elenco Consentiti di per utilizzare il servizio di invio Forms. [mailto:aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con il nome dell&#39;organizzazione GitHub e il nome dell&#39;archivio per aggiungerli al elenco Consentiti di per l&#39;utilizzo del servizio di invio Forms.

## Configurare il servizio di invio Forms

Crea un nuovo progetto AEM configurato con il blocco Forms adattivo. Per informazioni su come creare un nuovo progetto AEM, consulta l&#39;articolo [Guida introduttiva - Esercitazione per sviluppatori](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial). Aggiorna il file `fstab.yaml` nel progetto. Sostituire il riferimento esistente con il percorso della cartella condivisa con `forms@adobe.com`.

È possibile [configurare il servizio di invio di Forms manualmente](#configuring-the-forms-submission-service-manually) o [configurare il servizio di invio di Forms utilizzando l&#39;API](#configuring-the-forms-submission-service-using-api).

### Configurazione manuale del servizio di invio Forms

![Flusso di lavoro per il servizio di invio moduli](/help/forms/assets/forms-submission-service-workflow.png)

#### &#x200B;1. Creare un modulo utilizzando una definizione di modulo

Creare un modulo utilizzando Google Sheets o Microsoft Excel. Per informazioni su come creare un modulo utilizzando una definizione di modulo in Microsoft Excel o Google Sheets, [fare clic qui](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms).

La schermata seguente mostra la definizione del modulo utilizzata per creare il modulo:

![Definizione modulo](/help/forms/assets/form-submission-definition.png)

>[!IMPORTANT]
>
>**Il foglio in cui è stato creato il modulo presenta restrizioni relative al nome. Solo `helix-default` e `shared-aem` possono essere utilizzati come nomi per il foglio.**

#### &#x200B;2. Abilitare il foglio di calcolo per accettare i dati.

Dopo aver creato e visualizzato in anteprima il modulo, abilita il foglio di calcolo corrispondente per iniziare a ricevere i dati. aggiungere un nuovo foglio come `incoming`. È possibile [abilitare manualmente il foglio di calcolo per accettare i dati](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/submit-forms#manually-enable-the-spreadsheet-to-accept-data).

![Foglio in ingresso](/help/forms/assets/form-submission-incoming-sheet.png)

>[!WARNING]
>
> Se il foglio `incoming` non esiste, AEM non invierà alcun dato a questa cartella di lavoro.

#### &#x200B;3. Condividi il foglio di calcolo e genera un collegamento.

Per condividere il foglio di calcolo con l&#39;account `forms@adobe.com` e generare un collegamento, effettuare le seguenti operazioni:

1. In Excel o Google Sheets, fai clic sul pulsante **Condividi** in alto a destra.
1. Aggiungi l&#39;account `forms@adobe.com` e
fai clic sull&#39;icona a forma di occhio, seleziona l&#39;accesso **Modifica** e fai clic su **Invia**.

   ![Condividi foglio in ingresso](/help/forms/assets/form-submission-share-incoming.png)

1. Per copiare il collegamento del foglio di calcolo, fare clic sul pulsante **Condividi** nell&#39;angolo superiore destro e selezionare **Copia collegamento**.

   ![Copia collegamento del foglio in ingresso](/help/forms/assets/form-submission-copy-link.png)

#### &#x200B;4. Collegare il foglio di calcolo nella definizione del modulo

Per configurare il servizio Invio di Forms con Google Sheets o Microsoft Excel, effettuare le seguenti operazioni:

1. Aprire il foglio di calcolo contenente la definizione del modulo.
1. Nella riga corrispondente al campo **Invia**, incolla il collegamento del foglio di calcolo copiato nella colonna **Azione**.

   ![Collega un foglio di calcolo](/help/forms/assets/form-submission-sheet-linking.png)

1. Visualizza l&#39;anteprima e pubblica il foglio utilizzando [AEM Sidekick](https://www.aem.live/docs/sidekick) con il servizio di invio modulo aggiornato.

>[!NOTE]
>
> È possibile fare riferimento al [foglio di calcolo](/help/forms/assets/spreadsheet.xlsx) per utilizzare il servizio di invio Forms.

### Configurazione del servizio di invio Forms tramite API

È inoltre possibile inviare una richiesta **POST** al modulo per aggiornare il foglio `incoming` con i dati.

>[!NOTE]
>
> * Se il foglio `incoming` non esiste, AEM non invierà alcun dato a questa cartella di lavoro.
> * Condividi il foglio `incoming` con Adobe Experience Manager `forms@adobe.com` e concedi l&#39;accesso di modifica.
> * Visualizza l&#39;anteprima e pubblica il foglio `incoming` nella barra laterale.

Per informazioni su come formattare la richiesta POST per la configurazione del foglio, consulta la [documentazione API](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/). Osserva l’esempio fornito di seguito:

Puoi utilizzare strumenti come curl o Postman per eseguire questa richiesta POST, come dimostrato di seguito.

* **Utilizzo di Postman**:

Ad esempio, invia la richiesta seguente in Postman dopo la sostituzione:
* `{id}` con il tuo ID modulo
* `site or repository` con il tuo archivio GitHub o nome sito
* `organization` con il tuo nome utente GitHub

  ```json
  POST 'https://forms.adobe.com/adobe/forms/af/submit/{id}' \
  --header 'Content-Type: application/json' \
  --header 'x-adobe-routing: tier=live,bucket=main--[site/repository]--[organization]' \
  --data '{
      "data": {
          "startDate": "2025-01-10",
          "endDate": "2025-01-25",
          "destination": "Australia",
          "class": "First Class",
          "budget": "2000",
          "amount": "1000000",
          "name": "Mary",
          "age": "35",
          "subscribe": null,
          "email": "mary@gmail.com"
              }
          }'
  ```

Facendo clic sul pulsante **Invia** in Postman viene restituita una risposta `201 Created` e il foglio `incoming` viene aggiornato con i dati inviati.

![schermata postman](/help/forms/assets/postman-api.png)

* **Utilizzo del comando Curl**:

Ad esempio, esegui il comando seguente nel terminale o nel prompt dei comandi dopo la sostituzione:
* `{id}` con il tuo ID modulo
* `site or repository` con il tuo archivio GitHub o nome sito
* `organization` con il tuo nome utente GitHub


>[!BEGINTABS]

>[!TAB Per macOS]

    &quot;json
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; \
    —header &quot;Content-Type: application/json&quot; \
    —header &quot;x-adobe-routing: tier=live,bucket=main—[site/repository]—[organization]&quot; \
    —data &quot;&lbrace;
    &quot;data&quot;: &lbrace;
    &quot;startDate&quot;: &quot;2025-01-10&quot;,
    &quot;endDate&quot;: &quot;2025-01-25&quot;,
    &quot;destination&quot;: &quot;Australia&quot;,
    &quot;classe&quot;: &quot;Prima classe&quot;,
    &quot;budget&quot;: &quot;2000&quot;,
    &quot;importo&quot;: &quot;1000000&quot;,
    &quot;nome&quot;: &quot;Joe&quot;,
    &quot;età&quot;: &quot;35&quot;,
    &quot;abbonamento&quot;: null,
    &quot;e-mail&quot;: &quot;mary@gmail.com&quot;
    &rbrace;
    &rbrace;&#39;
    
    &quot;

>[!TAB Per Windows OS]

    &quot;json
    
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; ^
    —header &quot;Content-Type: application/json&quot; ^
    —header &quot;x-adobe-routing: tier=live,bucket=main—[site/repository]—[organization]&quot; ^
    —data &quot;{\&quot;data\&quot;: {\&quot;startDate\&quot;: \&quot;2025-01-10\&quot;, \&quot;endDate\&quot;: \&quot;2025-01-25\&quot;, \&quot;destinazione\&quot;: \&quot;Australia\&quot;, \&quot;classe\&quot;: \&quot;Prima classe\&quot;, \&quot;budget\&quot;: \&quot;2000\&quot;, \&quot;importo\&quot;: \&quot;1000000\&quot;, \&quot;nome\&quot;: \&quot;Joe\&quot;, \&quot;età\&quot;: \&quot;35\&quot;, \&quot;sottoscrizione\&quot;: null, \&quot;e-mail\&quot;: \&quot;mary@gmail.com\&quot;}}&quot;
    
    &quot;

>[!ENDTABS]

La richiesta POST sopra indicata aggiorna il foglio `incoming` con la seguente risposta:

```json
    < HTTP/1.1 201 Created
    < Connection: keep-alive
    < Content-Length: 0
    < X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
    < X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
    < Accept-Ranges: bytes
    < Date: Fri, 10 Jan 2025 13:06:10 GMT
    < Via: 1.1 varnish
    < Access-Control-Allow-Origin: *
    < X-Served-By: cache-del21750-DEL
    < X-Cache: MISS
    < X-Cache-Hits: 0
    < X-Timer: S1736514370.704084,VS0,VE1234
```

Nella schermata seguente viene visualizzata la schermata del foglio `incoming` aggiornato dall&#39;invio di dati tramite API:

![foglio aggiornato](/help/forms/assets/updated-sheet.png)

## Consulta anche

{{see-more-forms-eds}}