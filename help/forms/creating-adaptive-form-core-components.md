---
title: Come si crea un modulo adattivo basato su componenti core?
description: Scopri come creare un modulo adattivo utilizzando [!DNL Experience Manager Forms]. I Forms adattivi sono moduli HTML5 reattivi che semplificano la raccolta e l’elaborazione delle informazioni. Approfondisci le modalità di creazione di un modulo adattivo basato su un modello dati modulo (FDM) e su uno schema XML o JSON.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '2281'
ht-degree: 47%

---

# Creare un modulo adattivo {#creating-an-adaptive-form-core-components}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-an-adaptive-form-core-components.html) |
| AEM as a Cloud Service | Questo articolo |


I moduli adattivi consentono di creare moduli coinvolgenti e reattivi, che si rivelano, inoltre, dinamici e adattivi. AEM Forms fornisce una procedura guidata intuitiva che consente agli utenti aziendali di creare rapidamente moduli adattivi. La procedura guidata fornisce una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati per creare un modulo adattivo.

Prima di iniziare, scopri i tipi di componenti dei moduli disponibili:

* [Componenti core dei moduli adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it): si tratta di componenti di acquisizione dati standardizzati. Questi componenti forniscono funzionalità di personalizzazione e riducono i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale. Uno sviluppatore può facilmente personalizzare e assegnare uno stile a questi componenti. L’Adobe consiglia di utilizzare questi componenti moderni ed estensibili per sviluppare Forms adattivo.

* [Componenti di base dei moduli adattivi](creating-adaptive-form.md): si tratta dei classici (precedenti) componenti di acquisizione dati. Puoi continuare a utilizzarli per modificare i componenti di base esistenti basati su modulo adattivo. Se stai creando nuovi moduli, l’Adobe consiglia di utilizzare  [Componenti core Forms adattivi](creating-adaptive-form-core-components.md) per creare un Forms adattivo.

![Creazione guidata di un modulo adattivo](/help/release-notes/assets/wizard.png)


## Prerequisiti

Per creare un modulo adattivo è necessario quanto segue:

* **Abilitare i componenti core Forms adattivi per il tuo ambiente**: quando crei un programma, i Componenti core adattivi di Forms sono già abilitati per il tuo ambiente. Se disponi di un ambiente Forms as a Cloud Service basato sull’Archetipo 39 o versioni precedenti, consulta [Abilitare i componenti core dei moduli adattivi per il tuo ambiente](enable-adaptive-forms-core-components.md). Quando abiliti i componenti core per il tuo ambiente, vengono aggiunti il modello e l&#39;area di lavoro del **componente core moduli adattivi**. Se la tua versione dell’SDK di AEM è precedente alla 2023.02.0, [assicurati di aver abilitato il flag `prerelease` nel tuo ambiente ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features), poiché i componenti core dei moduli adattivi facevano parte della versione prerelease precedente alla versione 2023.02.0.

* **Un modello di modulo adattivo**: un modello fornisce una struttura di base e definisce l’aspetto (layout e stili) di un modulo adattivo. Include componenti preformattati contenenti determinate proprietà e struttura del contenuto. Fornisce inoltre le opzioni per definire un tema e un’azione di invio. Il tema definisce l’aspetto, mentre l’azione di invio definisce l’azione da intraprendere al momento dell’invio di un modulo adattivo. Ad esempio, l’invio dei dati raccolti a un’origine dati. Il Cloud Service fornisce un modello OOTB, denominato vuoto:

   * Il modello `blank` è incluso in ogni nuovo programma AEM Forms as a Cloud Service.
   * È possibile installare il pacchetto di riferimento tramite Gestione pacchetti per aggiungere il `blank` modello al programma AEM Forms as a Cloud Service.
   * È inoltre possibile [creare un modello di Forms adattivo (componenti core)](/help/forms/template-editor-core-components.md) da zero.
   * Puoi anche distribuire [modelli di esempio](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) nell&#39;ambiente. che consentono di iniziare a creare rapidamente i moduli.

