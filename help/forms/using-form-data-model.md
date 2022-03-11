---
title: Come si utilizza il modello dati del modulo?
description: Scopri come creare frammenti di modulo adattivi e Forms basati su un modello di dati del modulo. Approfondisci la generazione e la modifica di dati di esempio per gli oggetti del modello dati nel modello dati del modulo. Puoi utilizzare questi dati per visualizzare in anteprima e testare Adaptive Forms.
feature: Form Data Model
role: User
level: Beginner, Intermediate
exl-id: 827ce457-6585-46fb-8e28-1d970a40d949
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 1%

---

# Utilizzare il modello di dati del modulo {#use-form-data-model}

![integrazione dei dati](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] l’integrazione dei dati consente di utilizzare origini dati back-end diverse per creare un modello dati modulo da utilizzare come schema in vari Forms adattivi <!--and interactive communications--> flussi di lavoro. Richiede la configurazione delle origini dati e la creazione di Form Data Model in base agli oggetti e ai servizi del modello dati disponibili nelle origini dati. Per ulteriori informazioni, consulta gli argomenti di seguito:

* [[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md)
* [Configurare origini dati](configure-data-sources.md)
* [Crea modello dati modulo](create-form-data-models.md)
* [Utilizzare il modello dati del modulo](work-with-form-data-model.md)

Un modello dati modulo è un’estensione dello schema JSON che può essere utilizzata per:

* [Creare frammenti e Forms adattivi](#create-af)

<!--* [Create interactive communications and building blocks like text, list, and condition fragments](#create-ic)-->
* [Anteprima con dati di esempio](#preview-ic)
* [utilizzo del servizio Form Data Model](#prefill)
* [Riscrittura dei dati del modulo adattivo inviati nelle origini dati](#write-af)
* [Richiamare i servizi utilizzando le regole del modulo adattivo](#invoke-services)

## Creare frammenti e Forms adattivi {#create-af}

Puoi creare [Forms adattivo](creating-adaptive-form.md) e frammenti di modulo adattivi <!-- [Adaptive Form Fragments](adaptive-form-fragments.md) --> basato su un modello dati del modulo. Per utilizzare un modello dati modulo durante la creazione di un modulo adattivo o di un frammento di modulo adattivo, effettuare le seguenti operazioni:

1. Nella scheda Modello modulo della schermata Aggiungi proprietà, selezionare **[!UICONTROL Modello dati modulo]** in **[!UICONTROL Seleziona da]** elenco a discesa.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Tocca per espandere **[!UICONTROL Seleziona modello dati modulo]**. Sono elencati tutti i modelli di dati modulo disponibili.

   Seleziona un modello dati da.

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**Solo frammenti di modulo adattivi**) È possibile creare un frammento di modulo adattivo basato su un solo oggetto modello dati all’interno di un modello dati modulo. Espandi **[!UICONTROL Definizioni dei modelli di dati del modulo]** a discesa. Elenca tutti gli oggetti del modello dati nel modello dati del modulo specificato. Selezionare un oggetto modello dati dall’elenco.

   ![create-af-3](assets/create-af-3.png)

   Una volta creato il modulo adattivo o il frammento di modulo adattivo basato su un modello dati modulo, gli oggetti del modello dati modulo vengono visualizzati nella **[!UICONTROL Origini dati]** della scheda del browser Contenuto nell’editor di moduli adattivi.

   >[!NOTE]
   >
   >Per un frammento di modulo adattivo, nella scheda Origini dati viene visualizzato solo l’oggetto modello dati selezionato al momento della creazione e gli oggetti modello dati associati.

   ![data-model-objects-tab](assets/data-model-objects-tab.png)

   È possibile trascinare gli oggetti modello dati sul modulo adattivo o sul frammento per aggiungere campi modulo. I campi modulo aggiunti mantengono le proprietà dei metadati e il binding con le proprietà dell’oggetto modello dati. Il binding assicura che i valori dei campi vengano aggiornati nelle origini dati corrispondenti all’invio del modulo e precompilati al momento del rendering del modulo.

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

L’editor per modelli dati modulo consente di generare e modificare dati di esempio per gli oggetti modello dati nel modello dati del modulo. Puoi utilizzare questi dati per visualizzare in anteprima e verificare <!--interactive communications and--> Forms adattivo. È necessario generare i dati di esempio prima di visualizzare l’anteprima come descritto in [Utilizzare il modello dati del modulo](work-with-form-data-model.md#sample).

<!--To preview an interactive communication with sample Form Data Model data:

1. On [!DNL  Experience Manager] author instance, navigate to **[!UICONTROL Forms > Forms & Documents]**.
1. Select an interactive communication and tap **[!UICONTROL Preview]** in the toolbar to select **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, or **[!UICONTROL Both Channels]** to preview the interactive communication.
1. In the Preview [*channel*] dialog, ensure that **[!UICONTROL Test Data of Form Data Model]** is selected and tap **[!UICONTROL Preview]**.

The interactive communication opens with prefilled sample data.

![web-preview](assets/web-preview.png)-->

Per visualizzare in anteprima un modulo adattivo con dati di esempio, apri il modulo adattivo in modalità di creazione e tocca **[!UICONTROL Anteprima]**.

## Precompilazione tramite il servizio Form Data Model {#prefill}

[!DNL Experience Manager Forms] fornisce il servizio di precompilazione del modello di dati del modulo pronto all’uso che è possibile abilitare per l’Adaptive Forms <!--and interactive communications--> basato sul modello dati del modulo. Il servizio di precompilazione richiede le origini dati per gli oggetti del modello dati nel modulo adattivo <!--and interactive communication--> esegue quindi la precompilazione dei dati durante il rendering del modulo o della comunicazione.

Per abilitare il servizio di precompilazione del modello di dati del modulo per un modulo adattivo, apri le proprietà del contenitore del modulo adattivo e seleziona **[!UICONTROL Servizio di precompilazione modello dati modulo]** dal **[!UICONTROL Servizio di precompilazione]** a discesa nel pannello a soffietto Base. Quindi, salva le proprietà.

![servizio di precompilazione](assets/prefill-service.png)

<!--To configure Form Data Model prefill service in an interactive communication, you can select Form Data Model Prefill Service in the Prefill Service drop-down while creating it or later by modifying the properties.

![edit-ic-props](assets/edit-ic-props.png)

Edit Properties dialog for an interactive communication-->

## Scrivere i dati del modulo adattivo inviati nelle origini dati {#write-af}

Quando un utente invia un modulo basato su un modello di dati modulo, è possibile configurare il modulo in modo da scrivere i dati inviati per un oggetto modello dati nelle relative origini dati. Per ottenere questo caso d&#39;uso, [!DNL Experience Manager Forms] fornire [Azione di invio del modello dati del modulo](configuring-submit-actions.md)disponibile solo per Adattivo Forms basato su un modello dati del modulo. Scrive i dati inviati per un oggetto modello dati nella relativa origine dati.

Per configurare l’azione di invio del modello dati modulo, apri le proprietà del contenitore del modulo adattivo e seleziona **[!UICONTROL Invia utilizzando il modello dati del modulo]** dal menu a discesa Invia azione sotto il pannello a soffietto Invio. Quindi, sfoglia e seleziona un oggetto modello dati dal **[!UICONTROL Nome dell’oggetto modello dati da inviare]** a discesa. Salva le proprietà.

All’invio del modulo, i dati per l’oggetto modello dati configurato vengono scritti nella rispettiva origine dati.

<!--![data-submission](assets/data-submission.png)-->

È inoltre possibile inviare allegati modulo a un’origine dati utilizzando la proprietà dell’oggetto modello dati binario. Per inviare allegati a un’origine dati JDBC, effettua le seguenti operazioni:

1. Aggiungere un oggetto modello dati che include una proprietà binaria al modello dati del modulo.
1. Nel modulo adattivo, trascina **[!UICONTROL File allegato]** dal browser Componenti nel modulo adattivo.
1. Tocca per selezionare il componente aggiunto e tocca ![settings_icon](assets/configure-icon.svg) per aprire il browser Proprietà del componente.
1. Nel campo Riferimento binding , tocca ![cartella_18](assets/folder-search-icon.svg) e selezionare la proprietà binaria aggiunta nel modello dati del modulo. Configura altre proprietà, a seconda delle necessità.

   Tocca ![pulsante di controllo](assets/save_icon.svg) per salvare le proprietà. Il campo allegato è ora associato alla proprietà binaria del modello dati del modulo.

1. Nella sezione Invio delle proprietà del contenitore di moduli adattivi, abilita **[!UICONTROL Invia allegati modulo]**. Invia l’allegato nel campo della proprietà binaria all’origine dati all’invio del modulo.

## Richiamare i servizi in Adaptive Forms utilizzando le regole {#invoke-services}

In un modulo adattivo basato su un modello di dati del modulo, è possibile [creare regole](rule-editor.md) per richiamare servizi configurati nel modello dati del modulo. La **[!UICONTROL Richiamare i servizi]** in una regola sono elencati tutti i servizi disponibili nel modello dati modulo e consentono di selezionare i campi di input e output per il servizio. È inoltre possibile utilizzare **[!UICONTROL Imposta valore]** tipo di regola per richiamare un servizio Form Data Model e impostare il valore di un campo sull&#39;output restituito dal servizio.

Ad esempio, la regola seguente richiama un servizio get che utilizza l&#39;ID dipendente come input e i valori restituiti sono compilati nei corrispondenti campi ID dipendente, Cognome, Nome e Genere del modulo.

![invoke-service](assets/invoke-service.png)

Inoltre, puoi utilizzare la `guidelib.dataIntegrationUtils.executeOperation` API per scrivere un JavaScript nell&#39;editor di codice per l&#39;editor di regole. <!-- For API details, see [API to invoke Form Data Model service](invoke-form-data-model-services.md).-->
