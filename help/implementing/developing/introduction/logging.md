---
title: Registrazione per AEM as a Cloud Service
description: Scopri come utilizzare la funzione di registrazione per AEM as a Cloud Service per configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
feature: Log Files, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2556'
ht-degree: 9%

---

# Registrazione per AEM as a Cloud Service {#logging-for-aem-as-a-cloud-service}

AEM as a Cloud Service è una piattaforma che consente ai clienti di includere codice personalizzato per creare esperienze univoche per la propria base di clienti. Tenendo presente questo aspetto, il servizio di registrazione è una funzione fondamentale per eseguire il debug e comprendere l’esecuzione del codice negli ambienti di sviluppo locali e cloud, in particolare negli ambienti di sviluppo di AEM as a Cloud Service.

Le impostazioni di registrazione e i livelli di registro di AEM as a Cloud Service vengono gestiti in file di configurazione memorizzati come parte del progetto AEM in Git e distribuiti come parte del progetto AEM tramite Cloud Manager. La registrazione in AEM as a Cloud Service può essere suddivisa in tre set logici:

* Registrazione AEM, che esegue la registrazione a livello di applicazione AEM
* Registrazione del server web/Dispatcher Apache HTTPD, che esegue la registrazione del server web e di Dispatcher sul livello di pubblicazione.
* La registrazione CDN, indicata dal nome, esegue la registrazione sulla CDN.

## Registrazione AEM {#aem-logging}

La registrazione a livello di applicazione AEM è gestita da tre registri:

1. Registri Java di AEM, che eseguono il rendering delle istruzioni di registrazione Java per l’applicazione AEM.
1. Registri di richieste HTTP, che registrano le informazioni sulle richieste HTTP e le relative risposte fornite da AEM
1. Registri di accesso HTTP, che registrano informazioni di riepilogo e richieste HTTP gestite da AEM

>[!NOTE]
>
>Le richieste HTTP che vengono servite dalla cache Dispatcher del livello di pubblicazione o dalla rete CDN a monte non vengono riportate in questi registri.

## Registrazione Java AEM {#aem-java-logging}

AEM as a Cloud Service fornisce accesso alle istruzioni di registro Java. Gli sviluppatori di applicazioni per AEM devono seguire le best practice generali per la registrazione Java, registrando le istruzioni pertinenti sull’esecuzione del codice personalizzato, ai seguenti livelli di registro:

<table>
<tr>
<td>
<b>Ambiente AEM</b></td>
<td>
<b>Livello registro</b></td>
<td>
<b>Descrizione</b></td>
<td>
<b>Disponibilità istruzione registro</b></td>
</tr>
<tr>
<td>
Sviluppo</td>
<td>
DEBUG</td>
<td>
Descrive cosa sta accadendo nell’applicazione.<br>
Quando la registrazione DEBUG è attiva, vengono registrate le istruzioni che forniscono un’immagine chiara delle attività che si verificano ed eventuali parametri chiave che influiscono sull’elaborazione.</td>
<td>
<ul>
<li> Sviluppo locale</li>
<li>Ambiente di sviluppo</li>
</ul></td>
</tr>
<tr>
<td>
Ambiente di staging</td>
<td>
AVVISO</td>
<td>
Descrive le condizioni che possono diventare errori.<br>
Quando la registrazione WARN è attiva, vengono registrate solo le istruzioni che indicano le condizionali che si stanno avvicinando alla sub-ottimizzazione.</td>
<td>
<ul>
<li> Sviluppo locale</li>
<li>Ambiente di sviluppo</li>
<li>Ambiente di staging</li>
</ul></td>
</tr>
<tr>
<td>
Produzione</td>
<td>
ERRORE </td>
<td>
Descrive le condizioni che indicano un errore e che devono essere risolte.<br>
Quando la registrazione degli errori è attiva, vengono registrate solo le istruzioni che indicano errori. Le istruzioni del registro degli ERRORI indicano un problema grave che deve essere risolto il prima possibile.</td>
<td>
<ul>
<li> Sviluppo locale</li>
<li>Ambiente di sviluppo</li>
<li>Ambiente di staging</li>
<li>Produzione</li>
</ul></td>
</tr>
</table>

