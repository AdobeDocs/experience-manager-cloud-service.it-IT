---
title: Gestione multisito di Ripoless
description: Scopri i consigli sulle best practice per impostare un progetto in modo riorganizzato con siti localizzati che sfruttano un’unica base di codice, ciascuno gestito da Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: e25e21984ebadde7076d95c6051b8bfca5b2ce03
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 1%

---


# Gestione multisito di Ripoless {#repoless-msm}

Scopri i consigli sulle best practice per impostare un progetto in modo riorganizzato con siti localizzati che sfruttano un’unica base di codice, ciascuno gestito da Edge Delivery Services.

## Panoramica {#overview}

[Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) e le relative funzionalità Live Copy consentono di utilizzare lo stesso contenuto del sito in più posizioni, consentendo al contempo l&#39;utilizzo di varianti. Puoi creare contenuti una sola volta e creare Live Copy. MSM mantiene relazioni live tra il contenuto sorgente e le relative Live Copy in modo che, quando modifichi il contenuto sorgente, sia possibile sincronizzare l’origine e le Live Copy.

Puoi utilizzare MSM per creare un’intera struttura di contenuto per il tuo marchio in diverse lingue e lingue, creando contenuti a livello centrale. I siti localizzati possono quindi essere consegnati per Edge Delivery Services, sfruttando una base di codice centrale.

## Requisiti {#requirements}

Per configurare MSM in un caso di utilizzo di repoless, devi prima completare una serie di attività.

