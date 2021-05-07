---
title: Test della qualità del codice - Cloud Services
description: Test della qualità del codice - Cloud Services
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 2%

---

# Test di qualità del codice {#code-quality-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="Test della qualità del codice"
>abstract="Il testing della qualità del codice valuta la qualità del codice dell’applicazione. Si tratta dell’obiettivo principale di una pipeline di sola qualità del codice e viene eseguita immediatamente dopo la fase di compilazione in tutte le pipeline non di produzione e produzione."

Il testing della qualità del codice valuta la qualità del codice dell’applicazione. Si tratta dell’obiettivo principale di una pipeline di sola qualità del codice e viene eseguita immediatamente dopo la fase di compilazione in tutte le pipeline non di produzione e produzione.

Per ulteriori informazioni sui diversi tipi di pipeline, consulta [Configurazione della pipeline CI-CD](/help/implementing/cloud-manager/configure-pipeline.md) .

## Regole per la qualità del codice {#understanding-code-quality-rules}

Nel testing della qualità del codice, il codice sorgente viene analizzato per garantire che soddisfi alcuni criteri di qualità. Attualmente, questo è implementato da una combinazione di SonarQube e l&#39;esame a livello di pacchetto di contenuti utilizzando OakPAL. Ci sono più di 100 regole che combinano regole Java generiche e regole specifiche per AEM. Alcune delle regole specifiche AEM vengono create in base alle best practice di AEM Engineering e sono denominate [Regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
>È possibile scaricare l&#39;elenco completo delle regole [qui](/help/implementing/cloud-manager/assets/CodeQuality-rules-CS.xlsx).

**Cancello a tre livelli**

In questa fase di test della qualità del codice è presente una struttura a tre livelli per i problemi identificati:

* **Critico**: Si tratta di problemi identificati dal gate che causano un errore immediato della pipeline.

* **Importante**: Questi sono problemi identificati dal gate che fanno sì che la pipeline entri in uno stato di pausa. Un manager distribuzione, un project manager o un proprietario business possono ignorare i problemi, nel qual caso la pipeline procede, oppure possono accettare i problemi, nel qual caso la pipeline si interrompe con un errore.

* **Informazioni**: Si tratta di questioni individuate dal cancello che sono fornite a scopo puramente informativo e non hanno alcun impatto sull’esecuzione della pipeline

I risultati di questo passaggio vengono consegnati come *Valutazioni*.

Nella tabella seguente sono riepilogati i rating e le soglie di errore per ciascuna categoria critica, importante e informativa:

| Nome | Definizione | Categoria | Soglia errore |
|--- |--- |--- |--- |
| Valutazione della sicurezza | A = 0 Vulnerabilità <br/>B = almeno 1 Vulnerabilità minore<br/> C = almeno 1 Vulnerabilità principale <br/>D = almeno 1 Vulnerabilità critica <br/>E = almeno 1 Vulnerabilità del blocco | Critico | &lt; B |
| Valutazione dell&#39;affidabilità | A = 0 Bug <br/>B = almeno 1 Bug secondario <br/>C = almeno 1 Bug principale <br/>D = almeno 1 Bug critico E = almeno 1 Bug blocco | Importante | &lt; C |
| Valutazione della manutenzione | Il costo eccezionale di riparazione per gli odori di codice è: <br/><ul><li>&lt;> </li><li>tra il 6% e il 10% il rating è a B </li><li>tra l&#39;11 e il 20% il rating è a C </li><li>tra il 21 e il 50% il rating è un D</li><li>qualsiasi cosa superiore al 50% è un E</li></ul> | Importante | &lt; A |
| Copertura | Una combinazione di copertura della linea di prova di unità e copertura della condizione utilizzando questa formula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)` <br/>dove: CT = condizioni che sono state valutate come &quot;true&quot; almeno una volta durante l&#39;esecuzione di unit test <br/>CF = condizioni che sono state valutate come &quot;false&quot; almeno una volta durante l&#39;esecuzione di unit test <br/>LC = linee coperte = line_to_cover - uncover_lines <br/><br/> B = numero totale di condizioni <br/>EL = numero totale di linee eseguibili (lines_to_cover) | Importante | &lt; 50% |
| Test di unità ignorati | Numero di prove di unità saltate. | Info | > 1 |
| Problemi aperti | Tipi di problemi generali - Vulnerabilità, Bug e Odori di Codice | Info | > 0 |
| Linee duplicate | Numero di righe interessate dai blocchi duplicati. <br/>Affinché un blocco di codice sia considerato duplicato:  <br/><ul><li>**Progetti non Java:**</li><li>Ci dovrebbero essere almeno 100 token successivi e duplicati.</li><li>Tali gettoni dovrebbero essere distribuiti almeno su: </li><li>30 righe di codice per COBOL </li><li>20 righe di codice per ABAP </li><li>10 righe di codice per altre lingue</li><li>**Progetti Java:**</li><li> Ci dovrebbero essere almeno 10 istruzioni successive e duplicate indipendentemente dal numero di token e righe.</li></ul> <br/>Le differenze nel rientro e nei valori letterali stringa vengono ignorate durante il rilevamento di duplicati. | Info | > 1% |
| Compatibilità Cloud Service | Numero di problemi di compatibilità Cloud Service identificati. | Info | > 0 |

>[!NOTE]
>
>Per definizioni più dettagliate, fai riferimento a [Definizioni metriche](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) .


>[!NOTE]
>
>Per ulteriori informazioni sulle regole per la qualità del codice personalizzato eseguite da [!UICONTROL Cloud Manager], consulta [Regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Gestione dei falsi positivi {#dealing-with-false-positives}

Il processo di scansione della qualità non è perfetto e talvolta identificherà erroneamente problemi che non sono effettivamente problematici. Questo viene indicato come *falso positivo*.

In questi casi, il codice sorgente può essere annotato con l’annotazione Java standard `@SuppressWarnings` che specifica l’ID regola come attributo dell’annotazione. Ad esempio, un problema comune è che la regola SonarQube per rilevare le password codificate può essere aggressiva riguardo a come viene identificata una password hardcoded.

Per osservare un esempio specifico, questo codice è abbastanza comune in un progetto AEM con codice per la connessione a un servizio esterno:

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube solleverà quindi una vulnerabilità di blocco. Dopo aver esaminato il codice, identifichi che questa non è una vulnerabilità e puoi annotarla con l’ID regola appropriato.

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
>
>È buona norma rendere l’annotazione `@SuppressWarnings` il più specifica possibile, ovvero annotare solo l’istruzione o il blocco specifici che causa il problema, ma è possibile annotarla a livello di classe.

>[!NOTE]
>Anche se non esiste un passaggio esplicito di test della sicurezza, durante il passaggio sulla qualità del codice sono ancora presenti regole di qualità del codice relative alla sicurezza valutate. Per ulteriori informazioni sulla sicurezza nel Cloud Service, consulta [Panoramica sulla sicurezza per AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) .
