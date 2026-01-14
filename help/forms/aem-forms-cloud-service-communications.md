---
title: Come si utilizza Forms as a Cloud Service per unire i dati con i modelli XDP e PDF o generare output in formati PCL, ZPL e PostScript?
description: Unisci automaticamente i dati ai modelli XDP e PDF o genera l’output nei formati PCL, ZPL e PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
feature: Adaptive Forms,APIs & Integrations
role: Admin, Developer, User
source-git-commit: 43b648eb3984867fda35ee04de10b78dd836b481
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 6%

---


# Usa elaborazione sincrona {#sync-processing-introduction}

Forms as a Cloud Service - API di comunicazione consente di creare, assemblare e distribuire comunicazioni personalizzate e orientate al brand, ad esempio corrispondenza aziendale, documenti, rendiconti, lettere per l’elaborazione delle richieste di rimborso, note sui benefit, lettere per l’elaborazione delle richieste, fatture mensili e kit di benvenuto. Puoi utilizzare le API di comunicazione per combinare un modello (XFA o PDF) con i dati del cliente per generare documenti in formati PDF, PS, PCL, DPL, IPL e ZPL.

Si consideri uno scenario in cui sono presenti uno o più modelli e più record di dati XML per ciascun modello. Puoi utilizzare le API di comunicazione per generare un documento di stampa per ciascun record. <!-- You can also combine the records into a single document. --> Il risultato è un documento PDF non interattivo. Un documento PDF non interattivo non consente agli utenti di immettere dati nei relativi campi.

Forms as a Cloud Service - Communications fornisce API on-demand e batch (API asincrone) per la generazione pianificata dei documenti:

* Le API sincrone sono adatte per casi di utilizzo su richiesta, a bassa latenza e per la generazione di documenti a record singolo. Queste API sono più adatte ai casi d’uso basati su azioni dell’utente. Ad esempio, la generazione di un documento dopo che un utente ha compilato un modulo.

* Le API in batch (API asincrone) sono adatte per casi di utilizzo pianificati di generazione di documenti con throughput elevato. Queste API generano documenti in batch. Ad esempio, bollette telefoniche, rendiconti per carta di credito e rendiconti dei benefit generati ogni mese.

## Utilizzare operazioni sincrone {#batch-operations}

Un&#39;operazione sincrona è un processo di generazione di documenti in modo lineare. Queste API sono classificate come API per tenant singolo e API per più tenant:

### API per singolo tenant

* API per la generazione di documenti
* API di manipolazione dei documenti

<!-- 
### Multi-tenant APIs

* Document utility APIs -->


### Autenticazione di un&#39;API a tenant singolo

Le operazioni API a tenant singolo supportano due tipi di autenticazione:

* **Autenticazione di base**: l&#39;autenticazione di base è uno schema di autenticazione semplice incorporato nel protocollo HTTP. Il client invia richieste HTTP con l&#39;intestazione Authorization che contiene la parola Basic seguita da uno spazio e da una stringa con codifica base64 nomeutente:password. Ad esempio, per autorizzare come amministratore/amministratore, il client invia una stringa con codifica Basic [base64 nome utente]: [password stringa con codifica base64].

