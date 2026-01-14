---
title: Come si imposta l’autenticazione JWT (JSON Web Token)?
description: Scopri come configurare l’autenticazione JWT (JSON Web Token) per Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
source-git-commit: 43b648eb3984867fda35ee04de10b78dd836b481
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 3%

---


# Autenticazione server-to-server JWT (JSON Web Token)

L’autenticazione JWT da server a server in AEM Forms, in particolare per le integrazioni lato server con AEM as a Cloud Service, prevede un processo specifico per interagire in modo sicuro con i servizi AEM. L’autenticazione da server a server JWT è supportata da AEM Developer Console.

## Prerequisiti

Prima di iniziare, accertati di soddisfare i seguenti prerequisiti:

* Assicurati di avere accesso a [Adobe Cloud Manager](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html) specifico per l&#39;ambiente che utilizzi.
* Assegna il ruolo [Amministratore di sistema o Sviluppatore per accedere ad Adobe Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-manager/content/requirements/access-rights).

## Come si genera un token di accesso utilizzando le credenziali JWT?

Segui i passaggi indicati di seguito per generare un token di accesso dalle credenziali JWT.

1. **Adobe Cloud Manager**

   1. Accedi al tuo [account Cloud Manager](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html).
   2. Nel programma selezionato, fai clic su **[!UICONTROL Panoramica programma]**.

      ![Account Cloud Manager](/help/forms/assets/jwt-cloud-manager-landing.png)

   3. Nel programma, fai clic sul menu con tre puntini e seleziona **[!UICONTROL Developer Console]**.

      ![Console per sviluppatori](/help/forms/assets/jwt-developer-console.png)

2. **AEM Developer Console**
   1. Accedi ad AEM Developer Console
   2. Fai clic su **[!UICONTROL Integrazioni]** nella barra dei menu superiore.

      ![Integrazioni](/help/forms/assets/jwt-integrations.png)

   3. Fai clic sull&#39;opzione per **[!UICONTROL creare un nuovo account tecnico]**.

      ![Crea nuovo account tecnico](/help/forms/assets/jwt-creae-new-tech-account.png)

   Dopo aver fatto clic su crea un nuovo account tecnico, vengono generate le informazioni necessarie per generare il token di accesso, come l’ID client e il segreto client, insieme ad altre informazioni tecniche sull’account, tra cui chiave privata, chiave pubblica e data di scadenza.

   ![Credenziali JWT](/help/forms/assets/jwt-credentials.png)


3. **Genera e salva credenziali**

   1. Registra credenziali API

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

4. **Generazione token di accesso**

   Genera i token a livello di programmazione utilizzando il comando cURL:

   **Credenziali richieste:**

   * ID client
   * Segreto client
   * Ambiti (in genere: `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`)

   **Endpoint token:**

   ```
   https://ims-na1.adobelogin.com/ims/token/v3
   ```

   **Richiesta di esempio (cURL):**

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


>[!NOTE]
>
> Per ulteriori informazioni sulle credenziali del servizio e su come generare un token di accesso utilizzando l&#39;API Adobe IMS, [fai clic qui](https://experienceleague.adobe.com/it/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials).

Ora puoi utilizzare il token di accesso generato per effettuare chiamate API per ambienti di sviluppo, stage o produzione.

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


>[!MORELIKETHIS]
>
>* [Introduzione ad AEM Forms as a Cloud Service Communications](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Architettura AEM Forms as a Cloud Service per API Forms adattivi e di comunicazione](/help/forms/aem-forms-cloud-service-architecture.md)
>* [Elaborazione comunicazione - API sincrone](/help/forms/aem-forms-cloud-service-communications.md)
>* [Elaborazione comunicazione - API batch](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [API Forms Communications - Tutorial](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)