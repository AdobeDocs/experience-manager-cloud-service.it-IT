---
title: Servizio di invio Forms per Edge Delivery Services
description: Memorizza gli invii dei moduli direttamente nei fogli di calcolo utilizzando il servizio di invio Forms in hosting di Adobe. Scopri la configurazione, l’utilizzo delle API e la configurazione per l’integrazione di Google Sheets, OneDrive e SharePoint.
keywords: Servizio di invio Forms, Edge Delivery Services Forms, integrazione foglio di calcolo, moduli Google Sheets, moduli OneDrive, moduli SharePoint, raccolta dati moduli
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: ae423010910f66cd5e35ad8bd6b0c077d5bbda97
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 1%

---

# Servizio di invio Forms per Edge Delivery Services

Il servizio di invio Forms è la soluzione ospitata di Adobe che memorizza automaticamente i dati di invio dei moduli direttamente nei fogli di calcolo preferiti: Google Sheets, Microsoft OneDrive o SharePoint. Questo elimina la necessità di complesse infrastrutture di back-end e fornisce al contempo la raccolta e la gestione dei dati in tempo reale.

## Panoramica

![Servizio di invio Forms](/help/forms/assets/form-submission-service.png)
*Figura: flusso di lavoro del servizio di invio Forms - dall&#39;invio del modulo all&#39;archiviazione del foglio di calcolo*

+++ Chi deve utilizzare questo servizio?

**Ideale per:**

- **Creatori di contenuti** creazione di semplici moduli di raccolta dati
- **Piccole aziende** che richiedono flussi di lavoro rapidi da modulo a foglio di calcolo
- **Team di marketing** che raccolgono informazioni sui lead
- **Organizzatori di eventi** che gestiscono le registrazioni

**Valuta alternative per:**

- Flussi di lavoro complessi che richiedono una logica personalizzata
- Integrazioni aziendali con i database
- Forms che necessita di convalida o elaborazione avanzata

+++

+++ Casi d’uso comuni

| Caso d’uso | Esempio | Vantaggi del foglio di calcolo |
|----------|---------|-------------------|
| **Contatta Forms** | Richieste di informazioni sul sito Web → fogli Google | Facile follow-up e importazione CRM |
| **Registrazione evento** | Iscrizioni conferenze → Excel Online | Tracciamento dei partecipanti in tempo reale |
| **Generazione lead** | Iscrizioni newsletter → SharePoint | Analisi di una campagna di marketing |
| **Raccolta feedback** | Risposte ai sondaggi → fogli Google | Visualizzazione dati rapida |

+++

## Vantaggi principali

Il servizio di invio Forms offre diversi vantaggi per una raccolta dati semplificata:

+++ Configurazione semplificata

- **Non è richiesta alcuna infrastruttura di back-end** - Adobe ospita l&#39;endpoint di invio
- **Integrazione diretta** con piattaforme di fogli di calcolo più diffuse
- **Mappatura automatica dei dati** dai campi modulo alle colonne del foglio di calcolo

+++


+++ Gestione dei dati in tempo reale

- **Acquisizione immediata dei dati** - gli invii vengono visualizzati immediatamente nel foglio di calcolo
- **Archiviazione strutturata**: colonne organizzate per analisi semplificate
- **Collaborazione in tempo reale** - più membri del team possono accedere e analizzare i dati

+++

+++ Sicurezza e controllo degli accessi integrati

- **Sfrutta le autorizzazioni esistenti** - utilizza i controlli di condivisione della piattaforma del foglio di calcolo
- **Sicurezza gestita da Adobe** - endpoint di invio sicuro con protezione di livello enterprise
- **Proprietà dei dati**: i dati rimangono nella piattaforma del foglio di calcolo scelta

+++

## Prerequisiti

Prima di configurare il servizio di invio Forms, verificare di disporre dei seguenti elementi:



+++ Requisiti tecnici

- **Archivio GitHub** configurato per il progetto Edge Delivery Services con il blocco Forms adattivo più recente installato
- **Approvazione dell&#39;accesso** - repository aggiunto al inserisco nell&#39;elenco Consentiti di

+++

+++ Configurazione piattaforma foglio di calcolo


Scegli una delle piattaforme supportate:

