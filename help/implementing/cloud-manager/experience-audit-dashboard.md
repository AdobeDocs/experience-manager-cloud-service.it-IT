---
title: Dashboard di Experience Audit
description: Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO tramite un’interfaccia dashboard chiara e informativa.
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 7%

---


# Dashboard di Experience Audit {#experience-audit-dashboard}

Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche implementate soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO tramite un’interfaccia dashboard chiara e informativa.

>[!NOTE]
>
>Questa funzione è disponibile solo per [il programma per i primi utilizzatori.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)
>
>Per informazioni dettagliate sulla funzione di audit dell&#39;esperienza esistente per AEM as a Cloud Service, consulta il documento [Test di audit dell&#39;esperienza](/help/implementing/cloud-manager/experience-audit-testing.md)

## Panoramica {#overview}

L’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche implementate:

1. soddisfino gli standard di base per prestazioni, accessibilità, best practice, SEO (Search Engine Optimization) e PWA (app web progressiva);

1. non introducano regressioni.

La funzione Audit dell’esperienza in Cloud Manager garantisce che l’esperienza dell’utente sul sito sia conforme agli standard più elevati.

I risultati dell’audit sono informativi e consentono agli utenti con ruolo Responsabile dell’implementazione di visualizzare i punteggi e cosa è cambiato tra i punteggi correnti e precedenti. Questa informazione è utile per determinare l’eventuale introduzione di una regressione con la distribuzione corrente.

L&#39;audit dell&#39;esperienza è basato su [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/), uno strumento open source di Google, ed è abilitato in tutte le pipeline di produzione di Cloud Manager.

## Disponibilità {#availability}

L’audit dell’esperienza è disponibile per Cloud Manager:

* Pipeline di produzione dei siti, per impostazione predefinita
* Sviluppo di pipeline full stack, facoltativamente
* Sviluppo di pipeline front-end, facoltativamente

