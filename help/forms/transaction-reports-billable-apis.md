---
title: API rapporti di transazioni fatturabili
description: Elenco di tutte le API contabilizzate come transazioni
feature: Adaptive Forms, Foundation Components
exl-id: 6dfcac3e-5654-4b4f-9134-0cd8be24332e
role: Admin, Developer, User
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 34%

---


# API rapporti di transazioni fatturabili {#transaction-reports-billable-apis}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/transaction-reports/transaction-reports-billable-apis) |
| AEM as a Cloud Service | Questo articolo |


AEM Forms fornisce diverse API per inviare moduli, elaborare documenti ed eseguire il rendering di documenti. Alcune API sono contabilizzate come transazioni e altre sono libere di utilizzare. Questo documento fornisce un elenco di tutte le API contabilizzate come transazioni in un report sulle transazioni. Di seguito sono riportati alcuni scenari comuni in cui viene utilizzata un’API fatturabile:

* Invio di un modulo adattivo
* Conversione di un documento da un formato a un altro
* Appiattimento di un documento di Dynamic PDF
* Generazione di un documento di record (tramite il servizio Forms o il servizio di output)
* Unione di un documento PDF interattivo con un altro documento PDF
* Utilizzo dei passaggi Assegna attività e API di comunicazione dei flussi di lavoro AEM

Le API di fatturazione non tengono conto del numero di pagine, della lunghezza di un documento o modulo o del formato finale del documento sottoposto a rendering. Un report di transazioni suddivide le transazioni in due categorie: Forms Inviato e Documenti Rendering.

* **Forms inviato:** Quando i dati vengono inviati da qualsiasi tipo di modulo creato con AEM Forms e vengono inviati a qualsiasi archivio di dati o database, viene considerato invio modulo. Ad esempio, l’invio di un modulo adattivo o di un set di moduli è considerato come un modulo inviato. Se una serie di moduli dispone di 5 moduli e quando la serie di moduli viene inviata, il servizio di reporting delle transazioni la conta come 5 invii.

* **Documenti sottoposti a rendering:** La generazione di un documento mediante la combinazione di un modello e di dati, la firma o la certificazione digitale di un documento, l&#39;utilizzo di API di servizi di documentazione fatturabili per i servizi di documentazione o la conversione di un documento da un formato a un altro sono considerati documenti sottoposti a rendering.

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_submission_graph_en"
>title="Tracciamento degli invii dei moduli"
>abstract="Questo grafico rappresenta il numero di invii di moduli adattivi durante specifici periodi di tempo. L’aumento degli invii potrebbe indicare che il modulo sta diventando più popolare o che è necessario raccogliere più dati dagli utenti. **Nota:** il grafico fornisce dati specifici per l’istanza corrente, consentendo di analizzare rapidamente le tendenze e prendere decisioni consapevoli. Per i dati degli invii delle altre istanze, accedi semplicemente alla dashboard della rispettiva istanza."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_conversions_graph_en"
>title="Tracciamento delle rappresentazioni di documenti"
>abstract="Questo grafico rappresenta la quantità di rappresentazioni di documenti durante specifici periodi di tempo. **Nota:** il grafico fornisce dati specifici per l’istanza corrente ed è utile per analizzare rapidamente le tendenze e prendere decisioni consapevoli. Per i dati degli invii delle altre istanze, accedi semplicemente alla dashboard della rispettiva istanza."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_newForms_graph_en"
>title="Tracciamento dei nuovi moduli"
>abstract="Il grafico fornisce informazioni sul numero di nuovi moduli creati durante specifici periodi di tempo. **Nota:** il grafico fornisce dati specifici per l’istanza di authoring di AEM Forms corrente. Per visualizzare i dati delle altre istanze, accedi alla dashboard della rispettiva istanza."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_publishedForms_graph_en"
>title="Tracciamento dei moduli pubblicati"
>abstract="Il grafico fornisce informazioni sul numero di moduli pubblicati. **Nota:** il grafico fornisce dati specifici per l’istanza di pubblicazione di AEM Forms corrente. Per visualizzare i dati di conversione delle altre istanze, accedi alla dashboard della rispettiva istanza."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formCreationAvgDuration_graph_en"
>title="Durata media per la generazione dei moduli"
>abstract="Il grafico mostra il tempo medio impiegato per creare un modulo. Ogni barra del grafico rappresenta un modulo specifico e l’altezza della barra indica la durata media necessaria per la creazione del modulo durante un determinato intervallo di tempo."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formPublishAvgDuration_en"
>title="Durata media per la creazione dei moduli"
>abstract="Nel grafico viene visualizzato il tempo medio necessario per creare e pubblicare un modulo, misurato dal giorno iniziale in cui il modulo è stato aperto per la modifica. **Nota:** il grafico fornisce dati specifici per l’istanza di authoring di AEM Forms corrente. Per visualizzare i dati delle altre istanze, accedi alla dashboard della rispettiva istanza."


