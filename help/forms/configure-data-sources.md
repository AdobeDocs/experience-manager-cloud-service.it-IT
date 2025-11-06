---
title: Come si configurano le origini dati?
description: Scopri come configurare i servizi web RESTful, i servizi web basati su SOAP e i servizi OData come origini dati per un modello dati modulo (FDM).
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 4%

---


# Configurare origini dati {#configure-data-sources}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/configure-data-sources.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

![Integrazione dei dati](do-not-localize/data-integeration.png)

L&#39;integrazione dei dati di [!DNL Experience Manager Forms] consente di configurare e connettersi a diverse origini dati. Sono supportati i seguenti tipi predefiniti:

* Database relazionali: MySQL, [!DNL Microsoft® SQL Server], [!DNL IBM® DB2®], postgreSQL e [!DNL Oracle RDBMS]
* Servizi Web RESTful
* Servizi Web basati su SOAP
* Servizi OData (versione 4.0)
* Microsoft® Dynamics
* Salesforce
* Archiviazione BLOB di Microsoft® Azure

L&#39;integrazione dei dati supporta OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), l&#39;autenticazione di base e i tipi di autenticazione con chiave API predefiniti e consente l&#39;implementazione dell&#39;autenticazione personalizzata per l&#39;accesso ai servizi Web. Mentre i servizi RESTful, basati su SOAP e OData sono configurati in [!DNL Experience Manager] as a Cloud Service, JDBC per i database relazionali e il connettore per il profilo utente [!DNL Experience Manager] sono configurati nella console Web [!DNL Experience Manager].

## Configurare il database relazionale {#configure-relational-database}

### Prerequisiti

Prima di configurare i database relazionali utilizzando la configurazione della console Web [!DNL Experience Manager], è necessario:

