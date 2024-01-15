---
title: Come si configurano le origini dati?
description: Scopri come configurare i servizi web RESTful, i servizi web basati su SOAP e i servizi OData come origini dati per un modello dati del modulo.
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 1%

---


# Configurare origini dati {#configure-data-sources}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/configure-data-sources.html) |
| AEM as a Cloud Service | Questo articolo |

![Integrazione dei dati](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] L’integrazione dei dati consente di configurare e connettersi a diverse origini dati. Sono supportati i seguenti tipi predefiniti:

* Database relazionali: MySQL, [!DNL Microsoft® SQL Server], [!DNL IBM® DB2®], postgreSQL e [!DNL Oracle RDBMS]
* Servizi Web RESTful
* Servizi web basati su SOAP
* Servizi OData (versione 4.0)
* Microsoft® Dynamics
* ForzaVendite
* Archiviazione BLOB di Microsoft® Azure

L’integrazione dei dati supporta OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), autenticazione di base e tipi di autenticazione con chiave API pronti all’uso e che consentono l’implementazione dell’autenticazione personalizzata per l’accesso ai servizi web. Mentre i servizi RESTful, SOAP e OData sono configurati in [!DNL Experience Manager] as a Cloud Service, JDBC per database relazionali e connettore per [!DNL Experience Manager] il profilo utente è configurato in [!DNL Experience Manager] console web.

## Configurare il database relazionale {#configure-relational-database}

### Prerequisiti

Prima di configurare i database relazionali utilizzando [!DNL Experience Manager] Configurazione della console Web, è obbligatorio:
* [Abilitare la rete avanzata tramite l’API di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html), in quanto le porte sono disattivate per impostazione predefinita.
* [Aggiungere dipendenze driver JDBC in Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies).


### Passaggi per configurare un database relazionale

È possibile configurare i database relazionali utilizzando [!DNL Experience Manager] Configurazione della console web. Effettua le seguenti operazioni:

1. Vai a [!DNL Experience Manager] console web in `https://server:host/system/console/configMgr`.
1. Individua **[!UICONTROL Pool connessioni JDBC Day Commons]** configurazione. Seleziona per aprire la configurazione in modalità di modifica.

   ![Pool di connettori JDBC](/help/forms/assets/jdbc_connector.png)

1. Nella finestra di dialogo di configurazione specificare i dettagli del database che si desidera configurare, ad esempio:

   * Nome classe Java™ per il driver JDBC
   * URI connessione JDBC
   * Nome utente e password per stabilire la connessione con il driver JDBC
   * Specificare una query SQL SELECT in **[!UICONTROL Query di convalida]** per convalidare le connessioni dal pool. La query deve restituire almeno una riga. In base al database, specificare una delle seguenti opzioni:
      * SELECT 1 (MySQL e MS® SQL)
      * SELECT 1 da dual (Oracle)
   * Nome dell’origine dati

   Stringhe di esempio per configurare un database relazionale:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > Consulta [Connessioni SQL con DataSourcePool JDBC](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html) per informazioni più dettagliate.

1. Seleziona **[!UICONTROL Salva]** per salvare la configurazione.

Ora è possibile utilizzare il database relazionale configurato con il modello dati del modulo.

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and select to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties are available for use in form data model. Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Select **[!UICONTROL Save]** to save the configuration. -->

## Configurare la cartella per le configurazioni del servizio cloud {#cloud-folder}

Per configurare i servizi cloud per i servizi RESTful, SOAP e OData è necessaria la configurazione della cartella Servizi cloud.

Tutte le configurazioni del servizio cloud in [!DNL Experience Manager] sono consolidati in `/conf` cartella in [!DNL Experience Manager] archivio. Per impostazione predefinita, il `conf` la cartella contiene `global` cartella in cui è possibile creare le configurazioni di cloud service. Tuttavia, devi abilitarlo manualmente per le configurazioni cloud. Puoi anche creare ulteriori cartelle in `conf` per creare e organizzare le configurazioni di cloud service.

Per configurare la cartella per le configurazioni del servizio cloud:

1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   * Consulta la [Browser configurazioni](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) per ulteriori informazioni.
1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud oppure ignora questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

   1. In **[!UICONTROL Browser configurazioni]**, seleziona la `global` cartella e seleziona **[!UICONTROL Proprietà]**.

   1. In **[!UICONTROL Proprietà di configurazione]** finestra di dialogo, abilita **[!UICONTROL Configurazioni cloud]**.

   1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. In **[!UICONTROL Browser configurazioni]**, seleziona **[!UICONTROL Crea]**.
