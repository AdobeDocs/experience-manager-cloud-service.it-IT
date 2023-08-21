---
title: Configurare l’invio asincrono del Forms adattivo dell’AEM
description: Scopri come configurare l’invio asincrono per Adaptive Forms. Approfondisci il funzionamento dell’invio asincrono per Adaptive Forms.
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: b8366fc19a89582f195778c92278cc1e15b15617
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 1%

---

# Configurare l’invio asincrono del Forms adattivo dell’AEM {#asynchronous-submission-of-adaptive-forms}


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/asynchronous-submissions-adaptive-forms.html) |
| AEM as a Cloud Service | Questo articolo |


In genere, i moduli web sono configurati per l’invio sincrono. Nell’invio sincrono, quando gli utenti inviano un modulo vengono reindirizzati a una pagina di conferma, a una pagina di ringraziamento oppure, in caso di invio non riuscito, a una pagina di errore. Tuttavia, le moderne esperienze web come le applicazioni a pagina singola stanno guadagnando popolarità, dove la pagina web rimane statica mentre l’interazione client-server avviene in background. Puoi configurare l’invio asincrono per fornire questa esperienza con Adaptive Forms.

Nell’invio asincrono, quando un utente invia un modulo, lo sviluppatore del modulo inserisce un’esperienza separata, ad esempio il reindirizzamento verso un altro modulo o una sezione separata del sito web. L’autore può anche inserire servizi separati come l’invio di dati a un altro archivio dati o aggiungere un motore di analisi personalizzato. In caso di invio asincrono, un modulo adattivo si comporta come un’applicazione a pagina singola in quanto il modulo non viene ricaricato o il suo URL non cambia quando i dati del modulo inviati vengono convalidati sul server.

Continua a leggere per i dettagli sull’invio asincrono in Adaptive Forms.

## Configurare l’invio asincrono {#configure}

Per configurare l’invio asincrono per un modulo adattivo:

1. In modalità di authoring di moduli adattivi, seleziona l’oggetto Contenitore modulo e tocca ![cmppr1](assets/configure-icon.svg) per aprirne le proprietà.
1. In **[!UICONTROL Invio]** proprietà, abilita **[!UICONTROL Utilizzare l’invio asincrono]**.
1. In **[!UICONTROL All’invio]** , selezionare una delle opzioni seguenti da eseguire in caso di invio corretto del modulo.

   * **[!UICONTROL Reindirizza a URL]**: reindirizza all’URL o alla pagina specificata al momento dell’invio del modulo. Puoi specificare un URL o sfogliare per scegliere il percorso di una pagina in **[!UICONTROL URL/percorso di reindirizzamento]** campo.
   * **[!UICONTROL Mostra messaggio]**: visualizza un messaggio all’invio del modulo. È possibile scrivere un messaggio nel campo di testo sotto **[!UICONTROL Mostra messaggio]** opzione. Il campo di testo supporta la formattazione RTF.

1. Tocca ![check-button1](assets/save_icon.svg) per salvare le proprietà.

## Funzionamento dell’invio asincrono {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] fornisce gestori predefiniti di errori e operazioni riuscite per l’invio dei moduli. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un modulo viene inviato, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull’evento di successo o errore per l’invio. Le informazioni vengono passate come parametri al gestore pertinente per eseguire la funzione.

Inoltre, gli autori e gli sviluppatori di moduli possono scrivere regole a livello di modulo per ignorare i gestori predefiniti. Per ulteriori informazioni, consulta [Ignora gestori predefiniti tramite regole](#custom).

Esaminiamo innanzitutto la risposta del server per gli eventi di successo e di errore.

### Risposta del server per l’evento di successo dell’invio {#server-response-for-submission-success-event}

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

* Tipo di formato dati modulo: XML o JSON
* Dati modulo in formato XML o JSON
* Opzione selezionata per reindirizzare a una pagina o visualizzare un messaggio come configurato nel modulo
* Contenuto dell’URL della pagina o del messaggio configurato nel modulo

Il gestore dei processi riusciti legge la risposta del server e di conseguenza reindirizza all’URL della pagina configurato o visualizza un messaggio.

### Risposta del server per l’evento di errore di invio {#server-response-for-submission-error-event}

La struttura della risposta del server per l’evento di errore di invio è la seguente:

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

* Motivo dell’errore, convalida CAPTCHA o lato server non riuscita
* Elenco di oggetti errore, che include l&#39;espressione SOM del campo che non ha superato la convalida e il messaggio di errore corrispondente

Il gestore degli errori legge la risposta del server e visualizza di conseguenza il messaggio di errore nel modulo.

## Ignora gestori predefiniti tramite regole {#custom}

Gli sviluppatori e gli autori di moduli possono scrivere regole a livello di modulo per ignorare i gestori predefiniti. La risposta del server per eventi di successo ed errore viene esposta a livello di modulo, a cui gli sviluppatori possono accedere utilizzando `$event.data` nelle regole.

Per scrivere regole per gestire eventi di successo e di errore, effettua le seguenti operazioni.

1. Apri il modulo adattivo in modalità di authoring, seleziona un oggetto modulo qualsiasi e tocca ![edit-rules1](assets/edit-rules-icon.svg) per aprire l’editor di regole.
1. Seleziona **[!UICONTROL Modulo]** nella struttura Oggetti modulo e tocca **[!UICONTROL Crea]**.
1. Scegli **[!UICONTROL è stato inviato correttamente]** o **[!UICONTROL invio non riuscito]** dal **[!UICONTROL Seleziona stato]** elenco a discesa.
1. Definisci un **[!UICONTROL Then]** azione per lo stato selezionato. Ad esempio, seleziona **[!UICONTROL Accedi a]** e quindi digita o incolla un URL. È inoltre possibile trascinare qualsiasi funzione utilizzando **[!UICONTROL Funzioni]** alla regola.

   ![gestore invio riuscito](assets/form-submission-handler.png)

1. Tocca **[!UICONTROL Fine]** per salvare la regola.
