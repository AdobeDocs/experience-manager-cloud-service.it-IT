---
title: Sviluppo locale con strumenti AI
description: Scopri come configurare gli strumenti di codifica AI con il contesto del progetto, le competenze dell’agente e i server MCP per accelerare lo sviluppo di AEM as a Cloud Service.
feature: Developing
role: Developer
exl-id: 09d6257d-36ad-49e5-831f-c44b356f1800
source-git-commit: f7a46a5b8c5bbe30ab5d6828ba99b2435b88dbeb
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---

# Sviluppo locale con strumenti AI {#local-development-with-ai-tools}

>[!IMPORTANT]
>
>Le funzionalità descritte in questo articolo sono **beta**. L&#39;accesso anticipato alle funzionalità sviluppate da Adobe consente ai clienti e ai partner di fornire un feedback (inviando un&#39;e-mail a [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)) e sviluppare i prodotti. Consente inoltre di prepararsi ad adottare nuove funzionalità prima della disponibilità generale.
>
>I rilasci di Beta possono contenere difetti e vengono forniti &quot;COSÌ COME SONO&quot; senza alcuna garanzia. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare o altrimenti supportare (tramite i servizi di supporto Adobe o in altro modo) le versioni beta. Adobe consiglia ai clienti di prestare attenzione e di non affidarsi al corretto funzionamento o alle prestazioni delle versioni beta o a qualsiasi documentazione o materiale di accompagnamento. Le funzioni e le API in versione beta sono soggette a modifiche senza preavviso. Di conseguenza, qualsiasi utilizzo delle versioni beta è interamente a rischio del cliente.

