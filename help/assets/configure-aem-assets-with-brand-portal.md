---
title: Configurare  AEM Assets come  [!DNL Cloud Service] con Brand Portal
description: Configurare AEM Assets con Brand Portal.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: db653daa2d3c271329812b35960f50ee22fb9943
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 20%

---


# Configurare  AEM Assets come [!DNL Cloud Service] con Portale marchio {#configure-aem-assets-with-brand-portal}

La configurazione di Adobe Experience Manager Assets Brand Portal consente di pubblicare risorse del marchio approvate da Adobe Experience Manager Assets come istanza [!DNL Cloud Service] in Brand Portal e distribuirle agli utenti del Brand Portal.

**Flusso di lavoro di configurazione**

 AEM Assets come [!DNL Cloud Service] è configurato con Portale marchio tramite  Developer Console, che fornisce un token account  Adobe Identity Management Services (IMS) per l&#39;autorizzazione del tenant del Portale marchio. Richiede configurazioni sia in  AEM Assets che  Adobe Developer Console.

1. In  AEM Assets, create un account IMS e generate una chiave pubblica (certificato).
1. In  Adobe Developer Console, crea un progetto per il tenant del Brand Portal (organizzazione).
1. In questo progetto, configura un&#39;API utilizzando la chiave pubblica per creare una connessione a un account di servizio.
1. Ottenete le credenziali dell&#39;account del servizio e le informazioni sul payload JSON Web Token (JWT).
1. In  AEM Assets, configurate l&#39;account IMS utilizzando le credenziali dell&#39;account del servizio e il payload JWT.
1. In  AEM Assets, configurate il servizio cloud Brand Portal utilizzando l&#39;account IMS e l&#39;endpoint del Brand Portal (URL organizzazione).
1. Verificate la configurazione pubblicando una risorsa da  AEM Assets al Brand Portal.

>[!NOTE]
>
>Un AEM Assets  come istanza [!DNL Cloud Service] può essere configurato solo con un tenant Brand Portal.

## Prerequisiti {#prerequisites}

Per configurare AEM Assets con Brand Portal, è necessario quanto segue:

* Un AEM Assets funzionante  come istanza [!DNL Cloud Service]
* URL tenant del Brand Portal
* Un utente con privilegi di amministratore di sistema nell’organizzazione IMS del tenant di Brand Portal

## Creare la configurazione {#create-new-configuration}

Effettuate i seguenti passaggi nella sequenza specificata per configurare  AEM Assets con Brand Portal.

