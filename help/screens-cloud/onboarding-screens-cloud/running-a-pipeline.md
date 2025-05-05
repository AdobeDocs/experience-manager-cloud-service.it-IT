---
title: Esecuzione di una pipeline
description: Questa pagina descrive l’esecuzione di una pipeline per Screens come progetto di Cloud Service in Cloud Manager.
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# Esecuzione di una pipeline per il programma Screens as a Cloud Service in Cloud Manager {#run-pipeline-screens-cloud}

Questa sezione descrive come eseguire la pipeline e distribuire il codice per il programma in Cloud Manager.

>[!NOTE]
>Consulta [Configurazione della pipeline CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=it) e [Distribuire il codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=it) per scoprire come eseguire la pipeline per il programma in Cloud Manager.

## Obiettivo {#objective}

La sezione seguente descrive come configurare la pipeline CI/CD e distribuire il codice per il programma in Cloud Manager.

## Passaggi per eseguire una pipeline per il progetto Screens in Cloud Manager {#steps-branch-creation}

1. Una volta completata la configurazione dell&#39;ambiente, l&#39;aggiornamento della scheda di invito all&#39;azione viene visualizzato nella pagina **Panoramica** di Cloud Manager.

   ![immagine](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Fare clic su **Configura pipeline** dalla pagina **Panoramica**.

1. Fai clic su **Avanti** dopo aver selezionato il ramo.

   ![immagine](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Seleziona le opzioni dalla procedura guidata **Configura pipeline**. Fai clic su **Salva**.

   >[!NOTE]
   >Per informazioni sulle opzioni della procedura guidata Configura pipeline, vedere [Configurazione delle impostazioni della pipeline da Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=it) per ulteriori dettagli.

   ![immagine](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. Una volta completata la pipeline di configurazione, la scheda di invito all’azione viene aggiornata.

   >[!NOTE]
   >Per ulteriori informazioni sulle fasi della distribuzione in Cloud Manager, vedere [Distribuzione del codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=it).

   ![immagine](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Fare clic su **Distribuisci**.

1. Fare clic su **Build** per avviare il processo di compilazione.

   ![immagine](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. Al termine del processo di compilazione, puoi visualizzare un collegamento a Author dalla scheda **Ambienti** della pagina **Panoramica** di Cloud Manager.

   ![immagine](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## Passaggio successivo {#whats-next}

Dopo aver appreso come configurare un ambiente per il programma in Cloud Manager, è possibile passare alla fase successiva del processo di onboarding: [Accesso al provider di servizi Screens](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