>[!NOTE]
>
>Questo articolo si concentra sullo sviluppo locale con strumenti di intelligenza artificiale per lo sviluppo **stack Java AEM**. Per Edge Delivery Services, consulta [Sviluppo con strumenti di intelligenza artificiale](https://www.aem.live/developer/ai-coding-agents).

Gli agenti di codifica IA (Claude Code, Cursor, GitHub Copilot e strumenti simili) hanno un’ampia conoscenza delle tecnologie sottostanti di AEM (Java, OSGi, Sling, JCR, HTL), ma non conoscono necessariamente le best practice per la generazione di codice e configurazione, o come eseguire il debug dei problemi comuni di sviluppo di AEM.

Quattro componenti complementari affrontano questo problema:

| Componente | Scopo |
|---|---|
| **AGENTI.md** | Un file di contesto specifico del progetto che basa l’intelligenza artificiale nel progetto AEM Cloud Service per ogni sessione |
| **Competenze agente** | Set di istruzioni riutilizzabili per attività di sviluppo ricorrenti, ad esempio la creazione di componenti e la configurazione di Dispatcher |
| **Server MCP locale Quickstart di AEM** | Espone i dati live runtime da un’istanza AEM SDK locale per supportare la risoluzione dei problemi |
| **Server MCP locale Dispatcher** | Abilita la convalida runtime e l&#39;ispezione di un&#39;istanza Dispatcher locale |

>[!NOTE]
>
> Utili anche per lo sviluppo locale, ma non trattati in questo articolo, sono i server MCP remoti di AEM Cloud Service. Per ulteriori informazioni, consulta l&#39;articolo [Utilizzo di MCP con Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

## AGENTS.md {#agentsmd}

`AGENTS.md` è un file Markdown nella directory principale del progetto AEM, in cui gli strumenti di codifica AI vengono caricati automaticamente all&#39;inizio di ogni sessione per essere basati sulle competenze essenziali del dominio Java stack di AEM Cloud Service (e non su altre soluzioni AEM come AEM 6.5 o Edge Delivery Services).

`AGENTS.md` non è un file statico copiato. Viene generato dall&#39;abilità `ensure-agents-md` descritta nella sezione successiva. L&#39;abilità legge `pom.xml` per risolvere il nome del progetto, individuare i moduli e rilevare i componenti aggiuntivi installati, producendo un file personalizzato per il progetto specifico.

>[!NOTE]
>
>Una volta che `AGENTS.md` esiste nella directory principale del progetto, l&#39;abilità `ensure-agents-md` non viene più eseguita. Modifica direttamente il file se la struttura del progetto cambia.

## Abilità agente {#agent-skills}

Le abilità sono set di istruzioni che codificano flussi di lavoro di sviluppo in più passaggi. Quando invocata, l’intelligenza artificiale segue la procedura dell’abilità anziché affidarsi esclusivamente alla conoscenza generale, producendo risultati coerenti e conformi alle convenzioni.

Adobe pubblica AEM as a Cloud Service skills nell&#39;archivio **[adobe/skills](https://github.com/adobe/skills/tree/beta/skills/aem/cloud-service/skills)** nel ramo `beta` poiché questa funzione non è ancora disponibile a livello generale:

| Abilità | Scopo |
|---|---|
| `ensure-agents-md` | Bootstrap `AGENTS.md` e `CLAUDE.md` personalizzati in base all&#39;effettiva struttura del modulo del progetto |
| `create-component` | Scaffolds un componente AEM completo: definizione del componente, finestra di dialogo XML, modello HTL, modello Sling, unit test e clientlibs |
| `dispatcher` | Assistente alla configurazione di Dispatcher e Apache HTTPD con tecnologia AI per l’authoring della configurazione, consulenze tecniche, risposta agli incidenti, ottimizzazione delle prestazioni e protezione |
| `workflow` | Singolo punto di ingresso per tutte le abilità del flusso di lavoro di AEM as a Cloud Service. Include la progettazione del modello di flusso di lavoro, il passaggio del processo personalizzato e lo sviluppo del selettore partecipanti, la configurazione del modulo di avvio, l’attivazione del flusso di lavoro e il supporto alla produzione, tra cui il debug di flussi di lavoro bloccati/non riusciti, la valutazione degli incidenti con i registri di Cloud Manager, l’analisi del pool di thread e la diagnostica dei processi Sling per il motore di flusso di lavoro Granite. |

### Installa abilità {#install-skills}

Scegli il metodo che corrisponde allo strumento di codifica AI. L’installazione delle abilità una volta le rende disponibili per tutti i progetti su quel computer.

#### Claude Code {#claude-code}

```bash
# Add the Adobe Skills marketplace (one-time setup)
/plugin marketplace add adobe/skills

# Install all available skills
/plugin install aem-cloud-service@adobe-skills
```

#### Abilità Npx {#npx-skills}

```bash
# Install all available skills
npx skills add https://github.com/adobe/skills/tree/main/skills/aem/cloud-service --all
```

#### Aggiornamento (estensione CLI GitHub) {#upskill-github-cli-extension}

```bash
# Install the gh-upskill extension (one-time setup)
gh extension install ai-ecoverse/gh-upskill

# Install all available skills
gh upskill adobe/skills --path skills/aem/cloud-service --all
```

### Utilizzare l’abilità make-agents-md {#use-the-ensure-agents-md-skill}

Dopo aver installato l’abilità, apri l’assistente AI in qualsiasi progetto AEM Cloud Service che non dispone ancora di `AGENTS.md`. L’abilità viene eseguita automaticamente prima di elaborare la prima richiesta, creando entrambi i file nella directory principale del progetto senza richiedere una chiamata esplicita.

### Utilizzare l’abilità di creazione dei componenti {#use-the-create-component-skill}

Al primo utilizzo, l&#39;abilità rileva automaticamente `project`, `package` e `group` da `pom.xml` e dai componenti esistenti, richiede di confermare i valori rilevati, quindi crea `.aem-skills-config.yaml` nella directory principale del progetto. Non è richiesta alcuna configurazione manuale prima del primo utilizzo.

Se preferisci creare il file in anticipo, inserisci `.aem-skills-config.yaml` nella directory principale del progetto con la seguente struttura:

```yaml
configured: true

project: "wknd"                                    # Check /apps/{project}/ or pom.xml
package: "com.adobe.aem.guides.wknd.core"          # Check core/pom.xml
group: "WKND Components"                           # Check existing component .content.xml files
```

Il file si trova all’esterno della directory delle abilità e non viene mai sovrascritto quando l’abilità viene aggiornata.

Descrivi il componente nella chat di IA:

```
Create an AEM component called "Hero Banner"

Dialog specification:
Title (title) - Textfield, mandatory
Subtitle (subtitle) - Textfield
Background Image (backgroundImage) - Fileupload
CTA Text (ctaText) - Textfield
CTA Link (ctaLink) - Pathfield
```

L’agente fa eco alle specifiche del campo per la conferma, quindi genera tutti i file dei componenti. I pattern supportati includono multicampo con elementi compositi nidificati, logica condizionale di visualizzazione/nascondere, estensione dei componenti core tramite Sling Resource Merger e test JUnit 5 con AEM Mocks.

### Utilizzare l’abilità Dispatcher {#use-the-dispatcher-skill}

Richiama l’abilità del dispatcher per qualsiasi lavoro di configurazione Dispatcher o Apache HTTPD. L’abilità indirizza le richieste a una delle sei sottocompetenze specialistiche in base alla natura della richiesta:

| Sub-abilità | Scopo |
|---|---|
| `workflow-orchestrator` | Lavoro end-to-end su progettazione, modifiche alla configurazione, convalida e follow-up |
| `config-authoring` | Modifiche concrete alla configurazione: filtri, regole di cache, riscritture, host, intestazioni e farm |
| `technical-advisory` | Linee guida concettuali, spiegazione delle politiche e raccomandazioni basate su citazioni |
| `incident-response` | Errori di runtime, anomalie della cache e regressioni |
| `performance-tuning` | Efficienza della cache, latenza e ottimizzazione del throughput |
| `security-hardening` | Analisi dell’esposizione e irrigidimento della produzione |

Per richieste ampie o nuove, inizia con la sottoabilità `workflow-orchestrator`. Per un lavoro mirato, descrivi la preoccupazione specifica e gli itinerari di competenze allo specialista appropriato.

L’abilità del dispatcher gestisce l’orchestrazione e le linee guida per gli advisory. Il server MCP di Dispatcher, descritto di seguito, fornisce i sette strumenti di convalida e runtime utilizzati dall’abilità quando necessita di prove locali.

## Server AEM Quickstart MCP {#aem-quickstart-mcp-server}

Model Context Protocol (MCP) è uno standard aperto che consente agli strumenti di codifica IA di connettersi a origini dati e servizi esterni. Il server MCP Quickstart di AEM è un pacchetto di contenuti che, una volta installato in un’istanza AEM SDK locale, espone i dati di runtime direttamente agli strumenti di intelligenza artificiale connessi, consentendo agli agenti di recuperare i registri, diagnosticare gli errori OSGi e controllare l’elaborazione delle richieste senza uscire dall’IDE.

### Installare il pacchetto dei contenuti {#install-the-content-package}

Scarica il pacchetto di contenuti dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=mcp*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=tipo di software%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=3) e installa `com.adobe.aem:com.adobe.aem.mcp-server-contribs-content` nel tuo Quickstart locale utilizzando Gestione pacchetti in `/crx/packmgr`.

