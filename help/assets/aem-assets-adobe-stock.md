---
title: Gestisci [!DNL Adobe Stock] risorse in [!DNL Assets].
description: Cerca, recupera, concedi licenze e gestisci [!DNL Adobe Stock] risorse da [!DNL Adobe Experience Manager]. Utilizza le risorse concesse in licenza come qualsiasi altra risorsa digitale.
contentOwner: Vishabh Gupta
feature: Adobe Stock
role: Admin, User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 4%

---

# Usa [!DNL Adobe Stock] risorse in [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/aem-assets-adobe-stock.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Il servizio [!DNL Adobe Stock] consente ai designer e alle aziende di accedere a milioni di foto, vettori, illustrazioni, video, modelli e risorse 3D di alta qualità e curate, senza royalty, per tutti i progetti creativi.

[!DNL Adobe Stock] per l&#39;offerta Enterprise, per impostazione predefinita, include i diritti di condivisione in tutta l&#39;organizzazione. Una volta che una risorsa è stata concessa in licenza da un utente dell’organizzazione, altri utenti dell’organizzazione possono identificarla, scaricarla e utilizzarla senza doverla concedere nuovamente in licenza. Una volta che una risorsa è stata concessa in licenza dalla tua organizzazione, il diritto di utilizzarla è permanente.

Le organizzazioni possono integrare il piano [!DNL Adobe Stock] aziendale con [!DNL Experience Manager Assets] per garantire che le risorse concesse in licenza siano ampiamente disponibili per i progetti creativi e di marketing, con le potenti funzionalità di gestione delle risorse di [!DNL Experience Manager]. [!DNL Experience Manager] utenti possono trovare, visualizzare in anteprima e concedere in licenza le risorse Adobe Stock salvate in [!DNL Experience Manager] senza uscire dall&#39;interfaccia [!DNL Experience Manager].

## Prerequisiti per integrare [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] consente agli utenti di cercare, visualizzare in anteprima, salvare e concedere in licenza [!DNL Adobe Stock] risorse direttamente da [!DNL Experience Manager].

Per abilitare questa integrazione, soddisfa i seguenti requisiti:

* [!DNL Experience Manager Assets] in esecuzione come istanza [!DNL Cloud Service].
* Un piano [!DNL Adobe Stock] dell&#39;organizzazione.
* Un utente con autorizzazioni in [!DNL Admin Console] per il profilo di prodotto Stock predefinito.
* Utente con autorizzazioni per [!DNL Developer Access profile] per la creazione dell&#39;integrazione in [!DNL Adobe Developer Console].

Un piano [!DNL Adobe Stock] dell&#39;organizzazione

* Fornisce prodotti autorizzati per [!DNL Adobe Stock] (scorte connesse ad Experience Manager).
* Crediti acquistati in [!DNL Adobe Admin Console] per il tuo diritto sulle azioni.
* Consente di gestire i crediti e le licenze a livello globale da [!DNL Adobe Admin Console].

All&#39;interno del diritto, esiste un profilo di prodotto predefinito per [!DNL Adobe Stock] in [!DNL Admin Console]. È possibile creare più profili, che determinano chi può concedere in licenza le risorse Stock. Un utente con accesso diretto al profilo di prodotto può accedere a [https://stock.adobe.com/](https://stock.adobe.com/it) e alle risorse Stock della licenza. Esiste invece un altro metodo per utilizzare Developer Access per creare un’integrazione (API). Questa integrazione autentica la comunicazione tra [!DNL Experience Manager Assets] e [!DNL Adobe Stock].

<!--
### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).
-->

<!-- 
TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in User Preferences panel. To access the panel from Experience Manager home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.
-->

## Integrare [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-adobe-stock-with-aem-assets}

Come sviluppatore, eseguire i passaggi seguenti per integrare [!DNL Adobe Experience Manager] e [!DNL Adobe Stock].