>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formFragments_graph_en"
>title="Tracciamento dei frammenti di modulo"
>abstract="Questo grafico consente di vedere quanti frammenti di modulo utilizzi nei tuoi moduli. **Nota:** il grafico fornisce dati specifici per l’istanza di pubblicazione di AEM Forms corrente. Per visualizzare i dati di conversione delle altre istanze, accedi alla dashboard della rispettiva istanza."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_avgFormPerFragments_graph_en"
>title="Tracciamento del tempo medio per frammento di modulo"
>abstract="Nel grafico viene visualizzato il tempo medio necessario per creare un frammento di modulo, misurato dal giorno iniziale in cui il frammento di modulo è stato aperto per la modifica. **Nota:** il grafico fornisce dati specifici per l’istanza di pubblicazione di AEM Forms corrente. Per visualizzare i dati di conversione delle altre istanze, accedi alla dashboard della rispettiva istanza."


<!-- 

>[!NOTE]
>
>Transaction Reports UI displays three categories: Forms Submitted, Documents Rendered, and Documents Processed. Both Documents Rendered and Documents Processed are accounted as Documents Rendered.
-->


<!--

## Billable Document Services APIs {#billable-document-services-apis}

### Generate PDF Service {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## API di Document Services fatturabili {#billable-document-services-apis}

### Genera servizio PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#section/Before-you-start" target="_blank">createPDF</a></td>
   <td>Genera un documento PDF da un modello e unisce i dati ad esso.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePrintedOutput/post" target="_blank">exportPDF</a></td>
   <td>Converte il file XDP o il documento PDF in tipi di file supportati.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

### Servizio di output {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutput" target="_blank">generatePDFOutput</a></td>
   <td>Unisce dati e modelli per creare un documento PDF.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutputOptions" target="_blank">generatePDFOutput (PDFOutputOptions)</a></td>
   <td>Unisce dati e modelli per creare un documento PDF.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePDFOutputBatch</a></td>
   <td>Unisce dati e modelli per creare un set di documenti PDF.</td>
   <td>Documenti elaborati</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutput" target="_blank">generatePrintedOutput</a></td>
   <td>Converte i documenti XDP e PDF in formati PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions" target="_blank">generatePrintedOutput (PrintedOutputOptions)</a></td>
   <td>Converte i documenti XDP e PDF in formati PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Converte un set di documenti XDP e PDF in un set di formati di file PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documenti elaborati</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
 </tbody>
</table>

### Servizio DocAssurance {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/docassurance/#tag/DocAssurance" target="_blank">secureDocument</a><br /> </td>
   <td>Questa API consente di proteggere il documento. Puoi utilizzare l’API per firmare, certificare, estendere o crittografare un documento PDF.</td>
   <td>Documenti elaborati</td>
   <td>Vengono fatturate solo le operazioni di firma e certificazione di secureDocument.</td>
  </tr>
 </tbody>
</table>

### Servizio Document of Record (DOR) {#document-of-record-dor-forms-service-and-output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://opensource.adobe.com/aem-forms-af-runtime/api/#tag/Generate-DoR/operation/generateDoR" target="_blank">rendering</a></td>
   <td>Richiama il metodo di rendering specificato per generare un documento di record utilizzando i parametri forniti.</td>
   <td>Documenti elaborati con il servizio Forms</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed using Output Service</td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

<!--

### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Convert PDF Service {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Converts a PDF document to a list of image documents. Supported image formats are JPEG, JPEG2K, PNG, and TIFF.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Converts a Flat PDF file to PostScript format using the options specified in the option spec.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Barcoded Forms Service {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>Decodes all the barcodes in a Document object and returns an org.w3c.dom.Document object that contains data that was retrieved from the barcode.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

