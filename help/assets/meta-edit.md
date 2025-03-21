---
title: Come modificare o aggiungere metadati
description: Scopri i metadati delle risorse in [!DNL Experience Manager Assets]  e vari modi con cui puoi modificare i metadati delle risorse.
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 12%

---

# Come modificare o aggiungere metadati {#how-to-edit-or-add-metadata}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

I metadati sono informazioni aggiuntive sulla risorsa in cui è possibile eseguire ricerche. Viene estratto automaticamente quando carichi un’immagine. Puoi modificare i metadati esistenti o aggiungere nuove proprietà di metadati ai campi esistenti (ad esempio, quando un campo di metadati è vuoto).

Poiché le aziende richiedono vocabolari di metadati controllati e affidabili, [!DNL Experience Manager Assets] non consente l&#39;aggiunta su richiesta di nuove proprietà di metadati. Anche se gli autori non possono aggiungere nuovi campi di metadati per le risorse, gli sviluppatori possono. Vedi [Creazione di una nuova proprietà metadati per Assets](meta-edit.md#editing-metadata-schema).

## Modifica dei metadati di una risorsa {#editing-metadata-for-an-asset}

Per modificare i metadati:

1. Effettua una delle seguenti operazioni:

   * Dall&#39;interfaccia utente di Assets, seleziona la risorsa e l&#39;icona **[!UICONTROL Visualizza proprietà]** dalla barra degli strumenti.
   * Dalla miniatura della risorsa, seleziona l&#39;azione rapida **[!UICONTROL Visualizza proprietà]**.
   * Dalla pagina della risorsa, seleziona **[!UICONTROL Visualizza proprietà]** dalla barra degli strumenti.

   Nella pagina della risorsa vengono visualizzati i relativi metadati. Questi metadati venivano estratti automaticamente quando venivano caricati (acquisiti) in Experience Manager Assets.

1. Apporta le modifiche necessarie ai metadati delle varie schede e, al termine, seleziona **[!UICONTROL Salva]** nella barra degli strumenti per salvare le modifiche. Seleziona **[!UICONTROL Chiudi]** per tornare all&#39;interfaccia Web di Assets.

   >[!NOTE]
   >
   >Se un campo di testo è vuoto, non è presente alcun set di metadati. Puoi immettere un valore nel campo e salvarlo per aggiungere tale proprietà di metadati.

Eventuali modifiche ai metadati di una risorsa vengono scritte nuovamente nel file binario originale come parte dei dati XMP. Questa operazione viene eseguita tramite il flusso di lavoro di reinserimento dei metadati di Experience Manager. Le modifiche apportate alle proprietà esistenti (ad esempio `dc:title`) vengono sovrascritte e le proprietà create (incluse le proprietà personalizzate come `cq:tags`) vengono aggiunte insieme allo schema.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Modifica dello schema metadati {#editing-metadata-schema}

Per informazioni dettagliate su come modificare lo schema metadati, vedere [Modifica dei moduli schema metadati](metadata-schemas.md#edit-metadata-schema-forms).

## Registrazione di uno spazio dei nomi personalizzato in Experience Manager {#registering-a-custom-namespace-within-aem}

Puoi aggiungere spazi dei nomi personalizzati in Experience Manager. Proprio come ci sono spazi dei nomi predefiniti come cq, jcr e sling, puoi avere uno spazio dei nomi per i metadati dell’archivio e l’elaborazione xml.

1. Vai alla pagina di amministrazione del tipo di nodo *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. Seleziona **[!UICONTROL Namespace]** nella parte superiore della pagina. La pagina di amministrazione dello spazio dei nomi viene visualizzata in una finestra.

1. Per aggiungere uno spazio dei nomi, seleziona **[!UICONTROL Nuovo]** in basso.
1. Specificare uno spazio dei nomi personalizzato nella convenzione dello spazio dei nomi XML (specificare l&#39;ID sotto forma di URI e un prefisso associato per l&#39;ID), quindi selezionare **[!UICONTROL Salva]**.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
