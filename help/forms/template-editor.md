---
title: Come si crea un modello di modulo adattivo?
description: Creare modelli di modulo adattivo per definire la struttura di base e il contenuto iniziale utilizzando l’Editor modelli.
exl-id: a882cba2-c621-4ff7-a972-c504641b5639
source-git-commit: b4cc89f32dcdddf93f12f087a20395e055ea85bb
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 1%

---

# Creare un modello di modulo adattivo {#adaptive-form-templates}

Quando si crea un modulo, è possibile aggiungere campi e componenti per definire la struttura del modulo, il contenuto e le azioni nell’editor. Aggiungi campi e componenti nel `guideRootPanel` del contenitore modulo. Con l’Editor modelli è possibile creare un modello che contiene la struttura di base e il contenuto iniziale utilizzabili dagli autori per creare moduli.

Ad esempio, si desidera che tutti gli autori dei moduli dispongano di determinate caselle di testo, pulsanti di navigazione e un pulsante di invio in un modulo di iscrizione. È possibile creare un modello con i componenti utilizzabili dagli autori per creare un modulo coerente con gli altri moduli di iscrizione. Quando gli autori utilizzano il modello per creare un modulo adattivo, il nuovo modulo eredita la struttura e i componenti specificati nel modello. L’Editor modelli consente di:

* Aggiungere componenti di intestazione e piè di pagina di un modulo nel livello struttura.
* Fornire il contenuto iniziale del modulo.
* Specifica un tema, Invia azioni.

È possibile scaricare e installare [!DNL AEM Forms] pacchetto di contenuti di riferimento da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) portale per importare temi e modelli di riferimento nell’ambiente.

## Utilizzo dei modelli {#working-with-templates}

Per accedere all’editor modelli dal menu Strumenti, vai a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]**. In questo caso, i modelli sono organizzati in cartelle abilitate per i modelli modificabili.

Experience Manager fornisce una cartella globale per organizzare i modelli. Tuttavia, non è attivato per impostazione predefinita. È possibile richiedere all&#39;amministratore di abilitare la cartella globale o creare una cartella per i modelli. Per ulteriori informazioni sulla creazione delle cartelle, consulta [Cartelle dei modelli](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors).

### Creazione di un modello {#create-template}

Dopo aver creato una cartella, apri la cartella ed esegui i seguenti passaggi per creare un modello:

1. Tocca **[!UICONTROL Crea]** all’interno della cartella creata.
1. Nella sezione Scegli un tipo di modello selezionare **[!UICONTROL Modello di modulo adattivo]** e toccare **[!UICONTROL Successivo]**.

1. Nella sezione Template Details (Dettagli modello) , specifica un Titolo modello e tocca **[!UICONTROL Crea]**.
Puoi anche fornire una descrizione.

1. Tocca **[!UICONTROL Fine]** per tornare alla console o tocca **[!UICONTROL Apri]** per aprire il modello nell’editor.

### Interfaccia utente dell’editor modelli {#template-editor-ui}

Quando aprite un modello per la modifica, potete vedere i seguenti componenti AEM Editor:

* **Barra degli strumenti della pagina**
Contiene le seguenti opzioni:

   * **Attiva/Disattiva pannello laterale**: Consente di mostrare o nascondere la barra laterale.
   * **Informazioni pagina**: Consente di specificare informazioni quali l’ora di pubblicazione/annullamento della pubblicazione, le miniature, le librerie lato client, i criteri pagina e la libreria lato client della progettazione della pagina.

   <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **Selettore modalità:** Consente di modificare la modalità.È possibile scegliere **[!UICONTROL Struttura]** modalità, **[!UICONTROL Contenuto iniziale]**, **[!UICONTROL Controllo layout]** modalità. La modalità Struttura consente di aggiungere e personalizzare l’intestazione e il piè di pagina. La modalità Contenuto iniziale consente di personalizzare il contenuto del modulo.
   * **Anteprima:** Consente di visualizzare un’anteprima dell’aspetto del modello quando lo si pubblica. È possibile utilizzare Selettore livello e Anteprima per attivare o disattivare le modalità di modifica e anteprima.