### Servizio assemblatore {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX">richiamare</a></td>
   <td>Esegue il DDX sui documenti di input specificati e restituisce un oggetto contenente i documenti risultanti</td>
   <td>Documenti elaborati</td>
   <td>Le seguenti operazioni non sono contabilizzate come operazioni:
    <ul>
     <li>Creazione di pacchetti o portfolio</li>
     <li>Unione di più XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX" target="_blank">richiamare</a></td>
   <td>Esegue il DDX sui documenti di input specificati e restituisce un oggetto contenente i documenti risultanti</td>
   <td>Documenti elaborati</td>
   <td>Tutti i formati di file di input supportati dai servizi PDF Generator, Forms e Output, il servizio Assembler supporta tutti questi formati come formati di file di output. </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA">toPDFA</a></td>
   <td>Convertire un documento specificato in PDF/A utilizzando le opzioni specificate.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

L’utilizzo dell’API di richiamo viene conteggiato come una transazione, quando si eseguono una o più delle seguenti operazioni:

1. Conversione da formati non PDF a formati PDF. <!--For instance, the conversion from XDP format to PDF format, catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. Conversione dal formato PDF al formato PDF/A.
1. Conversione dal formato PDF a formati non PDF. Gli esempi includono la trasformazione da PDF a formato immagine o la conversione da PDF a formato testo.


>[!NOTE]
>
>* L’API di richiamo del servizio assembler può chiamare internamente un’API fatturabile di un altro servizio a seconda dell’input. Pertanto, l’API di richiamo può essere contabilizzata come nessuna, singola o più transazioni. Il numero di transazioni conteggiate dipende dall’input e dalle API interne richiamate.
>* Un singolo documento PDF prodotto utilizzando il servizio assembler può essere contabilizzato come nessuna, singola o più transazioni. Il numero di transazioni conteggiate dipende dal codice fornito.
>

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. In order for a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## API di acquisizione dati fatturabili {#billable-data-capture-apis}

Tutti gli eventi di invio dei moduli adattivi vengono contabilizzati come transazioni. Per impostazione predefinita, l’invio di un modulo PDF non viene contabilizzato come una transazione. Utilizza il fornito [API registratore transazioni](record-transaction-custom-implementation.md) per registrare un invio di PDF forms come transazione.

### Moduli adattivi {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso d’uso</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td>Invio di un modulo adattivo</td>
   <td>Invia un modulo adattivo all’azione di invio configurata. </td>
   <td>Moduli inviati</td>
   <td>
    <ul>
     <li>Account invio corretto per una o due transazioni. Il numero di transazioni conteggiate dipende dal tipo di azione di invio utilizzato per la sottomissione. Ad esempio, l’invio di PDF tramite un’azione di invio tramite e-mail tiene conto di due conteggi di transazioni. Una transazione per l’invio di moduli e un’altra per PDF generata utilizzando il servizio Document of Record (DOR). </li>
     <li>L’utilizzo del modulo adattivo all’interno di un modulo adattivo (set di moduli adattivi) contabilizza una sola transazione. All’interno di un modulo adattivo è possibile disporre di un numero qualsiasi di moduli adattivi.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

<!--

### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Form set {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting a form set</td>
   <td>Submits form set to the submit URL configured in the form set.</td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
     <li>Every form in an HTML5 Forms form set accounts as a separate transaction. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

## Flussi di lavoro AEM fatturabili incentrati su moduli {#billable--form-centric-aem-workflows}

Assegna task e documenta i passaggi dei flussi di lavoro AEM incentrati su moduli vengono contabilizzati come transazioni. Se un passaggio del flusso di lavoro contabilizza una transazione e il flusso di lavoro non viene completato, il conteggio delle transazioni non viene stornato.

<!--
Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.
-->


<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->

### Flussi di lavoro AEM incentrati su moduli {#form-centric-aem-workflows}

<table>
 <tbody>
  <tr>
   <td><p>Caso d’uso</p> </td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td>Invio di un passaggio Assegna attività</td>
   <td>Moduli inviati</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Invio di un punto d'inizio di un'applicazione del flusso di lavoro </td>
   <td>Moduli inviati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Registrazione di API fatturabili come transazioni per il codice personalizzato {#recording-billable-apis-as-transactions-for-custom-code}

Azioni come l’invio di un modulo PDF, l’utilizzo dell’interfaccia utente dell’agente per visualizzare in anteprima una comunicazione interattiva, l’utilizzo di un invio di modulo non standard e le implementazioni personalizzate non vengono considerate come transazioni. AEM Forms fornisce un’API per registrare azioni quali le transazioni. Puoi richiamare l’API dalle implementazioni personalizzate a [registrare una transazione](/help/forms/record-transaction-custom-implementation.md).

## Articoli correlati {#related-articles}

* [Registrare una transazione per le implementazioni personalizzate](/help/forms/record-transaction-custom-implementation.md)
