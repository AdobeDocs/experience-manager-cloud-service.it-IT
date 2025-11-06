---
title: Test di qualità del codice
description: Scopri come funziona il test della qualità del codice delle pipeline e come può migliorare la qualità delle distribuzioni.
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 80%

---

# Test della qualità del codice {#code-quality-testing}

Scopri come funziona il test della qualità del codice delle pipeline e come può migliorare la qualità delle distribuzioni.

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="Test della qualità del codice"
>abstract="Il test di qualità del codice valuta il codice dell’applicazione in base a un set di regole relative alla qualità. È lo scopo principale di una pipeline destinata solo alla qualità del codice e viene eseguito immediatamente dopo la fase di build in tutte le pipeline di produzione e non di produzione."

## Introduzione {#introduction}

Il test di qualità del codice valuta il codice dell’applicazione in base a un set di regole relative alla qualità. È lo scopo principale di una pipeline destinata solo alla qualità del codice e viene eseguito immediatamente dopo la fase di build in tutte le pipeline di produzione e non di produzione.

Per ulteriori informazioni sui diversi tipi di pipeline, consulta il documento [Configurazione della pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

## Regole per la qualità del codice {#understanding-code-quality-rules}

Il test di qualità del codice controlla il codice sorgente per garantire che soddisfi determinati criteri di qualità. Questo passaggio è implementato tramite una combinazione di SonarQube e l’esame dei contenuti a livello di pacchetto tramite OakPAL. Sono presenti più di 100 regole, che combinano regole Java generiche e regole specifiche per AEM. Alcune regole specifiche per AEM si basano sulle best practice indicate dal team ingegneristico di AEM e sono note come [regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md).

È possibile scaricare l’attuale elenco completo delle regole [utilizzando questo collegamento](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx).

>[!IMPORTANT]
>
>A partire da giovedì 13 febbraio 2025 (Cloud Manager 2025.2.0), la qualità del codice di Cloud Manager utilizzerà una versione aggiornata di SonarQube 9.9 e un elenco aggiornato di regole che è possibile [scaricare qui](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS-2024-12-0.xlsx).

### Valutazioni a tre livelli {#three-tiered-gate}

I problemi identificati dai test di qualità del codice vengono assegnati a una delle tre categorie.

* **Critico**: si tratta di problemi che causano un errore immediato della pipeline.

* **Importante**: si tratta di problemi che causano la sospensione dell’esecuzione della pipeline. Un Responsabile della distribuzione, un Project Manager o un Proprietario business possono ignorare i problemi, consentendo alla pipeline di procedere. In alternativa, possono accettare i problemi, causando l’interruzione della pipeline con un errore.

* **Informazioni** - Problemi forniti a scopo puramente informativo e che non hanno alcun impatto sull&#39;esecuzione della pipeline

>[!NOTE]
>
>In una pipeline dedicata esclusivamente alla qualità del codice, gli errori importanti rilevati dal gate di qualità del codice non possono essere ignorati, in quanto il passaggio del test di qualità del codice rappresenta il passaggio finale dell’intera pipeline.

### Valutazioni {#ratings}

I risultati di questo passaggio vengono consegnati come **Valutazioni**.

Nella tabella seguente sono riepilogate le valutazioni e le soglie di errore per ciascuna categoria: problemi critici, importanti e informativi.

| Nome | Definizione | Categoria | Soglia di errore |
|--- |--- |--- |--- |
| Valutazione della sicurezza | A = Nessuna vulnerabilità <br/>B = Almeno 1 vulnerabilità minore<br/> C = Almeno 1 vulnerabilità importante <br/>D = Almeno 1 vulnerabilità critica <br/>E = Almeno 1 vulnerabilità bloccante | Critico | &lt; B |
| Valutazione dell’affidabilità | A = Nessun bug <br/>B = almeno 1 bug minore <br/>C = almeno 1 bug importante <br/>D = Almeno 1 bug critico <br>E = almeno 1 bug bloccante | Critico | &lt; D |
| Valutazione della manutenibilità | Definito dal costo residuo della correzione dei code smell come percentuale del tempo già trascorso nell’applicazione<br/><ul><li>A = &lt;= 5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = > 50%</li></ul> | Importante | &lt; A |
| Copertura | Definito da una combinazione di copertura di righe e copertura di condizioni dello unit test utilizzando la formula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = condizioni già valutate come `true` almeno una volta durante l’esecuzione degli unit test</li><li>`CF` = condizioni già valutate come `false` almeno una volta durante l’esecuzione degli unit test</li><li>`LC` = righe coperte = lines_to_cover - uncovered_lines</li><li>`B` = numero totale di condizioni</li><li>`EL` = numero totale di righe eseguibili (lines_to_cover)</li></ul> | Importante | &lt; 50% |
| Unit test ignorati | Numero di unit test ignorati | Info | > 1 |
| Problemi aperti | Tipi di problemi generali: vulnerabilità, bug e code smell | Info | > 0 |
| Righe duplicate | Definito come il numero di righe presenti in blocchi duplicati. Un blocco di codice si considera duplicato nelle seguenti condizioni.<br>Progetti non Java:<ul><li>Devono esserci almeno 100 token successivi e duplicati.</li><li>Tali token devono essere distribuiti, per lo meno, come segue: </li><li>30 righe di codice per COBOL </li><li>20 righe di codice per ABAP </li><li>10 righe di codice per altri linguaggi</li></ul>Progetti Java:<ul></li><li> Devono essere presenti almeno 10 istruzioni successive e duplicate indipendentemente dal numero di token e righe.</li></ul>Le differenze nel rientro e nelle stringhe letterali vengono ignorate quando si rilevano duplicati. | Info | > 1% |
| Compatibilità con Cloud Service | Numero di problemi di compatibilità con Cloud Service identificati | Info | > 0 |

>[!NOTE]
>
>Per ulteriori dettagli sulle definizioni, consulta il documento [Definizioni delle metriche di SonarQube](https://docs.sonarsource.com/sonarqube-server/latest/user-guide/code-metrics/metrics-definition/).

>[!NOTE]
>
>Per ulteriori informazioni sulle regole per la qualità del codice personalizzato eseguite da [!UICONTROL Cloud Manager], consulta [Regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Gestione dei falsi positivi {#dealing-with-false-positives}

Il processo di controllo qualità non è perfetto e talvolta identifica erroneamente problemi che non sono effettivamente problemi. Questo stato è denominato **falso positivo**.

In questi casi, il codice sorgente può essere annotato con l’annotazione Java standard `@SuppressWarnings` che specifica l’ID della regola come attributo dell’annotazione. Tra i falsi positivi comuni si annovera ad esempio il caso in cui la regola SonarQube per rilevare le password hardcoded può essere molto rigida riguardo al modo in cui una password hardcoded viene identificata.

Il codice riportato di seguito è abbastanza comune in un progetto AEM, che presenta un codice per la connessione a un servizio esterno.

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube genera una vulnerabilità di blocco. Dopo aver rivisto il codice, riconosci che tale errore non è una vulnerabilità e puoi annotare il codice con l’ID della regola appropriata.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Tuttavia, se in realtà il codice era:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

la soluzione corretta è rimuovere la password hardcoded.

>[!NOTE]
>
>Sebbene sia consigliabile rendere l&#39;annotazione `@SuppressWarnings` il più specifica possibile, ad esempio annotando solo l&#39;istruzione o il blocco causa del problema, è anche possibile aggiungere annotazioni a livello di classe.

>[!NOTE]
>Sebbene non esista un esplicito passaggio per i test di sicurezza, durante il passaggio di qualità del codice vengono valutate alcune regole per la qualità del codice relative alla sicurezza. Per ulteriori informazioni sulla sicurezza in Cloud Service, consulta [Panoramica sulla sicurezza di AEM as a Cloud Service](/help/security/cloud-service-security-overview.md).

## Ottimizzazione dell’analisi dei pacchetti di contenuti {#content-package-scanning-optimization}

Come parte del processo di analisi della qualità, Cloud Manager esegue l’analisi dei pacchetti di contenuti prodotti dalla build Maven. Cloud Manager offre ottimizzazioni per accelerare questo processo, che è efficace quando si osservano determinati vincoli relativi ai pacchetti. L’ottimizzazione più significativa riguarda i progetti che producono un singolo pacchetto &quot;all&quot; (tutti), contenente più pacchetti di contenuto della build contrassegnati come ignorati. Quando Cloud Manager rileva questo scenario, anziché decomprimere il pacchetto “all”, i singoli pacchetti di contenuti vengono analizzati direttamente e ordinati in base alle dipendenze. Consideriamo ad esempio il seguente output di build.

* `all/myco-all-1.0.0-SNAPSHOT.zip` (pacchetto di contenuti)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (pacchetto di contenuti ignorato)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (pacchetto di contenuti ignorato)

Se gli unici elementi all’interno di `myco-all-1.0.0-SNAPSHOT.zip` sono i due pacchetti di contenuti ignorati, allora i due pacchetti incorporati sono analizzati al posto del pacchetto di contenuti “all”.

Per i progetti che producono decine di pacchetti incorporati, è comprovato che questa ottimizzazione consente di risparmiare fino a 10 minuti per ogni esecuzione della pipeline.

Un caso speciale può verificarsi quando il pacchetto di contenuti “all” include una combinazione di pacchetti di contenuti e bundle OSGi ignorati. Ad esempio, se `myco-all-1.0.0-SNAPSHOT.zip` contiene i due pacchetti incorporati precedentemente menzionati oltre a uno o più bundle OSGi, allora viene creato un nuovo pacchetto di contenuti minimo con i soli bundle OSGi. Questo pacchetto viene sempre denominato `cloudmanager-synthetic-jar-package` e i bundle contenuti sono inseriti in `/apps/cloudmanager-synthetic-installer/install`.

>[!NOTE]
>
>* Questa ottimizzazione non influisce sui pacchetti distribuiti in AEM.
>* La corrispondenza tra pacchetti di contenuti incorporati e pacchetti di contenuti ignorati si basa sui nomi dei file. Questa ottimizzazione non può verificarsi se più pacchetti ignorati condividono lo stesso nome di file o se il nome di file cambia durante l’incorporamento.
