---
title: Inoltro dei registri per AEM as a Cloud Service
description: Scopri come inoltrare i registri a Splunk e ad altri fornitori di registrazione in AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e007f2e3713d334787446305872020367169e6a2
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# Inoltro del registro {#log-forwarding}

>[!NOTE]
>
>Questa funzione non è ancora stata rilasciata e alcune destinazioni di registrazione potrebbero non essere disponibili al momento del rilascio. Nel frattempo, puoi aprire un ticket di supporto per inoltrare i registri a **Splunk**, come descritto nella [articolo di registrazione](/help/implementing/developing/introduction/logging.md).

I clienti che dispongono di una licenza per un fornitore di servizi di registrazione o che ospitano un prodotto di registrazione possono inoltrare i registri AEM (incluso Apache/Dispatcher) e i registri CDN alle destinazioni di registrazione associate. AEM as a Cloud Service supporta le seguenti destinazioni di registrazione:

* Archiviazione BLOB di Azure
* DataDog
* Elasticsearch o OpenSearch
* HTTPS
* Splunk

L’inoltro dei registri viene configurato in modo self-service dichiarando una configurazione in Git e distribuendola tramite la pipeline di configurazione di Cloud Manager per i tipi di ambiente di sviluppo, staging e produzione nei programmi di produzione (non sandbox).

È disponibile un’opzione per instradare i registri di AEM e Apache/Dispatcher tramite l’infrastruttura di rete avanzata dell’AEM, ad esempio l’IP in uscita dedicato.

La larghezza di banda di rete associata ai registri inviati alla destinazione di registrazione è considerata parte dell&#39;utilizzo di I/O di rete dell&#39;organizzazione.


## Struttura di questo articolo {#how-organized}

Questo articolo è organizzato nel modo seguente:

* Configurazione: comune per tutte le destinazioni di registrazione
* Registrazione delle configurazioni di destinazione: ogni destinazione ha un formato leggermente diverso
* Formati delle voci di registro: informazioni sui formati delle voci di registro
* Rete avanzata: invio dei registri di AEM e Apache/Dispatcher tramite un’uscita dedicata o tramite una VPN


## Configurazione {#setup}

1. Crea la seguente cartella e struttura di file nella cartella di livello principale del progetto in Git:

   ```
   config/
        logForwarding.yaml
   ```

1. `logForwarding.yaml` deve contenere metadati e una configurazione simile al seguente formato (ad esempio, utilizziamo Splunk).

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

   Il **tipo** il parametro deve essere impostato su `LogForwarding` la versione deve essere impostata sulla versione dello schema, ovvero 1.

   Token nella configurazione (ad esempio `${{SPLUNK_TOKEN}}`) rappresentano segreti che non devono essere memorizzati in Git. Dichiarali invece come Cloud Manager  [Variabili di ambiente](/help/implementing/cloud-manager/environment-variables.md) di tipo **segreto**. Assicurati di selezionare **Tutti** come valore a discesa per il campo Service Applied (Servizio applicato), in modo che i registri possano essere inoltrati ai livelli di authoring, pubblicazione e anteprima.

   È possibile impostare valori diversi per i registri CDN e per i registri AEM (incluso Apache/Dispatcher), includendo **cdn** e/o **aem** blocco dopo il **predefinito** , in cui le proprietà possono ignorare quelle definite nel **predefinito** blocco; è necessaria solo la proprietà abilitata. Un possibile caso di utilizzo potrebbe essere l’utilizzo di un indice Splunk diverso per i registri CDN, come illustrato nell’esempio seguente.

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

