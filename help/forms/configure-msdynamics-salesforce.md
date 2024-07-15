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

L&#39;[[!DNL Experience Manager Forms] integrazione dei dati](data-integration.md) fornisce servizi cloud [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] per integrare i moduli adattivi con il modello di dati del modulo (FDM) preconfigurato. Il Forms adattivo può quindi interagire con i server [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] per abilitare i flussi di lavoro aziendali. Ad esempio:

* Scrivere i dati in [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] all&#39;invio del modulo adattivo.
* Scrivere dati in [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] tramite entità personalizzate definite nel modello dati modulo (FDM) e viceversa.
* Eseguire la query sui server [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] per i dati e precompilare Adaptive Forms.
* Lettura dei dati dal server [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce].

I servizi cloud [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] e il modello dati modulo (FDM) sono disponibili sul server [!DNL AEM Forms] dopo aver [configurato un progetto di sviluppo per Forms basato su Archetipo Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft® Dynamics 365 e [!DNL Salesforce] Cloud Services e Form Data Model (FDM) sono disponibili come predefiniti solo se si imposta un [!DNL Experience Manager Forms] come progetto [!DNL Cloud Service] basato su [Archetipo AEM 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) o versione successiva.

## Configura servizio cloud [!DNL Salesforce] {#configure-salesforce-cloud-service}

Prima di configurare i servizi cloud [!DNL Salesforce], assicurarsi di eseguire le attività seguenti:

* [Crea un&#39;applicazione abilitata per OAuth [!DNL Salesforce] connessa](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). Quando si crea l&#39;applicazione [!DNL Salesforce] connessa, specificare l&#39;URL di callback nel formato seguente:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Dove server e porta fanno riferimento al nome host e al numero di porta per il server [!DNL AEM Forms].

* Durante la creazione dell&#39;applicazione [!DNL Salesforce] connessa, specificare `full` e `offline_access` come valori per l&#39;ambito OAuth.

* Prendi nota dei valori per l’ID client (denominato Chiave consumer) e il segreto client (denominato Segreto consumer) per l’applicazione connessa.

Per configurare il servizio cloud [!DNL Salesforce], eseguire la procedura seguente:

1. Nell&#39;istanza dell&#39;autore [!DNL AEM Forms], passare a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Origini dati]**. L&#39;elenco delle cartelle wrapper disponibili include una cartella con il titolo specificato per `DappTitle` durante la [generazione del progetto di archetipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. Selezionare il nome della cartella, selezionare **[!UICONTROL Configurazione cloud Salesforce]**, quindi selezionare **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Impostazioni autenticazione]**:
   1. Specificare l&#39;URL del dominio [!DNL Salesforce] nel campo **[!UICONTROL Host]**. Ad esempio, [Nome-dominio].my.salesforce.com.
   1. Specificare l&#39;ID client (chiave consumer) e il segreto client (segreto consumer) per l&#39;applicazione connessa.
   1. Specificare **accesso offline completo** (`full` e `offine_access` valori separati da uno spazio) nel campo **[!UICONTROL Ambito autorizzazione]**.
   1. Seleziona **[!UICONTROL Connetti a OAuth]**. Sei stato reindirizzato alla pagina di accesso [!DNL Microsoft® Dynamics].
   1. Accedi con le credenziali di [!DNL Salesforce] e accetta per consentire alla configurazione del servizio cloud di connettersi al servizio [!DNL Salesforce]. Se la connessione ha esito positivo, si viene reindirizzati alla pagina di configurazione del servizio cloud [!DNL Salesforce], in cui viene visualizzato un messaggio di operazione riuscita.
1. Seleziona **[!UICONTROL Salva e chiudi]** per completare la configurazione.

### Accesso a [!DNL Salesforce] Form Data Model (FDM) preconfigurato

Un modello di dati modulo (FDM) [!DNL Salesforce] è disponibile nel server [!DNL AEM Forms] dopo aver [configurato un progetto di sviluppo per Forms basato su Archetipo Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

Per accedere al modello dati del modulo (FDM), passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni dati]**. L&#39;elenco delle cartelle disponibili include una cartella con il titolo specificato per `DappTitle` durante la [generazione del progetto dell&#39;archetipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment). Seleziona il nome della cartella, fai clic su **[!UICONTROL Modello dati Salesforce]**, quindi fai clic sull&#39;icona Modifica ![Modifica](assets/edit.png) per visualizzare il modello dati del modulo (FDM).

Dopo aver configurato il servizio [[!DNL Salesforce] Cloud Config](#configure-salesforce-cloud-service), puoi integrare moduli adattivi con il modello dati [!DNL Salesforce] pronto all&#39;uso.

## Configura servizio cloud [!DNL Microsoft® Dynamics 365] {#configure-dynamics-cloud-service}

Prima di configurare il servizio cloud [!DNL Microsoft® Dynamics 365], assicurarsi di eseguire le attività seguenti:

* [Registra un&#39;applicazione per [!DNL Microsoft® Dynamics 365] con Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). Quando si crea l&#39;applicazione [!DNL Microsoft® Dynamics 365] connessa, specificare gli URL di risposta nel formato seguente:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Dove server e porta fanno riferimento al nome host e al numero di porta per il server [!DNL AEM Forms].

* Prendi nota dei valori per l’ID client (noto anche come ID applicazione) e il segreto client per l’applicazione connessa.

Per configurare il servizio cloud [!DNL Microsoft® Dynamics 365], eseguire la procedura seguente:

1. Nell&#39;istanza dell&#39;autore [!DNL AEM Forms], passare a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Origini dati]**. L&#39;elenco delle cartelle wrapper disponibili include una cartella con il titolo specificato per `DappTitle` durante la [generazione del progetto di archetipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. Selezionare il nome della cartella, selezionare **[!UICONTROL Microsoft® Dynamics 365 Cloud Config]** e selezionare **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Impostazioni autenticazione]**:
   1. Immettere il valore per il campo **[!UICONTROL Directory principale servizio]**. Vai all&#39;istanza Dynamics e passa a [Risorse per sviluppatori](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) per visualizzare il valore del campo Service Root. Ad esempio `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. Specificare l&#39;ID client (definito ID applicazione) e il segreto client per l&#39;applicazione connessa.
   1. Sostituisci `{tenant}` con un ID tenant nei campi **[!UICONTROL URL OAuth]**, **[!UICONTROL URL token di aggiornamento]** e **[!UICONTROL URL token di accesso]**.
   1. Specifica l&#39;URL dell&#39;istanza di Dynamics nel campo **[!UICONTROL Risorsa]** per configurare [!UICONTROL Microsoft® Dynamics] con un modello di dati del modulo (FDM). Utilizza l’URL principale del servizio per derivare l’URL dell’istanza di Dynamics. Esempio: `https://<tenant-name>.dynamics.com`.

   1. Specificare `openid` nel campo **[!UICONTROL Ambito autorizzazione]** per il processo di autorizzazione in [!DNL Microsoft® Dynamics 365].
   1. Accedi con le credenziali di [!DNL Microsoft® Dynamics 365] e accetta per consentire alla configurazione del servizio cloud di connettersi al servizio [!DNL Microsoft® Dynamics 365]. Se la connessione ha esito positivo, si viene reindirizzati alla pagina di configurazione del servizio cloud [!DNL Microsoft® Dynamics 365], in cui viene visualizzato un messaggio di operazione riuscita.
1. Seleziona **[!UICONTROL Salva e chiudi]** per completare la configurazione.

### Accesso a [!DNL Microsoft® Dynamics 365] Form Data Model (FDM) preconfigurato

Un modello di dati modulo (FDM) [!DNL Microsoft® Dynamics 365] è disponibile nel server [!DNL AEM Forms] dopo aver [configurato un progetto di sviluppo per Forms basato su Archetipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Per accedere al modello dati del modulo (FDM), passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni dati]**. L&#39;elenco delle cartelle disponibili include una cartella con il titolo specificato per `DappTitle` durante la [generazione del progetto dell&#39;archetipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment). Selezionare il nome della cartella, selezionare il modello dati **[!UICONTROL Microsoft® Dynamics 365]** e l&#39;icona Modifica ![Modifica](assets/edit.png) per visualizzare il modello dati del modulo (FDM).

Dopo aver configurato il servizio [[!DNL Microsoft® Dynamics 365] Cloud Config](#configure-dynamics-cloud-service), puoi integrare moduli adattivi con il modello dati [!DNL Microsoft® Dynamics 365] pronto all&#39;uso.

>[!MORELIKETHIS]
>
>* [Configura origini dati per AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurare l&#39;archiviazione Azure per AEM Forms](/help/forms/configure-azure-storage.md)
>  [Aggiungi Forms Portal a una pagina AEM Sites](/help/forms/configure-forms-portal.md)