* **Autenticazione basata su token:** L&#39;autenticazione basata su token utilizza un token di accesso (token di autenticazione Bearer) per effettuare richieste ad Experience Manager as a Cloud Service. AEM Forms as a Cloud Service fornisce API per recuperare in modo sicuro il token di accesso. Per recuperare e utilizzare il token per autenticare una richiesta:

   1. [Recupera le credenziali di Experience Manager as a Cloud Service da Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=it).
   1. [Installa le credenziali di Experience Manager as a Cloud Service nel tuo ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=it). (server applicazioni, server web o altri server non AEM) configurati per inviare richieste al servizio cloud (effettuare chiamate).
   1. [Generare un token JWT e scambiarlo con le API Adobe IMS per un token di accesso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=it).
   1. Esegui l’API Experience Manager con il token di accesso come token di autenticazione Bearer.
   1. [Imposta le autorizzazioni appropriate per l&#39;utente dell&#39;account tecnico nell&#39;ambiente Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=it#configure-access-in-aem).

  >[!NOTE]
  >
  >Adobe consiglia di utilizzare l’autenticazione basata su token in un ambiente di produzione.

  >[!IMPORTANT]
  >
  > Per ulteriori informazioni, vedere [Autenticazione server-to-server OAuth](/help/forms/oauth-api-authetication.md) e [Autenticazione server-to-server JWT](/help/forms/jwt-api-authentication.md).
<!-- 

### Authenticate a multi-tenant API

#### Authentication Headers

Every inbound HTTP API call to the multi-tenant API must contain these three headers:


* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

The values which should be sent in the `x-api-key` and `x-gw-ims-org-id` headers are provided in the Credentials details screen in the [Adobe Developer Console](https://developer.adobe.com/console). The value of the `x-api-key` header is the Client ID and the value for the `x-gw-ims-org-id` header is the Organization ID.

#### Configure Adobe Developer console to generate an access token

To set up authentication APIs, create a project in Adobe Developer Console and add Communication APIs to the project on Adobe Developer Console. The integration generates API Key, Client Secret, Payload (JWT):

1. Contact you Adobe Developer Console administrator. Ask the administrator to add as a developer.
1. Log in to `https://developer.adobe.com/console/`. Use your developer account that your administrator has provisioned to log in to Adobe Developer Console.
1. Select your organization from the top-right corner. If you do not know your organization, contact your administrator.
1. Select **[!UICONTROL Create new project]**. A screen to get started with your new project appears. Select **[!UICONTROL Add API]**. A screen with list of all the APIs enabled for your account appears.
1. Select **[!UICONTROL AEM Forms - Communications]** and select **[!UICONTROL Next]**. A screen to configure the API appears.
1. Select **[!UICONTROL OPTION 1 Generate a key pair]** and select **[!UICONTROL Generate keypair]**. It creates and downloads the configuration file. The downloaded configuration file contains all your app settings, along with the only copy of your private key. Adobe does not record your private key, make sure to securely store the downloaded file. Select **[!UICONTROL Next]**.
1. Select **[!UICONTROL Integrations - Cloud Service]** and select **[!UICONTROL Save configured API]**. Select **[!UICONTROL Service Account (JWT)]** to view the API Key, Client Secret, and other information required to access the APIs. You set to use the token to access the APIs.

#### Programmatically generate and use an access token

To programmatically generate an access token, generate a JSON Web Token (JWT) and exchange it with the Adobe Identity Management Service (IMS) for an access token.

Use the following keys, referred to as claims, to construct JWT JSON object:


* `exp`- the requested expiration of the access token, expressed as several seconds since January 1, 1970 GMT. For most use cases, this is a relatively small value. For example, 5 minutes, for five minutes from now, this value should be 1670923791.
* `iss` - the Organization ID from the Adobe Developer Console project, in the format org_ident@AdobeOrg.
* `sub` - the Technical Account ID from the Adobe Developer Console integration, in the format: id@techacct.adobe.com.
* `aud` - the Client ID from the Adobe Developer Console integration prepended with `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - set to the literal value `true`

This JSON object must be then base64 encoded and signed using the private key for the project. Finally, the encoded value is sent in the body of a POST request to `https://ims-na1.adobelogin.com/ims/exchange/jwt` along with the Client ID and Client Secret for the project.

##### Example

```JSON

    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache

```

#### Language Support for JWT

While it is possible to do the entire JWT generation and exchange process in custom code, it is more common to use a higher-level library to do so. A number of such libraries are listed on the [Adobe I/O JWT Documentation](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

-->

### Configurare risorse e autorizzazioni (solo per le API di generazione documenti)

Per utilizzare le API sincrone, è necessario quanto segue:

* Utenti con privilegi di amministratore Experience Manager
* Caricare modelli e altre risorse nell’istanza di Experience Manager Forms Cloud Service

### Carica modelli e altre risorse nell’istanza di Experience Manager (solo per le API di generazione documenti)

In genere, un’organizzazione dispone di più modelli. Ad esempio, un modello per gli estratti conto della carta di credito, gli estratti conto benefit e le richieste di rimborso. Carica tutti i modelli XDP e PDF nella tua istanza Experience Manager. Per caricare un modello:

1. Apri l’istanza di Experience Manager.
1. Passa a Forms > Forms e documenti
1. Fai clic su Crea > Cartella e crea una cartella. Apri la cartella.
1. Fai clic su Crea > Carica file e carica i modelli.

### Richiama un’API

La [documentazione di riferimento API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) fornisce informazioni dettagliate su tutti i parametri, i metodi di autenticazione e i vari servizi forniti dalle API. La documentazione di riferimento API fornisce anche un file di definizione API in formato .yaml. Puoi scaricare il file .yaml e caricarlo in [Postman](https://www.postman.com/) per verificare la funzionalità delle API.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
> Scopri i passaggi dettagliati per richiamare le API di comunicazione di AEM Forms. Consulta l&#39;articolo [Richiama le API di comunicazione di AEM Forms tramite l&#39;autenticazione server-to-server OAuth](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md).

>[!MORELIKETHIS]
>
>* [Introduzione ad AEM Forms as a Cloud Service Communications](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Architettura AEM Forms as a Cloud Service per API Forms adattivi e di comunicazione](/help/forms/aem-forms-cloud-service-architecture.md)
>* [Elaborazione comunicazione - API sincrone](/help/forms/aem-forms-cloud-service-communications.md)
>* [Elaborazione comunicazione - API batch](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [API Forms Communications - Tutorial](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)