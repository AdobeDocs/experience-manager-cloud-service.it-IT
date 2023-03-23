---
title: Guida introduttiva all’Editor universale in AEM
description: Scopri come accedere all’editor universale e come iniziare a strumentalizzare la tua prima app AEM per utilizzarla.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# Guida introduttiva all’Editor universale in AEM {#getting-started}

Scopri come accedere all’editor universale e come iniziare a strumentalizzare la tua prima app AEM per utilizzarla.

>[!TIP]
>
>Se preferisci immergerti direttamente in un esempio, puoi rivedere il [App di esempio dell’editor universale su GitHub.](https://github.com/adobe/universal-editor-sample-editable-app)

## Passaggi di onboarding {#onboarding}

Anche se l’editor universale può modificare il contenuto da qualsiasi origine, questo documento utilizza un’app AEM come esempio.

Sono disponibili diversi passaggi per l’onboarding dell’app AEM e la strumentazione per l’utilizzo dell’editor universale.

1. [Richiedi l’accesso all’Editor universale.](#request-access)
1. [Includere la libreria principale dell’Editor universale.](#core-library)
1. [Aggiungi la configurazione OSGi necessaria.](#osgi-configurations)
1. [Strumento la pagina.](#instrument-page)

Questo documento ti guiderà attraverso questi passaggi.

## Richiedere l’accesso all’editor universale {#request-access}

È innanzitutto necessario richiedere l’accesso all’Editor universale. Per favore, vai a [https://experience.adobe.com/#/aem/editor](https://experience.adobe.com/#/aem/editor) e verifica se hai accesso all’Editor universale.

Se non disponi di accesso, può essere richiesto tramite un modulo collegato sulla stessa pagina.

## Includere la libreria core dell’editor universale {#core-library}

Prima di poter strumentalizzare l’app con l’Editor universale, è necessario includere la seguente dipendenza.

```javascript
@adobe/universal-editor-cors
```

Per attivare la strumentazione, è necessario aggiungere la seguente importazione al `index.js`.

```javascript
import "@adobe/universal-editor-cors";
```

### Alternativa per le app non React {#alternative}

Se non stai implementando un’app React e/o hai bisogno di eseguire il rendering lato server, un metodo alternativo consiste nell’includere quanto segue nel corpo del documento.

```html
<script src="https://cdn.jsdelivr.net/gh/adobe/universal-editor-cors/dist/universal-editor-embedded.js" async></script>
```

## Aggiungere le configurazioni OSGi necessarie {#osgi-configurations}

Per poter modificare AEM contenuto con l’app utilizzando l’Editor universale, le impostazioni CORS e cookie devono essere eseguite in AEM.

I seguenti [Le configurazioni OSGi devono essere impostate sull’istanza di authoring AEM.](/help/implementing/deploying/configuring-osgi.md)

* `SameSite Cookies = None` in `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`
* Rimuovi gli OPTIONS X-FRAME: Intestazione SAMEORIGIN in `org.apache.sling.engine.impl.SlingMainServlet`

### com.day.crx.security.token.impl.impl.TokenAuthenticationHandler {#samesite-cookies}

Il cookie del token di accesso deve essere inviato a AEM come dominio di terze parti. Pertanto, il cookie dello stesso sito deve essere impostato esplicitamente su `None`.

Questa proprietà deve essere impostata nel `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler` Configurazione OSGi.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
          token.samesite.cookie.attr="None" />
```

### org.apache.sling.engine.impl.SlingMainServlet {#sameorigin}

Opzioni X-Frame: SAMEORIGIN impedisce il rendering AEM pagine all’interno di un iframe. La rimozione dell’intestazione consente di caricare le pagine.

Questa proprietà deve essere impostata nel `org.apache.sling.engine.impl.SlingMainServlet` Configurazione OSGi.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
          jcr:primaryType="sling:OsgiConfig"
          sling.additional.response.headers="[X-Content-Type-Options=nosniff]"/>
```

## Strumento la pagina {#instrument-page}

Il servizio Universal Editor richiede un [nome risorsa uniforme (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) per identificare e utilizzare il sistema backend corretto per il contenuto dell’app in fase di modifica. Pertanto, è necessario uno schema URN per mappare il contenuto alle risorse di contenuto.

Gli attributi della strumentazione aggiunti alla pagina sono costituiti per lo più da [Microdati HTML,](https://developer.mozilla.org/en-US/docs/Web/HTML/Microdata) uno standard di settore che può essere utilizzato anche per rendere HTML più semantico, rendere i documenti HTML indicizzabili, ecc.

### Creazione di connessioni {#connections}

Le connessioni utilizzate nell&#39;app vengono memorizzate come `<meta>` tag nella pagina `<head>`.

```html
<meta name="urn:auecon:<referenceName>" content="<protocol>:<url>">
```

* `<referenceName>` - Questo è un nome breve che viene riutilizzato nel documento per identificare la connessione. Ad esempio `aemconnection`
* `<protocol>` - Indica il plug-in di persistenza del servizio di persistenza Universal Editor da utilizzare. Ad esempio `aem`
* `<url>` - Questo è l&#39;URL del sistema in cui le modifiche devono essere mantenute. Ad esempio `http://localhost:4502`

Identificatore breve `auecon` sta per Adobe Universal Editor Connection.

`itemid`s utilizzerà `urn` Prefisso per accorciare l&#39;identificatore.

```html
itemid="urn:<referenceName>:<resource>"
```

* `<referenceName>` - Questo è il riferimento menzionato nel `<meta>` tag . Ad esempio `aemconnection`
* `<resource>` - Questo è un puntatore alla risorsa nel sistema di destinazione. Ad esempio, un percorso di contenuto AEM come `/content/page/jcr:content`

>[!TIP]
>
>Vedere il documento [Attributi e tipi](attributes-types.md) per ulteriori dettagli sugli attributi e i tipi di dati richiesti dall’Editor universale.

### Esempio di connessione {#example}

```html
<html>
<head>
    <meta name="urn:auecon:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:auecon:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="container">
            <li itemscope itemid="urn:aemconnection/content/example/listitem" itemtype="component">
              <p itemprop="name" itemtype="text">Jane Doe</p>
              <p itemprop="title" itemtype="text">Journalist</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
 
...
 
            <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="component">
              <p itemprop="name" itemtype="text">John Smith</p>
              <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

## Sei pronto per l’utilizzo dell’editor universale {#youre-ready}

L’app è ora strumentalizzata per l’utilizzo dell’editor universale.

Fare riferimento al documento [Creazione di contenuti con l’editor universale](authoring.md) per scoprire quanto sia semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’Editor universale.

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md) - Scopri come l’editor universale consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare i contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Creazione di contenuti con l’editor universale](authoring.md) - Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’Editor universale.
* [Pubblicazione di contenuti con l’editor universale](publishing.md) - Scopri in che modo Universal Visual Editor pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.
* [Architettura dell’editor universale](architecture.md) - Scopri l’architettura dell’Editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md) - Scopri gli attributi e i tipi di dati richiesti dall’Editor universale.
* [Autenticazione dell’editor universale](authentication.md) - Scopri come l’editor universale si autentica.
