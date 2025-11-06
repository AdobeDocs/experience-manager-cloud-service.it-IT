---
title: Pubblicare moduli adattivi con Edge Delivery Services
description: Scopri come pubblicare, configurare e accedere ai moduli adattivi utilizzando Edge Delivery Services per l’utilizzo in produzione.
feature: Edge Delivery Services
role: Admin, Developer
level: Intermediate
keywords: pubblicazione di moduli, Edge Delivery Services, configurazione dei moduli, CORS, filtro referrer
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 100%

---

# Pubblicare moduli adattivi con Edge Delivery Services

La pubblicazione di un modulo adattivo ne consente l’accesso e l’invio da parte degli utenti finali su Edge Delivery Services. Questo processo prevede tre fasi principali: pubblicazione del modulo, configurazione delle impostazioni di sicurezza e accesso al modulo live.

**Che cosa imparerai:**

- Pubblicare un modulo in Edge Delivery Services
- Configurare le impostazioni di sicurezza per l’invio dei moduli
- Accedere e verificare il modulo pubblicato
- Impostare l’indirizzamento URL e i criteri CORS appropriati

## Prerequisiti

- Modulo adattivo creato utilizzando il modello di Edge Delivery Services
- Modulo testato e pronto per l’uso in produzione
- Autorizzazioni di authoring di AEM Forms
- Accesso a Cloud Manager (per la configurazione della produzione)
- Accesso degli sviluppatori al codice del blocco modulo (per la configurazione dell’invio)

## Panoramica del processo di pubblicazione

La pubblicazione dei moduli in Edge Delivery Services segue un approccio in tre fasi:

- **Fase 1: pubblicazione del modulo**: pubblica il modulo sulla CDN e verifica lo stato di pubblicazione
- **Fase 2: configurazione della sicurezza**: impostazione dei criteri CORS e dei filtri referrer per gli invii sicuri
- **Fase 3: accesso e convalida**: verifica la funzionalità del modulo e convalida il flusso di lavoro completo

Ogni fase si basa sulla precedente per garantire una distribuzione sicura e funzionale.

### Fase 1: pubblicazione del modulo

+++ Passaggio 1: avviare la pubblicazione

1. **Accedi al modulo**: apri il modulo adattivo nell’editor universale
2. **Inizia la pubblicazione**: fai clic sull’icona **Pubblica** nella barra degli strumenti

   ![Fai clic su Pubblica](/help/edge/docs/forms/universal-editor/assets/publish-form-ue.png)

+++


+++ Passaggio 2: rivedi e conferma

1. **Rivedi le risorse della pubblicazione**: il sistema mostra tutte le risorse in fase di pubblicazione, compreso il modulo

   ![Quando fai clic su Pubblica](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-review.png)

2. **Conferma la pubblicazione**: fai clic su **Pubblica** per continuare
3. **Verifica esito positivo**: cerca il messaggio di conferma

   ![Pubblicazione completata](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-success.png)

+++


+++ Passaggio 3: verifica lo stato della pubblicazione

**Verifica lo stato**: fai di nuovo clic sull’icona **Pubblica** per visualizzare lo stato corrente

![Stato pubblicazione](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-validate.png)

**Punto di controllo della convalida:**

- Il modulo mostra lo stato “Pubblicato” nell’editor
- Nessun messaggio di errore durante il processo di pubblicazione
- Il modulo viene visualizzato nell’elenco delle risorse pubblicate

+++


+++ Gestione dei moduli pubblicati

**Per annullare la pubblicazione di un modulo:**

1. Apri il modulo nell’editor
2. Fai clic sul menu a tre punti (⋯) nell’angolo in alto a destra
3. Seleziona **Annulla pubblicazione**

![Annulla la pubblicazione del modulo](/help/edge/docs/forms/universal-editor/assets/unpublish-ue.png)

+++


### Fase 2: configura le impostazioni di sicurezza

+++ Perché è necessaria la configurazione della sicurezza

Per abilitare l’invio sicuro dei moduli, è necessario configurare le impostazioni di sicurezza che:

- Consentono a Edge Delivery Services di inviare dati ad AEM
- Impedire l’accesso non autorizzato all’istanza di AEM
- Abilitare CORS (Cross-Origin Resource Sharing) per l’invio dei moduli
- Filtrare le richieste per consentire solo i domini Edge Delivery legittimi

