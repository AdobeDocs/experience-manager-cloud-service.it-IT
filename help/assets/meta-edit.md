---
title: Come modificare o aggiungere metadati
description: Scopri i metadati delle risorse in [!DNL Experience Manager Assets] e vari modi per modificare i metadati delle risorse.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 12%

---

# Come modificare o aggiungere metadati {#how-to-edit-or-add-metadata}

I metadati sono informazioni aggiuntive sulla risorsa in cui è possibile eseguire ricerche. Viene estratto automaticamente quando carichi un’immagine. Puoi modificare i metadati esistenti o aggiungere nuove proprietà di metadati ai campi esistenti (ad esempio, quando un campo di metadati è vuoto).

Poiché le aziende necessitano di vocabolari di metadati controllati e affidabili, [!DNL Experience Manager Assets] non consente l’aggiunta ad hoc di nuove proprietà di metadati. Anche se gli autori non possono aggiungere nuovi campi di metadati per le risorse, gli sviluppatori possono. Consulta [Creazione di una nuova proprietà di metadati per le risorse](meta-edit.md#editing-metadata-schema).

## Modifica dei metadati di una risorsa {#editing-metadata-for-an-asset}

Per modificare i metadati:

1. Effettua una delle operazioni seguenti:

   * Dall’interfaccia utente Assets, seleziona la risorsa e tocca o fai clic sul pulsante **[!UICONTROL Visualizza proprietà]** dalla barra degli strumenti.
   * Dalla miniatura della risorsa, seleziona la **[!UICONTROL Visualizza proprietà]** azione rapida.
   * Dalla pagina della risorsa, tocca o fai clic su **[!UICONTROL Visualizza proprietà]** dalla barra degli strumenti.

   Nella pagina delle risorse vengono visualizzati tutti i metadati della risorsa. Questi metadati venivano estratti automaticamente quando venivano caricati (acquisiti) in Experience Manager Assets.

1. Apporta le modifiche necessarie ai metadati delle varie schede e, al termine, per salvarle tocca o fai clic su **[!UICONTROL Salva]** nella barra degli strumenti. Tocca o fai clic su **[!UICONTROL Chiudi]** per tornare all’interfaccia web Assets.

   >[!NOTE]
   >
   >Se un campo di testo è vuoto, non è presente alcun set di metadati. Puoi immettere un valore nel campo e salvarlo per aggiungere tale proprietà di metadati.

Eventuali modifiche ai metadati di una risorsa vengono riscritte nel file binario originale come parte dei dati XMP. Questa operazione viene eseguita mediante un flusso di lavoro Experience Manager di reinserimento dei metadati. Modifiche apportate alle proprietà esistenti (ad esempio `dc:title`) vengono sovrascritti e le nuove proprietà create (incluse le proprietà personalizzate come `cq:tags`) vengono aggiunti insieme allo schema.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Modifica dello schema metadati {#editing-metadata-schema}

Per informazioni dettagliate su come modificare lo schema metadati, consulta [Modifica dei moduli schema metadati](metadata-schemas.md#edit-metadata-schema-forms).

## Registrazione di uno spazio dei nomi personalizzato in Experience Manager {#registering-a-custom-namespace-within-aem}

In Experience Manager puoi aggiungere spazi dei nomi personalizzati. Proprio come ci sono spazi dei nomi predefiniti come cq, jcr e sling, puoi avere uno spazio dei nomi per i metadati dell’archivio e l’elaborazione xml.

1. Vai alla pagina di amministrazione del tipo di nodo *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. Tocca o fai clic su **[!UICONTROL Namespace]** nella parte superiore della pagina. La pagina di amministrazione dello spazio dei nomi viene visualizzata in una finestra.

1. Per aggiungere uno spazio dei nomi, tocca o fai clic su **[!UICONTROL Nuovo]** in basso.
1. Specifica uno spazio dei nomi personalizzato nella convenzione dello spazio dei nomi XML (specifica l’ID sotto forma di URI e di un prefisso associato per l’ID), quindi tocca o fai clic su **[!UICONTROL Salva]**.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati da Assets](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
