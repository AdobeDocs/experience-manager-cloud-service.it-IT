---
title: Metadati a cascata
description: Questo articolo descrive come definire i metadati a catena per le risorse.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 1d3ad496-a964-476e-b1da-4aa6d8ad53b7
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 8%

---

# Metadati a catena {#cascading-metadata}

Quando acquisiscono le informazioni sui metadati di una risorsa, gli utenti forniscono informazioni nei vari campi disponibili. Puoi visualizzare campi di metadati specifici o valori di campo che dipendono dalle opzioni selezionate negli altri campi. Tale visualizzazione condizionale dei metadati è denominata metadati a catena. In altre parole, è possibile creare una dipendenza tra un particolare campo/valore di metadati e uno o più campi e/o i relativi valori.

Utilizza gli schemi di metadati per definire regole per la visualizzazione dei metadati a catena. Ad esempio, se lo schema di metadati include un campo del tipo di risorsa, puoi definire un set di campi pertinente da visualizzare in base al tipo di risorsa selezionata da un utente.

Di seguito sono riportati alcuni casi d’uso per i quali è possibile definire i metadati a catena:

* Se è richiesta la posizione dell&#39;utente, visualizzare i nomi delle città pertinenti in base alla scelta del paese e dello stato dell&#39;utente.
* Carica i nomi di marchi pertinenti in un elenco in base alla categoria di prodotto scelta dall’utente.
* Attiva/disattiva la visibilità di un particolare campo in base al valore specificato in un altro campo. Ad esempio, se l’utente desidera che la spedizione venga consegnata a un indirizzo diverso, visualizza i campi dell’indirizzo di spedizione separato.
* Imposta un campo come obbligatorio in base al valore specificato in un altro campo.
* Modifica le opzioni visualizzate per un particolare campo in base al valore specificato in un altro campo.
* Imposta il valore di metadati predefinito in un particolare campo in base al valore specificato in un altro campo.

## Configurare i metadati a catena in [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

Considera uno scenario in cui desideri visualizzare i metadati a catena in base al tipo di risorsa selezionata. Alcuni esempi

* Per un video, visualizza i campi applicabili come formato, codec, durata e così via.
* Per un documento Word o PDF, visualizzare i campi, ad esempio il conteggio delle pagine, l&#39;autore e così via.

Indipendentemente dal tipo di risorsa scelto, visualizza le informazioni sul copyright come campo obbligatorio.

