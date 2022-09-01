---
title: Implementazione in AEM as a Cloud Service
description: 'Implementazione in AEM as a Cloud Service '
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '3346'
ht-degree: 1%

---

# Implementazione in AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## Introduzione {#introduction}

Le basi dello sviluppo del codice sono simili in AEM as a Cloud Service rispetto alle soluzioni AEM On Premise e Managed Services. Gli sviluppatori scrivono il codice e lo testano localmente, che viene quindi inviato agli ambienti AEM as a Cloud Service remoti. Cloud Manager, uno strumento opzionale per la distribuzione dei contenuti per Managed Services, è necessario. Questo è ora l’unico meccanismo per distribuire il codice AEM ambienti as a Cloud Service.

L&#39;aggiornamento della [Versione AEM](/help/implementing/deploying/aem-version-updates.md) è sempre un evento di distribuzione separato dal push [codice personalizzato](#customer-releases). Visualizzate in un altro modo, le versioni del codice personalizzato devono essere testate rispetto alla versione AEM in produzione, in quanto questo è ciò che verrà distribuito in alto. AEM aggiornamenti di versione che si verificano in seguito, che saranno frequenti e vengono applicati automaticamente. Sono compatibili con le versioni precedenti del codice cliente già distribuito.

Il resto di questo documento descriverà come gli sviluppatori devono adattare le proprie pratiche in modo che funzionino con gli aggiornamenti della versione di AEM as a Cloud Service e con gli aggiornamenti dei clienti.

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## Rilasci di clienti {#customer-releases}

### Codifica rispetto alla versione AEM corretta {#coding-against-the-right-aem-version}

Per le soluzioni AEM precedenti, la versione AEM più recente è cambiata raramente (circa una volta all’anno con service pack trimestrali) e i clienti aggiornavano le istanze di produzione all’ultimo quickstart, facendo riferimento al Jar API. Tuttavia, AEM applicazioni as a Cloud Service vengono aggiornate automaticamente alla versione più recente di AEM più spesso, pertanto il codice personalizzato per le versioni interne deve essere generato in base alla versione AEM più recente.

Come per le versioni non cloud AEM esistenti, nella maggior parte dei casi sarà supportato uno sviluppo locale e offline basato su un quickstart specifico e dovrebbe essere lo strumento preferito per il debug.

>[!NOTE]
>Esistono sottili differenze operative tra il comportamento dell’applicazione su un computer locale e Adobe Cloud. Queste differenze architettoniche devono essere rispettate durante lo sviluppo locale e possono portare a un comportamento diverso durante l&#39;implementazione nell&#39;infrastruttura cloud. A causa di queste differenze, è importante eseguire test esaustivi sugli ambienti di sviluppo e stage prima di implementare un nuovo codice personalizzato in produzione.

Al fine di sviluppare codice personalizzato per una versione interna, la versione pertinente della [AEM SDK as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) devono essere scaricati e installati. Per ulteriori informazioni sull’utilizzo dei AEM strumenti di Dispatcher as a Cloud Service, consulta [questa pagina](/help/implementing/dispatcher/disp-overview.md).

Il video seguente fornisce una panoramica di alto livello su come distribuire il codice AEM as a Cloud Service:

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## Distribuzione di pacchetti di contenuti tramite Cloud Manager e Package Manager {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Implementazioni tramite Cloud Manager {#deployments-via-cloud-manager}

