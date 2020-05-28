---
title: Linee guida per lo sviluppo per AEM as a Cloud Service
description: Da completare
translation-type: tm+mt
source-git-commit: 8e8863d390132ff8df943548b04e9d7c636c4248
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 1%

---


# Linee guida per lo sviluppo per AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

Il codice in esecuzione in AEM come servizio cloud deve essere consapevole del fatto che è sempre in esecuzione in un cluster. Ciò significa che è sempre in esecuzione più di un&#39;istanza. Il codice deve essere resiliente, in particolare perché un&#39;istanza potrebbe essere arrestata in qualsiasi momento.

Durante l&#39;aggiornamento di AEM come servizio cloud, saranno presenti istanze con codice vecchio e nuovo in esecuzione in parallelo. Pertanto, il vecchio codice non deve essere in conflitto con il contenuto creato dal nuovo codice e il nuovo codice deve essere in grado di gestire il contenuto precedente.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Se è necessario identificare il master nel cluster, Apache Sling Discovery API può essere utilizzata per rilevarlo.

## Stato in memoria {#state-in-memory}

Lo stato non deve essere mantenuto in memoria ma mantenuto nella directory archivio. In caso contrario, questo stato potrebbe andare perso se un&#39;istanza viene arrestata.

## Stato del file system {#state-on-the-filesystem}

Il file system dell&#39;istanza non deve essere utilizzato in AEM come servizio cloud. Il disco è effimero e verrà smaltito quando le istanze vengono riciclate. L&#39;uso limitato del filesystem per l&#39;archiviazione temporanea in relazione all&#39;elaborazione di singole richieste è possibile, ma non dovrebbe essere abusato per i file enormi. Questo perché potrebbe avere un impatto negativo sulla quota di utilizzo delle risorse ed essere eseguito nei limiti del disco.

Ad esempio, se l’utilizzo del file system non è supportato, il livello Pubblica deve garantire che tutti i dati da mantenere vengano inviati a un servizio esterno per l’archiviazione a lungo termine.

## Osservazione {#observation}

Analogamente, con tutto ciò che sta accadendo in modo asincrono come agire su eventi di osservazione, non può essere garantito che sia eseguito localmente e quindi deve essere utilizzato con cura. Ciò è vero sia per gli eventi JCR che per gli eventi delle risorse Sling. Nel momento in cui si verifica una modifica, l’istanza può essere chiusa e sostituita da un’altra istanza. Altre istanze della topologia attive in quel momento saranno in grado di reagire a tale evento. In questo caso, tuttavia, non si tratterà di un evento locale e potrebbe addirittura non esserci un leader attivo in caso di elezioni di leader in corso al momento dell&#39;emissione dell&#39;evento.

## Attività in background e processi con esecuzione prolungata {#background-tasks-and-long-running-jobs}

Il codice eseguito come attività in background deve presupporre che l&#39;istanza in cui è in esecuzione possa essere ridotta in qualsiasi momento. Pertanto, il codice deve essere resiliente e la maggior parte delle importazioni deve essere ripristinabile. Ciò significa che se il codice viene rieseguito, non dovrebbe ricominciare dall&#39;inizio ma piuttosto avvicinarsi a quello che ha lasciato. Anche se questo non è un nuovo requisito per questo tipo di codice, in AEM come servizio cloud è più probabile che si verifichi una rimozione dell&#39;istanza.

Per ridurre al minimo i problemi, è necessario evitare i lavori a lungo termine, se possibile, che dovrebbero essere ripresi al minimo. Per eseguire tali processi, utilizzate Processi Sling, che dispongono di una garanzia almeno una volta e quindi se vengono interrotti, verranno rieseguiti il prima possibile. Ma probabilmente non dovrebbero ricominciare dall&#39;inizio. Per la pianificazione di tali processi, è consigliabile utilizzare il pianificatore [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) , in quanto questa è di nuovo l’esecuzione almeno una volta.

L&#39;Utilità di pianificazione Sling Commons non deve essere utilizzata per la pianificazione, perché non è possibile garantire l&#39;esecuzione. È molto più probabile che venga pianificato.

Allo stesso modo, con tutto ciò che sta accadendo in modo asincrono, come agire su eventi di osservazione, (che si tratti di eventi JCR o di eventi di risorse Sling), non può essere garantito di essere eseguito e quindi deve essere utilizzato con attenzione. Questo è già vero per le distribuzioni AEM al momento.

## Connessioni HTTP in uscita {#outgoing-http-connections}

