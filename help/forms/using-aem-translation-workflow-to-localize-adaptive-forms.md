---
title: Come possiamo utilizzare il flusso di lavoro di traduzione dell’AEM per localizzare il Forms adattivo e il documento di record?
description: Scopri come utilizzare i flussi di lavoro di traduzione dell’AEM per localizzare il Forms adattivo e il documento di record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---


# Localizzare Forms adattivo e documento di record{#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

I moduli localizzati consentono di fornire servizi a un pubblico più ampio in aree geografiche diverse. Il flusso di lavoro di traduzione Adobe Experience Manager consente di localizzare Adaptive Forms e i relativi documenti di record . È possibile utilizzare **traduzione automatica** o **traduttori umani** per localizzare un modulo adattivo.

Questo articolo spiega il processo per utilizzare il flusso di lavoro di traduzione AEM con Forms adattivo e documenti di record.

## Localizzazione di un modulo adattivo e di un documento record tramite traduzione automatica {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Il servizio di traduzione automatica traduce immediatamente il contenuto in modulo adattivo e documento di record. [!DNL AEM Forms] è preconfigurato per utilizzare una versione di prova di [!DNL Microsoft Translator] per la traduzione automatica. Per abilitare la traduzione automatica per il Forms adattivo e il documento di record, effettua le seguenti operazioni:

1. Il giorno [!DNL AEM Forms] , seleziona un modulo e tocca il **Aggiungi dizionario** opzione.
1. In entrata **Aggiungi dizionario a progetto di traduzione** , seleziona la **Crea un nuovo progetto di traduzione** o **Aggiungi a un progetto di traduzione esistente** opzione.
1. In **Titolo progetto** , specificare il titolo. Ad esempio `Government Reference Site - German locale.`
1. In **Lingue di destinazione** , specificare una lingua (ad esempio, `German(de)`) e fai clic su **Fine**. È possibile specificare più impostazioni internazionali. Il modulo viene tradotto in tutte le lingue specificate in **Lingue di destinazione** campo.
1. Nella finestra di dialogo Dizionario aggiunto fare clic su **Progetti aperti**. Nella schermata Progetti, apri il progetto creato.
1. Fai clic su **ellissi** nella parte inferiore della sezione **Riepilogo traduzione** affiancare. Viene visualizzata la schermata Riepilogo traduzione.
1. Fai clic su **Modifica** nella parte superiore della sezione **Riepilogo traduzione** schermo. Apri **Traduzione** e selezionare Traduzione automatica in **Metodo di traduzione** schermo. Seleziona la scheda appropriata **Provider traduzione** e **Configurazione cloud**. Fai clic su **Fine** nella parte superiore dello schermo.
1. Il giorno **Lavoro di traduzione** , fai clic su ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e fai clic su **Inizio**. Lo stato della sezione diventa Bozza. Al termine della traduzione, lo stato cambia in **Pronto per la revisione**. Aggiorna la pagina dopo alcuni minuti e verifica lo stato.
1. Dopo che lo stato diventa **Pronto per la revisione** il **Lavoro di traduzione** riquadro, aprire il modulo in una finestra del browser. Viene visualizzata una versione localizzata del modulo.

   >[!NOTE]
   >
   >* Prima di aprire la versione localizzata del modulo nella finestra del browser, verificare che le impostazioni internazionali del browser corrispondano a quelle del modulo. Ad esempio, se il modulo è tradotto in lingua tedesca (de), impostare le impostazioni internazionali del browser su Tedesco (de).
   >* I componenti per moduli adattivi non supportano le lingue da destra a sinistra (RTL). Ad esempio, ebraico.

   Insieme al modulo adattivo, viene localizzato anche il documento di record generato automaticamente.

   Per ulteriori informazioni sulle impostazioni e sulla configurazione del documento record, vedi:

[Configurazione modello del documento record](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Impostazioni del documento record](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizzare le informazioni di branding del documento record](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) e assicurati che le impostazioni locali del browser siano impostate sulla stessa lingua in cui hai localizzato il modulo adattivo utilizzando la lingua del computer. Le impostazioni locali del browser consentono di localizzare le informazioni di branding nel documento di record.
1. Per visualizzare il documento di record localizzato, tocca Genera anteprima. Il documento di Record PDF viene generato e aperto in una nuova scheda nel browser.

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

