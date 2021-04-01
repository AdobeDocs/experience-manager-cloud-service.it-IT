---
title: Come modificare o aggiungere metadati
description: Scopri i metadati delle risorse in [!DNL Experience Manager Assets] e vari modi per modificare i metadati delle risorse.
contentOwner: AG
feature: Metadati
role: Business Practices, Amministratore
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 9%

---


# Come modificare o aggiungere metadati {#how-to-edit-or-add-metadata}

I metadati sono informazioni aggiuntive sulla risorsa ricercabile. Viene estratto automaticamente quando carichi un’immagine. È possibile modificare i metadati esistenti o aggiungere nuove proprietà di metadati ai campi esistenti (ad esempio, quando un campo di metadati è vuoto).

Poiché le aziende hanno bisogno di vocabolari di metadati controllati e affidabili, [!DNL Experience Manager Assets] non consente l&#39;aggiunta ad hoc di nuove proprietà di metadati. Anche se gli autori non possono aggiungere nuovi campi di metadati per le risorse, gli sviluppatori possono farlo. Consulta [Creazione di una nuova proprietà di metadati per le risorse](meta-edit.md#editing-metadata-schema).

## Modifica dei metadati di una risorsa {#editing-metadata-for-an-asset}

Per modificare i metadati:

1. Effettua una delle operazioni seguenti:

   * Dall’interfaccia utente Assets, seleziona la risorsa e tocca o fai clic sull’icona **[!UICONTROL Visualizza proprietà]** nella barra degli strumenti.
   * Dalla miniatura della risorsa, seleziona l’azione rapida **[!UICONTROL Visualizza proprietà]** .
   * Dalla pagina della risorsa, tocca o fai clic su **[!UICONTROL Visualizza proprietà]** nella barra degli strumenti.

   Nella pagina della risorsa vengono visualizzati tutti i metadati della risorsa. Questi metadati sono stati estratti automaticamente al momento del caricamento (acquisizione) in AEM Assets.

1. Apporta le modifiche necessarie ai metadati delle varie schede e, al termine, per salvarle tocca o fai clic su **[!UICONTROL Salva]** nella barra degli strumenti. Tocca o fai clic su **[!UICONTROL Chiudi]** per tornare all’interfaccia web Assets.

   >[!NOTE]
   >
   >Se un campo di testo è vuoto, non sono presenti metadati esistenti. È possibile immettere un valore nel campo e salvarlo per aggiungere tale proprietà di metadati.

Qualsiasi modifica ai metadati di una risorsa viene riscritta nel binario originale come parte dei suoi dati XMP. Questo avviene tramite AEM flusso di lavoro di write-back dei metadati. Le modifiche apportate alle proprietà esistenti (ad esempio `dc:title`) vengono sovrascritte e le proprietà appena create (comprese le proprietà personalizzate come `cq:tags`) vengono aggiunte insieme allo schema.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Modifica dello schema metadati {#editing-metadata-schema}

Per informazioni dettagliate su come modificare lo schema dei metadati, vedere [Modifica dei moduli dello schema dei metadati](metadata-schemas.md#edit-metadata-schema-forms).

## Registrazione di uno spazio dei nomi personalizzato in AEM {#registering-a-custom-namespace-within-aem}

Puoi aggiungere i tuoi namespace all’interno di AEM. Come ci sono spazi dei nomi predefiniti come cq, jcr e sling, puoi avere uno spazio dei nomi per i metadati del tuo archivio e l&#39;elaborazione xml.

1. Vai alla pagina di amministrazione del tipo di nodo *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. Tocca o fai clic su **[!UICONTROL Namespace]** nella parte superiore della pagina. La pagina di amministrazione dello spazio dei nomi viene visualizzata in una finestra.

1. Per aggiungere uno spazio dei nomi, tocca o fai clic su **[!UICONTROL Nuovo]** in basso.
1. Specifica uno spazio dei nomi personalizzato nella convenzione dello spazio dei nomi XML (specifica l’id sotto forma di URI e un prefisso associato per l’id), quindi tocca o fai clic su **[!UICONTROL Salva]**.
