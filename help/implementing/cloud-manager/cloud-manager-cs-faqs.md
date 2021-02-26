---
title: Cloud Manager - Domande frequenti sugli Cloud Services
seo-title: Domande frequenti su Cloud Manager
description: Consulta le domande frequenti su Cloud Manager per Cloud Services per ottenere alcuni suggerimenti per la risoluzione dei problemi
seo-description: Segui questa pagina per ottenere le risposte su Cloud Manager - Domande frequenti sugli Cloud Services
translation-type: tm+mt
source-git-commit: 75a5ff02e5f7c0e0e3ba42c8559851d3c98c3c8d
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# Domande frequenti su Cloud Manager {#cloud-manager-faqs}

La sezione seguente contiene le risposte alle domande frequenti relative a Cloud Manager per Cloud Services.

## È possibile utilizzare Java 11 con le build di Cloud Manager? {#java-11-cloud-manager}

AEM build Cloud Manager non riesce quando si tenta di passare da Java 8 a 11. Il problema può avere molte cause e la maggior parte delle cause più comuni sono documentati di seguito:

* Aggiungete il maven-toolchain-plugin con le impostazioni corrette per Java 11 come documentato [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started).  Ad esempio, vedere il [codice del progetto di esempio wknd](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Se si verifica l&#39;errore riportato di seguito, è necessario rimuovere l&#39;uso di `maven-scr-plugin` e convertire tutte le annotazioni OSGi in annotazioni OSGi R6. Per istruzioni, vedere [qui](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Per le build di Cloud Manager, il plug-in maven per l&#39;applicazione non riesce con l&#39;errore `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Si tratta di un problema noto a causa del quale Cloud Manager utilizza una versione diversa di Java per eseguire il comando maven invece di compilare il codice. Per il momento, omettete `requireJavaVersion` dalle configurazioni del plug-in &quot;maven-esecuter&quot;.

## La nostra distribuzione è bloccata perché il controllo Qualità codice non è riuscito. C&#39;è un modo per aggirare questo assegno? {#deployment-stuck}

Tutti gli errori di qualità del codice, tranne *Valutazione sicurezza*, sono metriche non critiche, pertanto possono essere ignorate espandendo gli elementi nell&#39;interfaccia utente dei risultati.

Un utente con il ruolo [Gestione distribuzione, Project Manager o Business Owner](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements) può ignorare i problemi, nel qual caso la pipeline procede o possono accettare i problemi, nel qual caso la pipeline si interrompe con un errore.  Per ulteriori informazioni, vedere [Porte a tre livelli durante l&#39;esecuzione di una tubazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use).


## Siamo autorizzati a usare SNAPSHOT nella versione del progetto Maven? In che modo funziona il controllo delle versioni dei pacchetti e dei file JAR dei bundle per le distribuzioni di fase e produzione? {#snapshot-version}

Per informazioni sul controllo delle versioni dei pacchetti e dei file JAR per le distribuzioni di fase e produzione, fare riferimento agli scenari seguenti:

1. Per le implementazioni degli sviluppatori, i file del ramo Git `pom.xml` devono contenere `-SNAPSHOT` alla fine del valore `<version>`. Questo consente la distribuzione successiva in cui la versione non viene modificata per essere ancora installata. Nelle distribuzioni per gli sviluppatori, non viene aggiunta o generata alcuna versione automatica per la build Paradiso.

1. Nella distribuzione Stage e Produzione, viene generata una versione automatica come documentato [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code).

1. Per le versioni personalizzate nelle distribuzioni di fase e produzione, impostate una versione pari a 3 parti come `1.0.0`. Aumentate la versione ogni volta che dovete eseguire un&#39;altra distribuzione in produzione.

1. Cloud Manager aggiunge automaticamente la propria versione alle build di Stage e Produzione e crea anche un ramo Git. Non è richiesta alcuna configurazione speciale. Se si ignora il passaggio 3, la distribuzione funzionerebbe comunque correttamente e verrebbe automaticamente impostata una versione.

1. Se lasciate la versione con `-SNAPSHOT` per le build o le distribuzioni di fase e produzione, non si verificano problemi. Cloud Manager imposta automaticamente un numero di versione corretto e crea un tag per voi in Git. Se necessario, potete fare riferimento a questo tag in un secondo momento.

1. Se si desidera provare un codice sperimentale sull&#39;ambiente di sviluppo, è possibile creare un nuovo ramo Git e impostare la pipeline in modo che utilizzi quel ramo diverso. Questa funzione è utile quando le distribuzioni iniziano a non funzionare e si desidera eseguire il test con versioni precedenti del codice per vedere quando si è interrotta.

   Il comando Git di seguito crea un ramo remoto denominato *testbranch1* rispetto a un commit preesistente specifico `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  Questo ramo speciale può essere utilizzato in Cloud Manager senza influenzare altri rami:

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   Per ulteriori informazioni, consultare la [documentazione Git](https://git-scm.com/book/en/v2/Git-Internals-Git-References).

   Se si desidera eliminare il ramo test in un secondo momento, utilizzare il comando delete:

   `git push origin --delete testbranch1`

## La build Maven non riesce nelle installazioni di Cloud Manager, ma viene generata localmente senza errori. Come eseguire il debug? {#maven-build-fail}

Per ulteriori informazioni, vedere [Git Resource](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md).

## Cosa fare se la distribuzione di Cloud Manager non riesce nel passaggio di distribuzione in AEM come ambiente di Cloud Service? {#cloud-manager-deployment-cloud-service}

Il motivo più comune per cui la distribuzione non riesce è dovuto a autorizzazioni insufficienti per l&#39;utente *sling-distribution-importer*.
Per comprendere un problema, una causa e una soluzione, fare riferimento all&#39;esempio seguente:

****
ProblemaDurante la distribuzione di Cloud Manager in AEM come ambienti di Cloud Service, il passaggio di distribuzione non riesce e si verificano errori come quelli riportati di seguito.

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**Causa**

L&#39;utente di sling-distribution-importer necessita di autorizzazioni aggiuntive per i percorsi di contenuto definiti nel pacchetto ui.content.  Ciò significa che in genere è necessario aggiungere autorizzazioni sia per /conf che per /var.

****
SoluzioneLa soluzione consiste nell&#39;aggiungere uno script di  [configurazione OSGi ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying) RepositoryInitializer al pacchetto di distribuzione delle app per aggiungere ACL per l&#39;utente di sling-distribution-importer.
Nell&#39;errore di esempio riportato sopra, il pacchetto myapp-base.ui.content-*.zip include contenuto in `/conf` e `/var/workflow`. Affinché la distribuzione non abbia esito negativo, è necessario aggiungere autorizzazioni per l&#39;importazione sling-distribution in tali percorsi.
Di seguito è riportato un esempio [org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) di una configurazione OSGi di questo tipo che aggiunge autorizzazioni aggiuntive per l&#39;utente sling-distribution-importer.  Questa configurazione aggiunge le autorizzazioni in /var.  Questo file xml sotto [1] deve essere aggiunto al pacchetto dell&#39;applicazione in `/apps/myapp/config` (dove myapp è la cartella in cui è memorizzato il codice dell&#39;applicazione).
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. Se la causa non è *sling-distribution-importer*, la distribuzione potrebbe non riuscire a causa di una configurazione OSGi non valida che interrompe un servizio box. Controllate i registri durante la distribuzione per verificare se sono presenti errori evidenti.

1. La distribuzione potrebbe non riuscire a causa di configurazioni di dispatcher o apache non valide. Verifica le configurazioni Apache e Dispatcher localmente utilizzando l&#39;immagine Docker inclusa nell&#39;SDK. Vedere [Dispatcher in Cloud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery) su come impostare il contenitore del dispatcher Docker per semplificare i test locali.

1. La distribuzione potrebbe non riuscire a causa di altri errori durante la replica dei pacchetti di contenuto (distribuzione sling) dalle istanze di creazione a pubblicazione.

   Per simulare il problema in una configurazione locale, fare riferimento alla procedura seguente:

   * Installare un&#39;istanza Author e Publish (autore e pubblicazione) (utilizzando le barre SDK AEM più recenti)
   * Accedere all&#39;istanza Author
   * Vai a **Strumenti** -> **Distribuzione** -> **Distribuzione**
   * Distribuire i pacchetti di contenuto che fanno parte della base di codice e verificare se la coda viene bloccata con un errore

## Impossibile impostare una variabile tramite le variabili della pipeline impostate da aio cloud manager. Come risolvere questi problemi? {#set-variable}

Se viene visualizzato un errore `403` durante il tentativo di elencare o impostare le variabili della pipeline tramite comandi simili a quelli riportati di seguito, è necessario aggiungere il ruolo di prodotto *Gestione distribuzione* Cloud Manager nel Admin Console .\
Per ulteriori informazioni, consultate [Autorizzazioni API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md).

Comandi ed errori correlati:

`$ aio cloudmanager:list-pipeline-variables 222`

*Errore*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*Errore*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*Errore*:  `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