>[!IMPORTANT]
>
>**Richiesto per ambienti di produzione**: queste configurazioni sono obbligatorie per l’invio dei moduli in modo che funzionino negli ambienti di produzione.

+++



+++ Passaggio 1: configurare l’URL di invio del modulo

**Scopo**: invii diretti di moduli all’istanza AEM

**Posizione del file**: `blocks/form/constant.js` nel progetto Edge Delivery Services

**Esempi di configurazione:**

```javascript
// Production Environment
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';

// Local Development Environment  
export const submitBaseUrl = 'http://localhost:4503';

// Staging Environment
export const submitBaseUrl = 'https://publish-staging-p120-e12.adobeaemcloud.com';
```

**Punto di controllo della convalida:**

- File `constant.js` aggiornato con l’URL di pubblicazione AEM corretto
- L’URL corrisponde all’ambiente (produzione, stagin o locale)
- Nessuna barra finale nell’URL

+++



+++ Passaggio 2: configurare le impostazioni CORS

**Scopo**: consentire richieste di invio dei moduli da domini Edge Delivery Services

**Implementazione**: aggiungi la configurazione CORS alla configurazione di AEM Dispatcher o Apache

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**Punto di controllo della convalida:**

- Regole CORS applicate alla configurazione del dispatcher
- Sono inclusi tutti i domini richiesti (localhost, hlx.page, hlx.live)
- Configurazione distribuita nell’ambiente di destinazione

**Documentazione di riferimento:**

- [Guida alla configurazione CORS](https://experienceleague.adobe.com/it/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [Documentazione sul filtro referrer](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ Passaggio 3: configurare il filtro referrer

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

**Raggruppamento della configurazione:**

- **`allow.empty`**: rifiuta le richieste senza intestazioni referrer
- **`allow.hosts.regexp`**: consente richieste da domini Edge Delivery Services
- **`filter.methods`**: applica il filtro a questi metodi HTTP
- **`exclude.agents.regexp`**: agenti utente esclusi dal filtro

**Punto di controllo della convalida:**

- Configurazione del filtro referrer distribuita tramite Cloud Manager
- Configurazione attiva nell’istanza di pubblicazione di AEM
- L’invio del modulo di test funziona dal dominio Edge Delivery Services
- L’invio di moduli da parte di domini non autorizzati è bloccato

**Documentazione di riferimento:**

- [Configurare il filtro referrer tramite Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### Fase 3: accedere al modulo pubblicato



+++ Struttura dell’URL per Edge Delivery Services

**Formato URL standard:**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**Componenti URL:**

- **`<branch>`**: nome ramo Git (in genere `main`)
- **`<repo>`**: nome archivio
- **`<owner>`**: nome utente o organizzazione GitHub
- **`<form_name>`**: nome del modulo (lettere minuscole, trattini)

**URL specifici dell’ambiente:**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ Passaggi di convalida finali

**Verificare l’accessibilità del modulo:**

1. **Testa il caricamento modulo**: visita l’URL del modulo e conferma che viene caricato correttamente
2. **Testa l’invio del modulo**: compila e invia il modulo per verificare l’elaborazione dei dati
3. **Testa progettazione reattiva**: testa il modulo su dispositivi e dimensioni dello schermo diversi
4. **Convalida la sicurezza**: verifica che il CORS e il filtro referrer funzionino correttamente

**Risultati previsti:**

- Il modulo viene caricato senza errori
- Il rendering di tutti i campi viene eseguito correttamente
- I processi di invio modulo sono completati correttamente
- I dati vengono visualizzati nella destinazione configurata (foglio di calcolo, e-mail, ecc.)
- Nessun errore della console correlato al CORS o ai criteri di sicurezza

+++


## Passaggi successivi


- [Configurare le azioni di invio dei moduli](/help/edge/docs/forms/universal-editor/submit-action.md)
- [Attribuire lo stile e il tema ai moduli](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [Creare layout di moduli reattivi](/help/edge/docs/forms/universal-editor/responsive-layout.md)
- [Aggiungere la protezione reCAPTCHA](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)



