---
title: Domande frequenti su Cloud Manager
description: Trova le risposte alle domande più frequenti su Cloud Manager in AEM as a Cloud Service.
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 65632de3fbf81ef44d30994365e6365a6148b836
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Domande frequenti su Cloud Manager {#cloud-manager-faqs}

Questo documento fornisce le risposte alle domande più frequenti su Cloud Manager in AEM as a Cloud Service.

## È possibile utilizzare Java 11 con le build di Cloud Manager? {#java-11-cloud-manager}

Sì. Dovrai aggiungere il `maven-toolchains-plugin` con le impostazioni appropriate per Java 11.

Il processo è documentato [qui](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).

Ad esempio, consulta [codice progetto di esempio wknd](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

## La mia build non riesce con un errore su maven-scr-plugin dopo il passaggio da Java 8 a Java 11. Cosa posso fare? {#build-fails-maven-scr-plugin}

La build di AEM Cloud Manager potrebbe non riuscire quando si tenta di passare da Java 8 a 11. Se si verifica il seguente errore, è necessario rimuovere `maven-scr-plugin` e convertire tutte le annotazioni OSGi in annotazioni OSGi R6.

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

Per istruzioni su come rimuovere questo plug-in, vedi [qui.](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)

## La mia build non riesce con un errore su RequireJavaVersion dopo il passaggio da Java 8 a Java 11. Cosa posso fare? {#build-fails-requirejavaversion}

Per le build di Cloud Manager, l’ `maven-enforcer-plugin` può non riuscire con questo errore.

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

Si tratta di un problema noto a causa del quale Cloud Manager utilizza una versione diversa di Java per eseguire il comando maven anziché compilare il codice. omettere `requireJavaVersion` dal `maven-enforcer-plugin` configurazioni.

## Il controllo della qualità del codice non è riuscito e la distribuzione è bloccata. C&#39;è un modo per aggirare questo assegno? {#deployment-stuck}

Sì. Tutti gli errori di controllo della qualità del codice, ad eccezione della valutazione della sicurezza, sono metriche non critiche, quindi possono essere ignorati espandendo gli elementi nell&#39;interfaccia utente dei risultati.

Vedere il documento [Test della qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) per ulteriori dettagli.

## Posso usare SNAPSHOT per la versione del progetto Maven? {#use-snapshot}

Sì. Per le implementazioni per sviluppatori, il ramo git `pom.xml` i file devono contenere `-SNAPSHOT` alla fine del `<version>` valore.

Ciò consente di installare la distribuzione successiva anche se la versione non è stata modificata. Nelle implementazioni per sviluppatori, non viene aggiunta o generata alcuna versione automatica per la build Maven.

Puoi anche impostare la versione su `-SNAPSHOT` per build o implementazioni di stage e produzione. Cloud Manager imposta automaticamente un numero di versione corretto e crea un tag per te in git. Se necessario, puoi fare riferimento a questo tag in un secondo momento.

Ulteriori dettagli sulla gestione delle versioni sono [qui documentato.](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

## Come funziona il controllo delle versioni di pacchetti e bundle per le distribuzioni di stage e produzione? {#snapshot-version}

Nelle distribuzioni di stage e produzione, viene generata una versione automatica come [qui documentato.](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

Per il controllo delle versioni personalizzate nelle distribuzioni di stage e produzione, imposta una versione maven corretta in tre parti come `1.0.0`. Aumenta la versione ogni volta che distribuisci in produzione.

Cloud Manager aggiunge automaticamente la sua versione alle build di stage e produzione e crea un ramo git. Non è richiesta alcuna configurazione speciale. Se non si imposta una versione maven come descritto in precedenza, la distribuzione avrà comunque successo e verrà impostata automaticamente una versione.

## La build Maven non riesce per le implementazioni di Cloud Manager, ma viene generata localmente senza errori. Cosa c&#39;è che non va? {#maven-build-fail}

Vedi [questa risorsa git](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) per ulteriori dettagli.

## Cosa posso fare se un’implementazione di Cloud Manager non riesce al passaggio di implementazione in AEM as a Cloud Service? {#cloud-manager-deployment-cloud-service}

Il motivo più comune del mancato funzionamento di una distribuzione è dovuto a autorizzazioni insufficienti per `sling-distribution-importer` utente. In questa situazione, il passaggio di implementazione non riesce durante un’implementazione di Cloud Manager e vengono generati errori come quelli seguenti.

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

La `sling-distribution-importer` l’utente necessita di autorizzazioni aggiuntive per i percorsi di contenuto definiti nella `ui.content package`.  In genere, questo significa che devi aggiungere le autorizzazioni per entrambi `/conf` e `/var`.

La soluzione è quella di aggiungere un [Configurazione di RepositoryInitializer OSGi](/help/implementing/deploying/overview.md#repoint) script nel pacchetto di distribuzione delle app per aggiungere ACL per il `sling-distribution-importer` utente.

Nell&#39;errore precedente, il pacchetto `myapp-base.ui.content-*.zip` include il contenuto sotto `/conf` e `/var/workflow`. Affinché la distribuzione abbia successo, è necessario disporre delle autorizzazioni per `sling-distribution-importer` sotto questi percorsi è necessario.

Ecco un esempio di [`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) Configurazione OSGi che aggiunge autorizzazioni aggiuntive per `sling-distribution-importer` utente.  La configurazione aggiunge le autorizzazioni in `/var`.  Tale configurazione deve essere aggiunta al pacchetto dell&#39;applicazione in `/apps/myapp/config` (dove myapp è la cartella in cui è memorizzato il codice dell&#39;applicazione).

## L’implementazione di Cloud Manager non riesce al passaggio di distribuzione in AEM as a Cloud Service e ho già aggiunto una configurazione OSGi RepositoryInitializer. Che altro posso fare? {#build-failures}

Se [aggiunta di una configurazione OSGi RepositoryInitializer](#cloud-manager-deployment-cloud-service) l&#39;errore non è stato risolto, potrebbe essere dovuto a uno di questi problemi aggiuntivi.

* La distribuzione potrebbe non riuscire a causa di una configurazione OSGi non valida che interrompe un servizio preconfigurato.
   * Controlla i registri durante la distribuzione per vedere se ci sono errori evidenti.

* La distribuzione potrebbe non riuscire a causa di configurazioni non valide del dispatcher o di Apache.
   * Verifica le configurazioni Apache e dispatcher localmente utilizzando l’immagine Docker inclusa nell’SDK.
   * Vedi [Dispatcher nel cloud](/help/implementing/dispatcher/disp-overview.md#content-delivery) su come impostare il contenitore Docker del dispatcher per un semplice test locale.

* La distribuzione potrebbe non riuscire a causa di altri errori durante la replica dei pacchetti di contenuto (distribuzione Sling) dall’istanza di authoring alle istanze di pubblicazione.
   * Segui questi passaggi per simulare il problema su una configurazione locale.
      1. Installa un’istanza di authoring e pubblica localmente utilizzando i jar dell’SDK AEM più recenti.
      1. Accedi all’istanza di authoring.
      1. Vai a **Strumenti** -> **Distribuzione** -> **Distribuzione**.
      1. Distribuisci i pacchetti di contenuto che fanno parte della base di codice e controlla se la coda viene bloccata con un errore.

## Impossibile impostare una variabile utilizzando un comando aio. Cosa posso fare? {#set-variable}

È possibile ricevere un `403` errore come il seguente quando si tenta di elencare o impostare le variabili della pipeline tramite `aio` comandi.

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

In questo caso, l&#39;utente che esegue questi comandi deve essere aggiunto al **Gestione distribuzione** nell&#39;Admin Console.

Vedi [Autorizzazioni API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) per ulteriori dettagli.
