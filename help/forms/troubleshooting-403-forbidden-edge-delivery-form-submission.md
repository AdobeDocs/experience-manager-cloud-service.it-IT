---
title: Risoluzione dei problemi relativi a errori non consentiti 403 nell’invio di Edge Delivery Services Form
description: Scopri come diagnosticare e risolvere gli errori 403 Forbidden durante l’invio di moduli da Edge Delivery Services a AEM Publish. Questa guida descrive le cause più comuni, tra cui CORS, regole di Dispatcher e problemi relativi al filtro Referrer.
feature: Edge Delivery Services
role: Admin, Developer
exl-id: f397e059-f1b3-4afa-bd38-8f5fc591bb22
source-git-commit: d457bf9af377176222c2b96816fbbc4265e6b167
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 3%

---

# Risoluzione dei problemi relativi a errori non consentiti 403 nell’invio di Edge Delivery Services Form {#troubleshooting-403-forbidden-edge-delivery}

Durante l&#39;invio dei moduli da Edge Delivery Services a AEM Publish, è possibile che si verifichi un errore **403 Forbidden**. Questo errore indica che il server rifiuta di elaborare la richiesta, in genere a causa di configurazioni di sicurezza. Questo articolo ti aiuta a identificare e risolvere le cause più comuni di questo problema.

## Descrizione del problema

Gli utenti rilevano un errore **403 Forbidden** durante l&#39;invio dei moduli da Edge Delivery Services a AEM Publish. L’errore viene visualizzato come:

- Codice di stato HTTP: 403
- Messaggio di errore: &quot;Non consentito&quot; o &quot;Accesso negato&quot;
- L’invio del modulo non riesce senza raggiungere il servlet di invio di AEM

Questo problema si verifica in genere nelle integrazioni Edge Delivery Services in cui i moduli ospitati nei domini Edge (`.aem.live`, `.aem.page`, `.hlx.page`, `.hlx.live`) tentano di inviare dati alle istanze AEM Publish.

>[!IMPORTANT]
>
>Con le impostazioni di replica, è possibile ospitare più siti utilizzando lo stesso archivio. Ogni dominio del sito deve essere aggiunto singolarmente ai inserisce nell&#39;elenco Consentiti di invio dei moduli per funzionare correttamente.
>
>**Esempio:**
>
>- Archivio: `https://github.com/adobe/abc`
>- Sito 1: `main--abc--adobe.aem.live`
>- Sito 2: `main--abc1--adobe.aem.live`
>
>Entrambi i domini richiedono voci di inserisco nell&#39;elenco Consentiti separate per l’invio dei moduli da entrambi i siti.

## Cause comuni e soluzioni

Un errore 403 Forbidden nell’invio di un modulo Edge Delivery Services può avere più cause. Segui questi passaggi per la risoluzione dei problemi, nell’ordine in cui:

### &#x200B;1. Problemi CORS (Cross-Origin Resource Sharing)

**Sintomi:**

- La console del browser mostra i messaggi di errore relativi a CORS
- La scheda Rete mostra la richiesta bloccata prima di raggiungere il server
- Messaggi di errore che fanno riferimento a &quot;Richiesta tra origini bloccata&quot;

**Diagnosi:**

1. Apri gli strumenti per sviluppatori del browser (F12)
2. Controlla la scheda Console per i messaggi di errore CORS
3. Cerca messaggi come: `Access to fetch at 'https://publish-xxx.adobeaemcloud.com' from origin 'https://main--repo--owner.aem.live' has been blocked by CORS policy`

**Soluzione:**
Configura le impostazioni CORS in AEM per consentire le richieste dai domini del sito Edge Delivery specifici:

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Sites - Add each site domain individually
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true

# Legacy Franklin domains (if still in use)
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>Sostituisci `main--abc--adobe.aem.live` e `main--abc1--adobe.aem.live` con i tuoi domini del sito effettivi. Ogni sito ospitato dallo stesso archivio richiede una voce di configurazione CORS separata.