- **Fogli Google** - Account Google con autorizzazioni per la creazione di fogli
- **Microsoft OneDrive** - Account Microsoft 365 con accesso a Excel Online
- **SharePoint** - Accesso a SharePoint con autorizzazioni elenco/raccolta

+++

+++ Autorizzazioni e accesso

- **Modifica autorizzazioni** per il foglio di calcolo di destinazione
- **Funzionalità di condivisione** per concedere l&#39;accesso a `forms@adobe.com`
- **Autorizzazioni generazione collegamenti** per la piattaforma scelta

+++

>[!TIP]
>
>**Ti avvicini ora a Edge Delivery Services?** Inizia con l&#39;[esercitazione introduttiva](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial) per configurare le basi del progetto.

## Metodi di configurazione

Il servizio di invio Forms offre due approcci di configurazione. Scegli il metodo più adatto al tuo flusso di lavoro:


+++ Scegli il metodo di configurazione

| Metodo | Ideale per | Tempo richiesto | Livello tecnico |
|--------|----------|---------------|-----------------|
| **[Installazione manuale](#manual-configuration)** | Creatori di contenuti, configurazione una tantum | 10-15 minuti | Principiante |
| **[Configurazione API](#api-configuration)** | Sviluppatori, flussi di lavoro automatizzati | 5-10 minuti | Intermedio |

+++

+++ Configurazione del progetto

Prima di configurare uno di questi metodi, assicurati che le basi del progetto AEM siano pronte:

1. **Crea o aggiorna il progetto AEM** con il blocco Forms adattivo più recente ([Esercitazione introduttiva](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial))

2. **Aggiorna`fstab.yaml`** nella directory principale del progetto:

   ```yaml
   # Replace with the path to your shared folder
   mountpoints:
     /: https://drive.google.com/drive/folders/your-shared-folder-id
   ```


3. **Condividi la cartella del progetto** con `forms@adobe.com` (sono necessarie le autorizzazioni di modifica)

+++

+++

## Configurazione manuale

![Flusso di lavoro per il servizio di invio moduli](/help/forms/assets/forms-submission-service-workflow.png)
*Figura: flusso di lavoro completo per l&#39;installazione manuale del servizio di invio Forms*

Segui queste istruzioni dettagliate per configurare il modulo con l’invio di un foglio di calcolo:



+++ Passaggio 1: creare la definizione del modulo

Creare la struttura del modulo utilizzando Google Sheets o Microsoft Excel.

**Passaggi per la creazione del modulo:**

1. **Apri la piattaforma del foglio di calcolo** (fogli di Google o Microsoft Excel)
2. **Crea un nuovo foglio di calcolo** per il progetto modulo
3. **Denomina il foglio** (deve essere `helix-default` o `shared-aem`)
4. **Definisci la struttura del modulo** utilizzando la [guida alla creazione del modulo](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)

![Definizione modulo](/help/forms/assets/form-submission-definition.png)
*Esempio: definizione modulo con tipi di campo, etichette e regole di convalida*

>[!IMPORTANT]
>
>**Requisiti di denominazione dei fogli**
>
>Il foglio di definizione del modulo deve essere denominato:
>
>- `helix-default` (consigliato per moduli singoli)
>- `shared-aem` (per progetti multimodulo)
>
>Gli altri nomi di foglio non verranno riconosciuti dal sistema.

**Checkpoint di convalida:**

- Struttura del modulo completata con tutti i campi obbligatori
- Il foglio è denominato correttamente (`helix-default` o `shared-aem`)
- I tipi di campo e le regole di convalida sono configurati correttamente

+++

+++ Passaggio 2: creare il foglio di raccolta dati

Imposta un foglio dedicato per ricevere i dati di invio del modulo.

**Impostazione foglio dati:**

1. **Aggiungi un nuovo foglio** al foglio di calcolo esistente
2. **Denomina il foglio esattamente`incoming`** (distinzione maiuscole/minuscole)
3. **Configura intestazioni di colonna** corrispondenti ai campi modulo
4. **Salvare il foglio di calcolo** per assicurarsi che le modifiche vengano mantenute

![Foglio in ingresso](/help/forms/assets/form-submission-incoming-sheet.png)
*Esempio: foglio in ingresso con intestazioni di colonna corrispondenti ai campi modulo*

>[!WARNING]
>
>**Requisito critico**
>
>Il foglio deve essere denominato esattamente `incoming` (minuscolo). Senza questo foglio:
>
>- Gli invii dei moduli verranno rifiutati
>- Nessun dato verrà memorizzato
>- Gli utenti visualizzeranno gli errori di invio

**Checkpoint di convalida:**

- Il foglio `incoming` esiste nel tuo foglio di calcolo
- Le intestazioni di colonna corrispondono ai nomi dei campi modulo
- Il foglio è salvato correttamente e accessibile

>[!TIP]
>
>**Suggerimento pro:** copia i nomi di campo esatti dalla definizione del modulo per garantire una corrispondenza perfetta tra i campi modulo e le colonne del foglio di calcolo.

+++

+++ Passaggio 3: condividere un foglio di calcolo con Adobe Service

Concedi al servizio Adobe Forms Submission l’accesso al tuo foglio di calcolo.

**Processo di condivisione:**

1. **Fai clic sul pulsante Condividi** nell&#39;angolo superiore destro del foglio di calcolo
2. **Aggiungere l&#39;account del servizio Adobe:**
   - E-mail: `forms@adobe.com`
   - Livello di autorizzazione: **Editor** (obbligatorio per la scrittura dei dati)
3. **Invia l&#39;invito alla condivisione**
4. **Copia il collegamento del foglio di calcolo** per il passaggio successivo

   ![Condividi foglio in ingresso](/help/forms/assets/form-submission-share-incoming.png)
   *Processo di condivisione passo per passo per concedere l&#39;accesso al servizio Adobe*

**Istruzioni Specifiche Per La Piattaforma:**

**Fogli Google:**

- Aggiungi `forms@adobe.com` come editor
- Verificare che sia abilitato &quot;Chiunque disponga del collegamento può visualizzare&quot;
- Copia il collegamento condivisibile

**Microsoft Excel (OneDrive/SharePoint):**

- Aggiungi `forms@adobe.com` con autorizzazioni di modifica
- Imposta la condivisione del collegamento su &quot;Chiunque abbia il collegamento può modificare&quot;
- Copia l’URL di condivisione

  ![Copia collegamento del foglio in ingresso](/help/forms/assets/form-submission-copy-link.png)
  *Esempio: copia del collegamento condivisibile per la configurazione del modulo*

**Checkpoint di convalida:**

- `forms@adobe.com` ha accesso editor al tuo foglio di calcolo
- Il collegamento al foglio di calcolo viene copiato e pronto per l&#39;uso
- Le autorizzazioni di condivisione consentono l&#39;accesso esterno

+++

+++ Passaggio 4: connettere il modulo al foglio di calcolo

Collegare la definizione del modulo al foglio di calcolo di invio.

**Connessione Foglio Di Calcolo Modulo:**

1. **Apri il foglio di calcolo di definizione modulo** (quello con `helix-default` o `shared-aem` foglio)
2. **Individua la riga del campo Invia** nella definizione del modulo
3. **Incolla il collegamento del foglio di calcolo copiato** nella colonna **Azione** per il campo Invia
4. **Salva le modifiche** nella definizione del modulo

   ![Collega un foglio di calcolo](/help/forms/assets/form-submission-sheet-linking.png)

*Esempio: connessione dell&#39;azione di invio al foglio di calcolo della raccolta dati*

**Pubblicazione del modulo:**

1. **Apri AEM Sidekick** nel browser
2. **Visualizza l&#39;anteprima del modulo** per verificare la configurazione
3. **Pubblica il modulo** per renderlo attivo

**Convalida finale:**

- Il collegamento al foglio di calcolo viene aggiunto correttamente all’azione Invia campo
- La definizione del modulo viene salvata e pubblicata
- L’anteprima del modulo mostra correttamente tutti i campi
- Il pulsante Invia è configurato correttamente

>[!SUCCESS]
>
>**Installazione completata.** Il modulo è ora connesso al servizio di invio Forms. Testarlo inviando i dati di esempio e controllando il foglio `incoming`.

**Materiale di riferimento:**

- [Completare il foglio di calcolo di esempio](/help/forms/assets/spreadsheet.xlsx) con la configurazione corretta
- [Documentazione di AEM Sidekick](https://www.aem.live/docs/sidekick) per istruzioni sulla pubblicazione

+++

## Configurazione API

Il metodo API consente agli sviluppatori di inviare in modo programmatico i dati al servizio di invio Forms, ideale per flussi di lavoro automatizzati e integrazioni personalizzate.


+++ Quando utilizzare l’API

**Ideale per:**

- Sistemi automatizzati di raccolta dati
- Implementazioni di moduli personalizzati
- Integrazione con le applicazioni esistenti
- Flussi di lavoro per l’invio di dati in blocco

+++

+++ Prerequisiti API

Prima di utilizzare l’API, assicurati di disporre di:

- **Configurazione foglio di calcolo** completata (inclusi `incoming` fogli)
- **Accesso al servizio Adobe** concesso a `forms@adobe.com`
- **ID modulo** dal modulo pubblicato
- **Informazioni archivio** (nome organizzazione e sito)

>[!IMPORTANT]
>
>**Passaggi di installazione necessari**
>
>L’API richiede la stessa configurazione manuale del foglio di calcolo:
>
>- Il foglio `incoming` deve esistere
>- `forms@adobe.com` deve avere accesso come editor
>- Il foglio deve essere pubblicato tramite AEM Sidekick

+++

+++ Endpoint API e autenticazione

**URL di base:** `https://forms.adobe.com/adobe/forms/af/submit/{id}`

**Intestazioni richieste:**

- `Content-Type: application/json`
- `x-adobe-routing: tier=live,bucket=main--[repository]--[organization]`

**Documentazione API:** [Riferimento API completo](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)

+++

+++ Utilizzo di Postman

Postman fornisce un’interfaccia intuitiva per testare gli invii API.

**Istruzioni di installazione:**

1. **Crea una nuova richiesta POST** in Postman
2. **Configura l&#39;endpoint:** `https://forms.adobe.com/adobe/forms/af/submit/{id}`
3. **Sostituisci segnaposto:**
   - `{id}` → l&#39;ID modulo effettivo
   - `[repository]` → nome archivio GitHub
   - `[organization]` → nome utente/organizzazione GitHub

**Configurazione richiesta:**

```json
POST https://forms.adobe.com/adobe/forms/af/submit/your-form-id

Headers:
Content-Type: application/json
x-adobe-routing: tier=live,bucket=main--your-repo--your-org

Body (JSON):
{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Mary",
            "age": "35",
            "subscribe": null,
            "email": "mary@gmail.com"
                }
}
```

**Risposta prevista:**

- **Codice stato:** `201 Created`
- **I dati vengono visualizzati** nel foglio di calcolo `incoming` immediatamente

![schermata postman](/help/forms/assets/postman-api.png)
*Esempio: invio API riuscito tramite interfaccia Postman*

+++

+++ Utilizzo della riga di comando (curl)

Per gli sviluppatori che preferiscono terminale/prompt dei comandi, utilizza curl per inviare i dati a livello di programmazione.

**Installazione riga di comando:**

Sostituisci i segnaposto seguenti nei comandi seguenti:

- `{id}` → l&#39;ID modulo effettivo
- `[repository]` → nome archivio GitHub
- `[organization]` → nome utente/organizzazione GitHub

>[!BEGINTABS]

>[!TAB macOS/Linux]

```bash
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" \
    --header "Content-Type: application/json" \
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" \
    --data '{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Joe",
            "age": "35",
            "subscribe": null,
      "email": "joe@example.com"
                }
            }'
```

>[!TAB Prompt dei comandi di Windows]

```cmd
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" ^
    --header "Content-Type: application/json" ^
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" ^
  --data "{\"data\": {\"startDate\": \"2025-01-10\", \"endDate\": \"2025-01-25\", \"destination\": \"Australia\", \"class\": \"First Class\", \"budget\": \"2000\", \"amount\": \"1000000\", \"name\": \"Joe\", \"age\": \"35\", \"subscribe\": null, \"email\": \"joe@example.com\"}}"
```

>[!TAB Windows PowerShell]

```powershell
$body = @{
  data = @{
    startDate = "2025-01-10"
    endDate = "2025-01-25"
    destination = "Australia"
    class = "First Class"
    budget = "2000"
    amount = "1000000"
    name = "Joe"
    age = "35"
    subscribe = $null
    email = "joe@example.com"
  }
} | ConvertTo-Json -Depth 3

Invoke-RestMethod -Uri "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" `
  -Method POST `
  -Headers @{"Content-Type"="application/json"; "x-adobe-routing"="tier=live,bucket=main--your-repo--your-org"} `
  -Body $body
```

>[!ENDTABS]

+++

+++ Risposta e verifica API

**Risposta corretta:**

```http
HTTP/1.1 201 Created
Connection: keep-alive
Content-Length: 0
X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
Date: Fri, 10 Jan 2025 13:06:10 GMT
Access-Control-Allow-Origin: *
```

**Verifica dati:**

Dopo un invio corretto, verifica che i dati vengano visualizzati nel foglio di calcolo:

![foglio aggiornato](/help/forms/assets/updated-sheet.png)
*Esempio: dati scritti correttamente nel foglio in ingresso tramite API*

**Convalida risposta:**

- **Stato HTTP:** `201 Created` indica invio completato
- **X-Request-Id:** Identificatore univoco per il tracciamento dell&#39;invio
- **Dati visualizzati** nel foglio `incoming` in pochi secondi
- **Tutti i campi modulo** sono mappati correttamente alle colonne del foglio di calcolo

+++

## Risoluzione di problemi



+++ Problemi comuni e soluzioni

**Problema: Errore 403 Non Consentito**

```
Causes: Missing or incorrect access permissions
Solutions:
- Verify forms@adobe.com has Editor access to your spreadsheet
- Check that your repository is added to the allowlist
- Confirm the x-adobe-routing header format
```

**Problema: Errore 404 Non Trovato**

```
Causes: Incorrect Form ID or endpoint URL
Solutions:  
- Verify your Form ID is correct
- Check the API endpoint URL format
- Ensure your form is published and live
```


**Problema: dati non visualizzati nel foglio di calcolo**

```
Causes: Missing 'incoming' sheet or permission issues
Solutions:
- Confirm 'incoming' sheet exists (case-sensitive)
- Verify column headers match form field names exactly
- Check forms@adobe.com has edit permissions
- Ensure spreadsheet is shared properly
```


**Problema: errore formato JSON non valido**

```
Causes: Malformed request body
Solutions:
- Validate JSON syntax using online JSON validators
- Ensure proper escaping of special characters
- Check quote marks and brackets are balanced
```


+++

+++ Ottenimento della Guida

**Canali di supporto:**

- **Problemi di accesso anticipato:** E-mail [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)
- **Documentazione API:** [Riferimento sviluppatore](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)
- **Supporto community:** [Community Adobe Experience League](https://experienceleaguecommunities.adobe.com/)

+++

## Passaggi successivi

Ora che hai configurato il servizio di invio Forms, scopri i seguenti argomenti correlati:


+++ Migliora il tuo Forms

- **[Crea Forms avanzato](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)** - Aggiungi convalida, logica condizionale e stile personalizzato
- **[Guida ai componenti del modulo](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-components)** - Esplora i tipi di campo modulo disponibili

+++

+++ Metodi di invio alternativi

- **[Invii di pubblicazione AEM](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)** - Per flussi di lavoro complessi e integrazioni aziendali
- **[Azioni di invio personalizzate](/help/forms/configure-submit-actions-core-components.md)** - Gestione avanzata dell&#39;invio

+++

+++ Gestione dati

- **[Analisi modulo](/help/forms/view-understand-aem-forms-analytics-reports.md)** - Monitora prestazioni e utilizzo modulo
- **[Integrazione dei dati](/help/forms/configure-data-sources.md)** - Connessione dei moduli a database e sistemi di gestione delle relazioni con i clienti

+++

## Riepilogo

Il servizio di invio Forms fornisce una soluzione potente e senza codice per la raccolta dei dati del modulo direttamente nei fogli di calcolo. I vantaggi principali includono:

- **Configurazione rapida** - Nessuna infrastruttura di back-end richiesta
- **Dati in tempo reale** - Acquisizione immediata dell&#39;invio
- **Piattaforme flessibili** - Google Sheets, OneDrive o SharePoint
- **Accesso API** - Funzionalità di invio programmatiche
- **Sicurezza aziendale** - Endpoint gestiti da Adobe con controlli di accesso

**Inizio?** Segui la [guida alla configurazione manuale](#manual-configuration) per una configurazione visiva, oppure passa alla [configurazione API](#api-configuration) per l&#39;integrazione programmatica.