1. Seleziona la [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.
1. In **[!UICONTROL Schema Forms]** , selezionare un modulo schema, quindi selezionare **[!UICONTROL Modifica]** dalla barra degli strumenti per modificare lo schema.

   ![select_form](assets/select_form.png)

1. (Facoltativo) Nell’editor schema metadati, crea un campo da condizionare. Specifica un nome e un percorso di proprietà nel **[!UICONTROL Impostazioni]** scheda.

   Per creare una scheda, seleziona `+` per aggiungere una scheda e quindi un campo di metadati.

   ![add_tab](assets/add_tab.png)

1. Aggiungi un campo a discesa per il tipo di risorsa. Specifica un nome e un percorso di proprietà nel **[!UICONTROL Impostazioni]** scheda. Aggiungi una descrizione facoltativa.

   ![asset_type_field](assets/asset_type_field.png)

1. Le coppie chiave-valori sono le opzioni fornite a un utente del modulo. Puoi fornire le coppie chiave-valore manualmente o da un file JSON.

   * Per specificare manualmente i valori, selezionare **[!UICONTROL Aggiungi manualmente]**, e seleziona **[!UICONTROL Aggiungi scelta]** e specifica il testo e il valore dell’opzione. Specifica ad esempio i tipi di risorse Video, PDF, Word e Image.

   * Per recuperare dinamicamente i valori da un file JSON, seleziona **[!UICONTROL Aggiungi tramite percorso JSON]** e fornisci il percorso del file JSON. [!DNL Experience Manager] recupera le coppie chiave-valore in tempo reale quando il modulo viene presentato all’utente.

   Entrambe le opzioni si escludono a vicenda. Non è possibile importare le opzioni da un file JSON e modificarle manualmente.

   ![aggiungi_scelta](assets/add_choice.png)

   >[!NOTE]
   >
   >Quando aggiungi un file JSON, le coppie chiave-valore non vengono visualizzate nell’editor schema metadati, ma sono disponibili nel modulo pubblicato.

   >[!NOTE]
   >
   >Quando si aggiungono le scelte, se si fa clic sul campo popup, l&#39;interfaccia risulta distorta e l&#39;icona di eliminazione delle scelte non funziona più. Fai clic sul menu a discesa solo dopo aver salvato le modifiche. Se riscontri questo problema, salva lo schema e aprilo nuovamente per continuare a modificare.

1. (Facoltativo) Aggiungi gli altri campi obbligatori. Ad esempio, formato, codec e durata per il video del tipo di risorsa.

   Allo stesso modo, aggiungi campi dipendenti per altri tipi di risorse. Ad esempio, aggiungi il conteggio delle pagine dei campi e crea le risorse del documento, come i file di PDF e Word.

   ![video_dependent_fields](assets/video_dependent_fields.png)

1. Per creare una dipendenza tra il campo del tipo di risorsa e altri campi, scegli il campo dipendente e apri **[!UICONTROL Regole]** scheda.

   ![select_dependentfield](assets/select_dependentfield.png)

1. Sotto **[!UICONTROL Requisito]**, scegli il **[!UICONTROL Obbligatorio, in base alla nuova regola]** opzione.
1. Seleziona **[!UICONTROL Aggiungi regola]** e scegli la **[!UICONTROL Tipo risorsa]** per creare una dipendenza. Scegli anche il valore del campo in cui creare la dipendenza. In questo caso, scegli **[!UICONTROL Video]**. Seleziona **[!UICONTROL Fine]** per salvare le modifiche.

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >Un elenco a discesa con valori predefiniti manualmente può essere utilizzato con le regole. I menu a discesa con il percorso JSON configurato non possono essere utilizzati con regole che utilizzano valori predefiniti per applicare le condizioni. Se i valori vengono caricati da JSON in fase di runtime, non è possibile applicare una regola predefinita.

1. In **[!UICONTROL Visibilità]**, scegli l’opzione **[!UICONTROL Visibile, in base alla nuova regola]**.

1. Seleziona **[!UICONTROL Aggiungi regola]** e scegli la **[!UICONTROL Tipo risorsa]** per creare una dipendenza. Scegli anche il valore del campo in cui creare la dipendenza. In questo caso, scegli **[!UICONTROL Video]**. Seleziona **[!UICONTROL Fine]** per salvare le modifiche.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!CAUTION]
   >
   >Per ripristinare i valori, seleziona un punto qualsiasi dell’interfaccia diverso dai valori. Se i valori vengono reimpostati, selezionare nuovamente i valori.

   >[!NOTE]
   >
   >Puoi applicare la condizione **[!UICONTROL Requisito]** e **[!UICONTROL Visibilità]**, pur lasciandole indipendenti tra di loro.

1. Allo stesso modo, crea una dipendenza tra il valore Video nel campo Tipo di risorsa e altri campi, come Codec e Durata.
1. Ripeti i passaggi per creare una dipendenza tra le risorse del documento (PDF e Word) nel [!UICONTROL Tipo risorsa] campi e campi quali [!UICONTROL Conteggio pagine] e [!UICONTROL Autore].
1. Fai clic su **[!UICONTROL Salva]**. Applica lo schema metadati a una cartella.

1. Passa alla cartella a cui hai applicato lo schema metadati e apri la pagina delle proprietà di una risorsa. A seconda della scelta effettuata nel campo Tipo di risorsa, vengono visualizzati i campi di metadati a cascata pertinenti.

   ![Metadati a cascata per risorsa video](assets/video_asset.png)
   *Figura: Metadati a cascata della risorsa video*

   ![Metadati a cascata per risorsa documento](assets/doc_type_fields.png)
   *Figura: Metadati a cascata per la risorsa documento*

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
