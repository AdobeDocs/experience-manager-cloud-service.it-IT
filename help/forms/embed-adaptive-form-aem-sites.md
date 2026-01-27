---
title: Come si aggiunge un modulo adattivo a una pagina di AEM Sites?
description: Incorpora facilmente Forms adattivo in una pagina AEM Sites o in una pagina web ospitata al di fuori di AEM.
feature: Adaptive Forms
role: Admin, User, Developer
Keywords: Forms AEM Sites, Embed Form to a Sites page, Adaptive Forms AEM Sites, Embed Adaptive Forms to AEM Page, Embed Forms in an AEM Sites page
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '3280'
ht-degree: 0%

---

# Incorporare un modulo adattivo in una pagina AEM Sites {#embed-an-adaptive-form-to-aem-sites-page}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-aem-sites.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |


## Panoramica {#overview}

AEM Forms consente agli sviluppatori di moduli di incorporare facilmente Forms adattivo in una pagina AEM Sites o in una pagina web ospitata al di fuori di AEM. Il modulo adattivo incorporato è completamente funzionante e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e interagire contemporaneamente con il modulo. Questo consente agli utenti di compilare e inviare i moduli in modo semplice e senza mai uscire dalla pagina in cui si trovano. Questa integrazione consente di riutilizzare in modo pratico i Forms adattivi già creati.

È possibile utilizzare l’Editor pagina di AEM per incorporare rapidamente più moduli nelle pagine AEM Sites. L’utilizzo dell’Editor pagina di AEM consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno di una pagina Sites, sfruttando la potenza dei componenti di Adaptive Forms, tra cui comportamento dinamico, convalide, integrazione di dati, generazione di documenti di record e automazione dei processi aziendali. Consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

AEM Forms fornisce **[!UICONTROL Contenitore modulo adattivo]** e **[!UICONTROL Componenti Forms adattivo - Incorpora(v2)]**. È possibile utilizzare il componente **[!UICONTROL Forms adattivo - Incorpora(v2)]** per aggiungere un modulo adattivo esistente o creare un modulo utilizzando l&#39;editor di Forms adattivo, mentre **[!UICONTROL Contenitore di moduli adattivi]** consente di creare un nuovo modulo all&#39;interno di un frammento di esperienza o di una pagina AEM Sites.

![Esempio di modulo adattivo in una pagina AEM Sites](/help/forms/assets/adaptive-form-in-sites-page.png)

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). 

## Why embed an Adaptive Form in AEM Sites page or AEM Experience Fragment? 

Using **[!UICONTROL Adaptive Forms – Embed(v2)]** in AEM Page Editor lets you create seamless data capture experiences within a Sites page using the power of Adaptive Forms components including dynamic behavior, validations, data integration, generate document of record and business process automation. It also lets you use various features of AEM Sites pages like, versioning, targeting, translation, and multi-site manager, enhancing the overall form creation and management experience. Let's explore some of these features:

* **Versioning:** AEM Sites pages offer [robust versioning capabilities](/help/sites-cloud/authoring/sites-console/page-versions.md), allowing you to track and manage different versions of your forms. This enables you to make changes and enhancements to forms while maintaining the ability to roll back to previous versions if needed. Versioning ensures a controlled and organized approach to form development and evolution.
* **Targeting (Integration with Adobe Target):** With AEM Sites pages targeting capabilities, you can also [personalize the form experience for different audiences](/help/sites-cloud/integrating/integrating-adobe-target.md). By using user segments and targeting criteria, you can tailor the form's content, design, or behavior to specific groups of users. This enables you to provide a personalized and relevant form experience, increasing engagement and conversion rates.
* **Translation:** AEM Sites [seamless integration with translation services](/help/sites-cloud/administering/translation/overview.md), allowing you to translate forms into multiple languages easily. This feature simplifies the localization process, ensuring that your forms are accessible to a global audience. You can manage translations efficiently within AEM translation projects, reducing time and effort required for multilingual form support. See considerations section for more information on translation.  
* **Multi-site Management and Live Copy:** AEM Sites provide robust [Multi-site Management and Live Copy capabilities](/help/sites-cloud/administering/msm/overview.md), enabling you to create and manage multiple websites within a single environment. This feature now lets you reuse forms across different sites, ensuring consistency and reducing duplication efforts. With centralized control and management, you can efficiently maintain and update forms across multiple websites.
* **Themes:** AEM Sites pages provide a framework for designing and maintaining consistent visual styles across multiple web pages. These define colors, fonts, style sheets, and other visual elements that contribute to the overall look and feel of the website. [You can use the themes designed for an AEM Sites page for an Adaptive Form, saving time and effort](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes). 
* **Tagging:** AEM Sites pages allow you to [assign tags or labels to a page, an asset, or other content](/help/implementing/developing/introduction/tagging-framework.md). Tags are keywords or metadata labels that provide a way to categorize and organize content based on specific criteria. You can assign one or more tags to pages, assets, or any other content items within AEM to improve search and categorize the assets. 
* **Locking and Unlocking content:** AEM Sites allow users to [control access and modifications to pages](/help/sites-cloud/authoring/page-editor/edit-content.md) within the AEM Sites environment. When a page is locked, it means that it is protected from unauthorized changes or edits by other users. Only the user who has locked the content or a designated administrator can unlock it to allow modifications. 

