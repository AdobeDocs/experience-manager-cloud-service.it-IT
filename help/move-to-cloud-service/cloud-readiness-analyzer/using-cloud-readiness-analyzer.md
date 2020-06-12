---
title: Utilizzo di Cloud Ready Analyzer
description: Utilizzo di Cloud Ready Analyzer
translation-type: tm+mt
source-git-commit: 1ca9b2091befbafad0878d83fc7963c779146b2a
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 0%

---


# Utilizzo di Cloud Ready Analyzer {#using-cloud-readiness-analyzer}

## Considerazioni importanti per l&#39;utilizzo di Cloud Readiness Analyzer {#imp-considerations}

Seguite la sezione seguente per comprendere le considerazioni importanti durante l&#39;esecuzione di Cloud Readiness Analyzer (CRA):

* Il rapporto CRA viene creato utilizzando l&#39;output del [Rilevatore](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html)di pattern di Adobe Experience Manager (AEM). La versione del rilevatore di pattern utilizzato da CRA è inclusa nel pacchetto di installazione CRA.

* Il CRA può essere eseguito solo dall&#39;utente *amministratore* o da un utente del gruppo **Amministratori** .

* CRA è supportata nelle istanze AEM con versione 6.1 e successive.

* CRA può essere eseguito su qualsiasi ambiente, ma è preferibile eseguirlo in un ambiente *Stage* .

   >[!NOTE]
   >Per evitare un impatto sulle istanze business critical, si consiglia di eseguire CRA in un ambiente di staging *Author* il più vicino possibile all&#39;ambiente di produzione nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito su un clone dell&#39;ambiente di produzione *Author* .

* La generazione di report CRA può richiedere molto tempo, da alcuni minuti a poche ore. Il tempo richiesto dipende in larga misura dalle dimensioni e dalla natura del contenuto dell’archivio AEM, dalla versione AEM e da altri fattori.

* A causa del tempo significativo necessario per generare il rapporto, i risultati vengono conservati in una cache e sono disponibili per la visualizzazione e il download successivi fino alla scadenza della cache o all&#39;aggiornamento esplicito del rapporto.

## Disponibilità {#availability}

Cloud Readiness Analyzer può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Package Manager nella tua istanza sorgente Adobe Experience Manager (AEM).

>[!NOTE]
>Scaricate Cloud Readiness Analyzer dal portale di distribuzione software *in sospeso*.

## Esecuzione di Cloud Readiness Analyzer {#running-tool}

Segui questa sezione per apprendere come eseguire Cloud Reader Analyzer:

1. Seleziona Adobe Experience Manager e passa agli strumenti -> **Operazioni** -> **Cloud Readiness Analyzer**.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Dopo aver fatto clic su **Cloud Readiness Analyzer**, lo strumento avvia la generazione del rapporto e, dopo pochi minuti, il rapporto di riepilogo è disponibile nell’istanza di AEM.

   >[!NOTE]
   >Sarà necessario scorrere la pagina verso il basso per visualizzare il rapporto completo.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### AEM 6.3 e versioni successive {#aem-older-version}

Per AEM 6.3 e versioni successive, il modo principale per eseguire Cloud Reader Analyzer è:

1. Seleziona l’istanza Adobe Experience Manager e passa a Strumenti > **Operazioni** > **Cloud Readiness Analyzer**.

   >[!NOTE]
   >Il CRA avvia un processo in background per generare il rapporto non appena lo strumento viene aperto. Indica che la generazione del report è in corso fino a quando il report non è pronto. Puoi chiudere la scheda del browser e tornare in un secondo momento per visualizzare il rapporto al termine.

1. Una volta generato e visualizzato il rapporto CRA, potete scegliere di scaricare il rapporto in valori CSV (Comma Separated Value). Fate clic su **CSV** per scaricare il rapporto di riepilogo completo in formato CSV, come mostrato nella figura seguente.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)

   >[!NOTE]
   >È possibile forzare l&#39;applicazione CRA a cancellare la cache e a rigenerare il rapporto facendo clic sul pulsante **Aggiorna rapporto** nell&#39;angolo superiore sinistro.

### AEM 6.2 e 6.1 {#aem-specific-versions}

In AEM 6.2 l’interfaccia utente di Cloud Readiness Analyzer è limitata a un collegamento che genera e scarica il rapporto CSV. Per AEM 6.1, l’interfaccia utente non funziona e può essere utilizzata solo l’interfaccia HTTP.

In tutte le versioni, il Rilevatore di pattern incluso può essere eseguito in modo indipendente.

