---
title: Riutilizzo del codice in siti diversi
description: Se hai molti siti simili che per lo più si presentano e si comportano allo stesso modo, ma hanno contenuti diversi, scopri come condividere il codice tra più siti in un modello di repoless.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
source-git-commit: c9d0d3cd7e18b56db36a379b63f8fb48e18a40db
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 2%

---

# Riutilizzo del codice in siti diversi {#repoless}

Se hai molti siti simili che per lo più si presentano e si comportano allo stesso modo, ma hanno contenuti diversi, scopri come condividere il codice tra più siti in un modello di repoless.

## Una base di codice per più siti {#one-codebase}

Per impostazione predefinita, AEM è strettamente associato all’archivio del codice, che soddisfa la maggior parte dei casi d’uso. Tuttavia, è possibile che più siti differiscano principalmente per quanto riguarda il contenuto, ma che sfruttino la stessa base di codice.

Invece di creare più archivi GitHub e di eseguire ogni sito da un archivio GitHub dedicato mantenendo la sincronizzazione, AEM supporta l’esecuzione di più siti dalla stessa base di codice.

Questa configurazione semplificata, che elimina la necessità di replica del codice, è nota anche come [&quot;repoless&quot;](https://www.aem.live/docs/repoless), perché tutti tranne il primo sito non hanno bisogno di un proprio archivio GitHub.

Se il progetto richiede la flessibilità di riutilizzo del codice tra siti diversi, puoi attivare la funzione.

Indipendentemente dal numero di siti che si desidera creare in modalità di replica, è necessario creare il primo sito, che funge da sito di base. In questo documento viene illustrato come creare il primo sito per l&#39;utilizzo da parte di repoless.

## Prerequisiti {#prerequisites}

Per sfruttare questa funzione, assicurati di aver eseguito le seguenti operazioni.

* La configurazione del sito è già stata completata seguendo il documento [Guida introduttiva per sviluppatori per l&#39;authoring di WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).
* Stai eseguendo almeno AEM as a Cloud Service 2024.08.

Sarà inoltre necessario chiedere ad Adobe di configurare i seguenti elementi al posto tuo. Rivolgiti al tuo canale Slack o solleva un problema di supporto per richiedere ad Adobe di apportare queste modifiche:

* Chiedi di attivare il servizio di configurazione [aem.live](https://www.aem.live/docs/config-service-setup#prerequisites) per il tuo ambiente e di essere configurato come amministratore.
* Chiedi di abilitare la funzione Repoless per il programma da Adobe.
* Chiedi ad Adobe di creare l’organizzazione per te.

## Attiva funzione di ripolling {#activate}

Sono disponibili diversi passaggi per attivare la funzionalità di ripolling per il progetto.

1. [Recupera token di accesso](#access-token)
1. [Configura servizio di configurazione](#config-service)
1. [Aggiungi configurazione del sito e account tecnico](#access-control)
1. [Aggiorna configurazione AEM](#update-aem)
1. [Autentica sito](#authenticate-site)

In questi passaggi viene utilizzato il sito `https://wknd.site` come esempio. Sostituire il proprio in modo appropriato.

### Recupera token di accesso {#access-token}

Per utilizzare il servizio di configurazione e configurarlo per il caso d’uso dei ripoli è innanzitutto necessario un token di accesso.

1. Vai a `https://admin.hlx.page/login` e utilizza l&#39;indirizzo `login_adobe` per accedere con il provider di identità Adobe.
1. Verrai inoltrato a `https://admin.hlx.page/profile`.
1. Utilizzando gli strumenti per gli sviluppatori del browser, copiare il valore di `x-auth-token` dal cookie token Web JSON impostato dalla pagina `admin.hlx.page`.

Una volta ottenuto il token di accesso, questo può essere trasmesso nell’intestazione delle richieste cURL nel seguente formato.

```text
--header 'x-auth-token: <your-token>'
```

### Aggiungi mappatura percorso per configurazione sito e imposta account tecnico {#access-control}

Devi creare una configurazione del sito e aggiungerla alla mappatura del percorso.

1. Crea una nuova pagina nella directory principale del sito e scegli il modello [**Configurazione**](/help/edge/wysiwyg-authoring/tabular-data.md#other).
   * È possibile lasciare vuota la configurazione con solo le colonne predefinite `key` e `value`. Devi solo crearlo.
1. Crea un mapping nella configurazione pubblica alla configurazione del sito utilizzando un comando cURL simile al seguente.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/",
               "/content/<your-site-content>/configuration:/.helix/config.json"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```
1. Verifica che la configurazione pubblica sia stata impostata e sia disponibile con un comando cURL simile al seguente.

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```

Una volta mappata la configurazione del sito, puoi configurare il controllo degli accessi definendo l’account tecnico in modo che disponga dei privilegi per la pubblicazione.

1. Nel browser, recupera l’account tecnico nella risposta del seguente collegamento.

   ```text
   https://author-p<programID>-e<envionmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/<your-aem-project>/main/.helix/config.json
   ```

1. La risposta sarà simile alla seguente.

   ```json
   {
     "total": 1,
     "offset": 0,
     "limit": 1,
     "data": [
       {
         "key": "admin.role.publish",
         "value": "<tech-account-id>@techacct.adobe.com"
       }
     ],
     ":type": "sheet"
   }
   ```

1. Imposta l’account tecnico nella configurazione con un comando cURL simile al seguente.

   * Adattare il blocco `admin` per definire gli utenti che devono disporre di accesso amministrativo completo al sito.
      * Si tratta di un array di indirizzi e-mail.
      * È possibile utilizzare il carattere jolly `*`.
      * Per ulteriori informazioni, vedere il documento [Configurazione dell&#39;autenticazione per gli autori](https://www.aem.live/docs/authentication-setup-authoring#default-roles).

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/access.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "admin": {
           "role": {
               "admin": [
                   "<email>@<domain>.<tld>"
               ],
               "config_admin": [
                   "<tech-account-id>@techacct.adobe.com"
               ]
           },
           "requireAuth": "auto"
       }
   }'
   ```

Poiché ora si utilizza il servizio di configurazione, è possibile rimuovere `fstab.yaml` e `paths.json` dall&#39;archivio Git.

>[!NOTE]
>
>Utilizzando il servizio di configurazione ed esponendo la mappatura del percorso tramite `config.json`, il file `path.json` viene ignorato.

Una volta che AEM è configurato per l&#39;utilizzo in repoless, è necessario utilizzare il servizio di configurazione e fornire un `config.json` valido con la mappatura dei percorsi.

### Aggiorna configurazione AEM {#update-aem}

Ora puoi apportare le modifiche necessarie al Edge Delivery Services in AEM.

1. Accedi all&#39;istanza di authoring di AEM e vai a **Strumenti** -> **Servizi cloud** -> **Configurazione Edge Delivery Services** e seleziona la configurazione creata automaticamente per il tuo sito, quindi tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Nella finestra **Configurazione Edge Delivery Services**, modifica il tipo di progetto in **aem.live con configurazione di repoless** e tocca o fai clic su **Salva e chiudi**.
   ![Configurazione Edge Delivery Services](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. Torna al tuo sito utilizzando l’Editor universale e assicurati che continui a essere eseguito correttamente il rendering.
1. Modifica alcuni contenuti e ripubblica.
1. Visita il sito pubblicato all&#39;indirizzo `https://main--<your-aem-project>--<your-github-org>.aem.page/` e verifica che le modifiche siano state applicate correttamente.

Il progetto è ora configurato per l’utilizzo in repoless.

## Passaggi successivi {#next-steps}

Ora che il sito di base è configurato per l’utilizzo di repoless, puoi creare altri siti che sfruttano la stessa base di codice. Fai riferimento alla seguente documentazione a seconda del caso d’uso.

* [Gestione di più siti senza archivio](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [Ambienti di produzione e staging senza archivio](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)
* [Autenticazione del sito per l’authoring dei contenuti](/help/edge/wysiwyg-authoring/site-authentication.md)

## Risoluzione dei problemi {#troubleshooting}

Il problema più comune riscontrato dopo la configurazione del caso d’uso di Repoless è che le pagine nell’Editor universale non vengono più riprodotte oppure viene visualizzato un messaggio di errore di AEM as a Cloud Service o una pagina bianca. In tal caso:

* Visualizza l&#39;origine della pagina di cui è stato eseguito il rendering.
   * È stato eseguito il rendering di un elemento (intestazione HTML corretta con `scripts.js`, `aem.js` e file JSON relativi all&#39;editor)?
* Controllare l&#39;AEM `error.log` dell&#39;istanza di authoring per le eccezioni.
   * Il problema più comune è che il componente Pagina non riesce con errori 404.
   * Impossibile caricare `config.json or paths.json`
   * `component-definition.json` ecc. non può essere caricato
