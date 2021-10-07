---
title: Panoramica sullo strumento di mappatura utente
description: Panoramica sullo strumento di mappatura utente
source-git-commit: 9d131daf5b6a0b1530ebff48627f6130ef716f3e
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---


# Panoramica sullo strumento di mappatura utente {#overview-user-mapping-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Strumento di mappatura utente"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) consente di spostare gli utenti e i gruppi dal sistema AEM esistente a AEM as a Cloud Service. Gli utenti e i gruppi esistenti devono essere mappati ai loro ID IMS per evitare utenti e gruppi duplicati nell’istanza di authoring del Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Considerazioni importanti sull’utilizzo dello strumento di mappatura utente"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Utilizzo dello strumento di mappatura utente"

## Introduzione {#introduction}

Come parte del percorso di transizione as a Cloud Service ad Adobe Experience Manager (AEM), devi spostare gli utenti e i gruppi dal sistema di AEM esistente a AEM as a Cloud Service. Questa operazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Una modifica importante AEM as a Cloud Service è l’utilizzo completamente integrato degli ID Adobe per accedere al livello di authoring.  Questo richiede l&#39;utilizzo di [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS), che fornisce il single sign-on in tutte le applicazioni cloud di Adobe. Per ulteriori informazioni, consulta [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). A causa di questa modifica, gli utenti e i gruppi esistenti devono essere mappati ai loro ID IMS per evitare di duplicare utenti e gruppi nell’istanza di authoring del Cloud Service.

## Strumento di mappatura utente {#mapping-tool}

Lo strumento Content Transfer (senza User Mapping) eseguirà la migrazione di tutti gli utenti e i gruppi associati al contenuto in corso di migrazione. Lo strumento di mappatura utenti fa parte dello strumento Content Transfer (Trasferimento contenuti) e il suo unico scopo è modificare gli utenti e i gruppi in modo che possano essere riconosciuti correttamente da IMS, la funzionalità single sign-on utilizzata da AEM as a Cloud Service. Una volta apportate queste modifiche, lo strumento Content Transfer (Trasferimento contenuti) esegue la migrazione usuale degli utenti e dei gruppi del contenuto specificato.