* [Abilita la rete avanzata tramite l&#39;API di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=it), in quanto le porte sono disabilitate per impostazione predefinita.
* [Aggiungi dipendenze driver JDBC in Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=it#mysql-driver-dependencies).


### Passaggi per configurare un database relazionale

È possibile configurare i database relazionali utilizzando la configurazione della console Web [!DNL Experience Manager]. Effettua le seguenti operazioni:

1. Vai alla console Web [!DNL Experience Manager] in `https://server:host/system/console/configMgr`.
1. Individuare la configurazione **[!UICONTROL dei pool di connessioni JDBC Day Commons]**. Seleziona per aprire la configurazione in modalità di modifica.

   ![Pool di connettori JDBC](/help/forms/assets/jdbc_connector.png)

1. Nella finestra di dialogo di configurazione specificare i dettagli del database che si desidera configurare, ad esempio:

   * Nome classe Java™ per il driver JDBC
   * URI connessione JDBC
   * Nome utente e password per stabilire la connessione con il driver JDBC
   * Specificare una query SQL SELECT nel campo **[!UICONTROL Query di convalida]** per convalidare le connessioni dal pool. La query deve restituire almeno una riga. In base al database, specificare una delle seguenti opzioni:
      * SELECT 1 (MySQL e MS® SQL)
      * SELECT 1 from dual (Oracle) (Seleziona 1 da doppio)
   * Nome dell’origine dati

   Stringhe di esempio per configurare un database relazionale:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > Per informazioni più dettagliate, vedere [Connessioni SQL con DataSourcePool JDBC](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=it).

1. Seleziona **[!UICONTROL Salva]** per salvare la configurazione.

Ora è possibile utilizzare il database relazionale configurato con il modello dati del modulo (FDM).

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and select to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties are available for use in form data model (FDM). Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model (FDM) can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Select **[!UICONTROL Save]** to save the configuration. -->

## Configurare la cartella per le configurazioni del servizio cloud {#cloud-folder}

Per configurare i servizi cloud per i servizi RESTful, SOAP e OData è necessaria la configurazione della cartella Servizi cloud.

Tutte le configurazioni del servizio cloud in [!DNL Experience Manager] sono consolidate nella cartella `/conf` nell&#39;archivio [!DNL Experience Manager]. Per impostazione predefinita, la cartella `conf` contiene la cartella `global` in cui è possibile creare configurazioni del servizio cloud. Tuttavia, devi abilitarlo manualmente per le configurazioni cloud. È inoltre possibile creare cartelle aggiuntive in `conf` per creare e organizzare le configurazioni del servizio cloud.

Per configurare la cartella per le configurazioni del servizio cloud:

1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   * Per ulteriori informazioni, vedere la documentazione del [browser di configurazione](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=it).
1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud oppure ignora questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

   1. Nel **[!UICONTROL Browser configurazioni]**, selezionare la cartella `global` e selezionare **[!UICONTROL Proprietà]**.

   1. Nella finestra di dialogo **[!UICONTROL Proprietà configurazione]**, abilita **[!UICONTROL Configurazioni cloud]**.

   1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Nel **[!UICONTROL Browser configurazioni]**, selezionare **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
1. Seleziona **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

## Configurare i servizi web RESTful {#configure-restful-web-services}

I servizi Web RESTful possono essere descritti utilizzando [Specifiche Swagger](https://swagger.io/specification/v2/) in formato JSON o YAML in un file di definizione [!DNL Swagger] o un endpoint di servizio.

>[!NOTE]
> Per configurare il servizio Web RESTful in as a Cloud Service [!DNL Experience Manager], verificare di disporre del file [!DNL Swagger] ([Swagger versione 2.0](https://swagger.io/specification/v2/)) o del file [!DNL Swagger] ([Swagger versione 3.0](https://swagger.io/specification/v3/)) nel file system o dell&#39;URL in cui è ospitato il file.

### Configurazione dei servizi RESTful per la specifica API Open versione 2.0 {#configure-restful-services-open-api-2.0}

1. Vai a **[!UICONTROL Strumenti > Servizi cloud > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud, consulta [Configurare la cartella per le configurazioni del servizio cloud](configure-data-sources.md#cloud-folder).

1. Selezionare **[!UICONTROL Crea]** per aprire la **[!UICONTROL Creazione guidata configurazione Data Source]**. Specifica un nome e, facoltativamente, un titolo per la configurazione. Seleziona **[!UICONTROL Servizio RESTful]** dal menu a discesa **[!UICONTROL Tipo di servizio]**. Se necessario, sfoglia e seleziona un&#39;immagine di anteprima per la configurazione, quindi seleziona **[!UICONTROL Avanti]**.
1. Specificare i dettagli seguenti per il servizio RESTful:

   * Selezionare un URL o un file dal menu a discesa [!UICONTROL Swagger Source] e specificare di conseguenza [!DNL Swagger URL] nel file di definizione [!DNL &#x200B; Swagger] o caricare il file [!DNL Swagger] dal file system locale.
   * In base all&#39;input di Source [!DNL &#x200B; Swagger], i campi seguenti sono precompilati con i valori:

      * Schema: protocolli di trasferimento utilizzati dall’API REST. Il numero di tipi di schema visualizzati nell&#39;elenco a discesa dipende dagli schemi definiti nell&#39;origine [!DNL Swagger].
      * Host: il nome di dominio o l’indirizzo IP dell’host che serve l’API REST. È un campo obbligatorio.
      * Percorso base: prefisso URL per tutti i percorsi API. È un campo facoltativo.\
        Se necessario, modifica i valori precompilati per questi campi.

   * Selezionare il tipo di autenticazione, ovvero Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), Autenticazione di base, Chiave API o Autenticazione personalizzata, per accedere al servizio RESTful e fornire di conseguenza i dettagli per l&#39;autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specificare il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una di queste opzioni dall&#39;elenco a discesa **[!UICONTROL Posizione]** e specifica di conseguenza il nome dell&#39;intestazione o il parametro della query nel campo **[!UICONTROL Nome parametro]**.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

### Configurare i servizi RESTful per la versione 3.0 delle specifiche API aperte {#configure-restful-services-open-api-3.0}

1. Vai a **[!UICONTROL Strumenti > Servizi cloud > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud, consulta [Configurare la cartella per le configurazioni del servizio cloud](configure-data-sources.md#cloud-folder).

1. Selezionare **[!UICONTROL Crea]** per aprire la **[!UICONTROL Creazione guidata configurazione Data Source]**. Specifica un nome e, facoltativamente, un titolo per la configurazione. Seleziona **[!UICONTROL Servizio RESTful]** dal menu a discesa **[!UICONTROL Tipo di servizio]**. Se necessario, sfoglia e seleziona un&#39;immagine di anteprima per la configurazione, quindi seleziona **[!UICONTROL Avanti]**.
1. Specificare i dettagli seguenti per il servizio RESTful:

   * Selezionare un URL o un file dal menu a discesa [!UICONTROL Swagger Source] e specificare di conseguenza [!DNL Swagger 3.0 URL] nel file di definizione [!DNL &#x200B; Swagger] o caricare il file [!DNL Swagger] dal file system locale.
   * In base all&#39;input di Source [!DNL &#x200B; Swagger], vengono visualizzate le informazioni di connessione con il server di destinazione.
   * Selezionare il tipo di autenticazione, ovvero Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), Autenticazione di base, Chiave API o Autenticazione personalizzata, per accedere al servizio RESTful e fornire di conseguenza i dettagli per l&#39;autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specificare il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una di queste opzioni dall&#39;elenco a discesa **[!UICONTROL Posizione]** e specifica di conseguenza il nome dell&#39;intestazione o il parametro della query nel campo **[!UICONTROL Nome parametro]**.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio RESTful.

Alcune delle operazioni non supportate dalla versione 3.0 della specifica Open API dei servizi RESTful sono:

* Callback
* uno di/qualsiasi di
* Riferimento remoto
* Collegamenti
* Diversi corpi di richiesta per diversi tipi MIME per una singola operazione

Per informazioni dettagliate, vedere la specifica [OpenAPI 3.0](https://swagger.io/specification/v3/).

### Configurare i servizi RESTful tramite Service Endpoint {#configure-restful-services-service-endpoint}

<span class="preview"> La funzionalità Service Endpoint si trova nel programma Early Adopter ed è applicabile solo ai Componenti core. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

1. Vai a **[!UICONTROL Strumenti > Servizi cloud > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud, consulta [Configurare la cartella per le configurazioni del servizio cloud](configure-data-sources.md#cloud-folder).

1. Selezionare **[!UICONTROL Crea]** per aprire la **[!UICONTROL Creazione guidata configurazione Data Source]**.

1. Specifica un nome e, facoltativamente, un titolo per la configurazione. Seleziona **[!UICONTROL Servizio RESTful]** dal menu a discesa **[!UICONTROL Tipo di servizio]**. Se necessario, sfoglia e seleziona un&#39;immagine di anteprima per la configurazione, quindi seleziona **[!UICONTROL Avanti]**.

1. Nella pagina successiva, seleziona **[!UICONTROL Endpoint servizio]** dal menu a discesa **[!UICONTROL Servizio RESTful]**.

   ![Endpoint servizio](/help/forms/assets/select-service-endpoint.png)

1. Specificare **[!UICONTROL URL endpoint servizio]**.

   >[!NOTE]
   > Per impostazione predefinita, il tipo di metodo è POST.
1. Selezionare uno dei tipi di contenuto che si desidera scegliere dall&#39;elenco a discesa. I tipi di contenuto sono Dati modulo in più parti, JSON e codificati in URL (coppia chiave-valore).
1. Ora puoi selezionare uno qualsiasi dei tipi di autenticazione, ad esempio OAuth 2.0, Autenticazione di base, Chiave API, Autenticazione personalizzata, dall’elenco a discesa.
   ![Tipo di autenticazione dell&#39;endpoint del servizio](/help/forms/assets/service-endpoint-authtype.png)
1. Fai clic su Crea.

### Configurazione del client HTTP Form Data Model (FDM) per ottimizzare le prestazioni {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] forma un modello dati durante l&#39;integrazione con i servizi Web RESTful come origine dati include configurazioni client HTTP per l&#39;ottimizzazione delle prestazioni.

Impostare le seguenti proprietà della configurazione client HTTP del modello dati **[!UICONTROL Form per l&#39;origine dati REST]** per specificare l&#39;espressione regolare:

* Utilizzare la proprietà `http.connection.max.per.route` per impostare il numero massimo di connessioni consentite tra il modello dati del modulo (FDM) e i servizi Web RESTful. Il valore predefinito è 20 connessioni.

* Utilizzare la proprietà `http.connection.max` per specificare il numero massimo di connessioni consentite per ogni route. Il valore predefinito è 40 connessioni.

* Utilizzare la proprietà `http.connection.keep.alive.duration` per specificare la durata per la quale una connessione HTTP persistente viene mantenuta attiva. Il valore predefinito è 15 secondi.

* Utilizzare la proprietà `http.connection.timeout` per specificare la durata dell&#39;attesa di connessione da parte del server [!DNL Experience Manager Forms]. Il valore predefinito è 10 secondi.

* Utilizzare la proprietà `http.socket.timeout` per specificare il periodo massimo di inattività tra due pacchetti di dati. Il valore predefinito è 30 secondi.

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

1. Selezionare **[!UICONTROL Configurazione client HTTP modello dati modulo per origine dati REST]**.

1. Nella finestra di dialogo [!UICONTROL Configurazione client HTTP modello dati modulo per origine dati REST]:

   * Specifica il numero massimo di connessioni consentite tra il modello dati del modulo (FDM) e i servizi Web RESTful nel campo **[!UICONTROL Limite connessione in totale]**. Il valore predefinito è 20 connessioni.

   * Specificare il numero massimo di connessioni consentite per ogni route nel campo **[!UICONTROL Limite di connessioni per ogni route]**. Il valore predefinito è due connessioni.

   * Nel campo **[!UICONTROL Keep alive]** specificare la durata per la quale una connessione HTTP persistente viene mantenuta attiva. Il valore predefinito è 15 secondi.

   * Nel campo [!DNL Experience Manager Forms]Timeout connessione **[!UICONTROL specificare la durata dell&#39;attesa di una connessione da parte del server]**. Il valore predefinito è 10 secondi.

   * Specificare il periodo di tempo massimo per l&#39;inattività tra due pacchetti di dati nel campo **[!UICONTROL Timeout socket]**. Il valore predefinito è 30 secondi.

## Configurare i servizi Web di SOAP {#configure-soap-web-services}

I servizi Web basati su SOAP sono descritti utilizzando [le specifiche WSDL (Web Services Description Language)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] non supporta il modello WSDL in stile RPC.

Per configurare il servizio Web basato su SOAP in [!DNL Experience Manager] as a Cloud Service, verificare di disporre dell&#39;URL WSDL per il servizio Web e procedere come segue:

1. Vai a **[!UICONTROL Strumenti > Servizi cloud > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud, consulta [Configurare la cartella per le configurazioni del servizio cloud](configure-data-sources.md#cloud-folder).

1. Selezionare **[!UICONTROL Crea]** per aprire la **[!UICONTROL Creazione guidata configurazione Data Source]**. Specifica un nome e, facoltativamente, un titolo per la configurazione. Seleziona **[!UICONTROL Servizio Web SOAP]** dal menu a discesa **[!UICONTROL Tipo di servizio]**. Se necessario, sfoglia e seleziona un&#39;immagine di anteprima per la configurazione, quindi seleziona **[!UICONTROL Avanti]**.
1. Specificare quanto segue per il servizio Web SOAP:

   * URL WSDL per il servizio Web.
   * Endpoint servizio. Specificare un valore in questo campo per sostituire l&#39;endpoint del servizio indicato in WSDL.
   * Selezionare il tipo di autenticazione, ovvero Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), Autenticazione di base o Autenticazione personalizzata, per accedere al servizio SOAP e fornire i dettagli per l&#39;autenticazione.

     <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
     <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

     <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio Web SOAP.

### Abilitare l&#39;utilizzo delle istruzioni di importazione in SOAP Web Services WSDL {#enable-import-statements}

È possibile specificare un&#39;espressione regolare che funga da filtro per gli URL assoluti consentiti come istruzioni di importazione in SOAP Web Services WSDL. Per impostazione predefinita, in questo campo non è presente alcun valore. [!DNL Experience Manager] blocca pertanto tutte le istruzioni di importazione disponibili in WSDL. Se si specifica `.*` come valore in questo campo, [!DNL Experience Manager] consente tutte le istruzioni di importazione.

Impostare la proprietà `importAllowlistPattern` della configurazione **[!UICONTROL Modello dati modulo SOAP Inserire nell&#39;elenco Consentiti Web Services Import]** per specificare l&#39;espressione regolare. Il seguente file JSON mostra un esempio:

```json
{
  "importAllowlistPattern": ".*"
}
```

Per impostare i valori di una configurazione, [Genera configurazioni OSGi utilizzando AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=it#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [distribuisci la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=it#deployment-process) nell&#39;istanza Cloud Service.

## Configurare i servizi OData {#config-odata}

Un servizio OData è identificato dall&#39;URL radice del servizio. Per configurare un servizio OData in as a Cloud Service [!DNL Experience Manager], verificare di disporre dell&#39;URL principale del servizio e procedere come segue:

>[!NOTE]
>
> Il modello dati modulo supporta [OData versione 4](https://www.odata.org/documentation/).
>Per una guida dettagliata alla configurazione di [!DNL Microsoft®® Dynamics 365], online o on-premise, vedere [[!DNL Microsoft® Dynamics] Configurazione OData](ms-dynamics-odata-configuration.md).

1. Vai a **[!UICONTROL Strumenti > Servizi cloud > Origini dati]**. Seleziona per selezionare la cartella in cui desideri creare una configurazione cloud.

   Per informazioni sulla creazione e la configurazione di una cartella per le configurazioni del servizio cloud, consulta [Configurare la cartella per le configurazioni del servizio cloud](#cloud-folder).

1. Selezionare **[!UICONTROL Crea]** per aprire la **[!UICONTROL Creazione guidata configurazione Data Source]**. Specifica un nome e, facoltativamente, un titolo per la configurazione. Seleziona **[!UICONTROL Servizio OData]** dal menu a discesa **[!UICONTROL Tipo di servizio]**. Se necessario, sfoglia e seleziona un&#39;immagine di anteprima per la configurazione, quindi seleziona **[!UICONTROL Successivo]**.
1. Specificare i dettagli seguenti per il servizio OData:

   * URL principale del servizio per il servizio OData da configurare.
   * Selezionare il tipo di autenticazione, ovvero Nessuno, OAuth2.0([Codice di autorizzazione](https://oauth.net/2/grant-types/authorization-code/), [Credenziali client](https://oauth.net/2/grant-types/client-credentials/)), Autenticazione di base, Chiave API o Autenticazione personalizzata, per accedere al servizio OData e fornire i dettagli per l&#39;autenticazione.

   Se si seleziona **[!UICONTROL Chiave API]** come tipo di autenticazione, specificare il valore per la chiave API. La chiave API può essere inviata come intestazione di richiesta o come parametro di query. Seleziona una di queste opzioni dall&#39;elenco a discesa **[!UICONTROL Posizione]** e specifica di conseguenza il nome dell&#39;intestazione o il parametro della query nel campo **[!UICONTROL Nome parametro]**.

   >[!NOTE]
   >
   >Selezionare il tipo di autenticazione OAuth 2.0 per connettersi ai servizi [!DNL Microsoft®® Dynamics] utilizzando l&#39;endpoint OData come radice del servizio.

1. Selezionare **[!UICONTROL Crea]** per creare la configurazione cloud per il servizio OData.

<!--
## Configure Microsoft&reg; SharePoint List {#config-sharepoint-list}

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features). </span>

To save data in a tabular form use, Microsoft&reg; SharePoint List. To configure a Microsoft SharePoint List in [!DNL Experience Manager] as a Cloud Service, do the following:

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft&reg; SharePoint]**.   
1. Select a **Configuration Container**. The configuration is stored in the selected Configuration Container. 
1. Click **[!UICONTROL Create]** > **[!UICONTROL SharePoint List]** from the drop-down list. The SharePoint configuration wizard appears.  
1. Specify the **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** and **[!UICONTROL OAuth URL]**. For information on how to retrieve Client ID, Client Secret, Tenant ID for OAuth URL, see [Microsoft&reg; Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
    * You can retrieve the `Client ID` and `Client Secret` of your app from the Microsoft&reg; Azure portal.
    * In the Microsoft&reg; Azure portal, add the Redirect URI as `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Replace `[author-instance]` with the URL of your Author instance.
    * Add the API permissions `offline_access` and `Sites.Manage.All` in the **Microsoft&reg; Graph** tab to provide read/write permissions. Add `AllSites.Manage` permission in the **Sharepoint** tab to interact remotely with SharePoint data.
    * Use OAuth URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` with the `tenant-id` of your app from the Microsoft&reg; Azure portal.

      >[!NOTE]
      >
      > The **client secret** field is mandatory or optional depends upon your Azure Active Directory application configuration. If your application is configured to use a client secret, it is mandatory to provide the client secret.

1. Click **[!UICONTROL Connect]**. On a successful connection, the `Connection Successful` message appears.
1. Select **[!UICONTROL SharePoint Site]** and **[!UICONTROL SharePoint List]** from the drop-down list.
1. Select **[!UICONTROL Create]** to create the cloud configuration for the Microsoft&reg; SharePointList.

-->

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model (FDM), both the data source and [!DNL Experience Manager] Server running Form Data Model (FDM) authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model (FDM) on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and select **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and select **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, select **[!UICONTROL Select Certificate File]**, upload the certificate, and select **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Passaggi successivi {#next-steps}

Hai configurato le origini dati. È quindi possibile creare un modello dati modulo (FDM) oppure, se è già stato creato un modello dati modulo (FDM) senza un&#39;origine dati, associarlo alle origini dati configurate. Per ulteriori dettagli, vedere [Crea modello dati modulo](create-form-data-models.md).

<!--

>[!MORELIKETHIS]
>
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>*  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->