---
title: Configurare AEM Assets con Brand Portal
seo-title: Configurare AEM Assets con Brand Portal
description: Ottieni informazioni approfondite sulla configurazione di Risorse AEM con Brand Portal.
seo-description: Ottieni informazioni approfondite sulla configurazione di Risorse AEM con Brand Portal.
uuid: null
contentOwner: Vishabh Gupta
content-type: reference
topic-tags: brand-portal
products: SG_EXPERIENCEMANAGER/ASSETS
discoiquuid: null
translation-type: tm+mt
source-git-commit: e80c961effe4dfb472590562d3caebb13682401c

---


# Configurare AEM Assets con Brand Portal {#configure-aem-assets-with-brand-portal}

Risorse Adobe Experience Manager (AEM) è configurato con Brand Portal tramite Adobe I/O, che fornisce un token IMS per l’autorizzazione del tenant del Brand Portal.

## Prerequisiti {#prerequisites}

Per configurare Risorse AEM con Brand Portal è necessario disporre di quanto segue:

* Un’istanza cloud di Risorse AEM in esecuzione.
* URL tenant del Brand Portal.
* Un utente con privilegi di amministratore di sistema nell’organizzazione IMS del tenant Brand Portal.

**Per ulteriori informazioni, contattate il supporto** .

## Create configuration {#create-new-configuration}

Puoi creare una nuova configurazione su Adobe I/O per configurare Risorse AEM con Brand Portal.

Effettuate i seguenti passaggi nella sequenza elencata:

