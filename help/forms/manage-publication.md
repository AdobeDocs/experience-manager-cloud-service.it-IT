---
title: Come si pubblicano o annullano la pubblicazione dei moduli nelle istanze di anteprima o pubblicazione?
description: Scopri come pubblicare o annullare la pubblicazione di moduli dall’ambiente di authoring AEM per visualizzare in anteprima o pubblicare le istanze. Sia che si eseguano test dei moduli in un ambiente di staging o che si distribuiscano in tempo reale per gli utenti finali, AEM fornisce strumenti semplificati per gestire questo processo in modo efficiente.
Keywords: Manage publication, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: d3c089dcca80255f53c0888d46ee1b4b6246741e
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---


# &#x200B;Gestisci pubblicazione in Experience Manager Forms

In qualità di amministratore di Adobe Experience Manager Forms, puoi pubblicare i moduli dall’istanza di authoring a Experience Manager Forms. È possibile pianificare la pubblicazione di un modulo o di una cartella in una data o in un&#39;ora successiva. Dopo la pubblicazione, gli utenti possono accedere e compilare i moduli.

Nell’interfaccia di Experience Manager Forms, puoi pubblicare un modulo utilizzando:
* [Opzione Publish](#publish-forms-using-the-publish-option)
* [Opzione Gestisci pubblicazione](#publish-forms-using-the-manage-publication-option)

Se si apportano modifiche successive ai moduli o alla cartella originali in Experience Manager Forms, le modifiche non verranno applicate nell&#39;istanza **Publish** fino a quando non si ripubblica da Experience Manager Forms. Le modifiche in corso di lavorazione non sono disponibili nell&#39;istanza **Publish**. Nell&#39;istanza **Publish** sono disponibili solo le modifiche pubblicate da un amministratore.

## Publish forms utilizzando l&#39;opzione Publish

L&#39;opzione **Publish** consente di pubblicare immediatamente un modulo. Per pubblicare un modulo di Experience Manager utilizzando il pulsante **Publish** sulla barra degli strumenti. Per pubblicare i moduli utilizzando l’opzione Publish:

1. Dalla console Experience Manager Forms, passa alla cartella principale e seleziona il modulo da pubblicare.
1. Fai clic sull&#39;opzione **Publish** nella barra degli strumenti e controlla tutte le risorse di riferimento che verranno pubblicate con il modulo.
1. Fai clic su **[!UICONTROL Pubblica]**.

   ![Publish e Annulla pubblicazione modulo](/help/edge/docs/forms/assets/publish-form-option.png)

   Dopo la pubblicazione del modulo e delle risorse correlate, viene visualizzata una finestra di dialogo **Operazione completata**. Fai clic su **Chiudi** per chiudere la finestra di dialogo.

   ![Finestra di dialogo di successo](/help/forms/assets/publish-success.png)

### Annullare la pubblicazione del modulo

Dopo aver pubblicato correttamente il modulo utilizzando l&#39;opzione **Publish** e le relative risorse, puoi anche annullarne la pubblicazione utilizzando il pulsante **[!UICONTROL Annulla pubblicazione]** sulla barra degli strumenti. Per annullare la pubblicazione di un modulo:

1. Per annullare la pubblicazione del modulo e delle risorse correlate, selezionare il modulo e fare clic su **[!UICONTROL Annulla pubblicazione]** nella barra degli strumenti

   Quando fai clic sul pulsante **[!UICONTROL Annulla pubblicazione]**, viene visualizzata la finestra di dialogo **Annulla pubblicazione risorsa**.
1. Fai clic su **[!UICONTROL Annulla pubblicazione]** per avviare il processo di annullamento della pubblicazione

   ![Rimuovi ](/help/forms/assets/unpublish-asset.png)

   Dopo aver annullato la pubblicazione del modulo e delle risorse correlate, viene visualizzata la finestra di dialogo **Operazione riuscita**. Fai clic su **Chiudi** per chiudere la finestra di dialogo.

   ![annullamento pubblicazione completato](/help/forms/assets/unpublishing-start.png)

## Publish Form mediante l&#39;opzione Gestisci pubblicazione

Gestisci pubblicazione consente di pubblicare o annullare la pubblicazione dei contenuti da e verso la destinazione selezionata, di aggiungere contenuto all’elenco di pubblicazione dalla cartella Moduli e documenti, di selezionare i riferimenti da pubblicare e pianificare la pubblicazione a una data o un’ora successiva.  Per pubblicare i moduli con l’opzione Gestisci pubblicazione:

1. Dalla console Experience Manager Forms, passa alla cartella principale e seleziona il modulo da pubblicare.
1. Fai clic sull&#39;opzione **[!UICONTROL Gestisci pubblicazione]** nella barra degli strumenti.

   ![Opzione Gestisci pubblicazione](/help/forms/assets/manage-publication-option.png)

   Viene visualizzata l&#39;interfaccia **Gestisci pubblicazione**:

   ![Gestisci pubblicazione](/help/forms/assets/manage-publication.png)

   Nell&#39;interfaccia **Gestisci pubblicazione** sono disponibili le opzioni seguenti:

   * **Azioni**

      * **Publish**: Publish Forms alla destinazione selezionata
      * **Annulla pubblicazione**: annulla la pubblicazione dei moduli dalla destinazione

   * **Destinazione**

      * **Publish**: istanza Publish Forms to Experience Manager Forms (AEM) Publish.
      * **Anteprima**: istanza di anteprima da Publish Forms a Experience Manager Forms (AEM).

   * **Pianificazione**

      * **Ora**: Publish Forms immediatamente
      * **Più tardi**: Publish Forms basato su **Data di attivazione** o ora

1. Fai clic su **Avanti** per continuare.
1. Nella scheda **Ambito**, utilizza l&#39;opzione [Aggiungi contenuto](#add-content) per aggiungere altro contenuto per la pubblicazione. È ad esempio possibile aggiungere altri file Forms o Document of Record.
   ![scheda ambito](/help/forms/assets/scope-tab.png)
1. Fai clic su **[!UICONTROL Publish]** per pubblicare i moduli e le risorse correlate. Viene visualizzato un messaggio di operazione riuscita.
   ![messaggio di pubblicazione completato](/help/forms/assets/publish-successful.png)

### Aggiungi contenuto

La pubblicazione in Experience Manager Forms consente di aggiungere ulteriore contenuto (moduli e cartelle) all’elenco di pubblicazione. È possibile aggiungere altri moduli o cartelle all&#39;elenco dalla cartella `formsanddocuments`. Non è tuttavia possibile aggiungere moduli da più cartelle alla volta. Per aggiungere altri moduli per la pubblicazione:

1. Fai clic sul pulsante **Aggiungi contenuto** per aggiungere altro contenuto.

   ![Aggiungi contenuto](/help/forms/assets/add-content.png)

1. Selezionare il modulo dalla schermata **Seleziona percorso**. È possibile aggiungere più moduli da una cartella o più cartelle alla volta. Non è tuttavia possibile aggiungere moduli da più cartelle alla volta.

   ![Aggiungi contenuto](/help/forms/assets/add-assets.png)

1. Per configurare i riferimenti da pubblicare o meno per un modulo, selezionare il modulo e fare clic su **[!UICONTROL Riferimenti pubblicati]**.

   ![riferimenti pubblicati](/help/forms/assets/published-references.png)

1. Nella finestra di dialogo **Riferimenti pubblicati**, deseleziona le risorse che intendi non pubblicare e fai clic su **[!UICONTROL Fine]**.
   ![finestra di dialogo riferimenti pubblicati](/help/forms/assets/published-references-dialog.png)

<!--
### Include Folder Settings
By default, publishing a folder to Experience Manager Forms publishes all the assets, subfolders, and their references. To filter the folder for publishing:

1. Click **[Include Folder Settings]** to filter the folder.

    ![Include folder](/help/forms/assets/include-folder.png)

    The **[UICONTROL Include Folder Settings]** dialog appears. 
    
    ![Include folder dialog](/help/forms/assets/include-folder-dialog.png)
    
    The **[UICONTROL Include Folder Settings]** includes following options:

    * **[!UICONTROL Include folder contents]** checkbox. 
        * If selected, all forms and assets in the chosen folder, its subfolders (including all forms and assets within them), and references are published.
        * If not selected, only the forms and assets in the selected folder are published, while subfolder forms and assets are not.

    * **[!UICONTROL Include only immediate folder contents]** checkbox
        Selecting the **[!UICONTROL Include folder contents]** checkbox enables the **[!UICONTROL Include only immediate folder contents]** checkbox for selection.

        * If you select both options, all the forms and assets of the selected folder, subfolders (empty), and references are published. The forms and assets of the subfolders are not published.
        * -->


### Publish o annullare la pubblicazione di un modulo in un secondo momento

Oltre a consentire di pubblicare o annullare la pubblicazione dei moduli in una data e in un’ora successive, l’opzione Pubblica o Annulla pubblicazione successiva consente anche di configurare un flusso di lavoro. I moduli vengono pubblicati o ne viene annullata la pubblicazione dopo il completamento del flusso di lavoro. Per pianificare la pubblicazione o l&#39;annullamento della pubblicazione di un modulo:

1. Dalla console Experience Manager Forms, passa alla cartella principale e seleziona il modulo da pianificare per la pubblicazione.
1. Fai clic sull&#39;opzione **[!UICONTROL Gestisci pubblicazione]** nella barra degli strumenti.

   ![Gestisci pubblicazione](/help/forms/assets/manage-publication.png)

1. Fai clic su **Publish** o **Annulla pubblicazione** da **[!UICONTROL Azione]**, quindi seleziona la **[!UICONTROL Destinazione]** in cui desideri pubblicare o annullare la pubblicazione del contenuto.
   * **Anteprima**: utilizzare l&#39;opzione **Anteprima** per pubblicare o annullare la pubblicazione in un ambiente di anteprima Experience Manager Forms. Gli ambienti di anteprima Experience Manager Forms vengono utilizzati per testare i moduli di sviluppo.
   * **Publish**: utilizza l&#39;opzione Experience Manager Forms Publish per inviare il modulo all&#39;ambiente di pubblicazione Experience Manager Forms quando sarà pronto per l&#39;utilizzo in un ambiente di produzione.

1. Seleziona **[!UICONTROL Più tardi]** da Pianificazione.

   ![Gestisci pubblicazione più tardi](/help/forms/assets/manage-publication-later.png)

1. Seleziona un **[!UICONTROL Data di attivazione]** e specifica la data e l&#39;ora.
1. Fai clic su **[!UICONTROL Avanti]**.
1. Nella scheda **Ambito**, **[!UICONTROL Aggiungi contenuto]** (se necessario).
   ![Gestisci pubblicazione aggiungi contenuto in seguito](/help/forms/assets/publish-later-add-content.png)
1. Fai clic su **[!UICONTROL Avanti]**.
1. (Facoltativo) Nella scheda **Flussi di lavoro**, specifica un **[!UICONTROL Titolo flusso di lavoro]**.
1. Fai clic su **[!UICONTROL Publish Later]**.

   ![Flusso di lavoro Gestisci pubblicazione](/help/forms/assets/manage-publication-workflows.png)

## Determinazione dello stato di pubblicazione

Esistono diversi modi per determinare lo stato di pubblicazione:

* Accedi all’istanza di destinazione per verificare i moduli pubblicati e altre risorse (a seconda della data o dell’ora pianificata).

* Utilizza la vista timeline per determinare lo stato della pubblicazione.

* Utilizza il menu Informazioni pagina nell’editor di Forms adattivo.
