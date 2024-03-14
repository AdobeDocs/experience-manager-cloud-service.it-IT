---
title: Pubblicare un modulo Edge Delivery Services di AEM Forms
description: Pubblicare un modulo Edge Delivery Services di AEM Forms
feature: Edge Delivery Services
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
source-git-commit: b32e04dec83992ebfcea7874932a5ab77a1eaa70
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Pubblicare il modulo

Quando si è pronti a condividere il modulo con i clienti per la raccolta o l&#39;invio dei dati, è sufficiente pubblicarlo, rendendolo facilmente disponibile per l&#39;utilizzo da parte dei clienti.

![Ecosistema di authoring basato su documenti](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## Prerequisiti

* Hai un progetto AEM basato su [AEM Forms boilerplate](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) o [è stato aggiunto il blocco Forms adattivo al progetto AEM esistente](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)
* Il modulo è stato testato e pronto per l&#39;uso.
* Il tuo [il foglio di calcolo è configurato](/help/edge/docs/forms/submit-forms.md) per accettare i dati.


## Pubblicare il modulo

+++ 1. Pubblicare il foglio di calcolo

1. Apri l’account Microsoft SharePoint o Google Drive e passa alla directory del progetto AEM Edge Delivery.

1. Aprire il foglio di calcolo contenente il modulo. Ad esempio, il `enquiry` cartella di lavoro di Microsoft Excel modulo.

1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare l&#39;anteprima del foglio.

   ![Utilizza AEM Sidekick per visualizzare l’anteprima del foglio](/help/edge/assets/preview-form.png)

   Una volta completata correttamente l’operazione di anteprima, il contenuto del foglio di calcolo viene convertito in formato JSON. La pagina di anteprima presenta quindi questo contenuto in un formato tabella strutturato. Ad esempio, l’immagine allegata illustra il contenuto di un modulo di richiesta di informazioni.

   ![Forms Anteprima formato JSON](/help/edge/assets/forms-preview-json-format.png)

1. Utilizza AEM Sidekick per pubblicare il foglio. Assicurati di acquisire l’URL di pubblicazione, in quanto è necessario per il rendering del modulo nella sezione successiva. Il formato dell’URL è il seguente:


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` fa riferimento al ramo dell’archivio GitHub.
   * `<repository>` denota l’archivio GitHub.
   * `<owner>` fa riferimento al nome utente dell’account GitHub che ospita l’archivio GitHub.

   Ad esempio, se l’archivio del progetto è denominato &quot;portale&quot;, si trova sotto l’account &quot;wkndforms&quot; e stai utilizzando il ramo &quot;principale&quot;, l’URL avrà l’aspetto seguente:

   `https://main--portal--wkndforms.hlx.page/enquiry.json`

+++

+++ 2. Aggiungere il modulo alla pagina Web

Aggiungi il `<form>.json` a una pagina web per facilitare l’interazione con il cliente, consentendo ai compilatori di moduli di compilare e inviare facilmente il modulo.


Per aggiungere il modulo alla pagina Web:

1. Accedere al proprio account Microsoft SharePoint o Google Drive e passare al `[AEM Edge Delivery project directory]`.

1. Aprire un file di documento in cui si desidera incorporare il modulo. Ad esempio, puoi aprire `index.docx` oppure creare un nuovo documento.

1. Identificare la sezione desiderata all&#39;interno del documento in cui si desidera inserire il modulo e passare di conseguenza.

1. Aggiungi al file un blocco denominato &quot;Modulo&quot;, simile all’esempio fornito di seguito:

   | Modulo |
   |---|
   | [https://main--wefinance--wkndforms.hlx.live/enquiry.json](https://main--wefinance--wkndforms.hlx.live/enquiry.json) |

   ![Aggiungi al file un blocco denominato &quot;Modulo&quot;](/help/edge/assets/enquiry-doc-to-embed-form.png)

   Questo blocco funge da segnaposto in cui è incorporato il modulo. Nella seconda riga del blocco, aggiungi l’URL del `<form>.json` come collegamento ipertestuale.

   >[!IMPORTANT]
   >
   >
   > Verificare che l&#39;URL sia formattato come collegamento ipertestuale anziché come testo normale.

   Utilizza l’URL di anteprima (.page URL) a scopo di sviluppo o test oppure l’URL di pubblicazione (.live) per la produzione. Di seguito sono riportati alcuni esempi con URL di anteprima e pubblicazione:

   **URL di anteprima**
| Modulo | |—| | [https://main--wefinance--wkndforms.hlx.page/enquiry.json](https://main--wefinance--wkndforms.hlx.page/enquiry.json)  |


   **URL di pubblicazione**
| Modulo | |—| | [https://main--wefinance--wkndforms.hlx.live/enquiry.json](https://main--wefinance--wkndforms.hlx.live/enquiry.json)  |

1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare l&#39;anteprima della pagina web. Nella pagina viene ora visualizzato il modulo. Ad esempio, questo è il modulo basato su [foglio di calcolo interrogazione](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   ![Un esempio di modulo EDS](/help/edge/assets/eds-form.png)

1. Utilizza AEM Sidekick per pubblicare il modulo. Ora i tuoi clienti possono compilare il modulo e inviarlo.

+++

## Risoluzione dei problemi

+++ Impossibile inviare i dati al modulo

Se si verifica un errore simile al seguente messaggio, il foglio di calcolo non è configurato per [accetta gli elementi inviati](/help/edge/docs/forms/submit-forms.md) ancora dati.

![errore durante l’invio del modulo](/help/edge/assets/form-error.png)

+++


## Consulta anche

{{see-more-forms-eds}}
