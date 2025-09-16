---
title: Guida introduttiva all’editor universale in AEM
description: Scopri come accedere all’editor universale e come iniziare a preparare la tua prima app AEM per utilizzarla.
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: c4dcb1cecb756f746ecb856fcfd65d73833a5ee0
workflow-type: ht
source-wordcount: '979'
ht-degree: 100%

---


# Guida introduttiva all’editor universale in AEM {#getting-started}

Scopri come accedere all’editor universale e come iniziare a preparare la tua prima app AEM per utilizzarla.

>[!TIP]
>
>Se preferisci approfondire direttamente un esempio, puoi rivedere l’[app di esempio dell’editor universale su GitHub](https://github.com/adobe/universal-editor-sample-editable-app).

Anche se l’editor universale può modificare il contenuto da qualsiasi origine, questo documento utilizza un’app AEM come esempio. Questo documento ti guiderà attraverso questi passaggi.

## Preparare la pagina {#instrument-page}

Per eseguire il rendering e la modifica della pagina nell’editor, è necessaria una libreria JavaScript nell’editor universale.

Inoltre, il servizio di editor universale richiede un [nome di risorsa uniforme (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) per identificare e utilizzare il sistema di back-end corretto per il contenuto dell’app in fase di modifica. Pertanto, è necessario uno schema URN per mappare nuovamente il contenuto sulle risorse di contenuto.

### Includere la libreria CORS dell’editor universale {#cors-library}

Per consentire all’editor universale di connettersi all’app, l’app deve includere la libreria CORS dell’editor universale. Aggiungi il seguente script all’app.

```html
 <script src="https://universal-editor-service.adobe.io/cors.js" async></script>
```

### Creazione di connessioni {#connections}

Le connessioni utilizzate nell’app vengono memorizzate come `<meta>` tag nella pagina `<head>`.

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>`: classificazione della connessione con due opzioni.
   * `system`: per endpoint di connessione
   * `config`: per [definire impostazioni di configurazione facoltative](#configuration-settings)
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

Puoi utilizzare il prefisso `config` nell’URN della connessione per impostare gli endpoint del servizio e dell’estensione, se necessario.

Se non desideri utilizzare il servizio editor universale, ospitato da Adobe, ma la tua versione ospitata, puoi impostarlo in un meta tag. Per sovrascrivere l’endpoint di servizio predefinito fornito dall’editor universale, imposta un endpoint di servizio personalizzato:

* Meta name: `urn:adobe:aue:config:service`
* Meta content: `content="https://adobe.com"` (esempio)

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

Se desideri abilitare solo alcune estensioni per una pagina, puoi impostarle in un meta tag. Per recuperare le estensioni, imposta gli endpoint dell’estensione:

* Meta name: `urn:adobe:aue:config:extensions`
* Meta content: `content="https://adobe.com,https://anotherone.com,https://onemore.com"` (esempio)

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## Definisci per quali percorsi di contenuto o `sling:resourceType`s deve essere aperto l’editor universale. Facoltativo {#content-paths}

Se disponi di un progetto AEM esistente che utilizza [l’editor pagina](/help/sites-cloud/authoring/page-editor/introduction.md), quando gli autori di contenuto modificano le pagine, queste vengono aperte automaticamente con l’editor pagina. Puoi definire quale editor AEM aprire in base ai percorsi dei contenuti o a `sling:resourceType`, semplificando così l’esperienza per gli autori, indipendentemente dall’editor richiesto per il contenuto selezionato.

1. Apri Configuration Manager.

   `http://<host>:<port>/system/console/configMgr`

1. Individua il **Servizio URL editor universale** nell’elenco e fai clic su **Modifica i valori di configurazione**.

1. Definisci per quali percorsi di contenuto o `sling:resourceType`s deve essere aperto l’editor universale.

   * Nel campo **Universal Editor Opening Mapping**, specifica i percorsi per i quali è aperto l’editor universale.
   * Nel campo **Sling:resourceTypes che verrà aperto dall’editor universale**, fornisci un elenco di risorse aperte direttamente dall’editor universale.

1. Fai clic su **Salva**.

1. Controlla la [configurazione di Externalizer](/help/implementing/developing/tools/externalizer.md) e assicurati di disporre almeno degli ambienti locale, di authoring e di pubblicazione impostati come nell’esempio seguente.

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

Una volta completati questi passaggi di configurazione, AEM aprirà l’editor universale per le pagine nell’ordine seguente.

1. AEM controllerà le mappature in `Universal Editor Opening Mapping` e se il contenuto si trova in uno dei percorsi qui definiti, verrà aperto l’editor universale.
1. Per i contenuti non inclusi nei percorsi definiti in `Universal Editor Opening Mapping`, AEM controlla se il `resourceType` dei contenuti corrisponde a quelli definiti in **Sling:resourceTypes che verranno aperti dall’editor universale** e se i contenuti corrispondono a uno di questi tipi, l’editor universale verrà aperto in `${author}${path}.html`.
1. In caso contrario, AEM apre l’editor pagina.

Per definire le mappature nel campo **Universal Editor Opening Mapping** sono disponibili le seguenti variabili.

* `path`: percorso del contenuto della risorsa da aprire
* `localhost`: voce Externalizer per `localhost` senza schema, ad esempio `localhost:4502`
* `author`: voce Externalizer per autore senza schema, ad esempio `localhost:4502`
* `publish`: voce Externalizer per la pubblicazione senza schema, ad esempio `localhost:4503`
* `preview`: voce Externalizer per l’anteprima senza schema, ad esempio `localhost:4504`
* `env`: `prod`, `stage`, `dev` in base alle modalità di esecuzione definite di Sling
* `token`: token di query richiesto per `QueryTokenAuthenticationHandler`

### Mappature di esempio {#example-mappings}

* Apri tutte le pagine in `/content/foo` su Author di AEM:

   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Ciò comporta l’apertura di `https://localhost:4502/content/foo/x.html?login-token=<token>`

* Apri tutte le pagine in `/content/bar` su un server NextJS remoto, fornendo come informazioni tutte le variabili:

   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Ciò comporta l’apertura di `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

## Iniziare a utilizzare l’editor universale {#youre-ready}

L’app è ora preparata per l’utilizzo dell’editor universale.

Consulta [Authoring dei contenuti con l’editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md) per scoprire quanto è semplice e intuitivo per gli autori creare contenuti utilizzando l’editor universale.

{{ue-headless-auth}}

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md): scopri come l’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Authoring dei contenuti con l’editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md): scopri quanto è semplice e intuitivo per gli autori creare contenuto utilizzando l’editor universale.
* [Pubblicazione di contenuti con l’editor universale](/help/implementing/universal-editor/publishing.md): scopri in che modo l’editor universale pubblica i contenuti e in che modo le app possono gestire i contenuti pubblicati.
* [Architettura dell’editor universale](architecture.md): scopri l’architettura dell’editor universale e come avviene il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](authentication.md): scopri come l’editor universale effettua l’autenticazione.

