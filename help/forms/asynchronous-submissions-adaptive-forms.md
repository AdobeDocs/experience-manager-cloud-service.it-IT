---
title: Come si configura l’invio asincrono per Forms adattivo?
description: Scopri come configurare l’invio asincrono per Adaptive Forms. Approfondisci il funzionamento dell’invio asincrono per Adaptive Forms.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 026f4920-f8f9-4b08-b1b0-af50229633d7
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# Invio asincrono di Adaptive Forms {#asynchronous-submission-of-adaptive-forms}

In genere, i moduli web sono configurati per l’invio in modo sincrono. Nell’invio sincrono, quando gli utenti inviano un modulo, vengono reindirizzati a una pagina di conferma, a una pagina di ringraziamento o in caso di errore di invio, a una pagina di errore. Tuttavia, le moderne esperienze web come le applicazioni a pagina singola stanno guadagnando popolarità laddove la pagina web rimane statica mentre l&#39;interazione client-server avviene in background. Puoi configurare l’invio asincrono per fornire questa esperienza con Adaptive Forms.

Nell’invio asincrono, quando un utente invia un modulo, lo sviluppatore del modulo inserisce un’esperienza separata, come il reindirizzamento ad un altro modulo o a una sezione separata del sito web. L’autore può anche collegare servizi separati come l’invio di dati a un archivio dati diverso o aggiungere un motore di analisi personalizzato. In caso di invio asincrono, un modulo adattivo si comporta come un’applicazione a pagina singola, in quanto il modulo non viene ricaricato o il relativo URL non cambia quando i dati del modulo inviati vengono convalidati sul server.

Continua a leggere per i dettagli sull’invio asincrono in Adaptive Forms.

## Configurare l’invio asincrono {#configure}

Per configurare l’invio asincrono per un modulo adattivo:

1. In modalità di creazione del modulo adattivo, seleziona l’oggetto Contenitore modulo e tocca ![cmppr1](assets/configure-icon.svg) per aprire le relative proprietà.
1. In **[!UICONTROL Invio]** sezione proprietà, abilita **[!UICONTROL Utilizzare l’invio asincrono]**.
1. In **[!UICONTROL Al momento dell’invio]** selezionare una delle opzioni seguenti da eseguire in caso di invio corretto del modulo.

   * **[!UICONTROL Reindirizzare a URL]**: Reindirizza all’URL o alla pagina specificati all’invio del modulo. Puoi specificare un URL o sfogliare per scegliere il percorso di una pagina nel **[!UICONTROL URL/percorso di reindirizzamento]** campo .
   * **[!UICONTROL Mostra messaggio]**: Visualizza un messaggio all’invio del modulo. Puoi scrivere un messaggio nel campo di testo sotto il campo **[!UICONTROL Mostra messaggio]** opzione . Il campo di testo supporta la formattazione RTF.

1. Tocca ![pulsante di spunta1](assets/save_icon.svg) per salvare le proprietà.

## Funzionamento dell’invio asincrono {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] fornisce gestori di errori e di successo preconfigurati per l’invio dei moduli. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un modulo viene inviato, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull’evento riuscito o di errore per l’invio. Le informazioni vengono passate come parametri al gestore pertinente per eseguire la funzione .

Inoltre, gli autori e gli sviluppatori dei moduli possono scrivere regole a livello di modulo per ignorare i gestori predefiniti. Per ulteriori informazioni, consulta [Ignora gestori predefiniti utilizzando le regole](#custom).

Esaminiamo innanzitutto la risposta del server per gli eventi di successo ed errore.

### Risposta del server per l&#39;invio dell&#39;evento di successo {#server-response-for-submission-success-event}

La struttura della risposta del server per l’evento di successo dell’invio è la seguente:

```json
{oneOf: [
{  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouOption : {type : "string"}
   }},
  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouContent: {type: "string"}
   }
]

}
```

La risposta del server in caso di invio corretto del modulo include:

* Tipo di formato dei dati del modulo: XML o JSON
* Dati modulo in formato XML o JSON
* Opzione selezionata per reindirizzare a una pagina o visualizzare un messaggio come configurato nel modulo
* URL della pagina o contenuto del messaggio configurato nel modulo

Il gestore di successo legge la risposta del server e quindi reindirizza all’URL della pagina configurato o visualizza un messaggio.

### Risposta del server all’evento di errore di invio {#server-response-for-submission-error-event}

La struttura per la risposta del server all&#39;evento di errore di invio è la seguente:

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

La risposta del server in caso di errore nell’invio del modulo include:

* Motivo dell’errore, convalida CAPTCHA non riuscita o convalida lato server
* Elenco degli oggetti errore, che include l&#39;espressione SOM del campo che non ha superato la convalida e il messaggio di errore corrispondente

Il gestore errori legge la risposta del server e visualizza di conseguenza il messaggio di errore sul modulo.

## Ignora gestori predefiniti utilizzando le regole {#custom}

Gli sviluppatori e gli autori di moduli possono scrivere regole a livello di modulo per ignorare i gestori predefiniti. La risposta del server per gli eventi di successo ed errore è esposta a livello di modulo, a cui gli sviluppatori possono accedere utilizzando `$event.data` nelle regole.

Esegui i seguenti passaggi per scrivere regole per gestire eventi di successo ed errore.

1. Apri il modulo adattivo in modalità di creazione, seleziona un oggetto modulo qualsiasi e tocca ![edit-rules1](assets/edit-rules-icon.svg) per aprire l’editor di regole.
1. Seleziona **[!UICONTROL Modulo]** nell’albero Oggetti modulo e toccare **[!UICONTROL Crea]**.
1. Scegli **[!UICONTROL invio completato]** o **[!UICONTROL errore di invio]** dal **[!UICONTROL Seleziona stato]** elenco a discesa.
1. Definire un **[!UICONTROL Then]** per lo stato selezionato. Ad esempio, seleziona **[!UICONTROL Passa a]** quindi digita o incolla un URL. È inoltre possibile trascinare qualsiasi funzione utilizzando **[!UICONTROL Funzioni]** alla regola.

   ![handler di invio riuscito](assets/form-submission-handler.png)

1. Tocca **[!UICONTROL Fine]** per salvare la regola.
