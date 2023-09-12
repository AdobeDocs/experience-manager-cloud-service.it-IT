---
title: Abilitare Adobe Analytics per un modulo adattivo utilizzando Experience Cloud Setup Automation
description: Experience Cloud Setup Automation consente di collegare Adobe Analytics a un modulo adattivo. Aiuta a tracciare e analizzare l’interazione dell’utente con un modulo adattivo, offrendo informazioni approfondite sulle interazioni e sul coinvolgimento dei visitatori.
source-git-commit: b44b54a88b87dc391dfeb51fb8b83095c274bd38
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---


# Abilitare Adobe Analytics per un modulo adattivo utilizzando Experience Cloud Setup Automation {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

<span class="preview"> Si tratta di una funzione pre-release accessibile tramite [canale preliminare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

Experience Cloud Setup Automation consente di collegare Adobe Analytics ad Adaptive Forms per monitorare e analizzare l’interazione dell’utente con i moduli e offrire informazioni approfondite sulle interazioni e sul coinvolgimento dei visitatori. Experience Cloud Setup Automation consente inoltre di monitorare le prestazioni dei moduli tramite la valutazione di metriche quali tempi di completamento e punti di riconsegna. Questa analisi consente di ottimizzare i moduli per una migliore esperienza utente, distinguendo al contempo il comportamento degli utenti in base allo stato di accesso, ad esempio utenti anonimi, per identificare tendenze e modelli generali.

## Vantaggi dell’integrazione di Adobe Analytics con Adaptive Forms {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **Informazioni sul comportamento degli utenti finali**: Adobe Analytics consente di ottenere informazioni sul comportamento degli utenti finali, rivelare le azioni degli utenti, i tassi di abbandono e i tassi di completamento, consentendo una comprensione più approfondita del modo in cui i singoli utenti interagiscono con i moduli.
* **Consentire agli utenti aziendali non tecnici di ottenere informazioni approfondite**: Adobe Analytics, tramite la sua interfaccia di facile utilizzo, consente anche agli utenti non tecnici di accedere e interpretare i dati di utilizzo dei moduli, promuovendo decisioni basate sui dati per migliorare le esperienze di registrazione.
* **Ottimizzazione dell’esperienza di acquisizione dati in base all’utilizzo**: le organizzazioni identificano facilmente i punti critici nell’acquisizione dei dati, consentendo miglioramenti mirati che migliorano l’usabilità dei moduli e aumentano il numero di invii riusciti.

## Ambito delle metriche di utilizzo di Adaptive Forms {#scope-of-adaptive-forms-usage-metrics}

Adobe Analytics offre una gamma completa di metriche delle prestazioni di Adaptive Forms progettate per fornire informazioni preziose sull’utilizzo dei moduli. Queste metriche sono:

* **Rappresentazioni di moduli, invii di moduli, errori di convalida e visitatori univoci**, che consente di valutare l’utilizzo e l’efficacia dei moduli.

* **Approfondimenti visitatore** che include le frequenze di visite e invii e i conteggi di visitatori univoci, offrendo una visualizzazione completa del pubblico del modulo.

* **Tipo di dispositivo** dati che consentono di ottenere informazioni sui dispositivi utilizzati dagli utenti per accedere ai moduli.

* **Ripartizione geografica** mostra la distribuzione regionale degli utenti del modulo.

* **Origini di traffico** e **Moduli popolari** Le metriche, costituite dai domini di riferimento principali e dai moduli più visitati, consentono di comprendere da dove proviene il traffico e quali sono i moduli più popolari.

* **Attività utente nei moduli principali** fornisce informazioni approfondite su visite in loco, rappresentazioni di moduli, errori di convalida, moduli abbandonati e invii di moduli, consentendo di analizzare il comportamento degli utenti.

* **Timeline per il tempo trascorso sui moduli** che offre una visualizzazione del coinvolgimento degli utenti con i moduli basata su timeline.

* **Aree che richiedono assistenza visitatore** metriche che includono visualizzazioni della guida, istanze di errori di convalida e frequenze di visite sul campo, evidenziando i casi in cui gli utenti possono aver bisogno di assistenza nella compilazione dei moduli.

![Rapporto di Analytics](assets/analytics-report.png)


Per informazioni dettagliate su ciascuna metrica, visita [Visualizzazione e comprensione dei rapporti di AEM Forms Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Prerequisiti {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

Experience Cloud Setup Automation in Adobe Experience Manager Forms richiede un **Licenza Adobe Analytics**, **Raccolta Dati (Precedentemente Adobe Launch)** per gestire gli script di tracciamento e l&#39;integrazione con **Experience Platform Launch (API)** per l’aggregazione dati semplificata e la generazione di informazioni.

Se disponi di una licenza attiva per Experience Cloud Setup Automation, Adobe Analytics e l’API di Experience Platform Launch, è necessario verificarne la disponibilità all’interno della console per sviluppatori.

Per verificare che quanto sopra sia disponibile per l’ambiente Forms as a Cloud Service, visita il [console per sviluppatori](https://developer.adobe.com/console/projects), accedi al progetto e cerca nel progetto con l’ID del programma, ad esempio per l’ambiente con URL `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, l’id del programma è `p45913-e175111`. Assicurati che siano elencate le API Experience Cloud Setup Automation, Adobe Analytics e Experienci Platform Launch. Se questi sono elencati, puoi abilitare Adobe Analytics per il tuo Forms adattivo.

![Prerequisito per l’integrazione di Forms Analytics](assets/analytics-aem.png)

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html)
-->

## Configurare Adobe Analytics {#configure-adobe-analytics}

Per abilitare e configurare Adobe Analytics per il Forms adattivo, effettua le seguenti operazioni:

* [Abilitare Adobe Analytics per Forms adattivo basato su componenti di base](#integrate-adobe-analytics-with-aem-forms-for-foundation-component)
* [Abilitare Adobe Analytics per Forms adattivo basato su componenti core](#integrate-adobe-analytics-with-aem-forms-for-core-components)

### Abilitare Adobe Analytics con il componente Forms adattivo per Foundation {#integrate-adobe-analytics-with-aem-forms-for-foundation-component}

1. Crea un contenitore di configurazione per servizi cloud:
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Seleziona o crea un contenitore di configurazione e abilita la cartella per **[!UICONTROL Configurazioni cloud]**.
   1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.
1. Nella tua istanza AEM, vai a **[Forms]** >> **[Forms e documento]**.
1. Seleziona il **[!UICONTROL Modulo]** >> **[!UICONTROL Proprietà]**, Nella **[!UICONTROL Contenitore configurazione]**, seleziona il contenitore di configurazione creato o selezionato in **[!UICONTROL Browser configurazioni]** nel passaggio 1.
1. Seleziona il pannello Attività nella barra a sinistra e fai clic su **Configurazione analisi** e **Attivare Adobe Analytics**.
1. Immetti il nome desiderato per la suite di rapporti, fai clic su **[!UICONTROL Successivo]** e **[!UICONTROL Salva]**.
1. Dopo il salvataggio del progetto, la configurazione viene eseguita per un certo periodo di tempo fino all’integrazione di Adobe Analytics con il modulo adattivo. Puoi anche controllare il **stato dell’integrazione**.

   >[!NOTE]
   >
   >Se la configurazione richiede più di 15 minuti, riprova ad abilitare le analisi per i moduli.

1. Nella tua istanza AEM, vai a **[!UICONTROL Forms]** >> **[Forms e documento]** e seleziona il tuo **[!UICONTROL Modulo]**, come illustrato nell’immagine seguente, Adobe Analytics è integrato nel modulo.
1. Ora puoi visualizzare [Rapporto Adobe Analytics modulo adattivo](#view-adobe-analytics-report).

![Analisi AEM integrata](assets/analytics-aem-integrated.png)

### Abilitare Adobe Analytics con Forms adattivo per i componenti core {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. Nella tua istanza AEM, vai a **[!UICONTROL Forms]** >> **[!UICONTROL Forms e documento]** e seleziona il tuo **[!UICONTROL Modulo]**.
1. Selezionare il Pannello attività a sinistra e fare clic su **Configurazione analisi** e **Attivare Adobe Analytics**.
1. Immetti il nome desiderato per la suite di rapporti, fai clic su **[!UICONTROL Successivo]** e **[!UICONTROL Salva]**.
1. Dopo il salvataggio del progetto, la configurazione viene eseguita per un certo periodo di tempo fino all’integrazione di Adobe Analytics con il modulo adattivo. Puoi anche controllare il **stato dell’integrazione**.

   >[!NOTE]
   >
   >Se la configurazione richiede più di 15 minuti, riprova ad abilitare le analisi per i moduli.

1. Nella tua istanza AEM, vai a **[!UICONTROL Forms]** >> **[!UICONTROL Forms e documento]** e seleziona il tuo **[!UICONTROL Modulo]**, Adobe Analytics è integrato nel modulo.
1. Ora puoi visualizzare [Rapporto Adobe Analytics modulo adattivo](#view-adobe-analytics-report).

## Visualizzare il rapporto di Adaptive Forms Adobe Analytics {#view-adobe-analytics-report}

1. Nella tua istanza AEM, vai a **[!UICONTROL Forms]** >> **[!UICONTROL Forms e documento]**.
1. Seleziona il modulo, vedrai che Adobe Analytics è integrato come mostrato a sinistra, nel Forms attivato per Adobe Analytics.

   ![Visualizza rapporto](assets/activ-aa.png)

1. Clic **Adobe Analytics** per visualizzare il report e analizzare i dati sulle prestazioni.

Per collegare un modulo adattivo ad Adobe Analytics utilizzando il metodo manuale, visita [Integrare AEM Forms con Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md).
