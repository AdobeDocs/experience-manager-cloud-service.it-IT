---
title: Implementazione in AEM as a Cloud Service
description: Scopri le nozioni di base e le best practice per la distribuzione in AEM as a Cloud Service
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
role: Admin
source-git-commit: d6c5c70e8b6565a20866d392900aef219d3fd09d
workflow-type: tm+mt
source-wordcount: '3440'
ht-degree: 93%

---

# Implementazione in AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## Introduzione {#introduction}

Le basi dello sviluppo del codice sono simili in AEM as a Cloud Service rispetto alle soluzioni AEM On Premise e Managed Services. Gli sviluppatori scrivono e testano localmente il codice, che viene quindi inviato agli ambienti AEM as a Cloud Service remoti. Cloud Manager, che era uno strumento opzionale per la distribuzione dei contenuti per Managed Services, è necessario. Questo è ora l’unico meccanismo per distribuire il codice negli ambienti di produzione, staging e sviluppo di AEM as a Cloud Service. Per la convalida rapida delle funzionalità e il debug prima della distribuzione di tali ambienti, il codice può essere sincronizzato da un ambiente locale a un [ambiente di sviluppo rapido](/help/implementing/developing/introduction/rapid-development-environments.md).

L’aggiornamento della [Versione AEM](/help/implementing/deploying/aem-version-updates.md) è sempre un evento di distribuzione separato dal push del [codice personalizzato](#customer-releases). Considerando un’altra angolazione, le versioni del codice personalizzato devono essere testate rispetto alla versione AEM produzione, in quanto è quella su cui alla fine verranno implementate. Gli aggiornamenti delle versioni di AEM che avvengono dopo di che (che sono frequenti e vengono applicati automaticamente) sono intesi per essere compatibili con le versioni precedenti del codice cliente già distribuito.

Il resto di questo documento descrive come gli sviluppatori devono adattare le proprie pratiche in modo che funzionino con gli aggiornamenti della versione di AEM as a Cloud Service e con gli aggiornamenti dei clienti.

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## Versioni del cliente {#customer-releases}

### Codifica rispetto alla versione AEM corretta {#coding-against-the-right-aem-version}

Per le soluzioni AEM precedenti, la versione AEM più recente veniva cambiata raramente (circa una volta all’anno con service pack trimestrali) e i clienti aggiornavano le istanze di produzione all’ultimo quickstart quando ne avevano l’occasione, facendo riferimento al jar API. Tuttavia, le applicazioni AEM as a Cloud Service vengono aggiornate automaticamente alla versione più recente di AEM più spesso, pertanto il codice personalizzato per le versioni interne deve essere generato in base alla versione AEM più recente.

Come per le versioni AEM non cloud esistenti, nella maggior parte dei casi sarà supportato uno sviluppo locale e offline basato su un quickstart specifico e dovrebbe essere lo strumento preferito per il debug.

>[!NOTE]
>Esistono sottili differenze operative tra il comportamento dell’applicazione su un computer locale e su Adobe Cloud. Queste differenze architettoniche devono essere rispettate durante lo sviluppo locale e possono portare a un comportamento diverso durante l’implementazione nell’infrastruttura cloud. A causa di queste differenze, è importante eseguire test esaustivi sugli ambienti di sviluppo e staging prima di implementare un nuovo codice personalizzato in produzione.

Al fine di sviluppare un codice personalizzato per una versione interna, deve essere scaricata e installata la versione pertinente di [SDK di AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md). Per ulteriori informazioni sull&#39;utilizzo degli strumenti Dispatcher di AEM as a Cloud Service, vedere [Dispatcher nel cloud](/help/implementing/dispatcher/disp-overview.md).

Il video seguente fornisce una panoramica di alto livello su come distribuire il codice in AEM as a Cloud Service:

>[!VIDEO](https://video.tv.adobe.com/v/39832?quality=9&captions=ita)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## Distribuzione di pacchetti di contenuti tramite Cloud Manager e Gestione pacchetti {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Distribuzioni tramite Cloud Manager {#deployments-via-cloud-manager}

<!-- Alexandru: temporarily commenting this out, until I get some clarification from Brian 

![image](https://git.corp.adobe.com/storage/user/9001/files/e91b880e-226c-4d5a-93e0-ae5c3d6685c8) -->

I clienti distribuiscono il codice personalizzato agli ambienti cloud tramite Cloud Manager. Cloud Manager trasforma i pacchetti di contenuto assemblati localmente in un artefatto conforme al modello di funzioni Sling. Questo è il modo in cui viene descritta un’applicazione AEM as a Cloud Service quando viene eseguita in un ambiente cloud. Di conseguenza, quando si esaminano i pacchetti in [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) negli ambienti cloud, il nome includerà “cp2fm” e nei pacchetti trasformati saranno rimossi tutti i metadati. Non è possibile interagire con questi elementi, ovvero non è possibile scaricarli, replicarli o aprirli. Per la documentazione dettagliata sul convertitore, vedere [&#128279;](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)
sling-org-apache-sling-feature-cpconverter su GitHub.

I pacchetti di contenuto scritti per le applicazioni AEM as a Cloud Service devono avere una separazione netta tra contenuto immutabile e contenuto mutabile; Cloud Manager installerà solo il contenuto mutabile, producendo anche un messaggio come:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

Il resto di questa sezione descriverà la composizione e le implicazioni dei pacchetti immutabili e mutabili.

### Pacchetti di contenuti immutabili {#immutabe-content-packages}

Tutti i contenuti e il codice mantenuti nell’archivio immutabile devono essere controllati in git e distribuiti tramite Cloud Manager. In altre parole, a differenza delle soluzioni AEM correnti, il codice non viene mai distribuito direttamente in un’istanza AEM in esecuzione. Questo flusso di lavoro assicura che il codice in esecuzione per una determinata versione in qualsiasi ambiente Cloud sia identico, eliminando il rischio di variazione involontaria del codice in produzione. Ad esempio, la configurazione OSGI deve essere impegnata nel controllo del codice sorgente anziché gestita in fase di esecuzione tramite il gestore di configurazione della console web AEM.

Poiché le modifiche dell’applicazione dovute al pattern di distribuzione sono abilitate da un interruttore, non possono dipendere dalle modifiche nell’archivio mutabile con l’eccezione degli utenti del servizio, le loro ACL, i tipi di nodo e le modifiche della definizione dell’indice.

Per i clienti con basi di codice esistenti, è fondamentale seguire l’esercizio di ristrutturazione dell’archivio descritto nella documentazione di AEM per garantire che il contenuto che si trovava in /etc venga spostato nella posizione giusta.

Per questi pacchetti di codice si applicano alcune restrizioni aggiuntive, ad esempio [hook di installazione](https://jackrabbit.apache.org/filevault/installhooks.html) non supportati.

## Configurazione OSGI {#osgi-configuration}

Come accennato in precedenza, la configurazione OSGI deve essere impegnata nel controllo del codice sorgente anziché attraverso la console web. Le tecniche per farlo includono:

* Apportare le modifiche necessarie nell’ambiente AEM locale dello sviluppatore con il gestore di configurazione della console web AEM, quindi esportare i risultati nel progetto AEM su file system locale
* Creare manualmente la configurazione OSGI nel progetto AEM su file system locale, facendo riferimento alla gestione della configurazione della console AEM per i nomi delle proprietà.

Ulteriori informazioni sulla configurazione OSGI in [Configurazione OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Contenuto mutabile {#mutable-content}

In alcuni casi potrebbe essere utile preparare le modifiche al contenuto nel controllo della sorgente, in modo che possa essere distribuito da Cloud Manager ogni volta che un ambiente viene aggiornato. Ad esempio, potrebbe essere ragionevole eseguire il seeding di determinate strutture di cartelle principali. In alternativa, allinea le modifiche nei modelli modificabili per abilitare i componenti dei criteri aggiornati dalla distribuzione dell’applicazione.

Esistono due strategie per descrivere il contenuto che verrà distribuito da Cloud Manager nell’archivio mutabile, nei pacchetti di contenuto mutabile e nelle istruzioni. `repoinit`

### Pacchetti di contenuto mutabile {#mutable-content-packages}

Contenuti come gerarchie di percorsi di cartelle, utenti di servizi e controlli di accesso (ACL) vengono generalmente salvati in un progetto AEM basato su un archetipo maven. Le tecniche includono l’esportazione da AEM o la scrittura diretta come XML. Durante il processo di creazione e distribuzione, Cloud Manager crea un pacchetto con il pacchetto di contenuti mutabili risultante. Il contenuto mutabile viene installato in momenti diversi, durante la fase di distribuzione nella pipeline:

Prima dell’avvio della nuova versione dell’applicazione:

* definizioni dell’indice (aggiungi, modifica, rimuovi)

Durante l’avvio di una nuova versione dell’applicazione, ma prima del passaggio:

* Utenti del servizio (aggiungi)
* ACL dell’utente del servizio (aggiungi)
* tipi di nodo (aggiungi)

Dopo il passaggio alla nuova versione dell’applicazione:

* Tutti gli altri contenuti definibili tramite Jackrabbit vault. Esempio:
   * Cartelle (aggiungi, modifica, rimuovi)
   * Modelli modificabili (aggiungi, modifica, rimuovi)
   * Configurazione in base al contesto (qualsiasi cosa in `/conf`) (aggiungi, modifica, rimuovi)
   * Script (i pacchetti possono attivare gli hook di installazione in varie fasi del processo di installazione del pacchetto. Consulta la [documentazione di Jackrabbit FileVault](https://jackrabbit.apache.org/filevault/installhooks.html) sugli hook di installazione. AEM CS utilizza attualmente Filevault versione 3.4.0, che limita gli hook di installazione agli utenti amministratori, agli utenti di sistema e ai membri del gruppo di amministratori).

È possibile limitare l’installazione di contenuti mutabili all’authoring o alla pubblicazione incorporando i pacchetti in una cartella install.author o install.publish in `/apps`. La ristrutturazione per riflettere questa separazione è stata eseguita in AEM 6.5 e i dettagli sulla ristrutturazione del progetto consigliata sono disponibili nella [documentazione di AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=it).

>[!NOTE]
>I pacchetti di contenuto vengono distribuiti in tutti i tipi di ambiente (dev, stage, prod). Non è possibile limitare la distribuzione a un ambiente specifico. Questa limitazione è presente per garantire la possibilità di effettuare un test di esecuzione automatica. Il contenuto specifico di un ambiente richiede l’installazione manuale tramite [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md).

Inoltre, non esiste un meccanismo per ripristinare la versione precedente dopo l’applicazione delle modifiche al pacchetto di contenuti mutabili. Se i clienti rilevano un problema, possono scegliere di correggerlo nella versione successiva del codice o, come ultima risorsa, ripristinare l’intero sistema in un punto temporale prima della distribuzione.

Eventuali pacchetti di terzi inclusi devono essere convalidati come un servizio compatibile con AEM as a Cloud, altrimenti la loro inclusione provocherà un errore di distribuzione.

Come accennato in precedenza, i clienti con basi di codice esistenti devono conformarsi all&#39;esercizio di ristrutturazione dell&#39;archivio necessario per le modifiche dell&#39;archivio 6.5 descritte nella [documentazione di AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=it).

## Repoinit {#repoinit}

Per i casi seguenti, è preferibile adottare l’approccio della creazione di contenuti esplicita tramite codifica manuale istruzioni `repoinit` nelle configurazioni di fabbrica OSGi:

* Creare/eliminare/disabilitare utenti del servizio
* Creare/eliminare gruppi
* Creare/eliminare utenti
* Aggiungere ACL

  >[!NOTE]
  >
  >La definizione degli ACL richiede che le strutture dei nodi siano già presenti. Pertanto, potrebbe essere necessario creare in anticipo delle istruzioni di percorso.

* Aggiungi percorso (ad esempio, per le strutture di cartelle principali)
* Aggiungere CND (definizioni dei tipi di nodo)

Repoinit è preferibile per questi casi d’uso di modifica del contenuto supportati grazie ai seguenti vantaggi:

* `Repoinit` crea risorse all’avvio in modo che la logica possa dare per scontata l’esistenza di tali risorse. Nell’approccio a pacchetti di contenuti mutabili, le risorse vengono create dopo l’avvio, pertanto il codice dell’applicazione che si basa su di esse potrebbe non riuscire.
* `Repoinit` è un set di istruzioni relativamente sicuro in quanto si controlla esplicitamente l’azione da intraprendere. Inoltre, le uniche operazioni supportate sono aggiuntive, fatta eccezione per alcuni casi relativi alla sicurezza che consentono la rimozione di utenti, utenti del servizo e gruppi. Al contrario, è esplicita la rimozione di qualcosa nell’approccio a pacchetti di contenuti mutabili: quando definisci un filtro, tutto ciò che è presente ed è coperto da un filtro verrà eliminato. Tuttavia, è necessario prestare attenzione, in quanto con qualsiasi contenuto ci sono scenari in cui la presenza di nuovi contenuti può alterare il comportamento dell’applicazione.
* `Repoinit` esegue operazioni rapide e atomiche. I pacchetti di contenuti mutabili, al contrario, possono dipendere in modo molto efficiente dalle prestazioni delle strutture coperte da un filtro. Anche se si aggiorna un singolo nodo, è possibile creare un’istantanea di una struttura di grandi dimensioni.
* È possibile convalidare le istruzioni `repoinit` in un ambiente di sviluppo locale in fase di esecuzione, poiché verranno eseguite quando la configurazione OSGi sarà registrata.
* Le istruzioni `Repoinit` sono atomiche ed esplicite e vengono ignorate se lo stato è già corrispondente.

Quando Cloud Manager distribuisce l’applicazione, esegue queste istruzioni, indipendentemente dall’installazione di qualsiasi pacchetto di contenuto.

Per creare istruzioni `repoinit`, segui la procedura seguente:

1. Aggiungi la configurazione OSGi per il PID di fabbrica `org.apache.sling.jcr.repoinit.RepositoryInitializer` in una cartella di configurazione del progetto. Usa un nome descrittivo per la configurazione come **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**.
1. Aggiungi le istruzioni `repoinit` alla proprietà script della configurazione. La sintassi e le opzioni sono documentate nella [documentazione Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html). È necessario creare esplicitamente una cartella principale prima delle relative cartelle secondarie. Ad esempio, una creazione esplicita di `/content` prima di `/content/myfolder` prima di `/content/myfolder/mysubfolder`. Per le ACL impostate su strutture di basso livello, si consiglia di impostarle su un livello superiore e lavorare con una restrizione `rep:glob`. Esempio: `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Convalida nell’ambiente di sviluppo locale in fase di esecuzione.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>Per ACL definiti per nodi sottostanti `/apps` o `/libs`, l’esecuzione del `repoinit` inizia su un archivio vuoto. I pacchetti vengono installati dopo `repoinit`, pertanto le istruzioni non possono basarsi su elementi definiti nei pacchetti, ma devono definire le condizioni preliminari come le strutture principali sottostanti.

>[!TIP]
>
>Per gli ACL, la creazione di strutture profonde potrebbe essere complessa. Pertanto, è più ragionevole definire un ACL a un livello più elevato e vincolare laddove si suppone che agisca mediante una restrizione `rep:glob`.

Maggiori dettagli su `repoinit` sono disponibili nella [documentazione Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Gestione pacchetti “una tantum” per pacchetti di contenuti mutabili {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="Gestione pacchetti - Migrazione dei pacchetti di contenuto mutabile"
>abstract="Scopri l’utilizzo di Gestione pacchetti per i casi di utilizzo in cui un pacchetto di contenuti deve essere installato “una tantum”. L’installazione include l’importazione di contenuto specifico dalla produzione allo staging per eseguire il debug di un problema di produzione, il trasferimento di un piccolo pacchetto di contenuti dall’ambiente on-premise agli ambienti di AEM Cloud e molto altro ancora."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=it" text="Strumento trasferimento contenuti"

Ci sono casi d’uso in cui un pacchetto di contenuti deve essere installato come “una tantum”. Ad esempio, per eseguire il debug di un problema di produzione, è necessario importare contenuto specifico dalla produzione allo staging. Per questi scenari, è possibile utilizzare la funzione [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) in ambienti AEM as a Cloud Service.

Poiché Gestione pacchetti è un concetto di esecuzione, non è possibile installare contenuto o codice nell’archivio immutabile, quindi questi pacchetti di contenuto devono essere costituiti solo da contenuto mutabile (principalmente `/content` o `/conf`). Se il pacchetto di contenuti include contenuti misti (con contenuto mutabile e immutabile), verrà installato solo il contenuto mutabile.

>[!IMPORTANT]
>
>L’interfaccia utente di Gestione pacchetti potrebbe restituire un messaggio di errore **non definito** se l’installazione di un pacchetto richiede più di dieci minuti.
>
>Questo non è dovuto a un errore nell’installazione, ma a un timeout che Cloud Service ha per tutte le richieste.
>
>Non ripetere l’installazione se viene visualizzato un errore di questo tipo. L’installazione sta procedendo correttamente in background. Se si riavvia l’installazione, è possibile che alcuni conflitti siano introdotti da più processi di importazione simultanei.

Tutti i pacchetti di contenuto installati tramite Cloud Manager (mutabili e immutabili) verranno visualizzati in uno stato congelato nell’interfaccia utente di Gestione Pacchetti AEM. Questi pacchetti non possono essere reinstallati, rigenerati o persino scaricati e verranno elencati con un suffisso **“cp2fm”** che indica che l’installazione è stata gestita da Cloud Manager.

### Inclusione di pacchetti di terzi {#including-third-party}

È comune per la clientela includere pacchetti predefiniti da fonti terze, ad esempio fornitori di software come i partner di traduzione di Adobe. Si consiglia di ospitare questi pacchetti in un archivio remoto e farvi riferimento in `pom.xml`. Questo è possibile per gli archivi pubblici e anche per quelli privati con protezione tramite password, come descritto in [archivi maven protetti da password](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

Se non è possibile memorizzare il pacchetto in un archivio remoto, i clienti possono inserirlo in un archivio Maven locale basato su file system, che è impegnato in SCM come parte del progetto. Viene referenziato da qualsiasi cosa dipenda da esso. L’archivio viene dichiarato nel pom del progetto come illustrato di seguito:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Tutti i pacchetti di terze parti inclusi devono essere conformi alle linee guida per la codifica dei servizi e la creazione di pacchetti di AEM as a Cloud descritte nel presente articolo, altrimenti la loro inclusione provocherà un errore di distribuzione.

Il seguente `POM.xml` snippet Maven mostra come incorporare i pacchetti di terze parti nel pacchetto “Contenitore” del progetto, in genere denominato **“tutti”**, tramite la configurazione del plug-in maven **filevault-package-maven-plugin**.

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

Come per gli aggiornamenti AEM, le versioni dei clienti e delle clienti vengono distribuite utilizzando una strategia di distribuzione continua per eliminare i tempi di inattività dei cluster di authoring nelle giuste circostanze. La sequenza generale di eventi è descritta di seguito, dove i nodi con la versione precedente e nuova del codice del cliente eseguono la stessa versione del codice AEM.

* I nodi con la versione precedente sono attivi e viene creato e reso disponibile un candidato per la nuova versione.
* In presenza di definizioni di indice nuove o aggiornate, gli indici corrispondenti vengono elaborati. I nodi con la versione precedente utilizzeranno sempre gli indici precedenti, mentre i nodi con la nuova versione utilizzeranno sempre i nuovi indici.
* I nodi con la nuova versione si avviano, mentre le versioni precedenti continuano a servire il traffico.
* I nodi con la versione precedente sono in esecuzione e continuano a servire, mentre i nodi con la nuova versione vengono controllati per verificarne la disponibilità tramite controlli di integrità.
* I nodi con la nuova versione che sono pronti accetteranno il traffico e sostituiranno i nodi con la versione precedente, che viene disattivata.
* Nel corso del tempo, i nodi con la versione precedente vengono sostituiti dai nodi con la nuova versione, finché non rimarranno solo i nodi con le nuove versioni, completando in tal modo la distribuzione.
* Vengono così distribuiti eventuali contenuti mutabili nuovi o modificati.

## Indici {#indexes}

Gli indici nuovi o modificati causeranno un ulteriore passaggio di indicizzazione o reindicizzazione prima che la nuova versione possa assumere traffico. I dettagli sulla gestione degli indici in AEM as a Cloud Service sono disponibili in [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md). Puoi controllare lo stato di indicizzazione delle pagine della build in Cloud Manager e ricevere una notifica quando la nuova versione è pronta per il traffico.

>[!NOTE]
>
>Il tempo necessario per una distribuzione continua varia a seconda delle dimensioni dell’indice. Il motivo è che la nuova versione non può accettare il traffico finché non viene generato il nuovo indice.

Al momento, AEM as a Cloud Service non funziona con strumenti di gestione degli indici come lo strumento indice Oak di ACS Commons Ensure.

## Replica {#replication}

Il meccanismo di pubblicazione è retrocompatibile con le [API Java™ di replica di AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it).

Per sviluppare e testare tramite la replica con l’avvio rapido di AEM cloud ready, le funzionalità di replica classica devono essere utilizzate con un’impostazione di Authoring/Pubblicazione. Se il punto di ingresso dell’interfaccia utente in AEM Author viene rimosso per il cloud, gli utenti passano a `http://localhost:4502/etc/replication` per la configurazione.

## Codice compatibile con versioni precedenti per implementazioni continue {#backwards-compatible-code-for-rolling-deployments}

Come descritto in precedenza, la strategia di distribuzione continua di AEM as a Cloud Service implica che sia le versioni precedenti che quelle nuove possano funzionare contemporaneamente. Pertanto, presta attenzione alle modifiche del codice che non sono compatibili con la vecchia versione AEM che è ancora in esecuzione.

Inoltre, la vecchia versione deve essere testata per verificare la compatibilità con eventuali nuove strutture di contenuto mutabile applicate dalla nuova versione in caso di ripristino, in quanto il contenuto mutabile non viene rimosso.

### Utenti del servizio e modifiche ACL {#service-users-and-acl-changes}

La modifica degli utenti del servizio o delle ACL necessarie per accedere al contenuto o al codice potrebbe causare errori nelle versioni precedenti di AEM e causare l’accesso a tale contenuto o codice con utenti del servizio obsoleti. Per risolvere questo problema, la raccomandazione consiste nell’apportare modifiche distribuite su almeno due versioni, con la prima versione che funge da ponte prima di essere ripulita nella versione successiva.

### Modifiche all’indice {#index-changes}

Se vengono apportate modifiche agli indici, è importante che la vecchia versione continui a utilizzare i suoi indici fino a quando non viene terminata, mentre la nuova versione utilizza il proprio set modificato di indici. Lo sviluppatore deve seguire le tecniche di gestione dell&#39;indice descritte in [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md).

### Codifica conservativa per i ripristini {#conservative-coding-for-rollbacks}

Se viene segnalato o rilevato un errore dopo la distribuzione, è possibile che sia necessario eseguire il ripristino della versione precedente. È consigliato garantire che il nuovo codice sia compatibile con tutte le nuove strutture create dalla nuova versione, in quanto le nuove strutture (qualsiasi contenuto mutabile) non subiranno ripristini. Se il codice precedente non è compatibile, le correzioni dovranno essere applicate nelle versioni successive del cliente.

## Ambienti di sviluppo rapido (RDE) {#rde}

Gli [ambienti di sviluppo rapido](/help/implementing/developing/introduction/rapid-development-environments.md) (o RDE in breve) consentono agli sviluppatori di distribuire e rivedere rapidamente le modifiche, riducendo al minimo il tempo necessario per testare le funzionalità che sono già collaudate per funzionare in un ambiente di sviluppo locale.

A differenza degli ambienti di sviluppo regolari, che distribuiscono il codice tramite la pipeline di Cloud Manager, gli sviluppatori utilizzano gli strumenti della riga di comando per sincronizzare il codice da un ambiente di sviluppo locale agli RDE. Dopo aver testato correttamente le modifiche in un RDE, implementale in un ambiente di sviluppo Cloud regolare tramite la pipeline di Cloud Manager, che inserisce il codice attraverso i gate di qualità appropriati.

## Modalità di esecuzione {#runmodes}

Nelle soluzioni AEM esistenti, i clienti possono scegliere di eseguire istanze con modalità di esecuzione arbitrarie e applicare la configurazione OSGI o installare i bundle OSGI a quelle istanze specifiche. Le modalità di esecuzione definite includono solitamente il *servizio* (authoring e pubblicazione) e l’ambiente (RDE, sviluppo, staging, produzione).

AEM as a Cloud Service d’altra parte è più rigoroso su quali modalità di esecuzione sono disponibili e come i bundle OSGI e la configurazione OSGI possono essere mappati su di esse:

* Le modalità di esecuzione della configurazione OSGI devono fare riferimento ad ambienti RDE, di sviluppo, di staging o di produzione, oppure a servizi di authoring o pubblicazione. È supportata una combinazione di `<service>.<environment_type>`, mentre questi ambienti devono essere utilizzati in questo particolare ordine (ad esempio, `author.dev` o `publish.prod`). I token OSGI devono essere referenziati direttamente dal codice anziché utilizzando il metodo `getRunModes`, che non include più `environment_type` in fase di esecuzione. Per ulteriori informazioni, consulta [Configurazione OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).
* Le modalità di esecuzione dei bundle OSGI sono limitate al servizio (authoring, pubblicazione). I bundle OSGI per modalità di esecuzione devono essere installati nel pacchetto di contenuti in `install.author` o `install.publish`.

AEM as a Cloud Service non consente di utilizzare le modalità di esecuzione per installare contenuti per ambienti o servizi specifici. Se è necessario impostare un ambiente di sviluppo con dati o HTML non presenti negli ambienti di staging o di produzione: è possibile utilizzare Gestione pacchetti.

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

Viene utilizzata la configurazione OSGI dotata di modalità di esecuzione che hanno maggiore corrispondenza.

Quando viene sviluppato localmente, un parametro di avvio in modalità di esecuzione, `-r`, viene utilizzato per specificare la configurazione OSGI in modalità di esecuzione.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Configurazione delle attività di manutenzione nel controllo del codice sorgente {#maintenance-tasks-configuration-in-source-control}

Le configurazioni delle attività di manutenzione devono essere persistenti nel controllo del codice sorgente, poiché la schermata **Strumenti > Operazioni** non sarà più disponibile negli ambienti Cloud. Questo vantaggio assicura che i cambiamenti siano persistenti intenzionalmente piuttosto che applicati e dimenticati in modo reattivo. Per ulteriori informazioni, vedere [Attività di manutenzione in AEM as a Cloud Service](/help/operations/maintenance.md).
