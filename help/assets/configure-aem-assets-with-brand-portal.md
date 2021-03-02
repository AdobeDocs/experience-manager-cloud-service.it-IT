---
title: Configurare AEM Assets come a [!DNL Cloud Service] con Brand Portal
description: Configurare AEM Assets con Brand Portal.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: bafb952cd984885e0f309b8a78a96ae48320b7df
workflow-type: tm+mt
source-wordcount: '1651'
ht-degree: 19%

---


# Configurare AEM Assets come [!DNL Cloud Service] con Brand Portal {#configure-aem-assets-with-brand-portal}

La configurazione di Adobe Experience Manager Assets Brand Portal consente di pubblicare risorse del marchio approvate da Adobe Experience Manager Assets come istanza [!DNL Cloud Service] in Brand Portal e di distribuirle agli utenti di Brand Portal.

**Flusso di lavoro di configurazione**

AEM Assets as a [!DNL Cloud Service] è configurato con Brand Portal tramite Adobe Developer Console, che fornisce un token account Adobe Identity Management Services (IMS) per l’autorizzazione del tenant di Brand Portal. Richiede configurazioni sia in AEM Assets che in Adobe Developer Console.

1. In AEM Assets, crea un account IMS e genera una chiave pubblica (certificato).
1. In Adobe Developer Console, crea un progetto per il tenant di Brand Portal (organizzazione).
1. Nel progetto , configura un’API utilizzando la chiave pubblica per creare una connessione dell’account del servizio.
1. Ottieni le credenziali dell&#39;account del servizio e le informazioni sul payload JSON Web Token (JWT).
1. In AEM Assets, configura l’account IMS utilizzando le credenziali dell’account del servizio e il payload JWT.
1. In AEM Assets, configura il servizio cloud Brand Portal utilizzando l’account IMS e l’endpoint Brand Portal (URL organizzazione).
1. Verifica la configurazione pubblicando una risorsa da AEM Assets su Brand Portal.

>[!NOTE]
>
>Un’istanza di AEM Assets as a [!DNL Cloud Service] può essere configurata con un solo tenant di Brand Portal.

## Prerequisiti {#prerequisites}

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
1. [Verificare la configurazione](#test-configuration)

### Creare la configurazione IMS {#create-ims-configuration}

La configurazione IMS autentica le risorse AEM come istanza [!DNL Cloud Service] con il tenant di Brand Portal.

La configurazione IMS prevede due passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Configurare l’account IMS](#create-ims-account-configuration)

### Recuperare il certificato pubblico {#public-certificate}

La chiave pubblica (certificato) autentica il tuo profilo in Adobe Developer Console.

1. Accedi a Risorse AEM.
1. Dal pannello **Strumenti**, passa a **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.
1. Nella pagina Configurazioni Adobe IMS, fai clic su **[!UICONTROL Crea]**. Verrà reindirizzato alla pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]** . Per impostazione predefinita, viene visualizzata la scheda **Certificato** .
1. Seleziona **[!UICONTROL Adobe Brand Portal]** nell’elenco a discesa **[!UICONTROL Soluzione cloud]** .
1. Seleziona la casella di controllo **[!UICONTROL Crea nuovo certificato]** e specifica un **alias** per la chiave pubblica. L&#39;alias funge da nome della chiave pubblica.
1. Fai clic su **[!UICONTROL Crea certificato]**. Quindi, fai clic su **[!UICONTROL OK]** per generare la chiave pubblica.

   ![Crea certificato](assets/ims-config2.png)

