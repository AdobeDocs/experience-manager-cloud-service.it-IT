---
title: Test dell’audit dell’esperienza
description: Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 90%

---


# Test dell’audit dell’esperienza {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Test dell’audit dell’esperienza"
>abstract="Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO."

Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO.

## Panoramica {#overview}

L’audit dell’esperienza è una funzione disponibile nelle pipeline di produzione di Cloud Manager Sites atta a convalidare il processo di distribuzione e garantire che le modifiche implementate:

1. soddisfino gli standard di base per prestazioni, accessibilità, best practice, SEO (Search Engine Optimization) e PWA (app web progressiva);

1. non introducano regressioni.

L’audit dell’esperienza in Cloud Manager assicura che l’esperienza dell’utente sul sito sia degli standard più elevati.

I risultati dell’audit sono informativi e consentono agli utenti con ruolo Responsabile dell’implementazione di visualizzare i punteggi e cosa è cambiato tra i punteggi correnti e precedenti. Questa informazione è utile per determinare l’eventuale introduzione di una regressione con la distribuzione corrente.

L’audit dell’esperienza è basato su Google Lighthouse, uno strumento open source di Google abilitato in tutte le pipeline di produzione di Cloud Manager.

>[!INFO]
>
>A partire dal 31 agosto 2023, l’audit dell’esperienza passerà alla visualizzazione dei risultati specifici della piattaforma mobile. Tieni presente che le metriche delle prestazioni mobili in genere si registrano a un livello inferiore rispetto a quelle del desktop, pertanto in seguito a questa modifica dovresti prevedere un cambiamento nelle prestazioni riportate.

>[!TIP]
>
>Puoi configurare le pagine incluse nell’audit dell’esperienza quando [configuri la pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code).

## Comprensione dei risultati dell’audit dell’esperienza {#understanding-experience-audit-results}

L’audit dell’esperienza fornisce risultati di test aggregati e dettagliati a livello di pagina tramite la [pagina di esecuzione della pipeline di produzione](/help/implementing/cloud-manager/deploy-code.md).

* Le metriche aggregate calcolano i punteggi medi nelle pagine sottoposte a audit per migliorare le prestazioni, l’accessibilità, le best practice e la SEO (Search Engine Optimization).
* I singoli punteggi a livello di pagina sono disponibili anche tramite l’analisi in profondità.
* I dettagli dei punteggi consentono di visualizzare i risultati dei singoli test e ottenere indicazioni su come risolvere eventuali problemi individuati.
* Per determinare se le modifiche introdotte nella pipeline includono eventuali regressioni rispetto all’esecuzione precedente, Cloud Manager mantiene una cronologia dei risultati del test.

### Punteggi aggregati {#aggregate-scores}

Il punteggio a livello aggregato considera il punteggio medio delle pagine incluse nell’esecuzione. La modifica al livello aggregato rappresenta il punteggio medio delle pagine nell’esecuzione corrente rispetto alla media dei punteggi dell’esecuzione precedente, anche se la raccolta di pagine configurata per l’inclusione è stata modificata tra le esecuzioni.

È disponibile un punteggio a livello aggregato per ogni tipo di test, ad esempio prestazioni, accessibilità, SEO e best practice.

La metrica relativa al cambiamento può presentare uno dei seguenti valori.

* **Valore positivo**: rispetto all’ultima esecuzione della pipeline di produzione, nel test selezionato le pagine sono migliorate.

* **Valore negativo**: rispetto all’ultima esecuzione della pipeline di produzione, nel test selezionato le pagine hanno subito una regressione.

* **Nessun cambiamento**: rispetto all’ultima esecuzione della pipeline di produzione, le pagine hanno ottenuto lo stesso punteggio.

* **N/D**: non è disponibile alcun punteggio precedente con cui confrontare il dato.

![Risultati dell’audit dell’esperienza](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### Punteggi a livello di pagina {#page-level-scores}

Analizzando in profondità uno dei test, è possibile accedere a un punteggio più dettagliato a livello di pagina. Puoi visualizzare il punteggio ottenuto dalle singole pagine per il test specifico e i cambiamenti rispetto all’esecuzione del test precedente.

Facendo clic sui dettagli di una pagina, puoi accedere alle informazioni sugli elementi valutati e a indicazioni per risolvere i problemi in caso vengano rilevate opportunità di miglioramento.

![Punteggi a livello di pagina](/help/implementing/cloud-manager/assets/exp-audit-2.png)
