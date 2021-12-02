---
title: Test funzionali - Cloud Services
description: Test funzionali - Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 02db915e114c2af8329eaddbb868045944a3574d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Test funzionale {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Test funzionale"
>abstract="I test funzionali sono suddivisi in tre tipi: Test funzionali del prodotto, test funzionali personalizzati e test personalizzati dell’interfaccia utente"

I test funzionali sono suddivisi in tre tipi:


* [Test funzionale del prodotto](#product-functional-testing)
* [Test funzionale personalizzato](#custom-functional-testing)
* [Test personalizzati dell&#39;interfaccia utente](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)

## Test funzionale del prodotto {#product-functional-testing}

I test funzionali del prodotto sono un insieme di test di integrazione HTTP stabili (IT) intorno alle funzionalità principali in AEM (ad esempio, authoring e replica) che impediscono la distribuzione delle modifiche del codice dell’applicazione da parte del cliente in caso di interruzione di questa funzionalità di base.

I test funzionali del prodotto vengono eseguiti automaticamente ogni volta che un cliente distribuisce un nuovo codice a Cloud Manager e non può essere ignorato.

Fai riferimento a [Test funzionali del prodotto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) per le prove a campione.

## Test funzionale personalizzato {#custom-functional-testing}

Il passaggio di test delle funzionalità personalizzate nella pipeline è sempre presente e non può essere ignorato.

La build deve produrre zero o un JAR di test. Se genera JAR di prova zero, il passaggio di test viene superato per impostazione predefinita. Se la build produce più di un JAR di test, il JAR selezionato non è deterministico.

>[!NOTE]
>Il pulsante **Download Log (Scarica registro)** consente di accedere a un file ZIP contenente i registri per il modulo dettagliato di esecuzione del test. Questi registri non includono i registri del processo di runtime effettivo AEM, a cui è possibile accedere utilizzando la regolare funzionalità Download o Tail Logs (Registri code). Fai riferimento a [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md) per ulteriori dettagli.


## Scrittura di test funzionali {#writing-functional-tests}

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

All&#39;interno di questo file JAR, i nomi delle classi dei test effettivi da eseguire devono terminare in `IT`.

Ad esempio, una classe denominata `com.myco.tests.aem.it.ExampleIT` vengono eseguiti, ma una classe denominata `com.myco.tests.aem.it.ExampleTest` non lo farei.

Inoltre, per escludere il codice di prova dal controllo di copertura della scansione del codice, il codice di prova deve essere al di sotto di un pacchetto denominato `it` (il filtro di esclusione della copertura è `**/it/**/*.java`).

Le classi di test devono essere normali test JUnit. L’infrastruttura di test è progettata e configurata per essere compatibile con le convenzioni utilizzate dalla libreria di test aem-testing-clients. Invitiamo vivamente gli sviluppatori a utilizzare questa libreria e a seguire le relative best practice. Fai riferimento a [Collegamento Git](https://github.com/adobe/aem-testing-clients) per ulteriori dettagli.

## Esecuzione del test locale {#local-test-execution}

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
