---
title: Linee guida per lo sviluppo per AEM as a Cloud Service
description: Da completare
translation-type: tm+mt
source-git-commit: 171284a6f629dcf13d1fadfc6b7b5f0e69e41d84
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 1%

---


# Linee guida per lo sviluppo per AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

Il codice in esecuzione in AEM come Cloud Service deve essere consapevole del fatto che è sempre in esecuzione in un cluster. Ciò significa che ci sono sempre in esecuzione più di un’istanza. Il codice deve essere resiliente, in particolare perché un&#39;istanza potrebbe essere arrestata in qualsiasi momento.

Durante l&#39;aggiornamento di AEM come Cloud Service, ci saranno istanze con codice vecchio e nuovo in esecuzione in parallelo. Pertanto, il vecchio codice non deve essere in conflitto con il contenuto creato dal nuovo codice e il nuovo codice deve essere in grado di gestire il contenuto precedente.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Se è necessario identificare il primario nel cluster, Apache Sling Discovery API può essere utilizzata per rilevarlo.

## Stato in memoria {#state-in-memory}

Lo stato non deve essere mantenuto in memoria ma mantenuto nella directory archivio. In caso contrario, questo stato potrebbe andare perso se un&#39;istanza viene arrestata.

## Stato del file system {#state-on-the-filesystem}

Il file system dell&#39;istanza non deve essere utilizzato in AEM come Cloud Service. Il disco è effimero e verrà smaltito quando le istanze vengono riciclate. L&#39;uso limitato del filesystem per l&#39;archiviazione temporanea in relazione all&#39;elaborazione di singole richieste è possibile, ma non dovrebbe essere abusato per i file enormi. Questo perché potrebbe avere un impatto negativo sulla quota di utilizzo delle risorse ed essere eseguito nei limiti del disco.

Ad esempio, se l’utilizzo del file system non è supportato, il livello Pubblica deve garantire che tutti i dati da mantenere vengano inviati a un servizio esterno per l’archiviazione a lungo termine.

## Osservazione {#observation}

Analogamente, con tutto ciò che sta accadendo in modo asincrono come agire su eventi di osservazione, non può essere garantito che sia eseguito localmente e quindi deve essere utilizzato con cura. Ciò è vero sia per gli eventi JCR che per gli eventi delle risorse Sling. Nel momento in cui si verifica una modifica, l’istanza può essere chiusa e sostituita da un’altra istanza. Altre istanze della topologia attive in quel momento saranno in grado di reagire a tale evento. In questo caso, tuttavia, non si tratterà di un evento locale e potrebbe addirittura non esserci un leader attivo in caso di elezioni di leader in corso al momento dell&#39;emissione dell&#39;evento.

## Attività in background e processi con esecuzione prolungata {#background-tasks-and-long-running-jobs}

Il codice eseguito come attività in background deve presupporre che l&#39;istanza in cui è in esecuzione possa essere ridotta in qualsiasi momento. Pertanto, il codice deve essere resiliente e la maggior parte delle importazioni deve essere ripristinabile. Ciò significa che se il codice viene rieseguito, non dovrebbe ricominciare dall&#39;inizio ma piuttosto avvicinarsi a quello che ha lasciato. Anche se questo non è un nuovo requisito per questo tipo di codice, in AEM come Cloud Service è più probabile che si verifichi una rimozione dell&#39;istanza.

Per ridurre al minimo i problemi, è necessario evitare i lavori a lungo termine, se possibile, che dovrebbero essere ripresi al minimo. Per eseguire tali processi, utilizzate Processi Sling, che dispongono di una garanzia almeno una volta e quindi se vengono interrotti, verranno rieseguiti il prima possibile. Ma probabilmente non dovrebbero ricominciare dall&#39;inizio. Per la pianificazione di tali processi, è consigliabile utilizzare il pianificatore [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) , in quanto questa è di nuovo l’esecuzione almeno una volta.

L&#39;Utilità di pianificazione Sling Commons non deve essere utilizzata per la pianificazione, perché non è possibile garantire l&#39;esecuzione. È molto più probabile che venga pianificato.

Allo stesso modo, con tutto ciò che sta accadendo in modo asincrono, come agire su eventi di osservazione, (che si tratti di eventi JCR o di eventi di risorse Sling), non può essere garantito di essere eseguito e quindi deve essere utilizzato con attenzione. Questo è già vero per AEM distribuzioni nel presente.

## Connessioni HTTP in uscita {#outgoing-http-connections}

