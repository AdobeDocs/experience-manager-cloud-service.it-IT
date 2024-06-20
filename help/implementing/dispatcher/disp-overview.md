---
title: Dispatcher nel cloud
description: Scopri gli strumenti di Dispatcher, i moduli Apache supportati e le modalità legacy e flessibile.
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 98%

---

# Dispatcher nel cloud {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="Dispatcher nel cloud"
>abstract="Questa pagina descrive come scaricare ed estrarre gli strumenti di Dispatcher, i moduli Apache supportati e fornisce una panoramica di alto livello delle modalità legacy e flessibili."

## Introduzione {#apache-and-dispatcher-configuration-and-testing}

Questa pagina descrive gli strumenti di Dispatcher e come scaricarli ed estrarli, i moduli Apache supportati e fornisce una panoramica di alto livello delle modalità legacy e flessibili. Sono inoltre disponibili ulteriori riferimenti sulla convalida, il debug e la migrazione della configurazione di Dispatcher da AMS a AEM as a Cloud Service. <!-- ERROR: NOT FOUND (HTTP ERROR 404) Also, see [this video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-dispatcher-cloud.html) for additional details about deploying dispatcher files in a cloud service environment. -->

## Strumenti di Dispatcher {#dispatcher-sdk}

Gli strumenti di Dispatcher fanno parte dell’SDK globale di AEM as a Cloud Service e forniscono:

* Una struttura di file vaniglia contenente i file di configurazione da includere in un progetto Maven per Dispatcher.
* Strumenti che consentono ai clienti di verificare che la configurazione di Dispatcher includa solo direttive supportate di AEM as a Cloud Service. Inoltre, lo strumento verifica che la sintassi sia corretta in modo che Apache possa avviarsi correttamente.
* Immagine Docker che porta il Dispatcher localmente.

## Download ed estrazione degli strumenti {#extracting-the-sdk}

Strumenti di Dispatcher, parte del [SDK di AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), può essere scaricato da un file zip al portale di [Distribuzione di software](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html). Qualsiasi nuova configurazione disponibile in quella nuova versione di strumenti di Dispatcher può essere utilizzata per distribuire agli ambienti Cloud che eseguono tale versione di AEM nel Cloud o nella versione successiva.

Decomprimi l’SDK, che contiene i bundle gli strumenti Dispatcher per macOS, Linux® e Windows.

**Per macOS/Linux**, rendi eseguibile l’artefatto dello strumento di Dispatcher ed eseguilo. Estrae automaticamente i file degli strumenti di Dispatcher sotto la directory in cui è stato memorizzato (dove `version` è la versione degli strumenti di Dispatcher).

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Per Windows**, estrae l’archivio zip dello strumento di Dispatcher.

## Convalida e debug mediante gli strumenti di Dispatcher {#validation-debug}

Gli strumenti di Dispatcher vengono utilizzati per convalidare ed eseguire il debug della configurazione di Dispatcher del progetto. Scopri di più su come utilizzare questi strumenti nelle pagine a cui si fa riferimento di seguito, a seconda che la configurazione del Dispatcher del progetto sia strutturata in modalità flessibile o in modalità legacy:

* **Modalità flessibile**: la modalità consigliata e l’impostazione predefinita per [AEM archetipo 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) e versioni successive, che viene utilizzata anche da Cloud Manager per i nuovi ambienti creati dopo la versione 2021.7.0 di Cloud Manager. I clienti possono attivare questa modalità aggiungendo la cartella e il file `opt-in/USE_SOURCES_DIRECTLY`. Utilizzando questa modalità più flessibile, non ci sono limitazioni nella struttura del file sotto la cartella di riscrittura che in modalità legacy richiedeva un singolo file `rewrite.rules`. Inoltre, non esiste alcuna limitazione al numero di regole che puoi aggiungere. Per informazioni dettagliate sulla struttura delle cartelle e sulla convalida locale, consulta [Convalida e debug tramite gli strumenti di Dispatcher](/help/implementing/dispatcher/validation-debug.md).

