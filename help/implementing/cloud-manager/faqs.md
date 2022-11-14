---
title: Domande frequenti su Cloud Manager
description: Raccolta di risposte alle domande più frequenti su Cloud Manager in AEM as a Cloud Service.
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 698ea704d821d26067e29a89b562388d7517772e
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 100%

---


# Domande frequenti su Cloud Manager {#cloud-manager-faqs}

Questo documento fornisce le risposte alle domande più frequenti su Cloud Manager in AEM as a Cloud Service.

## È possibile utilizzare Java 11 con le build di Cloud Manager? {#java-11-cloud-manager}

Sì. È necessario aggiungere il `maven-toolchains-plugin` con le impostazioni corrette per Java 11.

Il processo è documentato [qui](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).

Ad esempio, consulta il [codice del progetto di esempio WKND](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

## Dopo il passaggio da Java 8 a Java 11, l’esecuzione della build non riesce e genera un errore relativo a maven-scr-plugin. Cosa posso fare? {#build-fails-maven-scr-plugin}

La build di AEM Cloud Manager potrebbe non riuscire durante il tentativo di passaggio da Java 8 a 11. Se riscontri il seguente errore, rimuovi `maven-scr-plugin` e converti tutte le annotazioni OSGi in annotazioni OSGi R6.

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

Per istruzioni su come rimuovere questo plug-in, vedi [qui.](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)

## Dopo il passaggio da Java 8 a Java 11, l’esecuzione della build non riesce e genera un errore relativo a RequireJavaVersion. Cosa posso fare? {#build-fails-requirejavaversion}

Per le build di Cloud Manager è possibile che l’esecuzione di `maven-enforcer-plugin` non riesca e generi questo errore.

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

Si tratta di un problema noto dovuto al fatto che Cloud Manager utilizza una versione diversa di Java per eseguire il comando maven e per la compilazione del codice. È sufficiente omettere `requireJavaVersion` dalle configurazioni `maven-enforcer-plugin`.

## Il controllo di qualità del codice non è riuscito e la distribuzione è bloccata. C’è un modo per aggirare questo controllo? {#deployment-stuck}

Sì. Tutti gli errori generati dal controllo di qualità del codice, a eccezione della valutazione di sicurezza, riguardano metriche non critiche e possono pertanto essere ignorati come parte di una pipeline di distribuzione espandendo gli elementi nell’interfaccia utente dei risultati.

L’utente con il ruolo [Responsabile dell’implementazione, Responsabile del progetto o Proprietario business](/help/onboarding/aem-cs-team-product-profiles.md#cloud-manager-product-profiles) può ignorare i problemi (facendo in tal caso procedere la pipeline) o accettarli (causando in tal caso l’arresto della pipeline con un errore).

Per ulteriori informazioni, consulta i documenti [Test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md#three-tiered-gate) e [Configurazione delle pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#non-production-pipelines).

## Posso usare SNAPSHOT per la versione del progetto Maven? {#use-snapshot}

Sì. Per le distribuzioni nell’ambiente di sviluppo, i file `pom.xml` del ramo Git devono contenere `-SNAPSHOT` dopo il valore `<version>`.

Ciò consente di installare la distribuzione successiva anche se la versione non è stata modificata. Per le distribuzioni nell’ambiente di sviluppo, non viene aggiunta né generata una versione automatica della build Maven.

È possibile impostare la versione su `-SNAPSHOT` per le build o le implementazioni negli ambienti di staging e produzione. Cloud Manager imposta automaticamente un numero di versione corretto e crea un tag in Git per l’utente. Se necessario, puoi fare riferimento a questo tag in un secondo momento.

Ulteriori informazioni sulla gestione delle versioni sono consultabili [qui.](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

## Come funziona il controllo delle versioni di pacchetti e bundle per le distribuzioni negli ambienti di staging e produzione? {#snapshot-version}

Per le distribuzioni negli ambienti di staging e produzione viene generata una versione automatica, come [documentato qui.](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

Per il controllo delle versioni personalizzato per le distribuzioni negli ambienti di staging e produzione, imposta una versione Maven in tre parti appropriata, come ad esempio `1.0.0`. Aumenta il numero della versione per ogni esecuzione della distribuzione nell’ambiente di produzione.

Cloud Manager aggiunge automaticamente la versione alle build di staging e produzione e crea un ramo Git. Non è richiesta alcuna configurazione speciale. Se non imposti una versione Maven come descritto in precedenza, la distribuzione verrà comunque eseguita correttamente e verrà impostata automaticamente una versione.

## L’esecuzione della build Maven non riesce per le distribuzioni di Cloud Manager, ma a livello locale non genera errori. Qual è il problema? {#maven-build-fail}

Per ulteriori informazioni, fai riferimento a [questa risorsa Git](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md).

## Cosa posso fare se l’esecuzione di una distribuzione di Cloud Manager non riesce al passaggio di distribuzione in AEM as a Cloud Service? {#cloud-manager-deployment-cloud-service}

Il motivo più comune che causa la mancata esecuzione di una distribuzione è l’assenza di autorizzazioni sufficienti dell’utente `sling-distribution-importer`. In questa situazione, il passaggio di distribuzione durante una distribuzione di Cloud Manager non riesce e vengono generati errori come quelli indicati di seguito.

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

L’utente `sling-distribution-importer` deve disporre di autorizzazioni aggiuntive per i percorsi contenuto definiti in `ui.content package`. In genere, questo significa che è necessario aggiungere le autorizzazioni per `/conf` e `/var`.

La soluzione per aggiungere gli elenchi di controllo accesso (ACL) per l’utente `sling-distribution-importer` è aggiungere uno script di [configurazione OSGi RepositoryInitializer](/help/implementing/deploying/overview.md#repoint) nel pacchetto di distribuzione delle app.

Nell’errore precedente, il pacchetto `myapp-base.ui.content-*.zip` include contenuti in `/conf` e `/var/workflow`. Affinché la distribuzione venga eseguita correttamente, è necessario che `sling-distribution-importer` disponga delle autorizzazioni in questi percorsi.

Di seguito è riportato un esempio di [`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) configurazione OSGi che consente di aggiungere ulteriori autorizzazioni per l’utente `sling-distribution-importer`. La configurazione aggiunge le autorizzazioni in `/var`. Tale configurazione deve essere aggiunta al pacchetto dell’applicazione in `/apps/myapp/config` (dove myapp è la cartella in cui è archiviato il codice dell’applicazione).

## L’esecuzione della distribuzione di Cloud Manager non riesce al passaggio di distribuzione in AEM as a Cloud Service e ho già aggiunto una configurazione OSGi RepositoryInitializer. Che altro posso fare? {#build-failures}

Se [aggiungendo una configurazione OSGi RepositoryInitializer](#cloud-manager-deployment-cloud-service) non hai risolto l’errore, la causa potrebbe essere uno di questi ulteriori problemi.

* La distribuzione potrebbe non riuscire a causa di una configurazione OSGi non valida che interrompe un servizio preconfigurato.
   * Per verificare la presenza di errori evidenti, controlla i registri durante la distribuzione.

* La distribuzione potrebbe non riuscire a causa di configurazioni dispatcher o Apache non valide.
   * Assicurati di eseguire i test delle configurazioni dispatcher e Apache a livello locale utilizzando l’immagine Docker inclusa nell’SDK.
   * Per informazioni su come configurare il contenitore Docker dispatcher per eseguire facilmente i test locali, consulta [Dispatcher nel cloud](/help/implementing/dispatcher/disp-overview.md#content-delivery).

* La distribuzione potrebbe non riuscire a causa di altri errori rilevati durante la replica dei pacchetti di contenuti (distribuzione Sling) dall’istanza di authoring a quella di pubblicazione.
   * Per simulare il problema in una configurazione locale, segui la procedura riportata di seguito.
      1. Installa a livello locale un’istanza di authoring e pubblicazione con i JAR dell’SDK di AEM più recenti.
      1. Accedi all’istanza di authoring.
      1. Vai a **Strumenti** -> **Implementazione** -> **Distribuzione**.
      1. Distribuisci i pacchetti di contenuti che fanno parte della base di codice e verifica se la coda si blocca generando un errore.

## Non riesco a impostare una variabile con un comando aio. Cosa posso fare? {#set-variable}

Quando tenti di elencare o impostare le variabili della pipeline con i comandi `aio` potresti visualizzare un errore `403` simile al seguente.

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

In questo caso è necessario aggiungere l’utente che esegue tali comandi al ruolo **Responsabile dell’implementazione** in Admin Console.

Per ulteriori dettagli, consulta [Autorizzazioni API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md).