1. [Recuperare il certificato pubblico](#public-certificate)
1. [Creare una connessione account di servizio (JWT)](#createnewintegration)
1. [Configurare l&#39;account IMS](#create-ims-account-configuration)
1. [Configurare il servizio cloud](#configure-the-cloud-service)
1. [Verificare la configurazione](#test-configuration)

### Creare la configurazione IMS {#create-ims-configuration}

La configurazione IMS autentica l&#39;AEM Assets  come istanza [!DNL Cloud Service] con il tenant del Brand Portal.

La configurazione IMS prevede due passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Configurare l&#39;account IMS](#create-ims-account-configuration)

### Recuperare il certificato pubblico {#public-certificate}

La chiave pubblica (certificato) autentica il tuo profilo in  Adobe Developer Console.

1. Effettuate l&#39;accesso a  AEM Assets.
1. Dal pannello **Strumenti**, andate a **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni IMS  Adobe]**.
1. Nella pagina Configurazioni IMS  Adobe, fare clic su **[!UICONTROL Crea]**. Verrà reindirizzato alla pagina **[!UICONTROL Adobe IMS Technical Account Configuration]**. Per impostazione predefinita, viene visualizzata la scheda **Certificate**.
1. Selezionare **[!UICONTROL Portale marchio Adobe]** nell&#39;elenco a discesa **[!UICONTROL Cloud Solution]**.
1. Selezionare la casella di controllo **[!UICONTROL Crea nuovo certificato]** e specificare un **alias** per la chiave pubblica. L&#39;alias funge da nome della chiave pubblica.
1. Fai clic su **[!UICONTROL Crea certificato]**. Quindi, fare clic su **[!UICONTROL OK]** per generare la chiave pubblica.

   ![Crea certificato](assets/ims-config2.png)

1. Fare clic sull&#39;icona **[!UICONTROL Scarica chiave pubblica]** e salvare il file di chiave pubblica (CRT) sul computer.

   La chiave pubblica verrà utilizzata in seguito per configurare l&#39;API per il tenant del Brand Portal e generare le credenziali dell&#39;account di servizio in  Adobe Developer Console.

   ![Scarica certificato](assets/ims-config3.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   Nella scheda **Account** viene creato  account IMS del Adobe che richiede le credenziali dell&#39;account del servizio generate in  Adobe Developer Console. Per il momento tieni aperta questa pagina.

   Aprite una nuova scheda e [create una connessione account di servizio (JWT) in  Adobe Developer Console](#createnewintegration) per ottenere le credenziali e il payload JWT per configurare l&#39;account IMS.

### Creare una connessione account di servizio (JWT) {#createnewintegration}

In  Adobe Developer Console, i progetti e le API sono configurati a livello di tenant del Brand Portal (organizzazione). La configurazione di un&#39;API crea una connessione JWT (Service Account). Esistono due metodi per configurare l&#39;API, generando una coppia di chiavi (chiavi private e pubbliche) o caricando una chiave pubblica. Per configurare  AEM Assets con Brand Portal, dovete generare una chiave pubblica (certificato) in  AEM Assets e creare le credenziali in  console Sviluppatore Adobe caricando la chiave pubblica. Queste credenziali sono necessarie per configurare l&#39;account IMS in  AEM Assets. Una volta configurato l&#39;account IMS, potete configurare il servizio cloud Brand Portal in  AEM Assets.

Effettuate le seguenti operazioni per generare le credenziali dell&#39;account del servizio e il payload JWT:

1. Accedete a  console per sviluppatori di Adobe con privilegi di amministratore di sistema nell’organizzazione IMS (tenant Brand Portal). L&#39;URL predefinito è [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Accertatevi di aver selezionato l&#39;organizzazione IMS corretta (tenant Brand Portal) dall&#39;elenco a discesa (organizzazione) nell&#39;angolo superiore destro.

1. Fare clic su **[!UICONTROL Crea nuovo progetto]**. Per la vostra organizzazione viene creato un progetto vuoto con un nome generato dal sistema.

   Fare clic su **[!UICONTROL Modifica progetto]** per aggiornare il **[!UICONTROL Titolo progetto]** e **[!UICONTROL Descrizione]**, quindi fare clic su **[!UICONTROL Salva]**.

1. Nella scheda **[!UICONTROL Panoramica progetto]**, fare clic su **[!UICONTROL Aggiungi API]**.

1. Nella **[!UICONTROL Aggiungi una finestra API]**, selezionare **[!UICONTROL AEM Brand Portal]** e fare clic su **[!UICONTROL Next]**.

   Assicuratevi di avere accesso al servizio AEM Brand Portal.

1. Nella finestra **[!UICONTROL Configura API]**, fare clic su **[!UICONTROL Carica la chiave pubblica]**. Quindi, fare clic su **[!UICONTROL Selezionare un file]** e caricare la chiave pubblica (.crt file) scaricata nella sezione [ottenere il certificato pubblico](#public-certificate).

   Fai clic su **[!UICONTROL Avanti]**.

   ![Carica chiave pubblica](assets/service-account3.png)

1. Verificare la chiave pubblica e fare clic su **[!UICONTROL Next]**.

1. Selezionate **[!UICONTROL Assets Brand Portal]** come profilo di prodotto predefinito, quindi fate clic su **[!UICONTROL Salva API configurata]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Seleziona profilo di prodotto](assets/service-account4.png)

1. Una volta configurata l&#39;API, verrete reindirizzati alla pagina di panoramica dell&#39;API. Dalla navigazione a sinistra in **[!UICONTROL Credenziali]**, fare clic sull&#39;opzione **[!UICONTROL Account di servizio (JWT)]**.

   >[!NOTE]
   >
   >Potete visualizzare le credenziali ed eseguire azioni quali generare token JWT, copiare i dettagli delle credenziali, recuperare il segreto client e così via.

1. Dalla scheda **[!UICONTROL Credenziali client]**, copiare l&#39; **[!UICONTROL ID client]**.

   Fare clic su **[!UICONTROL Recupera Segreto cliente]** e copiare il **[!UICONTROL segreto client]**.

   ![Credenziali account di servizio](assets/service-account5.png)

1. Passare alla scheda **[!UICONTROL Genera JWT]** e copiare le informazioni relative al payload **[!UICONTROL JWT]**.

Ora puoi utilizzare l&#39;ID client (chiave API), il segreto client e il payload JWT per [configurare l&#39;account IMS](#create-ims-account-configuration) in  AEM Assets.

<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
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

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.

-->

### Configurare l&#39;account IMS {#create-ims-account-configuration}

Verifica di aver eseguito i seguenti passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Creare una connessione account di servizio (JWT)](#createnewintegration)

Effettuate le seguenti operazioni per configurare l&#39;account IMS.

1. Aprite IMS Configuration e passate alla scheda **[!UICONTROL Account]**. La pagina è rimasta aperta durante il [recupero del certificato pubblico](#public-certificate).

1. Specifica un **[!UICONTROL titolo]** per l’account IMS.

   Nel campo **[!UICONTROL Server di autorizzazione]**, specificate l&#39;URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Specificate l&#39;ID client nel campo **[!UICONTROL Chiave API]**, **[!UICONTROL Segreto client]** e **[!UICONTROL Payload]** (payload JWT) che avete copiato durante la creazione della connessione dell&#39;account del servizio (JWT)](#createnewintegration).[

   Fai clic su **[!UICONTROL Crea]**.

   L&#39;account IMS è configurato.

   ![Configurazione dell’account IMS](assets/create-new-integration6.png)


1. Selezionate la configurazione dell&#39;account IMS e fate clic su **[!UICONTROL Verifica stato]**.

   Fare clic su **[!UICONTROL Check]** nella finestra di dialogo. In caso di configurazione corretta, viene visualizzato un messaggio che informa che il *Token viene recuperato correttamente*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Puoi disporre di una sola configurazione IMS.
>
>Verifica che la configurazione IMS superi il controllo di integrità. Se la configurazione non supera questa verifica, non è valida. Dovrai quindi eliminarla e creare una nuova configurazione valida.

### Configurare il servizio cloud {#configure-the-cloud-service}

Per configurare il servizio cloud Brand Portal, effettuate le seguenti operazioni:

1. Effettuate l&#39;accesso a  AEM Assets.

1. Dal pannello **Strumenti**, andate a **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Nella pagina Configurazioni Brand Portal, fate clic su **[!UICONTROL Crea]**.

1. Specifica un **[!UICONTROL titolo]** per la configurazione.

   Selezionare la configurazione IMS creata durante la [configurazione dell&#39;account IMS](#create-ims-account-configuration).

   Nel campo **[!UICONTROL URL servizio]**, specificate l&#39;URL tenant (organizzazione) del Portale marchio.

   ![](assets/create-cloud-service.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**. Viene creata la configurazione cloud.

   L&#39;AEM Assets  come istanza [!DNL Cloud Service] ora è configurato con il tenant del Brand Portal.

### Verificare la configurazione {#test-configuration}

Effettuate le seguenti operazioni per convalidare la configurazione:

1. Effettuate l&#39;accesso a  AEM Assets.

1. Dal pannello **Strumenti**, passare a **[!UICONTROL Distribuzione]** > **[!UICONTROL Distribuzione]**.

   ![](assets/test-bpconfig1.png)

   Un agente di distribuzione Brand Portal (**[!UICONTROL bpdistributionagent0]**) viene creato in **[!UICONTROL Pubblica su Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Fate clic su **[!UICONTROL Pubblica su Brand Portal]** per aprire l&#39;agente di distribuzione.

   Potete visualizzare le code di distribuzione nella scheda **[!UICONTROL Stato]**.

   Un agente di distribuzione contiene due code:
   * **Coda di elaborazione**: per la distribuzione delle risorse in Brand Portal.

   * **Coda di errore**: per le risorse per le quali la distribuzione non è riuscita.
   >[!NOTE]
   >
   >È consigliabile esaminare gli errori e cancellare periodicamente la **coda di errore**.

   ![](assets/test-bpconfig3.png)

1. Per verificare la connessione tra  AEM Assets come [!DNL Cloud Service] e Brand Portal, fare clic sull&#39;icona **[!UICONTROL Test Connection]**.

   ![](assets/test-bpconfig4.png)

   Viene visualizzato un messaggio che informa che il pacchetto di test *è stato consegnato correttamente*.

   >[!NOTE]
   >
   >Evita di disabilitare l’agente di distribuzione, in quanto potrebbe impedire la corretta distribuzione delle risorse (in esecuzione nella coda).

Ora puoi:

* [Pubblicare risorse da AEM Assets su Brand Portal](publish-to-brand-portal.md)
* [Pubblicare cartelle da AEM Assets su Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Pubblicare raccolte da AEM Assets su Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Pubblicare predefiniti, schemi e facet in Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Pubblicare tag in Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Per ulteriori informazioni, consultate la [documentazione del Portale del marchio](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/home.html).

## Registri di distribuzione {#distribution-logs}

Potete monitorare i registri degli agenti di distribuzione per il flusso di lavoro di pubblicazione delle risorse.

Ad esempio, è stata pubblicata una risorsa da  AEM Assets al Portale del marchio per convalidare la configurazione.

1. Seguire i passaggi (da 1 a 4) come mostrato nella sezione [Configurazione di prova](#test-configuration) e passare alla pagina agente di distribuzione.
1. Fare clic su **[!UICONTROL Registri]** per visualizzare i registri di elaborazione e di errore.

   ![](assets/test-bpconfig5.png)

L&#39;agente di distribuzione ha generato i seguenti registri:

* INFORMAZIONI: Si tratta di un registro generato dal sistema che attiva la configurazione corretta dell&#39;agente di distribuzione.
* DSTRQ1 (richiesta 1): si attiva durante la prova della connessione.

Quando viene pubblicata la risorsa, vengono generati i seguenti registri di richieste e risposte:

**Richiesta dell’agente di distribuzione**:

* DSTRQ2 (richiesta 2): viene attivata la richiesta di pubblicazione della risorsa.
* DSTRQ3 (richiesta 3): Il sistema attiva un’altra richiesta per pubblicare la  cartella AEM Assets (in cui esiste la risorsa) e replicare la cartella in Brand Portal.

**Risposta dell’agente di distribuzione**:

* queue-bpdistributionagent0 (DSTRQ2): la risorsa viene pubblicata su Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): Il sistema replica la cartella AEM Assets  (contenente la risorsa) in Brand Portal.

Nell’esempio precedente, viene attivata un’ulteriore combinazione di richiesta e risposta. Impossibile trovare la cartella principale (Aggiungi percorso) nel Portale marchio perché la risorsa è stata pubblicata per la prima volta. Pertanto, è stata attivata un&#39;ulteriore richiesta per creare una cartella principale con lo stesso nome in Portale marchio in cui la risorsa viene pubblicata.

>[!NOTE]
>
>La richiesta aggiuntiva viene generata nel caso in cui la cartella principale non esista nel Brand Portal o sia stata modificata in  AEM Assets.

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
