---
title: Linee guida per lo sviluppo in AEM as a Cloud Service
description: Scopri le linee guida per lo sviluppo su AEM modalità as a Cloud Service e su importanti modi in cui differisce da AEM nei locali e AEM in AMS.
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 01087aa2ec621d6bebd4d62edbc320df8122f71d
workflow-type: tm+mt
source-wordcount: '2591'
ht-degree: 2%

---

# Linee guida per lo sviluppo in AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="Linee guida per lo sviluppo in AEM as a Cloud Service"
>abstract="Scopri le linee guida per lo sviluppo su AEM modalità as a Cloud Service e su importanti modi in cui differisce da AEM nei locali e AEM in AMS."
>additional-url="https://video.tv.adobe.com/v/330555/?captions=ita/" text="Demo della struttura del pacchetto"

Questo documento presenta le linee guida per lo sviluppo su AEM modalità as a Cloud Service e su importanti modi in cui differisce da AEM nei locali e AEM in AMS.

## Il Codice Deve Essere Basato Su Cluster {#cluster-aware}

Il codice in esecuzione in AEM as a Cloud Service deve essere consapevole del fatto che è sempre in esecuzione in un cluster. Ciò significa che ci sono sempre in esecuzione più di un’istanza. Il codice deve essere resiliente, in particolare perché un’istanza potrebbe essere arrestata in qualsiasi momento.

Durante l&#39;aggiornamento di AEM as a Cloud Service, ci saranno istanze con codice vecchio e nuovo in esecuzione in parallelo. Pertanto, il vecchio codice non deve essere in conflitto con il contenuto creato dal nuovo codice e il nuovo codice deve essere in grado di gestire il vecchio contenuto.

Se è necessario identificare il principale nel cluster, l&#39;API Sling Discovery di Apache può essere utilizzata per rilevarlo.

## Stato in memoria {#state-in-memory}

Lo stato non deve essere mantenuto in memoria ma mantenuto nell&#39;archivio. In caso contrario, questo stato potrebbe andare perso se un&#39;istanza viene arrestata.

## Stato del filesystem {#state-on-the-filesystem}

Il file system dell&#39;istanza non deve essere utilizzato in AEM as a Cloud Service. Il disco è effimero e verrà eliminato quando le istanze vengono riciclate. L&#39;uso limitato del filesystem per l&#39;archiviazione temporanea in relazione all&#39;elaborazione di singole richieste è possibile, ma non deve essere abusato per file enormi. Questo perché potrebbe avere un impatto negativo sulla quota di utilizzo delle risorse ed essere sottoposto a limitazioni del disco.

Ad esempio, quando l’utilizzo del file system non è supportato, il livello di pubblicazione deve garantire che tutti i dati da mantenere vengano inviati a un servizio esterno per l’archiviazione a più lungo termine.

## Osservazione {#observation}

Simile, con tutto ciò che accade in modo asincrono come agire sugli eventi di osservazione, non può essere garantito di essere eseguito localmente e quindi deve essere utilizzato con cura. Questo vale sia per gli eventi JCR che per gli eventi di risorse Sling. Al momento in cui si verifica un cambiamento, l’istanza può essere rimossa e sostituita da un’istanza diversa. Altre istanze nella topologia che sono attive in quel momento saranno in grado di reagire a quell&#39;evento. In questo caso, tuttavia, non si tratterà di un evento locale e potrebbe persino non esserci un leader attivo in caso di elezioni di leader in corso al momento dell&#39;evento.

## Attività in background e processi con esecuzione lunga {#background-tasks-and-long-running-jobs}

Il codice eseguito come attività in background deve presupporre che l&#39;istanza in cui è in esecuzione possa essere disattivata in qualsiasi momento. Pertanto il codice deve essere resiliente e soprattutto riutilizzabile. Ciò significa che, se il codice viene rieseguito, non dovrebbe ricominciare dall&#39;inizio ma piuttosto essere vicino a dove è stato disattivato. Anche se questo non è un nuovo requisito per questo tipo di codice, in AEM as a Cloud Service è più probabile che si verifichi un&#39;istanza di rimozione.

