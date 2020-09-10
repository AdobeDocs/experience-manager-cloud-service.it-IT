---
title: Diagnostica ContextHub
description: ContextHub fornisce una pagina di diagnostica in cui potete vedere una panoramica del framework ContextHub
translation-type: tm+mt
source-git-commit: e361f24b943eff68982a37ac0dc2597f92450026
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Diagnostica ContextHub {#contexthub-diagnostics}

ContextHub fornisce una pagina di diagnostica in cui potete vedere una panoramica del framework ContextHub. Per aprire la pagina, passate alla `contexthub.diagnostics.html` pagina dell’istanza di authoring AEM, ad esempio:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

La pagina Diagnostica ContextHub fornisce informazioni sugli store e sui moduli dell&#39;interfaccia utente creati, sulle cartelle della libreria client che vengono caricate e sui collegamenti alle pagine utili.

>[!NOTE]
>
>Per poter restituire le informazioni diagnostiche, è necessario abilitare la modalità di debug, altrimenti la pagina di diagnostica sarà vuota. Per informazioni dettagliate su come abilitare la modalità di debug, consultate [questo documento](configuring-contexthub.md#debugging-contexthub) .

## Negozi {#stores}

Nella sezione Store sono elencati tutti gli store ContextHub configurati. Ogni elemento dell&#39;elenco è costituito dalle seguenti informazioni:

* **Titolo:** Il tipo [di](sample-stores.md) store su cui si basa lo store.
* **percorso:** Percorso del nodo del repository che contiene la configurazione.
* **resourceType:** Percorso del nodo del repository in cui è definito il tipo di archivio.
* **clientlibs:** Le categorie delle librerie client caricate che implementano il tipo di store.

## Moduli {#modules}

Nella sezione Moduli sono elencati tutti i moduli di interfaccia utente ContextHub configurati. Ogni elemento dell&#39;elenco è costituito dalle seguenti informazioni:

* **Titolo:** Il tipo [di modulo](sample-modules.md) dell&#39;interfaccia utente su cui si basa il modulo.
* **percorso:** Percorso del nodo del repository che contiene la configurazione.
* **resourceType:** Percorso del nodo del repository in cui è definito il tipo di modulo dell&#39;interfaccia utente.
* **clientlibs:** Le categorie delle librerie client caricate che implementano il tipo di modulo dell&#39;interfaccia utente.

## Clientlibs {#clientlibs}

Nella sezione Clientlibs sono elencate tutte le cartelle della libreria client caricate da ContextHub. Le librerie client sono classificate come segue:

* **kernel.js:** Librerie client che implementano il framework ContextHub, il motore del segmento e i tipi di store.
* **ui.js:** Librerie client che implementano l&#39;interfaccia utente ContextHub e i tipi di moduli dell&#39;interfaccia utente.
* **style.css:** File CSS caricati dalle librerie client.

## URL {#urls}

La sezione URL contiene collegamenti alle funzioni ContextHub:

* **Editor di configurazione:** Apre la pagina [Configurazione](configuring-contexthub.md) ContextHub in cui è possibile configurare store, modalità di interfaccia utente e moduli di interfaccia utente.
* **Configurazione dei moduli ContextHub:** Apre il `/etc/cloudsettings/default/contexthub.config.kernel.js` file, che contiene la rappresentazione oggetto Javascript delle configurazioni dell&#39;archivio ContextHub.
* **Configurazione dell’interfaccia utente ContextHub:** Apre il `/etc/cloudsettings/default/contexthub.config.ui.js` file, che contiene la rappresentazione oggetto Javascript delle configurazioni della modalità di interfaccia utente ContextHub.
* **kernel.js:** Apre il `/etc/cloudsettings/default/contexthub.kernel.js` file, che contiene il codice di origine delle librerie client che implementano il framework ContextHub, il motore del segmento e i tipi di store.
* **ui.js:** Apre il `/etc/cloudsettings/default/contexthub.ui.js` file, che contiene il codice sorgente delle librerie client che implementano i tipi di interfaccia utente e moduli dell&#39;interfaccia utente ContextHub.
* **style.css:** Apre il `/etc/cloudsettings/default/contexthub.styles.css` file, che contiene gli stili CSS per l&#39;interfaccia utente e i moduli dell&#39;interfaccia utente ContextHub.
