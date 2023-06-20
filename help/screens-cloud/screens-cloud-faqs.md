---
title: Domande frequenti su Screens as a Cloud Service
description: Questa pagina descrive le domande frequenti as a Cloud Service relative a Screens.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 2%

---

# Domande frequenti su Screens as a Cloud Service {#screens-cloud-faqs}

La sezione seguente fornisce le risposte alle domande frequenti relative al progetto Screens as a Cloud Service.

## Cosa devo fare se AEM Screens Player che punta a Screens as a Cloud Service non sceglie le clientlibs personalizzate con il formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service cambia le chiavi della cache lunga con ogni distribuzione. AEM Screens genera le cache offline quando il contenuto viene modificato, anziché quando Cloud Manager esegue la distribuzione. Queste chiavi di cache lunghe nei manifesti non sono valide, pertanto il lettore non riesce a scaricarle *clientlibs*.

Utilizzo di `longCacheKey="none"` nel tuo `clientlib` La cartella rimuove completamente le chiavi della cache lunghe per questi *clientlibs*.


## Cosa dobbiamo fare se il manifesto offline non include tutte le risorse come previsto? {#offline-manifest}

Le cache offline vengono generate utilizzando **bulk-offline-update-screens-service** utente del servizio. Alcuni percorsi non accessibili da `bulk-offline-update-screens-service`, causano la perdita di contenuto nei manifesti offline.

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

## Quali formati di immagine sono consigliati per la rappresentazione perfetta delle immagini in canali as a Cloud Service di AEM Screens?{#screens-cloud-image-format}

Si consiglia di utilizzare le immagini nel formato `.png` e `.jpeg` in un canale as a Cloud Service di AEM Screens, per una migliore esperienza di digital signage.
Le immagini nel formato `*.tif` (Formato file immagine tag) non sono supportati in AEM Screens as a Cloud Service. Nel caso in cui un canale abbia questo formato di immagine, sul lato lettore non verrà eseguito il rendering dell’immagine.

## Cosa devo fare se un canale in modalità Sviluppatore (online) non esegue il rendering su AEM Screens Player?{#screens-cloud-online-channel-blank-iframe}

Si consiglia di utilizzare le funzionalità di caching di AEM Screens, ma se devi eseguire il canale in modalità Sviluppatore e AEM Screens Player mostra una schermata vuota, controlla gli strumenti di sviluppo del lettore e cerca `X-Frame-Options` o `frame-ancestors` errori. La risoluzione consiste nel configurare il dispatcher in modo da consentire l’esecuzione di contenuto in iFrame. Di solito funziona la seguente configurazione:

```
Header set Content-Security-Policy "frame-ancestors ‘self’ file: localhost:*;"
```

## Qual è l’utilizzo del limite del codice di registrazione?

Come best practice, puoi limitare l’utilizzo del codice di registrazione. Se un codice di registrazione è compromesso, ma ha un limite di 100 registrazioni, l&#39;autore dell&#39;attacco può registrare solo fino a quel numero, ma non di più. Puoi sempre aggiornare il limite di utilizzo dopo aver creato il codice di registrazione e aver già registrato alcuni lettori del cliente. Se il cliente osserva un’attività di registrazione insolita per un codice di registrazione specifico, può abbassare il limite in tempo reale mentre indaga e può aumentare il numero indietro se si è trattato di un falso allarme, senza influire sui giocatori già registrati.
