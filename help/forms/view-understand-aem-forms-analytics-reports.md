---
title: Visualizzazione e comprensione dei rapporti di analisi adattiva di Forms
description: Forms adattivo si integra perfettamente con Adobe Analytics per acquisire e tenere traccia delle metriche delle prestazioni per i moduli e i documenti pubblicati.
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: 39ea959cb0a0568fd94ca455be935228479c0415
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---


# Visualizzazione e comprensione dei rapporti di analisi adattiva di Forms {#viewing-and-understanding-aem-forms-analytics-reports}

<span class="preview"> Si tratta di una funzione pre-release accessibile tramite [canale preliminare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

Nel panorama in rapida evoluzione dell’analisi digitale, è fondamentale rimanere in sintonia con le tendenze globali per prendere decisioni informate e ottimizzare le esperienze digitali. Per risolvere questo problema, Forms adattivo si integra perfettamente con Adobe Analytics per acquisire e tenere traccia delle metriche delle prestazioni per i moduli e i documenti pubblicati. L’obiettivo alla base dell’analisi di queste metriche è prendere decisioni basate sui dati, utilizzando metriche e analisi per migliorare l’usabilità e l’efficacia dei moduli.

Acquisendo e tenendo traccia degli indicatori di prestazioni chiave, le aziende possono individuare aree di miglioramento, ottimizzare le esperienze utente e, in ultima analisi, ottenere risultati migliori per creare esperienze cliente eccezionali.

## Configurare Adobe Analytics per Adaptive Forms {#setup-adobe-analytics-to-aem-forms}

Per il rapporto di AEM Forms Analytics, devi innanzitutto integrare Adobe Analytics in AEM Forms tramite Experience Cloud Setup Automation. Experience Cloud Setup Automation in Adaptive Forms richiede una licenza Adobe Analytics, Data Collection (in precedenza Adobe Launch) per gestire gli script di tracciamento e l’integrazione con l’API di Experience Platform Launch per l’aggregazione dati semplificata e la generazione di informazioni. Visita [Abilitare Adobe Analytics per un modulo adattivo utilizzando Experience Cloud Setup Automation](/help/forms/forms-experience-cloud-setup-automation.md) per informazioni complete sull&#39;installazione.

## Visualizzare il rapporto di Adaptive Forms Adobe Analytics {#view-adobe-analytics-report}

1. Nella tua istanza AEM, vai a **[!UICONTROL Forms]** >> **[!UICONTROL Forms e documento]**.
1. Seleziona il modulo, vedrai che Adobe Analytics è integrato come mostrato a sinistra, nel Forms attivato per Adobe Analytics.

   ![Visualizza rapporto](assets/activ-aa.png){width="100%"}

1. Clic **Adobe Analytics** per visualizzare il report e analizzare i dati sulle prestazioni.

## Rapporto di analisi di Adaptive Forms {#understanding-aem-forms-analytics-reports}

Adobe Analytics offre una gamma completa di metriche delle prestazioni di Adaptive Forms progettate per fornire informazioni preziose sull’utilizzo dei moduli. Queste metriche sono:

### **Quali sono le prestazioni di Adaptive Forms?** {#how-your-adaptive-form-is-performing}

Contiene le metriche Rendering moduli, Invio moduli, Errori di convalida e Visitatori univoci, che consentono di valutare l’utilizzo e l’efficacia dei moduli:

* **Rappresentazioni di moduli**: le rappresentazioni dei moduli mostrano il numero di volte in cui il modulo è stato renderizzato o aperto.

* **Invio di moduli**: l’invio di moduli indica quante volte i moduli adattivi vengono completati e inviati correttamente dagli utenti.

* **Errori di convalida**: errore di convalida visualizza il numero totale di errori correlati alla convalida che si sono verificati nei campi dei moduli.

* **Visitatori univoci**: i visitatori univoci rappresentano il numero di volte in cui un visitatore esegue il rendering del modulo. Per ulteriori informazioni sui visitatori univoci, consulta [Visitatori univoci, visite e comportamento del cliente](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html).

  ![Prestazioni Forms](assets/forms-performance.png){width="100%"}

### **Visitatori dei moduli** {#visitors-to-your-forms}

Consente di ottenere informazioni utili sull’attività del visitatore nei moduli:

* **Visite e invii**: descrive la frequenza delle visite ai moduli in un intervallo di date e il numero corrispondente di invii, per ulteriori informazioni su questo clic [Visite](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html).
* **Visitatori univoci e loro visite totali**: distingue tra utenti nuovi e utenti di ritorno. Ad esempio, un visitatore può visitare il tuo sito ogni giorno per un mese, ma continua a contare come un singolo visitatore univoco. Visita [Visitatori univoci](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html) per informazioni dettagliate.

  ![Visitatori Forms](assets/forms-visitors.png){width="100%"}

### **Tipo di dispositivo** {#device-type}

Tipo di dispositivo consente di identificare il tipo di dispositivo utilizzato per accedere ai moduli. Classifica il tipo di dispositivo come Tipo di dispositivo mobile. Ad esempio, in questo caso, è Tipo di dispositivo mobile: Altro e Tipo di dispositivo mobile: Telefono cellulare. I vari tipi di dispositivi mobili includono telefono cellulare, tablet, lettore multimediale, console di gioco e altro ancora.

![Tipo di dispositivo](assets/device-type.png){width="100%"}

### **Ripartizione geografica** {#geographical-breakdown}

Mostra la posizione da cui si accede a Forms. Fornisce informazioni specifiche per l&#39;area geografica degli utenti del modulo. Ad esempio, è possibile vedere che un utente del modulo include informazioni specifiche per l&#39;area geografica dell&#39;India, come illustrato nell&#39;immagine.

![Ripartizione geografica](assets/geographical-breakdown.png){width="100%"}

### **Principali fonti di traffico e moduli popolari** {#top-sources-of-traffic-and-popular-forms}

In questo modo è possibile identificare l&#39;origine primaria o il collegamento da cui si fa riferimento ai moduli. Ad esempio, nell’immagine seguente sono presenti istanze di ricerca per i moduli adattivi in cui il 18,9% **Digitato/Contrassegnato con segnalibro**, 70,49% in base a **Motori di ricerca** e il 24% proviene da **Altri siti Web**. Puoi definire gli elementi dimensionali in base alle tue esigenze. Inoltre, puoi individuare i moduli più visitati o più popolari.

![Siti di riferimento](assets/referred-sites.png){width="100%"}

### **Attività utente nei moduli principali** {#user-activity-on-top-forms}

Una visualizzazione completa del coinvolgimento degli utenti con visite sul campo, rappresentazioni dei moduli, errori di convalida, moduli abbandonati e invii di moduli fornisce informazioni approfondite sui moduli più attivi. Nell’immagine riportata di seguito, puoi vedere che il modulo di richiesta è il più attivo in base alle metriche Evento modulo.

![Attività utente](assets/user-activity.png){width="100%"}

### **Timeline per il tempo trascorso sui moduli** {#timeline-for-time-spent-on-forms}

È il tempo che gli utenti dedicano ai moduli nel tempo che consente di identificare i pattern di coinvolgimento.

![Tempo trascorso sui moduli](assets/time-spent-on-forms.png){width="100%"}

### **Aree in cui i visitatori richiedono assistenza per la compilazione del modulo** {#areas-requiring-assistance}

Metriche quali visualizzazioni dell’Aiuto, errori di convalida e visite sul campo rivelano dove gli utenti hanno bisogno di assistenza o come possiamo tracciare gli errori nei campi. Nell&#39;immagine seguente, ad esempio, viene visualizzato in un modulo con campi quali **Nome e cognome**, **Numero di telefono**, **DoB**. Il **Nome e cognome** Il campo include 12 visite, di cui 8 con errore di convalida e 1 con clic sull’icona della guida per visualizzare la guida in linea relativa a questo campo. Puoi visualizzare i dati delle metriche per altri campi modulo.

![Aree di assistenza](assets/assisting-areas.png){width="100%"}

### **Ultimo campo modulo visualizzato dai visitatori prima dell’abbandono del modulo** {#last-form-field-that-visitors-viewed}

Consente di analizzare i campi del modulo in cui gli utenti hanno trascorso del tempo prima di abbandonare il modulo. Ad esempio, nell’immagine seguente, su 5 moduli abbandonati, 2 rimangono sul campo **Nome e cognome**, 2 a sinistra sul campo **Numero di telefono**, e 1 lasciato sul campo **Input testo**.

![Visitatori sul campo](assets/field-visitors.png){width="100%"}