* **Barra laterale:** Fornisce i browser Contenuto, Proprietà, Risorse e Componenti .
* **Barra degli strumenti del componente:** Quando selezioni un componente, viene visualizzata una barra degli strumenti che consente di personalizzare il componente.
* **Pagina**: Area in cui aggiungere contenuto per creare il modello.

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

### Modifica di un modello {#editing-a-template}

Un modello di modulo adattivo viene creato utilizzando due livelli:

* Struttura
* Contenuto iniziale

Il selettore livello è disponibile accanto all’opzione Anteprima nell’angolo superiore destro dello schermo.

### Struttura {#structure}

Quando si seleziona il livello struttura nell’Editor modelli, è possibile visualizzare i contenitori layout sopra e sotto il contenitore Modulo adattivo. Gli autori possono utilizzare questi contenitori layout per intestazione e piè di pagina. È possibile aggiungere, modificare o personalizzare l’intestazione e il piè di pagina. Trascina il componente Intestazione modulo adattiva nel contenitore di layout sopra il contenitore Modulo adattivo per personalizzare l’intestazione del modello. Trascina il componente Piè di pagina modulo adattivo nel contenitore di layout sotto il contenitore Modulo adattivo per personalizzare il piè di pagina del modello.

![Contenitore di layout nel livello struttura](assets/header-layer-selector.png)

Contenitori di layout nel livello struttura

**A.** Contenitore di layout per componente Intestazione **B.** Contenitore di layout per componente Piè di pagina

Trascina il componente Intestazione modulo adattivo nel contenitore di layout sopra il contenitore Modulo adattivo . Dopo aver aggiunto il componente, puoi specificarne le proprietà che consentono di aggiungere un logo e il relativo titolo.

Allo stesso modo, quando trascini il componente piè di pagina nel contenitore di layout sotto il contenitore Modulo adattivo, puoi fornire le informazioni sul copyright e i dettagli aziendali.

![Intestazione e piè di pagina aggiunti nel livello Struttura](assets/header-and-footer.png)

Intestazione e piè di pagina aggiunti nel livello Struttura

#### Blocco/sblocco dei componenti nel livello struttura {#locking-unlocking-components-in-the-structure-layer}

Quando modificate il modello con il livello struttura selezionato, potete sbloccare l’intestazione e il piè di pagina del modello. Se un componente viene sbloccato nel modello, gli autori dei moduli possono modificare il componente nel modulo adattivo che utilizza il modello. Il blocco di un componente impedisce agli autori di moduli di modificarlo nel modulo adattivo. L’opzione Blocca è disponibile nella barra degli strumenti del componente.

Ad esempio, puoi aggiungere il componente di intestazione nel modello. Quando selezioni il componente, puoi vedere un’opzione Blocca nella barra degli strumenti del componente. In genere, l’intestazione include il nome e il logo della società e non si desidera che gli autori dei moduli modifichino il logo e l’intestazione di un modello. In un modulo adattivo creato utilizzando il modello con il componente intestazione bloccato, gli autori dei moduli non possono modificare il logo e il nome dell’azienda.

>[!NOTE]
>
>Non è consigliabile bloccare o sbloccare singolarmente l’immagine o il logo nel componente intestazione. Puoi sbloccare il componente intestazione.

### Contenuto iniziale {#initial-content}

Quando l’opzione Contenuto iniziale è selezionata, il contenitore Modulo adattivo del modello viene aperto come Modulo adattivo per la modifica. Come per la creazione di un modulo adattivo, è possibile specificare le impostazioni iniziali, ad esempio la selezione di un tema e l’invio di azioni.

Gli autori dei moduli lo utilizzano come base per creare un modulo. La struttura del flusso di contenuto è specificata nel livello Contenuto iniziale del modello. Per passare alla modifica del contenuto iniziale del modello di modulo, prima di visualizzare l’anteprima nella barra degli strumenti della pagina, toccare ![elenco a discesa canvas](assets/canvas-drop-down.png) **>** **[!UICONTROL Contenuto iniziale]**.


