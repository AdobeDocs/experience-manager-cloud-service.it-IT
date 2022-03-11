---
title: Diagnostica ContextHub
description: ContextHub fornisce una pagina di diagnostica in cui puoi visualizzare una panoramica del framework ContextHub
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# Diagnostica ContextHub {#contexthub-diagnostics}

ContextHub fornisce una pagina di diagnostica in cui puoi visualizzare una panoramica del framework ContextHub. Per aprire la pagina, passa alla pagina `contexthub.diagnostics.html` pagina dell’istanza di authoring AEM, ad esempio:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

La pagina Diagnostica ContextHub fornisce informazioni sugli archivi e sui moduli di interfaccia utente creati, sulle cartelle della libreria client caricate e sui collegamenti a pagine utili.

>[!NOTE]
>
>Per poter restituire le informazioni di diagnostica, è necessario attivare la modalità di debug, altrimenti la pagina di diagnostica sarà vuota. Vedi [presente documento](configuring-contexthub.md#debugging-contexthub) per informazioni dettagliate su come abilitare la modalità di debug.

## Negozi {#stores}

Nella sezione Stores sono elencati tutti gli archivi ContextHub configurati. Ogni voce dell&#39;elenco è costituita dalle seguenti informazioni:

* **Titolo:** La [tipo di archivio](sample-stores.md) su cui si basa il negozio.
* **percorso:** Percorso del nodo del repository che contiene la configurazione.
* **resourceType:** Percorso del nodo del repository in cui è definito il tipo di archivio.
* **clientlibs:** Le categorie delle librerie client caricate che implementano il tipo di archivio.

## Moduli {#modules}

La sezione Moduli elenca tutti i moduli dell’interfaccia utente di ContextHub configurati. Ogni voce dell&#39;elenco è costituita dalle seguenti informazioni:

* **Titolo:** La [Tipo di modulo interfaccia utente](sample-modules.md) su cui si basa il modulo dell’interfaccia utente.
* **percorso:** Percorso del nodo del repository che contiene la configurazione.
* **resourceType:** Percorso del nodo del repository in cui è definito il tipo di modulo dell&#39;interfaccia utente.
* **clientlibs:** Le categorie delle librerie client caricate che implementano il tipo di modulo dell’interfaccia utente.

## Clientlibs {#clientlibs}

Nella sezione Clientlibs sono elencati tutti i [cartelle della libreria client](/help/implementing/developing/introduction/clientlibs.md) che ContextHub è stato caricato. Le librerie client sono classificate come segue:

* **kernel.js:** Librerie client che implementano il framework ContextHub, il motore dei segmenti e i tipi di archivio.
* **ui.js:** Librerie client che implementano i tipi di moduli di interfaccia utente e interfaccia utente di ContextHub.
* **style.css:** File CSS caricati dalle librerie client.

## URL {#urls}

La sezione URL contiene collegamenti alle funzioni di ContextHub:

* **Editor di configurazione:** Apre la [Pagina Configurazione ContextHub](configuring-contexthub.md) dove puoi configurare negozi, modalità di interfaccia utente e moduli di interfaccia utente.
* **Configurazione dei moduli ContextHub:** Apre la `/etc/cloudsettings/default/contexthub.config.kernel.js` file , che contiene la rappresentazione dell’oggetto Javascript delle configurazioni dell’archivio ContextHub.
* **Configurazione dell’interfaccia utente di ContextHub:** Apre la `/etc/cloudsettings/default/contexthub.config.ui.js` file , che contiene la rappresentazione dell’oggetto Javascript delle configurazioni della modalità di interfaccia utente ContextHub.
* **kernel.js:** Apre la `/etc/cloudsettings/default/contexthub.kernel.js` , che contiene il codice sorgente delle librerie client che implementano il framework ContextHub, il motore dei segmenti e i tipi di archivio.
* **ui.js:** Apre la `/etc/cloudsettings/default/contexthub.ui.js` , che contiene il codice sorgente delle librerie client che implementano i tipi di moduli di interfaccia utente e interfaccia utente di ContextHub.
* **style.css:** Apre la `/etc/cloudsettings/default/contexthub.styles.css` , che contiene gli stili CSS per i moduli di interfaccia utente e interfaccia utente di ContextHub.
