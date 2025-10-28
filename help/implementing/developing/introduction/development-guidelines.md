---
title: Linee guida per lo sviluppo in AEM as a Cloud Service
description: Scopri le linee guida per lo sviluppo su AEM as a Cloud Service e le principali differenze rispetto ad AEM on-premise e AEM in AMS.
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
feature: Developing
role: Admin, Architect, Developer
source-git-commit: c7ba218faac76c9f43d8adaf5b854676001344cd
workflow-type: tm+mt
source-wordcount: '2768'
ht-degree: 4%

---

# Linee guida per lo sviluppo in AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="Linee guida per lo sviluppo in AEM as a Cloud Service"
>abstract="Scopri le linee guida per lo sviluppo su AEM as a Cloud Service e le principali differenze rispetto ad AEM on-premise e AEM in AMS."
>additional-url="https://video.tv.adobe.com/v/345903?captions=ita" text="Dimostrazione della struttura del pacchetto"

Questo documento presenta le linee guida per lo sviluppo su AEM as a Cloud Service e sulle differenze importanti tra AEM on-premise e AEM in AMS.

## Il Codice Deve Essere Basato Su Cluster {#cluster-aware}

Il codice in esecuzione in AEM as a Cloud Service deve tenere presente che è sempre in esecuzione in un cluster. Ciò significa che sono sempre in esecuzione più istanze. Il codice deve essere resiliente, soprattutto in quanto un’istanza potrebbe essere arrestata in qualsiasi momento.

Durante l’aggiornamento di AEM as a Cloud Service, sono presenti istanze con codice vecchio e nuovo in esecuzione in parallelo. Pertanto, il vecchio codice non deve interrompere il contenuto creato dal nuovo codice e il nuovo codice deve essere in grado di gestire il contenuto precedente.

Se è necessario identificare l’elemento primario nel cluster, è possibile utilizzare l’API di individuazione Apache Sling per rilevarlo.

## Stato in memoria {#state-in-memory}

Lo stato non deve essere mantenuto in memoria, ma deve essere mantenuto nell’archivio. In caso contrario, questo stato potrebbe andare perduto se un’istanza viene arrestata.

## Stato nel file system {#state-on-the-filesystem}

Non utilizzare il file system dell’istanza in AEM as a Cloud Service. Il disco è temporaneo e viene eliminato quando le istanze vengono riciclate. È possibile un uso limitato del file system per la memorizzazione temporanea in relazione al trattamento di singole richieste, ma non dovrebbe essere utilizzato impropriamente per file di grandi dimensioni. Questo perché potrebbe avere un impatto negativo sulla quota di utilizzo delle risorse ed essere soggetto a limitazioni del disco.

Ad esempio, se l’utilizzo del file system non è supportato, il livello di pubblicazione deve garantire che tutti i dati che devono essere mantenuti vengano inviati a un servizio esterno per lo storage a lungo termine.

## Osservazione {#observation}

Allo stesso modo, con tutto ciò che accade in modo asincrono, come agire su eventi di osservazione, non si può garantire che venga eseguito localmente e quindi deve essere utilizzato con cautela. Questo vale sia per gli eventi JCR che per gli eventi della risorsa Sling. Nel momento in cui si verifica una modifica, l’istanza può essere rimossa e sostituita da un’istanza diversa. Altre istanze della topologia attive in quel momento sono in grado di reagire a quell&#39;evento. In questo caso, tuttavia, non si tratterà di un evento locale e potrebbe addirittura non esserci un leader attivo nel caso in cui, al momento dell&#39;evento, si proceda alle elezioni per il leader.

## Attività in background e processi con esecuzione prolungata {#background-tasks-and-long-running-jobs}

Il codice eseguito come attività in background deve presupporre che l’istanza in cui viene eseguito possa essere disattivata in qualsiasi momento. Pertanto, il codice deve essere resiliente e, soprattutto, ripristinabile. Ciò significa che se il codice viene rieseguito, non dovrebbe iniziare di nuovo dall’inizio, ma piuttosto vicino al punto in cui è stato interrotto. Anche se questo non è un nuovo requisito per questo tipo di codice, in AEM as a Cloud Service è più probabile che si verifichi un’eliminazione dell’istanza.

Per ridurre al minimo il problema, è necessario evitare processi con tempi di esecuzione lunghi, se possibile, e riprenderli al minimo. Per eseguire tali processi, utilizza Sling Jobs, che dispongono di una garanzia almeno una volta e quindi, se vengono interrotti, verranno rieseguiti il prima possibile. Ma probabilmente non dovrebbero ricominciare dall&#39;inizio. Per la pianificazione di tali processi, è consigliabile utilizzare la pianificazione [Processi Sling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing), in quanto garantisce l&#39;esecuzione almeno una volta.