Sebbene la registrazione Java supporti diversi altri livelli di granularità della registrazione, AEM as a Cloud Service consiglia di utilizzare i tre livelli descritti in precedenza.

I livelli di registro di AEM sono impostati per tipo di ambiente tramite la configurazione OSGi, che a sua volta viene eseguita su Git e distribuita tramite Cloud Manager in AEM as a Cloud Service. Per questo motivo, è consigliabile mantenere coerenza e conoscenza delle istruzioni di registro per i tipi di ambiente in modo che i registri disponibili tramite AEM as Cloud Service siano disponibili al livello di registro ottimale senza richiedere la ridistribuzione dell’applicazione con la configurazione a livello di registro aggiornata.

>[!NOTE]
>
>Per garantire un monitoraggio efficace degli ambienti dei clienti, non modificare il livello di registro predefinito. Inoltre, non modificare il formato di registrazione predefinito. L’output del registro deve rimanere indirizzato ai file predefiniti. Consulta [la sezione seguente](#configuration-loggers) per le linee guida specifiche.

**Esempio di output del registro**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

**Formato registro**

<table>
<tbody>
<tr>
<td>Data e ora</td>
<td>29.04.2020 21:50:13,398</td>
</tr>
<tr>
<td>ID nodo AEM as a Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>Livello di registro</td>
<td>DEBUG</td>
</tr>
<tr>
<td>Thread</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Classe Java</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>Messaggio di registro</td>
<td>Nessun approvatore specificato. Impostazione predefinita: [ Gruppo utenti approvatori Creative ]</td>
</tr>
</tbody>
</table>

### Registratori configurazione {#configuration-loggers}

I registri Java di AEM sono definiti come configurazione OSGi e sono quindi destinati a ambienti AEM as a Cloud Service specifici utilizzando le cartelle in modalità di esecuzione.

Configura la registrazione Java per i pacchetti Java personalizzati tramite le configurazioni OSGi per la factory Sling LogManager. Sono supportate tre proprietà di configurazione:

| Proprietà di configurazione OSGi | Descrizione |
|---|---|
| `org.apache.sling.commons.log.names` | I pacchetti Java per i quali raccogliere le istruzioni di registro. |
| `org.apache.sling.commons.log.level` | Livello di log in cui registrare i pacchetti Java, specificato da `org.apache.sling.commons.log.names` |

La modifica di altre proprietà di configurazione OSGi LogManager può causare problemi di disponibilità in AEM as a Cloud Service.

Come indicato in una sezione precedente, per garantire un monitoraggio efficace degli ambienti dei clienti:

* Il livello di registro della configurazione di registro predefinita di AEM (Configurazione di registrazione Sling Apache) non deve essere modificato dal valore predefinito &quot;INFO&quot;.
* È accettabile impostare i livelli di registro su DEBUG per i singoli pacchetti di codice prodotto (utilizzando le istanze della factory di configurazione OSGi &quot;Apache Sling Logging Logger configuration&quot;), ma utilizzarlo con moderazione per evitare il deterioramento delle prestazioni e ripristinare su INFO quando non è più necessario.
* È accettabile regolare i livelli di registro per il codice sviluppato dal cliente.
* Tutti i registri, sia per il codice del prodotto AEM che per il codice sviluppato dal cliente, devono mantenere il formato di registrazione predefinito.
* L&#39;output del log deve rimanere indirizzato al file predefinito &quot;logs/error.log&quot;.

A tal fine, non è necessario apportare modifiche alle seguenti proprietà OSGi:

* **Configurazione registro Apache Sling** (PID: `org.apache.sling.commons.log.LogManager`): *tutte le proprietà*
* **Configurazione logger registrazione Sling Apache** (PID di fabbrica: `org.apache.sling.commons.log.LogManager.factory.config`):

   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

Di seguito sono riportati alcuni esempi delle configurazioni di registrazione consigliate (utilizzando il pacchetto Java segnaposto di `com.example`) per i tre tipi di ambiente AEM as a Cloud Service.

### Sviluppo {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### Fase {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### Produzione {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

## Registrazione richieste HTTP AEM {#aem-http-request-logging}

La registrazione delle richieste HTTP di AEM as a Cloud Service fornisce ad insight le richieste HTTP effettuate ad AEM e le relative risposte HTTP in ordine temporale. Questo registro è utile per comprendere le richieste HTTP effettuate ad AEM e l’ordine in cui vengono elaborate e a cui rispondono.

Per comprendere questo registro, è fondamentale mappare le coppie di richiesta HTTP e risposta in base ai rispettivi ID, indicati dal valore numerico tra parentesi. Spesso le richieste e le risposte corrispondenti presentano altre richieste HTTP e risposte interposte tra loro nel registro.

**Registro di esempio**

```
29/Apr/2020:19:14:21 +0000 [137] > POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] > GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

**Formato registro**

<table>
<tbody>
<tr>
<td>Data e ora</td>
<td>29 aprile 2020:19:14:21 +0000</td>
</tr>
<tr>
<td>ID coppia richiesta/risposta</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>Metodo HTTP</td>
<td>POST</td>
</tr>
<tr>
<td>URL</td>
<td>/conf/global/settings/dam/adminui-extension/metadataprofile/</td>
</tr>
<tr>
<td>Protocollo</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>ID nodo AEM as a Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Configurazione del registro {#configuring-the-log}

Il registro richieste HTTP di AEM non è configurabile in AEM as a Cloud Service.

## Registrazione accesso HTTP AEM {#aem-http-access-logging}

La registrazione degli accessi HTTP in AEM as Cloud Service mostra le richieste HTTP in ordine temporale. Ogni voce di registro rappresenta la richiesta HTTP che accede ad AEM.

Questo registro è utile per comprendere rapidamente quali richieste HTTP vengono effettuate ad AEM, se l’esito è positivo, visualizzando il codice di stato della risposta HTTP associato e il tempo impiegato per completare la richiesta HTTP. Questo registro può essere utile anche per eseguire il debug dell’attività di un utente specifico filtrando le voci del registro in base agli utenti.

**Esempio di output del registro**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| ID nodo AEM as a Cloud Service | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| Indirizzo IP del client | - |
| User | myuser@adobe.com |
| Data e ora | 30 aprile 2020:17:37:14 +0000 |
| metodo HTTP | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| Protocollo | HTTP/1.1 |
| Stato della risposta HTTP | 200 |
| Dimensione del corpo della risposta in byte | 1141 |
| Referrer | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| Agente utente | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### Configurazione del registro di accesso HTTP {#configuring-the-http-access-log}

Il registro dell’accesso HTTP non è configurabile in AEM as a Cloud Service.

## Registrazione del server web Apache e di Dispatcher {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service fornisce tre registri per i server web Apache e il livello dispatcher sulla pubblicazione:

* Registro accesso server web Apache HTTPD
* Registro errori server web Apache HTTPD
* Registro Dispatcher

Questi registri sono disponibili solo per il livello di pubblicazione.

Questo set di registri fornisce informazioni approfondite sulle richieste HTTP al livello di pubblicazione AEM as a Cloud Service prima che tali richieste raggiungano l’applicazione AEM. È importante comprendere che, idealmente, la maggior parte delle richieste HTTP ai server di livello Publish sono gestite da contenuto memorizzato nella cache dal server web Apache HTTPD e da AEM Dispatcher e non raggiungono mai l’applicazione AEM stessa. Pertanto, nei registri Java, Request o Access di AEM non sono presenti istruzioni di registro per queste richieste.

### Registro accesso server web Apache HTTPD {#apache-httpd-web-server-access-log}

Il registro di accesso al server web Apache HTTP fornisce istruzioni per ogni richiesta HTTP che raggiunge il server web/Dispatcher del livello di pubblicazione. Le richieste servite da una rete CDN a monte non vengono riportate in questi registri.

Consulta le informazioni sul formato del registro errori nella [documentazione ufficiale di Apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

**Esempio di output del registro**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

**Formato registro**

<table>
<tbody>
<tr>
<td>ID nodo di AEM as a Cloud Service</td>
<td>cm-p1234-e26813-aem-publish-5c787687c-lqlxr</td>
</tr>
<tr>
<td>Indirizzo IP del client</td>
<td>-</td>
</tr>
<tr>
<td>User</td>
<td>-</td>
</tr>
<tr>
<td>Data e ora</td>
<td>01/Maggio/2020:00:09:46 +0000</td>
</tr>
<tr>
<td>Metodo HTTP</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/example.html</td>
</tr>
<tr>
<td>Protocollo</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>Stato risposta HTTP</td>
<td>200</td>
</tr>
<tr>
<td>Dimensione</td>
<td>310</td>
</tr>
<tr>
<td>Referrer</td>
<td>-</td>
</tr>
<tr>
<td>Agente utente</td>
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, come Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Configurazione del registro di accesso al server web Apache HTTPD {#configuring-the-apache-httpd-webs-server-access-log}

Questo registro non è configurabile in AEM as a Cloud Service.

## Registro errori server web Apache HTTPD {#apache-httpd-web-server-error-log}

Il registro errori del server web Apache HTTP fornisce istruzioni per ogni errore nel server web/Dispatcher del livello di pubblicazione.

Consulta le informazioni sul formato del registro errori nella [documentazione ufficiale di Apache](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

**Esempio di output del registro**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**Formato registro**

<table>
<tbody>
<tr>
<td>Data e ora</td>
<td>Ven, 17 Luglio 02:16:42.608913 2020</td>
</tr>
<tr>
<td>Livello di evento</td>
<td>[mpm_worker:notice]</td>
</tr>
<tr>
<td>ID processo</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>Nome del pod</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>Messaggio</td>
<td>AH00094: Riga di comando: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D PRIMO PIANO -D </td>
</tr>
</tbody>
</table>

### Configurazione del registro errori del server web Apache HTTPD {#configuring-the-apache-httpd-web-server-error-log}

I livelli di log mod_rewrite sono definiti dalla variabile REWRITE_LOG_LEVEL nel file `conf.d/variables/global.var`.

Può essere impostato su error, warn, info, debug e trace1 - trace8, con il valore predefinito warn. Per eseguire il debug di RewriteRules, si consiglia di aumentare il livello di registro a trace2. È consigliabile eseguire il debug delle regole di riscrittura utilizzando [Dispatcher SDK](../../dispatcher/validation-debug.md). Il livello di registro massimo per AEM as a Cloud Service è `debug`. Pertanto, attualmente non è possibile eseguire il debug delle regole di riscrittura nel cloud.

Per ulteriori informazioni, consulta la [documentazione del modulo mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging).

Per impostare il livello di registro per ogni ambiente, utilizza il ramo condizionale appropriato nel file global.var, come descritto di seguito:

```
Define REWRITE_LOG_LEVEL debug

<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL error
  ...
</IfDefine>
```

## Registro Dispatcher {#dispatcher-log}

**Esempio**

```
[17/Jul/2020:23:48:06 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures.html" - 475ms [publishfarm/0] [action miss] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/climbing-new-zealand/_jcr_content/root/responsivegrid/carousel/item_1571266094599.coreimg.jpeg/1473680817282/sport-climbing.jpeg" 302 10ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/ski-touring-mont-blanc/_jcr_content/root/responsivegrid/carousel/item_1571168419252.coreimg.jpeg/1572047288089/adobestock-238230356.jpeg" 302 11ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
```

**Formato registro**

<table>
<tbody>
<tr>
<td>Data e ora</td>
<td>[17 luglio 2020:23:48:16 +0000]</td>
</tr>
<tr>
<td>Nome pod</td>
<td>[cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr]</td>
</tr>
<tr>
<td>Protocollo</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Codice di stato della risposta Dispatcher</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Durata</td>
<td>1949 ms</td>
</tr>
<tr>
<td>Farm</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>Stato cache</td>
<td>[azione mancante]</td>
</tr>
<tr>
<td>Host</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### Configurazione del registro errori di Dispatcher {#configuring-the-dispatcher-error-log}

I livelli di registro del dispatcher sono definiti dalla variabile DISP_LOG_LEVEL nel file `conf.d/variables/global.var`.

Può essere impostato su error, warn, info, debug e trace1, con il valore predefinito warn.

Sebbene la registrazione Dispatcher supporti diversi altri livelli di granularità della registrazione, AEM as a Cloud Service consiglia di utilizzare i livelli descritti di seguito.

Per impostare il livello di registro per ogni ambiente, utilizzare il ramo condizionale appropriato nel file `global.var`, come descritto di seguito:

```
Define DISP_LOG_LEVEL debug

<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL error
  ...
</IfDefine>
```

>[!NOTE]
>
>Per gli ambienti AEM as a Cloud Service, debug è il livello di dettaglio massimo. Il livello del registro di traccia non è supportato, pertanto è consigliabile evitare di impostarlo quando si lavora in ambienti cloud.

## Registro CDN {#cdn-log}

AEM as a Cloud Service fornisce l’accesso ai registri CDN, utili per i casi d’uso, inclusa l’ottimizzazione della percentuale di hit della cache. Il formato di registro CDN non può essere personalizzato e non è possibile impostarlo su modalità diverse, ad esempio info, avvertenza o errore.

**Esempio**

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

**Formato registro**

I registri CDN sono distinti dagli altri registri in quanto sono conformi al formato json.

| **Nome campo** | **Descrizione** |
|---|---|
| *marca temporale* | Ora di inizio della richiesta, dopo la chiusura di TLS |
| *ttfb* | Abbreviazione per *Time To First Byte*. L’intervallo di tempo compreso tra l’inizio della richiesta e il momento prima che il corpo della risposta inizi a essere trasmesso in streaming. |
| *cli_ip* | Indirizzo IP del client. |
| *cli_country* | Codice paese a due lettere [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) alfa-2 del paese client. |
| *rid* | Il valore dell’intestazione di richiesta utilizzato per identificare in modo univoco la richiesta. |
| *req_ua* | L’agente utente responsabile di effettuare una determinata richiesta HTTP. |
| *host* | Autorità a cui è destinata la richiesta. |
| *url* | Il percorso completo, inclusi i parametri di query. |
| *metodo* | Metodo HTTP inviato dal client, ad esempio “GET” o “POST”. |
| *res_ctype* | Tipo di contenuto utilizzato per indicare il tipo di file multimediale originale della risorsa. |
| *cache* | Stato della cache. I valori possibili sono HIT, MISS o PASS |
| *stato* | Il codice di stato HTTP come valore intero. |
| *res_age* | Il tempo (in secondi) in cui una risposta è stata memorizzata nella cache (in tutti i nodi). |
| *pop* | Centro dati del server cache CDN. |
| *regole* | Nomi delle [regole del filtro del traffico](/help/security/traffic-filter-rules-including-waf.md) e dei flag di WAF corrispondenti, che indicano anche se la corrispondenza ha generato un blocco. Vuoto se non corrisponde alcuna regola. |

I registri CDN possono essere estesi con le tue proprietà utilizzando [trasformazioni di richiesta/risposta](/help/implementing/dispatcher/cdn-configuring-traffic.md#logproperty).

## Come accedere ai registri {#how-to-access-logs}

### Ambienti cloud {#cloud-environments}

È possibile accedere ai registri di AEM as a Cloud Service per Cloud Services scaricandoli tramite l’interfaccia di Cloud Manager o scaricandoli dalla riga di comando tramite l’interfaccia della riga di comando di Adobe I/O. Per ulteriori informazioni, vedere la [documentazione di registrazione di Cloud Manager](/help/implementing/cloud-manager/manage-logs.md).

### Registri per aree geografiche di pubblicazione aggiuntive {#logs-for-additional-publish-regions}

Se per un particolare ambiente sono abilitate ulteriori aree di pubblicazione, i registri di ciascuna area saranno disponibili per il download da Cloud Manager, come indicato in precedenza.

I registri di AEM e i registri del dispatcher per le aree di pubblicazione aggiuntive specificheranno l’area nelle prime 3 lettere dopo l’ID ambiente, come esemplificato da **nld2** nell’esempio seguente, che fa riferimento a un’ulteriore istanza di pubblicazione di AEM situata nei Paesi Bassi:

```
cm-p7613-e12700-nld2-aem-publish-bcbb77549-5qmmt 127.0.0.1 - 07/Nov/2023:23:57:11 +0000 "HEAD /libs/granite/security/currentuser.json HTTP/1.1" 200 - "-" "Java/11.0.19"
```

### SDK locale {#local-sdk}

AEM as a Cloud Service SDK fornisce file di registro per supportare lo sviluppo locale.

I registri di AEM si trovano nella cartella `crx-quickstart/logs`, dove è possibile visualizzare i seguenti registri:

* Registro Java AEM: `error.log`
* Registro richieste HTTP AEM: `request.log`
* Registro dell&#39;accesso HTTP di AEM: `access.log`

I registri del livello Apache, incluso Dispatcher, si trovano nel contenitore Docker che contiene Dispatcher. Consulta la [documentazione di Dispatcher](/help/implementing/dispatcher/disp-overview.md) per informazioni su come avviare Dispatcher.

Per recuperare i registri:

1. Nella riga di comando, digitare `docker ps` per elencare i contenitori
1. Per accedere al contenitore, digita &quot;`docker exec -it <container> /bin/sh`&quot;, dove `<container>` è l&#39;ID del contenitore del dispatcher del passaggio precedente
1. Passa alla directory principale della cache in `/mnt/var/www/html`
1. I registri si trovano in `/etc/httpd/logs`
1. Esamina i registri: sono accessibili nella cartella XYZ, dove è possibile visualizzare i seguenti registri:
   * Registro di accesso al server web Apache HTTPD - `httpd_access.log`
   * Registri errori server web Apache HTTPD - `httpd_error.log`
   * Registri Dispatcher - `dispatcher.log`

I registri vengono stampati direttamente sull&#39;uscita terminale. Nella maggior parte dei casi, questi registri devono essere DEBUG, operazione che può essere eseguita passando il livello Debug come parametro durante l’esecuzione di Docker. Ad esempio:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Debug di produzione e staging {#debugging-production-and-stage}

In circostanze eccezionali, è necessario modificare i livelli di registro per ottenere una granularità più precisa negli ambienti di stage o produzione.

Anche se questo è possibile, richiede modifiche ai livelli di registro nei file di configurazione in Git da Warn and Error to Debug e l’esecuzione di una distribuzione in AEM as a Cloud Service per registrare tali modifiche di configurazione negli ambienti.

A seconda del traffico e della quantità di istruzioni di registro scritte da Debug, questo può comportare un impatto negativo sulle prestazioni dell’ambiente. Pertanto, si consiglia di modificare i livelli di debug di Stage e Production come segue:

* Fatto con buon senso, e solo se assolutamente necessario
* riportati ai livelli appropriati e ridistribuiti il più presto possibile

## Inoltro del registro {#log-forwarding}

Anche se i registri possono essere scaricati da Cloud Manager, per alcune organizzazioni è utile inoltrarli a una destinazione di registrazione preferita. AEM supporta i registri di streaming per le seguenti destinazioni:

* Archiviazione BLOB di Azure
* Datadog
* HTTPD
* Elasticsearch (e OpenSearch)
* Splunk

Per informazioni dettagliate su come configurare questa funzione, consulta l&#39;[articolo sull&#39;inoltro del registro](/help/implementing/developing/introduction/log-forwarding.md).

>[!NOTE]
>
>L’inoltro dei registri per gli ambienti di programmi sandbox non è supportato.