1. In **[!UICONTROL Crea configurazione]** , specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
1. Seleziona **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

## Configurare i servizi web RESTful {#configure-restful-web-services}

I servizi web RESTful possono essere descritti utilizzando [Specifiche Swagger](https://swagger.io/specification/v2/) in formato JSON o YAML in un [!DNL Swagger] file di definizione. Per configurare il servizio Web RESTful in [!DNL Experience Manager] as a Cloud Service, assicurati di disporre di [!DNL Swagger] file ([Swagger versione 2.0](https://swagger.io/specification/v2/)) o [!DNL Swagger] file ([Swagger versione 3.0](https://swagger.io/specification/v3/)) nel file system o nell&#39;URL in cui è ospitato il file.

### Configurazione dei servizi RESTful per la specifica API Open versione 2.0 {#configure-restful-services-open-api-2.0}

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Consulta [Configurare la cartella per le configurazioni del servizio cloud](configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni di cloud service.

1. Seleziona **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome e, facoltativamente, un titolo per la configurazione, quindi seleziona **[!UICONTROL Servizio RESTful]** dal **[!UICONTROL Tipo di servizio]** , sfogliare e selezionare un&#39;immagine di miniatura per la configurazione e selezionare **[!UICONTROL Successivo]**.
1. Specificare i dettagli seguenti per il servizio RESTful:

   * Seleziona un URL o un file da [!UICONTROL Sorgente Swagger] e quindi specificare il [!DNL Swagger URL] al[!DNL  Swagger] file di definizione o carica [!DNL Swagger] dal file system locale.
   * In base al[!DNL  Swagger] Input sorgente., i seguenti campi sono precompilati con i valori:

      * Schema: protocolli di trasferimento utilizzati dall’API REST. Il numero di tipi di schema visualizzati nell&#39;elenco a discesa dipende dagli schemi definiti nella [!DNL Swagger] sorgente.
      * Host: il nome di dominio o l’indirizzo IP dell’host che serve l’API REST. È un campo obbligatorio.
      * Percorso base: prefisso URL per tutti i percorsi API. È un campo facoltativo.\
        Se necessario, modifica i valori precompilati per questi campi.

   * Seleziona il tipo di autenticazione: Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), autenticazione di base, chiave API o autenticazione personalizzata: per accedere al servizio RESTful e fornire di conseguenza i dettagli per l’autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specifica il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una di queste opzioni dalla **[!UICONTROL Posizione]** e specificare il nome dell&#39;intestazione o il parametro di query nell&#39; **[!UICONTROL Nome parametro]** di conseguenza.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

### Configurare i servizi RESTful per la versione 3.0 delle specifiche API aperte {#configure-restful-services-open-api-3.0}

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Consulta [Configurare la cartella per le configurazioni del servizio cloud](configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni di cloud service.

1. Seleziona **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome e, facoltativamente, un titolo per la configurazione, quindi seleziona **[!UICONTROL Servizio RESTful]** dal **[!UICONTROL Tipo di servizio]** , sfogliare e selezionare un&#39;immagine di miniatura per la configurazione e selezionare **[!UICONTROL Successivo]**.
1. Specificare i dettagli seguenti per il servizio RESTful:

   * Seleziona un URL o un file da [!UICONTROL Sorgente Swagger] e quindi specificare il [!DNL Swagger 3.0 URL] al[!DNL  Swagger] file di definizione o carica [!DNL Swagger] dal file system locale.
   * In base al[!DNL  Swagger] Input di origine, vengono visualizzate le informazioni di connessione con il server di destinazione.
   * Seleziona il tipo di autenticazione: Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), autenticazione di base, chiave API o autenticazione personalizzata: per accedere al servizio RESTful e fornire di conseguenza i dettagli per l’autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specifica il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una di queste opzioni dalla **[!UICONTROL Posizione]** e specificare il nome dell&#39;intestazione o il parametro di query nell&#39; **[!UICONTROL Nome parametro]** di conseguenza.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

Alcune delle operazioni non supportate dalla versione 3.0 della specifica Open API dei servizi RESTful sono:
* Callback
* uno di/qualsiasi di
* Riferimento remoto
* Collegamenti
* Diversi corpi di richiesta per diversi tipi MIME per una singola operazione

Consulta [Specifiche OpenAPI 3.0](https://swagger.io/specification/v3/) per informazioni dettagliate.

### Configurazione client HTTP del modello dati modulo per ottimizzare le prestazioni {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] formare un modello dati durante l’integrazione con i servizi web RESTful come origine dati include configurazioni client HTTP per l’ottimizzazione delle prestazioni.

Imposta le seguenti proprietà del **[!UICONTROL Configurazione client HTTP modello dati modulo per origine dati REST]** per specificare l&#39;espressione regolare:

* Utilizza il `http.connection.max.per.route` per impostare il numero massimo di connessioni consentite tra il modello di dati del modulo e i servizi web RESTful. Il valore predefinito è 20 connessioni.

* Utilizza il `http.connection.max` per specificare il numero massimo di connessioni consentite per ogni route. Il valore predefinito è 40 connessioni.

* Utilizza il `http.connection.keep.alive.duration` per specificare la durata per la quale una connessione HTTP persistente viene mantenuta attiva. Il valore predefinito è 15 secondi.

* Utilizza il `http.connection.timeout` per specificare la durata, per la quale [!DNL Experience Manager Forms] il server attende una connessione da stabilire. Il valore predefinito è 10 secondi.

* Utilizza il `http.socket.timeout` per specificare il periodo massimo di inattività tra due pacchetti di dati. Il valore predefinito è 30 secondi.

Il seguente file JSON mostra un esempio:


```json
{   
   "http.connection.keep.alive.duration":"15",   
   "http.connection.max.per.route":"20",   
   "http.connection.timeout":"10",   
   "http.socket.timeout":"30",   
   "http.connection.idle.connection.timeout":"15",   
   "http.connection.max":"40" 
} 
```

1. Seleziona **[!UICONTROL Configurazione client HTTP modello dati modulo per origine dati REST]**.

1. In [!UICONTROL Configurazione client HTTP modello dati modulo per origine dati REST] finestra di dialogo:

   * Specifica il numero massimo di connessioni consentite tra il modello di dati del modulo e i servizi web RESTful nel **[!UICONTROL Limite di connessioni in totale]** campo. Il valore predefinito è 20 connessioni.

   * Specificare il numero massimo di connessioni consentite per ogni route nella **[!UICONTROL Limite di connessione per ciclo di lavorazione]** campo. Il valore predefinito è due connessioni.

   * Specifica la durata per la quale una connessione HTTP persistente viene mantenuta attiva nel **[!UICONTROL Mantieni vivo]** campo. Il valore predefinito è 15 secondi.

   * Specifica la durata, per la quale [!DNL Experience Manager Forms] il server attende che venga stabilita una connessione, nel **[!UICONTROL Timeout della connessione]** campo. Il valore predefinito è 10 secondi.

   * Specifica il periodo massimo di inattività tra due pacchetti di dati nella **[!UICONTROL Timeout socket]** campo. Il valore predefinito è 30 secondi.

## Configurare i servizi web SOAP {#configure-soap-web-services}

I servizi web basati su SOAP sono descritti utilizzando [Specifiche di Web Services Description Language (WSDL)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] non supportano il modello WSDL di tipo RPC.

Per configurare il servizio Web basato su SOAP in [!DNL Experience Manager] as a Cloud Service, assicurati di disporre dell’URL WSDL per il servizio Web e procedi come segue:

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Consulta [Configurare la cartella per le configurazioni del servizio cloud](configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni di cloud service.

1. Seleziona **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome e, facoltativamente, un titolo per la configurazione, quindi seleziona **[!UICONTROL Servizio web SOAP]** dal **[!UICONTROL Tipo di servizio]** , sfogliare e selezionare un&#39;immagine di miniatura per la configurazione e selezionare **[!UICONTROL Successivo]**.
1. Specificare quanto segue per il servizio Web SOAP:

   * URL WSDL per il servizio Web.
   * Endpoint servizio. Specificare un valore in questo campo per sostituire l&#39;endpoint del servizio indicato in WSDL.
   * Seleziona il tipo di autenticazione: Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), autenticazione di base o autenticazione personalizzata: per accedere al servizio SOAP e fornire i dettagli per l&#39;autenticazione.

     <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
     <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

     <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio web SOAP.

### Abilitare l&#39;utilizzo delle istruzioni di importazione nel WSDL dei servizi Web SOAP {#enable-import-statements}

È possibile specificare un&#39;espressione regolare che funga da filtro per gli URL assoluti consentiti come istruzioni di importazione nel WSDL dei servizi Web SOAP. Per impostazione predefinita, in questo campo non è presente alcun valore. Di conseguenza, [!DNL Experience Manager] blocca tutte le istruzioni di importazione disponibili in WSDL. Se si specifica `.*` come valore in questo campo, [!DNL Experience Manager] consente tutte le istruzioni di importazione.

Imposta il `importAllowlistPattern` proprietà del **[!UICONTROL Modello dati modulo SOAP Web Services Importa Inserisco nell&#39;elenco Consentiti]** per specificare l&#39;espressione regolare. Il seguente file JSON mostra un esempio:

```json
{
  "importAllowlistPattern": ".*"
}
```

Per impostare i valori di una configurazione: [Generare configurazioni OSGi utilizzando l’SDK per AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart), e [distribuire la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) all’istanza di Cloud Service.

## Configurare i servizi OData {#config-odata}

Un servizio OData è identificato dall&#39;URL radice del servizio. Per configurare un servizio OData in [!DNL Experience Manager] as a Cloud Service, assicurati di disporre dell’URL principale del servizio ed effettua le seguenti operazioni:

>[!NOTE]
>
> Il modello dati del modulo supporta [OData versione 4](https://www.odata.org/documentation/).
>Per una guida dettagliata alla configurazione di [!DNL Microsoft®® Dynamics 365], online o on-premise, vedi [[!DNL Microsoft® Dynamics] Configurazione OData](ms-dynamics-odata-configuration.md).

1. Vai a **[!UICONTROL Strumenti > Cloud Service > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Consulta [Configurare la cartella per le configurazioni del servizio cloud](#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni di cloud service.

1. Seleziona **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome e, facoltativamente, un titolo per la configurazione, quindi seleziona **[!UICONTROL Servizio OData]** dal **[!UICONTROL Tipo di servizio]** , sfogliare e selezionare un&#39;immagine di miniatura per la configurazione e selezionare **[!UICONTROL Successivo]**.
1. Specificare i dettagli seguenti per il servizio OData:

   * URL principale del servizio per il servizio OData da configurare.
   * Seleziona il tipo di autenticazione: Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), autenticazione di base, chiave API o autenticazione personalizzata: per accedere al servizio OData e fornire di conseguenza i dettagli per l&#39;autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specifica il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una di queste opzioni dalla **[!UICONTROL Posizione]** e specificare il nome dell&#39;intestazione o il parametro di query nell&#39; **[!UICONTROL Nome parametro]** di conseguenza.

   >[!NOTE]
   >
   Seleziona il tipo di autenticazione OAuth 2.0 con cui connetterti [!DNL Microsoft®® Dynamics] servizi che utilizzano l&#39;endpoint OData come radice del servizio.

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio OData.

<!--
## Configure Microsoft® SharePoint List {#config-sharepoint-list}

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

To save data in a tabular form use, Microsoft® SharePoint List. To configure a Microsoft SharePoint List in [!DNL Experience Manager] as a Cloud Service, do the following:

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.   
1. Select a **Configuration Container**. The configuration is stored in the selected Configuration Container. 
1. Click **[!UICONTROL Create]** > **[!UICONTROL SharePoint List]** from the drop-down list. The SharePoint configuration wizard appears.  
1. Specify the **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** and **[!UICONTROL OAuth URL]**. For information on how to retrieve Client ID, Client Secret, Tenant ID for OAuth URL, see [Microsoft&reg; Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
    * You can retrieve the `Client ID` and `Client Secret` of your app from the Microsoft&reg; Azure portal.
    * In the Microsoft&reg; Azure portal, add the Redirect URI as `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Replace `[author-instance]` with the URL of your Author instance.
    * Add the API permissions `offline_access` and `Sites.Manage.All` in the **Microsoft® Graph** tab to provide read/write permissions. Add `AllSites.Manage` permission in the **Sharepoint** tab to interact remotely with SharePoint data.
    * Use OAuth URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` with the `tenant-id` of your app from the Microsoft&reg; Azure portal.

      >[!NOTE]
      >
      > The **client secret** field is mandatory or optional depends upon your Azure Active Directory application configuration. If your application is configured to use a client secret, it is mandatory to provide the client secret.

1. Click **[!UICONTROL Connect]**. On a successful connection, the `Connection Successful` message appears.
1. Select **[!UICONTROL SharePoint Site]** and **[!UICONTROL SharePoint List]** from the drop-down list.
1. Select **[!UICONTROL Create]** to create the cloud configuration for the Microsoft® SharePointList.

-->

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and select **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and select **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, select **[!UICONTROL Select Certificate File]**, upload the certificate, and select **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Passaggi successivi {#next-steps}

Hai configurato le origini dati. Successivamente è possibile creare un modello dati modulo oppure, se è già stato creato un modello dati modulo senza un&#39;origine dati, è possibile associarlo alle origini dati configurate. Consulta [Crea modello dati modulo](create-form-data-models.md) per i dettagli.


<!--

>[!MORELIKETHIS]
>
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>*  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->