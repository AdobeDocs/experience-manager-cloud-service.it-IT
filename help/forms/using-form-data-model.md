---
title: Come si utilizza il modello dati del modulo?
description: Scopri come creare Forms adattivo e frammenti di moduli adattivi basati su un modello di dati del modulo. Approfondisci la generazione e la modifica di dati di esempio per gli oggetti modello dati nel modello dati del modulo. Puoi utilizzare questi dati per visualizzare in anteprima e testare Adaptive Forms.
feature: Form Data Model
role: User
level: Beginner, Intermediate
exl-id: 827ce457-6585-46fb-8e28-1d970a40d949
source-git-commit: a6e76d2b3650d57adafe543b2b694360e4bb4169
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 2%

---

# Utilizzare il modello di dati del modulo {#use-form-data-model}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/using-form-data-model.html) |
| AEM as a Cloud Service | Questo articolo |


![integrazione dei dati](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] l’integrazione dei dati consente di utilizzare diverse origini dati di back-end per creare un modello dati modulo da utilizzare come schema in vari Forms adattivi <!--and interactive communications--> flussi di lavoro. Richiede la configurazione delle origini dati e la creazione di un modello dati modulo basato su oggetti e servizi del modello dati disponibili nelle origini dati. Per ulteriori informazioni, consulta:

* [[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md)
* [Configurare origini dati](configure-data-sources.md)
* [Crea modello dati modulo](create-form-data-models.md)
* [Utilizzare il modello dati del modulo](work-with-form-data-model.md)

Un modello dati modulo è un’estensione dello schema JSON che puoi utilizzare per:

* [Creazione di Forms e frammenti adattivi](#create-af)
  <!--* [Create interactive communications and building blocks like text, list, and condition fragments](#create-ic)-->
* [Anteprima con dati di esempio](#preview-ic)
* [utilizzo del servizio Modello dati modulo](#prefill)
* [Riscrivere i dati del modulo adattivo inviati nelle origini dati](#write-af)
* [Richiama servizi tramite regole modulo adattivo](#invoke-services)

## Creazione di Forms e frammenti adattivi {#create-af}

Puoi creare [Forms adattivo](creating-adaptive-form.md) e frammenti di moduli adattivi <!-- [Adaptive Form Fragments](adaptive-form-fragments.md) --> basato su un modello dati modulo. Per utilizzare un modello di dati modulo durante la creazione di un modulo adattivo o di un frammento di modulo adattivo, effettua le seguenti operazioni:

1. Nella scheda Modello modulo della schermata Aggiungi proprietà, seleziona **[!UICONTROL Modello dati modulo]** nel **[!UICONTROL Seleziona da]** elenco a discesa.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Tocca per espandere **[!UICONTROL Seleziona modello dati modulo]**. Sono elencati tutti i modelli di dati dei moduli disponibili.

   Seleziona un dal modello dati.

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**Solo frammenti di moduli adattivi**) È possibile creare un frammento di modulo adattivo basato su un solo oggetto modello dati in un modello dati modulo. Espandi **[!UICONTROL Definizioni modello dati modulo]** a discesa. Elenca tutti gli oggetti modello dati nel modello dati del modulo specificato. Seleziona un oggetto modello dati dall’elenco.

   ![create-af-3](assets/create-af-3.png)

   Una volta creato il modulo adattivo o il frammento di modulo adattivo basato su un modello di dati del modulo, gli oggetti del modello di dati del modulo vengono visualizzati in **[!UICONTROL Origini dati]** del browser Contenuto nell’editor di moduli adattivi.

   >[!NOTE]
   >
   >Per un frammento di modulo adattivo, nella scheda Origini dati vengono visualizzati solo l’oggetto modello dati selezionato al momento dell’authoring e i relativi oggetti modello dati associati.

   ![data-model-objects-tab](assets/data-model-objects-tab.png)

   Per aggiungere campi modulo, puoi trascinare gli oggetti modello dati nel modulo adattivo o nel frammento. I campi modulo aggiunti mantengono le proprietà dei metadati e l’associazione con le proprietà dell’oggetto modello dati. L’associazione assicura che i valori dei campi vengano aggiornati nelle origini dati corrispondenti all’invio del modulo e precompilati al momento del rendering del modulo.

<!-- ## Create interactive communications {#create-ic}

You can create an interactive communication based on a Form Data Model that you can use to prefill interactive communication with data from configured data sources. In addition, the building blocks of an interactive communication, such as text, list, and condition document fragments can be based on a form data model.

You can choose a Form Data Model when creating an interactive communication or a document fragment. The following image shows the General tab of the Create Interactive Communication dialog.

![create-ic](assets/create-ic.png)

General tab of Create Interactive Communication dialog

For more information, see:

[Create an interactive communication](create-interactive-communication.md)

[Text in Interactive Communications](texts-interactive-communications.md)

[Conditions in Interactive Communications](conditions-interactive-communications.md)

[List fragments](lists.md) -->

## Anteprima con dati di esempio {#preview-ic}

L’editor modello dati modulo consente di generare e modificare dati di esempio per gli oggetti modello dati nel modello dati modulo. Puoi utilizzare questi dati per visualizzare in anteprima e testare <!--interactive communications and--> Forms adattivo. Prima di visualizzare l&#39;anteprima dovete generare i dati di esempio come descritto in [Utilizzare il modello dati del modulo](work-with-form-data-model.md#sample).

<!--To preview an interactive communication with sample Form Data Model data:

1. On [!DNL  Experience Manager] author instance, navigate to **[!UICONTROL Forms > Forms & Documents]**.
1. Select an interactive communication and tap **[!UICONTROL Preview]** in the toolbar to select **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, or **[!UICONTROL Both Channels]** to preview the interactive communication.
1. In the Preview [*channel*] dialog, ensure that **[!UICONTROL Test Data of Form Data Model]** is selected and tap **[!UICONTROL Preview]**.

The interactive communication opens with prefilled sample data.

![web-preview](assets/web-preview.png)-->

Per visualizzare in anteprima un modulo adattivo con dati di esempio, apri il modulo adattivo in modalità di creazione e tocca **[!UICONTROL Anteprima]**.

## Precompilare utilizzando il servizio Modello dati modulo {#prefill}

[!DNL Experience Manager Forms] fornisce il servizio predefinito Modello dati modulo che puoi abilitare per Forms adattivo <!--and interactive communications--> in base al modello dati del modulo. Il servizio di precompilazione interroga le origini dati per gli oggetti modello dati nel modulo adattivo <!--and interactive communication--> di conseguenza, esegue la precompilazione dei dati durante il rendering del modulo o della comunicazione.

Per abilitare il servizio di precompilazione del modello dati modulo per un modulo adattivo, apri le proprietà Contenitore modulo adattivo e seleziona **[!UICONTROL Servizio di precompilazione modello dati modulo]** dal **[!UICONTROL Servizio preriempimento]** nel pannello a soffietto Base. Quindi, salva le proprietà.

![preriempimento-servizio](assets/prefill-service.png)

<!--To configure Form Data Model prefill service in an interactive communication, you can select Form Data Model Prefill Service in the Prefill Service drop-down while creating it or later by modifying the properties.

![edit-ic-props](assets/edit-ic-props.png)

Edit Properties dialog for an interactive communication-->

## Scrivere i dati del modulo adattivo inviati nelle origini dati {#write-af}

Quando un utente invia un modulo basato su un modello dati del modulo, è possibile configurare il modulo in modo che scriva i dati inviati per un oggetto modello dati nelle relative origini dati. Per ottenere questo caso d’uso, [!DNL Experience Manager Forms] fornire [Azione di invio modello dati modulo](configuring-submit-actions.md), disponibile solo come standard per Adaptive Forms basato su un modello di dati per moduli. Scrive i dati inviati per un oggetto modello dati nella relativa origine dati.

Per configurare l’azione di invio Modello dati modulo, apri le proprietà Contenitore modulo adattivo e seleziona **[!UICONTROL Invia utilizzando il modello dati modulo]** dal menu a discesa Azione di invio nel pannello a soffietto Invio. Quindi, sfoglia e seleziona un oggetto modello dati dal menu **[!UICONTROL Nome dell’oggetto modello dati da inviare]** a discesa. Salva le proprietà.

All’invio del modulo, i dati per l’oggetto modello dati configurato vengono scritti nella rispettiva origine dati.

<!--![data-submission](assets/data-submission.png)-->

È inoltre possibile inviare gli allegati del modulo a un&#39;origine dati utilizzando la proprietà dell&#39;oggetto modello dati binario. Per inviare allegati a un&#39;origine dati JDBC, effettuare le seguenti operazioni:

1. Aggiungi al modello dati del modulo un oggetto modello dati che include una proprietà binaria.
1. Nel modulo adattivo, trascina **[!UICONTROL File allegato]** dal browser Componenti al modulo adattivo.
1. Tocca per selezionare il componente aggiunto e tocca ![icona_impostazioni](assets/configure-icon.svg) per aprire il browser Proprietà del componente.
1. Nel campo Associa riferimento, tocca ![foldersearch_18](assets/folder-search-icon.svg) e passa alla selezione della proprietà binaria aggiunta nel modello dati del modulo. Configura altre proprietà, a seconda delle necessità.

   Tocca ![pulsante di controllo](assets/save_icon.svg) per salvare le proprietà. Il campo allegato è ora associato alla proprietà binaria del modello dati del modulo.

1. Nella sezione Invio delle proprietà Contenitore modulo adattivo, abilita **[!UICONTROL Invia allegati modulo]**. Invia l’allegato nel campo della proprietà binaria all’origine dati al momento dell’invio del modulo.

## Richiama servizi in Adaptive Forms utilizzando le regole {#invoke-services}

In un modulo adattivo basato su un modello di dati del modulo è possibile: [creare regole](rule-editor.md) per richiamare i servizi configurati nel modello dati del modulo. Il **[!UICONTROL Richiama servizi]** L’operazione in una regola elenca tutti i servizi disponibili nel modello dati modulo e consente di selezionare i campi di input e output per il servizio. È inoltre possibile utilizzare **[!UICONTROL Imposta valore]** tipo di regola per richiamare un servizio Modello dati modulo e impostare il valore di un campo sull&#39;output restituito dal servizio.

Ad esempio, la regola seguente richiama un servizio get che utilizza come input l&#39;ID dipendente e i valori restituiti vengono inseriti nei campi ID dipendente, Cognome, Nome e Genere corrispondenti nel modulo.

![invoke-service](assets/invoke-service.png)

Inoltre, è possibile utilizzare `guidelib.dataIntegrationUtils.executeOperation` API per scrivere un JavaScript nell’editor di codice per l’editor di regole. <!-- For API details, see [API to invoke Form Data Model service](invoke-form-data-model-services.md).-->

### Richiama un modello di dati modulo utilizzando funzioni personalizzate {#invoke-form-data-model-using-custom-functions}

È possibile [richiamare un modello di dati modulo dall’editor di regole utilizzando funzioni personalizzate](/help/forms/rule-editor.md#custom-functions-in-rule-editor-custom-functions). Per richiamare il modello dati del modulo, aggiungi un modello dati del modulo al inserisco nell&#39;elenco Consentiti di. Per aggiungere un modello dati modulo a un elenco Consentiti:

1. Vai alla console web di Experience Manager all’indirizzo `https://server:host/system/console/configMgr`.
1. Individua **[!UICONTROL Inserimento in whitelist a livello di modulo adattivo del modello dati del modulo per chiamata di servizio - Configuration Factory]**.
1. Clic ![icona più](/help/forms/assets/Smock_Add_18_N.svg) per aggiungere la configurazione.
1. Aggiungi **[!UICONTROL Schema percorso contenuto]** per specificare la posizione del Forms adattivo.  Per impostazione predefinita, il valore è `/content/forms/af/(.*)` che include tutti i Forms adattivi. Puoi anche specificare il percorso per un modulo adattivo specifico.
1. Aggiungi **[!UICONTROL Pattern percorso modello dati modulo]** per specificare il percorso del modello dati del modulo. Per impostazione predefinita, il valore è `/content/dams/formsanddocuments-fdm/(.*)` che include tutto il modello dati del modulo. È inoltre possibile specificare il percorso per un modello dati modulo specifico.
1. Salva le impostazioni.

La configurazione aggiunta viene salvata in **[!UICONTROL Inserimento in whitelist a livello di modulo adattivo del modello dati del modulo per chiamata di servizio - Configuration Factory]** opzione.

>[!VIDEO](https://video.tv.adobe.com/v/3423977/adaptive-forms-custom-function-rule-editor)

>[!NOTE]
>
> Per richiamare un modello di dati modulo dall’editor di regole utilizzando funzioni personalizzate tramite un progetto di archetipo AEM:
>
>1. [Creare un file di configurazione](https://github.com/adobe/aem-core-forms-components/blob/master/it/config/src/main/content/jcr_root/apps/system/config/com.adobe.aemds.guide.factory.impl.AdaptiveFormFDMConfigurationFactoryImpl~core-components-it.cfg.json).
>1. Imposta le proprietà di getContentPathPattern e getFormDataModelPathPattern.
>1. Distribuisci il progetto.
