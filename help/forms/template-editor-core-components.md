---
title: Come si crea un modello di modulo adattivo basato su un componente core?
description: Crea modelli di moduli adattivi basati sul componente core per definire la struttura di base e il contenuto iniziale tramite l’Editor modelli.
Keywords: create adaptive form template, create adaptive form template based on core components, Use template to create adpative form.
exl-id: c1c050d3-953e-4e56-a96b-d84f2ec05e5e
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 1%

---

# Creare un modello di modulo adattivo basato su componenti core {#adaptive-form-templates}

Quando si crea un modulo, si aggiungono campi e componenti per definire la struttura del modulo, il contenuto e le azioni nell’editor. È possibile aggiungere campi e componenti in `guideRootPanel` del contenitore di moduli. Con Editor modelli è possibile creare un modello contenente la struttura di base e il contenuto iniziale che gli autori possono utilizzare per creare i moduli.

Ad esempio, si desidera che tutti gli autori di moduli dispongano di determinate caselle di testo, pulsanti di spostamento e un pulsante di invio in un modulo di iscrizione. È possibile creare un modello con i componenti che gli autori possono utilizzare per creare un modulo coerente con altri moduli di iscrizione. Quando gli autori utilizzano il modello per creare un modulo adattivo, il nuovo modulo eredita la struttura e i componenti specificati nel modello. Editor modelli consente di:

* Aggiungete i componenti intestazione e piè di pagina di un modulo nel livello struttura.
* Fornire il contenuto iniziale del modulo.
* Specifica un tema, Invia azioni.

<!--
You can download and install [!DNL AEM Forms] reference content package from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal to import reference themes and templates to your environment.
-->

## Prerequisito

**Abilitare i componenti core Forms adattivi per il tuo ambiente**: quando crei un programma, i Componenti core adattivi di Forms sono già abilitati per il tuo ambiente. Se disponi di un ambiente as a Cloud Service al modulo basato su [AEM Archetipo 39 o precedente](https://github.com/adobe/aem-project-archetype), [Abilitare i componenti core Forms adattivi per il tuo ambiente](enable-adaptive-forms-core-components.md).

>[!NOTE]
>
> Quando si distribuisce l’ambiente as a Cloud Service Forms basato su Archetipo 45, il **Forms adattivo (componente core)** I modelli e i temi basati sui componenti core vengono aggiunti al tuo ambiente.

## Utilizzo del modello {#working-with-templates}

Per accedere all’editor modelli dal menu Strumenti, vai a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]**. In questo caso, i modelli sono organizzati in cartelle abilitate per i modelli modificabili.

>[!NOTE]
>
> Puoi trovare i modelli modificabili basati su componenti core nelle cartelle specifiche dei componenti core.

In Experience Manager viene fornita una cartella globale per organizzare i modelli. Tuttavia, non è attivato per impostazione predefinita. Puoi richiedere all’amministratore di abilitare la cartella globale o di creare una cartella per i modelli. Per ulteriori informazioni su come creare cartelle, consulta [Cartelle modelli](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors).

## Creazione di un modello {#create-template}

Dopo aver creato una cartella, aprila ed esegui i seguenti passaggi per creare un modello:

1. Tocca **[!UICONTROL Crea]** all’interno della cartella creata.
1. In **[!UICONTROL Scegli un tipo di modello]** sezione, seleziona **[!UICONTROL Modello per modulo adattivo (componente core)]** e tocca **[!UICONTROL Successivo]**.

1. In **[!UICONTROL Dettagli Modello]** , fornisci un **Titolo modello** e tocca **[!UICONTROL Crea]**.
Puoi anche fornire una descrizione.

1. Tocca **[!UICONTROL Fine]** per tornare alla console, oppure tocca **[!UICONTROL Apri]** per aprire il modello nell’editor.

## Interfaccia utente dell’editor modelli {#template-editor-ui}

Quando apri un modello per la modifica, puoi vedere i seguenti componenti dell’editor AEM:

