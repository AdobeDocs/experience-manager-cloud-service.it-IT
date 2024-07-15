---
title: Come possiamo risolvere i problemi relativi alla memorizzazione nella cache per AEM Forms as a Cloud Service?
description: Risolvere i problemi relativi alla memorizzazione nella cache per AEM Forms as a Cloud Service.
contentOwner: khsingh
feature: Adaptive Forms
role: User
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 0b693cb51a96011235fa87a5899426c6b0c2509a
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 1%

---

# Prestazioni di memorizzazione in cache {#caching-performance}

Durante la configurazione o l’utilizzo della cache di Forms adattivo in un ambiente di Cloud Service si possono verificare alcuni dei seguenti problemi:

## Alcuni Forms adattivi contenenti immagini o video non vengono invalidati automaticamente dalla cache di Dispatcher {#images-videos-not-invalidated}

Puoi selezionare e aggiungere immagini o video dal browser di risorse a un modulo adattivo. Quando queste immagini vengono modificate nell’editor di Assets, la versione cache di un modulo adattivo contenente tali immagini non viene invalidata. Il modulo adattivo continua a mostrare immagini precedenti.

Per risolvere il problema, dopo la pubblicazione delle immagini e del video, annulla esplicitamente la pubblicazione e pubblica il Forms adattivo che fa riferimento a tali risorse.

## Alcuni Forms adattivi contenenti frammenti di contenuto o frammenti di esperienza non vengono invalidati automaticamente dalla cache di Dispatcher {#content-fragments-experience-fragments-not-invalidated}

Puoi aggiungere un frammento di contenuto o un frammento di esperienza a un modulo adattivo. Quando questi frammenti vengono modificati e pubblicati in modo indipendente, la versione cache di un modulo adattivo contenente tali frammenti non viene invalidata. Il modulo adattivo continua a mostrare frammenti meno recenti.

Per risolvere il problema, dopo aver pubblicato un frammento di contenuto o un frammento di esperienza aggiornato, annulla esplicitamente la pubblicazione e pubblica il Forms adattivo che utilizza queste risorse.

## Solo la prima istanza di Adaptive Forms è memorizzata nella cache {#only-first-instance-cached}

Se l’URL del modulo adattivo non contiene informazioni sulla localizzazione e l’opzione Usa impostazioni locali del browser nella gestione della configurazione è abilitata, viene distribuita una versione localizzata del modulo adattivo e un’istanza del modulo adattivo, basata sulla prima richiesta (impostazioni locali del browser richieste), viene memorizzata in cache e distribuita a ogni utente successivo.

Per risolvere il problema, effettua le seguenti operazioni:

1. Apri il progetto di Experience Manager.
1. Apri `dispatcher/scr/conf.d/rewrites/rewrite.rules` per la modifica.
1. Aprire `conf.d/httpd-dispatcher.conf` o qualsiasi altro file di configurazione configurato per il caricamento in fase di esecuzione.
1. Aggiungi il seguente codice al file e salvalo. Si tratta di un codice di esempio per modificarlo in base all’ambiente in uso.

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two characters which most likely are the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## Il caching CDN smette di funzionare dopo 300 secondi {#cdn-caching-stops-working-after-300-seconds}

La memorizzazione nella cache CDN smette di funzionare dopo 300 secondi e tutte le richieste da memorizzare nella cache su CDN vengono reindirizzate a Dispatcher.

Per risolvere il problema, imposta l’intestazione della pagina su 0:

1. Crea un file in `src\conf.d\available_vhosts`

1. Aggiungi quanto segue al file per impostare l’intestazione age

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. Salva e chiudi il file.
1. Modificare il soft link per `src\conf.d\enabled_vhosts\default.vhost` in modo che punti al nuovo file.
