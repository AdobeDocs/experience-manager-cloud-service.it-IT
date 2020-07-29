---
title: Registrazione
description: Scoprite come configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
translation-type: tm+mt
source-git-commit: c7100f53ce38cb8120074ec4eb9677fb7303d007
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 3%

---


# Registrazione {#logging}

AEM come Cloud Service è una piattaforma che consente ai clienti di includere codice personalizzato per creare esperienze univoche per la propria base di clienti. In questo senso, la registrazione è una funzione fondamentale per eseguire il debug e comprendere l&#39;esecuzione del codice sullo sviluppo locale e gli ambienti cloud, in particolare l&#39;AEM come un ambiente di sviluppo  Cloud Service.

AEM livelli di registrazione e di registro vengono gestiti in file di configurazione memorizzati come parte del progetto AEM in Git e distribuiti come parte del progetto AEM tramite Cloud Manager. L&#39;accesso AEM come Cloud Service può essere suddiviso in due set logici:

* Registrazione AEM, che esegue la registrazione a livello di applicazione AEM
* Registrazione Apache HTTPD Web Server/Dispatcher, che esegue la registrazione del server Web e di Dispatcher sul livello di pubblicazione.

## Registrazione AEM {#aem-loggin}

La registrazione a livello di applicazione AEM è gestita da tre registri:

1. AEM registri Java, che eseguono il rendering delle istruzioni di registrazione Java per l&#39;applicazione AEM.
1. Registri di richieste HTTP, che registrano le informazioni sulle richieste HTTP e le risposte fornite da AEM
1. Registri di accesso HTTP, quali informazioni di riepilogo del registro e richieste HTTP inviate da AEM

Notate che le richieste HTTP servite dalla cache Dispatcher del livello di pubblicazione o dalla rete CDN upstream non si riflettono in questi registri.

## Registrazione Java AEM {#aem-java-logging}

AEM come Cloud Service  fornisce l&#39;accesso alle istruzioni di registro Java. Gli sviluppatori di applicazioni per AEM devono seguire le best practice generali di registrazione Java, registrare le relative istruzioni sull&#39;esecuzione di codice personalizzato, ai seguenti livelli di registro:

<table>
<tr>
<td>
<b>Ambiente AEM</b></td>
<td>
<b>Livello registro</b></td>
<td>
<b>Descrizione</b></td>
<td>
<b>Disponibilità dell'istruzione del registro</b></td>
</tr>
<tr>
<td>
Sviluppo</td>
<td>
DEBUG</td>
<td>
Descrive cosa accade nell'applicazione.<br>

Quando la registrazione DEBUG è attiva, le istruzioni che forniscono un&#39;immagine chiara delle attività che si verificano e tutti i parametri chiave che influenzano l&#39;elaborazione vengono registrate.</td>
<td>
<ul>
<li> Sviluppo locale</li>
<li>Sviluppo</li>
</ul></td>
</tr>
<tr>
<td>
Area di visualizzazione</td>
<td>
AVVISO</td>
<td>
Descrive le condizioni che possono diventare errori.<br>
Quando la registrazione WARN è attiva, vengono registrate solo le istruzioni che indicano i condizionatori che si stanno avvicinando alla sub-ottimizzazione.</td>
<td>
<ul>
<li> Sviluppo locale</li>
<li>Sviluppo</li>
<li>Area di visualizzazione</li>
</ul></td>
</tr>
<tr>
<td>
Produzione</td>
<td>
ERRORE</td>
<td>
Descrive le condizioni che indicano un errore e che devono essere risolte.<br>
Quando la registrazione degli errori è attiva, vengono registrate solo le istruzioni che indicano gli errori. Le istruzioni del registro degli errori indicano un problema grave che dovrebbe essere risolto il prima possibile.</td>
<td>
<ul>
<li> Sviluppo locale</li>
<li>Sviluppo</li>
<li>Area di visualizzazione</li>
<li>Produzione</li>
</ul></td>
</tr>
</table>

Sebbene la registrazione Java supporti diversi altri livelli di granularità della registrazione, AEM come Cloud Service consiglia di utilizzare i tre livelli descritti in precedenza.

