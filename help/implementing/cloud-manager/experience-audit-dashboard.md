---
title: Dashboard di Experience Audit
description: Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione, garantendo che le modifiche soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO. Fornisce un’interfaccia dashboard chiara e informativa per monitorare queste metriche.
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5dc3d571c553f2972295172c7a6d0249be3285b8
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 6%

---


# Dashboard di Experience Audit {#experience-audit-dashboard}

Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione, garantendo che le modifiche soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO. Fornisce un’interfaccia dashboard chiara e informativa per monitorare queste metriche.

## Panoramica {#overview}

L’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche vengano implementate:

1. Soddisfa gli standard di base per prestazioni, accessibilità, best practice e SEO (Search Engine Optimization).

1. non introducano regressioni.

La funzione Audit dell’esperienza in Cloud Manager garantisce che l’esperienza dell’utente sul sito sia conforme agli standard più elevati.

I risultati dell’audit sono informativi e consentono agli utenti con ruolo Responsabile dell’implementazione di visualizzare i punteggi e cosa è cambiato tra i punteggi correnti e precedenti. Questa informazione è utile per determinare l’eventuale introduzione di una regressione con la distribuzione corrente.

L&#39;audit dell&#39;esperienza è basato su [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/), uno strumento open source di Google, ed è abilitato in tutte le pipeline di produzione di Cloud Manager.

## Disponibilità {#availability}

L’audit dell’esperienza è disponibile per Cloud Manager:

* (Impostazione predefinita) Pipeline di produzione di Sites
* Sviluppo di pipeline full stack (facoltativo)
* Sviluppo di pipeline front-end (facoltativo)

