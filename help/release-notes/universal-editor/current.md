---
title: Note sulla versione 2025.09.04 dell’editor universale
description: Queste sono le note sulla versione 2025.09.04 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 0c380e0faca1db0966d22d056dd1f824a731a7bc
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 71%

---


# Note sulla versione 2025.09.04 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 4 settembre 2025 di Universal Editor.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* Il comando Copia/Incolla è disponibile per [utenti che lo hanno adottato in anticipo](#copy-paste)

### Annullare/Ripetere {#undo-redo}

La funzione Annulla e Ripeti è ora disponibile per gli autori di contenuti dell’Editor universale.

* Sono incluse le modifiche apportate nel contesto, quelle effettuate tramite il pannello Proprietà, nonché l’aggiunta (o la duplicazione), lo spostamento e l’eliminazione di blocchi.
* Le operazioni Annulla e Ripeti sono limitate alla sessione corrente del browser.

## Funzioni per adozione anticipata {#early-adopter}

Se ti interessa testare queste nuove funzioni e condividere un feedback, invia un’e-mail al tuo Adobe Customer Success Manager dall’indirizzo e-mail associato al tuo Adobe ID.

### Nuovo editor Rich Text {#new-rte}

Il nuovo editor Rich Text ProseMirror, con un selettore di pagina nella finestra di dialogo del collegamento, è ora disponibile nel pannello di destra.

### Copia/Incolla {#copy-paste}

Gli autori di contenuti possono ora copiare e incollare componenti all’interno della stessa pagina.

## Altri miglioramenti {#other-improvements}

* Lo stile della barra degli strumenti dell’editor è stato aggiornato per allinearlo meglio al nuovo editor RTF in arrivo.
* I filtri nella finestra di dialogo del selettore risorse sono stati ripristinati.

## Rimozioni {#deprecations}

* I componenti `text-input` e `text-area` sono stati ufficialmente dichiarati obsoleti con la [versione 2025.07.09.](/help/release-notes/universal-editor/2025/2025-07-09.md)
   * In `model-definition.json`, utilizza il componente testo per creare input di testo per il pannello Proprietà.
