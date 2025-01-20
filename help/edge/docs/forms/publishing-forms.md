---
title: Pubblicazione di Forms per Edge Delivery Services
description: Scopri come funziona la pubblicazione di moduli con i Edge Delivery Services e come pubblicare moduli AEM con i Edge Delivery Services.
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---


# Pubblicazione di Forms per Edge Delivery Services

Questo articolo ti guida attraverso la procedura di pubblicazione dei moduli nei Edge Delivery Services AEM.
Per pubblicare i moduli in Edge Delivery Services, devi prima stabilire una connessione tra l’ambiente AEM e l’archivio GitHub. Una volta connessi, è possibile creare i moduli utilizzando l’Editor universale, che segue un approccio WYSIWYG (What You See Is What You Get) per un’esperienza utente fluida e coerente con Sites.

## Prerequisiti

* Ti avvicini ora ad Adaptive Forms? Configura l&#39;archivio GitHub seguendo l&#39;[esercitazione](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) fornita.
* Se utilizzi già Edge Delivery Services, aggiungi la versione più recente del [blocco Forms adattivo](/help/edge/docs/forms/tutorial.md#) all&#39;archivio GitHub.
* L’istanza Autore AEM Forms include un modello basato su Edge Delivery Services. Verifica che nell&#39;ambiente sia installata la [versione più recente dei Componenti core](https://github.com/adobe/aem-core-forms-components).
* Tieni a portata di mano l’URL dell’istanza di authoring di AEM Forms as a Cloud Service e dell’archivio GitHub.

## Publish Forms per Edge Delivery Services

Per pubblicare i moduli per i Edge Delivery Services, effettua le seguenti operazioni:

[1. Collegare l’archivio GitHub all’istanza AEM](#link-github-repository-to-aem-instance)

[2. Collegare l’istanza AEM all’archivio GitHub](#link-aem-instance-to-github-repository)

### Collegare l’archivio GitHub all’istanza AEM

Per collegare [il progetto nell&#39;archivio GitHub](/help/edge/docs/forms/tutorial.md) all&#39;istanza di AEM Forms Author, effettuare le seguenti operazioni:

1. Vai all’archivio GitHub creato o configurato per i tuoi Edge Delivery Services.
1. Apri il file `fstab.yaml` per la modifica.
1. Aggiorna il file `fstab.yaml` nell&#39;archivio GitHub con l&#39;URL dell&#39;istanza AEM Forms as a Cloud Service.

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   Ad esempio, se l’archivio GitHub è denominato &quot;aemcrosswalk&quot;, si trova sotto l’account &quot;wkndform&quot; e stai utilizzando il ramo &quot;main&quot;, l’URL dell’istanza di authoring ha l’aspetto seguente:

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. Eseguire il commit delle modifiche nel file `fstab.yaml`.

### Collegare l’istanza AEM all’archivio GitHub

Per collegare l&#39;istanza Autore AEM Forms a [il progetto nell&#39;archivio GitHub](/help/edge/docs/forms/tutorial.md), effettuare le seguenti operazioni:

[1. Creazione di un modulo adattivo basato sul modello Edge Delivery Services](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[2. Individua il contenitore di configurazione del modulo nell’istanza di authoring AEM](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3. Creare il modulo nell’Editor universale](#3-author-the-form-in-the-universal-editor)

[4. Publish e anteprima del modulo](#4-publish-and-preview-the-form)

#### 1. Creazione di un modulo adattivo basato sul modello Edge Delivery Services

1. Accedi all’istanza Autore di AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.1. Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Forms adattivo]**. Viene aperta la procedura guidata. Nella scheda Source, selezionare un modello di modulo basato su Edge Delivery Services:

   ![Crea EDS Forms](/help/edge/assets/create-eds-forms.png){width=50%, align-center}

1. Fare clic su **[!UICONTROL Crea]** per visualizzare la procedura guidata **Crea modulo**.
1. Specifica l&#39;**URL GitHub**. Ad esempio, se l’archivio GitHub è denominato &quot;aemcrosswalk&quot;, si trova sotto l’account &quot;wkndform&quot;, l’URL è:
   `https://github.com/wkndform/aemcrosswalk`
1. Fai clic su **[!UICONTROL Crea]**.

   ![Creazione guidata modulo](/help/edge/assets/create-form-wizard.png){width=50%, align-center}

   Non appena fai clic su **[!UICONTROL Crea]**, il modulo viene aperto nell&#39;editor universale per la creazione.

   ![crea il modulo](/help/edge/assets/author-form.png){width=50%, align-center}

   >[!NOTE]
   >
   > La configurazione dei Edge Delivery Services per i moduli basati sul modello Edge Delivery Services viene creata automaticamente nel contenitore di configurazione del modulo.

#### 2. Individua il contenitore di configurazione del modulo nell’istanza di authoring AEM

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazione Edge Delivery Services]** nell&#39;istanza Autore as a Cloud Service di AEM Forms.
1. Selezionare la cartella corrispondente al nome del modulo. Se ad esempio il modulo è denominato &#39;contact-us&#39;, scegliere la cartella `forms/contact-us`, quindi selezionare la configurazione e pubblicare la configurazione:

   Configurazione ![Edge Delivery Services](/help/forms/assets/aem-instance-eds-configuration.png){width=50%, align-center}

1. Fai clic su **[!UICONTROL Proprietà]** per visualizzare la configurazione.\
   ![Configurazione creata automaticamente](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%, align-center}

   Puoi lasciare invariata l’opzione Host di Edge. Il modulo viene pubblicato sia in ambiente di anteprima (.page) che in ambiente live (.live).

1. Fai clic su **[!UICONTROL Salva e chiudi]**. La configurazione viene salvata.

#### 3. Creare il modulo nell’Editor universale

Quando si fa clic su **[!UICONTROL Crea]**, il modulo viene aperto nell&#39;Editor universale per la creazione.

1. Apri il browser Contenuto e passa al componente **[!UICONTROL Modulo adattivo]** nella **struttura contenuto**.

   ![struttura contenuto](/help/edge/assets/content-tree.png){width=50%, align-center}

1. Fai clic sull&#39;icona **[!UICONTROL Aggiungi]** e aggiungi i componenti desiderati dall&#39;elenco **Componenti modulo adattivo**.

   ![aggiungi componente](/help/edge/assets/add-component.png){width=50%, align-center}

1. Seleziona il componente Modulo adattivo aggiunto e aggiornane le proprietà utilizzando **[!UICONTROL Proprietà]**.

   ![apri proprietà](/help/edge/assets/component-properties.png){width=50%, align-center}

   La schermata seguente mostra il semplice modulo &quot;Contact Us&quot; (Contattaci) creato in Universal Editor:

   ![contattaci modulo](/help/edge/assets/contact-us.png){width=50%, align-center}

#### 4. Publish e anteprima del modulo

Pubblicare il modulo in Edge Delivery Services facendo clic sul pulsante **[!UICONTROL Publish]** nell&#39;angolo superiore destro di Universal Editor.

![pubblica modulo](/help/edge/assets/publish-form.png){width=50%, align-center}


Di seguito viene illustrato come accedere al modulo sui Edge Delivery Services:

* **Versione di staging (per il test)**: la versione di staging visualizza la versione di lavoro non pubblicata del modulo a scopo di test. Utilizza il seguente formato URL per visualizzare in anteprima il modulo prima che venga pubblicato:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  Ad esempio, se l’archivio del progetto è denominato &quot;aemcrosswalk&quot;, si trova sotto l’account &quot;wkndform&quot; e stai utilizzando il ramo &quot;main&quot; e il modulo come &quot;contact us&quot; (contattaci), l’URL della versione di staging avrà l’aspetto seguente:
https://main--aemcrosswalk--wkndform.aem.page/content/forms/af/contact-us

* **Versione live (modulo pubblicato)**:   La versione live mostra la versione pubblicata più di recente del modulo, accessibile agli utenti finali. Utilizza il seguente formato URL per accedere alla versione live pubblicata del modulo:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  Ad esempio, se l’archivio del progetto è denominato &quot;aemcrosswalk&quot;, si trova sotto l’account &quot;wkndform&quot; e stai utilizzando il ramo &quot;main&quot; e il modulo come &quot;contact us&quot; (contattaci), l’URL della versione di staging avrà l’aspetto seguente:
https://main--aemcrosswalk--wkndform.aem.live/content/forms/af/contact-us

La struttura URL rimane invariata sia per le versioni in staging che per quelle live. Tuttavia, il contenuto visualizzato varia in base al contesto:

![Visualizza modulo pubblicato](/help/edge/assets/eds-view-publish-form.png){width=50%, align-center}

## Risoluzione dei problemi

Problemi durante il caricamento del modulo? Di seguito sono riportati alcuni problemi comuni e come risolverli:

* **URL modulo**: verifica che l&#39;URL del modulo non includa l&#39;estensione &quot;.html&quot; alla fine. Il servizio di consegna Edge non richiede questa estensione.

* **URL autore AEM** L: verificare che l&#39;URL dell&#39;autore AEM elencato nel file `fstab.yaml` sia formattato correttamente. Dovrebbero essere inclusi i seguenti dettagli:

   * Il proprietario GitHub corretto
   * Il nome dell’archivio corretto
   * Ramo specifico utilizzato per i Edge Delivery Services

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## Consulta anche

{{see-more-forms-eds}}