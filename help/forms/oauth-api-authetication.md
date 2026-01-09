---
title: Come si imposta l'autenticazione server-to-server OAuth?
description: Scopri come configurare l’autenticazione server-to-server OAuth per Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: e2f57a32fcc098a2331ad74540a3d48832c2b3c3
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 3%

---


# Autenticazione server-to-server OAuth

OAuth Server-to-Server Authentication consente l&#39;accesso sicuro e basato su token alle API di AEM Forms Communications senza richiedere l&#39;interazione dell&#39;utente. L&#39;autenticazione server-to-server OAuth è supportata da Adobe Developer Console.

## Prerequisiti

Prima di iniziare, accertati di soddisfare i seguenti prerequisiti:

* Assicurati di avere [accesso a Adobe Developer Console](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-manager/content/requirements/access-rights) specifico per l&#39;ambiente in uso.
* [Assegnare il ruolo Amministratore di sistema o Sviluppatore in Adobe Admin Console](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions) per abilitare l&#39;accesso a Adobe Developer Console.

## Come si genera un token di accesso utilizzando l’autenticazione server-to-server di OAuth?

Segui i passaggi seguenti per generare un token di accesso dalla console Adobe Developer ed effettua la prima chiamata API tramite l’autenticazione server-to-server OAuth.

### Configurazione del progetto Adobe Developer Console

