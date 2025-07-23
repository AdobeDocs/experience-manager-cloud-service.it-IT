---
title: Come creare moduli indipendenti basati su componenti core o modelli Edge Delivery Services e pubblicarli su Edge Delivery Services
description: Questo articolo spiega come creare moduli adattivi selezionando modelli basati su un componente core o su Edge Delivery Services nella procedura guidata per la creazione di moduli. Puoi anche pubblicare i moduli in AEM Edge Delivery Services.
feature: Edge Delivery Services
role: User
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: ht
source-wordcount: '1687'
ht-degree: 100%

---


# Dall’authoring alla pubblicazione: moduli AEM su Edge Delivery Services

<span class="preview"> Questa funzione è disponibile tramite il programma per i primi utilizzatori. Per richiedere l’accesso, invia un’e-mail con il nome dell’organizzazione e il nome dell’archivio GitHub dall’indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Ad esempio, se l’URL dell’archivio è https://github.com/adobe/abc, il nome dell’organizzazione è adobe e il nome dell’archivio è abc.</span>

Adobe Experience Manager (AEM) consente di creare moduli coinvolgenti, reattivi e dinamici. Offre diversi metodi di authoring, ciascuno adatto a diversi requisiti e livelli di esperienza utente.

Questo articolo si concentra sull’approccio in cui i moduli vengono creati all’interno dell’ambiente AEM e pubblicati tramite Edge Delivery Services. I moduli creati utilizzando modelli basati su componenti core possono essere pubblicati sia su AEM che su Edge Delivery Services, offrendo flessibilità di implementazione. Al contrario, i moduli creati utilizzando modelli basati su Edge Delivery Services possono essere pubblicati solo su Edge Delivery Services.

![Authoring e pubblicazione di un modulo adattivo](/help/edge/docs/forms/universal-editor/assets/author-publish-af.png){width=50% align=center}

## I vantaggi dell’authoring di moduli in AEM e della pubblicazione tramite Edge Delivery Services sono:

* **Mantenimento dei flussi di lavoro AEM esistenti**: le organizzazioni possono continuare a utilizzare i flussi di lavoro AEM e le strutture di governance, garantendo la coerenza e il controllo sulla creazione dei contenuti.

* **Prestazioni migliorate**: la pubblicazione tramite Edge Delivery Services comporta tempi di rendering più rapidi, migliorando l’esperienza utente e riducendo i tempi di caricamento delle pagine.

* **SEO migliorata**: Edge Delivery Services è progettato per fornire contenuti con punteggi elevati di Google Lighthouse, che possono comportare una migliore ottimizzazione SEO (Search Engine Optimization) e una maggiore visibilità.

* **Opzioni di distribuzione flessibili**: i moduli creati con componenti core possono essere pubblicati sia su AEM che su Edge Delivery Services, offrendo flessibilità nelle strategie di distribuzione.

## Prima di iniziare

Prima di iniziare a creare moduli in AEM e pubblicarli tramite Edge Delivery Services, verifica che siano soddisfatti i prerequisiti seguenti:

* assicurati di disporre di un archivio Github configurato per Edge Delivery Services.
   * Se non disponi di un archivio, consulta [nuovo progetto AEM preconfigurato con il Blocco moduli adattivi](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block).
   * Se disponi di un archivio, aggiungi il Blocco moduli adattivi all’archivio esistente. Istruzioni dettagliate sono disponibili nella [Guida introduttiva a Edge Delivery Services per moduli AEM](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project).
* Stabilisci una connessione tra l’ambiente AEM e l’archivio GitHub. [Come procedere?](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)

Un diagramma di flusso decisionale per guidare la configurazione e la pubblicazione di moduli adattivi:

![Flusso di lavoro per l’archivio Github](/help/forms/assets/repo-workflow.png){width=auto}

## Creare moduli in AEM e pubblicarli in Edge Delivery Services

