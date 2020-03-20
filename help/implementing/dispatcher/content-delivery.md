---
title: Distribuzione dei contenuti
description: 'Distribuzione dei contenuti '
translation-type: tm+mt
source-git-commit: d1c953e1caf440f18e488f07a32bcf5bc3880f67

---


# Distribuzione dei contenuti in AEM come servizio cloud {#content-delivery}

La distribuzione dei contenuti del servizio di pubblicazione include:

* CDN (in genere gestito da Adobe)
* dispatcher AEM
* Pubblicazione AEM

Il flusso di dati è il seguente:

1. L’URL viene aggiunto nel browser
1. Richiesta effettuata alla CDN mappata in DNS a tale dominio
1. Se il contenuto è completamente memorizzato nella cache su CDN, CDN lo trasmette al browser
1. Se il contenuto non è completamente memorizzato nella cache, la rete CDN richiama (proxy inverso) al dispatcher
1. Se il contenuto è completamente memorizzato nella cache del dispatcher, il dispatcher lo invia alla CDN
1. Se il contenuto non è completamente memorizzato nella cache, il dispatcher richiama (proxy inverso) alla pubblicazione AEM
1. Il contenuto viene rappresentato dal browser, che potrebbe anche memorizzarlo nella cache, a seconda delle intestazioni

Il tipo di contenuto HTML/testo viene impostato per scadere dopo 300 (5 minuti) al livello dispatcher, una soglia che viene rispettata sia dalla cache dispatcher che dalla CDN. Durante le ridistribuzioni del servizio di pubblicazione, la cache del dispatcher viene svuotata e successivamente riscaldata prima che i nuovi nodi di pubblicazione accettino il traffico.

Le sezioni seguenti forniscono maggiori dettagli sulla distribuzione dei contenuti, inclusa la configurazione CDN e il caching del dispatcher.

Le informazioni sulla replica dal servizio di creazione al servizio di pubblicazione sono disponibili [qui](/help/operations/replication.md).

>[!NOTE]
>Il traffico passa attraverso un server Web Apache, che supporta moduli incluso il dispatcher. Il dispatcher viene utilizzato principalmente come cache per limitare l’elaborazione sui nodi di pubblicazione al fine di migliorare le prestazioni.

## CDN {#cdn}

AEM offre tre opzioni:

1. CDN gestito da Adobe - CDN out-of-the-box di AEM. Questa è l&#39;opzione consigliata perché è completamente integrata.
1. La CDN del cliente punta alla CDN gestita di Adobe - il cliente punta il proprio CDN alla CDN out-of-the-box di AEM. Se la prima opzione non è disponibile, questa è l’opzione preferita successiva, in quanto sfrutta ancora l’integrazione di AEM con il suo CDN predefinito. I clienti continueranno a essere responsabili della gestione della propria rete CDN.
1. CDN gestito dal cliente - Il cliente porta la propria CDN ed è interamente responsabile della gestione.

>[!CAUTION]
>La prima opzione è altamente consigliata. Se scegliete la seconda opzione, Adobe non può essere ritenuta responsabile del risultato di eventuali configurazioni errate.

La seconda e la terza opzione sono consentite caso per caso. Ciò comporta l&#39;adempimento di alcuni prerequisiti, tra cui, a titolo esemplificativo, l&#39;integrazione con il fornitore CDN di un cliente precedente, difficilmente annullabile.

### CDN gestito da Adobe {#adobe-managed-cdn}

La preparazione per la distribuzione dei contenuti tramite la rete CDN di Adobe è semplice, come descritto di seguito:

1. Fornirai ad Adobe il certificato SSL firmato e la chiave segreta condividendo un collegamento a un modulo protetto contenente tali informazioni. Coordinare con l&#39;assistenza clienti su questa attività.
Nota: Aem come servizio Cloud non supporta i certificati convalidati (DV) del dominio.
1. Il supporto clienti quindi coordinerà con voi i tempi di un record DNS CNAME, indicando il loro FQDN `adobe-aem.map.fastly.net`.
1. Al momento della scadenza dei certificati SSL riceverete una notifica per consentirvi di inviare nuovamente i nuovi certificati SSL.

