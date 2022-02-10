---
title: Test della qualità del codice
description: Scopri come funziona il test della qualità del codice delle pipeline e come può migliorare la qualità delle distribuzioni.
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: ca3c1f255b8441a8d376a55a5353d58848384b8b
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 2%

---

# Test della qualità del codice {#code-quality-testing}

Scopri come funziona il test della qualità del codice delle pipeline e come può migliorare la qualità delle distribuzioni.

>[!CONTEXTUALHELP]
>
>
## Introduzione {#introduction}

Il test della qualità del codice valuta il codice dell’applicazione in base a un set di regole di qualità. È lo scopo principale di una pipeline di sola qualità del codice e viene eseguita immediatamente dopo la fase di compilazione in tutte le pipeline di produzione e non di produzione.

Consulta il documento [Configurazione della pipeline CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) per ulteriori informazioni sui diversi tipi di gasdotti.

## Regole per la qualità del codice {#understanding-code-quality-rules}

Il test di qualità del codice esegue la scansione del codice sorgente per garantire che soddisfi determinati criteri di qualità. Questa funzione è implementata tramite una combinazione di SonarQube e un esame a livello di pacchetto dei contenuti tramite OakPAL. Ci sono più di 100 regole, che combinano regole Java generiche e regole specifiche per AEM. Alcune delle regole specifiche AEM vengono create in base alle best practice di AEM Engineering e sono denominate [regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
Scaricare l’elenco completo delle regole [con questo collegamento.](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)

### Valutazioni a tre livelli {#three-tiered-gate}

I problemi identificati dai test di qualità del codice sono assegnati a una delle tre categorie.

* **Critico** - Si tratta di questioni che causano un immediato fallimento del gasdotto.

* **Importante** - Si tratta di problemi che fanno sì che la pipeline entri in uno stato di pausa. Un manager distribuzione, un project manager o un proprietario business possono ignorare i problemi, nel qual caso la pipeline procede, oppure possono accettare i problemi, nel qual caso la pipeline si interrompe con un errore.

* **Info** - Si tratta di questioni che vengono fornite a scopo puramente informativo e che non hanno alcun impatto sull’esecuzione della conduttura

I risultati di questo passaggio vengono consegnati come **Valutazioni**.

Nella tabella seguente sono riepilogati i rating e le soglie di errore per ciascuna categoria critica, importante e informativa.

| Nome | Definizione | Categoria | Soglia errore |
|--- |--- |--- |--- |
| Valutazione della sicurezza | A = Nessuna vulnerabilità <br/>B = Almeno 1 vulnerabilità minore<br/> C = Almeno 1 vulnerabilità principale <br/>D = Almeno 1 vulnerabilità critica <br/>E = Almeno 1 vulnerabilità di blocco | Critico | &lt; B |
| Valutazione dell&#39;affidabilità | A = Nessun bug <br/>B = almeno 1 bug minore <br/>C = almeno 1 bug principale <br/>D = Almeno 1 bug critico<br>E = almeno 1 bug di blocco | Critico | &lt; D |
| Valutazione della manutenzione | Definito dal costo residuo di bonifica per il codice, espresso in percentuale del tempo che è già passato nell&#39;applicazione<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = >50%</li></ul> | Importante | &lt; A |
| Copertura | Definito da una combinazione di copertura della linea di prova di unità e copertura delle condizioni utilizzando la formula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = Condizioni valutate come `true` almeno una volta durante l&#39;esecuzione di prove dell&#39;unità</li><li>`CF` = Condizioni valutate come `false` almeno una volta durante l&#39;esecuzione di prove dell&#39;unità</li><li>`LC` = Linee coperte = line_to_cover - uncover_lines</li><li>`B` = numero totale di condizioni</li><li>`EL` = numero totale di righe eseguibili (lines_to_cover)</li></ul> | Importante | &lt; 50% |
| Test di unità ignorati | Numero di prove di unità saltate | Info | > 1 |
| Problemi aperti | Tipi di problemi generali - Vulnerabilità, Bug e Odori di Codice | Info | > 0 |
| Linee duplicate | Definito come il numero di righe coinvolte nei blocchi duplicati. Un blocco di codice viene considerato duplicato nelle seguenti condizioni.<br>Progetti non Java:<ul><li>Ci dovrebbero essere almeno 100 token successivi e duplicati.</li><li>Tali gettoni devono essere distribuiti almeno: </li><li>30 righe di codice per COBOL </li><li>20 righe di codice per ABAP </li><li>10 righe di codice per altre lingue</li></ul>Progetti Java:<ul></li><li> Devono essere presenti almeno 10 istruzioni successive e duplicate indipendentemente dal numero di token e righe.</li></ul>Le differenze nel rientro e nei valori letterali stringa vengono ignorate quando si rilevano duplicati. | Info | > 1% |
| Compatibilità Cloud Service | Numero di problemi di compatibilità del servizio cloud identificati | Info | > 0 |

>[!NOTE]
Fai riferimento a [Definizioni delle metriche di SonarQube](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) definizioni più dettagliate.

>[!NOTE]
Per ulteriori informazioni sulle regole di qualità del codice personalizzato eseguite da [!UICONTROL Cloud Manager], consultare il documento [Regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Gestione dei falsi positivi {#dealing-with-false-positives}

Il processo di scansione della qualità non è perfetto e talvolta identificherà erroneamente problemi che non sono effettivamente problematici. Questo è indicato come **falso positivo**.

In questi casi, il codice sorgente può essere annotato con Java standard `@SuppressWarnings` annotazione che specifica l’ID della regola come attributo di annotazione. Ad esempio, un falso positivo comune è che la regola SonarQube per rilevare le password codificate può essere aggressiva riguardo al modo in cui viene identificata una password hardcoded.

Il codice seguente è abbastanza comune in un progetto AEM, con codice per la connessione a un servizio esterno.

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube solleverà quindi una vulnerabilità di blocco. Ma dopo aver esaminato il codice, riconosci che questa non è una vulnerabilità e puoi annotare il codice con l&#39;ID regola appropriato.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Tuttavia, se il codice era effettivamente questo:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Quindi la soluzione corretta è quella di rimuovere la password hardcoded.

>[!NOTE]
Anche se è una best practice fare `@SuppressWarnings` annotazione il più possibile specifica, ovvero annotare solo l’istruzione o il blocco specifici che causano il problema, è possibile annotare a livello di classe.

>[!NOTE]
Anche se non esiste un passaggio esplicito di test della sicurezza, durante il passaggio sulla qualità del codice sono state valutate le regole di qualità del codice relative alla sicurezza. Consulta il documento [Panoramica sulla sicurezza per AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) per ulteriori informazioni sulla sicurezza in Cloud Service.

## Ottimizzazione della scansione dei pacchetti di contenuti {#content-package-scanning-optimization}

Come parte del processo di analisi della qualità, Cloud Manager esegue l’analisi dei pacchetti di contenuto prodotti dalla build Maven. Cloud Manager offre ottimizzazioni per accelerare questo processo, che sono efficaci quando vengono osservati determinati vincoli di imballaggio. La più significativa è l’ottimizzazione eseguita per i progetti che producono un singolo pacchetto di contenuti, generalmente denominato pacchetto &quot;all&quot;, che contiene una serie di altri pacchetti di contenuti prodotti dalla build, contrassegnati come saltati. Quando Cloud Manager rileva questo scenario, anziché decomprimere il pacchetto &quot;all&quot;, i singoli pacchetti di contenuto vengono analizzati direttamente e ordinati in base alle dipendenze. Ad esempio, considera il seguente output di build.

* `all/myco-all-1.0.0-SNAPSHOT.zip` (pacchetto di contenuti)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (saltato-contenuto-pacchetto)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (saltato-contenuto-pacchetto)

Se gli unici elementi all&#39;interno `myco-all-1.0.0-SNAPSHOT.zip` sono i due pacchetti di contenuto saltato, quindi i due pacchetti incorporati verranno analizzati al posto del pacchetto di contenuto &quot;all&quot;.

Per i progetti che producono decine di pacchetti incorporati, questa ottimizzazione è stata mostrata in modo da risparmiare fino a 10 minuti per esecuzione della pipeline.

Un caso speciale può verificarsi quando il pacchetto di contenuti &quot;all&quot; contiene una combinazione di pacchetti di contenuti saltati e bundle OSGi. Ad esempio, se `myco-all-1.0.0-SNAPSHOT.zip` conteneva i due pacchetti incorporati precedentemente menzionati e uno o più bundle OSGi, quindi viene costruito un nuovo pacchetto di contenuti minimali con solo i bundle OSGi. Questo pacchetto viene sempre denominato `cloudmanager-synthetic-jar-package` e i bundle contenuti sono inseriti `/apps/cloudmanager-synthetic-installer/install`.

>[!NOTE]
* Questa ottimizzazione non influisce sui pacchetti distribuiti in AEM.
* Poiché la corrispondenza tra i pacchetti di contenuto incorporati e i pacchetti di contenuto saltato si basa sui nomi di file, questa ottimizzazione non può essere eseguita se più pacchetti di contenuto saltato hanno esattamente lo stesso nome di file o se il nome di file viene modificato durante l’incorporazione.

