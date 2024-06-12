---
title: Guida introduttiva all’editor universale in AEM
description: Scopri come accedere all’editor universale e come iniziare a preparare la tua prima app AEM per utilizzarla.
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 395cb7b2e37c7358baa7ae07329f42bd5a560cb1
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 68%

---


# Guida introduttiva all’editor universale in AEM {#getting-started}

Scopri come accedere all’editor universale e come iniziare a preparare la tua prima app AEM per utilizzarla.

>[!TIP]
>
>Se preferisci approfondire direttamente un esempio, puoi rivedere l’[app di esempio dell’editor universale su GitHub.](https://github.com/adobe/universal-editor-sample-editable-app)

## Passaggi di onboarding {#onboarding}

Anche se l’editor universale può modificare il contenuto da qualsiasi origine, questo documento utilizza un’app AEM come esempio.

Puoi eseguire diversi passaggi per onboarding dell’app AEM e strumentazione per l’utilizzo dell’editor universale.

1. [Includi la libreria principale dell’editor universale.](#core-library)
1. [Aggiungi la configurazione OSGi necessaria.](#osgi-configurations)
1. [Prepara la pagina.](#instrument-page)

Questo documento ti guiderà attraverso questi passaggi.

## Includi la libreria principale dell’editor universale {#core-library}

Prima che l’app possa essere instrumentata per l’utilizzo con l’editor universale, deve includere la seguente dipendenza.

```javascript
@adobe/universal-editor-cors
```

Per attivare la strumentazione, è necessario aggiungere la seguente importazione alla `index.js`.

```javascript
import "@adobe/universal-editor-cors";
```

### Alternativa per le app non React {#alternative}

Se non implementi un’app React e/o non richiedi il rendering lato server, un metodo alternativo consiste nell’includere quanto segue nel corpo del documento.

```html
<script src="https://universal-editor-service.experiencecloud.live/corslib/LATEST" async></script>
```

Si consiglia sempre di utilizzare la versione più recente, ma è possibile fare riferimento alle versioni precedenti del servizio in caso di modifiche che causano interruzioni.

* `https://universal-editor-service.experiencecloud.live/corslib/LATEST` - L&#39;ultima libreria EU CORS
* `https://universal-editor-service.experiencecloud.live/corslib/2/LATEST` - L’ultima libreria UE CORS nella versione 2.x
* `https://universal-editor-service.experiencecloud.live/corslib/2.1/LATEST` - L’ultima libreria UE CORS nella versione 2.1.x
* `https://universal-editor-service.experiencecloud.live/corslib/2.1.1`- La libreria UE CORS versione 2.1.1

## Aggiungi le configurazioni OSGi necessarie {#osgi-configurations}

Per poter modificare il contenuto di AEM con l’app utilizzando l’editor universale, le impostazioni CORS e cookie devono essere eseguiti in AEM.

Le seguenti [configurazioni OSGi devono essere impostate sull’istanza di authoring di AEM.](/help/implementing/deploying/configuring-osgi.md)

* `SameSite Cookies = None` in `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`
* Rimuovi X-FRAME-OPTIONS: intestazione SAMEORIGIN in `org.apache.sling.engine.impl.SlingMainServlet`

### com.day.crx.security.token.impl.impl.TokenAuthenticationHandler {#samesite-cookies}

Il cookie del token di accesso deve essere inviato ad AEM come dominio di terze parti. Pertanto, il cookie dello stesso sito deve essere impostato esplicitamente su `None`.

Questa proprietà deve essere impostata nella configurazione OSGi `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
          token.samesite.cookie.attr="None" />
```

### org.apache.sling.engine.impl.SlingMainServlet {#sameorigin}

X-Frame-Options: SAMEORIGIN impedisce il rendering di pagine AEM all’interno di un iframe. La rimozione dell’intestazione consente di caricare le pagine.

Questa proprietà deve essere impostata nella configurazione OSGi `org.apache.sling.engine.impl.SlingMainServlet`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
          jcr:primaryType="sling:OsgiConfig"
          sling.additional.response.headers="[X-Content-Type-Options=nosniff]"/>
```

## Prepara la pagina {#instrument-page}

Il servizio di editor universale richiede un [nome risorsa uniforme (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) per identificare e utilizzare il sistema back-end corretto per il contenuto dell’app in fase di modifica. Pertanto, è necessario uno schema URN per mappare il contenuto alle risorse di contenuto.

### Creazione di connessioni {#connections}

Le connessioni utilizzate nell’app vengono memorizzate come `<meta>` tag nella pagina `<head>`.

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>` - Questa è una classificazione della connessione con due opzioni.
   * `system` - Per endpoint di connessione
   * `config` - Per [definizione delle impostazioni di configurazione facoltative](#configuration-settings)
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

È possibile utilizzare `config` Prefisso nell’URN della connessione per impostare gli endpoint del servizio e dell’estensione, se necessario.

Se non desideri utilizzare il servizio Universal Editor, ospitato da Adobe, ma la tua versione ospitata, puoi impostarlo in un tag meta. Per sovrascrivere l&#39;endpoint di servizio predefinito fornito da Universal Editor, impostare un endpoint di servizio personalizzato:

* Nome metadati - `urn:adobe:aue:config:service`
* Metadati - `content="https://adobe.com"` (esempio)

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

Se desideri abilitare solo alcune estensioni per una pagina, puoi impostarle in un tag meta. Per recuperare le estensioni, imposta gli endpoint dell&#39;estensione:

* Nome metadati: `urn:adobe:aue:config:extensions`
* Metadati: `content="https://adobe.com,https://anotherone.com,https://onemore.com"` (esempio)

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
* [Pubblicazione di contenuti con l’editor universale](/help/sites-cloud/authoring/universal-editor/publishing.md) - Scopri come l’Editor universale pubblica i contenuti e come le app possono gestire i contenuti pubblicati.
* [Architettura dell’editor universale](architecture.md): scopri l’architettura dell’editor universale e come avviene il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](authentication.md): scopri come l’editor universale effettua l’autenticazione.

