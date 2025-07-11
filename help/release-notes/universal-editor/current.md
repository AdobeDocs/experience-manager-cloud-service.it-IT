---
title: Note sulla versione 2025.07.09 dell’editor universale
description: Queste sono le note sulla versione 2025.07.09 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 199ee7e11f6706773bd426c3d27236d6ea791a6c
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 25%

---


# Note sulla versione 2025.07.09 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 9 luglio 2025 di Universal Editor.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* [Facendo clic sul pulsante **Aggiungi** sulla barra degli strumenti dei contenitori,](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components) se è consentito un solo tipo di componente, questo viene inserito immediatamente senza richiedere la selezione dal menu a discesa.
* [L&#39;opzione della barra degli strumenti dell&#39;intestazione di autenticazione](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings) è stata posizionata dietro un interruttore di funzionalità, in quanto non è utile nella maggior parte dei casi.
* [Poiché la nidificazione dei contenitori non è consentita per più campi nel pannello delle proprietà,](/help/implementing/universal-editor/field-types.md#fields) la routine di rendering ora filtra i contenitori nidificati dall&#39;elenco dei campi per impedire la nidificazione non valida.

## Funzioni per adozione anticipata {#early-adopter}

Se ti interessa testare queste nuove funzioni e condividere i tuoi commenti, invia un’e-mail al tuo Customer Success Manager Adobe dall’indirizzo e-mail associato al tuo Adobe ID.

### Nuovo editor Rich Text {#new-rte}

Il nuovo editor Rich Text ProseMirror, con un selettore di pagina nella finestra di dialogo del collegamento, è ora disponibile nel pannello di destra.

### Annulla/Ripristina {#undo-redo}

La funzione Annulla e Ripeti è ora disponibile per gli autori di contenuti dell’Editor universale.

* Sono incluse le modifiche apportate nel contesto, quelle effettuate tramite il pannello Proprietà, nonché l’aggiunta (o la duplicazione), lo spostamento e l’eliminazione di blocchi.
* Le operazioni Annulla e Ripeti sono limitate alla sessione corrente del browser.

## Altri miglioramenti {#other-improvements}

* È stato risolto un problema che impediva la rimozione di un singolo riferimento a una risorsa durante la modifica tramite la barra delle proprietà.
* È stato risolto un problema che causava il caricamento indefinito del pannello Proprietà, poiché i riferimenti alle risorse venivano automaticamente convertiti in array, causando uno stato di caricamento infinito.
   * I valori di riferimento delle risorse vengono ora memorizzati così come sono, senza conversione automatica in array.
* È stato risolto un problema a causa del quale il pannello Proprietà non visualizzava campi quando era definito un modello, ma non conteneva alcun contenuto.
   * Questo causava uno stato di caricamento infinito per il pannello Proprietà per risposte di dettaglio vuote, come nel caso di frammenti di contenuto vuoti.
* La configurazione ESLint è stata sottoposta a refactoring per compatibilità con la versione 9, incluso il supporto di regole aggiornate e plug-in.

## Obsoleti {#deprecations}

* Il componente `text-input` è ora ufficialmente obsoleto.
   * In `model-definition.json`, utilizzare il componente testo per creare input di testo per il pannello Proprietà.
