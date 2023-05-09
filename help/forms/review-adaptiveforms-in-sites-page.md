---
title: Creazione e gestione di revisioni di Adaptive Forms incorporate o create nella pagina Sites
seo-title: Review is a mechanism that allows reviewer to perform different tasks for adaptive forms using Assign Task step
description: La revisione è un meccanismo che consente al revisore di eseguire diverse attività per i moduli adattivi utilizzando la fase Assegna attività
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: daeb407e27b9f1d390fe40151ca16ec0196712e6
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 4%

---


# Passaggio di revisione per Forms nella pagina del sito {#review-step-forms-aem-sites-page}

Utilizzo della [Assegna passaggio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) del flusso di lavoro AEM, il revisore esamina il modulo inviato ed esegue azioni al riguardo. Per esaminare il modulo inviato utilizzando la fase Assegna attività, attenersi alla procedura descritta di seguito.

1. [Creare un flusso di lavoro AEM](#create-an-aem-workflow)
1. [Configurare l’azione di invio del contenitore Modulo adattivo](#configure-submit-action)
1. [Invia un modulo adattivo dopo la revisione](#submit-af-after-review)

## Creare un flusso di lavoro AEM {#create-an-aem-workflow}

1. Apri l’istanza di authoring in modalità di modifica.
1. Vai a **[!UICONTROL Strumenti]** >  **[!UICONTROL Flusso di lavoro]** >  **[!UICONTROL Modelli]** > **[!UICONTROL Crea]** > **[!UICONTROL Crea modello]**
1. Specifica il titolo del flusso di lavoro e aggiungi il **[Assegna attività]** step
1. Tocca ![settings_icon](assets/settings_icon.png) sulla barra delle azioni. La **[!UICONTROL Assegna attività]** viene visualizzata la finestra di dialogo .
1. Apri [!UICONTROL Modulo e documento] scheda e apri [!UICONTROL Prepopolato] e specifica:

   * Seleziona file di dati di input tramite
   * Seleziona allegati di input tramite

   ![Passaggio di revisione](/help/forms/assets/assigntask-review1.gif)

1. Apri **[!UICONTROL Assegnatario]** scheda e apri [!UICONTROL Prepopolato] a discesa e specifica **[!UICONTROL Opzioni di assegnazione]**:

   ![Passaggio di revisione](/help/forms/assets/review-assignstep.png)

1. Per salvare le modifiche, fai clic su **[!UICONTROL Completati]**.

## Configurare l’azione Invia {#configure-submit-action}

Ora configura l’azione Invia di un componente Contenitore di modulo adattivo nella pagina del sito :

1. Vai alla pagina del sito.
1. Tocca ![settings_icon](assets/settings_icon.png) di un contenitore Modulo adattivo. La **[!UICONTROL Contenitore di moduli adattivi]** viene visualizzata la finestra di dialogo .
1. Apri **[!UICONTROL Invio]** scheda e specifica **[!UICONTROL Invia azione]** a [Richiamare un flusso di lavoro AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. Fai clic su [Fine] per salvare le impostazioni.

![sottomissione tab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## Invia un modulo adattivo dopo la revisione {#submit-af-after-review}

Per esaminare e confermare il modulo adattivo inviato:

1. Vai a [!UICONTROL Strumenti] >  [!UICONTROL Flusso di lavoro] >  [!UICONTROL Istanze]
1. Nella casella in entrata è possibile vedere che è in corso la creazione di un’istanza.
1. Seleziona l’istanza e fai clic su [!UICONTROL Apri].
1. Ora è possibile visualizzare il modulo inviato.

Il revisore esegue diverse azioni come:

* **Invia**: Il revisore completa il modulo e lo invia per ulteriore elaborazione.
* **Salva**: Il revisore salva il modulo nello stato corrente senza inviarlo.
* **Reimposta**: Il revisore cancella tutte le modifiche apportate al modulo e lo ripristina allo stato originale.
* **Delega**: Il revisore trasferisce la proprietà del modulo a un’altra persona per ulteriori azioni o revisioni.