* In questo documento si presuppone che sia già stato creato un sito per il progetto in base alla [Guida introduttiva per sviluppatori per l&#39;authoring di WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).
* È necessario che [abbia già abilitato la funzionalità di ripolling per il progetto.](/help/edge/wysiwyg-authoring/repoless.md)

## Caso d’uso {#use-case}

In questo documento si presuppone che sia già stata creata una struttura di base del sito localizzato per il progetto. Ad esempio, utilizza la seguente struttura per il marchio wknd, presente in Svizzera e Germania.

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

Il contenuto in `language-masters` è l&#39;origine di Live Copy per i siti localizzati: Germania (`de`) e Svizzera (`ch`). L&#39;obiettivo di questo documento è la creazione di Edge Delivery Services che utilizzano tutti la stessa base di codice per ogni sito localizzato.

## Configurazione {#configuration}

Sono disponibili diversi passaggi per configurare il caso di utilizzo dei ripoli MSM.

1. [Aggiornare le configurazioni del sito AEM.](#update-aem-configurations)
1. [Crea nuovi siti Edge Delivery Services per le pagine localizzate.](#create-edge-sites)
1. [Aggiorna la configurazione cloud in AEM per i siti localizzati.](#update-cloud-configurations)

### Aggiornare le configurazioni del sito AEM {#update-aem-configurations}

[Le configurazioni](/help/implementing/developing/introduction/configurations.md) possono essere considerate come aree di lavoro che possono essere utilizzate per raccogliere gruppi di impostazioni e i relativi contenuti associati a scopo organizzativo. Quando crei un sito in AEM, viene creata automaticamente una configurazione per esso.

In genere si desidera condividere determinati contenuti tra siti, ad esempio:

* Modelli creati dal contenuto nella blueprint
* Modelli per frammenti di contenuto, persistenti, query e così via

Puoi creare configurazioni aggiuntive per facilitare tale condivisione. Per il caso d’uso WKND, sono necessarie configurazioni per i seguenti percorsi.

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

In altre parole, avrai una configurazione per la directory principale del contenuto del brand wknd (`/content/wknd`) utilizzato dai blueprint e una configurazione utilizzata da ciascun sito localizzato (Svizzera e Germania).

1. Accedi all’istanza di authoring AEM.
1. Passare a **Browser configurazioni** scegliendo **Strumenti** -> **Generale** -> **Browser configurazioni**.
1. Seleziona la configurazione creata automaticamente per il progetto (in questo caso wknd), quindi tocca o fai clic su **Crea** nella barra degli strumenti.
1. Nella finestra di dialogo **Crea configurazione**, fornisci un **Nome** descrittivo per il sito localizzato (ad esempio `Switzerland`) e per il **Titolo** utilizza lo stesso titolo della dimensione localizzata (in questo caso `ch`).
1. Seleziona la funzione **Configurazione cloud** e le eventuali funzioni aggiuntive necessarie per il progetto, ad esempio **Modelli modificabili**.
1. Tocca o fai clic su **Crea**.

Crea le configurazioni per ogni sito localizzato necessario. Nel caso di wknd, è necessario creare una configurazione per `de` insieme alla configurazione `ch`.

Una volta create le configurazioni, è necessario assicurarsi che i siti localizzati le utilizzino.

1. Accedi all’istanza di authoring AEM.
1. Passa alla **console Sites** da **navigazione** -> **siti**.
1. Selezionare il sito localizzato come `Switzerland`.
1. Tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Nella finestra delle proprietà della pagina, seleziona la scheda **Avanzate** e, nell&#39;intestazione **Configurazione**, deseleziona l&#39;opzione **Ereditata da /content/wknd**, dove `wknd` è la directory principale del sito.
1. Nel campo **Configurazione cloud**, utilizza il browser percorsi per selezionare la configurazione creata per il sito localizzato, ad esempio `Switzerland` in `/conf/wknd/ch`.
1. Tocca o fai clic su **Salva e chiudi**.

Assegna le rispettive configurazioni ai siti localizzati aggiuntivi. Nel caso di wknd, è necessario assegnare la configurazione `/conf/wknd/de` anche al sito Germania.

### Creazione di nuovi siti Edge Delivery Services per le pagine localizzate {#create-edge-sites}

Per collegare più siti a Edge Delivery Services per una configurazione di siti multilingue e con più aree geografiche, è necessario impostare un nuovo sito aem.live per ciascuno dei siti MSM AEM. Esiste una relazione 1:1 tra i siti MSM dell’AEM e i siti aem.live con un archivio Git condiviso e una base di codice.

In questo esempio verrà creato il sito `wknd-ch` per la presenza svizzera di WKND, il cui contenuto localizzato si trova nel percorso AEM `/content/wknd/ch`.

1. Recupera il token di autenticazione e l’account tecnico per il programma.
   * Per informazioni dettagliate su come [ottenere il token di accesso](/help/edge/wysiwyg-authoring/repoless.md#access-token) e l&#39;account tecnico [del programma, consulta il documento **Riutilizzo del codice tra siti**.](/help/edge/wysiwyg-authoring/repoless.md#access-control)
1. Crea un nuovo sito effettuando la seguente chiamata al servizio di configurazione. Considera:
   * Il nome del progetto nell’URL del POST deve essere il nuovo nome del sito che stai creando. In questo esempio è `wknd-ch`.
   * La configurazione di `code` deve essere la stessa utilizzata per la creazione iniziale del progetto.
   * `content` > `source` > `url` deve essere adattato al nome del nuovo sito che stai creando. In questo esempio è `wknd-ch`.
   * Ad esempio, il nome del sito nell&#39;URL di POST e `content` > `source` > `url` devono essere uguali.

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
                       "*@adobe.com"
                   ],
                   "publish": [
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

1. Verificare che la configurazione pubblica del nuovo sito funzioni chiamando `https://main--wknd-ch--<your-github-org>.aem.page/config.json` e verificando il contenuto del JSON restituito.

Ripeti i passaggi per creare altri siti localizzati. Nel caso di wknd, è necessario creare anche un sito `wknd-de` per la presenza tedesca.

### Aggiornare le configurazioni cloud in AEM per le pagine localizzate {#update-cloud-configurations}

Le pagine in AEM devono essere configurate per utilizzare i nuovi siti Edge Delivery creati nella sezione precedente per la presenza localizzata. In questo esempio, il contenuto in `/content/wknd/ch` deve sapere come utilizzare il sito `wknd-ch` creato. Analogamente, il contenuto in `/content/wknd/de` deve utilizzare il sito `wknd-de`.

1. Accedi all&#39;istanza di creazione dell&#39;AEM e vai a **Strumenti** -> **Cloud Service** -> **Configurazione Edge Delivery Services**.
1. Seleziona la configurazione creata automaticamente per il progetto e quindi la cartella creata per la pagina localizzata. In questo caso, la Svizzera (`ch`).
1. Tocca o fai clic su **Crea** > **Configurazione** nella barra degli strumenti.
1. Nella finestra **Configurazione Edge Delivery Services**:
   * Fornisci la tua organizzazione GitHub nel campo **Organizzazione**.
   * Modifica il nome del sito con il nome del sito creato nella sezione precedente. In questo caso, sarebbe `wknd-ch`.
   * Cambia il tipo di progetto in **aem.live con configurazione di repoless**.
1. Tocca o fai clic su **Salva e chiudi**.

## Verifica la configurazione {#verify}

Dopo aver apportato tutte le modifiche di configurazione necessarie, verifica che tutto funzioni come previsto.

1. Accedi all’istanza di authoring AEM.
1. Passa alla **console Sites** da **navigazione** -> **siti**.
1. Selezionare il sito localizzato come `Switzerland`.
1. Tocca o fai clic su **Modifica** nella barra degli strumenti.
1. Assicurati che la pagina venga riprodotta correttamente nell’Editor universale e utilizzi lo stesso codice della directory principale del sito.
1. Apporta una modifica alla pagina e ripubblica.
1. Visita il tuo nuovo sito Edge Delivery Services per la pagina localizzata all&#39;indirizzo `https://main--wknd-ch--<your-github-org>.aem.page`.

Se visualizzi le modifiche apportate, la configurazione MSM funziona correttamente.
