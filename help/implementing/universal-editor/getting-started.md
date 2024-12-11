---
title: Guida introduttiva all’editor universale in AEM
description: Scopri come accedere all’editor universale e come iniziare a preparare la tua prima app AEM per utilizzarla.
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 8357caf2b0d396f6a1bd7b6160d6b48d8d6c026c
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 62%

---


# Guida introduttiva all’editor universale in AEM {#getting-started}

Scopri come accedere all’editor universale e come iniziare a preparare la tua prima app AEM per utilizzarla.

>[!TIP]
>
>Se preferisci approfondire direttamente un esempio, puoi rivedere l’[app di esempio dell’editor universale su GitHub.](https://github.com/adobe/universal-editor-sample-editable-app)

Sebbene Universal Editor possa modificare il contenuto da qualsiasi origine, questo documento utilizzerà come esempio un’app AEM. Questo documento ti guiderà attraverso questi passaggi.

## Prepara la pagina {#instrument-page}

Per eseguire il rendering e la modifica della pagina nell’editor universale è necessaria una libreria JavaScript.

Il servizio Universal Editor richiede inoltre un URN [per identificare e utilizzare il sistema di back-end corretto per il contenuto dell&#39;app da modificare. ](https://en.wikipedia.org/wiki/Uniform_Resource_Name) Pertanto, è necessario uno schema URN per mappare il contenuto alle risorse di contenuto.

### Includi la libreria CORS di Universal Editor {#cors-library}

Per consentire all&#39;editor universale di connettersi all&#39;app, l&#39;app deve includere la libreria CORS dell&#39;editor universale. Aggiungi il seguente script all’app.

```html
 <script src="https://universal-editor-service.adobe.io/cors.js" async></script>
```

### Creazione di connessioni {#connections}

Le connessioni utilizzate nell’app vengono memorizzate come `<meta>` tag nella pagina `<head>`.

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>` - Classificazione della connessione con due opzioni.
   * `system` - Per endpoint di connessione
   * `config` - Per [definire impostazioni di configurazione facoltative](#configuration-settings)
* `<referenceName>`: questo è un nome breve che viene utilizzato nuovamente nel documento per identificare la connessione. Ad esempio, `aemconnection`.
* `<protocol>`: indica il plug-in di persistenza del servizio di persistenza dell’editor universale da utilizzare. Ad esempio, `aem`
* `<url>`: questo è l’URL del sistema in cui le modifiche devono essere mantenute. Ad esempio, `http://localhost:4502`

L’identificatore `urn:adobe:aue:system` rappresenta la connessione per Adobe Universal Editor.

Negli identificatori `data-aue-resource` verrà utilizzato il prefisso `urn` per accorciare l’identificatore.

```html
data-aue-resource="urn:<referenceName>:<resource>"
```

* `<referenceName>`: questo è il riferimento menzionato nel tag `<meta>`. Ad esempio, `aemconnection`.
* `<resource>`: questo è un puntatore verso la risorsa nel sistema di destinazione. Ad esempio, un percorso di contenuto AEM come `/content/page/jcr:content`

>[!TIP]
>
>Per ulteriori dettagli sugli attributi e i tipi di dati richiesti dall’editor universale, consulta [Attributi e tipi](attributes-types.md).

### Connessione di esempio {#example}

```html
<meta name="urn:adobe:aue:system:<referenceName>" content="<protocol>:<url>">

<html>
<head>
    <meta name="urn:adobe:aue:system:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:adobe:aue:system:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul data-aue-resource="urn:aemconnection:/content/example/list" data-aue-type="container">
            <li data-aue-resource="urn:aemconnection:/content/example/listitem" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">Jane Doe</p>
              <p data-aue-prop="title" data-aue-type="text">Journalist</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>

...

            <li data-aue-resource="urn:fcsconnection:/documents/mytext" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">John Smith</p>
              <p data-aue-resource="urn:aemconnection:/content/example/another-source" data-aue-prop="title" data-aue-type="text">Photographer</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### Impostazioni di configurazione {#configuration-settings}

È possibile utilizzare il prefisso `config` nell&#39;URN della connessione per impostare gli endpoint del servizio e dell&#39;estensione, se necessario.

Se non desideri utilizzare il servizio Universal Editor, ospitato da Adobe, ma la tua versione ospitata, puoi impostarlo in un tag meta. Per sovrascrivere l&#39;endpoint di servizio predefinito fornito da Universal Editor, impostare un endpoint di servizio personalizzato:

* Nome metadati - `urn:adobe:aue:config:service`
* Meta content - `content="https://adobe.com"` (esempio)

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

Se desideri abilitare solo alcune estensioni per una pagina, puoi impostarle in un tag meta. Per recuperare le estensioni, imposta gli endpoint dell&#39;estensione:

* Nome metadati: `urn:adobe:aue:config:extensions`
* Contenuto metadati: `content="https://adobe.com,https://anotherone.com,https://onemore.com"` (esempio)

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## Iniziare a utilizzare l’editor universale {#youre-ready}

L’app è ora preparata per l’utilizzo dell’editor universale.

Consulta [Authoring dei contenuti con l’editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md) per scoprire quanto è semplice e intuitivo per gli autori creare contenuti utilizzando l’editor universale.

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md): scopri come l’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Authoring dei contenuti con l’editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md): scopri quanto è semplice e intuitivo per gli autori di contenuto creare contenuto utilizzando l’editor universale.
* [Pubblicazione di contenuti con l&#39;editor universale](/help/sites-cloud/authoring/universal-editor/publishing.md) - Scopri come l&#39;editor universale pubblica i contenuti e come le app possono gestire i contenuti pubblicati.
* [Architettura dell’editor universale](architecture.md): scopri l’architettura dell’editor universale e come avviene il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](authentication.md): scopri come l’editor universale effettua l’autenticazione.