In addition, Adaptive Forms in AEM Page Editor use [Adaptive Forms Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it#features). These Core Components provide a standard and easier methods to style and customize the components, identical to [AEM Sites WCM Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it).

-->

## Come si crea o si incorpora un modulo adattivo nella pagina di AEM Sites o in un frammento di esperienza AEM? {#various-options-to-create-or-embed-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Puoi sfruttare appieno questa funzione utilizzando le seguenti opzioni:

* **[Crea un modulo adattivo utilizzando modelli approvati e incorporalo in una pagina AEM Sites](#embed-form-using-adaptive-form-wizzard-aem-sites):** Puoi utilizzare modelli preapprovati per creare e incorporare rapidamente Forms adattivo in linea con le linee guida di branding e gli standard di progettazione della tua organizzazione.

* **[Incorpora i moduli esistenti in una pagina AEM Sites](#embed-an-adaptive-form-in-sites-editor):** Puoi integrare facilmente i moduli già creati nei tuoi siti Web, consentendo ai visitatori di interagire direttamente con essi.

* **[Convertire un modulo adattivo incorporato in un frammento di esperienza](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Convertire un modulo adattivo incorporato aggiunto a una pagina AEM Sites in un frammento di esperienza per riutilizzare il modulo in più pagine AEM Sites.

* **[Crea e aggiungi un modulo adattivo personalizzato a una pagina di AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** Puoi utilizzare il componente **[!UICONTROL Contenitore modulo adattivo]** per creare un nuovo modulo da zero, adattandolo in modo specifico alle tue esigenze e preferenze di progettazione.

* **[Crea e aggiungi un modulo adattivo personalizzato a un frammento di esperienza](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor):** Puoi estendere la portata dei moduli aggiungendoli ai frammenti di esperienza AEM, in modo da riutilizzarli in più pagine o siti.

* **Aggiungere più moduli a una pagina AEM Sites o a un frammento di esperienza:** È possibile creare o aggiungere più Forms adattivi a una pagina AEM Sites per fornire più scelte agli utenti in base alle loro preferenze e ai loro requisiti. È possibile utilizzare l’Editor pagina di AEM per incorporare rapidamente più moduli nelle pagine AEM Sites. Puoi utilizzare più volte il componente **[!UICONTROL Contenitore modulo adattivo]** per aggiungere Forms adattivo a una pagina di AEM Sites. Puoi utilizzare il componente **[!UICONTROL Forms adattivo - Incorpora]** più volte in una pagina di AEM Sites, solo se è selezionata l&#39;opzione **[!UICONTROL Modulo occupa l&#39;intera larghezza del frame]**. Se l&#39;opzione **[!UICONTROL Modulo occupa l&#39;intera larghezza del frame]** non è selezionata, la pagina di AEM Sites supporta un solo modulo adattivo per esistere senza un iframe. Per aggiungere altro Forms adattivo utilizzando il componente **[!UICONTROL Forms adattivo - Incorpora]**, seleziona **[!UICONTROL Il modulo copre l&#39;intera larghezza del frame]**.

## Considerazioni per incorporare un modulo adattivo in una pagina AEM Sites o in un frammento esperienza AEM {#consideration}

* Quando crei o aggiungi un modulo utilizzando il componente **[!UICONTROL Forms adattivo - Incorpora(v2)]**, i moduli vengono tradotti e localizzati utilizzando il flusso di traduzione AEM Forms. In questo caso, viene mantenuto un singolo modulo a cui viene fatto riferimento in tutte le copie in lingua delle pagine di Sites. Il componente **[!UICONTROL Forms adattivo - Incorpora(v2)]** non fornisce l&#39;accesso a varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

* Quando si utilizza il **[!UICONTROL Contenitore modulo adattivo]** per creare un modulo, i moduli vengono tradotti e localizzati attraverso il flusso di traduzione AEM Sites. Per ogni lingua viene generata una copia separata (copia per lingua) della pagina del sito e dei moduli corrispondenti e, quando un autore di contenuto modifica una regola in un modulo nella pagina padre, le stesse modifiche devono essere apportate in tutte le copie per lingua del modulo. **[!UICONTROL Contenitore modulo adattivo]** consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.


## Requisiti per incorporare un modulo adattivo nella pagina AEM Sites o nel frammento di esperienza AEM {#before-you-start-embedding-an-adaptive-form}

Prima di iniziare a incorporare un nuovo modulo adattivo o un modulo adattivo preesistente utilizzando **[!UICONTROL Forms adattivo - Incorpora(v2)]**, aggiungi **Librerie client Forms adattive** alla tua pagina AEM Sites:


### Aggiungere librerie client Forms adattive alla pagina o al frammento di esperienza AEM Sites

Quando l&#39;opzione **[!UICONTROL Quando il modulo copre l&#39;intera larghezza di una pagina]** è selezionata nella finestra di dialogo di configurazione **[!UICONTROL Contenitori modulo]** e vengono utilizzati Forms adattivi, è necessario includere le librerie client nella pagina del sito corrispondente.

![Se il modulo copre l&#39;intera larghezza di una pagina, l&#39;opzione è selezionata e vengono utilizzati moduli adattivi](/help/forms/assets/overlaycorecomponent.gif)

**Scenario 1: Utilizzo Di Componenti Pagina Sites Separati**

Aggiungi le **librerie client Customheaderlibs** e **Customfooterlibs** alla pagina AEM Sites utilizzando la pipeline di distribuzione. Per aggiungere le librerie client:

1. Accedi e clona l&#39;[archivio Git AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html?lang=it).
2. Apri la cartella dell’archivio Git di AEM Cloud Service in un editor di testo del piano. Ad esempio, Microsoft® Visual Code.
3. Aprire il file `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` e aggiungere il codice seguente al file:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

4. Aprire il file `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` e aggiungere il codice seguente al file:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

5. Aprire il file `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` e aggiungere il codice seguente al file:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

6. Aprire il file `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` e aggiungere il codice seguente al file:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

7. [Esegui la pipeline di distribuzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=it) per distribuire le librerie client nell&#39;ambiente AEM as a Cloud Service.

>[!NOTE]
>
> Hardcode la libreria client della funzione personalizzata solo quando è richiesta per tutti i moduli. Per le librerie che differiscono in base al tipo di modulo, aggiungerle tramite i criteri della pagina del modello, come illustrato nella sezione successiva.

**Caso 2: utilizzo del componente per la pagina Same Sites**

Includi le librerie client di runtime o le librerie di funzioni personalizzate nel criterio pagina del modello utilizzato per la creazione di pagine con moduli.

1. Apri la pagina AEM Sites o il frammento di esperienza per la modifica. Per aprire la pagina per la modifica, selezionarla e fare clic su **[!UICONTROL Modifica]**.
2. Apri il modello della pagina Sites o Frammento esperienza. Per aprire il modello, vai a **[!UICONTROL Informazioni pagina]** ![Informazioni pagina](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Modifica modello]**. Apre il modello corrispondente nell’editor modelli.
3. Vai alla sezione **[!UICONTROL Informazioni pagina]** ![Informazioni pagina](/help/forms/assets/Smock_Properties_18_N.svg) del modello e seleziona l&#39;opzione **[!UICONTROL Criteri pagina]**. Vengono visualizzate le proprietà del modello AEM Sites, in cui è possibile definire funzioni personalizzate o librerie client di runtime.
4. Fai clic sul pulsante **[!UICONTROL Aggiungi]** nella scheda **[!UICONTROL Proprietà]** per aggiungere nuove librerie di funzioni personalizzate o le librerie di runtime.
5. Fai clic su **[Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3476178?quality=12&learn=on)

### Abilita Forms adattivo: incorpora(v2) per la pagina o il frammento di esperienza AEM Sites

Per abilitare il componente **[!UICONTROL Forms adattivo - Incorpora(v2)]** nel criterio del modello, eseguire la procedura seguente:

1. Apri la pagina AEM Sites o il frammento di esperienza per la modifica. Per aprire la pagina per la modifica, selezionarla e fare clic su **[!UICONTROL Modifica]**.
1. Apri il modello della pagina Sites o Frammento esperienza. Per aprire il modello, vai a **[!UICONTROL Informazioni pagina]** ![Informazioni pagina](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Modifica modello]**. Apre il modello corrispondente nell’editor modelli.
1. Nella visualizzazione Struttura fare clic sull&#39;icona **[!UICONTROL Criteri]** ![Criteri](/help/forms/assets/Smock_FeedManagement_18_N.svg) nella barra dei menu. Nell&#39;elenco **[!UICONTROL Componenti consentiti]** e selezionare la casella di controllo **[!UICONTROL Forms adattivo - Incorpora(v2)]** in **[Nome progetto archetipo AEM] - Modulo adattivo**.
1. Fai clic su **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

## Incorporare un modulo adattivo utilizzando il componente Forms adattivo - Incorpora(v2) {#embed-an-adaptive-form-in-sites-editor-or-experience-fragment}

Utilizza il componente **[!UICONTROL Forms adattivo - Incorpora(v2)]** per creare un modulo adattivo direttamente nell&#39;editor di AEM Sites utilizzando la procedura guidata per la creazione di moduli. Il modulo risultante viene salvato come entità esterna, consentendo il suo riutilizzo in altre pagine Sites e moduli autonomi. Puoi incorporare un modulo nuovo di zecca da zero, personalizzandolo in base a specifici requisiti e preferenze di progettazione, direttamente in una pagina AEM Sites o in Frammento esperienza. Per i moduli monouso, si consiglia di eseguire l’authoring diretto su una pagina AEM Sites, mentre i frammenti di esperienza sono ideali per i moduli che devono essere riutilizzati su più pagine del sito web.

Puoi incorporare facilmente un nuovo modulo utilizzando **[!UICONTROL Forms adattivo - Incorpora(v2)]**.  Ad esempio, immagina di incorporare un nuovo modulo per i contatti in una pagina AEM Sites o in un frammento di esperienza AEM. Eventuali aggiornamenti o modifiche apportate al modulo di contatto all’interno della pagina AEM Sites o al frammento di esperienza si applicano automaticamente a tutte le pagine in cui viene distribuito. Questo semplifica la gestione dei moduli del sito web, garantendo un’esperienza utente fluida e semplificando al contempo il processo complessivo.

Utilizzando **[!UICONTROL Forms adattivo - Incorpora(v2)]**, puoi:

* [Incorporare un nuovo modulo utilizzando la procedura guidata Forms adattivo nella pagina AEM Sites](#embed-form-using-adaptive-form-wizzard-aem-sites)
* [Incorporare un nuovo modulo utilizzando la procedura guidata Forms adattivo in un frammento di esperienza](#embed-form-using-adaptive-form-wizzard-experience-fragment)
* [Incorporare un modulo adattivo esistente in una pagina AEM Sites](#embed-an-adaptive-form-in-sites-editor)
* [Incorporare un modulo esistente in un frammento di esperienza](#embed-an-adaptive-form-in-experience-fragment)
* [Convertire un modulo adattivo nella pagina di AEM Sites in un frammento di esperienza](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Incorporare un nuovo modulo utilizzando la procedura guidata Forms adattivo nella pagina AEM Sites {#embed-form-using-adaptive-form-wizzard-aem-sites}

I passaggi per incorporare un nuovo modulo in una pagina AEM Sites sono i seguenti:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina il componente **[!UICONTROL Forms adattivo - Incorpora(v2)]** sulla pagina.
1. Fai clic sull&#39;icona **Plus** per reindirizzarti alla procedura guidata di creazione del modulo.

   ![Forms adattivo - Componente di incorporamento](/help/forms/assets/aemformcontainer.png)

1. Crea un nuovo modulo adattivo dalla procedura guidata **[!UICONTROL Creazione modulo]**.
Il **[!UICONTROL percorso risorsa]** include già il percorso di un modulo adattivo creato
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

Successivamente, è possibile [impostare l&#39;azione di invio](/help/forms/configuring-submit-actions.md) e le proprietà avanzate di un modulo adattivo incorporato utilizzando la procedura guidata di creazione del modulo.


### Incorporare un nuovo modulo utilizzando la procedura guidata Forms adattivo in un frammento di esperienza {#embed-form-using-adaptive-form-wizzard-experience-fragment}

I passaggi per incorporare un nuovo modulo in un frammento di esperienza sono i seguenti:

1. Apri il frammento di esperienza in modalità di modifica.
1. Dal pannello del browser Componenti, trascina il componente **[!UICONTROL Forms adattivo - Incorpora(v2)]** sulla pagina.
1. Fai clic sull&#39;icona **Plus** per reindirizzarti alla procedura guidata di creazione del modulo.

   ![Forms adattivo - Componente di incorporamento](/help/forms/assets/aemformcontainer.png)

1. Crea un nuovo modulo adattivo dalla procedura guidata **[!UICONTROL Creazione modulo]**.
Il **[!UICONTROL percorso risorsa]** include già il percorso di un modulo adattivo creato
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nel frammento di esperienza.

Successivamente, è possibile [impostare l&#39;azione di invio](/help/forms/configuring-submit-actions.md) e le proprietà avanzate di un modulo adattivo incorporato utilizzando la procedura guidata di creazione del modulo.

### Incorporare un modulo adattivo esistente in una pagina AEM Sites {#embed-an-adaptive-form-in-sites-editor}

Con il componente **[!UICONTROL Forms adattivo - Incorpora(v2)]** puoi integrare facilmente un modulo adattivo preesistente in una pagina in AEM Sites. Questa funzione migliora in modo significativo l’adattabilità e la riutilizzabilità di Adaptive Forms, offrendo ai clienti un modo pratico per riutilizzare i moduli già creati. Immagina ad esempio di incorporare un modulo per i contatti in una pagina di AEM Sites, eliminando la necessità di ricreare il modulo più volte.

Per incorporare un modulo adattivo esistente in una pagina Sites:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Trascina il componente **[!UICONTROL Forms adattivo - Incorpora(v2)]** dal browser Componenti alla pagina Sites.
1. Seleziona il componente **[!UICONTROL Forms adattivo - Incorpora]** nella pagina Sites e seleziona ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg) nella barra delle azioni. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica Forms adattivo - Incorpora(v2)]**.
1. Sfoglia e seleziona il modulo adattivo da incorporare nel **[!UICONTROL percorso risorsa]**.
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

Successivamente, è possibile [impostare l&#39;azione di invio](/help/forms/configuring-submit-actions.md) e le proprietà avanzate di un modulo adattivo incorporato utilizzando la procedura guidata di creazione del modulo.

### Incorporare un modulo adattivo esistente in un frammento di esperienza {#embed-an-adaptive-form-in-experience-fragment}

Puoi anche estendere l’accessibilità dei moduli incorporandoli in Frammento esperienza AEM. Per incorporare un modulo adattivo in un frammento di esperienza:

1. Apri un frammento di esperienza in modalità di modifica.
1. Trascina il componente **[!UICONTROL Forms adattivo - Incorpora(v2)]** dal browser Componenti al frammento di esperienza.
1. Seleziona il componente **[!UICONTROL Forms adattivo - Incorpora]** nel frammento di esperienza e seleziona ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg) nella barra delle azioni. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica Forms adattivo - Incorpora(v2)]**.
1. Sfoglia e seleziona il modulo adattivo da incorporare nel **[!UICONTROL percorso risorsa]**.
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nel frammento di esperienza.

Successivamente, è possibile [impostare l&#39;azione di invio](/help/forms/configuring-submit-actions.md) e le proprietà avanzate di un modulo adattivo incorporato utilizzando la procedura guidata di creazione del modulo.

### Convertire un modulo in una pagina di AEM Sites in un frammento di esperienza {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

È possibile convertire un modulo adattivo esistente in un editor di pagine Sites in un frammento di esperienza per riutilizzare il modulo in più pagine o siti.

Per convertire un modulo adattivo nella pagina di AEM Sites in un frammento di esperienza:

1. Apri la pagina AEM Sites contenente il modulo adattivo (nel componente Contenitore Forms adattivo) in modalità di modifica.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Sulla barra dei menu, seleziona l&#39;icona ![Converti in variante di frammento di esperienza](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Converti in variante di frammento di esperienza.

   ![Fai clic sul logo dell&#39;archivio file per convertire un modulo adattivo nella pagina di AEM Sites in un frammento di esperienza](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Viene visualizzata una finestra di dialogo per convertire il contenitore Moduli adattivi in un nuovo frammento di esperienza o aggiungerlo a un frammento di esperienza esistente.

1. Nella finestra di dialogo **[!UICONTROL Converti in variante di esperienza]**, imposta i valori per le seguenti opzioni:

   * **Azione:** Seleziona questa opzione per creare un frammento di esperienza o Aggiungi a un frammento di esperienza esistente.
   * **Percorso principale:** Specificare il percorso della cartella in cui ospitare il frammento di esperienza. L’opzione è disponibile solo per la creazione di un nuovo frammento di esperienza.
   * **Modello:** Specifica il percorso del modello Frammento esperienza. Se non disponi di un modello di Frammento esperienza, [crealo](/help/implementing/developing/extending/experience-fragments.md). L’opzione è disponibile solo per aggiungere un modulo adattivo a un frammento di esperienza esistente.
   * **Titolo frammento:** Specifica il titolo del frammento esperienza. Il titolo identifica in modo univoco un frammento esperienza.
   * **Tag frammento:** Specifica il tag del frammento di esperienza. Il tag identifica in modo univoco la categoria di un frammento di esperienza.

## Configurare le proprietà di Adaptive Form-Embed(v2)

È possibile personalizzare le impostazioni avanzate del componente **[!UICONTROL Modulo adattivo - Incorpora(v2)]**. Nella finestra di dialogo **[!UICONTROL Modifica Forms adattivo - Incorpora]** puoi specificare quanto segue:

* **Percorso risorsa**: seleziona un modulo adattivo da incorporare. Viene compilato automaticamente se viene rilasciato dal browser Assets.
* **Invio post** : seleziona l&#39;azione da attivare all&#39;invio del modulo. Puoi scegliere di visualizzare un messaggio di ringraziamento o una pagina di ringraziamento.
   * **Mostra messaggio di ringraziamento**: scrivi un messaggio utilizzando l&#39;editor Rich Text per visualizzarlo all&#39;invio del modulo. Questa opzione è disponibile solo quando si sceglie di visualizzare un messaggio di ringraziamento.
   * **Mostra pagina di ringraziamento**: sfoglia e seleziona la pagina da visualizzare all&#39;invio del modulo. Questa opzione è disponibile solo quando si sceglie di visualizzare una pagina di ringraziamento.
   * **Reindirizza alla pagina di ringraziamento**: abilita l&#39;opzione per sostituire la pagina contenente il modulo adattivo incorporato con la pagina di ringraziamento. In caso contrario, la pagina di ringraziamento sostituisce il modulo adattivo nel componente **[!UICONTROL Forms adattivo - Incorpora(v2)]**, senza aggiornare i siti sottostanti alla pagina. Questa opzione è disponibile solo quando si sceglie di visualizzare una pagina di ringraziamento.
   * **Messaggio di ringraziamento**: breve conferma o riconoscimento visualizzato sullo schermo dopo l&#39;invio di un modulo.
   * **Pagina ringraziamento**: sfoglia e seleziona la pagina da visualizzare dopo aver inviato correttamente un modulo.

* **Usa lingua della pagina**: usa locale della pagina AEM Sites invece delle impostazioni locali del modulo adattivo. Questa opzione è applicabile solo per il modulo adattivo (Foundation).
* **Imposta stato attivo sul modulo**: selezionare questa opzione per impostare lo stato attivo sul primo campo del modulo adattivo. Questa opzione è applicabile solo per il modulo adattivo (Foundation).
* **Tema**: seleziona un tema che definisca lo stile dei componenti del modulo adattivo. Lo stile include proprietà di aspetto quali lo stile del carattere, il colore di sfondo, le dimensioni e l&#39;allineamento. Questa opzione è applicabile solo per il modulo adattivo (Foundation).

  >[!NOTE]
  >
  > È possibile utilizzare le opzioni **Usa lingua pagina**, **Imposta stato attivo su modulo** e **Tema** solo per modulo adattivo (Foundation).

* **Il modulo occupa l&#39;intera larghezza del frame**:
Un frame in linea (iframe) è un elemento di HTML che carica un modulo adattivo in una pagina AEM Sites.

   * Se la casella di controllo **[!UICONTROL Modulo occupa l&#39;intera larghezza della cornice]** è selezionata, un modulo adattivo occupa l&#39;intera larghezza del contenitore in cui viene inserito. In questo caso, non viene utilizzato un iframe per eseguire il rendering del modulo. Il layout e il design di un modulo adattivo si adattano a coprire l’intera larghezza del contenitore, rendendolo reattivo e in grado di adattarsi a diverse dimensioni dello schermo. Questa opzione consente di incorporare più Forms adattivi all’interno di una pagina AEM Sites.

         >[ !NOTA]
         >
         > Per incorporare più moduli in una pagina AEM Sites, seleziona **[!UICONTROL Il modulo occupa l&#39;intera larghezza della casella di controllo frame]**.
     
   * Se la casella di controllo **[!UICONTROL Modulo copre l&#39;intera larghezza del frame]** non è selezionata, un modulo adattivo non copre l&#39;intera larghezza del contenitore. Viene invece utilizzato un iframe per eseguire il rendering del modulo, che non può essere esteso oltre una larghezza specifica. Questo approccio è utile quando un modulo adattivo ha limiti definiti e deve coesistere con altri componenti AEM adiacenti all’interno del contenitore. Se questa opzione non è selezionata, è possibile incorporare un solo Forms adattivo nella pagina AEM Sites senza un iframe.

         >[!NOTE]
         >
         > La pagina AEM Sites supporta un solo modulo adattivo per esistere senza un iframe. Per aggiungere altro Forms adattivo utilizzando il componente **[!UICONTROL Forms adattivo - Incorpora]**, seleziona **[!UICONTROL Il modulo copre l&#39;intera larghezza del frame]**.
     
* **Altezza**: specificare l&#39;altezza del contenitore. Lascia vuoto questo campo per ridimensionare automaticamente il contenitore.
* **Libreria client CSS**: specificare il percorso di una libreria client CSS.

<!--
In AEM Sites page, you can add an Adaptive Form using:

* **Adaptive Forms - Embed component**
   Adaptive Forms - Embed component enables AEM Sites authors to include an existing Adaptive Form within an AEM Sites page, thereby enhancing the reusability of adaptive forms. Existing Adaptive Forms can be used standalone or embedded in the site page. This integration provides a convenient way for customers to reuse Adaptive Forms they have already created.

* **Asset browser**
  All the forms are available under Assets. You can drag-drop the form as an asset on your page.

## Prerequisites {#prerequisites}

 To embed an Adaptive Form in an AEM Sites page that uses an editable template, ensure that the AEM Form component is configured as an allowed component in the associated template. 

In case **Adaptive Forms - Embed component** is not visible in the **Component browser panel** of AEM sites page, perform the following steps as illustrated in the video.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

In case Sites page is using a static template, you need to configure it in the paragraph system of the site page. 

## Embedding an Adaptive Form {#af-component}

To embed an Adaptive Form using the **[!UICONTROL Adaptive Forms - Embed]** component:

1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the [!UICONTROL Adaptive Forms - Embed] component on the page. Alternatively, you can search for an Adaptive Form in the Assets browser and drag-drop it onto the Sites page. You can add a new Adaptive Form or embed an existing Adaptive Form. 

   >[!NOTE]
   >
   >Multiple Adaptive Forms - Embed components on a page are not supported.

1. To create and embed a new form, on the component toolbar, select the **Create Form** icon. A window to create the form opens. 

1. Select the embedded Adaptive Forms - Embed component in the sites page, and then select ![settings_icon](assets/settings_icon.png) on the action bar. The **[!UICONTROL Edit Adaptive Forms - Embed]** dialog opens.
1. In the Edit Adaptive Forms - Embed dialog, specify the following.

    **Asset Type:** Select the type of asset to embed. 
    * **Asset Path**: Browse and select the Adaptive Form to embed. It is auto-populated if you dropped it from the Assets browser.
    * **Post Submission** : Select the action to trigger on form submission. You can choose to show a thank you message or a thank you page.
        * Show

        * **Thank You Message**: Write a message using the rich text editor to show on form submission. This option is available only when you choose to show a thank you message.
        * **Thank You Page**: Browse and select the page to display on form submission. This option is available only when you choose to show a thank you page.
           * **Redirect to thank you page**: Enable the option to replace the page containing the embedded Adaptive Form with thank you page. Otherwise, the thank you page replaces the Adaptive Form in the [!UICONTROL Adaptive Forms - Embed] component, without refreshing underlying sites the page. This option is available only when you choose to show a thank you page.
    * **Use Page Language**: Use local of the AEM Sites page instead locale of Adaptive Form.
    * **Set Focus on Form**: Select to set the focus on the first field of the Adaptive Form.
    * **Theme**: Select a theme that defines styling for components of your Adaptive Form. Styling includes appearance properties such as font style, background color, dimensions, and alignment.
    * **Form covers entire width of the frame**: If checked, iframe is not used to render the form. 
    * **Height**: Specify the height of the container. Leave it blank to automatically resize the container.
    * **CSS Client library**: Specify path to a CSS client library.

1. Save the settings. The Adaptive Form  is now embedded in the page.


AEM site also lets you create an Adaptive Form on the fly using the Adaptive Forms - Embed component. Follow the steps to create an Adaptive Form using the **Adaptive Forms - Embed component** on AEM sites page:
1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the Adaptive Forms - Embed component on the page.
1. Click the **Plus** icon and you are redirected to the form creation wizard.

    ![Adaptive Forms - Embed Component](/help/forms/assets/aemformcontainer.png)

1. You can now embed an Adaptive Form on AEM site pages using the [!UICONTROL AEM Forms Container Component].
-->

## Pubblicare un modulo adattivo incorporato {#publishing-embedded-adaptive-form}

Prendiamo in considerazione i seguenti scenari per la pubblicazione di un modulo adattivo incorporato nella pagina dei siti di AEM:

* Se pubblichi la pagina dei siti di AEM per la prima volta e include un modulo adattivo incorporato, pubblica la pagina dei siti e la risorsa incorporata.
* Se hai modificato solo il modulo adattivo incorporato in una pagina del sito pubblicata, pubblica la risorsa originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se hai modificato la pagina Sites e il modulo adattivo incorporato, ripubblica la pagina Sites e la risorsa incorporata.

## Modifica modulo adattivo incorporato  {#modifying-embedded-adaptive-form}

Per modificare una configurazione o una proprietà del modulo adattivo incorporato, effettuate una delle seguenti operazioni.

* Apri il modulo originale in un modulo adattivo nel rispettivo editor e modificalo.
* Selezionare il modulo adattivo nella pagina del sito in modalità di modifica, quindi selezionare **[!UICONTROL Modifica in una nuova finestra]**. Il modulo originale viene aperto in modalità di modifica modificabile.

>[!NOTE]
>
>Le modifiche apportate nel modulo adattivo originale si riflettono automaticamente nel modulo incorporato. Tuttavia, ripubblica il modulo adattivo o la pagina del sito per riflettere le modifiche nella pagina pubblicata.

## Best practice {#best-practices}

Quando incorpori Forms adattivo nelle pagine dei siti di AEM, considera gli aspetti seguenti:

* Intestazione e piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze utente e gli invii di moduli incorporati sono supportati e visibili nelle schede Bozze e Forms inviate nel portale Forms.
* L’azione di invio configurata nel modulo originale viene mantenuta nel modulo incorporato.
* Se hai configurato Adobe Analytics per il modulo originale, i dati di analisi del modulo incorporato vengono acquisiti in Adobe Analytics. Tuttavia, non è disponibile nel rapporto di analisi di Forms.

## Consulta anche {#see-also}

* [Creare un modulo autonomo](/help/forms/creating-adaptive-form-core-components.md)
* [Creare un modulo direttamente in una pagina di AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
