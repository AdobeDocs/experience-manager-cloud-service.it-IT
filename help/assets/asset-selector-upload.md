---
title: Selettore risorse per [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service]
description: Utilizza il selettore delle risorse per cercare, trovare e recuperare i metadati e le rappresentazioni delle risorse all’interno dell’applicazione.
role: Admin,User
exl-id: d6ff601c-3111-421a-9a94-cc524ce7e432
source-git-commit: f9f5b2a25933e059cceacf2ba69e23d528858d4b
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 1%

---

# Caricare file e cartelle in Asset Selector {#upload-files-folders}

Puoi caricare file o cartelle in Asset Selector dal file system locale. Per caricare i file utilizzando il file system locale, in genere è necessario utilizzare una funzione di caricamento fornita da una micro applicazione front-end Asset Selector.

## Carica risorse dal file system locale {#basic-upload}

Per aggiungere risorse a Selettore risorse, effettua le seguenti operazioni:

1. Se utilizzi la visualizzazione della barra, passa ai puntini di sospensione e fai clic sull&#39;icona ![carica](assets/upload-icon.svg) **[!UICONTROL Carica]**. D&#39;altra parte, fai clic sull&#39;icona ![carica](assets/upload-icon.svg) **[!UICONTROL Carica]** in alto a destra in caso di visualizzazione modale. Viene visualizzata la schermata [!UICONTROL Carica Assets].

   ![Carica risorse nel selettore risorse](assets/upload-assets.png)

   Inoltre, nella sezione **[!UICONTROL Trascina qui i file o le cartelle]**, puoi trascinare le risorse dal file system locale o fare clic su **[!UICONTROL Sfoglia]** per selezionare manualmente i file o le cartelle disponibili nel file system locale. Questo elenco di file che fanno parte del caricamento è disponibile come elenco.

   ![Carica risorse di base in Asset Selector](assets/basic-upload.png)

   È inoltre possibile visualizzare in anteprima le immagini selezionate utilizzando le miniature e fare clic sull&#39;icona X per rimuovere una particolare immagine dall&#39;elenco. L’icona X viene visualizzata solo quando passi il cursore del mouse sul nome o sulle dimensioni dell’immagine. Puoi anche fare clic su **[!UICONTROL Rimuovi tutti]** per eliminare tutti gli elementi dall&#39;elenco di caricamento.

1. Per completare il processo di caricamento, fare clic su **[!UICONTROL Carica]**. Vengono visualizzate le risorse caricate. Vedi [caricamento di base](/help/assets/asset-selector-customization.md#basic-upload) per il codice configurabile.

## Caricare risorse con metadati {#upload-assets-with-metadata}

Puoi aggiungere metadati alle risorse mentre le carichi immediatamente nell’applicazione. I metadati includono vari campi, ad esempio l’oggetto dell’azienda, i dettagli del prodotto, la campagna e così via. A tale scopo, viene utilizzata la proprietà `metadataSchema`. Vai a [proprietà del selettore risorse](/help/assets/asset-selector-properties.md) per ulteriori informazioni sulla proprietà `metadataSchema`.

Vedi [carica con metadati](/help/assets/asset-selector-customization.md#upload-with-metadata) per lo snippet di codice necessario per la configurazione.

![carica risorse con metadati](assets/upload-with-metadata.png)

1. Definisci il nome per il caricamento utilizzando il campo **[!UICONTROL Nome campagna]**. Puoi usare un nome esistente o crearne uno nuovo. Il Selettore risorse offre più opzioni quando si digita il nome.

   Come best practice, l’Adobe consiglia di specificare i valori negli altri campi e di migliorare l’esperienza di ricerca delle risorse caricate.

1. Definisci allo stesso modo i valori per i campi **[!UICONTROL Parole chiave]**, **[!UICONTROL Canali]**, **[!UICONTROL Intervallo temporale]** e **[!UICONTROL Area]**. Assegnare tag e raggruppare le risorse per parole chiave, canali e posizione consente a tutti coloro che utilizzano il contenuto aziendale approvato di trovare tali risorse e mantenerle organizzate.

1. Fai clic su **[!UICONTROL Carica]** per caricare le risorse nel selettore risorse. [!UICONTROL Visualizza dettagli] viene visualizzata la casella di conferma. Fai clic su [!UICONTROL Continua].

1. Avvia il caricamento di Assets. Fai clic su [!UICONTROL Nuovo caricamento] per riavviare la procedura di caricamento. Fai clic su [!UICONTROL Fine] per completare il caricamento.


## Caricamento personalizzato {#customize-upload}

Asset Selector (Selettore risorse) consente di aggiungere un modulo di caricamento personalizzato. Sono disponibili diverse personalizzazioni. Ad esempio, la proprietà [hideUploadButton](/help/assets/asset-selector-properties.md) consente di nascondere il pulsante di caricamento visualizzato per impostazione predefinita nell&#39;applicazione. È invece possibile personalizzarlo per eseguire il rendering all’esterno dell’applicazione MFE in base al requisito. Consulta [caricamento personalizzato](/help/assets/asset-selector-customization.md#customized-upload) per la configurazione.

![Caricamento personalizzato](assets/customized-upload.png)
