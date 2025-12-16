---
title: Note sulla versione 2025.12.12 dell’editor universale
description: Queste sono le note sulla versione 2025.12.11 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b7b89587a81d0cadc81d4b2a486c022557c4a9fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 21%

---


# Note sulla versione 2025.12.12 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 12 dicembre 2025 di Universal Editor.

>[!TIP]
>
>Se desideri testare le **prossime** funzionalità dell’editor universale prima che vengano rilasciate, consulta le [note sulla versione di anteprima dell’editor universale.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* Il supporto è stato aggiunto alle tabelle esistenti nell&#39;editor Rich Text [.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)
* Tasto di tabulazione abilitato per la nidificazione di elenchi nell&#39;editor di testo RTF [.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)
* È ora possibile disabilitare la funzione di accesso per sviluppatori tramite il tag [meta `aem-dev-login`.](/help/implementing/universal-editor/customizing.md#meta-tags)
* Facendo clic con il pulsante destro del mouse nella sezione di sovrapposizione viene ora visualizzato un menu di [opzioni contestuali.](/help/sites-cloud/authoring/universal-editor/authoring.md#context-options)
* [Il rientro con ambito](/help/implementing/universal-editor/configure-rte.md#indentation) è ora supportato nell&#39;editor di testo RTF [.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)

## Funzioni per adozione anticipata {#early-adopter}

Se ti interessa testare le prossime funzionalità elencate di seguito e condividere i tuoi commenti, invia un’e-mail al tuo Customer Success Manager Adobe dall’indirizzo e-mail associato al tuo Adobe ID.

* La copia superficiale è stata implementata per i frammenti di contenuto.

## Altri miglioramenti {#other-improvements}

* La barra delle proprietà ora è sincronizzata quando più campi cambiano nel contesto.
* Il selettore Frammento di contenuto ora si apre come previsto sulle istanze AEM 6.5.
* Il tasto Esc ora chiude le finestre di dialogo nell’editor Rich Text.
* L&#39;azione **Rimuovi componente** è ora disponibile solo quando è selezionato un componente.
* L’editor di frammenti di contenuto corretto (vecchio o nuovo) ora viene aperto in base all’istanza utilizzata (se il nome host è il pattern di AEM as a Cloud Service, utilizza il nuovo editor, altrimenti utilizza l’editor legacy).
* La convalida del filtro viene aggiunta all’azione duplicata.
* I titoli lunghi vengono ora troncati nella barra delle proprietà.
* Gli array di gestione multisito con più di 10 valori ora vengono gestiti correttamente.
* Gli errori di conflitto durante la creazione di più componenti con lo stesso nome vengono ora gestiti correttamente.
* È stata aggiunta la gestione di array di gestione multisito con valori > 10.