Per informazioni dettagliate sulla configurazione CORS, consulta la [Guida alla configurazione CORS](https://experienceleague.adobe.com/it/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).

### &#x200B;2. Regole Dispatcher

**Sintomi:**

- L’errore 403 si verifica senza messaggi CORS nella console del browser
- La richiesta raggiunge il server ma è bloccata da Dispatcher
- L’errore si verifica prima di raggiungere il livello dell’applicazione AEM

**Diagnosi:**

1. Verifica se l’URL della richiesta corrisponde a qualsiasi regola del filtro Dispatcher
2. Esamina la configurazione di Dispatcher per `/filter` regole che potrebbero bloccare le richieste POST
3. Verifica che l’endpoint per l’invio del modulo sia consentito nella configurazione di Dispatcher

**Soluzione:**
Aggiorna la configurazione di Dispatcher per consentire le richieste di invio del modulo:

1. Verificare che le richieste POST agli endpoint di invio del modulo siano consentite
2. Aggiungere regole di filtro appropriate per i domini Edge Delivery
3. Verifica che il percorso del servlet di invio non sia bloccato

Esempio di configurazione del filtro Dispatcher:

```apache
/filter {
  # Allow POST requests to form submission servlet
  /0100 { /type "allow" /method "POST" /url "/content/forms/af/*" }
  /0101 { /type "allow" /method "POST" /url "/adobe/forms/af/submit/*" }
  /0102 { /type "allow" /method "POST" /url "/content/forms/portal/submit/adaptiveform" }
}
```

### &#x200B;3. Problemi relativi al filtro referrer

**Sintomi:**

- Errore 403 senza problemi CORS nella console del browser
- La richiesta raggiunge AEM ma viene rifiutata dal filtro Sling Referrer
- Si verifica un errore a livello dell’applicazione AEM

**Diagnosi:**
Controlla i registri di errore di AEM per i messaggi di rifiuto del filtro Referrer:

1. [Accedere ai registri di AEM Cloud Service tramite Cloud Manager](/help/implementing/cloud-manager/manage-logs.md)
2. Cercare le voci in `aemerror.log` contenenti:
   - &quot;Filtro referrer rifiutato&quot;
   - &quot;org.apache.sling.security.impl.ReferrerFilter&quot;
   - Messaggi che indicano errori di convalida del referente

**Voce di registro di esempio:**

```
[ERROR] org.apache.sling.security.impl.ReferrerFilter Referrer filter rejected request with referrer 'https://main--abc--adobe.aem.live' for POST /content/forms/af/submit
```

**Soluzione:**
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

>[!IMPORTANT]
>
>**Per le impostazioni di repoless:** È necessario aggiungere ogni dominio del sito singolarmente all&#39;array `allow.hosts`. L’utilizzo di soli modelli regex potrebbe non essere sufficiente per tutti gli scenari. Includi domini specifici e modelli regex per una copertura completa.

>[!WARNING]
>
>Il filtro referrer di AEM non è un factory di configurazione OSGi, il che significa che è attiva solo una configurazione alla volta su un servizio AEM. Quando possibile, evita di aggiungere configurazioni personalizzate del filtro Referrer, in quanto sovrascriveranno le configurazioni native di AEM e potrebbero interrompere le funzionalità del prodotto.

## Passaggi diagnostici

Segui questi passaggi per identificare la causa specifica dell’errore 403:

### Passaggio 1: controllare la console del browser

1. Apri gli strumenti per sviluppatori del browser (F12)
2. Passa alla scheda Console
3. Tenta invio modulo
4. Cercare messaggi di errore relativi a CORS

**Se sono presenti errori CORS:** Segui la soluzione CORS precedente.
**In assenza di errori CORS:** Procedere con il passaggio 2.

### Passaggio 2: selezionare la scheda Rete

1. Apri gli strumenti per sviluppatori del browser (F12)
2. Passa alla scheda Rete
3. Tenta invio modulo
4. Controlla i dettagli della richiesta non riuscita
5. Esaminare le intestazioni di risposta e lo stato

**Se la richiesta non raggiunge il server:** È probabile che si tratti di un problema di Dispatcher.
**Se la richiesta raggiunge il server ma non riesce:** Probabile problema con il filtro Referrer.

### Passaggio 3: controllare i registri di AEM

1. Accesso a Cloud Manager
2. Accedere agli ambienti → i registri → dell’ambiente
3. Scarica o visualizza `aemerror.log`
4. Cerca voci al momento dell&#39;invio del modulo
5. Cerca il filtro Referrer o i messaggi relativi alla sicurezza

## Prevenzione e best practice

### &#x200B;1. Configurazione corretta durante l&#39;installazione

- Configurare le impostazioni CORS, Dispatcher e Referrer Filter durante la configurazione iniziale di Edge Delivery Services
- inserire nell&#39;elenco Consentiti **Per ogni nuovo sito:** Aggiungi il dominio specifico a tutti i (CORS, Referrer Filter)
- Test dell’invio dei moduli nell’ambiente di sviluppo prima della pubblicazione

### &#x200B;2. Configurazioni specifiche per l’ambiente

- Utilizzare configurazioni diverse per gli ambienti di sviluppo, staging e produzione
- Includi domini localhost per test di sviluppo locale
- **Documenta tutti i domini del sito** che devono inserire nell&#39;elenco Consentiti l&#39;accesso per il tuo archivio

### &#x200B;3. Monitoraggio e registrazione

- Imposta il monitoraggio del registro per i rifiuti del filtro Referrer
- Implementare la corretta gestione degli errori nel codice di invio del modulo
- Utilizzare gli strumenti per sviluppatori del browser durante il test

### &#x200B;4. Documentazione e conoscenze del team

- **Gestisci un Registro di sistema** di tutti i domini del sito che utilizzano lo stesso archivio
- Formazione del team di sviluppo sui passaggi di risoluzione dei problemi
- Gestisce un elenco di controllo per l&#39;impostazione di Edge Delivery Services Form
- inserire nell&#39;elenco Consentiti **Aggiorna** ogni volta che vengono creati nuovi siti dagli archivi esistenti

## Gestione del dominio del sito per le impostazioni di Repoless

Con le architetture Helix-5 e repoless, seguire queste linee guida:

### Durante la creazione di nuovi siti

1. **Identificare il dominio del sito** (ad esempio, `main--newsite--adobe.aem.live`)
2. **Aggiorna la configurazione CORS** per includere il nuovo dominio
3. **Aggiorna il filtro Referrer** per includere il nuovo dominio in `allow.hosts`
4. **Invio modulo di prova** dal nuovo sito
5. **Documenta il nuovo dominio** nel Registro di sistema del sito

### Modelli di denominazione dei domini

- Schema standard: `{branch}--{site}--{owner}.aem.live`
- Ogni sito ottiene un dominio univoco anche quando si condivide lo stesso archivio
- È possibile utilizzare entrambi i domini `.aem.live` e `.aem.page`

### Gestione configurazione

- Utilizza voci di dominio specifiche in `allow.hosts` per una maggiore sicurezza
- Supplemento con schemi regex per una copertura più ampia
- Controlla e aggiorna regolarmente i elenchi Consentiti man mano che i siti vengono aggiunti o rimossi

## Risorse aggiuntive

- [Configurazione del filtro Referrer con AEM Headless](/help/headless/deployment/referrer-filter.md)
- [Guida alla configurazione CORS](https://experienceleague.adobe.com/it/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [Informazioni sulla condivisione delle risorse tra le origini](https://experienceleague.adobe.com/it/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)
- [Documentazione di Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/publish-forms.md)

## Argomenti correlati

- [Configurazione delle azioni di invio](/help/forms/configuring-submit-actions.md)
- [Servizio di invio dei moduli](/help/forms/forms-submission-service.md)
- [Panoramica di Edge Delivery Services](/help/edge/overview.md)


**Hai bisogno di ulteriore assistenza?** Se riscontri ancora problemi dopo aver seguito questi passaggi di risoluzione dei problemi, contatta l&#39;Assistenza clienti Adobe con:

- Messaggi di errore specifici
- Dettagli dell’ambiente AEM Cloud Service
- **Tutti i domini del sito Edge Delivery Services** che richiedono l&#39;accesso per l&#39;invio del modulo
- Voci di registro rilevanti dal momento dell’errore

**Hai bisogno di ulteriore assistenza?** Se riscontri ancora problemi dopo aver seguito questi passaggi di risoluzione dei problemi, contatta l&#39;Assistenza clienti Adobe con:

- Messaggi di errore specifici
- Dettagli dell’ambiente AEM Cloud Service
- Informazioni sul dominio Edge Delivery Services
- Voci di registro rilevanti dal momento dell’errore
