---
title: Come si configura  [!DNL Microsoft Dynamics] OData per AEM Forms?
description: Scopri come creare il modello dati modulo (FDM) in base alle entità, agli attributi e ai servizi definiti nel servizio  [!DNL Microsoft Dynamics] .
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Configurazione OData [!DNL Microsoft Dynamics] {#microsoft-dynamics-odata-configuration}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/ms-dynamics-odata-configuration.html) |
| AEM as a Cloud Service | Questo articolo |

![integrazione dei dati](assets/data-integeration.png)

[!DNL Microsoft Dynamics] è un software CRM (Customer Relationship Management) e ERP (Enterprise Resource Planning) che fornisce soluzioni aziendali per la creazione e la gestione di account cliente, contatti, lead, opportunità e casi. [[!DNL Experience Manager Forms] Integrazione dati](data-integration.md) fornisce una configurazione del servizio cloud OData per integrare Forms con il server [!DNL Microsoft Dynamics] online e locale. Consente di creare un modello di dati modulo (FDM) basato su entità, attributi e servizi definiti nel servizio [!DNL Microsoft Dynamics]. Il modello di dati del modulo (FDM) può essere utilizzato per creare Forms adattivo che interagisce con il server [!DNL Microsoft Dynamics] per abilitare i flussi di lavoro aziendali. Ad esempio:

* Esegui query sul server [!DNL Microsoft Dynamics] per dati e precompila Forms adattivo
* Scrivi dati in [!DNL Microsoft Dynamics] all&#39;invio di un modulo adattivo
* Scrivere dati in [!DNL Microsoft Dynamics] tramite entità personalizzate definite in Form Data Model (FDM) e viceversa

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  Il Cloud Service OData di MS Dynamics (servizio OData) è disponibile con tutte le modalità di esecuzione. Per ulteriori informazioni sulla configurazione delle modalità di esecuzione per un&#39;istanza [!DNL Experience Manager], vedere [Modalità di esecuzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=it#runmodes).

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione degli invii di moduli. Ulteriori informazioni su queste opzioni sono disponibili nell&#39;articolo [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md).


## Prerequisiti {#prerequisites}

Prima di iniziare l&#39;impostazione e la configurazione di [!DNL Microsoft Dynamics], verificare di disporre di:

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* Configurazione di [!DNL Microsoft Dynamics] 365 in linea o installazione di un&#39;istanza di una delle seguenti [!DNL Microsoft Dynamics] versioni:

   * [!DNL Microsoft Dynamics] 365 on-premise
   * [!DNL Microsoft Dynamics] 2016 on-premise

* [Registrazione dell&#39;applicazione per  [!DNL Microsoft Dynamics] servizio in linea con [!DNL Microsoft Azure] Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Prendi nota dei valori per l’ID client (noto anche come ID applicazione) e il segreto client per il servizio registrato. Questi valori vengono utilizzati durante [la configurazione del servizio cloud per il tuo [!DNL Microsoft Dynamics] servizio](#configure-cloud-service-for-your-microsoft-dynamics-service).

## Imposta URL di risposta per l&#39;applicazione [!DNL Microsoft Dynamics] registrata {#set-reply-url-for-registered-microsoft-dynamics-application}

Per impostare l&#39;URL di risposta per l&#39;applicazione [!DNL Microsoft Dynamics] registrata, eseguire le operazioni seguenti:

>[!NOTE]
>
>Utilizzare questa procedura solo durante l&#39;integrazione di [!DNL Experience Manager Forms] con il server [!DNL Microsoft Dynamics] online.

1. Vai all&#39;account di Active Directory [!DNL Microsoft Azure] e aggiungi il seguente URL di configurazione del servizio cloud nelle impostazioni **[!UICONTROL URL di risposta]** per l&#39;applicazione registrata:

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Directory di Azure](assets/azure_directory_new.png)

1. Salva la configurazione.

## Configura [!DNL Microsoft Dynamics] per IFD {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics] utilizza l&#39;autenticazione basata sulle attestazioni per fornire l&#39;accesso ai dati nel server CRM [!DNL Microsoft Dynamics] agli utenti esterni. Per abilitare questa impostazione, eseguire le operazioni seguenti per configurare [!DNL Microsoft Dynamics] per la distribuzione con connessione Internet (IFD) e configurare le impostazioni delle attestazioni.

>[!NOTE]
>
> Utilizzare questa procedura solo durante l&#39;integrazione di [!DNL Experience Manager Forms] con il server [!DNL Microsoft Dynamics] locale.

1. Configurare l&#39;istanza locale di [!DNL Microsoft Dynamics] per IFD come descritto in [Configurare IFD per [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Eseguire i comandi seguenti utilizzando Windows PowerShell per configurare le impostazioni delle attestazioni in [!DNL Microsoft Dynamics] abilitato per IFD:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Per informazioni dettagliate, consulta [Registrazione app per CRM locale (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd).

## Configurare il client OAuth nel computer AD FS {#configure-oauth-client-on-ad-fs-machine}

Per registrare un client OAuth nel computer Active Directory Federation Services (ADFS) e concedere l&#39;accesso al computer ADFS, eseguire le operazioni seguenti:

>[!NOTE]
>
>Utilizzare questa procedura solo durante l&#39;integrazione di [!DNL Experience Manager Forms] con il server [!DNL Microsoft Dynamics] locale.

1. Esegui il comando seguente:

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Dove:

   * `Client-ID` è un ID client che può essere generato utilizzando qualsiasi generatore GUID.
   * `redirect-uri` è l&#39;URL del servizio cloud OData [!DNL Microsoft Dynamics] in [!DNL Experience Manager Forms]. Il servizio cloud predefinito installato con [!DNL Experience Manager Forms] è distribuito al seguente URL:
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Eseguire il comando seguente per concedere l&#39;accesso al computer AD FS:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   Dove:

   * `resource` è l&#39;URL organizzazione [!DNL Microsoft Dynamics].

1. [!DNL Microsoft Dynamics] utilizza il protocollo HTTPS. Per richiamare gli endpoint AD FS dal server [!DNL Forms], installare il certificato del sito [!DNL Microsoft Dynamics] nell&#39;archivio certificati Java utilizzando il comando `keytool` nel computer che esegue [!DNL Experience Manager Forms].

## Configura servizio cloud per il servizio [!DNL Microsoft Dynamics] {#configure-cloud-service-for-your-microsoft-dynamics-service}

Un servizio OData è identificato dall&#39;URL radice del servizio. Per configurare un servizio OData in [!DNL Experience Manager] as a Cloud Service, verificare di disporre dell&#39;URL principale del servizio e procedere come segue:

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>Per una guida dettagliata alla configurazione di [!DNL Microsoft Dynamics 365], online o on-premise, vedere [[!DNL Microsoft Dynamics] Configurazione OData](ms-dynamics-odata-configuration.md).

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud, consulta [Configurare la cartella per le configurazioni del servizio cloud](#cloud-folder).

1. Selezionare **[!UICONTROL Crea]** per aprire la **[!UICONTROL Creazione guidata configurazione Data Source]**. Specifica un nome e, facoltativamente, un titolo per la configurazione. Seleziona **[!UICONTROL Servizio OData]** dal menu a discesa **[!UICONTROL Tipo di servizio]**. Se necessario, sfoglia e seleziona un&#39;immagine di anteprima per la configurazione, quindi seleziona **[!UICONTROL Successivo]**.
Nella scheda **[!UICONTROL Impostazioni autenticazione]**:

   1. Immettere il valore per il campo **[!UICONTROL Directory principale servizio]**. Vai all&#39;istanza Dynamics e passa a **[!UICONTROL Risorse per sviluppatori]** per visualizzare il valore del campo Service Root. Ad esempio, https://&lt;nome-tenant>/api/data/v9.1/

   1. Seleziona **[!UICONTROL OAuth 2.0]** come tipo di autenticazione.

   1. Sostituisci i valori predefiniti nei campi **[!UICONTROL ID client]** (indicato anche come **ID applicazione**), **[!UICONTROL Segreto client]**, **[!UICONTROL URL OAuth]**, **[!UICONTROL URL token di aggiornamento]**, **[!UICONTROL URL token di accesso]** e **[!UICONTROL Risorsa]** con i valori della configurazione del servizio [!DNL Microsoft Dynamics]. È obbligatorio specificare l&#39;URL dell&#39;istanza dinamica nel campo **[!UICONTROL Risorsa]** per configurare [!DNL Microsoft Dynamics] con un modello dati modulo (FDM). Utilizza l’URL principale del servizio per derivare l’URL dell’istanza di Dynamics. Ad esempio, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Specificare **[!UICONTROL openid]** nel campo **[!UICONTROL Ambito autorizzazione]** per il processo di autorizzazione in [!DNL Microsoft Dynamics].

      ![Impostazioni autenticazione](assets/dynamics_authentication_settings_new.png)
Modello dati modulo (FDM)
1. Fai clic su **[!UICONTROL Connetti a OAuth]**. Sei stato reindirizzato alla pagina di accesso [!DNL Microsoft Dynamics].
1. Accedi con le credenziali di [!DNL Microsoft Dynamics] e accetta per consentire alla configurazione del servizio cloud di connettersi al servizio [!DNL Microsoft Dynamics]. È un task occasionale per stabilire il modello dati del modulo (FDM) per il servizio cloud e il servizio.

   Si è il modello dati modulo nella pagina di configurazione del servizio cloud, in cui viene visualizzato un messaggio che informa che la configurazione OData è stata salvata correttamente.

Il servizio cloud Cloud Service OData (OData Service) di MS Dynamics è configurato e connesso al servizio Dynamics. Modello dati modulo (FDM)

## Crea modello dati modulo (FDM) {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

Dopo aver configurato il servizio cloud MS Dynamics OData, puoi utilizzarlo durante la creazione del modello dati modulo (FDM). Per ulteriori informazioni, vedere [Creare un modello dati modulo (FDM)](create-form-data-models.md).

Successivamente, puoi creare un modello di dati modulo basato su modulo adattivo (FDM) e utilizzarlo in vari casi di utilizzo di moduli adattivi, ad esempio:

* Precompila modulo adattivo eseguendo una query sulle informazioni provenienti da entità e servizi [!DNL Microsoft Dynamics]
* Richiama [!DNL Microsoft Dynamics] operazioni server definite in un modello dati modulo (FDM) utilizzando le regole del modulo adattivo
* Scrivi i dati del modulo inviati in [!DNL Microsoft Dynamics] entità

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

È possibile [configurare l&#39;azione di invio Modello dati modulo](/help/forms/using-form-data-model.md) per un modulo adattivo per inviare dati a Microsoft Dynamics OData.

Per ulteriori informazioni sulla creazione e l&#39;utilizzo di Form Data Model (FDM) nei flussi di lavoro aziendali, vedere [Integrazione dei dati](data-integration.md).

## Articoli correlati

{{af-submit-action}}
