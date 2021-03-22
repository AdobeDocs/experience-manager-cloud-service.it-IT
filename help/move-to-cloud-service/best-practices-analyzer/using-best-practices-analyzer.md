---
title: Utilizzo di Best Practices Analyzer
description: Utilizzo di Best Practices Analyzer
translation-type: tm+mt
source-git-commit: 3d1aa714bacc74f77672ce2d7265da5239a6c6ff
workflow-type: tm+mt
source-wordcount: '2512'
ht-degree: 43%

---


# Utilizzo di Best Practices Analyzer {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="Utilizzo di Best Practices Analyzer"
>abstract="Esamina la documentazione relativa all’utilizzo di Best Practices Analyzer (precedentemente Cloud Readiness Analyzer) e il rapporto generato. Il rapporto di Best Practices Analyzer (Analisi di best practice) viene utilizzato per acquisire una comprensione di alto livello della preparazione generale all’aggiornamento."
>additional-url=""

## Considerazioni importanti sull&#39;utilizzo di Best Practices Analyzer {#imp-considerations}

Leggi la sezione seguente per comprendere le considerazioni importanti sull’esecuzione di Best Practices Analyzer (BPA):

* Il rapporto BPA viene creato utilizzando l&#39;output del rilevatore pattern [Adobe Experience Manager (AEM)](https://docs.adobe.com/content/help/it-IT/experience-manager-65/deploying/upgrading/pattern-detector.html). La versione del rilevatore pattern utilizzata da BPA è inclusa nel pacchetto di installazione BPA.

* Il BPA può essere eseguito solo dall&#39;utente **admin** o da un utente nel gruppo **administrators** .

* BPA è supportato nelle istanze AEM con versione 6.1 e successive.

   >[!NOTE]
Per i requisiti speciali per l’installazione di BPA in AEM 6.1, consulta  [Installazione in AEM 6.1](#installing-on-aem61) .

* BPA può essere eseguito in qualsiasi ambiente, ma è preferibile eseguirlo in un ambiente *Stage*.

   >[!NOTE]
Per evitare un impatto sulle istanze business critical, si consiglia di eseguire BPA in un ambiente  ** Authoring il più simile possibile all’ambiente di  ** produzione nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito su un clone dell’ambiente di *authoring* di produzione.

* La generazione dei contenuti dei rapporti BPA può richiedere molto tempo, da diversi minuti a poche ore. Il tempo richiesto dipende in larga misura dalle dimensioni e dalla natura del contenuto dell’archivio AEM, dalla versione di AEM e da altri fattori.

* A causa del tempo significativo che potrebbe essere necessario per generare il contenuto del rapporto, il processo avviene in background e viene mantenuto nella cache. La visualizzazione e il download del rapporto dovrebbero essere relativamente veloci poiché viene utilizzata la cache del contenuto fino alla scadenza o all’aggiornamento esplicito del rapporto. Durante la generazione del contenuto del rapporto puoi chiudere la scheda del browser e tornare in un secondo momento per visualizzare il rapporto una volta che il relativo contenuto è disponibile nella cache.

## Disponibilità {#availability}

[!CONTEXTUALHELP]
id="aemcloud_bpa_download"
title="Scarica Best Practices Analyzer"
abstract="È possibile scaricare Best Practices Analyzer come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM)."

È possibile scaricare Best Practices Analyzer come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM).

>[!NOTE]
Scarica Best Practices Analyzer dal portale  [di ](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) distribuzione software.

## Visualizzazione del rapporto di Best Practices Analyzer {#viewing-report}

### Adobe Experience Manager 6.3.0 e versioni successive {#aem-later-versions}

Leggi questa sezione per scoprire come visualizzare il rapporto di Best Practices Analyzer (Analisi di best practice):

1. Seleziona Adobe Experience Manager e passa a Strumenti -> **Operazioni** -> **Best Practices Analyzer**.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic1.png)

1. Fai clic su **Genera report** per eseguire Best Practices Analyzer.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic2.png)

1. Durante la generazione del rapporto da parte del BPA, puoi vedere lo stato di avanzamento dello strumento sullo schermo. Mostra il numero di elementi analizzati e mostra anche il numero di risultati rilevati.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic3.png)


1. Una volta generato il rapporto BPA, questo visualizza un riepilogo e il numero dei risultati in un formato tabulare organizzato in base al tipo di risultato e al livello di importanza. Per ottenere ulteriori dettagli su un particolare risultato, puoi fare clic sul numero corrispondente al tipo di risultato nella tabella.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic4.png)

   L’azione precedente scorre automaticamente fino alla posizione del risultato nel rapporto.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic5.png)