Per impostazione predefinita, per una configurazione CDN gestita da Adobe, tutto il traffico pubblico può essere indirizzato al servizio di pubblicazione, sia per gli ambienti di produzione che per quelli non di produzione (sviluppo e fase). Se desiderate limitare il traffico al servizio di pubblicazione per un determinato ambiente (ad esempio, limitando l’area di gestione temporanea per un intervallo di indirizzi IP), per configurare tali restrizioni dovete rivolgervi all’assistenza clienti.

### CDN cliente punta ad Adobe Managed CDN {#point-to-point-CDN}

Supportato se desiderate utilizzare il vostro CDN esistente, ma non potete soddisfare i requisiti di un CDN gestito dal cliente. In questo caso, gestite la vostra rete CDN, ma indicate la rete CDN gestita da Adobe.

Attenzione:

1. È necessario disporre di un CDN esistente.
1. Lo gestirà.
1. Devi essere in grado di configurare CDN per lavorare con Aem come servizio cloud. Consulta le istruzioni di configurazione riportate di seguito.
1. Gli esperti CDN tecnici sono in servizio in caso di problemi correlati.
1. È necessario eseguire e superare con successo un test di carico prima di passare alla produzione.

Istruzioni di configurazione:

1. Impostate l’ `X-Forwarded-Host` intestazione con il nome del dominio.
1. Impostate l&#39;intestazione Host con il dominio di origine, che è l&#39;ingresso CDN di Adobe. Il valore deve provenire da Adobe.
1. Inviate l’intestazione SNI all’origine. Come l&#39;intestazione Host, l&#39;intestazione sni deve essere il dominio di origine.
1. Impostate il `X-Edge-Key`, necessario per indirizzare correttamente il traffico ai server AEM. Il valore deve provenire da Adobe.

### CDN gestito cliente {#customer-managed-cdn}

Supportata se è necessario utilizzare la rete CDN esistente.  In questo caso, gestisci la tua CDN, indicandola ad AEM.

Puoi gestire la tua CDN, a condizione:

1. Esiste una CDN.
1. Deve essere un CDN supportato. Al momento, Akamai è supportato. Se l’organizzazione desidera gestire una rete CDN non supportata, rivolgetevi all’assistenza clienti.
1. Lo gestirà.
1. Devi essere in grado di configurare CDN per lavorare con Aem come servizio cloud. Consulta le istruzioni di configurazione riportate di seguito.
1. Gli esperti CDN tecnici sono in servizio in caso di problemi correlati.
1. Devi fornire whitelist di nodi CDN a Cloud Manager, come descritto nelle istruzioni di configurazione.
1. È necessario eseguire e superare con successo un test di carico prima di passare alla produzione.

Istruzioni di configurazione:

1. Fornite ad Adobe la whitelist del fornitore CDN chiamando l&#39;API di creazione/aggiornamento dell&#39;ambiente con un elenco di CIDR da inserire nella whitelist.
1. Impostate l’ `X-Forwarded-Host` intestazione con il nome del dominio.
1. Impostate l&#39;intestazione Host con il dominio di origine, che è l&#39;Aem come ingresso del servizio Cloud. Il valore deve provenire da Adobe.
1. Inviate l’intestazione SNI all’origine. L’intestazione SNI deve essere il dominio di origine.
1. Imposta `X-Edge-Key` ciò che è necessario per indirizzare correttamente il traffico ai server AEM. Il valore deve provenire da Adobe.

Prima di accettare il traffico live, è necessario verificare con l&#39;assistenza clienti Adobe che il ciclo di traffico end-to-end funziona correttamente.

### Caching {#caching}

Il processo di caching segue le regole presentate di seguito.

### HTML/Testo {#html-text}

* per impostazione predefinita, è memorizzata nella cache dal browser per 5 minuti, in base all’intestazione del controllo cache emesso dal livello apache. Anche la CDN rispetta questo valore.
* può essere ignorato per tutto il contenuto HTML/Testo definendo la `EXPIRATION_TIME` variabile in `global.vars` AEM come strumenti Dispatcher SDK di Servizi cloud.

È necessario assicurarsi che un file con `src/conf.dispatcher.d/cache` la regola seguente:

```
/0000
{ /glob "*" /type "allow" }
```