È vivamente consigliato che qualsiasi connessione HTTP in uscita imposti timeout ragionevoli di connessione e lettura. Per il codice che non applica questi timeout, AEM istanze in esecuzione su AEM come Cloud Service applicheranno un timeout globale. Questi valori di timeout sono 10 secondi per le chiamate di connessione e 60 secondi per le chiamate di lettura per le connessioni utilizzate dalle seguenti librerie Java popolari:

 Adobe consiglia di utilizzare la libreria [](https://hc.apache.org/httpcomponents-client-ga/) Apache HttpComponents Client 4.x fornita per effettuare connessioni HTTP.

Le alternative che funzionano, ma che possono richiedere di fornire la dipendenza sono:

* [java.net.UR](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) e/o [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (fornito da AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (non consigliato in quanto è obsoleto e sostituito dalla versione 4.x)
* [OK Http](https://square.github.io/okhttp/) (non fornito da AEM)

## Nessuna personalizzazione interfaccia classica {#no-classic-ui-customizations}

AEM come Cloud Service supporta solo l&#39;interfaccia touch per il codice cliente di terze parti. L’interfaccia classica non è disponibile per la personalizzazione.

## Evitare i binari nativi {#avoid-native-binaries}

Il codice non sarà in grado di scaricare i file binari in fase di esecuzione né di modificarli. Ad esempio, non sarà in grado di decomprimere `jar` o `tar` i file.

## Nessun binario in streaming tramite AEM come Cloud Service {#no-streaming-binaries}

I file binari devono essere accessibili tramite la rete CDN, che servirà i file binari al di fuori dei servizi di AEM di base.

Ad esempio, non utilizzare `asset.getOriginal().getStream()`, che attiva il download di un binario sul disco temporaneo del servizio AEM.

## Nessun agente di replica inversa {#no-reverse-replication-agents}

La replica inversa da Pubblica a Autore non è supportata in AEM come Cloud Service. Se tale strategia è necessaria, potete utilizzare uno store di persistenza esterno condiviso tra le farm di istanze Pubblica e potenzialmente il cluster Autore.

## È possibile che sia necessario portare gli agenti di replica successivi {#forward-replication-agents}

Il contenuto viene replicato da Autore a Pubblica tramite un meccanismo secondario di pubblicazione. Gli agenti di replica personalizzati non sono supportati.

## Monitoraggio e debug {#monitoring-and-debugging}

### Registri {#logs}

Per lo sviluppo locale, le voci di registro sono scritte in file locali nella `/crx-quickstart/logs` cartella.

Negli ambienti Cloud, gli sviluppatori possono scaricare i registri tramite Cloud Manager o utilizzare uno strumento della riga di comando per localizzare i registri. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Impostazione del livello di registro**

Per modificare i livelli di registro per gli ambienti Cloud, la configurazione Sling Logging OSGI deve essere modificata, seguita da una ridistribuzione completa. Poiché non è istantaneo, essere cauti nell&#39;attivare log verbosi in ambienti di produzione che ricevono molto traffico. In futuro, è possibile che ci saranno meccanismi per cambiare più rapidamente il livello di registro.

>[!NOTE]
>
>Per eseguire le modifiche di configurazione elencate di seguito, è necessario crearle in un ambiente di sviluppo locale e quindi inviarle a un AEM come istanza di Cloud Service. Per ulteriori informazioni su come eseguire questa operazione, vedere [Distribuzione di AEM come Cloud Service](/help/implementing/deploying/overview.md).

**Attivazione del livello di registro DEBUG**

Il livello di registro predefinito è INFO, ovvero i messaggi DEBUG non vengono registrati.
Per attivare il livello di registro DEBUG, impostare la variabile

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

da eseguire il debug. Non lasciare il registro a livello di registro DEBUG più a lungo del necessario, in quanto genera molti registri.
Una riga nel file di debug in genere inizia con DEBUG, quindi fornisce il livello di registro, l&#39;azione del programma di installazione e il messaggio di registro. Ad esempio:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

I livelli di registro sono i seguenti:

| 0 | Errore irreversibile | L&#39;azione non è riuscita e il programma di installazione non può proseguire. |
|---|---|---|
| 1 | Errore | L&#39;azione non è riuscita. L&#39;installazione continua, ma una parte di CRX non è stata installata correttamente e non funzionerà. |
| 2 | Avvertenza | L&#39;azione è riuscita ma ha incontrato dei problemi. CRX può funzionare o meno correttamente. |
| 3 | Informazioni | L&#39;azione è riuscita. |

### Cassetti di thread {#thread-dumps}

Le discariche di thread negli ambienti Cloud vengono raccolte in modo continuativo, ma al momento non possono essere scaricate in modo autonomo. Nel frattempo, contattate AEM supporto se sono necessari dei thread dumps per il debug di un problema, specificando la finestra temporale esatta.

## Console di sistema CRX/DE Lite {#crxde-lite-and-system-console}

### Sviluppo locale {#local-development}

Per lo sviluppo locale, gli sviluppatori hanno accesso completo ai CRXDE Lite (`/crx/de`) e alla AEM Web Console (`/system/console`).

Sullo sviluppo locale (tramite l&#39;avvio rapido per il cloud) `/apps` e `/libs` può essere scritto direttamente, il che è diverso dagli ambienti Cloud in cui tali cartelle di livello superiore sono immutabili.

### AEM as a Cloud Service Development tools {#aem-as-a-cloud-service-development-tools}

I clienti possono accedere a CRXDE lite nell&#39;ambiente di sviluppo, ma non sullo stage o sulla produzione. L&#39;archivio immutabile (`/libs`, `/apps`) non può essere scritto in fase di esecuzione, pertanto il tentativo di eseguire tale operazione potrebbe causare errori.

Un set di strumenti per il debug AEM come ambienti di sviluppo di Cloud Service è disponibile in Developer Console per gli ambienti di sviluppo, fase e produzione. Per determinare l’URL, regolate gli URL del servizio Autore o Pubblica nel modo seguente:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Come scelta rapida, il seguente comando CLI di Cloud Manager può essere utilizzato per avviare la console dello sviluppatore in base a un parametro di ambiente descritto di seguito:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Per ulteriori informazioni, consulta [questa pagina](/help/release-notes/home.md) .

Gli sviluppatori possono generare informazioni sullo stato e risolvere diverse risorse.

Come illustrato di seguito, le informazioni sullo stato disponibili includono lo stato di bundle, componenti, configurazioni OSGI, indici di quercia, servizi OSGI e processi Sling.

![Dev Console 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Come illustrato di seguito, gli sviluppatori possono risolvere dipendenze e servlet del pacchetto:

![Dev Console 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Dev Console 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Utile anche per il debug, la console Sviluppatore dispone di un collegamento allo strumento Spiega query:

![Dev Console 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Per i programmi regolari, l&#39;accesso alla Developer Console è definito dal &quot;Cloud Manager - ruolo sviluppatore&quot; nel Admin Console , mentre per i programmi sandbox, Developer Console è disponibile per qualsiasi utente con un profilo di prodotto che dia loro accesso a AEM come Cloud Service. Per tutti i programmi, è necessario &quot;Cloud Manager - Ruolo sviluppatore&quot; per le discariche di stato e gli utenti devono essere definiti anche nel profilo di prodotto Utenti AEM o Amministratori AEM sui servizi di creazione e pubblicazione per visualizzare i dati di dump dello stato di entrambi i servizi. Per ulteriori informazioni sulla configurazione delle autorizzazioni per l&#39;utente, consulta la Documentazione [di](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)Cloud Manager.


### AEM Staging and Production Service {#aem-staging-and-production-service}

I clienti non avranno accesso agli strumenti di sviluppo per gli ambienti di produzione e di staging.

### Monitoraggio delle prestazioni {#performance-monitoring}

 Adobe controlla le prestazioni dell&#39;applicazione e adotta misure per far fronte a eventuali peggioramenti. Al momento, le metriche dell&#39;applicazione non possono essere osservate.

## Indirizzo IP Egress dedicato

Su richiesta, AEM un Cloud Service fornirà un indirizzo IP statico e dedicato per il traffico in uscita HTTP (porta 80) e HTTPS (porta 443) programmato nel codice Java.

### Vantaggi

Questo indirizzo IP dedicato può migliorare la sicurezza durante l&#39;integrazione con fornitori SaaS (come un fornitore CRM) o altre integrazioni esterne a AEM come Cloud Service che offre un  inserì nell&#39;elenco Consentiti di indirizzi IP. Aggiungendo l&#39;indirizzo IP dedicato al inserire nell&#39;elenco Consentiti di , si garantisce che solo il traffico dal Cloud Service del cliente AEM possa fluire nel servizio esterno. Oltre al traffico proveniente da qualsiasi altro IP consentito.

Senza la funzione di indirizzo IP dedicato abilitata, il traffico che esce dal AEM come Cloud Service scorre attraverso un insieme di IP condivisi con altri clienti.

### Configurazione

Per abilitare un indirizzo IP dedicato, inviate una richiesta all&#39;Assistenza clienti, che fornirà le informazioni sull&#39;indirizzo IP. La richiesta deve specificare ogni ambiente e richiedere ulteriori informazioni se i nuovi ambienti necessitano della funzione dopo la richiesta iniziale. Gli ambienti del programma sandbox non sono supportati.

### Utilizzo delle funzioni

La funzione è compatibile con il codice Java o con librerie che generano traffico in uscita, purché utilizzino le proprietà standard del sistema Java per le configurazioni proxy. In pratica, questo dovrebbe includere la maggior parte delle librerie comuni.

Di seguito è riportato un esempio di codice:

```
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

Lo stesso IP dedicato viene applicato a tutti i programmi dei clienti nell&#39;organizzazione  Adobe e a tutti gli ambienti in ciascuno dei loro programmi. Si applica sia ai servizi di creazione che ai servizi di pubblicazione.

Sono supportate solo le porte HTTP e HTTPS. Ciò include HTTP/1.1, nonché HTTP/2 se crittografati.

### Considerazioni sul debug

Per verificare che il traffico sia effettivamente in uscita sull&#39;indirizzo IP dedicato previsto, controllate i registri nel servizio di destinazione, se disponibili. In caso contrario, potrebbe essere utile chiamare un servizio di debug come [https://ifconfig.me/ip](https://ifconfig.me/ip), che restituirà l&#39;indirizzo IP chiamante.
