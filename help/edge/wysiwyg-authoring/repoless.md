---
title: Riutilizzo del codice tra siti diversi
description: Se hai molti siti simili che per lo più si presentano e si comportano allo stesso modo, ma hanno contenuti diversi, scopri come condividere il codice tra più siti in un modello di repoless.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: e25e21984ebadde7076d95c6051b8bfca5b2ce03
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---


# Riutilizzo del codice tra siti diversi {#repoless}

Se hai molti siti simili che per lo più si presentano e si comportano allo stesso modo, ma hanno contenuti diversi, scopri come condividere il codice tra più siti in un modello di repoless.

## Una base di codice per più siti {#one-codebase}

Per impostazione predefinita, l’AEM è strettamente associato all’archivio del codice, che soddisfa la maggior parte dei casi d’uso. Tuttavia, è possibile che più siti differiscano principalmente per quanto riguarda il contenuto, ma che sfruttino la stessa base di codice.

Invece di creare più archivi GitHub e di eseguire ogni sito da un archivio GitHub dedicato mantenendo la sincronizzazione, l’AEM supporta l’esecuzione di più siti dalla stessa base di codice.

Questa configurazione semplificata, che elimina la necessità di replica del codice, è nota anche come [&quot;repoless&quot;,](https://www.aem.live/docs/repoless) perché tutti tranne il primo sito non hanno bisogno di un proprio archivio GitHub.

Se il progetto richiede la flessibilità di riutilizzo del codice tra siti diversi, puoi attivare la funzione.

Indipendentemente dal numero di siti che si desidera creare in modalità di replica, è necessario creare il primo sito, che funge da sito di base. In questo documento viene illustrato come creare il primo sito per l&#39;utilizzo da parte di repoless.

## Prerequisiti {#prerequisites}

Per sfruttare questa funzione, assicurati di aver eseguito le seguenti operazioni.

* La configurazione del sito è già stata completata seguendo il documento [Guida introduttiva per sviluppatori per l&#39;authoring di WYSIWYG con Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* Stai eseguendo almeno AEM as a Cloud Service 2024.08.

Sarà inoltre necessario chiedere ad Adobe di configurare due elementi per te. Rivolgiti a Adobe tramite il tuo canale di Slack o solleva un problema di supporto per effettuare queste richieste.

* Il servizio di configurazione [aem.live](https://www.aem.live/docs/config-service-setup#prerequisites) è attivo per il tuo ambiente e sei configurato come amministratore.
* La funzione di ripolling deve essere abilitata per il programma per Adobe.

## Attiva funzione di ripolling {#activate}

Sono disponibili diversi passaggi per attivare la funzionalità di ripolling per il progetto.

1. [Recupera token di accesso](#access-token)
1. [Configura servizio di configurazione](#config-service)
1. [Imposta controllo di accesso](#access-control)
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

### Configurare il servizio di configurazione {#config-service}

Come indicato nei [prerequisiti,](#prerequisites) il servizio di configurazione deve essere abilitato per il tuo ambiente. Puoi controllare la configurazione del servizio di configurazione con questo comando cURL.

```text
curl  --location 'https://admin.hlx.page/config/<your-github-org>.json' \
--header 'x-auth-token: <your-token>'
```

Se il servizio di configurazione è configurato correttamente, verrà restituito un JSON simile al seguente.

```json
{
  "title": "<your-github-org>",
  "description": "Your GitHub Org",
  "lastModified": "2024-11-14T12:14:04.230Z",
  "created": "2024-11-14T12:13:37.032Z",
  "version": 1,
  "users": [
    {
      "email": "justthisguyyouknow@adobe.com",
      "roles": [
        "admin"
      ],
      "id": "<your-id>"
    }
  ]
}
```

Contatta Adobe tramite il canale di Slack del progetto o solleva un problema di supporto se il servizio di configurazione non è abilitato. Una volta ottenuto il token e verificato che il servizio di configurazione è abilitato, puoi continuare la configurazione.

1. Verifica che l’origine di contenuto sia configurata correttamente.

   ```text
   curl --request GET \
   --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>.json \
   --header 'x-auth-token: <your-token>'
   ```

1. Aggiungi un mapping di percorso alla configurazione pubblica.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```

Una volta creata la configurazione pubblica, puoi accedervi tramite un URL simile a `https://main--<your-aem-project>--<your-github-org>.aem.page/config.json` per verificarla.

### Imposta controllo di accesso {#access-control}

Per impostare il controllo degli accessi, devi fornire l’account tecnico.

1. Crea una nuova pagina nella directory principale del sito e scegli il modello [**Configurazione**.](/help/edge/wysiwyg-authoring/tabular-data.md#other)
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
1. Nel browser, ora puoi recuperare l’account tecnico nella risposta del seguente collegamento.

   ```text
   https://author-p<programID>-e<envionmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/<your-aem-project>/main/.helix/config.json
   ```

La risposta sarà simile alla seguente.

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

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/access.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "admin": {
           "role": {
               "admin": [
                   "*@adobe.com"
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

Una volta configurato l&#39;AEM per l&#39;utilizzo in repoless, è necessario utilizzare il servizio di configurazione e fornire un `config.json` valido con la mappatura dei percorsi.

### Aggiorna configurazione AEM {#update-aem}

Ora è possibile apportare le modifiche necessarie ai Edge Delivery Services dell’AEM.

1. Accedi all&#39;istanza di creazione dell&#39;AEM e vai a **Strumenti** -> **Cloud Service** -> **Configurazione Edge Delivery Services** e seleziona la configurazione creata automaticamente per il tuo sito, quindi tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Nella finestra Configurazione **Edge Delivery Services**, modifica il tipo di progetto in **aem.live con configurazione di repoless** e tocca o fai clic su **Salva e chiudi**.
   Configurazione di ![Edge Delivery Services](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. Torna al tuo sito utilizzando l’Editor universale e assicurati che continui a essere eseguito correttamente il rendering.
1. Modifica alcuni contenuti e ripubblica.
1. Visita il sito pubblicato all&#39;indirizzo `https://main--<your-aem-project>--<your-github-org>.aem.page/` e verifica che le modifiche siano state applicate correttamente.

Il progetto è ora configurato per l’utilizzo in repoless.

## Passaggi successivi {#next-steps}

Ora che il sito di base è configurato per l’utilizzo di repoless, puoi creare altri siti che sfruttano la stessa base di codice. Fai riferimento alla seguente documentazione a seconda del caso d’uso.

* [Gestione multisito di Ripoless](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [Repoless Stage e ambienti di produzione](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)

## Risoluzione dei problemi {#troubleshooting}

Il problema più comune riscontrato dopo la configurazione del caso d’uso di Repoless è che le pagine nell’Editor universale non vengono più riprodotte oppure viene visualizzato un messaggio di errore di AEM as a Cloud Service o una pagina bianca. In tal caso:

* Visualizza l&#39;origine della pagina di cui è stato eseguito il rendering.
   * È stato eseguito il rendering di un elemento (intestazione HTML corretta con `scripts.js`, `aem.js` e file JSON relativi all&#39;editor)?
* Controllare l&#39;AEM `error.log` dell&#39;istanza di authoring per le eccezioni.
   * Il problema più comune è che il componente Pagina non riesce con errori 404.
   * Impossibile caricare `config.json or paths.json`
   * `component-definition.json` ecc. non può essere caricato