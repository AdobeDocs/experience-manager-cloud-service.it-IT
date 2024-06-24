---
title: Diagnostica ContextHub
description: ContextHub fornisce una pagina di diagnostica in cui puoi visualizzare una panoramica del framework ContextHub
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Diagnostica ContextHub {#contexthub-diagnostics}

ContextHub fornisce una pagina di diagnostica in cui puoi visualizzare una panoramica del framework ContextHub. Per aprire la pagina, vai al `contexthub.diagnostics.html` pagina dell’istanza dell’autore AEM, ad esempio:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

La pagina Diagnostica ContextHub fornisce informazioni sugli archivi e i moduli di interfaccia utente creati, sulle cartelle della libreria client caricate e sui collegamenti a pagine utili.

>[!NOTE]
>
>Per restituire le informazioni di diagnostica, è necessario attivare la modalità di debug. In caso contrario, la pagina di diagnostica è vuota. Consulta [questo documento](configuring-contexthub.md#debugging-contexthub) per informazioni dettagliate su come abilitare la modalità di debug.

## Negozi {#stores}

La sezione Archivi elenca tutti gli store ContextHub configurati. Ogni voce dell&#39;elenco è costituita dalle seguenti informazioni:

* **Titolo:** Il [tipo di archivio](sample-stores.md) su cui si basa il negozio.
* **percorso:** Percorso del nodo dell’archivio che contiene la configurazione.
* **resourceType:** Percorso del nodo dell’archivio in cui è definito il tipo di archivio.
* **clientlibs:** Le categorie delle librerie client caricate che implementano il tipo di archivio.

## Moduli {#modules}

La sezione Moduli elenca tutti i moduli dell’interfaccia utente ContextHub configurati. Ogni voce dell&#39;elenco è costituita dalle seguenti informazioni:

* **Titolo:** Il [Tipo di modulo interfaccia utente](sample-modules.md) su cui si basa il modulo dell’interfaccia utente.
* **percorso:** Percorso del nodo dell’archivio che contiene la configurazione.
* **resourceType:** Percorso del nodo dell’archivio in cui è definito il tipo di modulo dell’interfaccia utente.
* **clientlibs:** Le categorie delle librerie client caricate che implementano il tipo di modulo dell’interfaccia utente.

## Clientlibs {#clientlibs}

La sezione Clientlibs elenca tutte le[cartelle di librerie client](/help/implementing/developing/introduction/clientlibs.md) ContextHub caricato. Le librerie client sono suddivise in categorie come segue:

* **kernel.js:** Librerie client che implementano il framework ContextHub, il motore di segmenti e i tipi di archivio.
* **ui.js:** Librerie client che implementano i tipi di moduli UI e interfaccia utente di ContextHub.
* **style.css:** File CSS caricati dalle librerie client.

## URL {#urls}

La sezione URL contiene collegamenti alle funzioni di ContextHub:

* **Editor configurazione:** Apre il [Pagina Configurazione ContextHub](configuring-contexthub.md) dove è possibile configurare store, modalità di interfaccia utente e moduli di interfaccia utente.
* **Configurazione dei moduli ContextHub:** Apre il `/etc/cloudsettings/default/contexthub.config.kernel.js` , che contiene la rappresentazione dell&#39;oggetto JavaScript delle configurazioni dell&#39;archivio ContextHub.
* **Configurazione dell’interfaccia utente di ContextHub:** Apre il `/etc/cloudsettings/default/contexthub.config.ui.js` , che contiene la rappresentazione dell&#39;oggetto JavaScript delle configurazioni della modalità interfaccia utente di ContextHub.
* **kernel.js:** Apre il `/etc/cloudsettings/default/contexthub.kernel.js` , che contiene il codice sorgente delle librerie client che implementano il framework ContextHub, il motore dei segmenti e i tipi di archivio.
* **ui.js:** Apre il `/etc/cloudsettings/default/contexthub.ui.js` , che contiene il codice sorgente delle librerie client che implementano i tipi di moduli UI e interfaccia utente di ContextHub.
* **style.css:** Apre il `/etc/cloudsettings/default/contexthub.styles.css` , che contiene gli stili CSS per i moduli UI e UI di ContextHub.
