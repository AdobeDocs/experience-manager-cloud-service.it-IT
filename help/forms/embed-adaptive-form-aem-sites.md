---
title: Come si aggiunge un modulo adattivo a una pagina di AEM Sites?
description: Incorpora facilmente Forms adattivo in una pagina AEM Sites o in una pagina web ospitata al di fuori dell’AEM.
feature: Adaptive Forms
Keywords: Forms AEM Sites, Embed Form to a Sites page, Adaptive Forms AEM Sites, Embed Adaptive Forms to AEM Page, Embed Forms in an AEM Sites page
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '3164'
ht-degree: 0%

---

# Incorporare un modulo adattivo in una pagina dei siti AEM {#embed-an-adaptive-form-to-aem-sites-page}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-aem-sites.html) |
| AEM as a Cloud Service | Questo articolo |


## Panoramica {#overview}

AEM Forms consente agli sviluppatori di moduli di incorporare facilmente Forms adattivo in una pagina AEM Sites o in una pagina web ospitata al di fuori dell’AEM. Il modulo adattivo incorporato è completamente funzionante e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e interagire contemporaneamente con il modulo. Questo consente agli utenti di compilare e inviare i moduli in modo semplice e senza mai uscire dalla pagina in cui si trovano. Questa integrazione consente di riutilizzare in modo pratico i Forms adattivi già creati.

È possibile utilizzare l’Editor pagina AEM per incorporare rapidamente più moduli nelle pagine AEM Sites. L’editor di pagine AEM consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno di una pagina Sites, sfruttando la potenza dei componenti di Adaptive Forms, tra cui comportamento dinamico, convalide, integrazione dei dati, generazione di documenti di record e automazione dei processi aziendali. Consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

AEM Forms fornisce **[!UICONTROL Contenitore modulo adattivo]** e **[!UICONTROL Forms adattivo - Incorpora(v2)]** componenti. È possibile utilizzare **[!UICONTROL Forms adattivo - Incorpora(v2)]** per aggiungere un modulo adattivo esistente o creare un modulo utilizzando l’editor di Forms adattivo, mentre **[!UICONTROL Contenitore modulo adattivo]** per creare un nuovo modulo all’interno di una pagina Frammento di esperienza o AEM Sites.

![Esempio di modulo adattivo in una pagina AEM Sites](/help/forms/assets/adaptive-form-in-sites-page.png)

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). 

## Why embed an Adaptive Form in AEM Sites page or AEM Experience Fragment? 

Using **[!UICONTROL Adaptive Forms – Embed(v2)]** in AEM Page Editor lets you create seamless data capture experiences within a Sites page using the power of Adaptive Forms components including dynamic behavior, validations, data integration, generate document of record and business process automation. It also lets you use various features of AEM Sites pages like, versioning, targeting, translation, and multi-site manager, enhancing the overall form creation and management experience. Let's explore some of these features:

* **Versioning:** AEM Sites pages offer [robust versioning capabilities](/help/sites-cloud/authoring/features/page-versions.md), allowing you to track and manage different versions of your forms. This enables you to make changes and enhancements to forms while maintaining the ability to roll back to previous versions if needed. Versioning ensures a controlled and organized approach to form development and evolution.
* **Targeting (Integration with Adobe Target):** With AEM Sites pages targeting capabilities, you can also [personalize the form experience for different audiences](/help/sites-cloud/integrating/integration-adobe-target-ims.md). By using user segments and targeting criteria, you can tailor the form's content, design, or behavior to specific groups of users. This enables you to provide a personalized and relevant form experience, increasing engagement and conversion rates.
* **Translation:** AEM Sites [seamless integration with translation services](/help/sites-cloud/administering/translation/overview.md), allowing you to translate forms into multiple languages easily. This feature simplifies the localization process, ensuring that your forms are accessible to a global audience. You can manage translations efficiently within AEM translation projects, reducing time and effort required for multilingual form support. See considerations section for more information on translation.  
* **Multi-site Management and Live Copy:** AEM Sites provide robust [Multi-site Management and Live Copy capabilities](/help/sites-cloud/administering/msm/overview.md), enabling you to create and manage multiple websites within a single environment. This feature now lets you reuse forms across different sites, ensuring consistency and reducing duplication efforts. With centralized control and management, you can efficiently maintain and update forms across multiple websites.
* **Themes:** AEM Sites pages provide a framework for designing and maintaining consistent visual styles across multiple web pages. These define colors, fonts, style sheets, and other visual elements that contribute to the overall look and feel of the website. [You can use the themes designed for an AEM Sites page for an Adaptive Form, saving time and effort](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes). 
* **Tagging:** AEM Sites pages allow you to [assign tags or labels to a page, an asset, or other content](/help/implementing/developing/introduction/tagging-framework.md). Tags are keywords or metadata labels that provide a way to categorize and organize content based on specific criteria. You can assign one or more tags to pages, assets, or any other content items within AEM to improve search and categorize the assets. 
* **Locking and Unlocking content:** AEM Sites allow users to [control access and modifications to pages](/help/sites-cloud/authoring/fundamentals/editing-content.md) within the AEM Sites environment. When a page is locked, it means that it is protected from unauthorized changes or edits by other users. Only the user who has locked the content or a designated administrator can unlock it to allow modifications. 

