---
title: Come abilitare Adobe Analytics per un’analisi rapida di un modulo adattivo?
description: Experience Cloud Setup Automation consente di collegare Adobe Analytics a un modulo adattivo per ottenere analisi rapide e informazioni approfondite sulle interazioni e sul coinvolgimento dei visitatori.
keywords: Abilita Adobe Analytics per un modulo adattivo utilizzando Experience Cloud Setup Automation, Abilita Adobe Analytics in Forms, Adobe Analytics in Adaptive Forms, integrazione Forms Analytics, Forms e Adobe Analytics
feature: Adaptive Forms
role: Admin, User
exl-id: 0e1aa040-08b4-4c1a-b247-ad6fff410187
source-git-commit: a23576b5dc6d78a29fe19cd23f3c4788f2bee23e
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 2%

---

# Abilitare Adobe Analytics per un modulo adattivo utilizzando Experience Cloud Setup Automation {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Questo articolo |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html?lang=it) |

Experience Cloud Setup Automation consente di collegare Adobe Analytics ad Adaptive Forms, facilitando l’analisi rapida dell’interazione dell’utente con i moduli e fornendo informazioni approfondite sulle interazioni e sul coinvolgimento dei visitatori. Experience Cloud Setup Automation consente inoltre di monitorare le prestazioni dei moduli tramite la valutazione di metriche quali tempi di completamento e punti di riconsegna. Questa analisi consente di ottimizzare i moduli per una migliore esperienza utente, distinguendo al contempo il comportamento degli utenti in base allo stato di accesso, ad esempio utenti anonimi, per identificare tendenze e modelli generali.

## Vantaggi dell’integrazione di Adobe Analytics con Adaptive Forms {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **Informazioni sul comportamento dell&#39;utente finale**: Adobe Analytics consente di ottenere informazioni sul comportamento dell&#39;utente finale, rivelare le azioni dell&#39;utente, gli abbandoni e i tassi di completamento, consentendo una comprensione più approfondita del modo in cui i singoli utenti interagiscono con i moduli.
* **Consentire agli utenti aziendali non tecnici di ottenere informazioni**: Adobe Analytics, tramite la sua interfaccia di facile utilizzo, consente anche agli utenti non tecnici di accedere e interpretare i dati di utilizzo dei moduli, favorendo decisioni basate sui dati per migliorare le esperienze di registrazione.
* **Ottimizzazione dell&#39;esperienza di acquisizione dati in base all&#39;utilizzo**: le organizzazioni identificano facilmente i punti critici nell&#39;acquisizione dei dati, con miglioramenti mirati che migliorano l&#39;usabilità dei moduli e aumentano le richieste di invio corrette.

## Ambito delle metriche di utilizzo di Adaptive Forms {#scope-of-adaptive-forms-usage-metrics}

Adobe Analytics offre una gamma completa di metriche delle prestazioni di Adaptive Forms progettate per fornire informazioni preziose sull’utilizzo dei moduli e offre un’analisi rapida. Queste metriche sono:

* **Rappresentazioni di moduli, invii di moduli, errori di convalida e visitatori univoci**, che consentono di valutare l&#39;utilizzo e l&#39;efficacia dei moduli.

* **Visitor Insights** che include le frequenze di visita e invio e il numero di visitatori univoci, offrendo una visualizzazione completa del pubblico del modulo.

* **Tipo di dispositivo** dati che forniscono informazioni sui dispositivi utilizzati dagli utenti per accedere ai moduli.

* **La suddivisione geografica** rivela la distribuzione regionale degli utenti del modulo.

* Le metriche **Origini traffico** e **Moduli popolari**, costituite dai principali domini di riferimento e dai moduli più visitati, consentono di comprendere da dove proviene il traffico e quali moduli sono più popolari.

* **L&#39;attività utente nei primi moduli** fornisce informazioni approfondite sulle visite ai campi, sulle rappresentazioni dei moduli, sugli errori di convalida, sui moduli abbandonati e sull&#39;invio dei moduli, consentendo di analizzare il comportamento degli utenti.

* **Timeline per il tempo trascorso sui moduli**, che offre una visualizzazione del coinvolgimento degli utenti con i moduli basata su una cronologia.

