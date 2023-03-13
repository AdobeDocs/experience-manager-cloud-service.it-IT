---
title: Come configurare Microsoft Dynamics 365 e Salesforce modelli di dati per moduli adattivi pronti all’uso?
description: Scopri come integrare Microsoft Dynamics 365 e Salesforce con moduli adattivi.
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# Configurazione [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] servizi cloud {#configure-azure-storage}

[[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md) fornisce [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] servizi cloud per integrare moduli adattivi con modelli di dati per moduli pronti all’uso. Il Forms adattivo può quindi interagire con [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] per abilitare i flussi di lavoro aziendali. Esempio:

* Scrivi dati in [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] all’invio di un modulo adattivo.
* Scrivi dati in [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] tramite entità personalizzate definite nel modello dati modulo e viceversa.
* Query [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] server per dati e precompilazione di Adaptive Forms.
* Leggi dati da [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] server.

[!DNL Microsoft Dynamics 365] e [!DNL Salesforce] I servizi cloud e i modelli di dati dei moduli sono disponibili con la funzione integrata di [!DNL AEM Forms] server dopo di te [configurare un progetto di sviluppo per Forms basato su archetipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft Dynamics 365 e [!DNL Salesforce] I servizi cloud e i modelli di dati del modulo sono disponibili come predefiniti solo se hai impostato un’ [!DNL Experience Manager Forms] as a [!DNL Cloud Service] progetto basato su [Archetipo AEM 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) o più tardi.

## Configura [!DNL Salesforce] servizio cloud {#configure-salesforce-cloud-service}

Prima di configurare [!DNL Salesforce] servizi cloud, assicurati di eseguire le seguenti attività:

* [Creare una connessione abilitata per OAuth [!DNL Salesforce] applicazione](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). Quando si crea la connessione [!DNL Salesforce] , specificare l&#39;URL di callback nel formato seguente:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Dove server e porta si riferiscono al nome host e al numero di porta per [!DNL AEM Forms] server.

* Durante la creazione della connessione [!DNL Salesforce] applicazione, specificare `full` e `offline_access` come valori per l’ambito OAuth.

* Prendi nota dei valori per l’ID client (denominato Chiave consumer) e il segreto client (denominato Segreto consumer) per l’applicazione connessa.

Per configurare il [!DNL Salesforce] servizio cloud:

1. On [!DNL AEM Forms] istanza di authoring, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Origini dati]**. L&#39;elenco delle cartelle wrapper disponibili include una cartella con il titolo specificato per `DappTitle`  durante [generazione del progetto di archetipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Tocca il nome della cartella, seleziona **[!UICONTROL Configurazione cloud Salesforce]**, e tocca **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Impostazioni di autenticazione]** scheda:
   1. Specifica la [!DNL Salesforce] URL del dominio in **[!UICONTROL Host]** campo. Ad esempio: [Nome di dominio].my.salesforce.com.
   1. Specificare l&#39;ID client (chiave consumer) e il segreto client (segreto consumer) per l&#39;applicazione connessa.
   1. Specifica **accesso offline completo** (`full` e `offine_access` valori separati da uno spazio) nella **[!UICONTROL Ambito autorizzazione]** campo.
   1. Tocca **[!UICONTROL Connetti a OAuth]**. Sei stato reindirizzato a [!DNL Microsoft Dynamics] pagina di accesso.
   1. Accedi con il [!DNL Salesforce] credenziali e accettazione per consentire alla configurazione del servizio cloud di connettersi a [!DNL Salesforce] servizio. Se la connessione ha esito positivo, viene effettuato il reindirizzamento al [!DNL Salesforce] pagina di configurazione del servizio cloud, in cui viene visualizzato un messaggio di successo.
1. Tocca **[!UICONTROL Salva e chiudi]** per completare l&#39;impostazione della configurazione.

### Accesso preconfigurato [!DNL Salesforce] Modello dati modulo

A [!DNL Salesforce] Il Modello dati modulo è disponibile come strumento pronto all’uso sulla [!DNL AEM Forms] server dopo di te [configurare un progetto di sviluppo per Forms basato su archetipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Per accedere al modello dati del modulo, passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni di dati]**. L’elenco delle cartelle disponibili include una cartella con il titolo specificato per `DappTitle`  durante [generazione del progetto di archetipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Tocca il nome della cartella, seleziona la **[!UICONTROL Modello dati Salesforce]**, quindi tocca Modifica ![Modifica](assets/edit.png) per visualizzare il modello dati del modulo.

Dopo aver configurato [[!DNL Salesforce] Servizio di configurazione cloud](#configure-salesforce-cloud-service), puoi integrare moduli adattivi con [!DNL Salesforce] Modello dati.

## Configura [!DNL Microsoft Dynamics 365] servizio cloud {#configure-dynamics-cloud-service}

Prima di configurare [!DNL Microsoft Dynamics 365] cloud service, assicurati di eseguire le seguenti attività:

* [Registra una richiesta per [!DNL Microsoft Dynamics 365] con Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). Quando si crea la connessione [!DNL Microsoft Dynamics 365] , specificare gli URL di risposta nel seguente formato:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Dove server e porta si riferiscono al nome host e al numero di porta per [!DNL AEM Forms] server.

* Prendi nota dei valori per l’ID client (noto anche come ID applicazione) e il segreto client per l’applicazione connessa.

Per configurare il [!DNL Microsoft Dynamics 365] servizio cloud:

1. On [!DNL AEM Forms] istanza di authoring, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Origini dati]**. L&#39;elenco delle cartelle wrapper disponibili include una cartella con il titolo specificato per `DappTitle`  durante [generazione del progetto di archetipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Tocca il nome della cartella, seleziona **[!UICONTROL Configurazione cloud Microsoft Dynamics 365]**, e tocca **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Impostazioni di autenticazione]** scheda:
   1. Immetti il valore per **[!UICONTROL Directory principale servizio]** campo. Vai all’istanza Dynamics e passa a [Risorse per sviluppatori](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) per visualizzare il valore del campo Service Root. Esempio, `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. Specificare l&#39;ID client (definito ID applicazione) e il segreto client per l&#39;applicazione connessa.
   1. Sostituisci `{tenant}` con un ID tenant in **[!UICONTROL URL OAuth]**, **[!UICONTROL Aggiorna URL token]**, e **[!UICONTROL URL token di accesso]** campi.
   1. Specifica l’URL dell’istanza di Dynamics nel **[!UICONTROL Risorsa]** campo da configurare [!UICONTROL Microsoft Dynamics] con un modello dati modulo. Utilizza l’URL principale del servizio per derivare l’URL dell’istanza di Dynamics. Esempio: `https://<tenant-name>.dynamics.com`.

   1. Specifica `openid` nel **[!UICONTROL Ambito autorizzazione]** campo per il processo di autorizzazione [!DNL Microsoft Dynamics 365].
   1. Accedi con il [!DNL Microsoft Dynamics 365] credenziali e accettazione per consentire alla configurazione del servizio cloud di connettersi a [!DNL Microsoft Dynamics 365] servizio. Se la connessione ha esito positivo, viene effettuato il reindirizzamento al [!DNL Microsoft Dynamics 365] pagina di configurazione del servizio cloud, in cui viene visualizzato un messaggio di successo.
1. Tocca **[!UICONTROL Salva e chiudi]** per completare l&#39;impostazione della configurazione.

### Accesso preconfigurato [!DNL Microsoft Dynamics 365] Modello dati modulo

A [!DNL Microsoft Dynamics 365] Il Modello dati modulo è disponibile come strumento pronto all’uso sulla [!DNL AEM Forms] server dopo di te [configurare un progetto di sviluppo per Forms basato su archetipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Per accedere al modello dati del modulo, passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni di dati]**. L’elenco delle cartelle disponibili include una cartella con il titolo specificato per `DappTitle`  durante [generazione del progetto di archetipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Tocca il nome della cartella, seleziona la **[!UICONTROL Modello dati Microsoft Dynamics 365]**, quindi tocca Modifica ![Modifica](assets/edit.png) per visualizzare il modello dati del modulo.

Dopo aver configurato [[!DNL Microsoft Dynamics 365] Servizio di configurazione cloud](#configure-dynamics-cloud-service), puoi integrare moduli adattivi con [!DNL Microsoft Dynamics 365] Modello dati.
