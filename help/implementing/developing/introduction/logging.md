---
title: Registrazione
description: Scoprite come configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
translation-type: tm+mt
source-git-commit: 17ba5068b0df0724bcebeecb2323b7dcdc8d8cfa
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 3%

---


# Registrazione {#logging}

AEM come Cloud Service è una piattaforma che consente ai clienti di includere codice personalizzato per creare esperienze univoche per la propria base di clienti. In questo senso, la registrazione è una funzione fondamentale per eseguire il debug e comprendere l&#39;esecuzione del codice sullo sviluppo locale e gli ambienti cloud, in particolare l&#39;AEM come un ambiente di sviluppo  Cloud Service.

AEM livelli di registrazione e di registro vengono gestiti in file di configurazione memorizzati come parte del progetto AEM in Git e distribuiti come parte del progetto AEM tramite Cloud Manager. L&#39;accesso AEM come Cloud Service può essere suddiviso in due set logici:

* Registrazione AEM, che esegue la registrazione a livello di applicazione AEM
* Registrazione server/dispatcher Web Apache HTTPD, che esegue la registrazione del server Web e del dispatcher nel livello di pubblicazione.

## Registrazione AEM {#aem-loggin}

La registrazione a livello di applicazione AEM è gestita da tre registri:

1. AEM registri Java, che eseguono il rendering delle istruzioni di registrazione Java per l&#39;applicazione AEM.
1. Registri di richieste HTTP, che registrano le informazioni sulle richieste HTTP e le risposte fornite da AEM
1. Registri di accesso HTTP, quali informazioni di riepilogo del registro e richieste HTTP inviate da AEM

>[!NOTE]
>
>Le richieste HTTP servite dalla cache del dispatcher del livello di pubblicazione o dalla rete CDN upstream non vengono riportate in questi registri.

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
Quando la registrazione DEBUG è attiva, vengono registrate le istruzioni che forniscono un'immagine chiara delle attività che si verificano e tutti i parametri chiave che influiscono sull'elaborazione.</td>
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
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>AEM come ID nodo Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>Livello registro</td>
<td>DEBUG</td>
</tr>
<tr>
<td>Thread</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Java, classe</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>Messaggio registro</td>
<td>Nessun approver specificato, impostazione predefinita per [ gruppo di utenti di Creative Approvers ]</td>
</tr>
</tbody>
</table>

### Registratori di configurazione {#configuration-loggers}

AEM registri Java sono definiti come configurazione OSGi, e quindi indirizzati AEM specifici come ambienti Cloud Service di  utilizzando le cartelle in modalità di esecuzione.

Configurare la registrazione Java per i pacchetti Java personalizzati tramite le configurazioni OSGi per la fabbrica Sling LogManager. Esistono due proprietà di configurazione supportate:

| OSGi, proprietà Configuration | Descrizione |
|---|---|
| org.apache.sling.commons.log.names | I pacchetti Java per i quali raccogliere le istruzioni di registro. |
| org.apache.sling.commons.log.level | Il livello di registro a cui registrare i pacchetti Java, specificato da org.apache.sling.commons.log.names |

La modifica di altre proprietà di configurazione LogManager OSGi potrebbe causare problemi di disponibilità in AEM come Cloud Service.

Di seguito sono riportati alcuni esempi delle configurazioni di registrazione consigliate (utilizzando il pacchetto Java segnaposto di `com.example`) per i tre AEM come tipi di ambiente di Cloud Service.

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

**Formato registro**

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
<td>/conf/global/settings/dam/adminui-extension/metadata-profile/</td>
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

Il registro AEM richieste HTTP non è configurabile in AEM come Cloud Service.

## Registrazione AEM accesso HTTP {#aem-http-access-logging}

AEM come registrazione di accesso HTTP Cloud Service, vengono visualizzate le richieste HTTP in ordine temporale. Ogni voce di registro rappresenta la richiesta HTTP che accede a AEM.

Questo registro è utile per comprendere rapidamente a quali richieste HTTP vengono inviate per AEM, se riuscite guardando il codice di stato della risposta HTTP corrispondente e per quanto tempo è necessario completare la richiesta HTTP. Questo registro può essere utile anche per eseguire il debug dell&#39;attività di un utente specifico filtrando le voci di registro per Utenti.

**Esempio di output del registro**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

**Formato registro**

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
<td>30/Apr/2020:17:37:14 +000</td>
</tr>
<tr>
<td>Metodo HTTP</td>
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
<td>1141</td>
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

## Registrazione server Web Apache e dispatcher {#apache-web-server-and-dispatcher-logging}

AEM come Cloud Service fornisce tre registri per i server Web Apache e il livello dispatcher nella pubblicazione:

* Registro di accesso al server Web Apache HTTPD
* Registro errori server Web Apache HTTPD
* Registro dei dispatcher

Questi registri sono disponibili solo per il livello Pubblica.