1. Passa a [Adobe Developer Console](https://developer.adobe.com/console)
2. Accedi con il tuo Adobe ID

3. Crea un nuovo progetto o accedi al progetto esistente

>[!BEGINTABS]

>[!TAB Per creare un nuovo progetto]

1. Dalla sezione **Guida rapida**, fai clic su **Crea nuovo progetto**
2. Viene creato un nuovo progetto con un nome predefinito

   ![Crea progetto ADC](/help/forms/assets/adc-home.png)

3. Fai clic su **Modifica progetto** nell&#39;angolo superiore destro

   ![Modifica progetto](/help/forms/assets/adc-edit-project.png)

4. Fornisci un nome significativo (ad esempio, &quot;formsproject&quot;)
5. Fai clic su **Salva**

   ![Modifica nome progetto](/help/forms/assets/adc-edit-projectname.png)

>[!TAB Per passare al progetto esistente]

1. Fai clic su **Tutti i progetti** da Adobe Developer Console

   ![Progetti di ricerca](/help/forms/assets/search-adc-project.png)

2. Individua il progetto e fai clic su per aprirlo.

   ![Individua Progetti](/help/forms/assets/locate-adc-project.png)

>[!ENDTABS]

### Aggiungere API Forms

Aggiungi API Forms in base a ciò che desideri fare:

* **API di AEM Forms Communications**: da utilizzare quando è necessario generare, convertire, assemblare o proteggere documenti (PDF e formati correlati).
* **API Forms Runtime adattive**: da utilizzare quando è necessario eseguire il rendering, inviare o elaborare Forms adattivi in fase di esecuzione.

>[!BEGINTABS]

>[!TAB Per le API di comunicazione di AEM Forms]

1. Fai clic su **Aggiungi API**

   ![Aggiungi API](/help/forms/assets/adc-add-api.png)

2. Seleziona **API di comunicazione Forms**
   1. Nella finestra di dialogo _Aggiungi API_, filtra per **Experience Cloud**
   2. Seleziona **&quot;API di comunicazione Forms&quot;**

      ![Aggiungi API di comunicazione Forms](/help/forms/assets/adc-add-forms-api.png)

   3. Fai clic su **Avanti**
   4. Seleziona il metodo di autenticazione da server a server **OAuth**

      ![Seleziona metodo di autenticazione](/help/forms/assets/adc-add-authentication-method.png)

>[!TAB Per le API runtime di Forms adattivi]

1. **Fai clic su Aggiungi API**

   ![Aggiungi API](/help/forms/assets/adc-add-api.png)

2. **Seleziona l&#39;API di AEM Forms Delivery e Runtime**
   1. Nella finestra di dialogo _Aggiungi API_, filtra per **Experience Cloud**
   2. Seleziona **&quot;AEM Forms Delivery and Runtime API&quot;**
      ![Aggiungi API di comunicazione Forms](/help/forms/assets/adc-add-runtime-api.png)

   3. Fai clic su **Avanti**
   4. Selezionare il metodo di autenticazione da server a server **OAuth**.
      ![Seleziona metodo di autenticazione](/help/forms/assets/adc-add-authentication-method.png)

>[!ENDTABS]

>[!NOTE]
>
> Puoi anche aggiungere l&#39;API e il metodo di autenticazione al progetto esistente facendo clic su **Aggiungi al progetto** > **API**\
> ![Aggiungi API al progetto esistente](/help/forms/assets/add-api-existing-project.png)

### Aggiungi profilo prodotto

Il profilo di prodotto fornisce le autorizzazioni (o autorizzazioni) per le credenziali di accesso alle risorse di AEM.

1. Seleziona il **profilo prodotto** che corrisponde all&#39;URL dell&#39;istanza di AEM (`https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com`).

   * **Tipo di servizio** - specifica i servizi o le autorizzazioni associati all&#39;istanza di AEM

   * **Tipo di ambiente** - specifica se l&#39;ambiente è per il servizio Author o Publish

   * **Programma XXX** - identifica l&#39;ID del programma Cloud Manager

   * **Ambiente XXX** - identifica l&#39;ID ambiente specifico all&#39;interno di tale programma

   >
   >
   > I profili di prodotto sono legati a un’istanza AEM specifica (programma + ambiente). Scegli sempre il profilo che corrisponde all’URL dell’istanza.

2. Fai clic su **Salva API configurata**. L’API e il profilo di prodotto vengono aggiunti al progetto

   ![Seleziona configurazione progetto](/help/forms/assets/adc-add-product-profile.png)

### Generare e salvare le credenziali

1. Passare al progetto in Adobe Developer Console
2. Fai clic sulle credenziali da server a server **OAuth**
3. Visualizza la sezione **Dettagli credenziali**

   ![Visualizza credenziali](/help/forms/assets/adc-view-credential.png)

**Registra credenziali API**

```text
    API Credentials:
    ================
    Client ID: <your_client_id>
    Client Secret: <your_client_secret>
    Technical Account ID: <tech_account_id>
    Organization ID: <org_id>
    Scopes: AdobeID,openid,read_organizations
```

### Generazione token di accesso

Genera il token di accesso manualmente o a livello di programmazione:

>[!BEGINTABS]

>[!TAB Per test]

Generare manualmente i token di accesso in Adobe Developer Console:

1. **Accedi al progetto**
   1. In Adobe Developer Console, apri il progetto
   2. Fai clic su **Server-to-Server OAuth**

2. **Genera token di accesso**
   1. Fai clic sul pulsante **&quot;Genera token di accesso&quot;** nella sezione API del progetto
   2. Copia il token di accesso generato

   ![Genera token di accesso](/help/forms/assets/adc-access-token.png)

   >[!NOTE]
   >
   > Il token di accesso è valido solo per **24 ore**

>[!TAB Per La Produzione]

Genera i token a livello di programmazione utilizzando l&#39;API [Adobe IMS](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service):

**Credenziali richieste:**

* ID client
* Segreto client
* Ambiti (in genere: `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`)

**Endpoint token:**

```
https://ims-na1.adobelogin.com/ims/token/v3
```

**Richiesta di esempio (curl):**

```bash
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials' \
-d 'client_id=<YOUR_CLIENT_ID>' \
-d 'client_secret=<YOUR_CLIENT_SECRET>' \
-d 'scope=AdobeID,openid,read_organizations'
```

**Risposta:**

```json
    {
    "access_token": "eyJhbGciOiJSUz...",
    "token_type": "bearer",
    "expires_in": 86399
    }
```

>[!ENDTABS]

Ora puoi utilizzare il token di accesso generato per effettuare chiamate API per ambienti di sviluppo, stage o produzione.

>[!NOTE]
>
> Per ulteriori informazioni sull&#39;implementazione server-to-server di OAuth per generare il token di accesso ed effettuare chiamate API, [fai clic qui](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation).

## Best practice: gestione delle credenziali per lo sviluppo, la gestione temporanea e la produzione

* Utilizza sempre credenziali separate per Sviluppo, Staging e Produzione.

* Mappa ciascuna credenziale all’URL dell’ambiente AEM corretto.

* Archivia i segreti in modo sicuro e non esegui mai il commit nel controllo del codice sorgente.

* Tieni traccia della validità dei token di accesso, in quanto i token sono validi solo per 24 ore.

## Passaggi successivi

Per informazioni su come impostare l&#39;ambiente per le API di comunicazione sincrona di Forms, vedere [Elaborazione sincrona di AEM Forms as a Cloud Service Communications](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md).


## Articoli correlati

Scopri come impostare l’ambiente per le API di comunicazione Forms sincrone (su richiesta) e asincrone (in batch):

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="API sincrone" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="API sincrone"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="API di comunicazione AEM Forms - Sincrono">API di comunicazione AEM Forms - Sincrono</a>
                    </p>
                    <p class="is-size-6">Scopri come impostare l’ambiente per le API di comunicazione Forms sincrone (on-demand) che generano o elaborano documenti all’istante. </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="API di comunicazione AEM Forms - Asincrono" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="API asincrone"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="API asincrone">API di comunicazione AEM Forms - Asincrono (batch)</a>
                    </p>
                    <p class="is-size-6">Scopri come impostare l’ambiente per le API di comunicazione Forms asincrone (in batch) che generano o elaborano più documenti in modo pianificato.</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


