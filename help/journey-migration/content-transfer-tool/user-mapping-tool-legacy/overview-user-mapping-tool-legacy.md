---
title: Panoramica sullo strumento di mappatura utenti (legacy)
description: Panoramica sullo strumento di mappatura utenti (legacy)
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: 69dfe7f98628ab67cc3a994c32b1530550ec6a01
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 11%

---

# Panoramica sullo strumento di mappatura utenti {#overview-user-mapping-tool}


<!-- Alexandru: drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## Introduzione {#introduction}

Come parte del percorso di transizione verso Adobe Experience Manager (AEM) as a Cloud Service, è necessario spostare utenti e gruppi dal sistema AEM esistente a AEM as a Cloud Service. Questa operazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Una modifica importante per AEM as a Cloud Service è l’utilizzo completamente integrato degli Adobe ID per accedere al livello di authoring.  A tal fine è necessario utilizzare [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per gestire utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate nell’Adobe Identity Management System (IMS) che fornisce il single sign-on in tutte le applicazioni cloud Adobe. Per ulteriori informazioni, consulta [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). A causa di questa modifica, gli utenti e i gruppi esistenti devono essere mappati ai loro ID IMS per evitare di duplicare utenti e gruppi nell’istanza di authoring del Cloud Service.

## Strumento di mappatura utente {#mapping-tool}

Lo strumento Content Transfer (Trasferimento contenuti) (senza mappatura utenti) eseguirà la migrazione di tutti gli utenti e i gruppi associati al contenuto da migrare. Lo strumento di mappatura utenti fa parte dello strumento Content Transfer (Trasferimento contenuti) e il suo unico scopo è quello di modificare gli utenti in modo che possano essere riconosciuti correttamente da IMS, la funzionalità single sign-on utilizzata dagli as a Cloud Service AEM. Al termine di queste modifiche, lo strumento Content Transfer (Trasferimento contenuti) migra gli utenti e i gruppi del contenuto specificato come di consueto.

### Passaggio successivo {#whats-next}

Dopo aver appreso cos’è uno strumento di mappatura utenti, puoi rivedere considerazioni importanti e casi eccezionali prima di utilizzare lo strumento di mappatura utenti. Consulta [Considerazioni importanti per lo strumento di mappatura utenti](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) per ulteriori dettagli.