<!--
1. [Obtain public certificate](#public-certificate)
   
   In [!DNL Experience Manager], create an IMS account and generate a public certificate (public key).

1. [Create service account (JWT) connection](#createnewintegration) 
   
   In [!DNL Adobe Developer Console], create a project for your [!DNL Adobe Stock] organization. Under the project, configure an API using the public key to create a service account (JWT) connection. Get the service account credentials and JWT payload information.

1. [Configure IMS account](#create-ims-account-configuration)

   In [!DNL Experience Manager], configure the IMS account using the service account credentials and JWT payload.

1. [Configure cloud service](#configure-the-cloud-service)

   In [!DNL Experience Manager], configure an [!DNL Adobe Stock] cloud service using the IMS account.


### Create an IMS configuration {#create-an-ims-configuration}

The IMS configuration authenticates your [!DNL Experience Manager Assets] author instance with the [!DNL Adobe Stock] entitlement. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your product profile in Adobe Developer Console.

1. Log in to your [!DNL Experience Manager Assets] cloud instance.

1. From the **[!UICONTROL Tools]** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. The **[!UICONTROL Adobe IMS Technical Account Configuration]** page opens. 

1. In the **[!UICONTROL Certificate]** tab, select **[!UICONTROL Adobe Stock]** from the **[!UICONTROL Cloud Solution]** drop-down list.  

1. You can create a certificate or reuse an existing certificate for the configuration. 

   To create a certificate, select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 

1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine. The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.

   Click **[!UICONTROL Next]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. In the **Account** tab, Adobe IMS account is created which requires the service account credentials.

   Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration). 

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at organization level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. In this example, the service account credentials are generated by uploading the public key.

To generate the service account credentials and JWT payload:

1. Log in to Adobe Developer Console with system administrator privileges. The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Ensure that you have selected the correct IMS organization (Stock entitlement) from the drop-down (organization) list.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]**. Update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and then click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL Adobe Stock]**. Click **[!UICONTROL Next]**. 

1. In the **[!UICONTROL Configure API]** window, select **[!UICONTROL Service Account (JWT)]** authentication. Click **[!UICONTROL Next]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Click **[!UICONTROL Upload your public key]**. Click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. Click **[!UICONTROL Next]**.

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select the default **[!UICONTROL Adobe Stock]** product profile and click **[!UICONTROL Save configured API]**. 

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option. Here, you can view the credentials and perform actions such as generate JWT tokens, copy credential details, and retrieve client secret.

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### Configure IMS account {#create-ims-account-configuration}

You must have the [certificate](#public-certificate) and [service account (JWT) credentials](#createnewintegration) to configure the IMS account.

To configure the IMS account: 

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, enter the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).  

   Enter the client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

1. Click **[!UICONTROL Create]**. An IMS account configuration is created. 

   ![configure-ims-acount](assets/aem-stock-ims-config.png)
   
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![health-check](assets/aem-stock-healthcheck.png)
-->

1. [Configura un programma in [!DNL Developer Console]](#set-up-a-program-in-developer-console)
1. [Aggiungi configurazione nell&#39;istanza di authoring  [!DNL AEM] &#x200B;](#add-configuration-in-the-aem-author-instance)

### Configura un programma in [!DNL Developer Console] {#set-up-a-program-in-developer-console}

Eseguire la procedura seguente per configurare un programma in [!DNL Developer Console]:
1. Passa a [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/14431/user/servicesandapis) e accedi alla tua organizzazione.
1. Seleziona **[!UICONTROL Crea nuovo progetto]** disponibile nel dashboard **[!UICONTROL Progetti]**.
   ![integrare risorse aem con adobe stock](/help/assets/assets/create-new-project-in-adobe-dev-console.png)
1. Fai clic su **[!UICONTROL Aggiungi al progetto]** e seleziona **[!UICONTROL API]**.
1. Seleziona **[!UICONTROL Adobe Stock]** e fai clic su **[!UICONTROL Avanti]**.
1. Specifica un **[!UICONTROL nome credenziali]** e verifica che **[!UICONTROL OAuth Server-to-Server]** sia selezionato, quindi fai clic su **[!UICONTROL Avanti]**.
1. Seleziona **[!UICONTROL AEM Assets]** **[!UICONTROL Profilo di prodotto]** e fai clic su **[!UICONTROL Salva API configurata]**. Viene visualizzato un messaggio di operazione riuscita per confermare che hai creato un progetto in [!DNL Developer Console]. Verrà aperto il dashboard del progetto con il nome del progetto nella parte superiore, **[!UICONTROL Adobe Stock]** in **[!UICONTROL APIS]** e **[!UICONTROL AEM Assets]** in **[!UICONTROL Profilo di prodotto]** e **[!UICONTROL Scheda credenziali da server a server OAuth]** in **[!UICONTROL Credenziali connesse]**.
   ![integrare aem assets e adobe stock](/help/assets/assets/adc-project-name.png)
1. Seleziona la scheda di credenziali da server a server **[!UICONTROL OAuth]** e vengono visualizzati i **[!UICONTROL Dettagli credenziali]**. Utilizza questi [!DNL OAuth Server-to-Server] dettagli delle credenziali del progetto, ad esempio **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]**, **[!UICONTROL Ambito]**, **[!UICONTROL Nome credenziali]**, **[!UICONTROL ID account tecnico]**, **[!UICONTROL ID organizzazione]** per [aggiungere la configurazione nell&#39;istanza di authoring di AEM](#add-configuration-in-the-aem-author-instance).
   ![risorse aem e adobe stock](/help/assets/assets/oauth-server-server-credentials-details-page.png)

### Aggiungi configurazione nell&#39;istanza di authoring [!DNL AEM] {#add-configuration-in-the-aem-author-instance}

Per aggiungere la configurazione nell&#39;istanza di authoring [!DNL AEM], eseguire la procedura seguente:

1. [Configura un nuovo [!DNL Adobe Stock IMS configuration] nell&#39;istanza dell&#39;autore [!DNL AEM] &#x200B;](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)
1. [Aggiungi la configurazione cloud a cui connettersi [!DNL Adobe Stock]](#add-cloud-configuration-to-connect-adobe-stock)

#### Configura un nuovo [!DNL Adobe Stock IMS configuration] nell&#39;istanza [!DNL AEM author] {#set-up-adobe-stock-ims-configuration-in-aem-author-instance}

Eseguire la procedura seguente per configurare un nuovo [!DNL Adobe Stock IMS configuration] nell&#39;istanza di authoring [!DNL AEM]:
1. Passa all&#39;istanza dell&#39;autore [!DNL AEM].
1. Fai clic su ![aem assets and adobe stock](/help/assets/assets/Hammer.svg), seleziona **[!UICONTROL Security]** e seleziona **[!UICONTROL Adobe IMS Configurations]**.
1. Fai clic su **[!UICONTROL Crea]** per creare una nuova configurazione IMS. Nella pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]** sono visualizzati più campi, ad esempio **[!UICONTROL Soluzione cloud]**, **[!UICONTROL Titolo]**, **[!UICONTROL Server autorizzazioni]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]**, **[!UICONTROL Ambito]** e **[!UICONTROL ID organizzazione]**. Segui queste istruzioni per specificare i dettagli in questi campi:
   * **[!UICONTROL Soluzione cloud]**: Selezionare **[!UICONTROL Adobe Stock]**.
   * **[!UICONTROL Titolo]**: specifica un nome per questa integrazione.
   * **[!UICONTROL Server autorizzazioni]**: aggiungere [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/) come server autorizzazioni.
   * **[!UICONTROL ID client]**: passa al dashboard del progetto, fai clic sull&#39;opzione **[!UICONTROL OAuth Server-to-Server]** disponibile nel riquadro a sinistra, seleziona **[!UICONTROL Dettagli credenziali]**, copia il **[!UICONTROL ID client]** e incollalo qui (vedi [passaggio 7](#set-up-a-program-in-developer-console)).

   * **[!UICONTROL Segreto client]**: passa al dashboard del progetto, fai clic sull&#39;opzione **[!UICONTROL OAuth Server-to-Server]** disponibile nel riquadro a sinistra, seleziona **[!UICONTROL Dettagli credenziali]**, fai clic su **[!UICONTROL Recupera segreto client]**, copia il **[!UICONTROL segreto client]** e incollalo qui (vedi [passaggio 7](#set-up-a-program-in-developer-console)).

   * **[!UICONTROL Ambito]**: passa al dashboard del progetto, fai clic sull&#39;opzione **[!UICONTROL OAuth Server-to-Server]** disponibile nel riquadro a sinistra, seleziona **[!UICONTROL Dettagli credenziali]**, copia **[!UICONTROL Ambito]** e incollalo qui (vedi [passaggio 7](#set-up-a-program-in-developer-console)).

   * **[!UICONTROL ID organizzazione]**: passa al dashboard del progetto, fai clic sull&#39;opzione **[!UICONTROL OAuth Server-to-Server]** disponibile nel riquadro a sinistra, seleziona **[!UICONTROL Dettagli credenziali]**, copia il **[!UICONTROL ID organizzazione]** e incollalo qui (vedi [passaggio 7](#set-up-a-program-in-developer-console)).

     ![risorse aem e adobe stock](/help/assets/assets/adobe-ims-technical-account-configuration.png)
1. Fai clic su **[!UICONTROL Crea]**. Viene aperta la pagina **[!UICONTROL Configurazioni Adobe IMS]** in cui viene visualizzata l&#39;integrazione [!DNL Adobe Stock] creata.

#### Aggiungi la configurazione cloud per la connessione a [!DNL Adobe Stock] {#add-cloud-configuration-to-connect-adobe-stock}

Eseguire la procedura seguente per aggiungere la configurazione cloud per connettersi a [!DNL Adobe Stock]:

1. Passa all&#39;istanza [!DNL AEM author].
1. Fai clic su ![aem assets and adobe stock](/help/assets/assets/Hammer.svg), seleziona **[!UICONTROL Cloud Services]**, sfoglia e seleziona **[!UICONTROL Adobe Stock]**.
   ![utilizzo di adobe stock con aem](/help/assets/assets/adding-cloud-config-to-adobe-stock.png)
1. Fare clic su **[!UICONTROL Crea]** e nella pagina **[!UICONTROL Configurazione Adobe Stock]** sono visualizzati più campi. Segui queste istruzioni per specificare i dettagli in questi campi:
   * **[!UICONTROL Titolo]**: passa alla pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]** (vedi [passaggio 3](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)), copia il titolo e incollalo qui.
   * **[!UICONTROL Configurazione Adobe IMS associata]**: seleziona l&#39;integrazione [!DNL Adobe Stock] creata.
   * **[!UICONTROL Lingua]**: Seleziona **[!UICONTROL Inglese (Stati Uniti)]**.
1. Fai clic su **[!UICONTROL Salva e chiudi]**.
   ![utilizzo di adobe stock con aem](/help/assets/assets/adobe-stock-config-page.png)

<!--
### Configure cloud service {#configure-the-cloud-service}

To configure the [!DNL Adobe Stock] cloud service:

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. In the [!DNL Adobe Stock Configurations] page, click **[!UICONTROL Create]**.

1. Specify a **[!UICONTROL Title]** for the cloud configuration. 

   Select the IMS configuration that you have created while [configuring the IMS account](#create-ims-account-configuration).

   Select your locale from the drop-down list.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Click **[!UICONTROL Save & Close]**. 
-->
L&#39;istanza dell&#39;autore [!DNL Experience Manager Assets] è ora integrata con [!DNL Adobe Stock]. È possibile creare più configurazioni di [!DNL Adobe Stock] (ad esempio, configurazioni basate sulle impostazioni locali). È ora possibile accedere, cercare e concedere in licenza le risorse [!DNL Adobe Stock] dall&#39;interfaccia utente di [!DNL Experience Manager].

![risorse-magazzino-ricerca](assets/aem-stock-searchstocks.png)

>[!NOTE]
>
>In questa fase dell&#39;integrazione, solo gli amministratori possono accedere alle risorse [!DNL Adobe Stock], cercare le risorse Stock (utilizzando omnisearch) e concedere in licenza le risorse [!DNL Adobe Stock].
>
>Gli amministratori possono aggiungere altri utenti o gruppi al servizio cloud [!DNL Adobe Stock] e concedere autorizzazioni a questi utenti non amministratori in [!DNL Experience Manager] per accedere alla configurazione Stock.

1. Per aggiungere utenti o gruppi, selezionare la configurazione cloud [!DNL Adobe Stock] e fare clic su **[!UICONTROL Proprietà]**.

1. Cerca per aggiungere gli utenti o i gruppi ai quali hai assegnato le autorizzazioni per accedere alla configurazione di Adobe Stock. Vedi [assegnare le autorizzazioni al gruppo di utenti](#assign-permissions-to-group).


## Assegna autorizzazioni a gruppo di utenti {#assign-permissions-to-group}

Gli amministratori possono creare gruppi di utenti e concedere autorizzazioni ad alcuni utenti o gruppi per accedere al servizio cloud [!DNL Adobe Stock].

Di seguito sono riportate le autorizzazioni necessarie affinché un utente possa cercare e concedere in licenza le risorse Adobe Stock:

* Configura il percorso: `/conf/global/settings/stock`
* Privilegi: `jcr:read`
* Tipo di autorizzazione: `Allow`

Puoi creare un gruppo di utenti o assegnare le autorizzazioni a un gruppo di utenti esistente. Le autorizzazioni possono essere assegnate dall&#39;interfaccia [!DNL Experience Manager Assets] o dalla console [!DNL User Admin].

**Per fornire l&#39;accesso a un gruppo di utenti da [!DNL Experience Manager]:**

1. Nell&#39;interfaccia utente di [!DNL Experience Manager], passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Gruppi]**. Crea un gruppo utenti per [!DNL Adobe Stock].

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Autorizzazioni]**.

1. Cerca il gruppo di utenti nel pannello a sinistra e aggiungi la nuova **[!UICONTROL voce di controllo di accesso]** per Adobe Stock.

   * Configura il percorso: `/conf/global/settings/stock`
   * Privilegi: `jcr:read`
   * Tipo di autorizzazione: `Allow`

   Fare clic su **[!UICONTROL Aggiungi]**.

   ![autorizzazioni-utente](assets/aem-stock-user-permissions.png)

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Adobe Stock]**. Selezionare la configurazione cloud [!DNL Adobe Stock] e fare clic su **[!UICONTROL Proprietà]**.

1. Aggiungere il gruppo utenti creato alla configurazione [!DNL Adobe Stock]. Fai clic su **[!UICONTROL Salva e chiudi]**.

   ![assegna-utente](assets/aem-stock-adduser.png)

**Per fornire l&#39;accesso a un utente da [!DNL User Admin Console]:**

1. Aprire l&#39;Admin Console utente [!DNL Experience Manager]. URL predefinito: `http://localhost:4502/userdamin`.

1. Nel pannello a sinistra, cerca l&#39;utente immettendo `user_id` o `name`. Fare doppio clic per aprire le proprietà utente.

1. Passare alla scheda **[!UICONTROL Autorizzazioni]** e consentire le autorizzazioni `read` per la configurazione cloud [!DNL Adobe Stock]: `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Se la configurazione cloud non è consentita, l&#39;utente può accedere solo a **[!UICONTROL Assets]** nell&#39;interfaccia [!DNL Experience Manager].
   >
   >Per consentire l&#39;accesso a [!UICONTROL risorse Assets] e [!DNL Adobe Stock], assicurati che la configurazione cloud sia consentita per l&#39;utente.

1. Fai clic su **[!UICONTROL Salva]** per aggiornare le autorizzazioni.

   ![assegna-utente-in-utente-amministratore](assets/aem-stock-user-admin-console.png)

1. Aggiungere l&#39;utente o il gruppo alla configurazione cloud [!DNL Adobe Stock].


## Accedere alle risorse di Adobe Stock {#access-stock-assets}

Un utente non amministratore con autorizzazioni per la configurazione cloud [!DNL Adobe Stock] può cercare e concedere in licenza le risorse [!DNL Adobe Stock] dall&#39;interfaccia [!DNL Experience Manager].

L&#39;utente deve eseguire un passaggio aggiuntivo per attivare la configurazione cloud [!DNL Adobe Stock] prima di accedere alle risorse [!DNL Adobe Stock]. Si tratta di un’attività una tantum. Se all&#39;utente vengono assegnate autorizzazioni su più configurazioni cloud [!DNL Adobe Stock], l&#39;utente può selezionare la configurazione desiderata tra le **[!UICONTROL Preferenze utente]**.

Per attivare la configurazione cloud [!DNL Adobe Stock]:

1. Accedi a [!DNL Experience Manager].

1. Fai clic sull&#39;icona utente in alto a destra, quindi fai clic su **[!UICONTROL Preferenze]**. Viene visualizzata la finestra **[!UICONTROL Preferenze utente]**.

1. Seleziona la **[!UICONTROL Configurazione Stock]** desiderata dall&#39;elenco a discesa e fai clic su **[!UICONTROL Accetta]** per attivare la configurazione.

   ![preferenze utente](assets/aem-stock-preferences.png)

1. Passa a **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**. È ora possibile visualizzare, cercare e concedere in licenza [!DNL Adobe Stock] risorse.

Nella tabella seguente viene illustrato il funzionamento delle autorizzazioni utente durante l&#39;accesso alle risorse [!DNL Adobe Stock]:

| User | Gruppo | Autorizzazioni | Accetta configurazione Stock nelle preferenze utente | Accedere ad Assets | Accedere ad Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| admin | N/D | Tutti | N/D | Sì | Sì |
| test-doc1 | Utente DAM | /conf/global/settings/stock/cloud-config | Sì | Sì | Sì |
| test-doc1 | Utente DAM | /conf/global/settings/stock/cloud-config | No | Errore: impossibile caricare i dati | No |
| test-doc1 | Utente DAM | **consenti**: /conf/global/settings/stock **nega**: /cloud-config | La configurazione Stock non è visibile | Sì | No |

## Usa e gestisci [!DNL Adobe Stock] risorse in [!DNL Experience Manager] {#usemanage}

Utilizzando questa funzionalità, le organizzazioni possono consentire ai propri utenti di lavorare utilizzando [!DNL Adobe Stock] risorse in [!DNL Experience Manager Assets]. Dall&#39;interfaccia utente di [!DNL Experience Manager], gli utenti possono cercare [!DNL Adobe Stock] risorse e concedere in licenza le risorse richieste.

Una volta ottenuta la licenza per una risorsa [!DNL Adobe Stock] in [!DNL Experience Manager], è possibile utilizzarla e gestirla come una risorsa tipica. In [!DNL Experience Manager], gli utenti possono cercare e visualizzare in anteprima le risorse; copiare e pubblicare le risorse; condividere le risorse in [!DNL Brand Portal]; accedere e utilizzare le risorse tramite l&#39;app desktop [!DNL Experience Manager] e così via.

![Cerca [!DNL Adobe Stock] risorse e filtra i risultati dall&#39;area di lavoro [!DNL Adobe Experience Manager]](assets/adobe-stock-search-results-workspace.png)

**A.** Cerca risorse simili a quelle di cui è stato fornito l&#39;ID [!DNL Adobe Stock]. **B.** Cerca risorse corrispondenti alla tua selezione di forma o orientamento. **C.** Cerca uno o più tipi di risorse supportati **D.** Apri o comprimi il riquadro dei filtri **E.** Concedi la licenza e salva la risorsa selezionata in [!DNL Experience Manager] **F.** Salva la risorsa in [!DNL Experience Manager] con filigrana **G.** Esplora le risorse nel sito Web [!DNL Adobe Stock] simili a quelle selezionate **H.** Visualizza le risorse selezionate nel sito Web [!DNL Adobe Stock] **I.** Numero di risorse selezionate dai risultati della ricerca **J.** Passaggio tra la vista a schede e la vista a elenco

### Trovare le risorse {#find-assets}

Gli utenti di [!DNL Experience Manager] possono cercare risorse in [!DNL Experience Manager] e [!DNL Adobe Stock]. Quando il percorso di ricerca non è limitato a [!DNL Adobe Stock], vengono visualizzati i risultati di ricerca di [!DNL Experience Manager] e [!DNL Adobe Stock].

* Per cercare [!DNL Adobe Stock] risorse, fai clic su **[!UICONTROL Navigazione]** > **[!UICONTROL Assets]** > **[!UICONTROL Cerca in Adobe Stock]**.

* Per cercare le risorse tra [!DNL Adobe Stock] e [!DNL Experience Manager Assets], fai clic su Cerca ![cerca](assets/do-not-localize/search_icon.png).

In alternativa, inizia a digitare `Location: Adobe Stock` nella barra di ricerca per selezionare [!DNL Adobe Stock] risorse. [!DNL Experience Manager] offre funzionalità di filtro avanzate sulle risorse trovate, consentendo agli utenti di inserire rapidamente le risorse richieste utilizzando filtri, ad esempio tipi di risorse supportate, orientamento dell&#39;immagine e stato della licenza.

>[!NOTE]
>
>Assets ricercati da [!DNL Adobe Stock] sono visualizzati in [!DNL Experience Manager]. [!DNL Adobe Stock] risorse vengono recuperate e archiviate nell&#39;archivio [!DNL Experience Manager] solo dopo che un utente [salva una risorsa](/help/assets/aem-assets-adobe-stock.md#saveassets) o [licenze e salva una risorsa](/help/assets/aem-assets-adobe-stock.md#licenseassets). Le Assets già archiviate in [!DNL Experience Manager] vengono visualizzate ed evidenziate per semplificare l&#39;accesso e la consultazione. Inoltre, le risorse [!DNL Stock] vengono salvate con alcuni metadati aggiuntivi per indicare l&#39;origine come [!DNL Stock].

![Filtri di ricerca in [!DNL Experience Manager] ed evidenziate [!DNL Adobe Stock] risorse nei risultati di ricerca](assets/aem-search-filters2.jpg)

### Salva e visualizza le risorse richieste {#saveassets}

Selezionare una risorsa da salvare in [!DNL Experience Manager]. Fai clic su [!UICONTROL Salva] nella barra degli strumenti nella parte superiore e specifica il nome e il percorso della risorsa. Le risorse senza licenza vengono salvate localmente con una filigrana.

La prossima volta che cerchi risorse, le risorse salvate vengono evidenziate con un contrassegno, per indicare che tali risorse sono disponibili in [!DNL Experience Manager Assets].

>[!NOTE]
>
>Le risorse aggiunte di recente presentano un badge Nuovo invece di Un badge Concesso in licenza.

### Ottieni licenza per risorse {#licenseassets}

Gli utenti possono concedere in licenza [!DNL Adobe Stock] risorse utilizzando la quota del proprio piano aziendale [!DNL Adobe Stock]. Quando si concede in licenza una risorsa, questa viene salvata senza filigrana ed è disponibile per la ricerca e l&#39;utilizzo in [!DNL Experience Manager Assets].

![Finestra di dialogo per concedere in licenza e salvare [!DNL Adobe Stock] risorse in [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Accedere ai metadati e alle proprietà delle risorse {#access-metadata-and-asset-properties}

Gli utenti possono accedere e visualizzare in anteprima i metadati, incluse le proprietà dei metadati [!DNL Adobe Stock] per le risorse salvate in [!DNL Experience Manager], e aggiungere **[!UICONTROL Riferimenti licenza]** per una risorsa. Tuttavia, gli aggiornamenti al riferimento della licenza non sono sincronizzati tra il sito Web [!DNL Experience Manager] e [!DNL Adobe Stock].

Gli utenti possono visualizzare le proprietà sia per le risorse con licenza che per quelle senza licenza.

![Visualizzare e accedere ai metadati e ai riferimenti di licenza delle risorse salvate](assets/metadata_properties.jpg)


## Limitazioni note {#known-limitations}

* **La funzionalità per impedire agli utenti di concedere licenze non funziona correttamente**: tutti gli utenti con autorizzazioni `read` per la configurazione Stock possono cercare e concedere licenze alle risorse [!DNL Adobe Stock].

* **Gli utenti non amministratori devono attivare manualmente la configurazione cloud [!DNL Adobe Stock]**: nella finestra **[!UICONTROL Preferenze utente]**, la **[!UICONTROL Configurazione Stock]** mostra la configurazione cloud [!DNL Adobe Stock] come abilitata, ma non funziona per un utente non amministratore. L&#39;utente deve fare clic sul pulsante **[!UICONTROL Accetta]** per attivare la configurazione Stock. In assenza di questo passaggio, verrà visualizzato un messaggio di errore durante l&#39;accesso a **[!UICONTROL Assets]**.

* **Avviso immagine editoriale non visualizzato**: quando si concede la licenza a un&#39;immagine, gli utenti non possono verificare se un&#39;immagine è Solo per uso editoriale. Per evitare possibili abusi, gli amministratori possono disattivare l’accesso alle risorse editoriali da Admin Console.

* **È stato visualizzato un tipo di licenza errato**: è possibile che in [!DNL Experience Manager] venga visualizzato un tipo di licenza errato per una risorsa. Gli utenti possono accedere al sito Web [!DNL Adobe Stock] per visualizzare il tipo di licenza.

* **I campi di riferimento e i metadati non sono sincronizzati**: quando un utente aggiorna un campo di riferimento licenza, le informazioni di riferimento licenza vengono aggiornate in [!DNL Experience Manager] ma non nel sito Web [!DNL Adobe Stock]. Analogamente, se l&#39;utente aggiorna i campi di riferimento nel sito Web [!DNL Adobe Stock], gli aggiornamenti non vengono sincronizzati in [!DNL Experience Manager].

<!--
## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations users can work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.
-->

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

<!--
### Find assets {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* To search for assets across [!DNL Adobe Stock] and [!DNL Experience Manager Assets], click search ![search](assets/do-not-localize/search_icon.png).

Alternatively, start typing `Location: Adobe Stock` in the search bar to select [!DNL Adobe Stock] assets. [!DNL Experience Manager] offers advanced filtering capabilities on the searched assets, allowing users to quickly zero-in on the required assets using filters, such as types of supported assets, image orientation, and licensed state.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] assets are fetched and stored in [!DNL Experience Manager] repository only after a user either [saves an asset](/help/assets/aem-assets-adobe-stock.md#saveassets) or [licenses and saves an asset](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Search filters in Experience Manager and highlighted Adobe Stock assets in search results](assets/aem-search-filters2.jpg)

*Figure: Search filters in [!DNL Experience Manager] and highlighted [!DNL Adobe Stock] assets in search results.*

### Save and view the required assets {#saveassets}

Select an asset that you want to save in [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. The unlicensed assets are saved locally with a watermark.

Next time when you search for assets, the saved assets are highlighted with a badge, to indicate that such assets are available in [!DNL Experience Manager Assets].

>[!NOTE]
>
>The recently added assets display a New badge instead of Licensed badge.

### License assets {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. When you license an asset, it is saved without a watermark and is available for searching and using in [!DNL Experience Manager Assets].

![Dialog to license and save Adobe Stock assets in Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figure: Dialog to license and save [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets].*

### Access metadata and asset properties {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

Users can see the properties for both, licensed and unlicensed assets.

![View and access metadata and license references of saved assets](assets/metadata_properties.jpg)

*Figure: View and access metadata and license references of saved assets.*

## Known limitations {#known-limitations}

* **Editorial image warning is not displayed**: When licensing an image, users cannot check if an image is Editorial Use Only. To prevent possible misuse, the administrators can turn off the access to editorial assets from the Admin Console.

* **Wrong license type is displayed**: It is possible that an incorrect license type is displayed in [!DNL Experience Manager] for an asset. Users can log into the [!DNL Adobe Stock] website to see the license type.

* **Reference fields and metadata are not synced**: When a user updates a license reference field, the license reference information is updated in [!DNL Experience Manager] but not on the [!DNL Adobe Stock] website. Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].
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

>[!MORELIKETHIS]
>
>* [Esercitazione video sull&#39;utilizzo di risorse Adobe Stock con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html?lang=it)
>* [Guida al piano aziendale di Adobe Stock](https://helpx.adobe.com/it/enterprise/using/adobe-stock-enterprise.html)
>* [Domande frequenti su Adobe Stock](https://helpx.adobe.com/it/stock/faq.html)
