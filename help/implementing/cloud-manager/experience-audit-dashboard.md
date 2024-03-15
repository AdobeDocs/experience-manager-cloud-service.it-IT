---
title: Dashboard di Experience Audit
description: Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO tramite un’interfaccia dashboard chiara e informativa.
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
source-git-commit: 3ba5184275e539027728ed134c47f66fa4746d9a
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 7%

---


# Dashboard di Experience Audit {#experience-audit-dashboard}

Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO tramite un’interfaccia dashboard chiara e informativa.

>[!NOTE]
>
>Questa funzione è disponibile solo per [il programma di adozione anticipata.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)
>
>Per informazioni dettagliate sulla funzione Audit dell’esperienza esistente per AEM as a Cloud Service, consulta il documento [Test di Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md)

## Panoramica {#overview}

L’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche implementate:

1. soddisfino gli standard di base per prestazioni, accessibilità, best practice, SEO (Search Engine Optimization) e PWA (app web progressiva);

1. non introducano regressioni.

L’audit dell’esperienza in Cloud Manager assicura che l’esperienza dell’utente sul sito sia degli standard più elevati.

I risultati dell’audit sono informativi e consentono agli utenti con ruolo Responsabile dell’implementazione di visualizzare i punteggi e cosa è cambiato tra i punteggi correnti e precedenti. Questa informazione è utile per determinare l’eventuale introduzione di una regressione con la distribuzione corrente.

Audit dell’esperienza è basato su [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/), uno strumento open source di Google, ed è abilitato in tutte le pipeline di produzione di Cloud Manager.

## Disponibilità {#availability}

L’audit dell’esperienza è disponibile per Cloud Manager:

* Pipeline di produzione dei siti, per impostazione predefinita
* Sviluppo di pipeline full stack, facoltativamente
* Sviluppo di pipeline front-end, facoltativamente

