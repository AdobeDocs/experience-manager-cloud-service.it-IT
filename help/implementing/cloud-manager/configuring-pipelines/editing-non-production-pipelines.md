---
title: Modifica di una pipeline non di produzione
description: Modifica di una pipeline non di produzione
index: false
source-git-commit: 881b4d75a15af55aaf1203e8d673059aab15b793
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Modifica di una pipeline non di produzione {#edit-non-prod-pipeline}

Puoi modificare le configurazioni della pipeline dalla sezione **Scheda pipeline** da **Panoramica del programma** pagina.

>[!IMPORTANT]
>Non è possibile modificare una pipeline in esecuzione.

Per modificare la pipeline non di produzione configurata, effettua le seguenti operazioni:

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Seleziona la pipeline non di produzione e fai clic su **...**. Fai clic su **Modifica**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. La **Modifica pipeline di produzione** viene visualizzata la finestra di dialogo.

   1. La **Configurazione** consente di aggiornare **Nome della pipeline**, **Trigger distribuzione** e **Comportamento di errori di metrica importanti**.

      >[!NOTE]
      >Vedi [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. La **Codice sorgente** consente di aggiornare **Archivio** e **Ramo Git**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. Fai clic su **Aggiorna** una volta completata la modifica della pipeline non di produzione.

## Azioni aggiuntive di pipeline non di produzione {#additional-nonprod-actions}

### Esecuzione di una pipeline non di produzione {#run-nonprod}

Puoi eseguire la pipeline di produzione dalla scheda Pipelines :

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Fai clic su **...** dal **Tubi** scheda e fai clic su **Esegui**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### Eliminazione di una pipeline non di produzione {#delete-nonprod}

Puoi eliminare la pipeline di produzione dalla scheda Pipelines :

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Fai clic su **...** dal **Tubi** scheda e fai clic su **Elimina**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)
