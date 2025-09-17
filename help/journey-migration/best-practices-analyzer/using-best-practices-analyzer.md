---
title: Utilizzo di Best Practices Analyzer
description: Scopri come utilizzare Best Practices Analyzer per comprendere lo stato di preparazione all’aggiornamento.
exl-id: e8498e17-f55a-4600-87d7-60584d947897
feature: Migration
role: Admin
source-git-commit: 951f7fb56d1d8a3285973fda945cbc21f310925f
workflow-type: tm+mt
source-wordcount: '2796'
ht-degree: 37%

---

# Utilizzo di Best Practices Analyzer {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="Utilizzo di Best Practices Analyzer"
>abstract="Consulta la documentazione relativa all’utilizzo di Best Practices Analyzer (precedentemente Cloud Readiness Analyzer) ed esamina il rapporto generato. Il rapporto di Best Practices Analyzer viene utilizzato per acquisire una comprensione di alto livello dello stato di preparazione generale all’aggiornamento."
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[Webinar] Strumenti che consentono di accelerare il percorso verso Adobe Experience Manager as a Cloud Service"

## Considerazioni importanti sull’utilizzo di Best Practices Analyzer {#imp-considerations}

La sezione seguente per contiene considerazioni importanti sull’esecuzione di Best Practices Analyzer (BPA):

* Il report BPA viene creato utilizzando l&#39;output del rilevatore pattern [di Adobe Experience Manager (AEM)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html). La versione del rilevatore pattern utilizzata da BPA è inclusa nel pacchetto di installazione di BPA.

* BPA può essere eseguito solo dall&#39;utente **admin** o da un utente del gruppo **amministratori**.

* BPA è supportato nelle istanze di AEM con versione 6.1 e successive.

  >[!NOTE]
  >Per i requisiti speciali per l&#39;installazione di BPA in AEM 6.1, vedere [Installazione in AEM 6.1](#installing-on-aem61).

* BPA può essere eseguito in qualsiasi ambiente, ma è preferibile eseguirlo in un ambiente *Stage*.

  >[!NOTE]
  >Per evitare un impatto sulle istanze business critical, è consigliabile eseguire BPA in un ambiente *Stage* il più simile possibile all&#39;ambiente *Produzione* nelle aree di personalizzazioni, configurazioni, contenuto e applicazioni utente. In alternativa, può essere eseguito su un clone dell’ambiente di *authoring* di produzione.

* La generazione del contenuto del rapporto BPA può richiedere molto tempo, da alcuni minuti ad alcune ore. Il tempo richiesto dipende in larga misura dalle dimensioni e dalla natura del contenuto dell’archivio AEM, dalla versione di AEM e da altri fattori.

* A causa del tempo significativo che potrebbe essere necessario per generare il contenuto del rapporto, il processo avviene in background e viene mantenuto nella cache. La visualizzazione e il download del rapporto dovrebbero essere relativamente veloci poiché viene utilizzata la cache del contenuto fino alla scadenza o all’aggiornamento esplicito del rapporto. Durante la generazione del contenuto del rapporto puoi chiudere la scheda del browser e tornare in un secondo momento per visualizzare il rapporto una volta che il relativo contenuto è disponibile nella cache.

## Disponibilità {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_download"
>title="Scaricare Best Practices Analyzer"
>abstract="Best Practices Analyzer può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite il gestore di pacchetti nella tua istanza di origine di Adobe Experience Manager (AEM)."

Best Practices Analyzer può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) nell&#39;istanza Adobe Experience Manager (AEM) di origine.

