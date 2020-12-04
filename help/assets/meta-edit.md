---
title: Come modificare o aggiungere i metadati
description: Scopri i metadati delle risorse in  [!DNL Experience Manager Assets] vari modi per modificare i metadati delle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3207151a76c51637551907d15a34f1a6b7450d02
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 9%

---


# Come modificare o aggiungere metadati {#how-to-edit-or-add-metadata}

I metadati sono informazioni aggiuntive sulla risorsa ricercabile. Viene estratto automaticamente quando caricate un’immagine. Potete modificare i metadati esistenti o aggiungere nuove proprietà di metadati ai campi esistenti (ad esempio, quando un campo di metadati è vuoto).

Poiché le aziende necessitano di vocabolari di metadati controllati e affidabili, [!DNL Experience Manager Assets] non consente l&#39;aggiunta ad hoc di nuove proprietà di metadati. Sebbene gli autori non possano aggiungere nuovi campi di metadati per le risorse, gli sviluppatori possono farlo. Consultate [Creazione di nuove proprietà di metadati per risorse](meta-edit.md#editing-metadata-schema).

## Modifica dei metadati per una risorsa {#editing-metadata-for-an-asset}

Per modificare i metadati:

1. Effettua una delle operazioni seguenti:

   * Nell’interfaccia utente Risorse, seleziona la risorsa e tocca o fai clic sull’icona **[!UICONTROL Visualizza proprietà]** nella barra degli strumenti.
   * Dalla miniatura della risorsa, selezionate l&#39;azione rapida **[!UICONTROL Visualizza proprietà]**.
   * Dalla pagina della risorsa, tocca o fai clic su **[!UICONTROL Visualizza proprietà]** dalla barra degli strumenti.

   Nella pagina della risorsa vengono visualizzati tutti i metadati della risorsa. Questi metadati sono stati estratti automaticamente quando sono stati caricati (assimilati)  AEM Assets.

1. Apporta le modifiche necessarie ai metadati delle varie schede e, al termine, per salvarle tocca o fai clic su **[!UICONTROL Salva]** nella barra degli strumenti. Tocca o fai clic su **[!UICONTROL Chiudi]** per tornare all’interfaccia web Assets.

   >[!NOTE]
   >
   >Se un campo di testo è vuoto, non esiste alcun set di metadati. Potete immettere un valore nel campo e salvarlo per aggiungere la proprietà dei metadati.

Qualsiasi modifica ai metadati di una risorsa viene riscritta nel binario originale come parte dei dati XMP. Questo avviene tramite AEM flusso di lavoro di riscrittura dei metadati. Le modifiche apportate alle proprietà esistenti (ad esempio `dc:title`) vengono sovrascritte e le proprietà create di recente (comprese le proprietà personalizzate come `cq:tags`) vengono aggiunte insieme allo schema.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Modifica dello schema metadati {#editing-metadata-schema}

Per informazioni dettagliate su come modificare lo schema di metadati, vedere [Modifica dei moduli dello schema di metadati](metadata-schemas.md#edit-metadata-schema-forms).

## Registrazione di uno spazio dei nomi personalizzato all&#39;interno di AEM {#registering-a-custom-namespace-within-aem}

Potete aggiungere spazi dei nomi personalizzati all&#39;interno di AEM. Così come esistono spazi dei nomi predefiniti come cq, jcr e sling, potete avere uno spazio dei nomi per i metadati dell&#39;archivio e l&#39;elaborazione xml.

1. Vai alla pagina di amministrazione del tipo di nodo *https://&lt;host>:&lt;porta>/crx/explorer/nodetypes/index.jsp*.
1. Tocca o fai clic su **[!UICONTROL Spazi dei nomi]** nella parte superiore della pagina. La pagina di amministrazione dello spazio dei nomi viene visualizzata in una finestra.

1. Per aggiungere uno spazio nomi, fare clic o toccare **[!UICONTROL Nuovo]** in basso.
1. Specificate uno spazio dei nomi personalizzato nella convenzione dello spazio dei nomi XML (specificate l&#39;ID sotto forma di URI e un prefisso associato per l&#39;id), quindi fate clic o toccate **[!UICONTROL Salva]**.
