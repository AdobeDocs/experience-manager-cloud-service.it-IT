---
title: Implementazione di AEM come servizio cloud
description: 'Implementazione di AEM come servizio cloud '
translation-type: tm+mt
source-git-commit: 44df22ace403c962ffbabac5eec9302d98fc94f2

---


# Implementazione di AEM come servizio cloud {#deploying-to-aem-as-a-cloud-service}

## Introduzione {#introduction}

Le basi dello sviluppo del codice sono simili in AEM come servizio cloud rispetto alle soluzioni AEM On Premise e Managed Services. Gli sviluppatori scrivono il codice e lo sottopongono a test localmente, che vengono quindi inviati a AEM remoto come ambienti di servizio cloud. Cloud Manager, uno strumento opzionale per la distribuzione dei contenuti per i servizi gestiti, è obbligatorio. Questo è ora l&#39;unico meccanismo per distribuire il codice ad AEM come ambienti di servizio cloud.

L&#39;aggiornamento della versione di AEM è sempre un evento di distribuzione separato dall&#39;invio di codice personalizzato. Visualizzate in un altro modo, le versioni di codice personalizzate devono essere testate rispetto alla versione AEM in produzione, dal momento che questo è l’elemento su cui verranno distribuite. Gli aggiornamenti delle versioni di AEM che si verificano successivamente, e che saranno frequenti se confrontati con i servizi gestiti oggi, vengono applicati automaticamente. Sono compatibili con il codice cliente già distribuito.

Il resto di questo documento descriverà come gli sviluppatori devono adattare le proprie prassi in modo che utilizzino sia AEM che gli aggiornamenti della versione di un servizio cloud, nonché gli aggiornamenti dei clienti.

>[!NOTE]
>È consigliabile che i clienti con basi di codice esistenti seguano l’esercizio di ristrutturazione del repository descritto nella documentazione [di](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)AEM.


## Aggiornamenti della versione di AEM {#version-updates}

È fondamentale comprendere che AEM verrà aggiornato frequentemente, potenzialmente anche una volta al giorno, e si concentrerà sulle correzioni di bug e sui miglioramenti delle prestazioni. L&#39;aggiornamento verrà eseguito in modo trasparente e senza causare tempi di inattività. L&#39;aggiornamento è concepito per essere compatibile con le versioni precedenti, pertanto non è necessario modificare il codice personalizzato. In realtà, gli aggiornamenti di AEM sono eventi indipendenti dalle distribuzioni del codice cliente. L’aggiornamento AEM viene implementato sopra l’ultimo push del codice con esito positivo, il che implica che tutte le modifiche apportate dall’ultimo push alla produzione non verranno distribuite.

>[!NOTE]
>
> Se il codice personalizzato è stato messo in stato di pre-produzione e successivamente rifiutato dall’utente, il successivo aggiornamento di AEM rimuoverà tali modifiche per riflettere il tag git dell’ultima release cliente riuscita in produzione.

Su una frequenza regolare, verrà rilasciata una nuova funzione che si concentrerà sulle funzioni aggiunte e migliorate che avranno un impatto maggiore sull&#39;esperienza dell&#39;utente rispetto alle versioni giornaliere. Una release di una funzione viene attivata non dalla distribuzione di un set di modifiche di grandi dimensioni, ma piuttosto dal rovesciamento di un interruttore di rilascio, attivando il codice che si è accumulato nel corso di giorni o settimane attraverso gli aggiornamenti giornalieri.

I controlli sanitari sono utilizzati per monitorare lo stato della domanda. Se questi controlli non vengono eseguiti correttamente durante un aggiornamento di AEM come servizio cloud, la release non procederà per tale ambiente e Adobe controllerà il motivo per cui l&#39;aggiornamento ha causato questo comportamento imprevisto.

### Archivio nodi composito {#composite-node-store}

