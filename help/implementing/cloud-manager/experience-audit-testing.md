---
title: Test dell’audit dell’esperienza
description: Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 3ba5184275e539027728ed134c47f66fa4746d9a
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 56%

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

L’audit dell’esperienza è basato su Google Lighthouse, uno strumento open source di Google.

>[!INFO]
>
>A partire dal 31 agosto 2023, l’audit dell’esperienza passerà alla visualizzazione dei risultati specifici della piattaforma mobile. Le metriche delle prestazioni mobili in genere si registrano a un livello inferiore rispetto a quelle del desktop, pertanto in seguito a questo cambiamento è necessario prevedere un cambiamento nelle prestazioni riportate.

## Disponibilità {#availability}

L’audit dell’esperienza è disponibile per Cloud Manager:

* Per impostazione predefinita, le pipeline di produzione dei siti.
* Pipeline di sviluppo front-end, facoltativamente.

Consulta la [Sezione Configurazione](#configuration) per ulteriori informazioni su come configurare il controllo di audit per gli ambienti opzionali.

## Configurazione {#configuration}

L’audit dell’esperienza è disponibile per impostazione predefinita per le pipeline di produzione. Facoltativamente, può essere abilitato per le pipeline di sviluppo front-end. In tutti i casi, è necessario definire quali percorsi di contenuto vengono valutati durante l’esecuzione della pipeline.

Puoi configurare le pagine incluse nell’audit dell’esperienza al momento della configurazione della pipeline.

1. A seconda del tipo di pipeline che desideri configurare, segui le istruzioni riportate di seguito:

   * Aggiungi un nuovo [pipeline di produzione,](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) se desideri definire i percorsi che devono essere valutati dal controllo di audit.
   * Aggiungi un nuovo [pipeline non di produzione,](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) se desideri abilitare il controllo di audit su una pipeline front-end o di sviluppo full-stack.
   * Oppure puoi [modificare una pipeline esistente,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) e aggiorna le opzioni esistenti.

1. Se stai aggiungendo o modificando una pipeline non di produzione per la quale desideri utilizzare l’audit dell’esperienza, seleziona la **Audit dell’esperienza** casella di controllo sulla **Codice sorgente** scheda.

   ![Abilitazione dell’audit dell’esperienza](assets/experience-audit-enable.jpg)

   * Questo è necessario solo per le pipeline non di produzione.
   * Il **Audit dell’esperienza** viene visualizzata quando la casella di controllo è selezionata.

1. Sia per le pipeline di produzione che per quelle non di produzione, definisci i percorsi da includere nell’audit dell’esperienza sulla **Audit dell’esperienza** scheda.

   * I percorsi delle pagine devono iniziare con `/` e sono relativi al tuo sito.
   * Ad esempio, se il sito è `wknd.site` e desidera includere `https://wknd.site/us/en/about-us.html` nell’audit dell’esperienza, immetti il percorso `/us/en/about-us.html`.

   ![Definizione di un percorso per l’audit dell’esperienza](assets/experience-audit-add-page.png)

1. Tocca o fai clic su **Aggiungi pagina** e il percorso viene completato automaticamente con l’indirizzo dell’ambiente e aggiunto alla tabella dei percorsi.

   ![Salvataggio del percorso nella tabella](assets/experience-audit-page-added.png)

1. Continua ad aggiungere i percorsi che desideri ripetendo i due passaggi precedenti.

   * Puoi aggiungere fino a un massimo di 25 percorsi.
   * Se non definisci alcun percorso, per impostazione predefinita la pagina Home del sito viene inclusa nell’audit dell’esperienza.

1. Per salvare la pipeline, fai clic su **Salva**.

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

* **Valore positivo** : rispetto all’ultima esecuzione della pipeline di produzione, nel test selezionato le pagine sono migliorate.

* **Valore negativo** - rispetto all’ultima esecuzione della pipeline di produzione, nel test selezionato le pagine hanno subito una regressione.

* **Nessuna modifica** - Le pagine hanno ottenuto lo stesso punteggio dall’ultima esecuzione della pipeline di produzione.

* **N/D**: non è disponibile alcun punteggio precedente con cui confrontare il dato.

![Risultati dell’audit dell’esperienza](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### Punteggi a livello di pagina {#page-level-scores}

Analizzando in profondità uno dei test, è possibile accedere a un punteggio più dettagliato a livello di pagina. Puoi visualizzare il punteggio ottenuto dalle singole pagine per il test specifico e i cambiamenti rispetto all’esecuzione del test precedente.

Facendo clic sui dettagli di una pagina, puoi accedere alle informazioni sugli elementi valutati e a indicazioni per risolvere i problemi in caso vengano rilevate opportunità di miglioramento.

![Punteggi a livello di pagina](/help/implementing/cloud-manager/assets/exp-audit-2.png)
