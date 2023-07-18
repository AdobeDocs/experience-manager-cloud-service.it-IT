---
title: Come si crea un modello di modulo adattivo?
description: Crea modelli per moduli adattivi per definire la struttura di base e il contenuto iniziale tramite l’Editor modelli.
exl-id: a882cba2-c621-4ff7-a972-c504641b5639
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '2038'
ht-degree: 1%

---

# Creare un modello di modulo adattivo {#adaptive-form-templates}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/template-editor.html) |
| AEM as a Cloud Service | Questo articolo |

Quando si crea un modulo, si aggiungono campi e componenti per definire la struttura del modulo, il contenuto e le azioni nell’editor. È possibile aggiungere campi e componenti in `guideRootPanel` del contenitore di moduli. Con Editor modelli è possibile creare un modello contenente la struttura di base e il contenuto iniziale che gli autori possono utilizzare per creare i moduli.

Ad esempio, si desidera che tutti gli autori di moduli dispongano di determinate caselle di testo, pulsanti di spostamento e un pulsante di invio in un modulo di iscrizione. È possibile creare un modello con i componenti che gli autori possono utilizzare per creare un modulo coerente con altri moduli di iscrizione. Quando gli autori utilizzano il modello per creare un modulo adattivo, il nuovo modulo eredita la struttura e i componenti specificati nel modello. Editor modelli consente di:

* Aggiungete i componenti intestazione e piè di pagina di un modulo nel livello struttura.
* Fornire il contenuto iniziale del modulo.
* Specifica un tema, Invia azioni.

Puoi scaricare e installare [!DNL AEM Forms] pacchetto di contenuti di riferimento da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) per importare nell&#39;ambiente i temi e i modelli di riferimento.

## Utilizzo dei modelli {#working-with-templates}

Per accedere all’editor modelli dal menu Strumenti, vai a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]**. In questo caso, i modelli sono organizzati in cartelle abilitate per i modelli modificabili.

In Experience Manager viene fornita una cartella globale per organizzare i modelli. Tuttavia, non è attivato per impostazione predefinita. Puoi richiedere all’amministratore di abilitare la cartella globale o di creare una cartella per i modelli. Per ulteriori informazioni su come creare cartelle, consulta [Cartelle modelli](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors).

### Creazione di un modello {#create-template}

Dopo aver creato una cartella, aprila ed esegui i seguenti passaggi per creare un modello:

1. Tocca **[!UICONTROL Crea]** all’interno della cartella creata.
1. Nella sezione Scegli un tipo di modello, selezionare **[!UICONTROL Modello modulo adattivo]** e tocca **[!UICONTROL Successivo]**.

1. Nella sezione Dettagli modello, specifica un Titolo modello e tocca **[!UICONTROL Crea]**.
Puoi anche fornire una descrizione.

1. Tocca **[!UICONTROL Fine]** per tornare alla console, oppure tocca **[!UICONTROL Apri]** per aprire il modello nell’editor.

### Interfaccia utente dell’editor modelli {#template-editor-ui}

Quando apri un modello per la modifica, puoi vedere i seguenti componenti dell’editor AEM:

* **Barra degli strumenti Pagina**
Contiene le seguenti opzioni:

   * **Attiva/Disattiva pannello laterale**: consente di mostrare o nascondere la barra laterale.
   * **Informazioni pagina**: consente di specificare informazioni quali l’ora di pubblicazione/annullamento della pubblicazione, le miniature, le librerie lato client, i criteri di pagina e la libreria lato client della progettazione della pagina.
     <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **Selettore modalità:** Consente di modificare la modalità.È possibile scegliere **[!UICONTROL Struttura]** modalità, **[!UICONTROL Contenuto iniziale]**, **[!UICONTROL Controllo layout]** modalità. La modalità Struttura consente di aggiungere e personalizzare intestazione e piè di pagina. La modalità Contenuto iniziale consente di personalizzare il contenuto del modulo.
   * **Anteprima:** Consente di visualizzare in anteprima l’aspetto del modello quando lo si pubblica. Potete utilizzare Selettore livello (Layer Selector) e Anteprima (Preview) per attivare o disattivare le modalità di modifica e anteprima.