Per ridurre al minimo i problemi, i posti di lavoro a lungo termine dovrebbero essere evitati, se possibile, e dovrebbero essere ripresi al minimo. Per eseguire tali lavori, utilizza Processi Sling, che hanno una garanzia almeno una volta e quindi se vengono interrotti, verrà rieseguito il prima possibile. Ma probabilmente non dovrebbero ricominciare dall&#39;inizio. Per pianificare tali lavori, è consigliabile utilizzare il [Processi Sling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) scheduler in questo modo assicura l’esecuzione almeno una volta.

L’utilità di pianificazione Sling Commons non deve essere utilizzata per la pianificazione in quanto l’esecuzione non può essere garantita. È più probabile che sia programmato.

Allo stesso modo, con tutto ciò che sta accadendo in modo asincrono, come agire sugli eventi di osservazione (che si tratti di eventi JCR o di eventi di risorse Sling), non può essere garantito di essere eseguito e quindi deve essere utilizzato con cura. Questo vale già per AEM distribuzioni nel presente.

## Connessioni HTTP in uscita {#outgoing-http-connections}

Si consiglia vivamente che tutte le connessioni HTTP in uscita impostino tempi di connessione e di lettura ragionevoli; i valori consigliati sono 1 secondo per il timeout della connessione e 5 secondi per il timeout della lettura. I numeri esatti devono essere determinati in base alle prestazioni del sistema backend che gestisce queste richieste.

Per il codice che non applica questi timeout, AEM istanze in esecuzione su AEM as a Cloud Service applicheranno un timeout globale. Questi valori di timeout sono di 10 secondi per le chiamate di connessione e di 60 secondi per le chiamate di lettura per le connessioni.

L&#39;Adobe raccomanda l&#39;uso del [Libreria client 4.x Apache HttpComponents Client](https://hc.apache.org/httpcomponents-client-ga/) per la creazione di connessioni HTTP.

Le alternative che funzionano, ma che possono richiedere di fornire la dipendenza sono:

* [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) e/o [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (Fornito da AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (non consigliato in quanto obsoleto e sostituito dalla versione 4.x)
* [OK Http](https://square.github.io/okhttp/) (Non fornito da AEM)

Oltre a fornire timeout, è necessario implementare anche una corretta gestione di tali timeout e codici di stato HTTP imprevisti.

## Nessuna personalizzazione dell’interfaccia classica {#no-classic-ui-customizations}

AEM as a Cloud Service supporta solo l’interfaccia utente touch per il codice cliente di terze parti. Interfaccia classica non disponibile per la personalizzazione.

## Evitare i binari nativi {#avoid-native-binaries}

Il codice non sarà in grado di scaricare i binari in fase di runtime né modificarli. Ad esempio, non sarà in grado di rimuovere il pacchetto `jar` o `tar` file.

## Nessun binario in streaming tramite AEM as a Cloud Service {#no-streaming-binaries}

I binari sono accessibili tramite la rete CDN, che servirà i binari al di fuori dei servizi di base AEM.

Ad esempio, non utilizzare `asset.getOriginal().getStream()`, che attiva il download di un binario sul disco effimero del servizio AEM.

## Nessun agente di replica inversa {#no-reverse-replication-agents}

La replica inversa da Pubblica a Autore non è supportata in AEM as a Cloud Service. Se tale strategia è necessaria, puoi utilizzare un archivio di persistenza esterno condiviso tra la farm delle istanze Publish e potenzialmente il cluster Author.

## È possibile che sia necessario portare gli agenti di replica successivi {#forward-replication-agents}

Il contenuto viene replicato da Autore a Pubblica tramite un meccanismo secondario di pubblicazione. Gli agenti di replica personalizzati non sono supportati.

## Monitoraggio e debug {#monitoring-and-debugging}

### Registri {#logs}

Per lo sviluppo locale, le voci dei registri vengono scritte in file locali nel `/crx-quickstart/logs` cartella.

Negli ambienti Cloud, gli sviluppatori possono scaricare i registri tramite Cloud Manager o utilizzare uno strumento a riga di comando per visualizzare i registri. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Impostazione del livello di registro**

Per modificare i livelli di registro per gli ambienti Cloud, la configurazione Sling Logging OSGI deve essere modificata e seguita da una ridistribuzione completa. Poiché questo non è istantaneo, presta attenzione nell&#39;abilitare registri dettagliati su ambienti di produzione che ricevono molto traffico. In futuro, è possibile che ci saranno meccanismi per cambiare più rapidamente il livello di log.

>[!NOTE]
>
>Per eseguire le modifiche di configurazione elencate di seguito, è necessario crearle in un ambiente di sviluppo locale e quindi inviarle a un&#39;istanza AEM as a Cloud Service. Per ulteriori informazioni su come eseguire questa operazione, consulta [Distribuzione a AEM as a Cloud Service](/help/implementing/deploying/overview.md).

**Attivazione del livello di registro DEBUG**

Il livello di registro predefinito è INFO, ovvero i messaggi DEBUG non vengono registrati. Per attivare il livello di registro DEBUG, aggiornare la seguente proprietà alla modalità di debug.

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

Ad esempio, imposta `/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` con il seguente valore.

```json
{
   "org.apache.sling.commons.log.names": [
      "com.example"
   ],
   "org.apache.sling.commons.log.level": "DEBUG",
   "org.apache.sling.commons.log.file": "logs/error.log",
   "org.apache.sling.commons.log.additiv": "false"
}
```

Non lasciare il registro a livello di registro DEBUG più a lungo del necessario, in quanto questo genera molte voci.

È possibile impostare livelli di registro discreti per i diversi ambienti AEM utilizzando il targeting di configurazione OSGi basato sulla modalità di esecuzione, se è opportuno effettuare sempre l&#39;accesso `DEBUG` durante lo sviluppo. Esempio:

| Ambiente | Posizione di configurazione OSGi in modalità di esecuzione | `org.apache.sling.commons.log.level` valore della proprietà | | - | - | - | | Sviluppo | /apps/example/config/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | DEBUG | | Stage | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | AVVERTENZA | | Produzione | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | ERRORE |

Una riga nel file di debug solitamente inizia con DEBUG, e quindi fornisce il livello di log, l&#39;azione di installazione e il messaggio di log. Esempio:

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

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

Per lo sviluppo locale, gli sviluppatori hanno pieno accesso ad CRXDE Lite (`/crx/de`) e la Console Web AEM (`/system/console`).

Tieni presente che nello sviluppo locale (utilizzando l’SDK), `/apps` e `/libs` può essere scritto direttamente in , che è diverso dagli ambienti Cloud in cui tali cartelle di livello superiore non sono modificabili.

### AEM strumenti di sviluppo as a Cloud Service {#aem-as-a-cloud-service-development-tools}

I clienti possono accedere a CRXDE lite nell’ambiente di sviluppo del livello di authoring, ma non in quello di stage o produzione. Archivio immutabile (`/libs`, `/apps`) non può essere scritto in fase di runtime, pertanto il tentativo di eseguire questa operazione genera errori.

È invece possibile avviare il browser Repository dalla Console per sviluppatori, fornendo una visualizzazione in sola lettura nell’archivio per tutti gli ambienti sui livelli di authoring, pubblicazione e anteprima. Ulteriori informazioni sul browser Repository [qui](/help/implementing/developing/tools/repository-browser.md).

Nella Console per sviluppatori per gli ambienti RDE, sviluppo, stage e produzione è disponibile un set di strumenti per il debug AEM ambienti di sviluppo as a Cloud Service. L’URL può essere determinato regolando gli url del servizio Author o Publish come segue:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Come scelta rapida, il seguente comando CLI di Cloud Manager può essere utilizzato per avviare la console dello sviluppatore in base a un parametro di ambiente descritto di seguito:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Vedi [questa pagina](/help/release-notes/home.md) per ulteriori informazioni.

Gli sviluppatori possono generare informazioni sullo stato e risolvere varie risorse.

Come illustrato di seguito, le informazioni sugli stati disponibili includono lo stato dei bundle, dei componenti, delle configurazioni OSGI, degli indici oak, dei servizi OSGI e dei processi Sling.

![Console di sviluppo 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Come illustrato di seguito, gli sviluppatori possono risolvere le dipendenze dei pacchetti e i servlet:

![Console di sviluppo 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Console di sviluppo 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Utile anche per il debug, la Console per sviluppatori ha un collegamento allo strumento Explain Query :

![Console di sviluppo 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Per i programmi di produzione, l’accesso alla Console per sviluppatori è definito nell’Admin Console dal ruolo &quot;Cloud Manager - Developer Role&quot; , mentre per i programmi sandbox, la Console per sviluppatori è disponibile per qualsiasi utente con un profilo di prodotto che consente loro di accedere a AEM as a Cloud Service. Per tutti i programmi, è necessario &quot;Cloud Manager - Ruolo sviluppatore&quot; per le immagini di stato e per il browser e gli utenti dell’archivio, nonché per visualizzare i dati di entrambi i servizi, è necessario definire il profilo di prodotto Utenti AEM o Amministratori sia sui servizi di authoring che su quelli di pubblicazione. Per ulteriori informazioni sulla configurazione delle autorizzazioni utente, consulta [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Monitoraggio delle prestazioni {#performance-monitoring}

L&#39;Adobe monitora le prestazioni delle applicazioni e adotta misure per risolvere il problema se si osserva un deterioramento. Al momento, le metriche dell’applicazione non possono essere osservate.

## Invio di e-mail {#sending-email}

Le sezioni seguenti descrivono come richiedere, configurare e inviare e-mail.

>[!NOTE]
>
>Il servizio di posta può essere configurato con il supporto OAuth2. Per ulteriori informazioni, consulta [Supporto OAuth2 per il servizio di posta](/help/security/oauth2-support-for-mail-service.md).

### Abilitazione dell’e-mail in uscita {#enabling-outbound-email}

Per impostazione predefinita, le porte utilizzate per inviare e-mail sono disabilitate. Per attivare una porta, configura [rete avanzata](/help/security/configuring-advanced-networking.md), assicurandosi di impostare per ogni ambiente necessario il `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` le regole di inoltro porta dell&#39;endpoint, che mappano la porta prevista (ad esempio, 465 o 587) su una porta proxy.

È consigliabile configurare una rete avanzata con un `kind` impostato su `flexiblePortEgress` poiché Adobe può ottimizzare le prestazioni del traffico in uscita flessibile della porta. Se è necessario un indirizzo IP di uscita univoco, scegli una `kind` parametro di `dedicatedEgressIp`. Se hai già configurato la VPN per altri motivi, puoi utilizzare anche l’indirizzo IP univoco fornito da tale variante di rete avanzata.

È necessario inviare e-mail tramite un server di posta anziché direttamente ai client di posta elettronica. In caso contrario, le e-mail potrebbero essere bloccate.

### Invio di e-mail {#sending-emails}

La [Servizio di posta CQ Servizio OSGI](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) devono essere utilizzati e le e-mail devono essere inviate al server di posta indicato nella richiesta di assistenza anziché direttamente ai destinatari.

### Configurazione {#email-configuration}

Le e-mail in AEM devono essere inviate utilizzando il [Servizio Day CQ Mail OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Consulta la sezione [Documentazione di AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) per informazioni sulla configurazione delle impostazioni e-mail. Per AEM as a Cloud Service, notare i seguenti adeguamenti necessari al `com.day.cq.mailer.DefaultMailService OSGI` servizio:

* Il nome host del server SMTP deve essere impostato su $[env:AEM_PROXY_HOST;default=proxy.tunnel]
* La porta del server SMTP deve essere impostata sul valore della porta proxy originale impostata nel parametro portForwards utilizzato nella chiamata API durante la configurazione della rete avanzata. Ad esempio, 30465 (anziché 465)

La porta del server SMTP deve essere impostata come `portDest` valore impostato nel parametro portForwards utilizzato nella chiamata API durante la configurazione di reti avanzate e il `portOrig` Il valore deve essere un valore significativo compreso nell’intervallo richiesto tra 30000 e 30999. Ad esempio, se la porta del server SMTP è 465, utilizzare la porta 30465 come `portOrig` valore.

In questo caso e presupponendo che SSL debba essere abilitato, nella configurazione del **OSGI servizio di posta CQ Day** servizio:

* Imposta `smtp.port` a `30465`
* Imposta `smtp.ssl` a `true`

In alternativa, se la porta di destinazione è 587, un `portOrig` è necessario utilizzare il valore 30587. E supponendo che SSL debba essere disabilitato, la configurazione del servizio OSGI Day CQ Mail Service:

* Imposta `smtp.port` a `30587`
* Imposta `smtp.ssl` a `false`

La `smtp.starttls` la proprietà viene impostata automaticamente da AEM as a Cloud Service in fase di runtime a un valore appropriato. Pertanto, se `smtp.ssl` è impostato su true, `smtp.startls` viene ignorato. Se `smtp.ssl` è impostato su false, `smtp.starttls` è impostato su true. Ciò è a prescindere dal `smtp.starttls` i valori impostati nella configurazione OSGI.


Facoltativamente, è possibile configurare il servizio di posta con il supporto OAuth2. Per ulteriori informazioni, consulta [Supporto OAuth2 per il servizio di posta](/help/security/oauth2-support-for-mail-service.md).

### Configurazione e-mail legacy {#legacy-email-configuration}

Prima della versione 2021.9.0, l’e-mail era configurata tramite una richiesta di assistenza clienti. Si osservano i seguenti adeguamenti necessari `com.day.cq.mailer.DefaultMailService OSGI` servizio:

AEM as a Cloud Service richiede l&#39;invio della posta attraverso la porta 465. Se un server di posta non supporta la porta 465, è possibile utilizzare la porta 587, purché l’opzione TLS sia abilitata.

Se è stata richiesta la porta 465:

* set `smtp.port` a `465`
* set `smtp.ssl` a `true`

e se la porta 587 è stata richiesta:

* set `smtp.port` a `587`
* set `smtp.ssl` a `false`

La `smtp.starttls` la proprietà viene impostata automaticamente da AEM as a Cloud Service in fase di runtime a un valore appropriato. Pertanto, se `smtp.ssl` è impostato su true, `smtp.startls` viene ignorato. Se `smtp.ssl` è impostato su false, `smtp.starttls` è impostato su true. Ciò è a prescindere dal `smtp.starttls` i valori impostati nella configurazione OSGI.

L&#39;host del server SMTP deve essere impostato su quello del server di posta.

## Evitare proprietà multivalore di grandi dimensioni {#avoid-large-mvps}

L’archivio di contenuti Oak alla base AEM as a Cloud Service non è destinato a essere utilizzato con un numero eccessivo di proprietà con più valori (MVP). Una regola generale consiste nel mantenere gli MVP al di sotto dei 1000. Tuttavia, le prestazioni effettive dipendono da molti fattori.

Gli avvisi vengono registrati per impostazione predefinita dopo aver superato 1000. Sono simili ai seguenti.

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

Le MVP di grandi dimensioni possono causare errori a causa del documento MongoDB che supera i 16 MB e causare errori simili a quelli seguenti.

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

Vedi la [Documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property) per ulteriori dettagli.

## [!DNL Assets] Linee guida per lo sviluppo e casi d’uso {#use-cases-assets}

Per informazioni sui casi di utilizzo, le raccomandazioni e i materiali di riferimento per le risorse as a Cloud Service per lo sviluppo, consulta [Riferimenti per sviluppatori per Assets.](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis)
