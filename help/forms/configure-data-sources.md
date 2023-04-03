---
title: Come si configurano le origini dati?
description: L'integrazione dei dati di Experience Manager Forms consente di configurare e connettersi a diverse origini dati. Scopri come configurare i servizi web RESTful, i servizi web basati su SOAP e i servizi OData come origini dati e utilizzarli per creare modelli di dati per i moduli.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: 936aa33ca334523aa84300f540bde9543eb7ffb4
workflow-type: tm+mt
source-wordcount: '2135'
ht-degree: 0%

---

# Configurare origini dati {#configure-data-sources}

![Integrazione dei dati](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] L&#39;integrazione dei dati consente di configurare e connettersi a diverse origini dati. I seguenti tipi sono supportati come predefiniti:

* Database relazionali - MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2]e [!DNL Oracle RDBMS]
* Servizi web RESTful
* Servizi web basati su SOAP
* Servizi OData (versione 4.0)
* Microsoft® Dynamics
* ForzaVendita
* Archiviazione BLOB di Microsoft® Azure

L’integrazione dei dati supporta i tipi di autenticazione predefiniti OAuth2.0, autenticazione di base e API Key e consente l’implementazione dell’autenticazione personalizzata per l’accesso ai servizi web. Mentre i servizi RESTful, basati su SOAP e OData sono configurati in [!DNL Experience Manager] as a Cloud Service, JDBC per database relazionali e connettore per [!DNL Experience Manager] il profilo utente è configurato in [!DNL Experience Manager] console web.

## Configurare il database relazionale {#configure-relational-database}

### Prerequisiti

Prima di configurare i database relazionali utilizzando [!DNL Experience Manager] Configurazione della console Web, obbligatoria per:
* [Abilitare le reti avanzate tramite l’API di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html), poiché le porte sono disattivate per impostazione predefinita.
* [Aggiungere dipendenze del driver JDBC in Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies).


### Passaggi per configurare il database relazionale

È possibile configurare database relazionali utilizzando [!DNL Experience Manager] Configurazione della console Web. Effettua le seguenti operazioni:

1. Vai a [!DNL Experience Manager] console web all’indirizzo `https://server:host/system/console/configMgr`.
1. Individua **[!UICONTROL Pool di connessioni JDBC Day Commons]** configurazione. Tocca per aprire la configurazione in modalità di modifica.

   ![Pool di connettori JDBC](/help/forms/assets/jdbc_connector.png)

1. Nella finestra di dialogo di configurazione, specifica i dettagli del database da configurare, ad esempio:

   * Nome classe Java™ per il driver JDBC
   * URI di connessione JDBC
   * Nome utente e password per stabilire la connessione con il driver JDBC
   * Specificare una query SQL SELECT nel **[!UICONTROL Query di convalida]** campo per convalidare le connessioni dal pool. La query deve restituire almeno una riga. In base al database, specifica una delle seguenti opzioni:
      * SELECT 1 (MySQL e MS SQL)
      * SELECT 1 from dual (Oracle)
   * Nome dell’origine dati

   Stringhe di esempio per la configurazione del database relazionale:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > Fai riferimento a [Connessioni SQL con JDBC DataSourcePool](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html) per informazioni più dettagliate.

1. Tocca **[!UICONTROL Salva]** per salvare la configurazione.

Ora è possibile utilizzare il database relazionale configurato con il modello dati del modulo.

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties will be available for use in form data model. Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Tap **[!UICONTROL Save]** to save the configuration. -->

## Configurare la cartella per le configurazioni del servizio cloud {#cloud-folder}

La configurazione della cartella dei servizi cloud è necessaria per configurare i servizi cloud per i servizi RESTful, SOAP e OData.

Tutte le configurazioni del servizio cloud in [!DNL Experience Manager] sono consolidate nelle `/conf` cartella in [!DNL Experience Manager] archivio. Per impostazione predefinita, la `conf` la cartella contiene `global` in cui puoi creare configurazioni di servizi cloud. Tuttavia, devi abilitarlo manualmente per le configurazioni cloud. Puoi anche creare cartelle aggiuntive in `conf` per creare e organizzare configurazioni di servizi cloud.

Per configurare la cartella per le configurazioni del servizio cloud:

