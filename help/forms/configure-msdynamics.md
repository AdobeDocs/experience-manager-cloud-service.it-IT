---
title: Come si configura Microsoft Dynamics 365 in modelli di dati di moduli preconfigurati per Adaptive Forms?
description: Scopri come integrare Microsoft Dynamics 365 con Adaptive Forms.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 29ee324c-cd4c-403b-bb3d-b1eda8e8ad88
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 1%

---


# Configurazione di Microsoft® Dynamics 365 per AEM Forms

L’integrazione dei dati di Adobe Experience Manager Forms fornisce una configurazione del servizio cloud per integrare Forms con il server Microsoft Dynamics. Consente di creare il modello dati modulo (FDM) in base alle entità, agli attributi e ai servizi definiti nel servizio Microsoft Dynamics. Il Modello dati modulo (FDM) può essere utilizzato per creare Forms adattivo che interagiscono con il server Microsoft Dynamics per abilitare i flussi di lavoro aziendali. Ad esempio:

* Esegui una query sul server Microsoft Dynamics per dati e precompila Forms adattivo.
* Scrivere dati in Microsoft Dynamics all’invio di moduli adattivi.
* Scrivi dati in Microsoft Dynamics tramite entità personalizzate definite in Modello dati modulo (FDM).

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione degli invii di moduli. Ulteriori informazioni su queste opzioni sono disponibili nell&#39;articolo [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md).

<!-- 
[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Microsoft&reg; Dynamics 365] Cloud Services to integrate Adaptive Forms with out of the box Form Data Model (FDM). The Adaptive Forms can then interact with [!DNL Microsoft&reg; Dynamics 365] servers to enable business workflows. For example:

* Write data into [!DNL Microsoft&reg; Dynamics 365] on Adaptive Form submission.
* Write data in [!DNL Microsoft&reg; Dynamics 365] through custom entities defined in Form Data Model (FDM) and conversely.
* Query [!DNL Microsoft&reg; Dynamics 365]server for data and prepopulate Adaptive Forms.
* Read data from [!DNL Microsoft&reg; Dynamics 365] server.

