---
title: Ambienti di produzione e staging senza archivio
description: Scopri come impostare siti separati per gli ambienti di staging e produzione sfruttando un’unica base di codice in modo repoless.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 701bd9bc-30e8-4654-8248-a06d441d1504
source-git-commit: beda1168323d511cd7b89bb5d0a6eccb742de36f
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 2%

---

# Ambienti di produzione e staging senza archivio {#repoless-stage-prod}

Scopri come impostare siti separati per gli ambienti di staging e produzione sfruttando un’unica base di codice in modo repoless.

## Panoramica {#overview}

È possibile impostare un sito per l’ambiente di produzione separato dall’ambiente di staging. L&#39;impostazione di un secondo sito per un&#39;installazione separata di staging e produzione è simile all&#39;[installazione richiesta per la gestione multisito](/help/edge/wysiwyg-authoring/repoless-msm.md). Infatti, può essere combinato con le strutture del sito MSM se necessario.

Questo documento utilizza l’esempio tipico di ambienti di staging e produzione separati. Puoi creare ambienti separati per qualsiasi ambiente.

## Requisiti {#requirements}

Per configurare gli ambienti di staging e produzione di repoless, è necessario prima completare le seguenti attività:

* In questo documento si presuppone che sia già stato creato un sito per il progetto in base alla [Guida introduttiva per sviluppatori per l&#39;authoring di WYSIWYG con Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* È necessario che [abbia già abilitato la funzionalità di ripolling per il progetto.](/help/edge/wysiwyg-authoring/repoless.md)

## Configurazione {#configuration}

Questo documento descrive come impostare un sito di produzione separato per il progetto utilizzando la stessa base di codice. Vengono fatte le seguenti ipotesi.

* Il sito di staging è già configurato e ora desideri creare una configurazione per il sito di produzione.
* La struttura del contenuto nell’authoring di AEM è simile.
* Le stesse mappature dei percorsi verranno utilizzate per la staging e la produzione.

In questo esempio, si presume che sia già stato creato un sito di produzione per il progetto denominato wknd, il cui archivio GitHub è anche denominato wknd.

Esistono due passaggi per configurare un sito di produzione separato.

1. [Crea nuovi siti Edge Delivery Services per l&#39;ambiente di produzione](#create-edge-site).
1. [Aggiorna la configurazione cloud in AEM per il sito di produzione](#update-cloud-configuration).

### Creazione di nuovi siti Edge Delivery Services per l&#39;ambiente di produzione {#create-edge-site}

1. Recupera il token di autenticazione e l’account tecnico per il programma.
   * Per informazioni dettagliate su come [ottenere il token di accesso](/help/edge/wysiwyg-authoring/repoless.md#access-token) e l&#39;account tecnico [del programma, consulta il documento **Riutilizzo del codice tra siti**.](/help/edge/wysiwyg-authoring/repoless.md#access-control)
1. Crea un nuovo sito effettuando la seguente chiamata al servizio di configurazione. Considera:
   * Il nome del progetto nell’URL POST deve essere il nuovo nome del sito che stai creando. In questo esempio è `wknd-prod`.
   * La configurazione di `code` deve essere la stessa utilizzata per la creazione iniziale del progetto.
   * `content` > `source` > `url` deve essere adattato al nome del nuovo sito che stai creando. In questo esempio è `wknd-prod`.
   * Ad esempio, il nome del sito nell&#39;URL POST e `content` > `source` > `url` devono essere uguali.
   * Adattare il blocco `admin` per definire gli utenti che devono disporre di accesso amministrativo completo al sito.
      * Si tratta di un array di indirizzi e-mail.
      * È possibile utilizzare il carattere jolly `*`.
      * Per ulteriori informazioni, vedere il documento [Configurazione dell&#39;autenticazione per gli autori](https://www.aem.live/docs/authentication-setup-authoring#default-roles).

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "code": {
           "owner": "<your-github-org>",
           "repo": "wknd",
           "source": {
               "type": "github",
               "url": "https://github.com/<your-github-org>/wknd"
           }
       },
       "content": {
           "source": {
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-prod/main",
               "type": "markup",
               "suffix": ".html"
           }
       },
       "access": {
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
       }
   }'
   ```

1. Aggiungi la mappatura del percorso per il nuovo sito effettuando la seguente chiamata al servizio di configurazione.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/:/"
           ],
           "includes": [
               "/content/wknd/"
           ]
       }
   }'
   ```

Verificare che la configurazione pubblica del nuovo sito funzioni chiamando `https://main--wknd-prod--<your-github-org>.aem.page/config.json` e verificando il contenuto del JSON restituito.

### Aggiornare le configurazioni cloud in AEM per il sito di produzione {#update-cloud-configuration}

L’AEM di produzione deve essere configurato per utilizzare i nuovi siti Edge Delivery creati nella sezione precedente per un sito di produzione dedicato. In questo esempio, il contenuto in `/content/wknd` dell&#39;ambiente di produzione deve sapere come utilizzare il sito `wknd-prod` creato.

1. Accedi all&#39;istanza di produzione di AEM e vai a **Strumenti** -> **Servizi cloud** -> **Configurazione Edge Delivery Services**.
1. Seleziona la configurazione creata automaticamente per il progetto.
1. Tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Nella finestra **Configurazione Edge Delivery Services**:
   * Fornisci la tua organizzazione GitHub nel campo **Organizzazione**.
   * Modifica il nome del sito con il nome del sito creato nella sezione precedente. In questo caso, sarebbe `wknd-prod`.
   * Cambia il tipo di progetto in **aem.live con configurazione di repoless**.
1. Tocca o fai clic su **Salva e chiudi**.

## Verifica la configurazione {#verify}

Dopo aver apportato tutte le modifiche di configurazione necessarie, verifica che tutto funzioni come previsto.

1. Accedi all’istanza di authoring di produzione di AEM.
1. Passa alla **console Sites** da **navigazione** -> **siti**.
1. Seleziona una pagina del sito.
1. Tocca o fai clic su **Modifica** nella barra degli strumenti.
1. Assicurati che la pagina venga riprodotta correttamente nell’Editor universale e utilizzi lo stesso codice della directory principale del sito.
1. Apporta una modifica alla pagina e ripubblica.
1. Visita il tuo nuovo sito Edge Delivery Services per quella pagina all&#39;indirizzo `https://main--wknd-prod--<your-github-org>.aem.page`.

Se vengono visualizzate le modifiche apportate, la configurazione separata del sito di produzione funziona correttamente.

## Utilizzo {#usage}

Dopo aver configurato il progetto con gli ambienti di staging e produzione di Repoless, puoi gestire il codice per tali ambienti in modo indipendente. Il diagramma seguente illustra la relazione del contenuto nei vari ambienti in AEM, nei siti Edge Delivery Services e negli archivi GitHub.

![Illustrazione degli ambienti AEM e degli ambienti prod/stage ripoless](assets/repoless/aem-edge-github.png)