In addition, Adaptive Forms in AEM Page Editor use [Adaptive Forms Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#features). These Core Components provide a standard and easier methods to style and customize the components, identical to [AEM Sites WCM Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=en).

-->

## Come si crea o si incorpora un modulo adattivo nella pagina di AEM Sites o in un frammento di esperienza AEM? {#various-options-to-create-or-embed-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Puoi sfruttare appieno questa funzione utilizzando le seguenti opzioni:

* **[Creare un modulo adattivo utilizzando modelli approvati e incorporarlo in una pagina AEM Sites](#embed-form-using-adaptive-form-wizzard-aem-sites):** Puoi sfruttare i modelli pre-approvati per creare e incorporare rapidamente Forms adattivo in linea con le linee guida di branding e gli standard di progettazione della tua organizzazione.

* **[Incorporare moduli esistenti in una pagina AEM Sites](#embed-an-adaptive-form-in-sites-editor):** Puoi integrare facilmente nei tuoi siti web i moduli già creati, consentendo ai visitatori di interagire direttamente con essi.

* **[Convertire un modulo adattivo incorporato in frammento di esperienza](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Converti un modulo adattivo incorporato aggiunto a una pagina AEM Sites in un frammento di esperienza per riutilizzare il modulo su più pagine AEM Sites.

* **[Creare e aggiungere un modulo adattivo personalizzato a una pagina AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** È possibile utilizzare **[!UICONTROL Contenitore modulo adattivo]** componente per creare un nuovo modulo da zero, adattandolo in modo specifico ai requisiti e alle preferenze di progettazione.

* **[Creare e aggiungere un modulo adattivo personalizzato a un frammento di esperienza](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor):** Puoi estendere la portata dei moduli aggiungendoli ai Frammenti esperienza AEM per consentirne il riutilizzo su più pagine o siti.

* **Aggiungere più moduli a una pagina o a un frammento di esperienza di AEM Sites:**  Puoi creare o aggiungere più Forms adattivi a una pagina AEM Sites per fornire più scelte agli utenti in base alle loro preferenze e ai loro requisiti. È possibile utilizzare l’Editor pagina AEM per incorporare rapidamente più moduli nelle pagine AEM Sites. È possibile utilizzare **[!UICONTROL Contenitore modulo adattivo]** più volte per aggiungere Forms adattivo a una pagina AEM Sites. È possibile utilizzare **[!UICONTROL Forms adattivo - Incorpora]** componente più volte in una pagina AEM Sites, solo se **[!UICONTROL La forma copre l&#39;intera larghezza della cornice]** è selezionata. Se il valore **[!UICONTROL La forma copre l&#39;intera larghezza della cornice]** non è selezionata, la pagina AEM Sites supporta un solo modulo adattivo senza iframe. Per aggiungere altro Forms adattivo utilizzando **[!UICONTROL Forms adattivo - Incorpora]** componente, seleziona **[!UICONTROL La forma copre l&#39;intera larghezza della cornice]** opzione.

## Considerazioni per incorporare un modulo adattivo nella pagina di AEM Sites o nel frammento di esperienza AEM {#consideration}

* Quando si crea o si aggiunge un modulo utilizzando **[!UICONTROL Forms adattivo - Incorpora(v2)]** i moduli vengono tradotti e localizzati utilizzando il flusso di traduzione AEM Forms. In questo caso, viene mantenuto un singolo modulo a cui viene fatto riferimento in tutte le copie in lingua delle pagine di Sites. **[!UICONTROL Forms adattivo - Incorpora(v2)]** Il componente non fornisce l’accesso a varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

* Quando si utilizza **[!UICONTROL Contenitore modulo adattivo]** per creare un modulo, i moduli vengono tradotti e localizzati attraverso il flusso di traduzione AEM Sites. Per ogni lingua viene generata una copia separata (copia per lingua) della pagina del sito e dei moduli corrispondenti e, quando un autore di contenuto modifica una regola in un modulo nella pagina padre, le stesse modifiche devono essere apportate in tutte le copie per lingua del modulo. **[!UICONTROL Contenitore modulo adattivo]** consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.


## Requisiti per incorporare un modulo adattivo nella pagina di AEM Sites o nel frammento di esperienza AEM {#before-you-start-embedding-an-adaptive-form}

Prima di iniziare a incorporare un nuovo modulo adattivo o un modulo adattivo preesistente utilizzando **[!UICONTROL Forms adattivo - Incorpora(v2)]**, abilita **Componenti core Forms adattivi** e aggiungi **Librerie client Forms adattive** alla pagina AEM Sites:

+++  Abilitare i componenti core Forms adattivi per il tuo ambiente AEM Cloud Service

Assicurati che [I componenti core Forms adattivi sono abilitati per l’ambiente AEM Forms as a Cloud Service](enable-adaptive-forms-core-components.md).

+++

+++  Aggiungere librerie client Forms adattive alla pagina o al frammento di esperienza AEM Sites

Quando **[!UICONTROL Quando il modulo occupa l’intera larghezza di una pagina]** è selezionata in **[!UICONTROL Contenitori modulo]** finestra di dialogo per configurazione e viene utilizzato Forms adattivo che utilizza i componenti core, è necessario includere le librerie client nella pagina del sito corrispondente.

![Quando si seleziona un modulo che copre l’intera larghezza di una pagina, si utilizza un modulo adattivo con componenti core](/help/forms/assets/overlaycorecomponent.gif)


Aggiungi il **Customheaderlibs** e **Customfooterlibs** le librerie client nella pagina AEM Sites utilizzando la pipeline di distribuzione. Per aggiungere le librerie client:

1. Accedere e clonare [Archivio Git AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Apri la cartella AEM Cloud Service Git Repository in un editor di testo per piani. Ad esempio, Microsoft® Visual Code.
1. Apri `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` e aggiungi al file il seguente codice:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Apri `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` e aggiungi al file il seguente codice:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Apri `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` e aggiungi al file il seguente codice:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Apri `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` e aggiungi al file il seguente codice:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. [Eseguire la pipeline di distribuzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) per distribuire le librerie client nell’ambiente AEM as a Cloud Service.

+++

+++ Abilita **[!UICONTROL Forms adattivo - Incorpora(v2)]** per la pagina o il frammento di esperienza di AEM Sites

Per abilitare **[!UICONTROL Forms adattivo - Incorpora(v2)]** nel criterio del modello, effettuare le seguenti operazioni:

1. Apri la pagina AEM Sites o il frammento di esperienza per la modifica. Per aprire la pagina per la modifica, selezionarla e fare clic su **[!UICONTROL Modifica]**.
1. Apri il modello della pagina Sites o Frammento esperienza. Per aprire il modello, passare alla **[!UICONTROL Informazioni pagina]** ![Informazioni pagina](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Modifica modello]**. Apre il modello corrispondente nell’editor modelli.
1. Nella vista Struttura, fare clic sul pulsante **[!UICONTROL Policy]** ![Policy](/help/forms/assets/Smock_FeedManagement_18_N.svg) nella barra dei menu. In **[!UICONTROL Componenti consentiti]** e seleziona la **[!UICONTROL Forms adattivo - Incorpora(v2)]**  casella di controllo sotto **[Nome progetto archetipo AEM] - Modulo adattivo**.
1. Clic **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

## Incorporare un modulo adattivo utilizzando il componente Forms adattivo - Incorpora(v2) {#embed-an-adaptive-form-in-sites-editor-or-experience-fragment}

Utilizza il **[!UICONTROL Forms adattivo - Incorpora(v2)]** per creare un modulo adattivo direttamente nell’editor di AEM Sites tramite la procedura guidata per la creazione di moduli. Il modulo risultante viene salvato come entità esterna, consentendo il suo riutilizzo in altre pagine Sites e moduli autonomi. Puoi incorporare un modulo nuovo di zecca da zero, personalizzandolo in base a specifici requisiti e preferenze di progettazione, direttamente in una pagina AEM Sites o in Frammento esperienza. Per i moduli monouso, si consiglia di eseguire l’authoring diretto su una pagina AEM Sites, mentre i frammenti di esperienza sono ideali per i moduli che devono essere riutilizzati su più pagine del sito web.

Puoi incorporare facilmente un nuovo modulo utilizzando **[!UICONTROL Forms adattivo - Incorpora(v2)]**.  Ad esempio, immagina di incorporare un nuovo modulo per i contatti in una pagina AEM Sites o in un frammento di esperienza AEM. Eventuali aggiornamenti o modifiche apportate al modulo di contatto all’interno della pagina AEM Sites o al frammento di esperienza si applicano automaticamente a tutte le pagine in cui viene distribuito. Questo semplifica la gestione dei moduli del sito web, garantendo un’esperienza utente fluida e semplificando al contempo il processo complessivo.

Utilizzo di **[!UICONTROL Forms adattivo - Incorpora(v2)]**, è possibile:

* [Incorporare un nuovo modulo utilizzando la procedura guidata Forms adattivo nella pagina AEM Sites](#embed-form-using-adaptive-form-wizzard-aem-sites)
* [Incorporare un nuovo modulo utilizzando la procedura guidata Forms adattivo in un frammento di esperienza](#embed-form-using-adaptive-form-wizzard-experience-fragment)
* [Incorporare un modulo adattivo esistente in una pagina AEM Sites](#embed-an-adaptive-form-in-sites-editor)
* [Incorporare un modulo esistente in un frammento di esperienza](#embed-an-adaptive-form-in-experience-fragment)
* [Convertire un modulo adattivo in una pagina di AEM Sites in un frammento di esperienza](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Incorporare un nuovo modulo utilizzando la procedura guidata Forms adattivo nella pagina AEM Sites {#embed-form-using-adaptive-form-wizzard-aem-sites}

I passaggi per incorporare un nuovo modulo in una pagina AEM Sites sono i seguenti:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Dal pannello del browser Componenti, trascina **[!UICONTROL Forms adattivo - Incorpora(v2)]** sulla pagina.
1. Fai clic su **Più** e si viene reindirizzati alla procedura guidata di creazione del modulo.

   ![Forms adattivo: componente Incorpora](/help/forms/assets/aemformcontainer.png)

1. Creare un nuovo modulo adattivo da **[!UICONTROL Creazione modulo]** procedura guidata.
Il **[!UICONTROL Percorso risorsa]** include già il percorso di un modulo adattivo creato
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

Quindi, puoi [impostare l&#39;azione di invio](/help/forms/configuring-submit-actions.md) e le proprietà avanzate di un modulo adattivo incorporato tramite la procedura guidata di creazione del modulo.


### Incorporare un nuovo modulo utilizzando la procedura guidata Forms adattivo in un frammento di esperienza {#embed-form-using-adaptive-form-wizzard-experience-fragment}

I passaggi per incorporare un nuovo modulo in un frammento di esperienza sono i seguenti:

1. Apri il frammento di esperienza in modalità di modifica.
1. Dal pannello del browser Componenti, trascina **[!UICONTROL Forms adattivo - Incorpora(v2)]** sulla pagina.
1. Fai clic su **Più** e si viene reindirizzati alla procedura guidata di creazione del modulo.

   ![Forms adattivo: componente Incorpora](/help/forms/assets/aemformcontainer.png)

1. Creare un nuovo modulo adattivo da **[!UICONTROL Creazione modulo]** procedura guidata.
Il **[!UICONTROL Percorso risorsa]** include già il percorso di un modulo adattivo creato
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nel frammento di esperienza.

Quindi, puoi [impostare l&#39;azione di invio](/help/forms/configuring-submit-actions.md) e le proprietà avanzate di un modulo adattivo incorporato tramite la procedura guidata di creazione del modulo.

### Incorporare un modulo adattivo esistente in una pagina AEM Sites {#embed-an-adaptive-form-in-sites-editor}

Con il **[!UICONTROL Forms adattivo - Incorpora(v2)]** componente, puoi integrare facilmente un modulo adattivo preesistente in una pagina di AEM Sites. Questa funzione migliora in modo significativo l’adattabilità e la riutilizzabilità di Adaptive Forms, offrendo ai clienti un modo pratico per riutilizzare i moduli già creati. Immagina ad esempio di incorporare un modulo per i contatti in una pagina di AEM Sites, eliminando la necessità di ricreare il modulo più volte.

Per incorporare un modulo adattivo esistente in una pagina Sites:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Trascina la selezione **[!UICONTROL Forms adattivo - Incorpora(v2)]** dal browser Componenti alla pagina Sites.
1. Tocca il **[!UICONTROL Forms adattivo - Incorpora]** nella pagina Sites e tocca ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg) sulla barra delle azioni. Il **[!UICONTROL Modifica Forms adattivo - Incorpora(v2)]** viene visualizzata una finestra di dialogo.
1. Sfoglia e seleziona il modulo adattivo da incorporare nel **[!UICONTROL Percorso risorsa]**.
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

Quindi, puoi [impostare l&#39;azione di invio](/help/forms/configuring-submit-actions.md) e le proprietà avanzate di un modulo adattivo incorporato tramite la procedura guidata di creazione del modulo.

### Incorporare un modulo adattivo esistente in un frammento di esperienza {#embed-an-adaptive-form-in-experience-fragment}

Puoi anche estendere l’accessibilità dei moduli incorporandoli in Frammento esperienza AEM. Per incorporare un modulo adattivo in un frammento di esperienza:

1. Apri un frammento di esperienza in modalità di modifica.
1. Trascina la selezione **[!UICONTROL Forms adattivo - Incorpora(v2)]** dal browser Componenti al frammento di esperienza.
1. Tocca il **[!UICONTROL Forms adattivo - Incorpora]** nel frammento esperienza e tocca ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg) sulla barra delle azioni. Il **[!UICONTROL Modifica Forms adattivo - Incorpora(v2)]** viene visualizzata una finestra di dialogo.
1. Sfoglia e seleziona il modulo adattivo da incorporare nel **[!UICONTROL Percorso risorsa]**.
1. Salva le impostazioni. Il modulo adattivo è ora incorporato nel frammento di esperienza.

Quindi, puoi [impostare l&#39;azione di invio](/help/forms/configuring-submit-actions.md) e le proprietà avanzate di un modulo adattivo incorporato tramite la procedura guidata di creazione del modulo.

### Convertire un modulo in una pagina di AEM Sites in un frammento di esperienza {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

È possibile convertire un modulo adattivo esistente in un editor di pagine Sites in un frammento di esperienza per riutilizzare il modulo in più pagine o siti.

Per convertire un modulo adattivo nella pagina di AEM Sites in un frammento di esperienza:

1. Apri la pagina AEM Sites contenente il modulo adattivo (nel componente Contenitore Forms adattivo) in modalità di modifica.
1. Apri la Struttura contenuto e seleziona la **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Nella barra dei menu, seleziona ![Icona Converti in variante di frammento esperienza](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Icona Converti in variante di frammento esperienza.

   ![Fai clic sul logo dell’archivio file per convertire un modulo adattivo nella pagina AEM Sites in un frammento di esperienza](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Viene visualizzata una finestra di dialogo per convertire il contenitore Moduli adattivi in un nuovo frammento di esperienza o aggiungerlo a un frammento di esperienza esistente.

1. Il giorno **[!UICONTROL Converti in frammento esperienza]** variante (variation), impostate i valori per le seguenti opzioni:

   * **Azione:** Seleziona questa opzione per creare un frammento di esperienza o Aggiungi a un frammento di esperienza esistente.
   * **Percorso principale:** Specifica il percorso della cartella in cui ospitare il frammento di esperienza. L’opzione è disponibile solo per la creazione di un nuovo frammento di esperienza.
   * **Modello:** Specifica il percorso del modello Frammento esperienza. Se non disponi di un modello Frammento esperienza, [crearlo](/help/implementing/developing/extending/experience-fragments.md). L’opzione è disponibile solo per aggiungere un modulo adattivo a un frammento di esperienza esistente.
   * **Titolo frammento:** Specifica il titolo del frammento di esperienza. Il titolo identifica in modo univoco un frammento esperienza.
   * **Tag frammento:** Specifica il tag del frammento di esperienza. Il tag identifica in modo univoco la categoria di un frammento di esperienza.

## Configurare le proprietà di Adaptive Form-Embed(v2)

È possibile personalizzare le impostazioni avanzate del **[!UICONTROL Modulo adattivo - Incorpora(v2)]** componente. In **[!UICONTROL Modifica Forms adattivo - Incorpora]** , puoi specificare quanto segue:

* **Percorso risorsa**: sfoglia e seleziona un modulo adattivo da incorporare. Viene compilato automaticamente se viene rilasciato dal browser Risorse.
* **Invio post** : seleziona l’azione da attivare all’invio del modulo. Puoi scegliere di visualizzare un messaggio di ringraziamento o una pagina di ringraziamento.
   * **Mostra messaggio di ringraziamento**: scrivi un messaggio utilizzando l’editor Rich Text. Questa opzione è disponibile solo quando si sceglie di visualizzare un messaggio di ringraziamento.
   * **Mostra pagina di ringraziamento**: sfoglia e seleziona la pagina da visualizzare all’invio del modulo. Questa opzione è disponibile solo quando si sceglie di visualizzare una pagina di ringraziamento.
   * **Reindirizza alla pagina di ringraziamento**: abilita l’opzione per sostituire la pagina contenente il modulo adattivo incorporato con la pagina di ringraziamento. In caso contrario, la pagina di ringraziamento sostituisce il modulo adattivo nel **[!UICONTROL Forms adattivo - Incorpora(v2)]** senza aggiornare i siti sottostanti nella pagina. Questa opzione è disponibile solo quando si sceglie di visualizzare una pagina di ringraziamento.
   * **Messaggio di ringraziamento**: breve conferma o conferma visualizzata sullo schermo dopo l’invio corretto di un modulo.
   * **Pagina di ringraziamento**: dopo aver inviato correttamente un modulo, individua e seleziona la pagina da visualizzare.

* **Usa lingua della pagina**: utilizza la lingua locale della pagina AEM Sites invece della lingua del modulo adattivo. Questa opzione è applicabile solo per il modulo adattivo (Foundation).
* **Imposta stato attivo sul modulo**: seleziona per impostare lo stato attivo sul primo campo del modulo adattivo. Questa opzione è applicabile solo per il modulo adattivo (Foundation).
* **Tema**: seleziona un tema che definisce lo stile dei componenti del modulo adattivo. Lo stile include proprietà di aspetto quali lo stile del carattere, il colore di sfondo, le dimensioni e l&#39;allineamento. Questa opzione è applicabile solo per il modulo adattivo (Foundation).

  >[!NOTE]
  >
  > È possibile utilizzare **Usa lingua della pagina**, **Imposta stato attivo sul modulo** e **Tema** solo per Modulo adattivo (Foundation).

* **La forma copre l&#39;intera larghezza della cornice**: un frame in linea (iframe) è un elemento HTML che carica un modulo adattivo in una pagina AEM Sites.

   * Se il **[!UICONTROL La forma copre l&#39;intera larghezza della cornice]** Se è selezionata una casella di controllo, un modulo adattivo occupa l’intera larghezza del contenitore in cui viene inserito. In questo caso, non viene utilizzato un iframe per eseguire il rendering del modulo. Il layout e il design di un modulo adattivo si adattano a coprire l’intera larghezza del contenitore, rendendolo reattivo e in grado di adattarsi a diverse dimensioni dello schermo. Questa opzione consente di incorporare più Forms adattivi all’interno di una pagina AEM Sites.

     >[!NOTE]
     >
     > Per incorporare più moduli in una pagina AEM Sites, seleziona **[!UICONTROL La forma copre l&#39;intera larghezza della cornice]** casella di controllo.

   * Se il **[!UICONTROL La forma copre l&#39;intera larghezza della cornice]** non sia selezionata, un modulo adattivo non copre l’intera larghezza del contenitore. Viene invece utilizzato un iframe per eseguire il rendering del modulo, che non può essere esteso oltre una larghezza specifica. Questo approccio è utile quando un modulo adattivo ha confini definiti e deve coesistere con altri componenti AEM adiacenti all’interno del contenitore. Se questa opzione non è selezionata, è possibile incorporare un solo Forms adattivo nella pagina AEM Sites senza un iframe.

     >[!NOTE]
     >
     > La pagina di AEM Sites supporta un solo modulo adattivo per esistere senza un iframe. Per aggiungere altro Forms adattivo utilizzando **[!UICONTROL Forms adattivo - Incorpora]** componente, seleziona **[!UICONTROL La forma copre l&#39;intera larghezza della cornice]** opzione.

* **Altezza**: specifica l’altezza del contenitore. Lascia vuoto questo campo per ridimensionare automaticamente il contenitore.
* **Libreria client CSS**: specifica il percorso di una libreria client CSS.

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

1. To create and embed a new form, on the component toolbar, tap the **Create Form** icon. A window to create the form opens. 

1. Tap the embedded Adaptive Forms - Embed component in the sites page, and then tap ![settings_icon](assets/settings_icon.png) on the action bar. The **[!UICONTROL Edit Adaptive Forms - Embed]** dialog opens.
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

Prendiamo in considerazione i seguenti scenari per la pubblicazione di un modulo adattivo incorporato nella pagina dei siti AEM:

* Se pubblichi la pagina dei siti AEM per la prima volta e include un modulo adattivo incorporato, pubblica la pagina dei siti e la risorsa incorporata.
* Se hai modificato solo il modulo adattivo incorporato in una pagina del sito pubblicata, pubblica la risorsa originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se hai modificato la pagina Sites e il modulo adattivo incorporato, ripubblica la pagina Sites e la risorsa incorporata.

## Modifica modulo adattivo incorporato  {#modifying-embedded-adaptive-form}

Per modificare una configurazione o una proprietà del modulo adattivo incorporato, effettuate una delle seguenti operazioni.

* Apri il modulo originale in un modulo adattivo nel rispettivo editor e modificalo.
* In modalità di modifica, tocca il modulo adattivo all’interno della pagina del sito, quindi tocca **[!UICONTROL Modifica in una nuova finestra]**. Il modulo originale viene aperto in modalità di modifica modificabile.

>[!NOTE]
>
>Le modifiche apportate nel modulo adattivo originale si riflettono automaticamente nel modulo incorporato. Tuttavia, ripubblica il modulo adattivo o la pagina del sito per riflettere le modifiche nella pagina pubblicata.

## Best practice {#best-practices}

Quando incorpori Forms adattivo nelle pagine dei siti AEM, considera gli aspetti seguenti:

* Intestazione e piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze utente e gli invii di moduli incorporati sono supportati e visibili nelle schede Bozze e Forms inviate nel portale Forms.
* L’azione di invio configurata nel modulo originale viene mantenuta nel modulo incorporato.
* Se hai configurato Adobe Analytics per il modulo originale, i dati di analisi del modulo incorporato vengono acquisiti in Adobe Analytics. Tuttavia, non è disponibile nel rapporto di analisi di Forms.

## Consulta anche {#see-also}

* [Creazione di un Forms adattivo indipendente basato su Componente core](/help/forms/creating-adaptive-form-core-components.md)
* [Creare un modulo adattivo basato su componenti core direttamente in una pagina di AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