* **Barra laterale:** Fornisce i browser Contenuto, Proprietà, Risorse e Componenti.
* **Barra degli strumenti del componente:** Quando selezioni un componente, viene visualizzata una barra degli strumenti che consente di personalizzarlo.
* **Pagina**: l’area in cui aggiungere contenuto per creare il modello.

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

### Modifica di un modello {#editing-a-template}

Un modello di modulo adattivo viene creato utilizzando due livelli:

* Struttura
* Contenuto iniziale

Il selettore dei livelli è disponibile accanto all&#39;opzione Anteprima nell&#39;angolo superiore destro dello schermo.

### Struttura {#structure}

Quando selezioni il livello struttura nell’Editor modelli, puoi visualizzare i contenitori di layout sopra e sotto il Contenitore modulo adattivo. Gli autori possono utilizzare questi contenitori di layout per intestazione e piè di pagina. È possibile aggiungere, modificare o personalizzare l&#39;intestazione e il piè di pagina. Per personalizzare l’intestazione del modello, trascina il componente Intestazione modulo adattiva nel contenitore di layout sopra il Contenitore modulo adattivo. Per personalizzare il piè di pagina del modello, trascina il componente Piè di pagina modulo adattivo nel contenitore di layout sotto il contenitore modulo adattivo.

![Contenitore di layout nel livello struttura](assets/header-layer-selector.png)

Contenitori di layout nel livello struttura

**R.** Contenitore di layout per il componente Intestazione **B.** Contenitore di layout per il componente Piè di pagina

Trascina il componente Intestazione modulo adattivo nel contenitore di layout sopra il contenitore modulo adattivo. Dopo aver aggiunto il componente, puoi specificarne le proprietà che ti consentono di aggiungere un logo e il relativo titolo.

Allo stesso modo, quando trascini il componente Piè di pagina nel contenitore di layout sotto il Contenitore di moduli adattivi, puoi fornire le informazioni sul copyright e i dettagli dell’azienda.

![Intestazione e piè di pagina aggiunti nel livello Struttura](assets/header-and-footer.png)

Intestazione e piè di pagina aggiunti nel livello Struttura

#### Blocco/sblocco di componenti nel livello struttura {#locking-unlocking-components-in-the-structure-layer}

Quando modificate il modello con il livello struttura selezionato, potete sbloccare l&#39;intestazione e il piè di pagina del modello. Se un componente è sbloccato nel modello, gli autori dei moduli possono modificarlo nel modulo adattivo che utilizza il modello. Il blocco di un componente impedisce agli autori dei moduli di modificarlo nel modulo adattivo. L’opzione Blocca è disponibile nella barra degli strumenti del componente.

Ad esempio, puoi aggiungere il componente intestazione nel modello. Quando selezioni il componente, nella barra degli strumenti del componente è visibile un’opzione di blocco. In genere, l&#39;intestazione include il nome dell&#39;azienda e il logo e non si desidera che gli autori dei moduli modifichino il logo e l&#39;intestazione in un modello. In un modulo adattivo creato utilizzando il modello con il componente intestazione bloccato, gli autori dei moduli non possono modificare il logo e il nome della società.

>[!NOTE]
>
>Il blocco o lo sblocco di un’immagine o di un logo nel componente intestazione, singolarmente, non è consigliato. Puoi sbloccare il componente intestazione.

### Contenuto iniziale {#initial-content}

Quando l’opzione Contenuto iniziale è selezionata, il Contenitore di moduli adattivi del modello si apre come un Modulo adattivo da modificare. Analogamente all’authoring di un modulo adattivo, puoi specificare le impostazioni iniziali, ad esempio selezionare un tema e Inviare azioni.

Gli autori di moduli utilizzano tale modulo come base per la creazione di un modulo. La struttura del flusso di contenuto è specificata nel livello Contenuto iniziale del modello. Per passare alla modifica del contenuto iniziale del modello di modulo, prima di visualizzare l’anteprima nella barra degli strumenti della pagina tocca ![elenco a discesa area di lavoro](assets/canvas-drop-down.png) **>** **[!UICONTROL Contenuto iniziale]**.


