---
title: AEM come linee guida per lo sviluppo dei servizi cloud
description: 'Da completare '
translation-type: tm+mt
source-git-commit: cedc14b0d71431988238d6cb4256936a5ceb759b

---


# AEM come linee guida per lo sviluppo dei servizi cloud {#aem-as-a-cloud-service-development-guidelines}

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
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (non consigliato in quanto obsoleto e sostituito dalla versione 4.x)
* [OK Http](OK Http (Non fornito da AEM)) (Non fornito da AEM)

## Monitoraggio e debug {#monitoring-and-debugging}

### Registri {#logs}

* Per lo sviluppo locale, le voci di registro sono scritte in file locali
   * `./crx-quickstart/logs`
* Negli ambienti Cloud, gli sviluppatori possono scaricare i registri tramite Cloud Manager o utilizzare uno strumento della riga di comando per localizzare i registri. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->
* Per modificare i livelli di registro per gli ambienti Cloud, la configurazione Sling Logging OSGI deve essere modificata, seguita da una ridistribuzione completa. Poiché non è istantaneo, essere cauti nell&#39;attivare log verbosi in ambienti di produzione che ricevono molto traffico. In futuro, è possibile che ci saranno meccanismi per cambiare più rapidamente il livello di registro.

### Cassetti di thread {#thread-dumps}

Le discariche di thread negli ambienti Cloud vengono raccolte in modo continuativo, ma al momento non possono essere scaricate in modo autonomo. Nel frattempo, contattate il supporto di AEM se sono necessari dei thread dumps per il debug di un problema, specificando la finestra temporale esatta.

### Console di sistema CRX/DE Lite {#crxde-lite-and-system-console}

## Sviluppo locale {#local-development}

Per lo sviluppo locale, gli sviluppatori possono accedere completamente a CRXDE Lite (`/crx/de`) e alla console Web di AEM (`/system/console`).

Sullo sviluppo locale (tramite l&#39;avvio rapido per il cloud) `/apps` e `/libs` può essere scritto direttamente, il che è diverso dagli ambienti Cloud in cui tali cartelle di livello superiore sono immutabili.

## AEM come strumenti di sviluppo dei servizi cloud {#aem-as-a-cloud-service-development-tools}

I clienti possono accedere a CRXDE lite nell&#39;ambiente di sviluppo, ma non sullo stage o sulla produzione. L&#39;archivio immutabile (`/libs`, `/apps`) non può essere scritto in fase di esecuzione, pertanto il tentativo di eseguire tale operazione potrebbe causare errori.

Una serie di strumenti per il debug di AEM come ambienti per sviluppatori di servizi cloud sono disponibili in Developer Console per gli ambienti di sviluppo, fase e produzione. Per determinare l’URL, regolate gli URL del servizio di creazione e pubblicazione nel modo seguente:

`https://dev-console>-<namespace>.<cluster>.dev.adobeaemcloud.com`

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

**Servizio di gestione e produzione AEM**

I clienti non avranno accesso agli strumenti di sviluppo per gli ambienti di produzione e di staging.

### Diagnostica {#diagnostics}

La console di sistema è disponibile per gli ambienti di sviluppo. Tuttavia, non sono disponibili discariche diagnostiche per la fase di produzione e la fase di produzione.