1. Puoi scaricare il rapporto in formato CSV facendo clic su **Esporta in CSV**, come illustrato nella figura riportata di seguito.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
È possibile forzare la cancellazione della cache del BPA e la rigenerazione del rapporto facendo clic su  **Aggiorna rapporto**.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
Durante la rigenerazione del rapporto, mostra l’avanzamento in termini di percentuale completata come mostrato nell’immagine seguente.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic8.png)


#### Utilizzo dei filtri nel rapporto di Best Practices Analyzer {#bpa-filters}

Per filtrare i risultati relativi a [ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), procedi come segue:

1. Fai clic sull’icona della barra a sinistra sul lato sinistro della pagina. Verrà visualizzato il **filtro ACS Commons**. Fai clic sul **filtro ACS Commons** per visualizzare la casella di controllo interattiva come mostrato nell&#39;immagine seguente.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
L’icona della barra a sinistra viene visualizzata solo se il BPA rileva l’utilizzo di ACS Commons.

1. Deseleziona la casella per filtrare tutti i risultati relativi a ACS Commons. Dovresti visualizzare un **Conteggio risultati filtrati** nel rapporto, come mostrato nell&#39;immagine seguente. Il filtro viene applicato anche al rapporto quando viene esportato in formato CSV.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
I risultati di ACS Commons non devono essere ignorati. Per determinare la compatibilità con AEM come Cloud Service, fai riferimento alla [documentazione](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility) .


### Adobe Experience Manager 6.2 e 6.1 {#aem-specific-versions}

In Adobe Experience Manager 6.2, lo strumento Best Practices Analyzer (Analisi best practice) è limitato a un collegamento che consente di generare e scaricare il rapporto CSV.

In Adobe Experience Manager 6.1, lo strumento non funziona e può essere utilizzata solo l’interfaccia HTTP.

>[!NOTE]
In tutte le versioni, il rilevatore pattern incluso può essere eseguito in modo indipendente.

## Interpretazione del rapporto di Best Practices Analyzer {#cra-report}

[!CONTEXTUALHELP]
id="aemcloud_bpa_interpreting"
title="Interpretazione del rapporto di Best Practices Analyzer"
abstract="Sono disponibili due opzioni per visualizzare gli output dei rapporti BPA: Interfaccia utente e CSV. Quando lo strumento Best Practices Analyzer viene eseguito nell&#39;istanza AEM, il rapporto dell&#39;interfaccia utente viene visualizzato come risultato nella finestra dello strumento. Il formato CSV del rapporto include informazioni generate dall’output del rilevatore pattern, ordinate e organizzate per tipo di categoria, sottotipo e livello di importanza."
additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=en" text="Categorie di rapporti di Best Practices Analyzer"

Quando lo strumento Best Practices Analyzer viene eseguito nell&#39;istanza AEM, il rapporto viene visualizzato come risultato nella finestra dello strumento.

Il rapporto si presenta con questo formato:

* **Panoramica rapporto**: informazioni sul rapporto stesso, tra cui:
   * **Data del rapporto**: quando il contenuto del rapporto è stato generato e reso disponibile per la prima volta.
   * **Data di scadenza**: quando scade la cache del contenuto del rapporto.
   * **Tempo di generazione**: tempo impiegato dal processo di generazione del contenuto del rapporto.
   * **Conteggio risultati**: numero totale di risultati inclusi nel rapporto.
* **Panoramica** del sistema: Informazioni sul sistema AEM su cui è stato eseguito il BPA.
* **Categorie dei risultati**: diverse sezioni che riguardano ciascuna uno o più risultati della stessa categoria. Ogni sezione include quanto segue: nome della categoria, sottotipi, conteggio e importanza dei risultati, riepilogo, collegamento alla documentazione della categoria e informazioni su singoli risultati.

A ciascun risultato viene assegnato un livello di importanza per dare un’indicazione approssimativa del grado di priorità dell’intervento richiesto.

>[!NOTE]
Per ulteriori informazioni su ciascuna categoria di ricerca, consulta  [Categorie rilevatore pattern](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html).

La tabella seguente descrive i livelli di importanza:

| Importanza | Descrizione |
|--- |--- |
| INFO | Questo risultato è fornito a scopo informativo. |
| ADVISORY (AVVISO) | Questo risultato potrebbe costituire un problema di aggiornamento. Si raccomanda di effettuare ulteriori indagini. |
| MAJOR (IMPORTANTE) | È probabile che questo risultato costituisca un problema di aggiornamento da risolvere. |
| CRITICAL (CRITICO) | È molto probabile che questo risultato costituisca un problema di aggiornamento che deve essere risolto per evitare la perdita di funzioni o prestazioni. |


