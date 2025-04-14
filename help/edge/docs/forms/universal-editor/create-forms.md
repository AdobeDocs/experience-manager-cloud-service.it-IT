---
title: Come si creano moduli indipendenti basati su un modello di Edge Delivery Services utilizzando l’editor universale?
description: In questo articolo viene illustrato come utilizzare l’editor universale per creare moduli selezionando un modello basato su Edge Delivery Services nella procedura guidata per la creazione di moduli. Puoi anche pubblicare i moduli in AEM Edge Delivery Services.
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: b0cedf31a8759cdf403e1e7d6aadcab3bba03bab
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 87%

---

# Creazione di Forms adattivo con Universal Editor

<span class="preview"> Questa funzione è disponibile tramite il programma per i primi utilizzatori. Per richiedere l’accesso, invia un’e-mail con il nome dell’organizzazione e il nome dell’archivio GitHub dall’indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Ad esempio, se l’URL dell’archivio è https://github.com/adobe/abc, il nome dell’organizzazione è adobe e il nome dell’archivio è abc.</span>

Universal Editor è un editor visivo versatile che offre un’esperienza di modifica dei moduli che consente di vedere cosa si ottiene (WYSIWYG). Semplifica la creazione di moduli reattivi e facili da usare con una funzione di trascinamento della selezione, utilizzando i componenti di Forms adattivi disponibili come caselle di testo, pulsanti di scelta e caselle di controllo.

AEM fornisce un blocco, noto come blocco di Forms adattivo, per facilitare la creazione di Edge Delivery Services Forms per l’acquisizione e l’archiviazione di dati tramite Universal Editor. Puoi [creare un nuovo progetto AEM preconfigurato con il Blocco moduli adattivi](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) oppure [aggiungere il Blocco moduli adattivi a un progetto AEM Site esistente](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project).

![Flusso di lavoro per l’archivio Github](/help/edge/assets/repo-workflow.png)

Questo articolo illustra come creare e creare moduli autonomi con Universal Editor selezionando un modello basato su Edge Delivery Services dalla Creazione guidata moduli.

## Prerequisiti

