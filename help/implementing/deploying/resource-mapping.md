---
title: Mappatura delle risorse
description: Scopri come definire reindirizzamenti, URL personalizzati e host virtuali per AEM utilizzando la mappatura delle risorse.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 1a1bb23c-d1d1-4e2b-811b-753e6a90a01b
role: Admin
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Mappatura delle risorse{#resource-mapping}

La mappatura delle risorse viene utilizzata per definire reindirizzamenti, URL personalizzati e host virtuali per l’AEM.

Ad esempio, puoi utilizzare queste mappature per:

* Aggiungi il prefisso `/content` a tutte le richieste in modo che la struttura interna sia nascosta ai visitatori del tuo sito Web.
* Definisci un reindirizzamento in modo che tutte le richieste alla pagina `/content/en/gateway` del sito Web vengano reindirizzate a `https://gbiv.com/`.

Un possibile prefisso di mappatura HTTP per tutte le richieste a `localhost:4503` con `/content`. Una mappatura come questa può essere utilizzata per nascondere la struttura interna dai visitatori al sito web in quanto consente:

`localhost:4503/content/we-retail/en/products.html`

Da accedere tramite:

`localhost:4503/we-retail/en/products.html`

Poiché il mapping aggiunge automaticamente il prefisso `/content` a `/we-retail/en/products.html`.

>[!CAUTION]
>
>Gli URL personalizzati non supportano i pattern regex.

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione di Sling e [Mapping per la risoluzione delle risorse](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) e [Risorse](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html).

## Visualizzazione delle definizioni di mappatura {#viewing-mapping-definitions}

Le mappature formano due elenchi che JCR Resource Resolver valuta (dall’alto verso il basso) per trovare una corrispondenza.

Questi elenchi possono essere visualizzati (insieme alle informazioni di configurazione) nell&#39;opzione **JCR ResourceResolver** della console Felix; ad esempio, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configurazione
Mostra la configurazione corrente (come definita per [Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map)).

* Prova di configurazione
Questo ti consente di immettere un URL o un percorso di risorsa. Fai clic su **Risolvi** o **Mappa** per confermare come il sistema trasforma la voce.

* **Voci mappa risolutore**
Elenco di voci utilizzate dai metodi ResourceResolver.resolve per mappare gli URL alle risorse.

* **Mappatura delle voci di mapping**
Elenco di voci utilizzate dai metodi ResourceResolver.map per mappare i percorsi delle risorse agli URL.

I due elenchi mostrano varie voci, comprese quelle definite come predefinite dalle applicazioni. Queste voci hanno spesso lo scopo di semplificare gli URL dell’utente.

Gli elenchi associano un **Pattern**, un&#39;espressione regolare corrispondente alla richiesta, con un **Replacement** che definisce il reindirizzamento da imporre.

Ad esempio:

**Pattern** `^[^/]+/[^/]+/welcome$`

Attiva:

**Sostituzione** `/libs/cq/core/content/welcome.html`.

Per reindirizzare una richiesta:

`https://localhost:4503/welcome` &quot;

A:

`https://localhost:4503/libs/cq/core/content/welcome.html`

All’interno dell’archivio vengono create nuove definizioni di mappatura.

>[!NOTE]
>
>Sono disponibili molte risorse che spiegano come definire le espressioni regolari. Ad esempio, [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Creazione di definizioni di mappatura in AEM {#creating-mapping-definitions-in-aem}

In un’installazione standard di AEM puoi trovare la cartella:

`/etc/map/http`

Questa cartella è la struttura utilizzata per definire le mappature per il protocollo HTTP. È possibile creare altre cartelle ( `sling:Folder`) in `/etc/map` per qualsiasi altro protocollo che si desidera mappare.

#### Configurazione di un reindirizzamento interno a /content {#configuring-an-internal-redirect-to-content}

Per creare il mapping con il prefisso `/content` per qualsiasi richiesta a https://localhost:4503/:

1. Utilizzando CRXDE passa a `/etc/map/http`.

1. Crea un nodo:

   * **Tipo** `sling:Mapping`
Questo tipo di nodo è destinato a tali mappature, anche se il suo utilizzo non è obbligatorio.

   * **Nome** `localhost_any`

1. Fare clic su **Salva tutto**.
1. **Aggiungi** le seguenti proprietà a questo nodo:

   * **Nome** `sling:match`

      * **Tipo** `String`

      * **Valore** `localhost.4503/`

   * **Nome** `sling:internalRedirect`

      * **Tipo** `String`

      * **Valore** `/content/`

1. Fare clic su **Salva tutto**.

Questa mappatura gestisce una richiesta come:
`localhost:4503/geometrixx/en/products.html`
come se:
`localhost:4503/content/geometrixx/en/products.html`
richiesto.

>[!NOTE]
>
>Consulta [Risorse](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) nella documentazione di Sling per ulteriori informazioni sulle proprietà sling disponibili e su come configurarle.
>Ad esempio, [Interpolazione stringa](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html#string-interpolation-for-etcmap) è utile perché consente di configurare una mappatura che ottiene i valori per ambiente tramite le variabili di ambiente.

>[!NOTE]
>
>È possibile utilizzare `/etc/map.publish` per mantenere le configurazioni per l&#39;ambiente di pubblicazione. Queste configurazioni devono essere replicate e la nuova posizione ( `/etc/map.publish`) deve essere configurata per **Posizione mappatura** del [Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map) dell&#39;ambiente di pubblicazione.
