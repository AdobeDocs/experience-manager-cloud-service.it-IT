---
title: Come si crea un modulo adattivo?
description: Scopri come creare un modulo adattivo utilizzando [!DNL Experience Manager Forms]. Adaptive Forms sono moduli HTML5 reattivi che semplificano la raccolta e l'elaborazione delle informazioni. Scopri come creare un modulo adattivo basato su un modello di dati modulo e su uno schema XML o JSON.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
source-git-commit: a4fd268cb143c1356de3db9d55b16ccb58b67d4b
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---


# Creare un modulo adattivo (componenti core) {#creating-an-adaptive-form-core-components}

I moduli adattivi consentono di creare moduli coinvolgenti e reattivi, che si rivelano, inoltre, dinamici e adattivi. AEM Forms fornisce una procedura guidata aziendale intuitiva per creare rapidamente Adaptive Forms. La procedura guidata consente di navigare a schede rapide per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati per creare un modulo adattivo.

Prima di iniziare, scopri il tipo di componenti Forms disponibili:

* [Componenti core adattabili di Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it): Si tratta di componenti di acquisizione dati standardizzati. Questi componenti offrono funzionalità di personalizzazione, tempi di sviluppo ridotti e costi di manutenzione inferiori per le esperienze di iscrizione digitale. Uno sviluppatore può personalizzare e personalizzare facilmente questi componenti. Adobe consiglia di utilizzare questi componenti moderni ed estensibili per sviluppare Adaptive Forms.

* [Componenti adattivi di Forms Foundation](creating-adaptive-form.md): Si tratta di componenti di acquisizione dati classici (vecchi). Puoi continuare a utilizzarli per modificare i componenti di base esistenti basati su Modulo adattivo. Se si creano nuovi moduli, Adobe consiglia di utilizzare  [Componenti core adattabili di Forms](creating-adaptive-form-core-components.md) per creare un Forms adattivo.

![Creazione guidata di un modulo adattivo](/help/release-notes/assets/wizard.png)


## Prerequisiti

Per creare un modulo adattivo è necessario quanto segue:

