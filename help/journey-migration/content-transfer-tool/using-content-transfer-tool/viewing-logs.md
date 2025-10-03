---
title: Visualizzazione dei registri di un set di migrazione nello strumento Content Transfer (Trasferimento contenuti)
description: Visualizzazione dei registri di un set di migrazione nello strumento Content Transfer (Trasferimento contenuti)
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
feature: Migration
role: Admin
source-git-commit: 91f9bcafc087b6f9329d7a47509cc659714705ff
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 36%

---

# Visualizzazione dei registri di un set di migrazione {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visualizzazione dei registri"
>abstract="Al termine dell’estrazione dell’acquisizione, verifica la presenza di eventuali errori o avvisi nei registri. Eventuali errori devono essere risolti immediatamente affrontando i problemi segnalati o contattando il supporto Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=it#troubleshooting" text="Risoluzione di problemi"
>additional-url="https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html" text="Contattare il supporto Adobe"

Al completamento di ogni passaggio (estrazione e acquisizione), controlla i registri e cerca gli errori.  Eventuali errori devono essere risolti immediatamente affrontando i problemi segnalati o contattando il supporto Adobe.

## Passaggi per visualizzare i registri {#viewing-logs}

### Registri di estrazione

Per visualizzare i registri di estrazione, passa all’istanza Adobe Experience Manager di origine, quindi seleziona il set di migrazione desiderato.

Quindi, segui i passaggi seguenti:

1. Seleziona un set di migrazione e fai clic su **Visualizza registro** nella barra delle azioni. Viene visualizzata la finestra di dialogo Registri. Fai clic su **Registro estrazione** per visualizzare i registri in una nuova scheda.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/logs.png) \
   Oppure fai clic sullo stato **FINISHED** per visualizzare i registri in una nuova scheda.

1. Per visualizzare i registri senza utilizzare l’interfaccia utente, puoi accedere all’ambiente AEM sorgente tramite SSH e visualizzare il `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

### Registri di acquisizione

Per visualizzare i registri di acquisizione, passare all&#39;elenco Processi di acquisizione in Cloud Acceleration Manager, quindi individuare il processo di migrazione desiderato e fare clic sui tre punti (**...**) del processo. Puoi quindi fare clic su **Scarica registro** per scaricare i registri.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
