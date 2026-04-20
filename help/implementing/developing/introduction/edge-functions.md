---
title: Funzioni di AEM Edge
description: Scopri come eseguire JavaScript a livello di CDN con le funzioni AEM Edge per abilitare la personalizzazione, la sicurezza e le esperienze dinamiche vicine all’utente finale.
feature: Developing, Edge Delivery Services
role: Developer
source-git-commit: f8000bef01d6b72fb3ac2ae81be9fc19ed1a67d1
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 3%

---


# Funzioni di AEM Edge {#aem-edge-functions}

>[!IMPORTANT]
>
>Funzioni Edge di AEM è una funzione **beta**. Le funzioni e la documentazione potrebbero cambiare senza preavviso. Per partecipare al programma di accesso anticipato e fornire feedback, invia un&#39;e-mail a [aemcs-edge-functions-feedback@adobe.com](mailto:aemcs-edge-functions-feedback@adobe.com).

Le funzioni Edge di AEM consentono di eseguire JavaScript a livello di CDN, avvicinando l’elaborazione dei dati all’utente finale. Questo riduce la latenza e consente esperienze dinamiche e reattive senza un viaggio di andata e ritorno all’origine.

I casi d’uso comuni includono:

- Personalizzazione dei contenuti in base a informazioni quali geolocalizzazione, tipo di dispositivo o attributi utente
- Funge da middleware tra la rete CDN e l’origine
- Riformattazione o aggregazione di risposte da API di terze parti prima che raggiungano il browser
- Composizione e distribuzione di HTML con rendering server alla rete Edge tramite contenuti uniti da più back-end

Le funzioni Edge di AEM sono compatibili sia con Edge Delivery Services che con lo stack Java di AEM Cloud Service.

## Vantaggi principali {#key-benefits}

| Vantaggio | Descrizione |
|---|---|
| **Prestazioni** | TTFB veloce attraverso Edge SSR che restituisce HTML con rendering completo. Chiamate API a bassa latenza tramite recuperi paralleli e hop di rete ottimizzati. |
| **SEO / GEO** | Il server HTML è indicizzato al primo scansiono. Il contenuto con rendering completo è pronto per i crawler di intelligenza artificiale. |
| **Sicurezza** | Mantieni le credenziali API lato server, nascoste al JavaScript client. Eseguire l&#39;autenticazione con un provider di identità e limitare l&#39;accesso ai contenuti. |
| **Personalizzazione** | Personalizza il contenuto prima che la pagina venga caricata in base ai segnali geo e del dispositivo. Esegui ricerche del pubblico ai margini per una consegna mirata. |

## Prerequisiti {#prerequisites}