[!DNL Microsoft&reg; Dynamics 365] cloud services and Form Data Model (FDM) are available out of the box on the [!DNL AEM Forms] Server after you [set up a development project for Forms based on Experience Manager archetype](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft&reg; Dynamics 365 cloud services and Form Data Model (FDM) are available out of the box only if you set up an [!DNL Experience Manager Forms] as a [!DNL Cloud Service] project based on [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) or later.-->

## Prerequisiti

Prima di integrare [!DNL Microsoft® Dynamics 365] con AEM Forms as a Cloud Service, assicurati di aver eseguito i seguenti passaggi:


1. **Configura l&#39;account in Microsoft Dynamics 365**

   Segui i passaggi descritti nel video per configurare un account Microsoft Dynamics 365. In questo video viene creato un account di prova a scopo dimostrativo.

   >[!VIDEO](https://video.tv.adobe.com/v/3444389/)

1. **Creare un account in Power Platform Admin Center**

   Creare un account in **Power Platform Admin Center** per:

   * Aggiungi Dataverse
   * Abilita applicazioni Microsoft Dynamics 365

   Segui i passaggi descritti nel video per creare un account in Power Platform Admin Center. In questo video, è stato creato un account di prova a scopo dimostrativo.

   >[!VIDEO](https://video.tv.adobe.com/v/3444388)

1. **Registra un&#39;applicazione per [!DNL Microsoft® Dynamics 365] in Azure Active Directory**

   Seguire i passaggi del video per registrare un&#39;applicazione per [!DNL Microsoft® Dynamics 365] in Azure Active Directory.

   >[!VIDEO](https://video.tv.adobe.com/v/3444369/dynamics365integration-microsoftdynamics-apiaccess-azuread-appregistration)

   >[!NOTE]
   >
   >* Per creare l&#39;applicazione [!DNL Microsoft® Dynamics 365] connessa, selezionare **Web** come piattaforma e specificare l&#39;**URI reindirizzamento** nel formato seguente: `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html`.
   >* Assicurati di salvare l’ID client (noto anche come ID applicazione) e il segreto client per riferimento futuro.

## Connettere Forms a Microsoft® Dynamics 365

Dopo aver configurato i prerequisiti di cui sopra, puoi procedere con l’integrazione di Adaptive Forms con Microsoft® Dynamics 365. Per inviare dati a Microsoft® Dynamics 365 all’invio del modulo, effettua le seguenti operazioni:

[&#x200B;1. Configurare la configurazione del servizio cloud per Microsoft Dynamics](#1-configure-cloud-service-configuration-for-microsoft-dynamics)

[&#x200B;2. Creare un modello dati modulo (FDM)](#2-create-form-data-model-fdm)

### &#x200B;1. Configurare la configurazione del servizio cloud per Microsoft Dynamics

>[!VIDEO](https://video.tv.adobe.com/v/3444370/cloudconfiguration-dataintegration-adobeexperiencemanager-aemforms-microsoftdynamics)

Per configurare la configurazione del servizio cloud [!DNL Microsoft® Dynamics 365], eseguire la procedura seguente:

1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Origini dati]** nell&#39;istanza di authoring [!DNL AEM Forms].

   ![Seleziona Cloud Data Source](/help/forms/assets/dynamics-data-source.png)
1. Seleziona un Contenitore di configurazione. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]**.

   ![Crea configurazione cloud](/help/forms/assets/dynamics-select-configuration.png)

   Viene visualizzata la configurazione guidata **Crea configurazione Data Source**.

   ![Creazione guidata configurazione Data Source](/help/forms/assets/dynamics-create-data-configuration.png)

1. Specifica il **[!UICONTROL Titolo]**, **[!UICONTROL Nome]** e seleziona **[!UICONTROL Tipo di servizio]** come **Servizio OData**.
1. Fai clic su **[!UICONTROL Avanti]**. Viene visualizzata la scheda **Autenticazione**.

   ![Scheda Autenticazione](/help/forms/assets/dynamics-authentication-tab.png)

1. Specificare il valore per il campo **[!UICONTROL Directory principale servizio]**.

   Vai all&#39;istanza di Dynamics in **Power Platform Admin Center** e passa a [Developer Resources](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) per visualizzare il valore di **Service Root**. L&#39;**endpoint API Web** rappresenta il valore **Service Root** per l&#39;istanza Dynamics che si desidera integrare con Adaptive Forms. L&#39;URL **radice servizio** è nel formato seguente: `https://<tenant-name>.dynamics.com/api/data/v9.1/`

   ![Campo principale servizio](/help/forms/assets/dynamics-service-root.png)

1. Selezionare **[!UICONTROL Tipo di autenticazione]** come **OAuth2.0**.
1. Specificare **ID client** (indicato come ID applicazione) e **Segreto client** per l&#39;applicazione connessa.
È possibile recuperare **ID client** e **Segreto client** dall&#39;applicazione Azure Active Directory.

   ![ID client e segreto client](/help/forms/assets/dynamics-azure-app-resgistration.png)

1. Specifica quanto segue nei campi **[!UICONTROL URL OAuth]**, **[!UICONTROL URL token di aggiornamento]** e **[!UICONTROL URL token di accesso]**.
È possibile recuperare l&#39;**[!UICONTROL URL OAuth]**, l&#39;**[!UICONTROL URL token di aggiornamento]** e l&#39;**[!UICONTROL URL token di accesso]** dalla sezione **Endpoints** dell&#39;applicazione Azure Active Directory.

   ![Endpoint app Azure](/help/forms/assets/dynamics-azure-app-endpoints.png)

1. Specificare `openid` nel campo **[!UICONTROL Ambito autorizzazione]** per il processo di autorizzazione in [!DNL Microsoft® Dynamics 365].
1. Specifica l&#39;URL dell&#39;istanza di dinamica nel campo **[!UICONTROL Risorsa]** per configurare [!DNL Microsoft® Dynamics 365] con un modello di dati del modulo (FDM).
È possibile copiare l&#39;**URL ambiente** da **Power Platform Admin Center** o derivare l&#39;URL istanza di Dynamics utilizzando l&#39;**URL radice servizio**. L&#39;URL della risorsa è nel seguente formato: `https://<tenant-name>.dynamics.com`.

   ![Campo risorsa app di alimentazione](/help/forms/assets/dynamics-resource-field.png)

1. Accedi con le credenziali di [!DNL Microsoft® Dynamics 365] e accetta per consentire alla configurazione del servizio cloud di connettersi al servizio [!DNL Microsoft® Dynamics 365]. Se la connessione ha esito positivo, si viene reindirizzati alla pagina di configurazione del servizio cloud [!DNL Microsoft® Dynamics 365], in cui viene visualizzato un messaggio di operazione riuscita.
1. Seleziona **[!UICONTROL Crea]** per salvare la configurazione.

### &#x200B;2. Creare un modello dati modulo (FDM)

>[!VIDEO](https://video.tv.adobe.com/v/3444367/aemforms-adobeexperiencemanager-formdatamodel--dataintegration-digitalforms)

È possibile utilizzare il modello di dati del modulo (FDM) utilizzando la configurazione cloud [!DNL Microsoft® Dynamics 365] creata. Per creare un modello dati modulo, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni dati]**.
   ![Crea modello dati modulo](/help/forms/assets/dynamics-create-fdm.png)

1. Fai clic su **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modello dati modulo]**.
   ![Selezionare il modello dati modulo](/help/forms/assets/dynamics-select-fdm.png)

   Viene visualizzata la procedura guidata **Crea modello dati modulo**.
1. Fai clic su **[!UICONTROL Avanti]**.
1. Selezionare la configurazione cloud creata dalla scheda **Seleziona origine dati**.
   ![Seleziona configurazione cloud](/help/forms/assets/dynamics-select-cloud-config.png)

1. Fai clic sull&#39;icona Modifica ![Modifica](assets/edit.png) per visualizzare e configurare il modello dati del modulo (FDM).

È quindi possibile [configurare il modello dati del modulo (FDM)](/help/forms/work-with-form-data-model.md#configure-services) e utilizzarlo in vari casi di utilizzo di moduli adattivi, ad esempio:

* Precompila modulo adattivo eseguendo una query sulle informazioni provenienti da entità e servizi [!DNL Microsoft Dynamics]
* Richiama [!DNL Microsoft Dynamics] operazioni server definite in un modello dati modulo (FDM) utilizzando le regole del modulo adattivo
* Scrivi i dati del modulo inviati in [!DNL Microsoft Dynamics] entità
* È possibile configurare l&#39;azione di invio Modello dati modulo per un modulo adattivo per inviare dati a [!DNL Microsoft Dynamics].

È quindi possibile utilizzare l&#39;opzione [Invia utilizzando il modello dati del modulo (FDM)](/help/forms/using-form-data-model.md) in un **modulo adattivo** per trasferire i dati dal modulo al [!DNL Microsoft® Dynamics 365] configurato.


>[!MORELIKETHIS]
>
>* [Configura origini dati per AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurare l&#39;archiviazione Azure per AEM Forms](/help/forms/configure-azure-storage.md)
>  [Aggiungi Forms Portal a una pagina AEM Sites](/help/forms/configure-forms-portal.md)
