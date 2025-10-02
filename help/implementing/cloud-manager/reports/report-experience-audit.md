---
title: Dashboard di audit dell’esperienza
description: Scopri in che modo l’audit dell’esperienza convalida il processo di distribuzione, garantendo che le modifiche soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO. Fornisce un’interfaccia dashboard chiara e informativa per monitorare queste metriche.
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5f9d53958076b77cd333a042003c83853594db87
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 8%

---


# Dashboard di Experience Audit {#experience-audit-dashboard}

<!-- Engineer architect over this feature was Bogdan Anton; scrum master Alexandru Nica -->

Scopri come l’audit dell’esperienza convalida il processo di distribuzione, garantendo che le modifiche soddisfino gli standard di base in termini di prestazioni, accessibilità, best practice e SEO (Search Engine Optimization). Fornisce un’interfaccia dashboard chiara e informativa per monitorare queste metriche.

## Panoramica {#overview}

L’audit dell’esperienza convalida il processo di distribuzione e garantisce che le modifiche vengano implementate:

1. Soddisfa gli standard di base in termini di prestazioni, accessibilità, best practice e SEO.
1. non introducano regressioni.

La funzione Audit dell’esperienza in Cloud Manager garantisce che l’esperienza dell’utente sul sito sia conforme agli standard più elevati.

I risultati dell’audit sono informativi e consentono agli utenti con ruolo Responsabile dell’implementazione di visualizzare i punteggi e cosa è cambiato tra i punteggi correnti e precedenti. Questa informazione è utile per determinare l’eventuale introduzione di una regressione con la distribuzione corrente.

L&#39;audit dell&#39;esperienza è basato su [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/), uno strumento open source di Google, ed è abilitato in tutte le pipeline di produzione di Cloud Manager.

## Disponibilità {#availability}

L’audit dell’esperienza è disponibile per Cloud Manager:

* Impostazione predefinita. Pipeline di produzione di Sites.
* (Facoltativo) Sviluppo di pipeline full stack.
* Sviluppo di pipeline front-end (facoltativo).

