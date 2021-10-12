---
title: Domande frequenti su Screens as a Cloud Service
description: Questa pagina descrive le domande frequenti as a Cloud Service di Screens.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: cf091056bdb96917a6d22bf1197d9b34ebbf9610
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Domande frequenti su Screens as a Cloud Service {#screens-cloud-faqs}

La sezione seguente fornisce le risposte alle domande frequenti relative al progetto as a Cloud Service Screens.

## Cosa devo fare se il lettore AEM Screens che punta a Screens as a Cloud Service non sceglie le clientlib personalizzate con il formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service cambia le chiavi di cache lunghe con ogni distribuzione. AEM Screens genera le cache offline quando il contenuto viene modificato, anziché quando Cloud Manager esegue la distribuzione. Le chiavi di cache lunghe nei manifesti non sono valide, pertanto il lettore non riesce a scaricare questi *clientlibs*.

L&#39;utilizzo di `longCacheKey="none"` nella cartella `clientlib` rimuove completamente le chiavi di cache lunghe per queste *clientlibs*.


## Cosa fare se il manifesto offline non include tutte le risorse come previsto? {#offline-manifest}

Le cache offline vengono generate utilizzando l&#39;utente di servizio **bulk-offline-update-screens-service** . Alcuni percorsi, non accessibili da `bulk-offline-update-screens-service`, generano contenuti mancanti nei manifesti offline.

Nel codice, ovvero `ui.config or ui.apps`, crea una configurazione OSGi nella cartella di configurazione con il seguente contenuto e assegna il titolo al nome del file come `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

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

Si consiglia di utilizzare le immagini in formato `.png` e `.jpeg` in un canale as a Cloud Service di AEM Screens, per una migliore esperienza di segnaletica digitale.
Le immagini nel formato `*.tif` (formato File immagine tag) non sono supportate in AEM Screens as a Cloud Service. Nel caso in cui un canale abbia questo formato di immagine, sul lato del lettore l&#39;immagine non verrà riprodotta.