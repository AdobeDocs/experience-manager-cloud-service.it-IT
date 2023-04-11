---
title: Note sulla versione [!DNL Workfront for Experience Manager enhanced connector]
description: Note sulla versione [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: a65f736f922bcb58c09773ff9c6d6f7104b6157d
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 1%

---

# Note sulla versione [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

La sezione seguente illustra le note generali sulla versione di [!DNL Workfront for Experience Manager enhanced connector].

## Data di pubblicazione {#release-date}

Data di rilascio dell’ultima versione 1.9.9 di [!DNL Workfront for Experience Manager enhanced connector] è il 10 aprile 2023.

## Funzioni principali {#release-highlights}

La versione più recente del [!DNL Workfront for Experience Manager enhanced connector] include gli aggiornamenti:

* Experience Manager visualizza un `DateTimeParseException` eccezione quando riceve l’ultima data di modifica da Workfront durante la creazione della cartella collegata.

* Problemi durante la creazione di più cartelle di progetto collegate in un breve periodo di tempo.

* Impossibile configurare un limite di soglia per il numero di nuove cartelle collegate al progetto.

>[!IMPORTANT]
>
>L’Adobe consiglia di [aggiornamento alla versione più recente 1.9.9](../assets/update-workfront-enhanced-connector.md) del [!DNL Workfront for Experience Manager enhanced connector].

## Problemi noti {#known-issues}

* Durante la configurazione di cartelle collegate a un progetto con AEM 6.4, Experience Manager non salva i valori per **[!UICONTROL sottocartelle]** e **[!UICONTROL Crea cartella collegata in progetti con portfolio]** campi. Il valore per **[!UICONTROL sottocartelle]** aggiornamenti dei campi in **[!UICONTROL indefinito]** e il valore per **[!UICONTROL Crea cartella collegata in progetti con portfolio]** aggiornamenti dei campi in **[!UICONTROL Portfolio predefinito]** automaticamente dopo il salvataggio della configurazione.

* Quando utilizzi l’esperienza Workfront classica, la **[!UICONTROL Invia a]** opzione disponibile in **[!UICONTROL Altro]** l’elenco a discesa non consente di selezionare la destinazione all’interno di Experience Manager. La **[!UICONTROL Invia a]** funziona correttamente utilizzando **[!UICONTROL Azioni documento]** elenco a discesa. La **[!UICONTROL Invia a]** funziona correttamente per **[!UICONTROL Altro]** l’elenco a discesa e **[!UICONTROL Azioni documento]** elenco a discesa disponibile nella nuova esperienza Workfront.

## Versioni precedenti {#previous-releases}

### Versione di marzo 2023 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.8, rilasciata il 3 marzo 2023, include i seguenti aggiornamenti:

* Miglioramenti delle prestazioni in Experience Manager durante la creazione di cartelle collegate a un progetto in Workfront.

* Le eliminazioni di commenti in Workfront ora si riflettono nell’Experience Manager.

* Possibilità di gestire il blocco dei nuovi clienti di rete su Experience Manager as a Cloud Service dalla configurazione del connettore.


### Versione di gennaio 2023 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.7, rilasciata il 20 febbraio 2023, include i seguenti aggiornamenti:

* L’editor dei metadati non elenca le proprietà dei moduli personalizzati Workfront dopo l’installazione della versione 1.9.6.

* Viene visualizzata la console di sviluppo `/content/dam/jcr:content/metadata/wfProjectURL not found` messaggio di errore dopo l’installazione del connettore avanzato Workfront e l’apertura della home page di Assets.

### Versione di dicembre 2022 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.6, rilasciata il 09 dicembre, include i seguenti aggiornamenti:

**Miglioramento**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* Il connettore avanzato di Workfront ora supporta l’esecuzione di ricerche full-text su risorse e cartelle.

**Correzioni di bug**

* I metadati della versione del documento non vengono sincronizzati in modo appropriato tra Workfront e Experience Manager.
* Problemi durante la creazione di una cartella collegata ad Experience Manager in Workfront quando la cartella utilizza uno schema mancante nella configurazione globale.
* Il modulo dell’editor dello schema metadati smette di rispondere quando si fa clic su un campo a causa di un tempo di caricamento più lungo del previsto. È stata aggiunta una configurazione OSGi specifica per i moduli personalizzati per risolvere il problema. I nomi dei moduli personalizzati aggiunti all’editor dello schema metadati sono disponibili nei registri.

### Versione di novembre 2022 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.5, rilasciata l’11 novembre, include i seguenti aggiornamenti:

* Quando si definisce un solo valore per un campo con più valori in Workfront, il valore del campo non viene mappato in modo appropriato su Experience Manager.

* Nell’Experience Manager viene visualizzata la `SERVER_ERROR` sulla **[!UICONTROL Collega file e cartelle esterni]** durante l’accesso alle cartelle di risorse a causa di autorizzazioni non valide su `/content/dam/collections`.

* Abilitazione della **[!UICONTROL Pubblicare risorse in Brand Portal]** nella pagina di configurazione del connettore avanzato di Workfront viene creato un evento errato. L’evento non viene eliminato nemmeno dopo la disattivazione dell’opzione.

   Per risolvere il problema:

   1. Aggiornamento alla versione 1.9.5 del connettore avanzato.

   1. Disattiva la **[!UICONTROL Pubblicare risorse in Brand Portal]** in impostazioni avanzate.

   1. Abilita la **[!UICONTROL Pubblicare risorse in Brand Portal]** opzione .

   1. Elimina le sottoscrizioni di eventi errate.

      1. Esegui chiamate GET a `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Esegui una chiamata API per ogni numero di pagina.

      1. Cerca il seguente testo per trovare le sottoscrizioni di eventi che corrispondono al seguente URL e non hanno un `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Assicurati che il contenuto tra `"objId": "",` e `"url"` corrisponde alla risposta JSON. Il metodo consigliato per eseguire questa operazione è quello di copiare da qualsiasi sottoscrizione evento con un `objId` quindi eliminare il numero.

      1. Prendi nota dell’ID sottoscrizione evento.

      1. Elimina la sottoscrizione dell’evento errata. Effettuare una chiamata API Delete a `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` poiché il codice di risposta indica l’eliminazione corretta delle sottoscrizioni di eventi errate.
   >[!NOTE]
   >
   >Se hai già eliminato le sottoscrizioni di eventi errate prima di eseguire i passaggi indicati in questa procedura, puoi saltare l’ultimo passaggio di questa procedura.

### Versione di ottobre 2022 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.4, rilasciata il 07 ottobre, include i seguenti aggiornamenti:

* Impossibile visualizzare la scheda Sottoscrizioni evento nella pagina di configurazione del connettore avanzato a causa di un numero elevato di eventi.

* Workfront non è in grado di recuperare l’elenco delle cartelle esistenti in un progetto, con conseguente creazione di cartelle duplicate.

### Versione di settembre 2022 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.3, rilasciata il 16 settembre, include i seguenti aggiornamenti:

* Impossibile caricare un file di dimensioni superiori a 8 GB.
* Problemi durante la pubblicazione automatica delle risorse inviate da Workfront a AEM.
* Il campo Percorso principale non è disponibile per il campo Tag durante la modifica di un modulo schema metadati predefinito.
* Problemi durante l’aggiunta di nuove versioni in Workfront tramite flussi di lavoro AEM.
* Quando esegui una ricerca AEM delle risorse disponibili in Workfront, AEM visualizza un messaggio di errore.
* Quando si crea un flusso di lavoro AEM per la creazione di attività da una risorsa e non si definisce un nome di attività padre, l’attività non viene creata in Workfront.

### Versione di agosto 2022 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.2, rilasciata il 3 agosto, include i seguenti aggiornamenti:

* La **[!UICONTROL Carica documento]** il passaggio del flusso di lavoro non allega un documento a Workfront.

* La **[!UICONTROL Carica documento]** il passaggio del flusso di lavoro non allega un documento alle attività e ai problemi in Workfront. Il passaggio del flusso di lavoro collega un documento a Progetti con successo.

### Versione di luglio 2022 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versione 1.9.1 include i seguenti aggiornamenti:

* È stato aggiunto il supporto per l’autenticazione tra le applicazioni Experience Manager e Workfront tramite la chiave API Workfront per le istanze migrate ad Adobe IMS.

* Quando si collegano file o cartelle esterni, l&#39;applicazione Workfront visualizza la `SERVER_ERROR` messaggio di errore. Il messaggio di errore fa riferimento a un&#39;eccezione non autorizzata a causa di una mancata corrispondenza nelle chiavi API.

* Quando esegui un flusso di lavoro Crea attività per una risorsa, nei messaggi di registro viene visualizzata l’eccezione Null Pointer.

* Quando si abilita la `Replace Spaces with DASH` l&#39;opzione di configurazione in Impostazioni avanzate in Experience Manager si traduce in creazione di cartelle duplicate in Workfront.

### Versione di giugno 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ora include i seguenti aggiornamenti:

* Quando effettui il caricamento tramite una cartella collegata o utilizzi la `Send To` azione disponibile in Workfront per caricare le risorse in Experience Manager as a Cloud Service, le risorse vengono danneggiate e non possono essere aperte in Adobe Photoshop.

### Versione di marzo 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ora include i seguenti aggiornamenti:

* È ora possibile creare cartelle collegate tra Adobe Workfront e AEM Assets as a Cloud Service anche se sono presenti più configurazioni di cartelle collegate al progetto.

* È stato aggiunto il supporto per l’impaginazione dell’abbonamento a eventi.

* È stato aggiunto il supporto per AEM 6.4.x.

* È stato aggiunto il supporto per gli ambienti proxy.

* Diverse correzioni di bug si basano sul feedback di partner e clienti.

>[!MORELIKETHIS]
>
>* [Integrare [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [Integrare [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)