* possono essere sostituiti a un livello di granulosità più sottile dalle direttive apache mod_header. Esempio:

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200 s-maxage=200"
</LocationMatch>
```

È necessario assicurarsi che un file con `src/conf.dispatcher.d/cache` la regola seguente:

```
/0000
{ /glob "*" /type "allow" }
```

* Altri metodi, incluso il progetto [AEM ACS](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)dispatcher-ttl, non sostituiranno correttamente i valori.

### Librerie lato client (js, css) {#client-side-libraries}

* utilizzando il framework di libreria lato client di AEM, il codice JavaScript e CSS viene generato in modo tale che i browser possano memorizzarlo nella cache in modo indefinito, dal momento che qualsiasi modifica si verifica come nuovi file con un percorso univoco.  In altre parole, il codice HTML che fa riferimento alle librerie client verrà prodotto come necessario, in modo che i clienti possano provare nuovi contenuti mentre vengono pubblicati. Il controllo della cache è impostato su &quot;immutabile&quot; o su 30 giorni per i browser meno recenti che non rispettano il valore &quot;immutabile&quot;.
* per ulteriori dettagli, consultate la sezione [Librerie lato client e coerenza](#content-consistency) delle versioni.

### Immagini {#images}

* non memorizzato nella cache

### Altri tipi di contenuto {#other-content}

* nessuna cache predefinita
* può essere scavalcato da un dolore `mod_headers`. Esempio:

```
<LocationMatch "\.(css|js)$">
    Header set Cache-Control "max-age=500 s-maxage=500"