>[!NOTE]
>Scarica Best Practices Analyzer dal portale [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

## Connettività dell’ambiente Source {#source-environment-connectivity}

L’istanza AEM di origine potrebbe essere in esecuzione dietro un firewall e raggiungere solo alcuni host aggiunti a un Elenco consentiti. Per caricare automaticamente in Cloud Acceleration Manager il rapporto generato da BPA, i seguenti endpoint devono essere accessibili dall’istanza che esegue AEM:

* Servizio di archiviazione BLOB di Azure: `casstorageprod.blob.core.windows.net`


## Visualizzazione del rapporto di Best Practices Analyzer {#viewing-report}

### Adobe Experience Manager 6.3.0 e versioni successive {#aem-later-versions}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa_upload_setup"
>title="Caricare automaticamente il rapporto di Best Practices Analyzer in CAM"
>abstract="Specifica la chiave di caricamento BPA per caricare automaticamente il rapporto BPA generato in Cloud Acceleration Manager (CAM)."

Segui questa sezione per scoprire come visualizzare il rapporto Best Practices Analyzer:

1. Seleziona Adobe Experience Manager e passa a Strumenti > **Operazioni** > **Best Practices Analyzer**.

   ![Analisi delle best practice](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. Fai clic su **Genera report** per eseguire Best Practices Analyzer.

   ![Genera report](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

>[!NOTE]
> A partire dalla versione 2.1.54 di BPA, è stata introdotta una nuova funzione per ottenere il punteggio Lighthouse.


1. Dopo aver fatto clic su **Genera report**, verrà visualizzato un pop-up con la richiesta dell&#39;URL del sito pubblico AEM per il punteggio Lighthouse. L’utente deve immettere un URL valido nel campo fornito.

   ![immagine](/help/journey-migration/best-practices-analyzer/assets/bpa_popup_url.png)

   1. Se l’URL è valido, verrà visualizzato un messaggio di successo.

      ![immagine](/help/journey-migration/best-practices-analyzer/assets/valid_url.png)

   1. Se l’URL non è valido, viene visualizzato un messaggio di errore.

      ![immagine](/help/journey-migration/best-practices-analyzer/assets/invalid_url.png)

1. Fornisci la chiave di caricamento BPA per caricare automaticamente il report BPA generato in [Cloud Acceleration Manager (CAM)](/help/journey-migration/cloud-acceleration-manager/introduction/benefits-cam.md). Per ottenere la chiave di caricamento, passa a [Analisi delle best practice in CAM](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

   ![Imposta chiave caricamento BPA](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key.png)

>[!NOTE]
>È possibile saltare il caricamento automatico in CAM selezionando **Ignora caricamento automatico report in CAM**. Se scegli di saltare, dovrai scaricare manualmente il rapporto BPA come file con valori separati da virgole e quindi caricare il file in CAM. Si consiglia di utilizzare l’opzione carica chiave, in quanto semplifica l’operazione.

>[!IMPORTANT]
>Quando si carica manualmente in CAM, le dimensioni dei report sono limitate a circa 200 MB. Per i rapporti più grandi dovrai sfruttare il caricamento automatico.

1. Il pulsante **Genera** diventa attivo quando viene fornita una chiave valida. Fai clic su **Genera** per avviare la generazione del rapporto.

   ![Genera report](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key1.png)

1. Durante la generazione del rapporto da parte di BPA, è possibile visualizzare lo stato di avanzamento dello strumento sullo schermo. Visualizza lo stato di avanzamento in termini di percentuale di completamento. Mostra inoltre il numero di elementi analizzati e il numero di risultati trovati.

   ![Generazione del report](/help/journey-migration/best-practices-analyzer/assets/BPA_generate_upload.png)

>[!NOTE]
>La marca temporale della scadenza della chiave di caricamento BPA viene visualizzata nell’angolo in alto a destra. È necessario rinnovare la chiave di caricamento BPA quando è vicina alla scadenza. Per rinnovare la chiave, puoi fare clic su **Rinnova** per passare a CAM e rinnovare la chiave.

1. Una volta generato, il rapporto BPA visualizza un riepilogo e il numero dei risultati in formato tabulare organizzato in base al tipo di risultato e al livello di importanza. Per ottenere ulteriori dettagli su un particolare risultato, è possibile fare clic sul numero corrispondente al tipo di risultato nella tabella.

   ![Panoramica report](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. È possibile scaricare il report in formato CSV facendo clic su **Esporta in CSV**. È inoltre possibile visualizzare il report in CAM facendo clic su **Vai a CAM**. Verrà visualizzata la pagina [Analisi delle best practice](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis) in CAM.

È possibile forzare il BPA a cancellare la cache e rigenerare il report facendo clic su **Aggiorna report**.

![Aggiorna report](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. Se la cache scade, puoi visualizzare l&#39;ultimo rapporto generato in CAM facendo clic su **Visualizza l&#39;ultimo rapporto generato in CAM** oppure avviare una nuova generazione facendo clic su **Genera nuovo rapporto**.

![Nessun rapporto](/help/journey-migration/best-practices-analyzer/assets/BPA_regeneratereport.png)


#### Utilizzo dei filtri nel rapporto di Best Practices Analyzer {#bpa-filters}

Per filtrare i risultati relativi a [ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), effettua le seguenti operazioni:

1. Fai clic sull’icona della barra a sinistra nella pagina. Verrà visualizzato il **filtro ACS Commons**. Fai clic sul **filtro ACS Commons** per visualizzare la casella di controllo interattiva come illustrato nell&#39;immagine seguente.

   ![Filtro Commons ACS](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
   >L’icona della barra a sinistra viene visualizzata solo se BPA rileva l’utilizzo di ACS Commons.

1. Deseleziona la casella per escludere tutti i risultati relativi ad ACS Commons. Dovresti visualizzare un **Conteggio risultati filtrati** nel report, come illustrato nell&#39;immagine seguente. Il filtro viene applicato anche al rapporto quando viene esportato in formato CSV (Virgola-Separated-Value).

   ![Conteggio risultati filtrati](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
   >I risultati di ACS Commons non devono essere ignorati. Consulta la [documentazione](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility) per determinare la compatibilità con AEM as a Cloud Service.

<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## Interpretazione del rapporto di Best Practices Analyzer {#cra-report}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_interpreting"
>title="Interpretazione del rapporto di Best Practices Analyzer"
>abstract="Sono disponibili due opzioni per visualizzare gli output del rapporto BPA: interfaccia utente e CSV. Quando lo strumento Best Practices Analyzer viene eseguito nell’istanza di AEM, il rapporto per l’interfaccia utente viene visualizzato sotto forma di risultati nella finestra dello strumento. Il formato CSV del rapporto include informazioni generate dall’output del rilevatore di pattern, ordinate e organizzate per tipo di categoria, sottotipo e livello di importanza."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=it#analysis-report" text="Analisi del rapporto di Best Practices Analyzer"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=it" text="Categorie del rapporto di Best Practices Analyzer"

Quando lo strumento Best Practices Analyzer viene eseguito nell’istanza di AEM, il rapporto viene visualizzato come risultati nella finestra dello strumento.

Il rapporto si presenta con questo formato:

* **Panoramica rapporto**: informazioni sul rapporto stesso, tra cui:
   * **Data del rapporto**: quando il contenuto del rapporto è stato generato e reso disponibile per la prima volta.
   * **Data di scadenza**: quando scade la cache del contenuto del rapporto.
   * **Tempo di generazione**: tempo impiegato dal processo di generazione del contenuto del rapporto.
   * **Conteggio risultati**: numero totale di risultati inclusi nel rapporto.
* **Panoramica del sistema**: informazioni sul sistema AEM su cui è stato eseguito BPA.
* **Categorie dei risultati**: diverse sezioni che riguardano ciascuna uno o più risultati della stessa categoria. Ogni sezione include quanto segue: nome della categoria, sottotipi, conteggio e importanza dei risultati, riepilogo, collegamento alla documentazione della categoria e informazioni su singoli risultati.

A ciascun risultato viene assegnato un livello di importanza per dare un’indicazione approssimativa del grado di priorità dell’intervento richiesto.

>[!NOTE]
>Per ulteriori informazioni su ciascuna categoria di risultati, vedere [Categorie del rilevatore pattern](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=it).

La tabella seguente descrive i livelli di importanza:

| Importanza | Descrizione |
|--- |--- |
| INFO | Questo risultato è fornito a scopo informativo. |
| ADVISORY (AVVISO) | Questo risultato potrebbe costituire un problema di aggiornamento. Si raccomanda di effettuare ulteriori indagini. |
| MAJOR (IMPORTANTE) | È probabile che questo risultato costituisca un problema di aggiornamento da risolvere. |
| CRITICAL (CRITICO) | È molto probabile che questo risultato costituisca un problema di aggiornamento che deve essere risolto per evitare la perdita di funzioni o prestazioni. |

## Interpretazione del rapporto CSV di Best Practices Analyzer {#cra-csv-report}

Quando fai clic sull&#39;opzione **CSV** nell&#39;istanza di AEM, il rapporto Best Practices Analyzer in formato CSV viene creato dalla cache del contenuto e restituito al browser. A seconda delle impostazioni del browser, il report viene scaricato automaticamente come file con il nome predefinito `results.csv`.

Se la cache è scaduta, il rapporto viene rigenerato prima che il file CSV venga generato e scaricato.

Il formato CSV del rapporto include informazioni generate dall’output del rilevatore pattern, ordinate e organizzate per tipo di categoria, sottotipo e livello di importanza. Il formato è adatto alla visualizzazione e la modifica in un’applicazione come Microsoft Excel. Lo scopo è quello di fornire tutte le informazioni sui risultati in un formato ripetibile che può essere utile quando si confrontano i rapporti nel tempo per misurare l’avanzamento.

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

Il BPA fornisce un’interfaccia HTTP che può essere utilizzata come alternativa all’interfaccia utente all’interno di AEM. L’interfaccia supporta sia i comandi HEAD che GET. Può essere utilizzato per generare il rapporto BPA e restituirlo in uno dei tre formati seguenti: JSON, CSV e valori delimitati da tabulazioni (TSV).

I seguenti URL sono disponibili per l&#39;accesso HTTP, dove `<host>` è il nome host, e se necessario la porta, del server in cui è installato BPA:
* `http://<host>/apps/best-practices-analyzer/analysis/report.json` per il formato JSON
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` per il formato CSV
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` per il formato TSV

### Esecuzione di una richiesta HTTP {#executing-http-request}

L’interfaccia HTTP può essere utilizzata in diversi modi.

Un modo semplice consiste nell’aprire una scheda del browser nello stesso browser in cui hai già effettuato l’accesso ad AEM come amministratore. Puoi inserire l’URL nella scheda del browser e visualizzare o scaricare i risultati dal browser.

È inoltre possibile utilizzare uno strumento della riga di comando come `curl` o `wget` e qualsiasi applicazione client HTTP. Se non utilizzi una scheda del browser con una sessione autenticata, devi fornire nel commento un nome utente e una password amministratore.

Il seguente è un esempio di come eseguire questa operazione:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`.

### Intestazioni e parametri {#http-headers-and-parameters}

Le seguenti intestazioni HTTP sono utilizzate da questa interfaccia:

* `Cache-Control: max-age=<seconds>`: specifica l&#39;intervallo di aggiornamento della cache in secondi. (consulta [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)).
* `Prefer: respond-async`: specifica che il server deve rispondere in modo asincrono. (consulta [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)).
* `Prefer: return=minimal`: specifica che il server deve restituire una risposta minima. (consulta [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)).

I seguenti parametri di query HTTP sono disponibili per comodità nei casi in cui le intestazioni HTTP potrebbero non essere facilmente utilizzate:

* `max-age` (numero, facoltativo): specifica l&#39;intervallo di aggiornamento della cache in secondi. Questo numero deve essere maggiore o uguale a 0. L&#39;intervallo di aggiornamento predefinito è di 86400 secondi. Senza questo parametro o l’intestazione corrispondente, viene utilizzata una nuova cache per distribuire le richieste per 24 ore, momento in cui la cache deve essere rigenerata. L&#39;utilizzo di `max-age=0` forzerà la cancellazione della cache e avvierà la rigenerazione del report, utilizzando l&#39;intervallo di aggiornamento precedente diverso da zero per la cache appena generata.
* `respond-async` (booleano, facoltativo): specifica che la risposta deve essere fornita in modo asincrono. Se si utilizza `respond-async=true` quando la cache non è aggiornata, il server restituirà una risposta di `202 Accepted` senza attendere l&#39;aggiornamento della cache e la generazione del report. Se la cache è aggiornata, questo parametro non ha alcun effetto. Il valore predefinito è `false`. Senza questo parametro o l’intestazione corrispondente, il server risponderà in modo sincrono, il che potrebbe richiedere molto tempo e un adeguamento del tempo di risposta massimo per il client HTTP.
* `may-refresh-cache` (booleano, facoltativo): specifica che il server può aggiornare la cache in risposta a una richiesta se la cache corrente è vuota, non aggiornata o non aggiornata. Se `may-refresh-cache=true` o non è specificato, il server potrebbe avviare un&#39;attività in background che richiamerà il rilevatore pattern e aggiornerà la cache. Se `may-refresh-cache=false`, il server non avvierà alcuna attività di aggiornamento che altrimenti sarebbe stata eseguita se la cache fosse vuota o non aggiornata, nel qual caso il report è vuoto. Questo parametro non influisce su eventuali attività di aggiornamento già in corso.
* `return-minimal` (booleano, facoltativo): specifica che la risposta dal server deve includere solo lo stato contenente l&#39;indicazione di avanzamento e lo stato della cache in formato JSON. Se `return-minimal=true`, il corpo della risposta è limitato all&#39;oggetto di stato. Se `return-minimal=false` o non è specificato, viene fornita una risposta completa.
* `log-findings` (booleano, facoltativo): specifica che il server deve registrare il contenuto della cache al momento della prima generazione o aggiornamento. Ogni risultato dalla cache viene registrato come stringa JSON. Questa registrazione verrà eseguita solo se `log-findings=true` e la richiesta genera una nuova cache.

Se sono presenti sia un’intestazione HTTP che il parametro di query corrispondente, il parametro di query avrà la priorità.

Un modo semplice per avviare la generazione del rapporto tramite l’interfaccia HTTP è l’utilizzo del seguente comando:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`.

Una volta effettuata la richiesta, non c’è bisogno che il client rimanga attivo affinché venga generato il rapporto. La generazione del rapporto può essere avviata con un client utilizzando una richiesta HTTP GET e, una volta generato, può essere visualizzato dalla cache con un altro client o con lo strumento BPA nell’interfaccia utente di AEM.

### Risposte {#http-responses}

Sono possibili i seguenti valori di risposta:

* `200 OK`: indica che la risposta contiene i risultati del rilevatore pattern generati nell&#39;intervallo di aggiornamento della cache.
* `202 Accepted`: utilizzato per indicare che la cache non è aggiornata. Quando `respond-async=true` e `may-refresh-cache=true` questa risposta indica che è in corso un&#39;attività di aggiornamento. Quando `may-refresh-cache=false` questa risposta indica semplicemente che la cache non è aggiornata.
* `400 Bad Request`: indica che la richiesta ha restituito un errore. Un messaggio nel formato Dettagli del problema (vedere [RFC 7807](https://tools.ietf.org/html/rfc7807)) fornisce ulteriori dettagli.
* `401 Unauthorized`: indica che la richiesta non è stata autorizzata.
* `500 Internal Server Error`: indica che si è verificato un errore interno del server. Un messaggio nel formato Dettagli del problema fornisce ulteriori dettagli.
* `503 Service Unavailable`: indica che il server è occupato con un’altra risposta e non può soddisfare questa richiesta in modo tempestivo. È probabile che ciò si verifichi solo quando vengono effettuate richieste sincrone. Un messaggio nel formato Dettagli del problema fornisce ulteriori dettagli.

## Informazioni per l’amministratore

### Regolazione durata cache {#cache-adjustment}

La durata predefinita della cache BPA è di 24 ore. Con l’opzione per aggiornare un rapporto e rigenerare la cache, sia nell’istanza di AEM che nell’interfaccia HTTP, questo valore predefinito è probabilmente appropriato per la maggior parte degli usi del BPA. Se il tempo di generazione del rapporto è particolarmente lungo per l’istanza di AEM, è possibile regolare la durata della cache per ridurre al minimo la rigenerazione del rapporto.

Il valore della durata della cache viene memorizzato come la proprietà `maxCacheAge` nel seguente nodo di archivio:
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

Il valore di questa proprietà corrisponde alla durata della cache, in secondi. Un amministratore può regolare la durata della cache utilizzando CRX/DE Lite.

### Installazione in AEM 6.1 {#installing-on-aem61}

BPA utilizza un account utente del servizio di sistema denominato `repository-reader-service` per eseguire il rilevatore pattern. Questo account è disponibile in AEM 6.2 e versioni successive. In AEM 6.1, l&#39;account deve essere creato *prima dell&#39;installazione di* di BPA, eseguendo la procedura seguente:

1. Per creare un utente segui le istruzioni in [Creazione di un nuovo utente di servizio](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user). Imposta UserID su `repository-reader-service` e lascia vuoto il Percorso intermedio, quindi fai clic sul segno di spunta verde.

2. Segui le istruzioni riportate nella sezione [Gestione di utenti e gruppi](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups), in particolare Aggiunta di utenti a un gruppo, per aggiungere l’utente `repository-reader-service` al gruppo `administrators`.

3. Installa il pacchetto BPA tramite Gestione pacchetti nell’istanza AEM di origine. Questa azione aggiunge la necessaria modifica alla configurazione ServiceUserMapper per l’utente di servizio del sistema `repository-reader-service`.)
