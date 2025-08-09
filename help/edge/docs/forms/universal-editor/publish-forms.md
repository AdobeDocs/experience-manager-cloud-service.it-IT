---
title: Pubblicare Forms adattivo con Edge Delivery Services
description: Scopri come pubblicare, configurare e accedere a Adaptive Forms utilizzando Edge Delivery Services per la produzione.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
keywords: [pubblicazione di moduli, Edge Delivery Services, configurazione dei moduli, CORS, filtro referrer]
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: tm+mt
source-wordcount: 746
ht-degree: 2%

---

# Pubblicare Forms adattivo con Edge Delivery Services

La pubblicazione di un modulo adattivo ne consente l’accesso e l’invio da parte degli utenti finali su Edge Delivery Services. Questo processo prevede tre fasi principali: pubblicazione del modulo, configurazione delle impostazioni di protezione e accesso al modulo live.

**Operazioni da eseguire:**

- Pubblicare il modulo in Edge Delivery Services
- Configurare le impostazioni di protezione per l&#39;invio dei moduli
- Accedere e verificare il modulo pubblicato
- Impostare il routing URL e i criteri CORS appropriati

## Prerequisiti

- Modulo adattivo creato utilizzando un modello di Edge Delivery Services
- Modulo testato e pronto per l’uso in produzione
- Autorizzazioni di authoring di AEM Forms
- Accesso a Cloud Manager (per la configurazione di produzione)
- Accesso degli sviluppatori al codice del blocco modulo (per la configurazione dell’invio)

## Panoramica del processo di pubblicazione

La pubblicazione dei moduli in Edge Delivery Services segue un approccio in tre fasi:

- **Fase 1: pubblicazione modulo** - Pubblica il modulo sul CDN e verifica lo stato di pubblicazione
- **Fase 2: configurazione della sicurezza** - Impostazione dei criteri CORS e dei filtri di riferimento per gli invii sicuri
- **Fase 3: accesso e convalida** - Verificare la funzionalità del modulo e convalidare il flusso di lavoro completo

Ogni fase si basa sulla precedente per garantire una distribuzione sicura e funzionale.

### Fase 1: Pubblicazione del modulo

+++ Passaggio 1: avviare la pubblicazione

1. **Accedi al modulo**: apri il modulo adattivo nell&#39;editor universale
2. **Inizia pubblicazione**: fai clic sull&#39;icona **Pubblica** nella barra degli strumenti

   ![Fai clic su Pubblica](/help/forms/assets/publish-icon-eds-form.png)

+++


+++ Passaggio 2: rivedere e confermare

1. **Rivedi la pubblicazione delle risorse**: il sistema mostra tutte le risorse in fase di pubblicazione, compreso il modulo

   ![Quando si fa clic su Pubblica](/help/forms/assets/on-click-publish.png)

2. **Conferma pubblicazione**: fai clic su **Pubblica** per continuare
3. **Verifica esito positivo**: cerca il messaggio di conferma

   ![Pubblicazione completata](/help/forms/assets/publish-success.png)

+++


+++ Passaggio 3: verificare lo stato della pubblicazione

**Verifica stato**: fai di nuovo clic sull&#39;icona **Pubblica** per visualizzare lo stato corrente

![Stato di pubblicazione](/help/forms/assets/publish-status.png)

**Checkpoint di convalida:**

- Il modulo mostra lo stato &quot;Pubblicato&quot; nell’editor
- Nessun messaggio di errore durante il processo di pubblicazione
- Il modulo viene visualizzato nell’elenco delle risorse pubblicate

+++


+++ Gestione di Published Forms

**Per annullare la pubblicazione di un modulo:**

1. Aprire il modulo nell’editor
2. Fai clic sul menu a tre punti (⋯) nell’angolo superiore destro
3. Seleziona **Annulla pubblicazione**

![Annulla pubblicazione modulo](/help/forms/assets/unpublish--form.png)

+++


### Fase 2: Configurare le impostazioni di protezione

+++ Perché è necessaria la configurazione della sicurezza

Per abilitare l’invio sicuro dei moduli, devi configurare le impostazioni di protezione che:

- Consenti a Edge Delivery Services di inviare dati ad AEM
- Impedire l’accesso non autorizzato all’istanza di AEM
- Abilita CORS (Cross-Origin Resource Sharing) per l’invio dei moduli
- Filtrare le richieste per consentire solo i domini Edge Delivery legittimi

