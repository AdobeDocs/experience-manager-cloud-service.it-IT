---
title: Come si creano e gestiscono le revisioni di Adaptive Forms incorporate o create nella pagina Sites?
description: La revisione è un meccanismo che consente al revisore di eseguire diverse attività per i moduli adattivi utilizzando la fase Assegna attività.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 7e3eb3426002408a90e08bee9c2a8b7a7bfebb61
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 4%

---


# Creare e gestire recensioni per un modulo adattivo {#review-step-forms-aem-sites-page}

Utilizzo di [Assegna passaggio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) del flusso di lavoro dell’AEM, il revisore esamina il modulo inviato ed esegue un’azione su di esso. Per rivedere il modulo inviato tramite il passaggio Assegna attività, eseguire la procedura seguente:

1. [Creare un flusso di lavoro AEM](#create-an-aem-workflow)
1. [Configurare l’azione di invio del contenitore Modulo adattivo](#configure-submit-action)
1. [Inviare un modulo adattivo dopo la revisione](#submit-af-after-review)

## Creare un flusso di lavoro AEM {#create-an-aem-workflow}

1. Apri l’istanza di authoring in modalità di modifica.
1. Vai a **[!UICONTROL Strumenti]** >  **[!UICONTROL Flusso di lavoro]** >  **[!UICONTROL Modelli]** > **[!UICONTROL Crea]** > **[!UICONTROL Crea modello]**
1. Specifica il titolo del flusso di lavoro e aggiungi **[Assegna attività]** passaggio
1. Tocca ![icona_impostazioni](assets/settings_icon.png) sulla barra delle azioni. Il **[!UICONTROL Assegna attività]** viene visualizzata una finestra di dialogo.
1. Apri [!UICONTROL Modulo e documento] scheda e apri [!UICONTROL Prepopolato] e specificare:

   * Seleziona file di dati di input tramite
   * Seleziona allegati di input tramite

   ![Passaggio di revisione](/help/forms/assets/assigntask-review1.gif)

1. Apri **[!UICONTROL Assegnatario]** scheda e apri [!UICONTROL Prepopolato] e specificare **[!UICONTROL Assegna opzioni]**:

   ![Passaggio di revisione](/help/forms/assets/review-assignstep.png)

1. Per salvare le modifiche, fai clic su **[!UICONTROL Completati]**.

## Configura azione di invio {#configure-submit-action}

Ora configura l’azione Invia di un componente Contenitore modulo adattivo sulla pagina del sito:

1. Passa alla pagina del sito.
1. Tocca ![icona_impostazioni](assets/settings_icon.png) di un contenitore di moduli adattivi. Il **[!UICONTROL Contenitore modulo adattivo]** viene visualizzata una finestra di dialogo.
1. Apri **[!UICONTROL Invio]** e specifica **[!UICONTROL Azione di invio]** a [Richiama un flusso di lavoro AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. Clic [Fine] per salvare le impostazioni.

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## Inviare un modulo adattivo dopo la revisione {#submit-af-after-review}

Per rivedere e confermare il modulo adattivo inviato:

1. Vai a [!UICONTROL Strumenti] >  [!UICONTROL Flusso di lavoro] >  [!UICONTROL Istanze]
1. Nella casella in entrata è possibile vedere che è in corso la creazione di un&#39;istanza.
1. Seleziona l’istanza e fai clic su [!UICONTROL Apri].
1. A questo punto è possibile visualizzare il modulo inviato.

Il revisore esegue azioni diverse come:

* **Invia**: il revisore compila il modulo e lo invia per l’ulteriore elaborazione.
* **Salva**: il revisore salva il modulo nello stato corrente senza inviarlo.
* **Reimposta**: il revisore cancella tutte le modifiche apportate al modulo e lo ripristina allo stato originale.
* **Delega**: il revisore trasferisce la proprietà del modulo a un’altra persona per ulteriori azioni o revisioni.
