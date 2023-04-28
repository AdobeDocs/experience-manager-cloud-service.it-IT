---
title: Configurare AEM Assets come [!DNL Cloud Service] con Brand Portal
description: Configurare AEM Assets con Brand Portal.
contentOwner: Vishabh Gupta
feature: Brand Portal,Asset Distribution,Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '2508'
ht-degree: 12%

---

# Configurare Experience Manager Assets con Brand Portal {#configure-aem-assets-with-brand-portal}

La configurazione di Adobe Experience Manager Assets Brand Portal consente di pubblicare risorse di marchio approvate da Adobe Experience Manager Assets come [!DNL Cloud Service] Iscriviti a Brand Portal e distribuiscili agli utenti Brand Portal.

## Attivare Brand Portal utilizzando Cloud Manager {#activate-brand-portal}

L’utente di Cloud Manager attiva Brand Portal per un Experience Manager Assets as a [!DNL Cloud Service] istanza. Il flusso di lavoro di attivazione crea le configurazioni richieste (token di autorizzazione, configurazione IMS e servizio cloud Brand Portal) nel back-end e riflette lo stato del tenant Brand Portal in Cloud Manager. Attivando Brand Portal gli utenti Experience Manager Assets possono pubblicare le risorse in Brand Portal e distribuirle agli utenti Brand Portal.

**Prerequisiti**

Per attivare Brand Portal su Experience Manager Assets as a è necessario quanto segue [!DNL Cloud Service] istanza:

* Un Experience Manager Assets funzionante come [!DNL Cloud Service] istanza.
* Un utente con accesso a Cloud Manager, assegnato a Profili del prodotto Cloud Manager. Vedi [accesso a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager) per ulteriori informazioni.

>[!NOTE]
>
>È necessario un ambiente di produzione configurato per un Experience Manager Assets as a [!DNL Cloud Service] istanza per la connessione con il tenant Brand Portal.

**Passaggi per attivare Brand Portal**

È possibile attivare Brand Portal durante la creazione degli ambienti di produzione per il Experience Manager Assets as a [!DNL Cloud Service] o separatamente. Supponiamo che l’ambiente sia già stato creato e che sia ora necessario attivare Brand Portal.

1. Accedi ad Adobe Cloud Manager e passa a **[!UICONTROL Ambienti]**.

   La **[!UICONTROL Ambienti]** visualizza l’elenco di tutti gli ambienti esistenti.

