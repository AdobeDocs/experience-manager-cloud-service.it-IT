---
title: Gestione delle entità principali
description: Gestione delle entità principali per la migrazione tramite Admin Console
exl-id: a75598d0-8f59-466b-984e-dfe527388c2a
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Gestione delle entità principali {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="Gestione delle entità principali"
>abstract="Impara a gestire gli utenti durante o dopo una migrazione dei contenuti"

Prima del trasferimento dei contenuti all’ambiente cloud AEM as a Cloud Service, è possibile eseguire alcune attività su Admin Console.  Si tratta di: creare utenti, gruppi e assegnare utenti a gruppi; questi utenti e gruppi esistono in IMS, il servizio Identity Management di Adobe, utilizzato per gestire utenti e gruppi per tutti i servizi basati su cloud di Adobe.

## Creazione di gruppi e dei relativi utenti in Admin Console

[L’utilizzo di Admin Console per le entità principali di AEM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up) fornisce istruzioni dettagliate sulla creazione di utenti e gruppi in IMS e su come aggiungere gli utenti ai gruppi contemporaneamente o successivamente.  Il documento include tre opzioni per la creazione: manualmente tramite Admin Console, caricando il file CSV in Admin Console e con uno strumento User Sync.

L’opzione manuale consente di creare un gruppo o un utente alla volta; caricando il file CSV si possono creare e collegare più utenti e gruppi contemporaneamente; e lo strumento User Sync permette di utilizzare un IDP esistente per creare e gestire gli utenti e i gruppi IMS.

Quando un utente utilizza IMS per accedere ad AEM, viene creata una sua rappresentazione AEM.  Inoltre, tutti i gruppi IMS in cui si trova l’utente avranno gruppi AEM equivalenti creati in AEM.  Questi utenti e gruppi AEM creati da IMS sono ancora gestiti principalmente utilizzando Admin Console.

Una volta completata la migrazione dei contenuti, in genere i gruppi IMS necessitano di alcune configurazioni aggiuntive per poter accedere ai contenuti migrati.  Consulta [Migrazione delle entità principali dopo la migrazione](/help/journey-migration/managing-principals-after-migration.md)

Per ulteriori informazioni sull’integrazione e l’amministrazione di utenti e gruppi AEM e IMS, consulta anche l’[esercitazione, Utenti, gruppi e autorizzazioni AEM](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions).
