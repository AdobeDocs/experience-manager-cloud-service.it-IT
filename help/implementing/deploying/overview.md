---
title: Implementazione in AEM as a Cloud Service
description: Implementazione in AEM as a Cloud Service
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '3462'
ht-degree: 42%

---

# Implementazione in AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## Introduzione {#introduction}

Le basi dello sviluppo del codice sono simili in AEM as a Cloud Service rispetto alle soluzioni AEM On Premise e Managed Services. Gli sviluppatori scrivono il codice e lo testano localmente, che viene quindi inviato in ambienti remoti su AEM as a Cloud Service. Cloud Manager, che era uno strumento opzionale per la distribuzione dei contenuti per Managed Services, è necessario. Questo strumento di distribuzione è ora l’unico meccanismo per distribuire il codice negli ambienti di sviluppo, stage e produzione as a Cloud Service dell’AEM. Per una convalida e un debug rapidi delle funzioni prima di distribuire gli ambienti precedentemente menzionati, è possibile sincronizzare il codice da un ambiente locale a un [Ambiente di sviluppo rapido](/help/implementing/developing/introduction/rapid-development-environments.md).

L’aggiornamento della [Versione AEM](/help/implementing/deploying/aem-version-updates.md) è sempre un evento di distribuzione separato dal push del [codice personalizzato](#customer-releases). In un altro modo, le versioni del codice personalizzato devono essere testate rispetto alla versione dell’AEM in produzione, perché è ciò che viene distribuito nella parte superiore. Gli aggiornamenti delle versioni dell’AEM che si verificano dopo di che, sono frequenti e vengono applicati automaticamente. È previsto che siano compatibili con le versioni precedenti del codice cliente già distribuito.

Il resto di questo documento descrive come gli sviluppatori devono adattare le loro pratiche in modo da lavorare sia con gli aggiornamenti della versione di AEM as a Cloud Service che con gli aggiornamenti dei clienti.

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## Versioni del cliente {#customer-releases}

### Codifica rispetto alla versione AEM corretta {#coding-against-the-right-aem-version}

Per le soluzioni AEM precedenti, la versione AEM più recente veniva cambiata raramente (circa una volta all’anno con service pack trimestrali) e i clienti aggiornavano le istanze di produzione all’ultimo quickstart quando ne avevano l’occasione, facendo riferimento al jar API. Tuttavia, le applicazioni su AEM as a Cloud Service vengono aggiornate automaticamente alla versione più recente dell’AEM più spesso, pertanto il codice personalizzato per le versioni interne deve essere creato rispetto alla versione più recente dell’AEM.

Come per le versioni AEM non cloud esistenti, è supportato uno sviluppo locale offline basato su un avvio rapido specifico, che in genere dovrebbe essere lo strumento ideale per il debug.

>[!NOTE]
>Esistono sottili differenze operative tra il comportamento dell’applicazione su un computer locale e su Adobe Cloud. Queste differenze architettoniche devono essere rispettate durante lo sviluppo locale e possono portare a un comportamento diverso durante l’implementazione nell’infrastruttura cloud. A causa di queste differenze, è importante eseguire test esaustivi sugli ambienti di sviluppo e staging prima di implementare un nuovo codice personalizzato in produzione.

Per sviluppare un codice personalizzato per una versione interna, è necessario disporre della versione [SDK AS A CLOUD SERVICE AEM](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) devono essere scaricati e installati. Per ulteriori informazioni sull’utilizzo degli strumenti di Dispatcher di AEM as a Cloud Service, consulta [questa pagina](/help/implementing/dispatcher/disp-overview.md).

Il seguente video fornisce una panoramica di alto livello su come distribuire il codice in AEM as a Cloud Service:

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## Distribuzione di pacchetti di contenuti tramite Cloud Manager e Gestione pacchetti {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Distribuzioni tramite Cloud Manager {#deployments-via-cloud-manager}

<!-- Alexandru: temporarily commenting this out, until I get some clarification from Brian 

![image](https://git.corp.adobe.com/storage/user/9001/files/e91b880e-226c-4d5a-93e0-ae5c3d6685c8) -->

I clienti distribuiscono il codice personalizzato agli ambienti cloud tramite Cloud Manager. Cloud Manager trasforma i pacchetti di contenuti assemblati localmente in un artefatto conforme al modello di funzione Sling, che è il modo in cui viene descritta un’applicazione su AEM as a Cloud Service quando viene eseguita in un ambiente cloud. Di conseguenza, esaminando i pacchetti in [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) negli ambienti cloud, il nome include &quot;cp2fm&quot; e i pacchetti trasformati hanno tutti i metadati rimossi. Non è possibile interagire con questi elementi, ovvero non è possibile scaricarli, replicarli o aprirli. La documentazione dettagliata sul convertitore può essere [trovata qui](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

I pacchetti di contenuti scritti per le applicazioni su AEM as a Cloud Service devono avere una netta separazione tra contenuto immutabile e mutabile e Cloud Manager installa solo il contenuto mutabile, generando anche un messaggio come segue:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

Il resto di questa sezione descrive la composizione e le implicazioni dei pacchetti immutabili e mutabili.

### Pacchetti di contenuti immutabili {#immutabe-content-packages}

Tutti i contenuti e il codice mantenuti nell’archivio immutabile devono essere controllati in git e distribuiti tramite Cloud Manager. In altre parole, a differenza delle soluzioni AEM correnti, il codice non viene mai distribuito direttamente in un’istanza AEM in esecuzione. Questo flusso di lavoro garantisce che il codice in esecuzione per una determinata versione in qualsiasi ambiente Cloud sia identico, eliminando in tal modo il rischio di varianti non intenzionali del codice in produzione. Ad esempio, la configurazione OSGI deve essere salvata nel controllo del codice sorgente anziché gestita in fase di runtime tramite il gestore di configurazione della console web AEM.

Poiché le modifiche dell’applicazione dovute al modello di distribuzione vengono abilitate da un commutatore, non possono dipendere dalle modifiche nell’archivio mutabile, ad eccezione degli utenti del servizio, dei relativi ACL, tipi di nodo e modifiche alla definizione dell’indice.

Per i clienti con basi di codice esistenti, è fondamentale seguire l’esercizio di ristrutturazione dell’archivio descritto nella documentazione di AEM per garantire che il contenuto che si trovava in /etc venga spostato nella posizione giusta.

Per questi pacchetti di codice si applicano alcune restrizioni aggiuntive, ad esempio non è supportata l’[installazione di hook](https://jackrabbit.apache.org/filevault/installhooks.html).

## Configurazione OSGI {#osgi-configuration}

Come accennato in precedenza, la configurazione OSGI deve essere impegnata nel controllo del codice sorgente anziché attraverso la console web. Le tecniche per farlo includono:

* Apportare le modifiche necessarie nell’ambiente AEM locale dello sviluppatore con il gestore di configurazione della console web AEM, quindi esportare i risultati nel progetto AEM su file system locale
* Creare manualmente la configurazione OSGI nel progetto AEM su file system locale, facendo riferimento alla gestione della configurazione della console AEM per i nomi delle proprietà.

Ulteriori informazioni sulla configurazione OSGI in [Configurazione OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Contenuto mutabile {#mutable-content}

A volte può essere utile preparare le modifiche al contenuto nel controllo del codice sorgente in modo che possa essere distribuito da Cloud Manager ogni volta che un ambiente viene aggiornato. Ad esempio, potrebbe essere ragionevole eseguire il seeding di determinate strutture di cartelle principali. In alternativa, allinea le modifiche nei modelli modificabili per abilitare i componenti dei criteri aggiornati dalla distribuzione dell’applicazione.

Esistono due strategie per descrivere il contenuto distribuito da Cloud Manager nell’archivio mutabile, i pacchetti di contenuti mutabili e `repoinit` istruzioni.

### Pacchetti di contenuto mutabile {#mutable-content-packages}

Contenuti come gerarchie di percorsi di cartelle, utenti di servizi e controlli di accesso (ACL) vengono generalmente salvati in un progetto AEM basato su un archetipo maven. Le tecniche includono l’esportazione da AEM o la scrittura diretta come XML. Durante il processo di creazione e distribuzione, Cloud Manager crea un pacchetto con il pacchetto di contenuti mutabili risultante. Il contenuto mutabile viene installato in tre momenti diversi durante la fase di distribuzione nella pipeline:

Prima dell’avvio della nuova versione dell’applicazione:

* definizioni dell’indice (aggiungi, modifica, rimuovi)

Durante l’avvio di una nuova versione dell’applicazione, ma prima del passaggio:

* Utenti del servizio (aggiungi)
* ACL dell’utente del servizio (aggiungi)
* tipi di nodo (aggiungi)

Dopo il passaggio alla nuova versione dell’applicazione:

* Tutti gli altri contenuti definibili tramite il caveau di Jackrabbit. Esempio:
   * Cartelle (aggiungi, modifica, rimuovi)
   * Modelli modificabili (aggiungi, modifica, rimuovi)
   * Configurazione in base al contesto (qualsiasi cosa in `/conf`) (aggiungi, modifica, rimuovi)
   * Script (i pacchetti possono attivare gli hook di installazione in varie fasi del processo di installazione del pacchetto. Consulta [Documentazione di Jackrabbit filevault](https://jackrabbit.apache.org/filevault/installhooks.html) informazioni sugli hook di installazione. AEM CS utilizza attualmente Filevault versione 3.4.0, che limita gli hook di installazione agli utenti amministratori, agli utenti di sistema e ai membri del gruppo Administrators).

È possibile limitare l’installazione di contenuti mutabili all’authoring o alla pubblicazione incorporando i pacchetti in una cartella install.author o install.publish in `/apps`. La ristrutturazione per rispecchiare tale separazione è stata effettuata in AEM 6.5, e i dettagli relativi alla ristrutturazione del progetto raccomandata si trovano nella [Documentazione AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=it)

>[!NOTE]
>I pacchetti di contenuto vengono distribuiti in tutti i tipi di ambiente (dev, stage, prod). Non è possibile limitare la distribuzione a un ambiente specifico. Questa limitazione è presente per garantire la possibilità di effettuare un test di esecuzione automatica. Il contenuto specifico di un ambiente richiede l’installazione manuale tramite [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md).

Inoltre, non esiste alcun meccanismo per eseguire il rollback delle modifiche del pacchetto di contenuti mutabili dopo la loro applicazione. Se i clienti rilevano un problema, possono scegliere di correggerlo nella versione successiva del codice o, come ultima risorsa, ripristinare l’intero sistema in un punto temporale prima della distribuzione.

Eventuali pacchetti di terze parti inclusi devono essere convalidati come compatibili con AEM as a Cloud Service, altrimenti la loro inclusione si traduce in un errore di distribuzione.

Come accennato in precedenza, i clienti con basi di codice esistenti devono conformarsi all’esercizio di ristrutturazione dell’archivio necessario per le modifiche all’archivio 6.5 descritte nel [Documentazione AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=it)

## Repoinit {#repoinit}

Per i casi seguenti, è preferibile adottare l’approccio della creazione di contenuti esplicita tramite codifica manuale istruzioni `repoinit` nelle configurazioni di fabbrica OSGi:

* Creare/eliminare/disabilitare utenti del servizio
* Creare/eliminare gruppi
* Creare/eliminare utenti
* Aggiungere ACL

  >[!NOTE]
  >
  >La definizione degli ACL richiede che le strutture dei nodi siano già presenti. Pertanto, potrebbe essere necessario creare in anticipo delle istruzioni di percorso.

* Aggiungere percorso (ad esempio per le strutture delle cartelle principali)
* Aggiungere CND (definizioni dei tipi di nodo)

Repoinit è preferibile per questi casi d’uso di modifica del contenuto supportati grazie ai seguenti vantaggi:

* `Repoinit` crea risorse all’avvio in modo che la logica possa dare per scontata l’esistenza di tali risorse. Nell’approccio a pacchetti di contenuti mutabili, le risorse vengono create dopo l’avvio, pertanto il codice dell’applicazione che si basa su di esse potrebbe non riuscire.
* `Repoinit` è un set di istruzioni relativamente sicuro in quanto si controlla esplicitamente l’azione da intraprendere. Inoltre, le uniche operazioni supportate sono additive, ad eccezione di alcuni casi relativi alla sicurezza che consentono la rimozione di Utenti, Utenti servizio e Gruppi. Al contrario, la rimozione di un elemento nell’approccio del pacchetto di contenuti mutabili è esplicita; quando definisci un filtro, viene eliminato tutto ciò che è presente in un filtro. Tuttavia, è necessario prestare attenzione, in quanto con qualsiasi contenuto ci sono scenari in cui la presenza di nuovi contenuti può alterare il comportamento dell’applicazione.
* `Repoinit` esegue operazioni rapide e atomiche. I pacchetti di contenuti mutabili, al contrario, possono dipendere in modo molto efficiente dalle prestazioni delle strutture coperte da un filtro. Anche se si aggiorna un singolo nodo, è possibile creare un’istantanea di una struttura di grandi dimensioni.
* È possibile convalidare `repoinit` in un ambiente di sviluppo locale in fase di runtime perché vengono eseguite al momento della registrazione della configurazione OSGi.
* `Repoinit` Le istruzioni sono atomiche ed esplicite e vengono ignorate se lo stato è già corrispondente.

Quando Cloud Manager distribuisce l’applicazione, esegue queste istruzioni, indipendentemente dall’installazione di qualsiasi pacchetto di contenuto.

Per creare `repoinit` istruzioni, seguire la procedura seguente:

1. Aggiungi la configurazione OSGi per il PID di fabbrica `org.apache.sling.jcr.repoinit.RepositoryInitializer` in una cartella di configurazione del progetto. Usa un nome descrittivo per la configurazione come **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**.
1. Aggiungi `repoinit` istruzioni alla proprietà script della configurazione. La sintassi e le opzioni sono documentate nella [documentazione Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html). È necessario creare in modo esplicito una cartella principale prima delle relative cartelle secondarie. Ad esempio, una creazione esplicita di `/content` prima di `/content/myfolder` prima di `/content/myfolder/mysubfolder`. Per gli ACL impostati su strutture di basso livello, si consiglia di impostarli su un livello più alto e lavorare con un `rep:glob` restrizione. Esempio: `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Convalida nell’ambiente di sviluppo locale in fase di esecuzione.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>Per gli ACL definiti per i nodi sottostanti `/apps` o `/libs` il `repoinit`, l’esecuzione viene avviata su un archivio vuoto. I pacchetti vengono installati dopo `repoinit` pertanto, le istruzioni non possono basarsi su nulla definito nei pacchetti, ma devono definire i prerequisiti, come le strutture padre sottostanti.

>[!TIP]
>
>Per gli ACL, la creazione di strutture profonde potrebbe essere complicata. Pertanto, è più ragionevole definire un ACL a un livello più elevato e vincolare laddove si suppone che agisca mediante un `rep:glob` restrizione.

Maggiori dettagli su `repoinit` si trova nella sezione [Documentazione di Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Gestione pacchetti “una tantum” per pacchetti di contenuti mutabili {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="Gestione pacchetti - Migrazione dei pacchetti di contenuto mutabile"
>abstract="Scopri l’utilizzo di Gestione pacchetti per i casi di utilizzo in cui un pacchetto di contenuti deve essere installato “una tantum”. L’installazione include l’importazione di contenuto specifico dalla produzione allo staging per eseguire il debug di un problema di produzione, il trasferimento di un piccolo pacchetto di contenuti dall’ambiente on-premise agli ambienti di AEM Cloud e molto altro ancora."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=it" text="Strumento trasferimento contenuti"

Ci sono casi d’uso in cui un pacchetto di contenuti deve essere installato come “una tantum”. Ad esempio, importare contenuto specifico dalla produzione alla gestione temporanea per eseguire il debug di un problema di produzione. Per questi scenari, [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) può essere utilizzato in ambienti su AEM as a Cloud Service.

Poiché Gestione pacchetti è un concetto di esecuzione, non è possibile installare contenuto o codice nell’archivio immutabile, quindi questi pacchetti di contenuto devono essere costituiti solo da contenuto mutabile (principalmente `/content` o `/conf`). Se il pacchetto di contenuti include contenuti misti (sia contenuti mutabili che immutabili), viene installato solo il contenuto mutabile.

>[!IMPORTANT]
>
>L’interfaccia utente di Gestione pacchetti potrebbe restituire un’ **non definito** messaggio di errore se l’installazione di un pacchetto richiede più di dieci minuti.
>
>Questa ora non è dovuta a un errore nell’installazione, ma a un timeout del Cloud Service per tutte le richieste.
>
>Non ripetere l’installazione se viene visualizzato un errore di questo tipo. L’installazione sta procedendo correttamente in background. Se si riavvia l&#39;installazione, alcuni conflitti potrebbero essere introdotti da più processi di importazione simultanei.

Tutti i pacchetti di contenuti installati tramite Cloud Manager (sia mutabili che immutabili) vengono visualizzati in stato congelato nell’interfaccia utente di Gestione pacchetti AEM. Questi pacchetti non possono essere reinstallati, rigenerati o scaricati e sono elencati con un **&quot;cp2fm&quot;** suffisso, che indica che l’installazione è stata gestita da Cloud Manager.

### Inclusione di pacchetti di terze parti {#including-third-party}

È comune per i clienti includere pacchetti pregenerati da fonti di terze parti, come fornitori di software come i partner di traduzione Adobe. Si consiglia di ospitare questi pacchetti in un archivio remoto e farvi riferimento in `pom.xml`. Questo metodo è possibile per archivi pubblici e anche per archivi privati con protezione tramite password, come descritto in [archivi maven protetti da password](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

Se non è possibile memorizzare il pacchetto in un archivio remoto, i clienti possono inserire in un archivio Maven locale basato su file system, che viene impegnato in SCM come parte del progetto. Viene referenziato da qualsiasi cosa dipenda da esso. L’archivio è dichiarato nel POM del progetto come illustrato di seguito:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Tutti i pacchetti di terze parti inclusi devono rispettare le linee guida di codifica e packaging as a Cloud Service dell’AEM descritte in questo articolo, altrimenti la loro inclusione si traduce in un errore di implementazione.

Il seguente Maven `POM.xml` snippet mostra come incorporare i pacchetti di terze parti nel pacchetto &quot;Container&quot; del progetto, in genere denominato **&#39;tutto&#39;**, mediante **filevault-package-maven-plugin** Configurazione del plug-in Maven.

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

Analogamente agli aggiornamenti AEM, le versioni dei clienti vengono distribuite utilizzando una strategia di distribuzione continua per eliminare i tempi di inattività del cluster di authoring nelle circostanze appropriate. La sequenza generale di eventi è descritta di seguito, dove i nodi con la vecchia e la nuova versione del codice del cliente eseguono la stessa versione del codice AEM.

* I nodi con la versione precedente sono attivi e viene creato e reso disponibile un candidato per la nuova versione.
* In presenza di definizioni di indice nuove o aggiornate, gli indici corrispondenti vengono elaborati. I nodi con la versione precedente utilizzano sempre i vecchi indici, mentre i nodi con la nuova versione utilizzano sempre i nuovi indici.
* I nodi con la nuova versione vengono avviati, mentre le versioni precedenti continuano a gestire il traffico.
* I nodi con la versione precedente sono in esecuzione e continuano a funzionare mentre i nodi con la nuova versione vengono controllati per verificarne la disponibilità tramite controlli di integrità.
* I nodi con la nuova versione pronti, accettano il traffico e sostituiscono i nodi con la versione precedente, che viene disattivata.
* Nel tempo, i nodi con la versione precedente vengono sostituiti da nodi con la nuova versione fino a quando rimangono solo i nodi con le nuove versioni, completando in tal modo la distribuzione.
* Viene quindi distribuito qualsiasi contenuto modificabile nuovo o modificato.

## Indici {#indexes}

Gli indici nuovi o modificati causano un passaggio di indicizzazione o reindicizzazione aggiuntivo prima che la nuova versione possa assumere il traffico. I dettagli sulla gestione degli indici in AEM as a Cloud Service si trovano in questo [articolo](/help/operations/indexing.md). Puoi controllare lo stato di indicizzazione delle pagine della build in Cloud Manager e ricevere una notifica quando la nuova versione è pronta per il traffico.

>[!NOTE]
>
>Il tempo necessario per una distribuzione continua varia a seconda delle dimensioni dell’indice. Il motivo è che la nuova versione non può accettare il traffico finché non viene generato il nuovo indice.

Al momento, AEM as a Cloud Service non funziona con gli strumenti di gestione dell’indice come ACS Commons Ensure Oak Index.

## Replica {#replication}

Il meccanismo di pubblicazione è retrocompatibile con [API Java™ di replica AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it).

Per sviluppare e testare la replica con l’avvio rapido dell’AEM pronto per il cloud, è necessario utilizzare le funzionalità di replica classiche con un’impostazione di authoring/pubblicazione. Se il punto di ingresso dell’interfaccia utente in AEM Author viene rimosso per il cloud, gli utenti passano a `http://localhost:4502/etc/replication` per la configurazione.

## Codice compatibile con versioni precedenti per implementazioni continue {#backwards-compatible-code-for-rolling-deployments}

Come descritto in precedenza, la strategia di distribuzione continua di AEM as a Cloud Service implica che sia le versioni precedenti che quelle nuove possano funzionare contemporaneamente. Pertanto, presta attenzione alle modifiche del codice che non sono compatibili con la vecchia versione AEM che è ancora in esecuzione.

Inoltre, in caso di rollback, la vecchia versione deve essere verificata per verificarne la compatibilità con le nuove strutture di contenuto mutabile applicate dalla nuova versione, perché il contenuto mutabile non viene rimosso.

### Utenti del servizio e modifiche ACL {#service-users-and-acl-changes}

La modifica degli utenti del servizio, o degli ACL che accedono a contenuti o codice, potrebbe causare errori nelle versioni precedenti di AEM, con conseguente accesso a tali contenuti o codice da parte di utenti del servizio obsoleti. Per risolvere questo problema, si consiglia di applicare le modifiche in almeno due versioni, utilizzando la prima come collegamento prima di eseguire la pulizia nella versione successiva.

### Modifiche all’indice {#index-changes}

Se vengono apportate modifiche agli indici, è importante che la nuova versione continui a utilizzare i suoi indici fino a quando non viene terminata, mentre la vecchia versione utilizza il proprio set modificato di indici. Lo sviluppatore deve seguire le tecniche di gestione degli indici descritte [nel presente articolo](/help/operations/indexing.md).

### Codifica conservativa per i ripristini {#conservative-coding-for-rollbacks}

Se dopo la distribuzione viene segnalato o rilevato un errore, è possibile che sia necessario eseguire un rollback alla versione precedente. Assicurati che il nuovo codice sia compatibile con tutte le nuove strutture create dalla nuova versione, poiché non viene eseguito il rollback delle nuove strutture (eventuali contenuti mutabili). Se il vecchio codice non è compatibile, le correzioni devono essere applicate nelle versioni successive dei clienti.

## Ambienti di sviluppo rapido (RDE) {#rde}

[Ambienti di sviluppo rapido](/help/implementing/developing/introduction/rapid-development-environments.md) (o RDE in breve) consentono agli sviluppatori di implementare e rivedere rapidamente le modifiche, riducendo al minimo il tempo necessario per testare le funzionalità che sono già collaudate per funzionare in un ambiente di sviluppo locale.

A differenza degli ambienti di sviluppo regolari, che distribuiscono il codice tramite la pipeline di Cloud Manager, gli sviluppatori utilizzano strumenti della riga di comando per sincronizzare il codice da un ambiente di sviluppo locale all’RDE. Dopo aver testato correttamente le modifiche in un RDE, implementale in un ambiente di sviluppo Cloud regolare tramite la pipeline di Cloud Manager, che inserisce il codice attraverso i gate di qualità appropriati.

## Modalità di esecuzione {#runmodes}

Nelle soluzioni AEM esistenti, i clienti possono scegliere di eseguire istanze con modalità di esecuzione arbitrarie e applicare la configurazione OSGI o installare i bundle OSGI a quelle istanze specifiche. Le modalità di esecuzione definite includono solitamente il *servizio* (authoring e pubblicazione) e l’ambiente (RDE, sviluppo, staging, produzione).

AEM as a Cloud Service d’altra parte è più rigoroso su quali modalità di esecuzione sono disponibili e come i bundle OSGI e la configurazione OSGI possono essere mappati su di esse:

* Le modalità di esecuzione della configurazione OSGI devono fare riferimento a RDE, sviluppo, stage, produzione per l’ambiente o authoring, pubblicazione per il servizio. Una combinazione di `<service>.<environment_type>` viene supportato, mentre questi ambienti devono essere utilizzati in questo particolare ordine (ad esempio `author.dev` o `publish.prod`). I token OSGI devono essere referenziati direttamente dal codice anziché utilizzando `getRunModes` , che non include più il `environment_type` in fase di runtime. Per ulteriori informazioni, consulta [Configurazione OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).
* Le modalità di esecuzione dei bundle OSGI sono limitate al servizio (authoring, pubblicazione). I bundle OSGI per modalità di esecuzione devono essere installati nel pacchetto di contenuti in `install.author` o `install.publish`.

AEM as a Cloud Service non consente di utilizzare le modalità di esecuzione per installare contenuti per ambienti o servizi specifici. Se è necessario eseguire il seeding di un ambiente di sviluppo con dati o HTML che non si trovano negli ambienti di staging o produzione, è possibile utilizzare Gestione pacchetti.

Le configurazioni supportate per la modalità di esecuzione sono:

* **config** (*il valore predefinito si applica a tutti i servizi AEM*)
* **config.author** (*si applica a tutti i servizi di authoring AEM*)
* **config.author.dev** (*si applica al servizio di authoring di sviluppo AEM*)
* **config.author.rde** (*si applica al servizio di authoring AEM RDE*)
* **config.author.stage** (*si applica al servizio di authoring di staging AEM*)
* **config.author.prod** (*si applica al servizio di authoring di produzione AEM*)
* **config.publish** (*si applica al servizio di pubblicazione AEM*)
* **config.publish.dev** (*si applica al servizio di pubblicazione di sviluppo AEM*)
* **config.publish.rde** (*si applica al servizio di pubblicazione AEM RDE*)
* **config.publish.stage** (*si applica al servizio di pubblicazione di staging AEM*)
* **config.publish.prod** (*si applica al servizio di pubblicazione di produzione AEM*)
* **config.dev** (*si applica ai servizi di sviluppo AEM*)
* **config.rde** (*si applica ai servizi RDE*)
* **config.stage** (*si applica ai servizi di staging AEM*)
* **config.prod** (*si applica ai servizi di produzione AEM*)

Viene utilizzata la configurazione OSGI con le modalità di esecuzione più corrispondenti.

Quando si sviluppa localmente, un parametro di avvio in modalità di esecuzione, `-r`, viene utilizzato per specificare la configurazione OSGI in modalità di esecuzione.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Configurazione delle attività di manutenzione nel controllo del codice sorgente {#maintenance-tasks-configuration-in-source-control}

Le configurazioni delle attività di manutenzione devono essere rese persistenti nel controllo del codice sorgente perché **Strumenti > Operazioni** non è disponibile in ambienti Cloud. Questo vantaggio assicura che i cambiamenti siano intenzionalmente persistenti piuttosto che applicati e dimenticati in modo reattivo. Consulta [Articolo sull’attività di manutenzione](/help/operations/maintenance.md) per ulteriori informazioni.
