---
title: Test di Experience Audit - Cloud Services
description: Test di Experience Audit - Cloud Services
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Test di Experience Audit {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Test di Experience Audit"
>abstract="Experience Audit è una funzione disponibile nelle pipeline di produzione di Cloud Manager Sites, basata su Google Lighthouse, uno strumento open source di Google. Questa funzione è abilitata in tutte le pipeline di produzione di Cloud Manager."

Experience Audit è una funzione disponibile nelle pipeline di produzione di Cloud Manager Sites, basata su Google Lighthouse, uno strumento open source di Google. Questa funzione è abilitata in tutte le pipeline di produzione di Cloud Manager.

Convalida il processo di distribuzione e assicura che le modifiche implementate:

1. Soddisfare gli standard di base per prestazioni, accessibilità, best practice, SEO (Search Engine Optimization) e PWA (Progressive Web App).

1. Non includere regressioni in queste dimensioni.

Experience Audit in Cloud Manager garantisce che l’esperienza digitale degli utenti finali sul sito possa essere mantenuta ai massimi standard. I risultati sono informativi e consentono all’utente di visualizzare i punteggi e il cambiamento tra il punteggio corrente e quello precedente. Questa informazione è utile per determinare se vi è una regressione che verrà introdotta con la distribuzione corrente.

## Risultati di Experience Audit {#understanding-experience-audit-results}

Experience Audit fornisce risultati di test aggregati e dettagliati a livello di pagina tramite la pagina di esecuzione della pipeline di produzione .

* Le metriche a livello di aggregazione misurano il punteggio medio nelle pagine sottoposte a controllo per migliorare le prestazioni, l’accessibilità, le best practice e l’ottimizzazione SEO (Search Engine Optimization).
   >[!NOTE]
   >Il punteggio progressivo dell’app Web (PWA) non è incluso nel punteggio di riepilogo e verrà visualizzato solo nella schermata dei dettagli del rapporto a livello di pagina.
* I singoli punteggi a livello di pagina sono disponibili anche tramite drill-down.
* Sono disponibili dettagli dei punteggi per vedere quali sono i risultati dei singoli test, oltre a indicazioni su come risolvere eventuali problemi identificati durante il controllo dell’esperienza.
* Una cronologia dei risultati del test viene mantenuta in Cloud Manager, in modo che i clienti possano vedere se le modifiche introdotte nell’esecuzione della pipeline includono eventuali regressioni rispetto all’esecuzione precedente.

### Aggregare i punteggi {#aggregate-scores}

È disponibile un punteggio a livello aggregato per ogni tipo di test, ad esempio prestazioni, accessibilità, SEO e best practice.
>[!NOTE]
>Il punteggio progressivo dell’app Web (PWA) non è incluso nel punteggio di riepilogo e verrà visualizzato solo nella schermata dei dettagli del rapporto a livello di pagina.

Il punteggio di livello aggregato prende il punteggio medio delle pagine incluse nell’esecuzione. La modifica a livello di aggregato rappresenta il punteggio medio delle pagine nell’esecuzione corrente rispetto alla media dei punteggi dell’esecuzione precedente, anche se la raccolta di pagine configurate per l’inclusione è stata modificata tra le esecuzioni.

Il valore della metrica di modifica può essere uno dei seguenti:

* **Valore positivo** : le pagine sono migliorate nel test selezionato dall’ultima esecuzione della pipeline di produzione

* **Valore**  negativo: le pagine sono state ripristinate nel test selezionato dall’ultima esecuzione della pipeline di produzione

* **Nessuna modifica** : le pagine hanno ottenuto lo stesso punteggio dall’ultima esecuzione della pipeline di produzione

* **N/D** : non era disponibile alcun punteggio precedente da confrontare con

   ![](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### Punteggi a livello di pagina {#page-level-scores}

Effettuando il drilling verso uno qualsiasi dei test, è possibile visualizzare un punteggio più dettagliato a livello di pagina. L’utente sarà in grado di visualizzare il punteggio delle singole pagine per il test specifico e la modifica rispetto alla precedente esecuzione del test.

Facendo clic sui dettagli di una singola pagina, verranno fornite informazioni sugli elementi della pagina valutati e indicazioni per risolvere i problemi in caso di opportunità di miglioramento. I dettagli dei test e le relative indicazioni sono forniti da Google Lighthouse.

![](/help/implementing/cloud-manager/assets/exp-audit-2.png)
