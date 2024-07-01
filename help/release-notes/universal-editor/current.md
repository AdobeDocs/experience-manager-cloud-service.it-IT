---
title: Note sulla versione di Universal Editor 2024.06.28
description: Queste sono le note sulla versione 2024.06.28 di Universal Editor.
feature: Release Information
role: Admin
source-git-commit: cc94ad2ba42707bb7541217f0225b995f64ad84f
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---


# Note sulla versione di Universal Editor 2024.06.28 {#release-notes}

Queste sono le note sulla versione del 28 giugno 2024 di Universal Editor.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novità {#what-is-new}

* **Home**: le pagine recenti vengono visualizzate come elenco, senza immagini di anteprima.
* **Barra della posizione**: è stata aggiunta la convalida URL avanzata, che impone l’utilizzo degli URL HTTPS e degli hash di supporto negli URL per l’esecuzione di applicazioni con indirizzamento hash.
* **Navigazione tramite tastiera**: la selezione della sovrapposizione pagina è stata scollegata dallo stato attivo della barra delle proprietà per migliorare la navigazione da tastiera sulla pagina senza perdere lo stato attivo.
* **Etichette elemento**: il valore di fallback per le etichette ora utilizza `data-aue-prop` invece di `data-aue-type` per una più chiara identificazione nelle sovrapposizioni e nella struttura del contenuto.
* **Finestra modale Editor Rich Text**: A **Annulla** è stato aggiunto al modale editor rich text quando lo si apre dal pannello proprietà.
* **Servizio UE sul nodo**: è stato reintrodotto il supporto HTTP per il servizio Universal Editor, in quanto tutte le connessioni HTTPS vengono terminate a livello di Dispatcher.
* **API di copia interna**: è stata aggiunta un’API al servizio Universal Editor per copiare i componenti, che consentirà la futura introduzione delle opzioni della barra degli strumenti per copiare e duplicare i contenuti.

## Correzioni di bug {#bug-fixes}

* **Breadcrumb pannello proprietà**: il menu delle breadcrumb nel pannello delle proprietà per gli elementi profondamente nidificati, che non rimaneva aperto, è stato corretto.
* **Selettore frammento di contenuto**: il selettore Frammento di contenuto è stato migliorato per garantire che rispetti le regole definite nel modello Frammento di contenuto o nel `data-aue-filter`.
* **Inserimento componente**: l’elenco per inserire nuovi componenti che non sono stati aggiornati con precisione dopo essere passati a un’altra pagina è stato corretto.
* **Stato pubblicazione**: la gestione degli stati di pubblicazione è stata migliorata per funzionare in modo più coerente.
* **Correzioni varie**: questa versione contiene anche varie correzioni minori, la pulizia del debito tecnologico, miglioramenti della sicurezza e test consolidati per la stabilità e le prestazioni complessive.
