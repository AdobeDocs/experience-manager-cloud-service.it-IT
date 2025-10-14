---
title: Java &trade; test funzionali
description: Scopri come scrivere Java &trade; test funzionali per AEM as a Cloud Service
exl-id: e014b8ad-ac9f-446c-bee8-adf05a6b4d70
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 498a58c89910f41e6b86c5429629ec9282028987
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 78%

---

# Test funzionali Java™

Scopri come scrivere test funzionali Java™ per AEM as a Cloud Service

## Guida introduttiva ai test funzionali {#getting-started-functional-tests}

Al momento della creazione di un nuovo archivio di codice in Cloud Manager, una cartella `it.tests` viene creata automaticamente con esempi di test.

>[!NOTE]
>
>Se l’archivio è stato creato prima della creazione automatica delle cartelle `it.tests` di Cloud Manager, puoi anche generare la versione più recente utilizzando l’[archetipo di progetto AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests).

Una volta ottenuto il contenuto della cartella `it.tests`, puoi utilizzarla come base per i test e quindi:

1. [Sviluppa i test case](#writing-functional-tests).
1. [Eseguire i test localmente](#local-test-execution).
1. Salvare il codice nell’archivio di Cloud Manager ed eseguire una pipeline di Cloud Manager.

## Scrittura di test funzionali personalizzati {#writing-functional-tests}

Per scrivere test funzionali personalizzati è possibile utilizzare gli stessi strumenti impiegati da Adobe per la scrittura dei test funzionali del prodotto. Per la scrittura dei test, puoi consultare i [test funzionali del prodotto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) in GitHub come esempio.

Il codice per i test funzionali personalizzati è il codice Java incluso nella cartella `it.tests` del progetto. Deve produrre un unico JAR con tutti i test funzionali. Se la generazione produce più di un JAR di test, quello selezionato non è deterministico. Se non viene prodotto alcun JAR di test, il passaggio di test viene superato per impostazione predefinita. Per i test di esempio, consulta [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests).

I test vengono eseguiti su un’infrastruttura di test gestita da Adobe, che prevede almeno due istanze di authoring, due istanze di pubblicazione e una configurazione del Dispatcher. Questa configurazione significa che i test funzionali personalizzati vengono eseguiti sull’intero stack di AEM.

### Struttura dei test funzionali {#functional-tests-structure}

I test funzionali personalizzati devono essere inclusi come file JAR separati prodotti dalla stessa build Maven degli artefatti da implementare in AEM. Generalmente, questa build è di un modulo Maven separato. Il file JAR risultante deve contenere tutte le dipendenze richieste e generalmente viene creato con il `maven-assembly-plugin` utilizzando il descrittore `jar-with-dependencies`.

Inoltre, l’intestazione del manifesto `Cloud-Manager-TestType` del file JAR deve essere impostata su `integration-test`.

Di seguito è riportata una configurazione di esempio per `maven-assembly-plugin`.

```XML
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
</build>
```

All’interno di questo file JAR, i nomi delle classi dei test effettivi da eseguire devono terminare con `IT`.

Ad esempio, una classe denominata `com.myco.tests.aem.it.ExampleIT` verrebbe eseguita, mentre una denominata `com.myco.tests.aem.it.ExampleTest` no.

Inoltre, per escludere il codice di test dal controllo di copertura dell’analisi del codice, il codice di test deve trovarsi all’interno di un pacchetto denominato `it` (il filtro di esclusione della copertura è `**/it/**/*.java`).

Le classi di test devono essere normali test JUnit. L’infrastruttura di test è progettata e configurata per la compatibilità con le convenzioni utilizzate dalla libreria di test `aem-testing-clients`. Si consiglia ai team di sviluppo di utilizzare questa libreria e seguire le relative best practice.

Per ulteriori dettagli, consulta l’[`aem-testing-clients`archivio GitHub.](https://github.com/adobe/aem-testing-clients)

>[!TIP]
>
>[Guarda questo video](https://www.youtube.com/watch?v=yJX6r3xRLHU) per scoprire come utilizzare i test funzionali personalizzati per acquisire maggiore dimestichezza con le pipeline CI/CD.

### Prerequisiti {#prerequisites}

1. I test in Cloud Manager sono eseguiti utilizzando un utente amministratore tecnico.

>[!NOTE]
>
>Per eseguire i test funzionali dal computer locale, crea un utente con autorizzazioni di tipo amministratore per ottenere lo stesso comportamento.

1. L&#39;infrastruttura a contenitori per il test funzionale è limitata dai seguenti vincoli:


| Tipo | Valore | Descrizione |
|----------------------|-------|--------------------------------------------------------------------|
| CPU | 0.5 | Quantità di tempo CPU riservato per ogni esecuzione di test |
| Memoria | 0,5 Gi | Quantità di memoria allocata al test, valore in gibibyte. |
| Timeout | 30 min | Il limite di tempo dopo il quale il test viene interrotto. |
| Durata consigliata | 15 min | Adobe consiglia di non richiedere più tempo alla scrittura dei test. |

>[!NOTE]
>
> Se hai bisogno di più risorse, crea un caso per l’Assistenza clienti e descrivi il tuo caso d’uso. Il team di Adobe esamina la tua richiesta e fornisce assistenza adeguata.

#### Dipendenze

* aem-cloud-testing-client:

Le modifiche imminenti all&#39;infrastruttura containerizzata per l&#39;esecuzione dei test funzionali richiedono l&#39;aggiornamento della libreria [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) nei test funzionali personalizzati alla versione **1.2.1** o successiva. Verificare che la dipendenza nel file `it.tests/pom.xml` sia aggiornata di conseguenza.

```
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

>[!NOTE]
>
>Questa modifica deve essere eseguita prima del 6 aprile 2024.
>>Se non si aggiorna la libreria di dipendenze, possono verificarsi errori di pipeline nel passaggio &quot;Test funzionali personalizzato&quot;.

### Esecuzione locale dei test {#local-test-execution}

Prima di attivare i test funzionali in una pipeline di Cloud Manager, si consiglia di eseguirli localmente utilizzando [SDK di AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) o un’istanza di AEM as a Cloud Service.

#### Esecuzione in un IDE {#running-in-an-ide}

Poiché le classi di test sono test JUnit, possono essere eseguite da IDE Java ™ principali come Eclipse, IntelliJ e NetBeans. Poiché i test funzionali del prodotto e i test funzionali personalizzati sono basati sulla stessa tecnologia, entrambi possono essere eseguiti a livello locale copiando i test del prodotto nei test personalizzati.

Tuttavia, durante l’esecuzione di questi test, è necessario impostare diverse proprietà di sistema previste dalla libreria `aem-testing-clients` (e dalla libreria sottostante Sling Testing Client).

Le proprietà del sistema sono indicate di seguito.

| Proprietà | Descrizione | Esempio |
|-------------------------------------|------------------------------------------------------------------|-------------------------|
| `sling.it.instances` | Il numero di istanze da associare al servizio cloud deve essere impostato su `2`. | `2` |
| `sling.it.instance.url.1` | Imposta l’URL dell’autore. | `http://localhost:4502` |
| `sling.it.instance.runmode.1` | Modalità di esecuzione della prima istanza. Imposta su `author`. | `author` |
| `sling.it.instance.adminUser.1` | Impostato su Autore utente amministratore. | `admin` |
| `sling.it.instance.adminPassword.1` | Imposta la password amministratore per l’authoring. |                         |
| `sling.it.instance.url.2` | impostato per pubblicare l’URL. | `http://localhost:4503` |
| `sling.it.instance.runmode.2` | Modalità di esecuzione della seconda istanza. Imposta su `publish`. | `publish` |
| `sling.it.instance.adminUser.2` | Impostato per pubblicare l’utente amministratore. | `admin` |
| `sling.it.instance.adminPassword.2` | Imposta per pubblicare la password amministratore. |                         |



#### Esecuzione di tutti i test con Maven {#using-maven}

1. Apri una shell e passa alla cartella `it.tests` nell’archivio.

1. Esegui il comando seguente fornendo i parametri necessari per avviare i test utilizzando Maven.

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```

