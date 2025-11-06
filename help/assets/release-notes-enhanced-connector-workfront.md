---
title: Note sulla versione di [!DNL Workfront for Experience Manager enhanced connector]
description: Note sulla versione di [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 100%

---

# Note sulla versione di [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

La sezione seguente illustra le note generali sulla versione di [!DNL Workfront for Experience Manager enhanced connector].

La data di rilascio della versione più recente 1.9.21 di [!DNL Workfront for Experience Manager enhanced connector] è il 25 giugno 2025.

## Caratteristiche principali della versione {#release-highlights}

La versione più recente di [!DNL Workfront for Experience Manager enhanced connector] include le seguenti correzioni di bug e miglioramenti:

* È stata migliorata la registrazione delle richieste API per evitare la registrazione di falsi positivi di errori di autenticazione.

* È stata risolta una perdita di connessione nelle chiamate API di Workfront.

* Supporto del connettore avanzato Workfront con 6.5 LTS per le versioni Java 17 e Java 21.

>[!NOTE]
>
>AEM 6.4 ha raggiunto il termine del supporto esteso. Consulta i nostri [periodi di supporto tecnico](https://helpx.adobe.com/it/support/programs/eol-matrix.html). Le versioni supportate sono disponibili [qui](https://experienceleague.adobe.com/docs/?lang=it).

>[!IMPORTANT]
>
>Adobe consiglia di [aggiornare alla versione 1.9.20 più recente](/help/assets/workfront-connector-install.md) di [!DNL Workfront for Experience Manager enhanced connector].

## Problemi noti {#known-issues}

* Durante la configurazione di cartelle collegate a un progetto tramite AEM 6.4, Experience Manager non salva i valori per i campi **[!UICONTROL sottocartelle]** e **[!UICONTROL Crea cartella collegata in progetti con portfolio]**. Il valore per il campo **[!UICONTROL sottocartelle]** si aggiorna a **[!UICONTROL non definito]** e il valore per il campo **[!UICONTROL Crea cartella collegata in progetti con portfolio]** si aggiorna a **[!UICONTROL Portfolio predefinito]** automaticamente, a seguito del salvataggio della configurazione.

* Durante l’utilizzo dell’esperienza Workfront classica, l’opzione **[!UICONTROL Invia a]** disponibile nell’elenco a discesa **[!UICONTROL Altro]** non consente di selezionare la destinazione target in Experience Manager. L’opzione **[!UICONTROL Invia a]** funziona correttamente utilizzando l’elenco a discesa **[!UICONTROL Azioni documento]**. L’opzione **[!UICONTROL Invia a]** funziona correttamente per gli elenchi a discesa **[!UICONTROL Altro]** e **[!UICONTROL Azioni documento]** disponibile nella nuova esperienza Workfront.

## Versioni precedenti {#previous-releases}

### Versione di settembre 2024 {#september-2024-release}

* Il tipo MIME viene perso durante il caricamento e la creazione di una nuova versione di una risorsa esistente.

### Versione di aprile 2024 {#april-2024-release}

* La mancata chiusura dei client HTTP causa problemi di memoria insufficiente.


### Versione di marzo 2024 {#march-2024-release}

* L’elaborazione dei caricamenti di più risorse da Workfront riscontra problemi.
* Non vengono aggiunte virgolette di chiusura quando si utilizza Workfront per cercare cartelle in Experience Manager`SERVER_ERROR`.

### Versione di febbraio 2024 {#february-2024-release}

* Abilita la funzione di attivazione/disattivazione per consentire ai clienti di AEM Cloud di configurare e impostare un connettore.

* La chiusura del `resourceResolver` effettuata senza chiudere esplicitamente la sessione sottostante, causa perdite di sessione nelle istanze AEM. È fondamentale chiudere esplicitamente la sessione, in quanto la chiusura automatica del Risolutore risorse non comporta la chiusura implicita della sessione.

### Versione di gennaio 2024 {#january-2024-release}

* Al momento la configurazione di [!DNL Workfront] in [!DNL CRX DE] non memorizza il `project ID`, causando errori quando si applica l’autorizzazione di sola lettura. Ulteriori informazioni su come [configurare le autorizzazioni](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html?lang=it#linked-folders).

* Nessuna documentazione pubblica disponibile su come aggiungere proprietà personalizzate alla definizione predefinita dell’indice. Ulteriori informazioni su [aggiunta di proprietà personalizzate](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html?lang=it#metadata-schema-mapping).

* L’eliminazione delle configurazioni di connessione sul connettore avanzato influisce in modo significativo sulle sottoscrizioni evento e su altre configurazioni salvate, causando il reindirizzamento a un URL precedente.

* L’installazione del pacchetto dei componenti aggiuntivi per i moduli non installa **[!UICONTROL Attiva/Disattiva router]**, con conseguente errore della funzionalità [!DNL WFEC AMS environment Toggle].

* L’abilitazione delle sottoscrizioni a eventi nella configurazione EWC comporta errori ripetuti di chiamata API con errore `HTTP 400` durante la prima configurazione del connettore migliorato [!DNL Workfront].

* L’eliminazione di commenti sulle risorse delle cartelle collegate a Workfront non riesce a trovare il percorso della cartella collegata ad AEM.

* Il supporto insufficiente per risorse di file di grandi dimensioni in AEM causa un problema di dimensioni di 4 byte.

* Nessuna elaborazione del tempo di richiesta per i flussi critici nella cartella collegata, nell’aggiornamento del documento e nell’aggiornamento delle note.

### Versione di novembre 2023 {#nov-2023-release}

* Quando si visualizza l’elenco delle cartelle AEM, il caricamento della finestra di dialogo richiede più di un minuto.
* Gli utenti di [!DNL Workfront] autorizzati ricevono regolarmente i registri di errore di autenticazione.

### Versione di ottobre 2023 {#october-2023-release}

* Quando in Impostazioni avanzate le sottoscrizioni agli eventi sono disattivate, è comunque possibile selezionare le opzioni per **iscriversi agli eventi di aggiornamento del documento per aggiornare i metadati delle risorse AEM**, **pubblicare tutte le risorse del progetto in Brand Portal al completamento del progetto** e **abilitare la sincronizzazione commenti**.

* Alcune delle risorse memorizzate in Experience Manager non vengono riprodotte correttamente quando vengono visualizzate in anteprima in Workfront.

* Durante la riconfigurazione della connessione di Experience Manager con Workfront, le sottoscrizioni agli eventi, come l’aggiornamento della sincronizzazione commenti, l’eliminazione e l’aggiornamento del documento, non vengono create correttamente.

* Miglioramenti importanti delle prestazioni API per creazione di cartelle collegate, aggiornamento, abilitazione di cartelle collegate, abilitazione e disabilitazione della sincronizzazione commenti, salvataggio anticipato delle impostazioni sul connettore.

### Versione di settembre 2023 {#september-2023-release}

* Il connettore avanzato Experience Manager recupera tutte le sottoscrizioni agli eventi da Workfront durante l’eliminazione di una sottoscrizione a un evento relativa un progetto, con conseguente impatto sulle prestazioni dell’applicazione.

* Quando viene inviata una risorsa da Workfront a Experience Manager, il tipo MIME della risorsa non è impostato su `dc:format` attributo all’interno di Experience Manager.

* Gli ID progetto Workfront memorizzati sul connettore avanzato Experience Manager includono duplicati.

### Versione di agosto 2023 {#august-2023-release}

* Impossibile creare cartelle collegate in Experience Manager. Nessun account utente associato alla cartella collegata.

* Race condition durante gli aggiornamenti dei metadati per una risorsa in Experience Manager.

### Versione di giugno 2023 {#june-2023-release}

* Dopo aver configurato la rete avanzata, si verificano problemi durante l’invio di contenuti da Adobe Workfront ad AEM as a Cloud Service.


### Versione di maggio 2023 {#may-2023-release}

* Workfront restituisce una risposta HTTP 409 per sottoscrizioni a eventi duplicate basate su una chiamata REST da Experience Manager a Workfront, che causa un’eccezione Null Pointer.

### Versione di aprile 2023 {#april-2023-release}

La versione 1.9.9 di [!DNL Workfront for Experience Manager enhanced connector], rilasciata il 10 aprile 2023, include i seguenti aggiornamenti:

* Experience Manager visualizza un’ eccezione `DateTimeParseException` quando riceve la data dell’ultima modifica da Workfront durante la creazione della cartella collegata.

* Problemi durante la creazione di più cartelle di progetto collegate in un breve periodo di tempo.

* Impossibile configurare un limite di soglia per il numero di nuovi set di cartelle collegate al progetto.

### Versione di marzo 2023 {#march-2023-release}

La versione 1.9.8 di [!DNL Workfront for Experience Manager enhanced connector], rilasciata il 3 marzo 2023, include i seguenti aggiornamenti:

* Miglioramenti delle prestazioni in Experience Manager durante la creazione di cartelle collegate a un progetto in Workfront.

* Le eliminazioni di commenti in Workfront ora si riflettono in Experience Manager.

* Possibilità di gestire il blocco di clienti di nuovi server di rete su Experience Manager as a Cloud Service partendo dalla configurazione del connettore.

### Versione di gennaio 2023 {#january-2022-release}

La versione 1.9.7 di [!DNL Workfront for Experience Manager enhanced connector], rilasciata il 2 febbraio 2023, include i seguenti aggiornamenti:

* Nell’editor metadati non sono elencate le proprietà dei moduli personalizzati di Workfront dopo l’installazione della versione 1.9.6.

* La console di sviluppo visualizza messaggio di errore `/content/dam/jcr:content/metadata/wfProjectURL not found` dopo l’installazione del connettore avanzato di Workfront e all’apertura della pagina Home di Assets.

### Versione di dicembre 2022 {#december-2022-release}

La versione 1.9.6 di [!DNL Workfront for Experience Manager enhanced connector], rilasciata il 9 dicembre, include i seguenti aggiornamenti:

**Miglioramento**

<!--

* Workfront enhanced connector now lets you use new search parameters to be more specific while defining folder names on large repositories.

-->

* Il connettore avanzato di Workfront supporta ora la ricerca testuale su risorse e cartelle.

**Correzioni di bug**

* I metadati della versione del documento non vengono sincronizzati in modo appropriato tra Workfront e Experience Manager.
* Problemi durante la creazione di una cartella collegata a Experience Manager in Workfront quando la cartella utilizza uno schema di cui manca la definizione nella configurazione globale.
* Il modulo dell’Editor schema metadati non risponde quando si fa clic su qualsiasi campo a causa di un tempo di caricamento più lungo del previsto. Per risolvere il problema è stata aggiunta una configurazione OSGi specifica per i moduli personalizzati. I nomi dei moduli personalizzati aggiunti all’Editor schema metadati sono disponibili nei registri.

### Versione di novembre 2022 {#november-2022-release}

La versione 1.9.5 di [!DNL Workfront for Experience Manager enhanced connector], rilasciata l’11 novembre, include i seguenti aggiornamenti:

* Quando viene definito un solo valore per un campo con più valori in Workfront, il valore del campo non viene mappato in modo appropriato su Experience Manager.

* Durante l’accesso alle cartelle di risorse, Experience Manager visualizza `SERVER_ERROR` sulla schermata **[!UICONTROL Collega file e cartelle esterni]** a causa di autorizzazioni non valide in `/content/dam/collections`.

* L’abilitazione dell’opzione **[!UICONTROL Pubblica risorse in Brand Portal]** nella pagina di configurazione del connettore avanzato di Workfront crea un evento non corretto. L’evento non viene eliminato neanche dopo che l’opzione viene disabilitata.

  Per risolvere il problema:

   1. Effettua l’aggiornamento alla versione 1.9.5 del connettore avanzato.

   1. In impostazioni avanzate, disattiva l’opzione **[!UICONTROL Pubblica risorse in Brand Portal]**.

   1. Abilita l’opzione **[!UICONTROL Pubblica risorse in Brand Portal]**.

   1. Elimina le sottoscrizioni evento errate.

      1. Esegui chiamate GET a `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Esegui una chiamata API per ogni numero di pagina.

      1. Per trovare sottoscrizioni a eventi che corrispondono al seguente URL e non hanno un `objId`, cerca il testo seguente:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Assicurati che il contenuto tra `"objId": "",` e `"url"` corrisponda alla risposta JSON. Il metodo consigliato per eseguire questa operazione consiste nel copiare da qualsiasi Sottoscrizione evento che dispone di `objId` e quindi eliminare il numero.

      1. Prendi nota dell’ID di sottoscrizione all’evento.
      1. Elimina la sottoscrizione all’evento errata. Effettua una chiamata API di eliminazione a `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` in quanto il codice di risposta indica l’eliminazione corretta delle sottoscrizioni a eventi errate.

         >[!NOTE]
         >
         >Se hai già eliminato le sottoscrizioni a eventi errate prima di eseguire i passaggi indicati in questa procedura, puoi saltare l’ultimo passaggio.

### Versione di ottobre 2022 {#october-2022-release}

La versione 1.9.4 di [!DNL Workfront for Experience Manager enhanced connector], rilasciata il 7 ottobre, include i seguenti aggiornamenti:

* Impossibile visualizzare la scheda Sottoscrizioni eventi nella pagina di configurazione del connettore avanzato a causa di molti eventi.

* Workfront non è in grado di recuperare l’elenco delle cartelle esistenti in un progetto, determinando la creazione di cartelle duplicate.

### Versione di settembre 2022 {#september-2022-release}

La versione 1.9.3 di [!DNL Workfront for Experience Manager enhanced connector], rilasciata il 16 settembre, include i seguenti aggiornamenti:

* Impossibile caricare un file di dimensioni superiori a 8 GB.
* Problemi durante la pubblicazione automatica delle risorse inviate da Workfront ad AEM.
* Il campo Percorso radice non è disponibile per il campo Tag durante la modifica di un modulo dello schema metadati predefinito.
* Problemi durante l’aggiunta di nuove versioni in Workfront utilizzando i flussi di lavoro di AEM.
* Quando si esegue una ricerca AEM per le risorse disponibili in Workfront, AEM mostra un messaggio di errore.
* Durante la creazione di un flusso di lavoro AEM per definire un’attività da una risorsa e non viene stabilito il nome di un’attività principale, l’attività non viene creata in Workfront.

### Versione di agosto 2022 {#august-2022-release}

La versione 1.9.2 di [!DNL Workfront for Experience Manager enhanced connector], rilasciata il 3 agosto, include i seguenti aggiornamenti:

* Il passaggio del flusso di lavoro **[!UICONTROL Carica documento]** non riesce ad allegare un documento a Workfront.

* Il passaggio del flusso di lavoro **[!UICONTROL Carica documento]** non riesce ad allegare un documento ad Attività e problemi in Workfront. Il passaggio del flusso di lavoro allega correttamente un documento ai progetti.

### Versione di luglio 2022 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.1 include i seguenti aggiornamenti:

* È stato aggiunto il supporto per l’autenticazione tra le applicazioni Experience Manager e Workfront utilizzando la chiave API di Workfront per le istanze migrate ad Adobe IMS.

* Quando si collegano file o cartelle esterni, l’applicazione Workfront visualizza il messaggio di errore `SERVER_ERROR`. Il messaggio di errore fa riferimento a un’eccezione non autorizzata a causa di una mancata corrispondenza nelle chiavi API.

* Quando esegui un flusso di lavoro Crea attività per una risorsa, nei messaggi di registro viene visualizzata l’eccezione Null Pointer.

* Quando si abilita l’opzione di configurazione `Replace Spaces with DASH` in Impostazioni avanzate in Experience Manager, vengono create cartelle duplicate in Workfront.

### Versione di giugno 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ora include i seguenti aggiornamenti:

* Quando effettui il caricamento tramite una cartella collegata o utilizzi l’azione `Send To` disponibile in Workfront per caricare le risorse in Experience Manager as a Cloud Service, le risorse vengono danneggiate e non possono essere aperte in Adobe Photoshop.

### Versione di marzo 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ora include i seguenti aggiornamenti:

* Ora puoi creare cartelle collegate tra Adobe Workfront e AEM Assets as a Cloud Service anche in presenza di più configurazioni di cartelle collegate a un progetto.

* È stato aggiunto il supporto per la paginazione delle sottoscrizioni a eventi.

* È stato aggiunto il supporto per AEM 6.4.x.

* È stato aggiunto il supporto per gli ambienti proxy.

* Sono stati corretti diversi bug in base ai feedback ricevuti da partner e clienti.

>[!MORELIKETHIS]
>
>* [Integrare [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=it)
