---
title: Esecuzione del proprio servizio Universal Editor
description: Scopri come eseguire il servizio Universal Editor per lo sviluppo locale o come parte dell’infrastruttura.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 300dc71969e8e1da32d4f86f0a987b7e2777ccf5
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 2%

---


# Esecuzione del proprio servizio Universal Editor {#local-ue-service}

Scopri come eseguire il servizio Universal Editor per lo sviluppo locale o come parte dell’infrastruttura.

>[!NOTE]
>
>I servizi dell&#39;editor universale locale non sono necessari o supportati per i progetti che utilizzano l&#39;authoring AEM con Edge Delivery Services.

## Panoramica {#overview}

Il servizio Universal Editor è ciò che lega Universal Editor e il sistema di back-end. Per poter sviluppare in locale per Universal Editor, è necessario eseguire una copia locale del servizio. Ciò è dovuto al fatto che:

* Il servizio ufficiale dell’editor universale di Adobe è ospitato a livello globale e l’istanza AEM locale dovrebbe essere esposta a Internet.
* Durante lo sviluppo con un SDK AEM locale, non è possibile accedere al servizio Universal Editor di Adobe da Internet.
* Se l&#39;istanza di AEM presenta restrizioni IP e il servizio Universal Editor di Adobe non è incluso in un intervallo IP definito, è possibile ospitarlo personalmente.

## Casi d’uso {#use-cases}

Una copia personalizzata del servizio Universal Editor è utile per:

* Sviluppa localmente su AEM per l’utilizzo con Universal Editor.
* Esegui il servizio Universal Editor come parte dell&#39;infrastruttura, indipendentemente dal servizio Universal Editor di Adobe.

Sono supportati entrambi i casi di utilizzo. Questo documento spiega come eseguire AEM in HTTPS insieme a una copia locale del servizio Universal Editor.

Per eseguire il servizio Universal Editor come parte dell&#39;infrastruttura, è necessario seguire gli stessi passaggi dell&#39;esempio di sviluppo locale.

## Configurare AEM per l’esecuzione su HTTPS {#aem-https}

All’interno di un frame esterno protetto con HTTPS, non è possibile caricare un frame HTTP non sicuro. Il servizio Editor universale viene eseguito su HTTPS, pertanto anche AEM o qualsiasi altra pagina remota deve essere eseguito su HTTPS.

A questo scopo, devi configurare AEM per l’esecuzione su HTTPS. A scopo di sviluppo, puoi utilizzare un certificato autofirmato.

[Consulta questo documento](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=it) su come configurare AEM in esecuzione su HTTPS, incluso un certificato autofirmato utilizzabile.

## Installare il servizio Universal Editor {#install-ue-service}

Universal Editor Service non è un&#39;intera copia di Universal Editor, ma solo un sottoinsieme delle sue funzioni per garantire che le chiamate dall&#39;ambiente AEM locale non vengano instradate su Internet, ma da un endpoint definito controllato.

