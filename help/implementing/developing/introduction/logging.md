---
title: Registrazione per AEM as a Cloud Service
description: Scopri come utilizzare la funzione di registrazione per AEM as a Cloud Service per configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
source-git-commit: 97a1781f0a2d59d2bed7b03c7d4f045c81784f60
workflow-type: tm+mt
source-wordcount: '2797'
ht-degree: 8%

---

# Registrazione per AEM as a Cloud Service {#logging-for-aem-as-a-cloud-service}

AEM as a Cloud Service è una piattaforma che consente ai clienti di includere codice personalizzato per creare esperienze univoche per la propria base di clienti. Tenendo presente questo aspetto, il servizio di registrazione è una funzione fondamentale per eseguire il debug e comprendere l’esecuzione del codice negli ambienti di sviluppo locali e cloud, in particolare negli ambienti di sviluppo dell’as a Cloud Service AEM.

Le impostazioni di registrazione e i livelli di registro as a Cloud Service dall’AEM vengono gestiti in file di configurazione memorizzati come parte del progetto AEM in Git e distribuiti come parte del progetto AEM tramite Cloud Manager. La registrazione in AEM as a Cloud Service può essere suddivisa in due set logici:

* Registrazione AEM, che esegue la registrazione a livello di applicazione AEM
* Registrazione del server web/Dispatcher Apache HTTPD, che esegue la registrazione del server web e del Dispatcher sul livello di pubblicazione.
* La registrazione CDN, indicata dal nome, esegue la registrazione sulla CDN. Questa funzione verrà gradualmente implementata per i clienti a inizio settembre.

## Registrazione AEM {#aem-logging}

La registrazione a livello di applicazione AEM è gestita da tre registri:

1. Registri Java AEM, che restituiscono istruzioni di registrazione Java per l’applicazione AEM.
1. Registri di richieste HTTP, che registrano le informazioni sulle richieste HTTP e le relative risposte fornite dall’AEM
1. Registri di accesso HTTP, che registrano le informazioni di riepilogo e le richieste HTTP gestite dall’AEM

>[!NOTE]
>
>Le richieste HTTP trasmesse dalla cache di Dispatcher del livello di pubblicazione o dalla rete CDN a monte non vengono riportate in questi registri.

## Registrazione Java AEM {#aem-java-logging}

AEM as a Cloud Service fornisce accesso alle istruzioni di registro Java. Gli sviluppatori di applicazioni per AEM devono seguire le best practice generali relative alla registrazione Java, registrando le istruzioni pertinenti sull’esecuzione del codice personalizzato, ai seguenti livelli di registro:

<table>
<tr>
<td>
<b>Ambiente AEM</b></td>
<td>
<b>Livello registro</b></td>
<td>
<b>Descrizione</b></td>
<td>
<b>Disponibilità istruzione di registro</b></td>
</tr>
<tr>
<td>
Ambiente di sviluppo</td>
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

Mentre la registrazione Java supporta diversi altri livelli di granularità della registrazione, AEM as a Cloud Service consiglia di utilizzare i tre livelli descritti in precedenza.

I livelli di registro AEM sono impostati per tipo di ambiente tramite la configurazione OSGi, che a sua volta viene impegnata in Git e implementata tramite Cloud Manager in AEM as a Cloud Service. Per questo motivo, è consigliabile mantenere le istruzioni di registro coerenti e ben note per i tipi di ambiente per garantire che i registri disponibili tramite AEM come Cloud Service siano disponibili al livello di registro ottimale senza richiedere la redistribuzione dell’applicazione con la configurazione a livello di registro aggiornata.

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
<td>21 29.04.2020:50:13,398</td>
</tr>
<tr>
<td>ID nodo as a Cloud Service AEM</td>
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
<td>Nessun approvatore specificato. Impostazione predefinita: [ Gruppo utenti approvatori creativi ]</td>
</tr>
</tbody>
</table>

### Registratori configurazione {#configuration-loggers}

I registri Java AEM sono definiti come configurazione OSGi e quindi sono destinati a ambienti specifici as a Cloud Service AEM utilizzando le cartelle in modalità di esecuzione.

Configura la registrazione Java per i pacchetti Java personalizzati tramite le configurazioni OSGi per la factory Sling LogManager. Sono supportate due proprietà di configurazione:

| Proprietà di configurazione OSGi | Descrizione |
|---|---|
| org.apache.sling.commons.log.names | I pacchetti Java per i quali raccogliere le istruzioni di registro. |
| org.apache.sling.commons.log.level | Livello di registro in cui registrare i pacchetti Java, specificato da org.apache.sling.commons.log.names |

