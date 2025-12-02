---
title: Usa pipeline di configurazione
description: Scopri come utilizzare le pipeline di configurazione per distribuire diverse configurazioni in AEM as a Cloud Service, ad esempio le impostazioni di inoltro del registro, le attività di manutenzione relative all’eliminazione e varie configurazioni CDN.
feature: Operations
role: Admin
exl-id: bd121d31-811f-400b-b3b8-04cdee5fe8fa
source-git-commit: ac04829b63ca5e2fee71f6c71d0730f21c576382
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 2%

---

# Utilizzare le pipeline di configurazione {#config-pipelines}

Scopri come utilizzare le pipeline di configurazione per distribuire diverse configurazioni in AEM as a Cloud Service, ad esempio le impostazioni di inoltro del registro, le attività di manutenzione relative all’eliminazione e varie configurazioni CDN.

## Panoramica {#overview}

Una pipeline di configurazione di Cloud Manager distribuisce i file di configurazione (creati in formato YAML) in un ambiente di destinazione. È possibile configurare in questo modo diverse funzioni in AEM as a Cloud Service, tra cui l’inoltro del registro, le attività di manutenzione relative all’eliminazione e diverse funzioni CDN.

Per i progetti **Distribuzione pubblicazione**, le pipeline di configurazione possono essere distribuite tramite Cloud Manager ai tipi di ambiente di sviluppo, staging e produzione. I file di configurazione possono essere distribuiti in ambienti di sviluppo rapido (RDE) utilizzando [strumenti della riga di comando](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline).

Le pipeline di configurazione possono essere distribuite anche tramite Cloud Manager per **progetti Edge Delivery**.

Nelle sezioni seguenti di questo documento viene fornita una panoramica di informazioni importanti su come utilizzare le pipeline di configurazione e su come strutturare le relative configurazioni. Descrive i concetti generali condivisi tra tutte le funzionalità o un sottoinsieme di quelle supportate dalle pipeline di configurazione.

