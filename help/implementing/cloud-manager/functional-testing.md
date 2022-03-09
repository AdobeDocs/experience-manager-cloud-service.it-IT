---
title: Test funzionale
description: Scopri i tre diversi tipi di test funzionali incorporati nel processo di distribuzione as a Cloud Service AEM per garantire la qualità e l’affidabilità del codice.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 15de47e28e804fd84434d5e8e5d2fe8fe6797241
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---


# Test funzionale {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Test funzionale"
>abstract="Scopri i tre diversi tipi di test funzionali incorporati nel processo di distribuzione as a Cloud Service AEM per garantire la qualità e l’affidabilità del codice."

Scopri i tre diversi tipi di test funzionali incorporati in [AEM processo di distribuzione as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) per garantire la qualità e l&#39;affidabilità del codice.

## Panoramica {#overview}

Ci sono tre diversi tipi di test funzionali in AEM as a Cloud Service.

* [Test funzionale del prodotto](#product-functional-testing)
* [Test funzionale personalizzato](#custom-functional-testing)
* [Test personalizzati dell&#39;interfaccia utente](#custom-ui-testing)

Per tutti i test funzionali, i risultati dettagliati dei test possono essere scaricati come `.zip` utilizzando **Scarica il registro della build** nella schermata di panoramica della build come parte del [processo di distribuzione.](/help/implementing/cloud-manager/deploy-code.md) Questi registri non includono i registri del processo di runtime AEM effettivo. Per accedere a tali registri, fai riferimento al documento [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md) per ulteriori dettagli.

## Test funzionale del prodotto {#product-functional-testing}

I test funzionali del prodotto sono una serie di test di integrazione HTTP stabili (IT) delle funzionalità principali in AEM, come le attività di authoring e replica. Questi test impediscono la distribuzione delle modifiche apportate dal cliente al codice dell&#39;applicazione personalizzato in caso di interruzione delle funzionalità di base.

I test funzionali del prodotto vengono eseguiti automaticamente ogni volta che distribuisci un nuovo codice in Cloud Manager e non possono essere ignorati.

Fai riferimento a [test funzionali del prodotto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) in GitHub per test di esempio.

## Test funzionale personalizzato {#custom-functional-testing}

Il passaggio di test funzionale personalizzato nella pipeline è sempre presente e non può essere ignorato.

La build deve produrre zero o un JAR di test. Se genera JAR di prova zero, il passaggio di test viene superato per impostazione predefinita. Se la build produce più di un JAR di test, il JAR selezionato non è deterministico.

### Scrittura di test funzionali {#writing-functional-tests}

I test funzionali personalizzati devono essere assemblati come file JAR separato prodotto dalla stessa build Maven degli artefatti da distribuire in AEM. Generalmente si tratta di un modulo Maven separato. Il file JAR risultante deve contenere tutte le dipendenze richieste e generalmente viene creato utilizzando `maven-assembly-plugin` utilizzando `jar-with-dependencies` descrittore.

Inoltre, il JAR deve avere il `Cloud-Manager-TestType` intestazione manifest impostata su `integration-test`. In futuro, saranno supportati ulteriori valori di intestazione.

Di seguito è riportato un esempio di configurazione per `maven-assembly-plugin`.

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

Le classi di test devono essere normali test JUnit. L&#39;infrastruttura di test è progettata e configurata in modo da essere compatibile con le convenzioni utilizzate `aem-testing-clients` libreria di test. Invitiamo vivamente gli sviluppatori a utilizzare questa libreria e a seguire le relative best practice.

Fai riferimento alla [`aem-testing-clients` Archivio GitHub](https://github.com/adobe/aem-testing-clients) per ulteriori dettagli.

## Test personalizzati dell&#39;interfaccia utente {#custom-ui-testing}

Il test personalizzato dell’interfaccia utente è una funzione opzionale che consente di creare ed eseguire automaticamente i test dell’interfaccia utente per le applicazioni. I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium).

Fare riferimento al documento [Test personalizzati dell&#39;interfaccia utente](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) per ulteriori informazioni.

## Esecuzione del test locale {#local-test-execution}

Poiché le classi di test sono test JUnit, possono essere eseguite da IDE Java principali come Eclipse, IntelliJ, NetBeans e così via.

Tuttavia, durante l&#39;esecuzione di questi test, sarà necessario impostare una varietà di proprietà di sistema previste dal `aem-testing-clients` (e la libreria sottostante Sling Testing Clients).

Le proprietà del sistema sono le seguenti.

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