Come già detto, gli aggiornamenti nella maggior parte dei casi non generano tempi di inattività, anche per l&#39;autore, che è un cluster di nodi. Gli aggiornamenti a rotolamento sono possibili grazie alla funzione &quot;composito node store&quot; in Oak. Questa funzione consente ad AEM di fare riferimento a più repository contemporaneamente. In una distribuzione continuativa, la nuova versione di AEM verde contiene un archivio immutabile `/libs` (basato su TarMK), distinto dalla versione precedente di AEM blu, anche se entrambi fanno riferimento a un archivio mutabile condiviso basato su DocumentMK che contiene aree come `/content`, `/conf`, `/etc` e altre. Poiché sia il blu che il verde hanno versioni proprie di `/libs`, possono essere entrambi attivi durante l&#39;aggiornamento continuo, assumendo entrambi il traffico fino a quando il blu non viene completamente sostituito dal verde.

## Rilasci dei clienti {#customer-releases}

### Codifica rispetto alla versione AEM corretta {#coding-against-the-right-aem-version}

Per le soluzioni AEM precedenti, la versione più recente di AEM veniva modificata raramente (all’incirca ogni anno con Service Pack trimestrali) e i clienti aggiornavano le istanze di produzione all’ultimo avvio rapido, facendo riferimento all’API Jar. Tuttavia, AEM come applicazione di servizio cloud viene aggiornato automaticamente alla versione più recente di AEM più spesso, pertanto il codice personalizzato per le versioni interne deve essere creato in base alle nuove interfacce AEM.

Come per le versioni AEM non cloud esistenti, nella maggior parte dei casi sarà supportato uno sviluppo locale offline basato su uno specifico quickstart, che sarà lo strumento preferito per il debug.

> [!NOTA}
>Esistono sottili differenze operative tra il comportamento dell&#39;applicazione su un computer locale e quello di Adobe Cloud. Queste differenze architettoniche devono essere rispettate durante lo sviluppo locale e possono portare a un comportamento diverso durante la distribuzione nell&#39;infrastruttura cloud. A causa di queste differenze è importante eseguire test esaustivi sugli ambienti di sviluppo e di stage prima di distribuire il nuovo codice personalizzato in produzione.

Di seguito è illustrata la procedura che consente a uno sviluppatore di accedere alla versione pertinente degli artifact di AEM, che verrà definita AEM come SDK per servizi cloud, necessaria per sviluppare codice personalizzato per una versione interna. Informazioni sul dispatcher sono disponibili [in questa pagina](/help/implementing/dispatcher/overview.md).

## Distribuzione di pacchetti di contenuti tramite Cloud Manager e Package Manager {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Implementazioni tramite Cloud Manager {#deployments-via-cloud-manager}

