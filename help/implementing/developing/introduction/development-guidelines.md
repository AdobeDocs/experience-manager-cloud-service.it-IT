---
title: Linee guida per lo sviluppo per AEM as a Cloud Service
description: Linee guida per lo sviluppo per AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: 5a4353cb31337882a1c13b0ed830ea64f617181a
workflow-type: tm+mt
source-wordcount: '2284'
ht-degree: 1%

---


# Linee guida per lo sviluppo per AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

Il codice in esecuzione in AEM come Cloud Service deve essere consapevole del fatto che è sempre in esecuzione in un cluster. Ciò significa che ci sono sempre in esecuzione più di un’istanza. Il codice deve essere resiliente, in particolare perché un’istanza potrebbe essere arrestata in qualsiasi momento.

Durante l&#39;aggiornamento di AEM come Cloud Service, ci saranno istanze con codice vecchio e nuovo in esecuzione in parallelo. Pertanto, il vecchio codice non deve essere in conflitto con il contenuto creato dal nuovo codice e il nuovo codice deve essere in grado di gestire il vecchio contenuto.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Se è necessario identificare il principale nel cluster, l&#39;API Sling Discovery di Apache può essere utilizzata per rilevarlo.

## Stato in memoria {#state-in-memory}

Lo stato non deve essere mantenuto in memoria ma mantenuto nell&#39;archivio. In caso contrario, questo stato potrebbe andare perso se un&#39;istanza viene arrestata.

## Stato del file system {#state-on-the-filesystem}

Il file system dell&#39;istanza non deve essere utilizzato in AEM come Cloud Service. Il disco è effimero e verrà eliminato quando le istanze vengono riciclate. L&#39;uso limitato del filesystem per l&#39;archiviazione temporanea in relazione all&#39;elaborazione di singole richieste è possibile, ma non deve essere abusato per file enormi. Questo perché potrebbe avere un impatto negativo sulla quota di utilizzo delle risorse ed essere sottoposto a limitazioni del disco.

Ad esempio, quando l’utilizzo del file system non è supportato, il livello di pubblicazione deve garantire che tutti i dati da mantenere vengano inviati a un servizio esterno per l’archiviazione a più lungo termine.

## Osservazione {#observation}

Simile, con tutto ciò che accade in modo asincrono come agire sugli eventi di osservazione, non può essere garantito di essere eseguito localmente e quindi deve essere utilizzato con cura. Questo vale sia per gli eventi JCR che per gli eventi di risorse Sling. Al momento in cui si verifica un cambiamento, l’istanza può essere rimossa e sostituita da un’istanza diversa. Altre istanze nella topologia che sono attive in quel momento saranno in grado di reagire a quell&#39;evento. In questo caso, tuttavia, non si tratterà di un evento locale e potrebbe persino non esserci un leader attivo in caso di elezioni di leader in corso al momento dell&#39;evento.

## Attività in background e processi a esecuzione lunga {#background-tasks-and-long-running-jobs}

Il codice eseguito come attività in background deve presupporre che l&#39;istanza in cui è in esecuzione possa essere disattivata in qualsiasi momento. Pertanto, il codice deve essere resiliente e la maggior parte delle importazioni deve essere ripristinabile. Ciò significa che, se il codice viene rieseguito, non dovrebbe ricominciare dall&#39;inizio ma piuttosto essere vicino a dove è stato disattivato. Anche se questo non è un nuovo requisito per questo tipo di codice, in AEM come Cloud Service è più probabile che si verifichi una rimozione dell&#39;istanza.

Per ridurre al minimo i problemi, i posti di lavoro a lungo termine dovrebbero essere evitati, se possibile, e dovrebbero essere ripresi al minimo. Per eseguire tali lavori, utilizza Processi Sling, che hanno una garanzia almeno una volta e quindi se vengono interrotti, verrà rieseguito il prima possibile. Ma probabilmente non dovrebbero ricominciare dall&#39;inizio. Per pianificare tali lavori, è consigliabile utilizzare la pianificazione [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) in quanto questa è di nuovo l&#39;esecuzione almeno una volta.

L’utilità di pianificazione Sling Commons non deve essere utilizzata per la pianificazione in quanto l’esecuzione non può essere garantita. È più probabile che sia programmato.

Allo stesso modo, con tutto ciò che sta accadendo in modo asincrono, come agire sugli eventi di osservazione (che si tratti di eventi JCR o di eventi di risorse Sling), non può essere garantito di essere eseguito e quindi deve essere utilizzato con cura. Questo vale già per AEM distribuzioni nel presente.

