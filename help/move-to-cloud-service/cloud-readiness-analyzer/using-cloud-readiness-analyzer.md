---
title: Utilizzo di Cloud Readiness Analyzer (Analisi di preparazione al cloud)
description: Utilizzo di Cloud Readiness Analyzer (Analisi di preparazione al cloud)
translation-type: tm+mt
source-git-commit: ba2105d389617fe0c7e26642799b3a7dd3adb8a1
workflow-type: tm+mt
source-wordcount: '2091'
ht-degree: 77%

---


# Utilizzo di Cloud Readiness Analyzer (Analisi di preparazione al cloud){#using-cloud-readiness-analyzer}

## Considerazioni importanti sull’utilizzo di Cloud Readiness Analyzer (Analisi di preparazione al cloud) {#imp-considerations}

La sezione seguente per contiene considerazioni importanti sull’esecuzione di Cloud Readiness Analyzer (CRA; Analisi di preparazione al cloud):

* Il rapporto CRA viene creato utilizzando l’output del [rilevatore pattern](https://docs.adobe.com/content/help/it-IT/experience-manager-65/deploying/upgrading/pattern-detector.html) di Adobe Experience Manager (AEM). La versione del rilevatore pattern utilizzata da CRA è inclusa nel pacchetto di installazione CRA.

* CRA può essere eseguito solo dall’utente **amministratore** o da un utente del gruppo **amministratori**.

* CRA è supportato nelle istanze AEM con versione 6.1 e successive.

   >[!NOTE]
   > Per l’installazione di CRA in AEM 6.1, controlla i requisiti speciali in [Installazione su AEM 6.1](#installing-on-aem61).

* CRA può essere eseguito in qualsiasi ambiente, ma è preferibile eseguirlo in un ambiente *stage*.

   >[!NOTE]
   >Per evitare un impatto sulle istanze aziendali fondamentali, si consiglia di eseguire CRA in un ambiente di *authoring* il più simile possibile all’ambiente di *produzione* nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito su un clone dell’ambiente di *authoring* di produzione.

* La generazione del contenuto del rapporto CRA può richiedere tempi lunghi, da alcuni minuti ad alcune ore. Il tempo richiesto dipende in larga misura dalle dimensioni e dalla natura del contenuto dell’archivio AEM, dalla versione di AEM e da altri fattori.

* A causa del tempo significativo che potrebbe essere necessario per generare il contenuto del rapporto, il processo avviene in background e viene mantenuto nella cache. La visualizzazione e il download del rapporto dovrebbero essere relativamente veloci poiché viene utilizzata la cache del contenuto fino alla scadenza o all’aggiornamento esplicito del rapporto. Durante la generazione del contenuto del rapporto puoi chiudere la scheda del browser e tornare in un secondo momento per visualizzare il rapporto una volta che il relativo contenuto è disponibile nella cache.

## Disponibilità {#availability}

Cloud Readiness Analyzer (Analisi di preparazione al cloud) può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM).

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

### Adobe Experience Manager 6.2 e 6.1 {#aem-specific-versions}

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

* `Cache-Control: max-age=<seconds>`: Specifica la durata della freschezza della cache, in secondi. (consulta [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)).
* `Prefer: respond-async`: Specifica che il server deve rispondere in modo asincrono. (consulta [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)).
* `Prefer: return=minimal`: Specifica che il server deve restituire una risposta minima. (consulta [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)).

I seguenti parametri di query HTTP sono disponibili per comodità nei casi in cui le intestazioni HTTP potrebbero non essere facilmente utilizzate:

* `max-age` (numero, facoltativo): Specifica la durata della freschezza della cache, in secondi. Questo numero deve essere maggiore o uguale a 0. La durata predefinita della freschezza è di 86400 secondi. Senza questo parametro o l&#39;intestazione corrispondente verrà utilizzata una nuova cache per distribuire le richieste per 24 ore, al momento in cui la cache deve essere rigenerata. Utilizzando `max-age=0` verrà svuotata la cache e verrà avviata una rigenerazione del rapporto, utilizzando il precedente ciclo di vita di freschezza diverso da zero per la cache appena generata.
* `respond-async` (booleano, facoltativo): Specifica che la risposta deve essere fornita in modo asincrono. Using `respond-async=true` when the cache is stale will cause the server to return a response of `202 Accepted` without waiting for the cache to be refreshed and for the report to be generated. Se la cache è aggiornata, questo parametro non ha alcun effetto. The default value is `false`. Without this parameter or the corresponding header the server will respond synchronously, which may require a significant amount of time and require an adjustment to the maximum response time for the HTTP client.
* `may-refresh-cache` (booleano, facoltativo): Specifica che il server potrebbe aggiornare la cache in risposta a una richiesta se la cache corrente è vuota, obsoleta o presto non disponibile. Se `may-refresh-cache=true`o se non è specificato, il server potrebbe avviare un&#39;attività in background che richiamerà il Rilevatore pattern e aggiornerà la cache. Se `may-refresh-cache=false` il server non avvia alcuna attività di aggiornamento che altrimenti sarebbe stata eseguita se la cache fosse vuota o obsoleta, nel qual caso il rapporto sarà vuoto. Qualsiasi attività di aggiornamento già in corso di elaborazione non verrà interessata da questo parametro.
* `return-minimal` (booleano, facoltativo): Specifica che la risposta del server deve includere solo lo stato contenente l&#39;indicazione di avanzamento e lo stato della cache nel formato JSON. Se `return-minimal=true`necessario, il corpo della risposta sarà limitato all&#39;oggetto status. Se `return-minimal=false`o se non è specificato, verrà fornita una risposta completa.
* `log-findings` (booleano, facoltativo): Specifica che il server deve registrare il contenuto della cache quando viene creata o aggiornata per la prima volta. Ogni ricerca dalla cache verrà registrata come stringa JSON. La registrazione si verifica solo se `log-findings=true` e la richiesta genera una nuova cache.

Se sono presenti sia un’intestazione HTTP che il parametro di query corrispondente, il parametro di query avrà la priorità.

Un modo semplice per avviare la generazione del rapporto tramite l’interfaccia HTTP è l’utilizzo del seguente comando:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

Una volta effettuata la richiesta, non c’è bisogno che il client rimanga attivo affinché venga generato il rapporto. La generazione di report può essere avviata con un client utilizzando una richiesta di GET HTTP e, una volta generato, visualizzato dalla cache con un altro client o con lo strumento CRA nell&#39;interfaccia utente AEM.

### Risposte {#http-responses}

Sono possibili i seguenti valori di risposta:

* `200 OK`: Indica che la risposta contiene i risultati del rilevamento dei pattern generati nel corso della durata di freschezza della cache.
* `202 Accepted`: Utilizzato per indicare che la cache non è aggiornata. Quando `respond-async=true` e `may-refresh-cache=true` questa risposta indica che è in corso un&#39;attività di aggiornamento. Quando `may-refresh-cache=false` questa risposta indica semplicemente che la cache non è aggiornata.
* `400 Bad Request`: indica che la richiesta ha restituito un errore. A message in Problem Details format (see [RFC 7807](https://tools.ietf.org/html/rfc7807)) provides more details.
* `401 Unauthorized`: Indica che la richiesta non è stata autorizzata.
* `500 Internal Server Error`: indica che si è verificato un errore interno del server. Un messaggio nel formato Dettagli del problema fornisce ulteriori dettagli.
* `503 Service Unavailable`: indica che il server è occupato con un’altra risposta e non può soddisfare questa richiesta in modo tempestivo. È probabile che ciò si verifichi solo quando vengono effettuate richieste sincrone. Un messaggio nel formato Dettagli del problema fornisce ulteriori dettagli.

## Informazioni per l’amministratore

### Regolazione della durata della cache {#cache-adjustment}

La durata predefinita della cache dello strumento CRA è di 24 ore. Data la presenza, sia nell’istanza AEM che nell’interfaccia HTTP, dell’opzione per aggiornare un rapporto e rigenerare la cache, questo valore predefinito è probabilmente adatto alla maggior parte degli usi del CRA. Se la generazione del rapporto richiede tempi particolarmente lunghi per la tua istanza di AEM, puoi regolare la durata della cache al fine di ridurre al minimo la rigenerazione del rapporto.

Il valore della durata della cache viene memorizzato come la proprietà `maxCacheAge` nel seguente nodo di archivio:
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

Il valore di questa proprietà corrisponde alla durata della cache, in secondi. Un amministratore può regolare la durata della cache utilizzando CRX/DE Lite.

### Installazione in AEM 6.1 {#installing-on-aem61}

Per eseguire il rilevatore pattern, CRA utilizza un account utente di servizio del sistema denominato `repository-reader-service`. Questo account è disponibile in AEM 6.2 e versioni successive. In AEM 6.1, l’account deve essere creato *prima* dell’installazione di CRA, eseguendo le operazioni seguenti:

1. Per creare un utente segui le istruzioni in [Creazione di un nuovo utente di servizio](https://docs.adobe.com/content/help/it-IT/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user). Imposta UserID su `repository-reader-service` e lascia vuoto il Percorso intermedio, quindi fai clic sul segno di spunta verde.

2. Segui le istruzioni riportate nella sezione [Gestione di utenti e gruppi](https://docs.adobe.com/content/help/it-IT/experience-manager-65/administering/security/security.html#managing-users-and-groups), in particolare Aggiunta di utenti a un gruppo, per aggiungere l’utente `repository-reader-service` al gruppo `administrators`.

3. Installa il pacchetto CRA tramite Gestione pacchetti nell’istanza AEM di origine. Questa azione aggiunge la necessaria modifica alla configurazione ServiceUserMapper per l’utente di servizio del sistema `repository-reader-service`.)
