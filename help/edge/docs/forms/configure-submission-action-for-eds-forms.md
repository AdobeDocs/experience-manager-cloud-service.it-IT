---
title: Configurare le azioni di invio per AEM Forms con Edge Delivery Services
description: Scopri come configurare le azioni di invio in AEM Forms utilizzando Edge Delivery Services. Scegli tra Servizio di invio moduli e Azione di invio di AEM Publish per gestire i dati del modulo in modo sicuro ed efficiente.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2d16a9bd1f498dd0f824e867fd3b5676fb311bb3
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 13%

---

# Configurare le azioni di invio per AEM Forms

Configura la gestione dell’invio dei moduli per indirizzare i dati a fogli di calcolo, e-mail o sistemi backend tramite AEM Forms con Edge Delivery Services.

## Guida rapida alle decisioni

Scegliere il metodo di invio:

| Metodo | Ideale per | Complessità configurazione | Casi d’uso |
|--------|----------|------------------|-----------|
| **Servizio di invio Forms** | Acquisizione dati semplice | Bassa | Moduli di contatto, sondaggi, raccolta di dati di base |
| **Invio pubblicazione AEM** | Flussi di lavoro complessi | Alta | Integrazioni aziendali, elaborazione personalizzata, flussi di lavoro |

## Prerequisiti

Prima di configurare le azioni di invio, verifica di disporre di:

- Istanza di AEM Forms as a Cloud Service
- Progetto Edge Delivery Services configurato
- Modulo creato tramite l’authoring di documenti o l’editor universale
- Autorizzazioni richieste per le destinazioni (fogli di calcolo, sistemi e-mail o AEM)

+++ Metodo 1: Servizio di invio Forms

Il servizio di invio Forms è un endpoint ospitato da Adobe ideale per scenari di acquisizione dati semplici.

### Destinazioni supportate

- **Fogli di calcolo**: fogli Google, Microsoft Excel (OneDrive/SharePoint)
- **E-mail**: invia i dati del modulo agli indirizzi e-mail specificati

### Passaggi di configurazione

1. **Configurazione dell&#39;accesso di destinazione**
   - Per i fogli di calcolo: concedere l&#39;autorizzazione di modifica a `forms@adobe.com` nel foglio di calcolo di destinazione
   - Per l’e-mail: verifica che gli indirizzi e-mail dei destinatari siano accessibili

2. **Configura invio modulo**
   - Aprire il modulo nell’ambiente di authoring
   - Imposta l&#39;azione di invio su &quot;Forms Submission Service&quot;
   - Specifica l’URL o gli indirizzi e-mail del foglio di calcolo di destinazione
   - Salvare e pubblicare il modulo

3. **Invio di prova**
   - Inviare i dati di prova tramite il modulo
   - Verifica che i dati vengano visualizzati nella destinazione
   - Controlla i registri di errore se l’invio non riesce

### Note importanti

- L&#39;account del servizio `forms@adobe.com` richiede l&#39;accesso in modifica ai fogli di calcolo di destinazione
- Le notifiche e-mail vengono inviate subito dopo l’invio del modulo
- La convalida dei dati avviene a livello di servizio

![Flusso del servizio di invio Forms](/help/forms/assets/eds-fss.png)

+++

+++ Metodo 2: Invio pubblicazione AEM

Invia i dati del modulo direttamente all’istanza Publish di AEM as a Cloud Service per un’elaborazione complessa.

### Quando utilizzare AEM Publish

- Flussi di lavoro AEM personalizzati richiesti dopo l’invio
- Integrazione di Form Data Model (FDM) con i database
- Integrazioni di servizi di terze parti (Marketo, Power Automate, Workfront Fusion)
- Archiviazione BLOB di Azure o librerie di documenti SharePoint
- Logica di convalida o elaborazione lato server complessa

### Azioni di invio disponibili