## Interpretazione del rapporto CSV di Best Practices Analyzer {#cra-csv-report}

Quando fai clic sull’opzione **CSV** dall’istanza AEM, il formato CSV del rapporto Best Practices Analyzer (Analisi best practice) viene creato dalla cache del contenuto e restituito al browser in uso. A seconda delle impostazioni del browser, è possibile che venga scaricato automaticamente come file con il nome predefinito `results.csv`.

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

Il BPA fornisce un’interfaccia HTTP che può essere utilizzata come alternativa all’interfaccia utente in AEM. L’interfaccia supporta sia i comandi HEAD che GET. Può essere utilizzato per generare il rapporto BPA e restituirlo in uno dei tre formati seguenti: Valori JSON, CSV e separati da tabulazioni (TSV).

I seguenti URL sono disponibili per l’accesso HTTP, dove `<host>` è il nome host e, se necessario, la porta del server in cui è installato il BPA:
* `http://<host>/apps/best-practices-analyzer/analysis/report.json` per il formato JSON
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` per il formato CSV
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` per il formato TSV

### Esecuzione di una richiesta HTTP {#executing-http-request}

L’interfaccia HTTP può essere utilizzata in diversi modi.

Un modo semplice consiste nell’aprire una scheda del browser nello stesso browser in cui hai già effettuato l’accesso ad AEM come amministratore. Puoi inserire l’URL nella scheda del browser e visualizzare o scaricare i risultati dal browser.

Puoi inoltre utilizzare uno strumento della riga di comando, ad esempio `curl` o `wget`, nonché qualsiasi applicazione client HTTP. Se non utilizzi una scheda del browser con una sessione autenticata, devi fornire nel commento un nome utente e una password amministratore.

Il seguente è un esempio di come eseguire questa operazione:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`.

### Intestazioni e parametri {#http-headers-and-parameters}

Le seguenti intestazioni HTTP sono utilizzate da questa interfaccia:

* `Cache-Control: max-age=<seconds>`: Specifica l’intervallo di aggiornamento della cache in secondi. (consulta [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)).
* `Prefer: respond-async`: Specifica che il server deve rispondere in modo asincrono. (consulta [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)).
* `Prefer: return=minimal`: Specifica che il server deve restituire una risposta minima. (consulta [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)).

I seguenti parametri di query HTTP sono disponibili per comodità nei casi in cui le intestazioni HTTP potrebbero non essere facilmente utilizzate:

* `max-age` (numero, facoltativo): Specifica l’intervallo di aggiornamento della cache in secondi. Questo numero deve essere maggiore o uguale a 0. L’intervallo di aggiornamento predefinito è di 86400 secondi. Senza questo parametro o l’intestazione corrispondente verrà utilizzata una nuova cache per servire le richieste per 24 ore, a cui deve essere rigenerata la cache. L’utilizzo di `max-age=0` forza la cancellazione della cache e avvia la rigenerazione del rapporto, utilizzando l’intervallo di aggiornamento precedente diverso da zero per la cache appena generata.
* `respond-async` (booleano, facoltativo): Specifica che la risposta deve essere fornita in modo asincrono. Se si utilizza `respond-async=true` quando la cache non è aggiornata, il server restituirà una risposta di `202 Accepted` senza attendere che la cache venga aggiornata e che il rapporto venga generato. Se la cache è aggiornata, questo parametro non ha alcun effetto. Il valore predefinito è `false`. Senza questo parametro o l&#39;intestazione corrispondente il server risponderà in modo sincrono, il che potrebbe richiedere molto tempo e una regolazione del tempo di risposta massimo per il client HTTP.
* `may-refresh-cache` (booleano, facoltativo): Specifica che il server può aggiornare la cache in risposta a una richiesta se la cache corrente è vuota, obsoleta o presto obsoleta. Se `may-refresh-cache=true` o se non è specificato, il server può avviare un&#39;attività in background che richiamerà il rilevatore pattern e aggiornerà la cache. Se `may-refresh-cache=false` il server non avvia alcuna attività di aggiornamento che altrimenti sarebbe stata eseguita se la cache è vuota o obsoleta, nel qual caso il rapporto sarà vuoto. Questo parametro non influisce sulle attività di aggiornamento già in corso.
* `return-minimal` (booleano, facoltativo): Specifica che la risposta dal server deve includere solo lo stato contenente l&#39;indicazione di avanzamento e lo stato della cache nel formato JSON. Se `return-minimal=true`, il corpo della risposta sarà limitato all&#39;oggetto status. Se `return-minimal=false` o se non è specificato, verrà fornita una risposta completa.
* `log-findings` (booleano, facoltativo): Specifica che il server deve registrare il contenuto della cache quando viene generato o aggiornato per la prima volta. Ogni risultato della cache verrà registrato come stringa JSON. Questa registrazione si verifica solo se `log-findings=true` e la richiesta genera una nuova cache.

Se sono presenti sia un’intestazione HTTP che il parametro di query corrispondente, il parametro di query avrà la priorità.

Un modo semplice per avviare la generazione del rapporto tramite l’interfaccia HTTP è l’utilizzo del seguente comando:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`.

