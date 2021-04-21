---
title: Registrazione di AEM come Cloud Service
description: Scopri come configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati in AEM come Cloud Service.
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
translation-type: tm+mt
source-git-commit: e87b71dd5081b95ca3fd55e66455476c85a50f6c
workflow-type: tm+mt
source-wordcount: '2332'
ht-degree: 3%

---

# Registrazione di AEM come Cloud Service {#logging-for-aem-as-a-cloud-service}

AEM come Cloud Service è una piattaforma che consente ai clienti di includere codice personalizzato per creare esperienze univoche per la propria base di clienti. Tenendo presente questo aspetto, la registrazione è una funzione fondamentale per eseguire il debug e comprendere l’esecuzione del codice sullo sviluppo locale e gli ambienti cloud, in particolare gli ambienti AEM come ambienti di sviluppo del Cloud Service.

AEM livelli di log e di log vengono gestiti in file di configurazione memorizzati come parte del progetto AEM in Git e distribuiti come parte del progetto AEM tramite Cloud Manager. L&#39;accesso AEM come Cloud Service può essere suddiviso in due set logici:

* Registrazione AEM, che esegue la registrazione a livello di applicazione AEM
* Registrazione server Web/Dispatcher HTTPD di Apache, che esegue la registrazione del server web e del Dispatcher sul livello di pubblicazione.

## Registrazione AEM {#aem-loggin}

La registrazione a livello di applicazione AEM è gestita da tre registri:

1. AEM i registri Java, che eseguono il rendering delle istruzioni di registrazione Java per l’applicazione AEM.
1. Registri di richiesta HTTP, che registrano le informazioni sulle richieste HTTP e le loro risposte fornite da AEM
1. Registri di accesso HTTP, che registrano le informazioni di riepilogo e le richieste HTTP servite da AEM

>[!NOTE]
>
>Le richieste HTTP servite dalla cache del Dispatcher del livello di pubblicazione o dalla rete CDN a monte non vengono riportate in questi registri.

## AEM registrazione Java {#aem-java-logging}

AEM come Cloud Service fornisce l&#39;accesso alle istruzioni di registro Java. Gli sviluppatori di applicazioni per AEM devono seguire le best practice generali sulla registrazione Java, registrare istruzioni pertinenti sull’esecuzione del codice personalizzato, ai seguenti livelli di log:

<table>
<tr>
<td>
<b>Ambiente AEM</b></td>
<td>
<b>Livello registro</b></td>
<td>
<b>Descrizione</b></td>
<td>
<b>Disponibilità del registro</b></td>
</tr>
<tr>
<td>
Sviluppo</td>
<td>
DEBUG</td>
<td>
Descrive cosa accade nell'applicazione.<br>
Quando la registrazione DEBUG è attiva, vengono registrate le istruzioni che forniscono un’immagine chiara delle attività che si verificano e di tutti i parametri chiave che influenzano l’elaborazione.</td>
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
Descrive le condizioni che indicano un errore e devono essere risolte.<br>
Quando la registrazione di ERRORI è attiva, vengono registrate solo le istruzioni che indicano errori. Le istruzioni del registro degli errori indicano un problema grave che deve essere risolto il prima possibile.</td>
<td>
<ul>
<li> Sviluppo locale</li>
<li>Sviluppo</li>
<li>Area di visualizzazione</li>
<li>Produzione</li>
</ul></td>
</tr>
</table>

Mentre la registrazione Java supporta diversi altri livelli di granularità della registrazione, AEM come Cloud Service consiglia di utilizzare i tre livelli descritti sopra.

AEM I livelli di registro sono impostati per tipo di ambiente tramite la configurazione OSGi, che a sua volta si impegna a utilizzare Git, e vengono distribuiti tramite Cloud Manager per AEM come Cloud Service. Per questo motivo, è meglio mantenere le istruzioni di registro coerenti e ben note per i tipi di ambiente, al fine di garantire che i registri disponibili tramite AEM come Cloud Service siano disponibili a livello di log ottimale senza richiedere la ridistribuzione dell’applicazione con la configurazione aggiornata del livello di log.