Per creare moduli in AEM e pubblicarli in Edge Delivery Services, segui questi passaggi:

[&#x200B;1. Scegliere un modello e creare il modulo](#choose-a-template-and-create-the-form)

[&#x200B;2. Creare il modulo](#author-the-form)

[&#x200B;3. Pubblicare un modulo](#publish-a-form)

### Scegliere un modello e creare il modulo

Puoi creare moduli su un’istanza di AEM per la pubblicazione su Edge Delivery Services utilizzando:

>[!BEGINTABS]

>[!TAB Modello basato su Edge Delivery Services]

Per scegliere il modello e creare il modulo, segui i passaggi seguenti:

1. Accedi all’istanza di authoring di AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Seleziona **[!UICONTROL Crea]**  > **[!UICONTROL Moduli adattivi]**. Viene aperta la procedura guidata.
1. Nella scheda **Origine**, seleziona un **modello basato su Edge Delivery Services**:

   ![Creare moduli EDS](/help/edge/assets/create-eds-forms.png)

   Quando selezioni un **modello basato su Edge Delivery Services**, viene abilitato il pulsante **[!UICONTROL Crea]**.
1. (Facoltativo) Nelle schede **[!UICONTROL Origine dati]** o **[!UICONTROL Invio]**, puoi selezionare un’origine dati o un’azione di invio.
1. (Facoltativo) Nella scheda **[!UICONTROL Consegna]**, puoi specificare una data di pubblicazione o di annullamento della pubblicazione per un modulo.
1. Fai clic su **[!UICONTROL Crea]** per visualizzare la procedura guidata **Crea modulo**:

   1. Specifica **Nome** e **Titolo**.
   1. Specifica l’**URL di GitHub**. Ad esempio, se l’archivio GitHub è denominato `edsforms` e si trova sotto l’account `wkndforms`, l’URL è:
      `https://github.com/wkndforms/edsforms`

   ![Procedura guidata per la creazione di un modulo](/help/edge/assets/create-form-wizard.png)

   Quando fai clic su **[!UICONTROL Crea]**, il modulo viene aperto nell’editor universale per l’authoring.

   ![Schermata dell’editor universale che mostra un modulo creato con la palette dei componenti a sinistra, l’area di lavoro del modulo al centro e il pannello delle proprietà a destra](/help/edge/assets/author-form.png)
1. Fai clic su **[!UICONTROL Crea]** per creare il modulo. Ora puoi [creare il modulo utilizzando l’editor universale](#author-the-form).

>[!TAB Modello basato su componenti core]

Per scegliere il modello e creare il modulo, segui i passaggi seguenti:

1. Accedi all’istanza di authoring di AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Seleziona **[!UICONTROL Crea]**  > **[!UICONTROL Moduli adattivi]**. Viene aperta la procedura guidata.
1. Nella scheda **Origine**, seleziona un **modello basato su componente core** e un **tema**, il pulsante **[!UICONTROL Crea]** è abilitato:

   ![Modello basato su componente core](/help/forms/assets/core-component-based-template.png)

1. (Facoltativo) Nelle schede **[!UICONTROL Origine dati]** o **[!UICONTROL Invio]**, puoi selezionare un’origine dati o un’azione di invio.
1. (Facoltativo) Nella scheda **[!UICONTROL Consegna]**, puoi specificare una data di pubblicazione o di annullamento della pubblicazione per un modulo.
1. Fai clic su **[!UICONTROL Crea]** per visualizzare la procedura guidata **Crea modulo** per:
   1. Specificare il **Nome** e il **Titolo**.
   1. Specificare la posizione nel campo **percorso** in cui deve essere salvato il modulo adattivo.

   ![Procedura guidata per la creazione di un modulo](/help/forms/assets/create-cc-form.png)

   Quando fai clic su **[!UICONTROL Crea]**, il modulo viene aperto nell’editor di moduli adattivi per l’authoring.

   ![Editor di moduli adattivi](/help/forms/assets/af-editor-form.png)

1. Fai clic su **[!UICONTROL Crea]** per creare il modulo. Ora puoi [creare il modulo utilizzando l’editor di moduli adattivi](#author-the-form).

>[!ENDTABS]

### Creare il modulo

I moduli creati utilizzando il modello basato su Edge Delivery Services vengono aperti nell’[editor universale](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) per l’authoring. Tuttavia, i moduli creati utilizzando il modello basato su componenti core vengono aperti nell’editor di moduli adattivi per l’authoring.

Per l’authoring di moduli utilizzando l’editor universale per i modelli basati su Edge Delivery Services o l’editor di moduli adattivi per un modello basato su componente core, segui i passaggi seguenti:

>[!BEGINTABS]

>[!TAB Modello basato su Edge Delivery Services]


1. Apri il Browser dei contenuti e accedi al componente **[!UICONTROL Modulo adattivo]** nella **Struttura contenuto**.

   ![struttura contenuto](/help/edge/assets/content-tree.png)

1. Fai clic sull’icona **[!UICONTROL Aggiungi]** e aggiungi i componenti desiderati dall’elenco **Componenti modulo adattivo**.
   ![aggiungi componente](/help/edge/assets/add-component.png)

   La schermata seguente mostra il `Registration Form` creato nell’editor universale:

   ![Schermata del modulo Contattaci completato nell’editor universale, che mostra i campi modulo per nome, e-mail, telefono e messaggio con stile e layout appropriati](/help/edge/assets/contact-us.png)

>[!NOTE]
>
> Per istruzioni dettagliate sull’authoring di un modulo adattivo tramite l’editor universale, [fai clic qui](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

Ora puoi [configurare e personalizzare le azioni di invio dei moduli](/help/edge/docs/forms/universal-editor/submit-action.md).

>[!TAB Modello basato su componenti core]

1. Fai clic su **[!UICONTROL Inserisci componente]** nella sezione **Trascina qui i componenti**.

   ![Trascina qui i componenti](/help/forms/assets/drag-components-af-editor.png)

1. Aggiungi i componenti desiderati dall’elenco **Componenti del modulo adattivo**.

   ![Aggiungi componenti](/help/forms/assets/add-component-af.png)

La schermata seguente mostra il `Enrollment Form` creato nell’editor di moduli adattivi:

![Editor di moduli adattivi](/help/forms/assets/af-editor-form.png)

>[!NOTE]
>
> Per istruzioni dettagliate sull’authoring di un modulo adattivo basato sul modello dei componenti core, [fai clic qui](/help/forms/creating-adaptive-form-core-components.md).

Ora puoi [configurare le azioni di invio dei moduli](/help/forms/configure-submit-actions-core-components.md).

>[!ENDTABS]

### Pubblicare il modulo

Per pubblicare un modulo adattivo su Edge Delivery Services, devi [creare una configurazione Edge Delivery Services in un’istanza AEM ](#create-an-edge-delivery-services-configuration).

#### Creare una configurazione di Edge Delivery Services

Per creare la configurazione di Edge Delivery Services, segui i passaggi seguenti:

>[!BEGINTABS]
>[!TAB Modello basato su Edge Delivery Services]


La configurazione di Edge Delivery Services per moduli basati sul modello Edge Delivery Services viene creata automaticamente nel contenitore di configurazione del modulo.

![Configurazione di Edge Delivery Services](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB Modello basato su componenti core]

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Configurazione Edge Delivery Services]** nell’istanza di authoring di AEM Forms as a Cloud Service.

   ![Selezionare la configurazione di Edge Delivery Services](/help/edge/assets/select-eds-conf.png)

2. Seleziona la cartella corrispondente al nome del modulo. Ad esempio, se il modulo è denominato `enrollment-form`, scegli la cartella `forms/enrollment-form` e fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Configurazione]**:

   ![Configurazione di Edge Delivery Services](/help/forms/assets/create-eds-conf.png)

3. Fai clic su **[!UICONTROL Configurazione Edge Delivery Services]** e su **[!UICONTROL Proprietà]** per aprire le proprietà:

   ![Configurazione creata automaticamente](/help/forms/assets/eds-conf.png)

   Viene visualizzata la finestra Configurazione Edge Delivery Services.

4. Nella configurazione di Edge Delivery Services, specifica quanto segue:

   * **Organizzazione**: specifica il nome dell’organizzazione GitHub.

   * **Nome del sito**: specifica il nome dell’archivio GitHub.
   * **Ramo**: specifica il nome del ramo. Lascia vuota la casella di testo se utilizzi il ramo principale.
   * **(Facoltativo) Host di Edge**: lascia invariata l’opzione host di Edge. Il modulo viene pubblicato sia nell’ambiente di anteprima (.page) che nell’ambiente live (.live).
   * **(Facoltativo) Token di autenticazione del sito**: utilizza il token di autenticazione del sito per autenticare in modo sicuro le richieste tra l’istanza di AEM ed Edge Delivery Services.

5. Fai clic su **[!UICONTROL Salva e chiudi]**. La configurazione viene creata.

>[!ENDTABS]

#### Accedere al modulo in Edge Delivery Services

Per accedere al modulo in Edge Delivery Services, è obbligatorio pubblicarlo. Per pubblicare il modulo, esegui i passaggi seguenti:

>[!BEGINTABS]
>[!TAB Nell’editor universale]

1. Pubblica il modulo facendo clic sul pulsante **[!UICONTROL Pubblica]** nell’angolo in alto a destra dell’editor universale.

![Schermata dell’editor universale che mostra la finestra di dialogo di pubblicazione con le opzioni di pubblicazione del modulo e i pulsanti di conferma](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> Per informazioni su come pubblicare un modulo in Edge Delivery Services, consulta l’articolo [Pubblicare e distribuire](/help/edge/docs/forms/universal-editor/publish-forms.md).

>[!TAB Nell’editor di moduli adattivi]

1. Dalla console Experience Manager Forms, passa alla cartella principale e seleziona il modulo che desideri pubblicare.

1. Fai clic sull’opzione **[!UICONTROL Pubblica]** nella barra degli strumenti e controlla tutte le risorse di riferimento che verranno pubblicate insieme al modulo.

![Pubblicare il modulo nell’editor di moduli adattivi](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> Per informazioni su come pubblicare un modulo nell’editor di moduli adattivi, consulta l’articolo [Gestire la pubblicazione in Experience Manager Forms](/help/forms/manage-publication.md).

>[!ENDTABS]

* **Versione di staging (per il test)**: la versione di staging mostra la versione di lavoro non pubblicata del modulo a scopo di test. Utilizza il seguente formato URL per visualizzare l’anteprima del modulo prima della pubblicazione:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`



* **Versione live (modulo pubblicato)**: la versione live mostra la versione pubblicata più recente del modulo, accessibile agli utenti finali. Utilizza il seguente formato URL per accedere alla versione live pubblicata del modulo:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  La struttura URL rimane invariata sia per le versioni di staging che per quelle live. Tuttavia, il contenuto visualizzato varia in base al contesto.

Le schermate seguenti confrontano gli URL dei moduli live e di staging e le anteprime visive per i moduli creati utilizzando modelli basati su Edge Delivery Services e su componenti core:

>[!BEGINTABS]
>[!TAB Modello basato su Edge Delivery Services]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
    <thead>
    <tr>
      <th style="width: 20%;"><strong>Versione</strong></th>
      <th style="width: 80%;"><strong>Immagine</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>Versione di staging</td>
      <td><img src="/help/forms/assets/registration-form-staged-version.png" alt="Versione di staging del modulo di registrazione" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>Versione live</td>
      <td><img src="/help/forms/assets/registration-form-live-version.png" alt="Versione live del modulo di registrazione" style="width: 100%; height: auto;" /></td>
    </tr>
    </tbody>
  </table>

>[!TAB Modello basato su componenti core]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
  <thead>
    <tr>
      <th style="width: 20%;"><strong>Versione</strong></th>
      <th style="width: 80%;"><strong>Immagine</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Versione di staging</td>
      <td><img src="/help/forms/assets/enrollment-form-staged-version.png" alt="Versione di staging del modulo di iscrizione" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>Versione live</td>
      <td><img src="/help/forms/assets/enrollment-form-live-version.png" alt="Versione live del modulo di iscrizione" style="width: 100%; height: auto;" /></td>
    </tr>
  </tbody>
  </table>

>[!ENDTABS]

## Risoluzione dei problemi

Ci sono problemi durante il caricamento del modulo? Di seguito sono riportati alcuni problemi comuni e come risolverli:

* **URL modulo**: verifica che l’URL del modulo non includa l’estensione “.html” alla fine. Edge Deliver Service non richiede questa estensione.

* **URL di authoring di AEM**: verifica che l’URL di authoring di AEM elencato nel file `fstab.yaml` sia formattato correttamente. Dovrebbe includere i seguenti dettagli:

   * Il proprietario GitHub corretto
   * Il nome dell’archivio corretto
   * Il ramo specifico utilizzato per Edge Delivery Services

## Iniziare a creare i moduli

{{universal-editor-see-also}}

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.

### Managing a form

You can perform several operations on form using the AEM Forms user interface.

1. Login into your AEM Forms as a Cloud Service author instance.
1. Select **[!UICONTROL Adobe Experience Manager]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Forms & Documents]**.

1. Select a form and the toolbar displays the following operations you can perform on the selected form.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operation</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>Edit</p> </td>
   <td><p>Opens the form in edit mode.<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>Properties</p> </td>
   <td><p>Provides options to modify the properties of the form.<br /> <br /> </p> </td>
  </tr>
  <td><p>Copy</p> </td>
   <td><p> Provides options to copy the form  and paste it at the desired location. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Preview</p> </td>
   <td><p>Provides options to preview the form as HTML or perform a custom preview by merging data from an XML file with the form. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Downloads the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Start Review/Manage Review</p> </td>
   <td><p>Allows initiating and managing a review of the selected form.<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publish / Unpublish</p> </td>
   <td><p>Publishes / unpublishes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Delete</p> </td>
   <td><p>Deletes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Compare</p> </td>
   <td><p>Compares two different form for previewing purposes.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table> 


## How Edge Delivery Services Forms Work?

Users can author Edge Delivery Services Forms using document-based authoring tools such as Google Drive, SharePoint, or the Universal Editor (WYSIWYG authoring), while leveraging the basic styling, behaviour and components available in the GitHub repository. Once authored, Edge Delivery Services Forms can send data to any platform using the Forms Submission Service.

![How Edge Delivery Services Forms works](/help/edge/docs/forms/assets/eds-forms-working.png)

### Key components of Edge Delivery Services Forms

The key components of Edge Delivery Servies Forms are:

* **GitHub Repository**: The GitHub repository serves as a boilerplate for creating Edge Delivery Services Forms. The forms leverage basic styling and functionality from the repository and allow users to add customizations and custom components to the Edge Delivery Services Forms.

* **Form Authoring**: Edge Delivery Services Forms support two types of authoring: WYSIWYG and document-based authoring. Document-based authoring enables users to create forms using familiar tools like Google Docs and Microsoft Office. WYSIWYG authoring allows users to design forms visually using the Universal Editor, making it easy for non-technical users to create and manage forms. Universal Editor offers an intuitive form creation experience and provides access to numerous form capabilities.

* **Forms Submission Service**: The Forms Submission Service allows you to store data from forms submissions on any platform, such as OneDrive, SharePoint, or Google Sheets, making it easy to access and manage form data within your preferred system.-->