1. Per tipi di ambiente diversi da RDE (attualmente non supportato), crea una pipeline di configurazione della distribuzione di destinazione in Cloud Manager.

   * [Consulta Configurazione delle pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).
   * [Consulta Configurazione delle pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

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

Ciascuno dei server di registrazione distribuiti a livello globale produrrà un nuovo file ogni pochi secondi, sotto `aemcdn` cartella. Una volta creato, il file non verrà più aggiunto a. Il formato del nome file è YYY-MM-DDThh:mm:ss.sss-uniqueid.log Ad esempio, 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

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

Ogni file contiene più voci di registro json, ciascuna su una riga separata. I formati delle voci di registro sono descritti in [articolo di registrazione](/help/implementing/developing/introduction/logging.md), e ogni voce di registro include anche le proprietà aggiuntive menzionate nella [Formati voce registro](#log-format) sezione successiva.

#### Registri AEM archiviazione BLOB di Azure {#azureblob-aem}

I registri AEM (incluso Apache/Dispatcher) vengono visualizzati sotto una cartella con la seguente convenzione di denominazione:

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

In ogni cartella verrà creato un singolo file che verrà aggiunto a. I clienti sono responsabili dell’elaborazione e della gestione di questo file, in modo che non aumenti troppo.

Vedere i formati delle voci di registro in [articolo di registrazione](/help/implementing/developing/introduction/logging.md). Le voci del registro includeranno anche le proprietà aggiuntive menzionate nella [Formati voce registro](#log-formats) sezione successiva.


### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  dataDog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      
```

Considerazioni:

* Crea una chiave API, senza alcuna integrazione con un provider cloud specifico.


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
```

Considerazioni:

* Per le credenziali, assicurati di utilizzare le credenziali di distribuzione anziché le credenziali dell’account. Queste sono le credenziali generate in una schermata che potrebbe assomigliare a questa immagine:

![Credenziali di distribuzione elastica](/help/implementing/developing/introduction/assets/ec-creds.png)

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

#### Registri CDN HTTPS {#https-cdn}

Le richieste web (POST) verranno inviate in modo continuo, con un payload json che è un array di voci di registro, con il formato di voce di registro descritto in [articolo di registrazione](/help/implementing/developing/introduction/logging.md#cdn-log). Proprietà aggiuntive sono menzionate nella [Formati voce registro](#log-formats) sezione successiva.

È inoltre presente una proprietà denominata `sourcetype`, impostato sul valore `aemcdn`.

>[!NOTE]
>
> Prima di inviare la prima voce di registro CDN, il server HTTP deve completare correttamente una richiesta una tantum: una richiesta inviata al percorso ``wellknownpath`` deve rispondere con ``*``.


#### Registri AEM HTTPS {#https-aem}

Per i registri AEM (inclusi apache/dispacher), le richieste web (POST) verranno inviate in modo continuo, con un payload json che è un array di voci di registro, con i vari formati di voce di registro come descritto in [articolo di registrazione](/help/implementing/developing/introduction/logging.md). Proprietà aggiuntive sono menzionate nella [Formati voce registro](#log-format) sezione successiva.

È inoltre presente una proprietà denominata `sourcetype`, impostato su uno dei seguenti valori:

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

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
      index: "AEMaaCS"
```

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

Consulta la sezione Generale [articolo di registrazione](/help/implementing/developing/introduction/logging.md) per il formato di ciascun tipo di registro (registri CDN e registri AEM, compresi Apache/Dispatcher).

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

>[!NOTE]
>
>Questa funzione non è ancora pronta per essere utilizzata dai primi.


Alcune organizzazioni scelgono di limitare il traffico che può essere ricevuto dalle destinazioni di registrazione.

Per il registro CDN, puoi inserire gli indirizzi IP nell’elenco Consentiti, come descritto in [questo articolo](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Se l’elenco di indirizzi IP condivisi è troppo grande, puoi inviare il traffico a un archivio BLOB di Azure (non Adobe) in cui è possibile scrivere la logica per inviare i registri da un IP dedicato alla destinazione finale.

Per i registri AEM (incluso Apache/Dispatcher), puoi configurare l’inoltro dei registri in modo che venga eseguito [rete avanzata](/help/security/configuring-advanced-networking.md). Vedere i modelli per i tre tipi di rete avanzati riportati di seguito, che utilizzano un `port` insieme al parametro `host` parametro.

### Uscita flessibile della porta {#flex-port}

Se il traffico di registro si dirige verso una porta diversa da 443 (ad esempio, 8443 di seguito), configura la rete avanzata come segue:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 8443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

e configura il file yaml come segue:

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "${{AEM_PROXY_HOST}}"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### IP in uscita dedicato {#dedicated-egress}


Se il traffico di registro deve provenire da un IP in uscita dedicato, configura una rete avanzata come segue:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443, 
            "portOrig": 30443
        }    
    ]
}
```

e configura il file yaml come segue:

```
      
kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443    
```

### VPN {#vpn}

Se il traffico di registro deve passare attraverso una VPN, configura la rete avanzata come segue:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443,
            "portOrig": 30443
        }    
    ]
}

kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443     
```
