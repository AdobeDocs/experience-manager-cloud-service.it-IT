---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: Endpoint REST di AEM Forms, Invia a endpoint REST, Dati Post a URL REST, Configura azione endpoint REST
feature: Adaptive Forms, Core Components
exl-id: 58c63ba6-aec5-4961-a70a-265990ab9cc8
title: "Come configurare un’azione di invio per un modulo adattivo?"
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Configurare un modulo adattivo per l’azione di invio dell’endpoint REST

Utilizza il **[!UICONTROL Invia all’endpoint REST]** per pubblicare i dati inviati a un URL REST. L’URL può essere interno (il server sul quale viene eseguito il rendering del modulo) o esterno.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione degli invii di moduli. Per ulteriori informazioni su queste opzioni, consulta [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md)  articolo.

## Vantaggi

Alcuni dei vantaggi della configurazione di **[!UICONTROL Invia all’endpoint REST]** le azioni di invio per Adaptive Forms sono:

* Consente l’integrazione diretta dei dati dei moduli con sistemi e servizi esterni tramite API RESTful.
* Fornisce flessibilità nella gestione delle richieste di dati da Adaptive Forms, supportando strutture di dati dinamiche e complesse.
* Supporta la mappatura dinamica dei campi modulo ai parametri nell’URL dell’endpoint REST, consentendo l’invio di dati adattabili e personalizzabili.


## Configurare l’azione di invio Invia a endpoint REST {#steps-to-configure-submit-to-restendpoint-submit-action}

Per configurare l’azione di invio:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fai clic su  **[!UICONTROL Invio]** scheda.
1. Dalla sezione **[!UICONTROL Azione di invio]** elenco a discesa, seleziona **[!UICONTROL Invia all’endpoint Rest]**.
   ![Configurazione dell’azione dell’endpoint &quot;Invia a Rest&quot;](/help/forms/assets/submit-action-restendpoint.png)

   Per pubblicare i dati su un server interno, specifica il percorso della risorsa. I dati vengono inseriti nel percorso della risorsa. Ad esempio, `/content/restEndPoint`. Per tali richieste successive, vengono utilizzate le informazioni di autenticazione della richiesta di invio.

   Per pubblicare dati su un server esterno, fornisci un URL. Il formato dell’URL è `https://host:port/path_to_rest_end_point`. Assicurati di configurare il percorso per gestire la richiesta POST in modo anonimo.

   ![Mappatura per i valori dei campi passati come parametri della pagina di ringraziamento](assets/post-enabled-actionconfig.png)

   Nell’esempio precedente, l’utente ha inserito le informazioni in `textbox` viene acquisito tramite il parametro `param1`. Sintassi per pubblicare i dati acquisiti tramite `param1` è:

   `String data=request.getParameter("param1");`

   Analogamente, i parametri utilizzati per la registrazione di dati e allegati XML sono `dataXml` e `attachments`.

   Ad esempio, questi due parametri vengono utilizzati nello script per analizzare i dati in un punto finale rest. Utilizza la sintassi seguente per archiviare e analizzare i dati:

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   In questo esempio, `data` memorizza i dati XML e `att` memorizza i dati dell&#39;allegato.

   Il **[!UICONTROL Invia all’endpoint REST]** Azione di invio invia i dati compilati nel modulo a una pagina di conferma configurata come parte della richiesta HTTP GET. Puoi aggiungere il nome del campo da richiedere. Il formato della richiesta è:

   `{fieldName}={request parameter name}`

   Come mostrato nell&#39;immagine seguente, `param1` e `param2` vengono passati come parametri con valori copiati da **casella di testo** e **numericbox** campi per l’azione successiva.

   ![Configurazione dell’azione di invio endpoint REST](assets/action-config.png)

   È inoltre possibile **[!UICONTROL Abilita richiesta POST]** e fornisci un URL per pubblicare la richiesta. Per inviare i dati al server AEM che ospita il modulo, utilizzare un percorso relativo corrispondente al percorso radice del server AEM. Ad esempio, `/content/forms/af/SampleForm.html`. Per inviare dati a qualsiasi altro server, utilizzare il percorso assoluto.

1. Fai clic su **[!UICONTROL Fine]**.

## Best practice

* Quando pubblichi i dati su un server esterno, accertati che l’URL sia sicuro e configura il percorso in modo da gestire la richiesta di POST in modo anonimo per proteggere le informazioni riservate.
* Per passare i campi come parametri in un URL REST, tutti i campi devono avere nomi di elementi diversi, anche se i campi sono posizionati su pannelli diversi.

## Articoli correlati

{{af-submit-action}}