* [Configurazioni supportate](#configurations) - Elenco di configurazioni che possono essere distribuite con le pipeline di configurazione.
* [Creare e gestire le pipeline di configurazione](#creating-and-managing) - Creare una pipeline di configurazione
* [Sintassi comune](#common-syntax) - Sintassi condivisa tra le configurazioni.
* [Struttura cartella](#folder-structure) - Descrive la struttura prevista dalle pipeline di configurazione per le configurazioni.
* [Variabili di ambiente segrete](#secret-env-vars) - Esempi di utilizzo delle variabili di ambiente per non divulgare i segreti nelle configurazioni.
* [Variabili pipeline segrete](#secret-pipeline-vars) - Esempi di utilizzo delle variabili di ambiente per non divulgare i segreti nelle configurazioni prima dei progetti Edge Delivery Services.

## Configurazioni supportati {#configurations}

La tabella seguente offre un elenco completo di tali configurazioni, con collegamenti alla documentazione dedicata che descrive la sintassi di configurazione specifica e altre informazioni.

| Tipo | Valore `kind` YAML | Descrizione | Consegna pubblicazione | Edge Delivery |
|---|---|---|---|---|
| [Regole filtro traffico, incluso WAF](/help/security/traffic-filter-rules-including-waf.md) | `CDN` | Dichiarare le regole per bloccare il traffico dannoso | X | X |
| [Richiedi trasformazioni](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) | `CDN` | Dichiarare le regole per trasformare la forma della richiesta di traffico | X | X |
| [Trasformazioni risposta](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) | `CDN` | Dichiarare le regole per trasformare la forma della risposta per una determinata richiesta | X | X |
| [Reindirizzamenti lato server](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) | `CDN` | Dichiara reindirizzamenti lato server in stile 301/302 | X | X |
| [Selettori origine](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | Dichiarare le regole per indirizzare il traffico a diversi backend, incluse le applicazioni non Adobe | X | X |
| [Pagine errore CDN](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | Sostituisci la pagina di errore predefinita se non è possibile raggiungere l’origine AEM, facendo riferimento alla posizione del contenuto statico con hosting autonomo nel file di configurazione | X |  |
| [Rimozione CDN](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | Dichiara le chiavi API di rimozione utilizzate per rimuovere la rete CDN | X |  |
| [Token HTTP CDN gestito dal cliente](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | Dichiara il valore della chiave X-AEM-Edge-Key necessaria per chiamare la rete CDN di Adobe da una rete CDN del cliente | X |  |
| [Autenticazione di base](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | Dichiara i nomi utente e le password per una finestra di dialogo di autenticazione di base che protegge alcuni URL. | X | X |
| [Attività di manutenzione Pulizia versione](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Ottimizza l’archivio AEM dichiarando le regole per determinare quando le versioni del contenuto devono essere eliminate | X |  |
| [Attività di manutenzione eliminazione registro di controllo](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Ottimizza il registro di controllo di AEM per migliorare le prestazioni dichiarando regole su quando eliminare i registri | X |  |
| [Attività manutenzione eliminazione flusso di lavoro](/help/operations/maintenance.md) | `MaintenanceTasks` | Riduci al minimo il numero di istanze del flusso di lavoro per migliorare le prestazioni del motore del flusso di lavoro.<br><br>Vedi anche [Rimozione regolare delle istanze del flusso di lavoro](/help/sites-cloud/administering/workflows-administering.md#regular-purging-of-workflow-instances) | X |  |
| [Inoltro registro](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | Configura gli endpoint e le credenziali per l’inoltro dei registri a varie destinazioni, tra cui Archiviazione BLOB di Azure, Datadog, HTTPS, Elasticsearch, Splunk | X | X |
| [Registrazione di un ID client](/help/implementing/developing/open-api-based-apis.md) | `API` | Iscrivi i progetti API Adobe Developer Console in un ambiente AEM specifico registrando l’ID client. Necessario per l’utilizzo di API basate su OpenAPI che richiedono l’autenticazione | X |  |

## Creare e gestire le pipeline di configurazione {#creating-and-managing}

Per informazioni su come creare e configurare **Pipeline di configurazione della distribuzione di pubblicazione**, consulta [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). Durante la creazione di una pipeline di configurazione in Cloud Manager, assicurati di selezionare una **distribuzione di destinazione** anziché **codice full stack** durante la configurazione della pipeline. Come indicato in precedenza, la configurazione per gli RDE viene distribuita utilizzando [strumenti della riga di comando](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline) anziché una pipeline.

Per informazioni su come creare e configurare **pipeline di configurazione di Edge Delivery**, consulta l&#39;articolo [Aggiungere una pipeline di Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).

## Sintassi comune {#common-syntax}

Ogni file di configurazione inizia con proprietà simili al seguente snippet di esempio:

```yaml
   kind: "CDN"
   version: "1"
   metadata: ...
   data: ...
```

| Proprietà | Descrizione | Predefiniti |
|---|---|---|
| `kind` | Stringa che determina il tipo di configurazione, ad esempio inoltro registro, regole del filtro del traffico o trasformazioni richieste | Obbligatorio, nessun valore predefinito |
| `version` | Stringa che rappresenta la versione dello schema | Obbligatorio, nessun valore predefinito |
| `metadata` | (Facoltativo) Contiene un array di stringhe `envTypes` che determina per quali tipi di ambiente viene elaborata la configurazione. Per **Distribuzione pubblicazione** i valori possibili sono `dev`, `stage` e `prod`. Per **Edge Delivery**, deve essere utilizzato solo un valore di `prod`. Ad esempio, se l&#39;array include solo `dev`, la configurazione non viene caricata negli ambienti di staging o di produzione, anche se la configurazione è distribuita lì. | Tutti i tipi di ambiente, ovvero (dev, stage, prod) per la distribuzione delle pubblicazioni o solo prod per Edge Delivery. |

È possibile utilizzare l&#39;utilità `yq` per convalidare localmente la formattazione YAML del file di configurazione (ad esempio, `yq cdn.yaml`).

## Consegna pubblicazione {#yamls-for-aem}

Le configurazioni di **Distribuzione pubblicazione** verranno distribuite in un ambiente di destinazione. Quando si esegue il targeting di più ambienti, è possibile organizzare i diversi file in modi diversi. Ad esempio, se l&#39;array include solo `dev`, la configurazione non viene caricata negli ambienti di staging o di produzione, anche se la configurazione è distribuita lì.

```yaml
   kind: "CDN"
   version: "1"
   metadata:
    envType: ["dev"]
```

### Struttura delle cartelle {#folder-structure}

Una cartella denominata `/config` o simile deve trovarsi nella parte superiore della struttura, con uno o più file YAML in una struttura al di sotto di essa.

Ad esempio:

```text
/config
  cdn.yaml
```

Oppure

```text
/config
  /dev
    cdn.yaml
```

I nomi delle cartelle e dei file sotto `/config` sono arbitrari. Il file YAML, tuttavia, deve includere un valore di proprietà [`kind` valido](#configurations).

In genere, le configurazioni vengono distribuite in tutti gli ambienti. Se tutti i valori delle proprietà sono identici per ciascun ambiente, è sufficiente un singolo file YAML. Tuttavia, è comune che i valori delle proprietà differiscano tra gli ambienti, ad esempio durante il test di un ambiente inferiore.

Le sezioni seguenti illustrano alcune strategie per strutturare i file.

### Un singolo file di configurazione per tutti gli ambienti {#single-file}

La struttura del file è simile alla seguente:

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Utilizza questa struttura quando la stessa configurazione è sufficiente per tutti gli ambienti e per tutti i tipi di configurazione (CDN, inoltro registro e così via). In questo scenario, la proprietà dell&#39;array `envTypes` includerebbe tutti i tipi di ambiente.

```yaml
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

Utilizzando variabili di ambiente (o pipeline) di tipo segreto, è possibile che [proprietà segrete](#secret-env-vars) varino in base all&#39;ambiente, come illustrato dal seguente riferimento a `${{SPLUNK_TOKEN}}`.

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

### Un file separato per tipo di ambiente {#file-per-env}

La struttura del file è simile alla seguente:

```text
/config
  cdn-dev.yaml
  cdn-stage.yaml
  cdn-prod.yaml
  logForwarding-dev.yaml
  logForwarding-stage.yaml
  logForwarding-prod.yaml
```

Utilizza questa struttura quando possono esserci differenze nei valori delle proprietà. Nei file, ci si aspetta che il valore dell&#39;array `envTypes` corrisponda al suffisso. Ad esempio, `cdn-dev.yaml` e `logForwarding-dev.yaml` con valore di `["dev"]`, `cdn-stage.yaml` e `logForwarding-stage.yaml` con valore di `["stage"]` e così via.

### Una cartella per ambiente {#folder-per-env}

In questa strategia, esiste una cartella `config` separata per ogni ambiente, con una pipeline separata dichiarata in Cloud Manager per ogni ambiente.

Questo approccio è particolarmente utile se disponi di più ambienti di sviluppo, ciascuno dei quali ha valori di proprietà univoci.

La struttura del file è simile alla seguente:

```text
/config/dev1
  cdn.yaml
  logForwarding.yaml
/config/dev2
  cdn.yaml
  logForwarding.yaml
/config/prod  
  cdn.yaml
  logForwarding.yaml
```

Una variazione di questo approccio consiste nel mantenere un ramo separato per ogni ambiente.

## Edge Delivery Services {#yamls-for-eds}

Le pipeline di configurazione di Edge Delivery non dispongono di ambienti di sviluppo, staging e produzione separati. Negli ambienti di distribuzione della pubblicazione, le modifiche progrediscono attraverso i livelli di sviluppo, stage e produzione. Al contrario, una pipeline di configurazione di Edge Delivery applica la configurazione direttamente a tutte le mappature di dominio registrate in Cloud Manager per un sito Edge Delivery.


Di conseguenza, distribuisci una struttura di file semplice come:

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Se una regola deve essere diversa per ogni sito Edge Delivery, utilizza la sintassi *when* per distinguere le regole tra loro. Si noti, ad esempio, che il dominio corrisponde a dev.example.com nello snippet seguente, che può essere distinto dal dominio `www.example.com`.

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
    # Block simple path
    - name: block-path
      when:
        allOf:
          - reqProperty: domain
            equals: "dev.example.com"
          - reqProperty: path
            equals: '/block/me'
      action: block
```

Se si include il campo di metadati *envTypes*, deve essere utilizzato solo il valore **prod** (anche omettendo il campo di metadati envTypes va bene). Per il *livello* reqProperty, deve essere utilizzato solo il valore **publish**.

## Variabili di ambiente segrete {#secret-env-vars}

Per evitare che le informazioni riservate vengano archiviate nel controllo del codice sorgente, i file di configurazione supportano variabili di ambiente Cloud Manager di tipo **secret**. Per alcune configurazioni, incluso l’inoltro del registro, le variabili di ambiente segrete sono obbligatorie per alcune proprietà.

Tieni presente che le variabili di ambiente segrete vengono utilizzate per i progetti di distribuzione della pubblicazione; consulta la sezione Variabili segrete della pipeline per i progetti Edge Delivery Services.

Il frammento seguente è un esempio dell&#39;utilizzo della variabile di ambiente segreta `${{SPLUNK_TOKEN}}` nella configurazione.

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

Per informazioni dettagliate sull&#39;utilizzo delle variabili di ambiente, vedere [Variabili di ambiente Cloud Manager](/help/implementing/cloud-manager/environment-variables.md).

## Variabili segrete della pipeline {#secret-pipeline-vars}

Per i progetti Edge Delivery Services, utilizzare le variabili della pipeline Cloud Manager di tipo **secret** in modo che non sia necessario archiviare le informazioni riservate nel controllo del codice sorgente. La casella di selezione *Passaggio applicato* deve utilizzare l&#39;opzione **distribuisci**.

La sintassi è identica al frammento mostrato nella sezione precedente.

Per informazioni dettagliate sull&#39;utilizzo delle variabili di pipeline, vedere [Variabili di pipeline in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).
