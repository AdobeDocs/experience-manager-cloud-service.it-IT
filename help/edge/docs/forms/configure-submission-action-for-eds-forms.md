---
title: Configurare le azioni di invio per AEM Forms con Edge Delivery Services
description: Scopri come configurare le azioni di invio in AEM Forms utilizzando Edge Delivery Services. Scegli tra Servizio di invio moduli e Azione di invio di AEM Publish per gestire i dati del modulo in modo sicuro ed efficiente.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2d16a9bd1f498dd0f824e867fd3b5676fb311bb3
workflow-type: ht
source-wordcount: '810'
ht-degree: 100%

---

# Configurare le azioni di invio per i moduli adattivi.

Configura la gestione dell’invio dei moduli per indirizzare i dati a fogli di calcolo, e-mail o sistemi back-end tramite AEM Forms con Edge Delivery Services.

## Guida rapida alle decisioni

Scegli il metodo di invio:

| Metodo | Ideale per | Complessità della configurazione | Casi d’uso |
|--------|----------|------------------|-----------|
| **Servizio di invio dei moduli** | Acquisizione semplice dei dati | Bassa | Moduli di contatto, sondaggi, raccolta di dati di base |
| **Invio AEM Publish** | Flussi di lavoro complessi | Alta | Integrazioni aziendali, elaborazione personalizzata, flussi di lavoro |

## Prerequisiti

Prima di configurare le azioni di invio, verifica di disporre di:

- Istanza AEM Forms as a Cloud Service
- Progetto Edge Delivery Services configurato
- Modulo creato tramite l’authoring di documenti o l’editor universale
- Autorizzazioni richieste per le destinazioni target (fogli di calcolo, sistemi e-mail o AEM)

+++ Metodo 1: servizio di invio dei moduli

Il servizio di invio dei moduli è un endpoint ospitato da Adobe ideale per scenari di acquisizione dati semplici.

### Destinazioni supportate

- **Fogli di calcolo**: fogli Google, Microsoft Excel (OneDrive/SharePoint)
- **E-mail**: invia i dati del modulo agli indirizzi e-mail specificati

### Passaggi di configurazione

1. **Configurare l’accesso alla destinazione**
   - Per i fogli di calcolo: concedere l’autorizzazione di modifica a `forms@adobe.com` nel foglio di calcolo di destinazione
   - Per l’e-mail: verificare che gli indirizzi e-mail dei destinatari siano accessibili

2. **Configurare l’invio del modulo**
   - Aprire il modulo nell’ambiente di authoring
   - Impostare l’azione di invio su “Servizo di invio dei moduli”
   - Specificare gli indirizzi e-mail o l’URL del foglio di calcolo di destinazione
   - Salvare e pubblicare il modulo

3. **Invio di prova**
   - Inviare i dati di prova tramite il modulo
   - Verificare che i dati vengano visualizzati nella destinazione target
   - Controllare i registri di errore in caso di invio non riuscito

### Note importanti

- L’account del servizio `forms@adobe.com` richiede l’accesso in modifica ai fogli di calcolo di destinazione
- Le notifiche e-mail vengono inviate subito dopo l’invio del modulo
- La convalida dei dati avviene a livello di servizio

![Flusso del servizio di invio moduli](/help/forms/assets/eds-fss.png)

+++

+++ Metodo 2: Invio AEM Publish

Invia i dati del modulo direttamente all’istanza Publish di AEM as a Cloud Service per elaborazioni complesse.

### Quando utilizzare AEM Publish

- Flussi di lavoro AEM personalizzati richiesti dopo l’invio
- Integrazione del modello dati modulo (FDM) con i database
- Integrazioni di servizi di terze parti (Marketo, Power Automate, Workfront Fusion)
- Archiviazione BLOB di Azure o librerie di documenti SharePoint
- Logica di elaborazione o convalida complessa lato server

### Azioni di invio disponibili