Per scaricare il rapporto CSV per Adobe Experience Manager (AEM) 6.1 e 6.2, effettuate le seguenti operazioni:

1. Passa alla consoleConfigurazione **Web di** Adobe Experience Manager utilizzando `https://serveraddress:serverport/system/console/configMgr`.

1. Selezionate la scheda **Stato** e cercate **Rilevamento** pattern dall&#39;elenco a discesa, come illustrato nella figura riportata di seguito.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. Potete scaricare il rapporto di riepilogo in una cartella zip o in un formato JSON.

## Report di riepilogo CRA {#cra-summary-report}

Quando si esegue Cloud Readiness Analyzer nell’interfaccia utente di AEM, il rapporto viene visualizzato come risultati nella finestra degli strumenti.

Il formato del rapporto è:

* *Panoramica* report: Informazioni sul rapporto stesso, inclusa la data in cui è stato generato.
* *Panoramica* del sistema: Informazioni sul sistema AEM su cui è stata eseguita la CRA.
* *Ricerca di categorie*: Più sezioni che ciascuna di esse affronta uno o più risultati della stessa categoria. Ogni sezione include quanto segue: Nome della categoria, sottotipi, conteggio e importanza, riepilogo, collegamento alla documentazione della categoria e informazioni di ricerca individuali.

A ciascun risultato viene assegnato un livello di importanza tale da indicare una priorità di azione.

Segui la tabella seguente per comprendere i livelli di importanza:

| Importanza | Descrizione |
|--- |--- |
| INFO | Questa conclusione è fornita a scopo informativo. |
| AVVISO | Questo risultato potrebbe essere un problema di aggiornamento. Si raccomanda di effettuare ulteriori indagini. |
| PRINCIPALE | Questo risultato potrebbe rappresentare un problema di aggiornamento da risolvere. |
| CRITICO | Questo risultato è molto probabile che sia un problema di aggiornamento che deve essere risolto per evitare la perdita di funzioni o prestazioni. |

## Report CSV CRA {#crs-csv-report}

Quando fate clic sull’opzione **CSV** dall’istanza di AEM, il formato CSV del rapporto Analisi prontezza cloud viene creato dalla cache dei risultati e restituito al browser. A seconda delle impostazioni del browser, il rapporto verrà scaricato automaticamente come file con un nome predefinito di `results.csv`. Se la cache è scaduta, il rapporto verrà rigenerato prima che il file CSV venga creato e scaricato.

Il formato CSV del rapporto include informazioni generate dall&#39;output Rilevatore pattern, ordinate e organizzate per tipo di categoria, sottotipo e livello di importanza. Il formato è adatto per la visualizzazione e la modifica in un&#39;applicazione come Microsoft Excel. È stato progettato per fornire tutte le informazioni di ricerca in un formato ripetibile che può essere utile quando si confrontano i report nel tempo per misurare l&#39;avanzamento.

Le colonne del rapporto sul formato CSV sono:

* **codice**: il codice categoria
* **type**: il nome della categoria
* **sottotipo**: il sottotipo della categoria
* **importanza**: il livello di importanza
* **identificatore**: identificatore principale della ricerca
* **altro**: ulteriori informazioni sulla ricerca
* **messaggio**: il messaggio fornito per la ricerca
* **moreInfo**: un collegamento che può essere utilizzato per accedere alla guida online sulla categoria
* **contesto**: una stringa JSON per la ricerca di dati

Il valore &quot;\N&quot; di una colonna per un singolo risultato indica che non sono stati forniti dati.

## Interfaccia HTTP {#http-interface}

CRA fornisce un&#39;interfaccia HTTP che può essere utilizzata come alternativa all&#39;interfaccia utente di AEM. L&#39;interfaccia supporta sia i comandi HEAD che GET. Può essere utilizzato per generare il rapporto CRA e restituirlo in uno dei tre formati seguenti: Valori JSON, CSV e separati da tabulazioni (TSV).

I seguenti URL sono disponibili per l’accesso HTTP, dove `<host>` è il nome host e la porta, se necessario, del server in cui è installato il CRA:
* `http://<host>/apps/readiness-analyzer/analysis/result.json` per il formato JSON
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` per il formato CSV
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` per formato TSV

### Esecuzione di una richiesta HTTP {#executing-http-request}

L&#39;interfaccia HTTP può essere utilizzata in diversi metodi.

Un modo semplice consiste nell’aprire una scheda del browser nello stesso browser in cui avete già effettuato l’accesso ad AEM come amministratore. Potete inserire l’URL nella scheda del browser e visualizzare o scaricare i risultati dal browser.

