---
title: Utilizzo AEM flusso di lavoro di traduzione per localizzare Adaptive Forms e Document of Record
seo-title: Using AEM translation workflow to localize Adaptive Forms and Document of Record
description: Scopri come utilizzare AEM flussi di lavoro di traduzione per localizzare Adaptive Forms e Document of Record.
seo-description: Learn to use AEM translation workflows to localize Adaptive Forms and Document of Record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# Utilizzo AEM flusso di lavoro di traduzione per localizzare Adaptive Forms e Document of Record {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

I moduli localizzati consentono di distribuire un pubblico più ampio in più aree geografiche. Il flusso di lavoro di traduzione di Adobe Experience Manager consente di localizzare Adaptive Forms e i loro documenti di record . È possibile utilizzare **traduzione automatica** o **traduttori** per localizzare un modulo adattivo.

Questo articolo spiega il processo per utilizzare AEM flusso di lavoro di traduzione con Adaptive Forms e documenti di registrazione.

## Localizzazione di un modulo adattivo e di un documento di record utilizzando la traduzione automatica {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Il servizio di traduzione automatica traduce immediatamente il contenuto in Modulo adattivo e Documento di registrazione. [!DNL AEM Forms] è preconfigurato per utilizzare una versione di prova di [!DNL Microsoft Translator] per la traduzione automatica. Esegui i seguenti passaggi per abilitare la traduzione automatica per l&#39;Adaptive Forms e il Documento di record:

1. Sulla [!DNL AEM Forms] Interfaccia utente, seleziona un modulo e tocca **Aggiungi dizionario** opzione .
1. In **Aggiungi dizionario al progetto di traduzione** seleziona la **Crea un nuovo progetto di traduzione** o **Aggiungi a un progetto di traduzione esistente** opzione .
1. In **Titolo del progetto** Specifica il titolo. Esempio, `Government Reference Site - German locale.`
1. In **Lingue di destinazione** specificare un&#39;impostazione internazionale (ad esempio, `German(de)`) e fai clic su **Fine**. È possibile specificare più impostazioni internazionali. Il modulo viene convertito in tutte le impostazioni internazionali specificate nella **Lingue di destinazione** campo .
1. Nella finestra di dialogo Dizionario aggiunto fare clic su **Apri progetti**. Nella schermata Progetti , apri il progetto appena creato.
1. Fai clic sul pulsante **ellissi** nella parte inferiore del **Riepilogo della traduzione** piastrelle. Viene visualizzata la schermata Riepilogo traduzioni.
1. Fai clic sul pulsante **Modifica** nella parte superiore della **Riepilogo della traduzione** schermo. Apri **Traduzione** e selezionare Traduzione automatica nel **Metodo di traduzione** schermo. Selezionare il **Provider di traduzione** e **Configurazione cloud**. Fai clic sul pulsante **Fine** nella parte superiore dello schermo.
1. Sulla **Processo di traduzione** riquadro, fai clic su ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e fai clic su **Inizio**. Lo stato della tessera diventa Bozza. Al termine della traduzione, lo stato cambia in **Pronto per la revisione**. Aggiorna la pagina dopo alcuni minuti e verifica lo stato.
1. Dopo che lo stato cambia in **Pronto per la revisione** sulla **Processo di traduzione** aprire il modulo in una finestra del browser. Viene visualizzata una versione localizzata del modulo.

   >[!NOTE]
   >
   >* Prima di aprire la versione localizzata del modulo nella finestra del browser, assicurarsi che le impostazioni internazionali del browser corrispondano alle impostazioni internazionali del modulo. Ad esempio, se il modulo è tradotto in tedesco(de), impostare le impostazioni internazionali del browser su Tedesco(de).
   >* I componenti per modulo adattivo non supportano le lingue RTL (da destra a sinistra). Per esempio, l&#39;ebraico.


   Insieme al modulo adattivo, viene localizzato anche il documento di record generato automaticamente.

   Per ulteriori informazioni sulle impostazioni e sulla configurazione del documento di record, vedere:

[Configurazione modello del documento record](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Impostazioni del documento di registrazione](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizzare le informazioni di branding del documento di registrazione](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) e assicurarsi che le impostazioni internazionali del browser siano impostate sulla stessa lingua in cui è stato localizzato il modulo adattivo utilizzando la lingua della macchina. Le impostazioni internazionali del browser consentono di localizzare le informazioni sul marchio nel documento di registrazione.
1. Per visualizzare il documento di record localizzato, toccare Genera anteprima. Il PDF Document of Record viene generato e aperto in una nuova scheda del browser.

<!-- ## Localizing an Adaptive Form and its Document of Record using Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Human translation the content is sent to a translation provider and translated by professional translators. When complete, the translated content is returned and imported into AEM. When your translation provider is integrated with AEM, content is automatically sent between AEM and the translation provider.

For translation, a dictionary containing files in XLIFF format is shared with the professional translators. The dictionary includes a separate XLIFF file for each locale. Each XLIFF file contains text that will be displayed to the end users and placeholders for the corresponding localized text.

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

