---
title: Eliminazione della cache CDN
description: Scopri come rimuovere gli oggetti memorizzati in cache dalla cache CDN Adobe configurando il token API di eliminazione che può quindi essere utilizzato nelle chiamate API.
feature: CDN Cache
exl-id: 4d091677-b817-4aeb-b131-7a5407ace3e0
role: Admin
source-git-commit: 5b777171cb9246c2a0174985e060d7d1b6ed8591
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Eliminazione della cache CDN {#cdn-purge-cache}

La rimozione rimuove un oggetto dalla cache CDN di Adobe, determinando richieste future che procedono all’origine come mancanti nella cache, anziché essere servite dalla cache.
AEM as a Cloud Service consente di configurare un token API di rimozione, che può quindi essere utilizzato nelle chiamate API di rimozione. Leggi [Configurazione delle credenziali CDN e dell&#39;autenticazione](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) per scoprire come configurare questo token utilizzando le direttive di autenticazione della pipeline di configurazione di Cloud Manager.

Sono supportate tre varianti di eliminazione:

* [Eliminazione URL singolo](#single-purge). Eliminare una singola risorsa alla volta.
* [Rimuovi tramite chiave sostitutiva](#surrogate-key-purge) - elimina più risorse contemporaneamente.
* [Rimozione completa](#full-purge) - elimina tutte le risorse.

Tutte le varianti di eliminazione condividono quanto segue:

* Il metodo HTTP deve essere impostato su `PURGE`.
* L’URL può essere qualsiasi dominio associato al servizio AEM a cui è destinata la richiesta di eliminazione.
* `X-AEM-Purge-Key` deve essere fornito in un&#39;intestazione HTTP.

>[!CAUTION]
>La rimozione della cache CDN, in particolare con il flag rigido, aumenterà il traffico all’origine e potrebbe causare un’interruzione quando non viene eseguita correttamente.

Puoi fare riferimento a [un&#39;esercitazione](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache) incentrata sulla configurazione delle chiavi di eliminazione e sull&#39;esecuzione dell&#39;eliminazione della cache CDN.

## Eliminazione di un singolo URL {#single-purge}

Puoi eliminare una singola risorsa alla volta nel modo seguente:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

Come mostrato nell&#39;esempio precedente, è possibile **facoltativamente** specificare se la rete CDN deve eseguire una rimozione di **hard** (impostazione predefinita) o di **soft** sugli oggetti memorizzati in cache.

L’eliminazione rigida predefinita rende il contenuto immediatamente inaccessibile alle nuove richieste fino a quando non viene recuperato dall’origine. La rimozione temporanea contrassegna il contenuto come non aggiornato, ma lo distribuisce comunque ai client, che non devono quindi attendere finché non viene recuperato dall’origine.

## Elimina chiave sostitutiva {#surrogate-key-purge}

Le chiavi sostitutive sono identificatori univoci utilizzati per eliminare un set di contenuti. Vengono applicati al contenuto aggiungendo un&#39;intestazione `Surrogate-Key` alla risposta. È possibile fare riferimento a una o più chiavi sostitutive in una chiamata API di eliminazione.

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

I `Surrogate-Key` sono separati da spazi. Analogamente all’eliminazione con un singolo URL, puoi configurare un’eliminazione rigida o temporanea.

## Pulizia completa {#full-purge}

Puoi eseguire una rimozione completa di tutte le risorse memorizzate in cache come segue:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

Tenere presente che l&#39;intestazione `X-AEM-Purge` deve includere il valore &#39;all&#39;.

## Interazioni con il livello Apache/Dispatcher {#apache-layer}

Come descritto in [Flusso di distribuzione dei contenuti](/help/implementing/dispatcher/overview.md), la rete CDN recupera il contenuto dal livello Apache/Dispatcher, se la cache è scaduta. Ciò significa che prima di eliminare una risorsa dalla rete CDN, è necessario assicurarsi che una nuova versione del contenuto sia disponibile anche in Dispatcher. Per ulteriori dettagli vedi anche [Annullamento della validità della cache di Dispatcher](/help/implementing/dispatcher/caching.md#disp).