Questo set di registri fornisce informazioni approfondite sulle richieste HTTP al AEM come livello di pubblicazione Cloud Service prima che tali richieste arrivino all’applicazione AEM. Questo è importante perché, idealmente, la maggior parte delle richieste HTTP ai server dei livelli di pubblicazione è gestita da contenuto memorizzato nella cache dal server Web Apache HTTPD e dal dispatcher AEM e non riesce mai a raggiungere l’applicazione AEM. Pertanto, non esistono istruzioni di registro per queste richieste nei registri AEM Java, Request o Access.

### Registro di accesso al server Web Apache HTTPD {#apache-httpd-web-server-access-log}

Il registro di accesso al server Web Apache HTTP fornisce istruzioni per ogni richiesta HTTP che raggiunge il server Web/dispatcher del livello Publish. Notate che le richieste servite da una CDN upstream non vengono riportate in questi registri.

Consultate le informazioni sul formato del registro errori nella [documentazione ufficiale di apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

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
<td>AEM come ID nodo del servizio cloud</td>
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
<td>01/maggio/2020:00:09:46 +000</td>
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

### Configurazione del registro di accesso al server Web Apache HTTPD {#configuring-the-apache-httpd-webs-server-access-log}

Questo registro non è configurabile in AEM come Cloud Service.

## Registro errori server Web Apache HTTPD {#apache-httpd-web-server-error-log}

Il registro errori del server Web Apache HTTP fornisce istruzioni per ogni errore nel server Web/dispatcher del livello di pubblicazione.

Consultate le informazioni sul formato del registro errori nella [documentazione ufficiale di apache](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

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
<td>Venerdì 17 Luglio 02:16:42.608913 2020</td>
</tr>
<tr>
<td>Livello evento</td>
<td>[mpm_Worker:Notice]</td>
</tr>
<tr>
<td>ID processo</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>Nome contenitore</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>Messaggio</td>
<td>AH00094: Riga di comando: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### Configurazione del registro errori server Web Apache HTTPD {#configuring-the-apache-httpd-web-server-error-log}

I livelli di registro mod_rewrite sono definiti dalla variabile REWRITE_LOG_LEVEL nel file `conf.d/variables/global.var`.

Può essere impostato su Errore, Avverti, Informazioni, Debug e Trace1 - Trace8, con il valore predefinito Avverti. Per eseguire il debug delle regole di riscrittura, è consigliabile aumentare il livello di registro a Trace2.

Per ulteriori informazioni, consultare la [documentazione del modulo mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging).

Per impostare il livello di registro per l&#39;ambiente, utilizzare il ramo condizionale appropriato nel file global.var, come descritto di seguito:

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

**Formato registro**

<table>
<tbody>
<tr>
<td>Data e ora</td>
<td>[17/lug/2020:23:48:16 +000]</td>
</tr>
<tr>
<td>Nome contenitore</td>
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
<td>Codice stato risposta del dispatcher</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Durata</td>
<td>1949 ms</td>
</tr>
<tr>
<td>Agriturismo</td>
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

### Configurazione del registro errori del dispatcher {#configuring-the-dispatcher-error-log}

I livelli del registro del dispatcher sono definiti dalla variabile DISP_LOG_LEVEL nel file `conf.d/variables/global.var`.

Può essere impostato su Errore, Avverti, Informazioni, Debug e Trace1, con il valore predefinito Avverti.

Mentre la registrazione del dispatcher supporta diversi altri livelli di granularità della registrazione, il AEM come Cloud Service consiglia di utilizzare i livelli descritti di seguito.

Per impostare il livello di registro per l&#39;ambiente, utilizzare il ramo condizionale appropriato nel file `global.var`, come descritto di seguito:

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

AEM come Cloud Service, è possibile accedere ai registri dei servizi cloud scaricando l&#39;interfaccia di Cloud Manager o inserendo nella riga di comando i registri utilizzando l&#39;interfaccia  riga di comando Adobe I/O. Per ulteriori informazioni, consulta la [documentazione di registrazione di Cloud Manager](/help/implementing/cloud-manager/manage-logs.md).

### SDK locale {#local-sdk}

AEM come Cloud Service SDK fornisce file di registro per supportare lo sviluppo locale.

AEM file di registro si trovano nella cartella `crx-quickstart/logs`, in cui è possibile visualizzare i seguenti file di registro:

* AEM registro Java: `error.log`
* AEM registro delle richieste HTTP: `request.log`
* AEM registro di accesso HTTP: `access.log`

I registri dei livelli Apache, incluso il dispatcher, si trovano nel contenitore Docker che contiene il dispatcher. Per informazioni sull&#39;avvio del dispatcher, vedere la [documentazione del dispatcher](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html).

Per recuperare i file di registro:

1. Nella riga di comando, digitare `docker ps` per elencare i contenitori
1. Per accedere al contenitore, digitare &quot;`docker exec -it <container> /bin/sh`&quot;, dove `<container>` è l&#39;ID del contenitore del dispatcher dal passaggio precedente
1. Andate alla directory principale della cache in `/mnt/var/www/html`
1. I file di registro si trovano sotto `/etc/httpd/logs`
1.  Inspect i registri: sono accessibili nella cartella XYZ, dove è possibile visualizzare i seguenti file di registro:
   * Registro di accesso al server Web Apache HTTPD - `httpd_access.log`
   * Registri di errore del server Web Apache HTTPD - `httpd_error.log`
   * Registri del dispatcher - `dispatcher.log`

I registri vengono inoltre stampati direttamente sull&#39;uscita terminale. Nella maggior parte dei casi, questi registri devono essere DEBUG, che può essere realizzato trasmettendo il livello Debug come parametro durante l&#39;esecuzione di Docker. Esempio:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Debug di produzione e fase {#debugging-production-and-stage}

In circostanze eccezionali, è necessario modificare i livelli di registro per eseguire il log a una granularità maggiore negli ambienti Stage o Produzione.

Anche se questo è possibile, richiede modifiche ai livelli di registro nei file di configurazione in Git da Avverti ed Errore a Debug, ed esegue una distribuzione da AEM come Cloud Service per registrare le modifiche di configurazione con gli ambienti.

A seconda del traffico e della quantità di istruzioni di registro scritte da Debug, questo può causare un impatto negativo sulle prestazioni sull&#39;ambiente, pertanto si consiglia di modificare i livelli di debug di Stage e Produzione:

* Fatto con prudenza, e solo quando assolutamente necessario
* Ripristinati i livelli appropriati e ridistribuiti il prima possibile

## Registri splunk {#splunk-logs}

I clienti che dispongono di account Splunk possono richiedere tramite ticket di assistenza clienti che i loro registri di Cloud Service AEM vengano inoltrati all&#39;indice appropriato. I dati di registrazione sono equivalenti a quelli disponibili tramite i download del registro di Cloud Manager, ma i clienti potrebbero trovare utile sfruttare le funzionalità di query disponibili nel prodotto Splunk.

La larghezza di banda di rete associata ai registri inviati a Splunk è considerata parte dell&#39;utilizzo di I/O di rete del cliente.

### Abilitazione dell&#39;inoltro frastagliato {#enabling-splunk-forwarding}

Nella richiesta di assistenza, i clienti devono indicare:

* Indirizzo endpoint HEC splunk
* Indice Splunk
* La porta Splunk
* Il token Splunk HEC. Per ulteriori informazioni, vedere [questa pagina](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples).

Le proprietà di cui sopra devono essere specificate per ciascuna combinazione di programma/tipo di ambiente pertinente.  Ad esempio, se un cliente voleva un ambiente di sviluppo, staging e produzione, dovrebbe fornire tre serie di informazioni, come indicato di seguito.

>[!NOTE]
>
>L&#39;inoltro splunk per gli ambienti di programmi sandbox non è supportato.

Accertatevi che la richiesta iniziale includa tutti gli ambienti di sviluppo che devono essere attivati, oltre agli ambienti stage/prod.

Se i nuovi ambienti di sviluppo creati dopo la richiesta iniziale sono destinati all&#39;inoltro Splunk, ma non lo hanno attivato, è necessario effettuare una richiesta aggiuntiva.

Inoltre, se gli ambienti di sviluppo sono stati richiesti, è possibile che altri ambienti di sviluppo non inclusi nella richiesta o persino negli ambienti sandbox avranno l&#39;opzione di inoltro Splunk abilitata e condivideranno un indice Splunk. I clienti possono utilizzare il campo `aem_env_id` per distinguere tra questi ambienti.

Di seguito è riportato un esempio di richiesta di assistenza clienti:

Programma 123, Production Env

* Indirizzo endpoint HEC splunk: `splunk-hec-ext.acme.com`
* Indice splunk: acme_123prod (il cliente può scegliere qualsiasi convenzione di denominazione)
* Porta splunk: 443
* Token Splunk HEC: ABC123

Program 123, Stage Env

* Indirizzo endpoint HEC splunk: `splunk-hec-ext.acme.com`
* Indice splunk: acme_123stage
* Porta splunk: 443
* Token Splunk HEC: ABC123

Programma 123, Dev Envs

* Indirizzo endpoint HEC splunk: `splunk-hec-ext.acme.com`
* Indice splunk: acme_123dev
* Porta splunk: 443
* Token Splunk HEC: ABC123

Può essere sufficiente che lo stesso indice Splunk venga utilizzato per ogni ambiente, nel qual caso il campo `aem_env_type` può essere utilizzato per distinguere in base ai valori dev, stage e prod. In presenza di più ambienti di sviluppo, è possibile utilizzare anche il campo `aem_env_id`. Alcune organizzazioni possono scegliere un indice separato per i registri dell&#39;ambiente di produzione se l&#39;indice associato limita l&#39;accesso a un set ridotto di utenti Splunk.

Esempio di voce di registro:

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
