---
title: Configurare AEM Assets come a [!DNL Cloud Service] con Brand Portal
description: Configurare AEM Assets con Brand Portal.
contentOwner: Vishabh Gupta
feature: Brand Portal,Distribuzione delle risorse,Configurazione
role: Administrator
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
translation-type: tm+mt
source-git-commit: d3c19e460f72a980e058ef6117f6352bda4d1e8a
workflow-type: tm+mt
source-wordcount: '2416'
ht-degree: 13%

---

# Configurare AEM Assets come [!DNL Cloud Service] con Brand Portal {#configure-aem-assets-with-brand-portal}

La configurazione di Adobe Experience Manager Assets Brand Portal consente di pubblicare risorse del marchio approvate da Adobe Experience Manager Assets come istanza [!DNL Cloud Service] in Brand Portal e di distribuirle agli utenti di Brand Portal.

## Attivare Brand Portal utilizzando Cloud Manager {#activate-brand-portal}

L’utente di Cloud Manager attiva Brand Portal per un’istanza di AEM Assets as a0/> . [!DNL Cloud Service] Il flusso di lavoro di attivazione crea le configurazioni richieste (token di autorizzazione, configurazione IMS e servizio cloud di Brand Portal) nel back-end e riflette lo stato del tenant di Brand Portal in Cloud Manager. L’attivazione di Brand Portal consente agli utenti di AEM Assets di pubblicare risorse su Brand Portal e di distribuirle agli utenti di Brand Portal.

**Prerequisiti**

Per attivare Brand Portal sul tuo AEM Assets come istanza [!DNL Cloud Service] è necessario quanto segue:

