---
title: Utilizzo della dashboard di realizzazione del valore per analizzare le tendenze di utilizzo di moduli e documenti
description: Scopri come utilizzare la dashboard Informazioni sull’utilizzo di Forms per monitorare e comprendere le prestazioni dei moduli e dei frammenti di modulo.
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components, Core Components
hide: true
hidefromtoc: true
source-git-commit: 09d383638d6caba596d22a7c6b544768de5245a0
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 1%

---

# Utilizzo della dashboard di realizzazione del valore per analizzare le tendenze di utilizzo di moduli e documenti

<span class="preview"> Questa funzionalità è disponibile tramite il programma di accesso anticipato. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo ufficiale a aem-forms-ea@adobe.com. <span>

![Dashboard per la realizzazione del valore](/help/edge/docs/forms/universal-editor/assets/forms-insights-banner.svg)

Monitorando regolarmente le metriche presentate nella dashboard &quot;Informazioni sull’utilizzo di Forms&quot;, puoi ottenere informazioni utili sulle prestazioni di moduli, documenti e frammenti di modulo. Utilizza questi dati per prendere decisioni informate sulla progettazione dei moduli, sulla gestione dei frammenti e sulla strategia complessiva dei moduli.

Questo articolo fornisce istruzioni d’uso dettagliate e l’interpretazione delle metriche per il dashboard di realizzazione del valore. Per una panoramica concettuale e i vantaggi del dashboard, vedere [informazioni sul dashboard di realizzazione del valore](/help/forms/aem-forms-value-realization-dashboard.md).


## Accesso al dashboard di informazioni sull’utilizzo

Per accedere alla dashboard di Informazioni sull’utilizzo di Forms:

1. Passa a **Forms** > **Forms e documenti**
1. Fare clic su **Dashboard InProduct**. Il dashboard viene aperto in una nuova finestra.

   ![Dashboard per la realizzazione del valore](/help/forms/assets/forms-usage-insights.png)

## Panoramica

Il quadro comandi è costituito da due sezioni principali:

- **Attività moduli e documenti nel tempo:** Questa sezione fornisce informazioni sull&#39;utilizzo e l&#39;evoluzione dei moduli in un periodo selezionato.
- **Utilizzo frammento:** Questa sezione consente di monitorare l&#39;adozione e il riutilizzo dei frammenti di modulo.

## Attività moduli e documenti nel tempo

Questa sezione contiene quattro grafici, ciascuno dei quali tiene traccia di un aspetto diverso dell’attività del modulo. Tutti i grafici condividono la stessa struttura:

- **Tipo di grafico:** grafico a linee e grafico a barre
- **Asse X:** Data (visualizzazione attività giornaliera)
- **Asse Y:** Conteggio (che rappresenta il numero di occorrenze dell&#39;attività tracciata)
- **Periodo di tempo:** regolabile tramite un menu a discesa (opzioni: &quot;Ultimi 30 giorni&quot;, &quot;Ultimi 12 mesi&quot;)




### Invii modulo

- **Scopo:** In questo grafico viene visualizzato il numero di volte in cui i moduli sono stati inviati correttamente nel periodo di tempo selezionato.

  ![Grafico invii Forms](/help/forms/assets/forms-submissions-vr-dashboard-form-insights.png)
- **Informazioni da estrarre:**
   - **Analisi delle tendenze:** Osservare la tendenza generale degli invii di moduli. Il numero aumenta, diminuisce o rimane relativamente costante?
   - **Periodi di picco:** identifica giorni o periodi con tassi di invio insolitamente elevati. Esamina le possibili cause di questi picchi (ad esempio campagne di marketing, eventi specifici).
   - **Periodi di bassa attività:** Identifica i periodi con tassi di invio bassi ed esamina le possibili cause (ad esempio tempi di inattività dei moduli, problemi di usabilità).
   - **Analisi comparativa:** confrontare le percentuali di invio in diversi periodi di tempo (ad esempio, gli ultimi 30 giorni rispetto ai 30 giorni precedenti) per valutare le modifiche delle prestazioni.

### Rappresentazioni documenti

- **Scopo:** Questo grafico tiene traccia del numero di documenti generati in seguito all&#39;invio di moduli. Ciò è importante se i moduli attivano la creazione di documenti (ad esempio, contratti, report).

  ![Grafico Rappresentazioni Documenti](/help/forms/assets/document-rendetions-vr-dashboard-form-insights.png)


- **Informazioni da estrarre:**
   - **Correlazione con l&#39;invio di moduli:** Confrontare la tendenza delle rappresentazioni di documenti con la tendenza dell&#39;invio di moduli. Idealmente, dovrebbero essere strettamente correlate. Le discrepanze possono indicare problemi nel processo di generazione dei documenti.
   - **Volume di generazione del documento:** Valuta il volume complessivo dei documenti generati per comprendere il carico di lavoro sul sistema di generazione dei documenti.

### Moduli creati


- **Scopo:** In questo grafico viene visualizzato il numero di nuovi moduli creati nel periodo di tempo selezionato.

  ![Grafico creato da Forms](/help/forms/assets/forms-created-vr-dashboard-form-insights.png)

- **Informazioni da estrarre:**
   - **Velocità di creazione moduli:** tieni traccia della velocità di creazione dei nuovi moduli. Questo fornisce informazioni sulla domanda di nuovi moduli all’interno dell’organizzazione.
   - **Picchi nella creazione:** Identifica i periodi con attività di creazione moduli insolitamente elevate. Ciò può indicare progetti o iniziative specifici che richiedono nuovi moduli.

### Forms pubblicato

- **Scopo:** Questo grafico tiene traccia del numero di moduli pubblicati (resi disponibili per l&#39;uso) nel periodo di tempo selezionato.

  ![Grafico Forms pubblicato](/help/forms/assets/forms-publish-vr-dashboard-form-insights.png)


- **Informazioni da estrarre:**
   - **Frequenza distribuzione moduli:** Monitorare la frequenza con cui i nuovi moduli vengono distribuiti agli utenti.
   - **Ritardo tra creazione e pubblicazione:** Analizzare la differenza di tempo tra il grafico &quot;Forms Created&quot; e il grafico &quot;Forms Published&quot;. Un ritardo significativo può indicare colli di bottiglia nel processo di approvazione o distribuzione del modulo.

## Utilizzo frammento

Questa sezione fornisce informazioni sull’utilizzo dei frammenti di modulo, che sono componenti riutilizzabili che possono essere incorporati in più moduli.

![Grafico Forms pubblicato](/help/forms/assets/fragment-usage-vr-dashboard-form-insights.png)

### Numero di frammenti di modulo in uso

- **Tipo di grafico:** Visualizzazione numerica (con un singolo valore)
- **Scopo:** Visualizza il numero totale di frammenti di modulo univoci attualmente utilizzati nei moduli attivi.
- **Informazioni da estrarre:**
   - **Adozione frammento:** Valuta l&#39;adozione complessiva dei frammenti di modulo all&#39;interno dell&#39;organizzazione. Un numero più alto indica un maggiore utilizzo di componenti riutilizzabili.

### Riutilizzo di frammenti di moduli

- **Tipo di grafico:** Visualizzazione numerica (con un singolo valore)
- **Scopo:** Visualizza il numero totale di volte in cui i frammenti di modulo sono stati riutilizzati in diversi moduli. Questa metrica indica l’efficacia con cui i frammenti vengono utilizzati per evitare duplicazioni e mantenere la coerenza.
- **Informazioni da estrarre:**
   - **Frequenza di riutilizzo frammenti:** Monitora la frequenza con cui i frammenti esistenti vengono riutilizzati nei nuovi moduli. Un numero più elevato indica un migliore utilizzo dei componenti riutilizzabili e una maggiore efficienza.

## Scenari di esempio

- **Scenario:** si nota un calo improvviso in &quot;Invii modulo&quot;.
   - **Azione:** Analizzare le possibili cause, ad esempio i tempi di inattività dei moduli, problemi di usabilità o il calo del traffico verso la pagina di destinazione del modulo.
- **Scenario:** il valore &quot;Riutilizzo frammento di modulo&quot; è basso.
   - **Azione:** Promuovi al tuo team i vantaggi dell&#39;utilizzo dei frammenti di modulo, assicurati che i frammenti siano ben organizzati e facili da trovare e fornisci informazioni su come creare e riutilizzare i frammenti in modo efficace.
- **Scenario:** si verifica un ritardo significativo tra &quot;Forms Created&quot; e &quot;Forms Published&quot;.
   - **Azione:** Rivedi il processo di approvazione e distribuzione del modulo per identificare ed eliminare i colli di bottiglia.



## Consulta anche

- [Informazioni sulla dashboard di realizzazione del valore](/help/forms/aem-forms-value-realization-dashboard.md)
