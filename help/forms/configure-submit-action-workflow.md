---
title: Come integrare il flusso di lavoro di AEM con un modulo adattivo?
description: Esplora il processo di avvio automatico del flusso di lavoro con l’azione di invio AEM Forms.
keywords: Flusso di lavoro di AEM, Integrazione di un modulo adattivo con il flusso di lavoro di AEM, Richiama il flusso di lavoro di AEM Azione di invio
feature: Adaptive Forms, Core Components
exl-id: b7788e3d-acd8-4867-b232-f9767cf6b2f5
role: User, Developer
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 1%

---

# Integrare AEM Adaptive Form con AEM Workflow: semplificazione dei processi aziendali

L&#39;azione di invio **[!UICONTROL Richiama un flusso di lavoro AEM]** associa un modulo adattivo a un flusso di lavoro AEM. Quando un modulo viene inviato, il flusso di lavoro associato viene avviato automaticamente nell’istanza Autore. Puoi salvare i file di dati, gli allegati e il documento di record nella posizione di payload del flusso di lavoro o in una variabile. Se il flusso di lavoro è contrassegnato per l’archiviazione dati esterna e configurato per un’archiviazione dati esterna, è disponibile solo l’opzione della variabile. Puoi effettuare una selezione dall’elenco di variabili disponibili per il modello di flusso di lavoro. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni in una fase successiva e non al momento della creazione del flusso di lavoro, assicurati che siano presenti le configurazioni di variabili richieste.