È vivamente consigliato che qualsiasi connessione HTTP in uscita imposti timeout ragionevoli di connessione e lettura. Per il codice che non applica questi timeout, le istanze AEM in esecuzione su AEM come servizio cloud applicheranno un timeout globale. Questi valori di timeout sono 10 secondi per le chiamate di connessione e 60 secondi per le chiamate di lettura per le connessioni utilizzate dalle seguenti librerie Java popolari:

Adobe consiglia di utilizzare la libreria [](https://hc.apache.org/httpcomponents-client-ga/) Apache HttpComponents Client 4.x fornita per effettuare connessioni HTTP.

Le alternative che funzionano, ma che possono richiedere di fornire la dipendenza sono:

* [java.net.UR](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) e/o [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (fornito da AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (non consigliato in quanto è obsoleto e sostituito dalla versione 4.x)
* [OK Http](https://square.github.io/okhttp/) (non fornito da AEM)

## Nessuna personalizzazione interfaccia classica {#no-classic-ui-customizations}

AEM come servizio Cloud supporta solo l&#39;interfaccia touch per il codice cliente di terze parti. L’interfaccia classica non è disponibile per la personalizzazione.

## Evitare i binari nativi {#avoid-native-binaries}

Il codice non sarà in grado di scaricare i file binari in fase di esecuzione né di modificarli. Ad esempio, non sarà in grado di decomprimere `jar` o `tar` i file.

## Nessun binario in streaming tramite AEM come servizio cloud {#no-streaming-binaries}

I file binari devono essere accessibili tramite la rete CDN, che servirà i file binari al di fuori dei servizi AEM di base.

Ad esempio, non utilizzate `asset.getOriginal().getStream()`, il che attiva il download di un binario sul disco temporaneo del servizio AEM.

## Nessun agente di replica inversa {#no-reverse-replication-agents}

La replica inversa da Pubblica a Autore non è supportata in AEM come servizio cloud. Se tale strategia è necessaria, potete utilizzare uno store di persistenza esterno condiviso tra le farm di istanze Pubblica e potenzialmente il cluster Autore.

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
>Per eseguire le modifiche di configurazione elencate di seguito, è necessario crearle in un ambiente di sviluppo locale e quindi inviarle a un’istanza AEM come servizio cloud. Per ulteriori informazioni su come eseguire questa operazione, consulta [Implementazione in AEM come servizio](/help/implementing/deploying/overview.md)cloud.

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

Le discariche di thread negli ambienti Cloud vengono raccolte in modo continuativo, ma al momento non possono essere scaricate in modo autonomo. Nel frattempo, contattate il supporto di AEM se sono necessari dei thread dumps per il debug di un problema, specificando la finestra temporale esatta.

## Console di sistema CRX/DE Lite {#crxde-lite-and-system-console}

### Sviluppo locale {#local-development}

Per lo sviluppo locale, gli sviluppatori possono accedere completamente a CRXDE Lite (`/crx/de`) e alla console Web di AEM (`/system/console`).

Sullo sviluppo locale (tramite l&#39;avvio rapido per il cloud) `/apps` e `/libs` può essere scritto direttamente, il che è diverso dagli ambienti Cloud in cui tali cartelle di livello superiore sono immutabili.

### AEM as a Cloud Service Development tools {#aem-as-a-cloud-service-development-tools}

I clienti possono accedere a CRXDE lite nell&#39;ambiente di sviluppo, ma non sullo stage o sulla produzione. L&#39;archivio immutabile (`/libs`, `/apps`) non può essere scritto in fase di esecuzione, pertanto il tentativo di eseguire tale operazione potrebbe causare errori.

Una serie di strumenti per il debug di AEM come ambienti per sviluppatori di servizi cloud sono disponibili in Developer Console per gli ambienti di sviluppo, fase e produzione. Per determinare l’URL, regolate gli URL del servizio Autore o Pubblica nel modo seguente:

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

Per i programmi regolari, l&#39;accesso alla Developer Console è definito da &quot;Cloud Manager - ruolo sviluppatore&quot; nell&#39;Admin Console, mentre per i programmi sandbox, Developer Console è disponibile per qualsiasi utente con un profilo di prodotto che dia loro accesso ad AEM come servizio cloud. Per ulteriori informazioni sulla configurazione delle autorizzazioni per l&#39;utente, consulta la Documentazione [di](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)Cloud Manager.



### Servizio di gestione e produzione AEM {#aem-staging-and-production-service}

I clienti non avranno accesso agli strumenti di sviluppo per gli ambienti di produzione e di staging.

### Monitoraggio delle prestazioni {#performance-monitoring}

Adobe controlla le prestazioni delle applicazioni e adotta misure per risolvere eventuali situazioni di deterioramento. Al momento, le metriche dell&#39;applicazione non possono essere osservate.
