---
title: Note sulla versione 2025.11.06 dell’editor universale
description: Queste sono le note sulla versione 2025.11.06 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 5c762da645ee26164d39af3936fc6b3fcbd43f0b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 50%

---


# Note sulla versione 2025.11.06 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 6 novembre 2025 di Universal Editor.

>[!TIP]
>
>Se desideri testare le **prossime** funzionalità dell’editor universale prima che vengano rilasciate, consulta le [note sulla versione di anteprima dell’editor universale.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Funzioni per adozione anticipata {#early-adopter}

Se ti interessa testare queste nuove funzioni e condividere un feedback, invia un’e-mail al tuo Adobe Customer Success Manager dall’indirizzo e-mail associato al tuo Adobe ID.

### Nuovo editor Rich Text {#new-rte}

Il nuovo editor Rich Text ProseMirror, con un selettore di pagina nella finestra di dialogo del collegamento, è ora disponibile nel pannello di destra. [Questo editor Rich Text offre opzioni di configurazione flessibili.](/help/implementing/universal-editor/configure-rte.md)

## Altri miglioramenti {#other-improvements}

* È ora possibile eliminare correttamente i campi di metadati `og:title`.
* È stato risolto un problema di navigazione che si verificava quando un utente modificava la barra della posizione nell’editor del browser in modo che le modifiche venissero applicate correttamente e l’editor e/o l’app ora passasse all’URL richiesto.
* La risoluzione del modello di campo è stata corretta e l’editor utilizza il modello del componente, se presente.
* Il componentId è ora incluso nell’azione /add.
* È stata corretta la possibilità di eliminare alcune proprietà di metadati che in precedenza non era possibile rimuovere.
* Il recupero non elaborato ora viene eseguito in modo condizionale per xwalk quando non è impostato dal plug-in AEM.
* La gestione MSM dei frammenti di contenuto con l’editor Rich Text è stata corretta.
* L&#39;evidenziazione delle immagini in un&#39;immagine è ora supportata.