Per ulteriori informazioni su come configurare il controllo di audit per gli ambienti facoltativi, vedere la [sezione Configurazione](#configuration).

I controlli di audit vengono eseguiti come parte della pipeline. I controlli di audit possono anche essere [eseguiti su richiesta](#on-demand) al di fuori delle pipeline.

## Configurazione {#configuration}

L’audit dell’esperienza è disponibile per impostazione predefinita per le pipeline di produzione. Facoltativamente, può essere abilitato per lo sviluppo di pipeline full stack e front-end. In tutti i casi, è necessario definire quali percorsi di contenuto vengono valutati durante l’esecuzione della pipeline.

1. A seconda del tipo di pipeline che desideri configurare, effettua una delle seguenti operazioni:

   * Aggiungi una nuova [pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) per definire i percorsi che dovranno essere valutati dal controllo di audit.
   * Aggiungi una nuova [pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) se desideri abilitare il controllo di audit su una pipeline front-end o full-stack di sviluppo.
   * In alternativa, è possibile [modificare una pipeline esistente](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) e aggiornare le opzioni esistenti.

1. Per utilizzare Audit dell&#39;esperienza quando si aggiunge o si modifica una pipeline non di produzione, selezionare la casella di controllo **Audit dell&#39;esperienza**. È possibile trovare questa opzione nella scheda **Codice Source**.

   ![Abilitazione dell&#39;audit dell&#39;esperienza](assets/experience-audit-enable.jpg)

   * Necessario solo per pipeline non di produzione.
   * La scheda **Audit dell&#39;esperienza** viene visualizzata quando la casella di controllo è selezionata.

1. Sia per le pipeline di produzione che per quelle non di produzione, puoi definire i percorsi da includere nell’audit dell’esperienza nella scheda **Audit dell’esperienza**.

   * I percorsi delle pagine devono iniziare con `/` e sono relativi al sito.
   * Ad esempio, se il sito è `wknd.site` e si desidera includere `https://wknd.site/us/en/about-us.html` nell&#39;audit dell&#39;esperienza, immettere il percorso `/us/en/about-us.html`.

   ![Definizione di un percorso per l’audit dell’esperienza](assets/experience-audit-add-page.png)

1. Facendo clic su **Aggiungi pagina**, il percorso viene completato automaticamente con l’indirizzo dell’ambiente e aggiunto alla tabella dei percorsi.

   ![Salvataggio del percorso nella tabella](assets/experience-audit-page-added.png)

1. Continua ad aggiungere i percorsi che desideri ripetendo i due passaggi precedenti.

   * Puoi aggiungere fino a un massimo di 25 percorsi.
   * Se non definisci alcun percorso, per impostazione predefinita la pagina Home del sito viene inclusa nell’audit dell’esperienza.

1. Fai clic su **Salva**.

## Risultati dell’audit dell’esperienza {#results}

I risultati dell&#39;audit dell&#39;esperienza sono presentati nella fase **Test dello staging** della pipeline di produzione tramite la [pagina di esecuzione della pipeline di produzione](/help/implementing/cloud-manager/deploy-code.md).

![Dashboard nella pipeline](assets/experience-audit-dashboard.png)

L&#39;audit dell&#39;esperienza fornisce i punteggi medi di Google Lighthouse per le [pagine configurate](#configuration) e la differenza di punteggio rispetto all&#39;analisi precedente.

Da questa visualizzazione di riepilogo nella fase **Test dello staging** della pipeline, sono disponibili due opzioni:

* **[Visualizza le pagine più lente](#view-slowest-pages)**
* **[Visualizza il report completo](#view-full-report)**

Puoi accedere ai risultati completi del controllo di audit facendo clic sulla scheda **Rapporti** nel dashboard di Cloud Manager. Oltre al riepilogo mostrato nei dettagli di esecuzione della pipeline, puoi visualizzare [direttamente il report completo](#view-full-report).

>[!TIP]
>
>Nelle sezioni seguenti viene descritto come visualizzare i risultati dell’audit dell’esperienza.
>
>* Per ulteriori dettagli sul funzionamento del controllo di audit, vedere [Dettagli valutazione controllo esperienza](#details).
>* Per informazioni su come eseguire un audit dell&#39;esperienza su richiesta, consulta [Rapporti di audit on demand](#on-demand).
>* Se si verificano problemi con il controllo di audit, vedere [Problemi rilevati durante il controllo di audit dell&#39;esperienza](#issues).
>* Per suggerimenti generali sulle prestazioni, vedere [Suggerimenti generali sulle prestazioni](#performance-tips).

### Visualizzare le pagine più lente {#view-slowest-pages}

Fai clic su **Visualizza pagine più lente** per aprire la finestra di dialogo **5 pagine più lente**. Vengono visualizzate le cinque pagine con le prestazioni più basse [configurate per l&#39;audit](#configuration).

![Cinque più lenti](assets/experience-audit-slowest-five.png)

Cloud Manager suddivide i punteggi per **Prestazioni**, **Accessibilità**, **Best practice** e **SEO**, mostrando la deviazione di ogni metrica dal controllo precedente.

Per impostazione predefinita, viene visualizzata la finestra di dialogo con i punteggi per i dispositivi mobili. Puoi visualizzare i punteggi del desktop utilizzando l&#39;interruttore **Dispositivi** nella parte superiore della finestra di dialogo.

La finestra di dialogo offre una rapida panoramica. Per informazioni dettagliate, fare clic su **Visualizza report completo**.

### Visualizza il rapporto completo {#view-full-report}

Per visualizzare il rapporto completo sull’audit dell’esperienza, effettua le seguenti operazioni:

* Fai clic su **`View full report`** nella finestra di dialogo **[5 pagine più lente](#view-slowest-pages)**.
* Fare clic su **`View full report`** quando si visualizza l&#39;[esecuzione di una pipeline](#results).
* Fai clic sulla scheda **Rapporti** in Cloud Manager.

È stata aperta la scheda **Rapporti** di Cloud Manager, che mostra **Audit dell&#39;esperienza**.

![Rapporti di audit dell&#39;esperienza](assets/experience-audit-reports.png)

La relazione si articola in due aree:

* **[Punteggi pagina — tendenza](#trend)**
* **[Risultati analisi controllo esperienza](#results)**

#### Punteggi di pagina — tendenza {#trend}

Per impostazione predefinita, la visualizzazione selezionata per **Punteggi pagina — tendenza** è **punteggi mediani** per **ultimo anno**.

È possibile scegliere di visualizzare le tendenze per specifiche categorie di Lighthouse facendo clic sul nome della categoria nella legenda.

![Tendenza selezionabile](assets/experience-audit-trend-selectable.png)

Utilizza il menu a discesa **Seleziona** nella parte superiore del grafico per selezionare dettagli specifici della pagina e i menu a discesa **Visualizza** e **Attiva** nella parte inferiore per scegliere rispettivamente diversi intervalli di tempo e il tipo di trigger.

Il menu a discesa **Visualizza** offre la possibilità di selezionare un intervallo di tempo predefinito o un intervallo personalizzato per una visualizzazione più specifica.

![Visualizzazione tendenze](assets/experience-audit-trend-view.png)

Quando si sposta il mouse sul grafico, una descrizione comando visualizza i valori per le categorie di Google Lighthouse in specifici momenti nel tempo.

![Dettagli tendenza](assets/experience-audit-trend-details.png)

Se fai clic sul grafico in un determinato momento, viene visualizzato un messaggio con i dettagli della scansione. Fai clic su **apri analisi audit esperienza** per caricare i risultati dell&#39;analisi nella sezione **[Risultati analisi audit esperienza](#scan-results)**.

![Seleziona un&#39;altra scansione](assets/experience-audit-open-scan.png)

#### Risultati scansione dell’audit dell’esperienza {#scan-results}

La sezione **Risultati analisi audit esperienza** fornisce consigli su come migliorare il punteggio e i dettagli di tutte le pagine digitalizzate. È diviso in due sezioni:

* **[Recommendations](#recommendations)**
* **[Pagine digitalizzate](#scanned-pages)**

##### Consigli {#recommendations}

La sezione **Recommendations** mostra un set aggregato di approfondimenti. Per impostazione predefinita, vengono visualizzati i consigli per **prestazioni**. Utilizza il menu a discesa accanto all&#39;intestazione **Recommendations** per passare a un&#39;altra categoria.

![Recommendations](assets/experience-audit-recommendations.png)

Fai clic su un consiglio per visualizzarne i dettagli.

![Dettagli consiglio](assets/experience-audit-recommendations-details.png)

Quando disponibili, i dettagli espansi dei consigli contengono anche la percentuale di impatto dei consigli, per concentrarti sui cambiamenti più incisivi. Inoltre, le raccomandazioni estese possono includere collegamenti alla documentazione AEM e suggerimenti utili per guidare l’utente nell’implementazione delle correzioni suggerite.

Fai clic sul collegamento **visualizza pagine** nella visualizzazione dei dettagli per visualizzare le pagine a cui si applica il consiglio.

![Pagine per i dettagli dei consigli](assets/experience-audit-details-pages.png)

##### Pagine scansionate {#scanned-pages}

La sezione **Pagine digitalizzate** fornisce dettagli sui punteggi di tutte le pagine digitalizzate. Utilizza i pulsanti **Precedente** e **Successivo** per scorrere i risultati e scegliere il numero di pagine da visualizzare.

![Pagine digitalizzate](assets/experience-audit-scanned-pages.png)

Fai clic sul collegamento di una pagina particolare per aggiornare il filtro **Seleziona** della sezione ](#trend) [**Punteggi pagina — tendenza** e visualizzare la scheda **Punteggi e consigli** per la pagina selezionata.

![Risultati pagina](assets/experience-audit-page-results.png)

La scheda **Rapporti non elaborati** fornisce punteggi per ogni controllo di audit della pagina. Fare clic sulla data del report nella colonna **Report di Lighthouse** per recuperare un file JSON dei dati non elaborati.

![Report non elaborato](assets/experience-audit-raw-reports.png)

Nel browser viene visualizzata una nuova scheda che ti indirizza a `https://googlechrome.github.io/lighthouse/viewer/`. Carica automaticamente un URL firmato contenente il rapporto JSON non elaborato di Lighthouse per la pagina selezionata, consentendo un’ispezione dettagliata.

![Visualizzazione del report non elaborato](assets/experience-audit-view-raw-report.png)

## Rapporti di controllo della scansione su richiesta {#on-demand}

Oltre a essere eseguiti durante l’esecuzione della pipeline, i rapporti di audit dell’esperienza possono essere generati on-demand. Questa opzione è una buona soluzione per scansionare le pagine rapidamente, senza dover eseguire una pipeline.

Per eseguire un&#39;analisi on-demand, passa alla scheda **Report** per visualizzare il report di audit completo, quindi fai clic sul pulsante **Esegui analisi**.

![Analisi su richiesta](assets/experience-audit-on-demand.png)

Il pulsante **Esegui scansione** non è più disponibile ed è contrassegnato con un&#39;icona dell&#39;orologio quando è già in esecuzione un&#39;analisi su richiesta.

![Analisi su richiesta in esecuzione](assets/experience-audit-on-demand-running.png)

Le scansioni on-demand attivano un controllo dell&#39;esperienza per le ultime 25 [pagine configurate](#configuration) e in genere terminano in pochi minuti.

Al termine, il grafico dei punteggi viene aggiornato automaticamente e puoi esaminare i risultati esattamente come per una scansione dell’esecuzione della pipeline.

Puoi filtrare il grafico dei punteggi in base al tipo di trigger utilizzando il selettore **Trigger**.

![Filtro trigger](assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>È possibile avviare una scansione on-demand solo se l’ambiente non viene eliminato e non sono presenti altre scansioni in sospeso nello stesso ambiente.

## Problemi rilevati da Audit dell’esperienza {#issues}

Se le [pagine configurate](#configuration) per l&#39;audit non erano disponibili o si sono verificati altri errori nel controllo di audit, l&#39;audit dell&#39;esperienza riflette questo fatto.

La pipeline mostra una sezione di errore espandibile per visualizzare i percorsi URL relativi a cui non poteva accedere.

![Problemi rilevati dall&#39;audit dell&#39;esperienza](assets/experience-audit-issues.png)

Se si visualizza il report completo, i dettagli sono visualizzati nella sezione **[Risultati analisi audit dell&#39;esperienza](#results)**, anch&#39;essa espandibile.

![Problemi relativi ai report completi](assets/experience-audit-issues-report.png)

Alcuni motivi per cui le pagine potrebbero non essere disponibili sono i seguenti:

* La configurazione blocca l’accesso.
* La pagina non esiste.
* La pagina viene reindirizzata richiedendo un’autenticazione diversa da quella di base.
* Si è verificato un problema interno.

>[!TIP]
>
>[L&#39;accesso ai report non elaborati](#scanned-pages) per una pagina può fornire dettagli sul motivo per cui non è stato possibile controllare la pagina.

## Suggerimenti generali sulle prestazioni {#performance-tips}

Due dei problemi di impatto più comuni e facili da risolvere riguardano Cumulative Layout Shifts (CLS) e Largest Contentful Paint (LCP).

Puoi migliorare queste aree eseguendo le seguenti operazioni:

* Caricamento non lento delle immagini al di sopra della piega: il contenuto visibile nel browser senza dover scorrere verso il basso.
* Assegnare la corretta priorità al caricamento delle risorse (ad esempio, caricando in modo asincrono le immagini sotto la piega dopo il caricamento del documento).
* Preacquisizione dei file JavaScript e CSS utilizzati per eseguire il rendering del contenuto sopra la piega (se necessario).
* Riservare lo spazio verticale assegnando proporzioni ai contenitori che vengono caricati lentamente o renderizzati in un secondo momento.
* Conversione di immagini in formato WebP per ridurne le dimensioni.
* Utilizzo di `<picture>` e dell&#39;immagine `srcset` con dimensioni dell&#39;immagine diverse per le diverse dimensioni del riquadro di visualizzazione (assicurandosi che il ridimensionamento funzioni).

## Dettagli della valutazione di Audit dell’esperienza {#details}

I dettagli seguenti forniscono informazioni aggiuntive su come l’audit dell’esperienza valuta il sito. Non sono necessarie per l’utilizzo generale della funzione e sono fornite qui per completezza.

* Il controllo di audit esegue la scansione del dominio di origine (`.com`) dai [percorsi di pagina del controllo dell&#39;esperienza configurati](#configuration) dell&#39;editore per simulare esperienze utente reali, consentendo di prendere decisioni migliori sulla gestione e l&#39;ottimizzazione dei siti Web.
* Nelle pipeline full stack di produzione, viene analizzato l’ambiente di staging. Per garantire che il controllo fornisca dettagli rilevanti durante il controllo, il contenuto dell’ambiente di staging deve essere il più simile possibile all’ambiente di produzione.
* Le pagine visualizzate nell&#39;elenco a discesa **Seleziona** nella sezione [**Punteggi pagina — tendenza**](#trend) sono tutte pagine note analizzate in passato dall&#39;audit dell&#39;esperienza.
* [Un consiglio](#recommendations) può avere un guadagno potenziale e una differenza rispetto all&#39;analisi precedente.
* L’audit dell’esperienza stima i potenziali miglioramenti elaborando il rapporto non elaborato per ogni pagina. Mette in correlazione i byte sprecati o i millisecondi con le informazioni, assegnando un impatto ponderato sul punteggio delle prestazioni. L’audit fornisce queste informazioni, insieme alle pagine interessate, per aiutarti a decidere quale consiglio seguire.
Per ulteriori dettagli, consulta la [sezione Suggerimenti generali sulle prestazioni](#performance-tips).
* Una pipeline front-end può essere implementata in un ambiente esistente e più pipeline front-end possono essere indirizzate allo stesso ambiente. Poiché i risultati della scansione sono aggregati a livello di ambiente, i punteggi, le tendenze e i consigli sono coerenti. Questi risultati vengono visualizzati nell’ambiente selezionato, indipendentemente dalla pipeline che ha attivato l’analisi.
