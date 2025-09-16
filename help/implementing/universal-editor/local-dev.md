---
title: Esecuzione del servizio editor universale
description: Scopri come eseguire il servizio editor universale per lo sviluppo locale o come parte dell’infrastruttura.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 5435f776e38abf5245c58985e747ce05443f3c2a
workflow-type: ht
source-wordcount: '950'
ht-degree: 100%

---


# Esecuzione del servizio editor universale {#local-ue-service}

Scopri come eseguire il servizio editor universale per lo sviluppo locale o come parte dell’infrastruttura.

>[!NOTE]
>
>I servizi editor universale locale non sono necessari o supportati per i progetti che utilizzano l’authoring AEM con Edge Delivery Services.

## Panoramica {#overview}

Il servizio editor universale è ciò che lega l’editor universale e il sistema di back-end. Per poter sviluppare in locale l’editor universale, è necessario eseguire una copia locale del servizio editor universale. Questo perché:

* Il servizio editor universale ufficiale di Adobe è ospitato a livello globale e l’istanza AEM locale dovrebbe essere esposta a Internet.
* Durante lo sviluppo con AEM SDK locale, non è possibile accedere al servizio editor universale di Adobe da Internet.
* Se l’istanza di AEM presenta restrizioni IP e il servizio editor universale di Adobe non è incluso in un intervallo IP definito, è possibile ospitarlo personalmente.

## Casi d’uso {#use-cases}

Una copia personalizzata del servizio editor universale è utile per:

* Lo sviluppo locale su AEM per l’utilizzo con l’editor universale.
* L’esecuzione del servizio editor universale come parte dell’infrastruttura, indipendentemente dal servizio editor universale di Adobe.

Sono supportati entrambi i casi d’uso. Questo documento spiega come eseguire AEM in HTTPS insieme a una copia locale del servizio editor universale.

Per eseguire il servizio editor universale come parte dell’infrastruttura, è necessario seguire gli stessi passaggi dell’esempio di sviluppo locale.

## Configurare AEM per l’esecuzione su HTTPS {#aem-https}

All’interno del frame esterno protetto con HTTPS, non è possibile caricare un frame HTTP non sicuro. Il servizio editor universale viene eseguito su HTTPS, pertanto anche AEM o qualsiasi altra pagina remota deve essere eseguito su HTTPS.

A questo scopo, devi configurare AEM per l’esecuzione su HTTPS. A scopo di sviluppo, puoi utilizzare un certificato autofirmato.

