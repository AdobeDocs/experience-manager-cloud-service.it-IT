---
title: Aggiungere o creare un modulo adattivo (componenti core) nella pagina AEM Sites
seo-title: How to add or create an Adaptive Form (Core Components) to an AEM Sites page?
description: È possibile utilizzare il modulo adattivo (componenti core) in una pagina AEM Sites per compilare e inviare un modulo senza uscire dalle pagine AEM Sites.
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 1046231f-787c-4e49-9ba0-e7dd59e41bce
source-git-commit: 1d5641dd07cc68dade247fe30bb57663872e5560
workflow-type: tm+mt
source-wordcount: '2135'
ht-degree: 2%

---

# Creare o aggiungere un modulo adattivo utilizzando l’Editor di AEM Sites {#add-an-adaptive-form-to-aem-sites-page}

È possibile creare o incorporare facilmente Adaptive Forms in una pagina AEM Sites per consentire agli utenti di compilare e inviare un modulo senza uscire dalla pagina Sites. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e di interagire contemporaneamente con il modulo.

Per creare o aggiungere un modulo adattivo a una pagina AEM Sites, è possibile scegliere uno dei metodi seguenti:

* **Creare un modulo adattivo utilizzando il componente contenitore di Forms adattivo**: La [Contenitore di moduli adattivi](#af-container-component) Il componente ti consente di creare esperienze di iscrizione digitale utilizzando i componenti Forms adattivi direttamente nell’editor AEM Sites. Questa integrazione offre un’esperienza diretta agli autori di AEM Sites che desiderano creare e gestire moduli all’interno delle proprie pagine AEM Sites.

* **Aggiungere un modulo adattivo esistente**: La [Forms adattivo - Incorporamento (v2)](#embed-existing-af) Il componente consente di aggiungere facilmente un modulo adattivo preesistente a una pagina in AEM Sites. Questa funzione migliora l&#39;adattabilità e la riutilizzabilità di Adaptive Forms. Questa integrazione offre ai clienti un modo pratico per riutilizzare l&#39;Adaptive Forms già creato.

* **Creazione guidata Forms adattiva per creare un modulo**: Utilizza la [Forms adattivo - Incorporamento (v2)](#embed-new-af) per creare un modulo adattivo dall’interno dell’editor AEM Sites utilizzando la procedura guidata Creazione modulo. Il modulo viene salvato come entità esterna. È possibile riutilizzare il modulo anche in altre pagine di Sites e moduli indipendenti.

* **Aggiungere più Forms adattivi in una pagina AEM Sites**: Per aggiungere più componenti adattivi di Forms in una pagina AEM Sites, utilizza i componenti contenitore di AEM Forms - [Forms adattivo - Incorporamento (v2)](#embed-new-af) e [Contenitore di moduli adattivi](#af-container-component). Nel caso in cui sia necessario aggiungere più moduli adattivi come div all’interno di una pagina AEM Sites, è possibile utilizzare il componente Contenitore di moduli adattivi.

È possibile utilizzare l’Editor di regole per aggiungere o controllare il comportamento dinamico dei componenti Modulo adattivo. Ad esempio, nascondere o mostrare un componente. L’Editor regole non è disponibile per i componenti Modulo non adattivo. Utilizza quindi la tua diligenza quando utilizzi componenti modulo non adattivi nel componente Contenitore di AEM Forms.

## Creare un modulo adattivo utilizzando il componente contenitore di Forms adattivo {#af-container-component}

La [!UICONTROL Contenitore di moduli adattivi] Il componente consente di creare esperienze di iscrizione digitale utilizzando i componenti di Forms adattivi nell’editor AEM Sites. È possibile creare un modulo adattivo trascinando e rilasciando i componenti del modulo.

### Prerequisiti {#prerequisites-af-container}

+++ Abilita **[!UICONTROL Contenitore Forms adattivo]** componente.

Per abilitare [!UICONTROL Contenitore Forms adattivo] nel criterio del modello, esegui i seguenti passaggi:

1. Vai a [!UICONTROL Informazioni pagina] > [!UICONTROL Modifica modello]
1. Fai clic sul pulsante [!UICONTROL Criterio] e seleziona la **[!UICONTROL Contenitore Forms adattivo]**  sotto la casella di controllo **[Nome progetto Archetype AEM] - Modulo adattivo**.
1. Fai clic su **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ Includi librerie client Forms adattive nella pagina AEM Sites

Per utilizzare i componenti Forms adattivi in una pagina AEM Sites, includi le librerie client Customheaderlibs e Customfooterlibs nella pagina AEM Sites utilizzando l’archivio Archetype/Git AEM e la pipeline di distribuzione.

1. Apri il tuo [Archivio AEM Forms Archetype o Git duplicato](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) in un editor di testo. Ad esempio, Codice di Visual Studio.
1. Accedi a `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copia il valore di `sling:resourceSuperType`. Ad esempio, il valore è `core/wcm/components/page/v3/page`.

   ![risorsa sling](/help/forms/assets/slingresource.png)

1. Crea la struttura simile nella posizione `ui.apps/src/main/content/jcr_root/apps` uguale a `core/wcm/components/page/v3/page`.

   ![struttura sovrapposta](/help/forms/assets/overlaystructure.png)

1. Aggiungi `customheaderlibs.html` e `customfooterlibs.html` file.

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

   Il customfooterlibs.html viene utilizzato per JavaScript e il customheaderlibs.html per il css.

1. [Eseguire la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) per distribuire le modifiche.

+++

### Creare un modulo adattivo utilizzando il componente contenitore di Forms adattivo {#create-af-using-af-container}


Per creare un modulo adattivo utilizzando [!UICONTROL Contenitore Forms adattivo] componente:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina **[!UICONTROL Contenitore Forms adattivo]** nella pagina.
1. Crea un modulo adattivo utilizzando i componenti Forms adattivi.
1. Salva le impostazioni.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Il modulo è pronto. Quando pubblichi la pagina AEM Sites, pubblica automaticamente il Modulo adattivo e le relative risorse di riferimento associate.

#### Configurare le proprietà dei contenitori di moduli adattivi {#configure-additional-settings-container}

Puoi personalizzare le impostazioni avanzate della [!UICONTROL Contenitore di moduli adattivi] componente. Ad esempio:

* È possibile configurare il servizio di precompilazione per caricare un modulo adattivo con valori precompilati sulla pagina di un sito.
* È possibile configurare le impostazioni del modello dati per associare il modulo adattivo a un’origine dati.
* È possibile configurare le azioni di invio per inviare i dati su Microsoft® OneDrive, Microsoft® OneDrive o altre origini dati all’invio di un modulo. Puoi anche creare e selezionare un’azione di invio personalizzata per il tuo Adaptive Forms.

Per impostare le proprietà di **[!UICONTROL Contenitore Forms adattivo]** fai clic sul ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) sulla barra delle azioni. La **[!UICONTROL Modifica contenitore Forms adattivo]** viene visualizzata la finestra di dialogo .

![Finestra di dialogo per modifica](/help/forms/assets/adaptiveformcontainer-editdialog.png)

In [!UICONTROL Modifica contenitore Forms adattivo] è possibile specificare quanto segue.
* **Scheda Base**
   * **Servizio di precompilazione**: È possibile utilizzare il servizio di precompilazione per compilare automaticamente i campi di un modulo adattivo utilizzando i dati esistenti. Quando un utente apre un modulo, i valori relativi a tali campi vengono precompilati. Per informazioni sul servizio di precompilazione, vedi [Precompilare i campi del modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **Categoria libreria client**: Specifica la [Funzioni JavaScript](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) utilizzati nelle espressioni e supportati da Adaptive Forms.
* **Modello dati**: Un modello dati consente di integrare entità e servizi da origini dati diverse in un modulo adattivo. Scegli **[!UICONTROL Modello dati modulo]** se il modulo adattivo creato prevede il recupero e la scrittura di dati da e verso più origini dati.
   * **Modello dati modulo**: Un modello dati modulo consente a un modulo adattivo di comunicare con origini dati diverse. Per informazioni sulla configurazione di un’origine dati, consulta [Configura le origini dati.](/help/forms/configure-data-sources.md)
   * **Schema**: Lo schema rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end della tua organizzazione. È possibile [associare lo schema a un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) e utilizza i relativi elementi per aggiungere contenuto dinamico a un modulo adattivo.

      >[!NOTE]
      >
      > Dopo aver configurato il modello dati Modulo, non è possibile modificare il modello di modulo associato. Tuttavia, è possibile modificare lo schema associato al modello dati del modulo.

* **Scheda Invio**

   * **Reindirizza all’URL**
      * **URL/percorso di reindirizzamento**: Specifica l’URL o il percorso a cui viene reindirizzato un modulo adattivo dopo l’invio.

      * **Invia azione**: Un’azione di invio viene attivata quando l’utente fa clic sul pulsante Invia in un modulo adattivo. È possibile [configurare l’azione di invio nel modulo adattivo](/help/forms/configuring-submit-actions.md). I moduli adattivi forniscono le seguenti azioni di invio predefinite:
         * Invia all’endpoint REST
         * Invia e-mail
         * Invia usando il modello dati modulo
         * Richiamare un flusso di lavoro AEM
         * Invia a SharePoint
         * Invia a OneDrive
         * Invia ad Azure Blob Storage

   È inoltre possibile [estendere le azioni di invio predefinite](custom-submit-action-form.md) per creare un’azione di invio personalizzata.

* **Mostra messaggio**
   * **Contenuto del messaggio**: Scrivere un messaggio utilizzando l’editor Rich Text da visualizzare durante l’invio del modulo. Questa opzione è disponibile solo quando scegli di mostrare un messaggio di ringraziamento.

## Incorporare un modulo adattivo  {#aem-container-component}

Utilizzo **[!UICONTROL Forms adattivo - Incorporamento (V2)]** È possibile incorporare un nuovo modulo adattivo o un modulo adattivo esistente nella pagina del sito. La [!UICONTROL Forms adattivo - Incorporamento (v2)] component consente di:

* [Aggiungere un modulo adattivo esistente](#embed-new-af)

* [Creare e aggiungere un nuovo modulo adattivo](#embed-existing-af)

### Prerequisiti {#prerequisites}

+++ Abilita la **Forms adattivo - Incorporamento** componente.

Per abilitare [!UICONTROL Forms adattivo - Incorporamento (v2)] nel criterio del modello, esegui i seguenti passaggi:

1. Vai a [!UICONTROL Informazioni pagina] > [!UICONTROL Modifica modello]

1. Fai clic sul pulsante [!UICONTROL Criterio] e seleziona la **[!UICONTROL Modulo adattivo - Incorporamento (v2)]** sotto la casella di controllo **[!UICONTROL [Nome progetto Archetype AEM] - Forms]** gruppo .
1. Fai clic su **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ Includi librerie client Forms adattive nella pagina AEM Sites

Quando il **[!UICONTROL Quando il modulo copre l’intera larghezza di una pagina]** è selezionata nella **[!UICONTROL Contenitori di moduli]** configura la finestra di dialogo e **Forms adattivo utilizzando i componenti core** vengono utilizzati, è necessario includere le clientlibs nella pagina del sito corrispondente.

![Gif sovrapposto](/help/forms/assets/overlaycorecomponent.gif)

Per utilizzare i componenti Forms adattivi in una pagina AEM Sites, includi le `Customheaderlibs` e `Customfooterlibs` librerie client alla pagina AEM Sites utilizzando l’archivio Archetype/Git AEM e la pipeline di distribuzione.

1. Apri il tuo [Archivio AEM Forms Archetype o Git duplicato](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) in un editor di testo. Ad esempio, Codice di Visual Studio.
1. Accedi a `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copia il valore di `sling:resourceSuperType`. Ad esempio, il valore è `core/wcm/components/page/v3/page`.

   ![risorsa sling](/help/forms/assets/slingresource.png)

1. Crea la struttura simile nella posizione `ui.apps/src/main/content/jcr_root/apps` uguale a `core/wcm/components/page/v3/page`.

   ![struttura sovrapposta](/help/forms/assets/overlaystructure.png)

1. Aggiungi `customheaderlibs.html` e `customfooterlibs.html` file.

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

   La `customfooterlibs.html` viene utilizzato per JavaScript e `customheaderlibs.html` per il CSS.

1. [Eseguire la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) per distribuire le modifiche.

+++

### Aggiungere un modulo adattivo esistente alla pagina AEM Sites {#embed-existing-af}

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina [!UICONTROL Forms adattivo - Incorporamento] nella pagina.
1. Tocca [!UICONTROL Forms adattivo - Incorporamento] nella pagina Sites e tocca ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) sulla barra delle azioni. La **[!UICONTROL Modifica Forms adattivo - Incorpora]** viene visualizzata la finestra di dialogo .
1. Sfoglia e seleziona il modulo adattivo da incorporare nel [!UICONTROL Percorso risorsa].
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina .

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)



### Creare e aggiungere un nuovo modulo adattivo alla pagina AEM Sites {#embed-new-af}

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina [!UICONTROL Forms adattivo - Incorporamento (v2)] nella pagina.
1. Fai clic sul pulsante **Plus** e si viene reindirizzati alla procedura guidata di creazione del modulo.

   ![Forms adattivo - Componente da incorporare](/help/forms/assets/aemformcontainer.png)

1. Creare un nuovo modulo adattivo da [!UICONTROL Creazione di moduli] procedura guidata.
1. La [!UICONTROL Percorso risorsa] include già il percorso di un modulo adattivo creato
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina .

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

#### Configurare un modulo adattivo - Proprietà di incorporamento (v2) {#configure-adaptive-form-embed}

Puoi personalizzare le impostazioni avanzate della [!UICONTROL Modulo adattivo - Incorporamento (v2)] componente. In [!UICONTROL Modifica Forms adattivo - Incorpora (v2)] è possibile specificare quanto segue.

* **Percorso risorsa**: Sfoglia e seleziona il modulo adattivo da incorporare. Viene compilato automaticamente se viene rilasciato dal browser Risorse.
* **Invia invio** : Selezionare l’azione da attivare all’invio del modulo. Puoi scegliere di mostrare un messaggio di ringraziamento o una pagina di ringraziamento.
   * **Mostra messaggio di ringraziamento**: Scrivere un messaggio utilizzando l’editor Rich Text da visualizzare durante l’invio del modulo. Questa opzione è disponibile solo quando scegli di mostrare un messaggio di ringraziamento.
   * **Mostra pagina di ringraziamento**: Individuare e selezionare la pagina da visualizzare durante l’invio del modulo. Questa opzione è disponibile solo quando scegli di mostrare una pagina di ringraziamento.
   * **Reindirizza alla pagina di ringraziamento**: Abilita l’opzione per sostituire la pagina contenente il modulo adattivo incorporato con la pagina di ringraziamento. In caso contrario, la pagina di ringraziamento sostituisce il Modulo adattivo nel [!UICONTROL Forms adattivo - Incorporamento] senza aggiornare i siti sottostanti la pagina. Questa opzione è disponibile solo quando scegli di mostrare una pagina di ringraziamento.
* **Usa lingua pagina**: Utilizza locale della pagina AEM Sites invece delle impostazioni internazionali del modulo adattivo.
* **Imposta lo stato attivo sul modulo**: Selezionare questa opzione per impostare lo stato attivo sul primo campo del modulo adattivo.
* **Il modulo copre l&#39;intera larghezza del frame**: Se questa opzione è selezionata, l’iframe non viene utilizzato per il rendering del modulo.
* **Altezza**: Specifica l’altezza del contenitore. Lascia vuoto per ridimensionare automaticamente il contenitore.
* **Libreria client CSS**: Specifica il percorso di una libreria client CSS.

### È stata aggiunta la possibilità di pubblicare Forms adattivo utilizzando il componente Modulo adattivo - Incorpora (v2)  {#publish-embedded-adaptive-form}

Considera i seguenti scenari per la pubblicazione di Forms adattivo aggiunto utilizzando **[!UICONTROL Modulo adattivo - Incorporamento (v2)]** componente:

* Quando si pubblica una pagina AEM Sites per la prima volta, i moduli aggiunti alla pagina Sites vengono pubblicati automaticamente.
* Quando modifichi un modulo adattivo aggiunto a una pagina Sites già pubblicata, pubblica manualmente il corrispondente Forms adattivo.
* Quando modifichi una pagina Sites e il corrispondente Forms adattivo, ripubblica la pagina Sites e tutti i Forms adattivi aggiunti alla pagina Sites.

### Modifica del componente Forms adattivo aggiunto utilizzando il componente Modulo adattivo - Incorpora (v2)  {#modifying-embedded-adaptive-form}

Per modificare una configurazione o proprietà di un modulo adattivo, effettuare una delle seguenti operazioni:

* Apri il modulo originale in un modulo adattivo nel rispettivo editor e modificalo.
* Tocca Modulo adattivo dalla pagina del sito in modalità di modifica, quindi tocca **[!UICONTROL Modifica in una nuova finestra]**. Il modulo originale viene aperto in modalità di modifica che è possibile modificare.

## Modificare il layout di un modulo adattivo aggiunto a una pagina AEM Sites {#change-layout-af-aem-sites-page}

Nella pagina AEM Sites, la [Modalità Layout](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) consente di ridimensionare un modulo adattivo creato o aggiunto a una pagina AEM Sites.

![Supporto di layout AF](/help/forms/assets/afsite-layoutsupport.gif)

AEM pagina siti mantiene un riferimento al modulo adattivo. Quando traduci una pagina AEM Sites, traduce automaticamente un Modulo adattivo e le relative risorse di riferimento associate utilizzando [progetti di traduzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) in altre lingue.

## Best practice {#best-practices}

* Le intestazioni e i piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze degli utenti e gli invii dei moduli incorporati sono supportati e visibili nelle schede Bozze e Inviate Forms sul portale Forms.