Una volta effettuata la richiesta, non c’è bisogno che il client rimanga attivo affinché venga generato il rapporto. La generazione del rapporto può essere avviata con un client utilizzando una richiesta HTTP GET e, una volta generato, può essere visualizzata dalla cache con un altro client o con lo strumento BPA nell’interfaccia utente AEM.

### Risposte {#http-responses}

Sono possibili i seguenti valori di risposta:

* `200 OK`: Indica che la risposta contiene i risultati del rilevatore pattern generati nell’intervallo di aggiornamento della cache.
* `202 Accepted`: Utilizzato per indicare che la cache non è aggiornata. Quando `respond-async=true` e `may-refresh-cache=true` questa risposta indica che è in corso un’attività di aggiornamento. Quando `may-refresh-cache=false` questa risposta indica semplicemente che la cache è obsoleta.
* `400 Bad Request`: indica che la richiesta ha restituito un errore. Un messaggio nel formato Dettagli del problema (consulta [RFC 7807](https://tools.ietf.org/html/rfc7807)) fornisce ulteriori dettagli.
* `401 Unauthorized`: Indica che la richiesta non è stata autorizzata.
* `500 Internal Server Error`: indica che si è verificato un errore interno del server. Un messaggio nel formato Dettagli del problema fornisce ulteriori dettagli.
* `503 Service Unavailable`: indica che il server è occupato con un’altra risposta e non può soddisfare questa richiesta in modo tempestivo. È probabile che ciò si verifichi solo quando vengono effettuate richieste sincrone. Un messaggio nel formato Dettagli del problema fornisce ulteriori dettagli.

## Informazioni per l’amministratore

### Regolazione della durata della cache {#cache-adjustment}

La durata predefinita della cache BPA è di 24 ore. Con l’opzione per aggiornare un rapporto e rigenerare la cache, sia nell’istanza AEM che nell’interfaccia HTTP, è probabile che questo valore predefinito sia appropriato per la maggior parte degli usi del BPA. Se la generazione del rapporto richiede tempi particolarmente lunghi per la tua istanza di AEM, puoi regolare la durata della cache al fine di ridurre al minimo la rigenerazione del rapporto.

Il valore della durata della cache viene memorizzato come la proprietà `maxCacheAge` nel seguente nodo di archivio:
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

Il valore di questa proprietà corrisponde alla durata della cache, in secondi. Un amministratore può regolare la durata della cache utilizzando CRX/DE Lite.

### Installazione in AEM 6.1 {#installing-on-aem61}

Per eseguire il rilevatore pattern, BPA utilizza un account utente di servizio di sistema denominato `repository-reader-service` . Questo account è disponibile in AEM 6.2 e versioni successive. Al AEM 6.1, questo account deve essere creato *prima dell&#39;installazione di* BPA, eseguendo le seguenti operazioni:

1. Per creare un utente segui le istruzioni in [Creazione di un nuovo utente di servizio](https://docs.adobe.com/content/help/it-IT/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user). Imposta UserID su `repository-reader-service` e lascia vuoto il Percorso intermedio, quindi fai clic sul segno di spunta verde.

2. Segui le istruzioni riportate nella sezione [Gestione di utenti e gruppi](https://docs.adobe.com/content/help/it-IT/experience-manager-65/administering/security/security.html#managing-users-and-groups), in particolare Aggiunta di utenti a un gruppo, per aggiungere l’utente `repository-reader-service` al gruppo `administrators`.

3. Installa il pacchetto BPA tramite Gestione pacchetti nell&#39;istanza di AEM sorgente. Questa azione aggiunge la necessaria modifica alla configurazione ServiceUserMapper per l’utente di servizio del sistema `repository-reader-service`.)
