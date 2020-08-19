---
title: Test della qualità del codice - Cloud Services
description: Test della qualità del codice - Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 3%

---


# Verifica della qualità del codice {#code-quality-testing}

Il test della qualità del codice valuta la qualità del codice dell’applicazione. Si tratta dell&#39;obiettivo principale di una conduttura di sola qualità del codice ed è eseguito immediatamente dopo la fase di costruzione in tutti i gasdotti non di produzione e produzione.

Per ulteriori informazioni sui diversi tipi di tubazioni, vedere [Configurazione della tubazione](/help/implementing/cloud-manager/configure-pipeline.md) CI-CD.

## Regole per la qualità del codice personalizzato {#understanding-code-quality-rules}

In Test qualità codice, il codice sorgente viene analizzato per garantire che soddisfi determinati criteri di qualità. Attualmente, questo è implementato tramite una combinazione di SonarQube e l&#39;esame a livello di pacchetto di contenuti tramite OakPAL. Ci sono più di 100 regole che combinano regole Java generiche e regole AEM specifiche. Alcune delle regole specifiche AEM vengono create in base alle best practice di AEM Engineering e sono denominate regole [di qualità del codice](/help/implementing/cloud-manager/custom-code-quality-rules.md)personalizzate.

>[!NOTE]
>Puoi scaricare l&#39;elenco completo delle regole [qui](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx).

I risultati di questo passaggio vengono presentati come *Valutazione*. La tabella seguente riassume la valutazione per i criteri di prova:

| Nome | Definizione | Categoria | Soglia di errore |
|--- |--- |--- |--- |
| Valutazione sicurezza | A = 0 Vulnerabilità <br/>B = almeno 1 Vulnerabilità<br/> minore C = almeno 1 Vulnerabilità maggiore <br/>D = almeno 1 Vulnerabilità critica <br/>E = almeno 1 Vulnerabilità blocco | Critico | &lt; B |
| Valutazione affidabilità | A = 0 Bug <br/>B = almeno 1 Bug Minore <br/>C = almeno 1 Bug Principale <br/>D = almeno 1 Bug Critico E = almeno 1 Bug Blocco | Importante | &lt; C |
| Classificazione manutenibilità | L&#39;eccezionale costo di riparazione per gli odori di codice è: <br/><ul><li>&lt;=5% del tempo che è già passato nell&#39;applicazione, la valutazione è A </li><li>tra il 6 e il 10% il rating è a B </li><li>tra l&#39;11% e il 20% il rating è a C </li><li>tra il 21% e il 50% la valutazione è una D</li><li>un valore superiore al 50% è un E</li></ul> | Importante | &lt; A |
| Copertura | Una combinazione di copertura della linea di prova di unità e copertura della condizione utilizzando la seguente formula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>dove: CT = condizioni che sono state valutate come &#39;true&#39; almeno una volta durante l&#39;esecuzione di unit test <br/>CF = condizioni che sono state valutate come &#39;false&#39; almeno una volta durante l&#39;esecuzione di unit test <br/>LC = linee coperte = lines_to_cover - uncover_lines <br/><br/> B = numero totale di condizioni <br/>EL = numero totale di linee eseguibili (lines_to_cover) | Importante | &lt; 50% |
| Test di unità ignorati | Numero di unit test ignorati. | Info | > 1 |
| Problemi aperti | Tipi di problemi generali - Vulnerabilità, bug e odori di codice | Info | > 0 |
| Linee duplicate | Numero di righe coinvolte in blocchi duplicati. <br/>Per considerare un blocco di codice come duplicato: <br/><ul><li>**Progetti non Java:**</li><li>Devono essere presenti almeno 100 token successivi e duplicati.</li><li>Tali token devono essere ripartiti almeno su: </li><li>30 righe di codice per COBOL </li><li>20 righe di codice per ABAP </li><li>10 righe di codice per altre lingue</li><li>**Progetti Java:**</li><li> Devono essere presenti almeno 10 istruzioni successive e duplicate, indipendentemente dal numero di token e di righe.</li></ul> <br/>Le differenze nei rientri e nei letterali di stringa vengono ignorate durante il rilevamento di duplicati. | Info | > 1% |
| Compatibilità Cloud Service | Numero di problemi di compatibilità Cloud Service identificati. | Info | > 0 |

>[!NOTE]
>
>Per informazioni più dettagliate, fare riferimento a Definizioni [metriche](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) .


>[!NOTE]
>
>Per ulteriori informazioni sulle regole di qualità del codice personalizzate eseguite da [!UICONTROL Cloud Manager], consulta Regole [di qualità del codice](/help/implementing/cloud-manager/custom-code-quality-rules.md)personalizzate.

## Gestione dei falsi positivi {#dealing-with-false-positives}

Il processo di scansione della qualità non è perfetto e a volte identificherà erroneamente i problemi che non sono effettivamente problematici. Questo viene definito &quot;falso positivo&quot;.

In questi casi, il codice sorgente può essere annotato con l&#39; `@SuppressWarnings` annotazione Java standard che specifica l&#39;ID regola come attributo annotazione. Ad esempio, un problema comune è che la regola SonarQube per rilevare le password hardcoded può essere aggressiva per quanto riguarda il modo in cui viene identificata una password hardcoded.

Per osservare un esempio specifico, questo codice è abbastanza comune in un progetto AEM con codice per la connessione a un servizio esterno:

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

>[!NOTE]
>Anche se non è presente un passaggio esplicito di verifica della sicurezza, durante il passaggio della qualità del codice sono ancora presenti regole di qualità del codice relative alla sicurezza valutate. Per ulteriori informazioni sulla sicurezza in Cloud Service Cloud Service, fare riferimento a Panoramica sulla [sicurezza per AEM come](/help/security/cloud-service-security-overview.md) .