**Compatibilità:** convalidata con AEM SDK `2026.2.24678.20260226T154829Z-260200` e versioni successive.

### Strumenti disponibili {#available-tools}

| Strumento  | Descrizione |
|---|---|
| `aem-logs` | Recupera le voci di registro AEM e OSGi, filtrabili per pattern regex, livello di registro e conteggio delle voci |
| `diagnose-osgi-bundle` | Diagnostica il motivo per cui un bundle o un componente DS non viene avviato; segnala pacchetti mancanti, riferimenti non soddisfatti e problemi di configurazione |
| `recent-requests` | Restituisce le richieste HTTP recenti con la traccia di elaborazione interna completa di Sling (risoluzione delle risorse, risoluzione degli script, catena di filtri), filtrabile per percorso regex |

### Configurare l’IDE {#configure-your-ide}

#### Cursore {#cursor}

In Impostazioni cursore, aggiungi un nuovo server MCP personalizzato:

```json
"aem-cs-sdk": {
  "type": "streamable-http",
  "url": "http://localhost:4502/bin/mcp",
  "headers": {
    "Authorization": "Basic YWRtaW46YWRtaW4="
  }
}
```

#### Copilota GitHub con IntelliJ IDEA {#github-copilot-with-ihtellij-idea}

Passa a **Strumenti > Copilota GitHub > MCP (Model Context Protocol)** e fai clic su **Configura**. Aggiungi:

```json
"aem-cs-sdk": {
  "url": "http://localhost:4502/bin/mcp",
  "requestInit": {
    "headers": {
      "Authorization": "Basic YWRtaW46YWRtaW4="
    }
  }
}
```

#### Altri IDE {#other-ides}

Qualsiasi client MCP può connettersi puntando a `http://localhost:4502/bin/mcp` con intestazione `Authorization: Basic YWRtaW46YWRtaW4=`. Configura le intestazioni personalizzate utilizzando le impostazioni MCP dell’IDE.