* **Abilitare i componenti core Forms adattivi per il tuo ambiente**: Quando crei un nuovo programma, i componenti core Forms adattivi sono già abilitati per il tuo ambiente. Se disponi di un ambiente as a Cloud Service Forms basato su Archetype 39 o versioni precedenti, [Abilitare i componenti core Forms adattivi per il tuo ambiente](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). Quando abiliti i componenti core per il tuo ambiente, **Forms adattivo (componente core)** il tema modello e canvas viene aggiunto all’ambiente. Se la tua versione SDK AEM precedente alla 2023.02.0, [assicurati di `prerelease` flag abilitato nell’ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#new-features) in quanto i componenti core di Forms adattivi facevano parte della versione pre-release precedente alla versione 2023.02.0.

* **Un modello di modulo adattivo**: Un modello fornisce una struttura di base e definisce l’aspetto (layout e stili) di un modulo adattivo. Dispone di componenti preformattati contenenti determinate proprietà e struttura del contenuto. Offre inoltre le opzioni per definire un tema e un’azione di invio. Il tema definisce l’aspetto e l’aspetto dell’azione di invio definisce l’azione da intraprendere in seguito all’invio di un Modulo adattivo. Ad esempio, l’invio dei dati raccolti a un’origine dati. Il servizio cloud fornisce un modello OOTB denominato vuoto:

   * La `blank` Il modello è incluso in ogni nuovo programma AEM Forms as a Cloud Service.
   * Puoi installare il pacchetto di riferimento, tramite Gestione pacchetti, per aggiungere il `blank` al programma as a Cloud Service di AEM Forms.
   * È inoltre possibile [creare un nuovo modello di Forms adattivo (componenti core)](template-editor.md) da zero.

* **Un tema Modulo adattivo**: Un tema contiene dettagli di stile per i componenti e i pannelli. Gli stili includono proprietà quali colori di sfondo, colori dello stato, trasparenza, allineamento e dimensioni. Quando applichi un tema, lo stile specificato si riflette sui componenti corrispondenti.  La `Canvas` Il modello è incluso in ogni nuovo programma AEM Forms as a Cloud Service.

   <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Autorizzazioni**: Aggiungi gli utenti a [!DNL forms-users] gruppo. I membri del [!DNL forms-users] i gruppi dispongono delle autorizzazioni necessarie per creare un modulo adattivo. Per un elenco dettagliato dei gruppi di utenti specifici dei moduli, vedere [Gruppi e autorizzazioni](forms-groups-privileges-tasks.md).


## Creare un modulo adattivo (componenti core) {#create-an-adaptive-form-core-components}

1. Accedi al tuo [!DNL Experience Manager Forms] Istanza di authoring. Può essere un’istanza Cloud o un’istanza di sviluppo locale.

1. Immetti le credenziali nella pagina di accesso di Experience Manager. Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra tocca **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

1. Tocca **[!UICONTROL Crea]**  > **[!UICONTROL Forms adattivo]**. Viene visualizzata la procedura guidata. Nella scheda Origine, seleziona un modello:

   ![Modello dei componenti core](/help/forms/assets/core-components-template.png)

   Quando selezioni un modello, un tema e un’azione di invio specificati nel modello vengono selezionati automaticamente e la **[!UICONTROL Crea]** è abilitato. Puoi andare al **[!UICONTROL Stile]** o **[!UICONTROL Invio]** schede per selezionare un tema diverso o inviare un&#39;azione. Se il modello selezionato non specifica un tema, il pulsante crea rimane disattivato. Puoi andare al **[!UICONTROL Stili]** per selezionare manualmente un tema.

   >[!NOTE]
   >
   >
   > In caso contrario, **Forms adattivo (componente core)** modello nell’ambiente, [Abilitare i componenti core Forms adattivi per il tuo ambiente](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). Quando abiliti i componenti core per il tuo ambiente, **Forms adattivo (componente core)** viene aggiunto all’ambiente.

1. In **[!UICONTROL Stile]** seleziona un tema:

   * Quando il modello selezionato specifica un tema, il tema viene selezionato automaticamente nella procedura guidata. Puoi anche scegliere un tema diverso dalla scheda Stile .

   * Se il modello selezionato non specifica un tema, è possibile utilizzare la scheda Stile per scegliere un tema. La **[!UICONTROL Crea]** viene attivato solo dopo aver selezionato un tema.

1. (Facoltativo) Nella scheda Dati, seleziona un modello dati:

   * **Modello dati modulo**: A [Modello dati modulo](data-integration.md) consente di integrare entità e servizi da origini dati diverse in un modulo adattivo. Scegliere Modello dati modulo se il modulo adattivo creato prevede il recupero e la scrittura di dati da e verso più origini dati.

   * **Schema JSON**: [Schema JSON](adaptive-form-json-schema-form-model.md) Il nostro modulo adattivo basato su componenti core consente un’integrazione diretta con il sistema back-end della tua organizzazione grazie alla possibilità di associare uno schema JSON, che rappresenta la struttura dei dati prodotti o utilizzati. Questa associazione consente agli autori di aggiungere in modo dinamico contenuti al modulo adattivo utilizzando gli elementi dello schema. Gli elementi dello schema sono facilmente accessibili nella scheda Oggetti modello dati del browser Contenuto durante il processo di creazione e tutti i campi vengono aggiunti automaticamente a qualsiasi modulo adattivo appena creato.

   Per impostazione predefinita, tutti i campi dello schema JSON associato vengono selezionati e convertiti automaticamente nei corrispondenti componenti Modulo adattivo, semplificando il processo di creazione. La procedura guidata offre la comodità aggiuntiva di consentire di scegliere in modo selettivo quali campi includere nel modulo adattivo tramite le caselle di controllo.

1. In **[!UICONTROL Invio]** seleziona un’azione di invio:

   * Quando selezioni un modello, l’azione di invio specificata nel modello viene selezionata automaticamente. È possibile selezionare un’altra azione di invio dalla scheda Invio. La **[!UICONTROL Invio]** visualizza tutte le azioni di invio disponibili.

   * Se il modello selezionato non specifica un’azione di invio, è possibile utilizzare la **[!UICONTROL Invio]** scheda per selezionare un’azione di invio

1. (Facoltativo) In **[!UICONTROL Consegna]** È possibile specificare una data di pubblicazione o di annullamento della pubblicazione per un modulo adattivo.

1. Tocca **[!UICONTROL Crea]**. Viene visualizzata una finestra di dialogo per specificare il titolo, il nome e la posizione in cui salvare il modulo adattivo:

   * **[!UICONTROL Titolo]** Specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nel [!DNL Experience Manager Forms] interfaccia utente.
   * **[!UICONTROL Nome:]** Specifica il nome del modulo. Nel repository viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo nome viene generato automaticamente. È possibile modificare il valore suggerito. Il campo name può includere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti con un trattino.
   * **[!UICONTROL Percorso:]** Specifica il percorso in cui salvare il modulo adattivo. Puoi salvare il modulo adattivo direttamente in `/content/dam/formsanddocuments` o creare una cartella come `/content/dam/formsanddocuments/adaptiveforms` per salvare un modulo adattivo. Assicurati di creare la cartella prima di utilizzarla nel percorso. La **[!UICONTROL Percorso]** non crea automaticamente una cartella.

1. Tocca **[!UICONTROL Crea]**. Viene creato un modulo adattivo che viene aperto nell’editor Forms adattivo. L’editor visualizza il contenuto disponibile nel modello.  In base al tipo di Modulo adattivo, gli elementi modulo presenti nel <!--XFA form template, XML schema or --> Lo schema JSON o il modello dati del modulo sono visualizzati nella **[!UICONTROL Oggetti del modello dati]** della scheda **[!UICONTROL Browser dei contenuti]** nella barra laterale. Puoi anche trascinare questi elementi per creare il modulo adattivo.

Ora è possibile trascinare i componenti core di Forms adattivi nel contenitore Forms adattivo per progettare e creare il modulo.

## Componenti core adattabili di Forms disponibili

I componenti core Forms adattivi sono componenti standard per l’acquisizione dei dati. Questi componenti offrono funzionalità di personalizzazione, consentono di ridurre i tempi di sviluppo e i costi di manutenzione per le esperienze di iscrizione digitale. [Documentazione sui componenti core adattabili di Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) presenta un elenco dettagliato dei componenti disponibili e informazioni dettagliate sulle funzionalità di ciascun componente. È inoltre possibile visitare [https://aemcomponents.dev/](https://aemcomponents.dev/) per visualizzare i componenti core disponibili in azione.

## Modificare le proprietà del modello di modulo di un modulo adattivo {#edit-form-model}

1. Seleziona il modulo adattivo e tocca ![Informazioni sulla pagina](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Apri proprietà]**. Viene visualizzata la pagina Proprietà modulo .

1. Vai a **[!UICONTROL Modello Modulo]** e scegliere un modello di modulo. Se il modulo adattivo non dispone di un modello di modulo, è possibile scegliere uno schema JSON o un modello di dati del modulo. Se invece il modulo adattivo è già basato su un modello di modulo, è possibile passare a un altro modello di modulo dello stesso tipo. Ad esempio, se il modulo utilizza uno schema JSON, è possibile passare facilmente a un altro schema JSON; analogamente, se il modulo utilizza un modello dati modulo, è possibile passare a un altro modello dati modulo.

1. Tocca **[!UICONTROL Salva]** per salvare le proprietà.
