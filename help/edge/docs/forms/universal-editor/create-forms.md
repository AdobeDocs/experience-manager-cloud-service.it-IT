---
title: Come si crea un Forms adattivo indipendente con Universal Editor?
description: Questo articolo spiega come creare un Forms adattivo utilizzando la procedura guidata di creazione dei moduli nell’istanza di authoring di AEM e pubblicare i moduli in AEM Edge Delivery Services.
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 3db311812f6c4521baf1364523a0e0b1134fee65
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 44%

---

# Creare moduli autonomi tramite l’Editor universale (WYSIWYG)

<span class="preview"> Questa funzione è disponibile tramite il programma per i primi utilizzatori. Per richiedere l&#39;accesso, invia un&#39;e-mail con il nome dell&#39;organizzazione GitHub e il nome dell&#39;archivio dall&#39;indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . Ad esempio, se l’URL dell’archivio è https://github.com/adobe/abc, il nome dell’organizzazione è adobe e il nome dell’archivio è abc.</span>

Questo articolo illustra come creare moduli autonomi con l&#39;Editor universale selezionando un modello basato su Edge Delivery Services dalla Creazione guidata moduli. È inoltre possibile pubblicare i moduli creati con Universal Editor in AEM Edge Delivery Services.

<!--To publish forms to Edge Delivery Services, you must first establish a connection between your AEM environment and your GitHub repository. Once connected, you can author the forms using the Universal Editor, which follows a WYSIWYG (What You See Is What You Get) approach for a seamless and consistent user experience with Sites.-->

Prima di iniziare, scopri i tipi di componenti dei moduli disponibili:

* [Edge Delivery Services per AEM Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) è un insieme componibile di servizi che consente un ambiente di sviluppo rapido in cui gli autori possono aggiornare, pubblicare e avviare rapidamente nuovi moduli tramite Universal Editor. Universal Editor semplifica la creazione di moduli per Adobe Edge Delivery Services con un’interfaccia WYSIWYG visiva e intuitiva.

