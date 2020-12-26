---
title: Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Sites]
description: 'Utilizzate le risorse disponibili in una distribuzione remota. [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] '
contentOwner: AG
translation-type: tm+mt
source-git-commit: caf50490c573c2f119f2cbfa14ee7cca12854364
workflow-type: tm+mt
source-wordcount: '2688'
ht-degree: 28%

---


# Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Nelle grandi aziende l’infrastruttura necessaria per la creazione di siti web può essere dislocata in luoghi diversi. A volte, le funzionalità per la creazione di siti web e le risorse digitali utilizzate per creare i siti possono trovarsi in implementazioni diverse. Un motivo può essere rappresentato dalla distribuzione geografica delle implementazioni esistenti necessarie per lavorare in parallelo. Un altro motivo può essere costituito dalle acquisizioni che portano a un&#39;infrastruttura eterogenea che la società madre desidera utilizzare insieme.

Gli utenti possono creare pagine Web in [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] è il sistema Digital Asset Management (DAM) che fornisce le risorse necessarie per i siti Web. [!DNL Experience Manager] supporta ora il caso d&#39;uso di cui sopra integrando  [!DNL Sites] e  [!DNL Assets].

## Panoramica della funzione Risorse collegate {#overview-of-connected-assets}

Quando modificate le pagine in [!UICONTROL Editor pagina] come destinazione, gli autori possono cercare, sfogliare e incorporare facilmente le risorse da una diversa distribuzione [!DNL Assets] che funge da origine delle risorse. Gli amministratori creano un&#39;integrazione una tantum di una distribuzione di [!DNL Experience Manager] con funzionalità [!DNL Sites] con un&#39;altra implementazione di [!DNL Experience Manager] con funzionalità [!DNL Assets].

Per gli autori [!DNL Sites], le risorse remote sono disponibili come risorse locali di sola lettura. Questa funzionalità supporta la ricerca e l’utilizzo di un numero limitato di risorse remote alla volta. Per rendere disponibili molte risorse remote in una distribuzione [!DNL Sites] in una sola volta, è consigliabile migrare le risorse in massa.

### Prerequisiti e implementazioni supportate {#prerequisites}

Prima di utilizzare o configurare questa funzionalità, verifica questi aspetti:

* Gli utenti fanno parte dei gruppi di utenti appropriati per ciascuna distribuzione.
* Per i tipi di distribuzione [!DNL Adobe Experience Manager], uno dei criteri supportati è soddisfatto. Per ulteriori informazioni sul funzionamento di questa funzionalità in [!DNL Experience Manager] 6.5, vedere [Risorse collegate nell&#39;Experience Manager  6.5 Risorse](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] come  [!DNL Cloud Service] | [!DNL Experience Manager] 6.5  [!DNL Sites] su AMS | [!DNL Experience Manager] 6.5  [!DNL Sites] in sede |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]come[!DNL Cloud Service]** | Supportato | Supportato | Supportato |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] su AMS** | Supportato | Supportato | Supportato |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] in sede** | Non supportato | Non supportato | Non supportato |

### Formati di file supportati {#mimetypes}

Gli autori ricercano le immagini e i seguenti tipi di documenti in Content Finder e utilizzano le risorse ricercate in Editor pagina. I documenti vengono aggiunti al componente `Download` e le immagini al componente `Image`. Gli autori possono inoltre aggiungere le risorse remote in qualsiasi componente [!DNL Experience Manager] personalizzato che estende i componenti predefiniti `Download` o `Image`. I formati supportati sono:

* **Formati** immagine: Formati supportati dal  [componente ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) Immagine. [!DNL Dynamic Media] le immagini non sono supportate.
* **Formati** del documento: Vedere i formati [ di documento ](file-format-support.md#document-formats)supportati.

### Utenti e gruppi interessati {#users-and-groups-involved}

Di seguito sono descritti i diversi ruoli coinvolti nella configurazione e nell’utilizzo della funzionalità e i relativi gruppi di utenti. L&#39;ambito locale viene utilizzato per il caso di utilizzo in cui un autore crea una pagina Web. L&#39;ambito remoto viene utilizzato per la distribuzione DAM. Le risorse remote vengono recuperate dall&#39;autore [!DNL Sites].

| Ruolo | Ambito | Gruppo di utenti | Nome utente nella procedura dettagliata | Requisito |
|------|--------|-----------|-----|----------|
| [!DNL Sites] administrator | Locale | [!DNL Experience Manager] `administrators` | `admin` | Configurare [!DNL Experience Manager] e configurare l&#39;integrazione con la distribuzione remota [!DNL Assets]. |
| Utente DAM | Locale | `Authors` | `ksaner` | Utilizzato per visualizzare e duplicare le risorse recuperate in `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Locale | <ul><li>`Authors` (con accesso in lettura sul DAM remoto e accesso dell&#39;autore sul locale  [!DNL Sites]) </li> <li>`dam-users` locale  [!DNL Sites]</li></ul> | `ksaner` | Gli utenti finali sono [!DNL Sites] autori che utilizzano questa integrazione per migliorare la velocità dei contenuti. Gli autori ricercano e sfogliano le risorse in DAM remoto utilizzando [!UICONTROL Content Finder] e utilizzando le immagini richieste nelle pagine Web locali. Vengono utilizzate le credenziali dell’utente `ksaner` di DAM. |
| [!DNL Assets] administrator | Remoto | [!DNL Experience Manager] `administrators` | `admin` su remoto  [!DNL Experience Manager] | Configurare la condivisione risorse tra le origini (CORS, Cross-Origin Resource Sharing). |
| Utente DAM | Remoto | `Authors` | `ksaner` su remoto  [!DNL Experience Manager] | Ruolo di authoring nella distribuzione remota [!DNL Experience Manager]. Cercate e sfogliate le risorse in Risorse collegate utilizzando il Content Finder][!UICONTROL  |
| Distributore DAM (utente tecnico) | Remoto | <ul> <li> [!DNL Sites] `Authors`</li> <li> `connectedassets-assets-techaccts` </li> </ul> | `ksaner` su remoto  [!DNL Experience Manager] | Questo utente presente nella distribuzione remota viene utilizzato dal server locale [!DNL Experience Manager] (non dal ruolo di [!DNL Sites] autore) per recuperare le risorse remote, per conto dell&#39;autore [!DNL Sites]. Questo ruolo non è lo stesso dei due ruoli `ksaner` precedenti e appartiene a un gruppo di utenti diverso. |
| [!DNL Sites] utente tecnico | Locale | `connectedassets-sites-techaccts` | - | Consente la distribuzione [!DNL Assets] di cercare riferimenti alle risorse nelle [!DNL Sites] pagine Web. |

## Configurare una connessione tra [!DNL Sites] e [!DNL Assets] distribuzioni {#configure-a-connection-between-sites-and-assets-deployments}

Un amministratore [!DNL Experience Manager] può creare questa integrazione. Una volta create, le autorizzazioni necessarie per utilizzarle vengono stabilite tramite i gruppi di utenti. I gruppi di utenti sono definiti nella distribuzione [!DNL Sites] e nella distribuzione DAM.

Per configurare le risorse connesse e la connettività [!DNL Sites] locale, effettua le seguenti operazioni:

1. Accedi a una distribuzione [!DNL Sites] esistente. Questa distribuzione [!DNL Sites] viene utilizzata per l&#39;authoring delle pagine Web, ad esempio in `https://[sites_servername]:port`. Poiché l&#39;authoring delle pagine avviene durante la [!DNL Sites] distribuzione, chiamiamo la distribuzione [!DNL Sites] locale dal punto di vista dell&#39;authoring delle pagine.

1. Accedi a una distribuzione [!DNL Assets] esistente. Questa distribuzione [!DNL Assets] viene utilizzata per gestire le risorse digitali, ad esempio in `https://[assets_servername]:port`.

1. Assicurarsi che gli utenti e i ruoli con l&#39;ambito appropriato siano presenti nella distribuzione [!DNL Sites] e nella distribuzione [!DNL Assets] su AMS. Crea un utente tecnico nella [!DNL Assets] distribuzione e aggiungi al gruppo di utenti indicato in [utenti e gruppi coinvolti](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Accedi alla distribuzione [!DNL Sites] locale in `https://[sites_servername]:port`. Fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Configurazione risorse collegate]**. Immettete i seguenti valori:

   1. Un **[!UICONTROL Titolo]** della configurazione.
   1. **[!UICONTROL URL DAM remoto]** è l&#39;URL della  [!DNL Assets] posizione nel formato  `https://[assets_servername]:[port]`.
   1. Credenziali di un distributore DAM (utente tecnico).
   1. Nel campo **[!UICONTROL Punto di montaggio]**, immettete il percorso locale [!DNL Experience Manager] in cui [!DNL Experience Manager] recupera le risorse. Ad esempio, la cartella `connectedassets`. Le risorse recuperate da DAM vengono memorizzate in questa cartella nella distribuzione [!DNL Sites].
   1. **[!UICONTROL L’]** URL dei siti locali è il percorso della  [!DNL Sites] distribuzione. [!DNL Assets] Questo valore viene utilizzato per mantenere i riferimenti alle risorse digitali recuperate dalla  [!DNL Sites] distribuzione.
   1. Credenziali di [!DNL Sites] utente tecnico.
   1. Il valore del campo **[!UICONTROL Soglia di ottimizzazione trasferimento binario originale]** specifica se le risorse originali (comprese le rappresentazioni) vengono trasferite in modo sincrono o meno. Le risorse con file di dimensioni ridotte possono essere recuperate rapidamente, mentre le risorse con file di dimensioni relativamente maggiori sono sincronizzate in modo asincrono. Il valore dipende dalle funzionalità di rete.
   1. Seleziona **[!UICONTROL Archivio dati condiviso con risorse collegate]** se per memorizzare le risorse utilizzi un archivio dati in comune tra le due implementazioni di In questo caso, il limite di soglia non ha importanza in quanto i binari di attività effettivi sono disponibili nell&#39;archivio dati e non sono trasferiti.

   ![Configurazione tipica per la funzionalità delle risorse connesse](assets/connected-assets-typical-config.png)

   *Figura: Configurazione tipica per la funzionalità delle risorse connesse.*

1. Le risorse digitali esistenti nella distribuzione [!DNL Assets] sono già elaborate e le rappresentazioni vengono generate. che vengono recuperate utilizzando questa funzionalità e non è quindi necessario rigenerare le rappresentazioni. Disattivate gli avviatori del flusso di lavoro per impedire la rigenerazione delle rappresentazioni. Regolate le configurazioni del modulo di avvio nella distribuzione ([!DNL Sites]) per escludere la cartella `connectedassets` (le risorse vengono recuperate in questa cartella).

   1. Durante la distribuzione di [!DNL Sites], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Avviatori]**.

   1. Individua i moduli di avvio con flussi di lavoro come **[!UICONTROL Aggiorna risorsa DAM]** e **[!UICONTROL Writeback di metadati DAM]**.

   1. Seleziona il modulo di avvio del flusso di lavoro e fai clic su **[!UICONTROL Proprietà]** nella barra delle azioni.

   1. Nella procedura guidata [!UICONTROL Proprietà], modificare i campi **[!UICONTROL Path]** come le seguenti mappature per aggiornare le espressioni regolari per escludere il punto di montaggio **[!UICONTROL connection assets]**.

   | Prima | Dopo |
   | ------------------------------------------------------- | -------------------------------------------------------------------------- |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Quando gli autori recuperano una risorsa, vengono recuperati tutti i rendering disponibili nell’implementazione remota. Se desideri creare più rendering per una risorsa recuperata, ignora questo passaggio di configurazione. Il flusso di lavoro [!UICONTROL DAM Update Asset] viene attivato e crea più rappresentazioni. Queste rappresentazioni sono disponibili solo nella [!DNL Sites] distribuzione locale e non nella distribuzione DAM remota.

1. Aggiungete la distribuzione [!DNL Sites] come origine consentita nella configurazione CORS nella distribuzione [!DNL Assets]. Per ulteriori informazioni, vedere [comprendere CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

<!-- TBD: Check if Launchers are to be disabled on CS instances. Is this option even available to the users on CS? -->

## Utilizzare le risorse remote {#use-remote-assets}

Gli autori del sito Web utilizzano Content Finder per connettersi alla distribuzione DAM. Gli autori possono sfogliare, cercare e trascinare le risorse remote in un componente. Per eseguire l’autenticazione nel DAM remoto, tieni a portata di mano le credenziali dell’utente DAM fornite dal tuo amministratore.

Gli autori possono utilizzare le risorse disponibili nella DAM locale e nella distribuzione DAM remota, in una singola pagina Web. Utilizza Content Finder per passare dalla ricerca nel DAM locale alla ricerca nel DAM remoto.

Vengono recuperati solo i tag delle risorse remote con un tag corrispondente esatto insieme alla stessa gerarchia tassonomia, disponibile nella distribuzione locale [!DNL Sites]. Tutti gli altri tag vengono eliminati. Gli autori possono cercare risorse remote utilizzando tutti i tag presenti nella distribuzione remota [!DNL Experience Manager], in quanto offre una ricerca full-text.

### Procedura dettagliata per l’utilizzo {#walk-through-of-usage}

Utilizza la configurazione precedente per provare l’esperienza di authoring e comprendere il funzionamento di questa caratteristica. Utilizza documenti o immagini di tua scelta nell’implementazione remota di DAM.

1. Andate all&#39;interfaccia [!DNL Assets] nella distribuzione remota accedendo a **[!UICONTROL Risorse]** > **[!UICONTROL File]** dall&#39;area di lavoro [!DNL Experience Manager]. In alternativa, puoi accedere a `https://[assets_servername_ams]:[port]/assets.html/content/dam` in un browser. Carica le risorse che hai scelto.
1. Nella [!DNL Sites] distribuzione, nell&#39;attivatore del profilo in alto a destra, fare clic su **[!UICONTROL Impersona come]**. Specifica `ksaner` come nome utente, seleziona l’opzione fornita e fai clic su **[!UICONTROL OK]**.
1. Apri una pagina del sito web We.Retail in **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Modifica la pagina. In alternativa, accedi a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` tramite un browser per modificare una pagina.

   Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell’angolo in alto a sinistra della pagina.

1. Aprite la scheda [!UICONTROL Risorse] e fate clic su **[!UICONTROL Accedi a Risorse collegate]**.
1. Immetti le credenziali: `ksaner` come nome utente e `password` come password. Questo utente dispone di autorizzazioni di authoring sia per le [!DNL Experience Manager] distribuzioni.
1. Cerca la risorsa aggiunta a DAM. Le risorse remote vengono visualizzate nel pannello a sinistra. Filtra immagini o documenti e filtra ulteriormente i tipi di documenti supportati. Trascina le immagini su un componente `Image`, e i documenti su un componente `Download`.

   Le risorse recuperate sono di sola lettura nella distribuzione locale [!DNL Sites]. Potete comunque utilizzare le opzioni fornite dai componenti [!DNL Sites] per modificare la risorsa recuperata. La modifica per componenti non è distruttiva.

   ![Opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto.*

1. Un autore del sito riceve una notifica se una risorsa viene recuperata in modo asincrono e se un’attività di recupero ha esito negativo. Durante l&#39;authoring o anche dopo l&#39;authoring, gli autori possono visualizzare informazioni dettagliate sulle attività di recupero e sugli errori nell&#39;interfaccia utente [processi asincroni](/help/operations/asynchronous-jobs.md).

   ![Notifica relativa al recupero asincrono delle risorse in background.](assets/assets_async_transfer_fails.png)

   *Figura: notifica relativa al recupero asincrono delle risorse in background.*

1. Quando si pubblica una pagina, [!DNL Experience Manager] visualizza un elenco completo delle risorse utilizzate nella pagina. Assicurati che le risorse remote vengano recuperate correttamente al momento della pubblicazione. Per verificare lo stato di ciascuna risorsa recuperata, vedete l&#39;interfaccia utente [processi asincroni](/help/operations/asynchronous-jobs.md).

   >[!NOTE]
   >
   >La pagina viene pubblicata anche se una o più risorse remote non vengono recuperate. Il componente che utilizza la risorsa remota viene pubblicato come vuoto. L&#39;area di notifica [!DNL Experience Manager] visualizza una notifica per gli errori che vengono visualizzati nella pagina dei processi asincroni.

>[!CAUTION]
>
>Una volta utilizzate in una pagina Web, le risorse remote recuperate sono ricercabili e utilizzabili da chiunque disponga delle autorizzazioni per accedere alla cartella locale. Le risorse recuperate vengono memorizzate nella cartella locale (`connectedassets` nel passaggio precedente). Le risorse possono inoltre essere cercate e visualizzate nell’archivio locale tramite [!UICONTROL Content Finder].

Le risorse recuperate possono essere utilizzate come qualsiasi altra risorsa locale, ad eccezione del fatto che i metadati associati non possono essere modificati.

### Verificare l&#39;utilizzo di una risorsa tra le pagine Web {#asset-usage-references}

[!DNL Experience Manager] consente agli utenti DAM di controllare tutti i riferimenti a una risorsa. Consente di comprendere e gestire l’utilizzo di una risorsa in [!DNL Sites] e nelle risorse composte. Molti autori di pagine Web sulla [!DNL Experience Manager Sites] distribuzione possono utilizzare una risorsa su un [!DNL Assets] remoto in diverse pagine Web. Per semplificare la gestione delle risorse e non generare riferimenti interrotti, è importante che gli utenti DAM verifichino l’utilizzo di una risorsa tra le pagine Web locali e remote. La scheda [!UICONTROL Riferimenti] nella pagina [!UICONTROL Proprietà] di una risorsa elenca i riferimenti locali e remoti della risorsa.

Per visualizzare e gestire i riferimenti nella distribuzione [!DNL Assets], attenetevi alla seguente procedura:

1. Selezionate una risorsa nella console [!DNL Assets] e fate clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Fare clic sulla scheda **[!UICONTROL Riferimenti]**. Consultate **[!UICONTROL Riferimenti locali]** per l&#39;utilizzo della risorsa nella distribuzione [!DNL Assets]. Consultate **[!UICONTROL Riferimenti remoti] per l&#39;utilizzo della risorsa nella [!DNL Sites] distribuzione in cui è stata recuperata la risorsa utilizzando la funzionalità Risorse collegate.

   ![riferimenti remoti nelle proprietà della risorsa](assets/connected-assets-remote-reference.png)

1. I riferimenti per le pagine [!DNL Sites] mostrano il totale dei riferimenti per ogni [!DNL Sites] locale. L&#39;individuazione di tutti i riferimenti e la visualizzazione del numero totale di riferimenti potrebbe richiedere del tempo.
1. L’elenco dei riferimenti è interattivo e gli utenti DAM possono fare clic su un riferimento per aprire la pagina di origine del riferimento. Se per qualche motivo non è possibile recuperare i riferimenti remoti, viene visualizzata una notifica che informa l&#39;utente dell&#39;errore.
1. Gli utenti possono spostare o eliminare la risorsa. Quando spostate o eliminate una risorsa, il numero totale di riferimenti di tutte le risorse/cartelle selezionate viene visualizzato in una finestra di dialogo di avviso. Quando eliminate una risorsa per la quale non sono ancora visualizzati i riferimenti, viene visualizzata una finestra di dialogo di avviso.

   ![forza eliminazione avviso](assets/delete-referenced-asset.png)

## Limitazioni e best practice {#tip-and-limitations}

* Per informazioni dettagliate sull&#39;utilizzo delle risorse, configurate la funzionalità [Asset Insight](/help/assets/assets-insights.md) sull&#39;istanza [!DNL Sites].

### Gestione delle autorizzazioni e delle risorse {#permissions-and-managing-assets}

* Le risorse locali non vengono sincronizzate con le risorse originali nell’implementazione remota. Eventuali modifiche, eliminazioni o revoche delle autorizzazioni nell’implementazione DAM non vengono propagate downstream.
* Le risorse locali sono copie in sola lettura. [!DNL Experience Manager]I componenti apportano modifiche non distruttive alle risorse. Non sono consentite altre modifiche.
* Le risorse recuperate localmente sono disponibili solo a scopo di authoring. I flussi di lavoro di aggiornamento delle risorse non possono essere applicati e i metadati non possono essere modificati.
* Sono supportati solo le immagini e i formati di documento elencati. [!DNL Dynamic Media]Le risorse , i frammenti di contenuto e i frammenti di esperienza non sono supportati.
* [!DNL Experience Manager] non recupera gli schemi di metadati. Ciò significa che tutti i metadati recuperati potrebbero non essere visualizzati. Se lo schema viene aggiornato separatamente, vengono visualizzate tutte le proprietà.
* Tutti gli autori [!DNL Sites] dispongono di autorizzazioni di lettura sulle copie recuperate, anche se gli autori non possono accedere alla distribuzione DAM remota.
* Nessun supporto API per personalizzare l’integrazione.
* Questa funzionalità supporta la ricerca e l’utilizzo diretti delle risorse remote. Per rendere disponibili molte risorse remote nell’implementazione locale con un’unica operazione, è consigliabile eseguire la migrazione delle risorse.
* Non è possibile utilizzare una risorsa remota come miniatura di pagina nell&#39;interfaccia utente [!UICONTROL Proprietà pagina]. È possibile impostare una miniatura di una pagina Web nell&#39;interfaccia utente [!UICONTROL Proprietà pagina] dalla [!UICONTROL Miniatura] facendo clic su [!UICONTROL Seleziona immagine].

### Configurazione e licenze {#setup-licensing}

* [!DNL Assets] la distribuzione  [!DNL Adobe Managed Services] è supportata.
* [!DNL Sites] può connettersi a un singolo  [!DNL Assets] archivio alla volta.
* Una licenza di [!DNL Assets] funzionamento come repository remoto.
* Una o più licenze di [!DNL Sites] funzionamento come distribuzione di authoring locale.

### Utilizzo {#usage}

* Gli utenti possono cercare risorse remote e trascinarle sulla pagina locale durante l’authoring. Non sono supportate altre funzionalità.
* L’operazione di recupero si interrompe per timeout dopo 5 secondi. Gli autori possono rilevare dei problemi durante il recupero delle risorse, ad esempio in caso di problemi di rete. Gli autori possono riprovare trascinando la risorsa remota da [!UICONTROL Content Finder] a [!UICONTROL Editor pagina].
* Le risorse recuperate possono essere sottoposte a semplici modifiche non distruttive e alle modifiche supportate tramite il componente `Image` di Le risorse sono di sola lettura.
* L’unico metodo per recuperare nuovamente la risorsa consiste nel trascinarla su una pagina. Non esiste un supporto API o altri metodi per recuperare nuovamente una risorsa e aggiornarla.
* Se le risorse vengono disattivate da DAM, continueranno a essere utilizzate su [!DNL Sites] pagine.
* Le voci di riferimento remote di una risorsa vengono recuperate in modo asincrono. I riferimenti e il conteggio totale non sono in tempo reale e potrebbe esserci una differenza se un autore di siti utilizza la risorsa mentre un utente DAM visualizza il riferimento. Gli utenti DAM possono aggiornare la pagina e riprovare tra qualche minuto per ottenere il totale.

## Risoluzione dei problemi {#troubleshoot}

Per risolvere gli errori più comuni, effettuate le seguenti operazioni:

* Se non riuscite a cercare risorse remote da [!UICONTROL Content Finder], accertatevi che i ruoli e le autorizzazioni richiesti siano già presenti.
* Una risorsa recuperata dalla diga remota potrebbe non essere pubblicata su una pagina Web per uno o più motivi. Non esiste sul server remoto, mancano le autorizzazioni necessarie per recuperarlo o l&#39;errore di rete può essere dovuto a cause. Assicurarsi che la risorsa non venga rimossa dal DAM remoto. Verificate che siano disponibili le autorizzazioni appropriate e che i prerequisiti siano soddisfatti. Provate ad aggiungere la risorsa alla pagina e ripubblicatela. Controlla l’[elenco dei processi asincroni](/help/operations/asynchronous-jobs.md) per verificare la presenza di errori nel recupero delle risorse.
* Se non riuscite ad accedere alla distribuzione DAM remota dalla distribuzione locale [!DNL Sites], accertatevi che i cookie intersito siano consentiti. Se i cookie cross-site sono bloccati, le due distribuzioni di [!DNL Experience Manager] potrebbero non essere autenticate. Ad esempio, [!DNL Google Chrome] in modalità Incognito può bloccare i cookie di terze parti. Per consentire i cookie nel browser [!DNL Chrome], fai clic sull&#39;icona a forma di occhio nella barra degli indirizzi, vai a Sito che non funziona > Bloccato, seleziona l&#39;URL DAM remoto e consenti il cookie del token di login. In alternativa, consultare la Guida relativa all&#39;attivazione dei cookie di terze parti [e](https://support.google.com/chrome/answer/95647).

   ![Errore del cookie in Chrome in modalità incognito](assets/chrome-cookies-incognito-dialog.png)

* Se i riferimenti remoti non vengono recuperati e si verifica un messaggio di errore, verificate che la distribuzione di Siti sia disponibile e verificate la presenza di problemi di connettività di rete. Riprovare più tardi per controllare. [!DNL Assets] la distribuzione tenta due volte di stabilire la connessione con la  [!DNL Sites] distribuzione e quindi segnala un errore.

![impossibile ripetere i riferimenti remoti della risorsa](assets/reference-report-failure.png)
