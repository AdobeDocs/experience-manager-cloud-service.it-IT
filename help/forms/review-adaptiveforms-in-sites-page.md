---
title: Come si invia un modulo adattivo per la revisione? Come si gestiscono le recensioni per un modulo adattivo AEM?
description: La revisione è un meccanismo che consente al revisore di eseguire diverse attività per i moduli adattivi utilizzando la fase Assegna attività.
feature: Adaptive Forms
hide: true
hidefromtoc: true
role: User
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---


# Creare e gestire recensioni per un modulo adattivo {#review-step-forms-aem-sites-page}

Utilizzando il [Passaggio assegnazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?lang=it#assign-task-step) del flusso di lavoro AEM, il revisore esamina il modulo inviato ed esegue azioni su di esso. Per rivedere il modulo inviato tramite il passaggio Assegna attività, eseguire la procedura seguente:

1. [Creare un flusso di lavoro AEM](#create-an-aem-workflow)
1. [Configurare l’azione di invio del contenitore Modulo adattivo](#configure-submit-action)
1. [Invia un modulo adattivo dopo la revisione](#submit-af-after-review)

## Creare un flusso di lavoro AEM {#create-an-aem-workflow}

1. Apri l’istanza di authoring in modalità di modifica.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** > **[!UICONTROL Crea]** > **[!UICONTROL Crea modello]**
1. Specifica il titolo del flusso di lavoro e aggiungi il passaggio **[Assegna attività]**
1. Seleziona ![icona_impostazioni](assets/settings_icon.png) nella barra delle azioni. Viene visualizzata la finestra di dialogo **[!UICONTROL Assegna attività]**.
1. Apri la scheda [!UICONTROL Modulo e documento], apri il menu a discesa [!UICONTROL Precompilato] e specifica:

   * Seleziona file di dati di input tramite
   * Seleziona allegati di input tramite

   ![Passaggio di revisione](/help/forms/assets/assigntask-review1.gif)

1. Apri la scheda **[!UICONTROL Assegnatario]** e apri l&#39;elenco a discesa [!UICONTROL Prepopolato] e specifica **[!UICONTROL Assegna opzioni]**:

   ![Passaggio di revisione](/help/forms/assets/review-assignstep.png)

1. Per salvare le modifiche, fai clic su **[!UICONTROL Completati]**.

## Configura azione di invio {#configure-submit-action}

Ora configura l’azione Invia di un componente Contenitore modulo adattivo sulla pagina del sito:

1. Passa alla pagina del sito.
1. Seleziona ![icona_impostazioni](assets/settings_icon.png) di un contenitore di moduli adattivi. Viene visualizzata la finestra di dialogo **[!UICONTROL Contenitore modulo adattivo]**.
1. Apri la scheda **[!UICONTROL Invio]** e specifica **[!UICONTROL Azione di invio]** per [Richiama un flusso di lavoro AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=it#invoke-an-aem-workflow)

1. Fai clic su [Fine] per salvare le impostazioni.

![inoltroscheda-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## Inviare un modulo adattivo dopo la revisione {#submit-af-after-review}

Per rivedere e confermare il modulo adattivo inviato:

1. Vai a [!UICONTROL Strumenti] > [!UICONTROL Flusso di lavoro] > [!UICONTROL Istanze]
1. Nella casella in entrata è possibile vedere che è in corso la creazione di un&#39;istanza.
1. Selezionare l&#39;istanza e fare clic su [!UICONTROL Apri].
1. A questo punto è possibile visualizzare il modulo inviato.

Il revisore esegue azioni diverse come:

* **Invia**: il revisore completa il modulo e lo invia per l&#39;ulteriore elaborazione.
* **Salva**: il revisore salva il modulo nello stato corrente senza inviarlo.
* **Ripristina**: il revisore cancella tutte le modifiche apportate al modulo e lo ripristina allo stato originale.
* **Delega**: il revisore trasferisce la proprietà del modulo a un&#39;altra persona per ulteriori azioni o revisioni.
