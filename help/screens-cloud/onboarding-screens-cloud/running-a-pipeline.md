---
title: Esecuzione di una pipeline
description: Questa pagina descrive l’esecuzione di una pipeline per Screens come progetto di Cloud Service in Cloud Manager.
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# Esecuzione di una pipeline per il programma as a Cloud Service Screens in Cloud Manager {#run-pipeline-screens-cloud}

Questa sezione descrive come eseguire la pipeline e distribuire il codice per il programma in Cloud Manager.

>[!NOTE]
>Consulta [Configurazione della pipeline CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html) e [Implementare il codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html) per scoprire come eseguire la pipeline per il programma in Cloud Manager.

## Obiettivo {#objective}

La sezione seguente descrive come configurare la pipeline CI/CD e distribuire il codice per il programma in Cloud Manager.

## Passaggi per eseguire una pipeline per il progetto Screens in Cloud Manager {#steps-branch-creation}

1. Una volta completata correttamente la configurazione dell’ambiente, l’aggiornamento della scheda di invito all’azione viene visualizzato nel file di **Panoramica** pagina.

   ![immagine](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Clic **Configurare la pipeline** dal **Panoramica** pagina.

1. Clic **Successivo** dopo aver selezionato il ramo.

   ![immagine](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Seleziona le opzioni dalla **Configurare la pipeline** procedura guidata. Fai clic su **Salva**.

   >[!NOTE]
   >Per informazioni sulle opzioni della procedura guidata Configura pipeline, consulta [Configurazione delle impostazioni della pipeline da Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html) per ulteriori dettagli.

   ![immagine](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. Una volta completata la pipeline di configurazione, la scheda di invito all’azione viene aggiornata.

   >[!NOTE]
   >Per informazioni sulle fasi di implementazione in Cloud Manager, consulta [Implementazione del codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html) per ulteriori dettagli.

   ![immagine](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Clic **Distribuisci**.

1. Clic **Genera** per avviare il processo di compilazione.

   ![immagine](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. Al termine del processo di generazione, puoi visualizzare un collegamento di authoring dall’ **Ambienti** Scheda dalla scheda di Cloud Manager **Panoramica** pagina.

   ![immagine](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## Passaggio successivo {#whats-next}

Dopo aver appreso come configurare un ambiente per il programma in Cloud Manager, puoi procedere con il passaggio successivo nel processo di onboarding: [Navigazione al provider di servizi Screens](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
