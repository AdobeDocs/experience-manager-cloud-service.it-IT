---
title: Come configurare [!DNL Microsoft Dynamics] OData?
description: Scopri come creare il modello dati modulo in base alle entità, agli attributi e ai servizi definiti in [!DNL Microsoft Dynamics] servizio. Il modello dati modulo può essere utilizzato per creare Forms adattivo che interagisce con [!DNL Microsoft Dynamics] per abilitare i flussi di lavoro aziendali.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# [!DNL Microsoft Dynamics] Configurazione OData {#microsoft-dynamics-odata-configuration}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/ms-dynamics-odata-configuration.html) |
| AEM as a Cloud Service | Questo articolo |

![integrazione dei dati](assets/data-integeration.png)

[!DNL Microsoft Dynamics] è un software CRM (Customer Relationship Management) e ERP (Enterprise Resource Planning) che fornisce soluzioni aziendali per la creazione e la gestione di account, contatti, lead, opportunità e casi cliente. [[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md) fornisce una configurazione del servizio cloud OData per integrare Forms sia online che on-premise [!DNL Microsoft Dynamics] server. Consente di creare un modello dati modulo basato su entità, attributi e servizi definiti in [!DNL Microsoft Dynamics] servizio. Il modello dati modulo può essere utilizzato per creare Forms adattivo che interagisce con [!DNL Microsoft Dynamics] per abilitare i flussi di lavoro aziendali. Ad esempio:

* Query [!DNL Microsoft Dynamics] server per dati e precompilazione di Adaptive Forms
* Scrivi dati in [!DNL Microsoft Dynamics] all’invio di un modulo adattivo
* Scrivi dati in [!DNL Microsoft Dynamics] tramite entità personalizzate definite nel modello dati modulo e viceversa

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  Il Cloud Service OData di MS Dynamics (servizio OData) è disponibile con tutte le modalità di esecuzione. Per ulteriori informazioni sulla configurazione delle modalità di esecuzione per un [!DNL Experience Manager] istanza, vedi [Modalità di esecuzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=it#runmodes).

## Prerequisiti {#prerequisites}

Prima di iniziare l’impostazione e la configurazione [!DNL Microsoft Dynamics], assicurati di disporre di:

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* Configurato [!DNL Microsoft Dynamics] 365 online o installato un&#39;istanza di uno dei seguenti elementi [!DNL Microsoft Dynamics] versioni:

   * [!DNL Microsoft Dynamics] 365 on-premise
   * [!DNL Microsoft Dynamics] 2016 on-premise

* [Ha registrato la domanda per [!DNL Microsoft Dynamics] servizio online con [!DNL Microsoft Azure] Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Prendi nota dei valori per l’ID client (noto anche come ID applicazione) e il segreto client per il servizio registrato. Questi valori vengono utilizzati durante [configurazione del servizio cloud per il tuo [!DNL Microsoft Dynamics] servizio](#configure-cloud-service-for-your-microsoft-dynamics-service).

## Imposta URL di risposta per registrato [!DNL Microsoft Dynamics] applicazione {#set-reply-url-for-registered-microsoft-dynamics-application}

Per impostare l&#39;URL di risposta per i messaggi registrati, procedere come segue [!DNL Microsoft Dynamics] applicazione:

>[!NOTE]
>
>Utilizzare questa procedura solo durante l&#39;integrazione [!DNL Experience Manager Forms] con online [!DNL Microsoft Dynamics] server.

1. Vai a [!DNL Microsoft Azure] Account di Active Directory e aggiungi il seguente URL di configurazione del servizio cloud in **[!UICONTROL URL di risposta]** impostazioni per l&#39;applicazione registrata:

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Directory di Azure](assets/azure_directory_new.png)

1. Salva la configurazione.

## Configura [!DNL Microsoft Dynamics] per IFD {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics] utilizza l&#39;autenticazione basata sulle attestazioni per fornire accesso ai dati su [!DNL Microsoft Dynamics] Server CRM per utenti esterni. Per abilitare questa impostazione, effettuare le seguenti operazioni per configurare [!DNL Microsoft Dynamics] per l&#39;implementazione con connessione Internet (IFD) e configurare le impostazioni delle attestazioni.

>[!NOTE]
>
>Utilizzare questa procedura solo durante l&#39;integrazione [!DNL Experience Manager Forms] con on-premise [!DNL Microsoft Dynamics] server.

1. Configura [!DNL Microsoft Dynamics] istanza locale di IFD come descritto in [Configura IFD per [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Eseguire i comandi seguenti utilizzando Windows PowerShell per configurare le impostazioni delle attestazioni su IFD abilitato [!DNL Microsoft Dynamics]:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Consulta [Registrazione app per CRM on-premise (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) per i dettagli.

## Configurare il client OAuth nel computer AD FS {#configure-oauth-client-on-ad-fs-machine}

Per registrare un client OAuth nel computer Active Directory Federation Services (ADFS) e concedere l&#39;accesso al computer ADFS, eseguire le operazioni seguenti:

>[!NOTE]
>
>Utilizzare questa procedura solo durante l&#39;integrazione [!DNL Experience Manager Forms] con on-premise [!DNL Microsoft Dynamics] server.

1. Esegui il comando seguente:

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Dove:

   * `Client-ID` è un ID client che può essere generato utilizzando qualsiasi generatore GUID.
   * `redirect-uri` è l’URL del [!DNL Microsoft Dynamics] Servizio cloud OData su [!DNL Experience Manager Forms]. Il servizio cloud predefinito installato con [!DNL Experience Manager Forms] viene distribuito al seguente URL:
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Eseguire il comando seguente per concedere l&#39;accesso al computer AD FS:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   Dove:

   * `resource` è il [!DNL Microsoft Dynamics] URL organizzazione.

1. [!DNL Microsoft Dynamics] utilizza il protocollo HTTPS. Per richiamare endpoint AD FS da [!DNL Forms] server, installazione [!DNL Microsoft Dynamics] certificato del sito all’archivio certificati Java utilizzando `keytool` sul computer che esegue [!DNL Experience Manager Forms].

## Configurare il servizio cloud per [!DNL Microsoft Dynamics] servizio {#configure-cloud-service-for-your-microsoft-dynamics-service}

Un servizio OData è identificato dall&#39;URL radice del servizio. Per configurare un servizio OData in [!DNL Experience Manager] as a Cloud Service, assicurati di disporre dell’URL principale del servizio ed effettua le seguenti operazioni:

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>Guida dettagliata alla configurazione di [!DNL Microsoft Dynamics 365], online o on-premise, vedi [[!DNL Microsoft Dynamics] Configurazione OData](ms-dynamics-odata-configuration.md).

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Consulta [Configurare la cartella per le configurazioni del servizio cloud](#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni di cloud service.

1. Tocca **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome e, facoltativamente, un titolo per la configurazione, quindi seleziona **[!UICONTROL Servizio OData]** dal **[!UICONTROL Tipo di servizio]** a discesa, se necessario sfoglia e seleziona un’immagine di miniatura per la configurazione, quindi tocca **[!UICONTROL Successivo]**.
In **[!UICONTROL Impostazioni di autenticazione]** scheda:

   1. Immetti il valore per **[!UICONTROL Directory principale servizio]** campo. Vai all’istanza Dynamics e passa a **[!UICONTROL Risorse per sviluppatori]** per visualizzare il valore del campo Service Root. Ad esempio, https://&lt;tenant-name>/api/data/v9.1/

   1. Seleziona **[!UICONTROL OAuth 2.0]** come tipo di autenticazione.

   1. Sostituisci i valori predefiniti in **[!UICONTROL ID client]** (denominati anche **ID applicazione**), **[!UICONTROL Segreto client]**, **[!UICONTROL URL OAuth]**, **[!UICONTROL Aggiorna URL token]**, **[!UICONTROL URL token di accesso]**, e **[!UICONTROL Risorsa]** campi con i valori del [!DNL Microsoft Dynamics] configurazione del servizio. È obbligatorio specificare l’URL dell’istanza di Dynamics nel **[!UICONTROL Risorsa]** campo da configurare [!DNL Microsoft Dynamics] con un modello di dati modulo. Utilizza l’URL principale del servizio per derivare l’URL dell’istanza di Dynamics. Ad esempio: [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Specifica **[!UICONTROL openid]** nel **[!UICONTROL Ambito autorizzazione]** campo per il processo di autorizzazione [!DNL Microsoft Dynamics].

      ![Impostazioni di autenticazione](assets/dynamics_authentication_settings_new.png)
Modello dati modulo
1. Clic **[!UICONTROL Connetti a OAuth]**. Sei stato reindirizzato a [!DNL Microsoft Dynamics] pagina di accesso.
1. Accedi con il [!DNL Microsoft Dynamics] credenziali e accettazione per consentire alla configurazione del servizio cloud di connettersi a [!DNL Microsoft Dynamics] servizio. Stabilire un modello di dati modulo tra il servizio cloud e il servizio è un’attività una tantum.

   Si è il modello dati modulo nella pagina di configurazione del servizio cloud, in cui viene visualizzato un messaggio che informa che la configurazione OData è stata salvata correttamente.

Il servizio cloud Cloud Service OData (OData Service) di MS Dynamics è configurato e connesso al servizio Dynamics. Modello dati modulo modello dati modulo

## Crea modello dati modulo {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

Dopo aver configurato il servizio cloud MS Dynamics OData Cloud Ser Form Data Model (ce), puoi utilizzare il servizio durante la creazione di modelli di dati del modulo. Per ulteriori informazioni, consulta [Crea modello dati modulo](create-form-data-models.md).

Successivamente, puoi creare un modulo adattivo basato sul modello di dati del modulo e utilizzarlo in vari casi di utilizzo di moduli adattivi, ad esempio:

* Precompilare un modulo adattivo interrogando le informazioni [!DNL Microsoft Dynamics] entità e servizi
* Richiama [!DNL Microsoft Dynamics] operazioni server definite in un modello di dati modulo utilizzando le regole del modulo adattivo
* Scrivi i dati modulo inviati in [!DNL Microsoft Dynamics] entità

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

Per ulteriori informazioni sulla creazione e l’utilizzo del modello dati modulo nei flussi di lavoro aziendali, consulta [Integrazione dei dati](data-integration.md).