>[!NOTE]
>
>Il valore `Basic YWRtaW46YWRtaW4=` è la codifica Base64 di `admin:admin`, le credenziali predefinite per un Quickstart locale. Non utilizzarlo con ambienti non locali.

## Server Dispatcher MCP {#dispatcher-mcp-server}

Il server Dispatcher MCP è fornito in bundle con AEM Dispatcher SDK. Consente agli strumenti di intelligenza artificiale di convalidare la configurazione Dispatcher e Apache HTTPD, la gestione delle richieste di traccia e il comportamento della cache rispetto a un’istanza Dispatcher in esecuzione localmente in Docker.

A differenza dell’abilità del dispatcher, il server MCP di Dispatcher espone solo strumenti: sette strumenti MCP e nessun prompt o risorsa.

### Prerequisiti {#prerequisites}

- Docker Desktop 4.x o versione successiva, installato ed in esecuzione
- AEM Dispatcher SDK scaricato dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=mcp*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=tipo di software%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=3)

>[!NOTE]
>
>Se vedi `client version 1.43 is too new`, imposta `DOCKER_API_VERSION=1.41` nella tua shell o in `mcp.json`.

### Installare Dispatcher SDK {#install-the-dispatcher-sdk}

**macOS e Linux:**

```bash
chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
./aem-sdk-dispatcher-tools-<version>-unix.sh
cd dispatcher-sdk-<version>
chmod +x ./bin/docker_run_mcp.sh
./bin/docker_run_mcp.sh test
```

**Windows:**

```powershell
Expand-Archive aem-sdk-dispatcher-tools-<version>-windows.zip
```

Eseguire `./bin/docker_run_mcp.sh help` per recuperare la configurazione IDE di copia e incolla e `./bin/docker_run_mcp.sh version` per confermare la versione MCP e SDK nel bundle. Utilizza `./bin/docker_run_mcp.sh diagnose` per analizzare i problemi di connettività.

### Configura cursore {#configure-cursor}

Aggiungi una voce `aem-dispatcher-mcp` a `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "aem-dispatcher-mcp": {
      "command": "<path_to_dispatcher_sdk>/bin/docker_run_mcp.sh",
      "env": {
        "DOCKER_API_VERSION": "1.43",
        "AEM_DEPLOYMENT_MODE": "cloud",
        "MCP_LOG_LEVEL": "trace",
        "MCP_LOG_FILE": "/tmp/dispatcher-mcp.log",
        "DISPATCHER_CONFIG_PATH": "<path_to_dispatcher_src>"
      }
    }
  }
}
```

Sostituisci `<path_to_dispatcher_sdk>` con il percorso di Dispatcher SDK estratto e `<path_to_dispatcher_src>` con la directory del dispatcher del progetto `src`. Impostare `DISPATCHER_CONFIG_PATH` sulla radice di configurazione che include i file in cui è definito `/docroot`. `MCP_LOG_LEVEL` e `MCP_LOG_FILE` sono impostazioni di debug facoltative. Se vedi `client version 1.43 is too new`, imposta `DOCKER_API_VERSION` su `1.41`. Se altri server MCP sono già configurati, aggiungere la voce `aem-dispatcher-mcp` senza sostituirli. Riavvia cursore dopo il salvataggio.

Altri IDE possono essere configurati in modo simile. Il SDK `docs/DispatcherMCP.md` include esempi completi per Claude Desktop e VS Code.

### Strumenti disponibili {#available-tools-dispatcher}

| Strumento  | Descrizione |
|---|---|
| `validate` | Convalida le configurazioni HTTPD di Dispatcher e Apache |
| `lint` | Esegue controlli statici in base alla modalità e analisi delle best practice |
| `sdk` | Esegue i flussi di lavoro di Dispatcher SDK: `validate`, `validate-full`, `three-phase-validate`, `docker-test`, `check-files`, `diff-baseline` |
| `trace_request` | Traccia il comportamento della richiesta con prove di runtime |
| `inspect_cache` | Controlla il comportamento della cache e della directory principale dei documenti per un URL di destinazione |
| `monitor_metrics` | Legge le metriche di runtime dai registri Dispatcher e HTTPD |
| `tail_logs` | Dettagli dei registri di runtime pertinenti di Dispatcher e HTTPD |

La superficie MCP espone intenzionalmente solo questi sette strumenti; i prompt e le risorse rimangono nel livello abilità. La documentazione completa di riferimento è disponibile in `docs/DispatcherMCP.md` all&#39;interno del SDK Dispatcher estratto.