È inoltre possibile utilizzare uno strumento della riga di comando, ad esempio `curl` o `wget` , nonché qualsiasi applicazione client HTTP. Se non utilizzate una scheda del browser con una sessione autenticata, dovete fornire un nome utente e una password amministratore come parte del commento.

Esempio di come eseguire questa operazione:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`.

### Intestazioni e parametri {#http-headers-and-parameters}

Le seguenti intestazioni HTTP sono utilizzate da questa interfaccia:

* `Cache-Control: max-age=<seconds>`: Specificate la durata della freschezza della cache in secondi. (vedere [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: Indica che il server deve rispondere in modo asincrono. (vedere [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1).)

I seguenti parametri di query HTTP sono disponibili come comodità per i casi in cui le intestazioni HTTP potrebbero non essere facilmente utilizzate:

* `max-age` (numero, facoltativo): Specificate la durata della freschezza della cache in secondi. Questo numero deve essere maggiore o uguale a 0. La durata predefinita della freschezza è di 86400 secondi, il che significa che senza questo parametro o l&#39;intestazione corrispondente verrà utilizzata una nuova cache per distribuire le richieste per 24 ore prima che il rapporto venga rigenerato. L&#39;utilizzo `max-age=0` forzerà la cancellazione della cache e avvierà una rigenerazione del report. Subito dopo questa richiesta, la durata della freschezza verrà reimpostata sul precedente valore diverso da zero.
* `respond-async` (booleano, facoltativo): Specificate che la risposta deve essere fornita in modo asincrono. Se si utilizza `respond-async=true` la cache non aggiornata, il server restituirà una risposta `202 Accepted, processing cache` senza attendere che venga generato il rapporto e che la cache venga aggiornata. Se la cache è fresca, questo parametro non ha alcun effetto. Il valore predefinito è `false`, il che significa che senza questo parametro o l&#39;intestazione corrispondente, il server risponderà in modo sincrono, il che potrebbe richiedere molto tempo e richiedere un adeguamento al tempo di risposta massimo per il client HTTP.

Se sono presenti sia un&#39;intestazione HTTP che il parametro di query corrispondente, il parametro di query avrà la precedenza.

Un modo semplice per avviare la generazione del report tramite l&#39;interfaccia HTTP è tramite il seguente comando:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

Una volta effettuata la richiesta, il client non deve rimanere attivo per la generazione del rapporto. La generazione di rapporti può essere avviata con un client utilizzando una richiesta HTTP GET e, una volta generato il rapporto, può essere visualizzata dalla cache di un altro client o dallo strumento CSV nell&#39;interfaccia utente di AEM.

### Risposte (#http-responses)

Sono possibili i seguenti valori di risposta:

* `200 OK`: La risposta contiene i risultati del rilevamento dei pattern generati nel corso della durata di freschezza della cache.
* `202 Accepted, processing cache`: Sono state fornite risposte asincrone per indicare che la cache era obsoleta e che è in corso un aggiornamento.
* `400 Bad Request`: Indica che la richiesta ha restituito un errore. Un messaggio in formato Dettagli problema (vedere [RFC 7807](https://tools.ietf.org/html/rfc7807)) fornisce ulteriori dettagli.
* `401 Unauthorized`: La richiesta non era autorizzata.
* `500 Internal Server Error`: Indica che si è verificato un errore interno del server. Un messaggio in formato Dettagli problema fornisce ulteriori dettagli.
* `503 Service Unavailable`: Indica che il server è occupato con un&#39;altra risposta e non può soddisfare questa richiesta in modo tempestivo. Questo è simile a quando vengono effettuate richieste sincrone. Un messaggio in formato Dettagli problema fornisce ulteriori dettagli.

## Regolazione del ciclo di vita della cache {#cache-adjustment}

La durata predefinita della cache CRA è di 24 ore. Con l&#39;opzione per aggiornare un rapporto e rigenerare la cache, sia nell&#39;interfaccia utente che nell&#39;interfaccia HTTP, questo valore predefinito è probabilmente adatto per la maggior parte degli usi del CRA. Se il tempo di generazione del rapporto è particolarmente lungo per l’istanza di AEM, puoi regolare la durata della cache al fine di ridurre al minimo la rigenerazione del rapporto.

Il valore del ciclo di vita della cache viene memorizzato come `maxCacheAge` proprietà nel seguente nodo del repository:
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

Il valore di questa proprietà corrisponde alla durata della cache, in secondi. Un amministratore può regolare la durata della cache utilizzando l’interfaccia CRX/DE Lite su AEM.





