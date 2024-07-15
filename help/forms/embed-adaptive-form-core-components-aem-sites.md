---
title: Come si aggiunge o crea un componente core Modulo adattivo nella pagina AEM Sites?
description: Utilizza i componenti core modulo adattivo in una pagina AEM Sites per compilare e inviare un modulo senza uscire dalle pagine AEM Sites.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '2071'
ht-degree: 1%

---

# Creare o aggiungere un modulo adattivo tramite l’editor di AEM Sites {#add-an-adaptive-form-to-aem-sites-page}

Puoi creare o incorporare facilmente Forms adattivo in una pagina di AEM Sites per consentire agli utenti di compilare e inviare un modulo senza uscire dalla pagina Sites. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e interagire contemporaneamente con il modulo.

Per creare o aggiungere un modulo adattivo a una pagina di AEM Sites, puoi scegliere uno dei seguenti metodi:

* **Creare un modulo adattivo utilizzando il componente Contenitore Forms adattivo**: il componente [Contenitore modulo adattivo](#af-container-component) consente di creare esperienze di registrazione digitale utilizzando componenti Forms adattivo direttamente nell&#39;editor di AEM Sites. Questa integrazione offre un’esperienza fluida agli autori di AEM Sites che desiderano creare e gestire moduli all’interno delle loro pagine AEM Sites.

* **Aggiungi un modulo adattivo esistente**: il componente [Forms adattivo - Incorpora(v2)](#embed-existing-af) consente di aggiungere facilmente un modulo adattivo preesistente in una pagina di AEM Sites. Questa funzione migliora l’adattabilità e la riutilizzabilità di Adaptive Forms. Questa integrazione offre ai clienti un modo pratico per riutilizzare i Forms adattivi già creati.

* **Crea un modulo con l&#39;Adaptive Forms Wizard**: usa il componente [Adaptive Forms - Embed(v2)](#embed-new-af) per creare un modulo adattivo dall&#39;editor di AEM Sites tramite la procedura guidata per la creazione di moduli. Il modulo viene salvato come entità esterna. Puoi riutilizzare questo modulo anche in altre pagine Sites e moduli autonomi.

* **Aggiungere più Forms adattivi in una pagina AEM Sites**: per aggiungere più Forms adattivi in una pagina AEM Sites, utilizza i componenti contenitore AEM Forms - [Forms adattivi - Incorpora(v2)](#embed-new-af) e [Contenitore modulo adattivo](#af-container-component). Nel caso in cui sia necessario aggiungere più di un modulo adattivo come div all’interno di una pagina AEM Sites, puoi utilizzare il componente Contenitore modulo adattivo.

È possibile utilizzare l’Editor regole per aggiungere o controllare il comportamento dinamico dei componenti Modulo adattivo. Ad esempio, puoi nascondere o mostrare un componente. L’editor di regole non è disponibile per i componenti di moduli non adattivi. Pertanto, utilizza la tua diligenza durante l’utilizzo dei componenti Modulo non adattivo nel componente Contenitore di AEM Forms.

## Creare un modulo adattivo utilizzando il componente Contenitore Forms adattivo {#af-container-component}

Il componente [!UICONTROL Contenitore modulo adattivo] consente di creare esperienze di registrazione digitale utilizzando i componenti Adaptive Forms nell&#39;editor di AEM Sites. Per creare un modulo adattivo, trascina i componenti del modulo.

### Prerequisiti {#prerequisites-af-container}

+++ Abilita il componente **[!UICONTROL Contenitore Forms adattivo]**.

Per abilitare il componente [!UICONTROL Contenitore Forms adattivo] nel criterio del modello, eseguire la procedura seguente:

1. Vai a [!UICONTROL Informazioni pagina] > [!UICONTROL Modifica modello]
1. Fai clic sul [!UICONTROL Criterio] e seleziona la casella di controllo **[!UICONTROL Contenitore Forms adattivo]** in **[Nome progetto archetipo AEM] - Modulo adattivo**.
1. Fai clic su **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ Pagina Includi librerie client Forms adattive ad AEM Sites

Per utilizzare i componenti Forms adattivi in una pagina di AEM Sites, includi le librerie client Customheaderlibs e Customfooterlibs nella pagina di AEM Sites utilizzando l’archivio e la pipeline di distribuzione di Archetipo/Git AEM.

1. Apri il progetto [Archetipo AEM Forms o Archivio Git clonato](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) in un editor di testo. Ad esempio, Visual Studio Code.
1. Accedi a `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copia il valore di `sling:resourceSuperType`. Ad esempio, il valore è `core/wcm/components/page/v3/page`.

   ![risorsa Sling](/help/forms/assets/slingresource.png)

1. Creare la struttura simile nel percorso `ui.apps/src/main/content/jcr_root/apps` come `core/wcm/components/page/v3/page`.

   ![struttura sovrapposta](/help/forms/assets/overlaystructure.png)

1. Aggiungere `customheaderlibs.html` e `customfooterlibs.html` file.

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly> 
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly> 
   ```

   Il file customfooterlibs.html viene utilizzato per JavaScript e il file customheaderlibs.html per css.

1. [Esegui la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) per distribuire le modifiche.

+++

### Creare un modulo adattivo utilizzando il componente Contenitore Forms adattivo {#create-af-using-af-container}


Per creare un modulo adattivo utilizzando il componente [!UICONTROL Contenitore Forms adattivo]:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina il componente **[!UICONTROL Contenitore Forms adattivo]** sulla pagina.
1. Creare un modulo adattivo utilizzando i componenti Forms adattivi.
1. Salva le impostazioni.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Modulo pronto. Quando pubblichi la pagina AEM Sites, questo pubblica automaticamente il modulo adattivo e le relative risorse di riferimento associate.

#### Configurare le proprietà del contenitore di moduli adattivi {#configure-additional-settings-container}

È possibile personalizzare le impostazioni avanzate del componente [!UICONTROL Contenitore modulo adattivo]. Ad esempio:

* Puoi configurare il servizio di precompilazione in modo da caricare un modulo adattivo con valori precompilati sulla pagina di un sito.
* È possibile configurare le impostazioni del modello dati per associare il modulo adattivo a un’origine dati.
* È possibile configurare le azioni di invio per inviare i dati in Microsoft® OneDrive, Microsoft® OneDrive o altre origini dati all&#39;invio di un modulo. Puoi anche creare e selezionare un’azione di invio personalizzata per il Forms adattivo.

Per impostare le proprietà del componente **[!UICONTROL Contenitore Forms adattivo]**, fare clic sull&#39;![icona_impostazioni](/help/forms/assets/Smock_Wrench_18_N.svg) sulla barra delle azioni. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica contenitore Forms adattivo]**.

![Finestra di dialogo per modifica](/help/forms/assets/adaptiveformcontainer-editdialog.png)

Nella finestra di dialogo [!UICONTROL Modifica contenitore Forms adattivo] puoi specificare quanto segue.
* **Scheda Base**
   * **Servizio di precompilazione**: è possibile utilizzare il servizio di precompilazione per compilare automaticamente i campi di un modulo adattivo utilizzando dati esistenti. Quando un utente apre un modulo, i valori di tali campi vengono precompilati. Per informazioni sul servizio di precompilazione, consulta [Campi modulo adattivo precompilati](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **Categoria libreria client**: specificare le [funzioni JavaScript](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) utilizzate nelle espressioni e supportate da Forms adattivo.
* **Modello dati**: un modello dati consente di integrare entità e servizi da origini dati diverse a un modulo adattivo. Scegliere **[!UICONTROL Modello dati modulo]** se il modulo adattivo che si sta creando prevede il recupero e la scrittura di dati da e verso più origini dati.
   * **Modello dati modulo**: un modello dati modulo (FDM) consente a un modulo adattivo di comunicare con origini dati diverse. Per informazioni sulla configurazione di un&#39;origine dati, vedere [Configurare origini dati](/help/forms/configure-data-sources.md).
   * **Schema**: lo schema rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end dell&#39;organizzazione. È possibile [associare lo schema a un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) e utilizzarne gli elementi per aggiungere contenuto dinamico a un modulo adattivo.

     >[!NOTE]
     >
     > Dopo aver configurato il modello dati del modulo (FDM), non è possibile modificare il modello modulo associato. Tuttavia, è possibile modificare lo schema associato al modello dati del modulo (FDM).

* **Scheda Invio**

   * **Reindirizza all&#39;URL**
      * **URL/percorso di reindirizzamento**: specifica l&#39;URL o il percorso a cui viene reindirizzato un modulo adattivo dopo l&#39;invio.

      * **Azione di invio**: un&#39;azione di invio viene attivata quando un utente fa clic sul pulsante Invia in un modulo adattivo. Puoi [configurare l&#39;azione di invio in Modulo adattivo](/help/forms/configuring-submit-actions.md). I moduli adattivi forniscono le seguenti azioni di invio pronte all’uso:
         * Invia all’endpoint REST
         * Invia e-mail
         * Invia utilizzando il modello dati modulo (FDM)
         * Richiama un flusso di lavoro AEM
         * Invia a SharePoint
         * Invia a OneDrive
         * Invia ad Azure Blob Storage

  Puoi anche [estendere le azioni di invio predefinite](custom-submit-action-form.md) per creare un&#39;azione di invio personalizzata.

* **Mostra messaggio**
   * **Contenuto messaggio**: scrivi un messaggio utilizzando l&#39;editor Rich Text per visualizzarlo all&#39;invio del modulo. Questa opzione è disponibile solo quando si sceglie di visualizzare un messaggio di ringraziamento.

## Incorporare un modulo adattivo  {#aem-container-component}

Utilizzando il componente **[!UICONTROL Forms adattivo - Incorpora (V2)]**, puoi incorporare un nuovo modulo adattivo o incorporare un modulo adattivo esistente nella pagina del sito. Il componente [!UICONTROL Forms adattivo - Incorpora(v2)] consente di:

* [Aggiungi un modulo adattivo esistente](#embed-new-af)

* [Creare e aggiungere un nuovo modulo adattivo](#embed-existing-af)

### Prerequisiti {#prerequisites}

+++ Abilita il componente **Forms adattivo - Incorpora**.

Per abilitare il componente [!UICONTROL Forms adattivo - Incorpora(v2)] nel criterio del modello, eseguire la procedura seguente:

1. Vai a [!UICONTROL Informazioni pagina] > [!UICONTROL Modifica modello]

1. Fai clic sul [!UICONTROL Criterio] e seleziona la casella di controllo **[!UICONTROL Modulo adattivo - Incorpora (v2)]** nel gruppo **[!UICONTROL [Nome progetto archetipo AEM] - Forms]**.
1. Fai clic su **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ Pagina Includi librerie client Forms adattive ad AEM Sites

Quando l&#39;opzione **[!UICONTROL Quando il modulo copre l&#39;intera larghezza di una pagina]** è selezionata nella finestra di dialogo di configurazione **[!UICONTROL Contenitori modulo]** e vengono utilizzati **Forms adattivi che utilizzano i componenti core**, è necessario includere le clientlibs nella pagina del sito corrispondente.

![Sovrapposizione Gif](/help/forms/assets/overlaycorecomponent.gif)

Per utilizzare i componenti Forms adattivi in una pagina di AEM Sites, includi le librerie client `Customheaderlibs` e `Customfooterlibs` nella pagina di AEM Sites utilizzando l’archivio e la pipeline di distribuzione di tipo Archetipo AEM/Git.

1. Apri il progetto [Archetipo AEM Forms o Archivio Git clonato](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) in un editor di testo. Ad esempio, Visual Studio Code.
1. Accedi a `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copia il valore di `sling:resourceSuperType`. Ad esempio, il valore è `core/wcm/components/page/v3/page`.

   ![risorsa Sling](/help/forms/assets/slingresource.png)

1. Creare la struttura simile nel percorso `ui.apps/src/main/content/jcr_root/apps` come `core/wcm/components/page/v3/page`.

   ![struttura sovrapposta](/help/forms/assets/overlaystructure.png)

1. Aggiungere `customheaderlibs.html` e `customfooterlibs.html` file.

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
       data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
       <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly>
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
     data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
     <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly>
   ```

   `customfooterlibs.html` viene utilizzato per JavaScript e `customheaderlibs.html` per CSS.

1. [Esegui la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) per distribuire le modifiche.

+++

### Aggiungi un modulo adattivo esistente alla pagina AEM Sites {#embed-existing-af}

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina il componente [!UICONTROL Forms adattivo - Incorpora] sulla pagina.
1. Seleziona il componente [!UICONTROL Forms adattivo - Incorpora] nella pagina Sites e seleziona ![icona_impostazioni](/help/forms/assets/Smock_Wrench_18_N.svg) nella barra delle azioni. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica Forms adattivo - Incorpora]**.
1. Sfoglia e seleziona il modulo adattivo da incorporare nel [!UICONTROL percorso risorsa].
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)



### Crea e aggiungi un nuovo modulo adattivo alla pagina AEM Sites {#embed-new-af}

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina il componente [!UICONTROL Forms adattivo - Incorpora(v2)] sulla pagina.
1. Fai clic sull&#39;icona **Plus** per reindirizzarti alla procedura guidata di creazione del modulo.

   ![Forms adattivo - Componente di incorporamento](/help/forms/assets/aemformcontainer.png)

1. Crea un nuovo modulo adattivo dalla procedura guidata [!UICONTROL Creazione modulo].
1. Il [!UICONTROL percorso risorsa] include già il percorso di un modulo adattivo creato
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

#### Configura modulo adattivo - Proprietà Incorpora (v2) {#configure-adaptive-form-embed}

È possibile personalizzare le impostazioni avanzate del componente [!UICONTROL Modulo adattivo - Incorpora(v2)]. Nella finestra di dialogo [!UICONTROL Modifica Forms adattivo - Incorpora(v2)] puoi specificare quanto segue.

* **Percorso risorsa**: sfoglia e seleziona il modulo adattivo da incorporare. Viene compilato automaticamente se viene rilasciato dal browser Assets.
* **Invio Post**: selezionare l&#39;azione da attivare all&#39;invio del modulo. Puoi scegliere di visualizzare un messaggio di ringraziamento o una pagina di ringraziamento.
   * **Mostra messaggio di ringraziamento**: scrivi un messaggio utilizzando l&#39;editor Rich Text per visualizzarlo all&#39;invio del modulo. Questa opzione è disponibile solo quando si sceglie di visualizzare un messaggio di ringraziamento.
   * **Mostra pagina di ringraziamento**: sfoglia e seleziona la pagina da visualizzare all&#39;invio del modulo. Questa opzione è disponibile solo quando si sceglie di visualizzare una pagina di ringraziamento.
   * **Reindirizza alla pagina di ringraziamento**: abilita l&#39;opzione per sostituire la pagina contenente il modulo adattivo incorporato con la pagina di ringraziamento. In caso contrario, la pagina di ringraziamento sostituisce il modulo adattivo nel componente [!UICONTROL Forms adattivo - Incorpora], senza aggiornare i siti sottostanti nella pagina. Questa opzione è disponibile solo quando si sceglie di visualizzare una pagina di ringraziamento.
* **Usa lingua della pagina**: usa locale della pagina AEM Sites invece delle impostazioni locali del modulo adattivo.
* **Imposta stato attivo sul modulo**: selezionare questa opzione per impostare lo stato attivo sul primo campo del modulo adattivo.
* **Il modulo occupa l&#39;intera larghezza del frame**: se questa opzione è selezionata, iframe non viene utilizzato per il rendering del modulo.
* **Altezza**: specificare l&#39;altezza del contenitore. Lascia vuoto questo campo per ridimensionare automaticamente il contenitore.
* **Libreria client CSS**: specificare il percorso di una libreria client CSS.

### Publish ha aggiunto il Forms adattivo utilizzando il componente Modulo adattivo - Incorpora (v2)  {#publish-embedded-adaptive-form}

Considera i seguenti scenari per la pubblicazione di Forms adattivi aggiunti tramite il componente **[!UICONTROL Modulo adattivo - Incorpora(v2)]**:

* Quando pubblichi una pagina AEM Sites per la prima volta, i moduli aggiunti alla pagina Sites vengono pubblicati automaticamente.
* Quando modifichi un modulo adattivo aggiunto a una pagina Sites già pubblicata, pubblica manualmente il Forms adattivo corrispondente.
* Quando modifichi una pagina Sites e il corrispondente Forms adattivo, ripubblica la pagina Sites e tutti i Forms adattivi aggiunti alla pagina Sites.

### Modificare il Forms adattivo aggiunto utilizzando il componente Modulo adattivo - Incorpora (v2)  {#modifying-embedded-adaptive-form}

Per modificare la configurazione o la proprietà di un modulo adattivo, effettua una delle seguenti operazioni:

* Apri il modulo originale in un modulo adattivo nel rispettivo editor e modificalo.
* Selezionare il modulo adattivo nella pagina del sito in modalità di modifica, quindi selezionare **[!UICONTROL Modifica in una nuova finestra]**. Il modulo originale viene aperto in modalità di modifica modificabile.

## Modificare il layout di un modulo adattivo aggiunto a una pagina AEM Sites {#change-layout-af-aem-sites-page}

Nella pagina AEM Sites, la [modalità Layout](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) consente di ridimensionare un modulo adattivo creato o aggiunto a una pagina AEM Sites.

![AF-layout-support](/help/forms/assets/afsite-layoutsupport.gif)

La pagina dei siti dell’AEM contiene un riferimento al modulo adattivo. Quando traduci una pagina di AEM Sites, un modulo adattivo e le relative risorse di riferimento associate vengono tradotti automaticamente utilizzando i [progetti di traduzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) in altre lingue.

## Best practice {#best-practices}

* Intestazione e piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze utente e gli invii di moduli incorporati sono supportati e visibili nelle schede Bozze e Forms inviate nel portale Forms.

>[!MORELIKETHIS]
>
>* [Incorpora modulo adattivo basato su componenti core in una pagina Web esterna](/help/forms/embed-adaptive-form-core-components-external-web-page.md)
>* [Incorpora modulo adattivo in una pagina Web esterna](/help/forms/embed-adaptive-form-external-web-page.md)