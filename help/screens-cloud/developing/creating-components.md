---
title: Creazione di componenti
description: I componenti AEM vengono utilizzati per memorizzare, formattare ed eseguire il rendering dei contenuti resi disponibili sulle pagine web. Segui questa pagina per scoprire come creare canali e componenti di rendering.
exl-id: a81e812e-29ed-45de-b2d0-1fb0a8c5ce1a
feature: Developing Screens
role: Admin, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# Creazione di componenti {#creating-components}

I componenti AEM vengono utilizzati per memorizzare, formattare ed eseguire il rendering dei contenuti resi disponibili sulle pagine web.

## Authoring dei canali {#authoring-channels}

Il canale è l&#39;oggetto principale dei contenuti inviati a un insieme di display. Pertanto, un autore di contenuti in genere apre un canale nell’editor per aggiungere o modificare contenuti. Poiché il canale è un ***cq:Page***, per aggiungere e modificare i componenti sul canale seguirà lo stesso pattern UX tradizionale.

Tuttavia, poiché i componenti di un canale vengono in genere visualizzati a schermo intero, l’esperienza di authoring ne risentirà quando si tenta di modificare singoli componenti o di comporre nuovi ordini. Pertanto, il canale si basa sui selettori per eseguire il rendering di diverse viste dei componenti. L’ambiente di authoring utilizza il selettore di modifica per attivare il rendering del canale personalizzato.

Ad esempio `http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

L’utente non deve preoccuparsi di aggiungere il selettore all’URL durante la modifica. Una logica lato client è in ascolto dell&#39;evento switch di livello e aggiunge il selettore se il canale ha il tipo di risorsa dedicato *screens/core/components/channel.*

## Rendering dei componenti {#rendering-components}

Per abilitare l’authoring corretto, i componenti devono fornire i due rendering seguenti:

| **Component** | **Rappresentazioni** |
|---|---|
| *my-component/my-component.html* | rendering di produzione |
| *my-component/edit.html* | modifica del rendering in una vista più piccola |

I componenti incorporati utilizzano le seguenti categorie di librerie client:

| **Component** | **Libreria client** |
|---|---|
| *cq.screens.components.edit* | CSS e JS che devono essere caricati durante la creazione |
| *cq.screens.components.production* | CSS e JS che devono essere caricati quando il canale è in esecuzione |
| *cq.screens.components* | CSS e JS condivisi |

>[!NOTE]
>
>Per sviluppare componenti personalizzati, utilizzare il modello di componente di esempio ***[AEM Screens](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)***.