* **Barra degli strumenti Pagina**
Contiene le seguenti opzioni:

   * **Attiva/Disattiva pannello laterale**: consente di mostrare o nascondere la barra laterale.
   * **Informazioni pagina**: consente di specificare informazioni quali l’ora di pubblicazione/annullamento della pubblicazione, le miniature, le librerie lato client, i criteri di pagina e la libreria lato client della progettazione della pagina.
     <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **Selettore modalità:** Consente di modificare la modalità. Puoi scegliere **[!UICONTROL Struttura]** modalità, **[!UICONTROL Contenuto iniziale]**, **[!UICONTROL Controllo layout]** modalità. La modalità Struttura consente di aggiungere e personalizzare intestazione e piè di pagina. La modalità Contenuto iniziale consente di personalizzare il contenuto del modulo.
   * **Anteprima:** Consente di visualizzare in anteprima l’aspetto del modello quando lo si pubblica. Potete utilizzare Selettore livello (Layer Selector) e Anteprima (Preview) per attivare o disattivare le modalità di modifica e anteprima.
* **Barra laterale:** Fornisce i browser Contenuto, Proprietà, Risorse e Componenti.
* **Barra degli strumenti del componente:** Quando selezioni un componente, viene visualizzata una barra degli strumenti che consente di personalizzarlo.
* **Pagina**: l’area in cui aggiungere contenuto per creare il modello.

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

## Modifica di un modello {#editing-a-template}

Di seguito sono elencate le diverse modalità per selezionare e modificare l’aspetto appropriato del modello:

