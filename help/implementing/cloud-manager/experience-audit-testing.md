---
title: Test di audit delle esperienze - Cloud Services
description: Test di audit delle esperienze - Cloud Services
translation-type: tm+mt
source-git-commit: 561345f58ce8e448176507e3bba114324dc18256
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Verifica esperienza {#experience-audit-testing}

Experience Audit è una funzione disponibile nelle pipeline di produzione di siti di Cloud Manager, uno strumento open source di Google. Questa funzione è abilitata in tutti i gasdotti di produzione di Cloud Manager.

Convalidare il processo di distribuzione e garantire che le modifiche implementate:

1. Soddisfare gli standard di base per prestazioni, accessibilità, procedure ottimali, SEO (ottimizzazione motore di ricerca) e PWA (app Web progressiva).

1. Non includete regressioni in queste dimensioni.

Experience Audit in Cloud Manager assicura che l&#39;esperienza digitale degli utenti finali sul sito possa essere mantenuta ai massimi standard. I risultati sono informativi e consentono all’utente di visualizzare i punteggi e la modifica tra i punteggi correnti e precedenti. Questa informazione è utile per determinare se esiste una regressione che verrà introdotta con la distribuzione corrente.

## Informazioni sui risultati di Experience Audit {#understanding-experience-audit-results}

Experience Audit fornisce risultati di test aggregati e dettagliati a livello di pagina tramite la pagina di esecuzione della pipeline di produzione.

* Le metriche a livello di aggregazione misurano il punteggio medio tra le pagine sottoposte a controllo per ottenere prestazioni, accessibilità, procedure ottimali, SEO (Ottimizzazione motore di ricerca).
   >[!NOTE]
   >La valutazione progressiva dell&#39;app Web (PWA) non è inclusa nella valutazione di riepilogo e verrà visualizzata solo nella schermata dei dettagli a livello di pagina.
* I singoli punteggi a livello di pagina sono disponibili anche tramite drill down.
* Sono disponibili dettagli dei punteggi per vedere quali sono i risultati dei singoli test, nonché indicazioni su come risolvere eventuali problemi individuati durante il controllo dei contenuti.
* Una cronologia dei risultati del test è persistente in Cloud Manager in modo che i clienti possano vedere se le modifiche introdotte nell&#39;esecuzione della pipeline includono eventuali regressioni dall&#39;esecuzione precedente.

### Aggrega punteggi {#aggregate-scores}

È disponibile una valutazione a livello aggregato per ogni tipo di test, ad esempio prestazioni, accessibilità, SEO e procedure ottimali.
>[!NOTE]
>La valutazione progressiva dell&#39;app Web (PWA) non è inclusa nella valutazione di riepilogo e verrà visualizzata solo nella schermata dei dettagli a livello di pagina.

Il punteggio del livello aggregato prende il punteggio medio delle pagine incluse nell&#39;esecuzione. La modifica a livello di aggregazione rappresenta il punteggio medio delle pagine nell&#39;esecuzione corrente rispetto alla media dei punteggi dell&#39;esecuzione precedente, anche se la raccolta di pagine configurate per l&#39;inclusione è stata modificata tra le esecuzioni.

Il valore della metrica Modifica può essere uno dei seguenti:

* **Valore** positivo: le pagine sono migliorate nel test selezionato dall&#39;ultima esecuzione del ciclo di produzione

* **Valore** negativo: le pagine sono state raggruppate nel test selezionato dall&#39;ultima esecuzione del ciclo di produzione

* **Nessuna modifica** : le pagine hanno ottenuto lo stesso punteggio dall&#39;ultima esecuzione del ciclo di produzione

* **N/D** - Non c&#39;era un punteggio precedente disponibile rispetto a

   ![](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### Punteggi a livello di pagina {#page-level-scores}

Effettuando il drill-through in uno dei test, è possibile visualizzare un punteggio più dettagliato sul livello di pagina. L&#39;utente sarà in grado di visualizzare il punteggio ottenuto dalle singole pagine per il test specifico insieme alla modifica rispetto all&#39;esecuzione precedente del test.

Facendo clic sui dettagli di una singola pagina verranno fornite informazioni sugli elementi della pagina che sono stati valutati e indicazioni per risolvere i problemi in caso di rilevamento di opportunità di miglioramento. I dettagli dei test e le relative indicazioni sono forniti da Google Lighthouse.

![](/help/implementing/cloud-manager/assets/exp-audit-2.png)

