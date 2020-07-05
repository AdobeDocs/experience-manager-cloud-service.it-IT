---
title: Utilizzo di Cloud Readiness Analyzer (Analisi di preparazione al cloud)
description: Utilizzo di Cloud Readiness Analyzer (Analisi di preparazione al cloud)
translation-type: tm+mt
source-git-commit: a0e58c626f94b778017f700426e960428b657806
workflow-type: tm+mt
source-wordcount: '1871'
ht-degree: 89%

---


# Utilizzo di Cloud Readiness Analyzer (Analisi di preparazione al cloud){#using-cloud-readiness-analyzer}

## Considerazioni importanti sull’utilizzo di Cloud Readiness Analyzer (Analisi di preparazione al cloud) {#imp-considerations}

La sezione seguente per contiene considerazioni importanti sull’esecuzione di Cloud Readiness Analyzer (CRA; Analisi di preparazione al cloud):

* Il rapporto CRA viene creato utilizzando l’output del [rilevatore pattern](https://docs.adobe.com/content/help/it-IT/experience-manager-65/deploying/upgrading/pattern-detector.html) di Adobe Experience Manager (AEM). La versione del rilevatore pattern utilizzata da CRA è inclusa nel pacchetto di installazione CRA.

* CRA may only be run by the **admin** user or a user in the **administrators** group.

* CRA è supportato nelle istanze AEM con versione 6.1 e successive.

   >[!NOTE]
   > Consulta [Installazione su AEM 6.1](#installing-on-aem61) per i requisiti speciali per l&#39;installazione di CRA su AEM 6.1.

* CRA può essere eseguito in qualsiasi ambiente, ma è preferibile eseguirlo in un ambiente *stage*.

   >[!NOTE]
   >Per evitare un impatto sulle istanze aziendali fondamentali, si consiglia di eseguire CRA in un ambiente di *authoring* il più simile possibile all’ambiente di *produzione* nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito su un clone dell’ambiente di *authoring* di produzione.

* La generazione del contenuto del rapporto CRA può richiedere tempi lunghi, da alcuni minuti ad alcune ore. Il tempo richiesto dipende in larga misura dalle dimensioni e dalla natura del contenuto dell’archivio AEM, dalla versione di AEM e da altri fattori.

* A causa del tempo significativo che potrebbe essere necessario per generare il contenuto del rapporto, il processo avviene in background e viene mantenuto nella cache. La visualizzazione e il download del rapporto dovrebbero essere relativamente veloci poiché viene utilizzata la cache del contenuto fino alla scadenza o all’aggiornamento esplicito del rapporto. Durante la generazione del contenuto del rapporto puoi chiudere la scheda del browser e tornare in un secondo momento per visualizzare il rapporto una volta che il relativo contenuto è disponibile nella cache.

## Disponibilità {#availability}

Cloud Readiness Analyzer può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM).

>[!NOTE]
>Scarica Cloud Readiness Analyzer (Analisi di preparazione al cloud) dal portale di [distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

## Visualizzazione del rapporto di Cloud Readiness Analyzer (Analisi di preparazione al cloud) {#viewing-report}

### Adobe Experience Manager 6.3.0 e versioni successive {#aem-later-versions}

Leggi questa sezione per scoprire come visualizzare il rapporto di Cloud Readiness Analyzer (Analisi di preparazione al cloud):

1. Seleziona Adobe Experience Manager e passa a Strumenti > **Operazioni** > **Cloud Readiness Analyzer** (Analisi di preparazione al cloud).

   ![immagine](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Dopo aver fatto clic su **Cloud Readiness Analyzer** (Analisi di preparazione al cloud), lo strumento inizia a generare il rapporto e, una volta disponibile, lo visualizza.

   >[!NOTE]
   >Per visualizzare il rapporto completo, dovrai scorrere la pagina verso il basso.

   ![immagine](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-1.png)

1. Una volta generato e visualizzato il rapporto CRA, puoi scaricarlo in formato con valori delimitati da virgole facendo clic su **CSV**, come illustrato nella figura riportata di seguito.

   ![immagine](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-2.png)

   >[!NOTE]
   >Per cancellare la cache e generare nuovamente il rapporto CRA, fai clic su **Refresh Report** (Aggiorna rapporto).

###  Adobe Experience Manager 6.2 e 6.1 {#aem-specific-versions}

In Adobe Experience Manager 6.2, lo strumento Cloud Readiness Analyzer (Analisi di preparazione al cloud) è limitato a un collegamento che consente di generare e scaricare il rapporto CSV.

In Adobe Experience Manager 6.1, lo strumento non funziona e può essere utilizzata solo l’interfaccia HTTP.

>[!NOTE]
>In tutte le versioni, il rilevatore pattern incluso può essere eseguito in modo indipendente.

## Interpretazione del rapporto di Cloud Readiness Analyzer (Analisi di preparazione al cloud) {#cra-report}

Quando lo strumento Cloud Readiness Analyzer (Analisi di preparazione al cloud) viene eseguito nell’istanza di AEM, il rapporto viene visualizzato sotto forma di risultati nella finestra dello strumento.

Il rapporto si presenta con questo formato:

* **Panoramica rapporto**: informazioni sul rapporto stesso, tra cui:
   * **Data del rapporto**: quando il contenuto del rapporto è stato generato e reso disponibile per la prima volta.
   * **Data di scadenza**: quando scade la cache del contenuto del rapporto.
   * **Tempo di generazione**: tempo impiegato dal processo di generazione del contenuto del rapporto.
   * **Conteggio risultati**: numero totale di risultati inclusi nel rapporto.
* **Panoramica del sistema**: informazioni sul sistema AEM su cui è stata eseguito lo strumento CRA.
* **Categorie dei risultati**: diverse sezioni che riguardano ciascuna uno o più risultati della stessa categoria. Ogni sezione include quanto segue: nome della categoria, sottotipi, conteggio e importanza dei risultati, riepilogo, collegamento alla documentazione della categoria e informazioni su singoli risultati.

A ciascun risultato viene assegnato un livello di importanza per dare un’indicazione approssimativa del grado di priorità dell’intervento richiesto.

La tabella seguente descrive i livelli di importanza:

| Importanza | Descrizione |
|--- |--- |
| INFO | Questo risultato è fornito a scopo informativo. |
| ADVISORY (AVVISO) | Questo risultato potrebbe costituire un problema di aggiornamento. Si raccomanda di effettuare ulteriori indagini. |
| MAJOR (IMPORTANTE) | È probabile che questo risultato costituisca un problema di aggiornamento da risolvere. |
| CRITICAL (CRITICO) | È molto probabile che questo risultato costituisca un problema di aggiornamento che deve essere risolto per evitare la perdita di funzioni o prestazioni. |


## Interpretazione del rapporto CSV di Cloud Readiness Analyzer (Analisi di preparazione al cloud) {#cra-csv-report}

Quando fai clic sull’opzione **CSV** nell’istanza di AEM, il rapporto di Cloud Readiness Analyzer (Analisi di preparazione al cloud) viene creato dalla cache del contenuto e restituito al browser in formato CSV. A seconda delle impostazioni del browser, è possibile che venga scaricato automaticamente come file con il nome predefinito `results.csv`.

Se la cache è scaduta, il rapporto verrà generato nuovamente prima che il file CSV venga creato e scaricato.

Il formato CSV del rapporto include informazioni generate dall’output del rilevatore pattern, ordinate e organizzate per tipo di categoria, sottotipo e livello di importanza. Il formato è adatto alla visualizzazione e la modifica in un’applicazione come Microsoft Excel. È stato progettato per fornire tutte le informazioni sui risultati in un formato ripetibile che può essere utile quando si confrontano i rapporti nel tempo per misurare l’avanzamento.

Le colonne del rapporto in formato CSV sono:

* **code** (codice): codice della categoria
* **type** (tipo): nome della categoria
* **subtype** (sottotipo): sottotipo della categoria
* **importance** (importanza): livello di importanza
* **identifier** (identificatore): identificatore principale del risultato
* **other** (altro): ulteriori informazioni sul risultato
* **message** (messaggio): messaggio fornito per il risultato
* **moreInfo** (ulteriori informazioni): collegamento che consente di accedere alla sezione sulla categoria in oggetto nella guida online
* **context** (contesto): una stringa JSON contenente dati sul risultato

Un valore “\N” in una colonna di un singolo risultato indica che non sono stati forniti dati.

## Interfaccia HTTP {#http-interface}

Lo strumento CRA fornisce un’interfaccia HTTP che può essere utilizzata come alternativa all’interfaccia utente in AEM. L’interfaccia supporta sia i comandi HEAD che GET. Può essere utilizzata per generare il rapporto CRA e restituirlo in uno dei tre formati seguenti: JSON, CSV e valori delimitati da tabulazioni (TSV).

I seguenti URL sono disponibili per l’accesso HTTP, dove `<host>` è il nome host (e, se necessario, la porta) del server in cui è installato lo strumento CRA:
* `http://<host>/apps/readiness-analyzer/analysis/result.json` per il formato JSON
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` per il formato CSV
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` per il formato TSV

### Esecuzione di una richiesta HTTP {#executing-http-request}

L’interfaccia HTTP può essere utilizzata in diversi modi.

Un modo semplice consiste nell’aprire una scheda del browser nello stesso browser in cui hai già effettuato l’accesso ad AEM come amministratore. Puoi inserire l’URL nella scheda del browser e visualizzare o scaricare i risultati dal browser.

Puoi inoltre utilizzare uno strumento della riga di comando, ad esempio `curl` o `wget`, nonché qualsiasi applicazione client HTTP. Se non utilizzi una scheda del browser con una sessione autenticata, devi fornire nel commento un nome utente e una password amministratore.

Il seguente è un esempio di come eseguire questa operazione:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`.

### Intestazioni e parametri {#http-headers-and-parameters}

Le seguenti intestazioni HTTP sono utilizzate da questa interfaccia:

* `Cache-Control: max-age=<seconds>`: specifica l’intervallo di aggiornamento della cache in secondi (consulta [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)).
* `Prefer: respond-async`: indica che il server deve rispondere in modo asincrono (consulta [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)).

I seguenti parametri di query HTTP sono disponibili per comodità nei casi in cui le intestazioni HTTP potrebbero non essere facilmente utilizzate:

* `max-age` (numero, facoltativo): specifica l’intervallo di aggiornamento della cache in secondi. Questo numero deve essere maggiore o uguale a 0. L’intervallo di aggiornamento predefinito è di 86.400 secondi. Pertanto, se non si specifica questo parametro o l’intestazione corrispondente, per distribuire le richieste verrà utilizzata una nuova cache per 24 ore, dopodiché sarà necessario generare di nuovo il rapporto. L’utilizzo di `max-age=0` forzerà la cancellazione della cache e avvierà la nuova generazione del rapporto. Subito dopo questa richiesta, l’intervallo di aggiornamento viene reimpostato sul precedente valore diverso da zero.
* `respond-async` (booleano, facoltativo): specifica che la risposta deve essere fornita in modo asincrono. Se si utilizza `respond-async=true` quando la cache non è aggiornata, il server restituirà una risposta `202 Accepted, processing cache` senza attendere che venga generato il rapporto e che la cache venga aggiornata. Se la cache è aggiornata, questo parametro non ha alcun effetto. Il valore predefinito è `false`, ciò significa che senza questo parametro o l’intestazione corrispondente, il server risponderà in modo sincrono, il che potrebbe richiedere molto tempo e un adeguamento del tempo di risposta massimo del client HTTP.

Se sono presenti sia un’intestazione HTTP che il parametro di query corrispondente, il parametro di query avrà la priorità.

Un modo semplice per avviare la generazione del rapporto tramite l’interfaccia HTTP è l’utilizzo del seguente comando:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

Una volta effettuata la richiesta, non c’è bisogno che il client rimanga attivo affinché venga generato il rapporto. La generazione del rapporto può essere avviata con un client utilizzando una richiesta HTTP GET e, una volta generato, può essere visualizzato nella cache di un altro client o nello strumento CSV nell’interfaccia utente di AEM.

### Risposte {#http-responses}

Sono possibili i seguenti valori di risposta:

* `200 OK`: la risposta contiene i risultati del rilevatore pattern generati quando la cache era aggiornata.
* `202 Accepted, processing cache`: nelle risposte asincrone, indica che la cache era obsoleta e che è in corso un aggiornamento.
* `400 Bad Request`: indica che la richiesta ha restituito un errore. Un messaggio nel formato Dettagli del problema (consulta [RFC 7807](https://tools.ietf.org/html/rfc7807)) fornisce ulteriori dettagli.
* `401 Unauthorized`: indica che la richiesta non era autorizzata.
* `500 Internal Server Error`: indica che si è verificato un errore interno del server. Un messaggio nel formato Dettagli del problema fornisce ulteriori dettagli.
* `503 Service Unavailable`: indica che il server è occupato con un’altra risposta e non può soddisfare questa richiesta in modo tempestivo. È probabile che ciò si verifichi solo quando vengono effettuate richieste sincrone. Un messaggio nel formato Dettagli del problema fornisce ulteriori dettagli.

## Informazioni amministratore

### Regolazione della durata della cache {#cache-adjustment}

La durata predefinita della cache dello strumento CRA è di 24 ore. Data la presenza, sia nell’istanza AEM che nell’interfaccia HTTP, dell’opzione per aggiornare un rapporto e rigenerare la cache, questo valore predefinito è probabilmente adatto alla maggior parte degli usi del CRA. Se la generazione del rapporto richiede tempi particolarmente lunghi per la tua istanza di AEM, puoi regolare la durata della cache al fine di ridurre al minimo la rigenerazione del rapporto.

Il valore della durata della cache viene memorizzato come la proprietà `maxCacheAge` nel seguente nodo di archivio:
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

Il valore di questa proprietà corrisponde alla durata della cache, in secondi. Un amministratore può regolare la durata della cache utilizzando CRX/DE Lite.

### Installazione su AEM 6.1 {#installing-on-aem61}

CRA utilizza un account utente del servizio di sistema denominato `repository-reader-service` per eseguire il Rilevatore pattern. Questo account è disponibile su AEM 6.2 e versioni successive. In AEM 6.1, questo account deve essere creato *prima* dell&#39;installazione di CRA, eseguendo le operazioni seguenti:

1. Seguite le istruzioni in [Creazione di un nuovo utente](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user) di servizi per creare un utente. Impostate UserID su `repository-reader-service` e lasciate vuoto il Percorso intermedio, quindi fate clic sul segno di spunta verde.

2. Seguite le istruzioni riportate nella sezione [Gestione di utenti e gruppi](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security.html#managing-users-and-groups), in particolare le istruzioni per l’aggiunta di utenti a un gruppo per aggiungere l’ `repository-reader-service` utente al `administrators` gruppo.

3. Installate il pacchetto CRA tramite Package Manager nell’istanza AEM di origine. (In questo modo verrà aggiunta la necessaria modifica alla configurazione ServiceUserMapper per l’utente del servizio `repository-reader-service` di sistema.)
