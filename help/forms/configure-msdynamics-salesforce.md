---
title: Come configurare Microsoft Dynamics 365 e Salesforce per modelli di dati di moduli preconfigurati per Adaptive Forms?
description: Scopri come integrare Microsoft Dynamics 365 e Salesforce con Adaptive Forms.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# Configurare Microsoft® Dynamics 365 o Salesforce per AEM Forms {#configure-azure-storage}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | Questo articolo |

[[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md) fornisce [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] servizi cloud per integrare moduli adattivi con Form Data Model (FDM) pronto all’uso. Il Forms adattivo può quindi interagire con [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] per abilitare i flussi di lavoro aziendali. Ad esempio:

* Scrivi dati in [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] all’invio di un modulo adattivo.
* Scrivi dati in [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] tramite entità personalizzate definite in Form Data Model (FDM) e viceversa.
* Query [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] server per dati e precompilazione di Adaptive Forms.
* Leggi dati da [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] server.

[!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] I servizi cloud e il modello dati del modulo (FDM) sono disponibili come funzionalità integrata nella [!DNL AEM Forms] Server dopo di te [configurare un progetto di sviluppo per Forms basato su archetipo Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft® Dynamics 365 e [!DNL Salesforce] Cloud Services e Form Data Model (FDM) sono disponibili come funzionalità integrata solo se è stata impostata una [!DNL Experience Manager Forms] as a [!DNL Cloud Service] progetto basato su [Archetipo AEM 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) o più tardi.

## Configura [!DNL Salesforce] servizio cloud {#configure-salesforce-cloud-service}

Prima di configurare [!DNL Salesforce] servizi cloud, assicurati di eseguire le seguenti attività:

* [Creare una connessione abilitata per OAuth [!DNL Salesforce] applicazione](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). Quando si crea la connessione [!DNL Salesforce] , specificare l&#39;URL di callback nel formato seguente:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Dove server e porta fanno riferimento al nome host e al numero di porta per [!DNL AEM Forms] Server.

* Durante la creazione della connessione [!DNL Salesforce] applicazione, specificare `full` e `offline_access` come valori per l’ambito OAuth.

* Prendi nota dei valori per l’ID client (denominato Chiave consumer) e il segreto client (denominato Segreto consumer) per l’applicazione connessa.

Per configurare il [!DNL Salesforce] servizio cloud:

1. On [!DNL AEM Forms] istanza di authoring, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Origini dati]**. L&#39;elenco delle cartelle wrapper disponibili include una cartella con il titolo specificato per `DappTitle`  durante [generazione del progetto di archetipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. Seleziona il nome della cartella e fai clic su **[!UICONTROL Configurazione cloud Salesforce]**, e seleziona **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Impostazioni di autenticazione]** scheda:
   1. Specifica la [!DNL Salesforce] URL del dominio in **[!UICONTROL Host]** campo. Ad esempio: [Nome di dominio].my.salesforce.com.
   1. Specificare l&#39;ID client (chiave consumer) e il segreto client (segreto consumer) per l&#39;applicazione connessa.
   1. Specifica **accesso offline completo** (`full` e `offine_access` valori separati da uno spazio) nella **[!UICONTROL Ambito autorizzazione]** campo.
   1. Seleziona **[!UICONTROL Connetti a OAuth]**. Sei stato reindirizzato a [!DNL Microsoft® Dynamics] pagina di accesso.
   1. Accedi con il [!DNL Salesforce] credenziali e accettazione per consentire alla configurazione del servizio cloud di connettersi a [!DNL Salesforce] servizio. Se la connessione ha esito positivo, viene effettuato il reindirizzamento al [!DNL Salesforce] pagina di configurazione del servizio cloud, in cui viene visualizzato un messaggio di successo.
1. Seleziona **[!UICONTROL Salva e chiudi]** per completare l&#39;impostazione della configurazione.

### Accesso preconfigurato [!DNL Salesforce] Modello dati modulo (FDM)

A [!DNL Salesforce] Il modello di dati del modulo (FDM) è disponibile come strumento predefinito nella [!DNL AEM Forms] Server dopo di te [configurare un progetto di sviluppo per Forms basato su archetipo Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

Per accedere al modello dati del modulo (FDM), vai a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni di dati]**. L’elenco delle cartelle disponibili include una cartella con il titolo specificato per `DappTitle`  durante [generazione del progetto di archetipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment). Seleziona il nome della cartella, quindi fai clic su **[!UICONTROL Modello dati Salesforce]** e seleziona Modifica ![Modifica](assets/edit.png) per visualizzare il modello dati del modulo (FDM).

Dopo aver configurato [[!DNL Salesforce] Servizio di configurazione cloud](#configure-salesforce-cloud-service), puoi integrare moduli adattivi con [!DNL Salesforce] Modello dati.

## Configura [!DNL Microsoft® Dynamics 365] servizio cloud {#configure-dynamics-cloud-service}

Prima di configurare [!DNL Microsoft® Dynamics 365] cloud service, assicurati di eseguire le seguenti attività:

* [Registra una richiesta per [!DNL Microsoft® Dynamics 365] con Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). Quando si crea la connessione [!DNL Microsoft® Dynamics 365] , specificare gli URL di risposta nel seguente formato:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Dove server e porta fanno riferimento al nome host e al numero di porta per [!DNL AEM Forms] Server.

* Prendi nota dei valori per l’ID client (noto anche come ID applicazione) e il segreto client per l’applicazione connessa.

Per configurare il [!DNL Microsoft® Dynamics 365] servizio cloud:

1. On [!DNL AEM Forms] istanza di authoring, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Origini dati]**. L&#39;elenco delle cartelle wrapper disponibili include una cartella con il titolo specificato per `DappTitle`  durante [generazione del progetto di archetipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. Seleziona il nome della cartella e fai clic su **[!UICONTROL Configurazione cloud Microsoft® Dynamics 365]**, e seleziona **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Impostazioni di autenticazione]** scheda:
   1. Immetti il valore per **[!UICONTROL Directory principale servizio]** campo. Vai all’istanza Dynamics e passa a [Risorse per sviluppatori](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) per visualizzare il valore del campo Service Root. Ad esempio `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. Specificare l&#39;ID client (definito ID applicazione) e il segreto client per l&#39;applicazione connessa.
   1. Sostituisci `{tenant}` con un ID tenant in **[!UICONTROL URL OAuth]**, **[!UICONTROL Aggiorna URL token]**, e **[!UICONTROL URL token di accesso]** campi.
   1. Specifica l’URL dell’istanza di Dynamics nel **[!UICONTROL Risorsa]** campo da configurare [!UICONTROL Microsoft® Dynamics] con un modello di dati modulo (FDM). Utilizza l’URL principale del servizio per derivare l’URL dell’istanza di Dynamics. Esempio: `https://<tenant-name>.dynamics.com`.

   1. Specifica `openid` nel **[!UICONTROL Ambito autorizzazione]** campo per il processo di autorizzazione [!DNL Microsoft® Dynamics 365].
   1. Accedi con il [!DNL Microsoft® Dynamics 365] credenziali e accettazione per consentire alla configurazione del servizio cloud di connettersi a [!DNL Microsoft® Dynamics 365] servizio. Se la connessione ha esito positivo, viene effettuato il reindirizzamento al [!DNL Microsoft® Dynamics 365] pagina di configurazione del servizio cloud, in cui viene visualizzato un messaggio di successo.
1. Seleziona **[!UICONTROL Salva e chiudi]** per completare l&#39;impostazione della configurazione.

### Accesso preconfigurato [!DNL Microsoft® Dynamics 365] Modello dati modulo (FDM)

A [!DNL Microsoft® Dynamics 365] Il modello di dati del modulo (FDM) è disponibile come strumento predefinito nella [!DNL AEM Forms] Server dopo di te [configurare un progetto di sviluppo per Forms basato su archetipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Per accedere al modello dati del modulo (FDM), vai a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni di dati]**. L’elenco delle cartelle disponibili include una cartella con il titolo specificato per `DappTitle`  durante [generazione del progetto di archetipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment). Seleziona il nome della cartella, quindi fai clic su **[!UICONTROL Modello dati Microsoft® Dynamics 365]** e seleziona Modifica ![Modifica](assets/edit.png) per visualizzare il modello dati del modulo (FDM).

Dopo aver configurato [[!DNL Microsoft® Dynamics 365] Servizio di configurazione cloud](#configure-dynamics-cloud-service), puoi integrare moduli adattivi con [!DNL Microsoft® Dynamics 365] Modello dati.

>[!MORELIKETHIS]
>
>* [Configurare le origini dati per AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurare l’archiviazione Azure per AEM Forms](/help/forms/configure-azure-storage.md)
>  [Aggiungere Forms Portal a una pagina di AEM Sites](/help/forms/configure-forms-portal.md)
