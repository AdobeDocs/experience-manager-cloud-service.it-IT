---
title: Come configurare i modelli di dati predefiniti per i moduli adattivi per Microsoft Dynamics 365 e Salesforce?
description: Scopri come integrare Microsoft Dynamics 365 e Salesforce con moduli adattivi.
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# Configurazione [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] servizi cloud {#configure-azure-storage}

[[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md) fornisce [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] servizi cloud per integrare moduli adattivi con modelli di dati modulo predefiniti. L&#39;Adaptive Forms può quindi interagire con [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] server per abilitare i flussi di lavoro aziendali. Esempio:

* Scrivere dati in [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] all’invio di moduli adattivi.
* Scrivi dati in [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] attraverso entità personalizzate definite in Form Data Model e viceversa.
* Query [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] server per i dati e precompilare Adaptive Forms.
* Leggi dati da [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] server.

[!DNL Microsoft Dynamics 365] e [!DNL Salesforce] i servizi cloud e i modelli di dati per moduli sono disponibili nella pagina [!DNL AEM Forms] server dopo [impostare un progetto di sviluppo per Forms basato su archetipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft Dynamics 365 e [!DNL Salesforce] i servizi cloud e i modelli di dati per moduli sono disponibili preconfigurati solo se è stata impostata una [!DNL Experience Manager Forms] come [!DNL Cloud Service] basato su [Archetipo AEM 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) o successiva.

## Configura [!DNL Salesforce] servizio cloud {#configure-salesforce-cloud-service}

Prima di configurare la [!DNL Salesforce] servizi cloud, assicurati di eseguire le seguenti attività:

* [Creare un OAuth connesso abilitato [!DNL Salesforce] applicazione](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). Durante la creazione della connessione [!DNL Salesforce] , specifica l’URL di callback nel seguente formato:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Dove server e porta si riferiscono al nome host e al numero di porta per il [!DNL AEM Forms] server.

* Durante la creazione della connessione [!DNL Salesforce] applicazione, specificare `full` e `offline_access` come valori per l’ambito OAuth.

* Prendi nota dei valori per l’ID cliente (noto come Chiave consumatore) e segreto cliente (noto come Segreto consumatore) per l’applicazione connessa.

Esegui i seguenti passaggi per configurare il [!DNL Salesforce] servizio cloud:

1. On [!DNL AEM Forms] istanza autore, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Origini dati]**. L’elenco delle cartelle wrapper disponibili include una cartella con il titolo specificato per `DappTitle`  while [generazione del progetto archetipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Tocca il nome della cartella e seleziona **[!UICONTROL Configurazione cloud Salesforce]**, e tocca **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Impostazioni di autenticazione]** scheda:
   1. Specifica la [!DNL Salesforce] URL di dominio nel **[!UICONTROL Host]** campo . Ad esempio: [Nome di dominio].my.salesforce.com.
   1. Specifica l&#39;ID cliente (indicato come chiave di consumo) e il segreto client (noto come segreto di consumo) per l&#39;applicazione connessa.
   1. Specifica **full offline_access** (`full` e `offine_access` valori separati da uno spazio) nel **[!UICONTROL Ambito di autorizzazione]** campo .
   1. Tocca **[!UICONTROL Connettiti a OAuth]**. Viene reindirizzato a [!DNL Microsoft Dynamics] pagina di accesso.
   1. Accedi con il tuo [!DNL Salesforce] credenziali e accettazione per consentire la connessione della configurazione del servizio cloud [!DNL Salesforce] servizio. Se la connessione ha esito positivo, viene reindirizzato al [!DNL Salesforce] pagina di configurazione del servizio cloud, che visualizza un messaggio di successo.
1. Tocca **[!UICONTROL Salva e chiudi]** per completare la configurazione.

### Accesso immediato [!DNL Salesforce] Modello dati modulo

A [!DNL Salesforce] Il modello dati modulo è disponibile come impostazione predefinita nella [!DNL AEM Forms] server dopo [impostare un progetto di sviluppo per Forms basato su archetipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Per accedere al modello dati modulo, passare a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni dati]**. L’elenco delle cartelle disponibili include una cartella con il titolo specificato per `DappTitle`  while [generazione del progetto archetipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Tocca il nome della cartella e seleziona la **[!UICONTROL Modello dati Salesforce]**, quindi tocca Modifica ![Modifica](assets/edit.png) per visualizzare il modello dati del modulo.

Dopo aver configurato la [[!DNL Salesforce] Servizio di configurazione cloud](#configure-salesforce-cloud-service), è possibile integrare i moduli adattivi con [!DNL Salesforce] Modello dati.

## Configura [!DNL Microsoft Dynamics 365] servizio cloud {#configure-dynamics-cloud-service}

Prima di configurare la [!DNL Microsoft Dynamics 365] cloud service, assicurati di eseguire le seguenti attività:

* [Registra una domanda per [!DNL Microsoft Dynamics 365] con Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). Durante la creazione della connessione [!DNL Microsoft Dynamics 365] , specifica gli URL di risposta nel formato seguente:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Dove server e porta si riferiscono al nome host e al numero di porta per il [!DNL AEM Forms] server.

* Prendi nota dei valori dell’ID client (noto anche come ID applicazione) e del segreto client per l’applicazione connessa.

Esegui i seguenti passaggi per configurare il [!DNL Microsoft Dynamics 365] servizio cloud:

1. On [!DNL AEM Forms] istanza autore, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Origini dati]**. L’elenco delle cartelle wrapper disponibili include una cartella con il titolo specificato per `DappTitle`  while [generazione del progetto archetipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Tocca il nome della cartella e seleziona **[!UICONTROL Configurazione cloud Microsoft Dynamics 365]**, e tocca **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Impostazioni di autenticazione]** scheda:
   1. Immetti il valore per la **[!UICONTROL Directory principale servizio]** campo . Vai all’istanza di Dynamics e passa a [Riferimenti per sviluppatori](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) per visualizzare il valore del campo Directory principale del servizio. Esempio, `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. Specifica l’ID client (indicato come ID applicazione) e il segreto client per l’applicazione connessa.
   1. Sostituisci `{tenant}` con un ID tenant nel **[!UICONTROL URL OAuth]**, **[!UICONTROL Aggiorna URL token]** e **[!UICONTROL URL token di accesso]** campi.
   1. Specifica l’URL dell’istanza di dinamica nel **[!UICONTROL Risorsa]** campo da configurare [!UICONTROL Microsoft Dynamics] con un modello dati modulo. Utilizza l’URL principale del servizio per derivare l’URL dell’istanza Dynamics. Esempio: `https://<tenant-name>.dynamics.com`.

   1. Specifica `openid` in **[!UICONTROL Ambito di autorizzazione]** campo del processo di autorizzazione [!DNL Microsoft Dynamics 365].
   1. Accedi con il tuo [!DNL Microsoft Dynamics 365] credenziali e accettazione per consentire la connessione della configurazione del servizio cloud [!DNL Microsoft Dynamics 365] servizio. Se la connessione ha esito positivo, viene reindirizzato al [!DNL Microsoft Dynamics 365] pagina di configurazione del servizio cloud, che visualizza un messaggio di successo.
1. Tocca **[!UICONTROL Salva e chiudi]** per completare la configurazione.

### Accesso immediato [!DNL Microsoft Dynamics 365] Modello dati modulo

A [!DNL Microsoft Dynamics 365] Il modello dati modulo è disponibile come impostazione predefinita nella [!DNL AEM Forms] server dopo [impostare un progetto di sviluppo per Forms basato su archetipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Per accedere al modello dati modulo, passare a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni dati]**. L’elenco delle cartelle disponibili include una cartella con il titolo specificato per `DappTitle`  while [generazione del progetto archetipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Tocca il nome della cartella e seleziona la **[!UICONTROL Modello dati di Microsoft Dynamics 365]**, quindi tocca Modifica ![Modifica](assets/edit.png) per visualizzare il modello dati del modulo.

Dopo aver configurato la [[!DNL Microsoft Dynamics 365] Servizio di configurazione cloud](#configure-dynamics-cloud-service), è possibile integrare i moduli adattivi con [!DNL Microsoft Dynamics 365] Modello dati.
