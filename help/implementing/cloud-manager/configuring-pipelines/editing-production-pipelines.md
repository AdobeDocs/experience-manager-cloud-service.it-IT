---
title: Modifica di una pipeline di produzione
description: Modifica di una pipeline di produzione
index: false
source-git-commit: b9d28088ad18a389108ebfb81aa750c63e637922
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Modifica di una pipeline di produzione {#edit-prod-pipeline}

Puoi modificare le configurazioni della pipeline dalla sezione **Panoramica del programma** pagina.

Per modificare la pipeline configurata, effettua le seguenti operazioni:

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Fai clic su **...** dal **Tubi** scheda e fai clic su **Modifica**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. La **Modifica pipeline di produzione** viene visualizzata la finestra di dialogo.

   1. La **Configurazione** consente di aggiornare **Nome della pipeline**, **Trigger distribuzione** e **Comportamento di errore delle metriche importanti**.

      >[!NOTE]
      >Vedi [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. La **Origine** scheda ti offre un’opzione per selezionare o deselezionare **Sospendi prima dell’implementazione in produzione** e **Pianificato** opzioni da **Opzioni di distribuzione della produzione**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. La **Audit delle esperienze** consente di aggiornare o aggiungere nuove pagine.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. Fai clic su **Aggiorna** una volta completata la modifica della pipeline.

## Azioni aggiuntive della pipeline di produzione {#additional-prod-actions}

### Esecuzione di una pipeline di produzione {#run-prod}

Puoi eseguire la pipeline di produzione dalla scheda Pipelines :

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Fai clic su **...** dal **Tubi** scheda e fai clic su **Esegui**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

### Eliminazione di una pipeline di produzione {#delete-prod}

Puoi eliminare la pipeline di produzione dalla scheda Pipelines :

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Fai clic su **...** dal **Tubi** scheda e fai clic su **Elimina**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >Un utente con il ruolo di Deployment Manager ora può eliminare la pipeline di produzione in modo self-service tramite il **Elimina** dalla scheda Pipeline.