* [Configura l’archivio GitHub](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) per stabilire una connessione tra l’ambiente AEM e l’archivio GitHub.
* Se utilizzi già Edge Delivery Services, aggiungi la versione più recente del [Blocco moduli adattivi](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) all’archivio GitHub.
* L’istanza di authoring di AEM Forms include un modello basato su Edge Delivery Services. Assicurati che nel tuo ambiente sia installata la [versione più recente dei Componenti core](https://github.com/adobe/aem-core-forms-components).
* Tieni a portata di mano l’URL dell’istanza di authoring di AEM Forms as a Cloud Service e dell’archivio GitHub.

## Utilizzo dei moduli nell’editor universale

Con Universal Editor è possibile creare facilmente moduli autonomi interattivi e reattivi. Nell’editor universale puoi eseguire le azioni seguenti sui moduli:
* [Creazione di un modulo](#create-a-form)
* [Authoring di un modulo](#author-a-form)
* [Pubblicazione di un modulo](#publish-a-form)
* [Gestione di un modulo](#manage-a-form)

>[!NOTE]
>
> Puoi anche [creare un modulo in AEM Site utilizzando il modello per siti di Edge Delivery Services nell’editor universale e pubblicarlo in Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project).


### Creazione di un modulo

1. Accedi all’istanza di authoring di AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Seleziona **[!UICONTROL Crea]**  > **[!UICONTROL Moduli adattivi]**. Viene aperta la procedura guidata.
1. Nella scheda **Origine**, seleziona un modello per moduli basato su Edge Delivery Services:

   ![Crea moduli EDS](/help/edge/assets/create-eds-forms.png)


   Quando selezioni un modello basato su Edge Delivery Services, il pulsante **[!UICONTROL Crea]** è abilitato.
1. (Facoltativo) Nelle schede **[!UICONTROL Origine dati]** o **[!UICONTROL Invio]**, puoi selezionare un’origine dati o un’azione di invio.
1. (Facoltativo) Nella scheda **[!UICONTROL Consegna]**, puoi specificare una data di pubblicazione o di annullamento della pubblicazione per un modulo.

1. Fai clic su **[!UICONTROL Crea]** per visualizzare la procedura guidata **Crea modulo**.
1. Specifica **Nome** e **Titolo**.
1. Specifica l’**URL di GitHub**. Ad esempio, se l’archivio GitHub è denominato `edsforms` e si trova sotto l’account `wkndforms`, l’URL è:
   `https://github.com/wkndforms/edsforms`
1. Fai clic su **[!UICONTROL Crea]**.

   ![Procedura guidata per la creazione di un modulo](/help/edge/assets/create-form-wizard.png)

   Non appena fai clic su **[!UICONTROL Crea]**, il modulo viene aperto nell’editor universale per la creazione.

   ![crea il modulo](/help/edge/assets/author-form.png)

   <!-- >[!NOTE]
        >
        > The Edge Delivery Services configuration for the forms based on Edge Delivery Services template is created automatically at the form's configuration container.-->

   Quando fai clic su **[!UICONTROL Crea]**, il modulo viene aperto nell’editor universale per la creazione.

### Authoring di un modulo

1. Apri il Browser dei contenuti e accedi al componente **[!UICONTROL Modulo adattivo]** nella **Struttura contenuto**.

   ![struttura contenuto](/help/edge/assets/content-tree.png)

1. Fai clic sull’icona **[!UICONTROL Aggiungi]** e aggiungi i componenti desiderati dall’elenco **Componenti modulo adattivo**.

   ![aggiungi componente](/help/edge/assets/add-component.png)

1. Seleziona il componente Modulo adattivo aggiunto e aggiornane le proprietà utilizzando **[!UICONTROL Proprietà]**.

   ![apri proprietà](/help/edge/assets/component-properties.png)

   La schermata seguente mostra il modulo `Registration Form` semplice creato nell’editor universale:

   ![modulo contattaci](/help/edge/assets/contact-us.png)

   Ora puoi [configurare e personalizzare le azioni di invio per i moduli](/help/edge/docs/forms/universal-editor/submit-action.md).


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

### Pubblicazione di un modulo

Ora, pubblica il modulo in Edge Delivery Services facendo clic sul pulsante **[!UICONTROL Pubblica]** nell’angolo in alto a destra dell’editor universale.

![pubblica modulo](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> Per informazioni su come pubblicare un modulo in Edge Delivery Services, consulta l’articolo [Pubblicare e distribuire](/help/edge/docs/forms/universal-editor/publish-forms.md).

Di seguito viene descritto come accedere al modulo su Edge Delivery Services:

* **Versione di staging (per il test)**: la versione di staging mostra la versione di lavoro non pubblicata del modulo a scopo di test. Utilizza il seguente formato URL per visualizzare l’anteprima del modulo prima della pubblicazione:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  Ad esempio, se l’archivio del progetto è denominato “edsforms”, si trova sotto l’account “wkndforms”, e stai utilizzando il ramo “main” e il modulo come “Modulo di registrazione”, la versione in staging dell’URL avrà l’aspetto seguente:
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **Versione live (modulo pubblicato)**: la versione live mostra la versione pubblicata più recente del modulo, accessibile agli utenti finali. Utilizza il seguente formato URL per accedere alla versione live pubblicata del modulo:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  Ad esempio, se l’archivio del progetto è denominato “edsforms”, si trova sotto l’account “wkndforms”, e stai utilizzando il ramo “main” e il modulo come “Modulo di registrazione”, la versione in staging dell’URL avrà l’aspetto seguente:
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

La struttura URL rimane invariata sia per le versioni di staging sia per quelle live. Tuttavia, il contenuto visualizzato varia in base al contesto:

![Visualizza modulo pubblicato](/help/edge/assets/eds-view-publish-form.png)

### Gestione di un modulo

Puoi eseguire diverse operazioni sul modulo utilizzando l’interfaccia utente di AEM Forms.

1. Accedi all’istanza di authoring di AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.

1. Selezionando un modulo, sulla barra degli strumenti vengono visualizzate le operazioni seguenti che è possibile eseguire sul modulo selezionato.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operazione</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>Modifica</p> </td>
   <td><p>Apre il modulo in modalità di modifica.<br /> <br />  </p> </td>
  </tr>
    <tr>
   <td><p>Proprietà</p> </td>
   <td><p>Fornisce opzioni per modificare le proprietà del modulo.<br /> <br /> </p> </td>
  </tr>
  <td><p>Copia</p> </td>
   <td><p> Fornisce opzioni per copiare il modulo e incollarlo nella posizione desiderata. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Anteprima</p> </td>
   <td><p>Fornisce opzioni per visualizzare in anteprima il modulo come HTML o per eseguire un’anteprima personalizzata unendo i dati di un file XML con il modulo. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Scarica</p> </td>
   <td><p>Scarica il modulo selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Avvia/Gestisci revisione</p> </td>
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
   <td><p>Confronta</p> </td>
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