Nel livello Contenuto iniziale, puoi creare il modello di modulo adattivo utilizzato dagli autori come base. La creazione di un modello è simile alla creazione di un modulo e consente di utilizzare le opzioni disponibili nella barra laterale. Sidebar fornisce contenuti, proprietà, risorse e browser di componenti.

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>Quando si seleziona Archivia contenuto o Archivia PDF come azione di invio, viene visualizzata un&#39;opzione per specificare il percorso di archiviazione. Se si specifica il percorso nel modello, tutti i moduli creati da esso avranno lo stesso percorso. È possibile specificare il percorso di archiviazione corretto o assicurarsi che gli autori dei moduli lo aggiornino per impedire che i dati di ogni modulo vengano archiviati nella stessa posizione.

#### Creazione di un modello di modulo adattivo con schede e pannelli {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Ad esempio, puoi creare un modello con le seguenti schede:

* Informazioni generali
* Informazioni professionali

È stato aggiunto un logo, un titolo e un piè di pagina nel livello struttura. Bloccare l&#39;intestazione e il piè di pagina per impedire agli autori di moduli di modificarli quando utilizzano il modello per creare moduli.

Modificare il livello da Struttura a Contenuto iniziale e iniziare ad aggiungere contenuto al modulo. Per creare una struttura a schede, aggiungi un pannello secondario in guideRootPanel del contenitore di moduli adattivi. Per aggiungere un pannello:

* Per aggiungere un pannello, tocca il **[!UICONTROL +]** quando si seleziona il pulsante **[!UICONTROL Trascina qui i componenti]** opzione.

* Puoi trascinare il componente Pannello dal browser Componenti nella barra laterale.
* È possibile aggiungere un pannello figlio di `guideRootPanel` dalla barra degli strumenti del componente.

Per creare le schede Informazioni generali e Informazioni professionali, aggiungi due pannelli nel pannello secondario di `guideRootPanel`. Seleziona i pannelli e tocca ![cmppr](assets/configure-icon.svg) per aprire le proprietà nella barra laterale. Modifica i nomi degli elementi come `general-info` e `professional-info`e titoli rispettivamente come Informazioni generali e Informazioni professionali. Nella barra laterale, tocca contenuto per aprire il browser contenuti. Nella scheda Oggetti modulo, seleziona `guideRootPanel`. Nell’editor, viene selezionato guideRootPanel. Tocca ![cmppr](assets/configure-icon.svg) nella barra degli strumenti del componente per aprirne le proprietà. Nel campo Layout pannello, seleziona **[!UICONTROL Schede in alto]** e tocca **[!UICONTROL Fine]**. Viene applicata la struttura a schede del modello.

#### Aggiunta di contenuto nelle schede {#adding-content-in-tabs}

Dopo aver aggiunto i pannelli e averli strutturati come schede, puoi aggiungere campi all’interno delle schede. Quando selezioni una scheda nell’editor, puoi visualizzare **[!UICONTROL Trascina qui i componenti]** opzione. È possibile trascinare componenti quali caselle di testo, voci di elenco e pulsanti. Puoi trascinare i componenti dal browser Componenti nella barra laterale.

Ogni componente dispone di proprietà che migliorano l’acquisizione e la manipolazione dei dati. Ad esempio, puoi abilitare **[!UICONTROL Campo obbligatorio]** di un componente. Gli autori possono specificare un messaggio visualizzato dai clienti quando non compilano un campo obbligatorio. Specifica il messaggio in **[!UICONTROL Messaggio campo obbligatorio]** proprietà.

Nel modello di esempio, i campi Nome, Numero di telefono e Data di nascita vengono aggiunti nella scheda Informazioni generali. Nella scheda Informazioni professionali, Tipo di impiego attualmente impiegato, vengono aggiunti i campi Istruzione e qualifica.

Dopo aver aggiunto i campi, puoi aggiungere pulsanti quali Invia e Reimposta.

### Abilitazione del modello {#enabling-the-template}

Quando create un modello, questo viene aggiunto come bozza. Abilita il modello per utilizzarlo per creare Forms adattivo. Per abilitare un modello:

1. Accedi a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Modelli]** e aprire la cartella in cui è stato creato il modello.

