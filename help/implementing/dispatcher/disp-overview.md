---
title: Dispatcher nel cloud
description: 'Dispatcher nel cloud '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 5545f7c271137050d522904bfa94e20f0286e059
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 2%

---

# Dispatcher nel cloud {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="Dispatcher nel cloud"
>abstract="Questa pagina descrive come scaricare ed estrarre gli strumenti del dispatcher, i moduli apache supportati e fornisce una panoramica di alto livello delle modalità legacy e flessibile."

## Introduzione {#apache-and-dispatcher-configuration-and-testing}

Questa pagina descrive gli strumenti del dispatcher e come scaricarli ed estrarli, i moduli apache supportati e fornisce una panoramica di alto livello delle modalità legacy e flessibili. Sono inoltre disponibili ulteriori riferimenti sulla convalida, il debug e la migrazione della configurazione del Dispatcher da AMS a AEM come Cloud Service

## Strumenti Dispatcher {#dispatcher-sdk}

Gli strumenti di Dispatcher fanno parte del AEM generale come SDK per Cloud Service e forniscono:

* Una struttura di file vaniglia contenente i file di configurazione da includere in un progetto Maven per Dispatcher.
* Possibilità per i clienti di verificare che la configurazione di Dispatcher includa solo AEM come direttive supportate dal Cloud Service.        Inoltre, il tooling verifica che la sintassi sia corretta in modo che apache possa avviarsi con successo.
* Immagine Docker che porta il Dispatcher localmente.

## Download ed estrazione degli strumenti {#extracting-the-sdk}

Gli strumenti Dispatcher, parte del [AEM come Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), possono essere scaricati da un file zip dal portale [Distribuzione software](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) . Qualsiasi nuova configurazione disponibile in quella nuova versione di Dispatcher Tools può essere utilizzata per distribuire agli ambienti Cloud che eseguono tale versione di AEM nel Cloud o nella versione successiva.

Decomprimi l’SDK, che crea i bundle degli strumenti Dispatcher per macOS, Linux e Windows.

**Per macOS/Linux**, esegui l’artefatto dello strumento Dispatcher e eseguilo. Estrae automaticamente i file degli strumenti del Dispatcher sotto la directory in cui è stato memorizzato (dove `version` è la versione degli strumenti del Dispatcher).

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Per Windows**, estrarre l’archivio zip Dispatcher Tooling.

## Convalida e debug mediante gli strumenti di Dispatcher {#validation-debug}

Gli strumenti del dispatcher vengono utilizzati per convalidare ed eseguire il debug della configurazione del Dispatcher del progetto. Scopri di più su come utilizzare questi strumenti nelle pagine a cui si fa riferimento di seguito, a seconda che la configurazione del dispatcher del progetto sia strutturata in modalità flessibile o in modalità legacy:

* **Modalità flessibile** : la modalità consigliata e quella predefinita per  [AEM archetipo 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) e versioni successive, che viene utilizzata anche da Cloud Manager per i nuovi ambienti creati dopo il rilascio di Cloud Manager 2021.7.0. I clienti possono attivare questa modalità aggiungendo la cartella e il file `opt-in/USE_SOURCES_DIRECTLY`. Utilizzando questa modalità più flessibile, non ci sono limitazioni nella struttura del file sotto la cartella di riscrittura che in modalità legacy richiedeva un singolo file `rewrite.rules`. Inoltre, non esiste alcuna limitazione al numero di regole che puoi aggiungere. Per informazioni dettagliate sulla struttura delle cartelle e sulla convalida locale, consulta [Convalida e debug mediante gli strumenti di Dispatcher](/help/implementing/dispatcher/validation-debug.md).

* **Modalità legacy** : per informazioni sulla struttura delle cartelle e sulla convalida locale per la configurazione del dispatcher in modalità legacy, consulta  [Convalida e debug tramite gli strumenti di Dispatcher (legacy)](/help/implementing/dispatcher/validation-debug-legacy.md)

Per ulteriori informazioni su come migrare dal modello di configurazione legacy a quello più flessibile, fornito con AEM archetipo 28 in poi, consulta [questa documentazione](/help/implementing/dispatcher/validation-debug.md#migrating).

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

I clienti non possono aggiungere moduli arbitrari, tuttavia è possibile considerare moduli aggiuntivi da includere in futuro. I clienti possono trovare l’elenco delle direttive disponibili per una determinata versione di Dispatcher eseguendo il comando di inserire nell&#39;elenco Consentiti della convalida nell’SDK.

Le direttive consentite nei file di configurazione di Apache possono essere elencate eseguendo il comando di inserire nell&#39;elenco Consentiti della convalida:

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## Struttura delle cartelle {#folder-structure}

La struttura di cartelle apache e dispatcher del progetto varia leggermente in base alla modalità utilizzata dal progetto, come descritto nella sezione [Convalida e debug utilizzando la sezione Strumenti Dispatcher](#validation-debug) precedente.

## Migrazione della configurazione del Dispatcher da AMS {#ams-aem}

Per informazioni dettagliate su come migrare la configurazione del Dispatcher da AMS a AEM come Cloud Service, consulta la [Migrazione della configurazione del Dispatcher da AMS a AEM](/help/implementing/dispatcher/ams-aem.md) come pagina di Cloud Service.
