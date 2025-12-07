---
title: Migliorare l’individuazione dei contenuti con i metadati generati dall’intelligenza artificiale in visualizzazione Amministratore
description: Scopri come migliorare l’individuazione dei contenuti con i metadati generati dall’intelligenza artificiale in Admin View
feature: Smart Tags,Tagging
role: Admin,User
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 10%

---


# Miglioramento dell’individuazione dei contenuti con metadati generati dall’intelligenza artificiale {#ai-smart-tags}

| Interfaccia utente | Collegamento articolo |
| -------- | ---------------------------- |
| Vista risorse | [Fai clic qui](/help/assets/ai-generated-metadata-assets-view.md) |
| Visualizzazione amministratore | Questo articolo |

Invece di fare affidamento sull’input manuale, l’intelligenza artificiale assegna automaticamente tag descrittivi alle risorse digitali. Questi tag generati dall’IA migliorano la qualità dei metadati, rendendo le risorse più facili da cercare, classificare e consigliare. Questo approccio non solo migliora l’efficienza eliminando l’assegnazione tag manuale, ma garantisce anche coerenza e scalabilità su grandi volumi di contenuti digitali. Ad esempio, se la risorsa è un’immagine, l’intelligenza artificiale è in grado di identificare oggetti, scene, emozioni o anche loghi del brand al suo interno e generare tag rilevanti come &quot;tramonto&quot;, &quot;spiaggia&quot;, &quot;vacanza&quot; o &quot;sorriso&quot;. I contenuti generati dall’intelligenza artificiale possono migliorare la ricerca delle risorse sfruttando tecniche di ricerca sia semantiche che lessicali. Ulteriori informazioni su [Cerca in Assets](search-assets.md). <!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![Tag avanzati migliorati](assets/enhanced-smart-tags1.png)

## Come si abilitano i metadati generati dall’intelligenza artificiale? {#enable-ai-generated-metadata}

Per abilitare i metadati generati dall’intelligenza artificiale:

* La versione minima richiesta di AEM è `20626`.

## Configurare titoli generati dall’intelligenza artificiale {#configure-ai-generated-titles}

AEM consente di configurare la visualizzazione dei titoli delle risorse nella vista a schede o nella vista a elenco della pagina Sfoglia risorse. Puoi scegliere di visualizzare il titolo della risorsa definito dall’utente, il titolo generato tramite IA o utilizzare il titolo generato tramite IA solo se non è presente alcun titolo per la risorsa.

Per configurare i titoli generati dall’intelligenza artificiale:

1. Passa a **[!UICONTROL Strumenti > Assets > Configurazioni Assets > Configurazione miglioramento smart tag]**.

1. Seleziona una delle opzioni seguenti:

   * **Visualizza titolo controller di dominio (predefinito)**: specifica il titolo nel campo **[!UICONTROL Titolo]** disponibile nelle proprietà della risorsa per visualizzarlo nella vista a schede o nella vista a elenco. Se il titolo della risorsa non è definito, AEM Assets visualizza il nome del file.

   * **Visualizza titolo generato dall&#39;intelligenza artificiale**: visualizza il titolo generato dall&#39;intelligenza artificiale e ignora il titolo specificato nelle proprietà della risorsa. Se per una risorsa non è disponibile il titolo generato dall’intelligenza artificiale, AEM Assets visualizza il titolo predefinito della risorsa disponibile nelle relative proprietà.

   * **Visualizza titolo generato dall&#39;intelligenza artificiale solo se il titolo del controller di dominio non esiste**: AEM Assets visualizza il titolo generato dall&#39;intelligenza artificiale solo se per una risorsa non è definito alcun titolo.

     ![Configurare titoli generati dall’IA](assets/configure-title-ai-generated.png)

## Utilizzo di metadati generati dall’intelligenza artificiale {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

Per utilizzare la funzione dei tag avanzati, esegui i seguenti passaggi:

1. Nell&#39;interfaccia [!DNL Experience Manager], passare alla cartella desiderata e fare clic su **[!UICONTROL Aggiungi Assets]**. <!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.--> I formati di file immagine compatibili sono `png`, `jpg`, `jpeg`,`psd`, `tiff`, `gif`, `webp`, `crw`, `cr2`, `3fr`, `nef`, `arw` e `bmp`.

1. Attendi che la nuova risorsa caricata venga elaborata. Al termine, vai a proprietà risorsa.

1. Passa alla scheda **[!UICONTROL Generato da IA]**. Se la versione di [!DNL Experience Manager] non è compatibile o non è aggiornata, la scheda non è visibile. Sono presenti i seguenti campi:

   * **[!UICONTROL Titolo generato]:** Il titolo fornisce un titolo chiaro e conciso che acquisisce l&#39;idea di base di una risorsa caricata, semplificandone la comprensione immediata. Quando aggiungi una risorsa, se fornisci un titolo (in `dc:title`), questo verrà visualizzato nella visualizzazione Sfoglia risorse. Se non specificato, viene assegnato automaticamente un titolo generato dall’intelligenza artificiale.
   * **[!UICONTROL Descrizione generata]:** La descrizione fornisce un riepilogo breve ma informativo di ciò che riguarda la risorsa, aiutando gli utenti e il modulo di ricerca a comprenderne rapidamente la rilevanza.
   * **[!UICONTROL Parole chiave generate]:** Le parole chiave sono termini di destinazione che rappresentano i temi principali di una risorsa, facilitando l&#39;assegnazione di tag e il filtraggio del contenuto.

1. [Facoltativo] Se ritieni che manchino dei tag rilevanti, puoi aggiungere altri tag o crearne di nuovi. A questo scopo, scrivi i tag nel campo **[!UICONTROL Parole chiave generate]** e fai clic su **[!UICONTROL Salva]**.

## Disattiva i metadati generati dall’intelligenza artificiale {#disable-ai-generated-metadata}

Per disabilitare i metadati generati dall’intelligenza artificiale:

1. Passa a **[!UICONTROL Strumenti > Assets > Configurazioni Assets > Configurazione miglioramento smart tag]**.

1. Selezionare **[!UICONTROL Disabilita miglioramenti smart tag]**.

1. Fai clic su **[!UICONTROL Salva]**.

I metadati generati dall’intelligenza artificiale sono disabilitati per le nuove risorse o cartelle caricate in AEM Assets. Le risorse o cartelle esistenti con campi di metadati generati dall’intelligenza artificiale continuano a visualizzare questi campi.