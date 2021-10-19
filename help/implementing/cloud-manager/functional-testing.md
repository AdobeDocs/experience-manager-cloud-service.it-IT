---
title: Test funzionali - Cloud Services
description: Test funzionali - Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 058fa606bbc667a36b78d5271947e2741f36240f
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 3%

---

# Test funzionale {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Test funzionale"
>abstract="I test funzionali sono suddivisi in tre tipi: Test funzionali del prodotto, test funzionali personalizzati e test personalizzati dell’interfaccia utente"

I test funzionali sono suddivisi in tre tipi:


* Test funzionale del prodotto
* Test funzionale personalizzato
* Test personalizzati dell&#39;interfaccia utente

## Test funzionale del prodotto {#product-functional-testing}

I test funzionali del prodotto sono un insieme di test di integrazione HTTP stabili (IT) intorno alle funzionalità di base in AEM (ad esempio, authoring e replica) che impediscono la distribuzione delle modifiche del codice dell’applicazione da parte del cliente in caso di interruzione di questa funzionalità di base.

I test funzionali del prodotto vengono eseguiti automaticamente ogni volta che un cliente distribuisce un nuovo codice a Cloud Manager e non può essere ignorato.

Fai riferimento a [Test funzionali del prodotto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) per le prove a campione.

## Test funzionale personalizzato {#custom-functional-testing}

Il passaggio di test delle funzionalità personalizzate nella pipeline è sempre presente e non può essere ignorato.

Tuttavia, se la build non produce JAR di test, il test viene superato per impostazione predefinita.

>[!NOTE]
>Il pulsante **Download Log (Scarica registro)** consente di accedere a un file ZIP contenente i registri per il modulo dettagliato di esecuzione del test. Questi registri non includono i registri del processo di runtime effettivo AEM, a cui è possibile accedere utilizzando la regolare funzionalità Download o Tail Logs (Registri code). Fai riferimento a [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md) per ulteriori dettagli.

## Test personalizzati dell&#39;interfaccia utente {#custom-ui-testing}

AEM fornisce ai suoi clienti una suite integrata di gate di qualità di Cloud Manager per garantire un aggiornamento fluido delle loro applicazioni. In particolare, i gate di test IT consentono già ai clienti di creare e automatizzare i propri test che utilizzano API AEM.

