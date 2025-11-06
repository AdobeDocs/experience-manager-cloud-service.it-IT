---
title: Diagnostica ContextHub
description: ContextHub fornisce una pagina di diagnostica in cui puoi visualizzare una panoramica del framework ContextHub
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
feature: Developing, Personalization
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Diagnostica ContextHub {#contexthub-diagnostics}

ContextHub fornisce una pagina di diagnostica in cui puoi visualizzare una panoramica del framework ContextHub. Per aprire la pagina, vai alla pagina `contexthub.diagnostics.html` dell&#39;istanza Autore AEM, ad esempio:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

La pagina Diagnostica ContextHub fornisce informazioni sugli archivi e i moduli di interfaccia utente creati, sulle cartelle della libreria client caricate e sui collegamenti a pagine utili.

>[!NOTE]
>
>Per restituire le informazioni di diagnostica, è necessario attivare la modalità di debug. In caso contrario, la pagina di diagnostica è vuota. Consulta [questo documento](configuring-contexthub.md#debugging-contexthub) per informazioni dettagliate su come abilitare la modalità di debug.

## Negozi {#stores}

La sezione Archivi elenca tutti gli store ContextHub configurati. Ogni voce dell&#39;elenco è costituita dalle seguenti informazioni:

* **Titolo:** Il tipo di archivio [store](sample-stores.md) su cui si basa l&#39;archivio.
* **percorso:** Percorso del nodo dell&#39;archivio che contiene la configurazione.
* **resourceType:** il percorso del nodo dell&#39;archivio in cui è definito il tipo di archivio.
* **clientlibs:** le categorie delle librerie client caricate che implementano il tipo di archivio.

## Moduli {#modules}

La sezione Moduli elenca tutti i moduli dell’interfaccia utente ContextHub configurati. Ogni voce dell&#39;elenco è costituita dalle seguenti informazioni:

* **Titolo:** il tipo di modulo [UI](sample-modules.md) su cui si basa il modulo UI.
* **percorso:** Percorso del nodo dell&#39;archivio che contiene la configurazione.
* **resourceType:** il percorso del nodo dell&#39;archivio in cui è definito il tipo di modulo dell&#39;interfaccia utente.
* **clientlibs:** le categorie delle librerie client caricate che implementano il tipo di modulo dell&#39;interfaccia utente.

## Clientlibs {#clientlibs}

La sezione Clientlibs elenca tutte le [cartelle della libreria client](/help/implementing/developing/introduction/clientlibs.md) caricate da ContextHub. Le librerie client sono suddivise in categorie come segue:

* **kernel.js:** librerie client che implementano il framework ContextHub, il motore di segmenti e i tipi di archivio.
* **ui.js:** librerie client che implementano i tipi di moduli UI e ContextHub.
* **style.css:** file CSS caricati dalle librerie client.

## URL {#urls}

La sezione URL contiene collegamenti alle funzioni di ContextHub:

* **Editor configurazione:** Apre la [pagina Configurazione ContextHub](configuring-contexthub.md) in cui è possibile configurare archivi, modalità interfaccia utente e moduli interfaccia utente.
* **Configurazione dei moduli ContextHub:** Apre il file `/etc/cloudsettings/default/contexthub.config.kernel.js`, che contiene la rappresentazione dell&#39;oggetto JavaScript delle configurazioni dell&#39;archivio ContextHub.
* **Configurazione dell&#39;interfaccia utente di ContextHub:** Apre il file `/etc/cloudsettings/default/contexthub.config.ui.js`, che contiene la rappresentazione dell&#39;oggetto JavaScript delle configurazioni della modalità dell&#39;interfaccia utente di ContextHub.
* **kernel.js:** Apre il file `/etc/cloudsettings/default/contexthub.kernel.js`, che contiene il codice sorgente delle librerie client che implementano il framework ContextHub, il motore dei segmenti e i tipi di archivio.
* **ui.js:** Apre il file `/etc/cloudsettings/default/contexthub.ui.js`, che contiene il codice sorgente delle librerie client che implementano i tipi di modulo UI e interfaccia utente di ContextHub.
* **style.css:** Apre il file `/etc/cloudsettings/default/contexthub.styles.css`, che contiene gli stili CSS per i moduli interfaccia utente e ContextHub.
