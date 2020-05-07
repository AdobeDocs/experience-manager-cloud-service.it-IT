---
title: Comprendere i risultati dei test - Servizi cloud
description: Comprendere i risultati dei test - Servizi cloud
translation-type: tm+mt
source-git-commit: 4b79f7dd3a55e140869985faa644f7da1f62846c
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 4%

---


# Risultati dei test {#understand-test-results}

Le esecuzioni della pipeline di Cloud Manager for Cloud Services supporteranno l&#39;esecuzione di test eseguiti nell&#39;ambiente del passaggio. Ciò è in contrasto con i test eseguiti durante il passaggio Genera e Prova unità che vengono eseguiti offline, senza l&#39;accesso ad alcun ambiente AEM in esecuzione.
Esistono due tipi di test eseguiti in questo contesto:
* Test scritti dal cliente
* Test scritti da Adobe

Entrambi i tipi di test sono eseguiti in un&#39;infrastruttura containerizzata progettata per eseguire questi tipi di test.


## Verifica della qualità del codice {#code-quality-testing}

Come parte della pipeline, il codice sorgente viene analizzato per garantire che le distribuzioni soddisfino determinati criteri di qualità. Attualmente, questo è implementato tramite una combinazione di SonarQube e l&#39;esame a livello di pacchetto di contenuti tramite OakPAL. Esistono più di 100 regole che combinano regole Java generiche e regole specifiche di AEM. La tabella seguente riassume la valutazione per i criteri di prova:

| Nome | Definizione | Categoria | Soglia di errore |
|--- |--- |--- |--- |
| Valutazione sicurezza | A = 0 Vulnerabilità <br/>B = almeno 1 Vulnerabilità<br/> minore C = almeno 1 Vulnerabilità maggiore <br/>D = almeno 1 Vulnerabilità critica <br/>E = almeno 1 Vulnerabilità blocco | Critico | &lt; B |
| Valutazione affidabilità | A = 0 Bug <br/>B = almeno 1 Bug Minore <br/>C = almeno 1 Bug Principale <br/>D = almeno 1 Bug Critico E = almeno 1 Bug Blocco | Importante | &lt; C |
| Classificazione manutenibilità | L&#39;eccezionale costo di riparazione per gli odori di codice è: <br/><ul><li>&lt;=5% del tempo che è già passato nell&#39;applicazione, la valutazione è A </li><li>tra il 6 e il 10% il rating è a B </li><li>tra l&#39;11% e il 20% il rating è a C </li><li>tra il 21% e il 50% la valutazione è una D</li><li>un valore superiore al 50% è un E</li></ul> | Importante | &lt; A |
| Copertura | Una combinazione di copertura della linea di prova di unità e copertura della condizione utilizzando la seguente formula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>dove: CT = condizioni che sono state valutate come &#39;true&#39; almeno una volta durante l&#39;esecuzione di unit test <br/>CF = condizioni che sono state valutate come &#39;false&#39; almeno una volta durante l&#39;esecuzione di unit test <br/>LC = linee coperte = lines_to_cover - uncover_lines <br/><br/> B = numero totale di condizioni <br/>EL = numero totale di linee eseguibili (lines_to_cover) | Importante | &lt; 50% |
| Test di unità ignorati | Numero di unit test ignorati. | Info | > 1 |
| Problemi aperti | Tipi di problemi generali - Vulnerabilità, bug e odori di codice | Info | > 0 |
| Linee duplicate | Numero di righe coinvolte in blocchi duplicati. <br/>Per considerare un blocco di codice come duplicato: <br/><ul><li>**Progetti non Java:**</li><li>Devono essere presenti almeno 100 token successivi e duplicati.</li><li>Tali token devono essere ripartiti almeno su: </li><li>30 righe di codice per COBOL </li><li>20 righe di codice per ABAP </li><li>10 righe di codice per altre lingue</li><li>**Progetti Java:**</li><li> Devono essere presenti almeno 10 istruzioni successive e duplicate, indipendentemente dal numero di token e di righe.</li></ul> <br/>Le differenze nei rientri e nei letterali di stringa vengono ignorate durante il rilevamento di duplicati. | Info | > 1% |
| Compatibilità con i servizi cloud | Numero di problemi di compatibilità del servizio cloud identificati. | Info | > 0 |


>[!NOTE]
>
>Per informazioni più dettagliate, fare riferimento a Definizioni [metriche](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) .

Puoi scaricare l&#39;elenco delle regole qui [code-quality-rules.xlsx](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx)

>[!NOTE]
>
>Per ulteriori informazioni sulle regole di qualità del codice personalizzate eseguite da [!UICONTROL Cloud Manager], consulta Regole [di qualità del codice](/help/implementing/cloud-manager/custom-code-quality-rules.md)personalizzate.

### Gestione dei falsi positivi {#dealing-with-false-positives}

Il processo di scansione della qualità non è perfetto e a volte identificherà erroneamente i problemi che non sono effettivamente problematici. Questo viene definito &quot;falso positivo&quot;.

In questi casi, il codice sorgente può essere annotato con l&#39; `@SuppressWarnings` annotazione Java standard che specifica l&#39;ID regola come attributo annotazione. Ad esempio, un problema comune è che la regola SonarQube per rilevare le password hardcoded può essere aggressiva per quanto riguarda il modo in cui viene identificata una password hardcoded.

Per un esempio specifico, questo codice è abbastanza comune in un progetto AEM con codice per la connessione a un servizio esterno:

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube solleverà una vulnerabilità di blocco. Dopo aver rivisto il codice, identificate che non si tratta di una vulnerabilità e potete annotarlo con l&#39;ID regola appropriato.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Tuttavia, se il codice fosse effettivamente questo:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Quindi la soluzione corretta è rimuovere la password hardcoded.

>[!NOTE]
>
>Sebbene sia buona norma rendere l’ `@SuppressWarnings` annotazione il più possibile specifica, ovvero annotare solo l’istruzione o il blocco specifico che causa il problema, è possibile inserire delle annotazioni a livello di classe.

## Scrittura di test funzionali {#writing-functional-tests}

I test funzionali scritti dal cliente devono essere compressi come file JAR separato prodotto dalla stessa build Maven degli artefatti da distribuire ad AEM. Generalmente questo sarebbe un modulo Maven separato. Il file JAR risultante deve contenere tutte le dipendenze richieste e generalmente viene creato utilizzando il plug-in maven-assembly utilizzando il descrittore jar-with-dependencies.

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

## Test funzionale personalizzato {#custom-functional-test}

Il passaggio di test funzionale personalizzato nella pipeline è sempre presente e non può essere ignorato.

Tuttavia, se la build non produce JAR di prova, il test viene superato per impostazione predefinita. Questo passaggio viene eseguito immediatamente dopo la distribuzione dell’area di visualizzazione.

>[!NOTE]
>Il pulsante **Download Log (Scarica registro)** consente di accedere a un file ZIP contenente i registri per il modulo dettagliato di esecuzione del test. Questi registri non includono i registri del processo di runtime AEM effettivo, a cui è possibile accedere tramite la regolare funzionalità Download o Registrazione code. Per ulteriori informazioni, consulta [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md) .

## Esecuzione test locale {#local-test-execution}

Poiché le classi di test sono test JUnit, possono essere eseguite da IDE Java mainstream come Eclipse, IntelliJ, NetBeans e così via.

Tuttavia, quando eseguite questi test necessariamente, sarà necessario impostare una varietà di proprietà di sistema previste dai client Aem-testing (e dai client Sling Testing sottostanti).

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