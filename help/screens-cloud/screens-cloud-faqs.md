---
title: Domande frequenti su Screens as a Cloud Service
description: Questa pagina descrive le Domande frequenti su Screens come un Cloud Service.
source-git-commit: 7a26bb50a8b95a2358912249e21daeb9c5e9c1a3
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Domande frequenti su Screens as a Cloud Service {#screens-cloud-faqs}

La sezione seguente fornisce le risposte alle domande frequenti (FAQ) relative a Screens come progetto di Cloud Service.

## Cosa devo fare se AEM Screens Player che punta a Screens come Cloud Service non sceglie le clientlibs personalizzate con il formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM come Cloud Service cambia le chiavi di cache lunghe con ogni distribuzione. AEM Screens genera le cache offline quando il contenuto viene modificato, anziché quando Cloud Manager esegue la distribuzione. Le chiavi di cache lunghe nei manifesti non sono valide, pertanto il lettore non riesce a scaricare questi *clientlibs*.

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
