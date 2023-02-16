---
title: Test funzionali
description: Scopri i tre diversi tipi di test funzionali integrati nel processo di distribuzione di AEM as a Cloud Service per garantire la qualità e l’affidabilità del codice.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 73a73f2f6c56386f3058d89e66b036e8f5e5a17b
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 72%

---


# Test funzionali {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Test funzionali"
>abstract="Scopri i tre diversi tipi di test funzionali integrati nel processo di distribuzione di AEM as a Cloud Service per garantire la qualità e l’affidabilità del codice."

Scopri i tre diversi tipi di test funzionali integrati nel [processo di distribuzione di AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) per garantire la qualità e l’affidabilità del codice.

## Panoramica {#overview}

AEM as a Cloud Service offre tre diversi tipi di test funzionali.

* [Test funzionali del prodotto](#product-functional-testing)
* [Test funzionali personalizzati](#custom-functional-testing)
* [Test dell’interfaccia utente personalizzati](#custom-ui-testing)

Per tutti i test funzionali, è possibile scaricare i risultati dettagliati come file `.zip` utilizzando il pulsante **Scarica registro build** nella schermata di panoramica della build come parte del [processo di distribuzione.](/help/implementing/cloud-manager/deploy-code.md)

Questi registri non includono i registri del processo di runtime effettivo di AEM. Per ulteriori informazioni su come accedere ai registri, consulta il documento [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md).

I test funzionali del prodotto e i test funzionali personalizzati di esempio sono basati sui [client di test di AEM.](https://github.com/adobe/aem-testing-clients)

### Test funzionali del prodotto {#product-functional-testing}

I test funzionali del prodotto sono una serie di test stabili di integrazione HTTP (IT) delle funzionalità principali in AEM, come le attività di authoring e replica. Questi test vengono gestiti da Adobe e hanno lo scopo di impedire la distribuzione di modifiche al codice personalizzato dell’applicazione nel caso in cui interrompano le funzionalità core.

I test funzionali del prodotto vengono eseguiti automaticamente ogni volta che si distribuisce un nuovo codice in Cloud Manager e non possono essere ignorati.

I test funzionali del prodotto vengono mantenuti come progetto open-source. Per ulteriori informazioni, consulta i [test funzionali del prodotto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) su GitHub.

### Test funzionali personalizzati {#custom-functional-testing}

Anche se i test funzionali del prodotto sono definiti da Adobe, puoi creare test di qualità personalizzati per la tua applicazione. Verranno eseguiti come test funzionali personalizzati come parte della pipeline di produzione per garantire la qualità dell’applicazione.

Il test funzionale personalizzato viene eseguito sia per le distribuzioni del codice personalizzato che per gli aggiornamenti push, il che rende particolarmente importante scrivere buoni test funzionali che impediscano AEM modifiche del codice di interrompere il codice dell&#39;applicazione. Il passaggio dei test funzionali personalizzati è sempre presente e non può essere ignorato.

### Test dell’interfaccia utente personalizzati {#custom-ui-testing}

I test dell’interfaccia utente personalizzati sono una funzione facoltativa che consente di creare ed eseguire automaticamente i test dell’interfaccia utente per le applicazioni. I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta di lingue e framework come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium.

Per ulteriori informazioni, consulta il documento [Test dell’interfaccia utente personalizzati](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing).

## Guida introduttiva ai test funzionali {#getting-started-functional-tests}

Dopo la creazione di un nuovo archivio di codice in Cloud Manager, un `it.tests` viene creata automaticamente con casi di test di esempio.

>[!NOTE]
>
>Se l’archivio è stato creato prima della creazione automatica di Cloud Manager `it.tests` cartelle, puoi anche generare la versione più recente utilizzando [AEM Archetipo di progetto.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)

Una volta ottenuto il contenuto del `it.tests` È possibile utilizzarlo come base per i propri test e quindi:

1. [Sviluppa i tuoi casi di test.](#writing-functional-tests)
1. [Esegui i test localmente.](#local-test-execution)
1. Invia il codice all’archivio di Cloud Manager ed esegui una pipeline di Cloud Manager.

## Scrittura di test funzionali personalizzati {#writing-functional-tests}

Per scrivere test funzionali personalizzati è possibile utilizzare gli stessi strumenti impiegati da Adobe per la scrittura dei test funzionali del prodotto. Per la scrittura dei test, puoi consultare i [test funzionali del prodotto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) in GitHub come esempio.

Il codice per i test funzionali personalizzati è il codice Java incluso nella cartella `it.tests` del progetto. Deve produrre un unico JAR con tutti i test funzionali. Se la generazione produce più di un JAR di test, quello selezionato non è deterministico. Se non viene prodotto alcun JAR di test, il passaggio di test viene superato per impostazione predefinita. Per dei test di esempio,[consulta la sezione Archetipo del progetto AEM](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests).

I test vengono eseguiti su un’infrastruttura di test gestita da Adobe, che prevede almeno due istanze di Author, due istanze di Publisher e una configurazione Dispatcher. Ciò significa che i test funzionali personalizzati vengono eseguiti sull’intero stack di AEM.

### Struttura dei test funzionali {#functional-tests-structure}

I test funzionali personalizzati devono essere inclusi come file JAR separati prodotti dalla stessa build Maven degli artefatti da distribuire in AEM. Generalmente si tratta di un modulo Maven separato. Il file JAR risultante deve contenere tutte le dipendenze richieste e generalmente viene creato con il `maven-assembly-plugin` utilizzando il descrittore `jar-with-dependencies`.

Inoltre, l’intestazione del manifesto `Cloud-Manager-TestType` del file JAR deve essere impostata su `integration-test`.

Di seguito è riportata una configurazione di esempio per `maven-assembly-plugin`.

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

All’interno di questo file JAR, i nomi delle classi dei test effettivi da eseguire devono terminare con `IT`.

Ad esempio, una classe denominata `com.myco.tests.aem.it.ExampleIT` verrebbe eseguita, mentre una denominata `com.myco.tests.aem.it.ExampleTest` no.

Inoltre, per escludere il codice di test dal controllo di copertura dell’analisi del codice, il codice di test deve trovarsi all’interno di un pacchetto denominato `it` (il filtro di esclusione della copertura è `**/it/**/*.java`).

Le classi di test devono essere normali test JUnit. L’infrastruttura di test è progettata e configurata per la compatibilità con le convenzioni utilizzate dalla libreria di test `aem-testing-clients`. Si consiglia ai team di sviluppo di utilizzare questa libreria e seguire le relative best practice.

Per ulteriori informazioni, consulta l’[`aem-testing-clients` archivio di GitHub](https://github.com/adobe/aem-testing-clients).

>[!TIP]
>
>[Guarda questo video](https://www.youtube.com/watch?v=yJX6r3xRLHU) per scoprire come utilizzare i test funzionali personalizzati per acquisire maggiore dimestichezza con le pipeline CI/CD.

### Esecuzione locale dei test {#local-test-execution}

Prima di attivare i test funzionali in una pipeline di Cloud Manager, si consiglia di eseguire i test funzionali localmente utilizzando l’ [AEM SDK as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) o un&#39;istanza effettiva AEM as a Cloud Service.

#### Prerequisiti {#prerequisites}

I test in Cloud Manager verranno eseguiti utilizzando un utente amministratore tecnico.

Per eseguire i test funzionali dal computer locale, crea un utente con autorizzazioni di tipo amministratore per ottenere lo stesso comportamento.

#### Esecuzione in un IDE {#running-in-an-ide}

Poiché le classi di test sono test JUnit, possono essere eseguite da IDE Java principali come Eclipse, IntelliJ e NetBeans. Poiché i test funzionali del prodotto e i test funzionali personalizzati sono basati sulla stessa tecnologia, entrambi possono essere eseguiti a livello locale copiando i test del prodotto nei test personalizzati.

Tuttavia, durante l’esecuzione di questi test, è necessario impostare diverse proprietà di sistema previste dalla libreria `aem-testing-clients` (e dalla libreria sottostante Sling Testing Client).

Le proprietà del sistema sono indicate di seguito.

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, for example, admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the publish URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

#### Esecuzione di tutti i test utilizzando Maven {#using-maven}

1. Apri una shell e passa alla `it.tests` nella directory archivio.

1. Esegui il seguente comando fornendo i parametri necessari per avviare i test utilizzando Maven.

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```
