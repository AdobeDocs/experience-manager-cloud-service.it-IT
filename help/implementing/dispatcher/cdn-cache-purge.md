---
title: Rimozione della cache CDN
description: Scopri come rimuovere gli oggetti memorizzati in cache dalla cache CDN Adobe configurando il token API di eliminazione che può quindi essere utilizzato nelle chiamate API.
feature: Dispatcher
source-git-commit: 7224db99c29c90fb5e93ac07d7d501e2e9aaf74e
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---

# Rimozione della cache CDN {#cdn-purge-cache}

>[!NOTE]
>Questa funzione non è ancora disponibile al pubblico. Per partecipare al programma di adozione anticipata, invia un messaggio e-mail a `aemcs-cdn-config-adopter@adobe.com`.

La rimozione rimuove un oggetto dalla cache CDN di Adobe, determinando richieste future che procedono all’origine come mancanti nella cache, anziché essere servite dalla cache.
AEM as a Cloud Service consente di configurare un token API di rimozione, che può quindi essere utilizzato nelle chiamate API. Leggi le <!--[Configuring CDN Credentials and Authentication article](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token)--> per scoprire come configurare questo token utilizzando le direttive di autenticazione della pipeline di configurazione di Cloud Manager.

Sono supportate tre varianti di eliminazione:

* [Eliminazione di un singolo URL](#single-purge) : elimina una singola risorsa alla volta.
* [Rimuovi per chiave sostitutiva](#surrogate-key-purge) : eliminazione di più risorse contemporaneamente.
* [Pulizia completa](#full-purge) : elimina tutte le risorse.

Tutte le varianti di eliminazione condividono quanto segue:

* Il metodo HTTP deve essere impostato su `PURGE`.
* L’URL può essere qualsiasi dominio associato al servizio AEM a cui è destinata la richiesta di eliminazione.
* Il `X-AEM-Purge-Key` deve essere fornito in un’intestazione HTTP.

>[!CAUTION]
>La rimozione della cache CDN, in particolare con il flag rigido, aumenterà il traffico all’origine e potrebbe causare un’interruzione quando non viene eseguita correttamente.

## Eliminazione di un singolo URL {#single-purge}

Puoi eliminare una singola risorsa alla volta nel modo seguente:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

Come mostrato nell’esempio precedente, puoi **facoltativamente** specifica se la rete CDN deve eseguire una **duro** purge (impostazione predefinita) o **morbido** eliminare gli oggetti memorizzati in cache.

L’eliminazione rigida predefinita rende il contenuto immediatamente inaccessibile alle nuove richieste fino a quando non viene recuperato dall’origine. La rimozione temporanea contrassegna il contenuto come non aggiornato, ma lo distribuisce comunque ai client, che non devono quindi attendere finché non viene recuperato dall’origine.

## Elimina chiave sostitutiva {#surrogate-key-purge}

Le chiavi sostitutive sono identificatori univoci utilizzati per eliminare un set di contenuti. Vengono applicati al contenuto aggiungendo una `Surrogate-Key` alla risposta. È possibile fare riferimento a una o più chiavi sostitutive in una chiamata API di eliminazione.

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

Il `Surrogate-Key`(s) sono separati da spazi. Analogamente all’eliminazione con un singolo URL, puoi configurare un’eliminazione rigida o temporanea.

## Pulizia completa {#full-purge}

Puoi eseguire una rimozione completa di tutte le risorse memorizzate in cache come segue:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

Tieni presente che `X-AEM-Purge` l’intestazione deve includere il valore &quot;all&quot;.

## Interazioni con il livello Apache/Dispatcher {#apache-layer}

Come descritto nella [Articolo sul flusso di distribuzione dei contenuti](/help/implementing/dispatcher/overview.md), la rete CDN recupera il contenuto dal livello Apache/Dispatcher, se la cache è scaduta. Ciò significa che prima di eliminare una risorsa dalla rete CDN, è necessario assicurarsi che una nuova versione del contenuto sia disponibile anche in Dispatcher. Per maggiori dettagli vedi anche [Annullamento della validità della cache di Dispatcher](/help/implementing/dispatcher/caching.md#disp).