## Connessioni HTTP in uscita {#outgoing-http-connections}

Si consiglia vivamente che tutte le connessioni HTTP in uscita impostino tempi di connessione e di lettura ragionevoli. Per il codice che non applica questi timeout, AEM istanze in esecuzione su AEM come Cloud Service applicheranno un timeout globale. Questi valori di timeout sono di 10 secondi per le chiamate di connessione e di 60 secondi per le chiamate di lettura per le connessioni utilizzate dalle seguenti librerie Java popolari:

L&#39;Adobe consiglia di utilizzare la [libreria client 4.x Apache HttpComponents fornita](https://hc.apache.org/httpcomponents-client-ga/) per effettuare connessioni HTTP.

Le alternative che funzionano, ma che possono richiedere di fornire la dipendenza sono:

* [java.net.](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) URLe/o  [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html)  (fornito da AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/)  (non consigliato in quanto è obsoleto e sostituito dalla versione 4.x)
* [OK Http](https://square.github.io/okhttp/)  (non fornito da AEM)

## Nessuna personalizzazione dell&#39;interfaccia classica {#no-classic-ui-customizations}

AEM come Cloud Service supporta solo l’interfaccia utente touch per il codice cliente di terze parti. Interfaccia classica non disponibile per la personalizzazione.

## Evitare i binari nativi {#avoid-native-binaries}

Il codice non sarà in grado di scaricare i binari in fase di runtime né modificarli. Ad esempio, non sarà in grado di decomprimere i file `jar` o `tar`.

## Nessun binario in streaming tramite AEM come Cloud Service {#no-streaming-binaries}

I binari sono accessibili tramite la rete CDN, che servirà i binari al di fuori dei servizi di base AEM.

Ad esempio, non utilizzare `asset.getOriginal().getStream()`, che attiva il download di un binario sul disco effimero del servizio AEM.

## Nessun agente di replica inversa {#no-reverse-replication-agents}

La replica inversa da Pubblica a Autore non è supportata in AEM come Cloud Service. Se tale strategia è necessaria, puoi utilizzare un archivio di persistenza esterno condiviso tra la farm delle istanze Publish e potenzialmente il cluster Author.

## È possibile che sia necessario portare gli agenti di replica successivi {#forward-replication-agents}

Il contenuto viene replicato da Autore a Pubblica tramite un meccanismo secondario di pubblicazione. Gli agenti di replica personalizzati non sono supportati.

## Monitoraggio e debug {#monitoring-and-debugging}

### Registri {#logs}

Per lo sviluppo locale, le voci dei registri vengono scritte in file locali nella cartella `/crx-quickstart/logs` .

Negli ambienti Cloud, gli sviluppatori possono scaricare i registri tramite Cloud Manager o utilizzare uno strumento a riga di comando per visualizzare i registri. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Impostazione del livello di registro**

Per modificare i livelli di registro per gli ambienti Cloud, la configurazione Sling Logging OSGI deve essere modificata e seguita da una ridistribuzione completa. Poiché questo non è istantaneo, presta attenzione nell&#39;abilitare registri dettagliati su ambienti di produzione che ricevono molto traffico. In futuro, è possibile che ci saranno meccanismi per cambiare più rapidamente il livello di log.

>[!NOTE]
>
>Per eseguire le modifiche di configurazione elencate di seguito, devi crearle in un ambiente di sviluppo locale e quindi inviarle a un AEM come istanza di Cloud Service. Per ulteriori informazioni su come eseguire questa operazione, consulta [Distribuzione di AEM come Cloud Service](/help/implementing/deploying/overview.md).

**Attivazione del livello di registro DEBUG**

Il livello di registro predefinito è INFO, ovvero i messaggi DEBUG non vengono registrati.
Per attivare il livello di log DEBUG, imposta la

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

per eseguire il debug. Non lasciare il registro a livello di registro DEBUG più a lungo del necessario, in quanto genera molti registri.
Una riga nel file di debug solitamente inizia con DEBUG, e quindi fornisce il livello di log, l&#39;azione di installazione e il messaggio di log. Esempio:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

I livelli di log sono i seguenti:

| 0 | Errore irreversibile | L&#39;azione non è riuscita e non è possibile continuare l&#39;installazione. |
|---|---|---|
| 1 | Errore | L&#39;azione non è riuscita. L&#39;installazione continua, ma una parte di CRX non è stata installata correttamente e non funzionerà. |
| 2 | Avvertenza | L&#39;azione è riuscita ma si sono verificati problemi. CRX potrebbe funzionare o meno correttamente. |
| 3 | Informazioni | L&#39;azione è riuscita. |

### Dump dei thread {#thread-dumps}

Le immagini di thread sugli ambienti Cloud vengono raccolte su base continuativa, ma al momento non possono essere scaricate in modo self-service. Nel frattempo, contatta AEM supporto se sono necessarie immagini thread per il debug di un problema, specificando l&#39;intervallo di tempo esatto.

## CRX/DE Lite e Developer Console {#crxde-lite-and-developer-console}

### Sviluppo locale {#local-development}

Per lo sviluppo locale, gli sviluppatori possono accedere completamente ad CRXDE Lite (`/crx/de`) e alla AEM Web Console (`/system/console`).

Sullo sviluppo locale (utilizzando l’avvio rapido per il cloud), `/apps` e `/libs` possono essere scritti direttamente, in modo diverso dagli ambienti Cloud in cui tali cartelle di livello superiore non sono modificabili.

### AEM come strumenti di sviluppo del Cloud Service {#aem-as-a-cloud-service-development-tools}

I clienti possono accedere a CRXDE lite nell’ambiente di sviluppo del livello di authoring, ma non in quello di stage o produzione. L&#39;archivio immutabile (`/libs`, `/apps`) non può essere scritto in fase di esecuzione, pertanto il tentativo di eseguire tale operazione provocherà errori.

Un set di strumenti per il debug AEM come ambienti di sviluppatori di Cloud Service è disponibile in Developer Console per gli ambienti di sviluppo, stage e produzione. L’URL può essere determinato regolando gli url del servizio Author o Publish come segue:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Come scelta rapida, il seguente comando CLI di Cloud Manager può essere utilizzato per avviare la console dello sviluppatore in base a un parametro di ambiente descritto di seguito:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Per ulteriori informazioni, consulta [questa pagina](/help/release-notes/home.md) .

Gli sviluppatori possono generare informazioni sullo stato e risolvere varie risorse.

Come illustrato di seguito, le informazioni sugli stati disponibili includono lo stato dei bundle, dei componenti, delle configurazioni OSGI, degli indici oak, dei servizi OSGI e dei processi Sling.

![Console di sviluppo 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Come illustrato di seguito, gli sviluppatori possono risolvere le dipendenze dei pacchetti e i servlet:

![Console di sviluppo 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Console di sviluppo 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Utile anche per il debug, la Console per sviluppatori ha un collegamento allo strumento Explain Query :

![Console di sviluppo 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Per i programmi di produzione, l’accesso alla Console per sviluppatori è definito nell’Admin Console dal ruolo &quot;Cloud Manager - Developer Role&quot; , mentre per i programmi sandbox, la Console per sviluppatori è disponibile per qualsiasi utente con un profilo di prodotto che gli consente di accedere a AEM come Cloud Service. Per tutti i programmi, è necessario &quot;Cloud Manager - Ruolo sviluppatore&quot; per le immagini di stato e gli utenti devono essere definiti anche nel profilo di prodotto Utenti AEM o Amministratori AEM sui servizi di authoring e pubblicazione per visualizzare i dati di dump di stato di entrambi i servizi. Per ulteriori informazioni sulla configurazione delle autorizzazioni per gli utenti, consulta [Documentazione di Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).


### Servizio di staging e produzione AEM {#aem-staging-and-production-service}

I clienti non avranno accesso agli strumenti per sviluppatori per gli ambienti di staging e produzione.

### Monitoraggio delle prestazioni {#performance-monitoring}

L&#39;Adobe monitora le prestazioni delle applicazioni e adotta misure per risolvere il problema se si osserva un deterioramento. Al momento, le metriche dell’applicazione non possono essere osservate.

## Indirizzo IP dedicato {#dedicated-egress-ip-address}

Su richiesta, AEM come Cloud Service fornirà un indirizzo IP statico e dedicato per il traffico in uscita HTTP (porta 80) e HTTPS (porta 443) programmato nel codice Java.

### Vantaggi {#benefits}

Questo indirizzo IP dedicato può migliorare la sicurezza durante l’integrazione con i fornitori SaaS (come un fornitore di gestione delle relazioni con i clienti) o altre integrazioni al di fuori di AEM come Cloud Service che offre un inserì nell&#39;elenco Consentiti di indirizzi IP. Aggiungendo l’indirizzo IP dedicato all’inserire nell&#39;elenco Consentiti, si garantisce che solo il traffico proveniente dal Cloud Service di AEM del cliente possa fluire nel servizio esterno. Oltre al traffico proveniente da qualsiasi altro IP consentito.

Senza la funzione di indirizzo IP dedicato abilitata, il traffico proveniente da AEM come Cloud Service scorre attraverso un set di IP condivisi con altri clienti.

### Configurazione {#configuration}

Per abilitare un indirizzo IP dedicato, invia una richiesta all’Assistenza clienti, che fornirà le informazioni sull’indirizzo IP. La richiesta deve specificare ogni ambiente ed effettuare richieste aggiuntive se i nuovi ambienti necessitano della funzione dopo la richiesta iniziale. Gli ambienti del programma sandbox non sono supportati.

### Utilizzo delle funzioni {#feature-usage}

La funzione è compatibile con il codice Java o con le librerie che generano traffico in uscita, purché utilizzino le proprietà standard del sistema Java per le configurazioni proxy. In pratica, dovrebbe includere la maggior parte delle librerie comuni.

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

Lo stesso IP dedicato viene applicato a tutti i programmi di un cliente nella propria organizzazione di Adobe e a tutti gli ambienti in ciascuno dei loro programmi. Si applica sia ai servizi di authoring che di pubblicazione.

Sono supportate solo le porte HTTP e HTTPS. Ciò include HTTP/1.1, nonché HTTP/2 se crittografato.

### Considerazioni sul debug {#debugging-considerations}

Per verificare che il traffico sia effettivamente in uscita sull’indirizzo IP dedicato previsto, controlla i registri nel servizio di destinazione, se disponibili. In caso contrario, potrebbe essere utile richiamare un servizio di debug come [https://ifconfig.me/ip](https://ifconfig.me/ip), che restituirà l&#39;indirizzo IP chiamante.

## Invio di e-mail {#sending-email}

AEM come Cloud Service richiede che la posta in uscita sia crittografata. Le sezioni seguenti descrivono come richiedere, configurare e inviare e-mail.

### Richiesta di accesso {#requesting-access}

Per impostazione predefinita, le e-mail in uscita sono disabilitate. Per attivarlo, invia un ticket di supporto con:

1. Nome di dominio completo per il server di posta (ad esempio `smtp.sendgrid.net`)
1. La porta da utilizzare. Deve essere la porta 465 se supportata dal server di posta, altrimenti la porta 587. Si noti che la porta 587 può essere utilizzata solo se il server di posta richiede e applica TLS su quella porta
1. ID del programma e dell&#39;ambiente per gli ambienti per i quali desiderano inviare messaggi di posta elettronica
1. Indica se l’accesso SMTP è necessario per l’autore, la pubblicazione o entrambi.

### Invio di e-mail {#sending-emails}

È necessario utilizzare il [servizio OSGI Day CQ Mail Service](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) e inviare e-mail al server di posta indicato nella richiesta di supporto anziché direttamente ai destinatari.

AEM CS richiede l&#39;invio della posta attraverso la porta 465. Se un server di posta non supporta la porta 465, è possibile utilizzare la porta 587, purché l’opzione TLS sia abilitata.

>[!NOTE]
>
>L’Adobe non supporta SMTP che si estende su un indirizzo IP dedicato univoco.

### Configurazione {#email-configuration}

Le e-mail in AEM devono essere inviate utilizzando il servizio OSGi [Day CQ Mail Service](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Per informazioni dettagliate sulla configurazione delle impostazioni e-mail, consulta la [AEM documentazione 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html) . Per AEM come Cloud Service, è necessario apportare le seguenti modifiche al servizio `com.day.cq.mailer.DefaultMailService OSGI`:

Se è stata richiesta la porta 465:

* impostare `smtp.port` su `465`
* impostare `smtp.ssl` su `true`

Se la porta 587 è stata richiesta (consentita solo se il server di posta non supporta la porta 465):

* impostare `smtp.port` su `587`
* impostare `smtp.ssl` su `false`

La proprietà `smtp.starttls` viene impostata automaticamente da AEM come Cloud Service in fase di esecuzione su un valore appropriato. Pertanto, se `smtp.tls` è impostato su true, `smtp.startls` viene ignorato. Se `smtp.ssl` è impostato su false, `smtp.starttls` è impostato su true. Questo è indipendentemente dai valori `smtp.starttls` impostati nella configurazione OSGI.