* Un’istanza di AEM Assets in esecuzione come [!DNL Cloud Service].
* Un utente con accesso a Cloud Manager, assegnato a Profili del prodotto Cloud Manager. Per ulteriori informazioni, consulta [accesso a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#accessing-cloud-manager) .

>[!NOTE]
>
>Un’istanza di AEM Assets as a [!DNL Cloud Service] può connettersi con un solo tenant di Brand Portal. Puoi disporre di più ambienti (sviluppo, produzione e stage) per l’istanza AEM Assets as a [!DNL Cloud Service], in cui Brand Portal viene attivato in un unico ambiente.

**Passaggi per attivare Brand Portal**

Puoi attivare Brand Portal durante la creazione degli ambienti per l’istanza AEM Assets come [!DNL Cloud Service] o separatamente. Supponiamo che gli ambienti siano già stati creati e che ora sia necessario attivare Brand Portal.

1. Accedi ad Adobe Cloud Manager e passa a **[!UICONTROL Ambienti]**.

   La pagina **[!UICONTROL Ambienti]** visualizza l&#39;elenco di tutti gli ambienti esistenti.

1. Seleziona gli ambienti (uno per uno) dall’elenco per visualizzare i dettagli dell’ambiente.

   Brand Portal ha diritto a uno degli ambienti disponibili e si riflette in **[!UICONTROL Informazioni sull’ambiente]**.

   Una volta trovato l’ambiente associato a Brand Portal, fai clic sul pulsante **[!UICONTROL Attiva Brand Portal]** per avviare il flusso di lavoro di attivazione.

   ![Attivare Brand Portal](assets/create-environment4.png)

1. L’attivazione del tenant di Brand Portal richiede pochi minuti, in quanto il flusso di lavoro di attivazione crea le configurazioni richieste nel back-end. Una volta attivato il tenant di Brand Portal, lo stato diventa Attivato.

   ![Visualizza stato](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal deve essere attivato sulla stessa organizzazione IMS di AEM Assets come istanza [!DNL Cloud Service].
>
>Se disponi di una configurazione cloud ([configurata manualmente tramite Adobe Developer Console](#manual-configuration)) per un’organizzazione IMS (org1-existing) e l’istanza AEM Assets as a [!DNL Cloud Service] è configurata per un’altra organizzazione IMS (org2-new), l’attivazione di Brand Portal da Cloud Manager ripristina l’organizzazione Brand IMS su `org2-new`. Anche se la configurazione cloud configurata manualmente su `org1-existing` sarà visibile nell’istanza di authoring di AEM Assets, ma non sarà più in uso dopo l’attivazione di Brand Portal da Cloud Manager.
>
>Se la configurazione cloud esistente di Brand Portal e AEM Assets as a [!DNL Cloud Service] utilizzano la stessa organizzazione IMS (org1), è sufficiente attivare Brand Portal da Cloud Manager.

**Consulta anche**:
* [Aggiungere utenti e ruoli in AEM Assets as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html?lang=en#role-definitions)

* [Gestione degli ambienti in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments)


**Accedi al tenant** di Brand Portal:

Dopo l’attivazione del tenant di Brand Portal in Cloud Manager, puoi accedere a Brand Portal da Admin Console o direttamente dall’URL del tenant.

L’URL predefinito del tenant di Brand Portal è: `https://<tenant-id>.brand-portal.adobe.com/`.

In questo caso, l’ID tenant è l’organizzazione IMS.

Se non sei sicuro dell’URL di Brand Portal, effettua le seguenti operazioni:

1. Accedi a [Admin Console](http://adminconsole.adobe.com/) e passa a **[!UICONTROL Prodotti]**.
1. Dalla barra a sinistra, seleziona **[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**.
1. Fai clic su **[!UICONTROL Vai a Brand Portal]** per aprire direttamente Brand Portal nel browser.

   Oppure copia l’URL del tenant di Brand Portal dal collegamento **[!UICONTROL Vai a Brand Portal]** e incollalo nel browser per aprire l’interfaccia di Brand Portal.

   ![Accedere a Brand Portal](assets/access-bp-on-cloud.png)


**Prova connessione**

Esegui i seguenti passaggi per convalidare la connessione tra l’istanza AEM Assets as a [!DNL Cloud Service] e il tenant di Brand Portal:

1. Accedi ad AEM Assets.

1. Dal pannello **Strumenti**, passa a **[!UICONTROL Implementazione]** > **[!UICONTROL Distribuzione]**.

   ![](assets/test-bpconfig1.png)

   Un agente di distribuzione di Brand Portal (**[!UICONTROL bpdistributionagent0]**) viene creato in **[!UICONTROL Pubblica su Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Fai clic su **[!UICONTROL Pubblica su Brand Portal]** per aprire l’agente di distribuzione.

   Puoi visualizzare le code di distribuzione nella scheda **[!UICONTROL Stato]** .

   Un agente di distribuzione contiene due code:
   * **Coda di elaborazione**: per la distribuzione delle risorse in Brand Portal.

   * **Coda di errore**: per le risorse per le quali la distribuzione non è riuscita.
   >[!NOTE]
   >
   >È consigliabile esaminare gli errori e cancellare periodicamente la **coda di errore**.

   ![](assets/test-bpconfig3.png)

1. Per verificare la connessione tra AEM Assets as a [!DNL Cloud Service] e Brand Portal, fai clic sull’ icona **[!UICONTROL Test connessione]** .

   ![](assets/test-bpconfig4.png)

   Viene visualizzato un messaggio che informa che il pacchetto di test *è stato consegnato correttamente*.

   >[!NOTE]
   >
   >Evita di disabilitare l’agente di distribuzione, in quanto potrebbe impedire la corretta distribuzione delle risorse (in esecuzione nella coda).

Per verificare la connessione tra l’istanza AEM Assets as a [!DNL Cloud Service] e il tenant di Brand Portal, pubblica una risorsa da AEM Assets a Brand Portal. Se la connessione ha esito positivo, la risorsa pubblicata è visibile nell’interfaccia di Brand Portal.


Ora puoi:

* [Pubblicare risorse da AEM Assets su Brand Portal](publish-to-brand-portal.md)
* [Pubblicare cartelle da AEM Assets su Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Pubblicare raccolte da AEM Assets su Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Pubblicare risorse da Brand Portal in AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=en)  - Asset Sourcing in Brand Portal
* [Pubblicare predefiniti, schemi e facet in Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Pubblicare tag in Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Per ulteriori informazioni, consulta la [documentazione di Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/home.html) .

**Registri di distribuzione**

Puoi monitorare i registri degli agenti di distribuzione per il flusso di lavoro di pubblicazione delle risorse.

Ora pubblichiamo una risorsa da AEM Assets su Brand Portal e vediamo i registri.

1. Segui i passaggi da 1 a 4 descritti nella sezione **Prova connessione** e passa alla pagina dell’agente di distribuzione.
1. Fai clic su **[!UICONTROL Registri]** per visualizzare i registri di elaborazione ed errore.

   ![](assets/test-bpconfig5.png)

L’agente di distribuzione ha generato i seguenti registri:

* INFORMAZIONI: Si tratta di un registro generato dal sistema che viene attivato in caso di configurazione corretta dell’agente di distribuzione.
* DSTRQ1 (richiesta 1): si attiva durante la prova della connessione.

Quando viene pubblicata la risorsa, vengono generati i seguenti registri di richieste e risposte:

**Richiesta dell’agente di distribuzione**:

* DSTRQ2 (richiesta 2): viene attivata la richiesta di pubblicazione della risorsa.
* DSTRQ3 (richiesta 3): Il sistema attiva un’altra richiesta per pubblicare la cartella AEM Assets (in cui si trova la risorsa) e replica la cartella in Brand Portal.

**Risposta dell’agente di distribuzione**:

* queue-bpdistributionagent0 (DSTRQ2): la risorsa viene pubblicata su Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): Il sistema replica la cartella AEM Assets (contenente la risorsa) in Brand Portal.

Nell’esempio precedente, viene attivata un’ulteriore combinazione di richiesta e risposta. Impossibile trovare la cartella principale (Aggiungi percorso) in Brand Portal perché la risorsa è stata pubblicata per la prima volta. Pertanto, è stata attivata un’ulteriore richiesta per creare una cartella principale con lo stesso nome in Brand Portal in cui viene pubblicata la risorsa.

>[!NOTE]
>
>Viene generata un’ulteriore richiesta nel caso in cui la cartella principale non esista in Brand Portal o sia stata modificata in AEM Assets.

Oltre al flusso di lavoro di automazione per attivare Brand Portal su AEM Assets as a [!DNL Cloud Service], esiste un altro metodo per configurare manualmente AEM Assets as a [!DNL Cloud Service] con Brand Portal utilizzando Adobe Developer Console, che non è più consigliato.

>[!NOTE]
>
>Se riscontri problemi durante l’attivazione del tenant di Brand Portal, contatta il supporto Adobe.

## Configurazione manuale tramite Adobe Developer Console {#manual-configuration}

La sezione seguente descrive come configurare manualmente AEM Assets as a [!DNL Cloud Service] con Brand Portal utilizzando Adobe Developer Console.

In precedenza, AEM Assets as a [!DNL Cloud Service] era configurato manualmente con Brand Portal tramite Adobe Developer Console, che fornisce un token account Adobe Identity Management Services (IMS) per l’autorizzazione del tenant di Brand Portal. Richiede configurazioni sia in AEM Assets che in Adobe Developer Console.

1. In AEM Assets, crea un account IMS e genera una chiave pubblica (certificato).
1. In Adobe Developer Console, crea un progetto per il tenant di Brand Portal (organizzazione).
1. Nel progetto , configura un’API utilizzando la chiave pubblica per creare una connessione dell’account del servizio.
1. Ottieni le credenziali dell&#39;account del servizio e le informazioni sul payload JSON Web Token (JWT).
1. In AEM Assets, configura l’account IMS utilizzando le credenziali dell’account del servizio e il payload JWT.
1. In AEM Assets, configura il servizio cloud Brand Portal utilizzando l’account IMS e l’endpoint Brand Portal (URL dell’organizzazione).
1. Verifica la configurazione pubblicando una risorsa da AEM Assets a Brand Portal.

>[!NOTE]
>
>Un’istanza di AEM Assets as a [!DNL Cloud Service] può essere configurata con un solo tenant di Brand Portal.

**Prerequisiti**

Per configurare AEM Assets con Brand Portal, è necessario quanto segue:

* Un’istanza di AEM Assets in esecuzione come [!DNL Cloud Service]
* URL tenant di Brand Portal
* Un utente con privilegi di amministratore di sistema nell’organizzazione IMS del tenant di Brand Portal

## Creare la configurazione {#create-new-configuration}

Esegui i seguenti passaggi nella sequenza specificata per configurare AEM Assets con Brand Portal.

1. [Recuperare il certificato pubblico](#public-certificate)
1. [Crea connessione account di servizio (JWT)](#createnewintegration)
1. [Configurare l’account IMS](#create-ims-account-configuration)
1. [Configurare il servizio cloud](#configure-the-cloud-service)

### Creare la configurazione IMS {#create-ims-configuration}

La configurazione IMS autentica il tuo AEM Assets come istanza [!DNL Cloud Service] con il tenant di Brand Portal.

La configurazione IMS prevede due passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Configurare l’account IMS](#create-ims-account-configuration)

### Recuperare il certificato pubblico {#public-certificate}

La chiave pubblica (certificato) autentica il tuo profilo in Adobe Developer Console.

1. Accedi ad AEM Assets.
1. Dal pannello **Strumenti**, passa a **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni IMS di Adobe]**.
1. Nella pagina Configurazioni IMS di Adobe, fai clic su **[!UICONTROL Crea]**. Reindirizzerà alla pagina **[!UICONTROL Adobe IMS Technical Account Configuration]** . Per impostazione predefinita, viene visualizzata la scheda **Certificato** .
1. Seleziona **[!UICONTROL Adobe Brand Portal]** nell’elenco a discesa **[!UICONTROL Soluzione cloud]** .
1. Seleziona la casella di controllo **[!UICONTROL Crea nuovo certificato]** e specifica un **alias** per la chiave pubblica. L&#39;alias funge da nome della chiave pubblica.
1. Fai clic su **[!UICONTROL Crea certificato]**. Quindi, fai clic su **[!UICONTROL OK]** per generare la chiave pubblica.

   ![Crea certificato](assets/ims-config2.png)

1. Fai clic sull&#39;icona **[!UICONTROL Scarica chiave pubblica]** e salva il file della chiave pubblica (CRT) sul computer.

   La chiave pubblica viene utilizzata in seguito per configurare l’API per il tenant di Brand Portal e generare le credenziali dell’account del servizio in Adobe Developer Console.

   ![Scarica certificato](assets/ims-config3.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   Nella scheda **Account** viene creato l’account Adobe IMS che richiede le credenziali dell’account del servizio generate in Adobe Developer Console. Per il momento tieni aperta questa pagina.

   Apri una nuova scheda e [crea una connessione a un account di servizio (JWT) in Adobe Developer Console](#createnewintegration) per ottenere le credenziali e il payload JWT per la configurazione dell’account IMS.

### Crea connessione account di servizio (JWT) {#createnewintegration}

In Adobe Developer Console, progetti e API sono configurati a livello di tenant di Brand Portal (organizzazione). La configurazione di un’API crea una connessione a un account di servizio (JWT). Esistono due metodi per configurare l’API, generando una coppia di chiavi (chiavi private e pubbliche) o caricando una chiave pubblica. Per configurare AEM Assets con Brand Portal, devi generare una chiave pubblica (certificato) in AEM Assets e creare credenziali in Adobe Developer Console caricando la chiave pubblica. Queste credenziali sono necessarie per configurare l’account IMS in AEM Assets. Una volta configurato l’account IMS, puoi configurare il servizio cloud Brand Portal in AEM Assets.

Esegui i seguenti passaggi per generare le credenziali dell’account del servizio e il payload JWT:

1. Accedi ad Adobe Developer Console con privilegi di amministratore di sistema nell’organizzazione IMS (tenant di Brand Portal). L&#39;URL predefinito è [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Accertati di aver selezionato l’organizzazione IMS corretta (tenant di Brand Portal) dall’elenco a discesa (organizzazione) che si trova nell’angolo in alto a destra.

1. Fai clic su **[!UICONTROL Crea nuovo progetto]**. Per la tua organizzazione viene creato un progetto vuoto con un nome generato dal sistema.

   Fai clic su **[!UICONTROL Modifica progetto]** per aggiornare il **[!UICONTROL Titolo progetto]** e **[!UICONTROL Descrizione]**, quindi fai clic su **[!UICONTROL Salva]**.

1. Nella scheda **[!UICONTROL Panoramica progetto]** , fai clic su **[!UICONTROL Aggiungi API]**.

1. In **[!UICONTROL Aggiungi una finestra API]**, seleziona **[!UICONTROL AEM Brand Portal]** e fai clic su **[!UICONTROL Avanti]**.

   Assicurati di avere accesso al servizio AEM Brand Portal.

1. Nella finestra **[!UICONTROL Configura API]**, fai clic su **[!UICONTROL Carica la chiave pubblica]**. Quindi, fai clic su **[!UICONTROL Seleziona un file]** e carica la chiave pubblica (.crt file) che hai scaricato nella sezione [Ottieni certificato pubblico](#public-certificate) .

   Fai clic su **[!UICONTROL Avanti]**.

   ![Carica chiave pubblica](assets/service-account3.png)

1. Verifica la chiave pubblica e fai clic su **[!UICONTROL Avanti]**.

1. Seleziona **[!UICONTROL Assets Brand Portal]** come profilo di prodotto predefinito e fai clic su **[!UICONTROL Salva API configurata]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Seleziona profilo prodotto](assets/service-account4.png)

1. Una volta configurata l’API, vieni reindirizzato alla pagina di panoramica dell’API. Nella navigazione a sinistra sotto **[!UICONTROL Credenziali]**, fai clic sull&#39;opzione **[!UICONTROL Account di servizio (JWT)]**.

   >[!NOTE]
   >
   >Puoi visualizzare le credenziali ed eseguire azioni quali generare token JWT, copiare i dettagli delle credenziali, recuperare il segreto client e così via.

1. Dalla scheda **[!UICONTROL Credenziali client]**, copia l&#39; **[!UICONTROL ID client]**.

   Fai clic su **[!UICONTROL Recupera segreto client]** e copia il **[!UICONTROL segreto client]**.

   ![Credenziali account di servizio](assets/service-account5.png)

1. Passa alla scheda **[!UICONTROL Genera JWT]** e copia le informazioni **[!UICONTROL Payload JWT]** .

Ora puoi utilizzare l’ID client (chiave API), il segreto client e il payload JWT su [configurare l’account IMS](#create-ims-account-configuration) in AEM Assets.

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

### Configurare l’account IMS {#create-ims-account-configuration}

Verifica di aver eseguito i seguenti passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Crea connessione account di servizio (JWT)](#createnewintegration)

Esegui i seguenti passaggi per configurare l’account IMS.

1. Apri la configurazione IMS e passa alla scheda **[!UICONTROL Account]** . Hai tenuto aperta la pagina durante [il recupero del certificato pubblico](#public-certificate).

1. Specifica un **[!UICONTROL titolo]** per l’account IMS.

   Nel campo **[!UICONTROL Server autorizzazioni]** , specifica l’URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Specifica l&#39;ID client nel campo **[!UICONTROL Chiave API]**, **[!UICONTROL Segreto client]** e **[!UICONTROL Payload]** (Payload JWT) che hai copiato durante la creazione della connessione dell&#39;account del servizio (JWT)](#createnewintegration).[

   Fai clic su **[!UICONTROL Crea]**.

   L’account IMS è configurato.

   ![Configurazione dell’account IMS](assets/create-new-integration6.png)


1. Seleziona la configurazione dell’account IMS e fai clic su **[!UICONTROL Verifica stato]**.

   Fare clic su **[!UICONTROL Controlla]** nella finestra di dialogo. Una volta completata la configurazione, viene visualizzato un messaggio che informa che il *Token viene recuperato correttamente*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Puoi disporre di una sola configurazione IMS.
>
>Verifica che la configurazione IMS superi il controllo di integrità. Se la configurazione non supera questa verifica, non è valida. Dovrai quindi eliminarla e creare una nuova configurazione valida.

### Configurare il servizio cloud {#configure-the-cloud-service}

Per configurare il servizio cloud Brand Portal, effettua le seguenti operazioni:

1. Accedi ad AEM Assets.

1. Dal pannello **Strumenti**, passa a **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Nella pagina Configurazioni Brand Portal, fai clic su **[!UICONTROL Crea]**.

1. Specifica un **[!UICONTROL titolo]** per la configurazione.

   Seleziona la configurazione IMS creata durante la [configurazione dell’account IMS](#create-ims-account-configuration).

   Nel campo **[!UICONTROL URL servizio]** , specifica l’URL del tenant di Brand Portal (organizzazione).

   ![](assets/create-cloud-service.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**. Viene creata la configurazione cloud.

   L’istanza AEM Assets as a [!DNL Cloud Service] è ora configurata con il tenant di Brand Portal.

Ora puoi verificare la configurazione controllando l’agente di distribuzione e pubblicando le risorse su Brand Portal.

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Log in to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click on the **[!UICONTROL Test Connection]** icon.

   ![](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=en) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![](assets/test-bpconfig5.png)

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