Nel livello Contenuto iniziale , è possibile creare il modello Modulo adattivo utilizzato dagli autori come base. La creazione di un modello è simile alla creazione di un modulo e le opzioni disponibili sono disponibili nella barra laterale. Sidebar fornisce browser per contenuti, proprietà, risorse e componenti.

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>Quando si seleziona Archivia contenuto o Memorizza PDF come azione di invio, si ottiene un&#39;opzione per specificare il percorso di archiviazione. Se si specifica il percorso nel modello, tutti i moduli creati da esso avranno lo stesso percorso. È possibile specificare il percorso di archiviazione corretto oppure assicurarsi che gli autori dei moduli lo aggiornino per evitare che i dati vengano memorizzati nello stesso percorso da ogni modulo.

#### Creazione di un modello di modulo adattivo con schede e pannelli {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Ad esempio, se desideri creare un modello con le seguenti schede:

* Informazioni generali
* Informazioni professionali

È stato aggiunto un logo, un titolo e un piè di pagina nel livello struttura. Bloccare l’intestazione e il piè di pagina per impedire agli autori di moduli di modificarli quando utilizzano il modello per creare moduli.

Modifica il livello da Struttura a Contenuto iniziale e inizia ad aggiungere contenuto al modulo. Per creare una struttura a schede, aggiungi un pannello secondario nel pannello guideRootPanel del contenitore Modulo adattivo. Per aggiungere un pannello:

* Per aggiungere un pannello, tocca **[!UICONTROL +]** quando si seleziona il pulsante **[!UICONTROL Trascina qui i componenti]** opzione .

* Puoi trascinare il componente Pannello dal browser Componenti nella barra laterale.
* Puoi aggiungere un pannello secondario di `guideRootPanel` dalla barra degli strumenti del componente.

Per creare le schede Informazioni generali e Informazioni professionali , aggiungi due pannelli nel pannello figlio della scheda `guideRootPanel`. Seleziona i pannelli e tocca ![cmppr](assets/configure-icon.svg) per aprire le proprietà nella barra laterale. Modificare i nomi degli elementi come `general-info` e `professional-info`, e titoli rispettivamente come Informazioni generali e Informazioni professionali. Nella barra laterale, tocca il contenuto per aprire il browser del contenuto. Nella scheda Oggetti modulo, selezionare `guideRootPanel`. Nell’editor, viene selezionato guideRootPanel. Tocca ![cmppr](assets/configure-icon.svg) nella barra degli strumenti del componente per aprire le relative proprietà. Nel campo Layout pannello selezionare **[!UICONTROL Schede in alto]** e toccare **[!UICONTROL Fine]**. Viene applicata la struttura del modello a schede.

#### Aggiunta di contenuto nelle schede {#adding-content-in-tabs}

Dopo aver aggiunto i pannelli e averli strutturati come schede, puoi aggiungere campi all’interno delle schede. Quando selezioni una scheda nell’editor, puoi visualizzare il **[!UICONTROL Trascina qui i componenti]** opzione . È possibile trascinare componenti quali caselle di testo, elementi di elenco e pulsanti. Puoi trascinare i componenti dal browser Componenti nella barra laterale.

Ogni componente dispone di proprietà che migliorano l’acquisizione e la manipolazione dei dati. Ad esempio, puoi abilitare il **[!UICONTROL Campo obbligatorio]** di un componente. Gli autori possono specificare un messaggio che i clienti visualizzano ignorando la compilazione di un campo obbligatorio. Specifica il messaggio in **[!UICONTROL Messaggio campo richiesto]** proprietà.

Nel modello di esempio, i campi Nome, Numero di telefono e Data di nascita vengono aggiunti nella scheda Informazioni generali. Nella scheda Informazioni professionali, Attualmente impiegato, vengono aggiunti i campi Tipo di impiego, Qualificazione didattica.

Dopo aver aggiunto i campi, puoi aggiungere pulsanti quali Invia e Reimposta.

### Abilitazione del modello {#enabling-the-template}

Quando crei un modello, questo viene aggiunto come bozza. Abilita il modello per utilizzarlo per la creazione di Forms adattivo. Per abilitare un modello:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Modelli]**, quindi apri la cartella in cui hai creato il modello.

1. Il modello creato viene contrassegnato come Bozza.
1. Seleziona il modello e tocca **[!UICONTROL Abilita]** nella barra degli strumenti.
Quando si crea un modulo adattivo, è possibile visualizzare il modello elencato quando viene richiesto di scegliere un modello.

## Importazione o esportazione di un modello {#importing-or-exporting-a-template}

