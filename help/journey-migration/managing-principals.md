---
title: Gestione delle entità
description: Gestione delle entità di migrazione tramite Admin Console
source-git-commit: 5bf497fb2122cc3d3ff0903aeb680a35e90f33b0
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Gestione delle entità {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="Gestione delle entità"
>abstract="Scopri cosa è necessario fare per gestire gli utenti durante o dopo una migrazione dei contenuti"

Prima del trasferimento dei contenuti all’ambiente cloud AEM as a Cloud Service, è possibile eseguire alcune attività sull’Admin Console.  Si tratta dei seguenti elementi: creazione di utenti, gruppi e assegnazione di utenti ai gruppi; questi utenti e gruppi saranno presenti in IMS, il servizio Identity Management di Adobe, utilizzato per gestire utenti e gruppi per tutti i servizi basati su cloud di Adobe.

### Creazione di gruppi e dei relativi utenti in Admin Console

[L&#39;utilizzo di Admin Console per le entità AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up) fornisce istruzioni dettagliate sulla creazione di utenti e gruppi in IMS e su come aggiungere gli utenti ai gruppi contemporaneamente o successivamente.  Il documento include tre opzioni per la creazione: manualmente tramite l’Admin Console, tramite il caricamento CSV tramite l’Admin Console e tramite uno strumento User Sync.

L’opzione manuale consente di creare un gruppo o un utente alla volta; il caricamento CSV consente di creare e collegare più utenti e gruppi contemporaneamente; e lo strumento User Sync consente di utilizzare un IDP esistente per creare e gestire gli utenti e i gruppi IMS.

Una volta che un utente utilizza IMS per accedere all’AEM, viene creata una sua rappresentazione AEM.  Inoltre, tutti i gruppi IMS in cui si trova l’utente avranno gruppi AEM equivalenti creati nell’AEM.  Questi utenti e gruppi AEM creati da IMS sono ancora gestiti principalmente utilizzando l’Admin Console.

Una volta completata la migrazione dei contenuti, in genere i gruppi IMS devono disporre di alcune configurazioni aggiuntive per poter accedere ai contenuti migrati.  Vedi [Migrazione delle entità dopo la migrazione](/help/journey-migration/managing-principals-after-migration.md)

Per ulteriori informazioni sull&#39;integrazione e l&#39;amministrazione di utenti e gruppi AEM e IMS, consulta anche l&#39;[esercitazione, Utenti, gruppi e autorizzazioni AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions).