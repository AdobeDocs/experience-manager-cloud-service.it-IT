---
title: Inoltro dei registri per AEM as a Cloud Service
description: Scopri come inoltrare i registri a Splunk e ad altri fornitori di registrazione in AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---

# Inoltro del registro {#log-forwarding}

>[!NOTE]
>
>Questa funzione non è ancora stata rilasciata e alcune destinazioni di registrazione potrebbero non essere disponibili al momento del rilascio. Nel frattempo, puoi aprire un ticket di supporto per inoltrare i registri a **Splunk**, come descritto nella [articolo di registrazione](/help/implementing/developing/introduction/logging.md).

I clienti che dispongono di una licenza per un fornitore di accesso o che ospitano un prodotto di accesso possono inoltrare i registri AEM, Apache/Dispatcher e CDN alle relative destinazioni di accesso. AEM as a Cloud Service supporta le seguenti destinazioni di registrazione:

* Archiviazione BLOB di Azure
* DataDog
* Elasticsearch o OpenSearch
* HTTPS
* Splunk

L’inoltro dei registri viene configurato in modo self-service dichiarando una configurazione in Git e distribuendola tramite la pipeline di configurazione di Cloud Manager per i tipi di ambiente di sviluppo, staging e produzione nei programmi di produzione (non sandbox).

La larghezza di banda di rete associata ai registri inviati alla destinazione di registrazione è considerata parte dell&#39;utilizzo di I/O di rete dell&#39;organizzazione.


## Struttura di questo articolo {#how-organized}

Questo articolo è organizzato nel modo seguente:

* Configurazione: comune per tutte le destinazioni di registrazione
* Registrazione delle configurazioni di destinazione: ogni destinazione ha un formato leggermente diverso
* Rete avanzata: invio dei registri di AEM e Apache/Dispatcher tramite un’uscita dedicata o tramite una VPN


## Configurazione {#setup}

1. Crea la seguente cartella e struttura di file nella cartella di livello principale del progetto in Git:

   ```
   config/
        logForwarding.yaml
   ```

1. logForwarding.yaml deve contenere metadati e una configurazione simile al seguente formato (ad esempio, viene utilizzato Splunk).

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

   Il **tipo** Il parametro deve essere impostato su LogForwarding e la versione deve essere impostata sulla versione dello schema, ovvero 1.

   Token nella configurazione (ad esempio `${{SPLUNK_TOKEN}}`) rappresentano segreti che non devono essere memorizzati in Git. Dichiarali invece come Cloud Manager  [Variabili di ambiente](/help/implementing/cloud-manager/environment-variables.md) di tipo **segreto**. Assicurati di selezionare **Tutti** come valore a discesa per il campo Service Applied (Servizio applicato), in modo che i registri possano essere inoltrati ai livelli di authoring, pubblicazione e anteprima.

   È possibile impostare valori diversi tra i registri CDN e tutto il resto (registri AEM e Apache), includendo un **cdn** e/o **aem** blocco dopo il **predefinito** , in cui le proprietà possono ignorare quelle definite nel **predefinito** blocco; è necessaria solo la proprietà abilitata. Un possibile caso di utilizzo potrebbe essere l’utilizzo di un indice Splunk diverso per i registri CDN, come illustrato nell’esempio seguente.

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

   Un altro scenario consiste nel disabilitare l’inoltro dei registri CDN o di tutto il resto (registri AEM e Apache). Ad esempio, per inoltrare solo i registri CDN, puoi configurare quanto segue:

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

* Servizi consentiti: è necessario selezionare il BLOB
* Risorse consentite: è necessario selezionare l’oggetto
* Autorizzazioni consentite: è necessario selezionare Scrivi, Aggiungi o Crea
* Una data/ora di inizio e di scadenza valida.

Ecco una schermata di esempio della configurazione del token SAS:

![Configurazione token SAS BLOB di Azure](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)


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

## Rete avanzata {#advanced-networking}

Se hai dei requisiti organizzativi per bloccare il traffico verso la destinazione di registrazione, puoi configurare l’inoltro dei registri in modo che venga eseguito [rete avanzata](/help/security/configuring-advanced-networking.md). Vedere i modelli per i tre tipi di rete avanzati riportati di seguito, che utilizzano un `port` insieme al parametro `host` parametro.

### Uscita flessibile della porta {#flex-port}

Se il traffico di registro si dirige verso una porta diversa da 443 (ad esempio, 8443 di seguito), configura la rete avanzata come segue:

```
{
    "portForwards": [
        {
            "name": "mylogging.service.logger.com",
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
      host: "proxy.tunnel"
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
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
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
      host: "proxy.tunnel"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### VPN {#vpn}

Se il traffico di registro deve passare attraverso una VPN, configura la rete avanzata come segue:

```
{
    "portForwards": [
        {
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
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
      host: "mylogging.service.com"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```