Per ulteriori informazioni su come configurare il controllo di audit per gli ambienti facoltativi, vedere la [sezione Configurazione](#configuration).

I controlli di audit vengono eseguiti come parte della pipeline. I controlli di audit possono anche essere [eseguiti su richiesta](#on-demand) al di fuori delle pipeline.

## Configurazione {#configuration}

L’audit dell’esperienza è disponibile per impostazione predefinita per le pipeline di produzione. Facoltativamente, può essere abilitato per lo sviluppo di pipeline full stack e front-end. In tutti i casi, è necessario definire quali percorsi di contenuto vengono valutati durante l’esecuzione della pipeline.

1. A seconda del tipo di pipeline che desideri configurare, effettua una delle seguenti operazioni:

   * [Aggiungi una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) per definire i percorsi che dovranno essere valutati dal controllo di audit.
   * [Aggiungi una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) se desideri abilitare il controllo di audit su una pipeline front-end o di sviluppo full-stack.
   * [Modifica una pipeline esistente](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) e aggiorna le opzioni esistenti.

1. Per utilizzare Audit dell&#39;esperienza quando si aggiunge o si modifica una pipeline non di produzione, selezionare la casella di controllo **Audit dell&#39;esperienza**. È possibile trovare questa opzione nella scheda **Codice Source**.

   ![Abilitazione dell&#39;audit dell&#39;esperienza](/help/implementing/cloud-manager/reports/assets/experience-audit-enable.jpg)

   * Necessario solo per pipeline non di produzione.
   * La scheda **Audit dell&#39;esperienza** viene visualizzata quando la casella di controllo è selezionata.

1. Sia per le pipeline di produzione che per quelle non di produzione, puoi definire i percorsi da includere nell’audit dell’esperienza nella scheda **Audit dell’esperienza**.

   * I percorsi delle pagine devono iniziare con `/` e sono relativi al sito.
   * Ad esempio, se il sito è `wknd.site` e si desidera includere `https://wknd.site/us/en/about-us.html` nell&#39;audit dell&#39;esperienza, immettere il percorso `/us/en/about-us.html`.

   ![Definizione di un percorso per l’audit dell’esperienza](/help/implementing/cloud-manager/reports/assets/experience-audit-add-page.png)

1. Facendo clic su **Aggiungi pagina**, il percorso viene completato automaticamente con l’indirizzo dell’ambiente e aggiunto alla tabella dei percorsi.

   ![Salvataggio del percorso nella tabella](/help/implementing/cloud-manager/reports/assets/experience-audit-page-added.png)

1. Continua ad aggiungere i percorsi che desideri ripetendo i due passaggi precedenti.

   * Puoi aggiungere fino a un massimo di 25 percorsi.
   * Se non definisci alcun percorso, per impostazione predefinita la pagina Home del sito viene inclusa nell’audit dell’esperienza.

1. Fai clic su **Salva**.

## Risultati dell’audit dell’esperienza {#results}

I risultati dell&#39;audit dell&#39;esperienza sono presentati nella fase **Test dello staging** della pipeline di produzione tramite la [pagina di esecuzione della pipeline di produzione](/help/implementing/cloud-manager/deploy-code.md).

![Dashboard nella pipeline](/help/implementing/cloud-manager/reports/assets/experience-audit-dashboard.png)

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

### Visualizzare le pagine più lente {#view-slowest-pages}

Fai clic su **Visualizza pagine più lente** per aprire la finestra di dialogo **5 pagine più lente**. Vengono visualizzate le cinque pagine con le prestazioni più basse [configurate per l&#39;audit](#configuration).

![Cinque più lenti](/help/implementing/cloud-manager/reports/assets/experience-audit-slowest-five.png)

Cloud Manager suddivide i punteggi per **Prestazioni**, **Accessibilità**, **Best practice** e **SEO**, mostrando la deviazione di ogni metrica dal controllo precedente.

Per impostazione predefinita, viene visualizzata la finestra di dialogo con i punteggi per i dispositivi mobili. Puoi visualizzare i punteggi del desktop utilizzando l&#39;interruttore **Dispositivi** nella parte superiore della finestra di dialogo.

La finestra di dialogo offre una rapida panoramica. Per informazioni dettagliate, fare clic su **Visualizza report completo**.

### Visualizza il rapporto completo {#view-full-report}

Per visualizzare il rapporto completo sull’audit dell’esperienza, effettua le seguenti operazioni:

* Fai clic su **`View full report`** nella finestra di dialogo **[5 pagine più lente](#view-slowest-pages)**.
* Fare clic su **`View full report`** quando si visualizza l&#39;[esecuzione di una pipeline](#results).
* Fai clic sulla scheda **Rapporti** in Cloud Manager.

È stata aperta la scheda **Rapporti** di Cloud Manager, che mostra **Audit dell&#39;esperienza**.

![Rapporti di audit dell&#39;esperienza](/help/implementing/cloud-manager/reports/assets/experience-audit-reports.png)

La relazione si articola in due aree:

* **[Punteggi pagina — tendenza](#trend)**
* **[Risultati analisi controllo esperienza](#results)**

#### Punteggi di pagina — tendenza {#trend}

Per impostazione predefinita, la visualizzazione selezionata per **Punteggi pagina — tendenza** è **punteggi mediani** per **ultimo anno**.

È possibile scegliere di visualizzare le tendenze per specifiche categorie di Lighthouse facendo clic sul nome della categoria nella legenda.

![Tendenza selezionabile](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-selectable.png)

Utilizza il menu a discesa **Seleziona** nella parte superiore del grafico per selezionare dettagli specifici della pagina e i menu a discesa **Visualizza** e **Attiva** nella parte inferiore per scegliere rispettivamente diversi intervalli di tempo e il tipo di trigger.

Il menu a discesa **Visualizza** offre la possibilità di selezionare un intervallo di tempo predefinito o un intervallo personalizzato per una visualizzazione più specifica.

![Visualizzazione tendenze](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-view.png)

Quando si sposta il mouse sul grafico, una descrizione comando visualizza i valori per le categorie di Google Lighthouse in specifici momenti nel tempo.

![Dettagli tendenza](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-details.png)

Se fai clic sul grafico in un determinato momento, viene visualizzato un pop-up con i dettagli della scansione. Fai clic su **apri analisi audit esperienza** per caricare i risultati dell&#39;analisi nella sezione **[Risultati analisi audit esperienza](#scan-results)**.

![Seleziona un&#39;altra scansione](/help/implementing/cloud-manager/reports/assets/experience-audit-open-scan.png)

#### Risultati scansione dell’audit dell’esperienza {#scan-results}

La sezione **Risultati analisi audit esperienza** fornisce dettagli sui punteggi di tutte le pagine digitalizzate. Utilizza i pulsanti **Precedente** e **Successivo** per scorrere i risultati e scegliere il numero di pagine da visualizzare.

![Pagine digitalizzate](/help/implementing/cloud-manager/reports/assets/experience-audit-scanned-pages.png)

Fai clic sul collegamento di una pagina particolare per aggiornare il filtro **Select** dei [**punteggi di pagina — trend** section](#trend) e visualizzare la scheda **Report non elaborati** che fornisce i punteggi per ogni controllo di audit della pagina. Fare clic sulla data del report nella colonna **Report di Lighthouse** per recuperare un file JSON dei dati non elaborati.

![Report non elaborato](/help/implementing/cloud-manager/reports/assets/experience-audit-raw-reports.png)

Una nuova scheda che si apre nel browser, ti indirizza a `https://googlechrome.github.io/lighthouse/viewer/`. Carica automaticamente un URL firmato contenente il rapporto JSON non elaborato di Lighthouse per la pagina selezionata, consentendo un’ispezione dettagliata.

![Visualizzazione del report non elaborato](/help/implementing/cloud-manager/reports/assets/experience-audit-view-raw-report.png)

## Rapporti di controllo della scansione su richiesta {#on-demand}

Oltre a essere eseguiti durante l’esecuzione della pipeline, i rapporti di audit dell’esperienza possono essere generati on-demand. Questa opzione è una buona soluzione per scansionare le pagine rapidamente, senza dover eseguire una pipeline.

Per eseguire un&#39;analisi su richiesta, passare alla scheda **Report** in modo da visualizzare il report di controllo completo e quindi fare clic sul pulsante **Esegui analisi**.

![Analisi su richiesta](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand.png)

Il pulsante **Esegui analisi** non è più disponibile ed è contrassegnato con un&#39;icona di orologio quando è già in esecuzione un&#39;analisi su richiesta.

![Analisi su richiesta in esecuzione](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand-running.png)

Le scansioni on-demand attivano un controllo dell&#39;esperienza per le ultime 25 [pagine configurate](#configuration) e in genere terminano in pochi minuti.

Al termine, il grafico dei punteggi viene aggiornato automaticamente e puoi esaminare i risultati esattamente come per una scansione dell’esecuzione della pipeline.

Puoi filtrare il grafico dei punteggi in base al tipo di trigger utilizzando il selettore **Trigger**.

![Filtro trigger](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>È possibile avviare un’analisi on-demand solo se l’ambiente non viene eliminato e non sono presenti altre analisi in sospeso nello stesso ambiente.

## Problemi rilevati da Audit dell’esperienza {#issues}

Se le [pagine configurate](#configuration) per l&#39;audit non erano disponibili o si sono verificati altri errori nel controllo di audit, l&#39;audit dell&#39;esperienza riflette questo fatto.

La pipeline mostra una sezione di errore espandibile per visualizzare i percorsi URL relativi a cui non poteva accedere.

![Problemi rilevati dall&#39;audit dell&#39;esperienza](/help/implementing/cloud-manager/reports/assets/experience-audit-issues.png)

Se si visualizza il report completo, i dettagli sono visualizzati nella sezione **[Risultati analisi audit dell&#39;esperienza](#results)**, anch&#39;essa espandibile.

![Problemi relativi ai report completi](/help/implementing/cloud-manager/reports/assets/experience-audit-issues-report.png)

Alcuni motivi per cui le pagine potrebbero non essere disponibili sono i seguenti:

* La configurazione blocca l’accesso.
* La pagina non esiste.
* La pagina viene reindirizzata richiedendo un’autenticazione diversa da quella di base.
* Si è verificato un problema interno.

>[!TIP]
>
>[L&#39;accesso ai report non elaborati](#scan-results) per una pagina può fornire dettagli sul motivo per cui non è stato possibile controllare la pagina.

## Dettagli della valutazione di Audit dell’esperienza {#details}

I dettagli seguenti forniscono informazioni aggiuntive su come l’audit dell’esperienza valuta il sito. Non sono necessarie per l’utilizzo generale della funzione e sono fornite qui per completezza.

* Il controllo di audit esegue la scansione del dominio di origine (`.com`) dai [percorsi di pagina del controllo dell&#39;esperienza configurati](#configuration) dell&#39;editore per simulare esperienze utente reali, consentendo di prendere decisioni migliori sulla gestione e l&#39;ottimizzazione dei siti Web.
* Nelle pipeline full stack di produzione, viene analizzato l’ambiente di staging. Per garantire che il controllo fornisca dettagli rilevanti durante il controllo, il contenuto dell’ambiente di staging deve essere il più simile possibile all’ambiente di produzione.
* Le pagine visualizzate nell&#39;elenco a discesa **Seleziona** nella sezione [**Punteggi pagina — tendenza**](#trend) sono tutte pagine note analizzate in passato dall&#39;audit dell&#39;esperienza.