* **Aree che richiedono assistenza ai visitatori** metriche che includono visualizzazioni della Guida, istanze di errori di convalida e frequenze di visite sul campo, evidenziando le aree in cui gli utenti potrebbero aver bisogno di assistenza per la compilazione dei moduli.

![Rapporto Analytics](assets/analytics-report.png){width="100%"}


Per informazioni dettagliate su ciascuna metrica, visita [Visualizzazione e comprensione dei rapporti di AEM Forms Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Prerequisiti {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

Experience Cloud Setup Automation richiede una **licenza Adobe Analytics**, **raccolta dati (in precedenza Adobe Launch)** per gestire gli script di tracciamento e **licenza Experience Manager Forms** per l&#39;aggregazione dati semplificata e la generazione di informazioni approfondite.

Se disponi di una licenza attiva per **Adobe Analytics** e **Experience Manager Forms** e di un&#39;integrazione con **Data Collection (in precedenza Adobe Launch)**, devi verificarne la disponibilità all&#39;interno della console per sviluppatori.

Per verificare la disponibilità di questi elementi per l&#39;ambiente Forms as a Cloud Service, visitare la [console per sviluppatori](https://developer.adobe.com/console/projects), passare al progetto e cercare il progetto con l&#39;ID programma - ID ambiente, ad esempio, per l&#39;ambiente con URL `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, ID programma - ID ambiente: `p45913-e175111`. Assicurati che siano elencate le API Experience Cloud Setup Automation, Adobe Analytics e Experienci Platform Launch. Se questi sono elencati, puoi abilitare Adobe Analytics per un’analisi rapida del tuo Forms adattivo.

![Integrazione prerequisito di Forms Analytics](assets/analytics-aem.png){width="100%"}

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html?lang=it)
-->

## Configurare Adobe Analytics {#configure-adobe-analytics}

Per abilitare e configurare Adobe Analytics per un’analisi rapida del tuo Forms adattivo, effettua le seguenti operazioni:

* [Abilitare Adobe Analytics per Forms adattivo basato su componenti di base](#integrate-adobe-analytics-with-aem-forms-for-foundation-component)
* [Abilitare Adobe Analytics per Forms adattivo basato su componenti core](#integrate-adobe-analytics-with-aem-forms-for-core-components)

>[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)


<!--
>[!NOTE]
>
> This is the demo video for **Foundation Component**. In **Core Component** you are required to perform similar steps but the container is not chosen for forms.
-->

### Abilitare Adobe Analytics con il componente Forms adattivo per Foundation {#integrate-adobe-analytics-with-aem-forms-for-foundation-component}

1. Crea un contenitore di configurazione per servizi cloud:
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Seleziona o crea un contenitore di configurazione e abilita la cartella per **[!UICONTROL Configurazioni cloud]**.
   1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.
1. Nell&#39;istanza AEM, vai a **[Forms]** >> **[Forms e documento]**.
1. Seleziona il **[!UICONTROL modulo]** >> **[!UICONTROL proprietà]**. Nel **[!UICONTROL contenitore configurazione]**, seleziona il contenitore configurazione creato o selezionato nel **[!UICONTROL browser configurazioni]** nel passaggio 1.
1. Seleziona il pannello attività nella barra a sinistra e fai clic su **Imposta analisi** e **Attiva Adobe Analytics**.
1. Specifica il nome che preferisci per la suite di rapporti. Fai clic su **[!UICONTROL Avanti]** e **[!UICONTROL Salva]**.
1. Dopo il salvataggio del progetto, la configurazione viene eseguita per un certo periodo di tempo fino all&#39;integrazione di Adobe Analytics con il modulo adattivo. Puoi anche controllare lo **stato di integrazione**.

   >[!NOTE]
   >
   >Se la configurazione richiede più di 15 minuti, riprova ad abilitare le analisi per i moduli.

1. Nell&#39;istanza dell&#39;AEM, vai a **[!UICONTROL Forms]** >> **[Forms e documento]** e seleziona il **[!UICONTROL Modulo]**, noterai che Adobe Analytics è integrato nel tuo modulo come illustrato nell&#39;immagine seguente.
1. Ora puoi visualizzare il tuo [report Adobe Analytics modulo adattivo](#view-adobe-analytics-report).

![Analisi AEM integrata](assets/analytics-aem-integrated.png){width="100%"}


### Abilitare Adobe Analytics con Forms adattivo per i componenti core {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. Nell&#39;istanza AEM, vai a **[!UICONTROL Forms]** >> **[!UICONTROL Forms e Document]** e seleziona il tuo **[!UICONTROL Form]**.
1. Selezionare il Pannello attività a sinistra e fare clic su **Imposta analisi** e **Attiva Adobe Analytics**.
1. Specifica il nome che preferisci per la suite di rapporti. Fai clic su **[!UICONTROL Avanti]** e **[!UICONTROL Salva]**.
1. Dopo il salvataggio del progetto, la configurazione viene eseguita per un certo periodo di tempo fino all&#39;integrazione di Adobe Analytics con il modulo adattivo. Puoi anche controllare lo **stato di integrazione**.

   >[!NOTE]
   >
   >Se la configurazione richiede più di 15 minuti, riprova ad abilitare le analisi per i moduli.

1. Nell&#39;istanza dell&#39;AEM, vai a **[!UICONTROL Forms]** >> **[!UICONTROL Forms e Document]** e seleziona il **[!UICONTROL Form]**, noterai che Adobe Analytics è integrato nel tuo modulo.
1. Ora puoi visualizzare il tuo [report Adobe Analytics modulo adattivo](#view-adobe-analytics-report).

## Visualizzare il rapporto di Adaptive Forms Adobe Analytics {#view-adobe-analytics-report}

1. Nell&#39;istanza AEM, vai a **[!UICONTROL Forms]** >> **[!UICONTROL Forms e documento]**.
1. Seleziona il modulo, vedrai che Adobe Analytics è integrato come mostrato a sinistra, nel Forms attivato per Adobe Analytics.

   ![Visualizza report](assets/activ-aa.png){width="100%"}

1. Fai clic su **Adobe Analytics** per visualizzare il tuo report e analizzare i dati sulle prestazioni.

Per collegare un modulo adattivo ad Adobe Analytics utilizzando il metodo manuale, visita [Integrare AEM Forms con Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md).

## Abilitare Analytics a Forms adattivo nei siti {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

La configurazione di analisi rapide per il modulo adattivo in AEM Sites consente di tenere traccia delle interazioni degli utenti e dell’invio dei moduli sulla pagina del modulo in Sites. Integrando perfettamente le analisi nel Forms di Sites, puoi ottenere informazioni preziose sul comportamento degli utenti, sui tassi di conversione e sulle aree in cui è possibile migliorare il modulo.

### Prerequisiti {#Prerequisites-to-connect-forms-analytics-to-sites}

Per connettersi e abilitare le analisi in Adaptive Forms per AEM Sites, assicurati che il tuo AEM Sites disponga di un Adobe Analytics attivo.

### Connettere Forms adattivo in Sites per abilitare Analytics {#Connect-analytics-to-adaptive-forms}

Per connettere il modulo adattivo in una pagina di AEM Sites per abilitare Analytics per un&#39;analisi rapida, includere la libreria client `customfooterlibs` nella pagina di AEM Sites utilizzando l&#39;archivio e la pipeline di distribuzione dell&#39;archetipo/Git AEM.

1. Apri il progetto [Archetipo AEM Forms o Archivio Git clonato](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) in un editor di testo. Ad esempio, Visual Studio Code.

1. Passa alla pagina dei tuoi siti in cui esiste il modulo adattivo, ad esempio In questo progetto demo abbiamo `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.

1. Copia il valore di `sling:resourceSuperType`. Ad esempio, il valore è `core/wcm/components/page/v3/page`.

   ![risorsa Sling](/help/forms/assets/slingresource.png){width="100%"}

1. Creare la struttura simile nel percorso `ui.apps/src/main/content/jcr_root/apps` come `core/wcm/components/page/v3/page`.

   ![struttura sovrapposta](/help/forms/assets/overlaystructure.png){width="100%"}

1. Aggiungi un file `customfooterlibs.html`.

   ```
   // customheaderlibs.html
   <sly data-sly-use.page="com.adobe.cq.wcm.core.components.models.Page">
   <sly data-sly-test="${page.data && page.dataLayerClientlibIncluded}" data-sly-call="${clientlib.js @ categories='core.forms.components.commons.v1.datalayer', async=true}"></sly>
   </sly>
   ```

   `customfooterlibs.html` è utilizzato per JavaScript.

1. [Esegui la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=it) per distribuire le modifiche.

### Abilitare le regole di analisi dei moduli in Forms in Sites {#bind-forms-analytics-rules-to-forms-in-sites}

1. Visita la **raccolta dati di Adobe Experience Platform**.
1. Fai clic su **Tag** che si trova sul lato sinistro.
1. Cercare nel progetto con l&#39;ID di programma come mostrato nell&#39;immagine seguente, ad esempio, per l&#39;ambiente con URL `https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html`, ID di programma: `45921`.

   ![Cerca-il-tuo-modulo-nella-raccolta-dati](/help/forms/assets/aep-data-collection.png){width="100%"}

1. Aggiungi la configurazione per **Regole modulo** e **Elementi dati** come indicato di seguito:

#### Aggiungi regole modulo {#form-rules}

1. Seleziona il modulo e aggiungi **Nuova proprietà** in alto a destra, oppure fai clic sul modulo.
1. Nella pagina delle proprietà, fai clic su **Regole** e seleziona gli eventi per il modulo. Nell&#39;immagine di esempio seguente, sono **Eventi modulo**.

   ![Cerca-il-tuo-modulo-nella-raccolta-dati](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. Seleziona tutti gli eventi del modulo e **copia** che si trova nella barra in alto a destra.
1. Dopo aver copiato, viene visualizzato un pop-up **Copia regola** in cui si cerca nella pagina Sites l&#39;ID progetto, per incollare le regole del modulo.

   ![Copia-regole-modulo](/help/forms/assets/copy-form-rules.png){width="100%"}

1. Fai clic su **copia** per incollare le regole del modulo nella pagina Sites.

#### Aggiungi elementi dati {#data-elements}

1. Seleziona il modulo e aggiungi **Nuova proprietà** in alto a destra, oppure fai clic sul modulo.
1. Nella pagina delle proprietà, fai clic su **Elementi dati** e seleziona gli eventi per il modulo.
1. Seleziona tutti gli eventi del modulo e **copia** che si trovano nella barra in alto a destra.
1. Dopo aver copiato, viene visualizzato un pop-up **Copia regola** in cui si cerca nella pagina Sites l&#39;ID progetto, per incollare le regole del modulo.
1. Fai clic su **copia** per incollare le regole del modulo nella pagina Sites.

   ![Elementi-dati-modulo](/help/forms/assets/form-data-elements.png){width="100%"}

Dopo aver associato le regole di Form e Sites tramite i passaggi sopra indicati, effettua le seguenti operazioni per abilitare Analytics per il modulo adattivo nella pagina Sites:

1. Fai clic su **Flusso di pubblicazione** a sinistra.
1. Fare clic su **Aggiungi libreria** e immettere il nome desiderato.
1. Nel menu a discesa **Ambiente** a destra, seleziona **sviluppo**.
1. Fare clic su **Aggiungi tutte le risorse modificate**.
1. Fai clic su **Salva e genera in sviluppo**.

![pubblicazione su sviluppo](/help/forms/assets/publish-to-dev.png){width="100%"}


<!--

## Best Practices

1.    Verify that Adobe Analytics is enabled on all the forms activated for Adobe Analytics.

1.    Check the Adobe Analytics report periodically to gain insights into user behavior and form performance. For instance, you may set the cadence to 15 days or the period you prefer to choose for report analysis. This enables you to improve the forms enrollment experience.

1.    Enable Analytics for all or most of your forms for tracking and analyzing user interaction with your forms and to gain insights into visitor interactions and engagement.

1. Check your forms performance after you update your form fields or components.

1.    Share Analytics report with your peer groups for review, you can schedule your report for a later time.

-->

## Consulta anche {#see-also}

* [Visualizzare e comprendere i rapporti di Adaptive Forms Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)
* [Aggiungere un modulo adattivo a una pagina o a un frammento di esperienza di AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Integrare AEM Forms con Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