La funzione di test dell’interfaccia utente personalizzata è una [funzionalità opzionale](#customer-opt-in) che consente ai nostri clienti di creare ed eseguire automaticamente i test dell’interfaccia utente per le loro applicazioni. I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium). Per ulteriori informazioni su come creare l’interfaccia utente e scrivere i test dell’interfaccia utente, consulta questo articolo. Inoltre, un progetto di test dell’interfaccia utente può essere facilmente generato utilizzando il AEM Project Archetype.

I clienti possono creare (tramite GIT) test personalizzati e suite di test per l’interfaccia utente. Il test dell’interfaccia utente viene eseguito come parte di un gate di qualità specifico per ogni pipeline di Cloud Manager con il relativo passaggio specifico e le relative informazioni sul feedback. Eventuali test dell’interfaccia utente, tra cui regressione e nuove funzionalità, consentiranno di rilevare gli errori e di segnalarli nel contesto del cliente.

I test dell’interfaccia utente del cliente vengono eseguiti automaticamente sulla pipeline di produzione nel passaggio &quot;Test personalizzati dell’interfaccia utente&quot;.

A differenza dei test funzionali personalizzati che sono test HTTP scritti in java, i test dell’interfaccia utente possono essere un’immagine docker con test scritti in qualsiasi lingua, purché rispettino le convenzioni definite in [Creazione di test dell’interfaccia utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests).

>[!NOTE]
>Si consiglia di seguire la struttura e la lingua *(js e audio)* opportunamente fornito nel [Archetipo di progetto AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) come punto di partenza.

### Opt-in del cliente {#customer-opt-in}

Per poter generare ed eseguire i test dell’interfaccia utente, i clienti devono &quot;effettuare l’opt-in&quot; aggiungendo un file al proprio archivio di codice, sotto il sottomodulo maven per i test dell’interfaccia (accanto al file pom.xml del sottomodulo dei test dell’interfaccia utente) e assicurarsi che questo file sia nella directory principale del predefinito `tar.gz` file.

*Nome file*: `testing.properties`

*Contenuto*: `ui-tests.version=1`

Se questo non è presente nella build `tar.gz` file, la build e le esecuzioni dei test dell’interfaccia utente verranno ignorate

Per aggiungere `testing.properties` aggiungi un `include` istruzione in `assembly-ui-test-docker-context.xml` file (nel sottomodulo di test dell’interfaccia utente):

    &quot;
    [..]
    &lt;includes>
    &lt;include>Dockerfile&lt;/include>
    &lt;include>wait-for-grid.sh&lt;/include>
    &lt;include>testing.properties&lt;/include> &lt;!>- modulo di test opt-in in Cloud Manager —>
    &lt;/includes>
    [..]
    &quot;

>[!NOTE]
>Le pipeline di produzione create prima del 10 febbraio 2021 dovranno essere aggiornate per poter utilizzare i test dell’interfaccia utente come descritto in questa sezione. In sostanza, l’utente deve modificare la pipeline di produzione e fare clic su **Salva** dall’interfaccia utente anche se non sono state apportate modifiche.
>Fai riferimento a [Configurazione della pipeline CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) per ulteriori informazioni sulla configurazione della pipeline.

### Scrittura di test funzionali {#writing-functional-tests}

I test funzionali scritti dal cliente devono essere imballati come file JAR separato prodotto dalla stessa build Maven degli artefatti da distribuire AEM. Generalmente si tratta di un modulo Maven separato. Il file JAR risultante deve contenere tutte le dipendenze richieste e generalmente viene creato utilizzando il plugin maven-assembly utilizzando il descrittore jar-with-dependencies.

Inoltre, il JAR deve avere l&#39;intestazione del manifesto Cloud-Manager-TestType impostata su integration-test. In futuro, saranno supportati ulteriori valori di intestazione. Un esempio di configurazione per il maven-assembly-plugin è:

```java
<build>
    <plugins>
        <!-- Create self-contained jar with dependencies -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.1.0</version>
            <configuration>
                <descriptorRefs>
                    <descriptorRef>jar-with-dependencies</descriptorRef>
                </descriptorRefs>
                <archive>
                    <manifestEntries>
                        <Cloud-Manager-TestType>integration-test</Cloud-Manager-TestType>
                    </manifestEntries>
                </archive>
            </configuration>
            <executions>
                <execution>
                    <id>make-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
```

All&#39;interno di questo file JAR, i nomi delle classi dei test effettivi da eseguire devono terminare in IT.

Ad esempio, una classe denominata `com.myco.tests.aem.ExampleIT` vengono eseguiti ma una classe denominata `com.myco.tests.aem.ExampleTest` non lo farei.

Le classi di test devono essere normali test JUnit. L’infrastruttura di test è progettata e configurata per essere compatibile con le convenzioni utilizzate dalla libreria di test aem-testing-clients. Invitiamo vivamente gli sviluppatori a utilizzare questa libreria e a seguire le relative best practice. Fai riferimento a [Collegamento Git](https://github.com/adobe/aem-testing-clients) per ulteriori dettagli.

### Esecuzione del test locale {#local-test-execution}

Poiché le classi di test sono test JUnit, possono essere eseguite da IDE Java principali come Eclipse, IntelliJ, NetBeans e così via.

Tuttavia, durante l’esecuzione di questi test, sarà necessario impostare una varietà di proprietà di sistema previste da aem-testing-clients (e dai client di test Sling sottostanti).

Le proprietà del sistema sono le seguenti:

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
