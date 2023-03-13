---
title: Creare un modulo adattivo
description: Scopri come creare un modulo adattivo utilizzando [!DNL Experience Manager Forms]. I Forms adattivi sono moduli HTML5 reattivi che semplificano la raccolta e l’elaborazione delle informazioni. Approfondisci le modalità di creazione di un modulo adattivo basato su un modello di dati modulo e uno schema XML o JSON.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
source-git-commit: ae208e9ac35c3c464d9beeaa3bc2bddc0ecf52bb
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 1%

---


# Creare un modulo adattivo (componenti core) {#creating-an-adaptive-form-core-components}

I moduli adattivi consentono di creare moduli coinvolgenti e reattivi, che si rivelano, inoltre, dinamici e adattivi. AEM Forms fornisce una procedura guidata intuitiva per la creazione rapida di Adaptive Forms. La procedura guidata fornisce una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati per la creazione di un modulo adattivo.

Prima di iniziare, scopri i tipi di componenti Forms disponibili:

* [Componenti core Forms adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en): si tratta di componenti di acquisizione dati standardizzati. Questi componenti forniscono funzionalità di personalizzazione, riducono i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale. Uno sviluppatore può personalizzare e assegnare uno stile a questi componenti. L’Adobe consiglia di sfruttare questi componenti moderni ed estensibili per sviluppare Forms adattivo.

* [Componenti adattivi di Forms Foundation](creating-adaptive-form.md): si tratta dei classici (vecchi) componenti di acquisizione dati. Puoi continuare a utilizzarli per modificare i componenti di base esistenti basati su modulo adattivo. Se stai creando nuovi moduli, l’Adobe consiglia di utilizzare  [Componenti core Forms adattivi](creating-adaptive-form-core-components.md) per creare un Forms adattivo.

![Creazione guidata di un modulo adattivo](/help/release-notes/assets/wizard.png)


## Prerequisiti

Per creare un modulo adattivo è necessario quanto segue:

* **Abilitare i componenti core Forms adattivi per il tuo ambiente**: quando crei un nuovo programma, i Componenti core adattivi di Forms sono già abilitati per il tuo ambiente. Se disponi di un ambiente Forms as a Cloud Service basato su Archetipo 39 o versioni precedenti, [Abilitare i componenti core Forms adattivi per il tuo ambiente](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). Quando si abilitano i Componenti core per l’ambiente, viene **Forms adattivo (componente core)** Il tema del modello e dell’area di lavoro viene aggiunto all’ambiente.

* **Un modello di modulo adattivo**: un modello fornisce una struttura di base e definisce l’aspetto (layout e stili) di un modulo adattivo. Include componenti preformattati contenenti determinate proprietà e struttura del contenuto. Fornisce inoltre le opzioni per definire un tema e un’azione di invio. Il tema definisce l’azione &quot;look and feel&quot; e &quot;submit&quot; definisce l’azione da intraprendere al momento dell’invio di un modulo adattivo. Ad esempio, l’invio dei dati raccolti a un’origine dati. Il servizio cloud fornisce un modello OOTB, denominato vuoto:

   * Il `blank` Questo modello è incluso in ogni nuovo programma as a Cloud Service di AEM Forms.
   * È possibile installare il pacchetto di riferimento tramite Gestione pacchetti per aggiungere `blank` al programma AEM Forms as a Cloud Service.
   * È inoltre possibile [creare un nuovo modello di Forms adattivo (Componenti core)](template-editor.md) da zero.

* **Un tema per moduli adattivi**: un tema contiene dettagli sullo stile dei componenti e dei pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l&#39;allineamento e le dimensioni. Quando applicate un tema, lo stile specificato viene riflesso sui componenti corrispondenti.  Il `Canvas` Questo modello è incluso in ogni nuovo programma as a Cloud Service di AEM Forms.

   <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Autorizzazioni**: aggiungi gli utenti a [!DNL forms-users] gruppo. I membri della [!DNL forms-users] dispongono delle autorizzazioni per creare un modulo adattivo. Per un elenco dettagliato dei gruppi di utenti specifici per i moduli, consulta [Gruppi e autorizzazioni](forms-groups-privileges-tasks.md).


## Creare un modulo adattivo (componenti core) {#create-an-adaptive-form-core-components}

1. Accedi al tuo [!DNL Experience Manager Forms] Istanza Autore. Può essere un’istanza Cloud o un’istanza di sviluppo locale.

1. Immetti le credenziali nella pagina di accesso di Experience Manager. Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra tocca **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

1. Tocca **[!UICONTROL Crea]**  > **[!UICONTROL Forms adattivo]**. Viene visualizzata la procedura guidata. Nella scheda Origine, seleziona un modello:

   ![Modello componenti core](/help/forms/assets/core-components-template.png)

   Quando selezioni un modello, viene selezionato automaticamente un tema e un’azione di invio specificati nel modello, e il **[!UICONTROL Crea]** è attivato. È possibile passare al **[!UICONTROL Stile]** o **[!UICONTROL Invio]** per selezionare un tema diverso o un’azione di invio diversa. Se il modello selezionato non specifica un tema, il pulsante Crea rimane disattivato. È possibile passare al **[!UICONTROL Stili]** per selezionare manualmente un tema.

   >[!NOTE]
   >
   >
   > In caso contrario, **Forms adattivo (componente core)** modello nell&#39;ambiente, [Abilitare i componenti core Forms adattivi per il tuo ambiente](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). Quando si abilitano i Componenti core per l’ambiente, viene **Forms adattivo (componente core)** viene aggiunto al tuo ambiente.

