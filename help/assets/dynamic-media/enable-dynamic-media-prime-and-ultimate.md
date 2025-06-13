---
title: Abilita  [!DNL Dynamic Media] Prime e Ultimate
description: Scopri come abilitare  [!DNL Dynamic Media] le offerte Prime e Ultimate.
feature: Asset Management
role: User, Admin
exl-id: 0ee161f5-bf44-41f1-928e-c07574fd43cc
source-git-commit: 82a3016149645701abe829ad89c493f480956267
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 4%

---

# Abilita [!DNL Dynamic Media] Prime e Ultimate {#enable-dynamic-media-prime-and-ultimate}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità dell’interfaccia utente</b></a>
        </td>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
    </tr>
    <tr>
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

[!DNL Adobe Experience Manager] as a Cloud Service consente di accedere alle offerte di [!DNL Dynamic Media] Prime e Ultimate per semplificare i flussi di lavoro digitali e ottimizzare la gestione dei contenuti. Consulta [Dynamic Media Prime e Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md) per comprenderne i vantaggi e le differenze chiave.

Questo articolo fornisce il flusso di lavoro end-to-end per abilitare le offerte Prime e Ultimate di [!DNL Dynamic Media].

## Abilita Ultimate [!DNL Dynamic Media] {#enable-dynamic-media-ultimate}

Per abilitare [!DNL Dynamic Media] Ultimate:

1. [Attiva [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)
1. [Configura [!DNL Dynamic Media] soluzioni](#configure-dynamic-media-solutions)
1. [Crea ed elenca [!DNL Dynamic Media] società](#create-and-list-dynamic-media-companies)
1. [Configurare il dominio personalizzato nel livello di consegna](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the [!DNL AEM] [!DNL Dynamic Media] API card](#onboarding-api-keys)
-->

Se devi abilitare [!DNL Dynamic Media Prime], consulta i collegamenti rapidi forniti in [Abilita [!DNL Dynamic Media Prime]](#enable-dynamic-media-prime).

### Attiva [!DNL Dynamic Media with OpenAPI] {#activate-dynamic-media-with-openapi}

[!DNL Dynamic Media] con funzionalità OpenAPI pone DAM al centro di un ecosistema agile ed efficiente della catena di fornitura dei contenuti per garantire la governance e la distribuzione delle risorse.

Il primo passaggio del processo di abilitazione di [!DNL Dynamic Media] Ultimate consiste nell&#39;attivare [[!DNL Dynamic Media] con OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) per l&#39;ambiente Cloud Service.

#### Preparati a iniziare {#prerequisites}

Prima di avviare il processo di attivazione, è necessario soddisfare i seguenti requisiti:

1. [Accesso a Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Il programma include [!DNL Dynamic Media] soluzioni](#configure-dynamic-media-solutions).
1. Hai [!DNL Dynamic Media] licenza Prime o Ultimate.

#### Abilitare le funzionalità di [!DNL Dynamic Media with OpenAPI] nell&#39;ambiente Cloud Service {#enable-dynamic-media-with-openapi-capabilites-in-your-CS-environment}

Eseguire la procedura seguente per abilitare [!DNL Dynamic Media with OpenAPI] per l&#39;ambiente del servizio cloud:

1. [Passare all&#39;interfaccia utente di Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).

1. [Creare un ambiente](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments), se non si dispone dell&#39;accesso a uno esistente.

1. Seleziona **[!UICONTROL Fai clic per attivare]** nella riga **[!UICONTROL Dynamic Media]** della sezione **[!UICONTROL Informazioni sull&#39;ambiente]** nella pagina dei dettagli dell&#39;ambiente.

   ![attiva elementi multimediali dinamici con funzionalità OpenAPI](/help/assets/assets/activate-adv-capabiliites-of-dm-openAPI.png)

1. Fare clic su **[!UICONTROL Attiva]** nella finestra di dialogo di conferma per avviare il processo di attivazione di [!DNL Dynamic Media with OpenAPI]. Dopo l’attivazione corretta, Cloud Manager visualizza i seguenti aggiornamenti di stato:
   1. **[!UICONTROL Fase ambiente]**: **[!UICONTROL In esecuzione]**
   1. ![DM attivato](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media &#x200B;]**:**[!UICONTROL &#x200B; Le funzionalità OpenAPI sono attivate &#x200B;]**

      ![attivazione completata](/help/assets/assets/activation-successful.png){width="700" align="left"}

#### Riprova attivazione {#retry-activation}

Se l&#39;attivazione non riesce, Cloud Manager visualizza i seguenti aggiornamenti di stato:

* **[!UICONTROL Fase ambiente]**: **[!UICONTROL DM con OpenAPI non riuscita]**
* ![DM attivato](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media &#x200B;]**:**[!UICONTROL &#x200B; Impossibile attivare le funzionalità OpenAPI &#x200B;]**

  ![riprova attivazione](/help/assets/assets/retry-dm-openapi-failed-activation.png){width="700" align="left"}

Seleziona **[!UICONTROL Fai clic per riprovare]** per riavviare l&#39;attivazione.

In alternativa, per riavviare il processo di attivazione, eseguire la procedura seguente:

1. Passa alla pagina in cui sono elencati tutti gli ambienti.

1. Fai clic su altre opzioni (![altre opzioni](/help/assets/assets/three-dots.svg)) alla fine della riga dell&#39;ambiente.

1. Seleziona **[!UICONTROL Riprova DM con attivazione OpenAPI]** per riavviare l&#39;attivazione.

   ![riprova attivazione dalla pagina dei dettagli dell&#39;ambiente](/help/assets/assets/restart-activation-process-from-list-environment-page.png)

### Configura [!DNL Dynamic Media] soluzioni {#configure-dynamic-media-solutions}

Configura le soluzioni [!UICONTROL Dynamic Media] per utilizzare le funzionalità di base e avanzate di [Dynamic Media con OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) in ambienti esistenti o nuovi disponibili in Cloud Manager.

#### Preparati a iniziare {#prerequisites-to-configure-dynamic-media-solutions}

Per configurare le soluzioni [!UICONTROL Dynamic Media], assicurati di disporre delle seguenti informazioni:

1. [Accesso a Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. Hai [!DNL Dynamic Media] licenza Ultimate.

#### Configura [!DNL Dynamic Media] soluzioni per la distribuzione delle risorse {#configure-dynamic-media-solutions-for-asset-delivery}

Esegui i passaggi seguenti:

1. [Crea un nuovo programma](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program) o passa a un programma esistente e fai clic su **[!UICONTROL Modifica]**. Nella pagina **[!UICONTROL Configurazione per la produzione]** viene visualizzata la scheda **[!UICONTROL Soluzioni e componenti aggiuntivi]**.

1. Seleziona **[!UICONTROL Assets]**, **[!UICONTROL Assets Prime]**, **[!UICONTROL Assets Ultimate]** o **[!UICONTROL Sites]** per aggiungere la soluzione **[!UICONTROL Dynamic Media]** al programma.

1. Seleziona la soluzione **[!UICONTROL Dynamic Media]** e fai clic su **[!UICONTROL Continua]** per aggiungere la soluzione **[!UICONTROL Dynamic Media]** al programma. Questa azione consente di riavviare tutti gli ambienti esistenti nel programma e di aggiungere la soluzione [!DNL Dynamic Media]. Inoltre, qualsiasi nuovo ambiente creato con il programma ottiene automaticamente [!DNL Dynamic Media].

   ![configurazione per produzione](/help/assets/assets/set-up-for-prod.png){width="500" align="left"}

Consulta [Attiva [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi) per iniziare a utilizzare le funzionalità di [!DNL Dynamic Media] con funzionalità OpenAPI nel tuo ambiente.

### Crea ed elenca [!DNL Dynamic Media] società {#create-and-list-dynamic-media-companies}

Crea ed elenca [!DNL Dynamic Media] aziende nel tuo ambiente AEM Cloud Service per gestire le configurazioni nel tuo ambiente AEM.

#### Preparati a iniziare {#prerequisites-to-create-and-list-dynamic-media-companies}

Per visualizzare le società (account) esistenti o aggiungere una nuova società [!DNL Dynamic Media] (account) nell&#39;organizzazione IMS, è necessario disporre di:

1. [Accesso a Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).

1. Hai [!DNL Dynamic Media] licenza Ultimate.

#### Crea ed elenca [!DNL Dynamic Media] società nella tua organizzazione IMS {#create-and-list-dynamic-media-companies-in-your-ims-organisation}

Eseguire la procedura seguente per creare ed elencare una nuova società [!DNL Dynamic Media] (account) che può essere configurata nell&#39;ambiente [!DNL AEM]:

1. Passare alla [pagina licenze Cloud Manager](https://experience-stage.adobe.com/#/@ssahnichstage/cloud-manager/license).

1. Fai clic su **[!UICONTROL Aggiungi società]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Crea società Dynamic Media]**.

1. Specifica un nome univoco per la società [!DNL Dynamic Media], seleziona un&#39;area geografica della società e aggiungi un elenco di ID e-mail di amministratore della società separati da virgole.

   ![Crea società Dynamic Media](/help/assets/assets/create-dynamic-media-company.png){width="500" align="left"}

1. Fai clic su **[!UICONTROL Crea]** per iniziare a creare la tua società. Questa azione aggiunge una nuova riga alla sezione **[!UICONTROL [!DNL Dynamic Media]aziende]** e visualizza **[!UICONTROL Configurazione]** come **[!UICONTROL STATO]** della società.

   ![ha avviato la creazione della società Dynamic Media](/help/assets/assets/dm-company-creation-initiated.png)

1. **Facoltativo:** Fai clic sull&#39;icona ![info](/help/assets/assets/info-icon-solid-black.svg) per visualizzare i dettagli della società. Lo stato **[!UICONTROL STATUS]** viene aggiornato a **[!UICONTROL Ready]** al momento della creazione della società.

   ![Informazioni sulla società di Dynamic Media](/help/assets/assets/dm-company-information.png)

1. In qualità di amministratore di Dynamic Media, controlla la tua cassetta postale per trovare un messaggio e-mail di benvenuto che includa un elenco di passaggi per [configurare [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#architecture-diagram-of-dynamic-media) la società nell&#39;ambiente Cloud Service [!DNL AEM] per iniziare.

   ![e-mail di benvenuto](/help/assets/assets/welcome-email.png)

#### Ritenta creazione società {#retry-company-creation}

Se la creazione della società [!DNL Dynamic Media] non riesce, eseguire i passaggi seguenti in base allo stato di errore:

1. Se **[!UICONTROL Stato]** è In sospeso, segnalare il problema al team di assistenza clienti per risolverlo.


   ![stato in sospeso](/help/assets/assets/company-creation-pending-status.png){width="350" align="center"}



1. Se **[!UICONTROL Stato]** non riesce, riprovare in base al motivo dell&#39;errore.

   ![stato non riuscito](/help/assets/assets/company-creation-failure-status.png){width="380" align="center"}

### Facoltativo: configurare il dominio personalizzato nel livello di consegna {#configure-custom-domain-in-delivery-tier}

Se AEM as a Cloud Service viene fornito con un dominio predefinito, puoi personalizzarlo in base alle tue esigenze. Allega un dominio personalizzato al livello di consegna utilizzando Cloud Manager.

#### Preparati a iniziare {#prerequisites-to-configure-custom-domain-in-delivery-tier}

Prima di avviare il processo di configurazione, è necessario soddisfare i seguenti requisiti:

1. [Accesso a Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Già attivato [!DNL Dynamic Media with OpenAPI] nel tuo ambiente](#activate-dynamic-media-with-openapi).
1. Abilitazione di [!DNL Dynamic Media with OpenAPI] in stato pronto.
1. Certificato di tipo EV o OV per il dominio da utilizzare per il livello di consegna. Per ulteriori dettagli, vedere [Introduzione ai certificati SSL](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates).

#### Configurare il dominio personalizzato nel livello di consegna tramite Cloud Manager {#configure-custom-domain-in-delivery-tier-using-cloud-manager}

Esegui i seguenti passaggi in Cloud Manager per configurare un dominio personalizzato nel livello di consegna:

1. [Aggiungere un certificato SSL gestito dal cliente](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert).

1. [Aggiungere un nome di dominio personalizzato](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings).

1. Passare alla pagina dei dettagli dell&#39;ambiente e [aggiungere una configurazione CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/domain-mappings/add-domain-mapping). Durante l&#39;aggiunta della configurazione, selezionare **[!UICONTROL Consegna]** nel campo **[!UICONTROL Livello]** della finestra di dialogo **[!UICONTROL Configura CDN]**.

   ![Configura CDN](/help/assets/assets/select-delivery-tier-in-configure-cdn-form.png)

   Dopo l&#39;aggiunta delle configurazioni, **[!UICONTROL STATUS]** di **[!UICONTROL Configurazioni CDN]** viene aggiornato a **[!UICONTROL Applicato]**.

   ![Configura stato distribuzione CDN](/help/assets/assets/cdn-configuration-deployment-status.png)

1. Fai clic su altre opzioni (![altre opzioni](/help/assets/assets/three-dots.svg)) e seleziona **[!UICONTROL Preparazione pubblicazione]** per visualizzare la finestra di dialogo **[!UICONTROL Preparazione pubblicazione]**.

   ![opzione di disponibilità pubblicazione](/help/assets/assets/go-live-readiness-option.png)

1. Eseguire i passaggi **[!UICONTROL Configura CNAME]** per mappare `cdn.adobeaemcloud.com` (record CNAME) nel record DNS del provider di servizi DNS. Questa mappatura assicura che le richieste ricevute al dominio personalizzato vengano reindirizzate al CDN di Adobe.

   ![finestra di dialogo di preparazione alla pubblicazione](/help/assets/assets/go-live-readiness-dialogbox.png){width="500" align="left"}

1. Fai clic su **[!UICONTROL Ok]**, il **[!UICONTROL STATO]** viene aggiornato a **[!UICONTROL Verificato]**. Il dominio personalizzato è pronto per l’utilizzo nell’URL di consegna.


   ![Configura CDN](/help/assets/assets/cdn-configurations-varified.png)



<!--
### Onboard API keys {#onboarding-api-keys}

Create an API key to access [!DNL Dynamic Media] with OpenAPIs and the delivery tier backed Asset Selector.

#### Prepare yourself for API keys onboarding process {#prerequisites-for-onboarding-api-keys} 

To start the API keys onboarding process, ensure you have:

1. [Access to Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Activated [!DNL Dynamic Media with OpenAPI] in your environment](#activate-dynamic-media-with-openapi).
1. [Access to the Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis#create-adobe-developer-console-adc-project).

#### Onboard the API keys using [!DNL AEM Dynamic Media] API card {#onboarding-api-keys-using-aem-dynamic-media-api-card}

Use the [Adobe Developer Console](https://developer.adobe.com/developer-console/) to onboard the API keys to:

1. [Access Dynamic Media APIs](#access-dynamic-media-apis)
1. [Access Delivery tier backed Asset Selector](#access-delivery-tier-backed-asset-selector)

#### Create an API key to access [!DNL Dynamic Media] with OpenAPIs {#access-dynamic-media-apis}

Execute the following steps to create an API key to access [!DNL Dynamic Media] with OpenAPIs:

1. Navigate to the **[!UICONTROL Admin Console]**. The Admin Console displays the **[!UICONTROL author]**, **[!UICONTROL delivery]** and **[!UICONTROL publish]** instances.
![instances on admin console](/help/assets/assets/delivery-instance-admin-console.png)
1. Select the **[!UICONTROL delivery]** instance to display the product profile with **[!UICONTROL AEM Dynamic Media enable API Services]** enabled by default. The product profile looks like this: **[!UICONTROL AEM Assets DM OpenAPI Users - delivery  - Program [ID Number] - Environment [ID Number]]**. 

   ![product profile on admin console](/help/assets/assets/admin-console-product-profile.png)

   >[!NOTE]
   >
   >This delivery instance is common for [!DNL Content Hub] and [!DNL Dynamic Media] with OpenAPI capabilities.

1. Navigate to the [Adobe Developer console](https://developer.adobe.com/console) and [create a new project](https://developer.adobe.com/dep/guides/dev-console/create-project/). See [Invoke OpenAPI-based AEM APIs for server to server authentication](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) to learn about creating a new project.
1. Select **[!UICONTROL AEM Dynamic Media API]** to access to the [!DNL Dynamic Media with OpenAPI capabilities] and click **[!UICONTROL Next]**.
![adobe developer console](/help/assets/assets/adobe-developer-console.png)
1. Select **[!UICONTROL Server-to-Server Authentication]** and click **[!UICONTROL Next]**. See [Server to Server authentication](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) to learn more about this authentication type.
![server-to-server-authentication](/help/assets/assets/server-to-server-authentication.png)
1. Select **[!UICONTROL OAuth Server-to-Server]**, specify a unique **[!UICONTROL Credential name]** and click **[!UICONTROL Next]**.
![oauth server to server credential](/help/assets/assets/oauth-server-server-and-credential-name.png)
1. Select your product profile (mentioned in step 2) to access the APIs using the environment's delivery endpoint and click **[!UICONTROL Save configured API]**.
![select product profile](/help/assets/assets/select-product-profile.png)
1. Select **[!UICONTROL AEM Dynamic Media API]**. Use the **[!UICONTROL OAuth Server-to-Server]** to fetch the **X-API-key** and access the token for the **authorization** header. 
![oauth server to server](/help/assets/assets/oauth-server-to-server-credentials.png)
Execute the below steps to use [Dynamic Media with OpenAPIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) using the **[!UICONTROL OAuth Server-to-Server]** credentials. 
    1. Copy the **[!UICONTROL API KEY (Client ID)]** and replace the `X-Api-Key` in the cURL.
    1. Click **[!UICONTROL Generate access token]** to generate an access token and replace `YOUR_JWT_HERE` with the token in the cURL.

The cURL looks like this:
```
headers: {
    'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    `},
```
See [Search Assets API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/search-assets-api#search-assets-api-header) for more information.

### Access Delivery tier backed Asset Selector {#access-delivery-tier-backed-asset-selector}

TBD: Wiki in progress..
-->

## Abilita Prime [!DNL Dynamic Media] {#enable-dynamic-media-prime}

Per abilitare [!DNL Dynamic Media] Prime:

1. [Attiva Dynamic Media con OpenAPI](#activate-dynamic-media-with-openapi)
1. [Facoltativo: configurare il dominio personalizzato nel livello di consegna](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the AEM Dynamic Media API card](#onboarding-api-keys)
-->
