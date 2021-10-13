---
title: Visualizzazione dei registri di un set di migrazione nello strumento Content Transfer (Trasferimento contenuti)
description: Visualizzazione dei registri di un set di migrazione nello strumento Content Transfer (Trasferimento contenuti)
source-git-commit: 5b569ab1b1cca7e5ec46b872f8726fddfc8b8d14
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 52%

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

Puoi visualizzare i registri di un set di migrazione esistente nella pagina *Overview* (Panoramica).
Effettua le seguenti operazioni:

1. Nella pagina *Overview* (Panoramica), seleziona il set di migrazione da eliminare e fai clic su **View Log** (Visualizza registro) nella barra delle azioni.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. Viene visualizzata la finestra di dialogo **Logs** (Registri). Fai clic su **Extraction Logs** (Registri di estrazione) per visualizzare i registri in una nuova scheda.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
Oppure,

   Puoi visualizzare i registri del set di migrazione anche nella schermata *Overview* (Panoramica). Seleziona il set di migrazione e fai clic sullo stato nel campo **EXTRACTION** (ESTRAZIONE). In questo caso, fai clic su **COMPLETATO** per visualizzare i registri in una nuova scheda.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. Per visualizzare i registri senza utilizzare l’interfaccia utente, puoi accedere all’ambiente AEM sorgente tramite SSH e visualizzare il `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.
