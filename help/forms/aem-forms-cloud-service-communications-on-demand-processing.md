---
title: Come si configurano le API sincrone di comunicazione interattiva?
description: Configurare l’ambiente di sviluppo per le API sincrone di comunicazioni interattive per Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: cbf640e0c4643616638de96e9daa460cdcf2a4a5
workflow-type: tm+mt
source-wordcount: '2574'
ht-degree: 1%

---


# Elaborazione delle API sincrone di AEM Forms as a Cloud Service Communications

Questa guida fornisce istruzioni complete per la configurazione e l’utilizzo delle API sincrone di AEM Forms Communications.

Scopri come configurare l’ambiente AEM as a Cloud Service, abilitare l’accesso API e richiamare le API di comunicazione utilizzando l’autenticazione server-to-server OAuth.

## Prerequisiti

Per configurare un ambiente per l’esecuzione e il test delle API di comunicazione di AEM Forms, assicurati di disporre dei seguenti elementi:

### Accesso e autorizzazioni

Assicurati di disporre dei diritti di accesso e delle autorizzazioni necessari prima di iniziare a configurare le API di comunicazione.

**Autorizzazioni utente e ruolo**

- Adobe ID creato in [https://account.adobe.com/](https://account.adobe.com/)
- Adobe ID associato all’e-mail della tua organizzazione
- Contesto del prodotto Adobe Managed Services assegnato
- Ruolo Sviluppatore assegnato in Adobe Admin Console
- Autorizzazione per la creazione di progetti in Adobe Developer Console

>[!NOTE]
>
> Per ulteriori informazioni sull&#39;assegnazione di ruoli e sulla concessione dell&#39;accesso agli utenti, vedere l&#39;articolo [Aggiungere utenti e ruoli](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-manager/content/requirements/users-and-roles).

**Accesso a Cloud Manager**

- Credenziali di accesso per [Cloud Manager](https://my.cloudmanager.adobe.com)
- Accesso per visualizzare e gestire gli ambienti del programma
- Autorizzazione per creare ed eseguire pipeline CI/CD
- Accesso ai dettagli e alla configurazione dell’ambiente

**Accesso archivio Git**

- Accesso all’archivio Git di Cloud Manager
- Credenziali Git per la clonazione e il push delle modifiche

### Strumenti di sviluppo

- **Node.js** per eseguire applicazioni di esempio
- Versione più recente di **Git**
- Accesso a **Terminal/Riga di comando**
- **Editor di testo o IDE** per la modifica dei file di configurazione (codice VS, IntelliJ, ecc.)
- **Postman** o strumento simile per test API

>[!NOTE]
>
> Si tratta di un processo una tantum per ambiente che deve essere completato prima di procedere con la configurazione delle API di AEM Forms Communications.

Ora cerchiamo di capire ogni passo nel dettaglio.

### Passaggio 1: aggiornare l’istanza di AEM

Per aggiornare l’istanza di AEM:

1. **Accedi ad Adobe Cloud Manager**
   1. Passa a [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
   2. Accedi con il tuo Adobe ID

2. **Passa alla panoramica del programma**
   1. Seleziona il programma dall’elenco. Viene visualizzata la pagina Panoramica del programma

3. **Individua dettagli ambiente**
   1. Seleziona l&#39;icona `ellipsis`(...) accanto al nome dell&#39;ambiente e fai clic su **Aggiorna**
   2. Fai clic sul pulsante **Invia** ed esegui la pipeline full stack suggerita.

      ![Aggiorna ambiente](/help/forms/assets/update-env.png)

### Passaggio 2: clonare l’archivio Git

Clona l’archivio Git di Cloud Manager per gestire i file di configurazione API.

1. **Individua la sezione dell&#39;archivio**
   1. Nella pagina **Panoramica del programma**, fai clic sulla scheda **Archivi**
   2. Individua il nome dell’archivio e fai clic sul menu con i puntini di sospensione (...)
   3. Copia l’URL dell’archivio

      >[!NOTE]
      >
      > Il formato dell&#39;URL è in genere `https://git.cloudmanager.adobe.com/<org>/<program>/`

2. **Clona utilizzando il comando Git**

   1. Apri il prompt dei comandi o il terminale
   2. Eseguire il comando `git clone` per clonare l&#39;archivio Git.

      ```bash
      git clone [repository-url]
      ```

      >[!NOTE]
      >
      > Per clonare l’archivio Git, utilizza le credenziali fornite da Adobe Cloud Manager.

      Ad esempio, per clonare l’archivio Git, esegui il seguente comando:

      ```bash
      https://git.cloudmanager.adobe.com/formsinternal01/AEMFormsInternal-ReleaseSanity-p43162-uk59167/
      ```

      ![Clonazione dell&#39;archivio Git](/help/forms/assets/repo-clone.png)


**Opzioni di integrazione archivio Git**

Adobe Cloud Manager supporta entrambe le opzioni dell’archivio:

- **Utilizzo diretto dell&#39;archivio Git di Cloud Manager**
   - Usa archivio Git nativo di Cloud Manager
   - Integrazione integrata con le pipeline

- **Integrazione con l&#39;archivio Git gestito dal cliente**
   - Connetti il tuo archivio Git (GitHub, GitLab, Bitbucket, ecc.)
   - Configurare la sincronizzazione con Adobe Cloud Manager

Per ulteriori informazioni su come integrare Adobe Cloud Manager e Adobe Cloud Manager, consulta [Documentazione sull&#39;integrazione Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html).

### Passaggio 3: accedere all’ambiente AEM Cloud Service e all’endpoint AEM Forms

Accedi ai dettagli dell’ambiente AEM Cloud Service per ottenere gli URL e gli identificatori necessari per la configurazione API.

1. **Accedi ad Adobe Cloud Manager**
   1. Passa a [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
   2. Accedi con il tuo Adobe ID

2. **Passa alla panoramica del programma**
Seleziona il programma dall’elenco. Viene visualizzata la pagina Panoramica del programma

3. **Accedere e visualizzare l&#39;ambiente AEM Cloud Service**

   Puoi visualizzare o accedere ai dettagli dell’ambiente AEM Cloud Service utilizzando una delle due opzioni seguenti:

   - **Opzione 1: dalla pagina Panoramica**

      1. Nella pagina **Panoramica del programma**
      2. Fare clic su **&quot;Ambienti&quot;** nel menu a sinistra.  Puoi visualizzare un elenco di tutti gli ambienti

         ![Visualizza tutti gli ambienti](/help/forms/assets/all-env.png)

      3. Fai clic sul nome dell’ambiente specifico per visualizzare i dettagli

         ![Opzione1-Dettagli ambiente](/help/forms/assets/option1-env.png)

   - **Opzione 2: dalla sezione Ambienti**

      1. Nella pagina Panoramica del programma
      2. Individua la sezione **Ambienti**
      3. Fai clic su **&quot;Mostra tutto&quot;** per visualizzare tutti gli ambienti
      4. Fai clic sul menu **puntini di sospensione (...)** accanto all&#39;ambiente
         ![Opzione1-Dettagli ambiente](/help/forms/assets/option2-env-details.png)
      5. Selezionare **&quot;Visualizza dettagli&quot;**

         ![Opzione1-Dettagli ambiente](/help/forms/assets/option1-env.png)

4. **Trova Il Tuo Endpoint AEM Forms**

   Nella pagina dei dettagli **Ambiente**, prendere nota dei dettagli seguenti:

   **URL servizio Author**

   - URL: `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`
   - Bucket: author-pXXXXX-eYYYY
Esempio: `https://author-p43162-e177398.adobeaemcloud.com`

   **URL servizio di pubblicazione**

   - URL: `https://publish-pXXXXX-eYYYYY.adobeaemcloud.com`
   - Bucket: publish-pXXXXX-eYYYY
Esempio: `https://publish-author-p43162-e177398.adobeaemcloud.com`

>[!NOTE]
>
> Per informazioni su come accedere all&#39;ambiente AEM Cloud Service e all&#39;endpoint AEM Forms, consulta [Gestione della documentazione degli ambienti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=it).

### Passaggio 4: configurazione dell’accesso API

Per configurare le API di AEM Forms Communications, effettua le seguenti operazioni:

#### 4.1 Configurazione del progetto Adobe Developer Console

1. **Accedi a Adobe Developer Console**
   1. Passa a [Adobe Developer Console](https://developer.adobe.com/console)
   2. Accedi con il tuo Adobe ID

2. **Crea nuovo progetto**
   1. Dalla sezione **Guida rapida**, fai clic su **Crea nuovo progetto**
   2. Viene creato un nuovo progetto con un nome predefinito

      ![Crea progetto ADC](/help/forms/assets/adc-home.png)

   3. Fai clic su **Modifica progetto** nell&#39;angolo superiore destro

      ![Modifica progetto](/help/forms/assets/adc-edit-project.png)

   4. Fornisci un nome significativo (ad esempio, &quot;formsproject&quot;)
   5. Fai clic su **Salva**

      ![Modifica nome progetto](/help/forms/assets/adc-edit-projectname.png)

#### 4.2 Aggiungere API di comunicazione Forms

Puoi aggiungere diverse API di comunicazione di AEM Forms a seconda dei requisiti.

**A. Per le API di Document Services**

1. Fai clic su **Aggiungi API**

   ![Aggiungi API](/help/forms/assets/adc-add-api.png)

2. Seleziona **API di comunicazione Forms**
   1. Nella finestra di dialogo _Aggiungi API_, filtra per **Experience Cloud**
   2. Seleziona **&quot;API di comunicazione Forms&quot;**

   ![Aggiungi API di comunicazione Forms](/help/forms/assets/adc-add-forms-api.png)


3. Seleziona il metodo di autenticazione da server a server **OAuth**

   ![Seleziona metodo di autenticazione](/help/forms/assets/adc-add-authentication-method.png)

**B. Per le API di Forms Runtime**

1. **Fai clic su Aggiungi API**
   - Nel progetto, fai clic sul pulsante **Aggiungi API**

   ![Aggiungi API](/help/forms/assets/adc-add-api.png)

2. **Seleziona l&#39;API di AEM Forms Delivery e Runtime**
   - Nella finestra di dialogo _Aggiungi API_, filtra per **Experience Cloud**
   - Seleziona **&quot;AEM Forms Delivery and Runtime API&quot;**
   - Fai clic su **Avanti**

   ![Aggiungi API runtime](/help/forms/assets/add-runtime-api.png)


3. **Metodo di autenticazione**
   - Selezionare il metodo di autenticazione da server a server **OAuth**.


   ![Seleziona metodo di autenticazione](/help/forms/assets/add-authentication-for-runtime-apis.png)

#### 4.3 Aggiungi profilo prodotto

Per aggiungere il profilo di prodotto, segui la procedura riportata di seguito:

1. Seleziona il **profilo prodotto** appropriato in base al livello di accesso richiesto:

   | Tipo di accesso | Profilo prodotto |
   |------------------|----------------------|
   | Accesso in sola lettura | `AEM Users - author - Program XXX - Environment XXX` |
   | Accesso in lettura/scrittura | `AEM Assets Collaborator Users - author - Program XXX - Environment XXX` |
   | Accesso amministrativo completo | `AEM Administrators - author - Program XXX - Environment XXX` |

2. Seleziona il **profilo prodotto** che corrisponde all&#39;URL del servizio di authoring (`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`). Ad esempio: selezionare `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`.

3. Fai clic su **Salva API configurata**. L’API e il profilo di prodotto vengono aggiunti al progetto

   ![Seleziona configurazione progetto](/help/forms/assets/adc-add-product-profile.png)

#### 4.4 Generare e salvare le credenziali

1. **Accedi alle credenziali**

   1. Passare al progetto in Adobe Developer Console
   2. Fai clic sulle credenziali **OAuth Server-to-Server**
   3. Visualizza la sezione **Dettagli credenziali**

   ![Visualizza credenziali](/help/forms/assets/adc-view-credential.png)

2. **Registra credenziali API**

   ```text
   API Credentials:
   ================
   Client ID: <your_client_id>
   Client Secret: <your_client_secret>
   Technical Account ID: <tech_account_id>
   Organization ID: <org_id>
   Scopes: AdobeID,openid,read_organizations
   ```

#### 4.5 Generazione token di accesso

**A. Per test**

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
   > Il token di accesso è valido per **24 ore**

**B. Per la produzione**

Generare i token a livello di programmazione utilizzando l’API Adobe IMS:

**Credenziali richieste:**

- ID client
- Segreto client
- Ambiti (in genere: `AdobeID,openid,read_organizations`)

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

#### 4.6 Registrare l’ID client con l’ambiente AEM

Per abilitare l’ID client del progetto ADC per comunicare con l’istanza di AEM, devi registrarlo utilizzando un file di configurazione YAML e distribuirlo tramite una pipeline di configurazione.

1. **Individuare o creare la directory di configurazione**

   1. Passare all&#39;archivio dei progetti AEM clonato, passare alla cartella `config`
   2. Se non esiste, creala a livello di directory principale del progetto:

   ```bash
   mkdir config
   ```

2. Creare un nuovo file denominato `api.yaml` nella directory `config`:

   ```bash
   touch config/api.yaml
   ```

3. Aggiungi il seguente codice nel file `api.yaml`:

   ```yaml
   kind: "API"
   version: "1"
   metadata:
   envTypes: ["dev"]  # or ["prod", "stage"] for production environments
   data:
   allowedClientIDs:
       author:
       - "<your_client_id>"
       publish:
       - "<your_client_id>"
       preview:
       - "<your_client_id>"
   ```

   Di seguito vengono illustrati i parametri di configurazione:

   - **tipo**: sempre impostato su `"API"` (identifica questa come configurazione API)
   - **versione**: versione API, in genere `"1"` o `"1.0"`
   - **envTypes**: Array di tipi di ambiente in cui si applica questa configurazione
      - `["dev"]` - Solo ambienti di sviluppo
      - `["stage"]` - Solo ambienti di staging
      - `["prod"]` - Solo ambienti di produzione
   - **allowedClientIDs**: gli ID client possono accedere alla tua istanza di AEM
      - **author**: ID client per il livello di authoring
      - **publish**: ID client per il livello di pubblicazione
      - **anteprima**: ID client per il livello di anteprima

   Aggiungere ad esempio `allowedClientIDs` come `6bc4589785e246eda29a545d3ca55980` e envTypes come `dev`:

   ![Aggiunta del file di configurazione](/help/forms/assets/create-api-yaml-file.png)

4. **Commit e modifiche push**

   1. Passa alla cartella principale dell’archivio clonato ed esegui i seguenti comandi:


   ```bash
       git add config/api.yaml
       git commit -m "Whitelist client id for api invocation"
       git push origin <your-branch>
   ```

   ![Modifiche Git push](/help/forms/assets/push-yaml-changes-in-git.png)


5. **Configura pipeline**

   1. **Accedi a Cloud Manager**
      1. Passa a [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
      2. Accedi con il tuo Adobe ID

   2. **Accedi al programma**
Seleziona il programma dall’elenco e vieni reindirizzato alla pagina Panoramica del programma

   3. **Individua la scheda Pipeline**
      1. Individua la scheda **Pipeline** nella pagina Panoramica del programma
      1. Fare clic sul pulsante **&quot;Aggiungi&quot;**

   4. **Seleziona tipo di pipeline**

      - **Per Gli Ambienti Di Sviluppo**: Selezionare **&quot;Aggiungi Pipeline Non Di Produzione&quot;**. Le pipeline non di produzione sono per ambienti di sviluppo e stage

      - **Per Gli Ambienti Di Produzione**: Selezionare **&quot;Aggiungi Pipeline Di Produzione&quot;**. Le pipeline di produzione richiedono approvazioni aggiuntive

        >[!NOTE]
        >
        > In questo caso, crea una pipeline non di produzione poiché è disponibile un ambiente di sviluppo.

   5. **Configura pipeline - Scheda Configurazione**

      Nella scheda **Configurazione**:

      a. **Tipo di pipeline**
      - Seleziona **&quot;Pipeline di distribuzione&quot;**

      b. **Nome pipeline**
      - Specifica un nome descrittivo. Ad esempio, assegna alla pipeline il nome `api-config-pipieline`

      c. **Trigger distribuzione**
      - **Manuale**: distribuisci solo quando attivato manualmente (consigliato per la configurazione iniziale)
      - **Su modifiche Git**: distribuzione automatica quando le modifiche vengono inviate al ramo

      d. **Comportamento in caso di errori di metriche importanti**
      - **Chiedi ogni volta**: richiede un&#39;azione in caso di errori (impostazione predefinita)
      - **Genera errore immediatamente**: genera automaticamente un errore di pipeline in caso di errori di metrica
      - **Continua immediatamente**: continua nonostante gli errori

      e. Fare clic su **&quot;Continua&quot;** per passare alla scheda **Codice Source**

      ![Pipeline di configurazione](/help/forms/assets/add-config-pipeline.png)

   6. **Configura pipeline - Scheda Codice Source**

      Nella scheda **Codice Source**:

      a. **Tipo di distribuzione**
      - Seleziona **&quot;Distribuzione di destinazione&quot;**

      b. **Opzioni di distribuzione**
      - Selezionare **&quot;Config&quot;** (distribuire solo i file di configurazione). Indica a Cloud Manager che si tratta di una distribuzione di configurazione.

      c. **Seleziona ambiente di distribuzione idoneo**
      - Scegli l’ambiente in cui distribuire la configurazione. In questo caso, si tratta di un ambiente `dev`.

      d. **Definisci dettagli codice Source**

      - **Archivio**: selezionare l&#39;archivio contenente il file `api.yaml`. Selezionare ad esempio l&#39;archivio `AEMFormsInternal-ReleaseSanity-p43162-uk59167`.
      - **Ramo Git**: seleziona il ramo. Ad esempio, in questo caso il nostro codice viene distribuito nel ramo `main`.
      - **Posizione codice**: immettere il percorso della directory `config`. Poiché `api.yaml` si trova nella cartella principale `config`, immettere `/config`

      e. Fare clic su **&quot;Salva&quot;** per creare la pipeline

      ![Pipeline di configurazione](/help/forms/assets/confirm-pipeline-1.png)

6. **Distribuisci configurazione**

   Una volta creata la pipeline, distribuire la configurazione `api.yaml`:

   1. **Dalla panoramica delle pipeline**
      1. Nella pagina Panoramica del programma, individua la scheda **Pipeline**
      2. Passa alla nuova pipeline di configurazione creata nell’elenco. Ad esempio, cerca il nome della pipeline creata (ad esempio, &quot;api-config-pipeline&quot;). Puoi visualizzare i dettagli della pipeline, compreso lo stato e l’ultima esecuzione.

   2. **Avvia la distribuzione**
      1. Fai clic sul pulsante **&quot;Build&quot;** (o sull&#39;icona di riproduzione ▶) accanto alla pipeline
      2. Conferma la distribuzione se richiesto e l’esecuzione della pipeline inizia

      ![esegui la pipeline](/help/forms/assets/run-config-pipeline.png)

   3. **Verifica distribuzione completata**
      - Attendi il completamento della pipeline.
         - Se l&#39;operazione ha esito positivo, lo stato diventa &quot;Completato&quot; (segno di spunta verde ✓).
         - In caso contrario, lo stato diventa &quot;Non riuscito&quot; (croce rossa ✗). Fai clic su **Scarica registri** per visualizzare i dettagli dell&#39;errore.

           ![Pipeline completata](/help/forms/assets/pipeline-suceess.png)

      Ora puoi iniziare a testare le API di comunicazione di Forms. A scopo di test, puoi utilizzare Postman, curl o qualsiasi altro client REST per richiamare le API.

### Passaggio 5: specifiche e test delle API

Ora che il tuo ambiente è configurato, puoi iniziare a testare le API di comunicazione di AEM Forms utilizzando [Interfaccia utente Swagger](#a-using-swagger-ui-for-api-testing) o a livello di programmazione sviluppando l&#39;applicazione NodeJS.

In questo esempio generiamo un PDF utilizzando le API di Document Services utilizzando il modello e il file XDP.

#### A. Utilizzo dell’interfaccia utente Swagger per i test API

L&#39;interfaccia utente Swagger fornisce un&#39;interfaccia interattiva per testare le API senza scrivere codice.Utilizzare la funzionalità **Prova** per richiamare e testare l&#39;API di servizio documenti [generate PDF](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm).

1. Passa alla documentazione API
   - API Forms: [Riferimento API Forms](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)
   - Document Services: [Riferimento API per Document Services](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)
Apri la documentazione delle [API di Document Services](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document) nel browser.
2. Espandere la sezione **Generazione documento** e selezionare [Genera un modulo PDF compilabile da un modello XDP o PDF, facoltativamente con unione dati](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm).
3. Nel riquadro destro fare clic su **Prova**.

   ![Test Swagger per API](/help/forms/assets/api-doc-generation.png)
4. Immetti i seguenti valori:

   | **Sezione** | **Parametro** | **Valore** |
   |--------------|---------------|------------|
   | bucket | istanza AEM | Nome dell&#39;istanza di AEM senza il nome di dominio di Adobe (`.adobeaemcloud.com`). Utilizzare ad esempio `p43162-e177398` come bucket. |
   | Protezione | Token Bearer | Utilizza il token di accesso dalle credenziali server-to-server OAuth di Adobe Developer Console Project |
   | Corpo testo | Modello | Carica un XDP per generare il modulo PDF. Ad esempio, puoi utilizzare [questo XDP](/help/forms/assets/ClosingForm.xdp) per generare un PDF. |
   | Corpo testo | dati | File XML facoltativo contenente i dati da unire al modello per generare un modulo PDF precompilato. È ad esempio possibile utilizzare [questo XML](/help/forms/assets/ClosingForm.xml) per generare un PDF. |
   | Parametri | X-Adobe-Accept-Experimental | 1 |

5. Fai clic su **Invia** per richiamare l&#39;API

   ![Invia API](/help/forms/assets/api-send.png)

6. Controlla la risposta nella scheda **Risposta**:
   - Se il codice di risposta è `200`, significa che il PDF è stato creato correttamente.
   - Se il codice di risposta è `400`, significa che i parametri di richiesta non sono validi o non sono corretti.
   - Se il codice di risposta è `500`, significa che si è verificato un errore interno del server.

   In questo caso, il codice di risposta è `200`, significa che il PDF è stato generato correttamente:

   ![Rivedi risposta](/help/forms/assets/api-success.png)

   Ora puoi scaricare il [PDF creato](/help/forms/assets/create-pdf.pdf) utilizzando il pulsante **Scarica** e visualizzarlo nel visualizzatore PDF:

   ![Visualizza PDF](/help/forms/assets/create-pdf.png)

>[!NOTE]
>
> A scopo di test, puoi anche utilizzare [Postman](https://www.postman.com/), [curl](https://curl.se/) o qualsiasi altro client REST per richiamare le API di AEM.

#### B. Programmaticamente sviluppando l’applicazione NodeJS

Sviluppa un&#39;applicazione Node.js per generare un modulo PDF compilabile da un modello **XDP** e un file di dati **XML** utilizzando l&#39;API **Document Services**

##### Prerequisiti

- Node.js installato nel sistema
- Istanza AEM as a Cloud Service attiva
- Token Bearer per l’autenticazione API da Adobe Developer Console
- File XDP di esempio: [ClosingForm.xdp](/help/forms/assets/ClosingForm.xdp)
- File XML di esempio: [ClosingForm.xml](/help/forms/assets/ClosingForm.xml)

Per sviluppare l’applicazione Node.js, segui lo sviluppo passo passo:

##### Passaggio 1: creare un nuovo progetto Node.js

Apri il comando/terminale ed esegui i seguenti comandi:

```bash
# Create a new directory
mkdir demo-nodejs-generate-pdf
cd demo-nodejs-generate-pdf

##### Initialize Node.js project
npm init -y
```

![Crea nuovo progetto js del nodo](/help/forms/assets/api-1.png)

##### Passaggio 2: installare le dipendenze richieste

Installa le librerie **node-fetch**, **dotenv** e **form-data** per effettuare richieste HTTP, leggere le variabili di ambiente e gestire rispettivamente i dati del modulo.

```bash
npm install node-fetch
npm install dotenv
npm install form-data
```

![installa dipendenze npm](/help/forms/assets/api-2.png)

##### Passaggio 3: aggiornare package.json

1. Apri il comando/terminale ed esegui il comando:

   ```bash
   code .
   ```

   ![apri progetto nell&#39;editor](/help/forms/assets/api-3.png)

   Apre il progetto nell’editor di codice.

2. Aggiornare il file `package.json` per aggiungere `type` a `module`.

   ```bash
   {
   "name": "demo-nodejs-generate-pdf",
   "version": "1.0.0",
   "type": "module",
   "main": "index.js",
   }
   ```

   ![aggiorna file pacchetto](/help/forms/assets/api-4.png)

##### Passaggio 4: creare un file .env

1. Creare un file .env a livello di directory principale di un progetto
2. Aggiungi la seguente configurazione e sostituisci i segnaposto con i valori effettivi delle credenziali server-to-server OAuth del progetto ADC.

   ```bash
   CLIENT_ID=<ADC Project OAuth Server-to-Server credential ClientID>
   CLIENT_SECRET=<ADC Project OAuth Server-to-Server credential Client Secret>
   SCOPES=<ADC Project OAuth Server-to-Server credential Scopes>
   ```

   ![crea file di ambiente](/help/forms/assets/api-5.png)

   >[!NOTE]
   >
   > È possibile copiare `CLIENT_ID`, `CLIENT_SECRET` e `SCOPES` dal progetto Adobe Developer Console.

##### Passaggio 5: creare src/index.js

1. Crea il file `index.js` a livello di directory principale del progetto
2. Aggiungi il seguente codice e sostituisci i segnaposto con i valori effettivi:

```javascript
// Import the dotenv configuration to load environment variables from the .env file
import "dotenv/config";

// Import fetch for making HTTP requests
import fetch from "node-fetch";
import fs from "fs";
import FormData from "form-data";

// REPLACE THE FOLLOWING VALUE WITH YOUR OWN
const bucket = <bucket-value>; // Your AEM Cloud Service Bucket name
const xdpFilePath = <xdp-file>;
const xmlFilePath = <xml-file>;

// Load environment variables
const clientId = process.env.CLIENT_ID;
const clientSecret = process.env.CLIENT_SECRET;
const scopes = process.env.SCOPES;

// Adobe IMS endpoint for obtaining an access token
const adobeIMSV3TokenEndpointURL = "https://ims-na1.adobelogin.com/ims/token/v3";

// Function to get an access token
const getAccessToken = async () => {
    console.log("Getting access token from IMS...");

    const options = {
        method: "POST",
        headers: {
            "Content-Type": "application/x-www-form-urlencoded",
        },
        body: `grant_type=client_credentials&client_id=${clientId}&client_secret=${clientSecret}&scope=${scopes}`,
    };

    const response = await fetch(adobeIMSV3TokenEndpointURL, options);
    const responseJSON = await response.json();

    console.log("Access token received.");
    return responseJSON.access_token;
};

// Function to generate PDF form from XDP and XML
const generatePDF = async () => {
    const accessToken = await getAccessToken();

    console.log("Generating PDF form from XDP and XML...");

    // Read XDP and XML files
    const xdpFile = fs.readFileSync(xdpFilePath);
    const xmlFile = fs.readFileSync(xmlFilePath);

    const url = `https://${bucket}.adobeaemcloud.com/adobe/document/generate/pdfform`;

    const formData = new FormData();
    formData.append("template", xdpFile, {
        filename: "form.xdp",
        contentType: "application/vnd.adobe.xdp+xml"
    });
    formData.append("data", xmlFile, {
        filename: "data.xml",
        contentType: "application/xml"
    });

    const response = await fetch(url, {
        method: "POST",
        headers: {
            Authorization: `Bearer ${accessToken}`,
            "X-Api-Key": clientId,
            "X-Adobe-Accept-Experimental": "1",
            ...formData.getHeaders()
        },
        body: formData,
    });

    if (response.ok) {
        const arrayBuffer = await response.arrayBuffer();
        fs.writeFileSync("generatedForm.pdf", Buffer.from(arrayBuffer));
        console.log("✅ PDF form generated successfully (saved as generatedForm.pdf)");
    } else {
        console.error("❌ Failed to generate PDF. Status:", response.status);
        console.error(await response.text());
    }
};

// Run the PDF generation function
generatePDF();
```

![crea index.js](/help/forms/assets/api-6.png)

##### Passaggio 6: eseguire l&#39;applicazione

```bash
node src/index.js
```

![esegui applicazione](/help/forms/assets/api-7.png)

PDF creato nella cartella `demo-nodejs-generate-pdf`. Passare alla cartella per trovare il file generato denominato `generatedForm.pdf`.

![visualizza pdf creato](/help/forms/assets/api-8.png)

Puoi aprire il [PDF](/help/forms/assets/create-pdf.png) generato per visualizzarlo.

## Risoluzione di problemi

### Problemi comuni e possibili cause

#### Problema 1: errore 403 non consentito

**Sintomi:**

- Le richieste API restituiscono `403 Forbidden`
- Messaggio di errore: *Accesso negato* o *autorizzazioni insufficienti*
- Si verifica anche con un token di accesso valido

**Cause possibili:**

- Autorizzazioni insufficienti nel profilo di prodotto collegato alle credenziali server-to-server OAuth
- Il gruppo di utenti del servizio in AEM Author non dispone delle autorizzazioni necessarie per i percorsi di contenuto richiesti

#### Problema 2: errore 401 non autorizzato

**Sintomi:**

- Le richieste API restituiscono `401 Unauthorized`
- Messaggio di errore: *Token non valido o scaduto*

**Cause possibili:**

- Token di accesso scaduto (valido solo per 24 ore)
- ID client e segreto client non corretti o non corrispondenti
- Intestazioni di autenticazione mancanti o non valide nella richiesta API

#### Problema 3: errore 404 non trovato

**Sintomi:**

- Le richieste API restituiscono `404 Not Found`
- Messaggio di errore: *Risorsa non trovata* o *Endpoint API non trovato*

**Cause possibili:**

- ID client non registrato nella configurazione `api.yaml` dell&#39;istanza AEM
- Parametro bucket errato (non corrisponde all’identificatore dell’istanza di AEM)
- ID risorsa (modulo o risorsa) non valido o inesistente

#### Problema 4: opzione di autenticazione server-to-server non disponibile

**Sintomi:**

- Opzione server-to-server OAuth mancante o disabilitata in Adobe Developer Console

**Possibile causa:**

- L&#39;utente che crea l&#39;integrazione non viene aggiunto come **Sviluppatore** nel profilo di prodotto associato

#### Problema 5: distribuzione della pipeline non riuscita

**Sintomi:**

- L’esecuzione della pipeline di configurazione non riesce
- I registri di distribuzione mostrano gli errori relativi a `api.yaml`

**Cause possibili:**

- Sintassi YAML non valida (problemi di rientro, virgolette o formato di matrice)
- `api.yaml` inserito in una directory non corretta
- ID client errato o non corretto nella configurazione


## Articoli correlati

Per informazioni su come impostare l&#39;ambiente per Batch (API asincrone), vedere [Elaborazione batch di comunicazioni AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-batch-processing.md).
