---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: Endpoint REST di AEM Forms, invia all’endpoint REST, invia dati all’URL REST, configura azione endpoint REST
feature: Adaptive Forms, Core Components
title: Come si configura un’azione di invio per un modulo adattivo?
role: User, Developer
source-git-commit: c20b8909bb884f14bd7fe59f190de3cd375a7111
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 4%

---

# Configurare un modulo adattivo per l’azione di invio dell’endpoint REST

Utilizza l&#39;azione **[!UICONTROL Invia all&#39;endpoint REST]** per inviare i dati inviati a un URL REST. L’URL può essere interno (il server sul quale viene eseguito il rendering del modulo) o esterno.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione degli invii di moduli. Ulteriori informazioni su queste opzioni sono disponibili nell&#39;articolo [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md).

## Vantaggi

Alcuni dei vantaggi della configurazione dell&#39;azione di invio **[!UICONTROL Invia all&#39;endpoint REST]** per Adaptive Forms sono:

* Consente l’integrazione diretta dei dati dei moduli con sistemi e servizi esterni tramite API RESTful.
* Fornisce flessibilità nella gestione delle richieste di dati da Adaptive Forms, supportando strutture di dati dinamiche e complesse.
* Supporta la mappatura dinamica dei campi modulo ai parametri nell’URL dell’endpoint REST, consentendo l’invio di dati adattabili e personalizzabili.


## Configurare l’azione di invio Invia a endpoint REST {#steps-to-configure-submit-to-restendpoint-submit-action}

Per configurare l’azione di invio in base alla specifica API aperta Swagger:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fare clic sulla scheda **[!UICONTROL Invio]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Invia azione]**, selezionare **[!UICONTROL Invia all&#39;endpoint REST]**.
   ![Configurazione dell&#39;azione Invia all&#39;endpoint REST](/help/forms/assets/submit-action-restendpoint.png)

   Per pubblicare i dati su un server interno, specifica il percorso della risorsa. I dati vengono inseriti nel percorso della risorsa. Ad esempio, `/content/restEndPoint`. Per tali richieste successive, vengono utilizzate le informazioni di autenticazione della richiesta di invio.

   Per pubblicare dati su un server esterno, fornisci un URL. Il formato dell&#39;URL è `https://host:port/path_to_rest_end_point`. Assicurati di configurare il percorso per gestire la richiesta POST in modo anonimo.

   ![Mappatura dei valori dei campi passati come parametri della pagina di ringraziamento](assets/post-enabled-actionconfig.png)

   Nell&#39;esempio precedente, le informazioni immesse dall&#39;utente in `textbox` vengono acquisite tramite il parametro `param1`. La sintassi per pubblicare i dati acquisiti tramite `param1` è:

   `String data=request.getParameter("param1");`

   Analogamente, i parametri utilizzati per la registrazione di dati e allegati XML sono `dataXml` e `attachments`.

   Ad esempio, questi due parametri vengono utilizzati nello script per analizzare i dati in un punto finale rest. Utilizza la sintassi seguente per archiviare e analizzare i dati:

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   In questo esempio, `data` memorizza i dati XML e `att` i dati dell&#39;allegato.

   L&#39;azione di invio **[!UICONTROL Invia all&#39;endpoint REST]** invia i dati compilati nel modulo a una pagina di conferma configurata come parte della richiesta HTTP GET. Puoi aggiungere il nome del campo da richiedere. Il formato della richiesta è:

   `{fieldName}={request parameter name}`

   Come mostrato nell&#39;immagine seguente, `param1` e `param2` vengono passati come parametri con valori copiati dai campi **textbox** e **numericbox** per l&#39;azione successiva.

   ![Configurazione dell&#39;azione di invio dell&#39;endpoint REST](assets/action-config.png)

   Puoi anche **[!UICONTROL abilitare la richiesta di POST]** e fornire un URL per pubblicare la richiesta. Per inviare i dati al server AEM che ospita il modulo, utilizzare un percorso relativo corrispondente al percorso radice del server AEM. Ad esempio, `/content/forms/af/SampleForm.html`. Per inviare dati a qualsiasi altro server, utilizzare il percorso assoluto.

1. Fai clic su **[!UICONTROL Fine]**.

### Configurare l’azione di invio in base all’endpoint del servizio REST {#config-service-endpoint-auth}

<span class="preview"> La funzionalità Service Endpoint si trova nel programma Early Adopter ed è applicabile solo ai Componenti core. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fare clic sulla scheda **[!UICONTROL Invio]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Invia azione]**, selezionare **[!UICONTROL Invia all&#39;endpoint REST]**.
1. Abilita la richiesta POST.
1. Specifica l’URL dell’endpoint REST.
1. Selezionare la configurazione creata per il tipo di autenticazione dell&#39;endpoint REST del servizio e i tipi di contenuto. Per ulteriori informazioni sul tipo di autenticazione e sui tipi di contenuto, visita [configurare le origini dati](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint).
   ![Configurazione dell&#39;endpoint REST](assets/rest-service-endpoint-config.png)
1. Fai clic su Fine.

## Best practice

* Quando pubblichi i dati su un server esterno, accertati che l’URL sia sicuro e configura il percorso in modo da gestire la richiesta di POST in modo anonimo per proteggere le informazioni riservate.
* Per passare i campi come parametri in un URL REST, tutti i campi devono avere nomi di elementi diversi, anche se i campi sono posizionati su pannelli diversi.

## Articoli correlati

{{af-submit-action}}
