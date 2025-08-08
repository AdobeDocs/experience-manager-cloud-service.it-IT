---
title: Come integrare il modello dati del modulo (FDM) per un modulo con il modulo adattivo?
description: Scopri come creare moduli basati su un modello dati modulo (FDM). Genera e modifica dati di esempio per gli oggetti del modello dati nel modello dati modulo (FDM).
feature: Edge Delivery Services, Adaptive Forms, Form Data Model
role: Admin, User
source-git-commit: 87650caea6eb907093f0f327f1dbc19641098e4a
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 19%

---

# Integrare i moduli con il modello dati del modulo

L’integrazione dei moduli con un modello dati modulo (FDM) consente di utilizzare diverse origini dati back-end per creare un modello dati modulo (FDM). Puoi utilizzare il modello dati modulo (FDM) come schema in vari flussi di lavoro di moduli. Configura le origini dati e crea un modello dati modulo (FDM) basato sugli oggetti e i servizi del modello dati disponibili nelle origini dati.

## Vantaggi dell’integrazione di Forms con Form Data Model (FDM)

* **Connettività back-end perfetta**: consente di connettere i moduli a vari sistemi back-end (ad esempio database, API REST, servizi SOAP, CRM) senza codice personalizzato. Ciò consente lo scambio di dati in tempo reale e riduce lo sforzo di integrazione.
* **Schema dati centralizzato** Il modello dati modulo funge da schema dati unificato che semplifica la mappatura e la gestione di oggetti dati e servizi utilizzati in più moduli e flussi di lavoro.

* **Precompilazione e invio modulo migliorati**: configura facilmente le azioni di precompilazione e invio tramite i servizi dati modulo, garantendo il recupero e l&#39;archiviazione accurati e aggiornati dei dati.

* **Supporto per flussi di lavoro dinamici**: il modello dati del modulo può essere integrato con i flussi di lavoro per automatizzare i processi aziendali in base ai dati inviati o recuperati, migliorando l&#39;efficienza complessiva.

## Prerequisiti

Prima di configurare il modulo con il modello dati modulo, assicurati di aver completato i seguenti passaggi:

* [Configura origini dati](/help/forms/configure-data-sources.md): configura l’origine dati per connettere il modulo ai dati di back-end.
* [Crea modello dati modulo (FDM)](/help/forms/create-form-data-models.md): crea un modello dati utilizzando oggetti dati e servizi dall’origine dati configurata.
* [Configura oggetti e servizi del modello dati](/help/forms/work-with-form-data-model.md): mappa gli oggetti e i servizi del modello dati per garantire un flusso di dati uniforme tra il modulo e l’origine dati.

>[!BEGINTABS]

>[!TAB Componente di base]

Per configurare il modello dati modulo con modulo adattivo basato su componente base, effettua le seguenti operazioni:

1. Apri il modulo adattivo per la modifica e passa alla sezione **[!UICONTROL Invio]** delle proprietà Contenitore modulo adattivo.
1. Dall&#39;elenco a discesa **[!UICONTROL Azione invio]**, selezionare **[!UICONTROL Invia utilizzando il modello dati modulo]**.

   ![invia tramite il modello dati modulo](/help/forms/assets/submit-uisng-fdm-fc.png)

1. Seleziona il **[!UICONTROL Modello dati creato per inviare]** la configurazione.
Per inviare allegati al database, selezionare **Invia allegati modulo**. Il documento di record (DoR) viene salvato nel database selezionando **Invia documento di record**.
1. Fai clic su **[!UICONTROL Salva]** per salvare le impostazioni di invio.

>[!TAB Componente core]

Per configurare il modello dati modulo con modulo adattivo basato su componente core, effettua le seguenti operazioni:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fare clic sulla scheda **[!UICONTROL Invio]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Azione invio]**, selezionare **[Invia utilizzando il modello dati modulo]**.
   ![invia tramite il modello dati modulo](/help/forms/assets/submit-uisng-fdm-cc.png)

1. Seleziona il **[!UICONTROL Modello dati creato per inviare]** la configurazione.
Per inviare allegati al database, selezionare **Invia allegati modulo**. Il documento di record (DoR) viene salvato nel database selezionando **Invia documento di record**.
1. Fai clic su **[!UICONTROL Salva]** per salvare le impostazioni di invio.

>[!TAB Editor universale]

Per configurare il modello dati modulo con un modulo adattivo creato in universale come, effettua le seguenti operazioni:

1. Apri il modulo adattivo per la modifica.
1. Fai clic sull&#39;estensione **Modifica proprietà modulo** nell&#39;editor.

   Viene visualizzata la finestra di dialogo **Proprietà modulo**.

   >[!NOTE]
   >
   > * Se l&#39;icona **Modifica proprietà modulo** non è visibile nell&#39;interfaccia di Universal Editor, abilitare l&#39;estensione **Modifica proprietà modulo** in Extension Manager.
   > * Per informazioni su come abilitare o disabilitare le estensioni nell&#39;editor universale, consulta l&#39;articolo [Caratteristiche principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

1. Fai clic sulla scheda **Invio** e seleziona **[!UICONTROL Invia utilizzando il modello dati del modulo]**.

   ![GIF OneDrive](/help/forms/assets/submit-uisng-fdm-ue.png)
Se si seleziona **Salva allegati con nome originale**, gli allegati vengono archiviati nella cartella utilizzando i nomi di file originali. Puoi anche salvare il documento di record (DoR) nell’archiviazione BLOB di Azure.

1. Selezionare la **[!UICONTROL configurazione archiviazione]**, in cui si desidera salvare i dati.
1. Fai clic su **[!UICONTROL Salva&amp;Chiudi]**

Per istruzioni dettagliate su come integrare i moduli creati nell&#39;editor universale, fare riferimento all&#39;articolo [Integrare Forms con Form Data Model nell&#39;editor universale](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

>[!ENDTABS]

## Articoli correlati

{{af-submit-action}}
