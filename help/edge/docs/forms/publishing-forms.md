---
title: Pubblicazione di moduli per Edge Delivery Services
description: Scopri come funziona la pubblicazione dei moduli con Edge Delivery Services e come pubblicare moduli AEM con Edge Delivery Services.
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: b90c27e3-22ea-4b18-b16e-a5c5a0ed58b8
source-git-commit: 67384a9141ced3bf5be63c8489dd5c329a288056
workflow-type: ht
source-wordcount: '993'
ht-degree: 100%

---

# Pubblicazione di moduli per Edge Delivery Services

Questo articolo ti guida attraverso il processo di pubblicazione dei moduli in Edge Delivery Services di AEM.
Per pubblicare i moduli in Edge Delivery Services, devi prima stabilire una connessione tra l’ambiente AEM e l’archivio GitHub. Una volta connessi, è possibile creare i moduli utilizzando l’editor universale, che segue un approccio WYSIWYG (What You See Is What You Get) per un’esperienza utente fluida e coerente con Sites.

## Prerequisiti

* Non hai esperienza con i Moduli adattivi? Configura l’archivio GitHub seguendo il [tutorial](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) fornito.
* Se utilizzi già Edge Delivery Services, aggiungi la versione più recente del [Blocco moduli adattivi](/help/edge/docs/forms/tutorial.md#) all’archivio GitHub.
* L’istanza di authoring di AEM Forms include un modello basato su Edge Delivery Services. Assicurati che nel tuo ambiente sia installata la [versione più recente dei Componenti core](https://github.com/adobe/aem-core-forms-components).
* Tieni a portata di mano l’URL dell’istanza di authoring di AEM Forms as a Cloud Service e dell’archivio GitHub.

## Pubblicare moduli per Edge Delivery Services

Per pubblicare i moduli per Edge Delivery Services, esegui i passaggi seguenti:

[1. Collega l’archivio GitHub all’istanza AEM](#link-github-repository-to-aem-instance)

[2. Collega l’istanza AEM all’archivio GitHub](#link-aem-instance-to-github-repository)

### Collegare l’archivio GitHub all’istanza AEM

Per collegare [il progetto nell’archivio GitHub](/help/edge/docs/forms/tutorial.md) all’istanza di authoring di AEM Forms, esegui i seguenti passaggi:

1. Passa all’archivio GitHub creato o configurato per i tuoi Edge Delivery Services.
1. Apri il file `fstab.yaml` per la modifica.
1. Aggiorna il file `fstab.yaml` nell’archivio GitHub con l’URL dell’istanza AEM Forms as a Cloud Service.

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   Ad esempio, se l’archivio del progetto è denominato “aemcrosswalk”, si trova sotto l’account “wkndforms” e stai utilizzando il ramo “main”, l’URL dell’istanza di authoring avrà l’aspetto seguente:

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. Conferma le modifiche al file `fstab.yaml`.

### Collegare l’istanza AEM all’archivio GitHub

Per collegare l’istanza di authoring AEM Forms al [progetto nell’archivio GitHub](/help/edge/docs/forms/tutorial.md), effettua i seguenti passaggi:

[1. Crea un modulo adattivo basato sul modello Edge Delivery Services](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[2. Individua il contenitore di configurazione del modulo nell’istanza di authoring AEM](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3. Creare il modulo nell’editor universale](#3-author-the-form-in-the-universal-editor)

[4. Pubblicare e visualizzare l’anteprima del modulo](#4-publish-and-preview-the-form)

#### 1. Crea un modulo adattivo basato sul modello Edge Delivery Services

1. Accedi all’istanza di authoring di AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.1. Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Moduli adattivi]**. Viene aperta la procedura guidata. Nella scheda Sorgente, seleziona un modello di modulo basato su Edge Delivery Services:

   ![Creare moduli EDS](/help/edge/assets/create-eds-forms.png){width=50%, align-center}

1. Fai clic su **[!UICONTROL Crea]** per visualizzare la procedura guidata **Crea modulo**.
1. Specifica l’**URL di GitHub**. Ad esempio, se l’archivio GitHub è denominato “aemcrosswalk”, si trova sotto l’account “wkndform”, l’URL è:
   `https://github.com/wkndform/aemcrosswalk`
1. Fai clic su **[!UICONTROL Crea]**.

   ![Creare una procedura guidata per modulo ](/help/edge/assets/create-form-wizard.png){width=50%, align-center}

   Non appena fai clic su **[!UICONTROL Crea]**, il modulo viene aperto nell’editor universale per la creazione.

   ![creazione del modulo](/help/edge/assets/author-form.png){width=50%, align-center}

   >[!NOTE]
   >
   > La configurazione di Edge Delivery Services per i moduli basati sul modello Edge Delivery Services viene creata automaticamente nel contenitore di configurazione del modulo.

#### 2. Individua il contenitore di configurazione del modulo nell’istanza di authoring AEM

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Configurazione Edge Delivery Services]** nell’istanza di authoring as a Cloud Service di AEM Forms.
1. Seleziona la cartella corrispondente al nome del modulo. Se ad esempio il modulo è denominato “contattaci” scegli la cartella `forms/contact-us`, quindi seleziona la configurazione e pubblicala:

   ![Configurazione Edge Delivery Services](/help/forms/assets/aem-instance-eds-configuration.png){width=50%, align-center}

1. Fai clic su **[!UICONTROL Proprietà]** per visualizzare la configurazione.\
   ![Configurazione creata automaticamente](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%, align-center}

   È possibile lasciare invariata l’opzione host di Edge. Il modulo viene pubblicato sia nell’ambiente di anteprima (.page) sia nell’ambiente live (.live).

1. Fai clic su **[!UICONTROL Salva e chiudi]**. La configurazione viene salvata.

#### 3. Creare il modulo nell’editor universale

Quando fai clic su **[!UICONTROL Crea]**, il modulo viene aperto nell’editor universale per la creazione.

1. Apri il Browser dei contenuti e accedi al componente **[!UICONTROL Modulo adattivo]** nella **Struttura contenuto**.

   ![struttura contenuto](/help/edge/assets/content-tree.png){width=50%, align-center}

1. Fai clic sull’icona **[!UICONTROL Aggiungi]** e aggiungi i componenti desiderati dall’elenco **Componenti modulo adattivo**.

   ![aggiungi componente](/help/edge/assets/add-component.png){width=50%, align-center}

1. Seleziona il componente Modulo adattivo aggiunto e aggiornane le proprietà utilizzando **[!UICONTROL Proprietà]**.

   ![apri proprietà](/help/edge/assets/component-properties.png){width=50%, align-center}

   La schermata seguente mostra il modulo “Contattaci” semplice creato nell’editor universale:

   ![modulo contattaci](/help/edge/assets/contact-us.png){width=50%, align-center}

#### 4. Pubblicare e visualizzare l’anteprima del modulo

Ora, pubblica il modulo in Edge Delivery Services facendo clic sul pulsante **[!UICONTROL Pubblica]** nell’angolo in alto a destra dell’editor universale.

![pubblica modulo](/help/edge/assets/publish-form.png){width=50%, align-center}


Di seguito viene descritto come accedere al modulo su Edge Delivery Services:

* **Versione di staging (per il test)**: la versione di staging mostra la versione di lavoro non pubblicata del modulo a scopo di test. Utilizza il seguente formato URL per visualizzare l’anteprima del modulo prima della pubblicazione:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  Ad esempio, se l’archivio del progetto è denominato “aemcrosswalk”, si trova nell’account “wkndforms” e stai utilizzando il ramo “main” e il modulo come “contattaci”, la versione di staging dell’URL avrà l’aspetto seguente:
https://main--aemcrosswalk--wkndform.aem.page/content/forms/af/contact-us

* **Versione live (modulo pubblicato)**: la versione live mostra la versione pubblicata più recente del modulo, accessibile agli utenti finali. Utilizza il seguente formato URL per accedere alla versione live pubblicata del modulo:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  Ad esempio, se l’archivio del progetto è denominato  “aemcrosswalk”, si trova sotto l’account “wkndforms” e stai utilizzando il ramo “main” e il modulo come “contattaci”, la versione in staging dell’URL avrà l’aspetto seguente:
https://main--aemcrosswalk--wkndform.aem.live/content/forms/af/contact-us

La struttura URL rimane invariata sia per le versioni di staging sia per quelle live. Tuttavia, il contenuto visualizzato varia in base al contesto:

![Visualizza modulo pubblicato](/help/edge/assets/eds-view-publish-form.png){width=50%, align-center}

## Risoluzione dei problemi

Ci sono problemi durante il caricamento del modulo? Di seguito sono riportati alcuni problemi comuni e come risolverli:

* **URL modulo**: verifica che l’URL del modulo non includa l’estensione “.html” alla fine. Edge Deliver Service non richiede questa estensione.

* **URL di authoring di AEM**: verifica che l’URL di authoring di AEM elencato nel file `fstab.yaml` sia formattato correttamente. Dovrebbe includere i seguenti dettagli:

   * Il proprietario GitHub corretto
   * Il nome dell’archivio corretto
   * Il ramo specifico utilizzato per Edge Delivery Services

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## Consulta anche

{{see-more-forms-eds}}
