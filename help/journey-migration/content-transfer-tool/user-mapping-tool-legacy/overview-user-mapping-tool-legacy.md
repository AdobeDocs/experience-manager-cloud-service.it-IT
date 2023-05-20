---
title: Panoramica sullo strumento di mappatura utente (Legacy)
description: Panoramica sullo strumento di mappatura utenti (legacy)
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: 8a258c2c929f9af84a1cde99072291a3e7f6cfc3
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 88%

---

# Panoramica sullo strumento di mappatura utenti (legacy) {#overview-user-mapping-tool}

>[!INFO]
>
>Questa documentazione fa riferimento a una versione obsoleta dello strumento. Per ulteriori informazioni sull’ultima versione, consulta [Mappatura utenti e migrazione entità](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

<!-- Alexandru: drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## Introduzione {#introduction}

Come parte del percorso di transizione ad Adobe Experience Manager (AEM) as a Cloud Service, devi spostare gli utenti e i gruppi dal sistema AEM esistente ad AEM as a Cloud Service. Questa operazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Una modifica importante per AEM as a Cloud Service è l’utilizzo completamente integrato degli Adobe ID per accedere al livello di authoring.  A tal fine è necessario utilizzare [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS), che fornisce un accesso singolo a tutte le applicazioni cloud di Adobe. Per ulteriori informazioni, consultare [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=it#identity-management). A causa di questo cambiamento, gli utenti e i gruppi esistenti devono essere mappati ai loro ID IMS per evitare che utenti e gruppi siano duplicati nell’istanza di authoring del Cloud Service.

## Strumento di mappatura utente {#mapping-tool}

Lo strumento Content Transfer (senza mappatura utente) eseguirà la migrazione di tutti gli utenti e i gruppi associati al contenuto in corso di migrazione. Lo strumento di mappatura utente fa parte dello strumento Content Transfer (Trasferimento contenuti) e il suo unico scopo è modificare gli utenti in modo che possano essere riconosciuti correttamente da IMS, la funzionalità ad accesso singolo utilizzata da AEM as a Cloud Service. Una volta apportate queste modifiche, lo strumento Content Transfer (Trasferimento contenuti) esegue la migrazione degli utenti e dei gruppi del contenuto specificato secondo la procedura comune.

### Passaggio successivo {#whats-next}

Dopo aver appreso l’uso di uno strumento di mappatura utente, è ora possibile esaminare considerazioni importanti e casi eccezionali prima di utilizzare lo strumento di mappatura utente. Consultare [Considerazioni importanti sullo strumento di mappatura utente](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) per ulteriori dettagli.
