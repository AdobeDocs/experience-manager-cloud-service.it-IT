---
title: Pubblicare un modulo Edge Delivery Services di AEM Forms
description: Pubblicare un modulo Edge Delivery Services di AEM Forms
feature: Edge Delivery Services
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 100%

---

# Pubblicare il modulo e iniziare a raccogliere i dati

Quando vuoi condividere il modulo con i clienti per la raccolta o l’invio dei dati, è sufficiente pubblicarlo, rendendolo facilmente disponibile per l’utilizzo da parte della clientela.

![Ecosistema di authoring basato su documenti](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## Prerequisiti

- Hai un progetto AEM basato su [moduli AEM ricorrenti](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) oppure [hai aggiunto il blocco di moduli adattivi al progetto AEM esistente](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)
- Il modulo è stato interamente testato ed è pronto per l’uso.
- Il [foglio di calcolo è configurato](/help/edge/docs/forms/submit-forms.md) per accettare i dati.


## Pubblicare il modulo

+++ &#x200B;1. Pubblicare il foglio di calcolo

1. Apri l’account Microsoft SharePoint o Google Drive e passa alla directory del progetto AEM Edge Delivery.

1. Apri il foglio di calcolo contenente il modulo. Ad esempio, il modulo di [interrogazione](/help/edge/assets/enquiry.xlsx) della cartella di lavoro Microsoft Excel.

1. Utilizza [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare l’anteprima del foglio.

   ![Utilizza AEM Sidekick per visualizzare l’anteprima del foglio](/help/edge/assets/preview-form.png)

   Una volta completata correttamente l’operazione di anteprima, il contenuto del foglio di calcolo viene convertito in formato JSON. La pagina di anteprima presenta quindi questo contenuto in un formato tabella strutturato. Ad esempio, l’immagine allegata illustra il contenuto di un modulo “enquiry”.

   ![Anteprima dei moduli in formato JSON](/help/edge/assets/forms-preview-json-format.png)

1. Utilizza AEM Sidekick per pubblicare il foglio. Assicurati di acquisire l’URL di pubblicazione, in quanto è necessario per il rendering del modulo nella sezione successiva. Il formato dell’URL è attualmente il seguente:


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form>.json
   ```

   - `<branch>` fa riferimento al ramo dell’archivio GitHub.
   - `<repository>` denota l’archivio GitHub.
   - `<owner>` fa riferimento al nome utente dell’account GitHub che ospita l’archivio GitHub.

   Ad esempio, se l’archivio del progetto è denominato “wefinance”, si trova sotto l’account “wkndform” e stai utilizzando il ramo “main” e il modulo come “interrogazione”, l’URL avrà l’aspetto seguente:

   `https://main--wefinance--wkndform.aem.live/enquiry.json`
&lt;!—(https://main--wefinance--wkndform.aem.live/enquiry.json)-->

+++

+++ &#x200B;2. Aggiungere il modulo alla pagina web

Aggiungi il `<form>.json` a una pagina web per facilitare l’interazione con il cliente, consentendo ai compilatori di moduli di compilare e inviare facilmente il modulo.


Per aggiungere il modulo alla pagina web:

1. accedi all’account Microsoft SharePoint o Google Drive e passa alla `[AEM Edge Delivery project directory]`.

1. Apri un file del documento in cui desideri incorporare il modulo. Ad esempio, puoi aprire il file [enquiry-form.docx](/help/edge/assets/enquiry-form.docx) oppure, in alternativa, creare un nuovo documento.

1. Identifica la sezione desiderata all’interno del documento in cui desideri inserire il modulo, quindi passa a tale sezione.

1. Aggiungi al file un blocco denominato “Modulo”. Ad esempio, se l’archivio del progetto è denominato “wefinance”, si trova sotto il proprietario dell’account “wkndform” e stai utilizzando il ramo “main”.

   | Modulo |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |

   ![Aggiungi al file un blocco denominato “Modulo”](/help/edge/assets/enquiry-doc-to-embed-form.png)

   Questo blocco funge da segnaposto in cui è incorporato il modulo. Nella seconda riga del blocco, aggiungi l’URL del file `<form>.json` come collegamento ipertestuale.

   >[!IMPORTANT]
   >
   >
   > Verifica che l’URL sia formattato come collegamento ipertestuale anziché essere visualizzato come testo normale.

   Utilizza l’URL di anteprima (.URL della pagina) a scopo di sviluppo o test oppure l’URL di pubblicazione (.live) per la produzione.

   Ad esempio, se l’archivio del progetto è denominato “wefinance”, si trova sotto il proprietario dell’account “wkndform” e stai utilizzando il ramo “main”.

   Di seguito sono riportati alcuni esempi con URL di anteprima e pubblicazione:

   **URL di anteprima**

   | Modulo |
   |---|
   | `https://main--wefinance--wkndform.aem.page/enquiry.json` |


   **URL di pubblicazione**

   | Modulo |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |

1. Utilizza [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare l’anteprima della pagina web. Nella pagina viene ora visualizzato il modulo. Ad esempio, questo è il modulo basato su [foglio di calcolo interrogazione](/help/edge/assets/enquiry-form.docx):


   ![Un esempio di modulo EDS](/help/edge/assets/updated-form.png)

1. Utilizza AEM Sidekick per pubblicare il modulo. Ora, ogni cliente può compilare il modulo e inviarlo.

+++

## Risoluzione dei problemi

+++ Impossibile inviare i dati al modulo

Se si verifica un errore simile al seguente messaggio, il foglio di calcolo non è ancora configurato con i dati di [accetta gli elementi inviati](/help/edge/docs/forms/submit-forms.md).

![errore durante l’invio del modulo](/help/edge/assets/form-error.png)

+++



