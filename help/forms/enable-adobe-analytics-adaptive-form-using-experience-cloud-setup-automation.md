---
title: Abilitare Adobe Analytics per un modulo adattivo
description: Experience Cloud Setup Automation consente di collegare Adobe Analytics a un modulo adattivo per monitorare le informazioni sulle interazioni e il coinvolgimento dei visitatori.
source-git-commit: 4fc6d29cd008b04ad97ceb17201c1f8d0e72439e
workflow-type: tm+mt
source-wordcount: '1534'
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

![Rapporto di Analytics](assets/analytics-report.png){width="100%"}


Per informazioni dettagliate su ciascuna metrica, visita [Visualizzazione e comprensione dei rapporti di AEM Forms Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Prerequisiti {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

Experience Cloud Setup Automation richiede un **Licenza Adobe Analytics**, **Raccolta Dati (Precedentemente Adobe Launch)** per gestire gli script di tracciamento e **Licenza Experience Manager Forms** per l’aggregazione dati semplificata e la generazione di informazioni.

Se si dispone di una licenza attiva per **Adobe Analytics** e **Experience Manager Forms** e l’integrazione con **Raccolta Dati (Precedentemente Adobe Launch)**, è necessario verificarne la disponibilità all’interno della console per sviluppatori.

Per verificare che quanto sopra sia disponibile per l’ambiente Forms as a Cloud Service, visita il [console per sviluppatori](https://developer.adobe.com/console/projects), accedi al progetto ed esegui una ricerca nel progetto con l’ID del programma, ad esempio l’ID dell’ambiente con l’URL `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, id programma - l’id ambiente è `p45913-e175111`. Assicurati che siano elencate le API Experience Cloud Setup Automation, Adobe Analytics e Experienci Platform Launch. Se questi sono elencati, puoi abilitare Adobe Analytics per il tuo Forms adattivo.

![Prerequisito per l’integrazione di Forms Analytics](assets/analytics-aem.png){width="100%"}

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

>[!VIDEO](https://video.tv.adobe.com/v/3424577/recaptcha-google-adaptive-forms/?quality=12&learn=on)


<!--
>[!NOTE]
>
> This is the demo video for **Foundation Component**. In **Core Component** you are required to perform similar steps but the container is not chosen for forms.
-->

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

![Analisi AEM integrata](assets/analytics-aem-integrated.png){width="100%"}


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

   ![Visualizza rapporto](assets/activ-aa.png){width="100%"}

1. Clic **Adobe Analytics** per visualizzare il report e analizzare i dati sulle prestazioni.

Per collegare un modulo adattivo ad Adobe Analytics utilizzando il metodo manuale, visita [Integrare AEM Forms con Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md).

## Abilitare Analytics a Forms adattivo nei siti {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

La configurazione di Analytics per il modulo adattivo in AEM Sites consente di monitorare le interazioni degli utenti e l’invio dei moduli nella pagina Modulo in Sites. Integrando perfettamente le analisi nel Forms di Sites, puoi ottenere informazioni preziose sul comportamento degli utenti, sui tassi di conversione e sulle aree in cui è possibile migliorare il modulo.

### Prerequisiti {#Prerequisites-to-connect-forms-analytics-to-sites}

Per connettersi e abilitare le analisi in Adaptive Forms per AEM Sites, assicurati che il tuo AEM Sites disponga di un Adobe Analytics attivo.

### Connettere Forms adattivo in Sites per abilitare Analytics {#Connect-analytics-to-adaptive-forms}

Per collegare un modulo adattivo a una pagina di AEM Sites per abilitare Analytics, includi `customfooterlibs` dalla libreria client alla pagina AEM Sites utilizzando l’archivio e la pipeline di distribuzione di Archetipo/Git AEM.

1. Apri il [Archetipo AEM Forms o archivio Git clonato](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) in un editor di testo. Ad esempio, Visual Studio Code.

1. Passa alla pagina dei tuoi Sites in cui esiste il modulo adattivo, ad esempio In questo progetto demo è disponibile `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.

1. Copia il valore di `sling:resourceSuperType`. Ad esempio, il valore è `core/wcm/components/page/v3/page`.

   ![risorsa sling](/help/forms/assets/slingresource.png){width="100%"}

1. Crea la struttura simile nel percorso `ui.apps/src/main/content/jcr_root/apps` uguale a `core/wcm/components/page/v3/page`.

   ![struttura di sovrapposizione](/help/forms/assets/overlaystructure.png){width="100%"}

1. Aggiungi un `customfooterlibs.html` file.

       &quot;
       // customheaderlibs.html
       &lt;sly data-sly-use.page=&quot;com.adobe.cq.wcm.core.components.models.Page&quot;>
       &lt;sly data-sly-test=&quot;${page.data &amp;&amp; page.dataLayerClientlibIncluded}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.commons.v1.datalayer&amp;#39;, async=true}&quot;>&lt;/sly>
       &lt;/sly>
       
       &quot;
   
   Il `customfooterlibs.html` viene utilizzato per JavaScript.

1. [Eseguire la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) per distribuire le modifiche.

### Abilitare le regole di analisi dei moduli in Forms in Sites {#bind-forms-analytics-rules-to-forms-in-sites}

1. Visita il **Raccolta dati di Adobe Experience Platform**.
1. Clic **Tag** sul lato sinistro.
1. Cerca nel tuo progetto con l’ID del programma come mostrato nell’immagine seguente, ad esempio per l’ambiente con URL `https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html`, l’id del programma è `45921`.

   ![Cercare il modulo nella raccolta dati](/help/forms/assets/aep-data-collection.png){width="100%"}

1. Aggiungi configurazione per **Regole modulo** e **Elementi dati** come indicato di seguito:

#### Aggiungi regole modulo {#form-rules}

1. Seleziona il modulo e aggiungi **Nuova proprietà** in alto a destra oppure fare clic sul modulo.
1. Nella pagina delle proprietà, fai clic su **Regole** e selezionare gli eventi per il modulo. Nell&#39;immagine di esempio riportata di seguito, è **Eventi modulo**.

   ![Cercare il modulo nella raccolta dati](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. Seleziona tutti gli eventi del modulo e **copia** che si trova sulla barra superiore destra.
1. Una volta copiata, **Copia regola** viene visualizzato un pop-up in cui si cerca nella pagina Sites l’ID progetto, per incollare le regole del modulo.

   ![Copiare-regole-modulo](/help/forms/assets/copy-form-rules.png){width="100%"}

1. Clic **copia** per incollare le regole del modulo nella pagina Sites.

#### Aggiungi elementi dati {#data-elements}

1. Seleziona il modulo e aggiungi **Nuova proprietà** in alto a destra oppure fare clic sul modulo.
1. Nella pagina delle proprietà, fai clic su **Elementi dati** e selezionare gli eventi per il modulo.
1. Seleziona tutti gli eventi del modulo e **copia** si trova sulla barra superiore destra.
1. Una volta copiata, **Copia regola** viene visualizzato un pop-up in cui si cerca nella pagina Sites l’ID progetto, per incollare le regole del modulo.
1. Clic **copia** per incollare le regole del modulo nella pagina Sites.

   ![Form-data-elements](/help/forms/assets/form-data-elements.png){width="100%"}

Dopo aver associato le regole di Form e Sites tramite i passaggi sopra indicati, effettua le seguenti operazioni per abilitare Analytics per il modulo adattivo nella pagina Sites:

1. Clic **Flusso di pubblicazione** a sinistra.
1. Clic **Aggiungi libreria** e inserisci il nome che preferisci.
1. In **Ambiente** a destra, seleziona **sviluppo**.
1. Clic **Aggiungi tutte le risorse modificate**.
1. Clic **Salva e genera in sviluppo**.

![pubblicazione su sviluppo](/help/forms/assets/publish-to-dev.png){width="100%"}


<!--

## Best Practices

1.	Verify that Adobe Analytics is enabled on all the forms activated for Adobe Analytics.

1.	Check the Adobe Analytics report periodically to gain insights into user behavior and form performance. For instance, you may set the cadence to 15 days or the period you prefer to choose for report analysis. This enables you to improve the forms enrollment experience.

1.	Enable Analytics for all or most of your forms for tracking and analyzing user interaction with your forms and to gain insights into visitor interactions and engagement.

1. Check your forms performance after you update your form fields or components.

1.	Share Analytics report with your peer groups for review, you can schedule your report for a later time.

-->