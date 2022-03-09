---
title: Test di Experience Audit
description: Scopri in che modo Experience Audit convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base per prestazioni, accessibilità, best practice e SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 15de47e28e804fd84434d5e8e5d2fe8fe6797241
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---


# Test di Experience Audit {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Test di Experience Audit"
>abstract="Scopri in che modo Experience Audit convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base per prestazioni, accessibilità, best practice e SEO."

Scopri in che modo Experience Audit convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base per prestazioni, accessibilità, best practice e SEO.

## Panoramica {#overview}

Experience Audit è una funzione disponibile nelle pipeline di produzione di Cloud Manager Sites che convalida il processo di distribuzione e garantisce che le modifiche siano implementate:

1. Soddisfare gli standard di base per prestazioni, accessibilità, best practice, SEO (Search Engine Optimization) e PWA (Progressive Web App).

1. Non introdurre regressioni.

Experience Audit in Cloud Manager assicura che l&#39;esperienza dell&#39;utente finale sul sito sia degli standard più elevati.

I risultati del controllo di audit sono informativi e consentono al gestore della distribuzione di visualizzare i punteggi e il cambiamento tra i punteggi correnti e precedenti. Questa informazione è utile per determinare se vi è una regressione che verrà introdotta con la distribuzione corrente.

Experience Audit è basato su Google Lighthouse, uno strumento open source di Google ed è abilitato in tutte le pipeline di produzione di Cloud Manager.

## Risultati di Experience Audit {#understanding-experience-audit-results}

Experience Audit fornisce risultati di test aggregati e dettagliati a livello di pagina tramite [pagina di esecuzione della pipeline di produzione.](/help/implementing/cloud-manager/deploy-code.md)

* Le metriche di aggregazione misurano i punteggi medi nelle pagine sottoposte a controllo per migliorare le prestazioni, l’accessibilità, le best practice, SEO (Search Engine Optimization).
* I singoli punteggi a livello di pagina sono disponibili anche tramite drill-down.
* Sono disponibili dettagli dei punteggi per visualizzare i risultati dei singoli test e indicazioni su come risolvere eventuali problemi individuati.
* In Cloud Manager viene mantenuta una cronologia dei risultati del test per determinare se le modifiche introdotte nella pipeline includono eventuali regressioni rispetto all’esecuzione precedente.

### Aggregare i punteggi {#aggregate-scores}

Il punteggio di livello aggregato prende il punteggio medio delle pagine incluse nell’esecuzione. La modifica a livello di aggregato rappresenta il punteggio medio delle pagine nell’esecuzione corrente rispetto alla media dei punteggi dell’esecuzione precedente, anche se la raccolta di pagine configurate per l’inclusione è stata modificata tra le esecuzioni.

È disponibile un punteggio a livello aggregato per ogni tipo di test, ad esempio prestazioni, accessibilità, SEO e best practice.

La metrica di modifica può avere uno dei seguenti valori.

* **Valore positivo** - Le pagine sono migliorate nel test selezionato dall’ultima esecuzione della pipeline di produzione.

* **Valore negativo** - le pagine sono state ripristinate nel test selezionato dall&#39;ultima esecuzione della pipeline di produzione.

* **Nessuna modifica** - Il punteggio delle pagine è lo stesso dall’ultima esecuzione della pipeline di produzione.

* **N/D** - Nessun punteggio precedente disponibile per il confronto.

![Risultati di Experience Audit](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### Punteggi a livello di pagina {#page-level-scores}

Effettuando il drilling verso uno qualsiasi dei test, è disponibile un punteggio più dettagliato a livello di pagina. Puoi vedere il punteggio ottenuto dalle singole pagine per il test specifico e la modifica rispetto all’esecuzione del test precedente.

Facendo clic nei dettagli di una singola pagina, vengono fornite informazioni sugli elementi della pagina valutati e indicazioni per risolvere i problemi in caso di rilevamento di opportunità di miglioramento.

![Punteggi a livello di pagina](/help/implementing/cloud-manager/assets/exp-audit-2.png)