I clienti distribuiscono il codice personalizzato agli ambienti cloud tramite Cloud Manager. È opportuno notare che Cloud Manager trasforma i pacchetti di contenuto assemblati localmente in un artefatto conforme al modello di funzioni Sling, in modo che un’applicazione AEM come servizio Cloud venga descritta quando viene eseguita in un ambiente cloud. Di conseguenza, quando si esaminano i pacchetti in Package Manager negli ambienti Cloud, il nome includerà &quot;cp2fm&quot; e i pacchetti trasformati hanno tutti i metadati rimossi. Non è possibile interagire con questi elementi, né scaricarli, replicarli o aprirli. La documentazione dettagliata sul convertitore è [disponibile qui](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

I pacchetti di contenuto scritti per AEM come applicazioni di servizio cloud devono disporre di una separazione netta tra contenuti immutabili e modificabili e Cloud Manager li applicherà non riuscendo a creare, generando un messaggio come:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

Il resto di questa sezione descriverà la composizione e le implicazioni dei pacchetti immutabili e mutabili.

### Pacchetti di contenuti immutabili {#immutabe-content-packages}

Tutto il contenuto e il codice memorizzati nell’archivio immutabile devono essere sottoposti a check-in e distribuiti tramite Cloud Manager. In altre parole, a differenza delle attuali soluzioni AEM, il codice non viene mai distribuito direttamente a un’istanza AEM in esecuzione. Questo garantisce che il codice in esecuzione per una determinata release in qualsiasi ambiente Cloud sia identico, eliminando il rischio di variazioni di codice non intenzionali durante la produzione. Ad esempio, la configurazione OSGI deve essere impegnata nel controllo del codice sorgente anziché gestita in fase di esecuzione tramite il gestore di configurazione della console Web AEM.

Poiché le modifiche dell&#39;applicazione a causa del pattern di distribuzione Blu-Verde sono abilitate da uno switch, non possono dipendere dalle modifiche nell&#39;archivio modificabile, ad eccezione degli utenti del servizio, dei relativi ACL, dei tipi di nodi e delle modifiche alla definizione dell&#39;indice.

Per i clienti con basi di codice esistenti, è fondamentale seguire l’esercizio di ristrutturazione dell’archivio descritto nella documentazione di AEM per garantire che il contenuto precedente in /etc sia spostato nella posizione giusta.

## Configurazione OSGI {#osgi-configuration}

Come già detto, la configurazione OSGI deve essere impegnata nel controllo del codice sorgente anziché tramite la console Web. Le tecniche per farlo includono:

* Apportare le modifiche necessarie nell’ambiente AEM locale dello sviluppatore con il gestore di configurazione della console Web AEM, quindi esportare i risultati nel progetto AEM nel file system locale
* Creazione manuale della configurazione OSGI nel progetto AEM nel file system locale, con riferimento al gestore di configurazione della console AEM per i nomi delle proprietà.

## Contenuto variabile {#mutable-content}

In alcuni casi potrebbe essere utile preparare le modifiche al contenuto nel controllo del codice sorgente in modo che possa essere distribuito da Cloud Manager ogni volta che un ambiente viene aggiornato. Ad esempio, potrebbe essere ragionevole generare determinate strutture di cartelle principali o allineare le modifiche nei modelli modificabili per abilitare i criteri in quelli per i componenti che sono stati aggiornati dalla distribuzione dell&#39;applicazione.

Esistono due strategie per descrivere il contenuto che verrà distribuito da Cloud Manager nell&#39;archivio modificabile, i pacchetti di contenuto modificabile e le istruzioni di reindirizzamento.

### Pacchetti di contenuti variabile {#mutable-content-packages}

Contenuto come gerarchie di percorsi di cartella, utenti di servizi e controlli di accesso (ACL, Access Control) viene generalmente impegnato in un progetto AEM basato su archetipo principale. Le tecniche includono l’esportazione da AEM o la scrittura diretta come XML. Durante il processo di creazione e distribuzione, Cloud Manager crea pacchetti per il pacchetto di contenuto variabile risultante. Il contenuto modificabile viene installato in 3 momenti diversi durante la fase di distribuzione nella pipeline:

Prima dell&#39;avvio della nuova versione dell&#39;applicazione:

* definizioni di indice (aggiungere, modificare, rimuovere)

Durante l&#39;avvio di una nuova versione dell&#39;applicazione, ma prima del passaggio:

* Utenti del servizio (aggiungere)
* ACL utente servizio (add)
* tipi di nodi (add)

Dopo il passaggio alla nuova versione dell&#39;applicazione:

* Tutti gli altri contenuti definibili tramite jackrabbit vault. Esempio:
   * Cartelle (aggiungere, modificare, rimuovere)
   * Modelli modificabili (aggiungere, modificare, rimuovere)
   * Configurazione in base al contesto (qualsiasi cosa sotto `/conf`) (aggiungere, modificare, rimuovere)
   * Script (i pacchetti possono attivare i ganci di installazione a varie fasi del processo di installazione del pacchetto)

È possibile limitare l’installazione di contenuto modificabile alla creazione o alla pubblicazione incorporando pacchetti in una cartella install.author o install.publish in `/apps`. Informazioni dettagliate nella documentazione [di](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/restructuring/repository-restructuring.html) AEM sulla ristrutturazione del progetto consigliata.

>[!NOTE] I pacchetti di contenuto vengono distribuiti a tutti i tipi di ambiente (dev, stage, prod). Non è possibile limitare la distribuzione a un ambiente specifico. Tale limitazione è in vigore per garantire la possibilità di eseguire un test dell&#39;esecuzione automatica. Il contenuto specifico per un ambiente richiede l&#39;installazione manuale tramite Package Manager.

Inoltre, non esiste alcun meccanismo per ripristinare le modifiche apportate al pacchetto di contenuto modificabile dopo che sono state applicate. Se i clienti rilevano un problema, possono scegliere di risolverlo nella release successiva del codice o come ultima risorsa, ripristinare l&#39;intero sistema a un punto nel tempo prima della distribuzione.

Tutti i pacchetti di terze parti inclusi devono essere convalidati come AEM compatibile con il servizio cloud. In caso contrario, la loro inclusione causerà un errore di distribuzione.

Come già detto, i clienti con basi di codice esistenti devono conformarsi al processo di ristrutturazione del repository descritto nella documentazione [di](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)AEM.

## Repoinit {#repoinit}

Per i seguenti casi, è preferibile adottare l&#39;approccio di codificare manualmente le istruzioni per la creazione di contenuti espliciti `repoinit` nelle configurazioni di fabbrica OSGI:

* Creare/eliminare/disabilitare gli utenti del servizio
* Creare ed eliminare gruppi
* Creare ed eliminare utenti
* Aggiunta di ACL
   > [!NOTE] La definizione di ACL richiede che le strutture dei nodi siano già presenti. Pertanto, prima di creare le istruzioni percorso potrebbe essere necessario.
* Aggiungi percorso (ad esempio per le strutture di cartelle principali)
* Aggiungere CND (definizioni dei tipi di nodo)

Repoinit è preferibile per questi casi di utilizzo supportati per la modifica del contenuto a causa dei seguenti vantaggi:

* Repoinit crea risorse all&#39;avvio, in modo che la logica possa dare per scontata l&#39;esistenza di tali risorse. Nell&#39;approccio basato su pacchetti di contenuto variabile, le risorse vengono create dopo l&#39;avvio, pertanto il codice dell&#39;applicazione che si basa su di esse potrebbe non riuscire.
* Repoinit è un insieme di istruzioni relativamente sicuro in quanto si controlla esplicitamente l&#39;azione da intraprendere. Inoltre, le uniche operazioni supportate sono additivi, ad eccezione di alcuni casi relativi alla sicurezza che consentono la rimozione di Utenti, Utenti di servizi e Gruppi. Al contrario, è esplicita la rimozione di qualcosa nell&#39;approccio basato su pacchetti di contenuti variabili;  quando definite un filtro, tutti gli elementi presenti coperti da un filtro verranno eliminati. Tuttavia, è necessario prestare attenzione, in quanto con qualsiasi contenuto esistono scenari in cui la presenza di nuovo contenuto può alterare il comportamento dell&#39;applicazione.
* Repoinit esegue operazioni rapide e atomiche. I pacchetti di contenuto variabile, al contrario, possono dipendere notevolmente dalle prestazioni in base alle strutture coperte da un filtro. Anche se aggiornate un singolo nodo, potrebbe essere creata un&#39;istantanea di una struttura ad albero grande.
* È possibile convalidare le istruzioni di ripristino in un ambiente di sviluppo locale in fase di esecuzione, dal momento che verranno eseguite quando la configurazione OSGi viene registrata.
* Le istruzioni Repoinit sono atomiche ed esplicite e ignorano se lo stato è già corrispondente.

Quando Cloud Manager distribuisce l&#39;applicazione, esegue queste istruzioni, indipendentemente dall&#39;installazione di qualsiasi pacchetto di contenuto.

Per creare delle istruzioni di reindirizzamento, attenersi alla procedura seguente:

1. Aggiungi configurazione OSGi per PID `org.apache.sling.jcr.repoinit.RepositoryInitializer` in una cartella di configurazione del progetto
1. Aggiungete istruzioni di reindirizzamento alla proprietà script della configurazione. La sintassi e le opzioni sono documentate nella documentazione di [Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html). Prima delle cartelle figlie, è necessario creare esplicitamente una cartella principale. Ad esempio, una creazione esplicita di `/content` before `/content/myfolder`, before `/content/myfolder/mysubfolder`. Per gli ACL impostati su strutture di basso livello, si consiglia di impostarli su un livello superiore e lavorare con una `rep:glob` limitazione.  Esempio `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Convalida nell&#39;ambiente di sviluppo locale in fase di esecuzione.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>Per gli ACL definiti per i nodi sottostanti `/apps` o `/libs` l&#39;esecuzione del ripristino verrà avviata in un repository vuoto. I pacchetti vengono installati dopo il riavvio, pertanto le istruzioni non possono basarsi su elementi definiti nei pacchetti, ma devono definire le condizioni preliminari come le strutture padre sottostanti.

>[!TIP]
>
>Per gli ACL la creazione di strutture profonde potrebbe essere ingombrante, quindi è più ragionevole definire un ACL su un livello più alto e limitare dove si suppone che agisca tramite una restrizione rep:idspn.

Maggiori informazioni sul repoinit sono disponibili nella documentazione [Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Package Manager: &quot;one offs&quot; per pacchetti di contenuto variabile {#package-manager-oneoffs-for-mutable-content-packages}

In alcuni casi, un pacchetto di contenuti deve essere installato come &quot;una tantum&quot;. Ad esempio, l&#39;importazione di contenuto specifico dalla produzione all&#39;area di produzione per eseguire il debug di un problema di produzione. Per questi scenari, Package Manager può essere utilizzato in AEM come ambiente di servizio cloud.

Poiché Package Manager è un concetto di runtime, non è possibile installare contenuto o codice nell&#39;archivio immutabile, pertanto questi pacchetti di contenuto devono essere costituiti solo da contenuto variabile (principalmente `/content` o `/conf`). Se il pacchetto di contenuti include contenuto misto (contenuto modificabile e non modificabile), verrà installato solo il contenuto modificabile.

Tutti i pacchetti di contenuto installati tramite Cloud Manager (sia modificabili che immutabili) verranno visualizzati in uno stato bloccato nell&#39;interfaccia utente di AEM Package Manager. Questi pacchetti non possono essere reinstallati, rigenerati o persino scaricati e saranno elencati con un suffisso **&quot;cp2fm&quot;** , a indicare che la loro installazione è stata gestita da Cloud Manager.

### Inclusione di pacchetti di terze parti {#including-third-party}

È comune per i clienti includere pacchetti pre-costruiti da fonti di terze parti come fornitori di software come i partner di traduzione di Adobe. Si consiglia di ospitare questi pacchetti in un repository remoto e di farvi riferimento nel `pom.xml`. Ciò è possibile solo per i repository pubblici.

Se non è possibile memorizzare il pacchetto in un archivio remoto, i clienti possono inserirlo in un archivio Maven locale basato su file system, che viene impegnato a SCM come parte del progetto e a cui fanno riferimento qualsiasi cosa dipenda da esso. Il repository è dichiarato nei programmi di progetto illustrati di seguito:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Tutti i pacchetti di terze parti inclusi devono essere conformi ad AEM come codici e linee guida per la creazione di pacchetti del servizio cloud descritte in questo articolo. In caso contrario, l&#39;inclusione di tali pacchetti comporterà un errore di distribuzione.

Lo snippet XML Maven POM seguente mostra come i pacchetti di terze parti possono essere incorporati nel pacchetto &quot;Container&quot; del progetto, in genere denominato **&#39;all&#39;**, tramite la configurazione del plug-in Maven **package-maven-plugin** difilevault-package.

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <subPackages>
           
          <!-- Include the application's ui.apps and ui.content packages -->
          ...
 
          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <!-- Set the version for all dependencies, including 3rd party packages, in the project's Reactor POM -->
          <subPackage>
              <groupId>com.adobe.cq</groupId>
              <artifactId>core.wcm.components.all</artifactId>
              <filter>true</filter>
          </subPackage>
 
 
          <subPackage>
              <groupId>com.3rdparty.groupId</groupId>
              <artifactId>core.3rdparty.artifactId</artifactId>
              <filter>true</filter>
          </subPackage>
      <subPackages>
  </configuration>
</plugin>
...
```

## Funzionamento delle implementazioni continue {#how-rolling-deployments-work}

Come per gli aggiornamenti di AEM, i rilasci dei clienti vengono distribuiti utilizzando una strategia di distribuzione continua per eliminare i tempi di inattività del cluster di autori nelle circostanze giuste. La sequenza generale degli eventi è come descritto di seguito, dove **Blue** è la vecchia versione del codice cliente e **Green** è la nuova versione. Blu e Verde eseguono la stessa versione del codice AEM.

* La versione blu è attiva e un candidato per la release per Green è costruito e disponibile
* In presenza di definizioni di indice nuove o aggiornate, vengono elaborati gli indici corrispondenti. Nella distribuzione blu verranno sempre utilizzati i vecchi indici, mentre in verde verranno sempre utilizzati i nuovi indici.
* Il verde sta iniziando mentre il blu sta ancora servendo
* Blue è in esecuzione e servire mentre Green è controllato per la disponibilità tramite controlli di integrità
* Nodi verdi che sono pronti ad accettare il traffico e sostituire i nodi blu, che vengono ridotti
* Nel tempo, i nodi blu vengono sostituiti da nodi verdi fino a quando non rimane solo verde, completando così la distribuzione
* Qualsiasi contenuto nuovo o modificato modificabile distribuito

## Indici {#indexes}

Gli indici nuovi o modificati causeranno un ulteriore passaggio di indicizzazione o reindicizzazione prima che la nuova versione (verde) possa iniziare il traffico. Informazioni dettagliate sulla gestione dell&#39;indice in Skyline sono disponibili in [questo articolo](/help/operations/indexing.md). Puoi controllare lo stato del processo di indicizzazione nella pagina di compilazione di Cloud Manager e riceverai una notifica quando la nuova versione sarà pronta per il traffico.

>[!NOTE]
>
>Il tempo necessario per una distribuzione continua varia a seconda delle dimensioni dell&#39;indice, poiché la versione verde non può accettare il traffico fino alla generazione del nuovo indice.

Al momento, Skyline non funziona con strumenti di gestione degli indici come lo strumento ACS Commons Verify Oak Index Tool.

## Replica {#replication}

Il meccanismo di pubblicazione è compatibile con le API Java di replica di [AEM](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html).

Per sviluppare e testare la replica con AEM QuickStart, con AEM già pronto per il cloud, le funzionalità di replica classica devono essere utilizzate con una configurazione Autore/Pubblicazione. Nel caso in cui il punto di ingresso dell&#39;interfaccia utente su AEM Author sia stato rimosso per il cloud, gli utenti accederebbero `http://localhost:4502/etc/replication` alla configurazione.

## Codice compatibile con le versioni precedenti per le installazioni continue {#backwards-compatible-code-for-rolling-deployments}

Come indicato in precedenza, AEM come strategia di distribuzione continua del servizio cloud implica che sia le versioni precedenti che quelle nuove possono funzionare contemporaneamente. Di conseguenza, prestate attenzione alle modifiche di codice che non sono compatibili con la vecchia versione di AEM che è ancora in funzione.

Inoltre, la vecchia release deve essere testata per verificare la compatibilità con eventuali nuove strutture di contenuto modificabili applicate dalla nuova release in caso di rollback, dal momento che il contenuto modificabile non viene rimosso.

### Utenti del servizio e modifiche ACL {#service-users-and-acl-changes}

La modifica degli utenti di servizi o degli ACL necessari per accedere al contenuto o al codice potrebbe causare errori nelle versioni precedenti di AEM, con conseguente accesso a tale contenuto o codice con utenti di servizi non aggiornati. Per risolvere questo problema, una raccomandazione consiste nell&#39;apportare modifiche distribuite su almeno 2 rilasci, con la prima release che funge da ponte prima di essere ripulita nella release successiva.

### Modifiche indice {#index-changes}

Se vengono apportate modifiche agli indici, è importante che la versione Blu continui a utilizzare i relativi indici fino a quando non viene terminata, mentre la versione Verde utilizza il proprio set modificato di indici. Lo sviluppatore deve seguire le tecniche di gestione dell&#39;indice descritte [in questo articolo](/help/operations/indexing.md).

### Codifica conservativa per i rollback {#conservative-coding-for-rollbacks}

Se un errore viene segnalato o rilevato dopo la distribuzione, è possibile che sia necessario eseguire il rollback alla versione Blu. Sarebbe opportuno garantire che il codice blu sia compatibile con tutte le nuove strutture create dalla versione verde, in quanto le nuove strutture (eventuali contenuti modificabili) non verranno ripristinate. Se il codice precedente non è compatibile, è necessario applicare delle correzioni nelle versioni successive del cliente.

## Modalità di esecuzione {#runmodes}

Nelle soluzioni AEM esistenti, i clienti possono eseguire le istanze con modalità di esecuzione arbitrarie e applicare la configurazione OSGI o installare i bundle OSGI a tali istanze specifiche. Le modalità di esecuzione definite in genere includono il *servizio* (autore e pubblicazione) e l&#39;ambiente (dev, stage, prod).

AEM come servizio cloud, d’altro canto, è più chiaro quali sono le modalità di esecuzione disponibili e come è possibile mappare i bundle OSGI e la configurazione OSGI:

* Le modalità di esecuzione della configurazione OSGI devono fare riferimento a dev, stage, prod per l’ambiente o l’autore, publish per il servizio. È `<service>.<environment_type>` supportata una combinazione di elementi, che devono essere utilizzati in questo particolare ordine (ad esempio author.dev o publish.prod). I token OSGI devono essere citati direttamente dal codice anziché utilizzando il `getRunModes` metodo, che non includerà più il token `environment_type` in fase di esecuzione.
* Le modalità di esecuzione dei bundle OSGI sono limitate al servizio (autore, pubblicazione). I bundle OSGI per modalità di esecuzione devono essere installati nel pacchetto di contenuto in `install/author` o `install/publish`.

Come le soluzioni AEM esistenti, non è possibile utilizzare le modalità di esecuzione per installare solo contenuti per ambienti o servizi specifici. Se si desidera generare un ambiente di sviluppo con dati o HTML non presenti sul palco o sulla produzione, è possibile utilizzare il gestore pacchetti.

Le configurazioni di modalità di esecuzione supportate sono:

* **config** (*l&#39;impostazione predefinita si applica a tutti i servizi* AEM)
* **config.author** (*applicabile a tutti i servizi* AEM Author)
* **config.author.dev** (*applicabile al servizio* AEM Dev Author)
* **config.author.stage** (*applicabile al servizio* AEM Staging Author)
* **config.author.prod** (*applicabile al servizio* AEM Production Author)
* **config.publish** (*applicabile al servizio* AEM Publish)
* **config.publish.dev** (*applicabile al servizio* AEM Dev Publish)
* **config.publish.stage** (*applicabile al servizio* AEM Staging Publish)
* **config.publish.prod** (*applicabile al servizio* AEM Production Publish)
* **config.dev** (*Si applica ai servizi AEM Dev)
* **config.stage** (*Si applica ai servizi di gestione temporanea AEM)
* **config.prod** (*Si applica ai servizi di produzione AEM)

Viene utilizzata la configurazione OSGI con le modalità di esecuzione più corrispondenti.

Quando si sviluppa localmente, è possibile passare un parametro di avvio in modalità di esecuzione per stabilire quale configurazione OSGI in modalità di esecuzione verrà utilizzata.

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Configurazione delle attività di manutenzione nel controllo del codice sorgente {#maintenance-tasks-configuration-in-source-control}

Le configurazioni delle attività di manutenzione devono essere mantenute nel controllo del codice sorgente, dal momento che la schermata **Strumenti > Operazioni** non sarà più disponibile negli ambienti Cloud. Questo ha il vantaggio di garantire che i cambiamenti siano intenzionalmente persistenti piuttosto che reattivamente applicati e forse dimenticati. Per ulteriori informazioni, fare riferimento all&#39;articolo [Attività di](/help/operations/maintenance.md) manutenzione.
