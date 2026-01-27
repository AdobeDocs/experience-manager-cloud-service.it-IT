---
title: Cancella cache componente e GraphQL
description: Scopri come abilitare e verificare la funzione di cancellazione della cache in AEM CIF.
feature: Commerce Integration Framework
role: Admin
exl-id: f89c07c7-631f-41a4-b5b9-0f629ffc36f0
index: false
source-git-commit: e707bddc17208d599491d27c5bc0134cb41233e0
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 3%

---


# Cancella cache componente e GraphQL {#clear-cache}

Questo documento fornisce una guida completa sull’abilitazione e la verifica della funzione di cancellazione della cache in AEM CIF.

>[!NOTE]
>
> Questa funzione è sperimentale.

## Abilitazione della funzione di cancellazione della cache nella configurazione di CIF {#enable-clear-cache}

Per impostazione predefinita, la funzione di cancellazione della cache è disabilitata nella configurazione di CIF. Per abilitarlo, devi aggiungere quanto segue ai progetti corrispondenti:

* Abilita il servlet `/bin/cif/invalidate-cache` che ti consente di attivare l&#39;API clear-cache con le richieste corrispondenti aggiungendo la configurazione `com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json` nel progetto come mostrato [qui.](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config.author/com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json)

  >[!NOTE]
  >
  > La configurazione deve essere abilitata solo per le istanze di authoring.

* Consenti al listener di cancellare la cache da ogni istanza di AEM (pubblicazione e authoring) aggiungendo la configurazione `com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json` nel progetto come mostrato [qui.](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json)
   * La configurazione deve essere abilitata sia per le istanze di authoring che per quelle di pubblicazione.
   * Abilitare la cache di Dispatcher (facoltativo): è possibile abilitare l&#39;impostazione della cache di eliminazione del dispatcher impostando la proprietà `enableDispatcherCacheInvalidation` su true nella configurazione precedente. Questa funzione consente di cancellare la cache dal dispatcher.

     >[!NOTE]
     >
     > Questo funziona solo con le istanze di pubblicazione.

   * Inoltre, assicurati di fornire il modello corrispondente che si adatta al tuo prodotto, categoria e pagina CMS che deve essere aggiunto al file di configurazione di cui sopra per rimuoverlo dalla cache del dispatcher.

* Per migliorare le prestazioni delle query SQL per trovare la pagina corrispondente relativa al prodotto e alla categoria, aggiungi l’indice corrispondente nel progetto (scelta consigliata). Per ulteriori informazioni, vedere [cifCacheInvalidationSupport.](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.apps/src/main/content/jcr_root/_oak_index/cifCacheInvalidationSupport/.content.xml)

## Verifica della funzione di cancellazione della cache {#verify-clear-cache}

Per verificare che tutto sia configurato correttamente:

* Attiva il servlet corrispondente nell&#39;istanza di authoring di AEM, ad esempio [http://localhost:4502/bin/cif/invalidate-cache](http://localhost:4502/bin/cif/invalidate-cache). Riceverai una risposta HTTP 200.
* Verificare che un nodo sia stato creato nel percorso seguente nelle istanze di authoring: `/var/cif/cacheinvalidation`. Il nome del nodo segue questo pattern: `cmd_{{timestamp}}`.
* Verifica che lo stesso nodo sia stato creato in ogni istanza di pubblicazione.

Ora, per verificare se le cache vengono cancellate correttamente:

1. Passare alle pagine PLP e PDP corrispondenti.
2. Aggiorna il nome di un prodotto o di una categoria nel motore di commerce. Le modifiche non vengono riportate in AEM immediatamente in base alle configurazioni della cache.
3. Attiva l’API del servlet, come illustrato di seguito:

   ```
   curl --location '{Author AEM Instance Url}/bin/cif/invalidate-cache' \
   --header 'Content-Type: application/json' \
   --header 'Authorization: ******' \ // Mandatory
   --header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
   --data '{
       "productSkus": ["Sku1", "Sku2"], // Optional: Pass the corresponding sku which got updated.
       "categoryUids":["CategoryUid"], // Optional : Pass the corresponding category-uid which got updated.
       "storePath": "/content/venia/us/en", // Mandatory : Needs to be given to know for which site we are removing the clear cache.
   }'
   ```

Se tutto va bene, le nuove modifiche si riflettono in ogni istanza. Se le modifiche non sono visibili nell’istanza di pubblicazione, prova ad accedere alle pagine PLP e PDP pertinenti in una finestra del browser privata/in incognito.

>[!NOTE]
>
> Le istanze di pubblicazione possono avere più livelli di cache. La funzione è responsabile solo della cancellazione della cache dalla memoria interna di AEM e dal dispatcher.

## Cancella API di annullamento validità cache {#clear-cache-api}

Questa è l’API che devi attivare ogni volta che desideri cancellare la cache dei dati relativi a commerce da AEM.

Tipo di richiesta: `POST`

### Intestazioni {#headers}

| Parametro | Valore | Obbligatorio/Obbligatorio | Commenti |
|------------------------------|-------------------|---|---|
| `Content-Type` | `application/json` | Obbligatorio |  |
| `Authorization` | Credenziali utente autore corrispondenti (tipo di autenticazione: autenticazione di base) | Obbligatorio | Aggiungi il nome utente e la password corrispondenti. |


