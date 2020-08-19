---
title: Test funzionale - Cloud Services
description: Test funzionale - Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 4%

---


# Test funzionale {#functional-testing}

Il test funzionale è suddiviso in due tipi:

* Test funzionale del prodotto
* Test funzionale personalizzato

## Test funzionale del prodotto {#product-functional-testing}

I test funzionali di prodotto sono una serie di test di integrazione HTTP (IT) stabili attorno alle funzionalità di base in AEM (ad esempio, creazione e replica) che impediscono la distribuzione delle modifiche apportate dal cliente al codice dell&#39;applicazione in caso di interruzione di questa funzionalità di base.

I test funzionali del prodotto vengono eseguiti automaticamente ogni volta che un cliente distribuisce il nuovo codice a Cloud Manager e non può essere ignorato.

Per i test di [funzionalità dei](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) prodotti, fare riferimento a Testdi funzionalità dei prodotti.

## Test funzionale personalizzato {#custom-functional-testing}

Il passaggio di test funzionale personalizzato nella pipeline è sempre presente e non può essere ignorato.

Tuttavia, se la build non produce JAR di prova, il test viene superato per impostazione predefinita.

>[!NOTE]
>Il pulsante **Download Log (Scarica registro)** consente di accedere a un file ZIP contenente i registri per il modulo dettagliato di esecuzione del test. Tali registri non includono i registri del processo AEM runtime effettivo, a cui è possibile accedere tramite la regolare funzionalità Download o Registrazione code. Per ulteriori informazioni, consultate [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md) .


### Scrittura di test funzionali {#writing-functional-tests}

I test funzionali scritti dal cliente devono essere confezionati come file JAR separato prodotto dalla stessa build Maven degli artefatti da distribuire a AEM. Generalmente questo sarebbe un modulo Maven separato. Il file JAR risultante deve contenere tutte le dipendenze richieste e generalmente viene creato utilizzando il plug-in maven-assembly utilizzando il descrittore jar-with-dependencies.

Inoltre, il JAR deve avere l’intestazione del manifesto di Cloud-Manager-TestType impostata su integration-test. In futuro, saranno supportati ulteriori valori di intestazione. Un esempio di configurazione per il plug-in maven-assembly è:

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

All&#39;interno di questo file JAR, i nomi delle classi dei test effettivi da eseguire devono terminare con l&#39;IT.

Ad esempio, una classe denominata `com.myco.tests.aem.ExampleIT` viene eseguita ma non viene `com.myco.tests.aem.ExampleTest` eseguita una classe denominata.

Le classi di test devono essere normali test JUnit. L&#39;infrastruttura di test è progettata e configurata per essere compatibile con le convenzioni utilizzate dalla libreria di test dei client Aem-testing. Gli sviluppatori sono invitati a utilizzare questa libreria e a seguire le procedure ottimali. Per ulteriori informazioni, consultate Collegamento [](https://github.com/adobe/aem-testing-clients) Git.

### Esecuzione test locale {#local-test-execution}

Poiché le classi di test sono test JUnit, possono essere eseguite da IDE Java mainstream come Eclipse, IntelliJ, NetBeans e così via.

Tuttavia, durante l&#39;esecuzione di questi test, sarà necessario impostare una serie di proprietà del sistema previste dai client Aem-testing (e dai client Sling Testing sottostanti).

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

