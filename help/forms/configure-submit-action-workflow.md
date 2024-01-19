---
Title: How to integrate AEM workflow with an Adaptive Form?
Description: Explore the process of automated workflow initiation with AEM Forms Submit Action.
keywords: Flusso di lavoro AEM, integra modulo adattivo con flusso di lavoro AEM, richiama azione di invio flusso di lavoro AEM
feature: Adaptive Forms, Core Components
source-git-commit: 95af49839d206f67ac02116730229f5b0531c5bb
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---


# Integrare il modulo adattivo AEM con il flusso di lavoro AEM: semplificazione dei processi aziendali

Il **[!UICONTROL Richiama un flusso di lavoro AEM]** Azione di invio associa un modulo adattivo a un flusso di lavoro AEM. Quando un modulo viene inviato, il flusso di lavoro associato viene avviato automaticamente nell’istanza Autore. Puoi salvare i file di dati, gli allegati e il documento di record nella posizione di payload del flusso di lavoro o in una variabile. Se il flusso di lavoro è contrassegnato per l’archiviazione dati esterna e configurato per un’archiviazione dati esterna, è disponibile solo l’opzione della variabile. Puoi effettuare una selezione dall’elenco di variabili disponibili per il modello di flusso di lavoro. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni in una fase successiva e non al momento della creazione del flusso di lavoro, assicurati che siano presenti le configurazioni di variabili richieste.

>[!NOTE]
>
>  Scopri come [creare un modello di flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem) per definire la serie di passaggi eseguiti all’avvio del flusso di lavoro da parte di un utente. Puoi anche definire le proprietà del modello, ad esempio se il flusso di lavoro è transitorio o utilizza più risorse.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione delle richieste di moduli. Per ulteriori informazioni su queste opzioni, consulta [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md)  articolo.

## Vantaggi

Alcuni dei vantaggi dell’integrazione del flusso di lavoro AEM con Adaptive Forms sono:

* L’integrazione del flusso di lavoro AEM consente di automatizzare processi aziendali complessi che richiedono l’invio di moduli.
* Il flusso di lavoro dell’AEM supporta la logica condizionale, consentendo così decisioni dinamiche basate su dati modulo o fattori esterni.
* Flusso di lavoro AEM indirizza le attività in base a regole e condizioni predefinite, garantendo che le attività vengano assegnate ai singoli utenti o ai gruppi appropriati.

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## Integrare il flusso di lavoro AEM con Adaptive Forms {#steps-to-integrate-workflow-with-af}

Per impostare il processo automatizzato con [Flusso di lavoro AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem) per un modulo adattivo, effettua le seguenti operazioni:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fai clic su  **[!UICONTROL Invio]** scheda.
1. Dalla sezione **[!UICONTROL Azione di invio]** elenco a discesa, seleziona **[!UICONTROL Richiama un flusso di lavoro AEM]** .
   ![Configurazione dell’azione Invia e-mail](/help/forms/assets/configure-invoke-aem-workflow.png)

1. Seleziona modello flusso di lavoro da **[!UICONTROL Modello flusso di lavoro]** elenco a discesa.
1. Seleziona l’opzione dalla sezione **[!UICONTROL Archivia file di dati tramite]** elenco a discesa.

   **File di dati**: contiene i dati inviati al modulo adattivo. È possibile utilizzare **[!UICONTROL Percorso file di dati]** per specificare il nome del file e il percorso del file relativo al payload. Ad esempio, il `/addresschange/data.xml` percorso crea una cartella denominata `addresschange` e lo posiziona in relazione al payload. È inoltre possibile specificare solo `data.xml` per inviare solo i dati inviati senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

1. Seleziona l’opzione dalla sezione **[!UICONTROL Memorizza allegati tramite]** elenco a discesa.

   **Allegati**: puoi utilizzare la **[!UICONTROL Percorso allegato]** per specificare il nome della cartella in cui archiviare gli allegati caricati nel modulo adattivo. La cartella viene creata in relazione al payload. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

1. Seleziona l’opzione dalla sezione **[!UICONTROL Documenti di record che utilizzano]** elenco a discesa.

   **Documento record**: contiene il documento di record generato per il modulo adattivo. È possibile utilizzare **[!UICONTROL Percorso del documento record]** per specificare il nome del file del documento di record e il percorso del file relativo al payload. Ad esempio, il `/addresschange/DoR.pdf` percorso crea una cartella denominata `addresschange` relativo al payload e posiziona il `DoR.pdf` relativo al payload. È inoltre possibile specificare solo `DoR.pdf` per salvare solo un documento di record senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.
1. Clic **[!UICONTROL Fine]**.

>[!NOTE]
>
> Ulteriori informazioni su [Flussi di lavoro AEM incentrati su Forms - Riferimento alla fase per automatizzare i processi aziendali](/help/forms/aem-forms-workflow-step-reference.md).

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## Articoli correlati

{{af-submit-action}}