---
title: Come possiamo utilizzare il flusso di lavoro di traduzione dell’AEM per localizzare il Forms adattivo e il documento di record?
description: Scopri come utilizzare i flussi di lavoro di traduzione dell’AEM per localizzare il Forms adattivo e il documento di record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 1%

---


# Localizzare Forms adattivo e documento di record{#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

I moduli localizzati consentono di fornire servizi a un pubblico più ampio in aree geografiche diverse. Il flusso di lavoro di traduzione Adobe Experience Manager consente di localizzare Adaptive Forms e i relativi documenti di record . Puoi utilizzare **traduzione automatica** o **traduttori umani** per localizzare un modulo adattivo.

Questo articolo spiega il processo per utilizzare il flusso di lavoro di traduzione AEM con Forms adattivo e documenti di record.

## Localizzazione di un modulo adattivo e di un documento record tramite traduzione automatica {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Il servizio di traduzione automatica traduce immediatamente il contenuto in modulo adattivo e documento di record. [!DNL AEM Forms] è preconfigurato per utilizzare una versione di prova di [!DNL Microsoft Translator] per la traduzione automatica. Per abilitare la traduzione automatica per il Forms adattivo e il documento di record, effettua le seguenti operazioni:

1. Nell&#39;interfaccia utente [!DNL AEM Forms], selezionare un modulo e selezionare l&#39;opzione **Aggiungi dizionario**.
1. Nella schermata **Aggiungi dizionario al progetto di traduzione**, seleziona l&#39;opzione **Crea un nuovo progetto di traduzione** o **Aggiungi a un progetto di traduzione esistente**.
1. Nel campo **Titolo progetto**, specifica il titolo. Ad esempio `Government Reference Site - German locale.`
1. Nel campo **Lingue di destinazione**, specificare una lingua (ad esempio, `German(de)`) e fare clic su **Fine**. È possibile specificare più impostazioni internazionali. Il modulo viene tradotto in tutte le lingue specificate nel campo **Lingue di destinazione**.
1. Nella finestra di dialogo Dizionario aggiunto fare clic su **Apri progetti**. Nella schermata Progetti, apri il progetto creato.
1. Fai clic sui **puntini di sospensione** nella parte inferiore del riquadro **Riepilogo traduzione**. Viene visualizzata la schermata Riepilogo traduzione.
1. Fai clic sull&#39;icona **Modifica** nella parte superiore della schermata **Riepilogo traduzione**. Apri la scheda **Traduzione** e seleziona Traduzione automatica nella schermata **Metodo di traduzione**. Selezionare il **provider di traduzione** e la **configurazione cloud** appropriati. Fai clic sull&#39;icona **Fine** nella parte superiore della schermata.
1. Nel riquadro **Processo di traduzione**, fai clic sull&#39;icona ![aem62forms_downarrow](assets/aem62forms_downarrow.png), quindi fai clic su **Inizio**. Lo stato della sezione diventa Bozza. Al termine della traduzione, lo stato diventa **Pronto per la revisione**. Aggiorna la pagina dopo alcuni minuti e verifica lo stato.
1. Quando lo stato cambia in **Pronto per la revisione** nella sezione **Processo di traduzione**, apri il modulo in una finestra del browser. Viene visualizzata una versione localizzata del modulo.

   >[!NOTE]
   >
   >* Prima di aprire la versione localizzata del modulo nella finestra del browser, verificare che le impostazioni internazionali del browser corrispondano a quelle del modulo. Ad esempio, se il modulo è tradotto in lingua tedesca (de), impostare le impostazioni internazionali del browser su Tedesco (de).
   >* I componenti per moduli adattivi non supportano le lingue da destra a sinistra (RTL). Ad esempio, ebraico.

   Insieme al modulo adattivo, viene localizzato anche il documento di record generato automaticamente.

   Per ulteriori informazioni sulle impostazioni e sulla configurazione del documento record, vedi:

[Configurazione modello del documento record](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Impostazioni del documento record](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizzare le informazioni di branding del documento record](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) e assicurarsi che le impostazioni locali del browser siano impostate sulla stessa lingua in cui è stato localizzato il modulo adattivo utilizzando la lingua del computer. Le impostazioni locali del browser consentono di localizzare le informazioni di branding nel documento di record.
1. Per visualizzare il documento di record localizzato, selezionare Genera anteprima. Il documento di Record PDF viene generato e aperto in una nuova scheda nel browser.

<!-- ## Localizing an Adaptive Form and its Document of Record using Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Human translation the content is sent to a translation provider and translated by professional translators. When complete, the translated content is returned and imported into AEM. When your translation provider is integrated with AEM, content is automatically sent between AEM and the translation provider.

For translation, a dictionary containing files in XLIFF format is shared with the professional translators. The dictionary includes a separate XLIFF file for each locale. Each XLIFF file contains text that is displayed to the end users and placeholders for the corresponding localized text.

Perform the following steps to localize a form and its Document of Record using Human Translators:

1. [Connect AEM with your translation service provider](/help/sites-administering/tc-tic.md) and [create translation integration framework configurations](/help/sites-administering/tc-tic.md).

1. [Associate the pages of your language master](/help/sites-administering/tc-tic.md) with the translation service and framework configurations.

1. [Identify the type of content](/help/sites-administering/tc-rules.md) to translate.

1. [Prepare the content for translation](/help/sites-administering/tc-prep.md) by authoring the language master and creating the root pages of language copies.

1. [Create translation projects](/help/sites-administering/tc-manage.md) to gather the content to translate and to prepare the translation process.

1. Use the translation projects to [manage the content translation process](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Adaptive Form components do not support right to left (RTL) languages. For example, Hebrew.
> -->