* **Un tema per moduli adattivi**: un tema contiene dettagli sullo stile dei componenti e dei pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l’allineamento e le dimensioni. Quando applichi un tema, lo stile specificato si riflette sui componenti corrispondenti.  Il `Canvas` Questo modello è incluso in ogni nuovo programma as a Cloud Service di AEM Forms. Puoi anche distribuire [temi di esempio](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) nell&#39;ambiente. In questo modo è possibile iniziare a definire lo stile dei moduli e fornire una struttura di base per creare o personalizzare un tema in base alle proprie esigenze aziendali.

  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create an Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Autorizzazioni**: aggiungi gli utenti a un gruppo [!DNL forms-users]. I membri del gruppo [!DNL forms-users] dispongono delle autorizzazioni per creare un modulo adattivo. Per un elenco dettagliato dei gruppi di utenti specifici per moduli, consulta [Gruppi e autorizzazioni](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Creare un modulo adattivo  {#create-an-adaptive-form-core-components}

1. Accedi all’istanza di authoring [!DNL Experience Manager Forms]. Può essere un’istanza Cloud o un’istanza di sviluppo locale.

1. Inserisci le credenziali nella pagina di accesso di Experience Manager. Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

1. Seleziona **[!UICONTROL Crea]**  > **[!UICONTROL Forms adattivo]**. Viene aperta la procedura guidata. Nella scheda Sorgente, seleziona un modello:

   ![Modello componenti core](/help/forms/assets/core-components-template.png)

   Quando selezioni un modello, vengono selezionati automaticamente un tema e un’azione di invio specificati nel modello, mentre viene abilitato il pulsante **[!UICONTROL Crea]**. È possibile passare alle schede **[!UICONTROL Stile]** o **[!UICONTROL Invio]** per selezionare un tema o un’azione di invio diversi. Se il modello selezionato non specifica un tema, il pulsante Crea rimane disabilitato. È possibile passare alla scheda **[!UICONTROL Stili]** per selezionare manualmente un tema.

   >[!NOTE]
   >
   >
   > Se non disponi del modello **Moduli adattivi (componente core)** nell’ambiente, [abilita la funzione Componenti core dei moduli adattivi per il tuo ambiente](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). Quando abiliti i componenti core per il tuo ambiente, viene aggiunto il modello **Moduli adattivi (componente core)**.

1. Nella scheda **[!UICONTROL Stile]**, seleziona un tema:

   * Quando il modello selezionato specifica un tema, lo stesso viene selezionato automaticamente nella procedura guidata. È possibile inoltre scegliere un tema diverso dalla scheda Stile.

   * Se il modello selezionato non specifica un tema, è possibile utilizzare la scheda Stile per sceglierne uno. Il pulsante **[!UICONTROL Crea]** viene abilitato solo dopo la selezione di un tema.

1. (Facoltativo) Nella scheda Dati, seleziona un modello dati:

   * **Modello dati modulo (FDM)**: A [Modello dati modulo](data-integration.md) consente di integrare entità e servizi da diverse origini dati a un modulo adattivo. Scegli Modello dati modulo (FDM) se il modulo adattivo che stai creando richiede il recupero e la scrittura di dati da e verso più origini dati.

   * **Schema JSON**: lo [Schema JSON](adaptive-form-json-schema-form-model.md) è nostro modulo adattivo basato su componenti core che consente l’integrazione perfetta con il sistema back-end della tua organizzazione, grazie alla possibilità di associare uno schema JSON, che rappresenta la struttura dei dati prodotti o utilizzati. Questa associazione consente agli autori di aggiungere contenuti al modulo adattivo in modo dinamico, utilizzando gli elementi dello schema. Gli elementi dello schema sono facilmente accessibili nella scheda Oggetti modello dati del browser Contenuto durante il processo di authoring e tutti i campi vengono aggiunti automaticamente a qualsiasi modulo adattivo creato.

   Per impostazione predefinita, tutti i campi dello schema JSON associato vengono selezionati e convertiti automaticamente nei componenti corrispondenti del modulo adattivo, semplificando il processo di authoring. La procedura guidata offre l’ulteriore comodità di consentire la scelta selettiva dei campi da includere nel modulo adattivo tramite l’utilizzo di caselle di controllo.

1. Nella scheda **[!UICONTROL Invio]**, seleziona un’azione di invio:

   * Quando selezioni un modello, l’azione di invio specificata in quel modello viene selezionata automaticamente. Dalla scheda Invio puoi selezionare un’azione di invio diversa. La scheda **[!UICONTROL Invio]** mostra tutte le azioni di invio disponibili.

   * Se nel modello selezionato non è specificata un’azione di invio, è possibile utilizzare la scheda **[!UICONTROL Invio]** per selezionarne una.

1. (Facoltativo) Nella scheda **[!UICONTROL Consegna]**, è possibile specificare una data di pubblicazione o di annullamento della pubblicazione per un modulo adattivo.

1. Seleziona **[!UICONTROL Crea]**. Viene visualizzata una finestra di dialogo che specifica il titolo, il nome e la posizione in cui salvare il modulo adattivo:

   * **[!UICONTROL Titolo]**: specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nell’interfaccia utente di [!DNL Experience Manager Forms].
   * **[!UICONTROL Nome:]** specifica il nome del modulo. Nell’archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo nome viene generato automaticamente. Puoi modificare il valore suggerito. Il campo nome può contenere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti da un trattino.
   * **[!UICONTROL Percorso:]** specifica la posizione in cui salvare il modulo adattivo. Puoi salvare il modulo adattivo direttamente all’indirizzo `/content/dam/formsanddocuments` o creare una cartella di salvataggio come `/content/dam/formsanddocuments/adaptiveforms`. Assicurati di creare la cartella prima di utilizzarla nel percorso. Il campo **[!UICONTROL Percorso]** non crea cartelle automaticamente.

1. Seleziona **[!UICONTROL Crea]**. Viene creato un modulo adattivo che viene aperto nell’editor di moduli adattivi. L’editor mostra i contenuti disponibili nel modello.  In base al tipo di modulo adattivo, gli elementi del modulo presenti nel <!--XFA form template, XML schema or --> Lo schema JSON o il modello dati del modulo (FDM) vengono visualizzati nel **[!UICONTROL Oggetti modello dati]** scheda di **[!UICONTROL Browser contenuti]** nella barra laterale. Puoi anche trascinare questi elementi per creare il modulo adattivo.

Ora puoi trascinare e rilasciare la [Componenti core Forms adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) al contenitore Forms adattivo per progettare e creare il modulo. Puoi anche visitare [https://aemcomponents.dev/](https://aemcomponents.dev/) per visualizzare i componenti core disponibili in azione.

## Configurare l’azione di invio per un modulo adattivo {#configure-submit-action-for-form}

Un’azione di invio consente di scegliere la destinazione dei dati acquisiti tramite un modulo adattivo. Viene attivato quando un utente fa clic sul pulsante Invia in un modulo adattivo. I moduli adattivi includono alcune azioni di invio pronte all’uso. Puoi anche estendere un’azione di invio predefinita per creare un’azione di invio personalizzata. Per configurare un&#39;azione di invio per il modulo:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).

1. Fai clic su  **[!UICONTROL Invio]** scheda.

   ![Fai clic sull’icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare un’azione di invio](/help/forms/assets/adaptive-forms-submit-message.png)

1. Seleziona e configura un **[!UICONTROL Azione di invio]**, in base alle tue esigenze. Per informazioni dettagliate sulle azioni di invio, vedere [Azione di invio modulo adattivo](/help/forms/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Reindirizza l’utente a una pagina o mostra un messaggio di ringraziamento all’invio del modulo

All&#39;invio di un modulo è possibile reindirizzare l&#39;utente a un&#39;altra pagina Web o a un messaggio. Per reindirizzare l’utente o configurare il messaggio di ringraziamento:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri **[!UICONTROL Invio]** scheda.

   ![Fai clic sull’icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo per configurare una pagina di reindirizzamento o un messaggio di ringraziamento](/help/forms/assets/adaptive-forms-redirect-message.png)

   * Per configurare un URL di reindirizzamento, per l’opzione Invia seleziona la **[!UICONTROL Reindirizza a URL]** e sfoglia e seleziona una pagina AEM Sites oppure specifica l’URL di una pagina esterna.

   * Per configurare un messaggio personalizzato o di ringraziamento, per all’opzione Invia, seleziona la **[!UICONTROL Mostra messaggio]** e inserisci un messaggio nella sezione **[!UICONTROL Contenuto del messaggio]** casella. Si tratta di una casella di testo RTF, è possibile utilizzare l&#39;opzione a schermo intero per visualizzare tutti gli elementi RTF disponibili.

## Configurare uno schema o un modello di dati del modulo (FDM) per un modulo adattivo{#configure-schema-or-data-model-for-form}

È possibile utilizzare il modello dati modulo (FDM) per collegare un modulo a un&#39;origine dati per inviare e ricevere dati in base alle azioni dell&#39;utente. È possibile anche collegare un modulo a uno schema JSON per ricevere i dati inviati in un formato predefinito. In base al requisito, connetti il modulo a uno schema JSON o a un modello dati modulo (FDM):

* [Creare uno schema JSON e caricarlo nell’ambiente](/help/forms/adaptive-form-json-schema-form-model.md)
* [Creare un modello dati modulo (FDM)](/help/forms/create-form-data-models.md)

### Configurare uno schema JSON o un modello dati modulo (FDM) per il modulo

Per configurare uno schema JSON o un modello dati modulo (FDM) per il modulo:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri **[!UICONTROL Modello dati]** scheda.

   ![Fai clic sull’icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo per configurare uno schema JSON o un modello di dati del modulo (FDM)](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Seleziona e configura uno schema JSON o un modello dati modulo (FDM), in base ai requisiti:

   * Quando selezioni il **[!UICONTROL Modello modulo]** , utilizza **[!UICONTROL Seleziona modello dati modulo]** per selezionare un modello di dati modulo (FDM) preconfigurato.
   * Quando selezioni il **[!UICONTROL Schema]** , utilizza **[!UICONTROL Schema]** per selezionare uno schema JSON per il modulo.

1. Clic **[!UICONTROL Fine]**.

## Configurare un servizio di precompilazione  {#configure-prefill-service-for-form}

Puoi utilizzare il servizio di precompilazione per compilare automaticamente i campi di un modulo adattivo utilizzando dati esistenti. Quando un utente apre un modulo, i valori di tali campi vengono precompilati. Operazioni disponibili:

* [Creare un servizio di precompilazione personalizzato](/help/forms/prepopulate-adaptive-form-fields.md)
* [Utilizza il servizio di precompilazione del modello dati del modulo](#fdm-prefill-service)

### Utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo adattivo {#fdm-prefill-service}

È possibile utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo adattivo utilizzando un modello dati modulo o un servizio di precompilazione personalizzato. Il servizio di precompilazione del modello dati del modulo utilizza [Ottieni il servizio del modello di dati del modulo configurato](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) per recuperare i dati. Per utilizzare il servizio di precompilazione del modello dati modulo per un modulo adattivo:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fai clic sulle proprietà Contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
   ![Fai clic sull’icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo per configurare una pagina di reindirizzamento o un messaggio di ringraziamento](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. Seleziona un modello dati modulo (FDM). Apri **[!UICONTROL Base]** scheda. Nel servizio di preriempimento, seleziona **[!UICONTROL Servizio preriempimento modello dati modulo]**.
1. Clic **[!UICONTROL Fine]**. Il modulo adattivo è ora configurato per l’utilizzo della precompilazione del modello dati del modulo. Ora è possibile utilizzare [editor di regole](rule-editor.md) per creare regole per precompilare i campi del modulo.

## Modificare le proprietà di un modello di modulo adattivo {#edit-form-model}

1. Seleziona il modulo adattivo e seleziona ![Informazioni pagina](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Apri proprietà]**. Viene visualizzata la pagina Proprietà modulo.

1. Vai alla scheda **[!UICONTROL Modello modulo]** e scegli un modello di modulo. Se il modulo adattivo non dispone di un modello di modulo, puoi scegliere uno schema JSON o un modello di dati del modulo (FDM). Se invece il modulo adattivo si basa già su un modello di modulo, puoi passare a un altro modello dello stesso tipo. Ad esempio, se il modulo utilizza uno schema JSON, puoi passare facilmente a un altro schema JSON e, analogamente, se il modulo utilizza un modello di dati del modulo (FDM), puoi passare a un altro modello di dati del modulo (FDM).

1. Seleziona **[!UICONTROL Salva]** per salvare le proprietà.


<!--

## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Add dynamic behavior to forms using the rule editor](rule-editor.md)
* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)

-->

## Consulta anche {#see-also}

{{see-also}}
* [Aggiungere un comportamento dinamico ai moduli tramite l’editor di regole](rule-editor.md)
* [Impostare il layout dei moduli per dimensioni di schermo e tipi di dispositivi diversi](/help/sites-cloud/authoring/page-editor/responsive-layout.md)