### Payload {#payload}

Nella tabella seguente sono illustrati gli attributi esistenti forniti dalla feature. Queste proprietà `InvalidateType` devono essere fornite in combinazione con l&#39;attributo obbligatorio (ad esempio `storePath`).

| `invalidateType` | Valore | Tipo (Array/String/Boolean) | La cache del dispatcher verrà cancellata? | Commenti |
|------------------------------|-------------------|---|---|---|
| `productSkus` | SKU del prodotto, che deve essere invalidato dalla cache. | Array | Sì | Cancella la cache dalla memoria interna utilizzando il seguente pattern:<br>```"\"sku\":\\s*\""```<br>Dispatcher<br><ul><li>Cancella la cache delle pagine PDP degli SKU corrispondenti</li><li>Cancella la cache della pagina categorie corrispondente in cui esistono (in base alla risposta graphql da commerce)</li><li>Cancella la cache in base alla seguente query:</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content, '{storePath}')<br>AND ( (content.[product] IN ('sku1','sku2') AND content.[productType] = 'combinedSku')<br> OR (content.[selection] IN ('sku1','sku2') AND content.[selectionType] IN ('combinedSku', 'sku')))``` |
| `categoryUids` | UID della categoria: da invalidare dalla cache. | Array | Sì | Cancella la cache dalla memoria interna utilizzando il seguente pattern:<br>```"\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\""```<br>Dispatcher<br><ul><li>Cancella la cache delle pagine delle categorie per i dati corrispondenti (inclusa la pagina delle categorie figlio)</li><li>Cancella tutte le pagine PDP con le categorie corrispondenti</li><li>Cancella la cache in base alla seguente query:</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content,'{storePath}')<br>AND ((content.[categoryId] in ('category1','category2')<br>AND content.[categoryIdType] in ('uid'))<br>OR (content.[category] in ('category1','category2') AND content.[categoryType] in ('uid')))``` |
| `regexPatterns` | Se devi cancellare i dati di risposta di GraphQL in base al modello regex, utilizza questo. | Array | No | |
| `cacheNames` | Questi valori sono definiti nella configurazione del client CIF GraphQL corrispondente in fabbrica >> Configurazione StorePath GraphQL corrispondente >> Configurazioni cache GraphQL | Array | No | |
| `invalidateAll` | True o false | Booleano | Sì | |

Questa tabella mostra la proprietà obbligatoria che deve essere passata in ogni chiamata API:

| Proprietà | Valore | Tipo (Array/String/Boolean) | La cache del dispatcher verrà cancellata? | Commenti |
|------------------------------|-------------------|---|---|---|
| `storePath` | Valore corrispondente del percorso del sito da cui rimuovere la cache (esempio: `/content/venia/us/en` come riferimento con il progetto Venia). | Stringa | Sì | Questo valore deve essere specificato con la combinazione di `invalidateType.` |

### Richiesta API di esempio {#sample-request}

```text
curl --location 'https://author-p10603-e145552-cmstg.adobeaemcloud.com/bin/cif/invalidate-cache' \
--header 'Content-Type: application/json' \
--header 'Authorization: ******' \
--header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
--data '{
"productSkus": ["VP01", "VT10"], // This will clear cache for the corresponding pages related with mentioned skus.
"categoryUids":["Mjk="], // This will clear cache for the corresponding pages related with mentioned categories.
"regexPatterns":["\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\"(Mjk=)\"", "\"sku\":\\s*\"(VP02|VP03)\""],
"cacheNames": ["venia/components/commerce/product"], // If this been added then it will clear respective caches for the corresponding storepath
"storePath": "/content/venia/us/en"
}'
```

## Estensibilità {#clear-cache-extensibility}

Questa funzione offre non solo le funzionalità di base, ma anche l’estensibilità, consentendo agli sviluppatori di sfruttarla e personalizzarla ulteriormente in base alle esigenze.

### Estensione dell’attributo esistente {#existing-attribute}

Nei casi in cui è necessario cancellare la cache che al momento non sono coperti dalla funzionalità esistente basata su attributi (ad esempio `categoryUids`), puoi fare riferimento a [questo file di riferimento](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/ExtendedCategoryUidInvalidation.java) per aggiungere nuovi modelli e definire ulteriori `invalidatePaths` che devono essere cancellati dalla cache oltre a ciò che gestisce l&#39;implementazione corrente.

### Aggiunta di un nuovo attributo personalizzato {#new-custom-attribute}

Se, ad esempio, non si desidera utilizzare l&#39;attributo esistente per cancellare la cache, è possibile creare un attributo personalizzato e definirne la funzionalità corrispondente.

* Se devi solo cancellare la cache dalla memoria interna di AEM (la risposta graphql), devi seguire [questo riferimento.](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomInvalidation.java)
* Se devi cancellare la cache dalla memoria interna e dalla cache del dispatcher, devi seguire [questo riferimento.](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomDispatcherInvalidation.java)

  >[!NOTE]
  >
  > È possibile ignorare la cache di cancellazione interna restituendo `null` per il metodo `getPatterns()`.
