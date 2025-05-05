---
title: Configura AEM Assets as a [!DNL Cloud Service]  con Brand Portal
description: Scopri come configurare AEM Assets con Brand Portal. La configurazione consente di pubblicare su Brand Portal le risorse del brand approvate da un’istanza di AEM e distribuirle agli utenti Brand Portal.
contentOwner: AK
feature: Brand Portal, Asset Distribution, Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 11%

---

# Configurare Experience Manager Assets con Brand Portal {#configure-aem-assets-with-brand-portal}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

La configurazione di Adobi Experience Manager Assets Brand Portal consente di pubblicare le risorse del brand approvate da Adobe Experience Manager Assets come istanza [!DNL Cloud Service] in Brand Portal e distribuirle agli utenti Brand Portal.

## Attivare Brand Portal tramite Cloud Manager {#activate-brand-portal}

L&#39;utente Cloud Manager attiva Brand Portal per un Experience Manager Assets come istanza [!DNL Cloud Service]. Il flusso di lavoro di attivazione crea le configurazioni richieste (token di autorizzazione, configurazione IMS e Brand Portal Cloud Service) nel back-end e riflette lo stato del tenant Brand Portal in Cloud Manager. L’attivazione di Brand Portal consente agli utenti di Experience Manager Assets di pubblicare le risorse in Brand Portal e distribuirle agli utenti di Brand Portal.

**Prerequisiti**

Per attivare Brand Portal nel Experience Manager Assets come istanza [!DNL Cloud Service] è necessario quanto segue:

* Experience Manager Assets in esecuzione come istanza [!DNL Cloud Service].
* Utente con accesso a Cloud Manager, assegnato ai profili del prodotto Cloud Manager. Per ulteriori informazioni, vedere [Accesso a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=it#accessing-cloud-manager).

>[!NOTE]
>
>Per connettersi al tenant Brand Portal è necessario un ambiente di produzione configurato per un&#39;istanza di Experience Manager Assets come [!DNL Cloud Service].

**Passaggi per attivare Brand Portal**

È possibile attivare Brand Portal durante la creazione degli ambienti di produzione per Experience Manager Assets come istanza [!DNL Cloud Service] o separatamente. Supponiamo che l’ambiente sia già stato creato e che ora sia necessario attivare Brand Portal.

1. Accedi ad Adobe Cloud Manager e passa a **[!UICONTROL Ambienti]**.

   Nella pagina **[!UICONTROL Ambienti]** viene visualizzato l&#39;elenco di tutti gli ambienti esistenti.

1. Seleziona gli ambienti (uno alla volta) dall’elenco per visualizzarne i dettagli.

   Brand Portal ha diritto a uno degli ambienti disponibili e si riflette nelle **[!UICONTROL Informazioni sull&#39;ambiente]**.

   Dopo aver individuato l&#39;ambiente associato a Brand Portal, fare clic sul pulsante **[!UICONTROL Attiva Brand Portal]** per avviare il flusso di lavoro di attivazione.

   ![Attiva Brand Portal](assets/create-environment4.png)

1. L’attivazione del tenant Brand Portal richiede alcuni minuti, poiché il flusso di lavoro di attivazione crea le configurazioni richieste nel backend. Una volta attivato il tenant Brand Portal, lo stato diventa Attivato.

   ![Visualizza stato](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal deve essere attivato sulla stessa organizzazione IMS di Experience Manager Assets come istanza [!DNL Cloud Service].
>
>Se disponi di una configurazione cloud di Brand Portal esistente ([configurata manualmente utilizzando Adobe Developer Console](#manual-configuration)) per un&#39;organizzazione IMS (organizzazione1-esistente) e la tua istanza di Experience Manager Assets come [!DNL Cloud Service] è configurata per un&#39;altra organizzazione IMS (organizzazione2-nuova), l&#39;attivazione di Brand Portal da Cloud Manager reimposta l&#39;organizzazione Brand Portal IMS su `org2-new`. Anche se la configurazione cloud configurata manualmente in `org1-existing` è visibile nell&#39;istanza di authoring di Experience Manager Assets, ma non sarà più in uso dopo l&#39;attivazione di Brand Portal da Cloud Manager.
>
>Se la configurazione cloud di Brand Portal esistente e Experience Manager Assets come istanza [!DNL Cloud Service] utilizzano la stessa organizzazione IMS (org1), devi attivare Brand Portal solo da Cloud Manager.
>
>Non modificare le impostazioni generate automaticamente.

**Vedere anche**:

* [Aggiungere utenti e ruoli in Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=it)

* [Gestione degli ambienti in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=it#adding-environments)


**Accedi al tuo tenant Brand Portal**:

Dopo l’attivazione del tenant Brand Portal in Cloud Manager, puoi accedere a Brand Portal da Admin Console o utilizzando direttamente l’URL del tenant.

L&#39;URL predefinito del tenant Brand Portal è: `https://<tenant-id>.brand-portal.adobe.com/`.

L’ID tenant è l’organizzazione IMS.


Se non sei sicuro dell’URL di Brand Portal, effettua le seguenti operazioni:

1. Accedi a [Admin Console](https://adminconsole.adobe.com/) e passa a **[!UICONTROL Products]**.
1. Dal pannello a sinistra, seleziona **[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**.
1. Fai clic su **[!UICONTROL Vai a Brand Portal]** per aprire direttamente Brand Portal nel browser.

   In alternativa, copia l&#39;URL del tenant Brand Portal dal collegamento **[!UICONTROL Vai a Brand Portal]** e incollalo nel browser per aprire l&#39;interfaccia di Brand Portal.

   ![Accedi a Brand Portal](assets/access-bp-on-cloud.png)


**Verifica connessione**

Per convalidare la connessione tra Experience Manager Assets come istanza [!DNL Cloud Service] e il tenant Brand Portal, effettua le seguenti operazioni:

1. Accedi a Experience Manager Assets.

1. Dal pannello **Strumenti**, passa a **[!UICONTROL Distribuzione]** > **[!UICONTROL Distribuzione]**.

   ![Passa all&#39;opzione di distribuzione](assets/test-bpconfig1.png)

   Un agente di distribuzione Brand Portal (**[!UICONTROL bpdistributionagent0]**) è stato creato in **[!UICONTROL Pubblica in Brand Portal]**.

   ![Crea agente di distribuzione](assets/test-bpconfig2.png)

1. Fare clic su **[!UICONTROL Pubblica in Brand Portal]** per aprire l&#39;agente di distribuzione.

   Puoi visualizzare le code di distribuzione nella scheda **[!UICONTROL Stato]**.

   Un agente di distribuzione contiene due code:
   * **Coda di elaborazione**: per la distribuzione delle risorse in Brand Portal.

   * **Coda di errore**: per le risorse per le quali la distribuzione non è riuscita.

   >[!NOTE]
   >
   >È consigliabile esaminare gli errori e cancellare periodicamente la **coda di errore**.

   ![Elaborazione coda per la distribuzione delle risorse](assets/test-bpconfig3.png)

1. Per verificare la connessione tra Experience Manager Assets as a [!DNL Cloud Service] e Brand Portal, fare clic sull&#39;icona **[!UICONTROL Verifica connessione]**.

   ![Verifica connessione tra AEM e Brand Portal](assets/test-bpconfig4.png)

   Viene visualizzato un messaggio che informa che il pacchetto di prova *è stato consegnato correttamente*.

   >[!NOTE]
   >
   >Evita di disabilitare l’agente di distribuzione, in quanto potrebbe impedire la corretta distribuzione delle risorse (in esecuzione nella coda).

Per verificare la connessione tra l&#39;istanza di Experience Manager Assets come [!DNL Cloud Service] e il tenant di Brand Portal, pubblicare una risorsa da Experience Manager Assets a Brand Portal. Se la connessione ha esito positivo, la risorsa pubblicata è visibile nell’interfaccia di Brand Portal.


Ora puoi:

* [Pubblicare risorse da Experience Manager Assets a Brand Portal](publish-to-brand-portal.md)
* [Pubblicare cartelle da Experience Manager Assets a Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Pubblicare raccolte da Experience Manager Assets a Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Pubblicare risorse da Brand Portal in Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=it) - Origine risorse in Brand Portal
* [Pubblicare predefiniti, schemi e facet in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=it)
* [Pubblicare tag in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=it)

Per ulteriori informazioni, consulta la [documentazione di Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=it).

**Registri di distribuzione**

Puoi monitorare i registri dell’agente di distribuzione per il flusso di lavoro di pubblicazione delle risorse.

Ora pubblichiamo una risorsa da Experience Manager Assets a Brand Portal e visualizziamo i registri.

1. Segui i passaggi da 1 a 4 descritti nella sezione **Verifica connessione** e passa alla pagina dell&#39;agente di distribuzione.
1. Fai clic su **[!UICONTROL Registri]** per visualizzare i registri di elaborazione e di errore.

   ![Elaborazione e registri errori](assets/test-bpconfig5.png)

L’agente di distribuzione ha generato i seguenti registri:

* INFO: si tratta di un registro generato dal sistema e viene attivato in caso di configurazione corretta dell’agente di distribuzione.
* DSTRQ1 (richiesta 1): si attiva durante la prova della connessione.

Quando viene pubblicata la risorsa, vengono generati i seguenti registri di richieste e risposte:

**Richiesta dell’agente di distribuzione**:

* DSTRQ2 (richiesta 2): viene attivata la richiesta di pubblicazione della risorsa.
* DSTRQ3 (richiesta 3): il sistema attiva un’altra richiesta per pubblicare la cartella Experience Manager Assets (in cui si trova la risorsa) e replica la cartella in Brand Portal.

**Risposta dell’agente di distribuzione**:

* queue-bpdistributionagent0 (DSTRQ2): la risorsa viene pubblicata su Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): il sistema replica la cartella Experience Manager Assets (contenente la risorsa) in Brand Portal.

Nell’esempio precedente, viene attivata un’ulteriore combinazione di richiesta e risposta. Impossibile trovare la cartella principale (Aggiungi percorso) in Brand Portal perché la risorsa è stata pubblicata per la prima volta, pertanto è stata attivata un’ulteriore richiesta per creare una cartella principale con lo stesso nome in Brand Portal in cui viene pubblicata la risorsa.

>[!NOTE]
>
>Se la cartella principale non esiste in Brand Portal o è stata modificata in Experience Manager Assets, viene generata un’ulteriore richiesta.

Oltre al flusso di lavoro di automazione per attivare Brand Portal su Experience Manager Assets come [!DNL Cloud Service], esiste un altro metodo per configurare manualmente Experience Manager Assets come [!DNL Cloud Service] con Brand Portal utilizzando Adobe Developer Console, che non è più consigliato.

>[!NOTE]
>
>Se riscontri problemi durante l’attivazione del tenant Brand Portal, contatta l’Assistenza clienti.

## Configurazione manuale con Adobe Developer Console {#manual-configuration}

>[!NOTE]
>
> Non puoi creare nuove credenziali JWT da giugno 2024 in poi. D’ora in poi, verranno create solo le credenziali OAuth.
> Ulteriori informazioni [sulla creazione di una configurazione OAuth](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration:~:text=For%20example%3A-,Creating%20an%20OAuth%20configuration,-To%20create%20a).

Nella sezione seguente viene descritto come configurare manualmente Experience Manager Assets as a [!DNL Cloud Service] con Brand Portal utilizzando Adobe Developer Console.

In precedenza, Experience Manager Assets as a [!DNL Cloud Service] era stato configurato manualmente con Brand Portal tramite Adobe Developer Console, che fornisce un token di account Adobe Identity Management Services (IMS) per l&#39;autorizzazione del tenant Brand Portal. Richiede configurazioni sia in Experience Manager Assets che in Adobe Developer Console.

<!--1. In Experience Manager Assets, create an IMS account and generate a public key (certificate).-->
<!--1. Under the project, configure an API using the public key to create a service account connection.
1. Get the service account credentials and JSON Web Token (JWT) payload information.
1. In Experience Manager Assets, configure the IMS account using the service account credentials and JWT payload.-->
1. In Adobe Developer Console, crea un progetto per il tenant Brand Portal (organizzazione).
1. In Experience Manager Assets, configura il servizio cloud Brand Portal utilizzando l’account IMS e l’endpoint Brand Portal (URL organizzazione).
1. Verifica la configurazione pubblicando una risorsa da Experience Manager Assets a Brand Portal.

>[!NOTE]
>
>Un&#39;istanza di Experience Manager Assets come [!DNL Cloud Service] deve essere configurata con un solo tenant Brand Portal.

**Prerequisiti**

Per configurare Experience Manager Assets con Brand Portal è necessario quanto segue:

* Experience Manager Assets in esecuzione come istanza [!DNL Cloud Service]
* URL tenant Brand Portal
* Utente con privilegi di amministratore di sistema nell’organizzazione IMS del tenant Brand Portal

## Crea configurazione {#create-new-configuration}

Per configurare Experience Manager Assets con Brand Portal, effettua le seguenti operazioni nella sequenza specificata.

1. [Configurare le credenziali OAuth in Adobe Developer Console](#config-oauth)
1. [Creare una nuova integrazione Adobe IMS utilizzando OAuth](#create-ims-account-configuration)
1. [Configurare il servizio cloud](#configure-cloud-service)
   <!--1. [Obtain public certificate](#public-certificate)-->
<!--1. [Create service account (JWT) connection](#createnewintegration) 
1. [Configure IMS account](#create-ims-account-configuration)-->

<!--
### Create IMS configuration {#create-ims-configuration}

The IMS configuration authenticates your Experience Manager Assets as a [!DNL Cloud Service] instance with the Brand Portal tenant. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)
-->
<!--

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your profile on Adobe Developer Console.

1. Login to Experience Manager Assets.
1. From the **Tools** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.
1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. It will redirect to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. By default, the **Certificate** tab opens.
1. Select **[!UICONTROL Adobe Brand Portal]** in the **[!UICONTROL Cloud Solution]** drop-down list.  
1. Select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 
1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

   ![Create Certificate](assets/ims-config2.png)

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (CRT) file on your machine.

   The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.  

   ![Download Certificate](assets/ims-config3.png)

1. Click **[!UICONTROL Next]**.

    In the **Account** tab, Adobe IMS account is created which requires the service account credentials that are generated in Adobe Developer Console. Keep this page open for now.

    Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration) to get the credentials and JWT payload for configuring the IMS account. 
-->
<!--

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at Brand Portal tenant (organization) level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. To configure Experience Manager Assets with Brand Portal, you must generate a public key (certificate) in Experience Manager Assets and create credentials in Adobe Developer Console by uploading the public key. These credentials are required to configure the IMS account in Experience Manager Assets. Once the IMS account is configured, you can configure the Brand Portal cloud service in Experience Manager Assets.

Perform the following steps to generate the service account credentials and JWT payload:

1. Login to Adobe Developer Console with system administrator privileges on the IMS organization (Brand Portal tenant). The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Ensure that you have selected the correct IMS organization (Brand Portal tenant) from the drop-down (organization) list located at the upper-right corner.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]** to update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**. 

   Ensure that you have access to the Experience Manager Brand Portal service.

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Then, click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. 

   Click **[!UICONTROL Next]**.

   ![Upload Public Key](assets/service-account3.png)

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Assets Brand Portal]** as the default product profile and click **[!UICONTROL Save configured API]**. 

   ![Select Product Profile](assets/service-account4.png)

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option.

   >[!NOTE] 
   >
   >* You can view the credentials and perform actions such as generate JWT tokens, copy credential details, retrieve client secret, and so on.
   >* Currently, only the Adobe's Developer Console Service Account (JWT) credential type is supported. Do not use the `OAuth Server-to-Server` credential type until it is supported in mid-April. Read more at [JWT Credentials Deprecation in Adobe Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=it).

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Service Account Credentials](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in Experience Manager Assets.
-->
<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create an integration page. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information is used to create IMS account configuration.

-->

### Configurare le credenziali OAuth in Adobe Developer Console {#config-oauth}

[Configura le credenziali OAuth in Adobe Developer Console](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#credentials-in-the-developer-console) e seleziona Brand Portal API.

### Creare una nuova integrazione Adobe IMS utilizzando OAuth {#create-ims-account-configuration}

[Crea una nuova integrazione Adobe IMS utilizzando OAuth](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration) e seleziona Brand Portal dal menu a discesa in Soluzione cloud.

<!--
Ensure that you have performed the following steps:

* [Obtain public certificate](#public-certificate)
* [Create service account (JWT) connection](#createnewintegration)
-->

<!--1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. Keep the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)  
-->
<!--
1. Complete the configuration based on details from the [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). Click **[!UICONTROL Create]**.
-->
<!--Specify client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

   The IMS account is configured. 

   ![IMS Account configuration](assets/create-new-integration6.png)

 <!--  
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![Adobe IMS Configurations Check Health.](assets/create-new-integration5.png)
-->
<!--
>[!CAUTION]
>
>You must have only one IMS configuration.
>
>Ensure that the IMS configuration passes the health check. If the configuration does not pass the health check, it is invalid. You must delete it and create another valid configuration.
-->

### Configurare il servizio cloud {#configure-cloud-service}

Per configurare il servizio cloud Brand Portal, effettua le seguenti operazioni:

1. Accedi a Experience Manager Assets.

1. Dal pannello **Strumenti**, passa a **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Nella pagina Configurazioni Brand Portal, fai clic su **[!UICONTROL Crea]**.

1. Specifica un **[!UICONTROL titolo]** per la configurazione.

   Seleziona la configurazione IMS creata durante [la configurazione dell&#39;account IMS](#create-ims-account-configuration).

   Nel campo **[!UICONTROL URL servizio]**, specifica l&#39;URL del tenant Brand Portal (organizzazione).

   ![Finestra di dialogo Configurazione Brand Portal.](assets/create-cloud-service.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**. Viene creata la configurazione cloud.

   L&#39;istanza di Experience Manager Assets come [!DNL Cloud Service] è ora configurata con il tenant Brand Portal.

Ora puoi testare la configurazione controllando l’agente di distribuzione e pubblicando le risorse in Brand Portal.

**se l&#39;anteprima protetta è abilitata, gli indirizzi IP in uscita in SPS verranno Inseriti nell&#39;elenco Consentiti**
Se si utilizza Dynamic Media-Scene7 con [anteprima protetta abilitata](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=it) per una società, si consiglia all&#39;amministratore della società Scene7 [di inserire nell&#39;elenco Consentiti gli IP pubblici in uscita](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=it#testing-the-secure-testing-service) per le rispettive aree tramite l&#39;interfaccia utente flash di SPS (Scene7 Publishing System).
Gli IP in uscita sono i seguenti:

| **Area** | **IP in uscita** |
|--- |--- |
| ND | 130.248.160.68, 20.94.203.130 |
| EMEA | 51.132.146.75, 130.248.244.202, 130.248.244.203, 130.248.244.204, 130.248.244.210, 130.248.244.211, 130.248.244.212 |
| APAC | 63.140.44.54 |

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Login to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![test-bpconfig1](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![test-bpconfig2](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![test-bpconfig3](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![test-bpconfig4](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=it) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=it)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=it)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=it) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![ctest-bpconfig4](assets/ctest-bpconfig4.png)

The distribution agent has generated the following logs:

* INFO: This is a system-generated log that triggers on successful configuration of the distribution agent. 
* DSTRQ1 (Request 1): Triggers on test connection.

On publishing the asset, the following request and response logs are generated:

**Distribution agent request**:

* DSTRQ2 (Request 2): The asset publishing request is triggered.
* DSTRQ3 (Request 3): The system triggers another request to publish the AEM Assets folder (in which the asset exists) and replicates the folder in Brand Portal.

**Distribution agent response**:

* queue-bpdistributionagent0 (DSTRQ2): The asset is published to Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): The system replicates the AEM Assets folder (containing the asset) in Brand Portal.

In the above example, an additional request and response is triggered. The system could not find the parent folder (Add Path) in Brand Portal because the asset was published for the first time, therefore, it triggered an additional request to create a parent folder with the same name in Brand Portal where the asset is published.  

>[!NOTE]
>
>Additional request is generated in case the parent folder does not exist in Brand Portal or has been modified in AEM Assets. 
-->

<!--

## Additional information {#additional-information}

Go to `/system/console/slingmetrics` for statistics related to the distributed content:

1. **Counter metrics**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Time metrics**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`

-->

<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
-->

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
