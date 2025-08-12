---
title: Inoltro registro per AEM as a Cloud Service
description: Scopri come inoltrare i registri ai fornitori di accesso in AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '2409'
ht-degree: 3%

---

# Inoltro del registro {#log-forwarding}

>[!NOTE]
>
>L’inoltro del registro è ora configurato in modo self-service, diverso dal metodo legacy, che richiedeva l’invio di un ticket di supporto Adobe. Consulta la sezione [Migrazione](#legacy-migration) se l&#39;inoltro del registro è stato configurato da Adobe.

I clienti con una licenza di un fornitore di registrazione o che ospitano un prodotto di registrazione possono inoltrare i registri di AEM (incluso Apache/Dispatcher) e i registri CDN alla destinazione di registrazione associata. AEM as a Cloud Service supporta le seguenti destinazioni di registrazione:

<table>
  <tbody>
    <tr>
      <th>Tecnologia di registro</th>
      <th>Private Beta*</th>
      <th>AEM</th>
      <th>Dispatcher</th>
      <th>CDN</th>
    </tr>
    <tr>
      <td>Amazon S3</td>
      <td style="background-color: #ffb3b3;">Sì</td>
      <td>Sì</td>
      <td>Sì</td>
      <td style="background-color: #ffb3b3;">No</td>
    </tr>
    <tr>
      <td>Archiviazione BLOB di Azure</td>
      <td>No</td>
      <td>Sì</td>
      <td>Sì</td>
      <td>Sì</td>
    </tr>
    <tr>
      <td>DataDog</td>
      <td>No</td>
      <td>Sì</td>
      <td>Sì</td>
      <td>Sì</td>
    </tr>
    <tr>
      <td>Dynatrace</td>
      <td style="background-color: #ffb3b3;">Sì</td>
      <td>Sì</td>
      <td>Sì</td>
      <td style="background-color: #ffb3b3;">No</td>
    </tr>
    <tr>
      <td>Elasticsearch<br>OpenSearch</td>
      <td>No</td>
      <td>Sì</td>
      <td>Sì</td>
      <td>Sì</td>
    </tr>
    <tr>
      <td>HTTPS</td>
      <td>No</td>
      <td>Sì</td>
      <td>Sì</td>
      <td>Sì</td>
    </tr>
    <tr>
      <td>New Relic</td>
      <td style="background-color: #ffb3b3;">Sì</td>
      <td>Sì</td>
      <td>Sì</td>
      <td style="background-color: #ffb3b3;">No</td>
    </tr>
    <tr>
      <td>Splunk</td>
      <td>No</td>
      <td>Sì</td>
      <td>Sì</td>
      <td>Sì</td>
    </tr>
    <tr>
      <td>Logica sumo</td>
      <td style="background-color: #ffb3b3;">Sì</td>
      <td>Sì</td>
      <td>Sì</td>
      <td style="background-color: #ffb3b3;">No</td>
    </tr>
  </tbody>
</table>
&lt;/html>

>[!NOTE]
>
> Per le tecnologie in Private Beta, invia un&#39;e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per richiedere l&#39;accesso.

L’inoltro dei registri viene configurato in modo self-service dichiarando una configurazione in Git e può essere distribuito tramite pipeline di configurazione Cloud Manager ai tipi di ambiente di sviluppo, staging e produzione. Il file di configurazione può essere implementato negli ambienti di sviluppo rapido (RDE, Rapid Developement Environments) utilizzando gli strumenti della riga di comando.

È disponibile un’opzione per instradare i registri AEM e Apache/Dispatcher tramite l’infrastruttura di rete avanzata di AEM, ad esempio l’IP in uscita dedicato.

La larghezza di banda di rete associata ai registri inviati alla destinazione di registrazione è considerata parte dell&#39;utilizzo di I/O di rete dell&#39;organizzazione.

## Struttura di questo articolo {#how-organized}

Questo articolo è organizzato nel modo seguente:

* Configurazione: comune per tutte le destinazioni di registrazione
* Trasporto e reti avanzate: prima di creare la configurazione di registrazione, è necessario considerare la configurazione della rete
* Registrazione delle configurazioni di destinazione: ogni destinazione ha un formato leggermente diverso
* Formati delle voci di registro: informazioni sui formati delle voci di registro
* Migrazione dall’inoltro di registro legacy: come passare dall’inoltro di registro precedentemente configurato da Adobe all’approccio self-service

## Configurazione {#setup}

1. Creare un file denominato `logForwarding.yaml`. Deve contenere metadati, come descritto nell&#39;articolo [Pipeline di configurazione](/help/operations/config-pipeline.md#common-syntax) (**tipo** deve essere impostato su `LogForwarding` e la versione impostata su &quot;1&quot;), con una configurazione simile alla seguente (ad esempio, si utilizza Splunk).

   ```yaml
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

1. Per tipi di ambiente diversi da RDE (che utilizza strumenti della riga di comando), creare una pipeline di configurazione della distribuzione di destinazione in Cloud Manager, come indicato da [questa sezione](/help/operations/config-pipeline.md#creating-and-managing). Si noti che le pipeline full stack e le pipeline a livello web non distribuiscono il file di configurazione.

1. Distribuisci la configurazione.

I token nella configurazione (ad esempio `${{SPLUNK_TOKEN}}`) rappresentano segreti, che non devono essere memorizzati in Git. Dichiarale invece come [Variabili di ambiente segrete](/help/operations/config-pipeline.md#secret-env-vars) di Cloud Manager. Assicurarsi di selezionare **Tutti** come valore a discesa per il campo Servizio applicato, in modo che i registri possano essere inoltrati ai livelli di authoring, pubblicazione e anteprima.

È possibile impostare valori diversi tra i registri CDN e i registri AEM (incluso Apache/Dispatcher), includendo un blocco **cdn** e/o **aem** aggiuntivo dopo il blocco **default**, in cui le proprietà possono ignorare quelle definite nel blocco **default**. È richiesta solo la proprietà abilitata. Un possibile caso di utilizzo potrebbe essere l’utilizzo di un indice Splunk diverso per i registri CDN, come illustrato nell’esempio seguente.

```yaml
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

Un altro scenario consiste nel disabilitare l’inoltro dei registri CDN o dei registri di AEM (incluso Apache/Dispatcher). Ad esempio, per inoltrare solo i registri CDN, puoi configurare quanto segue:

```yaml
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

## Trasporto e reti avanzate {#transport-advancednetworking}

Alcune organizzazioni scelgono di limitare il traffico che può essere ricevuto dalle destinazioni di registrazione, altre potrebbero richiedere l’uso di porte diverse da HTTPS (443).  In tal caso [La rete avanzata](/help/security/configuring-advanced-networking.md) dovrà essere configurata prima di distribuire la configurazione di inoltro del registro.

Utilizzare la tabella seguente per verificare quali sono i requisiti per la configurazione avanzata di rete e registrazione in base al fatto che si utilizzi o meno la porta 443 e che i registri debbano essere visualizzati da un indirizzo IP fisso.

<table>
  <tbody>
    <tr>
      <th>Porta di destinazione</th>
      <th>È necessario che i registri vengano visualizzati da IP fissi?</th>
      <th>Necessità di reti avanzate</th>
      <th>Definizione porta LogForwarding.yaml necessaria</th>
    </tr>
    <tr>
      <td rowspan="2" ro>HTTPS (443)</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Sì</td>
      <td>Sì, <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">uscita dedicata</a></td>
      <td>No</td>
    <tr>
    <tr>
      <td rowspan="2">Porta non standard (es. 8088)</td>
      <td>No</td>
      <td>Sì, <a href="/help/security/configuring-advanced-networking.md#flexible-port-egress-flexible-port-egress">Uscita flessibile</a></td>
      <td>Sì</td>
    </tr>
    <tr>
      <td>Sì</td>
      <td>Sì, <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">uscita dedicata</a></td>
      <td>Sì</td>
  </tbody>
</table>
&lt;/html>

>[!NOTE]
>La visualizzazione dei registri da un singolo indirizzo IP dipende dalla configurazione di rete avanzata scelta.  Per facilitare questa fase, è necessario utilizzare un’uscita dedicata.
>
> La configurazione di rete avanzata è un [processo in due fasi](/help/security/configuring-advanced-networking.md#configuring-and-enabling-advanced-networking-configuring-enabling) che richiede l&#39;abilitazione a livello di programma e ambiente.

Per i registri di AEM (incluso Apache/Dispatcher), se hai configurato [Rete avanzata](/help/security/configuring-advanced-networking.md), puoi utilizzare la proprietà `aem.advancedNetworking` per inoltrarli da un indirizzo IP in uscita dedicato o tramite una VPN.

L’esempio seguente mostra come configurare la registrazione su una porta HTTPS standard con rete avanzata.

```yaml
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

Per i registri CDN, puoi inserire nell&#39;elenco Consentiti gli indirizzi IP, come descritto in [Documentazione Fastly - Elenco IP pubblici](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Se l’elenco di indirizzi IP condivisi è troppo grande, puoi inviare traffico a un server https o a un archivio BLOB di Azure (non Adobe) in cui è possibile scrivere una logica per inviare i registri da un IP noto alla destinazione finale.

>[!NOTE]
>
>Non è possibile che i registri CDN vengano visualizzati dallo stesso indirizzo IP da cui vengono visualizzati i registri di AEM, perché i registri vengono inviati direttamente da Fastly e non da AEM Cloud Service.

## Registrazione della configurazione di destinazione {#logging-destinations}

Di seguito sono elencate le configurazioni per le destinazioni di registrazione supportate, insieme a eventuali considerazioni specifiche.

### Amazon S3 {#amazons3}

L’inoltro dei registri ad Amazon S3 supporta i registri di AEM e Dispatcher; i registri CDN non sono ancora supportati.

>[!NOTE]
>
>Registri scritti periodicamente in S3, ogni 10 minuti per ogni tipo di file di registro.  Questo può causare un ritardo iniziale nella scrittura dei registri in S3, una volta che la funzione è attivata.  [Ulteriori informazioni su questo comportamento](https://docs.fluentbit.io/manual/pipeline/outputs/s3#differences-between-s3-and-other-fluent-bit-outputs).

```yaml
kind: "LogForwarding"
version: "1.0"
metadata:
  envTypes: ["dev"]
data:
  awsS3:
    default:
      enabled: true
      region: "your-bucket-region"
      bucket: "your_bucket_name"
      accessKey: "${{AWS_S3_ACCESS_KEY}}"
      secretAccessKey: "${{AWS_S3_SECRET_ACCESS_KEY}}"
```

Per utilizzare il server di inoltro registro S3, è necessario preconfigurare un utente IAM di AWS con i criteri appropriati per l’accesso al bucket S3.  Per informazioni su come creare le credenziali utente IAM, consulta la [documentazione utente di AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

I criteri IAM devono consentire all&#39;utente di utilizzare `s3:putObject`.  Ad esempio:

```json
 {
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": [
            "s3:PutObject"
        ],
        "Resource": "arn:aws:s3:::your_bucket_name/*"
    }]
}
```

Per ulteriori informazioni su come implementare, consulta la [documentazione sui criteri bucket di AWS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html).

### Archiviazione BLOB di Azure {#azureblob}

```yaml
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

Se i registri non vengono più consegnati dopo il corretto funzionamento precedente, verificare se il token SAS configurato è ancora valido, in quanto potrebbe essere scaduto.

#### Registri CDN archiviazione BLOB di Azure {#azureblob-cdn}

Ogni server di registrazione distribuito a livello globale produrrà un nuovo file ogni pochi secondi, nella cartella `aemcdn`. Una volta creato, il file non verrà più aggiunto a. Il formato del nome file è YYY-MM-DDThh:mm:ss.sss-uniqueid.log. Ad esempio, 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

Ad esempio, a un certo punto del tempo:

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

E poi 30 secondi dopo:

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

Ogni file contiene più voci di registro json, ciascuna su una riga separata. I formati delle voci di registro sono descritti in [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) e ogni voce di registro include anche le proprietà aggiuntive menzionate nella sezione [Formati di voce di registro](#log-formats) seguente.

#### Registri AEM archiviazione BLOB di Azure {#azureblob-aem}

I registri di AEM (incluso Apache/Dispatcher) vengono visualizzati sotto una cartella con la seguente convenzione di denominazione:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

In ogni cartella verrà creato un singolo file che verrà aggiunto a. I clienti sono responsabili dell’elaborazione e della gestione di questo file, in modo che non aumenti troppo.

Consulta i formati delle voci di registro in [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Le voci di registro includeranno anche le proprietà aggiuntive menzionate nella sezione [Formati di voce di registro](#log-formats) seguente.

### Datadog {#datadog}

```yaml
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

#### Considerazioni

* Crea una chiave API, senza alcuna integrazione con un provider cloud specifico.
* La proprietà tags è facoltativa
* Per i registri di AEM, il tag di origine Datadog è impostato su uno dei seguenti valori: `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` o `aemhttpderror`
* Per i registri CDN, il tag di origine Datadog è impostato su `aemcdn`
* Il tag del servizio Datadog è impostato su `adobeaemcloud`, ma è possibile sovrascriverlo nella sezione dei tag
* Se la pipeline di acquisizione utilizza i tag Datadog per determinare l’indice appropriato per i registri di inoltro, verifica che tali tag siano configurati correttamente nel file YAML di inoltro del registro. I tag mancanti possono impedire l’acquisizione corretta del registro, se la pipeline dipende da essi.

### Elasticsearch e OpenSearch {#elastic}

```yaml
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

#### Considerazioni

* per impostazione predefinita, la porta è 443. Facoltativamente, può essere sostituito con una proprietà denominata `port`
* Per le credenziali, assicurati di utilizzare le credenziali di distribuzione anziché le credenziali dell’account. Queste sono le credenziali generate in una schermata che potrebbe assomigliare a questa immagine:

![Credenziali distribuzione elastica](/help/implementing/developing/introduction/assets/ec-creds.png)

* Per i registri di AEM, `index` è impostato su uno di `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` o `aemhttpderror`
* La proprietà della pipeline opzionale deve essere impostata sul nome della pipeline di acquisizione Elasticsearch o OpenSearch, che può essere configurata per instradare la voce di registro all’indice appropriato. Il tipo di processore della pipeline deve essere impostato su *script* e il linguaggio di script su *indolore*. Di seguito è riportato un frammento di script di esempio per instradare le voci di registro in un indice come aemaccess_dev_26_06_2024:

```text
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```yaml
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

#### Considerazioni

* La stringa URL deve includere **https://**, altrimenti la convalida non riuscirà.
* L’URL può includere una porta. Ad esempio, `https://example.com:8443/aem_logs/aem`. Se nella stringa URL non è inclusa alcuna porta, viene utilizzata la porta 443 (la porta HTTPS predefinita).

#### Registri CDN HTTPS {#https-cdn}

Le richieste Web (POST) verranno inviate in modo continuo, con un payload json che è un array di voci di registro, con il formato di voce di registro descritto in [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md#cdn-log). Proprietà aggiuntive sono menzionate nella sezione [Formati di voce di registro](#log-formats) di seguito.

Esiste anche una proprietà denominata `sourcetype`, impostata sul valore `aemcdn`.

>[!NOTE]
>
> Prima dell&#39;invio della prima voce di registro CDN, il server HTTP deve completare una richiesta una tantum: una richiesta inviata al percorso ``/.well-known/fastly/logging/challenge`` deve rispondere con un asterisco ``*`` nel corpo e il codice di stato 200.

#### Registri HTTPS AEM {#https-aem}

Per i registri di AEM (incluso apache/dispacher), le richieste web (POST) verranno inviate in modo continuo, con un payload json che è un array di voci di registro, con i vari formati di voci di registro come descritto in [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Proprietà aggiuntive sono menzionate nella sezione [Formati di voce di registro](#log-formats) di seguito.

Esiste anche una proprietà denominata `Source-Type`, impostata su uno dei seguenti valori:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### API registro New Relic {#newrelic-https}

L’inoltro del registro a New Relic sfrutta l’API HTTPS di New Relic per l’acquisizione.  Attualmente supporta solo i registri di AEM e Dispatcher; i registri CDN non sono ancora supportati.

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
  data:
    newRelic:
      default:
        enabled: true
        uri: "https://log-api.newrelic.com/log/v1"
        apiKey: "${{NR_API_KEY}}"
```

>[!NOTE]
>
>L’inoltro dei registri a New Relic è disponibile solo per gli account New Relic di proprietà del cliente.
>
>Invia un&#39;e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per richiedere l&#39;accesso.
>
>New Relic fornisce endpoint specifici per l’area geografica in base alla posizione in cui è stato eseguito il provisioning dell’account New Relic.  Per ulteriori informazioni, consulta la [documentazione di New Relic](https://docs.newrelic.com/docs/logs/log-api/introduction-log-api/#endpoint).

### API registro Dynatrace {#dynatrace-https}

L’inoltro del registro a Dynatrace sfrutta l’API HTTPS di Dynatrace per l’acquisizione.  Attualmente supporta solo i registri di AEM e Dispatcher; i registri CDN non sono ancora supportati.

L’attributo di ambito &quot;Ingest Logs&quot; (Acquisisci registri) è obbligatorio per il token.

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
  data:
    dynatrace:
      default:
        enabled: true
        environmentId: "${{DYNATRACE_ENVID}}"
        token: "${{DYNATRACE_TOKEN}}"  
```

>[!NOTE]
>
> Invia un&#39;e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per richiedere l&#39;accesso.

### Splunk {#splunk}

```yaml
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

#### Considerazioni

* Per impostazione predefinita, la porta è 443. Facoltativamente, può essere sostituito con una proprietà denominata `port`.
* Il campo sourcetype avrà uno dei seguenti valori, a seconda del registro specifico: *aemaccess*, *aemerror*,
  *aemrequest*, *aemdispatcher*, *aemhttpdaccess*, *aemhttpderror*, *aemcdn*
* Se gli IP richiesti sono stati inseriti nell&#39;elenco Consentiti e i registri non vengono ancora consegnati, verifica che non vi siano regole firewall che impongono la convalida del token Splunk. Fastly esegue un passaggio di convalida iniziale in cui viene inviato intenzionalmente un token Splunk non valido. Se il firewall è impostato in modo da interrompere le connessioni con token Splunk non validi, il processo di convalida non riuscirà e Fastly non sarà in grado di consegnare i registri all’istanza Splunk.

>[!NOTE]
>
> [Se si esegue la migrazione di](#legacy-migration) da Log Forwarding legacy a questo modello self-service, i valori del campo `sourcetype` inviati all&#39;indice Splunk potrebbero essere cambiati, quindi apportare le modifiche necessarie.

### Logica sumo {#sumologic}

L’inoltro dei registri alla logica di riepilogo supporta i registri di AEM e Dispatcher; i registri CDN non sono ancora supportati.

Durante la configurazione di Sumo Logic per l’acquisizione dei dati, viene visualizzato un &quot;indirizzo HTTP Source&quot; che fornisce l’host, l’URI del ricevitore e la chiave privata in una singola stringa.  Ad esempio:

`https://collectors.de.sumologic.com/receiver/v1/http/ZaVnC...`

È necessario copiare l&#39;ultima sezione dell&#39;URL (senza `/` precedente) e aggiungerla come [Variabile di ambiente segreta di CloudManager](/help/operations/config-pipeline.md#secret-env-vars) come descritto nella sezione [Configurazione](#setup) precedente, quindi fare riferimento a tale variabile nella configurazione.  Di seguito è riportato un esempio.

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  sumologic:
    default:
      enabled: true
      collectorURL: "https://collectors.de.sumologic.com/receiver/v1/http"
      privateKey: "${{SUMOLOGIC_PRIVATE_KEY}}"
      index: "aem-logs"
```

>[!NOTE]
> Per sfruttare la funzionalità del campo &quot;indice&quot; è necessario un abbonamento Sumo Logic Enterprise.  I registri delle sottoscrizioni non Enterprise verranno instradati alla partizione `sumologic_default` come standard.  Per ulteriori informazioni, vedere la [documentazione sul partizionamento logico Sumo](https://help.sumologic.com/docs/search/optimize-search-partitions/).

## Formati voce registro {#log-formats}

Consulta [Registrazione per AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) per il formato di ciascun tipo di registro (registri CDN e registri AEM, incluso Apache/Dispatcher).

Poiché i registri provenienti da più programmi e ambienti possono essere inoltrati alla stessa destinazione di registrazione, oltre all’output descritto nell’articolo sulla registrazione, in ogni voce di registro verranno incluse le seguenti proprietà:

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

Ad esempio, le proprietà potrebbero avere i seguenti valori:

```text
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## Migrazione dall’inoltro registro legacy {#legacy-migration}

Prima di raggiungere la configurazione di Log Forwarding tramite un modello self-service, ai clienti veniva richiesto di aprire i ticket di supporto, dove Adobe avviava l’integrazione.

I clienti che sono stati configurati in questo modo da Adobe sono invitati ad adattarsi al modello self-service quando lo desiderano. Ci sono diversi motivi per effettuare questa transizione:

* È stato eseguito il provisioning di un nuovo ambiente (ad esempio, un nuovo ambiente di sviluppo o RDE).
* Modifiche all’endpoint o alle credenziali Splunk esistenti.
* Adobe ha configurato l’inoltro dei registri prima che fossero disponibili i registri CDN e desideri ricevere i registri CDN.
* Una decisione consapevole di adattarsi in modo proattivo al modello self-service in modo che l’organizzazione disponga delle conoscenze necessarie anche prima che sia necessario un cambiamento sensibile al tempo.

Per eseguire la migrazione, è sufficiente configurare il file YAML come descritto nelle sezioni precedenti. Utilizza la pipeline di configurazione Cloud Manager per distribuire in ciascuno degli ambienti in cui deve essere applicata la configurazione.

È consigliabile, ma non obbligatorio, distribuire una configurazione in tutti gli ambienti in modo che siano tutti sotto il controllo self-service. In caso contrario, potresti dimenticare quali ambienti sono stati configurati da Adobe rispetto a quelli configurati in modo self-service.

>[!NOTE]
>
>È possibile che i valori del campo `sourcetype` inviati all&#39;indice Splunk siano stati modificati, quindi apportare le modifiche necessarie.
>
>Quando l’inoltro dei registri viene distribuito in un ambiente configurato in precedenza dal supporto Adobe, è possibile che vengano visualizzati registri duplicati per un massimo di alcune ore. Questo alla fine si risolverà automaticamente.
