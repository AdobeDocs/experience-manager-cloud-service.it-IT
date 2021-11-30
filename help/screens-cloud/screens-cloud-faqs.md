---
title: Domande frequenti su Screens as a Cloud Service
description: Questa pagina descrive le domande frequenti as a Cloud Service di Screens.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 489cc9963910ba9f94d30906127beb75f9ad37df
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Domande frequenti su Screens as a Cloud Service {#screens-cloud-faqs}

La sezione seguente fornisce le risposte alle domande frequenti relative al progetto as a Cloud Service Screens.

## Cosa devo fare se AEM Screens Player che punta a Screens as a Cloud Service non sceglie le clientlib personalizzate con il formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service cambia le chiavi di cache lunghe con ogni distribuzione. AEM Screens genera le cache offline quando il contenuto viene modificato, anziché quando Cloud Manager esegue la distribuzione. Le chiavi di cache lunghe nei manifesti non sono valide, pertanto il lettore non riesce a scaricare questi *clientlibs*.

Utilizzo `longCacheKey="none"` nel tuo `clientlib` La cartella rimuove completamente le chiavi di cache lunghe per queste *clientlibs*.


## Cosa fare se il manifesto offline non include tutte le risorse come previsto? {#offline-manifest}

Le cache offline vengono generate utilizzando **bulk-offline-update-screens-service** utente del servizio. Alcuni percorsi, non accessibili da `bulk-offline-update-screens-service`, porta a contenuti mancanti nei manifesti offline.

Nel tuo codice, cioè: `ui.config or ui.apps`, crea una configurazione OSGi nella cartella di configurazione con il seguente contenuto e assegna il titolo al nome del file come `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## Quali formati immagine sono consigliati per una riproduzione perfetta delle immagini nei canali as a Cloud Service di AEM Screens?{#screens-cloud-image-format}

Si consiglia di utilizzare le immagini nel formato `.png` e `.jpeg` in un canale as a Cloud Service AEM Screens, per una migliore esperienza di digital signage.
Le immagini nel formato `*.tif` (Formato del file immagine del tag) non supportato in AEM Screens as a Cloud Service. Nel caso in cui un canale abbia questo formato di immagine, sul lato del lettore l&#39;immagine non verrà riprodotta.

## Cosa devo fare se un canale in modalità Sviluppatore (online) non esegue il rendering su AEM Screens Player?{#screens-cloud-online-channel-blank-iframe}

Si consiglia di sfruttare le funzionalità di memorizzazione in cache di AEM Screens, ma se è necessario eseguire il canale in modalità Sviluppatore e AEM Screens Player mostra uno schermo vuoto, controlla gli strumenti per sviluppatori del lettore e cerca `X-Frame-Options` o `frame-ancestors` errori. La risoluzione consiste nel configurare il dispatcher per consentire l’esecuzione di contenuti in iFrames. Di solito funziona la seguente configurazione:

```
Header set Content-Security-Policy "frame-ancestors ‘self’ file: localhost:*;"
```

## Qual è l&#39;utilizzo del limite del codice di registrazione?

Come best practice, puoi limitare l’utilizzo del codice di registrazione. Se un codice di registrazione è compromesso, ma ha un limite di 100 registrazioni, l&#39;autore dell&#39;attacco può registrare solo fino a quel numero, ma non di più. È sempre possibile aggiornare il limite di utilizzo dopo la creazione del codice di registrazione e dopo la registrazione di alcuni giocatori del cliente. Se il cliente osserva un&#39;attività di registrazione insolita per un codice di registrazione specifico, può abbassare il limite in tempo reale mentre indaga e può aumentare il numero se si tratta di un falso allarme, senza influire sui giocatori già registrati.