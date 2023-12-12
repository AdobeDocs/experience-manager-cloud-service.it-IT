---
title: Come possiamo tradurre un Modulo adattivo basato su Componenti core?
description: Scopri come creare un modello di dati modulo in AEM Forms, testare il modello con dati e servizi di esempio e configurare varie opzioni per un modello.
feature: Adaptive Forms, Core Components
exl-id: ad46bf0f-e6ec-4c52-9695-5768a9968e16
source-git-commit: eaab351460363b83c7d3667e048235506cc71c41
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 3%

---

# Utilizzare la traduzione automatica o la traduzione umana per tradurre un modulo adattivo basato su componenti core {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

I moduli localizzati consentono di fornire servizi a un pubblico più ampio in aree geografiche diverse. Il flusso di lavoro di traduzione Adobe Experience Manager consente di localizzare Adaptive Forms e i relativi documenti di record . È possibile utilizzare **traduzione automatica** o **traduttori umani** per localizzare un modulo adattivo.

## Tradurre un modulo adattivo e un documento di record utilizzando la traduzione automatica {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Il servizio di traduzione automatica traduce immediatamente il contenuto in modulo adattivo e [Documento record](/help/forms/generate-document-of-record-core-components.md). AEM Forms as a Cloud Service è preconfigurato per utilizzare una versione di prova di Microsoft Translator per la traduzione automatica. Per abilitare la traduzione automatica per il Forms adattivo e il documento di record, effettua le seguenti operazioni:

1. Nell’interfaccia utente di AEM Forms, seleziona un modulo e fai clic su **[!UICONTROL Aggiungi dizionario]** opzione.
1. Nella schermata Aggiungi dizionario al progetto di traduzione, per **[!UICONTROL Progetto]** opzione

   * Per creare un progetto di traduzione, seleziona la **[!UICONTROL Crea un nuovo progetto di traduzione]** e nella **Titolo progetto** , specificare il titolo. Ad esempio `Government Reference Site - German locale.`
   * Per aggiungere un nuovo dizionario a un progetto di traduzione esistente, seleziona la **[!UICONTROL Aggiungi a un progetto di traduzione esistente]** e selezionare un&#39;opzione **[!UICONTROL Progetto di traduzione esistente]**.
