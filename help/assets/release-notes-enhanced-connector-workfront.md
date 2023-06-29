---
title: Note sulla versione [!DNL Workfront for Experience Manager enhanced connector]
description: Note sulla versione [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 87aeebad2576e91472530a2617b23bece4cd453f
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 1%

---

# Note sulla versione [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

La sezione seguente illustra le note generali sulla versione di [!DNL Workfront for Experience Manager enhanced connector].

## Data di pubblicazione {#release-date}

Data di rilascio dell’ultima versione 1.9.11 di [!DNL Workfront for Experience Manager enhanced connector] è il 19 giugno 2023.

## Elementi salienti della versione {#release-highlights}

Ultima versione di [!DNL Workfront for Experience Manager enhanced connector] include i seguenti aggiornamenti:

* Se hai configurato la rete avanzata, si verificano dei problemi durante l’invio di contenuti da Adobe Workfront a AEM as a Cloud Service.

>[!NOTE]
>
>L’AEM 6.4 ha raggiunto la fine del sostegno esteso. Per maggiori dettagli, consulta la nostra [periodi di assistenza tecnica](https://helpx.adobe.com/it/support/programs/eol-matrix.html). Trovare le versioni supportate [qui](https://experienceleague.adobe.com/docs/?lang=en).


>[!IMPORTANT]
>
>L’Adobe consiglia di: [aggiornamento alla versione più recente del 1.9.11](/help/assets/workfront-connector-install.md) del [!DNL Workfront for Experience Manager enhanced connector].

## Problemi noti {#known-issues}

* Durante la configurazione di cartelle collegate a un progetto con AEM 6.4, Experience Manager non salva i valori per **[!UICONTROL sottocartelle]** e **[!UICONTROL Creare una cartella collegata in progetti con portfolio]** campi. Il valore per **[!UICONTROL sottocartelle]** aggiornamenti dei campi a **[!UICONTROL non definito]** e il valore per **[!UICONTROL Creare una cartella collegata in progetti con portfolio]** aggiornamenti dei campi a **[!UICONTROL Portfolio predefinito]** dopo il salvataggio della configurazione.

* Quando utilizzi l’esperienza Workfront classica, il **[!UICONTROL Invia a]** opzione disponibile in **[!UICONTROL Altro]** L’elenco a discesa non consente di selezionare la destinazione in Experience Manager. Il **[!UICONTROL Invia a]** funziona correttamente utilizzando **[!UICONTROL Azioni documento]** elenco a discesa. Il **[!UICONTROL Invia a]** funziona correttamente per **[!UICONTROL Altro]** e la **[!UICONTROL Azioni documento]** disponibile nella nuova esperienza Workfront.

## Versioni precedenti {#previous-releases}

### Versione di maggio 2023 {#may-2023-release}

* Workfront restituisce una risposta HTTP 409 per sottoscrizioni di eventi duplicate basate su una chiamata REST da Experience Manager a Workfront, che causa un’eccezione NPE.

### Versione di aprile 2023 {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.9, rilasciata il 10 aprile 2023, include i seguenti aggiornamenti:

* L’Experience Manager mostra un `DateTimeParseException` eccezione quando riceve la data dell’ultima modifica da Workfront durante la creazione della cartella collegata.

* Problemi durante la creazione di più cartelle di progetto collegate in un breve periodo di tempo.

* Impossibile configurare un limite di soglia per il numero di nuove cartelle collegate al progetto.

### Versione di marzo 2023 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.8, rilasciata il 3 marzo 2023, include i seguenti aggiornamenti:

* Miglioramenti delle prestazioni in Experience Manager durante la creazione di cartelle collegate a un progetto in Workfront.

* Le eliminazioni di commenti in Workfront ora si riflettono in Experience Manager.

* Possibilità di gestire il blocco della configurazione del connettore da parte di nuovi clienti Experience Manager as a Cloud Service.


### Versione di gennaio 2023 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.7, rilasciata il 2 febbraio 2023, include i seguenti aggiornamenti:

* Nell’editor metadati non sono elencate le proprietà dei moduli personalizzati di Workfront dopo l’installazione della versione 1.9.6.

* Viene visualizzata la console di sviluppo `/content/dam/jcr:content/metadata/wfProjectURL not found` messaggio di errore dopo l’installazione del connettore avanzato di Workfront e l’apertura della pagina Home di Assets.

### Versione di dicembre 2022 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.6 di, rilasciata il 9 dicembre, include i seguenti aggiornamenti:

**Miglioramento**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* Il connettore avanzato di Workfront ora supporta l’esecuzione di ricerche full-text su risorse e cartelle.

**Correzioni di bug**

* I metadati della versione del documento non vengono sincronizzati in modo appropriato tra Workfront e Experience Manager.
* Problemi durante la creazione di una cartella collegata ad Experience Manager in Workfront quando la cartella utilizza uno schema di cui manca la definizione nella configurazione globale.
* Il modulo dell’editor schema metadati non risponde quando si fa clic su qualsiasi campo a causa di un tempo di caricamento più lungo del previsto. Per risolvere il problema è stata aggiunta una configurazione OSGi specifica per i moduli personalizzati. I nomi dei moduli personalizzati aggiunti all’editor schema metadati sono disponibili nei registri.

### Versione di novembre 2022 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.5 di, rilasciata l’11 novembre, include i seguenti aggiornamenti:

* Quando si definisce un solo valore per un campo con più valori in Workfront, il valore del campo non viene mappato in modo appropriato su Experience Manager.

* L&#39;Experience Manager visualizza `SERVER_ERROR` il **[!UICONTROL Collega file e cartelle esterni]** schermata durante l’accesso alle cartelle di risorse a causa di autorizzazioni non valide su `/content/dam/collections`.

* Abilitazione di **[!UICONTROL Pubblicare risorse in Brand Portal]** nella pagina di configurazione del connettore avanzato di Workfront crea un evento non corretto. L’evento non viene eliminato anche dopo la disattivazione dell’opzione.

  Per risolvere il problema:

   1. Effettua l’aggiornamento alla versione 1.9.5 del connettore avanzato.

   1. Disattiva il **[!UICONTROL Pubblicare risorse in Brand Portal]** in impostazioni avanzate.

   1. Abilita **[!UICONTROL Pubblicare risorse in Brand Portal]** opzione.

   1. Elimina le sottoscrizioni evento errate.

      1. Effettuare chiamate GET a `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Esegui una chiamata API per ogni numero di pagina.

      1. Cerca il testo seguente per trovare le sottoscrizioni di eventi che corrispondono al seguente URL e non hanno un `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Assicurati che il contenuto tra `"objId": "",` e `"url"` corrisponde alla risposta JSON. Il metodo consigliato per eseguire questa operazione consiste nel copiare da qualsiasi abbonamento a un evento con un `objId` e quindi eliminare il numero.

      1. Prendi nota dell’ID di abbonamento all’evento.

      1. Elimina la sottoscrizione di evento errata. Effettuare una chiamata API di eliminazione a `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` in quanto il codice di risposta indica l’eliminazione corretta delle sottoscrizioni di eventi errate.
  >[!NOTE]
  >
  >Se hai già eliminato le sottoscrizioni di eventi errate prima di eseguire i passaggi indicati in questa procedura, puoi saltare l’ultimo passaggio di questa procedura.

### Versione di ottobre 2022 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.4, rilasciata il 7 ottobre, include i seguenti aggiornamenti:

* Impossibile visualizzare la scheda Sottoscrizioni eventi nella pagina di configurazione del connettore avanzato a causa di molti eventi.

* Workfront non è in grado di recuperare l’elenco delle cartelle esistenti in un progetto, il che si traduce nella creazione di cartelle duplicate.

### Versione di settembre 2022 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.3 di, rilasciata il 16 settembre, include i seguenti aggiornamenti:

* Impossibile caricare un file di dimensioni superiori a 8 GB.
* Problemi durante la pubblicazione automatica delle risorse inviate da Workfront all’AEM.
* Il campo Percorso directory principale non è disponibile per il campo Tag durante la modifica di un modulo schema metadati predefinito.
* Problemi durante l’aggiunta di nuove versioni in Workfront tramite flussi di lavoro AEM.
* Quando esegui una ricerca AEM per le risorse disponibili in Workfront, AEM visualizza un messaggio di errore.
* Quando crei un flusso di lavoro AEM per la creazione di attività da una risorsa e non definisci il nome di un&#39;attività padre, l&#39;attività non viene creata in Workfront.

### Versione di agosto 2022 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.2, rilasciata il 3 agosto, include i seguenti aggiornamenti:

* Il **[!UICONTROL Carica documento]** il passaggio del flusso di lavoro non riesce ad allegare un documento a Workfront.

* Il **[!UICONTROL Carica documento]** Il passaggio del flusso di lavoro non riesce ad allegare un documento ad Attività e Problemi in Workfront. Il passaggio del flusso di lavoro allega correttamente un documento ai progetti.

### Versione di luglio 2022 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.1 include i seguenti aggiornamenti:

* È stato aggiunto il supporto per l’autenticazione tra le applicazioni Experience Manager e Workfront utilizzando la chiave API di Workfront per le istanze migrate ad Adobe IMS.

* Quando si collegano file o cartelle esterni, l&#39;applicazione Workfront visualizza `SERVER_ERROR` messaggio di errore. Il messaggio di errore fa riferimento a un’eccezione non autorizzata a causa di una mancata corrispondenza nelle chiavi API.

* Quando esegui un flusso di lavoro Crea attività per una risorsa, nei messaggi di registro viene visualizzata l’eccezione Nullo puntatore.

* Quando si abilita `Replace Spaces with DASH` L&#39;opzione di configurazione in Impostazioni avanzate in Experience Manager, genera la creazione di cartelle duplicate in Workfront.

### Versione di giugno 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ora include i seguenti aggiornamenti:

* Quando effettui il caricamento tramite una cartella collegata o utilizzi `Send To` disponibile in Workfront per caricare le risorse su Experience Manager as a Cloud Service, le risorse vengono danneggiate e non possono essere aperte in Adobe Photoshop.

### Versione di marzo 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ora include i seguenti aggiornamenti:

* Ora puoi creare cartelle collegate tra Adobe Workfront e AEM Assets as a Cloud Service anche in presenza di più configurazioni di cartelle collegate a un progetto.

* È stato aggiunto il supporto per l’impaginazione della sottoscrizione di eventi.

* È stato aggiunto il supporto per AEM 6.4.x.

* È stato aggiunto il supporto per gli ambienti proxy.

* Diverse correzioni di bug in base al feedback ricevuto da partner e clienti.

>[!MORELIKETHIS]
>
>* [Integrare [!DNL Workfront for Experience Manager enhanced connector] all&#39;Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