- [Inviare all’endpoint REST](/help/forms/configure-submit-action-restpoint.md)
- [Inviare e-mail utilizzando i servizi di posta di AEM](/help/forms/configure-submit-action-send-email.md)
- [Inviare utilizzando il modello dati modulo](/help/forms/configure-data-sources.md)
- [Richiamare il flusso di lavoro AEM](/help/forms/aem-forms-workflow-step-reference.md)
- [Inviare a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Inviare a OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Inviare all’archiviazione Blob di Azure](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Inviare a iMicrosoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [Inviare a Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Inviare a Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![Flusso di invio AEM Publish](/help/forms/assets/eds-aem-publish.png)

### Requisiti di configurazione

#### &#x200B;1. Aggiornare l’URL dell’istanza di AEM in Edge Delivery

Aggiorna l’URL dell’istanza di AEM Cloud Service nel file `constant.js` all’interno del blocco `form` di `submitBaseUrl`. È possibile configurare l’URL in base al proprio ambiente:

**Per l’istanza di Cloud Service**

```js
export const submitBaseUrl = '<aem-publish-instance-URL>';
```

**Per lo sviluppo locale**

```js
export const submitBaseUrl = 'http://localhost:<port-number>';
```

#### &#x200B;2. Filtro referrer OSGi

Configura il filtro Referrer per consentire i domini specifici del tuo sito Edge Delivery:

1. Crea o aggiorna il file di configurazione OSGi: `org.apache.sling.security.impl.ReferrerFilter.cfg.json`

2. Aggiungi la seguente configurazione ai domini specifici del tuo sito:

   ```json
   {
     "allow.empty": false,
     "allow.hosts": [
       "main--abc--adobe.aem.live",
       "main--abc1--adobe.aem.live"
     ],
     "allow.hosts.regexp": [
       "https://.*\\.aem\\.live:443",
       "https://.*\\.aem\\.page:443",
       "https://.*\\.hlx\\.page:443",
       "https://.*\\.hlx\\.live:443"
     ],
     "filter.methods": [
       "POST",
       "PUT",
       "DELETE",
       "COPY",
       "MOVE"
     ],
     "exclude.agents.regexp": [
       ""
     ]
   }
   ```

3. Distribuisci la configurazione tramite Cloud Manager

Per informazioni dettagliate sulla configurazione del filtro OSGi Referrer, consulta la guida del [filtro Referrer](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter).

#### &#x200B;3. Problemi relativi a CORS (Cross-Origin Resource Sharing)

Configura le impostazioni CORS in AEM per consentire richieste dai domini specifici del tuo sito Edge Delivery:

**Localhost sviluppatore**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true
```

**Siti Edge Delivery - Aggiungi ogni dominio del sito singolarmente**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true
```

**Domini Franklin precedenti (se ancora in uso)**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>Sostituisci `main--abc--adobe.aem.live` e `main--abc1--adobe.aem.live` con i domini effettivi del tuo sito. Ogni sito ospitato dallo stesso archivio richiede una voce di configurazione CORS separata.

Per informazioni dettagliate sulla configurazione CORS, consulta la [Guida alla configurazione CORS](https://experienceleague.adobe.com/it/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).


Per abilitare CORS per l’ambiente di sviluppo locale, consulta l’articolo [Informazioni su CORS](https://experienceleague.adobe.com/it/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing).

<!--
#### 4. CDN Redirect Rules

Configure your Edge Delivery CDN to route submissions:

- Route requests from `/adobe/forms/af/submit/...` to your AEM Publish instance
- Implementation varies by CDN provider (Fastly, Akamai, Cloudflare)-->

#### &#x200B;4. Configurazione modulo

1. Creare un modulo nell’editor universale
2. Configurare l’azione di invio per eseguire il targeting dell’azione AEM Forms
3. Specificare il percorso dell’endpoint di invio
4. Pubblicare il modulo sul sito Edge Delivery

+++
<!--
+++ Form Embedding

Embed forms created in one location into different web pages or sites.

### Use Cases

- Reuse standard forms across multiple landing pages
- Include specialized forms in Document-Authored content
- Maintain single form across multiple EDS projects

### CORS Configuration

Configure Cross-Origin Resource Sharing on the form source:

1. **Add CORS Headers** to form source responses:
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`  
   - `Access-Control-Allow-Headers: Content-Type`

2. **Example Configuration**:

        # Configuration for site hosting the form
        headers:
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS

### Embedding Steps

1. **Create and Publish Form**
   - Build form using Document Authoring or Universal Editor
   - Configure submission method (FSS or AEM Publish)
   - Publish to standalone URL

2. **Configure CORS**
   - Set up CORS headers on form source site
   - Allow host page domain to fetch form

3. **Embed in Host Page**
   - Add form embedding block to host page
   - Point block to published form URL
   - Publish host page

![Embedded Form Architecture](/help/forms/assets/eds-embedded-form.png)

+++-->

+++ Problemi comuni

| Problema | Soluzione |
|-------|----------|
| **Invio del modulo non riuscito** | Controllare gli errori della console, verificare l’URL dell’endpoint, confermare le autorizzazioni |
| **Modulo incorporato non visualizzato** | Configurare le intestazioni CORS nella sorgente del modulo, verificare l’URL del modulo |
| **errori 403/401 con AEM** | Aggiornare il filtro referrer Sling, controllare le impostazioni di autenticazione |
| **I dati non raggiungono il foglio di calcolo** | Verificare che `forms@adobe.com` disponga dell’accesso in modifica e controllare l’URL del foglio di calcolo |
| **Errori CORS** | Aggiungere le intestazioni `Access-Control-Allow-Origin` corrette alla sorgente del modulo |

+++

## Esempi di configurazione

+++ Modulo basato su documenti con invio del foglio di calcolo

1. Creare una struttura di modulo in Google Docs/Sheets
2. Configurare l’endpoint del servizio di invio dei moduli
3. Concedere a `forms@adobe.com` l’accesso in modifica al foglio di calcolo di destinazione
4. Pubblica il documento sul sito Edge Delivery.
5. Invio di moduli di prova e flusso di dati

+++

+++ Modulo editor universale con flusso di lavoro AEM

1. Creare un modulo nell’editor universale
2. Configurare l’azione di invio per “richiamare il flusso di lavoro AEM”
3. Configurare Dispatcher e il filtro referrer su AEM Publish
4. Configurare le regole di routing CDN
5. Pubblicare un modulo e testare l’esecuzione del flusso di lavoro

+++

## Best practice

- **Utilizzare il servizio di invio dei moduli** per semplici scenari di acquisizione dati
- **Scegliere AEM Publish** quando sono necessarie elaborazioni o integrazioni complesse
- **Verificare in modo approfondito** nell’ambiente di staging prima della distribuzione in produzione
- **Monitorare gli invii** tramite i registri di AEM ed errori della console
- **Implementare la corretta gestione degli errori** per gli invii non riusciti
- **Convalidare i dati** a livello client e server
- **Utilizzare HTTPS** per tutti gli invii di moduli e la trasmissione di dati

## Argomenti correlati

- [Authoring basato su documenti con moduli EDS](/help/edge/docs/forms/tutorial.md)
- [Editor universale con moduli EDS](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [Servizio di invio dei moduli AEM](/help/forms/forms-submission-service.md)
- [Configurare le origini dati](/help/forms/configure-data-sources.md)
- [Riferimento flusso di lavoro di AEM Forms](/help/forms/aem-forms-workflow-step-reference.md)