Per ulteriori informazioni su come configurare il controllo di audit per gli ambienti facoltativi, vedere la [sezione Configurazione](#configuration).

I controlli di audit vengono eseguiti come parte della pipeline. I controlli di audit possono anche essere [eseguiti su richiesta](#on-demand) al di fuori delle pipeline.

## Configurazione {#configuration}

L’audit dell’esperienza è disponibile per impostazione predefinita per le pipeline di produzione. Facoltativamente, può essere abilitato per lo sviluppo di pipeline full stack e front-end. In tutti i casi, è necessario definire quali percorsi di contenuto vengono valutati durante l’esecuzione della pipeline.

1. A seconda del tipo di pipeline che desideri configurare, segui le istruzioni riportate di seguito:

   * Aggiungi una nuova [pipeline di produzione,](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) se desideri definire i percorsi da valutare dal controllo di audit.
   * Aggiungi una nuova [pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) se desideri abilitare il controllo di audit su una pipeline front-end o di sviluppo full-stack.
   * Oppure puoi [modificare una pipeline esistente,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) e aggiornare le opzioni esistenti.

1. Se stai aggiungendo o modificando una pipeline non di produzione per la quale desideri utilizzare l&#39;audit dell&#39;esperienza, devi selezionare la casella di controllo **Audit dell&#39;esperienza** nella scheda **Codice Source**.

   ![Abilitazione dell&#39;audit dell&#39;esperienza](assets/experience-audit-enable.jpg)

   * Questo è necessario solo per le pipeline non di produzione.
   * La scheda **Audit dell&#39;esperienza** viene visualizzata quando la casella di controllo è selezionata.

1. Sia per le pipeline di produzione che per quelle non di produzione, puoi definire i percorsi da includere nell’audit dell’esperienza nella scheda **Audit dell’esperienza**.

   * I percorsi delle pagine devono iniziare con `/` e sono relativi al sito.
   * Ad esempio, se il sito è `wknd.site` e si desidera includere `https://wknd.site/us/en/about-us.html` nell&#39;audit dell&#39;esperienza, immettere il percorso `/us/en/about-us.html`.

   ![Definizione di un percorso per l’audit dell’esperienza](assets/experience-audit-add-page.png)

1. Tocca o fai clic su **Aggiungi pagina** e il percorso viene completato automaticamente con l&#39;indirizzo dell&#39;ambiente e aggiunto alla tabella dei percorsi.

   ![Salvataggio del percorso nella tabella](assets/experience-audit-page-added.png)

1. Continua ad aggiungere i percorsi che desideri ripetendo i due passaggi precedenti.

   * Puoi aggiungere fino a un massimo di 25 percorsi.
   * Se non definisci alcun percorso, per impostazione predefinita la pagina Home del sito viene inclusa nell’audit dell’esperienza.

1. Per salvare la pipeline, fai clic su **Salva**.

## Risultati dell’audit dell’esperienza {#results}

I risultati dell&#39;audit dell&#39;esperienza sono presentati nella fase **Test dello staging** della pipeline di produzione tramite la [pagina di esecuzione della pipeline di produzione.](/help/implementing/cloud-manager/deploy-code.md)

![Dashboard nella pipeline](assets/experience-audit-dashboard.jpg)

L&#39;audit dell&#39;esperienza fornisce i punteggi medi di Google Lighthouse per le [pagine configurate](#configuration) e la differenza di punteggio rispetto all&#39;analisi precedente.

Da questa visualizzazione di riepilogo nella fase **Test dello staging** della pipeline, sono disponibili due opzioni:

* **[Visualizza pagine più lente](#view-slowest-pages)**
* **[Visualizza report completo](#view-full-report)**

Oltre al riepilogo presentato nei dettagli di un&#39;esecuzione della pipeline, puoi anche accedere direttamente ai risultati completi del controllo di audit utilizzando la scheda **Rapporti** del dashboard di Cloud Manager per accedere direttamente a [il rapporto completo](#view-full-report).

>[!TIP]
>
>Nelle sezioni seguenti viene descritto come visualizzare i risultati dell’audit dell’esperienza.
>
>* Per informazioni dettagliate sul funzionamento del controllo di audit, vedere la sezione [Dettagli sulla valutazione del controllo di audit dell&#39;esperienza.](#details)
>* Se desideri sapere come eseguire un audit dell&#39;esperienza su richiesta, consulta la sezione [Rapporti di audit on demand.](#on-demand)
>* In caso di problemi con il controllo di audit, consulta la sezione [Problemi rilevati dal controllo di audit dell&#39;esperienza.](#issues)
>* Per suggerimenti generali sulle prestazioni, vedere la sezione [Suggerimenti generali sulle prestazioni.](#performance-tips)

### Visualizza pagine più lente {#view-slowest-pages}

Toccando o facendo clic su **Visualizza pagine più lente** si apre la finestra di dialogo **5 pagine più lente**, in cui sono visualizzate le cinque pagine con le prestazioni più basse [configurate per il controllo.](#configuration)

![Cinque più lenti](assets/experience-audit-slowest-five.jpg)

I punteggi sono suddivisi per **Prestazioni**, **Accessibilità**, **Best practice** e **SEO** insieme alla deviazione di ogni metrica dall&#39;ultimo controllo di audit.

Per impostazione predefinita, la finestra di dialogo si apre con i punteggi per i dispositivi mobili. Puoi modificare i punteggi del desktop con l&#39;interruttore **Dispositivi** nella parte superiore della finestra di dialogo.

La finestra di dialogo offre una panoramica rapida. Per informazioni dettagliate, tocca o fai clic su **Visualizza report completo**.

### Visualizza report completo {#view-full-report}

Per visualizzare il rapporto completo sull’audit dell’esperienza:

* Tocca o fai clic su **Visualizza report completo** nella finestra di dialogo **[5 pagine più lente](#view-slowest-pages)**.
* Tocca o fai clic su **Visualizza report completo** durante la visualizzazione della [esecuzione di una pipeline.](#results)
* Tocca o fai clic sulla scheda **Rapporti** in Cloud Manager.

È stata aperta la scheda **Rapporti** di Cloud Manager, che mostra **Audit dell&#39;esperienza**.

![Rapporti di audit dell&#39;esperienza](assets/experience-audit-reports.png)

La relazione si articola in due aree:

* **[Punteggi pagina - tendenza](#trend)**
* **[Risultati analisi audit esperienza](#results)**

#### Punteggi pagina - tendenza {#trend}

Per impostazione predefinita, la visualizzazione selezionata per **Punteggi pagina - tendenza** è **Punteggi mediani** per **Ultimi 6 mesi**.

Utilizza i menu a discesa **Seleziona** e **Visualizza** nella parte superiore e inferiore del pulsante del grafico per selezionare rispettivamente i dettagli specifici della pagina e i diversi intervalli di tempo. Tocca o fai clic sul pulsante e sul pulsante **aggiorna tendenza** nella parte superiore del grafico per applicare le selezioni e aggiornare il grafico.

Quando si sposta il mouse sul grafico, una descrizione comando visualizza i valori per le categorie di Google Lighthouse in specifici momenti nel tempo.

![Dettagli tendenza](assets/experience-audit-trend-details.png)

Se tocchi o fai clic sul grafico in un determinato momento, viene visualizzato un messaggio con i dettagli della scansione. Tocca o fai clic su **apri analisi audit esperienza** per caricare i risultati dell&#39;analisi nella sezione **[Risultati analisi audit esperienza](#scan-results)**.

![Seleziona un&#39;altra scansione](assets/experience-audit-open-scan.png)

#### Risultati analisi audit esperienza {#scan-results}

La sezione **Risultati dell&#39;analisi dell&#39;audit dell&#39;esperienza** fornisce consigli su come migliorare il punteggio e i dettagli di tutte le pagine digitalizzate. È diviso in due sezioni:

* **[Recommendations](#recommendations)**
* **[Pagine digitalizzate](#scanned-pages)**

##### Consigli {#recommendations}

La sezione **Recommendations** mostra un set aggregato di approfondimenti. Per impostazione predefinita, vengono visualizzati i consigli per **prestazioni**. Utilizza il menu a discesa accanto all&#39;intestazione **Recommendations** per passare a un&#39;altra categoria.

![Recommendations](assets/experience-audit-recommendations.png)

Tocca o fai clic sulla freccia per visualizzare i dettagli di qualsiasi consiglio.

![Dettagli consiglio](assets/experience-audit-recommendation-details.png)

Quando disponibili, i dettagli espansi dei consigli contengono anche la percentuale di impatto dei consigli, per concentrarti sui cambiamenti più incisivi.

Tocca o fai clic sul collegamento **visualizza pagine** nella visualizzazione dei dettagli per visualizzare le pagine a cui si applica il consiglio.

![Pagine per i dettagli dei consigli](assets/experience-audit-details-pages.png)

##### Pagine digitalizzate {#scanned-pages}

La sezione **Pagine digitalizzate** fornisce punteggi dettagliati su tutte le pagine digitalizzate. È possibile utilizzare i pulsanti **Precedente** e **Successivo** per scorrere i risultati e scegliere il numero di pagine da visualizzare.

![Pagine digitalizzate](assets/experience-audit-scanned-pages.png)

Toccando o facendo clic sul collegamento di una pagina particolare si aggiorna il filtro **Seleziona** della [**sezione Punteggi pagina - tendenza**](#trend) e viene visualizzata la scheda **Punteggi e consigli** per la pagina selezionata.

![Risultati pagina](assets/experience-audit-page-results.png)

La scheda **Rapporti non elaborati** fornisce punteggi per ogni controllo di audit della pagina. Tocca o fai clic sull&#39;icona **Scarica** per recuperare un file JSON dei dati non elaborati.

![Report non elaborato](assets/experience-audit-raw-reports.png)

Verrà aperta una nuova scheda nel browser che punta a `https://googlechrome.github.io/lighthouse/viewer/` con un URL firmato del report JSON (JavaScript Object Notation) non elaborato di Lighthouse per la pagina selezionata, che verrà aperto automaticamente per l&#39;ispezione dettagliata

![Visualizzazione del report non elaborato](assets/experience-audit-view-raw-report.png)

## Rapporti di audit on-demand {#on-demand}

Oltre a essere eseguiti durante l’esecuzione della pipeline, i rapporti di audit dell’esperienza possono essere generati on-demand. Questa è una buona soluzione per eseguire rapidamente la scansione delle pagine, senza dover eseguire una pipeline.

Per eseguire un&#39;analisi on-demand, passa alla scheda **Report** per visualizzare il report di audit completo, quindi tocca o fai clic sul pulsante **Esegui analisi**.

![Analisi su richiesta](assets/experience-audit-on-demand.png)

Le scansioni on-demand attivano un controllo dell&#39;esperienza per le ultime 25 [pagine configurate](#configuration) e in genere terminano in pochi minuti.

Al termine, il grafico dei punteggi verrà aggiornato automaticamente e potrai esaminare i risultati esattamente come per una scansione dell’esecuzione della pipeline.

Puoi filtrare il grafico dei punteggi in base al tipo di trigger utilizzando il selettore **Trigger**.

![Filtro trigger](assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>È possibile avviare una scansione on-demand solo se l’ambiente non viene eliminato e non sono presenti altre scansioni in sospeso nello stesso ambiente.

## L’audit dell’esperienza riscontra problemi {#issues}

Se le [pagine configurate](#configuration) per il controllo non erano disponibili, il controllo dell&#39;esperienza ne riflette la disponibilità.

La pipeline mostra una sezione di errore espandibile per visualizzare i percorsi URL relativi a cui non poteva accedere.

![Problemi rilevati dall&#39;audit dell&#39;esperienza](assets/experience-audit-issues.jpg)

Se visualizzi il report completo, i dettagli sono visualizzati nella sezione **[Risultati analisi controllo esperienza](#results)**.

![Problemi relativi ai report completi](assets/experience-audit-issues-reports.jpeg)

Alcuni motivi per cui le pagine potrebbero non essere disponibili sono i seguenti:

* La configurazione blocca l’accesso.
* La pagina non esiste.
* La pagina viene reindirizzata richiedendo un’autenticazione diversa da quella di base.
* Si è verificato un problema interno.
* Ecc.

>[!TIP]
>
>[L&#39;accesso ai report non elaborati](#scanned-pages) per una pagina può fornire dettagli sul motivo per cui non è stato possibile controllare la pagina.

## Suggerimenti generali sulle prestazioni {#performance-tips}

Due dei problemi di impatto più comuni e facili da risolvere riguardano Cumulative Layout Shifts (CLS) e Largest Contentful Paint (LCP).

Questi possono essere migliorati:

* Caricamento non lento delle immagini sopra la piega (il contenuto visibile nel browser senza dover scorrere verso il basso).
* Assegnare la corretta priorità al modo in cui le risorse vengono caricate (ad esempio, caricando in modo asincrono le immagini sotto la piega dopo il caricamento del documento).
* Preacquisizione dei file JavaScript e CSS utilizzati per eseguire il rendering del contenuto sopra la piega (se necessario).
* Riservare lo spazio verticale assegnando proporzioni ai contenitori che vengono caricati lentamente o renderizzati in un secondo momento.
* Conversione di immagini in formato WebP per ridurne le dimensioni.
* Utilizzo di `<picture>` e dell&#39;immagine `srcset` con dimensioni dell&#39;immagine diverse per le diverse dimensioni del riquadro di visualizzazione (assicurandosi che il ridimensionamento funzioni).

## Dettagli della valutazione di Experience Audit {#details}

I dettagli seguenti forniscono informazioni aggiuntive su come l’audit dell’esperienza valuta il sito. Non sono necessarie per l’utilizzo generale della funzione e sono fornite qui per completezza.

* Anche se i [percorsi di pagina di audit dell&#39;esperienza configurati](#configuration) mostrano il dominio `.com` dell&#39;editore, l&#39;audit analizza il dominio di origine (`.net`) per garantire che vengano rilevati i problemi introdotti durante lo sviluppo.
   * Il dominio `.com` utilizza una rete CDN e potrebbe fornire punteggi migliori o contenere risultati memorizzati nella cache.
* Nelle pipeline full stack di produzione, viene analizzato l’ambiente di staging.
   * Per garantire che il controllo fornisca dettagli rilevanti durante il controllo, il contenuto dell’ambiente di staging deve essere il più simile possibile all’ambiente di produzione.
* Le pagine visualizzate nel menu a discesa **Seleziona** nella sezione [**Punteggi pagina - tendenza**](#trend) sono tutte pagine note analizzate in passato dall&#39;audit dell&#39;esperienza.
* [Un consiglio](#recommendations) può avere un guadagno potenziale e una differenza rispetto all&#39;analisi precedente.
   * L’audit dell’esperienza stima il guadagno potenziale elaborando il rapporto non elaborato per ogni pagina e correlando i byte sprecati o i millisecondi con un’informazione approfondita che ha un impatto ponderato sul punteggio delle prestazioni.
   * L’audit fornisce queste informazioni (nonché le pagine interessate) per aiutare a decidere quale raccomandazione perseguire.
   * Per ulteriori dettagli, vedere la [sezione Suggerimenti generali sulle prestazioni](#performance-tips)
* Dato che una pipeline front-end può essere distribuita in un ambiente esistente (oppure che più pipeline front-end hanno come destinazione lo stesso ambiente) e i risultati della scansione sono aggregati a livello di ambiente, i punteggi, le tendenze e i consigli vengono visualizzati nello stesso ambiente selezionato, indipendentemente dall’esecuzione della pipeline che ha attivato la scansione.