I clienti distribuiscono il codice personalizzato agli ambienti cloud tramite Cloud Manager. È opportuno notare che Cloud Manager trasforma i pacchetti di contenuto assemblati localmente in un artefatto conforme al modello di funzioni Sling. Questo è il modo in cui viene descritta un’applicazione as a Cloud Service AEM quando viene eseguita in un ambiente cloud. Di conseguenza, quando si esaminano i pacchetti in [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) negli ambienti cloud, il nome includerà &quot;cp2fm&quot; e i pacchetti trasformati avranno tutti i metadati rimossi. Non è possibile interagire con questi elementi, ovvero non è possibile scaricarli, replicarli o aprirli. La documentazione dettagliata sul convertitore può essere [qui](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

I pacchetti di contenuto scritti per AEM applicazioni as a Cloud Service devono avere una separazione netta tra contenuto immutabile e contenuto mutabile; Cloud Manager installerà solo il contenuto mutabile, producendo anche un messaggio come:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

Il resto di questa sezione descriverà la composizione e le implicazioni dei pacchetti immutabili e mutabili.

### Pacchetti di contenuti immutabili {#immutabe-content-packages}

Tutti i contenuti e il codice mantenuti nell’archivio immutabile devono essere controllati in git e distribuiti tramite Cloud Manager. In altre parole, a differenza delle soluzioni AEM correnti, il codice non viene mai distribuito direttamente in un&#39;istanza AEM in esecuzione. Questo assicura che il codice in esecuzione per una determinata versione in qualsiasi ambiente Cloud sia identico, eliminando il rischio di variazione involontaria del codice in produzione. Ad esempio, la configurazione OSGI deve essere impegnata nel controllo del codice sorgente anziché gestita in fase di esecuzione tramite il gestore di configurazione della console Web AEM.

Poiché le modifiche dell&#39;applicazione dovute al pattern di distribuzione Blue-Green sono abilitate da un interruttore, non possono dipendere dalle modifiche nell&#39;archivio mutabile con l&#39;eccezione degli utenti del servizio, le loro ACL, i tipi di nodo e le modifiche della definizione dell&#39;indice.

Per i clienti con basi di codice esistenti, è fondamentale seguire l’esercizio di ristrutturazione dell’archivio descritto nella documentazione di AEM per garantire che il contenuto precedente sotto /etc venga spostato nella posizione giusta.

Per questi pacchetti di codice si applicano alcune restrizioni aggiuntive, ad esempio [installare gli hook](https://jackrabbit.apache.org/filevault/installhooks.html) non sono supportati.

## Configurazione OSGI {#osgi-configuration}

Come accennato in precedenza, la configurazione OSGI deve essere impegnata nel controllo del codice sorgente anziché attraverso la console web. Le tecniche per farlo includono:

* Apportare le modifiche necessarie nell&#39;ambiente AEM locale dello sviluppatore con il gestore di configurazione della console Web AEM, quindi esportare i risultati nel progetto AEM nel file system locale
* Creazione manuale della configurazione OSGI nel progetto AEM nel file system locale, riferimento alla gestione della configurazione della console AEM per i nomi delle proprietà.

Ulteriori informazioni sulla configurazione OSGI all&#39;indirizzo [Configurazione di OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Contenuto variabile {#mutable-content}

In alcuni casi potrebbe essere utile preparare le modifiche al contenuto nel controllo del codice sorgente in modo che possa essere distribuito da Cloud Manager ogni volta che un ambiente viene aggiornato. Ad esempio, potrebbe essere ragionevole impostare alcune strutture di cartelle principali o allineare le modifiche nei modelli modificabili per abilitare i criteri in quelli per i componenti aggiornati dalla distribuzione dell&#39;applicazione.

Esistono due strategie per descrivere il contenuto che verrà distribuito da Cloud Manager nell’archivio mutabile, i pacchetti di contenuto variabile e le istruzioni di reindirizzamento.

### Pacchetti di contenuto variabile {#mutable-content-packages}

Contenuti come gerarchie di percorsi di cartelle, utenti di servizi e controlli di accesso (ACL) vengono generalmente impegnati in un progetto AEM basato su archetipo maven. Le tecniche includono l’esportazione da AEM o la scrittura diretta come XML. Durante il processo di creazione e distribuzione, Cloud Manager crea un pacchetto con il pacchetto di contenuto variabile risultante. Il contenuto modificabile viene installato in 3 momenti diversi durante la fase di distribuzione nella pipeline:

Prima dell&#39;avvio della nuova versione dell&#39;applicazione:

* definizioni degli indici (aggiungere, modificare, rimuovere)

Durante l&#39;avvio di una nuova versione dell&#39;applicazione, ma prima del passaggio:

* Utenti del servizio (aggiungere)
* ACL dell&#39;utente del servizio (aggiungi)
* tipi di nodo (aggiungere)

Dopo il passaggio alla nuova versione dell&#39;applicazione:

* Tutti gli altri contenuti definibili tramite vault jackrabbit. Esempio:
   * Cartelle (aggiungere, modificare, rimuovere)
   * Modelli modificabili (aggiungere, modificare, rimuovere)
   * Configurazione in base al contesto (qualsiasi cosa in `/conf`) (aggiungere, modificare, rimuovere)
   * Script (i pacchetti possono attivare gli hook di installazione in varie fasi del processo di installazione del pacchetto. <!-- MISDIRECTED REQUEST, 421 ERROR, CAN'T FIND CORRECT PATH See the [Jackrabbit filevault documentation](https://jackrabbit.incubator.apache.org/filevault/installhooks.html) about install hooks. --> Nota che AEM CS utilizza attualmente Filevault versione 3.4.0, che limita gli hook di installazione agli utenti amministratori, agli utenti di sistema e al membro del gruppo di amministratori).

È possibile limitare l’installazione di contenuti modificabili all’authoring o alla pubblicazione incorporando pacchetti in una cartella install.author o install.publish in `/apps`. La ristrutturazione per rispecchiare tale separazione è stata effettuata nel AEM 6.5 e i dettagli relativi alla ristrutturazione del progetto raccomandata si trovano nella [Documentazione di AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=it)

>[!NOTE]
>I pacchetti di contenuto vengono distribuiti in tutti i tipi di ambiente (dev, stage, prod). Non è possibile limitare la distribuzione a un ambiente specifico. Questa limitazione è in vigore per garantire la possibilità di eseguire un test di esecuzione automatica. I contenuti specifici di un ambiente richiedono l’installazione manuale tramite [Gestione pacchetti.](/help/implementing/developing/tools/package-manager.md)

Inoltre, non esiste un meccanismo per ripristinare le modifiche al pacchetto di contenuti modificabili dopo l’applicazione. Se i clienti rilevano un problema, possono scegliere di correggerlo nella versione successiva del codice o come ultima risorsa, ripristinare l&#39;intero sistema in un punto temporale prima della distribuzione.

Eventuali pacchetti di terze parti inclusi devono essere convalidati come compatibili con AEM servizio as a Cloud Service, altrimenti la loro inclusione provocherà un errore di distribuzione.

Come indicato in precedenza, i clienti con basi di codice esistenti devono conformarsi all’esercizio di ristrutturazione dell’archivio richiesto dalle modifiche dell’archivio 6.5 descritte nella sezione [Documentazione di AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## Repoinit {#repoinit}

Per i casi seguenti, è preferibile adottare l’approccio della codifica manuale per la creazione esplicita di contenuti `repoinit` dichiarazioni nelle configurazioni di fabbrica OSGI:

* Creare/eliminare/disabilitare gli utenti del servizio
* Creare/eliminare gruppi
* Creare/eliminare utenti
* Aggiungi ACL

   >[!NOTE]
   >
   >La definizione delle ACL richiede che le strutture dei nodi siano già presenti. Pertanto, potrebbe essere necessario creare istruzioni di percorso precedenti.

* Aggiungi percorso (ad esempio per le strutture di cartelle principali)
* Aggiungere CND (definizioni dei tipi di nodo)

Repoinit è preferibile per questi casi d’uso di modifica del contenuto supportati a causa dei seguenti vantaggi:

* Repoinit crea risorse all’avvio in modo che la logica possa dare per scontata l’esistenza di tali risorse. Nell’approccio a pacchetti di contenuti mutabili, le risorse vengono create dopo l’avvio, pertanto il codice dell’applicazione che si basa su di esse potrebbe non riuscire.
* Repoinit è un set di istruzioni relativamente sicuro in quanto si controlla esplicitamente l&#39;azione da intraprendere. Inoltre, le uniche operazioni supportate sono additivi ad eccezione di alcuni casi relativi alla sicurezza che consentono la rimozione di utenti, utenti dei servizi e gruppi. Al contrario, è esplicita la rimozione di qualcosa nell’approccio a pacchetti di contenuti variabili; quando definisci un filtro, tutto ciò che è presente coperto da un filtro verrà eliminato. Tuttavia, è necessario prestare attenzione, in quanto con qualsiasi contenuto ci sono scenari in cui la presenza di nuovi contenuti può alterare il comportamento dell’applicazione.
* Repoinit esegue operazioni rapide e atomiche. I pacchetti di contenuti variabili al contrario possono dipendere in modo molto efficiente dalle prestazioni delle strutture coperte da un filtro. Anche se si aggiorna un singolo nodo, è possibile creare un&#39;istantanea di un albero di grandi dimensioni.
* È possibile convalidare le istruzioni di repoinit in un ambiente di sviluppo locale in fase di runtime, poiché verranno eseguite quando la configurazione OSGi viene registrata.
* Le istruzioni Repoinit sono atomiche ed esplicite e ignorano se lo stato è già corrispondente.

Quando Cloud Manager distribuisce l’applicazione, esegue queste istruzioni, indipendentemente dall’installazione di qualsiasi pacchetto di contenuto.

Per creare istruzioni di reindirizzamento, segui la procedura seguente:

1. Aggiungi la configurazione OSGi per il PID di fabbrica `org.apache.sling.jcr.repoinit.RepositoryInitializer` in una cartella di configurazione del progetto. Usa un nome descrittivo per la configurazione come **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**.
1. Aggiungi le istruzioni repoinit alla proprietà script della configurazione. La sintassi e le opzioni sono documentate in [Documentazione Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html). Si noti che è necessario creare esplicitamente una cartella padre prima delle relative cartelle figlio. Ad esempio, una creazione esplicita di `/content` prima `/content/myfolder`prima `/content/myfolder/mysubfolder`. Per le ACL impostate su strutture di basso livello si consiglia di impostarle su un livello superiore e lavorare con un `rep:glob` restrizione.  Esempio `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Convalida nell&#39;ambiente di sviluppo locale in fase di runtime.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>Per ACL definiti per nodi sottostanti `/apps` o `/libs` l’esecuzione del repoinit inizia su un archivio vuoto. I pacchetti vengono installati dopo il ripristino, pertanto le istruzioni non possono basarsi su elementi definiti nei pacchetti, ma devono definire le condizioni preliminari come le strutture padre sottostanti.

>[!TIP]
>
>Per gli ACL la creazione di strutture profonde potrebbe essere ingombrante, quindi è più ragionevole definire un ACL su un livello più alto e vincolare dove si suppone che agisca tramite una restrizione rep:glob.

Maggiori dettagli sul repoinit sono disponibili nella sezione [Documentazione Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Gestione pacchetti &quot;una offs&quot; per pacchetti di contenuti variabili {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="Gestione pacchetti - Migrazione dei pacchetti di contenuto variabile"
>abstract="Esplora l’utilizzo di package manager per i casi d’uso in cui un pacchetto di contenuti deve essere installato come &quot;una tantum&quot;, che include l’importazione di contenuti specifici dalla produzione alla gestione temporanea per eseguire il debug di un problema di produzione, il trasferimento di piccoli pacchetti di contenuti dall’ambiente locale agli ambienti AEM Cloud e altro ancora."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#cloud-migration" text="Strumento Content Transfer (Trasferimento contenuti)"

Ci sono casi d’uso in cui un pacchetto di contenuti deve essere installato come &quot;una tantum&quot;. Ad esempio, per eseguire il debug di un problema di produzione, è necessario importare contenuto specifico dalla produzione nella fase di staging. Per questi scenari, [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) può essere utilizzato in ambienti AEM as a Cloud Service.

Poiché Gestione pacchetti è un concetto di runtime, non è possibile installare contenuto o codice nell’archivio immutabile, quindi questi pacchetti di contenuto devono essere costituiti solo da contenuto variabile (principalmente `/content` o `/conf`). Se il pacchetto di contenuti include contenuti misti (con contenuto modificabile e non modificabile), verrà installato solo il contenuto modificabile.

>[!IMPORTANT]
>
>L’interfaccia utente di Gestione pacchetti potrebbe restituire un **indefinito** messaggio di errore se l&#39;installazione di un pacchetto richiede più di 10 minuti.
>
>Questo non è dovuto a un errore con l&#39;installazione, ma a un timeout che il Cloud Service ha per tutte le richieste.
>
>Non ripetere l&#39;installazione se viene visualizzato un errore di questo tipo. L&#39;installazione sta procedendo correttamente in background. Se si riavvia l&#39;installazione, alcuni conflitti potrebbero essere introdotti da più processi di importazione simultanei.

Tutti i pacchetti di contenuto installati tramite Cloud Manager (mutabili e immutabili) verranno visualizzati in uno stato congelato nell’interfaccia utente di AEM Package Manager. Questi pacchetti non possono essere reinstallati, ricostruiti o persino scaricati e verranno elencati con un **&quot;cp2fm&quot;** suffisso che indica che l’installazione è stata gestita da Cloud Manager.

### Inclusi Pacchetti Di Terze Parti {#including-third-party}

È comune per i clienti includere pacchetti precompilati da fonti di terze parti, come fornitori di software come i partner di traduzione di Adobe. Si consiglia di ospitare questi pacchetti in un archivio remoto e farvi riferimento in `pom.xml`. Questo è possibile per gli archivi pubblici e anche per gli archivi privati con protezione tramite password, come descritto in [archivi Maven protetti da password](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

Se non è possibile memorizzare il pacchetto in un archivio remoto, i clienti possono inserirlo in un archivio Maven locale basato su file system, che è impegnato in SCM come parte del progetto e a cui fa riferimento qualsiasi cosa dipenda da esso. L’archivio viene dichiarato nell’area di lavoro del progetto come illustrato di seguito:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Tutti i pacchetti di terze parti inclusi devono essere conformi alle AEM linee guida per la codifica dei servizi as a Cloud Service e la creazione di pacchetti descritte nel presente articolo, altrimenti la loro inclusione provocherà un errore di distribuzione.

Il seguente Maven `POM.xml` Lo snippet mostra come incorporare i pacchetti di terze parti nel pacchetto &quot;Container&quot; del progetto, in genere denominato **&quot;all&quot;**, tramite **filevault-package-maven-plugin** Configurazione del plug-in Maven.

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          ...

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

## Funzionamento delle implementazioni continue {#how-rolling-deployments-work}

Come per gli aggiornamenti AEM, le versioni dei clienti vengono implementate utilizzando una strategia di implementazione continua per eliminare i tempi di inattività dei cluster di authoring nelle giuste circostanze. La sequenza generale degli eventi è descritta di seguito, dove **Blu** è la vecchia versione del codice cliente e **Verde** è la nuova versione. Sia blu che verde eseguono la stessa versione del codice AEM.

* La versione blu è attiva e viene creato e disponibile un candidato per il rilascio per Green
* In presenza di definizioni di indice nuove o aggiornate, gli indici corrispondenti vengono elaborati. La distribuzione blu utilizzerà sempre i vecchi indici, mentre quella verde utilizzerà sempre i nuovi indici.
* Il verde sta iniziando mentre il blu sta ancora servendo
* Blue è in esecuzione e in servizio mentre Green è controllato per la preparazione tramite controlli di salute
* Nodi verdi che sono pronti ad accettare il traffico e sostituire i nodi blu, che vengono ridotti
* Nel tempo, i nodi blu vengono sostituiti dai nodi verdi fino a quando non rimane solo verde, completando così la distribuzione
* Eventuali contenuti modificabili nuovi o modificati vengono distribuiti

## Indici {#indexes}

Gli indici nuovi o modificati causeranno un ulteriore passaggio di indicizzazione o reindicizzazione prima che la nuova versione (verde) possa assumere traffico. I dettagli sulla gestione degli indici in AEM as a Cloud Service si trovano in [articolo](/help/operations/indexing.md). Puoi controllare lo stato del processo di indicizzazione nella pagina di build di Cloud Manager e riceverai una notifica quando la nuova versione è pronta per il traffico.

>[!NOTE]
>
>Il tempo necessario per una distribuzione continua varia a seconda delle dimensioni dell&#39;indice, poiché la versione verde non può accettare il traffico fino a quando non viene generato il nuovo indice.

Al momento, AEM as a Cloud Service non funziona con strumenti di gestione degli indici come lo strumento ACS Commons Assurance Oak Index.

## Replica {#replication}

Il meccanismo di pubblicazione è retrocompatibile con [API Java di replica di AEM](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html).

Per sviluppare e testare con la replica con l&#39;avvio rapido AEM cloud ready, le funzionalità di replica classica devono essere utilizzate con un&#39;impostazione Autore/Pubblicazione. Nel caso in cui il punto di ingresso dell’interfaccia utente su AEM Author sia stato rimosso per il cloud, gli utenti accederebbero a `http://localhost:4502/etc/replication` per la configurazione.

## Codice compatibile con versioni precedenti per implementazioni continue {#backwards-compatible-code-for-rolling-deployments}

Come descritto in precedenza, AEM strategia di distribuzione continua di as a Cloud Service implica che sia le versioni precedenti che quelle nuove possono funzionare contemporaneamente. Pertanto, presta attenzione alle modifiche del codice che non sono compatibili con la vecchia versione AEM che è ancora in esecuzione.

Inoltre, la vecchia versione deve essere testata per verificare la compatibilità con eventuali nuove strutture di contenuto variabile applicate dalla nuova versione in caso di rollback, in quanto il contenuto mutabile non viene rimosso.

### Utenti del servizio e modifiche ACL {#service-users-and-acl-changes}

La modifica degli utenti del servizio o delle ACL necessarie per accedere al contenuto o al codice potrebbe causare errori nelle versioni precedenti di AEM e causare l’accesso a tale contenuto o codice con utenti del servizio obsoleti. Per risolvere questo problema, una raccomandazione consiste nell’apportare modifiche distribuite su almeno 2 rilasci, con la prima release che funge da ponte prima di essere ripulita nella versione successiva.

### Modifiche all&#39;indice {#index-changes}

Se vengono apportate modifiche agli indici, è importante che la versione blu continui a utilizzare i suoi indici fino alla sua chiusura, mentre la versione verde utilizza il proprio set modificato di indici. Lo sviluppatore deve seguire le tecniche di gestione degli indici descritte [nel presente articolo](/help/operations/indexing.md).

### Codifica conservativa per i rollback {#conservative-coding-for-rollbacks}

Se viene segnalato o rilevato un errore dopo la distribuzione, è possibile che sia necessario eseguire il rollback alla versione Blue. Sarebbe opportuno garantire che il codice blu sia compatibile con tutte le nuove strutture create dalla versione verde, in quanto le nuove strutture (qualsiasi contenuto mutabile) non verranno rimandate indietro. Se il codice precedente non è compatibile, le correzioni dovranno essere applicate nelle versioni successive del cliente.

## Modalità di esecuzione {#runmodes}

Nelle soluzioni AEM esistenti, i clienti possono scegliere di eseguire istanze con modalità di esecuzione arbitrarie e applicare la configurazione OSGI o installare i bundle OSGI a quelle istanze specifiche. Le modalità di esecuzione definite includono in genere i *servizio* (autore e pubblicazione) e l’ambiente (sviluppo, stage, prod).

AEM as a Cloud Service d&#39;altra parte è più opinionista su quali modalità di esecuzione sono disponibili e come i bundle OSGI e la configurazione OSGI possono essere mappati su di loro:

* Le modalità di esecuzione della configurazione OSGI devono fare riferimento a dev, stage, prod per l’ambiente o l’autore, publish per il servizio. Una combinazione di `<service>.<environment_type>` è supportato, che devono essere utilizzati in questo particolare ordine (ad esempio `author.dev` o `publish.prod`). I token OSGI devono essere referenziati direttamente dal codice anziché utilizzando `getRunModes` , che non includerà più `environment_type` in fase di runtime. Per ulteriori informazioni, consulta [Configurazione di OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).
* Le modalità di esecuzione dei bundle OSGI sono limitate al servizio (autore, pubblicazione). I bundle OSGI per modalità di esecuzione devono essere installati nel pacchetto di contenuti in `install/author` o `install/publish`.

Come le soluzioni AEM esistenti, non c&#39;è modo di utilizzare le modalità di esecuzione per installare solo contenuti per ambienti o servizi specifici. Se si desidera impostare un ambiente di sviluppo con dati o HTML che non sono sul palco o in produzione, è possibile utilizzare il gestore dei pacchetti.

Le configurazioni supportate per la modalità di esecuzione sono:

* **config** (*Il valore predefinito si applica a tutti i servizi AEM*)
* **config.author** (*Si applica a tutti i servizi AEM Author*)
* **config.author.dev** (*Si applica al servizio AEM Dev Author*)
* **config.author.stage** (*Si applica a AEM servizio di authoring di staging*)
* **config.author.prod** (*Si applica AEM servizio di authoring di produzione*)
* **config.publish** (*Si applica al servizio di pubblicazione AEM*)
* **config.publish.dev** (*Si applica al servizio Pubblicazione sviluppo AEM*)
* **config.publish.stage** (*Si applica a AEM servizio di pubblicazione temporanea*)
* **config.publish.prod** (*Si applica a AEM servizio di pubblicazione di produzione*)
* **config.dev** (*Si applica ai servizi di sviluppo AEM*)
* **config.stage** (*Si applica ai servizi di staging AEM*)
* **config.prod** (*Si applica ai servizi di produzione AEM*)

Viene utilizzata la configurazione OSGI con le modalità di esecuzione più corrispondenti.

Quando si sviluppa localmente, un parametro di avvio in modalità runmode, `-r`, viene utilizzato per specificare la configurazione OSGI in modalità runmode.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Configurazione delle attività di manutenzione nel controllo del codice sorgente {#maintenance-tasks-configuration-in-source-control}

Le configurazioni delle attività di manutenzione devono essere mantenute nel controllo del codice sorgente poiché **Strumenti > Operazioni** Lo schermo non sarà più disponibile negli ambienti Cloud. Ciò ha il vantaggio di garantire che i cambiamenti siano intenzionalmente persistenti piuttosto che applicati reattivamente e forse dimenticati. Fai riferimento alla [Articolo attività di manutenzione](/help/operations/maintenance.md) per ulteriori informazioni.