* **Modalità legacy**: per informazioni sulla struttura delle cartelle e sulla convalida locale per la modalità legacy di configurazione del Dispatcher, consulta [Convalida e debug tramite gli strumenti di Dispatcher (legacy)](/help/implementing/dispatcher/validation-debug-legacy.md).

Per ulteriori informazioni su come eseguire la migrazione dal modello di configurazione legacy a quello più flessibile, fornito dall&#39;archetipo 28 di AEM in poi, vedi [questa documentazione](/help/implementing/dispatcher/validation-debug.md#migrating).

## Disposizione dei contenuti {#content-disposition}

Per il livello di pubblicazione, l’impostazione predefinita per il servizio dei blob è come allegato. Ingnora questa impostazione utilizzando l’[intestazione di disposizione dei contenuti](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition) standard nel Dispatcher.

Di seguito è riportato un esempio di come dovrebbe essere la configurazione:

```
<LocationMatch "^\/content\/dam.*\.(pdf).*">
 Header unset Content-Disposition
 Header set Content-Disposition inline
</LocationMatch>
```

## Moduli Apache supportati {#supported-directives}

La tabella seguente mostra i moduli Apache supportati:

| Nome modulo | Pagina di riferimento |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
| `mod_authn_core` | [https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html) |
| `mod_authn_file` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_file.html) |
| `mod_authz_core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html) |
| `mod_authz_groupfile` | [https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html) |
| `mod_deflate` | [https://httpd.apache.org/docs/2.4/mod/mod_deflate.html](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html) |
| `mod_dir` | [https://httpd.apache.org/docs/2.4/mod/mod_dir.html](https://httpd.apache.org/docs/2.4/mod/mod_dir.html) |
| `mod_env` | [https://httpd.apache.org/docs/2.4/mod/mod_env.html](https://httpd.apache.org/docs/2.4/mod/mod_env.html) |
| `mod_filter` | [https://httpd.apache.org/docs/2.4/mod/mod_filter.html](https://httpd.apache.org/docs/2.4/mod/mod_filter.html) |
| `mod_headers` | [https://httpd.apache.org/docs/2.4/mod/mod_headers.html](https://httpd.apache.org/docs/2.4/mod/mod_headers.html) |
| `mod_mime` | [https://httpd.apache.org/docs/2.4/mod/mod_mime.html](https://httpd.apache.org/docs/2.4/mod/mod_mime.html) |
| `mod_proxy` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html) |
| `mod_proxy_http` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_ssl (only the SSLProxyEngine directive)` | [https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |
| `mod_macro` | [https://httpd.apache.org/docs/2.4/mod/mod_macro.html](https://httpd.apache.org/docs/2.4/mod/mod_macro.html) |
| `mod_include (no directives supported)` | [https://httpd.apache.org/docs/2.4/mod/mod_include.html](https://httpd.apache.org/docs/2.4/mod/mod_include.html) |


I clienti non possono aggiungere moduli arbitrari, tuttavia è possibile considerare moduli aggiuntivi da includere in futuro. I clienti possono trovare l’elenco delle direttive disponibili per una determinata versione di Dispatcher eseguendo il comando di inserire nell&#39;elenco Consentiti della convalida nell’SDK.

Le direttive consentite nei file di configurazione Apache possono essere elencate eseguendo il comando di inserire nell&#39;elenco Consentiti della convalida:

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## Struttura delle cartelle {#folder-structure}

La struttura delle cartelle Apache e Dispatcher del progetto varia leggermente in base alla modalità utilizzata, come descritto nella sezione precedente [Convalida e debug mediante gli strumenti di Dispatcher](#validation-debug).

## Migrazione della configurazione di Dispatcher da AMS {#ams-aem}

Per informazioni dettagliate su come migrare la configurazione di Dispatcher da AMS a AEM as a Cloud Service, consulta la pagina [Migrazione della configurazione di Dispatcher da AMS a AEM](/help/implementing/dispatcher/ams-aem.md) as a Cloud Service.