1. Vai a **[!UICONTROL Strumenti > Generale > Browser di configurazione]**.
   * Consulta la sezione [Browser di configurazione](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) documentazione per ulteriori informazioni.
1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud o salta questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

   1. In **[!UICONTROL Browser di configurazione]**, seleziona `global` tocca e fai clic su **[!UICONTROL Proprietà]**.

   1. In **[!UICONTROL Proprietà di configurazione]** finestra di dialogo, attiva **[!UICONTROL Configurazioni cloud]**.

   1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. In **[!UICONTROL Browser di configurazione]**, tocca **[!UICONTROL Crea]**.
1. In **[!UICONTROL Crea configurazione]** , specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
1. Tocca **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

## Configurare i servizi web RESTful {#configure-restful-web-services}

Il servizio Web RESTful può essere descritto utilizzando [Specifiche Swagger](https://swagger.io/specification/v2/) in formato JSON o YAML in un [!DNL Swagger] file di definizione. Per configurare il servizio Web RESTful in [!DNL Experience Manager] as a Cloud Service, assicurati di avere [!DNL Swagger] file ([Swagger versione 2.0](https://swagger.io/specification/v2/)) o [!DNL Swagger] file ([Swagger versione 3.0](https://swagger.io/specification/v3/)) nel file system o nell&#39;URL in cui è ospitato il file.

### Configurare i servizi RESTful per Open API Specification versione 2.0 {#configure-restful-services-open-api-2.0}

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Vedi [Configurare la cartella per le configurazioni del servizio cloud](configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud.

1. Tocca **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome ed eventualmente un titolo per la configurazione, seleziona **[!UICONTROL Servizio RESTful]** dal **[!UICONTROL Tipo di servizio]** a discesa, se lo desideri, sfoglia e seleziona un’immagine in miniatura per la configurazione, quindi tocca **[!UICONTROL Successivo]**.
1. Specifica i seguenti dettagli per il servizio RESTful:

   * Seleziona URL o File dal [!UICONTROL Sorgente Swagger] e quindi specifica il [!DNL Swagger URL] al[!DNL  Swagger] file di definizione o carica il [!DNL Swagger] dal file system locale.
   * In base ai[!DNL  Swagger] Input origine. I seguenti campi sono precompilati con valori:

      * Schema: I protocolli di trasferimento utilizzati dall’API REST. Il numero di tipi di schemi visualizzati nell&#39;elenco a discesa dipende dagli schemi definiti nella [!DNL Swagger] sorgente.
      * Host: Il nome di dominio o l’indirizzo IP dell’host che serve l’API REST. È un campo obbligatorio.
      * Percorso di base: Prefisso URL per tutti i percorsi API. È un campo facoltativo.\
         Se necessario, modifica i valori precompilati per questi campi.
   * Seleziona il tipo di autenticazione — Nessuno, OAuth2.0, Autenticazione di base, Chiave API o Autenticazione personalizzata — per accedere al servizio RESTful e, di conseguenza, fornisci i dettagli per l’autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specifica il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una delle seguenti opzioni dal menu **[!UICONTROL Posizione]** elenco a discesa e specifica il nome dell’intestazione o il parametro della query nel **[!UICONTROL Nome parametro]** di conseguenza.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Tocca **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

### Configurare i servizi RESTful per Open API Specification versione 3.0 {#configure-restful-services-open-api-3.0}

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Vedi [Configurare la cartella per le configurazioni del servizio cloud](configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud.

1. Tocca **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome ed eventualmente un titolo per la configurazione, seleziona **[!UICONTROL Servizio RESTful]** dal **[!UICONTROL Tipo di servizio]** a discesa, se lo desideri, sfoglia e seleziona un’immagine in miniatura per la configurazione, quindi tocca **[!UICONTROL Successivo]**.
1. Specifica i seguenti dettagli per il servizio RESTful:

   * Seleziona URL o File dal [!UICONTROL Sorgente Swagger] e quindi specifica il [!DNL Swagger 3.0 URL] al[!DNL  Swagger] file di definizione o carica il [!DNL Swagger] dal file system locale.
   * In base ai[!DNL  Swagger] Input origine, vengono visualizzate le informazioni di connessione con il server di destinazione.
   * Seleziona il tipo di autenticazione — Nessuno, OAuth2.0, Autenticazione di base, Chiave API o Autenticazione personalizzata — per accedere al servizio RESTful e, di conseguenza, fornisci i dettagli per l’autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specifica il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una delle seguenti opzioni dal menu **[!UICONTROL Posizione]** elenco a discesa e specifica il nome dell’intestazione o il parametro della query nel **[!UICONTROL Nome parametro]** di conseguenza.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Tocca **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

Alcune delle operazioni non supportate da RESTful services Open API Specification versione 3.0 sono:
* Callback
* oneof/anyof
* Riferimento remoto
* Collegamenti
* Diversi corpi di richiesta per diversi tipi MIME per una singola operazione

Puoi fare riferimento a [Specifiche OpenAPI 3.0](https://swagger.io/specification/v3/) per informazioni dettagliate.

### Configurazione del client HTTP del modello dati modulo per ottimizzare le prestazioni {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] modello di dati modulo durante l’integrazione con i servizi web RESTful come origine dati include configurazioni client HTTP per l’ottimizzazione delle prestazioni.

Imposta le seguenti proprietà del **[!UICONTROL Configurazione client HTTP del modello dati modulo per l’origine dati REST]** configurazione per specificare l’espressione regolare:

* Utilizza la `http.connection.max.per.route` per impostare il numero massimo di connessioni consentite tra il modello dati del modulo e i servizi Web RESTful. Il valore predefinito è 20 connessioni.

* Utilizza la `http.connection.max` proprietà per specificare il numero massimo di connessioni consentite per ogni route. Il valore predefinito è 40 connessioni.

* Utilizza la `http.connection.keep.alive.duration` proprietà per specificare la durata per la quale viene mantenuta una connessione HTTP persistente. Il valore predefinito è 15 secondi.

* Utilizza la `http.connection.timeout` per specificare la durata per la quale la proprietà [!DNL Experience Manager Forms] il server attende una connessione da stabilire. Il valore predefinito è 10 secondi.

* Utilizza la `http.socket.timeout` per specificare il periodo di tempo massimo per l&#39;inattività tra due pacchetti di dati. Il valore predefinito è 30 secondi.

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

1. Tocca **[!UICONTROL Configurazione client HTTP del modello dati modulo per l’origine dati REST]**.

1. In [!UICONTROL Configurazione client HTTP del modello dati modulo per l’origine dati REST] finestra di dialogo:

   * Specificare il numero massimo di connessioni consentite tra il modello dati del modulo e i servizi web RESTful nella **[!UICONTROL Limite di connessione totale]** campo . Il valore predefinito è 20 connessioni.

   * Specificare il numero massimo di connessioni consentite per ogni route nella **[!UICONTROL Limite di connessione per rotta]** campo . Il valore predefinito è due connessioni.

   * Specifica la durata, per la quale una connessione HTTP persistente viene mantenuta in vita, nel **[!UICONTROL Mantieni vivo]** campo . Il valore predefinito è 15 secondi.

   * Specifica la durata per la quale il [!DNL Experience Manager Forms] il server attende una connessione da stabilire, nel **[!UICONTROL Timeout connessione]** campo . Il valore predefinito è 10 secondi.

   * Specifica il periodo di tempo massimo per l&#39;inattività tra due pacchetti di dati nel **[!UICONTROL Timeout del socket]** campo . Il valore predefinito è 30 secondi.

## Configurare i servizi Web SOAP {#configure-soap-web-services}

I servizi web basati su SOAP sono descritti utilizzando [Specifiche WSDL (Web Services Description Language)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] non supportano il modello WSDL di stile RPC.

Per configurare il servizio Web basato su SOAP in [!DNL Experience Manager] as a Cloud Service, assicurati di disporre dell’URL WSDL per il servizio Web ed effettua le seguenti operazioni:

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Vedi [Configurare la cartella per le configurazioni del servizio cloud](configure-data-sources.md#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud.

1. Tocca **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome ed eventualmente un titolo per la configurazione, seleziona **[!UICONTROL Servizio Web SOAP]** dal **[!UICONTROL Tipo di servizio]** a discesa, se lo desideri, sfoglia e seleziona un’immagine in miniatura per la configurazione, quindi tocca **[!UICONTROL Successivo]**.
1. Specifica quanto segue per il servizio Web SOAP:

   * URL WSDL per il servizio Web.
   * Endpoint servizio. Specificare un valore in questo campo per sostituire l&#39;endpoint del servizio menzionato in WSDL.
   * Selezionare il tipo di autenticazione, Nessuno, OAuth2.0, Autenticazione di base o Autenticazione personalizzata, per accedere al servizio SOAP e, di conseguenza, fornire i dettagli per l’autenticazione.

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Tocca **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio Web SOAP.

### Abilitare l’utilizzo di istruzioni di importazione in WSDL dei servizi Web SOAP {#enable-import-statements}

È possibile specificare un’espressione regolare che funga da filtro per gli URL assoluti consentiti come istruzioni di importazione in WSDL dei servizi Web SOAP. Per impostazione predefinita, questo campo non contiene alcun valore. Di conseguenza, [!DNL Experience Manager] blocca tutte le istruzioni di importazione disponibili in WSDL. Se si specifica `.*` come valore in questo campo, [!DNL Experience Manager] consente tutte le istruzioni di importazione.

Imposta la `importAllowlistPattern` proprietà **[!UICONTROL Inserire nell&#39;elenco Consentiti di importazione servizi Web SOAP del modello per dati modulo]** configurazione per specificare l’espressione regolare. Il seguente file JSON mostra un esempio:


```json
{
  "importAllowlistPattern": ".*"
}
```


Per impostare i valori di una configurazione, [Generare configurazioni OSGi utilizzando l’SDK AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)e [distribuire la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) all&#39;istanza di Cloud Service.

## Configurare i servizi OData {#config-odata}

Un servizio OData è identificato dall&#39;URL principale del servizio. Per configurare un servizio OData in [!DNL Experience Manager] as a Cloud Service, accertati di disporre dell&#39;URL principale del servizio ed effettua le seguenti operazioni:

>[!NOTE]
>
> Il modello dati del modulo supporta [OData versione 4](https://www.odata.org/documentation/).
>Guida dettagliata alla configurazione [!DNL Microsoft® Dynamics 365], on-line o on-premise, vedi [[!DNL Microsoft® Dynamics] Configurazione OData](ms-dynamics-odata-configuration.md).

1. Vai a **[!UICONTROL Strumenti > Cloud Services > Origini dati]**. Tocca per selezionare la cartella in cui desideri creare una configurazione cloud.

   Vedi [Configurare la cartella per le configurazioni del servizio cloud](#cloud-folder) per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud.

1. Tocca **[!UICONTROL Crea]** per aprire **[!UICONTROL Creazione guidata configurazione origine dati]**. Specifica un nome ed eventualmente un titolo per la configurazione, seleziona **[!UICONTROL Servizio OData]** dal **[!UICONTROL Tipo di servizio]** a discesa, se lo desideri, sfoglia e seleziona un’immagine in miniatura per la configurazione, quindi tocca **[!UICONTROL Successivo]**.
1. Specifica i seguenti dettagli per il servizio OData:

   * URL principale del servizio per il servizio OData da configurare.
   * Seleziona il tipo di autenticazione — Nessuno, OAuth2.0, Autenticazione di base, Chiave API o Autenticazione personalizzata — per accedere al servizio OData e, di conseguenza, fornisci i dettagli per l’autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specifica il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una delle seguenti opzioni dal menu **[!UICONTROL Posizione]** elenco a discesa e specifica il nome dell’intestazione o il parametro della query nel **[!UICONTROL Nome parametro]** di conseguenza.

   >[!NOTE]
   È necessario selezionare il tipo di autenticazione OAuth 2.0 con cui connettersi [!DNL Microsoft® Dynamics] servizi che utilizzano l&#39;endpoint OData come radice del servizio.

1. Tocca **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio OData.

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Passaggi successivi {#next-steps}

Hai configurato le origini dati. Successivamente è possibile creare un modello dati modulo oppure, se è già stato creato un modello dati modulo senza un’origine dati, è possibile associarlo alle origini dati configurate. Vedi [Crea modello dati modulo](create-form-data-models.md) per i dettagli.