Per eseguire una copia locale del servizio Editor universale è necessario [NodeJS versione 20](https://nodejs.org/en/download/releases).

Il servizio Universal Editor è disponibile tramite Software Distribution. Per informazioni dettagliate su come accedervi, consultare la [documentazione sulla distribuzione software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=it).

Salvare il file `universal-editor-service.cjs` da Distribuzione software nell&#39;ambiente di sviluppo locale.

## Creare un certificato per eseguire il servizio Universal Editor con HTTPS {#ue-https}

Il servizio Editor universale richiede inoltre un certificato per l&#39;esecuzione su HTTPS nell&#39;ambiente di sviluppo.

Esegui il comando seguente.

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

Il comando genera un file `key.pem` e un file `certificate.pem`. Salvare questi file nello stesso percorso del file `universal-editor-service.cjs`.

## Configurazione del servizio Universal Editor {#setting-up-service}

È necessario impostare alcune variabili di ambiente in NodeJS per eseguire il servizio Universal Editor in locale.

Nello stesso percorso dei file `universal-editor-service.cjs`, `key.pem` e `certificate.pem`, creare un file `.env` con il contenuto seguente.

```text
UES_PORT=8000
UES_PRIVATE_KEY=./key.pem
UES_CERT=./certificate.pem
UES_TLS_REJECT_UNAUTHORIZED=false
UES_CORS_PRIVATE_NETWORK=true
```

Nel nostro esempio, questi sono i valori minimi richiesti per lo sviluppo locale.

>[!NOTE]
>
>Se si esegue Chrome versione 130+, è necessario abilitare l&#39;invio di intestazioni CORS per [accesso alla rete privata](https://wicg.github.io/private-network-access/#private-network-request) utilizzando l&#39;opzione `UES_CORS_PRIVATE_NETWORK`.


La tabella seguente descrive questi e altri valori aggiuntivi disponibili.

| Valore | Facoltativo | Predefiniti | Descrizione |
|---|---|---|---|
| `UES_PORT` | Sì | `8080` | Porta su cui viene eseguito il server |
| `UES_PRIVATE_KEY` | Sì | Nessuno | Percorso della chiave privata per il server HTTPS |
| `UES_CERT` | Sì | Nessuno | Percorso del file di certificazione per il server HTTPS |
| `UES_TLS_REJECT_UNAUTHORIZED` | Sì | `true` | Rifiuta connessioni TLS non autorizzate |
| `UES_DISABLE_IMS_VALIDATION` | Sì | `false` | Disattiva convalida IMS |
| `UES_ENDPOINT_MAPPING` | Sì | Vuoto | Mappatura degli endpoint per le riscritture interne<br>Esempio: `UES_ENDPOINT_MAPPING='[{"https://your-public-facing-author-domain.net": "http://10.0.0.1:4502"}]'`<br>Risultato: il servizio Editor universale si connetterà a `http://10.0.0.1:4502` invece della connessione specificata `https://your-public-facing-author-domain.net` |
| `UES_LOG_LEVEL` | Sì | `info` | Livello di registro per il server. I valori possibili sono `silly`, `trace`, `debug`, `verbose`, `info`, `log`, `warn`, `error` e `fatal` |
| `UES_SPLUNK_HEC_URL` | Sì | Nessuno | URL HEC per endpoint Splunk |
| `UES_SPLUNK_TOKEN` | Sì | Nessuno | Token Splunk |
| `UES_SPLUNK_INDEX` | Sì | Nessuno | Indice in cui scrivere i registri |
| `UES_SPLUNK_SOURCE` | Sì | `universal-editor-service` | Nome dell&#39;origine nei registri di splunk |
| `UES_CORS_PRIVATE_NETWORK` | Sì | `false` | Abilita l&#39;invio di intestazioni CORS per consentire [la rete privata](https://wicg.github.io/private-network-access/#private-network-request). Richiesto per gli utenti di Chrome versione 130+ |

>[!NOTE]
>
>Prima della versione [&#128279;](/help/release-notes/universal-editor/current.md) di 2024.08.13 di Universal Editor, nel file `.env` erano richieste le seguenti variabili. Questi valori saranno supportati fino al 1° ottobre 2024 per la compatibilità con le versioni precedenti.
>
>`EXPRESS_PORT=8000`
>`EXPRESS_PRIVATE_KEY=./key.pem`
>`EXPRESS_CERT=./certificate.pem`
>`NODE_TLS_REJECT_UNAUTHORIZED=0`

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

Una volta impostato, ogni chiamata di aggiornamento del contenuto dovrebbe passare a `https://localhost:8000` anziché al servizio Universal Editor predefinito.

>[!NOTE]
>
>Il tentativo di accedere direttamente a `https://localhost:8000` genera un errore `404`. Questo è il comportamento previsto.
>
>Per verificare l&#39;accesso al servizio Universal Editor locale, utilizzare `https://localhost:8000/corslib/LATEST`. Per informazioni dettagliate, consulta la [sezione successiva](#editing).

>[!TIP]
>
>Per ulteriori dettagli sulla strumentazione delle pagine per l&#39;utilizzo del servizio Global Universal Editor, vedere il documento [Guida introduttiva all&#39;editor universale in AEM](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Modifica di una pagina con il servizio Local Universal Editor {#editing}

Con il servizio [Universal Editor Service in esecuzione localmente](#running-ue) e la [pagina di contenuto dotata di strumenti per l&#39;utilizzo del servizio locale](#using-loca-ue), ora è possibile avviare l&#39;editor.

1. Apri il browser per `https://localhost:8000/ping`.
1. Indirizza il browser per accettare [il certificato autofirmato](#ue-https).
1. Una volta che il certificato autofirmato è attendibile, è possibile modificare la pagina utilizzando il servizio Universal Editor locale.

