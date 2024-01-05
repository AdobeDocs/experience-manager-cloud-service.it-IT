---
title: 'Processo di provisioning: panoramica'
description: 'Processo di provisioning: panoramica'
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 98%

---


# AEM as a Cloud Service: onboarding e accesso

In questa pagina sono elencate le risorse di supporto autonomo relative al processo di provisioning per Experience Manager as a Cloud Service.

## Panoramica del processo di provisioning di AEM as a Cloud Service

Questa sezione riguarda gli articoli principali su:

* Accesso a AEM as a Cloud Service
* Processo di onboarding e provisioning di Adobe Experience Manager as a Cloud Service
* Aiuto e risorse


### Accesso a AEM as a Cloud Service

Una volta completato il provisioning automatico:

* Concessione dei diritti di accesso: viene creata un’organizzazione all’interno di Adobe Identity Management System (IMS)
* Per impostazione predefinita, le autorizzazioni di amministrazione vengono concesse all’amministratore designato.
* L’amministratore può aggiungere utenti e ruoli per altri membri del gruppo tramite Admin Console
* È possibile rivedere le autorizzazioni degli utenti basate sui ruoli per determinare le assegnazioni delle autorizzazioni in Cloud Manager

![processoverview.jpg](assets/processOverview.jpg)


Per ulteriori informazioni, consulta [Onboarding in Experience Manager as a Cloud Service su Experience League](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html).

### Risorse e collegamenti

* [Supporto IMS per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=it)
* [Autorizzazioni basate sui ruoli in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html#what-is-required)
* [Accesso a Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#getting-access)


## Processo di onboarding di Adobe Experience Manager as a Cloud Service

### 1. L’ordine di acquisto attiva il provisioning automatico.

### 2. Onboarding delle organizzazioni in Adobe Admin Console:

![processoverview2.jpg](assets/processOverview2.jpg)

* Amministratore di sistema:
   * Esegue il provisioning di programmi e ambienti di AEM.
   * Accede a Admin Console per le attività amministrative.
   * Richiede un dominio per confermare la proprietà del rispettivo dominio.
   * Imposta le directory degli utenti.
   * Configura l’IDP.
* Amministratore AEM:
   * Gestisce gruppi, autorizzazioni e privilegi locali.

### 3. Onboarding degli utenti e gestione degli accessi in Admin Console:

![processoverview3.jpg](assets/processOverview3.jpg)

Per l’onboarding degli utenti sono disponibili tre metodi, a seconda delle dimensioni e delle preferenze:
* Creare manualmente gli utenti in Admin Console
* Caricare il file .csv
* Sincronizzare gli utenti da Active Directory dell’azienda

### 4. L’amministratore configura l’organizzazione e concede agli utenti e ai gruppi le autorizzazioni di accesso agli ambienti

## Aiuto e risorse

* [Primo accesso a Cloud Service](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)
* [Configurazione dell’accesso a AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#accessing)