</LocationMatch>
```

*Anche altri metodi di impostazione delle intestazioni della cache possono funzionare

Prima di accettare il traffico live, i clienti devono verificare con il supporto clienti Adobe che il ciclo di traffico end-to-end funziona correttamente.

## Dispatcher {#disp}

Il traffico passa attraverso un server Web Apache, che supporta moduli incluso il dispatcher. Il dispatcher viene utilizzato principalmente come cache per limitare l’elaborazione sui nodi di pubblicazione al fine di migliorare le prestazioni.

Il contenuto di tipo HTML/testo è impostato con intestazioni della cache corrispondenti a una scadenza di 300 (5 minuti).

Il resto di questa sezione descrive considerazioni relative all&#39;annullamento della validità della cache del dispatcher.

### Annullamento della validità della cache del dispatcher durante l&#39;attivazione/disattivazione {#cache-activation-deactivation}

Come nelle versioni precedenti di AEM, la pubblicazione o l’annullamento della pubblicazione di pagine eliminerà il contenuto dalla cache del dispatcher. Se si sospetta un problema di caching, i clienti devono ripubblicare le pagine in questione.

Quando l’istanza di pubblicazione riceve una nuova versione di una pagina o di una risorsa dall’autore, utilizza l’agente di eliminazione per annullare i percorsi appropriati nel dispatcher. Il percorso aggiornato viene rimosso dalla cache del dispatcher, insieme ai relativi elementi principali, fino a un livello (è possibile configurarlo con [statfileslevel](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

### Annullamento della validità della cache del dispatcher esplicito {#explicit-invalidation}

In generale, non sarà necessario annullare manualmente il contenuto nel dispatcher, ma è possibile, se necessario, come descritto di seguito.

Prima di AEM come servizio cloud, erano disponibili due modi per annullare la validità della cache del dispatcher.

1. Richiamate l&#39;agente di replica, specificando l&#39;agente di eliminazione del dispatcher di pubblicazione
2. Chiamata diretta dell&#39; `invalidate.cache` API (ad esempio, `POST /dispatcher/invalidate.cache`)

L&#39; `invalidate.cache` approccio non sarà più supportato, in quanto riguarda solo un nodo dispatcher specifico.
Poiché AEM come servizio cloud opera a livello di servizio, non a livello di singolo nodo, le istruzioni di annullamento della validità contenute nella pagina [Invalidazione delle pagine cache da AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) non sono valide per AEM come servizio cloud.
Utilizzare invece l&#39;agente di flush di replica. Questa operazione può essere eseguita utilizzando l&#39;API Replication. La documentazione API di replica è disponibile [qui](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) e per un esempio di svuotamento della cache, consultate la pagina [di esempio](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) API, in particolare l&#39; `CustomStep` esempio che emette un&#39;azione di replica di tipo ACTIVATE a tutti gli agenti disponibili. L&#39;endpoint dell&#39;agente di flush non è configurabile ma preconfigurato per puntare al dispatcher, associato al servizio di pubblicazione che esegue l&#39;agente di flush. L&#39;agente di flush può in genere essere attivato da eventi OSGi o flussi di lavoro.

Il diagramma seguente illustra questo.

![](assets/cdnc.png "CDNCDN")

In caso di problemi di cancellazione della cache del dispatcher, contattare l’assistenza clienti che, se necessario, può cancellare la cache del dispatcher.

La rete CDN gestita da Adobe rispetta i TTL e non è quindi necessario scaricarla. Se si sospetta un problema, contattate l’assistenza clienti che potrà cancellare una cache CDN gestita da Adobe in base alle esigenze.

## Librerie lato client e coerenza delle versioni {#content-consistency}

Naturalmente le pagine sono costituite da HTML, JavaScript, CSS e immagini. I clienti sono invitati a sfruttare il framework Client-Side Libraries (clientlibs) per importare risorse Javascript e CSS in pagine HTML, tenendo conto delle dipendenze tra librerie JS.

Il framework clientlibs fornisce la gestione automatica delle versioni, consentendo agli sviluppatori di archiviare le modifiche apportate alle librerie JS nel controllo del codice sorgente e rendendo disponibile l&#39;ultima versione al momento del rilascio da parte del cliente. In caso contrario, gli sviluppatori dovrebbero modificare manualmente il codice HTML con i riferimenti alla nuova versione della libreria, il che è particolarmente costoso se molti modelli HTML condividono la stessa libreria.

Quando le nuove versioni delle librerie vengono rilasciate in produzione, le pagine HTML di riferimento vengono aggiornate con nuovi collegamenti alle versioni libreria aggiornate. Una volta scaduta la cache del browser per una determinata pagina HTML, non c&#39;è motivo di preoccuparsi che le vecchie librerie vengano caricate dalla cache del browser, dal momento che la pagina aggiornata (da AEM) ora fa riferimento alle nuove versioni delle librerie. In altre parole, una pagina HTML aggiornata includerà tutte le versioni libreria più recenti.

Il meccanismo di questo è un hash serializzato, che viene aggiunto al collegamento della libreria client, garantendo un URL univoco con le versioni affinché il browser memorizzi nella cache CSS/JS. L&#39;hash serializzato viene aggiornato solo quando il contenuto della libreria client cambia. Ciò significa che, se si verificano aggiornamenti non correlati (ovvero nessuna modifica al css/js sottostante della libreria client) anche con una nuova distribuzione, il riferimento rimane lo stesso, garantendo meno interruzioni nella cache del browser.

### Abilitazione delle versioni Longcache delle librerie lato client - AEM come servizio cloud - Avvio rapido SDK {#enabling-longcache}

clientlib predefinite in una pagina HTML sono simili a quelle dell&#39;esempio seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Quando la funzione di controllo delle versioni di clientlib rigorose è abilitata, nella libreria client viene aggiunta una chiave hash a lungo termine come selettore. Di conseguenza, il riferimento clientlib sarà simile al seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Il controllo delle versioni clientlib rigorose è abilitato per impostazione predefinita in tutti gli ambienti AEM come servizio cloud.

Per abilitare il controllo delle versioni di clientlib rigorose nell’SDK Quickstart locale, effettua le seguenti operazioni:

1. Passa a Gestione configurazione OSGi <host>/system/console/configMgr
1. Trovate il file di configurazione OSGi per Adobe Granite HTML Library Manager:
   * Selezionare la casella di controllo per abilitare il controllo delle versioni rigorose
   * Nel campo con l&#39;etichetta Chiave cache lato client a lungo termine, immettere il valore di /.*;hash
1. Salva le modifiche. Non è necessario salvare questa configurazione nel controllo del codice sorgente, in quanto AEM come servizio cloud attiverà automaticamente questa configurazione negli ambienti di sviluppo, fase e produzione.
1. Ogni volta che il contenuto della libreria client viene modificato, viene generata una nuova chiave hash e il riferimento HTML verrà aggiornato.
