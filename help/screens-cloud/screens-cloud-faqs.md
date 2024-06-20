---
title: Domande frequenti su Screens as a Cloud Service
description: Questa pagina descrive le domande frequenti su Screens as a Cloud Service.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 100%

---

# Domande frequenti su Screens as a Cloud Service {#screens-cloud-faqs}

La sezione seguente fornisce le risposte alle domande frequenti relative al progetto Screens as a Cloud Service.

## Cosa devo fare se AEM Screens Player che punta a Screens as a Cloud Service non sceglie le clientlibs personalizzate con il formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service cambia le chiavi della cache lunga a ogni distribuzione. AEM Screens genera le cache offline quando il contenuto viene modificato, anziché quando Cloud Manager esegue la distribuzione. Queste chiavi di cache lunghe nei manifest non sono valide, pertanto il lettore non riesce a scaricare *clientlibs*.

L’utilizzo di `longCacheKey="none"` nella tua cartella `clientlib` rimuove completamente le chiavi di cache lunghe per *clientlibs*.


## Cosa devo fare se il manifest offline non include tutte le risorse come previsto? {#offline-manifest}

Le cache offline vengono generate utilizzando l’utente del servizio **bulk-offline-update-screens-service**. Alcuni percorsi non accessibili da `bulk-offline-update-screens-service`, causano la perdita di contenuto nei manifest offline.

Nel codice, ovvero `ui.config or ui.apps`, crea una configurazione OSGi nella cartella di configurazione, con il seguente contenuto e assegna al file il nome come `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## Quali formati di immagine sono consigliati per la rappresentazione perfetta delle immagini in un canale AEM Screens as a Cloud Service?{#screens-cloud-image-format}

In un canale AEM Screens as a Cloud Service, adobe consiglia di utilizzare le immagini nel formato `.png` e `.jpeg`, per una migliore esperienza di segnaletica digitale.
Le immagini nel formato `*.tif` (file immagine formato tag) non sono supportati in AEM Screens as a Cloud Service. Se un canale ha questo formato di immagine, sul lato lettore l’immagine non viene riprodotta.

## Cosa devo fare se un canale in modalità Sviluppatore (online) non esegue il rendering su AEM Screens Player?{#screens-cloud-online-channel-blank-iframe}

Adobe consiglia di utilizzare le funzionalità di memorizzazione in cache di AEM Screens. Tuttavia, se è necessario eseguire il canale in modalità Sviluppatore e AEM Screens Player mostra una schermata vuota, controlla gli strumenti di sviluppo del lettore ed esegui una ricerca di errori `X-Frame-Options` o `frame-ancestors`. La risoluzione consiste nel configurare Dispatcher in modo da consentire l’esecuzione di contenuto in iFrame. Normalmente, funziona la seguente configurazione:

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## Qual è l’utilizzo del limite del codice di registrazione?

Come best practice, è possibile limitare l’utilizzo del codice di registrazione. Se un codice di registrazione è compromesso, ma ha un limite di 100 registrazioni, un hacker può registrare solo fino a quel numero, ma non di più. Puoi sempre aggiornare il limite di utilizzo dopo aver creato il codice di registrazione e aver già registrato alcuni lettori del cliente. Se il cliente osserva un’attività di registrazione insolita per un codice di registrazione specifico, può abbassare il limite in tempo reale durante l’analisi. Può diminuire il numero se si è trattato di un falso allarme, senza avere un impatto sui lettori già registrati.
