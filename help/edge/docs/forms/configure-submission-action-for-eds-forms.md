---
title: Configurare le azioni di invio per AEM Forms con Edge Delivery Services
description: Scopri come configurare le azioni di invio in AEM Forms utilizzando Edge Delivery Services. Scegli tra Servizio di invio moduli e Azione di invio di AEM Publish per gestire i dati del modulo in modo sicuro ed efficiente.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 12%

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

#### &#x200B;1. Configurazione di AEM Dispatcher

Configura Dispatcher nell’istanza AEM Publish:

- **Consenti percorsi di invio**: modifica `filters.any` per consentire le richieste POST a `/adobe/forms/af/submit/...`
- **Nessun reindirizzamento**: assicurati che le regole di Dispatcher non reindirizzino i percorsi di invio dei moduli

#### &#x200B;2. Filtro referrer OSGi

Nella console OSGi di AEM (`/system/console/configMgr`):

1. Trova &quot;Apache Sling Referrer Filter&quot; (Filtro Referrer Apache Sling)
2. Aggiungere il dominio Edge Delivery all’elenco &quot;Consenti host&quot;
3. Includi domini come `https://your-eds-domain.hlx.page`

#### &#x200B;3. Regole di reindirizzamento CDN

Configura la tua rete CDN di Edge Delivery per instradare gli invii:

- Inoltra le richieste da `/adobe/forms/af/submit/...` alla tua istanza di pubblicazione AEM
- L’implementazione varia a seconda del provider CDN (Fastly, Akamai, Cloudflare)

#### &#x200B;4. Configurazione modulo

1. Creare un modulo nell’editor universale
2. Configurare l’azione di invio per eseguire il targeting dell’azione AEM Forms
3. Specifica il percorso dell’endpoint di invio
4. Pubblicare un modulo su un sito Edge Delivery

+++

+++ Incorporamento modulo (facoltativo)

Incorpora i moduli creati in un percorso in pagine o siti Web diversi.

### Casi d’uso

- Riutilizzare i moduli standard in più pagine di destinazione
- Includi moduli specializzati nel contenuto creato da documenti
- Gestisci modulo singolo per più progetti EDS

### Configurazione CORS

Configura condivisione risorse tra origini nell&#39;origine del modulo:

1. **Aggiungi intestazioni CORS** alle risposte dell&#39;origine del modulo:
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`
   - `Access-Control-Allow-Headers: Content-Type`

2. **Esempio di configurazione**:

       &#x200B;# Configurazione per il sito che ospita il modulo
       intestazioni:
       - percorso: /forms/**
       personalizzato:
       Access-Control-Allow-Origin: https://host-domain.com
       Metodi Di Consenti-Controllo-Accesso: GET, OPTIONS
   

### Passaggi di incorporamento

1. **Crea e pubblica modulo**
   - Creare un modulo tramite l’authoring di documenti o l’editor universale
   - Configurare il metodo di invio (pubblicazione FSS o AEM)
   - Pubblica in URL autonomo

2. **Configura CORS**
   - Configurare le intestazioni CORS nel sito di origine del modulo
   - Consenti al dominio della pagina host di recuperare il modulo

3. **Incorpora nella pagina host**
   - Aggiungi blocco di incorporamento modulo alla pagina host
   - Posiziona blocco su URL modulo pubblicato
   - Pubblica pagina host

![Architettura modulo incorporato](/help/forms/assets/eds-embedded-form.png)

+++

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