1. Fai clic sull&#39;icona **[!UICONTROL Scarica chiave pubblica]** e salva il file della chiave pubblica (CRT) sul computer.

   La chiave pubblica verrà utilizzata in seguito per configurare l’API per il tenant di Brand Portal e generare le credenziali dell’account del servizio in Adobe Developer Console.

   ![Scarica certificato](assets/ims-config3.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   Nella scheda **Account** viene creato l’account Adobe IMS che richiede le credenziali dell’account del servizio generate in Adobe Developer Console. Per il momento tieni aperta questa pagina.

   Apri una nuova scheda e [crea una connessione a un account di servizio (JWT) in Adobe Developer Console](#createnewintegration) per ottenere le credenziali e il payload JWT per la configurazione dell’account IMS.

### Crea connessione account di servizio (JWT) {#createnewintegration}

In Adobe Developer Console, i progetti e le API sono configurati a livello di tenant di Brand Portal (organizzazione). La configurazione di un’API crea una connessione a un account di servizio (JWT). Esistono due metodi per configurare l’API, generando una coppia di chiavi (chiavi private e pubbliche) o caricando una chiave pubblica. Per configurare AEM Assets con Brand Portal, devi generare una chiave pubblica (certificato) in AEM Assets e creare credenziali in Adobe Developer Console caricando la chiave pubblica. Queste credenziali sono necessarie per configurare l’account IMS in AEM Assets. Una volta configurato l’account IMS, puoi configurare il servizio cloud Brand Portal in AEM Assets.

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

Ora puoi utilizzare l’ID client (chiave API), il segreto client e il payload JWT per [configurare l’account IMS](#create-ims-account-configuration) in AEM Assets.

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

1. Accedi a Risorse AEM.

1. Dal pannello **Strumenti**, passa a **[!UICONTROL Servizi cloud]** > **[!UICONTROL AEM Brand Portal]**.

1. Nella pagina Configurazioni Brand Portal, fai clic su **[!UICONTROL Crea]**.

1. Specifica un **[!UICONTROL titolo]** per la configurazione.

   Seleziona la configurazione IMS creata durante la [configurazione dell’account IMS](#create-ims-account-configuration).

   Nel campo **[!UICONTROL URL servizio]** , specifica l’URL del tenant di Brand Portal (organizzazione).

   ![](assets/create-cloud-service.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**. Viene creata la configurazione cloud.

   L’istanza di AEM Assets as a [!DNL Cloud Service] è ora configurata con il tenant di Brand Portal.

### Verificare la configurazione {#test-configuration}

Esegui i seguenti passaggi per convalidare la configurazione:

1. Accedi a Risorse AEM.

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

1. Per verificare la connessione tra AEM Assets come [!DNL Cloud Service] e Brand Portal, fai clic sull’ icona **[!UICONTROL Prova connessione]** .

   ![](assets/test-bpconfig4.png)

   Viene visualizzato un messaggio che informa che il pacchetto di test *è stato consegnato correttamente*.

   >[!NOTE]
   >
   >Evita di disabilitare l’agente di distribuzione, in quanto potrebbe impedire la corretta distribuzione delle risorse (in esecuzione nella coda).

Ora puoi:

* [Pubblicare risorse da AEM Assets su Brand Portal](publish-to-brand-portal.md)
* [Pubblicare cartelle da AEM Assets su Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Pubblicare raccolte da AEM Assets su Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Pubblicare risorse da Brand Portal in AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=en)  - Asset Sourcing in Brand Portal
* [Pubblicare predefiniti, schemi e facet in Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Pubblicare tag in Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Per ulteriori informazioni, consulta la [documentazione di Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/home.html) .

## Registri di distribuzione {#distribution-logs}

Puoi monitorare i registri degli agenti di distribuzione per il flusso di lavoro di pubblicazione delle risorse.

Ad esempio, abbiamo pubblicato una risorsa da AEM Assets su Brand Portal per convalidare la configurazione.

1. Segui i passaggi da 1 a 4 descritti nella sezione [Test Configuration](#test-configuration) e passa alla pagina dell&#39;agente di distribuzione.
1. Fai clic su **[!UICONTROL Registri]** per visualizzare i registri di elaborazione ed errore.

   ![](assets/test-bpconfig5.png)

L’agente di distribuzione ha generato i seguenti registri:

* INFORMAZIONI: Si tratta di un registro generato dal sistema che viene attivato in caso di configurazione corretta dell’agente di distribuzione.
* DSTRQ1 (richiesta 1): si attiva durante la prova della connessione.

Quando viene pubblicata la risorsa, vengono generati i seguenti registri di richieste e risposte:

**Richiesta dell’agente di distribuzione**:

* DSTRQ2 (richiesta 2): viene attivata la richiesta di pubblicazione della risorsa.
* DSTRQ3 (richiesta 3): Il sistema attiva un’altra richiesta per pubblicare la cartella Risorse AEM (in cui esiste la risorsa) e replica la cartella in Brand Portal.

**Risposta dell’agente di distribuzione**:

* queue-bpdistributionagent0 (DSTRQ2): la risorsa viene pubblicata su Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): Il sistema replica la cartella Risorse AEM (contenente la risorsa) in Brand Portal.

Nell’esempio precedente, viene attivata un’ulteriore combinazione di richiesta e risposta. Impossibile trovare la cartella principale (Aggiungi percorso) in Brand Portal perché la risorsa è stata pubblicata per la prima volta. Pertanto, è stata attivata un’ulteriore richiesta per creare una cartella principale con lo stesso nome in Brand Portal in cui viene pubblicata la risorsa.

>[!NOTE]
>
>Viene generata un’ulteriore richiesta nel caso in cui la cartella principale non esista in Brand Portal o sia stata modificata in AEM Assets.

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
