---
title: Inoltro registro per AEM as a Cloud Service
description: Scopri come inoltrare i registri a Splunk e ad altri fornitori di registrazione in AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 17d195f18055ebd3a1c4a8dfe1f9f6bc35ebaf37
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 0%

---

# Inoltro del registro {#log-forwarding}

>[!NOTE]
>
>Questa funzione non è ancora stata rilasciata e alcune destinazioni di registrazione potrebbero non essere disponibili al momento del rilascio. Nel frattempo, puoi aprire un ticket di supporto per inoltrare i registri a **Splunk**, come descritto in [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md).

I clienti che dispongono di una licenza per un fornitore di servizi di registrazione o che ospitano un prodotto di registrazione possono inoltrare i registri AEM (incluso Apache/Dispatcher) e i registri CDN alle destinazioni di registrazione associate. AEM as a Cloud Service supporta le seguenti destinazioni di registrazione:

* Archiviazione BLOB di Azure
* DataDog
* Elasticsearch o OpenSearch
* HTTPS
* Splunk

L’inoltro dei registri viene configurato in modo self-service dichiarando una configurazione in Git e distribuendola tramite la pipeline di configurazione di Cloud Manager ai tipi di ambiente di sviluppo, staging e produzione nei programmi di produzione (non sandbox).

È disponibile un’opzione per instradare i registri AEM e Apache/Dispatcher tramite l’infrastruttura di rete avanzata dell’AEM, ad esempio l’IP in uscita dedicato.

La larghezza di banda di rete associata ai registri inviati alla destinazione di registrazione è considerata parte dell&#39;utilizzo di I/O di rete dell&#39;organizzazione.


## Struttura di questo articolo {#how-organized}

Questo articolo è organizzato nel modo seguente:

* Configurazione: comune per tutte le destinazioni di registrazione
* Registrazione delle configurazioni di destinazione: ogni destinazione ha un formato leggermente diverso
* Formati delle voci di registro: informazioni sui formati delle voci di registro
* Rete avanzata: invio dei registri AEM e Apache/Dispatcher tramite un’uscita dedicata o tramite una VPN


## Configurazione {#setup}

1. Creare un file denominato `logForwarding.yaml`. Deve contenere metadati, come descritto nell&#39;articolo [config pipeline](/help/operations/config-pipeline.md#common-syntax) (**kind** deve essere impostato su `LogForwarding` e la versione impostata su &quot;1&quot;), con una configurazione simile alla seguente (ad esempio, si utilizza Splunk).

   ```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
   ```