Non utilizzare Sling Commons Scheduler per la pianificazione, in quanto l’esecuzione non può essere garantita. È solo più probabile che sia programmato.

Allo stesso modo, con tutto ciò che accade in modo asincrono, come agire su eventi di osservazione (che si tratti di eventi JCR o di eventi di risorse Sling), non può essere garantito che venga eseguito e pertanto deve essere utilizzato con cautela. Questo vale già per le distribuzioni AEM nel presente.

## Connessioni HTTP in uscita {#outgoing-http-connections}

Si consiglia vivamente che tutte le connessioni HTTP in uscita impostino timeout ragionevoli di connessione e lettura; i valori suggeriti sono 1 secondo per il timeout di connessione e 5 secondi per il timeout di lettura. I numeri esatti devono essere determinati in base alle prestazioni del sistema back-end che gestisce queste richieste.

Per il codice che non applica questi timeout, le istanze di AEM in esecuzione su AEM as a Cloud Service applicheranno un timeout globale. Questi valori di timeout sono di 10 secondi per le chiamate di connessione e di 60 secondi per le chiamate di lettura per le connessioni.

Adobe consiglia di utilizzare la [libreria Apache HttpComponents Client 4.x](https://hc.apache.org/httpcomponents-client-ga/) fornita per effettuare connessioni HTTP.

Le alternative che sono note per funzionare, ma che possono richiedere di fornire personalmente la dipendenza sono:

* [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) e/o [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (fornito da AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (non consigliato in quanto obsoleto e sostituito dalla versione 4.x)
* [OK Http](https://square.github.io/okhttp/) (non fornito da AEM)

Oltre a fornire timeout, è necessario anche gestire correttamente tali timeout e inserire codici di stato HTTP imprevisti.

## Gestione dei limiti di velocità delle richieste {#rate-limit-handling}

Quando la frequenza delle richieste in arrivo ad AEM supera i livelli integri, AEM risponde alle nuove richieste con il codice di errore HTTP 429. Le applicazioni che effettuano chiamate programmatiche ad AEM possono considerare di codificare in modo difensivo, riprovando dopo alcuni secondi con una strategia di backoff esponenziale. Prima di metà agosto 2023, AEM ha risposto alla stessa condizione con il codice di errore HTTP 503.

## Nessuna personalizzazione interfaccia classica {#no-classic-ui-customizations}

AEM as a Cloud Service supporta solo l’interfaccia utente touch per il codice cliente di terze parti. L’interfaccia classica non è disponibile per la personalizzazione.

## Nessuna libreria nativa o binaria nativa {#avoid-native-binaries}

Le librerie e i file binari nativi non devono essere distribuiti o installati in ambienti cloud.

Inoltre, il codice non deve tentare di scaricare binari nativi o estensioni Java native (ad esempio, JNI) in fase di esecuzione.

## Nessun file binario di streaming tramite AEM as a Cloud Service {#no-streaming-binaries}

I dati binari sono accessibili tramite la rete CDN, che distribuirà i dati binari al di fuori dei servizi AEM di base.

Non utilizzare, ad esempio, `asset.getOriginal().getStream()`, che attiva il download di un binario nel disco temporaneo del servizio AEM.

## Nessun agente di replica inversa {#no-reverse-replication-agents}

La replica inversa da Pubblica ad Autore non è supportata in AEM as a Cloud Service. Se tale strategia è necessaria, puoi utilizzare un archivio di persistenza esterno condiviso tra la farm delle istanze Publish e potenzialmente il cluster Author.

## È possibile che gli agenti di replica di inoltro debbano essere trasferiti {#forward-replication-agents}

Il contenuto viene replicato dall’istanza di authoring a quella di pubblicazione tramite un meccanismo pub-sub. Gli agenti di replica personalizzati non sono supportati.

## Nessun overload degli ambienti di sviluppo {#overloading-dev-envs}

Gli ambienti di produzione sono dimensionati più in alto per garantire un funzionamento stabile, mentre gli ambienti di staging sono dimensionati come gli ambienti di produzione per garantire test realistici in condizioni di produzione.

Gli ambienti di sviluppo e gli ambienti di sviluppo rapido devono essere limitati allo sviluppo, all’analisi degli errori e ai test funzionali e non devono essere progettati per elaborare carichi di lavoro elevati né grandi quantità di contenuti.

Ad esempio, la modifica della definizione di un indice in un archivio di contenuti di grandi dimensioni in un ambiente di sviluppo può causare la reindicizzazione, con conseguente elaborazione eccessiva. I test che richiedono contenuti sostanziali devono essere eseguiti in ambienti di staging.

## Monitoraggio e debug {#monitoring-and-debugging}

### Registri {#logs}

Per lo sviluppo locale, le voci di registro vengono scritte nei file locali nella cartella `/crx-quickstart/logs`.

Negli ambienti Cloud, gli sviluppatori possono scaricare i registri tramite Cloud Manager o utilizzare uno strumento da riga di comando per visualizzare i registri. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it) for more details. Custom logs are not supported and so all logs should be output to the error log. -->

**Impostazione del livello di registro**

Per modificare i livelli di registro per gli ambienti Cloud, è necessario modificare la configurazione OSGI Sling Logging, seguita da una ridistribuzione completa. Poiché non è istantaneo, presta attenzione all’abilitazione di registri dettagliati sugli ambienti di produzione che ricevono molto traffico. In futuro, è possibile che esistano meccanismi per modificare più rapidamente il livello del registro.

>[!NOTE]
>
>Per eseguire le modifiche di configurazione elencate di seguito, creale in un ambiente di sviluppo locale e quindi inviale a un’istanza di AEM as a Cloud Service. Per ulteriori informazioni su come eseguire questa operazione, vedere [Distribuzione in AEM as a Cloud Service](/help/implementing/deploying/overview.md).

**Attivazione del livello di registro DEBUG**

Il livello di registro predefinito è INFO, ovvero i messaggi DEBUG non vengono registrati. Per attivare il livello di registro DEBUG, aggiorna la seguente proprietà in modalità di debug.

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

Ad esempio, impostare `/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` con il seguente valore.

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

Non lasciare il registro a livello di registro DEBUG più a lungo del necessario, in quanto questo genera un numero elevato di voci.

È possibile impostare livelli di registro discreti per i diversi ambienti AEM utilizzando il targeting di configurazione OSGi basato sulla modalità di esecuzione, se è consigliabile registrare sempre a `DEBUG` durante lo sviluppo. Ad esempio:

| Ambiente | Percorso di configurazione OSGi per modalità di esecuzione | Valore proprietà `org.apache.sling.commons.log.level` |
| - | - | - |
| Sviluppo | /apps/example/config/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | DEBUG |
| Fase | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | AVVISO |
| Produzione | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | ERRORE  |

Una riga nel file di debug in genere inizia con DEBUG e quindi fornisce il livello di registro, l&#39;azione del programma di installazione e il messaggio di registro. Ad esempio:

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

I livelli del registro sono i seguenti:

| 0 | Errore irreversibile | Azione non riuscita. Impossibile continuare l&#39;installazione. |
|---|---|---|
| 1 | Errore | Azione non riuscita. L&#39;installazione procede, ma una parte di CRX non è stata installata correttamente e non funzionerà. |
| 2 | Avvertenza | L&#39;azione è stata completata ma si sono verificati problemi. CRX potrebbe funzionare correttamente o meno. |
| 3 | Informazioni | Azione completata. |

### Immagini thread {#thread-dumps}

Le immagini thread negli ambienti Cloud vengono raccolte su base continuativa, ma al momento non possono essere scaricate in modo autonomo. Nel frattempo, se sono necessarie immagini thread per il debug di un problema, contatta il supporto AEM e specifica la finestra di ora esatta.

## CRX/DE Lite e AEM as a Cloud Service Developer Console {#crxde-lite-and-developer-console}

### Sviluppo locale {#local-development}

Per lo sviluppo locale, gli sviluppatori hanno accesso completo a CRXDE Lite (`/crx/de`) e alla console Web di AEM (`/system/console`).

Nello sviluppo locale (utilizzando SDK), è possibile scrivere direttamente in `/apps` e `/libs`, che è diverso dagli ambienti Cloud, in cui le cartelle di primo livello non sono modificabili.

### Strumenti di sviluppo in AEM as a Cloud Service {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>Il Developer Console di AEM as a Cloud Service non deve essere confuso con il nome simile [*Adobe Developer Console*](https://developer.adobe.com/developer-console/).
>

>[!NOTE]
>Alcuni clienti avranno la possibilità di provare un’esperienza rinnovata per AEM Cloud Service Developer Console. Per ulteriori informazioni, consulta [questo articolo](/help/implementing/developing/introduction/aem-developer-console.md).

I clienti possono accedere a CRXDE lite nell’ambiente di sviluppo del livello di authoring, ma non in quello di stage o produzione. Impossibile scrivere nell&#39;archivio immutabile (`/libs`, `/apps`) in fase di esecuzione. Se si tenta di eseguire questa operazione, verranno generati errori.

È invece possibile avviare il Browser dell’archivio da AEM as a Cloud Service Developer Console, fornendo una vista in sola lettura nell’archivio per tutti gli ambienti sui livelli di authoring, pubblicazione e anteprima. Per ulteriori informazioni, vedere [Browser repository](/help/implementing/developing/tools/repository-browser.md).

In AEM as a Cloud Service Developer Console è disponibile un set di strumenti per il debug degli ambienti di sviluppo AEM as a Cloud Service per ambienti RDE, di sviluppo, di staging e di produzione. L’URL può essere determinato regolando gli URL del servizio Author o Publish come segue:

`https://dev-console-<namespace>.<cluster>.dev.adobeaemcloud.com`

Per avviare AEM as a Cloud Service Developer Console in base a un parametro di ambiente descritto di seguito, è possibile utilizzare il seguente comando CLI di Cloud Manager:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Per ulteriori informazioni, vedere [Informazioni sulla versione](/help/release-notes/home.md).

Gli sviluppatori possono generare informazioni sullo stato e risolvere varie risorse.

Come illustrato di seguito, le informazioni sugli stati disponibili includono lo stato di bundle, componenti, configurazioni OSGI, indici Oak, servizi OSGI e processi Sling.

![Console sviluppo 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Come illustrato di seguito, gli sviluppatori possono risolvere le dipendenze dei pacchetti e i servlet:

![Console sviluppo 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Console sviluppo 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Utile anche per il debug, AEM as a Cloud Service Developer Console dispone di un collegamento allo strumento Explain Query:

![Console sviluppo 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Per i programmi di produzione, l’accesso a AEM as a Cloud Service Developer Console è definito dal &quot;Cloud Manager - Ruolo Sviluppatore&quot; in Adobe Admin Console, mentre per i programmi sandbox, AEM as a Cloud Service Developer Console è disponibile per qualsiasi utente con un profilo di prodotto che gli consente di accedere a AEM as a Cloud Service. Per tutti i programmi, è necessario &quot;Cloud Manager - Ruolo sviluppatore&quot; per le immagini di stato e il browser dell’archivio e gli utenti devono essere definiti anche nel profilo di prodotto Utenti AEM o Amministratori AEM sui servizi di authoring e pubblicazione per visualizzare i dati di entrambi i servizi. Per ulteriori informazioni sulla configurazione delle autorizzazioni utente, vedere [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=it).

### Monitoraggio delle prestazioni {#performance-monitoring}

Adobe monitora le prestazioni delle applicazioni e adotta misure per affrontare eventuali deterioramenti. Al momento, non è possibile osservare le metriche delle applicazioni.

## Inviare e-mail {#sending-email}

Le sezioni seguenti descrivono come richiedere, configurare e inviare e-mail.

>[!NOTE]
>
>Il servizio di posta può essere configurato con il supporto OAuth2. Per ulteriori informazioni, vedere [Supporto OAuth2 per il servizio di posta](/help/security/oauth2-support-for-mail-service.md).

### Abilitazione dell’e-mail in uscita {#enabling-outbound-email}

Per impostazione predefinita, le porte utilizzate per l’invio delle e-mail sono disabilitate. Per attivare una porta, configurare [rete avanzata](/help/security/configuring-advanced-networking.md), assicurandosi di impostare per ogni ambiente necessario le regole di port forwarding dell&#39;endpoint `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`, che mappa la porta prevista (ad esempio, 465 o 587) su una porta proxy.

Si consiglia di configurare la rete avanzata con un parametro `kind` impostato su `flexiblePortEgress`, in quanto Adobe può ottimizzare le prestazioni del traffico in uscita dalla porta flessibile. Se è necessario un indirizzo IP in uscita univoco, scegliere un parametro `kind` di `dedicatedEgressIp`. Se hai già configurato la VPN per altri motivi, puoi utilizzare anche l’indirizzo IP univoco fornito dalla variante di rete avanzata.

È necessario inviare un messaggio e-mail tramite un server di posta anziché direttamente ai client di posta elettronica. In caso contrario, le e-mail potrebbero essere bloccate.

### Invio di e-mail {#sending-emails}

Utilizzare il servizio OSGI [&#x200B; del servizio di posta elettronica CQ &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=it#configuring-the-mail-service) Day e inviare le e-mail al server di posta indicato nella richiesta di supporto anziché direttamente ai destinatari.

### Configurazione {#email-configuration}

Le e-mail in AEM devono essere inviate utilizzando il servizio OSGi del servizio di posta CQ [Day](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=it#configuring-the-mail-service).

Per informazioni dettagliate sulla configurazione delle impostazioni e-mail, consulta la [documentazione di AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=it). Per AEM as a Cloud Service, prendere nota delle seguenti modifiche necessarie al servizio `com.day.cq.mailer.DefaultMailService OSGI`:

* Il nome host del server SMTP deve essere impostato su $[env:AEM_PROXY_HOST;default=proxy.tunnel]
* La porta del server SMTP deve essere impostata sul valore della porta proxy originale impostata nel parametro portForwards utilizzato nella chiamata API durante la configurazione della rete avanzata. Ad esempio, 30465 (anziché 465)

La porta del server SMTP deve essere impostata come valore `portDest` impostato nel parametro portForwards utilizzato nella chiamata API durante la configurazione della rete avanzata e il valore `portOrig` deve essere un valore significativo compreso nell&#39;intervallo richiesto 30000 - 30999. Ad esempio, se la porta del server SMTP è 465, la porta 30465 deve essere utilizzata come valore `portOrig`.

In questo caso, supponendo che SSL debba essere abilitato, nella configurazione del servizio OSGI **del servizio di posta CQ** Day :

* Imposta `smtp.port` su `30465`
* Imposta `smtp.ssl` su `true`

In alternativa, se la porta di destinazione è 587, è necessario utilizzare un valore `portOrig` di 30587. E supponendo che SSL sia disabilitato, la configurazione del servizio OSGI Day CQ Mail Service:

* Imposta `smtp.port` su `30587`
* Imposta `smtp.ssl` su `false`

La proprietà `smtp.starttls` verrà impostata automaticamente da AEM as a Cloud Service in fase di esecuzione su un valore appropriato. Pertanto, se `smtp.ssl` è impostato su true, `smtp.startls` viene ignorato. Se `smtp.ssl` è impostato su false, `smtp.starttls` è impostato su true. Indipendentemente dai valori `smtp.starttls` impostati nella configurazione OSGI.


Il servizio di posta può essere configurato facoltativamente con il supporto OAuth2. Per ulteriori informazioni, vedere [Supporto OAuth2 per il servizio di posta](/help/security/oauth2-support-for-mail-service.md).

### Configurazione e-mail legacy {#legacy-email-configuration}

Prima della versione 2021.9.0, l’e-mail era configurata tramite una richiesta di assistenza clienti. Prendere nota delle seguenti modifiche necessarie al servizio `com.day.cq.mailer.DefaultMailService OSGI`:

AEM as a Cloud Service richiede che la posta venga inviata tramite la porta 465. Se un server di posta non supporta la porta 465, è possibile utilizzare la porta 587 purché sia abilitata l’opzione TLS.

Se è stata richiesta la porta 465:

* imposta `smtp.port` su `465`
* imposta `smtp.ssl` su `true`

e se è stata richiesta la porta 587:

* imposta `smtp.port` su `587`
* imposta `smtp.ssl` su `false`

La proprietà `smtp.starttls` verrà impostata automaticamente da AEM as a Cloud Service in fase di esecuzione su un valore appropriato. Pertanto, se `smtp.ssl` è impostato su true, `smtp.startls` viene ignorato. Se `smtp.ssl` è impostato su false, `smtp.starttls` è impostato su true. Indipendentemente dai valori `smtp.starttls` impostati nella configurazione OSGI.

L&#39;host del server SMTP deve essere impostato su quello del server di posta.

## Evita Proprietà Con Più Valori Di Grandi Dimensioni {#avoid-large-mvps}

L’archivio dei contenuti Oak sottostante ad AEM as a Cloud Service non deve essere utilizzato con un numero eccessivo di proprietà con più valori (MVP). Una regola empirica è mantenere gli MVP al di sotto di 1000. Tuttavia, le prestazioni effettive dipendono da molti fattori.

Gli avvisi vengono registrati per impostazione predefinita dopo il superamento di 1000. Sono simili alle seguenti.

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

Gli MVP di grandi dimensioni possono causare errori dovuti al fatto che il documento MongoDB supera i 16 MB, con conseguente errore simile al seguente.

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

Per ulteriori dettagli, consulta la [documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property).

## [!DNL Assets] linee guida per lo sviluppo e casi d&#39;uso {#use-cases-assets}

Per informazioni sui casi d&#39;uso per lo sviluppo, le raccomandazioni e il materiale di riferimento per Assets as a Cloud Service, consulta [Riferimenti per sviluppatori per Assets](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