AEM livelli di registro vengono impostati per tipo di ambiente tramite la configurazione OSGi, che a sua volta si impegna per Git, e distribuiti tramite Cloud Manager per AEM come Cloud Service. Per questo motivo, è meglio mantenere le istruzioni di registro coerenti e ben note per i tipi di ambiente, al fine di garantire che i log disponibili tramite AEM come Cloud Service siano disponibili al livello di registro ottimale senza richiedere la ridistribuzione dell&#39;applicazione con la configurazione aggiornata del livello di registro.

### Formato registro {#log-format}

| Data e ora | AEM come ID di codice Cloud Service | Livello registro | Thread | Classe Java | Messaggio registro |
|---|---|---|---|---|---|
| 29.04.2020 21:50:13.398 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` | `*DEBUG*` | qtp2130572036-1472 | com.example.approval.workflow.impl.CustomApprovalWorkflow | Nessun approver specificato, impostazione predefinita per il gruppo di utenti di [ Creative Approvers ] |

**Esempio di output del registro**

`22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge`
`22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials`
`22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms`
`22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED`
`22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring`

### Registratori di configurazione {#configuration-loggers}

AEM registri Java sono definiti come configurazione OSGi, e quindi indirizzati AEM specifici come ambienti Cloud Service di  utilizzando le cartelle in modalità di esecuzione.

Configurare la registrazione Java per i pacchetti Java personalizzati tramite le configurazioni OSGi per la fabbrica Sling LogManager. Esistono due proprietà di configurazione supportate:

| OSGi, proprietà Configuration | Descrizione |
|---|---|
| org.apache.sling.commons.log.names | I pacchetti Java per i quali raccogliere le istruzioni di registro. |
| org.apache.sling.commons.log.level | Il livello di registro a cui registrare i pacchetti Java, specificato da org.apache.sling.commons.log.names |

La modifica di altre proprietà di configurazione LogManager OSGi potrebbe causare problemi di disponibilità in AEM come Cloud Service.

Di seguito sono riportati alcuni esempi delle configurazioni di registrazione consigliate (che utilizzano il pacchetto Java segnaposto di `com.example`) per i tre AEM come tipi di ambiente di Cloud Service.

### Sviluppo {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
}
```

### Stadio {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
}
```

### Produzione {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
}
```

## Registrazione richiesta HTTP AEM {#aem-http-request-logging}

AEM come registrazione di richieste HTTP  fornisce informazioni approfondite sulle richieste HTTP effettuate a AEM e le relative risposte HTTP in ordine di tempo. Questo registro è utile per comprendere le richieste HTTP effettuate per AEM e l’ordine in cui sono elaborate e a cui hanno risposto.

La chiave per comprendere questo registro è la mappatura delle coppie di richieste e risposte HTTP in base agli ID, indicati dal valore numerico tra parentesi. Spesso le richieste e le risposte corrispondenti hanno altre richieste HTTP e risposte inserite nel registro.

### Formato registro {#http-request-logging-format}

| Data e ora | ID coppia richiesta/risposta |  | Metodo HTTP | URL | Protocollo | AEM come ID nodo Cloud Service |
|---|---|---|---|---|---|---|
| 29/Apr/2020:19:14:21 +0000 | `[137]` | -> | POST | /conf/global/settings/dam/adminui-extension/metadata-profile/ | HTTP/1.1 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` |

**Esempio di registro**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

### Configurazione del registro {#configuring-the-log}

Il registro AEM richieste HTTP non è configurabile in AEM come Cloud Service.

## Registrazione AEM accesso HTTP {#aem-http-access-logging}

AEM come registrazione di accesso HTTP Cloud Service, vengono visualizzate le richieste HTTP in ordine temporale. Ogni voce di registro rappresenta la richiesta HTTP che accede a AEM.

Questo registro è utile per comprendere rapidamente a quali richieste HTTP vengono inviate per AEM, se riuscite guardando il codice di stato della risposta HTTP corrispondente e per quanto tempo è necessario completare la richiesta HTTP. Questo registro può essere utile anche per eseguire il debug dell&#39;attività di un utente specifico filtrando le voci di registro per Utenti.

### Formato registro {#access-log-format}
