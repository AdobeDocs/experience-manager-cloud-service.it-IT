---
title: Cloud Manager - Domande frequenti sui Cloud Services
seo-title: Cloud Manager FAQs
description: Fai riferimento a Cloud Manager per le domande frequenti sui Cloud Services per ricevere alcuni suggerimenti sulla risoluzione dei problemi
seo-description: Follow this page to get answers on Cloud Manager - Cloud Services FAQs
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 1%

---

# Domande frequenti su Cloud Manager {#cloud-manager-faqs}

La sezione seguente fornisce le risposte alle domande frequenti relative a Cloud Manager per Cloud Services.

## È possibile utilizzare Java 11 con le build di Cloud Manager? {#java-11-cloud-manager}

La build di AEM Cloud Manager non riesce quando si tenta di passare da Java 8 a 11. Il problema può avere molte cause e la maggior parte delle cause comuni sono documentate di seguito:

* Aggiungi il maven-toolchains-plugin con le impostazioni corrette per Java 11 come documentato [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started).  Ad esempio, consulta [codice progetto di esempio wknd](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Se incontri l&#39;errore qui sotto, devi rimuovere l&#39;uso di `maven-scr-plugin` e convertire tutte le annotazioni OSGi in annotazioni OSGi R6. Per istruzioni, consulta [qui](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Per le build di Cloud Manager, il plug-in maven per l’applicazione non riesce e viene restituito un errore. `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Si tratta di un problema noto a causa del quale Cloud Manager utilizza una versione diversa di Java per eseguire il comando maven anziché compilare il codice. Per il momento, ometti `requireJavaVersion` dalle configurazioni maven-enforcer-plugin.

## La distribuzione è bloccata perché il controllo della qualità del codice non è riuscito. C&#39;è un modo per aggirare questo assegno? {#deployment-stuck}

Tutti gli errori relativi alla qualità del codice tranne *Valutazione della sicurezza* sono metriche non critiche, in modo che possano essere ignorate espandendo gli elementi nell’interfaccia utente dei risultati.

Un utente con [Responsabile distribuzione, Project Manager o Proprietario business](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements) Il ruolo può ignorare i problemi, nel qual caso la pipeline procede o può accettare i problemi, nel qual caso la pipeline si interrompe con un errore.  Vedi [Cancelli a tre livelli durante l’esecuzione di una pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) per ulteriori dettagli.


## Siamo autorizzati a utilizzare SNAPSHOT nella versione del progetto Maven? Come funziona il controllo delle versioni dei pacchetti e dei file jar dei bundle per le implementazioni di Stage e Production? {#snapshot-version}

Per informazioni sul controllo delle versioni dei pacchetti e dei file jar dei bundle per le distribuzioni di Stage e Production, consulta i seguenti scenari:

1. Per le implementazioni per sviluppatori, il ramo Git `pom.xml` i file devono contenere `-SNAPSHOT` alla fine del `<version>` valore. Questo consente la distribuzione successiva in cui la versione non viene modificata per essere comunque installata. Nelle implementazioni per sviluppatori, non viene aggiunta o generata alcuna versione automatica per la build Maven.

1. Nella distribuzione Stage e Production viene generata una versione automatica come documentato [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code).

1. Per il controllo delle versioni personalizzate nelle implementazioni Stage e Produzione, imposta una versione maven corretta in 3 parti come `1.0.0`. Aumenta la versione ogni volta che devi eseguire un’altra implementazione in produzione.

1. Cloud Manager aggiunge automaticamente la propria versione alle build di Stage e Production e crea persino un ramo Git. Non è richiesta alcuna configurazione speciale. Se si salta il passaggio 3, la distribuzione funzionerà comunque correttamente e verrà impostata automaticamente una versione.

1. Non ci sono problemi, se lasci la versione con `-SNAPSHOT` per build o implementazioni di Stage e Production. Cloud Manager imposta automaticamente un numero di versione corretto e crea un tag per te in Git. Se necessario, puoi fare riferimento a questo tag in un secondo momento.

1. Se desideri provare un codice sperimentale nell’ambiente di sviluppo, puoi creare un nuovo ramo Git e impostare la pipeline in modo che utilizzi tale ramo diverso. Questo è utile quando le distribuzioni iniziano a non funzionare e desideri testare con le versioni precedenti del codice per vedere quando si è verificato un errore.

   Il comando Git seguente crea un ramo remoto denominato *testbranch1* contro un commit preesistente specifico `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  Questo ramo speciale può essere utilizzato in Cloud Manager senza influenzare altri rami:

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   Consulta la sezione [Documentazione Git](https://git-scm.com/book/en/v2/Git-Internals-Git-References) per ulteriori dettagli.

   Se desideri eliminare il ramo di test in un secondo momento, utilizza il comando delete :

   `git push origin --delete testbranch1`

## La build Maven non riesce nelle implementazioni di Cloud Manager, ma viene generata localmente senza errori. Come eseguire il debug? {#maven-build-fail}

Vedi [Risorsa Git](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) per ulteriori dettagli.

## Cosa fare se l’implementazione di Cloud Manager non riesce al passaggio di implementazione in AEM ambiente as a Cloud Service? {#cloud-manager-deployment-cloud-service}

Il motivo più comune per il mancato funzionamento delle implementazioni è dovuto a autorizzazioni insufficienti per *sling-distribution-importer* utente.
Fai riferimento all’esempio seguente per comprendere un problema, una causa e una soluzione:

**Problema**
Durante l’implementazione di Cloud Manager in ambienti as a Cloud Service, il passaggio di implementazione non riesce e si verificano errori come quelli riportati di seguito.

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**Causa**

L’utente sling-distribution-importer necessita di autorizzazioni aggiuntive in base ai percorsi di contenuto definiti nel pacchetto ui.content.  Questo solitamente significa che abbiamo bisogno di aggiungere autorizzazioni sia per /conf che per /var.

**Soluzione**
La soluzione a questo problema è aggiungere un [Configurazione di RepositoryInitializer OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=it#deploying) script sul pacchetto di distribuzione delle app per aggiungere ACL per l&#39;utente sling-distribution-importer.
Nell’errore di esempio riportato sopra, il pacchetto myapp-base.ui.content-*.zip include il contenuto sotto `/conf` e `/var/workflow`. Affinché la distribuzione non abbia esito negativo, è necessario aggiungere le autorizzazioni per sling-distribution-importer per tali percorsi.
Ecco un esempio [org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) di una configurazione OSGi di questo tipo che aggiunge autorizzazioni aggiuntive per l’utente sling-distribution-importer.  Questa configurazione aggiunge le autorizzazioni in /var.  Questo file xml qui sotto [1] deve essere aggiunto al pacchetto dell&#39;applicazione in `/apps/myapp/config` (dove myapp è la cartella in cui è memorizzato il codice dell&#39;applicazione).
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. Se la *sling-distribution-importer* non è la causa, quindi la distribuzione potrebbe non riuscire a causa di una configurazione OSGi non valida che interrompe un servizio preconfigurato. Controlla i registri durante la distribuzione per vedere se ci sono errori evidenti.

1. La distribuzione potrebbe non riuscire a causa di configurazioni del dispatcher o di Apache non valide. Verifica le configurazioni Apache e Dispatcher localmente utilizzando l’immagine Docker inclusa nell’SDK. Vedi [Dispatcher nel cloud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery) su come impostare il contenitore Docker del dispatcher per un semplice test locale.

1. La distribuzione potrebbe non riuscire a causa di altri errori durante la replica dei pacchetti di contenuto (distribuzione sling) dall’istanza di authoring alle istanze di pubblicazione.

   Fare riferimento ai passaggi seguenti per simulare questa situazione in un&#39;impostazione locale:

   * Installa un&#39;istanza Author e Publish (utilizzando i jar dell&#39;SDK AEM più recenti)
   * Accedi all’istanza Author
   * Vai a **Strumenti** -> **Distribuzione** -> **Distribuzione**
   * Distribuisci i pacchetti di contenuto che fanno parte della base di codice e controlla se la coda viene bloccata con un errore

## Impossibile impostare una variabile tramite variabili della pipeline impostate da aio cloud manager. Come eseguire il debug di questi problemi? {#set-variable}

Se ottieni un `403` errore quando si tenta di elencare o impostare le variabili della pipeline tramite comandi simili a quelli riportati di seguito, è necessario aggiungere come *Gestione distribuzione* Ruolo di prodotto di Cloud Manager nell’Admin Console.\
Vedi [Autorizzazioni API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) per ulteriori dettagli.

Comandi ed errori correlati:

`$ aio cloudmanager:list-pipeline-variables 222`

*Errore*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*Errore*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*Errore*: `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