Consulta la [Sezione Configurazione](#configuration) per ulteriori informazioni su come configurare il controllo di audit per gli ambienti opzionali.

I controlli di audit vengono eseguiti come parte della pipeline. I controlli di audit possono anche essere [esecuzione su richiesta](#on-demand) al di fuori delle pipeline.

## Configurazione {#configuration}

L’audit dell’esperienza è disponibile per impostazione predefinita per le pipeline di produzione. Facoltativamente, può essere abilitato per lo sviluppo di pipeline full stack e front-end. In tutti i casi, è necessario definire quali percorsi di contenuto vengono valutati durante l’esecuzione della pipeline.

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

## Risultati dell’audit dell’esperienza {#results}

I risultati dell’audit dell’esperienza sono presentati nel **Test dello staging** fase della pipeline di produzione tramite [pagina di esecuzione della pipeline di produzione.](/help/implementing/cloud-manager/deploy-code.md)

![Dashboard nella pipeline](assets/experience-audit-dashboard.jpg)

L’audit dell’esperienza fornisce la mediana dei punteggi di Google Lighthouse per [pagine configurate](#configuration) e la differenza di punteggio rispetto alla scansione precedente.

Da questa visualizzazione di riepilogo in **Test dello staging** della pipeline, sono disponibili due opzioni:

* **[Visualizza pagine più lente](#view-slowest-pages)**
* **[Visualizza report completo](#view-full-report)**

Oltre al riepilogo presentato nei dettagli di un’esecuzione della pipeline, puoi anche accedere direttamente ai risultati completi del controllo di audit utilizzando **Rapporti** della dashboard di Cloud Manager per accedere [la relazione completa](#view-full-report) direttamente.

>[!TIP]
>
>Nelle sezioni seguenti viene descritto come visualizzare i risultati dell’audit dell’esperienza.
>
>* Per informazioni dettagliate sul funzionamento del controllo di audit, consulta la sezione [Dettagli sulla valutazione dell’audit dell’esperienza.](#details)
>* Per informazioni su come eseguire un audit dell’esperienza su richiesta, consulta la sezione [Rapporti di audit on-demand.](#on-demand)
>* Se riscontri problemi con il controllo di audit, consulta la sezione [L’Audit Dell’Esperienza Riscontra Problemi.](#issues)
>* Per suggerimenti generali sulle prestazioni, consulta la sezione [Suggerimenti generali sulle prestazioni](#performance-tips)

### Visualizza pagine più lente {#view-slowest-pages}

Toccare o fare clic **Visualizza pagine più lente** apre il **Più lento di 5 pagine** , che mostra le cinque pagine con le prestazioni più basse [configurato per il controllo.](#configuration)

![Cinque più lenti](assets/experience-audit-slowest-five.jpg)

I punteggi sono suddivisi per **Prestazioni**, **Accessibilità**, **Best practice**, e **SEO** insieme alla deviazione di ciascuna metrica dall’ultimo controllo di audit.

Per impostazione predefinita, la finestra di dialogo si apre con i punteggi per i dispositivi mobili. È possibile modificare i punteggi del desktop utilizzando **Dispositivi** nella parte superiore della finestra di dialogo.

La finestra di dialogo offre una panoramica rapida. Per informazioni complete, tocca o fai clic su **Visualizza report completo**.

### Visualizza report completo {#view-full-report}

Per visualizzare il rapporto completo sull’audit dell’esperienza:

* Toccare o fare clic **Visualizza report completo** nel **[Più lento di 5 pagine](#view-slowest-pages)** .
* Toccare o fare clic **Visualizza report completo** quando si visualizza [esecuzione di una pipeline.](#results)
* Tocca o fai clic su **Rapporti** in Cloud Manager.

Il **Rapporti** di Cloud Manager, che mostra la **Audit dell’esperienza**.

![Rapporti di audit dell’esperienza](assets/experience-audit-reports.png)

La relazione si articola in due aree:

* **[Punteggi di pagina - tendenza](#trend)**
* **[Risultati analisi audit dell’esperienza](#results)**

#### Punteggi pagina - tendenza {#trend}

Per impostazione predefinita, la vista selezionata per **Punteggi di pagina - tendenza** è **punteggi mediani** per **Ultimi 6 mesi**.

Utilizza il **Seleziona** e **Visualizza** menu a discesa nella parte superiore e inferiore del pulsante grafico per selezionare rispettivamente dettagli specifici della pagina e diversi intervalli di tempo. Tocca o fai clic su e sul pulsante **tendenza aggiornamento** nella parte superiore del grafico per applicare le selezioni e aggiornare il grafico.

Quando si sposta il mouse sul grafico, una descrizione comando visualizza i valori per le categorie di Google Lighthouse in specifici momenti nel tempo.

![Dettagli tendenza](assets/experience-audit-trend-details.png)

Se tocchi o fai clic sul grafico in un determinato momento, viene visualizzato un messaggio con i dettagli della scansione. Tocca o fai clic su **apri analisi audit esperienza** per caricare i risultati della scansione in **[Risultati analisi audit dell’esperienza](#scan-results)** sezione.

![Seleziona un&#39;altra scansione](assets/experience-audit-open-scan.png)

#### Risultati analisi audit esperienza {#scan-results}

Il **Risultati analisi audit dell’esperienza** fornisce consigli su come migliorare il punteggio e i dettagli di tutte le pagine digitalizzate. È diviso in due sezioni:

* **[Recommendations](#recommendations)**
* **[Pagine digitalizzate](#scanned-pages)**

##### Consigli {#recommendations}

Il **Recommendations** mostra un set aggregato di informazioni approfondite. Per impostazione predefinita, i consigli per **prestazioni** vengono visualizzati. Utilizza il menu a discesa accanto al **Recommendations** per passare a un’altra categoria.

![Recommendations](assets/experience-audit-recommendations.png)

Tocca o fai clic sulla freccia per visualizzare i dettagli di qualsiasi consiglio.

![Dettagli consiglio](assets/experience-audit-recommendation-details.png)

Quando disponibili, i dettagli espansi dei consigli contengono anche la percentuale di impatto dei consigli, per concentrarti sui cambiamenti più incisivi.

Tocca o fai clic su **visualizza pagine** nella visualizzazione dettagli per visualizzare le pagine a cui si applica il consiglio.

![Pagine per i dettagli dei consigli](assets/experience-audit-details-pages.png)

##### Pagine digitalizzate {#scanned-pages}

Il **Pagine digitalizzate** Questa sezione fornisce punteggi dettagliati su tutte le pagine digitalizzate. È possibile utilizzare **Precedente** e **Successivo** per scorrere i risultati e scegliere il numero di pagine da visualizzare.

![Pagine digitalizzate](assets/experience-audit-scanned-pages.png)

Toccando o facendo clic sul collegamento di una pagina particolare, si aggiorna la **Seleziona** filtro del [**Punteggi di pagina - tendenza** sezione](#trend) e mostra la **Punteggi e raccomandazioni** per la pagina selezionata.

![Risultati pagina](assets/experience-audit-page-results.png)

Il **Rapporti non elaborati** Questa scheda ti fornisce punteggi per ogni controllo di audit della pagina. Tocca o fai clic su **Scarica** per recuperare un file JSON dei dati non elaborati.

![Report non elaborato](assets/experience-audit-raw-reports.png)

Verrà aperta una nuova scheda nel browser che punta a `https://googlechrome.github.io/lighthouse/viewer/` con un URL firmato del report JSON (JavaScript Object Notation) non elaborato di Lighthouse per la pagina selezionata, che si apre automaticamente per l’ispezione dettagliata

![Visualizzazione del rapporto non elaborato](assets/experience-audit-view-raw-report.png)

## Rapporti di audit on-demand {#on-demand}

Oltre a essere eseguiti durante l’esecuzione della pipeline, i rapporti di audit dell’esperienza possono essere generati on-demand. Questa è una buona soluzione per eseguire rapidamente la scansione delle pagine, senza dover eseguire una pipeline.

Per eseguire un&#39;analisi on-demand, passare alla  **Rapporti** per visualizzare il rapporto di audit completo, quindi tocca o fai clic sul pulsante **Esegui scansione** pulsante.

![Scansione su richiesta](assets/experience-audit-on-demand.png)

Le scansioni on-demand attivano un audit dell’esperienza per gli ultimi 25 [pagine configurate](#configuration) e in genere termina in pochi minuti.

Al termine, il grafico dei punteggi verrà aggiornato automaticamente e potrai esaminare i risultati esattamente come per una scansione dell’esecuzione della pipeline.

Puoi filtrare il grafico dei punteggi in base al tipo di trigger utilizzando **Trigger** selettore.

![Attiva filtro](assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>È possibile avviare una scansione on-demand solo se l’ambiente non viene eliminato e non sono presenti altre scansioni in sospeso nello stesso ambiente.

## L’audit dell’esperienza riscontra problemi {#issues}

Se [pagine configurate](#configuration) L’audit dell’esperienza ne tiene conto.

La pipeline mostra una sezione di errore espandibile per visualizzare i percorsi URL relativi a cui non poteva accedere.

![Problemi riscontrati dall’audit dell’esperienza](assets/experience-audit-issues.jpg)

Se visualizzi il rapporto completo, i dettagli sono visualizzati nella sezione **[Risultati analisi audit dell’esperienza](#results)** sezione.

![Problemi relativi ai rapporti completi](assets/experience-audit-issues-reports.jpeg)

Alcuni motivi per cui le pagine potrebbero non essere disponibili sono i seguenti:

* La configurazione blocca l’accesso.
* La pagina non esiste.
* La pagina viene reindirizzata richiedendo un’autenticazione diversa da quella di base.
* Si è verificato un problema interno.
* Ecc.

>[!TIP]
>
>[Accesso ai rapporti non elaborati](#scanned-pages) per una pagina può fornire dettagli sul motivo per cui non è stato possibile sottoporre a controllo la pagina.

## Suggerimenti generali sulle prestazioni {#performance-tips}

Due dei problemi di impatto più comuni e facili da risolvere riguardano Cumulative Layout Shifts (CLS) e Largest Contentful Paint (LCP).

Questi possono essere migliorati:

* Caricamento non lento delle immagini sopra la piega (il contenuto visibile nel browser senza dover scorrere verso il basso).
* Assegnare la corretta priorità al modo in cui le risorse vengono caricate (ad esempio, caricando in modo asincrono le immagini sotto la piega dopo il caricamento del documento).
* Preacquisizione di file JavaScript e CSS utilizzati per eseguire il rendering del contenuto sopra la piega (se necessari).
* Riservare lo spazio verticale assegnando proporzioni ai contenitori che vengono caricati lentamente o renderizzati in un secondo momento.
* Conversione di immagini in formato WebP per ridurne le dimensioni.
* Utilizzo di `<picture>` e immagine `srcset` con dimensioni dell&#39;immagine diverse per le diverse dimensioni dei riquadri di visualizzazione (e per garantire il corretto funzionamento del ridimensionamento).

## Dettagli della valutazione di Experience Audit {#details}

I dettagli seguenti forniscono informazioni aggiuntive su come l’audit dell’esperienza valuta il sito. Non sono necessarie per l’utilizzo generale della funzione e sono fornite qui per completezza.

* Anche se il [percorsi pagina di Experience Audit configurati](#configuration) mostra `.com` dell’editore, il controllo di audit esegue la scansione dell’origine (`.net`), per garantire che vengano rilevati i problemi introdotti durante lo sviluppo.
   * Il `.com` Il dominio utilizza una rete CDN e potrebbe fornire punteggi migliori o contenere risultati memorizzati nella cache.
* Nelle pipeline full stack di produzione, viene analizzato l’ambiente di staging.
   * Per garantire che il controllo fornisca dettagli rilevanti durante il controllo, il contenuto dell’ambiente di staging deve essere il più simile possibile all’ambiente di produzione.
* Le pagine visualizzate nel **Seleziona** menu a discesa nella [**Punteggi di pagina - tendenza** sezione](#trend) sono tutte le pagine note analizzate in passato dall’audit dell’esperienza.
* [Un consiglio](#recommendations) può avere un guadagno potenziale e una differenza rispetto alla scansione precedente.
   * L’audit dell’esperienza stima il guadagno potenziale elaborando il rapporto non elaborato per ogni pagina e correlando i byte sprecati o i millisecondi con un’informazione approfondita che ha un impatto ponderato sul punteggio delle prestazioni.
   * L’audit fornisce queste informazioni (nonché le pagine interessate) per aiutare a decidere quale raccomandazione perseguire.
   * Per maggiori dettagli, vedere [Sezione Suggerimenti generali sulle prestazioni](#performance-tips)
* Dato che una pipeline front-end può essere distribuita in un ambiente esistente (oppure che più pipeline front-end hanno come destinazione lo stesso ambiente) e i risultati della scansione sono aggregati a livello di ambiente, i punteggi, le tendenze e i consigli vengono visualizzati nello stesso ambiente selezionato, indipendentemente dall’esecuzione della pipeline che ha attivato la scansione.