1. Seleziona gli ambienti (uno per uno) dall’elenco per visualizzare i dettagli dell’ambiente.

   Brand Portal ha diritto a uno degli ambienti disponibili e si riflette nella **[!UICONTROL Informazioni sull&#39;ambiente]**.

   Una volta trovato l&#39;ambiente associato a Brand Portal, fai clic sul pulsante **[!UICONTROL Attiva Brand Portal]** per avviare il flusso di lavoro di attivazione.

   ![Attiva Brand Portal](assets/create-environment4.png)

1. L’attivazione del tenant Brand Portal richiede pochi minuti, in quanto il flusso di lavoro di attivazione crea le configurazioni richieste nel back-end. Una volta attivato il tenant Brand Portal, lo stato diventa Attivato.

   ![Visualizza stato](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal deve essere attivato sulla stessa organizzazione IMS di Experience Manager Assets come [!DNL Cloud Service] istanza.
>
>Se disponi di una configurazione cloud Brand Portal esistente ([configurato manualmente tramite la console Adobe Developer](#manual-configuration)) per un’organizzazione IMS (org1-esistente) e il tuo Experience Manager Assets as a [!DNL Cloud Service] L’istanza è configurata per un’altra organizzazione IMS (org2-new), attivando Brand Portal da Cloud Manager l’organizzazione Brand Portal IMS viene reimpostata su `org2-new`. Anche se la configurazione cloud configurata manualmente è attiva `org1-existing` sarà visibile nell’istanza di authoring di Experience Manager Assets ma non sarà più in uso dopo l’attivazione di Brand Portal da Cloud Manager.
>
>Se la configurazione cloud Brand Portal esistente e Experience Manager Assets as a [!DNL Cloud Service] Le istanze utilizzano la stessa organizzazione IMS (org1), è necessario attivare Brand Portal solo da Cloud Manager.
>
>Non modificare le impostazioni generate automaticamente.

**Consulta anche**:

* [Aggiungere utenti e ruoli in Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)

* [Gestione degli ambienti in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**Accedi al tuo tenant Brand Portal**:

Dopo l’attivazione del tenant Brand Portal in Cloud Manager, puoi accedere a Brand Portal dall’Admin Console o utilizzando direttamente l’URL del tenant.

L’URL predefinito del tenant Brand Portal è: `https://<tenant-id>.brand-portal.adobe.com/`.

In questo caso, l’ID tenant è l’organizzazione IMS.

Esegui i seguenti passaggi se non sei sicuro dell’URL Brand Portal:

1. Accedi a [Admin Console](https://adminconsole.adobe.com/) e passa a **[!UICONTROL Prodotti]**.
1. Dal pannello di sinistra, seleziona **[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**.
1. Fai clic su **[!UICONTROL Vai a Brand Portal]** per aprire direttamente Brand Portal nel browser.

   Oppure copia l’URL del tenant Brand Portal dal **[!UICONTROL Vai a Brand Portal]** collegalo e incollalo nel browser per aprire l’interfaccia di Brand Portal.

   ![Accedere a Brand Portal](assets/access-bp-on-cloud.png)


**Prova connessione**

Esegui i seguenti passaggi per convalidare la connessione tra Experience Manager Assets as a [!DNL Cloud Service] istanza e tenant Brand Portal:

1. Accedi a Experience Manager Assets.

1. Da **Strumenti** pannello, passa a **[!UICONTROL Distribuzione]** > **[!UICONTROL Distribuzione]**.

   ![](assets/test-bpconfig1.png)

   Un agente di distribuzione Brand Portal (**[!UICONTROL bpdistributionagent0]**) viene creato in **[!UICONTROL Pubblicare su Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Fai clic su **[!UICONTROL Pubblicare su Brand Portal]** per aprire l’agente di distribuzione.

   Puoi vedere le code di distribuzione sotto la sezione **[!UICONTROL Stato]** scheda .

   Un agente di distribuzione contiene due code:
   * **Coda di elaborazione**: per la distribuzione delle risorse in Brand Portal.

   * **Coda di errore**: per le risorse per le quali la distribuzione non è riuscita.
   >[!NOTE]
   >
   >È consigliabile esaminare gli errori e cancellare periodicamente la **coda di errore**.

   ![](assets/test-bpconfig3.png)

1. Verificare la connessione tra Experience Manager Assets come [!DNL Cloud Service] e Brand Portal, fai clic sul pulsante **[!UICONTROL Prova connessione]** icona.

   ![](assets/test-bpconfig4.png)

   Viene visualizzato un messaggio che informa che il *il pacchetto di test è stato consegnato correttamente*.

   >[!NOTE]
   >
   >Evita di disabilitare l’agente di distribuzione, in quanto potrebbe impedire la corretta distribuzione delle risorse (in esecuzione nella coda).

Verificare la connessione tra il Experience Manager Assets come [!DNL Cloud Service] istanza e tenant Brand Portal, pubblica una risorsa da Experience Manager Assets a Brand Portal. Se la connessione ha esito positivo, la risorsa pubblicata è visibile nell’interfaccia di Brand Portal.


Ora puoi:

* [Pubblicare risorse da Experience Manager Assets in Brand Portal](publish-to-brand-portal.md)
* [Pubblicare cartelle da Experience Manager Assets in Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Pubblicare raccolte da Experience Manager Assets in Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Pubblicare risorse da Brand Portal in Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=it) - Origine risorse in Brand Portal
* [Pubblicare predefiniti, schemi e facet in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Pubblicare tag in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Vedi [Documentazione di Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) per ulteriori informazioni.

**Registri di distribuzione**

Puoi monitorare i registri degli agenti di distribuzione per il flusso di lavoro di pubblicazione delle risorse.

Ora pubblichiamo una risorsa da Experience Manager Assets a Brand Portal e vediamo i registri.

1. Segui i passaggi da 1 a 4 descritti nella sezione **Prova connessione** e passa alla pagina dell’agente di distribuzione.
1. Fai clic su **[!UICONTROL Registri]** per visualizzare i registri di elaborazione ed errore.

   ![](assets/test-bpconfig5.png)

L’agente di distribuzione ha generato i seguenti registri:

* INFORMAZIONI: Si tratta di un registro generato dal sistema che viene attivato in caso di configurazione corretta dell’agente di distribuzione.
* DSTRQ1 (richiesta 1): si attiva durante la prova della connessione.

Quando viene pubblicata la risorsa, vengono generati i seguenti registri di richieste e risposte:

**Richiesta dell’agente di distribuzione**:

* DSTRQ2 (richiesta 2): viene attivata la richiesta di pubblicazione della risorsa.
* DSTRQ3 (richiesta 3): Il sistema attiva un’altra richiesta per pubblicare la cartella Experience Manager Assets (in cui si trova la risorsa) e replica la cartella in Brand Portal.

**Risposta dell’agente di distribuzione**:

* queue-bpdistributionagent0 (DSTRQ2): la risorsa viene pubblicata su Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): Il sistema replica la cartella Experience Manager Assets (contenente la risorsa) in Brand Portal.

Nell’esempio precedente, viene attivata un’ulteriore combinazione di richiesta e risposta. Impossibile trovare la cartella principale (Aggiungi percorso) in Brand Portal perché la risorsa è stata pubblicata per la prima volta. Pertanto, è stata attivata un&#39;ulteriore richiesta per creare una cartella principale con lo stesso nome in Brand Portal in cui viene pubblicata la risorsa.

>[!NOTE]
>
>Viene generata un’ulteriore richiesta nel caso in cui la cartella principale non esista in Brand Portal o sia stata modificata in Experience Manager Assets.

Insieme al flusso di lavoro di automazione per attivare Brand Portal su Experience Manager Assets as a [!DNL Cloud Service]esiste un altro metodo per configurare manualmente Experience Manager Assets come [!DNL Cloud Service] con Brand Portal che utilizza la console Adobe Developer, che non è più consigliata.

>[!NOTE]
>
>Se riscontri problemi durante l’attivazione del tenant Brand Portal, contatta l’Assistenza clienti .

## Configurazione manuale tramite la console Adobe Developer {#manual-configuration}

La sezione seguente descrive come configurare manualmente Experience Manager Assets as a [!DNL Cloud Service] con Brand Portal tramite la console Adobe Developer.

In precedenza, Experience Manager Assets as a [!DNL Cloud Service] è stato configurato manualmente con Brand Portal tramite Adobe Developer Console, che fornisce un token account Adobe Identity Management Services (IMS) per l’autorizzazione del tenant Brand Portal. Richiede configurazioni sia in Experience Manager Assets che nella console Adobe Developer.

1. In Experience Manager Assets, crea un account IMS e genera una chiave pubblica (certificato).
1. In Adobe Developer Console, crea un progetto per il tenant Brand Portal (organizzazione).
1. Nel progetto , configura un’API utilizzando la chiave pubblica per creare una connessione dell’account del servizio.
1. Ottieni le credenziali dell&#39;account del servizio e le informazioni sul payload JSON Web Token (JWT).
1. In Experience Manager Assets, configura l’account IMS utilizzando le credenziali dell’account del servizio e il payload JWT.
1. In Experience Manager Assets, configura il servizio cloud Brand Portal utilizzando l’account IMS e l’endpoint Brand Portal (URL organizzazione).
1. Verifica la configurazione pubblicando una risorsa da Experience Manager Assets a Brand Portal.

>[!NOTE]
>
>Un Experience Manager Assets as a [!DNL Cloud Service] L’istanza deve essere configurata con un solo tenant Brand Portal.

**Prerequisiti**

Per configurare Experience Manager Assets con Brand Portal è necessario quanto segue:

* Un Experience Manager Assets funzionante come [!DNL Cloud Service] istanza
* URL tenant Brand Portal
* Un utente con privilegi di amministratore di sistema nell’organizzazione IMS del tenant di Brand Portal

## Creare la configurazione {#create-new-configuration}

Esegui i seguenti passaggi nella sequenza specificata per configurare Experience Manager Assets con Brand Portal.

1. [Recuperare il certificato pubblico](#public-certificate)
1. [Crea connessione account di servizio (JWT)](#createnewintegration)
1. [Configurare l’account IMS](#create-ims-account-configuration)
1. [Configurare il servizio cloud](#configure-the-cloud-service)

### Creare la configurazione IMS {#create-ims-configuration}

La configurazione IMS autentica il tuo Experience Manager Assets come [!DNL Cloud Service] istanza con il tenant Brand Portal.

La configurazione IMS prevede due passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Configurare l’account IMS](#create-ims-account-configuration)

### Recuperare il certificato pubblico {#public-certificate}

La chiave pubblica (certificato) autentica il tuo profilo nella console Adobe Developer.

1. Accedi a Experience Manager Assets.
1. Da **Strumenti** pannello, passa a **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.
1. Nella pagina Configurazioni Adobe IMS , fai clic su **[!UICONTROL Crea]**. Verrà reindirizzato al **[!UICONTROL Configurazione dell’account tecnico Adobe IMS]** pagina. Per impostazione predefinita, la **Certificato** viene visualizzata la scheda .
1. Seleziona **[!UICONTROL Adobe Brand Portal]** in **[!UICONTROL Soluzione cloud]** elenco a discesa.
1. Seleziona la **[!UICONTROL Crea nuovo certificato]** e specifica un **alias** per la chiave pubblica. L&#39;alias funge da nome della chiave pubblica.
1. Fai clic su **[!UICONTROL Crea certificato]**. Quindi, fai clic su **[!UICONTROL OK]** per generare la chiave pubblica.

   ![Crea certificato](assets/ims-config2.png)

1. Fai clic sul pulsante **[!UICONTROL Scarica chiave pubblica]** e salva il file della chiave pubblica (CRT) sul computer.

   La chiave pubblica viene utilizzata in seguito per configurare l’API per il tenant Brand Portal e generare le credenziali dell’account del servizio in Adobe Developer Console.

   ![Scarica certificato](assets/ims-config3.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   In **Account** viene creato l’account Adobe IMS che richiede le credenziali dell’account del servizio generate in Adobe Developer Console. Per il momento tieni aperta questa pagina.

   Apri una nuova scheda e [creare una connessione account di servizio (JWT) nella console Adobe Developer](#createnewintegration) per ottenere le credenziali e il payload JWT per la configurazione dell’account IMS.

### Crea connessione account di servizio (JWT) {#createnewintegration}

Nella console Adobe Developer, i progetti e le API sono configurati a livello di tenant Brand Portal (organizzazione). La configurazione di un’API crea una connessione a un account di servizio (JWT). Esistono due metodi per configurare l’API, generando una coppia di chiavi (chiavi private e pubbliche) o caricando una chiave pubblica. Per configurare Experience Manager Assets con Brand Portal, devi generare una chiave pubblica (certificato) in Experience Manager Assets e creare le credenziali nella console Adobe Developer caricando la chiave pubblica. Queste credenziali sono necessarie per configurare l’account IMS in Experience Manager Assets. Una volta configurato l’account IMS, puoi configurare il servizio cloud Brand Portal in Experience Manager Assets.

Esegui i seguenti passaggi per generare le credenziali dell’account del servizio e il payload JWT:

1. Accedi alla console Adobe Developer con privilegi di amministratore di sistema nell’organizzazione IMS (tenant Brand Portal). L’URL predefinito è [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Accertati di aver selezionato l’organizzazione IMS corretta (tenant Brand Portal) dall’elenco a discesa (organizzazione) che si trova nell’angolo in alto a destra.

1. Fai clic su **[!UICONTROL Crea nuovo progetto]**. Per la tua organizzazione viene creato un progetto vuoto con un nome generato dal sistema.

   Fai clic su **[!UICONTROL Modifica progetto]** per aggiornare **[!UICONTROL Titolo del progetto]** e **[!UICONTROL Descrizione]** e fai clic su **[!UICONTROL Salva]**.

1. In **[!UICONTROL Panoramica del progetto]** scheda , fai clic su **[!UICONTROL Aggiungi API]**.

1. In **[!UICONTROL Aggiungi una finestra API]**, seleziona **[!UICONTROL AEM Brand Portal]** e fai clic su **[!UICONTROL Successivo]**.

   Assicurati di avere accesso al servizio Experience Manager Brand Portal.

1. In **[!UICONTROL Configurare l’API]** finestra, fai clic su **[!UICONTROL Carica la chiave pubblica]**. Quindi, fai clic su **[!UICONTROL Selezionare un file]** e carica la chiave pubblica (file .crt) scaricata nel [ottenere un certificato pubblico](#public-certificate) sezione .

   Fai clic su **[!UICONTROL Avanti]**.

   ![Carica chiave pubblica](assets/service-account3.png)

1. Verifica la chiave pubblica e fai clic su **[!UICONTROL Successivo]**.

1. Seleziona **[!UICONTROL Assets Brand Portal]** come profilo di prodotto predefinito e fai clic su **[!UICONTROL Salva API configurata]**.

   ![Seleziona profilo prodotto](assets/service-account4.png)

1. Una volta configurata l’API, vieni reindirizzato alla pagina di panoramica dell’API. Dalla navigazione a sinistra sotto **[!UICONTROL Credenziali]**, fai clic su **[!UICONTROL Account di servizio (JWT)]** opzione .

   >[!NOTE]
   >
   >Puoi visualizzare le credenziali ed eseguire azioni quali generare token JWT, copiare i dettagli delle credenziali, recuperare il segreto client e così via.

1. Da **[!UICONTROL Credenziali client]** , copia il **[!UICONTROL ID client]**.

   Fai clic su **[!UICONTROL Recupera segreto client]** e copia il **[!UICONTROL segreto client]**.

   ![Credenziali account di servizio](assets/service-account5.png)

1. Passa a **[!UICONTROL Genera JWT]** e copia la **[!UICONTROL Payload JWT]** informazioni.

Ora puoi utilizzare l’ID client (chiave API), il segreto client e il payload JWT su [configurare l’account IMS](#create-ims-account-configuration) in Experience Manager Assets.

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

1. Apri la configurazione IMS e passa alla pagina **[!UICONTROL Account]** scheda . Hai tenuto la pagina aperta mentre [ottenimento del certificato pubblico](#public-certificate).

1. Specifica un **[!UICONTROL titolo]** per l’account IMS.

   In **[!UICONTROL Server autorizzazioni]** specifica l’URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Specifica l’ID client nel **[!UICONTROL Chiave API]** campo, **[!UICONTROL Segreto client]** e **[!UICONTROL Payload]** (Payload JWT) che hai copiato mentre [creazione della connessione dell&#39;account del servizio (JWT)](#createnewintegration).

   Fai clic su **[!UICONTROL Crea]**.

   L’account IMS è configurato.

   ![Configurazione dell’account IMS](assets/create-new-integration6.png)


1. Seleziona la configurazione dell’account IMS e fai clic su **[!UICONTROL Verifica stato]**.

   Fai clic su **[!UICONTROL Controlla]** nella finestra di dialogo. Una volta completata la configurazione, viene visualizzato un messaggio che informa che *Recupero del token completato*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Puoi disporre di una sola configurazione IMS.
>
>Verifica che la configurazione IMS superi il controllo di integrità. Se la configurazione non supera questa verifica, non è valida. Dovrai quindi eliminarla e creare una nuova configurazione valida.

### Configurare il servizio cloud {#configure-the-cloud-service}

Esegui i seguenti passaggi per configurare il servizio cloud Brand Portal:

1. Accedi a Experience Manager Assets.

1. Da **Strumenti** pannello, passa a **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Nella pagina Configurazioni Brand Portal, fai clic su **[!UICONTROL Crea]**.

1. Specifica un **[!UICONTROL titolo]** per la configurazione.

   Seleziona la configurazione IMS creata mentre [configurazione dell’account IMS](#create-ims-account-configuration).

   In **[!UICONTROL URL servizio]** specifica l’URL del tenant Brand Portal (organizzazione).

   ![](assets/create-cloud-service.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**. Viene creata la configurazione cloud.

   Il tuo Experience Manager Assets as a [!DNL Cloud Service] L’istanza è ora configurata con il tenant Brand Portal.

Ora puoi testare la configurazione controllando l’agente di distribuzione e pubblicando le risorse in Brand Portal.

**Inserire nell&#39;elenco Consentiti gli IP Egress in SPS se l&#39;anteprima sicura è abilitata**
Se utilizzi Dynamic Media-Scene7 con [anteprima protetta abilitata](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en) per un&#39;azienda), allora si consiglia di amministratore dell&#39;azienda Scene7 [inserire nell&#39;elenco Consentiti gli IP in uscita pubblici](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en#testing-the-secure-testing-service) per le rispettive aree geografiche che utilizzano l’interfaccia flash SPS (Scene7 Publishing System).
Gli IP in uscita sono i seguenti:

| **Regione** | **IP avanzato** |
|--- |--- |
| ND | 130.248.160.68, 20.94.203.130 |
| EMEA | 185.34.189.3, 51.132.146.75 |
| APAC | 63.140.44.54 |

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Login to AEM Assets.

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
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

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

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)