---
title: Reindirizzamenti URL senza pipeline
description: Scopri come dichiarare i reindirizzamenti 301 o 302 senza accesso alle pipeline Git o Cloud Manager.
feature: Dispatcher
role: Admin
exl-id: dacb1eda-79e0-4e76-926a-92b33bc784de
source-git-commit: c80454204837529007c1fda7eef4486c213eb509
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Reindirizzamenti URL senza pipeline {#pipeline-free-redirects}

Per vari motivi, le organizzazioni riscrivono gli URL in un modo che causa un reindirizzamento 301 (o 302), il che significa che il browser viene reindirizzato a una pagina diversa.

Gli scenari includono:

* Una pagina HTML rimossa, quindi l&#39;utente viene portato a una pagina sostitutiva (a volte la home page) invece di visualizzare un errore `404 Page Not Found`.
* Una pagina HTML rinominata.
* Ottimizzazione SEO.

AEM as a Cloud Service offre [diversi approcci](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection) per implementare i reindirizzamenti lato client, ma la strategia descritta in questo articolo, reindirizzamenti senza pipeline, è una buona scelta quando:

* Le persone che gestiscono i reindirizzamenti sono utenti aziendali che non dispongono dell’accesso necessario per confermare le modifiche ai file nel controllo del codice sorgente o della possibilità di eseguire una pipeline di configurazione a livello web di Cloud Manager.
* Il numero di reindirizzamenti varia da poche a decine di migliaia.
* Si desidera scegliere l&#39;opzione di un&#39;interfaccia utente, che può essere creata come progetto personalizzato o utilizzando [ACS Commons Rewrite Map Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html).

Questa funzione si basa sulla capacità di Apache/Dispatcher dell’AEM di caricare (o ricaricare) uno o più file di mappa di riscrittura posizionati in una posizione specifica nell’archivio di pubblicazione. È importante ricordare che il modo in cui i file vengono ricevuti è al di fuori dell’ambito di questa funzione, ma puoi prendere in considerazione uno dei seguenti metodi:

* Acquisizione della mappa di riscrittura come risorsa nell’interfaccia utente di authoring e pubblicazione.
* Installazione di [ACS Commons Rewrite Map Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html), che include un&#39;interfaccia utente per la gestione dei mapping URL e può inoltre pubblicare il file di mapping di riscrittura.
* Massima flessibilità scrivendo un&#39;applicazione personalizzata. Ad esempio, un’interfaccia utente o un’interfaccia a riga di comando per gestire le mappature URL oppure un modulo per caricare una mappa di riscrittura, che utilizza quindi le API AEM per pubblicare il file della mappa di riscrittura.

>[!NOTE]
> Questa funzionalità richiede AEM versione **18311 o successiva**.

## Mappa di riscrittura {#rewrite-map}

Per impostazione predefinita, la mappa di riscrittura viene ricaricata (se modificata) dal server HTTP Apache ogni 300 secondi (il valore è configurabile). Il formato del file deve seguire il formato del file RewriteMap con mappa chiave-valore di testo normale descritto nella [documentazione di Apache](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html#txt).

È necessario creare un file denominato `managed-rewrite-maps.yaml` per specificare la posizione del file di mappa di riscrittura e distribuirlo una sola volta, utilizzando la pipeline full stack di Cloud Manager o la pipeline a livello web. Il file deve essere creato nella cartella [src/opt-in](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud/src/opt-in) della configurazione di Dispatcher. Utilizzare la [struttura di file in modalità flessibile](/help/implementing/dispatcher/validation-debug.md#flexible-mode-file-structure).

Puoi configurarlo con il seguente pattern:

```
maps:
- name: my.map
  path: <path-in-publish-repository>/redirectmap.txt
```

Se, ad esempio, il metodo scelto per inserire il file di mappa di riscrittura è quello di acquisirlo in AEM come risorsa denominata `mysite-redirectmap.txt` e quindi pubblicarlo, è possibile specificare una cartella in `/content/dam`:

```
maps:
- name: my.map
  path: /content/dam/redirectmaps/mysite-redirectmap.txt
```

Successivamente, in un file di configurazione di Apache come `rewrites/rewrite.rules` o `<yourfile>.vhost`, è necessario configurare il file di mappa a cui fa riferimento la proprietà name (`my.map` nell&#39;esempio precedente). Una volta caricato, il file di mappa viene salvato nell&#39;archivio locale del dispatcher nel percorso **fixed** `/tmp/rewrites/`.

La direttiva `RewriteMap` deve indicare che i dati sono memorizzati in un formato di file di gestione del database (DBM) utilizzando il formato `sdbm` (DBM semplice) e che il percorso completo del file è derivato dal prefisso del percorso di archiviazione e dalla proprietà name.

Il resto della configurazione dipende dal formato di `redirectmap.txt`. Il formato più semplice, illustrato nell’esempio seguente, è una mappatura uno a uno tra l’URL originale e l’URL mappato:

```
# RewriteMap from managed rewrite maps
RewriteMap map.foo dbm=sdbm:/tmp/rewrites/my.map
RewriteCond ${map.foo:$1} !=""
RewriteRule ^(.*)$ ${map.foo:$1|/} [L,R=301]
```


## Considerazioni {#considerations}

Considera quanto segue:

* Per impostazione predefinita, quando si carica una mappa di riscrittura, Apache si avvia senza attendere il caricamento dei file di mappa completi, e quindi possono esserci incoerenze temporanee fino al caricamento della mappa completa. Questa impostazione può essere modificata in modo che Apache attenda il caricamento dell’intero contenuto della mappa, ma l’avvio di Apache richiede più tempo. Per modificare questo comportamento in modo che Apache attenda, aggiungi `wait:true` al file `managed-rewrite-maps.yaml`.
* Per modificare la frequenza tra i caricamenti, aggiungere `ttl: <integer>` al file `managed-rewrite-maps.yaml`. Ad esempio: `ttl: 120`.
* Apache ha un limite di lunghezza di 1024 per le voci singole RewriteMap.