1. [Ottenere il certificato pubblico](#public-certificate)
1. [Crea integrazione I/O Adobe](#createnewintegration)
1. [Crea configurazione account IMS](#create-ims-account-configuration)
1. [Configurare il servizio cloud](#configure-the-cloud-service)
1. [Verifica della configurazione](#test-configuration)

### Crea configurazione IMS {#create-ims-configuration}

La configurazione IMS autentica il tenant del Brand Portal con l’istanza di creazione di AEM Assets.

La configurazione IMS prevede due passaggi:

* [Ottenere il certificato pubblico](#public-certificate)
* [Crea configurazione account IMS](#create-ims-account-configuration)

### Ottenere il certificato pubblico {#public-certificate}

Il certificato pubblico consente di autenticare il profilo sull&#39;I/O di Adobe.

1. Accedi all’istanza cloud di AEM Assets

1. Dal pannello **Strumenti** ![Strumenti](assets/tools.png) , passa a **[!UICONTROL Protezione]** > Configurazioni **** Adobe IMS.

   ![Interfaccia utente di configurazione account Adobe IMS](assets/ims-configuration1.png)

1. Viene visualizzata la pagina Configurazioni Adobe IMS.

   Fai clic su **[!UICONTROL Crea]**.

   Viene visualizzata la pagina Configurazione **[!UICONTROL account tecnico]** Adobe IMS.

1. Per impostazione predefinita, si apre la scheda **Certificato** .

   In **Cloud Solution**, selezionate **[!UICONTROL Adobe Brand Portal]**.

1. Contrassegnate la casella di controllo **[!UICONTROL Create un nuovo certificato]** e specificate un **alias** per il certificato. L’alias funge da nome della finestra di dialogo.

1. Fate clic su **[!UICONTROL Crea certificato]**. Viene visualizzata una finestra di dialogo. Fate clic su **[!UICONTROL OK]** per generare il certificato pubblico.

   ![Crea certificato](assets/ims-config2.png)

1. Fate clic su **[!UICONTROL Scarica chiave]** pubblica e salvate il file di certificato *AEM-Adobe-IMS.crt* sul computer. Il file del certificato viene utilizzato per [creare l&#39;integrazione](#createnewintegration)I/O Adobe.

   ![Scarica certificato](assets/ims-config3.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   Nella scheda **Account** , potete creare l&#39;account Adobe IMS, ma per questo dovrete disporre dei dettagli di integrazione. Tenete questa pagina aperta per ora.

   Aprite una nuova scheda e [create l&#39;integrazione](#createnewintegration) I/O Adobe per ottenere i dettagli di integrazione per le configurazioni dell&#39;account IMS.

### Crea integrazione I/O Adobe {#createnewintegration}

L&#39;integrazione I/O di Adobe genera Chiave API, Segreto cliente e Payload (JWT), necessaria per configurare le configurazioni dell&#39;account IMS.

1. Accedete alla console di I/O di Adobe con privilegi di amministratore di sistema nell’organizzazione IMS del tenant Brand Portal.

   URL predefinito: [https://console.adobe.io/](https://console.adobe.io/)

1. Fate clic su **[!UICONTROL Crea integrazione]**.

1. Selezionate **[!UICONTROL Accesso a un&#39;API]** e fate clic su **[!UICONTROL Continua]**.

   ![Crea nuova integrazione](assets/create-new-integration1.png)

1. Viene visualizzata una nuova pagina di integrazione.

   Seleziona la tua organizzazione dall’elenco a discesa.

   In **[!UICONTROL Experience Cloud]**, seleziona **[!UICONTROL AEM Brand Portal]** e fai clic su **[!UICONTROL Continua]**.

   Se l’opzione Portale marchio è disabilitata, accertatevi di aver selezionato l’organizzazione corretta dalla casella a discesa sopra l’opzione **[!UICONTROL Adobe Services]** . Se non conosci la tua organizzazione, contatta l’amministratore.

   ![Crea integrazione](assets/create-new-integration2.png)

1. Specificate un nome e una descrizione per l&#39;integrazione. Fate clic su **[!UICONTROL Seleziona un file dal computer]** e caricate il `AEM-Adobe-IMS.crt` file scaricato nella sezione [Ottieni certificati](#public-certificate) pubblici.

1. Seleziona il profilo della tua organizzazione.

   In alternativa, seleziona il profilo predefinito **[!UICONTROL Assets Brand Portal]** e fai clic su **[!UICONTROL Crea integrazione]**. L&#39;integrazione viene creata.

1. Fate clic su **[!UICONTROL Continua per visualizzare i dettagli]** dell&#39;integrazione.

   Copiare la chiave **[!UICONTROL API]**

   Fate clic su **[!UICONTROL Recupera Segreto]** cliente e copiate la chiave Segreto cliente.

   ![Informazioni su chiave API, segreto cliente e payload di un&#39;integrazione](assets/create-new-integration3.png)

1. Passate alla scheda **[!UICONTROL JWT]** e copiate il payload **** JWT.

   Le informazioni relative alla chiave API, alla chiave segreta client e al payload JWT verranno utilizzate per creare la configurazione dell&#39;account IMS.

### Crea configurazione account IMS {#create-ims-account-configuration}

Assicurarsi di aver eseguito i seguenti passaggi:

* [Ottenere il certificato pubblico](#public-certificate)
* [Crea integrazione I/O Adobe](#createnewintegration)

**Passaggi per creare la configurazione dell&#39;account IMS:**

1. Aprite la pagina Configurazione IMS, scheda **[!UICONTROL Account]** . Hai tenuto la pagina aperta alla fine della sezione [Ottieni certificato](#public-certificate)pubblico.

1. Specificate un **[!UICONTROL Titolo]** per l&#39;account IMS.

   Nel server **** di autorizzazione, immettete l’URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Incollate la chiave API, il segreto cliente e il payload JWT che avete copiato al termine dell&#39;integrazione [di](#createnewintegration)Crea I/O Adobe.

   Fai clic su **[!UICONTROL Crea]**.

   Viene creata l&#39;integrazione.

   ![Configurazione account IMS](assets/create-new-integration6.png)


1. Selezionate la configurazione IMS e fate clic su **[!UICONTROL Verifica stato]**. Viene visualizzata una finestra di dialogo.

   Fate clic su **[!UICONTROL Controlla]**. In caso di connessione riuscita, viene visualizzato il messaggio *Token recuperato* .

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Create una sola configurazione IMS valida. Non creare più configurazioni IMS.
>
> Verificate che la configurazione sia sana. Nel caso in cui la configurazione non sia sana, eliminarla e creare una nuova configurazione sana.


### Configurare il servizio cloud {#configure-the-cloud-service}

Per creare la configurazione del servizio cloud Brand Portal, effettuate le seguenti operazioni:

1. Accedi all’istanza cloud di AEM Assets

1. Dal pannello **Strumenti** ![Strumenti](assets/tools.png) , andate a Servizi **** Cloud > Portale **[!UICONTROL marchio]** AEM.

   Si apre la pagina Configurazioni Brand Portal.

1. Fai clic su **[!UICONTROL Crea]**.

1. Specificate un **[!UICONTROL Titolo]** per la configurazione.

   Selezionate IMS Configuration (Configurazione IMS) creata nel passaggio, [create IMS Account configuration](#create-ims-account-configuration).

   Nell’URL **[!UICONTROL del]** servizio, immettete l’URL tenant del Portale marchio.

   ![](assets/create-cloud-service.png)

1. Click **[!UICONTROL Save and Close]**. Viene creata la configurazione cloud. L’istanza cloud di AEM Assets è ora configurata con il tenant del Brand Portal.

### Test configuration {#test-configuration}

1. Accedi alla tua istanza cloud di Risorse AEM.

1. Dal pannello **Strumenti** ![Strumenti](assets/tools.png) , passa a **[!UICONTROL Distribuzione]** > **[!UICONTROL Distribuzione]**.

   ![](assets/test-bpconfig1.png)

1. Viene visualizzata la pagina Distribuzione.

   Un agente di distribuzione Brand Portal `bpdistributionagent0` viene creato in **[!UICONTROL Pubblica su Brand Portal]**.

   Click **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >Per impostazione predefinita, per un tenant Brand Portal viene creato un agente di distribuzione.

1. Viene visualizzata la pagina dell&#39;agente di distribuzione. Per impostazione predefinita, si apre la scheda **[!UICONTROL Stato]** , che popola le code di distribuzione.

   Un agente di distribuzione contiene due code:
   * Una coda di elaborazione per la distribuzione delle risorse a Brand Portal.
   * Coda di errore per le risorse per le quali la distribuzione non è riuscita.
   Potete sottoporre a test singole code o la configurazione complessiva.

   ![](assets/test-bpconfig3.png)

1. Per verificare la connessione tra AEM Assets e Brand Portal, fai clic su **[!UICONTROL Verifica connessione]**.

   ![](assets/test-bpconfig4.png)

   Nella parte inferiore della pagina viene visualizzato un messaggio che informa che il pacchetto di test è stato consegnato correttamente.

   >[!NOTE]
   >
   >Evitate di disattivare l’agente di distribuzione, in quanto potrebbe causare errori nella distribuzione delle risorse (in esecuzione nella coda).

Brand Portal è stato configurato con successo con l’istanza cloud di AEM Assets. È ora possibile:

* [Pubblicare risorse da Risorse AEM a Brand Portal](publish-to-brand-portal.md#publish-assets-to-bp)
* [Pubblicare cartelle da Risorse AEM a Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Pubblicare raccolte da Risorse AEM a Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)

## Registri di distribuzione {#distribution-logs}

È possibile controllare i registri per ottenere informazioni dettagliate sulle azioni eseguite sull&#39;agente di distribuzione.

Ad esempio, abbiamo pubblicato una risorsa da AEM Assets al Portale marchio per verificare la configurazione.

1. Seguite i passaggi (da 1 a 4) come mostrato in **[!UICONTROL Test Connection]** e andate alla pagina dell&#39;agente di distribuzione.

1. Selezionate la coda di distribuzione **[!UICONTROL queue-bpdistributionagent0]** e fate clic su **[!UICONTROL Registri]** per visualizzare i registri di distribuzione.

   ![](assets/test-bpconfig5.png)

La distribuzione contiene i seguenti file di registro:

* INFORMAZIONI: Si tratta di un registro generato dal sistema attivato in una configurazione corretta che abilita l&#39;agente di distribuzione.
* DSTRQ1 (richiesta 1): Attivazione alla connessione di prova.

Quando pubblicate la risorsa, vengono generati i seguenti registri di richieste e risposte:

**Richiesta** agente di distribuzione:
* DSTRQ2 (richiesta 2): Viene attivata la richiesta di pubblicazione delle risorse.
* DSTRQ3 (richiesta 3): Il sistema attiva un’altra richiesta per pubblicare la cartella in cui esiste la risorsa e replicare la cartella in Brand Portal.

**Risposta** agente di distribuzione:
* queue-bpdistributionagent0 (DSTRQ2): La risorsa viene pubblicata in Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): Il sistema replica la cartella contenente la risorsa in Brand Portal.

Nell&#39;esempio precedente, viene attivata un&#39;ulteriore richiesta e risposta. Impossibile trovare la cartella principale (ad esempio Aggiungi percorso) nel Portale marchio perché la risorsa è stata pubblicata per la prima volta, pertanto viene attivata un&#39;ulteriore richiesta per creare una cartella principale con lo stesso nome nel Portale marchio in cui viene pubblicata la risorsa.

Se esiste la cartella principale con lo stesso nome (alias Aggiungi percorso) in Brand Portal, non viene attivata alcuna richiesta aggiuntiva.

>[!NOTE]
>
>Per visualizzare i registri degli errori, selezionate la coda di distribuzione **[!UICONTROL error-queue-bpdistributionagent0]** e fate clic su **[!UICONTROL Registri]**.


## Informazioni aggiuntive {#additional-information}

Vai a `/system/console/slingmetrics` per le statistiche relative al contenuto distribuito:

1. **Metriche del contatore**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Metriche temporali**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`


Consultate la documentazione [di](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) Brand Portal per ulteriori informazioni sulla distribuzione di risorse, cartelle e raccolte agli utenti finali.

<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->