**Esempio di output del registro**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

**Formato del registro**

<table>
<tbody>
<tr>
<td>Data e ora</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>AEM come ID nodo Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>Livello di log</td>
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
<td>Messaggio di log</td>
<td>Nessun approvatore specificato, impostazione predefinita per [ gruppo di utenti di Creative Approvers ]</td>
</tr>
</tbody>
</table>

### Registratori di configurazione {#configuration-loggers}

I registri Java AEM sono definiti come configurazione OSGi e quindi indirizzati AEM specifici come ambienti di Cloud Service utilizzando le cartelle in modalità di esecuzione.

Configura la registrazione java per i pacchetti Java personalizzati tramite le configurazioni OSGi per la fabbrica Sling LogManager. Sono disponibili due proprietà di configurazione supportate:

| Proprietà di configurazione OSGi | Descrizione |
|---|---|
| org.apache.sling.commons.log.names | I pacchetti Java per i quali raccogliere le istruzioni di registro. |
| org.apache.sling.commons.log.level | Il livello di log a cui registrare i pacchetti Java, specificato da org.apache.sling.commons.log.names |

La modifica di altre proprietà di configurazione OSGi di LogManager può causare problemi di disponibilità in AEM come Cloud Service.

Di seguito sono riportati alcuni esempi delle configurazioni di registrazione consigliate (utilizzando il pacchetto Java segnaposto di `com.example`) per i tre tipi di ambiente AEM come Cloud Service.

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

AEM come registrazione delle richieste HTTP del Cloud Service fornisce informazioni approfondite sulle richieste HTTP effettuate a AEM e sulle relative risposte HTTP in ordine temporale. Questo registro è utile per comprendere le richieste HTTP effettuate a AEM e l’ordine in cui vengono elaborate e a cui rispondono.

La chiave per comprendere questo registro è la mappatura delle coppie di richieste e risposte HTTP in base ai loro ID, identificate dal valore numerico tra parentesi. Tieni presente che spesso le richieste e le risposte corrispondenti hanno altre richieste HTTP e risposte incrociate tra loro nel registro.

**Esempio di log**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

**Formato del registro**

