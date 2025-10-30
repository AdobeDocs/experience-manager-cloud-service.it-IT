---
title: Note sulla versione 2025.10.30 dell’editor universale
description: Queste sono le note sulla versione 2025.10.30 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: e3e571bef450ddc09eb30ab7d73b144ea521a87b
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 58%

---


# Note sulla versione 2025.10.30 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 30 ottobre 2025 di Universal Editor.

>[!TIP]
>
>Se desideri testare le **prossime** funzionalità dell’editor universale prima che vengano rilasciate, consulta le [note sulla versione di anteprima dell’editor universale.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* [Il nuovo editor Rich Text](#new-rte) ora può inserire immagini.
   * Questa funzionalità è disabilitata e deve essere abilitata in modo esplicito tramite una definizione di filtro [.](/help/implementing/universal-editor/configure-rte.md#toolbar)

## Funzioni per adozione anticipata {#early-adopter}

Se ti interessa testare queste nuove funzioni e condividere un feedback, invia un’e-mail al tuo Adobe Customer Success Manager dall’indirizzo e-mail associato al tuo Adobe ID.

### Nuovo editor Rich Text {#new-rte}

Il nuovo editor Rich Text ProseMirror, con un selettore di pagina nella finestra di dialogo del collegamento, è ora disponibile nel pannello di destra. [Questo editor Rich Text offre opzioni di configurazione flessibili.](/help/implementing/universal-editor/configure-rte.md)

## Altri miglioramenti {#other-improvements}

* L’evento di aggiornamento viene ora informato se l’azione è stata annullata.
* La stringa `No results` ora dipende dalle impostazioni locali del browser nei tag di Universal Editor.
* È stata corretta un’interruzione di riga aggiuntiva nel pulsante Publish di Universal Editor.
* La pulizia è stata effettuata per patch API.
* Il pulsante Seleziona contenuto è ora visibile in Safari.
* Compilazione RPM corretta.
* Aggiornamento CORS per evitare di aggiornare nuovamente il testo modificato dopo il salvataggio.