Un modulo funziona con il relativo modello. Quando si scarica un modulo adattivo creato utilizzando un modello personalizzato, il modello non viene scaricato. Quando si importa il modulo su un altro [!DNL AEM Forms] ad esempio, viene importato senza il relativo modello. Se un modulo viene importato ma il relativo modello non è disponibile, il modulo non viene sottoposto a rendering. Puoi creare un pacchetto del modello personalizzato da `/conf` nodo in `https://<server>:<port>/crx/packmgr`e la porta nel [!DNL AEM Forms] istanza in cui si desidera caricare il modulo. È inoltre possibile [Crea un modello utilizzando AEM Archeype e implementalo nell&#39;istanza dei Cloud Services](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites).

>[!NOTE]
>
> * Puoi anche configurare le [!UICONTROL Documento di registrazione] direttamente dall’editor di moduli adattivi o dall’editor di modelli di moduli adattivi. Per ulteriori informazioni, consulta [Genera documento di record per Forms adattivo](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).



## Associare uno schema del modello dati modulo a un modello {#associating-form-data-model-schema-in-template}

Gli autori possono associare un [!UICONTROL Schema del modello dati del modulo] in un modello di modulo adattivo nell’editor modelli. Consente agli autori di selezionare uno schema dall’editor modelli. Quando si associa uno schema a un modello e l’autore crea un modulo basato sul modello, lo schema viene preselezionato per il modulo. Consente agli autori dei moduli di regolare l’utilizzo dello schema e di risparmiare tempo anche per gli autori dei moduli. Per selezionare uno schema del modello dati modulo nell’editor modelli:

1. Tocca **[!UICONTROL Browser dei contenuti]** situato sul lato sinistro.
1. Passa al contenitore del modulo **[!UICONTROL Impostazione]**.
1. Seleziona **[!UICONTROL Modello dati]**.
1. Scegliere il modello dati del modulo tramite **[!UICONTROL Seleziona modello dati modulo]** e salva la configurazione.

![Modulo-Data-Model-Association-in-Forms](/help/forms/assets/select-form-data-model-img.png)



## Creazione di un modulo adattivo utilizzando il modello {#creating-an-adaptive-form-using-the-template}

Dopo aver creato e abilitato un modello, questo è disponibile in Forms Manager quando si crea un modulo adattivo. Per utilizzare un modello e creare un modulo adattivo, consulta [Creazione di un modulo adattivo](creating-adaptive-form.md).


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
    * To show or hide out of the box Adaptive Form templates that were added in AEM 6.0 Forms or AEM 6.1 Forms releases but are now deprecated, check or uncheck the **Include AEM 6.0 AF Templates** option. If this option is checked, in order to take effect, it requires the **Include Out of the box AF and AD Templates** configuration to be enabled.

1. Click **Save**. The display options for the out of the box templates are changed. -->

## Salvare un modulo adattivo come modello {#saving-adaptive-form-as-template}

È inoltre possibile salvare un modulo adattivo come modello da utilizzare in futuro. Per salvare un modulo adattivo come modello:

1. Seleziona un modulo adattivo per salvarlo come modello.
1. Fai clic su **[!UICONTROL Salva come modello]**. Viene visualizzata una finestra di dialogo.
1. Specifica **[!UICONTROL Titolo]** (campo obbligatorio), **[!UICONTROL Posizione]** (campo obbligatorio) e **[!UICONTROL Descrizione]** (campo facoltativo) per il modello.
1. Fai clic su **[!UICONTROL Crea]**.

   ![Salva come modulo come modello](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>Per utilizzare lo stesso criterio contenitore del modulo adattivo di origine, si consiglia di salvare il modello nella stessa cartella del modulo adattivo di origine. Nel caso in cui il modello venga salvato in qualsiasi altra cartella, il modello creato utilizza un criterio contenitore predefinito.

## Consigli {#recommendations}

* Quando si modificano le proprietà del modulo nell&#39;editor modelli, non utilizzare la proprietà BindReference.
* Per aggiungere un punto di interruzione, crealo quando crei un modello di modulo adattivo.
Per ulteriori informazioni sui punti di interruzione, vedi [Layout reattivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/responsive-layout.html#authoring).
