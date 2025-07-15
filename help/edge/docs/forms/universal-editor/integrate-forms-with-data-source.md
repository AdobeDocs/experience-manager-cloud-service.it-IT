---
title: Come integrare il modello dati modulo (FDM) per un modulo nell’editor universale?
description: Scopri come creare moduli basati su un modello dati modulo (FDM). Genera e modifica dati di esempio per gli oggetti del modello dati nel modello dati modulo (FDM).
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 94%

---

# Integrare i moduli con il modello dati modulo nell’editor universale

L’integrazione dei moduli con un modello di dati modulo (FDM) nell’editor universale consente di utilizzare diverse origini dati back-end per creare un modello di dati modulo (FDM). Puoi utilizzare il modello dati modulo (FDM) come schema in vari flussi di lavoro di moduli. Configura le origini dati e crea un modello dati modulo (FDM) basato sugli oggetti e i servizi del modello dati disponibili nelle origini dati.

## Considerazioni

* Se nell’interfaccia dell’editor universale non viene visualizzata l’icona **Origini dati** o la proprietà **Riferimento bind** nel pannello delle proprietà a destra, abilita l’estensione **Origine dati** in **Extension Manager**.

  ![Schermata dell&#39;interfaccia Extension Manager di Universal Editor che mostra le estensioni disponibili, inclusa l&#39;estensione Origini dati, che possono essere abilitate per l&#39;integrazione modulo](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

  Per informazioni su come abilitare e disabilitare le estensioni nell’editor universale, consulta l’articolo [Caratteristiche principali delle funzioni di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

* Il servizio di precompilazione dei moduli nell’editor universale non è attualmente supportato.

## Prerequisiti

Prima di configurare il modulo con il modello dati modulo nell’editor universale, assicurati di aver completato i seguenti passaggi:

* [Configura origini dati](/help/forms/configure-data-sources.md): configura l’origine dati per connettere il modulo ai dati di back-end.
* [Crea modello dati modulo (FDM)](/help/forms/create-form-data-models.md): crea un modello dati utilizzando oggetti dati e servizi dall’origine dati configurata.
* [Configura oggetti e servizi del modello dati](/help/forms/work-with-form-data-model.md): mappa gli oggetti e i servizi del modello dati per garantire un flusso di dati uniforme tra il modulo e l’origine dati.

## Creazione di moduli con il modello dati del modulo nell’editor universale

Nell’editor universale puoi creare:

* [Modulo basato su schema](#schema-based-form): un modulo basato su schema utilizza un’origine dati configurata durante la creazione del modulo nella scheda **Dati**, associando automaticamente i dati ai campi del modulo.
* [Modulo non basato su schema](#non-schema-based-form): per un modulo non basato su schema è necessario aggiungere manualmente un’origine dati e associare ogni campo dalla struttura del contenuto.

![Tipi di modulo nell’editor universale](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

Questi metodi offrono la flessibilità di collegare modelli di dati con moduli in base alle esigenze.

### Modulo basato su schema

Quando crei un modulo basato su schema, questo viene configurato automaticamente con un’origine dati e i campi modulo sono già collegati ai dati tramite associazioni di dati. Per creare un modulo basato su schema utilizzando la procedura guidata di creazione di moduli, esegui i seguenti passaggi:

1. Accedi all’istanza di authoring [!DNL Experience Manager Forms].
1. Inserisci le credenziali nella pagina di accesso di Experience Manager. Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Seleziona **[!UICONTROL Crea]**  > **[!UICONTROL Moduli adattivi]**. Viene aperta la procedura guidata. Nella scheda **Origine**, seleziona un modello:

   ![Modello di Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

   Quando selezioni un modello basato su Edge Delivery Services, il pulsante **[!UICONTROL Crea]** è abilitato. Per selezionare un’origine dati o un’azione di invio, è possibile passare alle schede **[!UICONTROL Origine dati]** o **[!UICONTROL Invio]**.

1. Nella scheda **Dati** è possibile selezionare uno dei seguenti modelli di dati:

   * **Modello dati modulo (FDM)**: integra nel modulo gli oggetti e i servizi del modello dati dalle origini dati. Se il modulo richiede la lettura e la scrittura di dati da più origini, scegli Modello dati modulo (FDM).

   * **Schema JSON**: integra il modulo con un sistema back-end associando uno schema JSON che definisce la struttura dei dati. Consente di aggiungere contenuti dinamici utilizzando gli elementi dello schema.

     Ad esempio, seleziona il modello dati del modulo creato denominato Modello dati modulo Animale domestico.

     ![Seleziona modello dati modulo](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     Per impostazione predefinita, tutti i campi dello schema JSON e del modello dati modulo associato vengono selezionati e convertiti automaticamente nei componenti del modulo corrispondenti, semplificando il processo di authoring. La procedura guidata consente inoltre di scegliere in modo selettivo i campi da includere nel modulo utilizzando le caselle di controllo.

1. Fai clic su **[!UICONTROL Crea]** per visualizzare la procedura guidata **Crea modulo**.
1. Specifica **Nome** e **Titolo**.
1. Specifica l’**URL di GitHub**. Ad esempio, se l’archivio GitHub è denominato `edsforms` e si trova sotto l’account `wkndforms`, l’URL è:
   `https://github.com/wkndforms/edsforms`
1. Fai clic su **[!UICONTROL Crea]**.

   ![Crea modulo basato su schema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   Non appena fai clic su **[!UICONTROL Crea]**, il modulo viene aperto nell’editor universale per la creazione.

   ![Schermata dell&#39;editor universale che mostra un modulo basato su schema con campi modulo precompilati e il browser Contenuto che visualizza gli elementi dell&#39;origine dati disponibili](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   Il modulo viene creato utilizzando gli elementi dati dall’origine dati associata, con i campi modulo che presentano l’associazione dati preconfigurata.

   ![Associazione automatica dei dati](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   Ora puoi aggiungere e [configurare l’azione di invio](/help/edge/docs/forms/universal-editor/submit-action.md) per il modulo.

### Modulo non basato su schema

Quando crei un modulo non basato su schema, non viene configurata alcuna origine dati. Puoi modificare le proprietà del modulo in un secondo momento per aggiungere un’origine dati e configurare manualmente le associazioni dei dati per i campi del modulo. Per modificare le proprietà del modulo e aggiungere un’origine dati, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring di [!DNL Experience Manager Forms].
1. Inserisci le credenziali nella pagina di accesso di Experience Manager. Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Seleziona il modulo per il quale desideri aggiungere un’origine dati e fai clic su **[!UICONTROL Proprietà]**.
   ![Apri proprietà modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   Vengono visualizzate le proprietà del modulo.
1. Fai clic per aprire la scheda **Modello modulo** e dal menu a discesa **Seleziona da**. Puoi selezionare una delle opzioni seguenti:

   * **Modello dati modulo (FDM)**: crea il modulo utilizzando un modello dati modulo.
   * **Connettore**: crea il modulo utilizzando l’origine dati Adobe Marketo.
   * **Schema**: crea il modulo utilizzando uno schema JSON caricato in AEM Forms.
   * **Nessuno**: crea il modulo da zero senza utilizzare alcun modello di modulo.

     Ad esempio, seleziona il modello dati del modulo (FDM)

     ![Seleziona scheda Modello del modulo](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. Seleziona il Modello dati modulo (FDM) creato dall’elenco a discesa. Ad esempio, seleziona dall’elenco a discesa il modello dati modulo creato e denominato Modello dati modulo Animale domestico.

   ![Seleziona Modello dati modulo](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   vQuando selezioni il modello dati modulo (FDM), viene visualizzata una finestra di dialogo di avvertenza. Fai clic su **OK** per chiudere la finestra di dialogo.

   ![Procedura guidata modello del modulo](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**.
1. Apri il modulo per la modifica. Il modulo viene aperto nell’editor universale per l’authoring.

   ![Authoring di moduli non basato su schema](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   Gli elementi modulo presenti nel modello dati modulo associato (FDM) vengono visualizzati nella scheda **[!UICONTROL Origine dati]** del **[!UICONTROL Browser dei contenuti]** nel **Pannello proprietà**.

   ![Origine dati modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. Seleziona gli elementi dei dati dalla scheda **[!UICONTROL Origine dati]** e fai clic su **[!UICONTROL Aggiungi]**.

   ![Aggiungi elementi dei dati](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   Puoi anche trascinare questi elementi per creare il modulo adattivo. Quando fai clic su **[!UICONTROL Aggiungi]**, gli elementi selezionati dalla scheda **[!UICONTROL Origine dati]** vengono aggiunti al modulo e viene visualizzato un segno di spunta prima degli elementi aggiunti.

   ![Schermata che mostra l&#39;Editor universale con un modulo non di schema generato trascinando elementi dati dalla scheda Source dati nella struttura del modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

Puoi aggiungere il binding dei dati a un campo modulo selezionandolo dalla proprietà **Riferimento bind**. Aggiungi, ad esempio, un riferimento di binding dei dati alla casella di testo **ID** già presente nel modulo.
Per selezionare il binding dei dati per il campo modulo dalla struttura dell’origine dati, effettua i seguenti passaggi:

1. Apri le proprietà del campo modulo per cui desideri aggiungere il riferimento di binding dei dati.
1. Passa alla proprietà **Riferimento bind** e fai clic sull’icona **Sfoglia**.

   ![Aggiungere manualmente il binding dei dati per un campo modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

1. Scegli il riferimento al binding dei dati dalla struttura dell’origine dati nella procedura guidata **Seleziona un riferimento bind**.

   ![seleziona riferimento binding dei dati](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

1. Seleziona l’elemento di dati dalla struttura dell’origine dati che desideri associare al campo modulo e fai clic su **Seleziona**.

   ![seleziona elemento di dati](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

   Il campo modulo si associa all’elemento dati e viene visualizzato nella proprietà **Riferimento bind**.

   ![Binding automatico dei dati](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   Puoi modificare anche manualmente la proprietà **Riferimento bind** per il campo modulo.

Puoi ora aggiungere e [configurare l’azione di invio](/help/edge/docs/forms/universal-editor/submit-action.md) per il modulo.

## Consulta anche

{{universal-editor-see-also}}