- [Invia a endpoint REST](/help/forms/configure-submit-action-restpoint.md)
- [Inviare e-mail tramite i servizi di posta AEM](/help/forms/configure-submit-action-send-email.md)
- [Invia usando il modello dati modulo](/help/forms/configure-data-sources.md)
- [Richiama il flusso di lavoro AEM](/help/forms/aem-forms-workflow-step-reference.md)
- [Invia a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Invia a OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Inviare ad Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Inviare a iMicrosoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [Inviare a Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Inviare a Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![Flusso invio pubblicazione AEM](/help/forms/assets/eds-aem-publish.png)

### Requisiti di configurazione

#### &#x200B;1. Aggiornare l’URL dell’istanza di AEM in Edge Delivery

Aggiorna l&#39;URL dell&#39;istanza di AEM Cloud Service nel file `constant.js` nel blocco `form` in `submitBaseUrl`. Puoi configurare l’URL in base all’ambiente:

**Per l&#39;istanza di Cloud Service**

```js
export const submitBaseUrl = '<aem-publish-instance-URL>';
```

**Per lo sviluppo locale**

```js
export const submitBaseUrl = 'http://localhost:<port-number>';
```

#### &#x200B;2. Filtro referrer OSGi

Configura il filtro Referrer per consentire domini del sito Edge Delivery specifici:

1. Crea o aggiorna il file di configurazione OSGi: `org.apache.sling.security.impl.ReferrerFilter.cfg.json`

2. Aggiungi la seguente configurazione ai tuoi domini di sito specifici:

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

3. Distribuire la configurazione tramite Cloud Manager

Per informazioni dettagliate sulla configurazione del filtro Referrer OSGi, consulta la [Guida del filtro Referrer](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter).

#### &#x200B;3. Problemi CORS (Cross-Origin Resource Sharing)

Configura le impostazioni CORS in AEM per consentire le richieste dai domini del sito Edge Delivery specifici:

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
>Sostituisci `main--abc--adobe.aem.live` e `main--abc1--adobe.aem.live` con i tuoi domini del sito effettivi. Ogni sito ospitato dallo stesso archivio richiede una voce di configurazione CORS separata.

Per informazioni dettagliate sulla configurazione CORS, consulta la [Guida alla configurazione CORS](https://experienceleague.adobe.com/it/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).


Per abilitare CORS per l&#39;ambiente di sviluppo locale, consulta l&#39;articolo [Comprendere la condivisione CORS](https://experienceleague.adobe.com/it/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing).

<!--
#### 4. CDN Redirect Rules

Configure your Edge Delivery CDN to route submissions:

- Route requests from `/adobe/forms/af/submit/...` to your AEM Publish instance
- Implementation varies by CDN provider (Fastly, Akamai, Cloudflare)-->

#### &#x200B;4. Configurazione modulo

1. Creare un modulo nell’editor universale
2. Configurare l’azione di invio per eseguire il targeting dell’azione AEM Forms
3. Specifica il percorso dell’endpoint di invio
4. Pubblicare un modulo su un sito Edge Delivery

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

| Problema   | Soluzione |
|-------|----------|
| **Invio del modulo non riuscito** | Controlla gli errori della console, verifica l’URL dell’endpoint, conferma le autorizzazioni |
| **Modulo incorporato non visualizzato** | Configurare le intestazioni CORS nell’origine del modulo, verificare l’URL del modulo |
| **errori 403/401 con AEM** | Aggiorna filtro Sling Referrer, controlla le impostazioni di autenticazione |
| **I dati non raggiungono il foglio di calcolo** | Verificare che `forms@adobe.com` disponga dell&#39;accesso di modifica e controllare l&#39;URL del foglio di calcolo |
| **Errori CORS** | Aggiungi `Access-Control-Allow-Origin` intestazioni corrette all&#39;origine del modulo |

+++

## Esempi di configurazione

+++ Modulo basato su documenti con invio di fogli di calcolo

1. Creare una struttura di modulo in Google Docs/Sheets
2. Configurare l’endpoint del servizio di invio Forms
3. Concedi a `forms@adobe.com` l&#39;accesso in modifica al foglio di calcolo di destinazione
4. Pubblica documento su sito Edge Delivery
5. Invio di moduli di prova e flusso di dati

+++

+++ Modulo editor universale con flusso di lavoro AEM

1. Creare un modulo in Universal Editor
2. Configurare l’azione di invio per &quot;Richiamare il flusso di lavoro AEM&quot;
3. Configurare Dispatcher e il filtro referente su AEM Publish
4. Configurare le regole di routing CDN
5. Pubblicare un modulo e testare l’esecuzione del flusso di lavoro

+++

## Best practice

- **Utilizza Forms Submission Service** per semplici scenari di acquisizione dati
- **Scegli AEM Publish** quando sono necessarie elaborazioni o integrazioni complesse
- **Verifica approfondita** nell&#39;ambiente di staging prima della distribuzione di produzione
- **Monitorare gli invii** tramite i registri di AEM ed errori della console
- **Implementare la corretta gestione degli errori** per gli invii non riusciti
- **Convalida dati** a livello client e server
- **Usa HTTPS** per tutti gli invii di moduli e la trasmissione di dati

## Argomenti correlati

- [Authoring basato su documenti con EDS Forms](/help/edge/docs/forms/tutorial.md)
- [Editor universale con EDS Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [Servizio di invio dei moduli AEM](/help/forms/forms-submission-service.md)
- [Configurare origini dati](/help/forms/configure-data-sources.md)
- [Riferimento flusso di lavoro di AEM Forms](/help/forms/aem-forms-workflow-step-reference.md)