La modifica di altre proprietà di configurazione OSGi LogManager può causare problemi di disponibilità in AEM as a Cloud Service.

Di seguito sono riportati alcuni esempi delle configurazioni di registrazione consigliate (utilizzando il pacchetto Java segnaposto di `com.example`) per i tre tipi di ambiente AEM as a Cloud Service.

### Ambiente di sviluppo {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
}
```

### Ambiente di staging {#stage}

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

## Registrazione richieste HTTP AEM {#aem-http-request-logging}

La registrazione delle richieste HTTP di AEM as a Cloud Service fornisce informazioni approfondite sulle richieste HTTP effettuate all’AEM e sulle relative risposte HTTP in ordine di tempo. Questo registro è utile per comprendere le richieste HTTP effettuate all’AEM e l’ordine in cui vengono elaborate e a cui rispondono.

Per comprendere questo registro, è fondamentale mappare le coppie di richiesta HTTP e risposta in base ai rispettivi ID, indicati dal valore numerico tra parentesi. Spesso le richieste e le risposte corrispondenti presentano altre richieste HTTP e risposte interposte tra loro nel registro.

**Esempio di registro**

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
<td>ID nodo as a Cloud Service AEM</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Configurazione del registro {#configuring-the-log}

Il registro delle richieste HTTP dell’AEM non è configurabile in AEM as a Cloud Service.

## Registrazione accesso HTTP AEM {#aem-http-access-logging}

La registrazione dell’accesso HTTP di Cloud Service in AEM mostra le richieste HTTP in ordine temporale. Ogni voce di registro rappresenta la richiesta HTTP che accede a AEM.

Questo registro è utile per capire rapidamente quali richieste HTTP vengono inviate all’AEM, se queste hanno esito positivo, visualizzando il codice di stato della risposta HTTP associato e il tempo impiegato per completare la richiesta HTTP. Questo registro può essere utile anche per eseguire il debug dell’attività di un utente specifico filtrando le voci del registro in base agli utenti.

**Esempio di output del registro**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| ID nodo as a Cloud Service AEM | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
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

## Registrazione del server web Apache e del Dispatcher {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service fornisce tre registri per i server web Apache e il livello dispatcher sulla pubblicazione:

* Registro accesso server web Apache HTTPD
* Registro errori server web Apache HTTPD
* Registro di Dispatcher

Questi registri sono disponibili solo per il livello di pubblicazione.

Questo set di registri fornisce informazioni approfondite sulle richieste HTTP al livello di pubblicazione as a Cloud Service dall’AEM prima che tali richieste raggiungano l’applicazione AEM. È importante comprendere che, idealmente, la maggior parte delle richieste HTTP ai server di livello Publish sono gestite da contenuto memorizzato nella cache dal server web Apache HTTPD e dal Dispatcher AEM e non raggiungono mai l’applicazione AEM stessa. Pertanto, nei registri Java, Request o Access dell’AEM non sono presenti istruzioni di registro per queste richieste.

### Registro accesso server web Apache HTTPD {#apache-httpd-web-server-access-log}

Il registro di accesso al server web Apache HTTP fornisce istruzioni per ogni richiesta HTTP che raggiunge il server web/Dispatcher del livello di pubblicazione. Le richieste servite da una rete CDN a monte non vengono riportate in questi registri.

Consulta le informazioni sul formato del registro degli errori in [documentazione ufficiale di apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

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
<td>1 maggio 2020:00:09:46 +0000</td>
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
<td>Referer</td>
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

Consulta le informazioni sul formato del registro degli errori in [documentazione ufficiale di apache](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

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
<td>Ven lug 17 02:16:42.608913 2020</td>
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

Può essere impostato su error, warn, info, debug e trace1 - trace8, con il valore predefinito warn. Per eseguire il debug di RewriteRules, si consiglia di aumentare il livello di registro a trace2. Si consiglia di eseguire il debug delle regole di riscrittura utilizzando [SDK di Dispatcher](../../dispatcher/validation-debug.md). Il livello log massimo per AEM as a Cloud Service è `debug`. Pertanto, attualmente non è possibile eseguire il debug delle regole di riscrittura nel cloud.

Consulta la [documentazione del modulo mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) per ulteriori informazioni.

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

## Registro di Dispatcher {#dispatcher-log}

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
<td>Codice di stato della risposta di Dispatcher</td>
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

Sebbene la registrazione di Dispatcher supporti diversi altri livelli di granularità della registrazione, l’as a Cloud Service AEM consiglia di utilizzare i livelli descritti di seguito.

Per impostare il livello di registro per ogni ambiente, utilizza il ramo condizionale appropriato nella `global.var` come descritto di seguito:

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

AEM as a Cloud Service fornisce accesso ai registri CDN, utili per i casi d’uso, inclusa l’ottimizzazione del rapporto di hit della cache. Il formato di registro CDN non può essere personalizzato e non è possibile impostarlo su modalità diverse, ad esempio info, avvertenza o errore.

I registri CDN verranno inoltrati a Splunk per nuove richieste di ticket di supporto per l’inoltro Splunk. I clienti che hanno già abilitato l’inoltro Splunk potranno aggiungere i registri CDN in futuro.

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
| *regole* | I nomi di qualsiasi corrispondenza [regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md) e WAF, che indicano anche se la corrispondenza ha prodotto un blocco. Vuoto se non corrisponde alcuna regola. |


## Come accedere ai registri {#how-to-access-logs}

### Ambienti cloud {#cloud-environments}

È possibile accedere ai registri AEM as a Cloud Service per i servizi cloud scaricandoli tramite l’interfaccia di Cloud Manager oppure scaricandoli dalla riga di comando tramite l’interfaccia della riga di comando di Adobe I/O. Per ulteriori informazioni, vedere [Documentazione di registrazione di Cloud Manager](/help/implementing/cloud-manager/manage-logs.md).

### Registri per aree geografiche di pubblicazione aggiuntive {#logs-for-additional-publish-regions}

Se per un particolare ambiente sono abilitate le Aree geografiche di pubblicazione aggiuntive, i registri di ciascuna area saranno disponibili per il download da Cloud Manager, come indicato in precedenza.

I registri AEM e i registri dispatcher per le aree geografiche di pubblicazione aggiuntive specificheranno la regione nelle prime 3 lettere successive all’ID ambiente, come esemplificato da **nld2** nel campione seguente, che fa riferimento a un’ulteriore istanza pubblicata dell’AEM situata nei Paesi Bassi:

```
cm-p7613-e12700-nld2-aem-publish-bcbb77549-5qmmt 127.0.0.1 - 07/Nov/2023:23:57:11 +0000 "HEAD /libs/granite/security/currentuser.json HTTP/1.1" 200 - "-" "Java/11.0.19"
```

### SDK locale {#local-sdk}

L’SDK as a Cloud Service per AEM fornisce file di registro per supportare lo sviluppo locale.

I registri AEM si trovano nella cartella `crx-quickstart/logs`, in cui è possibile visualizzare i seguenti registri:

* Registro Java AEM: `error.log`
* Registro richieste HTTP AEM: `request.log`
* Registro degli accessi HTTP AEM: `access.log`

I registri del livello Apache, incluso Dispatcher, si trovano nel contenitore Docker che contiene Dispatcher. Consulta la [Documentazione di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) per informazioni su come avviare Dispatcher.

Per recuperare i registri:

1. Nella riga di comando digitare `docker ps` per elencare i contenitori
1. Per accedere al contenitore, digita &quot;`docker exec -it <container> /bin/sh`&quot;, dove `<container>` è l’id contenitore del dispatcher del passaggio precedente
1. Passa alla directory principale della cache in `/mnt/var/www/html`
1. I registri si trovano in `/etc/httpd/logs`
1. Inspect i registri: sono accessibili nella cartella XYZ, dove è possibile visualizzare i seguenti registri:
   * Registro degli accessi al server web Apache HTTPD - `httpd_access.log`
   * Registri di errore del server web Apache HTTPD - `httpd_error.log`
   * Registri di Dispatcher - `dispatcher.log`

I registri vengono stampati direttamente sull&#39;uscita terminale. Nella maggior parte dei casi, questi registri devono essere DEBUG, operazione che può essere eseguita passando il livello Debug come parametro durante l’esecuzione di Docker. Ad esempio:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Debug di produzione e staging {#debugging-production-and-stage}

In circostanze eccezionali, è necessario modificare i livelli di registro per ottenere una granularità più precisa negli ambienti di stage o produzione.

Anche se questo è possibile, richiede modifiche ai livelli di registro nei file di configurazione in Git da Warn and Error to Debug e l’esecuzione di una distribuzione a AEM as a Cloud Service per registrare queste modifiche di configurazione con gli ambienti.

A seconda del traffico e della quantità di istruzioni di registro scritte da Debug, questo può comportare un impatto negativo sulle prestazioni dell’ambiente. Pertanto, si consiglia di modificare i livelli di debug di Stage e Production come segue:

* Fatto con buon senso, e solo se assolutamente necessario
* riportati ai livelli appropriati e ridistribuiti il più presto possibile

## Registri Splunk {#splunk-logs}

I clienti con account Splunk possono richiedere tramite ticket di assistenza clienti che i loro registri di AEM Cloud Service vengano inoltrati all’indice appropriato. I dati di registrazione sono equivalenti a quelli disponibili nei download dei registri di Cloud Manager, ma i clienti potrebbero trovare conveniente utilizzare le funzioni di query disponibili nel prodotto Splunk.

La larghezza di banda di rete associata ai registri inviati a Splunk è considerata parte dell&#39;utilizzo di I/O di rete del cliente.

I registri CDN verranno inoltrati a Splunk per richieste di nuovi ticket di supporto; i clienti che hanno già abilitato l’inoltro Splunk potranno aggiungere i registri CDN in futuro.

### Abilitazione dell’inoltro Splunk {#enabling-splunk-forwarding}

Nella richiesta di supporto, i clienti devono indicare:

* Indirizzo endpoint HEC di tipo Splunk. Questo endpoint deve avere un certificato SSL valido ed essere accessibile al pubblico.
* Indice Splunk
* Porta Splunk
* Token HEC Splunk. Consulta [questa pagina](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples) per ulteriori informazioni.

Le proprietà di cui sopra devono essere specificate per ciascuna combinazione di programma/tipo di ambiente pertinente. Ad esempio, se un cliente desidera ambienti di sviluppo, staging e produzione, deve fornire tre serie di informazioni, come indicato di seguito.

>[!NOTE]
>
>L’inoltro Splunk per ambienti di programmi sandbox non è supportato.

>[!NOTE]
>
>La funzionalità di inoltro Splunk non è possibile da un indirizzo IP in uscita dedicato.

È necessario assicurarsi che la richiesta iniziale includa tutti gli ambienti di sviluppo che devono essere abilitati, oltre agli ambienti di staging/produzione. Splunk deve avere un certificato SSL ed essere rivolto al pubblico.

Se uno qualsiasi dei nuovi ambienti di sviluppo creati dopo la richiesta iniziale deve avere Inoltro Splunk, ma non lo ha abilitato, è necessario effettuare una richiesta aggiuntiva.

Inoltre, se sono stati richiesti ambienti di sviluppo, è possibile che in altri ambienti di sviluppo non inclusi nella richiesta o persino in ambienti sandbox l’inoltro Splunk sia abilitato e che questi condividano un indice Splunk. I clienti possono utilizzare `aem_env_id` per distinguere tra questi ambienti.

Di seguito è riportato un esempio di richiesta di assistenza clienti:

Programma 123, Ambiente produzione

* Indirizzo endpoint HEC Splunk: `splunk-hec-ext.acme.com`
* Indice Splunk: acme_123prod (il cliente può scegliere qualsiasi convenzione di denominazione desideri)
* Porta Splunk: 443
* Token HEC Splunk: ABC123

Programma 123, Stage Env

* Indirizzo endpoint HEC Splunk: `splunk-hec-ext.acme.com`
* Indice Splunk: acme_123stage
* Porta Splunk: 443
* Token HEC Splunk: ABC123

Programma 123, Env sviluppo

* Indirizzo endpoint HEC Splunk: `splunk-hec-ext.acme.com`
* Indice Splunk: acme_123dev
* Porta Splunk: 443
* Token HEC Splunk: ABC123

Può essere sufficiente utilizzare lo stesso indice Splunk per ogni ambiente, nel qual caso `aem_env_type` può essere utilizzato per differenziare in base ai valori dev, stage e prod. Se sono presenti più ambienti di sviluppo, il `aem_env_id` può essere utilizzato anche. Alcune organizzazioni possono scegliere un indice separato per i registri dell’ambiente di produzione se l’indice associato limita l’accesso a un set ridotto di utenti Splunk.

Di seguito è riportato un esempio di voce di registro:

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
file_path: /var/log/aem/error.log
host: 172.34.200.12 
level: INFO
msg: [FelixLogListener] com.adobe.granite.repository Service [5091, [org.apache.jackrabbit.oak.api.jmx.SessionMBean]] ServiceEvent REGISTERED
orig_time: 16.07.2020 08:35:32.346
pod_name: aemloggingall-aem-author-77797d55d4-74zvt
splunk_customer: true
```
