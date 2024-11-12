---
title: Note sulla versione 2024.11.12 dell’editor universale
description: Queste sono le note sulla versione 2024.11.12 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 03ccad00e689052ada8cca976d6c385be01d3cc9
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 12%

---


# Note sulla versione 2024.11.12 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 12 novembre 2024 di Universal Editor.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novità {#what-is-new}

* **Opzione Riprova per timeout CORS:** Con [versione 2024.09.26,](/help/release-notes/universal-editor/2024/2024-09-26.md) è stato introdotto un pannello di errore quando l&#39;editor non è riuscito a stabilire una connessione alla pagina caricata, impedendo il caricamento di stati infiniti.
   * Con questa versione, l’editor continua automaticamente a riprovare e, una volta stabilita la connessione, è possibile riprendere la modifica.
   * Questa funzione è particolarmente utile per le pagine che potrebbero richiedere più tempo di un minuto prima dell’inizializzazione.
* **Miglioramenti dell&#39;estendibilità per sviluppatori:** Universal Editor ora supporta la trasmissione di eventi alle estensioni, consentendo agli sviluppatori di estensioni di sottoscrivere [eventi.](/help/implementing/universal-editor/events.md)
   * Questo consente agli sviluppatori di [reagire agli eventi dell&#39;editor all&#39;interno delle loro estensioni personalizzate.](/help/implementing/universal-editor/customizing.md#extending)
* **Selezione componente persistente:** I componenti selezionati nell&#39;editor persisteranno anche dopo l&#39;aggiornamento del browser.
   * In questo modo gli utenti possono continuare a lavorare senza perdere il loro contesto durante il ricaricamento della pagina.
* **Collegamenti rapidi localizzati:** La sezione **Collegamenti rapidi** nella schermata iniziale fornisce ora collegamenti localizzati alla documentazione, consentendo agli utenti di accedere facilmente alle guide pertinenti in base alle loro preferenze linguistiche.
* **ID richiesta per debug avanzato:** Le notifiche di errore ora includono un **ID richiesta** nella sezione dei dettagli, che è correlato a `x-request-id header`.
   * In questo modo i team di progettazione Adobe possono tracciare e diagnosticare più facilmente i problemi confrontando tali errori con i registri interni.

## Altri miglioramenti {#other-improvements}

* **Etichette di struttura contenuto lungo fisso:** è stato risolto un problema che causava la disattivazione delle etichette lunghe nel pannello **Struttura contenuto**
   * In questo modo le maniglie di trascinamento sono sempre visibili per il riordinamento dei contenuti.
* **Etichette proprietà lunghe corrette:** è stato corretto un bug a causa del quale le etichette dei campi lunghi nel pannello **Proprietà** si sovrapponevano alle informazioni di convalida dei campi
* **Scorrimento orizzontale nel pannello Proprietà:** è stato risolto un problema che causava lo scorrimento orizzontale di elementi di grandi dimensioni nel pannello **Proprietà**
* **Barra degli strumenti inattiva risolta durante le notifiche:** La barra degli strumenti **Adobe Experience Cloud** superiore è ora completamente funzionante quando vengono visualizzate le [notifiche](https://spectrum.adobe.com/page/toast/).
* **Stabilità migliorata:** sono stati aggiunti limiti di errore per gestire valori imprevisti, impedendo l&#39;arresto anomalo dell&#39;intera interfaccia utente quando un singolo renderer o convalida non riesce, migliorando la robustezza