* [Componenti core dei moduli adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it): si tratta di componenti di acquisizione dati standardizzati. Questi componenti forniscono funzionalità di personalizzazione e riducono i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale. Uno sviluppatore può facilmente personalizzare e assegnare uno stile a questi componenti. Puoi visitare [https://aemcomponents.dev/](https://aemcomponents.dev/) per visualizzare i componenti core disponibili in azione **Adobe consiglia di utilizzare questi componenti moderni ed estensibili per sviluppare moduli adattivi**.

* [Componenti di base dei moduli adattivi](/help/forms/creating-adaptive-form.md): si tratta dei classici (precedenti) componenti di acquisizione dati. Puoi continuare a utilizzarli per modificare i componenti di base esistenti basati su modulo adattivo. Se stai creando nuovi moduli, Adobe consiglia di utilizzare i [Componenti core dei moduli adattivi per la creazione di un modulo adattivo](#create-an-adaptive-form-core-components).

AEM Forms fornisce un blocco, noto come blocco di moduli adattivi, per facilitare la creazione di moduli di Edge Delivery Services per l’acquisizione e l’archiviazione dei dati. È possibile [creare un nuovo progetto AEM preconfigurato con il blocco Forms adattivo](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) o [aggiungere il blocco Forms adattivo a un progetto sito AEM esistente](#add-adaptive-forms-block-to-your-existing-aem-project).

![Flusso di lavoro archivio Github](/help/edge/assets/repo-workflow.png)

## Prerequisiti

* [Configura l&#39;archivio GitHub](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) per stabilire una connessione tra l&#39;ambiente AEM e l&#39;archivio GitHub.
* Se utilizzi già Edge Delivery Services, aggiungi la versione più recente del [Blocco moduli adattivi](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) all’archivio GitHub.
* L’istanza di authoring di AEM Forms include un modello basato su Edge Delivery Services. Assicurati che nel tuo ambiente sia installata la [versione più recente dei Componenti core](https://github.com/adobe/aem-core-forms-components).
* Tieni a portata di mano l’URL dell’istanza di authoring di AEM Forms as a Cloud Service e dell’archivio GitHub.

## Creare un modulo adattivo con l’editor universale

Con Universal Editor è possibile creare facilmente moduli autonomi reattivi e interattivi utilizzando componenti già pronti come campi di testo, caselle di controllo e pulsanti di scelta. Offre potenti funzioni come regole dinamiche, integrazione dati fluida e opzioni di personalizzazione, che consentono di creare moduli in base a requisiti specifici.

>[!NOTE]
>
> È inoltre possibile [creare un modulo in AEM Site utilizzando il modello Sito Edge Delivery Services in Universal Editor e pubblicarlo in Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project).

Per creare un modulo adattivo indipendente utilizzando l’editor universale, effettua le seguenti operazioni:

1. **Creazione di un modulo adattivo nell&#39;istanza di authoring di AEM Forms**

   1. Accedi all’istanza Autore AEM Forms as a Cloud Service.
   1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
   1. Selezionare **[!UICONTROL Crea]** > **[!UICONTROL Forms adattivo]**. Viene aperta la procedura guidata.
   1. Nella scheda **Source** selezionare un modello di modulo basato su Edge Delivery Services:

      ![Crea Forms EDS](/help/edge/assets/create-eds-forms.png)


      Quando selezioni un modello basato su Edge Delivery Services, il pulsante **[!UICONTROL Crea]** è abilitato.
   1. (Facoltativo) Nelle schede **[!UICONTROL Data Source]** o **[!UICONTROL Invio]**, puoi selezionare un&#39;origine dati o inviare un&#39;azione.
   1. (Facoltativo) Nella scheda **[!UICONTROL Consegna]**, è possibile specificare una data di pubblicazione o di annullamento della pubblicazione per un modulo adattivo.

   1. Fai clic su **[!UICONTROL Crea]** per visualizzare la procedura guidata **Crea modulo**.
   1. Specificare **Nome** e **Titolo**.
   1. Specifica l’**URL di GitHub**. Ad esempio, se l&#39;archivio GitHub si chiama `edsforms`, si trova sotto l&#39;account `wkndforms`, l&#39;URL è:
      `https://github.com/wkndforms/edsforms`
   1. Fai clic su **[!UICONTROL Crea]**.

      ![Creazione guidata modulo](/help/edge/assets/create-form-wizard.png)

      Non appena fai clic su **[!UICONTROL Crea]**, il modulo viene aperto nell’editor universale per la creazione.

      ![creare il modulo](/help/edge/assets/author-form.png)

      <!-- >[!NOTE]
        >
        > The Edge Delivery Services configuration for the forms based on Edge Delivery Services template is created automatically at the form's configuration container.-->

      Quando fai clic su **[!UICONTROL Crea]**, il modulo viene aperto nell’editor universale per la creazione.

1. **Creare il modulo nell&#39;editor universale**

   1. Apri il Browser dei contenuti e accedi al componente **[!UICONTROL Modulo adattivo]** nella **Struttura contenuto**.

      ![struttura contenuto](/help/edge/assets/content-tree.png)

   1. Fai clic sull’icona **[!UICONTROL Aggiungi]** e aggiungi i componenti desiderati dall’elenco **Componenti modulo adattivo**.

      ![aggiungi componente](/help/edge/assets/add-component.png)

   1. Seleziona il componente Modulo adattivo aggiunto e aggiornane le proprietà utilizzando **[!UICONTROL Proprietà]**.

      ![apri proprietà](/help/edge/assets/component-properties.png)

      La schermata seguente mostra il semplice modulo `Registration Form` creato nell&#39;editor universale:

      ![contattaci modulo](/help/edge/assets/contact-us.png)

      Ora puoi [configurare e personalizzare le azioni di invio del modulo](/help/edge/docs/forms/universal-editor/submit-action.md).


<!--
## **Edge Delivery Services configuration of form**



   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Edge Delivery Services Configuration]** on your AEM Forms as a Cloud Service author instance.

        ![Select Edge Delivery Services Configuration](/help/edge/assets/select-eds-conf.png)
   1. Select the folder that matches the form's name. For example, if your form is called 'registration-form' choose the folder `forms/registration-form` and selct the configuration and publish the configuration:

        ![Edge Delivery Services Configuration](/help/edge/assets/aem-instance-eds-configuration.png)

   1. Click **[!UICONTROL Properties]** to see the configuration.   
        ![Automatically created configuration](/help/edge/assets/aem-forms-create-configuration-github.png)

        You can leave the Edge Host option as it is. The form would be published to both preview (.page) and live (.live) environments. 

   1. Click **[!UICONTROL Save and Close]**. The configuration is saved. -->

## Pubblicare il modulo

A questo punto, pubblicare il modulo autonomo in Edge Delivery Services facendo clic sul pulsante **[!UICONTROL Pubblica]** nell&#39;angolo superiore destro di Universal Editor.

![pubblica modulo](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> Per informazioni su come pubblicare un modulo in Edge Delivery Services, consulta l&#39;articolo [Pubblica e distribuisci](/help/edge/docs/forms/universal-editor/publish-forms.md).

Di seguito viene descritto come accedere al modulo su Edge Delivery Services:

* **Versione di staging (per il test)**: la versione di staging mostra la versione di lavoro non pubblicata del modulo a scopo di test. Utilizza il seguente formato URL per visualizzare l’anteprima del modulo prima della pubblicazione:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  Ad esempio, se l’archivio del progetto è denominato &quot;edsforms&quot;, si trova sotto l’account &quot;wkndforms&quot; e si utilizza il ramo &quot;main&quot; e il modulo come &quot;Registration Form&quot;, l’URL della versione di staging avrà l’aspetto seguente:
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **Versione live (modulo pubblicato)**: la versione live mostra la versione pubblicata più recente del modulo, accessibile agli utenti finali. Utilizza il seguente formato URL per accedere alla versione live pubblicata del modulo:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  Ad esempio, se l’archivio del progetto è denominato &quot;edsforms&quot;, si trova sotto l’account &quot;wkndforms&quot; e si utilizza il ramo &quot;main&quot; e il modulo come &quot;Registration Form&quot;, l’URL della versione di staging avrà l’aspetto seguente:
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

La struttura URL rimane invariata sia per le versioni di staging sia per quelle live. Tuttavia, il contenuto visualizzato varia in base al contesto:

![Visualizza modulo pubblicato](/help/edge/assets/eds-view-publish-form.png)

## Gestione moduli

Puoi eseguire diverse operazioni sul modulo utilizzando l’interfaccia utente di AEM Forms.

1. Accedi all’istanza Autore AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

1. Selezionare un modulo e sulla barra degli strumenti vengono visualizzate le operazioni seguenti che è possibile eseguire sul modulo selezionato.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operazione</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>Modifica</p> </td>
   <td><p>Apre il modulo in modalità di modifica.<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>Proprietà</p> </td>
   <td><p>Fornisce opzioni per modificare le proprietà del modulo.<br /> <br /> </p> </td>
  </tr>
  <td><p>Copiare</p> </td>
   <td><p> Fornisce opzioni per copiare il modulo e incollarlo nella posizione desiderata. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Anteprima</p> </td>
   <td><p>Fornisce opzioni per visualizzare in anteprima il modulo come HTML o per eseguire un'anteprima personalizzata unendo i dati di un file XML con il modulo. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Scarica il modulo selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Avvia revisione/Gestisci revisione</p> </td>
   <td><p>Consente di avviare e gestire una revisione del modulo selezionato.<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>-->
  <tr>
   <td><p>Pubblica/Annulla pubblicazione</p> </td>
   <td><p>Pubblica/annulla la pubblicazione del modulo selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Elimina</p> </td>
   <td><p>Elimina il modulo selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Confronto</p> </td>
   <td><p>Confronta due moduli diversi a scopo di anteprima.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Risoluzione dei problemi

Ci sono problemi durante il caricamento del modulo? Di seguito sono riportati alcuni problemi comuni e come risolverli:

* **URL modulo**: verifica che l’URL del modulo non includa l’estensione “.html” alla fine. Edge Deliver Service non richiede questa estensione.

* **URL di authoring di AEM**: verifica che l’URL di authoring di AEM elencato nel file `fstab.yaml` sia formattato correttamente. Dovrebbe includere i seguenti dettagli:

   * Il proprietario GitHub corretto
   * Il nome dell’archivio corretto
   * Il ramo specifico utilizzato per Edge Delivery Services

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## Iniziare a creare i moduli

{{universal-editor-see-also}}
