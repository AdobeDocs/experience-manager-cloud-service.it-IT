---
title: Panoramica sullo strumento di mappatura utente (legacy)
description: Panoramica sullo strumento di mappatura utente (legacy)
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 21%

---


# Panoramica sullo strumento di mappatura utente (legacy) {#overview-user-mapping-tool}

>[!INFO]
>
>Questa documentazione fa riferimento a una versione obsoleta dello strumento. Per ulteriori informazioni sull&#39;ultima versione, vedere [Migrazione gruppo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

<!-- Alexandru: drafting this for now

NOTE: "LEGACY" for user mapping includes everything before (that is, not including) 2.0.16 of CTT.

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=it#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=it#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## Introduzione {#introduction}

Come parte del percorso di transizione ad Adobe Experience Manager (AEM) as a Cloud Service, devi spostare utenti e gruppi dal sistema AEM esistente ad AEM as a Cloud Service. Questa migrazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Una modifica importante per AEM as a Cloud Service è l’utilizzo completamente integrato degli Adobe ID per accedere al livello di authoring. Questa integrazione richiede l&#39;utilizzo di [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS) che fornisce il single sign-on in tutte le applicazioni cloud Adobe. Per ulteriori dettagli, vedere [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=it#identity-management). A causa di questa modifica, gli utenti e i gruppi esistenti devono essere mappati ai loro ID IMS per evitare di duplicare gli utenti e i gruppi nell’istanza di authoring di Cloud Service.

## Strumento di mappatura utente {#mapping-tool}

Lo strumento Content Transfer (Trasferimento contenuti) (senza mappatura utenti) esegue la migrazione di tutti gli utenti e i gruppi associati al contenuto da migrare. Lo strumento di mappatura utenti fa parte dello strumento Content Transfer (Trasferimento contenuti). Il suo unico scopo è modificare gli utenti in modo che vengano riconosciuti correttamente da IMS, la funzionalità single sign-on utilizzata da AEM as a Cloud Service. Al termine di queste modifiche, lo strumento Content Transfer (Trasferimento contenuti) migra gli utenti e i gruppi del contenuto specificato come di consueto.

### Passaggio successivo {#whats-next}

Dopo aver appreso l’uso di uno strumento di mappatura utente, è ora possibile esaminare considerazioni importanti e casi eccezionali prima di utilizzare lo strumento di mappatura utente. Consultare [Considerazioni importanti sullo strumento di mappatura utente](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) per ulteriori dettagli.
