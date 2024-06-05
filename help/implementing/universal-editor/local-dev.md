---
title: Sviluppo locale AEM con l’editor universale
description: Scopri in che modo Universal Editor supporta la modifica sulle istanze AEM locali a scopo di sviluppo.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 2%

---


# Sviluppo locale AEM con l’editor universale {#local-dev-ue}

Scopri in che modo Universal Editor supporta la modifica sulle istanze AEM locali a scopo di sviluppo.

## Panoramica {#overview}

Il servizio Universal Editor è ciò che lega Universal Editor e il sistema di back-end. Per poter sviluppare in locale per Universal Editor, è necessario eseguire una copia locale del servizio. Ciò è dovuto al fatto che:

* Il servizio ufficiale dell’editor universale di Adobe è ospitato a livello globale e l’istanza AEM locale dovrebbe essere esposta a Internet.
* Durante lo sviluppo con un SDK AEM locale, non è possibile accedere al servizio Universal Editor di Adobe da Internet.
* Se l&#39;istanza dell&#39;AEM ha restrizioni IP e il servizio Universal Editor di Adobe non è incluso in un intervallo IP definito, è possibile ospitarlo personalmente.

In questo documento viene illustrato come eseguire AEM in HTTPS insieme a una copia locale del servizio Universal Editor per sviluppare in locale AEM da utilizzare con Universal Editor.

## Configurare AEM per l’esecuzione su HTTPS {#aem-https}

All’interno di un frame esterno protetto con HTTPS non è possibile caricare un frame HTTP non protetto. Il servizio Universal Editor viene eseguito su HTTPS, pertanto anche su HTTPS deve essere eseguito AEM o qualsiasi altra pagina remota.

A questo scopo, devi configurare l’AEM per l’esecuzione su HTTPS. A scopo di sviluppo, puoi utilizzare un certificato autofirmato.

[Consulta questo documento](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=it) su come configurare AEM in esecuzione su HTTPS, incluso un certificato autofirmato, utilizzabile.

## Installare il servizio Universal Editor {#install-ue-service}

Universal Editor Service non è un&#39;intera copia di Universal Editor, ma solo un sottoinsieme delle sue funzioni per garantire che le chiamate dall&#39;ambiente AEM locale non vengano instradate su Internet, ma da un endpoint definito controllato.

[NodeJS versione 16](https://nodejs.org/en/download/releases) è necessario per eseguire una copia locale del servizio Universal Editor.

Il servizio Universal Editor è disponibile tramite Software Distribution. Consulta la sezione [Documentazione di Software Distribution](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=it) per informazioni dettagliate su come accedervi.

Salva il `universal-editor-service.cjs` da Software Distribution all&#39;ambiente di sviluppo locale.

## Creare un certificato per eseguire il servizio Universal Editor con HTTPS {#ue-https}

Il servizio Editor universale richiede inoltre un certificato per l&#39;esecuzione su HTTPS nell&#39;ambiente di sviluppo.

Esegui il comando seguente.

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

Il comando genera un `key.pem` e un `certificate.pem` file. Salva questi file nello stesso percorso del file `universal-editor-service.cjs` file.

## Configurazione del servizio Editor universale {#setting-up-service}

È necessario impostare alcune variabili di ambiente in NodeJS per eseguire il servizio Universal Editor in locale.

Sullo stesso percorso del `universal-editor-service.cjs`, `key.pem` e `certificate.pem` file, crea un `.env` file con il seguente contenuto.

```text
EXPRESS_PORT=8000
EXPRESS_PRIVATE_KEY=./key.pem
EXPRESS_CERT=./certificate.pem
NODE_TLS_REJECT_UNAUTHORIZED=0
```

La variabile ha i seguenti significati:

* `EXPRESS_PORT`: definisce la porta su cui il servizio Universal Editor è in ascolto
* `EXPRESS_PRIVATE`: punta al tuo [chiave privata creata in precedenza,](#ue-https) `key.pem`
* `EXPRESS_CERT`: punta al tuo [certificato creato in precedenza,](#ue-https) `certificate.pem`
* `NODE_TLS_REJECT_UNAUTHORIZED=0`: accetta certificati autofirmati

## Esecuzione del servizio Editor universale {#running-ue}

Per avviare il servizio Universal Editor, eseguire il comando seguente:

```text
$ node ./universal-editor-service.cjs
```

Dovrebbe trasmettere quanto segue al terminale:

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

Verificare che il servizio avvii il server HTTPS e non il server HTTP.

## Utilizzo del servizio Editor universale locale anziché del servizio globale {#using-local-ue}

Universal Editor conosce il servizio Universal Editor da utilizzare per modificare una pagina in base alla strumentazione. Questa operazione viene eseguita tramite i metatag nella pagina caricata nell’editor universale.

Per modificare una pagina con il servizio Universal Editor locale, è necessario impostare il seguente tag meta:

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

Una volta impostata, dovresti vedere ogni chiamata di aggiornamento del contenuto andare a `https://localhost:8000` anziché il servizio Universal Editor predefinito.

>[!NOTE]
>
>Tentativo di accesso diretto `https://localhost:8000` produce un `404` errore. Questo è il comportamento previsto.
>
>Per verificare l&#39;accesso al servizio Universal Editor locale, utilizzare `https://localhost:8000/corslib/LATEST`. Consulta la [sezione successiva](#editing) per i dettagli.

>[!TIP]
>
>Per ulteriori dettagli sulla strumentazione delle pagine per l&#39;utilizzo del servizio Global Universal Editor, consultare il documento [Guida introduttiva dell’Editor universale in AEM](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Modifica di una pagina con il servizio Local Universal Editor {#editing}

Con il [Servizio Universal Editor in esecuzione in locale](#running-ue) e il tuo [pagina di contenuti dotata di strumenti per utilizzare il servizio locale,](#using-loca-ue) ora puoi avviare l’editor.

1. Apri il browser per `https://localhost:8000/corslib/LATEST`.
1. Indica al browser di accettare [il certificato autofirmato.](#ue-https)
1. Una volta che il certificato autofirmato è attendibile, è possibile modificare la pagina utilizzando il servizio Universal Editor locale.

