---
title: Pipeline-free URL Redirects
description: Learn how to declare 301 or 302 redirects without access to Git or Cloud Manager pipelines.
feature: Dispatcher
role: Admin
source-git-commit: 567c75f456f609dbc254753b439151d0f4100bc0
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Pipeline-free URL Redirects {#pipeline-free-redirects}

>[!NOTE]
>This feature is not yet released.

For various reasons, organizations rewrite URLs in a way that causes a 301 (or 302) redirect, meaning that the browser is redirected to a different page.

Scenarios include:

* `404 Page Not Found`
* Una pagina HTML rinominata.
* Ottimizzazione SEO.

AEM as a Cloud Service offre [diversi approcci](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection) per implementare i reindirizzamenti lato client, ma la strategia descritta in questo articolo, reindirizzamenti senza pipeline, è una buona scelta quando:

* Le persone che gestiscono i reindirizzamenti sono utenti aziendali che non dispongono dell’accesso necessario per confermare le modifiche ai file nel controllo del codice sorgente o della possibilità di eseguire una pipeline di configurazione a livello web di Cloud Manager.
* The number of redirects ranges from a few to tens of thousands.
* [](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html)

The core of this feature is the ability for AEM Apache/Dispatcher to load (or reload) one or more rewrite map files that have been placed in a specified location in the publish repository. It is important to mention that how the files get there is outside the scope of this feature but you can consider one of the following methods:

* Ingesting the rewrite map as an asset in the author user interface and publishing it.
* [](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html)
* Full flexibility by writing a custom application. For example, either a user interface or command line interface to manage the url mappings or alternatively a form to upload a rewrite map, which then uses AEM APIs to publish the rewrite map file.

>[!NOTE]
> Questa funzionalità richiede AEM versione **18311 o successiva**.

## Mappa di riscrittura {#rewrite-map}

Per impostazione predefinita, la mappa di riscrittura viene ricaricata (se modificata) dal server HTTP Apache ogni 300 secondi (il valore è configurabile). Il formato del file deve seguire il formato del file RewriteMap con mappa chiave-valore di testo normale descritto nella [documentazione di Apache](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html#txt).

`managed-rewrite-maps.yaml` [](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud/src/opt-in) [](/help/implementing/dispatcher/validation-debug.md#flexible-mode-file-structure)

You can configure it with the following pattern:

```
maps:
- name: my.map
  path: <path-in-publish-repository>/redirectmap.txt
```

`mysite-redirectmap.txt``/content/dam`

```
maps:
- name: my.map
  path: /content/dam/redirectmaps/mysite-redirectmap.txt
```

`rewrites/rewrite.rules``<yourfile>.vhost``my.map`

`RewriteMap``sdbm`

`redirectmap.txt` Il formato più semplice, illustrato nell’esempio seguente, è una mappatura uno a uno tra l’URL originale e l’URL mappato:

```
# RewriteMap from managed rewrite maps
RewriteMap map.foo dbm=sdbm:/tmp/rewrites/my.map
RewriteCond ${map.foo:$1} !=""
RewriteRule ^(.*)$ ${map.foo:$1|/} [L,R=301]
```


## Considerazioni {#considerations}

Considera quanto segue:

* Per impostazione predefinita, quando si carica una mappa di riscrittura, Apache si avvia senza attendere il caricamento dell’intero file o dei file di mappa e, pertanto, possono verificarsi incoerenze temporanee fino al caricamento dell’intera o delle mappe. Questa impostazione può essere modificata in modo che Apache attenda il caricamento dell’intero contenuto della mappa, ma l’avvio di Apache richiederà più tempo. Per modificare questo comportamento in modo che Apache attenda, aggiungi `wait:true` al file `managed-rewrite-maps.yaml`.
* `ttl: <integer>``managed-rewrite-maps.yaml` Esempio `ttl: 120`.
* Apache has an 1024 length limit for RewriteMap single entries.
