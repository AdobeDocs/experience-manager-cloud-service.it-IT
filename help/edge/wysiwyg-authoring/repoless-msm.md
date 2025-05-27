---
title: Gestione di più siti senza archivio
description: Scopri i consigli sulle best practice per impostare un progetto in modalità senza archivio con siti localizzati che sfruttano un’unica base di codice, ciascuno gestito da Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: f6b861ed-18e4-4c81-92d2-49fadfe4669a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '1260'
ht-degree: 100%

---

# Gestione di più siti senza archivio {#repoless-msm}

Scopri i consigli sulle best practice per impostare un progetto in modalità senza archivio con siti localizzati che sfruttano un’unica base di codice, ciascuno gestito da Edge Delivery Services.

## Panoramica {#overview}

La [Gestione di più siti (Multi Site Manager, MSM](/help/sites-cloud/administering/msm/overview.md) e le relative funzioni Live Copy consentono di utilizzare lo stesso contenuto del sito in più posizioni, permettendo al contempo l’utilizzo di varianti. Puoi creare contenuti una sola volta e creare Live Copy. MSM mantiene relazioni live tra il contenuto di origine e le relative Live Copy in modo che, quando modifichi il contenuto di origine, sia possibile sincronizzare l’origine e le Live Copy.

Puoi utilizzare MSM per creare un’intera struttura di contenuto per il tuo brand in diverse lingue, creando contenuti a livello centrale. I siti localizzati possono quindi essere consegnati da Edge Delivery Services, sfruttando una base di codice centrale.

## Requisiti {#requirements}

Per configurare MSM in un caso di utilizzo senza archivio, devi prima completare le seguenti attività:

* In questo documento si presuppone che sia già stato creato un sito per il progetto in base alla [Guida introduttiva per sviluppatori per l’authoring di WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).
* È necessario che sia già [abilitata la funzione senza archivio per il progetto](/help/edge/wysiwyg-authoring/repoless.md).

## Caso d’uso {#use-case}

In questo documento si presuppone che sia già stata creata una struttura di base del sito localizzato per il progetto. Ad esempio, per il brand WKND presente in Svizzera e Germania, utilizza la seguente struttura.

```text
/content/wknd
/content/wknd/language-masters
/content/wknd/language-masters/en
/content/wknd/language-masters/de
/content/wknd/language-masters/fr
/content/wknd/language-masters/it
/content/wknd/ch
/content/wknd/ch/de
/content/wknd/ch/fr
/content/wknd/ch/it
/content/wknd/ch/en
/content/wknd/de
/content/wknd/de/de
/content/wknd/de/en
```

Il contenuto in `language-masters` è l’origine delle Live Copy per i siti localizzati: Germania (`de`) e Svizzera (`ch`). L’obiettivo di questo documento è creare siti Edge Delivery Services che utilizzano tutti la stessa base di codice per ogni sito localizzato.

## Configurazione {#configuration}

Sono disponibili diversi passaggi per configurare il caso d’uso senza archivio di MSM.

1. [Aggiornare le configurazioni del sito AEM](#update-aem-configurations).
1. [Creare nuovi siti Edge Delivery Services per le pagine localizzate](#create-edge-sites).
1. [Aggiornare la configurazione cloud in AEM per i siti localizzati](#update-cloud-configurations).

### Aggiornare le configurazioni del sito AEM {#update-aem-configurations}

Le [configurazioni](/help/implementing/developing/introduction/configurations.md) possono essere considerate come aree di lavoro da utilizzare per raccogliere gruppi di impostazioni e il relativo contenuto associato a scopo organizzativo. Quando crei un sito in AEM, viene anche creata automaticamente una configurazione per esso.

In genere, desideri condividere determinati contenuti tra siti, ad esempio:

* Modelli creati dal contenuto nella blueprint
* Modelli per frammenti di contenuto, persistenti, query e così via.

Per facilitare tale condivisione, puoi creare configurazioni aggiuntive. Per il caso d’uso WKND, sono necessarie configurazioni per i seguenti percorsi.

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

In altre parole, avrai una configurazione per la directory principale del contenuto del brand WKND (`/content/wknd`) utilizzato dalle blueprint e una configurazione utilizzata da ciascun sito localizzato (Svizzera e Germania).

1. Accedi all’istanza di authoring di AEM.
1. Passa a **Browser configurazioni** scegliendo **Strumenti** -> **Generale** -> **Browser configurazioni**.
1. Seleziona la configurazione creata automaticamente per il progetto (in questo caso WKND), quindi tocca o fai clic su **Crea** nella barra degli strumenti.
1. Nella finestra di dialogo **Crea configurazione**, fornisci un **Nome** descrittivo per il sito localizzato (ad esempio `Switzerland`) e per il **Titolo** utilizza lo stesso titolo della dimensione localizzata (in questo caso `ch`).
1. Seleziona la funzione **Configurazione cloud** e le eventuali funzioni aggiuntive necessarie per il progetto, ad esempio **Modelli modificabili**.
1. Tocca o fai clic su **Crea**.

Crea le configurazioni per ogni sito localizzato necessario. Nel caso di WKND, è necessario creare una configurazione per `de` insieme alla configurazione `ch`.

Una volta create le configurazioni, è necessario assicurarsi che i siti localizzati le utilizzino.

1. Accedi all’istanza di authoring di AEM.
1. Passa alla **console Sites** da **Navigazione** -> **Sites**.
1. Seleziona il sito localizzato come `Switzerland`.
1. Tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Nella finestra delle proprietà della pagina, seleziona la scheda **Avanzate** e, nell’intestazione **Configurazione**, deseleziona l’opzione **Ereditata da /content/wknd**, dove `wknd` è la directory principale del sito.
1. Nel campo **Configurazione cloud**, utilizza il browser percorsi per selezionare la configurazione creata per il sito localizzato, ad esempio `Switzerland` in `/conf/wknd/ch`.
1. Tocca o fai clic su **Salva e chiudi**.

Assegna le rispettive configurazioni ai siti localizzati aggiuntivi. Nel caso di WKND, è necessario assegnare la configurazione `/conf/wknd/de` anche al sito della Germania.

### Creare nuovi siti Edge Delivery Services per le pagine localizzate {#create-edge-sites}

Per connettere più siti ad Edge Delivery Services per una configurazione di siti multilingue e con più aree geografiche, è necessario impostare un nuovo sito aem.live per ciascuno dei siti MSM di AEM. Esiste una relazione 1:1 tra i siti MSM di AEM e i siti aem.live con un archivio Git condiviso e una base di codice.

In questo esempio, verrà creato il sito `wknd-ch` per la presenza svizzera di WKND, il cui contenuto localizzato si trova nel percorso `/content/wknd/ch` di AEM.

1. Recupera il token di autenticazione e l’account tecnico per il programma.
   * Consulta il documento **Riutilizzare il codice in siti diversi**, per informazioni dettagliate su come [ottenere il token di accesso](/help/edge/wysiwyg-authoring/repoless.md#access-token) e l’[account tecnico](/help/edge/wysiwyg-authoring/repoless.md#access-control) del programma.
1. Crea un nuovo sito effettuando la seguente chiamata al servizio di configurazione. Tieni presente che:
   * il nome del progetto nell’URL POST deve essere il nuovo nome del sito che stai creando. In questo esempio, è `wknd-ch`.
   * La configurazione del `code` deve essere la stessa utilizzata per la creazione del progetto iniziale.
   * `content` > `source` > `url` deve essere adattato al nome del nuovo sito che stai creando. In questo esempio, è `wknd-ch`.
   * Ovvero, il nome del sito nell’URL POST e il `content` > `source` > `url` devono essere uguali.
   * Adatta il blocco `admin` per definire gli utenti che devono disporre di accesso amministrativo completo al sito.
      * Si tratta di un array di indirizzi e-mail.
      * È possibile utilizzare il carattere jolly `*`.
      * Per ulteriori informazioni, consulta il documento [Configurazione dell’autenticazione per gli autori](https://www.aem.live/docs/authentication-setup-authoring#default-roles).

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
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
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-ch/main",
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
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/ch/:/"
           ],
           "includes": [
               "/content/wknd/ch/"
           ]
       }
   }'
   ```

1. Verifica che la configurazione pubblica del nuovo sito funzioni chiamando `https://main--wknd-ch--<your-github-org>.aem.page/config.json` e verificando il contenuto del file JSON restituito.

Ripeti i passaggi per creare altri siti localizzati. Nel caso di WKND, è necessario creare anche un sito `wknd-de` per la presenza tedesca.

### Aggiornare le configurazioni cloud in AEM per le pagine localizzate {#update-cloud-configurations}

Per la presenza localizzata, le pagine in AEM devono essere configurate per utilizzare i nuovi siti Edge Delivery creati nella sezione precedente. In questo esempio, il contenuto in `/content/wknd/ch` deve sapere come utilizzare il sito `wknd-ch` creato. Analogamente, il contenuto in `/content/wknd/de` deve poter utilizzare il sito `wknd-de`.

1. Accedi all’istanza di authoring di AEM e passa a **Strumenti** -> **Servizi cloud** -> **Configurazione Edge Delivery Services**.
1. Seleziona la configurazione creata automaticamente per il progetto e quindi la cartella creata per la pagina localizzata. In questo caso, sarebbe la Svizzera (`ch`).
1. Nella barra degli strumenti, tocca o fai clic su **Crea** > **Configurazione**.
1. Nella finestra **Configurazione Edge Delivery Services**:
   * Fornisci la tua organizzazione GitHub nel campo **Organizzazione**.
   * Modifica il nome del sito nel nome del sito che hai creato nella sezione precedente. In questo caso, sarebbe `wknd-ch`.
   * Cambia il tipo di progetto in **aem.live con configurazione senza archivio**.
1. Tocca o fai clic su **Salva e chiudi**.

## Verificare la configurazione {#verify}

Dopo aver apportato tutte le modifiche di configurazione necessarie, verifica che tutto funzioni come previsto.

1. Accedi all’istanza di authoring di AEM.
1. Passa alla **console Sites** da **Navigazione** -> **Sites**.
1. Seleziona il sito localizzato come `Switzerland`.
1. Nella barra degli strumenti, tocca o fai clic su **Modifica**.
1. Assicurati che la pagina esegua il rendering correttamente nell’editor universale e utilizzi lo stesso codice della directory principale del sito.
1. Apporta una modifica alla pagina e ripubblicala.
1. Visita il tuo nuovo sito Edge Delivery Services per la pagina localizzata in `https://main--wknd-ch--<your-github-org>.aem.page`.

Se visualizzi le modifiche che hai apportato, la configurazione MSM funziona correttamente.
