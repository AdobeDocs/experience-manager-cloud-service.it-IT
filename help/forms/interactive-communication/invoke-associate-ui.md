---
title: Richiama un’interfaccia utente di associazione nell’istanza Publish
description: Scopri come integrare e richiamare l’interfaccia utente di AEM Forms Associate sulle istanze Publish per consentire ai professionisti che si rivolgono al cliente di generare comunicazioni interattive personalizzate in tempo reale.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
hidefromtoc: true
source-git-commit: bfee883205f81012fea75cbd7dc5fddd7169fdbb
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 2%

---


# Generare comunicazioni personalizzate con l’interfaccia utente associata

<span> La funzionalità di comunicazione interattiva è disponibile nel programma per l&#39;adozione anticipata. Invia un&#39;e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com` per richiedere l&#39;accesso.</span>

L’interfaccia utente Associa può essere richiamata direttamente sulle istanze Publish, consentendo a professionisti che si rivolgono al cliente, come associati sul campo e agenti di servizio, di generare comunicazioni personalizzate in tempo reale durante le interazioni con il cliente.

La tabella seguente illustra i vari scenari reali in cui l’interfaccia utente Associa può essere utilizzata per inviare messaggi personalizzati ai clienti:

| Settore | Caso d’uso |
|----------|----------|
| **Servizi finanziari** | Generare lettere di conferma del prestito in tempo reale, rendiconti dei conti e riepiloghi dei profili di rischio durante le riunioni con i clienti |
| **Assicurazione** | Produrre immediatamente le carte di prova di assicurazione e i riepiloghi di smaltimento delle richieste di risarcimento presso i banchi assistenza |
| **Assistenza sanitaria** | Creare riepiloghi del piano di trattamento del paziente con quantità e pianificazioni aziendali calcolate |
| **Pubblica amministrazione** | Generare sul posto report di verifica della polizia, ricevute dei servizi ai cittadini e riepiloghi degli aggiornamenti dei casi |

## Prerequisiti

Prima di integrare l’interfaccia utente Associa all’applicazione, assicurati di disporre di:

- Comunicazione interattiva creata e pubblicata
- Browser con supporto per popup abilitato
- Associa [&#x200B; utenti deve far parte del gruppo forms-associates](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups)
- Autenticazione configurata utilizzando qualsiasi meccanismo di autenticazione [supportato da AEM](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/authentication/authentication) (ad esempio, gestori di autenticazione SAML 2.0, OAuth o personalizzati)

>[!NOTE]
>
>- In questo articolo viene illustrata la configurazione dell&#39;autenticazione utilizzando SAML 2.0 con [Microsoft Entra ID (Azure AD) come provider di identità](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings).
>- Per Associate UI (Interfaccia utente associata), sono necessarie ulteriori configurazioni SAML oltre alla configurazione standard descritta nell&#39;articolo [SAML 2.0 authentication](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/authentication/saml-2-0) (Autenticazione SAML 2.0). Per ulteriori informazioni, vedere la sezione [Configurazioni SAML aggiuntive per l&#39;interfaccia utente associata](#additional-saml-configurations-for-associate-ui).

### Configurazioni SAML aggiuntive per l’interfaccia utente associata

Quando configuri l’autenticazione SAML 2.0 per l’interfaccia utente Associate, devi applicare le seguenti impostazioni specifiche nei file di configurazione OSGi.

#### Gestore autenticazione SAML

Crea il file `com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json` in `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login"
    "idpUrl": "https://login.microsoftonline.com/{azure-tenant-id}/saml2",
    "idpCertAlias": "{your-certificate-alias}",
    "idpIdentifier": "https://sts.windows.net/{azure-tenant-id}/",
    "userIDAttribute": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
    "createUser": true,
    "userIntermediatePath": "saml",
    "synchronizeAttributes": [
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname=profile/givenName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname=profile/familyName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress=profile/email"
      ],
      "addGroupMemberships": true,
      "defaultGroups": ["forms-associates"],
      "defaultRedirectUrl": "/libs/fd/associate/ui.html",
      "idpHttpRedirect": false,
      "service.ranking": 5002
  }
```

| Proprietà | Descrizione |
|----------|-------------|
| `path` | Deve essere impostato su `/libs/fd/associate` per Associate UI |
| `defaultGroups` | Imposta su `forms-associates` per assegnare automaticamente gli utenti al gruppo richiesto |
| `defaultRedirectUrl` | Reindirizza gli utenti autenticati all&#39;interfaccia utente associata |
| `idpHttpRedirect` | Deve essere `false` per il flusso avviato da SP |
| `idpCertAlias` | Deve corrispondere esattamente all’alias del certificato nell’archivio fonti attendibili (distinzione maiuscole/minuscole) |

#### Autenticatore Sling

Aggiornare il file `org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json` in `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Filtro Dispatcher

Se non è già presente, aggiungere le regole seguenti al file `dispatcher/src/conf.dispatcher.d/filters/filters.any`:

```json
  # Allow Interactive Communications APIs and Associate UI
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/adobe/communications" }
  /XXXX { /type "allow" /method '(GET|POST|OPTIONS)' /url "/adobe/communications/*" }
  /XXXX { /type "allow" /method "GET" /url "/content/dam/fd:fonts/*" }
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/libs/fd/associate/*" }
```

>[!NOTE]
>
> Sostituisci `XXXX` con la sequenza numerica appropriata utilizzata nel file `filters.any` esistente.

## Richiamare l’interfaccia utente Associa nell’istanza di pubblicazione

Per richiamare l’interfaccia utente Associa dall’applicazione, configura l’URL dell’istanza Publish, prepara il payload dei dati e utilizza la funzione di integrazione per avviare l’interfaccia utente Associa in una nuova finestra del browser.

### Passaggio 1: configurare l’URL dell’istanza di pubblicazione

L’interfaccia utente Associa è accessibile tramite un endpoint specifico nell’istanza Publish di AEM Forms Cloud Service:

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

Sostituisci `{program-id}` e `{env-id}` con i valori effettivi dell&#39;ambiente.

Per motivi di sicurezza, parametri come l’ID comunicazione interattiva, il servizio di precompilazione e i parametri del servizio non vengono trasmessi attraverso l’URL. Al contrario, questi parametri vengono passati in modo sicuro utilizzando una funzione di JavaScript che comunica con l’interfaccia utente Associate tramite l’API postMessage del browser.

### Passaggio 2: preparare il payload dei dati

Struttura il payload dei dati con il seguente formato:

```javascript
const data = {
  id: "your-ic-id",              // Required: Interactive Communication ID
  prefill: {                      // Optional: Data to prefill the IC
    serviceName: "YourService",
    serviceParams: { key: "value" }
  },
  options: {}                     // Optional: Additional configuration options
};
```

**Componenti payload:**

| Componente | Obbligatorio | Descrizione |
|-----------|----------|-------------|
| `id` | Sì | Identificatore della comunicazione interattiva da caricare |
| `prefill` | Facoltativo | Contiene la configurazione del servizio per la precompilazione dei dati. |
| `prefill.serviceName` | Facoltativo | Nome del servizio Modello dati modulo da richiamare per la precompilazione dei dati |
| `prefill.serviceParams` | Facoltativo | Coppie chiave-valore passate al servizio di precompilazione |
| `options` | Facoltativo | Proprietà aggiuntive supportate per il rendering PDF: locale, includeAttachments, embedFonts, makeAccessible |

### Passaggio 3: implementare la funzione di integrazione

Crea una funzione JavaScript per avviare l’interfaccia utente Associa e gestire la comunicazione del messaggio:

```javascript
function launchAssociateUI(icId, prefillService, prefillParams, options) {
  if (!icId) {
    console.error('IC ID required');
    return;
  }
   
  const data = {
    id: icId,
    prefill: {
      serviceName: prefillService || '',
      serviceParams: prefillParams || {}
    },
    options: options || {}
  };
   
  const AEM_URL = 'https://your-aem.adobeaemcloud.com/libs/fd/associate/ui.html';
  const win = window.open(AEM_URL, '_blank');
   
  if (!win) {
    alert('Please enable pop-ups for this site');
    return;
  }
   
  const readyHandler = (event) => {
    if (event.data && event.data.type === 'READY' && event.data.source === 'APP') {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  };
   
  window.addEventListener('message', readyHandler);
   
  // Fallback timeout in case READY message is missed
  setTimeout(() => {
    if (win && !win.closed) {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  }, 1000);
}
```

### Passaggio 4: richiamare la funzione

Chiama la funzione con i parametri appropriati:

```javascript
// Basic invocation with IC ID only
launchAssociateUI('12345', '', {}, {});

// With prefill service
launchAssociateUI('12345', 'IC_FDM', 
  { customerId: '101'}, {});

// With all parameters
launchAssociateUI('12345', 'IC_FDM', 
  { customerId: "101" }, 
  { locale: 'en', includeAttachments: "true" });
```

## Pagina Test dell’integrazione con un esempio di HTML

Per osservare come viene visualizzata l’interfaccia utente Associa sul front-end e testare l’integrazione, ecco un semplice esempio di HTML. Questa pagina di esempio ti consente di inserire l’ID IC, configurare i parametri del servizio di precompilazione, impostare le opzioni di PDF e avviare l’interfaccia utente Associa nell’istanza Pubblica.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Associate UI Integration</title>
  <style>
    body { 
      font-family: sans-serif; 
      max-width: 600px; 
      margin: 50px auto; 
      padding: 20px; 
    }
    .form-group { 
      margin: 20px 0; 
    }
    label { 
      display: block; 
      margin-bottom: 5px; 
      font-weight: bold; 
    }
    input, textarea { 
      width: 100%; 
      padding: 8px; 
      border: 1px solid #ccc; 
      border-radius: 4px; 
      box-sizing: border-box;
    }
    textarea { 
      height: 80px; 
      font-family: monospace; 
    }
    button { 
      padding: 10px 20px; 
      margin: 5px; 
      cursor: pointer; 
      border-radius: 4px;
    }
    .btn-primary { 
      background: #007bff; 
      color: white; 
      border: none; 
    }
    .btn-primary:hover {
      background: #0056b3;
    }
    .error { 
      color: red; 
      font-size: 12px; 
      display: none; 
    }
  </style>
</head>
<body>
  <h1>Launch Associate UI</h1>
  
  <form id="form">
    <div class="form-group">
      <label>IC ID *</label>
      <input type="text" id="icId" placeholder="Enter Interactive Communication ID" required>
    </div>
    
    <div class="form-group">
      <label>Prefill Service</label>
      <input type="text" id="serviceName" placeholder="e.g., CustomerDataService">
    </div>
    
    <div class="form-group">
      <label>Service Parameters (JSON)</label>
      <textarea id="serviceParams" placeholder='{"customerId": "12345"}'>{}</textarea>
      <span id="paramsError" class="error">Invalid JSON format</span>
    </div>
    
    <div class="form-group">
      <label>Options (JSON)</label>
      <textarea id="options" placeholder='{"mode": "edit", "locale": "en_US"}'>{}</textarea>
      <span id="optionsError" class="error">Invalid JSON format</span>
    </div>
    
    <button type="button" onclick="reset()">Reset</button>
    <button type="button" class="btn-primary" onclick="launch()">Launch Associate UI</button>
  </form>

  <script>
    // Replace with your AEM Publish instance URL
    const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
    
    function validateJSON(str, errorId) {
      const err = document.getElementById(errorId);
      try {
        const obj = JSON.parse(str || '{}');
        err.style.display = 'none';
        return obj;
      } catch (e) {
        err.style.display = 'block';
        return null;
      }
    }
    
    function launch() {
      const icId = document.getElementById('icId').value.trim();
      if (!icId) { 
        alert('IC ID is required'); 
        return; 
      }
      
      const params = validateJSON(document.getElementById('serviceParams').value, 'paramsError');
      const opts = validateJSON(document.getElementById('options').value, 'optionsError');
      
      if (!params || !opts) { 
        alert('Please fix JSON errors before launching'); 
        return; 
      }
      
      const data = {
        id: icId,
        prefill: {
          serviceName: document.getElementById('serviceName').value.trim(),
          serviceParams: params
        },
        options: opts
      };
      
      const win = window.open(AEM_URL, '_blank');
      if (!win) { 
        alert('Pop-up blocked. Please enable pop-ups for this site.'); 
        return; 
      }
      
      const handler = (e) => {
        if (e.data && e.data.type === 'READY' && e.data.source === 'APP') {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      };
      
      window.addEventListener('message', handler);
      
      // Fallback timeout in case READY message is missed
      setTimeout(() => {
        if (win && !win.closed) {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      }, 1000);
    }
    
    function reset() {
      document.getElementById('form').reset();
      document.getElementById('serviceParams').value = '{}';
      document.getElementById('options').value = '{}';
      document.getElementById('paramsError').style.display = 'none';
      document.getElementById('optionsError').style.display = 'none';
    }
  </script>
</body>
</html>
```

### Funzionamento del campione

1. **Campo ID IC**: immettere l&#39;identificatore di comunicazione interattiva (obbligatorio)
2. **Servizio di precompilazione**: specificare il nome del servizio del modello dati modulo per la precompilazione dei dati
3. **Parametri del servizio**: immettere l&#39;oggetto JSON con i parametri da passare al servizio di precompilazione
4. **Opzioni**: immettere le opzioni di configurazione per PDF, ad esempio lingua, includeAttachments, embedFonts, makeAccessible
5. **Pulsante di avvio**: apre l&#39;interfaccia utente Associa in una nuova finestra e invia i dati di inizializzazione

## Esempi di payload dei dati

### Payload minimo (solo IC)

Utilizza questa opzione quando non sono necessari dati di precompilazione:

```json
{
  "id": "12345",
  "prefill": { 
    "serviceName": "", 
    "serviceParams": {} 
  },
  "options": {}
}
```

### Con dati di preriempimento

Utilizza questa opzione per popolare dinamicamente l’IC con i dati del cliente:

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": {}
}
```

### Con configurazione opzioni

Utilizzate questa opzione per specificare ulteriori opzioni di rendering:

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": { 
      locale: "en_US",
      includeAttachments: "true",
      webOptimized: "false",
      embedFonts: "false",
      makeAccessible: "false"
  }
}
```

## Risoluzione dei problemi

### Popup bloccato

**Problema**: la finestra Associa interfaccia utente non si apre.

**Soluzione**:
- Abilitare i popup per il dominio nelle impostazioni del browser
- Assicurarsi che `window.open()` sia chiamato da un&#39;azione dell&#39;utente (ad esempio, clic sul pulsante)
- Esegui il test con browser diversi per identificare il comportamento di blocco

### Dati non caricati

**Problema**: la comunicazione interattiva si apre ma i dati non si popolano.

**Soluzione**:
- Verificare che l&#39;ID IC sia corretto e che l&#39;IC sia pubblicato
- Verifica la presenza di errori JavaScript nella console del browser
- Assicurarsi che la struttura `postMessage` corrisponda esattamente alla specifica
- Verifica che il servizio Modello dati modulo sia configurato correttamente

### Errore di autenticazione

**Problema**: l&#39;utente riceve un errore di autenticazione all&#39;apertura dell&#39;interfaccia utente Associate.

**Soluzione**:
- Configurare l’autenticazione SAML 2.0 nell’istanza Publish
- Verifica che l&#39;utente faccia parte del gruppo **forms-associates**
- Controlla impostazioni di timeout sessione

### Errori CORS

**Problema**: errori di condivisione risorse tra le origini nella console.

**Soluzione**:
- Per lo sviluppo: utilizzare `'*'` come origine di destinazione in `postMessage`
- Per la produzione: specifica l’URL di origine esatto dell’applicazione
- Assicurati che le impostazioni CORS dell’istanza di pubblicazione consentano il dominio dell’applicazione

<!--## Best Practices

When implementing the Associate UI integration, follow these best practices:

1. **Validation**: Always validate the IC ID and JSON payload before sending
2. **Error Handling**: Implement proper error handling for `window.open()` failures
3. **User Experience**: Display a loading indicator while the Associate UI initializes
4. **Memory Management**: Remove event listeners after initialization to prevent memory leaks
5. **Testing**: Test the integration with popup blockers enabled to ensure graceful handling
6. **User Permissions**: Verify users have appropriate access to the forms-associates group-->

## Consulta anche

- [Associate UI in Interactive Communication Editor](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Comunicazioni interattive su Cloud](/help/forms/early-access-ea-features.md#interactive-communications-on-cloud)
- [Funzioni di accesso anticipato](/help/forms/early-access-ea-features.md)