* [Struttura](#structure)
* [Contenuto iniziale](#initial-content)
* [Layout](#layout)

Il selettore dei livelli è disponibile accanto all&#39;opzione Anteprima nell&#39;angolo superiore destro dello schermo.

### Struttura {#structure}

Quando si seleziona il livello struttura nell’Editor modelli, è utile predefinire il contenuto che non può essere modificato durante la creazione di Forms adattivi associati al modello.

<!-- you can see the layout containers above and below the Adaptive Form Container. Authors can use these layout containers for header and footer. -->


![Contenitore di layout nel livello struttura](/help/forms/assets/header-layer-selector-core-component.png)

<!--

**A. Layout container for Header component**
Drag-drop the Adaptive Form Header component in the layout container above the Adaptive Form Container. After you add the component, you can specify its properties that let you add a logo and provide its title.
**B. Adaptive Form Container component**
Drag-drop the Adaptive Form components in the Adaptive Form Container. You can specify the design and arrangement of fields and components in the template editor. After you add the components, you can specify its properties.
**C. Layout container for Footer component**
Similarly, when you drag-drop the footer component in the layout container below the Adaptive Form Container, you can provide the copyright information and company details. 
You can add, edit, or customize the header and footer. Drag-drop the Adaptive Form Header and Footer component to customize the template. Drag-drop the Adaptive Form components in the Adaptive Form Container. You can specify the design and arrangement of fields and components in the template editor. 


Header and footer are added in the Initial Content layer.
-->

#### Blocco/sblocco di componenti nel livello struttura {#locking-unlocking-components-in-the-structure-layer}

Quando modificate il modello con il livello struttura selezionato, potete sbloccare l&#39;intestazione e il piè di pagina del modello. Se un componente è sbloccato nel modello, gli autori dei moduli possono modificarlo nel modulo adattivo che utilizza il modello. Il blocco di un componente impedisce agli autori dei moduli di modificarlo nel modulo adattivo. L’opzione Blocca è disponibile nella barra degli strumenti del componente.

Ad esempio, puoi aggiungere il componente intestazione nel modello. Quando selezioni il componente, nella barra degli strumenti del componente è visibile un’opzione di blocco. In genere, l&#39;intestazione include il nome dell&#39;azienda e il logo e non si desidera che gli autori dei moduli modifichino il logo e l&#39;intestazione in un modello. In un modulo adattivo creato utilizzando il modello con il componente intestazione bloccato, gli autori dei moduli non possono modificare il logo e il nome della società.

>[!NOTE]
>
>Il blocco o lo sblocco di un’immagine o di un logo nel componente intestazione, singolarmente, non è consigliato. Puoi sbloccare il componente intestazione.

### Contenuto iniziale {#initial-content}

Quando l’opzione Contenuto iniziale è selezionata, il Contenitore di moduli adattivi del modello si apre come un Modulo adattivo da modificare. Ti consente di creare un contenuto predefinito che può essere modificato durante la creazione di un Forms adattivo associato al modello. Analogamente all’authoring di un modulo adattivo, puoi specificare le impostazioni iniziali, ad esempio selezionare un tema e Inviare azioni.

Gli autori di moduli utilizzano tale modulo come base per la creazione di un modulo. La struttura del flusso di contenuto è specificata nel livello Contenuto iniziale del modello. Per passare alla modifica del contenuto iniziale del modello di modulo, prima di visualizzare l’anteprima nella barra degli strumenti della pagina tocca ![elenco a discesa area di lavoro](assets/canvas-drop-down.png) **>** **[!UICONTROL Contenuto iniziale]**.

![Intestazione e piè di pagina aggiunti al livello Contenuto iniziale](assets/header-and-footer.png)

Nel livello Contenuto iniziale, puoi creare il modello di modulo adattivo utilizzato dagli autori come base. La creazione di un modello è simile alla creazione di un modulo e consente di utilizzare le opzioni disponibili nella barra laterale. Sidebar fornisce contenuti, proprietà, risorse e browser di componenti.

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>Quando si seleziona Archivia contenuto o Archivia PDF come azione di invio, si ottiene un&#39;opzione per specificare il percorso di archiviazione. Se si specifica il percorso nel modello, tutti i moduli creati da esso avranno lo stesso percorso. È possibile specificare il percorso di archiviazione corretto o assicurarsi che gli autori dei moduli lo aggiornino per impedire che i dati di ogni modulo vengano archiviati nella stessa posizione.

### Layout {#layout}

Quando modifichi un modello puoi definire il layout, che utilizza il layout dinamico standard. Il layout consente di gestire la larghezza di un componente in base alla larghezza del dispositivo per facilitare la progettazione di un modulo adattivo reattivo.

![Contenitore di layout nel livello struttura](/help/forms/assets/layout-template-core-component.png)

Consulta l’articolo [informazioni sul layout dinamico](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/responsive-layout-feature-video-understand.html?lang=en) per ulteriori informazioni.

## Abilitazione del modello {#enabling-the-template}

Quando create un modello, questo viene aggiunto come bozza. Abilita il modello per utilizzarlo per creare Forms adattivo. Per abilitare un modello:

1. Accedi a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Modelli]**e aprire la cartella in cui è stato creato il modello.
Il modello creato è contrassegnato come Bozza.
1. Seleziona il modello e tocca **[!UICONTROL Abilita]** nella barra degli strumenti.
Quando crei un modulo adattivo, puoi visualizzare il modello elencato quando ti viene richiesto di scegliere un modello.

## Importazione o esportazione di un modello {#importing-or-exporting-a-template}

Un modulo funziona con il relativo modello. Quando si scarica un modulo adattivo creato utilizzando un modello personalizzato, il modello non viene scaricato. Quando si importa il modulo su un altro [!DNL AEM Forms] istanza, viene importato senza il relativo modello. Se un modulo viene importato ma il relativo modello non è disponibile, il modulo non viene sottoposto a rendering. Puoi creare un pacchetto del modello personalizzato da `/conf` nodo in `https://<server>:<port>/crx/packmgr`, e portarlo in [!DNL AEM Forms] istanza in cui si desidera caricare il modulo. È inoltre possibile [Creare un modello utilizzando l’archetipo AEM e distribuirlo nell’istanza dei Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites).

>[!NOTE]
>
> * Puoi anche configurare il [!UICONTROL Documento record] direttamente dall’editor di moduli adattivi o dall’editor di modelli di moduli adattivi. Per ulteriori informazioni, consulta [Genera documento di record per Forms adattivo](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

## Associare uno schema modello dati modulo a un modello {#associating-form-data-model-schema-in-template}

Gli autori possono associare una [!UICONTROL Schema modello dati modulo] a un modello di modulo adattivo nell’editor di modelli. Consente agli autori di selezionare uno schema dall’editor modelli. Quando si associa uno schema a un modello e un autore di moduli crea un modulo basato su tale modello, lo schema viene preselezionato per il modulo. Consente agli autori di moduli di regolare l’utilizzo dello schema e consente di risparmiare tempo anche agli autori di moduli. Per selezionare uno schema di modello dati modulo nell’editor modelli:

1. Tocca **[!UICONTROL Browser contenuti]** sul lato sinistro.
1. Vai al contenitore del modulo **[!UICONTROL Impostazione]**.
1. Seleziona **[!UICONTROL Modello dati]**.
1. Scegli il modello dati del modulo tramite **[!UICONTROL Seleziona modello dati modulo]** e salva la configurazione.

![Form-Data-Model-Association-in-Forms](/help/forms/assets/select-form-data-model-img-core-component.png)

<!--

## Creating an Adaptive Form template with tabs and panels {#creating-an-adaptive-form-template-with-tabs-and-panels-nbs}

For example, you want to create a template with the following tabs:

* General Information
* Professional Information

You have added a logo, provided a title, and added a footer in the structure layer. Lock the header and footer to stop form authors from editing them when they use the template to create forms.

Change the layer from **Structure** to **Initial Content**, and start adding content to the form. To create a tabbed structure, add a child Panel in the guideRootPanel of the Adaptive Form container. To add a panel:

* You can add a panel by tapping the **[!UICONTROL +]** button when you select the **[!UICONTROL Drag components here]** option.

* You can drag-drop the panel component from the components browser in the sidebar.
* You can add child panel of the `guideRootPanel` from the component toolbar.

To create the General Information and Professional Information tabs, add two panels in the child panel of the `guideRootPanel`. Select the panels and tap ![cmppr](assets/configure-icon.svg) to open the properties in the sidebar. Change the element names as `general-info` and `professional-info`, and titles as General Information and Professional Information respectively. In the sidebar, tap content to open the content browser. In the Form Objects tab, select `guideRootPanel`. In the editor, the guideRootPanel is selected. Tap ![cmppr](assets/configure-icon.svg) in the component toolbar to open its properties. In the Panel Layout field, select **[!UICONTROL Tabs on Top]** and tap **[!UICONTROL Done]**. The tabbed template structure is applied.

### Adding content in tabs {#adding-content-in-tabs}

After you add panels and structure them as tabs, you can add fields inside the tabs. When you select a tab in the editor, you can see the **[!UICONTROL Drag components here]** option. You can drag-drop components such as text-boxes, list items, and buttons. You can drag-drop components from the components browser in the sidebar.

Each component has properties that enhance data capturing and manipulation. For example, you can enable the **[!UICONTROL Required field]** property of a component. Your authors can specify a message that your customers see when they skip filling a required field. Specify the message in **[!UICONTROL Required Field Message]** property.

In the example template, Name, Phone number, and Date of birth fields are added in the General Information tab. In the Professional Information tab, Currently employed, employment type, Educational qualification fields are added.

After you have added fields, you can add buttons such as Submit and Reset.
-->

### Aggiunta di proprietà personalizzate ai componenti di moduli adattivi tramite i criteri dei modelli

Le proprietà personalizzate consentono di associare attributi personalizzati (coppie chiave-valore) a un componente core Modulo adattivo utilizzando il modello di modulo. Le proprietà personalizzate si riflettono nel **[!UICONTROL proprietà]** sezione della rappresentazione headless del componente. Consente di creare un comportamento di modulo dinamico che si adatta in base ai valori degli attributi personalizzati. Ad esempio, gli sviluppatori possono progettare varie rappresentazioni di un componente Forms headless per piattaforme mobili, desktop o web, migliorando in modo significativo l’esperienza utente su un’ampia gamma di dispositivi.

I passaggi per aggiungere proprietà personalizzate ai campi del componente core Modulo adattivo sono i seguenti:

1. [Aggiungere un nome di gruppo personalizzato nel criterio di un editor di modelli](#add-a-custom-group-name)
1. [Seleziona un nome di gruppo personalizzato nella finestra di dialogo per modifica del componente di un modulo adattivo](#select-a-custom-group-name)

#### Aggiungi un nome gruppo personalizzato nel criterio dell’editor modelli {#add-a-custom-group-name}

1. Vai a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]**.
1. Seleziona il modello basato sui Componenti core e aprilo in modalità di modifica.
1. Fai clic su **[!UICONTROL Policy]** ![Policy](/help/forms/assets/Smock_FeedManagement_18_N.svg) icona di un campo del componente core Modulo adattivo in cui è necessario definire le proprietà personalizzate. Il **[!UICONTROL Campo modulo adattivo]** viene visualizzata.
1. Seleziona la **[!UICONTROL Proprietà personalizzate]** scheda.
1. Specifica la **[!UICONTROL Titolo criterio]** sotto **[!UICONTROL Policy]** sezione.
1. Specifica la **[!UICONTROL Nome gruppo]** e aggiungi una coppia chiave-valore associata a un gruppo specifico. Il nome del gruppo è visibile agli autori del modulo nella finestra di dialogo per modifica di un componente. Se selezioni il nome del gruppo, ogni coppia chiave-valore associata è applicabile a un componente.
1. Clic **[Fine]**.

![Aggiunta del nome del gruppo di proprietà personalizzate nell’editor modelli](/help/forms/assets/custom-properties-core-component.png)

Quando si aggiunge almeno un gruppo di proprietà personalizzate utilizzando il criterio del modello, il **[!UICONTROL Avanzate]** diventa visibile nella finestra di dialogo Modifica di un componente core corrispondente.

#### Seleziona un nome di gruppo personalizzato nella finestra di dialogo per modifica di un componente core {#select-a-custom-group-name}

1. Aprire un modulo adattivo in modalità di modifica.
1. Tocca il componente per il quale sono state definite le proprietà personalizzate nell’editor di modelli e tocca ![icona_impostazioni](assets/configure-icon.svg) per aprire la finestra di dialogo per modifica del componente.
1. Seleziona la **[!UICONTROL Avanzate]** scheda.
1. Seleziona il nome del gruppo di proprietà personalizzato da **[!UICONTROL Selezione proprietà personalizzata]** a discesa. Tutti i nomi dei gruppi personalizzati definiti vengono inseriti automaticamente nell’elenco a discesa.
1. Tocca **[!UICONTROL Fine]** per salvare le proprietà.

![seleziona il nome del gruppo di proprietà personalizzato](/help/forms/assets/select-custom-properties-group-name.png)

>[!NOTE]
>
> * Il **[!UICONTROL Proprietà personalizzate aggiuntive]** La casella di controllo consente di aggiungere in modo dinamico proprietà personalizzate specifiche del componente oltre a quelle fornite nel criterio del modello. La proprietà personalizzata del componente specifico ha la precedenza sulla proprietà personalizzata impostata nei criteri del modello quando i valori del nome chiave corrispondono.

## Creazione di un modulo adattivo utilizzando il modello {#creating-an-adaptive-form-using-the-template}

Dopo aver creato e abilitato un modello, questo sarà disponibile nel gestore dei moduli al momento della creazione di un modulo adattivo. Per utilizzare un modello e creare un modulo adattivo, consulta [Creazione di un modulo adattivo basato su componenti core](/help/forms/creating-adaptive-form-core-components.md).
<!--
## Change display option of out of the box templates  {#change-display-option-of-out-of-the-box-templates}

You can create custom templates for Adaptive Forms to define basic structure and initial content. [!DNL AEM Forms] also provides a set of out of the box template for Adaptive Forms. You can choose to show or hide the templates.

Perform the following steps to show and hide templates:

1. Log in to [!DNL AEM Forms] author instance and navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   >[!NOTE]
   >
   >The URL of AEM web console is https://'[server]:[port]'/system/console/configMgr

1. Locate and open the **FormsManager Configuration** settings:

    * To show or hide out of the box Adaptive Forms template, check or uncheck the **Include Out of the box AF and AD Templates** option.
    * To show or hide out of the box Adaptive Form templates that were added in AEM 6.0 Forms or AEM 6.1 Forms releases but are now deprecated, check or uncheck the **Include AEM 6.0 AF Templates** option. If this option is checked, and you want it to take effect, it requires the **Include Out of the box AF and AD Templates** configuration to be enabled.

1. Click **Save**. The display options for the out of the box templates are changed. 

## Save an Adaptive Form as a template {#saving-adaptive-form-as-template}

You can also save an Adaptive Form as a template for future use. To save a Adaptive Form as a template:

1. Select an Adaptive Form to save it as a template.
1. Click **[!UICONTROL Save as Template]**. A dialog box appears.
1. Specify **[!UICONTROL Title]** (mandatory field), **[!UICONTROL Location]** (mandatory field) and **[!UICONTROL Description]** (optional field) for the template. 
1. Click **[!UICONTROL Create]**.

   ![Save as Form as Template](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>To use the same container policy as of the source Adaptive Form, it is recommended to save the template in the same folder as of the source Adaptive Form. In case, the template is saved in any other folder, than the created template uses a default container policy.
-->

## Best practice {#best-practices}

* Crea modelli utilizzando i componenti basati su Componenti core, ad esempio Testo modulo adattivo, Contenitore modulo adattivo e altro ancora. Per informazioni sui componenti core Adaptive Forms: [fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it).
* Limita il numero di modelli in modo che corrispondano ai tipi di modulo fondamentalmente diversi disponibili sui siti web
* Fornisci la flessibilità e le funzionalità di configurazione necessarie ai componenti personalizzati utilizzati in un modello.

<!--
## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Create an Adaptive Form (core components)](/help/forms/creating-adaptive-form-core-components.md)

-->

## Consulta anche {#see-also}

{{see-also}}
* [Creare stili o temi per i moduli](using-themes-in-core-components.md)
* [Creare un modulo adattivo (componenti core)](/help/forms/creating-adaptive-form-core-components.md)