<table>
<tbody>
<tr>
<td>Data e ora</td>
<td>29/Apr/2020:19:14:21 +0000</td>
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
<td>AEM come ID nodo Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Configurazione del registro {#configuring-the-log}

Il registro AEM richiesta HTTP non è configurabile in AEM come Cloud Service.

## Registrazione AEM accesso HTTP {#aem-http-access-logging}

AEM come registrazione Cloud Service degli accessi HTTP mostra le richieste HTTP in ordine temporale. Ogni voce di registro rappresenta la richiesta HTTP che accede a AEM.

Questo registro è utile per comprendere rapidamente quali richieste HTTP vengono effettuate per AEM, se riescono guardando il codice di stato della risposta HTTP che accompagna e quanto tempo la richiesta HTTP ha impiegato per essere completata. Questo registro può anche essere utile per eseguire il debug di un&#39;attività specifica di un utente filtrando le voci di registro da Utenti.

**Esempio di output del registro**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

**Formato del registro**

<table>
<tbody>
<tr>
<td>AEM come ID nodo Cloud Service</td>
<td>cm-p1235-e2644-aem-author-59555cb5b8-8kgr2</td>
</tr>
<tr>
<td>Indirizzo IP del client</td>
<td>-</td>
</tr>
<tr>
<td>User</td>
<td>myuser@adobe.com</td>
</tr>
<tr>
<td>Data e ora</td>
<td>30/Apr/2020:17:37:14 +0000</td>
</tr>
<tr>
<td>metodo HTTP</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css</td>
</tr>
<tr>
<td>Protocollo</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>Stato della risposta HTTP</td>
<td>200</td>
</tr>
<tr>
<td>Tempo di richiesta HTTP in millisecondi</td>
<td>1 141</td>
</tr>
<tr>
<td>Referrer</td>
<td><code>"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"</code></td>
</tr>
<tr>
<td>Agente utente</td>
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, come Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Configurazione del registro di accesso HTTP {#configuring-the-http-access-log}

Il registro di accesso HTTP non è configurabile in AEM come Cloud Service.

## Registrazione di Apache Web Server e Dispatcher {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service fornisce tre registri per il livello Apache Web Server e dispatcher nella pubblicazione:

* Registro di accesso al server Web HTTPD di Apache
* Registro degli errori del server web HTTPD di Apache
* Registro di Dispatcher

Questi registri sono disponibili solo per il livello di pubblicazione.

Questo set di registri fornisce informazioni sulle richieste HTTP al AEM come livello di pubblicazione del Cloud Service prima che tali richieste raggiungano l’applicazione AEM. Questo è importante da comprendere in quanto, idealmente, la maggior parte delle richieste HTTP ai server del livello di pubblicazione sono servite da contenuti memorizzati nella cache da Apache HTTPD Web Server e AEM Dispatcher e non arrivano mai all’applicazione AEM stessa. Pertanto non ci sono istruzioni di registro per queste richieste nei registri AEM Java, Request o Access.

### Registro di accesso al server Web HTTPD di Apache {#apache-httpd-web-server-access-log}

Il registro di accesso Apache HTTP Web Server fornisce istruzioni per ogni richiesta HTTP che raggiunge il server Web/Dispatcher del livello Publish. Tieni presente che le richieste che vengono servite da una rete CDN a monte non vengono riportate in questi registri.

Consulta le informazioni sul formato del registro degli errori nella [documentazione ufficiale di apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

**Esempio di output del registro**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

**Formato del registro**

<table>
<tbody>
<tr>
<td>ID nodo AEM as a Cloud Service</td>
<td>cm-p1234-e26813-aem-publish-5c787687c-lqlxr</td>
</tr>
<tr>
<td>Indirizzo IP del client</td>
<td>-</td>
</tr>
<tr>
<td>Utente</td>
<td>-</td>
</tr>
<tr>
<td>Data e ora</td>
<td>01/maggio/2020:00:09:46 +0000</td>
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
<td>Stato della risposta HTTP</td>
<td>200</td>
</tr>
<tr>
<td>Dimensione</td>
<td>310</td>
</tr>
<tr>
<td>Referente</td>
<td>-</td>
</tr>
<tr>
<td>Agente utente</td>
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, come Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Configurazione del registro di accesso al server Web HTTPD di Apache {#configuring-the-apache-httpd-webs-server-access-log}

Questo registro non è configurabile in AEM come Cloud Service.

## Registro degli errori del server web HTTPD di Apache {#apache-httpd-web-server-error-log}

Il registro degli errori del server Web HTTP Apache fornisce istruzioni per ogni errore nel server Web/Dispatcher del livello di pubblicazione.

Consulta le informazioni sul formato del registro degli errori nella [documentazione ufficiale di apache](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

**Esempio di output del registro**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**Formato del registro**

<table>
<tbody>
<tr>
<td>Data e ora</td>
<td>Venerdì 17 luglio 02:16:42.608913 2020</td>
</tr>
<tr>
<td>Livello evento</td>
<td>[mpm_worker:Notice]</td>
</tr>
<tr>
<td>ID processo</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>Nome del contenitore</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>Messaggio</td>
<td>AH00094: Riga di comando: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### Configurazione del registro degli errori del server Web HTTPD di Apache {#configuring-the-apache-httpd-web-server-error-log}

I livelli di registro mod_rewrite sono definiti dalla variabile REWRITE_LOG_LEVEL nel file `conf.d/variables/global.var`.

Può essere impostato su Errore, Avverti, Informazioni, Debug e Trace1 - Trace8, con un valore predefinito Avverti. Per eseguire il debug di RewriteRules, si consiglia di elevare il livello di log a Trace2.

Per ulteriori informazioni, consulta la [documentazione del modulo mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) .

Per impostare il livello di log per ambiente, utilizza il ramo condizionale appropriato nel file global.var, come descritto di seguito:

```
Define REWRITE_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL Error
  ...
</IfDefine>
```

## Registro del dispatcher {#dispatcher-log}

**Esempio**

```
[17/Jul/2020:23:48:06 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures.html" - 475ms [publishfarm/0] [action miss] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/climbing-new-zealand/_jcr_content/root/responsivegrid/carousel/item_1571266094599.coreimg.jpeg/1473680817282/sport-climbing.jpeg" 302 10ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/ski-touring-mont-blanc/_jcr_content/root/responsivegrid/carousel/item_1571168419252.coreimg.jpeg/1572047288089/adobestock-238230356.jpeg" 302 11ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
```

**Formato del registro**

<table>
<tbody>
<tr>
<td>Data e ora</td>
<td>[17/lug/2020:23:48:16 +000]</td>
</tr>
<tr>
<td>Nome Pod</td>
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
<td>Codice di stato della risposta del dispatcher</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Durata</td>
<td>1949 ms</td>
</tr>
<tr>
<td>Azienda agricola</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>Stato della cache</td>
<td>[azione mancante]</td>
</tr>
<tr>
<td>Host</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### Configurazione del registro degli errori del dispatcher {#configuring-the-dispatcher-error-log}

I livelli di log del dispatcher sono definiti dalla variabile DISP_LOG_LEVEL nel file `conf.d/variables/global.var`.

Può essere impostato su Errore, Avverti, Informazioni, Debug e Trace1, con un valore predefinito Avverti.

Mentre la funzione di log del Dispatcher supporta diversi altri livelli di granularità della registrazione, la AEM come Cloud Service consiglia di utilizzare i livelli descritti di seguito.

Per impostare il livello di registro per ambiente, utilizza il ramo condizionale appropriato nel file `global.var` come descritto di seguito:

```
Define DISP_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL Error
  ...
</IfDefine>
```

## Come accedere ai registri {#how-to-access-logs}

### Ambienti cloud {#cloud-environments}

È possibile accedere ai registri AEM come Cloud Service per i servizi cloud scaricando tramite l’interfaccia di Cloud Manager o inserendo nella riga di comando i registri nella riga di comando utilizzando l’interfaccia della riga di comando di Adobe I/O. Per ulteriori informazioni, consulta la [documentazione sulla registrazione di Cloud Manager](/help/implementing/cloud-manager/manage-logs.md).

### SDK locale {#local-sdk}

AEM as a Cloud Service SDK fornisce file di registro per supportare lo sviluppo locale.

I registri AEM si trovano nella cartella `crx-quickstart/logs`, in cui è possibile visualizzare i seguenti registri:

* Registro Java AEM: `error.log`
* Registro delle richieste HTTP AEM: `request.log`
* Registro di accesso HTTP AEM: `access.log`

I registri di livello Apache, incluso il dispatcher, si trovano nel contenitore Docker che contiene il Dispatcher. Per informazioni su come avviare il Dispatcher, consulta la [documentazione di Dispatcher](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) .

Per recuperare i registri:

1. Nella riga di comando, digita `docker ps` per elencare i contenitori
1. Per accedere al contenitore, digita &quot;`docker exec -it <container> /bin/sh`&quot;, dove `<container>` è l’ID del contenitore del dispatcher del passaggio precedente
1. Passa alla directory principale della cache in `/mnt/var/www/html`
1. I log si trovano sotto `/etc/httpd/logs`
1. Inspect registra: sono accessibili nella cartella XYZ, dove è possibile visualizzare i seguenti registri:
   * Registro di accesso al server Web HTTPD di Apache - `httpd_access.log`
   * Log degli errori del server web HTTPD di Apache - `httpd_error.log`
   * Log del dispatcher - `dispatcher.log`

I registri vengono inoltre stampati direttamente nell&#39;uscita terminale. Nella maggior parte dei casi, questi log devono essere DEBUG, che può essere realizzato passando il livello Debug come parametro durante l&#39;esecuzione di Docker. Esempio:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Debug di produzione e stage {#debugging-production-and-stage}

In circostanze eccezionali, è necessario modificare i livelli di registro per accedere a una granularità più precisa negli ambienti Stage o Production.

Anche se questo è possibile, richiede modifiche ai livelli di registro nei file di configurazione in Git da Avverti ed Errore a Debug ed esegue una distribuzione da AEM come Cloud Service per registrare queste modifiche di configurazione con gli ambienti.

A seconda del traffico e della quantità di istruzioni di registro scritte da Debug, questo può causare un impatto negativo sulle prestazioni sull&#39;ambiente, pertanto, si consiglia di modificare i livelli di debug di Stage e Production:

* Fatto in modo giudizioso, e solo quando assolutamente necessario
* Ripristino dei livelli appropriati e ridistribuzione al più presto

## Registri Splunk {#splunk-logs}

I clienti che dispongono di account Splunk possono richiedere tramite ticket di assistenza clienti che i propri registri di Cloud Service AEM vengano inoltrati all’indice appropriato. I dati di registrazione equivalgono a quelli disponibili tramite i download del registro di Cloud Manager, ma i clienti potrebbero avere comodo sfruttare le funzioni di query disponibili nel prodotto Splunk.

La larghezza di banda di rete associata ai log inviati a Splunk è considerata parte dell&#39;utilizzo di I/O di rete del cliente.

### Abilitazione dell&#39;inoltro splunk {#enabling-splunk-forwarding}

Nella richiesta di assistenza, i clienti devono indicare:

* Indirizzo endpoint HEC Splunk
* Indice Splunk
* Porta Splunk
* Il token Splunk HEC. Per ulteriori informazioni, consulta [questa pagina](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples) .

Le proprietà di cui sopra devono essere specificate per ciascuna combinazione di programmi/tipi di ambiente pertinente.  Ad esempio, se un cliente desidera ambienti di sviluppo, staging e produzione, deve fornire tre set di informazioni, come indicato di seguito.

>[!NOTE]
>
>L&#39;inoltro di Splunk per ambienti di programmi sandbox non è supportato.

Assicurati che la richiesta iniziale includa tutti gli ambienti di sviluppo che devono essere abilitati, oltre agli ambienti stage/prod.

Se dopo la richiesta iniziale sono stati creati nuovi ambienti di sviluppo per cui è previsto l’inoltro Splunk, ma non è stato abilitato , è necessario effettuare una richiesta aggiuntiva.

Inoltre, se sono stati richiesti ambienti di sviluppo, è possibile che altri ambienti di sviluppo non inclusi nella richiesta o persino negli ambienti sandbox abbiano abilitato l’inoltro Splunk e condividano un indice Splunk. I clienti possono utilizzare il campo `aem_env_id` per distinguere tra questi ambienti.

Di seguito è riportato un esempio di richiesta di assistenza clienti:

Programma 123, Production Env

* Indirizzo endpoint HEC della splunk: `splunk-hec-ext.acme.com`
* Indice splunk: acme_123prod (il cliente può scegliere qualsiasi convenzione di denominazione desidera)
* Porta splunk: 443
* Token HEC Splunk: ABC123

Programma 123, Stage Env

* Indirizzo endpoint HEC della splunk: `splunk-hec-ext.acme.com`
* Indice splunk: acme_123stage
* Porta splunk: 443
* Token HEC Splunk: ABC123

Programma 123, Dev Envs

* Indirizzo endpoint HEC della splunk: `splunk-hec-ext.acme.com`
* Indice splunk: acme_123dev
* Porta splunk: 443
* Token HEC Splunk: ABC123

Può essere sufficiente che lo stesso indice Splunk sia utilizzato per ogni ambiente, nel qual caso il campo `aem_env_type` può essere utilizzato per differenziare in base ai valori dev, stage e prod. Se sono presenti più ambienti di sviluppo, è possibile utilizzare anche il campo `aem_env_id` . Alcune organizzazioni possono scegliere un indice separato per i registri dell&#39;ambiente di produzione se l&#39;indice associato limita l&#39;accesso a un set ridotto di utenti Splunk.

Ecco un esempio di voce di registro:

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