1. In **[!UICONTROL Stile]** , selezionare un tema:

   * Quando il modello selezionato specifica un tema, il tema viene selezionato automaticamente nella procedura guidata. È inoltre possibile scegliere un tema diverso dalla scheda Stile.

   * Se nel modello selezionato non è specificato un tema, è possibile utilizzare la scheda Stile per scegliere un tema. Il **[!UICONTROL Crea]** viene attivato solo dopo la selezione di un tema.

1. (Facoltativo) Nella scheda Dati, seleziona un modello dati:

   * **Modello dati modulo**: A [Modello dati modulo](data-integration.md) consente di integrare entità e servizi da diverse origini dati a un modulo adattivo. Scegli modello dati modulo se il modulo adattivo che stai creando richiede il recupero e la scrittura di dati da e verso più origini dati.

   * **Schema JSON**: [Schema JSON](adaptive-form-json-schema-form-model.md) Il nostro modulo adattivo basato su componenti core consente l’integrazione perfetta con il sistema back-end della tua organizzazione grazie alla possibilità di associare uno schema JSON, che rappresenta la struttura dei dati prodotti o utilizzati. Questa associazione consente agli autori di aggiungere contenuti al modulo adattivo in modo dinamico utilizzando gli elementi dello schema. Gli elementi dello schema sono facilmente accessibili nella scheda Oggetti modello dati del browser Contenuto durante il processo di authoring e tutti i campi vengono aggiunti automaticamente a qualsiasi nuovo modulo adattivo creato.

   Per impostazione predefinita, tutti i campi dello schema JSON associato vengono selezionati e convertiti automaticamente nei corrispondenti componenti del modulo adattivo, semplificando il processo di authoring. La procedura guidata offre l’ulteriore comodità di consentire la scelta selettiva dei campi da includere nel modulo adattivo tramite l’utilizzo di caselle di controllo.

1. In **[!UICONTROL Invio]** , seleziona un’azione di invio:

   * Quando selezioni un modello, l’azione di invio specificata nel modello viene selezionata automaticamente. Puoi selezionare un’azione di invio diversa dalla scheda Invio. Il **[!UICONTROL Invio]** visualizza tutte le azioni di invio disponibili.

   * Se nel modello selezionato non è specificata un&#39;azione di invio, è possibile utilizzare **[!UICONTROL Invio]** per selezionare un’azione di invio

1. (Facoltativo) In **[!UICONTROL Consegna]** , è possibile specificare una data di pubblicazione o di annullamento della pubblicazione per un modulo adattivo.

1. Tocca **[!UICONTROL Crea]**. Viene visualizzata una finestra di dialogo che specifica il titolo, il nome e la posizione in cui salvare il modulo adattivo:

   * **[!UICONTROL Titolo]** Specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nel [!DNL Experience Manager Forms] dell&#39;utente.
   * **[!UICONTROL Nome:]** Specifica il nome del modulo. Nell&#39;archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo del nome viene generato automaticamente. Puoi modificare il valore suggerito. Il campo del nome può contenere solo caratteri alfanumerici, trattini e trattini bassi. Tutti gli input non validi vengono sostituiti da un trattino.
   * **[!UICONTROL Percorso:]** Specifica la posizione in cui deve essere salvato il modulo adattivo. Puoi salvare il modulo adattivo direttamente all’indirizzo `/content/dam/formsanddocuments` o crea una cartella come `/content/dam/formsanddocuments/adaptiveforms` per salvare un modulo adattivo. Assicurati di creare la cartella prima di utilizzarla nel percorso. Il **[!UICONTROL Percorso]** non crea automaticamente una cartella.

1. Tocca **[!UICONTROL Crea]**. Viene creato un modulo adattivo che viene aperto nell’editor di Forms adattivo. L’editor visualizza i contenuti disponibili nel modello.  In base al tipo di modulo adattivo, gli elementi del modulo presenti nel <!--XFA form template, XML schema or --> Lo schema JSON o il modello dati del modulo vengono visualizzati nel **[!UICONTROL Oggetti modello dati]** scheda di **[!UICONTROL Browser contenuti]** nella barra laterale. Puoi anche trascinare questi elementi per creare il modulo adattivo.

Ora puoi trascinare e rilasciare i componenti core Adaptive Forms nel contenitore Forms adattivo per progettare e creare il modulo.

## Componenti core Forms adattivi disponibili

I componenti core Forms adattivi sono componenti di acquisizione dati standardizzati. Questi componenti forniscono funzionalità di personalizzazione, aiutano a ridurre i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale. [Documentazione dei Componenti core Forms adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en) dispone di un elenco dettagliato dei componenti disponibili con informazioni dettagliate sulle funzionalità di ciascun componente. Puoi anche visitare [https://aemcomponents.dev/](https://aemcomponents.dev/) per visualizzare i componenti core disponibili in azione.

## Modificare le proprietà di un modello di modulo adattivo {#edit-form-model}

1. Seleziona il modulo adattivo e tocca ![Informazioni pagina](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Apri proprietà]**. Viene visualizzata la pagina Proprietà modulo.

1. Vai a **[!UICONTROL Modello modulo]** e scegliere un modello di modulo. Se il modulo adattivo non dispone di un modello di modulo, puoi scegliere uno schema JSON o un modello di dati del modulo. Se invece il modulo adattivo è già basato su un modello di modulo, è possibile passare a un altro modello dello stesso tipo. Ad esempio, se il modulo utilizza uno schema JSON, puoi passare facilmente a un altro schema JSON e, analogamente, se il modulo utilizza un modello dati del modulo, puoi passare a un altro modello dati del modulo.

1. Tocca **[!UICONTROL Salva]** per salvare le proprietà.