- Un ambiente AEM as a Cloud Service
- Il profilo di prodotto Amministratore AEM nell&#39;istanza di authoring dell&#39;ambiente Cloud Service, **o** il ruolo Responsabile della distribuzione Cloud Manager nei siti Admin Console per Edge Delivery Services
- [Node.js e npm](https://nodejs.org/)

## Configurazione {#setup}

### Installare Adobe CLI {#install-adobe-cli}

Installare Adobe Developer CLI (`aio`):

```bash
npm install -g @adobe/aio-cli
```

Installa il plug-in AEM Edge Functions:

```bash
aio plugins install @adobe/aio-cli-plugin-aem-edge-functions
```

Autentica e configura il plug-in per l’ambiente:

```bash
aio login
aio aem edge-functions setup
```

Il comando di installazione richiede di accedere e quindi selezionare l&#39;ambiente AEM in cui si desidera utilizzare le funzioni AEM Edge.

### Clona la piastra {#boilerplate}

Copia [aem-edge-functions-boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate) nel tuo archivio, quindi installa le dipendenze:

```bash
npm install
```

## Creare la prima funzione {#create-your-function}

I servizi di funzioni di AEM Edge sono dichiarati in un file di configurazione YAML e distribuiti tramite la pipeline di configurazione di Cloud Manager.

### &#x200B;1. Configurare una pipeline di configurazione {#configuration-pipeline}

Prima di creare una funzione Edge, accertati che esista una pipeline di configurazione per l’ambiente in Cloud Manager. In caso contrario, [crea prima una pipeline di configurazione](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

>[!NOTE]
>
>Se si utilizza un ambiente di sviluppo rapido, è possibile distribuire la configurazione direttamente con `aio aem rde:install -t env-config ./config` anziché passare attraverso una pipeline di configurazione.

### &#x200B;2. Dichiarare i servizi di funzione di Edge {#declare-services}

Creare un file denominato `edgeFunctions.yaml` nella directory di configurazione:

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  services:
    - name: first-function
    - name: second-function
    # Uncomment to enable secrets
    # secrets:
    #   - key: API_TOKEN
    #     value: ${{ API_TOKEN_SECRET }}
```

La configurazione supporta fino a tre servizi. Le chiavi di primo livello sono:

| Chiave | Descrizione |
|---|---|
| `services` | Elenco dei servizi di funzioni edge, ciascuno identificato da un `name`. |
| `configs` | Coppie chiave/valore esposte a tutti i servizi delle funzioni edge come variabili di ambiente. |
| `secrets` | Coppie chiave/valore che fanno riferimento a segreti di Cloud Manager, esposte a tutti i servizi di funzioni edge. |

### &#x200B;3. Aggiungere regole del selettore origine CDN {#cdn-routing}

Le funzioni Edge vengono richiamate instradando il traffico CDN verso di esse tramite le regole del selettore di origine. Aggiungi quanto segue al file di configurazione `cdn.yaml` (o creane uno se non esiste):

```yaml
kind: 'CDN'
version: '1'
data:
  originSelectors:
    rules:
      - name: route-to-first-function
        when: { reqProperty: path, equals: "/weather" }
        action:
          type: selectAemOrigin
          originName: edgefunction-first-function
      - name: route-to-second-function
        when: { reqProperty: path, equals: "/hello-world" }
        action:
          type: selectAemOrigin
          originName: edgefunction-second-function
```

Le regole del selettore di origine ti consentono di indirizzare il traffico alle funzioni edge in base a qualsiasi condizione disponibile nel motore di regole CDN, ad esempio un percorso specifico, un dominio o un’intestazione di richiesta. Consulta [Selettori origine](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) per la sintassi completa della regola.

### &#x200B;4. Distribuire la configurazione {#deploy-configuration}

Esegui il commit di `edgeFunctions.yaml` e `cdn.yaml` nell&#39;archivio Git di Cloud Manager e attiva la pipeline di configurazione. Una volta completata correttamente la pipeline, gli endpoint della funzione Edge sono disponibili in:

- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/weather`
- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/hello-world`

dove `pXXXXX-eYYYYY` sono le coordinate dell&#39;ambiente. Se è configurato un dominio personalizzato, le funzioni sono raggiungibili anche in questi percorsi di dominio (ad esempio, `example.com/weather`).

## Creare e distribuire codice funzione di AEM Edge {#build-deploy}

### Build {#build}

Crea un pacchetto del codice della funzione Edge per la distribuzione:

```bash
aio aem edge-functions build
```

### Distribuzione {#deploy}

Distribuisci il pacchetto generato in un servizio di funzioni edge denominato. L&#39;argomento `function-name` deve corrispondere al valore `name` in `edgeFunctions.yaml`:

```bash
aio aem edge-functions deploy <function-name>
```

## Sviluppo locale {#local-development}

### Esegui localmente {#local-run}

Avviare un server di sviluppo locale in `http://127.0.0.1:7676`:

```bash
aio aem edge-functions serve
```

Consulta questa [documentazione di Calcola JavaScript](https://www.fastly.com/documentation/guides/compute/javascript/) per informazioni dettagliate su ciò che supporta il runtime locale.

### Test {#test}

Esegui il gruppo di test con [Mocha](https://mochajs.org/):

```bash
npm run test
```

### Debug remoto {#remote-debugging}

La rete CDN gestita di Adobe non espone un debugger remoto, ma espone il flusso del registro. Suddividi i registri di una funzione implementata per ricevere l&#39;output `console.log` direttamente nel terminale:

```bash
aio aem edge-functions tail-logs <function-name>
```

## Riferimento configurazione {#configuration-reference}

### Origini {#origins}

Per impostazione predefinita, le funzioni di spigolo possono essere recuperate da qualsiasi origine. Per limitare una funzione a un set definito di origini, dichiararle in `origins` in `edgeFunctions.yaml`:

```yaml
origins:
  - name: my-origin-name
    domain: example.com
```

Fai riferimento all&#39;origine denominata nel codice della funzione utilizzando l&#39;opzione di recupero `backend`:

```js
const request = new Request("https://example.com/test");
const response = await fetch(request, { backend: "my-origin-name" });
```

### Configurazione servizio {#service-configuration}

Esporre le variabili di ambiente alle funzioni utilizzando la chiave `configs` in `edgeFunctions.yaml`. I valori sono archiviati in un archivio di configurazione denominato `config_default`:

```yaml
configs:
  - key: LOG_LEVEL
    value: DEBUG
```

Leggi i valori di configurazione nel codice della funzione:

```js
import { ConfigStore } from "fastly:config-store";

const config = new ConfigStore('config_default');
const logLevel = config.get('LOG_LEVEL') || 'info';
```

>[!NOTE]
>
>- L&#39;archivio di configurazione è sempre denominato `config_default`.
>- I nomi delle chiavi fanno distinzione tra maiuscole e minuscole.
>- L’archivio di configurazione è condiviso tra tutti i servizi delle funzioni edge nello stesso ambiente.

### Segreti di servizio {#service-secrets}

In `edgeFunctions.yaml` sono presenti riferimenti ai segreti, non archiviati. Il campo `value` deve puntare a un segreto Cloud Manager utilizzando la sintassi `${{SECRET_REFERENCE}}`. Definisci prima il segreto sottostante in Cloud Manager. Vedi [Variabili segrete Cloud Manager](/help/implementing/cloud-manager/environment-variables.md).

```yaml
secrets:
  - key: API_TOKEN
    value: ${{ API_TOKEN_SECRET }}
```

Recupera i segreti nel codice della funzione utilizzando l&#39;helper `SecretStoreManager` dalla boilerplate:

```js
import { SecretStoreManager } from "./lib/config";

const apiToken = await SecretStoreManager.getSecret('API_TOKEN');
```

>[!NOTE]
>
>- L&#39;archivio segreto è sempre denominato `secret_default`.
>- I nomi delle chiavi fanno distinzione tra maiuscole e minuscole.
>- I segreti creati non sono modificabili.
>- L’archivio segreto è condiviso tra tutti i servizi delle funzioni edge nello stesso ambiente.

### Registrazione {#logging}

Le funzioni Edge di AEM si integrano con la funzione [Inoltro log di AEM](/help/implementing/developing/introduction/log-forwarding.md). Crea un file `logForwarding.yaml` insieme a `edgeFunctions.yaml`:

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["rde", "dev", "stage", "prod"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

Utilizza il logger nel codice della funzione per scrivere voci di registro strutturate:

```js
import { Logger } from "fastly:logger";

const logger = new Logger("customerSplunk");
logger.log(JSON.stringify({
  method: event.request.method,
  url: event.request.url
}));
```

>[!NOTE]
>
>I registri CDN, che includono le voci del registro funzioni di AEM Edge, possono essere scaricati da Cloud Manager per gli ambienti Java stack, ma non per i siti Edge Delivery Services.
>
