---
title: Migliorare l’individuazione dei contenuti con i metadati generati dall’intelligenza artificiale
description: Scopri come migliorare l’individuazione dei contenuti con i metadati generati dall’intelligenza artificiale
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 4%

---


# Migliorare l’individuazione dei contenuti con i metadati generati dall’intelligenza artificiale {#ai-smart-tags}

Invece di fare affidamento sull’input manuale, l’intelligenza artificiale assegna automaticamente tag descrittivi alle risorse digitali. Questi tag generati dall’IA migliorano la qualità dei metadati, rendendo le risorse più facili da cercare, classificare e consigliare. Questo approccio non solo migliora l’efficienza eliminando l’assegnazione tag manuale, ma garantisce anche coerenza e scalabilità su grandi volumi di contenuti digitali. Ad esempio, se la risorsa è un’immagine, l’intelligenza artificiale è in grado di identificare oggetti, scene, emozioni o anche loghi del brand al suo interno e generare tag rilevanti come &quot;tramonto&quot;, &quot;spiaggia&quot;, &quot;vacanza&quot; o &quot;sorriso&quot;. I contenuti generati dall’intelligenza artificiale possono migliorare la ricerca delle risorse sfruttando tecniche di ricerca sia semantiche che lessicali. Ulteriori informazioni su [Cerca in Assets](search-assets-view.md). <!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![Metadati generati da IA](/help/assets/assets/enhanced-smart-tags.png)

## Come si abilitano i metadati generati dall’intelligenza artificiale? {#enable-ai-generated-metadata}

Per abilitare i metadati generati dall’intelligenza artificiale:

* La versione minima richiesta di AEM è `20626`.


## Utilizzo di metadati generati da IA {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

Per utilizzare la funzione dei tag avanzati, esegui i seguenti passaggi:

1. Nell&#39;interfaccia [!DNL Experience Manager], passare alla cartella desiderata e fare clic su **[!UICONTROL Aggiungi Assets]**. <!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.--> I formati di file immagine compatibili sono `png`, `jpg`, `jpeg`,`psd`, `tiff`, `gif`, `webp`, `crw`, `cr2`, `3fr`, `nef`, `arw` e `bmp`.

1. Attendi che la nuova risorsa caricata venga elaborata. Al termine, vai ai dettagli della risorsa.

1. Passa alla scheda **[!UICONTROL Generato da IA]**. Se la versione di [!DNL Experience Manager] non è compatibile o non è aggiornata, la scheda non è visibile.  Sono presenti i seguenti campi:

   * **[!UICONTROL Titolo generato]:** Il titolo fornisce un titolo chiaro e conciso che acquisisce l&#39;idea di base di una risorsa caricata, semplificandone la comprensione immediata. Quando aggiungi una risorsa, se fornisci un titolo (in `dc:title`), questo verrà visualizzato nella visualizzazione Sfoglia risorse. Se non specificato, viene assegnato automaticamente un titolo generato dall’intelligenza artificiale.
   * **[!UICONTROL Descrizione generata]:** La descrizione fornisce un riepilogo breve ma informativo di ciò che riguarda la risorsa, aiutando gli utenti e il modulo di ricerca a comprenderne rapidamente la rilevanza.
   * **[!UICONTROL Parole chiave generate]:** Le parole chiave sono termini di destinazione che rappresentano i temi principali di una risorsa, facilitando l&#39;assegnazione di tag e il filtraggio del contenuto.

1. [Facoltativo] Se ritieni che manchino dei tag rilevanti, puoi aggiungere altri tag o crearne di nuovi. A questo scopo, scrivi i tag nel campo **[!UICONTROL Parole chiave generate]** e fai clic su **[!UICONTROL Salva]**.

Per informazioni su come disabilitare i metadati generati dall&#39;intelligenza artificiale, vedi [Disabilitare i metadati generati dall&#39;intelligenza artificiale](/help/assets/smart-tags.md#disable-ai-generated-metadata).