[Consulta questo documento](https://experienceleague.adobe.com/it/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard) su come configurare AEM in esecuzione su HTTPS, incluso un certificato autofirmato utilizzabile.

## Installare il servizio editor universale {#install-ue-service}

Il servizio editor universale non è un&#39;intera copia dell’editor universale, ma solo un sottoinsieme delle relative funzioni per garantire che le chiamate dall’ambiente AEM locale non vengano instradate su Internet, ma da un endpoint definito controllato.

Per eseguire una copia locale del servizio editor universale è necessario [NodeJS versione 20](https://nodejs.org/en/download/releases).

Il servizio editor universale è disponibile tramite distribuzione software. Per informazioni dettagliate su come accedervi, consulta la [documentazione sulla distribuzione software](https://experienceleague.adobe.com/it/docs/experience-cloud/software-distribution/home).

Salva il file `universal-editor-service.cjs` dalla distribuzione software nell’ambiente di sviluppo locale.

## Creare un certificato per eseguire il servizio editor universale con HTTPS {#ue-https}

Il servizio editor universale richiede inoltre un certificato per l’esecuzione su HTTPS nell’ambiente di sviluppo.

Esegui il comando seguente.

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

Il comando genera un file `key.pem` e un file `certificate.pem`. Salva questi file nello stesso percorso del file `universal-editor-service.cjs`.

## Configurazione del servizio editor universale {#setting-up-service}

È necessario impostare alcune variabili di ambiente in NodeJS per eseguire il servizio editor universale in locale.

Nello stesso percorso dei file `universal-editor-service.cjs`, `key.pem` e `certificate.pem`, crea un file `.env` con il contenuto seguente.

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
>Se stai eseguendo Chrome versione 130+, devi abilitare l’invio di intestazioni CORS per [accesso alla rete privata](https://wicg.github.io/private-network-access/#private-network-request) utilizzando l’opzione `UES_CORS_PRIVATE_NETWORK`.


La tabella seguente descrive questi e altri valori aggiuntivi disponibili.

| Valore | Facoltativo | Predefiniti | Descrizione |
|---|---|---|---|
| `UES_PORT` | Sì | `8080` | Porta su cui viene eseguito il server |
| `UES_PRIVATE_KEY` | Sì | Nessuna | Percorso della chiave privata per il server HTTPS |
| `UES_CERT` | Sì | Nessuna | Percorso del file di certificazione per il server HTTPS |
| `UES_TLS_REJECT_UNAUTHORIZED` | Sì | `true` | Rifiutare connessioni TLS non autorizzate |
| `UES_DISABLE_IMS_VALIDATION` | Sì | `false` | Disabilitare la convalida IMS |
| `UES_ENDPOINT_MAPPING` | Sì | Vuoto | Mappatura degli endpoint per le riscritture interne<br>Esempio: `UES_ENDPOINT_MAPPING='[{"https://your-public-facing-author-domain.net": "http://10.0.0.1:4502"}]'`<br>Risultato: il servizio editor universale si connetterà a `http://10.0.0.1:4502` invece della connessione `https://your-public-facing-author-domain.net` specificata |
| `UES_LOG_LEVEL` | Sì | `info` | Livello di registro per il server. I valori possibili sono `silly`, `trace`, `debug`, `verbose`, `info`, `log`, `warn`, `error` e `fatal` |
| `UES_SPLUNK_HEC_URL` | Sì | Nessuna | URL HEC per endpoint Splunk |
| `UES_SPLUNK_TOKEN` | Sì | Nessuna | Token Splunk |
| `UES_SPLUNK_INDEX` | Sì | Nessuna | Indice in cui scrivere i registri |
| `UES_SPLUNK_SOURCE` | Sì | `universal-editor-service` | Nome dell’origine nei registri di splunk |
| `UES_CORS_PRIVATE_NETWORK` | Sì | `false` | Abilita l’invio di intestazioni CORS per consentire [la rete privata](https://wicg.github.io/private-network-access/#private-network-request). Richiesto per gli utenti di Chrome versione 130+ |

>[!NOTE]
>
>Prima della ](/help/release-notes/universal-editor/current.md)versione 2024.08.13[ dell’editor universale, nel file `.env` erano richieste le seguenti variabili. Questi valori saranno supportati fino al 1° ottobre 2024 per la compatibilità con le versioni precedenti.
>
>`EXPRESS_PORT=8000`
>`EXPRESS_PRIVATE_KEY=./key.pem`
>`EXPRESS_CERT=./certificate.pem`
>`NODE_TLS_REJECT_UNAUTHORIZED=0`

## Esecuzione del servizio editor universale {#running-ue}

Per avviare il servizio editor universale, esegui questo comando:

```text
$ node ./universal-editor-service.cjs
```

Dovrebbe trasmettere quanto segue al terminale:

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

Verifica che il servizio avvii il server HTTPS e non il server HTTP.

## Utilizzo del servizio editor universale locale anziché del servizio globale {#using-local-ue}

L’editor universale conosce il servizio editor universale da utilizzare per modificare una pagina in base alla strumentazione. Questa operazione viene eseguita tramite i meta tag nella pagina caricata nell’editor universale.

Per modificare una pagina con il servizio editor universale locale, devi impostare il seguente meta tag:

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

Una volta impostato, ogni chiamata di aggiornamento del contenuto dovrebbe passare a `https://localhost:8000` anziché al servizio editor universale predefinito.

>[!NOTE]
>
>Il tentativo di accedere direttamente a `https://localhost:8000` genera un errore `404`. Questo è il comportamento previsto.
>
>Per verificare l’accesso al servizio editor universale locale, utilizza `https://localhost:8000/corslib/LATEST`. Per informazioni dettagliate, consulta la [sezione successiva](#editing).

>[!TIP]
>
>Per ulteriori dettagli sulla strumentazione delle pagine per l’utilizzo del servizio editor universale globale, consulta il documento [Guida introduttiva all’editor universale in AEM](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Modifica di una pagina con il servizio editor universale locale {#editing}

Con il [servizio editor universale in esecuzione localmente](#running-ue) e la [pagina contenuto dotata di strumenti per l’utilizzo del servizio locale](/help/implementing/universal-editor/getting-started.md), ora puopi avviare l’editor.

1. Apri il browser per `https://localhost:8000/ping`.
1. Indirizza il browser per accettare [il certificato autofirmato](#ue-https).
1. Una volta che il certificato autofirmato è attendibile, puoi modificare la pagina utilizzando il servizio editor universale locale.