1. In **Lingue di destinazione** , specificare una lingua (ad esempio, `German(de)`). È possibile specificare più impostazioni internazionali. Il modulo viene tradotto in tutte le lingue specificate in **Lingue di destinazione** campo. Clic **Fine**.
1. Nella finestra di dialogo Dizionario aggiunto fare clic su **Progetti aperti**.
1. Nella schermata Progetti, fai clic sul progetto creato. Ad esempio, fai clic su **Sito di riferimento per la pubblica amministrazione - lingua tedesca** affiancare.
1. Il giorno **Lavoro di traduzione** , fai clic su ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e fai clic su **Inizio**. Lo stato della sezione diventa Bozza. Al termine della traduzione, lo stato cambia in **Approvato**. Aggiorna la pagina dopo alcuni minuti e verifica lo stato.

   ![Avvia traduzione](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. Dopo che lo stato diventa **Approvato** il **Lavoro di traduzione** , fai clic su ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e fai clic su **Completa**.

1. Per visualizzare in anteprima il modulo localizzato, seleziona il modulo localizzato nell’interfaccia utente di AEM Forms. Clic **[!UICONTROL Anteprima]** >**[!UICONTROL Anteprima come HTML]**. Riapri il modulo dopo l’aggiunta di `afAcceptLang=<locale code>` all’URL del modulo. Ad esempio, aggiungi `afAcceptLang=de`per aprire la versione tedesca del modulo.


   >[!NOTE]
   >
   >* Prima di aprire la versione localizzata del modulo nella finestra del browser, verificare che le impostazioni internazionali del browser corrispondano a quelle del modulo. Ad esempio, se il modulo è tradotto in lingua tedesca (de), impostare le impostazioni internazionali del browser su Tedesco (de).
   >* I componenti dei moduli adattivi non supportano le lingue da destra a sinistra (RTL). Ad esempio, ebraico.

<!-- 
   Along with the Adaptive form, the auto-generated document of record is also localized.

   For more information on Document of Record settings and configuration, see:

   [Document of Record Template](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Document of Record settings](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Customize the branding information of the document of record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) and ensure that the browser locale is set to the same language to which you have localized the Adaptive Form using machine language. The browser locale helps localize the branding information in the document of record.
1. To view the localized document of record, select Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## Localizzazione di un modulo adattivo e del relativo documento di record tramite Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Traduzione umana il contenuto viene inviato a un fornitore di traduzione e tradotto da traduttori professionisti. Una volta completato, il contenuto tradotto viene rinviato e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.

Per la traduzione, un dizionario contenente file in formato XLIFF viene condiviso con i traduttori professionisti. Il dizionario include un file XLIFF separato per ciascuna lingua. Ogni file XLIFF contiene testo visualizzato agli utenti finali e segnaposto per il testo localizzato corrispondente.

Per localizzare un modulo e il relativo documento di record mediante Human Translators, effettuare le seguenti operazioni:

1. Nell’interfaccia utente di AEM Forms, seleziona un modulo e fai clic su **[!UICONTROL Aggiungi dizionario]** opzione.
1. Nella schermata Aggiungi dizionario al progetto di traduzione, per **[!UICONTROL Progetto]** opzione

   * Per creare un progetto di traduzione, seleziona la **[!UICONTROL Crea un nuovo progetto di traduzione]** e nella **Titolo progetto** , specificare il titolo. Ad esempio `Government Reference Site - German locale.`
   * Per aggiungere un nuovo dizionario a un progetto di traduzione esistente, seleziona la **[!UICONTROL Aggiungi a un progetto di traduzione esistente]** e selezionare un&#39;opzione **[!UICONTROL Progetto di traduzione esistente]**.
1. In **Lingue di destinazione** , specificare una lingua (ad esempio, `German(de)`). È possibile specificare più impostazioni internazionali. Il modulo viene tradotto in tutte le lingue specificate in **Lingue di destinazione** campo. Clic **Fine**.
1. Nella finestra di dialogo Dizionario aggiunto fare clic su **Progetti aperti**.
1. Nella schermata Progetti, fai clic sul progetto creato. Ad esempio, fai clic su **Sito di riferimento per la pubblica amministrazione - lingua tedesca** affiancare.
1. Nella parte inferiore della sezione **Riepilogo** , fai clic su **ellissi**. Viene visualizzata la schermata Proprietà progetto di traduzione.
1. Apri **[!UICONTROL Avanzate]** nella parte superiore della sezione **Proprietà progetto di traduzione** schermo. Per **[!UICONTROL Campo di traduzione]**, seleziona **[!UICONTROL Traduzione umana]**. Clic **Salva e chiudi** nella parte superiore dello schermo.
1. Il giorno **Lavoro di traduzione** , fai clic su ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e fai clic su **Esporta**. Nella finestra di dialogo Esporta, fai clic sull’opzione Scarica file esportato. Scarica un file .zip.
   ![Esporta file di traduzione](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. Estrai il file .zip scaricato. La cartella estratta contiene due file:
   * translation_export_summary.xml
   * [form-fields-file].xml.
1. Apri [form-fields-file].xml per la modifica. Aggiungi le stringhe e i messaggi localizzati per i campi modulo. Salva e chiudi il file.
1. Comprimere i file translation_export_summary.xml e [form-fields-file].xml.
1. Il giorno **Lavoro di traduzione** , fai clic su ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e fai clic su **Importa**. Seleziona l’archivio contenente [form-fields-file].xml. con stringhe e messaggi localizzati per i campi modulo.

   ![Importa file di traduzione](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. Per visualizzare in anteprima il modulo localizzato, seleziona il modulo localizzato nell’interfaccia utente di AEM Forms. Clic **[!UICONTROL Anteprima]** >**[!UICONTROL Anteprima come HTML]**. Riapri il modulo dopo l’aggiunta di `afAcceptLang=<locale code>` all’URL del modulo. Ad esempio, aggiungi `afAcceptLang=de`per aprire la versione tedesca del modulo.

## Consulta anche {#see-also}

{{see-also}}