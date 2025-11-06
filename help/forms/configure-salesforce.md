---
title: Come si configura Salesforce in modelli di dati modulo preconfigurati per Forms adattivo?
description: Scopri come integrare Salesforce con Adaptive Forms.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 184db05b-7237-4dce-8059-03c39b93d7d7
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Configurare Salesforce per AEM Forms {#configure-azure-storage}

L&#39;[[!DNL Experience Manager Forms] integrazione dei dati](data-integration.md) fornisce [!DNL Salesforce] servizi cloud per integrare Adaptive Forms con il modello dati del modulo OOTB (FDM). Il Forms adattivo può quindi interagire con i server [!DNL Salesforce] per abilitare i flussi di lavoro aziendali. Ad esempio:

* Scrivere i dati in [!DNL Salesforce] all&#39;invio del modulo adattivo.
* Scrivere i dati in [!DNL Salesforce] tramite entità personalizzate definite in Form Data Model (FDM) e viceversa.
* Eseguire una query sul server [!DNL Salesforce] per i dati e precompilare Adaptive Forms.
* Lettura dei dati dal server [!DNL Salesforce].

I servizi cloud [!DNL Salesforce] e il modello dati modulo (FDM) sono disponibili sul server [!DNL AEM Forms] dopo aver [configurato un progetto di sviluppo per Forms basato sull&#39;archetipo di Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>[!DNL Salesforce] servizi cloud e Form Data Model (FDM) sono disponibili come predefiniti solo se si imposta un [!DNL Experience Manager Forms] come progetto [!DNL Cloud Service] basato su [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) o versione successiva.

## Configura servizio cloud [!DNL Salesforce] {#configure-salesforce-cloud-service}

Prima di configurare i servizi cloud [!DNL Salesforce], assicurarsi di eseguire le attività seguenti:

* [Crea un&#39;applicazione abilitata per OAuth [!DNL Salesforce] connessa](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&type=5). Quando si crea l&#39;applicazione [!DNL Salesforce] connessa, specificare l&#39;URL di callback nel formato seguente:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Dove server e porta fanno riferimento al nome host e al numero di porta per il server [!DNL AEM Forms].

* Durante la creazione dell&#39;applicazione [!DNL Salesforce] connessa, specificare `full` e `offline_access` come valori per l&#39;ambito OAuth.

* Prendi nota dei valori per l’ID client (denominato Chiave consumer) e il segreto client (denominato Segreto consumer) per l’applicazione connessa.

Per configurare il servizio cloud [!DNL Salesforce], eseguire la procedura seguente:

1. Nell&#39;istanza dell&#39;autore [!DNL AEM Forms], passare a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Origini dati]**.
2. Seleziona il nome della cartella, seleziona **[!UICONTROL Configurazione cloud Salesforce]**, quindi seleziona **[!UICONTROL Proprietà]**.
3. Nella scheda **[!UICONTROL Impostazioni autenticazione]**:
   1. Specificare l&#39;URL del dominio [!DNL Salesforce] nel campo **[!UICONTROL Host]**. Ad esempio, [Nome-dominio].my.salesforce.com.
   2. Specificare l&#39;ID client (chiave consumer) e il segreto client (segreto consumer) per l&#39;applicazione connessa.
   3. Specificare **accesso offline completo** (`full` e `offine_access` valori separati da uno spazio) nel campo **[!UICONTROL Ambito autorizzazione]**.
   4. Seleziona **[!UICONTROL Connetti a OAuth]**. Sei stato reindirizzato alla pagina di accesso [!DNL Salesforce].
   5. Accedi con le credenziali di [!DNL Salesforce] e accetta per consentire alla configurazione del servizio cloud di connettersi al servizio [!DNL Salesforce]. Se la connessione ha esito positivo, si viene reindirizzati alla pagina di configurazione del servizio cloud [!DNL Salesforce], in cui viene visualizzato un messaggio di operazione riuscita.
4. Seleziona **[!UICONTROL Salva e chiudi]** per completare la configurazione.

### Accesso a [!DNL Salesforce] Form Data Model (FDM) preconfigurato

Un [!DNL Salesforce] Form Data Model (FDM) è disponibile nel server [!DNL AEM Forms] dopo che [hai impostato un progetto di sviluppo per Forms basato su Archetipo Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

Per accedere al modello dati modulo (FDM):

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni dati]**.
1. Seleziona il nome della cartella, fai clic su **[!UICONTROL Salesforce Data Model]** e seleziona l&#39;icona Modifica ![Modifica](assets/edit.png) per visualizzare il modello dati del modulo (FDM).

Dopo aver configurato il servizio [[!DNL Salesforce] Cloud Config](#configure-salesforce-cloud-service), puoi integrare moduli adattivi con il modello dati [!DNL Salesforce] pronto all&#39;uso.

>[!MORELIKETHIS]
>
>* [Configura origini dati per AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurare l&#39;archiviazione Azure per AEM Forms](/help/forms/configure-azure-storage.md)
>  [Aggiungi Forms Portal a una pagina AEM Sites](/help/forms/configure-forms-portal.md)
