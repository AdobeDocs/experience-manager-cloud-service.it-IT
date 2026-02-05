---
title: Gestione della cache in Dynamic Media con API aperte
description: Gestione della cache in Dynamic Media con API aperte
role: User
source-git-commit: 89f21f96a741acbd6458c3777227548fbc89e525
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# Gestione della cache in Dynamic Media con API aperte {#cache-management-dynamic-media-open-apis}

Una gestione efficace della cache è essenziale per fornire risorse digitali scalabili, aggiornate e a elevate prestazioni. In Dynamic Media con API aperte, la gestione della cache definisce come il contenuto viene memorizzato, aggiornato e distribuito tra i vari livelli della pipeline di consegna. Le risposte per la distribuzione delle risorse sono memorizzate nella cache a più livelli per garantire prestazioni ottimali e una rapida distribuzione dei contenuti.

Il caching prolungato in Dynamic Media con API aperte è costituito da [CDN Layer Caching](#cdn-layer-caching) e [External Cache Control (BYOCDN e Browser Caching)](#byocdn-browser-caching).

## CDN Layer Caching {#cdn-layer-caching}

Le risposte di consegna delle risorse vengono memorizzate nella cache in [Adobe Managed CDN](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn#aem-managed-cdn) per un periodo di tempo prolungato al fine di massimizzare le prestazioni e ridurre al minimo il carico sull&#39;origine. Questa memorizzazione in cache è completamente gestita da Adobe per garantire un’esperienza di elevata qualità coerente per gli utenti finali. La durata della cache è intenzionalmente ottimizzata per le prestazioni e non può essere personalizzata dagli utenti per mantenere l’affidabilità e la distribuzione efficiente dei contenuti tra tutti i clienti.

Tutti gli URL di consegna vengono memorizzati nella cache di Edge (Fastly) per un periodo di tempo prolungato, al fine di garantire prestazioni ottimali. Gli oggetti di consegna memorizzati nella cache includono rappresentazioni statiche, video, file binari di immagini originali e immagini trasformate in modo dinamico, come risorse ridimensionate o riformattate, generate tramite parametri URL. <!--The CDN is designed to serve these assets directly from the cache without revalidating them, unless an explicit purge is performed.-->

## Controllo della cache esterna (BYOCDN e caching del browser) {#byocdn-browser-caching}

Le risposte di consegna delle risorse includono un&#39;intestazione `Cache-Control` con `max-age` predefinito di **10 minuti** per i livelli di memorizzazione nella cache a valle. Questo vale per *Configurazioni BYOCDN (Bring-Your-Own-CDN)*, *browser per utenti finali* e qualsiasi *proxy di memorizzazione nella cache intermedi*, garantendo un controllo coerente della cache sull&#39;intero percorso di consegna.

### Personalizzazione delle intestazioni di controllo cache {#customizing-cache-control-headers}

Se si aumenta il tempo di trasmissione della cache per i valori live oltre la configurazione predefinita, aumenta la probabilità di distribuire contenuto non aggiornato, che può ritardare la visibilità degli aggiornamenti di contenuto nell’esperienza dell’utente finale. Se devi modificare il comportamento di controllo della cache per il caso d’uso specifico, puoi configurare regole CDN personalizzate per regolare le intestazioni di risposta. Questo consente di impostare durate della cache diverse in base alle esigenze. Consulta [Regole CDN personalizzate AEM per intestazioni di risposta](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic).

```
responseTransformations:
    rules:
      - name: cache-asset-delivery
        when:
          allOf:
            - reqProperty: path
              like: '/adobe/assets/urn:aaid:aem:*'
            - reqProperty: tier
              equals: delivery
        actions:
          - type: set
            respHeader: Cache-Control
            value: max-age=300
```

Per ulteriore assistenza o domande sulla gestione della cache, contatta il [supporto Adobe](https://helpx.adobe.com/in/contact.html).

## Annullamento validità cache attiva {#active-cache-invalidation}

Ogni volta che una risorsa viene aggiornata, eliminata o modificata (con eventuali modifiche ai metadati), Dynamic Media con API aperte invalida automaticamente ogni URL di consegna associato sulla rete CDN gestita di Adobe. Questo vale per gli URL che utilizzano ID di reindirizzamento o alias, insieme a eventuali URL che includono parametri di trasformazione come larghezza, formato o qualità. Questa invalidazione basata sugli eventi assicura che gli utenti ricevano sempre la versione più recente delle risorse senza alcun intervento manuale.

### Rimozione manuale della cache {#manual-cache-purging}

Se è necessario eliminare manualmente il contenuto memorizzato in cache, puoi farlo utilizzando le funzionalità di invalidamento della cache di AEM. Per istruzioni dettagliate su come eliminare specifici URL della cache, consulta [Annullamento della validità della cache CDN di AEM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-cache-purge#single-purge).

## Domande frequenti{#faq-cache-management}

+++**In che modo la gestione della cache influisce sulle integrazioni esistenti?**

Gli URL delle risorse rimangono invariati e l&#39;intestazione di controllo della cache inviata ai browser (e ad altri intermediari a valle) da Adobe Managed CDN continua a essere di 10 minuti con un [`stale-while-revalidate directive`](https://web.dev/articles/stale-while-revalidate#whats_it_mean), garantendo che i sistemi a valle continuino a sfruttare le cache in modo ottimale.

+++

+++**Che cosa attiva l&#39;eliminazione della cache?**

L’eliminazione della cache si attiva automaticamente quando una risorsa viene aggiornata, modificata, archiviata o eliminata.

<!--The cache purge triggers automatically in the following circumstances:
 
 - when an asset is updated, modified, or archived.
 - when an asset reaches `ready_for_delivery` state after approval.-->

+++

<!--
+++ **How long does it take for the cache to refresh after updating an asset?**

Any time the asset changes, the cache refreshes usually in *less than 60 seconds*.

+++

<!--
+++ **What happens if the cache purge system fails?**
The following mechanisms can be followed:
 
 - **Automatic retries:** 3 retry attempts with exponential backoff
 - **Monitoring:** Sev-2 alert fires if staleness exceeds 10 minutes
 - **Natural expiry:** Even without purge, cache expires after 10 hours maximum
 - **Manual override:** Engineers can manually purge via CLI tool

+++
-->

+++ **Quali sono tutti i tipi di risorse supportati per la memorizzazione nella cache di lunga durata?**

La memorizzazione in cache prolungata con annullamento della validità della cache attiva basato su eventi è applicabile a tutti i tipi di risorse in Dynamic Media con API aperte, indipendentemente dal tipo o dal formato della risorsa.

+++

+++ **Posso rinunciare al caching di lunga durata per il mio archivio?**

Contatta il [Supporto Adobe](https://helpx.adobe.com/in/contact.html) per spiegarne le motivazioni e Adobe ti contatterà per una discussione.

+++


>[!MORELIKETHIS]
>
>- [Integrare il Selettore risorse con varie applicazioni](/help/assets/integrate-asset-selector.md)
>- [URL personalizzati](/help/assets/vanity-urls.md)
