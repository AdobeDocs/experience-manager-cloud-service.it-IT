---
title: Riutilizzare il codice in siti diversi
description: Se disponi di molti siti simili che per lo più si presentano e si comportano allo stesso modo, ma hanno contenuti diversi, scopri come condividere il codice tra più siti diversi in un modello senza archivio.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
index: false
hide: true
hidefromtoc: true
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 100%

---

# Riutilizzare il codice in siti diversi {#repoless}

Se disponi di molti siti simili che per lo più si presentano e si comportano allo stesso modo, ma hanno contenuti diversi, scopri come condividere il codice tra più siti diversi in un modello senza archivio.

## Una base di codice per più siti {#one-codebase}

Per impostazione predefinita, AEM è strettamente associato all’archivio del codice, che soddisfa la maggior parte dei casi d’uso. Tuttavia, è possibile che più siti differiscano principalmente per quanto riguarda il contenuto, ma che sfruttino la stessa base di codice.

Invece di creare più archivi GitHub e di eseguire ogni sito da un archivio GitHub dedicato mantenendone la sincronizzazione, AEM supporta l’esecuzione di più siti dalla stessa base di codice.

Questa configurazione semplificata, che elimina la necessità di replica del codice, è nota anche come [“senza archivio”](https://www.aem.live/docs/repoless), perché tutti i siti, tranne il primo, non necessitano di un proprio archivio GitHub.

Se il progetto richiede la flessibilità di riutilizzo del codice tra siti diversi, puoi attivare la funzione.

Indipendentemente dal numero di siti che desideri creare in modalità senza archivio, è necessario creare il primo, che funge da sito di base. In questo documento viene illustrato come creare il primo sito per l’utilizzo senza archivio.

## Prerequisiti {#prerequisites}

Per sfruttare questa funzione, assicurati di aver eseguito le seguenti operazioni.

* La configurazione del sito sia già stata completata seguendo le indicazioni nel documento [Guida introduttiva per sviluppatori per l’authoring di WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).
* Stai eseguendo almeno la versione 2024.08 di AEM as a Cloud Service.

Sarà inoltre necessario chiedere a Adobe di configurare i seguenti elementi al posto tuo. Mettiti in contatto tramite il tuo canale Slack o genera un ticket di supporto per richiedere a Adobe di apportare queste modifiche:

* Chiedi di attivare il [servizio di configurazione aem.live](https://www.aem.live/docs/config-service-setup#prerequisites) per il tuo ambiente e di essere configurato come amministratore.
* Chiedi di abilitare la funzione senza archivio per il programma da Adobe.
* Chiedi ad Adobe di creare l’organizzazione per te.

## Attivare la funzione senza archivio {#activate}

Per attivare la funzionalità senza archivio per il progetto, sono disponibili diversi passaggi.

1. [Recuperare il token di accesso](#access-token)
1. [Impostare il servizio di configurazione](#config-service)
1. [Aggiungere la configurazione del sito e l’account tecnico](#access-control)
1. [Aggiornare la configurazione di AEM](#update-aem)
1. [Autenticare il sito](#authenticate-site)

In questi passaggi, il sito `https://wknd.site` viene utilizzato come esempio. Sostituiscilo con il tuo in modo appropriato.

### Recuperare il token di accesso {#access-token}

Per utilizzare il servizio di configurazione e configurarlo per il caso d’uso senza archivio è necessario innanzitutto un token di accesso.

1. Passa a `https://admin.hlx.page/login` e utilizza l’indirizzo `login_adobe` per accedere con il provider di identità Adobe.
1. Verrai reindirizzato a `https://admin.hlx.page/profile`.
1. Utilizzando gli strumenti per sviluppatori del browser, copia il valore del `x-auth-token` dal cookie del token web JSON impostato dalla pagina `admin.hlx.page`.

Una volta ottenuto il token di accesso, questo può essere trasmesso nell’intestazione delle richieste cURL nel seguente formato.

```text
--header 'x-auth-token: <your-token>'
```

### Aggiungere la mappatura dei percorsi per la configurazione del sito e l’impostazione dell’account tecnico {#access-control}

È necessario creare una configurazione del sito e aggiungerla alla mappatura dei percorsi.

1. Crea una nuova pagina nella directory principale del sito e scegli il modello [**Configurazione**](/help/edge/wysiwyg-authoring/tabular-data.md#other).
   * Puoi lasciare vuota la configurazione con solo le colonne predefinite `key` e `value`. Devi solo crearla.
1. Crea una mappatura nella configurazione pubblica per la configurazione del sito utilizzando un comando cURL simile al seguente.

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

1. Convalida che la configurazione pubblica sia stata impostata e sia disponibile con un comando cURL simile al seguente.

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```

Una volta mappata la configurazione del sito, puoi configurare il controllo degli accessi definendo l’account tecnico, in modo che disponga dei privilegi per la pubblicazione.

1. Accedi all’istanza di authoring di AEM e passa a **Strumenti** -> **Servizi cloud** -> **Configurazione Edge Delivery Services** e seleziona la configurazione creata automaticamente per il sito, quindi tocca o fai clic su **Proprietà** nella barra degli strumenti.

1. Nella finestra **Configurazione Edge Delivery Services**, seleziona la scheda **Autenticazione** e copia il valore per l’**ID account tecnico**.

   * Sarà simile a `<tech-account-id>@techacct.adobe.com`
   * L’account tecnico è lo stesso per tutti i siti in un singolo ambiente di authoring AEM.

1. Imposta l’account tecnico per la configurazione senza archivio con un comando cURL simile al seguente, utilizzando l’ID account tecnico copiato.

   * Adatta il blocco `admin` per definire gli utenti che devono disporre di accesso amministrativo completo al sito.
      * Si tratta di un array di indirizzi e-mail.
      * È possibile utilizzare il carattere jolly `*`.
      * Per ulteriori informazioni, consulta il documento [Configurazione dell’autenticazione per gli autori](https://www.aem.live/docs/authentication-setup-authoring#default-roles).

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

Poiché ora utilizzi il servizio di configurazione, puoi rimuovere `fstab.yaml` e `paths.json` dall’archivio Git.

>[!NOTE]
>
>Utilizzando il servizio di configurazione ed esponendo la mappatura del percorso tramite `config.json`, il file `path.json` viene ignorato.

Una volta che AEM è configurato per l’utilizzo senza archivio, utilizza il servizio di configurazione e fornisci un `config.json` valido con la mappatura dei percorsi.

### Aggiornare la configurazione di AEM {#update-aem}

Ora puoi apportare le modifiche necessarie ad Edge Delivery Services in AEM.

1. Accedi all’istanza di authoring AEM e passa a **Strumenti** -> **Servizi cloud** -> **Configurazione Edge Delivery Services** e seleziona la configurazione creata automaticamente per il tuo sito, quindi tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Nella finestra **Configurazione Edge Delivery Services**, modifica il tipo di progetto in **aem.live con configurazione senza archivio** e tocca o fai clic su **Salva e chiudi**.
   ![Configurazione di Edge Delivery Services](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. Torna al tuo sito utilizzando l’editor universale e assicurati che continui a esserne eseguito correttamente il rendering.
1. Modifica alcuni contenuti e ripubblicali.
1. Visita il sito pubblicato all’indirizzo `https://main--<your-aem-project>--<your-github-org>.aem.page/` e verifica che le modifiche siano state applicate correttamente.

Il progetto è ora configurato per l’utilizzo senza archivio.

## Passaggi successivi {#next-steps}

Ora che il sito di base è configurato per l’utilizzo senza archivio, puoi creare altri siti che sfruttano la stessa base di codice. Fai riferimento alla seguente documentazione a seconda del caso d’uso.

* [Gestione di più siti senza archivio](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [Ambienti di produzione e staging senza archivio](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)
* [Autenticazione del sito per l’authoring dei contenuti](/help/edge/wysiwyg-authoring/site-authentication.md)

## Risoluzione dei problemi {#troubleshooting}

Il problema più comune riscontrato dopo la configurazione del caso d’uso senza archivio è che le pagine nell’editor universale non vengono più riprodotte oppure viene visualizzato un messaggio di errore generico di AEM as a Cloud Service o una pagina bianca. In entrambi i casi:

* Visualizza l’origine della pagina di cui è stato eseguito il rendering.
   * È stato effettivamente eseguito il rendering di un elemento (intestazione HTML corretta con `scripts.js`, `aem.js` e file JSON relativi all’editor)?
* Controlla l’`error.log` AEM dell’istanza di authoring per le eccezioni.
   * Il problema più comune è che il componente Pagina non riesce restituendo errori 404.
   * Impossibile caricare `config.json or paths.json`
   * `component-definition.json`, ecc. non possono essere caricati
