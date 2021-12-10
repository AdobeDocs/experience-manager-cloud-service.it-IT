---
title: 'Risoluzione dei problemi relativi alle prestazioni della cache  '
seo-title: Troubleshooting caching performance
description: 'Risoluzione dei problemi relativi alle prestazioni della cache  '
seo-description: Troubleshooting caching performance
contentOwner: khsingh
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 1%

---

# Prestazioni di memorizzazione in cache {#caching-performance}

È possibile riscontrare alcuni dei seguenti problemi durante la configurazione o l’utilizzo della cache Forms adattiva in un ambiente di Cloud Service:

## Alcuni Forms adattivi contenenti immagini o video non vengono invalidati automaticamente dalla cache del Dispatcher {#images-videos-not-invalidated}

Puoi selezionare e aggiungere immagini o video dal browser delle risorse a un modulo adattivo. Quando queste immagini vengono modificate nell’editor di Assets, la versione cache di un modulo adattivo contenente tali immagini non viene annullata. Nel modulo adattivo vengono visualizzate le immagini precedenti.

Per risolvere il problema, dopo aver pubblicato le immagini e i video, annulla esplicitamente la pubblicazione e pubblica l’Adaptive Forms che fa riferimento a queste risorse.

## Alcuni Forms adattivi contenenti frammenti di contenuto o frammenti esperienza non vengono invalidati automaticamente dalla cache del Dispatcher {#content-fragments-experience-fragments-not-invalidated}

È possibile aggiungere un frammento di contenuto o un frammento esperienza a un modulo adattivo. Quando questi frammenti vengono modificati e pubblicati in modo indipendente, la versione cache di un Modulo adattivo contenente tali frammenti non viene invalidata. Il modulo adattivo continua a mostrare frammenti precedenti.

Per risolvere il problema, dopo aver pubblicato frammento di contenuto aggiornato o Frammento esperienza, annulla esplicitamente la pubblicazione e pubblica l’Adaptive Forms che utilizza queste risorse.

## Solo la prima istanza di Adaptive Forms è memorizzata nella cache {#only-first-instance-cached}

Se l’URL del modulo adattivo non contiene informazioni sulla localizzazione e l’opzione Usa impostazione internazionale browser in configuration manager è abilitata, viene fornita una versione localizzata del modulo adattivo e viene fornita a ogni utente successivo un’istanza del modulo adattivo, in base alla prima richiesta (richiesta locale del browser).

Esegui i seguenti passaggi per risolvere il problema:

1. Apri il progetto di Experience Manager.
1. Apri `dispatcher/scr/conf.d/rewrites/rewrite.rules` per la modifica.
1. Apri `conf.d/httpd-dispatcher.conf` o qualsiasi altro file di configurazione configurato per il caricamento in fase di runtime.
1. Aggiungi il seguente codice al file e salvalo. Si tratta di un codice di esempio modificarlo in base all’ambiente.

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two character which most likely will be the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## La memorizzazione in cache CDN smette di funzionare dopo 300 secondi {#cdn-caching-stops-working-after-300-seconds}

La memorizzazione in cache CDN smette di funzionare dopo 300 secondi e tutte le richieste da memorizzare in cache su CDN vengono reindirizzate a Dispatcher.

Per risolvere il problema, imposta l’intestazione di pagina su 0:

1. Crea un file in `src\conf.d\available_vhosts`

1. Aggiungi quanto segue al file per impostare l’intestazione della pagina

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. Salva e chiudi il file 
1. Modifica il collegamento software per `src\conf.d\enabled_vhosts\default.vhost` per puntare a nuovo file.