>[!IMPORTANT]
>
>**Richiesto per la produzione**: queste configurazioni sono obbligatorie per l&#39;invio dei moduli in modo che funzionino negli ambienti di produzione.

+++



+++ Passaggio 1: configurare l’URL di invio del modulo

**Finalità**: invio diretto di moduli all&#39;istanza AEM

**Posizione file**: `blocks/form/constant.js` nel progetto Edge Delivery Services

**Esempi di configurazione:**

```javascript
// Production Environment
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';

// Local Development Environment  
export const submitBaseUrl = 'http://localhost:4503';

// Staging Environment
export const submitBaseUrl = 'https://publish-staging-p120-e12.adobeaemcloud.com';
```

**Checkpoint di convalida:**

- File `constant.js` aggiornato con l&#39;URL di pubblicazione AEM corretto
- L’URL corrisponde all’ambiente (produzione, gestione temporanea o locale)
- Nessuna barra finale nell’URL

+++



+++ Passaggio 2: configurare le impostazioni CORS

**Scopo**: Consenti richieste di invio moduli da domini Edge Delivery Services

**Implementazione**: aggiungi la configurazione CORS alla configurazione di AEM Dispatcher o Apache

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**Checkpoint di convalida:**

- Regole CORS applicate alla configurazione del dispatcher
- Sono inclusi tutti i domini richiesti (localhost, hlx.page, hlx.live)
- Configurazione distribuita nell’ambiente di destinazione

**Documentazione di riferimento:**

- [Guida alla configurazione CORS](https://experienceleague.adobe.com/it/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [Documentazione Filtro Referrer](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ Passaggio 3: configurare il filtro Referrer

**Scopo**: limitare le operazioni di scrittura ai domini Edge Delivery Services autorizzati

**Metodo di implementazione**: configurare tramite Cloud Manager in AEM as a Cloud Service

**File di configurazione**: aggiungi alla configurazione OSGi del progetto

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
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

**Analisi stratificata configurazione:**

- **`allow.empty`**: rifiuta le richieste senza intestazioni referrer
- **`allow.hosts.regexp`**: consente richieste da domini Edge Delivery Services
- **`filter.methods`**: applica il filtro a questi metodi HTTP
- **`exclude.agents.regexp`**: agenti utente esclusi dal filtro

**Checkpoint di convalida:**

- Configurazione del filtro referrer distribuita tramite Cloud Manager
- Configurazione attiva nell’istanza di pubblicazione di AEM
- L’invio del modulo di test funziona dal dominio Edge Delivery Services
- L&#39;invio di moduli da parte di domini non autorizzati è bloccato

**Documentazione di riferimento:**

- [Configurare il filtro Referrer tramite Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### Fase 3: Accesso al modulo pubblicato



+++ Struttura URL per Edge Delivery Services

**Formato URL standard:**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**Componenti URL:**

- **`<branch>`**: nome ramo Git (in genere `main`)
- **`<repo>`**: nome archivio
- **`<owner>`**: nome utente o organizzazione GitHub
- **`<form_name>`**: nome del modulo (lettere minuscole, trattini)

**URL specifici dell&#39;ambiente:**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ Passaggi di convalida finali

**Verifica accessibilità modulo:**

1. **Caricamento modulo di prova**: visita l&#39;URL del modulo e conferma che venga caricato correttamente
2. **Invia modulo di prova**: compila e invia il modulo per verificare l&#39;elaborazione dei dati
3. **Verifica progettazione reattiva**: verifica modulo su dispositivi e dimensioni dello schermo diversi
4. **Convalida sicurezza**: verifica che CORS e il filtro referrer funzionino correttamente

**Risultati previsti:**

- Il modulo viene caricato senza errori
- Tutti i campi modulo vengono riprodotti correttamente
- Processi di invio modulo completati
- I dati vengono visualizzati nella destinazione configurata (foglio di calcolo, e-mail, ecc.)
- Nessun errore della console correlato a CORS o ai criteri di sicurezza

+++


## Passaggi successivi


- [Configurare le azioni di invio dei moduli](/help/edge/docs/forms/universal-editor/submit-action.md)
- [Personalizzare lo stile e il tema dei moduli](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [Aggiungere la protezione reCAPTCHA](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)
- [Creare layout di moduli reattivi](/help/edge/docs/forms/universal-editor/responsive-layout.md)