1. Posizionare il file in una cartella di primo livello denominata *config* o simile, come descritto in [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md#folder-structure).

1. Per tipi di ambiente diversi da RDE (attualmente non supportato), creare una pipeline di configurazione della distribuzione di destinazione in Cloud Manager, come indicato in [questa sezione](/help/operations/config-pipeline.md#creating-and-managing). Si noti che le pipeline full stack e le pipeline a livello web non distribuiscono il file di configurazione.

1. Distribuisci la configurazione.

I token nella configurazione (ad esempio `${{SPLUNK_TOKEN}}`) rappresentano segreti, che non devono essere memorizzati in Git. Dichiarale invece come [Variabili di ambiente segrete](/help/operations/config-pipeline.md#secret-env-vars) di Cloud Manager. Assicurarsi di selezionare **Tutti** come valore a discesa per il campo Servizio applicato, in modo che i registri possano essere inoltrati ai livelli di authoring, pubblicazione e anteprima.

È possibile impostare valori diversi tra i registri CDN e i registri AEM (incluso Apache/Dispatcher), includendo un blocco **cdn** e/o **aem** aggiuntivo dopo il blocco **default**, in cui le proprietà possono ignorare quelle definite nel blocco **default**. È richiesta solo la proprietà abilitata. Un possibile caso di utilizzo potrebbe essere l’utilizzo di un indice Splunk diverso per i registri CDN, come illustrato nell’esempio seguente.

```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
       cdn:
         enabled: true
         token: "${{SPLUNK_TOKEN_CDN}}"
         index: "AEMaaCS_CDN"   
```

Un altro scenario consiste nel disabilitare l’inoltro dei registri CDN o dei registri AEM (incluso Apache/Dispatcher). Ad esempio, per inoltrare solo i registri CDN, puoi configurare quanto segue:

```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
       aem:
         enabled: false
```

## Registrazione della configurazione di destinazione {#logging-destinations}

Di seguito sono elencate le configurazioni per le destinazioni di registrazione supportate, insieme a eventuali considerazioni specifiche.

### Archiviazione BLOB di Azure {#azureblob}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  azureBlob:
    default:
      enabled: true       
      storageAccountName: "example_acc"
      container: "aem_logs"
      sasToken: "${{AZURE_BLOB_SAS_TOKEN}}
      
```

Utilizzare un token SAS per l&#39;autenticazione. Deve essere creato dalla pagina della firma di accesso condiviso, anziché dalla pagina del token di accesso condiviso, e deve essere configurato con le seguenti impostazioni:

* Servizi consentiti: è necessario selezionare BLOB.
* Risorse consentite: è necessario selezionare l’oggetto.
* Autorizzazioni consentite: è necessario selezionare Scrivi, Aggiungi o Crea.
* Una data/ora di inizio e di scadenza valida.

Ecco una schermata di esempio della configurazione del token SAS:

![Configurazione token SAS BLOB di Azure](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

#### Registri CDN archiviazione BLOB di Azure {#azureblob-cdn}

Ogni server di registrazione distribuito a livello globale produrrà un nuovo file ogni pochi secondi, nella cartella `aemcdn`. Una volta creato, il file non verrà più aggiunto a. Il formato del nome file è YYY-MM-DDThh:mm:ss.sss-uniqueid.log. Ad esempio, 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

Ad esempio, a un certo punto del tempo:

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

E poi 30 secondi dopo:

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

Ogni file contiene più voci di registro json, ciascuna su una riga separata. I formati delle voci di registro sono descritti in [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) e ogni voce di registro include anche le proprietà aggiuntive menzionate nella sezione [Formati di voce di registro](#log-format) seguente.

#### Registri AEM archiviazione BLOB di Azure {#azureblob-aem}

I registri AEM (incluso Apache/Dispatcher) vengono visualizzati sotto una cartella con la seguente convenzione di denominazione:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

In ogni cartella verrà creato un singolo file che verrà aggiunto a. I clienti sono responsabili dell’elaborazione e della gestione di questo file, in modo che non aumenti troppo.

Consulta i formati delle voci di registro in [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Le voci di registro includeranno anche le proprietà aggiuntive menzionate nella sezione [Formati di voce di registro](#log-formats) seguente.


### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  datadog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      tags:
         tag1: value1
         tag2: value2
      
```

Considerazioni:

* Crea una chiave API, senza alcuna integrazione con un provider cloud specifico.
* la proprietà tags è facoltativa
* Per i registri AEM, il tag di origine Datadog è impostato su uno dei seguenti valori: `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` o `aemhttpderror`
* Per i registri CDN, il tag di origine Datadog è impostato su `aemcdn`
* il tag del servizio Datadog è impostato su `adobeaemcloud`, ma è possibile sovrascriverlo nella sezione dei tag


### Elasticsearch e OpenSearch {#elastic}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  elasticsearch:
    default:
      enabled: true
      host: "example.com"
      user: "${{ELASTICSEARCH_USER}}"
      password: "${{ELASTICSEARCH_PASSWORD}}"
      pipeline: "ingest pipeline name"
```

Considerazioni:

* per impostazione predefinita, la porta è 443. Facoltativamente, può essere sostituito con una proprietà denominata `port`
* Per le credenziali, assicurati di utilizzare le credenziali di distribuzione anziché le credenziali dell’account. Queste sono le credenziali generate in una schermata che potrebbe assomigliare a questa immagine:

![Credenziali distribuzione elastica](/help/implementing/developing/introduction/assets/ec-creds.png)

* Per i registri AEM, `index` è impostato su uno di `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` o `aemhttpderror`
* La proprietà opzionale della pipeline deve essere impostata sul nome della pipeline di acquisizione Elasticsearch o OpenSearch, che può essere configurata per instradare la voce di registro all’indice appropriato. Il tipo di processore della pipeline deve essere impostato su *script* e il linguaggio di script su *indolore*. Di seguito è riportato un frammento di script di esempio per instradare le voci di registro in un indice come aemaccess_dev_26_06_2024:

```
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      enabled: true
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

Considerazioni:

* La stringa URL deve includere **https://**, altrimenti la convalida non riuscirà.
* L’URL può includere una porta. Ad esempio, `https://example.com:8443/aem_logs/aem`. Se nella stringa URL non è inclusa alcuna porta, viene utilizzata la porta 443 (la porta HTTPS predefinita).

#### Registri CDN HTTPS {#https-cdn}

Le richieste Web (POST) verranno inviate in modo continuo, con un payload json che è un array di voci di registro, con il formato di voce di registro descritto in [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md#cdn-log). Proprietà aggiuntive sono menzionate nella sezione [Formati di voce di registro](#log-formats) di seguito.

Esiste anche una proprietà denominata `sourcetype`, impostata sul valore `aemcdn`.

>[!NOTE]
>
> Prima dell&#39;invio della prima voce di registro CDN, il server HTTP deve completare una richiesta una tantum: una richiesta inviata al percorso ``/.well-known/fastly/logging/challenge`` deve rispondere con un asterisco ``*`` nel corpo e il codice di stato 200.

#### Registri AEM HTTPS {#https-aem}

Per i registri AEM (incluso apache/dispacher), le richieste web (POST) verranno inviate in modo continuo, con un payload json che è un array di voci di registro, con i vari formati di voci di registro come descritto in [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Proprietà aggiuntive sono menzionate nella sezione [Formati di voce di registro](#log-format) di seguito.

Esiste anche una proprietà denominata `Source-Type`, impostata su uno dei seguenti valori:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### Splunk {#splunk}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
```

Considerazioni:

* per impostazione predefinita, la porta è 443. Facoltativamente, può essere sostituito con una proprietà denominata `port`.


<!--
### Sumo Logic {#sumologic}

   ```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "https://collectors.de.sumologic.com"
         uri: "/receiver/v1/http"
         privateKey: "${{SomeOtherToken}}"
   
   ```   
-->

## Formati voce registro {#log-formats}

Consulta [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) per il formato di ciascun tipo di registro (registri CDN e registri AEM, incluso Apache/Dispatcher).

Poiché i registri provenienti da più programmi e ambienti possono essere inoltrati alla stessa destinazione di registrazione, oltre all’output descritto nell’articolo sulla registrazione, in ogni voce di registro verranno incluse le seguenti proprietà:

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

Ad esempio, le proprietà potrebbero avere i seguenti valori:

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## Rete avanzata {#advanced-networking}

Alcune organizzazioni scelgono di limitare il traffico che può essere ricevuto dalle destinazioni di registrazione.

Per il registro CDN, puoi inserire gli indirizzi IP nell&#39;elenco Consentiti, come descritto nella [documentazione rapida - Elenco IP pubblico](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Se l’elenco di indirizzi IP condivisi è troppo grande, puoi inviare traffico a un server https o a un archivio BLOB di Azure (non Adobe) in cui è possibile scrivere una logica per inviare i registri da un IP noto alla destinazione finale.

Per i registri AEM (incluso Apache/Dispatcher), se hai configurato [rete avanzata](/help/security/configuring-advanced-networking.md), puoi utilizzare la proprietà advancedNetworking per inoltrarli da un indirizzo IP in uscita dedicato o tramite una VPN.

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      port: 443
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
    aem:
      advancedNetworking: true
```