>[!NOTE]
>
>  Scopri come [creare un modello di flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=it#extending-aem) per definire la serie di passaggi eseguiti quando un utente avvia il flusso di lavoro. Puoi anche definire le proprietà del modello, ad esempio se il flusso di lavoro è transitorio o utilizza più risorse.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione degli invii di moduli. Ulteriori informazioni su queste opzioni sono disponibili nell&#39;articolo [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md).

## Vantaggi

Alcuni dei vantaggi dell’integrazione del flusso di lavoro AEM con Adaptive Forms sono:

* L’integrazione del flusso di lavoro AEM consente di automatizzare processi aziendali complessi che richiedono l’invio di moduli.
* AEM Workflow supporta la logica condizionale e consente quindi di prendere decisioni dinamiche in base ai dati dei moduli o a fattori esterni.
* AEM Workflow indirizza le attività in base a regole e condizioni predefinite, garantendo che vengano assegnate alle persone o ai gruppi giusti.

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## Integrare il flusso di lavoro di AEM con Adaptive Forms {#steps-to-integrate-workflow-with-af}

>[!BEGINTABS]

>[!TAB Componente di base]

Per impostare il processo automatizzato con [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=it#extending-aem) per un modulo adattivo basato su componenti di base, eseguire la procedura seguente:

1. Apri il modulo adattivo per la modifica e passa alla sezione **[!UICONTROL Invio]** delle proprietà Contenitore modulo adattivo.
1. Dall&#39;elenco a discesa **[!UICONTROL Azione invio]**, selezionare **Azione invio** come **[!UICONTROL Richiama un flusso di lavoro AEM]**.
1. Selezionare il modello di flusso di lavoro dall&#39;elenco a discesa **[!UICONTROL Modello flusso di lavoro]**.
1. Selezionare l&#39;opzione dall&#39;elenco a discesa **[!UICONTROL Archivia file di dati utilizzando]**.

   **File di dati**: contiene i dati inviati al modulo adattivo. È possibile utilizzare l&#39;opzione **[!UICONTROL Percorso file dati]** per specificare il nome del file e il percorso del file relativo al payload. Il percorso `/addresschange/data.xml`, ad esempio, crea una cartella denominata `addresschange` e la inserisce in relazione al payload. È inoltre possibile specificare solo `data.xml` per inviare solo i dati inviati senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

   ![invoke-workflow-fc](/help/forms/assets/invoke-workflow-fc.png)

1. Selezionare l&#39;opzione dall&#39;elenco a discesa **[!UICONTROL Archivia allegati utilizzando]**.

   **Allegati**: è possibile utilizzare l&#39;opzione **[!UICONTROL Percorso allegato]** per specificare il nome della cartella in cui archiviare gli allegati caricati nel modulo adattivo. La cartella viene creata in relazione al payload. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

1. Selezionare l&#39;opzione dall&#39;elenco a discesa **[!UICONTROL Documenti di record utilizzando]**.

   **Documento record**: contiene il documento record generato per il modulo adattivo. È possibile utilizzare l&#39;opzione **[!UICONTROL Percorso del documento record]** per specificare il nome del file del documento record e il percorso del file relativo al payload. Ad esempio, il percorso `/addresschange/DoR.pdf` crea una cartella denominata `addresschange` relativa al payload e inserisce `DoR.pdf` relativa al payload. È inoltre possibile specificare solo `DoR.pdf` per salvare solo il documento di record senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.
1. Fai clic su **[!UICONTROL Fine]**.

   >[!NOTE]
   >
   > Ulteriori informazioni sui [flussi di lavoro AEM incentrati su Forms - Riferimento al passaggio per automatizzare i processi aziendali](/help/forms/aem-forms-workflow-step-reference.md).

>[!TAB Componente core]

Per impostare il processo automatizzato con [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=it#extending-aem) per un modulo adattivo basato su componenti core, eseguire la procedura seguente:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fare clic sulla scheda **[!UICONTROL Invio]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Invia azione]**, selezionare **[!UICONTROL Richiama un flusso di lavoro AEM]**.

   ![Configurazione azione di Invia e-mail](/help/forms/assets/configure-invoke-aem-workflow.png)

1. Selezionare il modello di flusso di lavoro dall&#39;elenco a discesa **[!UICONTROL Modello flusso di lavoro]**.
1. Selezionare l&#39;opzione dall&#39;elenco a discesa **[!UICONTROL Archivia file di dati utilizzando]**.

   **File di dati**: contiene i dati inviati al modulo adattivo. È possibile utilizzare l&#39;opzione **[!UICONTROL Percorso file dati]** per specificare il nome del file e il percorso del file relativo al payload. Il percorso `/addresschange/data.xml`, ad esempio, crea una cartella denominata `addresschange` e la inserisce in relazione al payload. È inoltre possibile specificare solo `data.xml` per inviare solo i dati inviati senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

1. Selezionare l&#39;opzione dall&#39;elenco a discesa **[!UICONTROL Archivia allegati utilizzando]**.

   **Allegati**: è possibile utilizzare l&#39;opzione **[!UICONTROL Percorso allegato]** per specificare il nome della cartella in cui archiviare gli allegati caricati nel modulo adattivo. La cartella viene creata in relazione al payload. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

1. Selezionare l&#39;opzione dall&#39;elenco a discesa **[!UICONTROL Documenti di record utilizzando]**.

   **Documento record**: contiene il documento record generato per il modulo adattivo. È possibile utilizzare l&#39;opzione **[!UICONTROL Percorso del documento record]** per specificare il nome del file del documento record e il percorso del file relativo al payload. Ad esempio, il percorso `/addresschange/DoR.pdf` crea una cartella denominata `addresschange` relativa al payload e inserisce `DoR.pdf` relativa al payload. È inoltre possibile specificare solo `DoR.pdf` per salvare solo il documento di record senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.
1. Fai clic su **[!UICONTROL Fine]**.

   >[!NOTE]
   >
   > Ulteriori informazioni sui [flussi di lavoro AEM incentrati su Forms - Riferimento al passaggio per automatizzare i processi aziendali](/help/forms/aem-forms-workflow-step-reference.md).

>[!TAB Editor universale]

Per impostare il processo automatizzato con [Flusso di lavoro AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=it#extending-aem) per un modulo adattivo creato in Universal Editor, effettuare le seguenti operazioni:

1. Apri il modulo adattivo per la modifica.
1. Fai clic sull&#39;estensione **Modifica proprietà modulo** nell&#39;editor.
Viene visualizzata la finestra di dialogo **Proprietà modulo**.

   >[!NOTE]
   >
   > * Se l&#39;icona **Modifica proprietà modulo** non è visibile nell&#39;interfaccia di Universal Editor, abilitare l&#39;estensione **Modifica proprietà modulo** in Extension Manager.
   > * Per informazioni su come abilitare o disabilitare le estensioni nell&#39;editor universale, consulta l&#39;articolo [Caratteristiche principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

1. Fai clic sulla scheda **Invio** e seleziona **[!UICONTROL Richiama un&#39;azione di invio del flusso di lavoro di AEM]**.


   ![Configurazione azione di Invia e-mail](/help/forms/assets/invoke-service-ue.png)

1. Selezionare il modello di flusso di lavoro dall&#39;elenco a discesa **[!UICONTROL Modello flusso di lavoro]**.
1. Selezionare l&#39;opzione dall&#39;elenco a discesa **[!UICONTROL Archivia file di dati utilizzando]**.

   **File di dati**: contiene i dati inviati al modulo adattivo. È possibile utilizzare l&#39;opzione **[!UICONTROL Percorso file dati]** per specificare il nome del file e il percorso del file relativo al payload. Il percorso `/addresschange/data.xml`, ad esempio, crea una cartella denominata `addresschange` e la inserisce in relazione al payload. È inoltre possibile specificare solo `data.xml` per inviare solo i dati inviati senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

1. Selezionare l&#39;opzione dall&#39;elenco a discesa **[!UICONTROL Archivia allegati utilizzando]**.

   **Allegati**: è possibile utilizzare l&#39;opzione **[!UICONTROL Percorso allegato]** per specificare il nome della cartella in cui archiviare gli allegati caricati nel modulo adattivo. La cartella viene creata in relazione al payload. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

1. Selezionare l&#39;opzione dall&#39;elenco a discesa **[!UICONTROL Documenti di record utilizzando]**.

   **Documento record**: contiene il documento record generato per il modulo adattivo. È possibile utilizzare l&#39;opzione **[!UICONTROL Percorso del documento record]** per specificare il nome del file del documento record e il percorso del file relativo al payload. Ad esempio, il percorso `/addresschange/DoR.pdf` crea una cartella denominata `addresschange` relativa al payload e inserisce `DoR.pdf` relativa al payload. È inoltre possibile specificare solo `DoR.pdf` per salvare solo il documento di record senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.
1. Fai clic su **[!UICONTROL Fine]**.

   >[!NOTE]
   >
   > Ulteriori informazioni sui [flussi di lavoro AEM incentrati su Forms - Riferimento al passaggio per automatizzare i processi aziendali](/help/forms/aem-forms-workflow-step-reference.md).

>[!ENDTABS]

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## Articoli correlati

{{af-submit-action}}
