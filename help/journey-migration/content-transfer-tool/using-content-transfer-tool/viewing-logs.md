---
title: Visualizzazione dei registri di un set di migrazione nello strumento Content Transfer (Trasferimento contenuti)
description: Visualizzazione dei registri di un set di migrazione nello strumento Content Transfer (Trasferimento contenuti)
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: 9a098eefbb730ae2930169cf7402ab4799043291
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 12%

---

# Visualizzazione dei registri di un set di migrazione {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visualizzazione dei registri"
>abstract="Al termine dell’estrazione dell’acquisizione, controlla i registri per eventuali errori/avvisi. Eventuali errori devono essere risolti immediatamente sia affrontando i problemi segnalati sia contattando il supporto Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="Risoluzione dei problemi"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="Contattare il supporto Adobe"

Al completamento di ogni passaggio (estrazione e acquisizione) controlla i registri e cerca gli errori.  Eventuali errori devono essere risolti immediatamente sia affrontando i problemi segnalati sia contattando il supporto Adobe.

## Passaggi per la visualizzazione dei registri {#viewing-logs}

Per visualizzare i registri di estrazione, passa all’istanza Adobe Experience Manager sorgente, quindi seleziona il set di migrazione desiderato.

Quindi, segui i passaggi seguenti:

1. Seleziona un set di migrazione e fai clic su **Visualizza registro** dalla barra delle azioni. Verrà visualizzata la finestra di dialogo Registri. Fai clic su **Registro di estrazione** per visualizzare i registri in una nuova scheda.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   Oppure, fai clic sul pulsante **COMPLETATO** stato per visualizzare i registri in una nuova scheda.

1. Per visualizzare i registri senza utilizzare l’interfaccia utente, puoi accedere all’ambiente AEM sorgente tramite SSH e visualizzare il `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

1. Per visualizzare i registri di acquisizione, vai all’elenco Processi di acquisizione in Cloud Acceleration Manager e fai clic sui tre punti (**...**). Puoi quindi fare clic su **Scarica registro** per scaricare i registri.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