1. Il modello creato è contrassegnato come Bozza.
1. Seleziona il modello e tocca **[!UICONTROL Abilita]** nella barra degli strumenti.
Quando crei un modulo adattivo, puoi visualizzare il modello elencato quando ti viene richiesto di scegliere un modello.

## Importazione o esportazione di un modello {#importing-or-exporting-a-template}

Un modulo funziona con il relativo modello. Quando si scarica un modulo adattivo creato utilizzando un modello personalizzato, il modello non viene scaricato. Quando si importa il modulo su un altro [!DNL AEM Forms] istanza, viene importato senza il relativo modello. Se un modulo viene importato ma il relativo modello non è disponibile, il modulo non viene sottoposto a rendering. Puoi creare un pacchetto del modello personalizzato da `/conf` nodo in `https://<server>:<port>/crx/packmgr`, e portarlo in [!DNL AEM Forms] istanza in cui si desidera caricare il modulo. È inoltre possibile [Creare un modello utilizzando AEM Archeype e distribuirlo nell’istanza dei Cloud Services](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites).

>[!NOTE]
>
> * Puoi anche configurare il [!UICONTROL Documento record] direttamente dall’editor di moduli adattivi o dall’editor di modelli di moduli adattivi. Per ulteriori informazioni, consulta [Genera documento di record per Forms adattivo](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).


## Associare uno schema modello dati modulo a un modello {#associating-form-data-model-schema-in-template}

Gli autori possono associare una [!UICONTROL Schema modello dati modulo] a un modello di modulo adattivo nell’editor di modelli. Consente agli autori di selezionare uno schema dall’editor modelli. Quando si associa uno schema a un modello e un autore di moduli crea un modulo basato su tale modello, lo schema viene preselezionato per il modulo. Consente agli autori di moduli di regolare l’utilizzo dello schema e consente di risparmiare tempo anche per l’autore di moduli. Per selezionare uno schema di modello dati modulo nell’editor modelli:

1. Tocca **[!UICONTROL Browser contenuti]** sul lato sinistro.
1. Vai al contenitore del modulo **[!UICONTROL Impostazione]**.
1. Seleziona **[!UICONTROL Modello dati]**.
1. Scegli il modello dati del modulo tramite **[!UICONTROL Seleziona modello dati modulo]** e salva la configurazione.

![Form-Data-Model-Association-in-Forms](/help/forms/assets/select-form-data-model-img.png)



## Creazione di un modulo adattivo utilizzando il modello {#creating-an-adaptive-form-using-the-template}

Dopo aver creato e abilitato un modello, questo sarà disponibile nel gestore dei moduli al momento della creazione di un modulo adattivo. Per utilizzare un modello e creare un modulo adattivo, consulta [Creazione di un modulo adattivo](creating-adaptive-form.md).


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

1. Click **Save**. The display options for the out of the box templates are changed. -->

## Salvare un modulo adattivo come modello {#saving-adaptive-form-as-template}

È inoltre possibile salvare un modulo adattivo come modello per utilizzi futuri. Per salvare un modulo adattivo come modello:

1. Seleziona un modulo adattivo per salvarlo come modello.
1. Clic **[!UICONTROL Salva come modello]**. Viene visualizzata una finestra di dialogo.
1. Specifica **[!UICONTROL Titolo]** (campo obbligatorio), **[!UICONTROL Posizione]** (campo obbligatorio) e **[!UICONTROL Descrizione]** (campo facoltativo) per il modello.
1. Fai clic su **[!UICONTROL Crea]**.

   ![Salva come modulo come modello](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>Per utilizzare lo stesso criterio contenitore del modulo adattivo di origine, si consiglia di salvare il modello nella stessa cartella del modulo adattivo di origine. Nel caso in cui il modello venga salvato in un’altra cartella, viene utilizzato un criterio contenitore predefinito.

## Consigli {#recommendations}

* Quando si modificano le proprietà del modulo nell&#39;editor modelli, non utilizzare la proprietà BindReference.
* Se desideri aggiungere un punto di interruzione, crealo quando crei un modello di modulo adattivo.
Per ulteriori informazioni sui punti di interruzione, consulta [Layout reattivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/responsive-layout.html#authoring).
