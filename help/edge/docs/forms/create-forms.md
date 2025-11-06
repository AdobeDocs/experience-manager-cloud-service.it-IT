---
title: Creare un modulo utilizzando il Blocco moduli adattivi
description: Guida introduttiva a Edge Delivery Services per AEM Forms. Crea rapidamente moduli perfetti. Authoring basato su documento di AEM Forms Edge Delivery = velocità sorprendente e moduli compatibili con SEO per utenti e motori di ricerca più soddisfatti.
feature: Edge Delivery Services
role: Admin, Developer
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 100%

---

# Creare un modulo utilizzando il Blocco moduli adattivi

>[!VIDEO](https://video.tv.adobe.com/v/3427881?quality=12&learn=on)

AEM Forms Edge Delivery fornisce un blocco, noto come Blocco moduli adattivi, per facilitare la creazione di moduli per l’acquisizione e l’archiviazione dei dati acquisiti. È possibile [creare un nuovo progetto AEM preconfigurato con Blocco moduli adattivi](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) o [aggiungere il Blocco moduli adattivi a un progetto AEM esistente](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project).

Questi moduli inviano i dati direttamente a un file Microsoft Excel o Fogli Google, consentendo di utilizzare un ecosistema dinamico e API affidabili di Fogli Google, Microsoft Excel e Microsoft SharePoint per elaborare facilmente i dati inviati o avviare un flusso di lavoro aziendale esistente.

![Ecosistema di authoring basato sul documento](/help/edge/assets/document-based-authoring-workflow-create-form.png)


## Prerequisiti

Prima di iniziare, assicurati di aver completato i seguenti passaggi:

- Configura un [progetto AEM utilizzando AEM Forms standard](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) [Blocco moduli adattivi aggiunto al progetto AEM esistente](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) e clona l’archivio GitHub corrispondente sul computer locale.
<!--In this document, the local folder of your Edge Delivery Services (EDS) project is referred as `[EDS Project repository]`.  -->
- Assicurati di avere accesso a Fogli Google o Microsoft SharePoint. Per impostare Microsoft SharePoint come origine di contenuto, vedi [Come usare SharePoint](https://www.aem.live/docs/setup-customer-sharepoint).



## Creare un modulo

<!--
+++ Step 1: Add the Adaptive Forms Block to your Edge Delivery Services (EDS) project.

The Adaptive  empowers users to create forms for an Edge Delivery Service Site. However, this block isn't included in the default AEM boilerplate (used to create an Edge Delivery Services project). To seamlessly integrate the Adaptive Forms Block into your Edge Delivery Services project:

1. **Clone the Adaptive Forms Block repository**: Clone the [Adaptive Forms Block repository](https://github.com/adobe-rnd/form-block) on your local machine. It contains the code to render the form on an EDS webpage. In this document, the local folder of your Forms Block repository is referred as `[Adaptive Forms Block repository]`.
2. **Locate the Adaptive Forms Block Repository:** Access the [Adaptive Forms Block repository]/blocks/src folder and copy its content. 

3. on your local machine and copy the `form` folder. 
4. **Paste the Adaptive Forms Block's code into your EDS Project:**
Navigate to the [EDS Project repository]/blocks/ folder on your local machine and create a 'form' folder. Paste the `[Adaptive Forms Block repository]/blocks/src content`, copied in perevious step to the `[EDS Project repository]/blocks/form` folder.
1. **Commit Changes to GitHub:** Check in the `[EDS Project repository]/blocks/form` folder and its underlying files to your Edge Delivery Services project on GitHub.

After completing these steps, the Adaptive Forms Block is successfully added to your Edge Delivery Services (EDS) project repository on GitHub. You can now create and add forms to a EDS Sites page.
 

**Troubleshooting GitHub build issues**

Ensure a smooth GitHub build process by addressing potential issues:

- **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file.

- **Handle Linting Errors:**
    Should you come across any linting errors, you can bypass them. Open the [EDS Project]/package.json file and modify the "lint" script from "lint": "npm run lint:js && npm run lint:css" to "lint": "echo 'skipping linting for now'". Save the file and commit the changes to your GitHub project. -->

+++ Passaggio 1: creare un modulo utilizzando Microsoft Excel o foglio Google.

Invece di navigare attraverso processi complessi, la creazione di un modulo può essere ottenuta facilmente utilizzando un foglio di calcolo. È possibile definire le righe e le colonne che costituiranno la struttura del modulo. Ogni riga rappresenta un singolo utente [campo modulo](/help/edge/docs/forms/form-components.md#available-components) e le intestazioni di colonna definiscono le corrispondenti [proprietà campo](/help/edge/docs/forms/form-components.md#components-properties).

Ad esempio, prendi in considerazione il seguente foglio di calcolo in cui le righe contornano i campi per un foglio di calcolo di [interrogazione](/help/edge/assets/enquiry.xlsx) e le intestazioni di colonna definiscono le relative proprietà:

![Foglio di calcolo di interrogazione](/help/edge/assets/enquiry-form-spreadsheet.png)

Per procedere con la creazione del modulo:

1. Accedi alla cartella del progetto AEM Edge Delivery su Microsoft SharePoint o Google Drive.

1. Crea una cartella di lavoro di Microsoft Excel o un foglio di Google ovunque all’interno della directory di progetto AEM Edge Delivery. Ad esempio, crea un foglio di calcolo denominato `enquiry` nella directory del progetto AEM Edge Delivery su Google Drive.

   <!-- ![Sample Content on Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)-->

1. Assicurati che il foglio sia condiviso con l’utente AEM appropriato (ad esempio `forms@adobe.com`) [in base alle configurazioni specificate per il progetto](https://www.aem.live/docs/setup-customer-sharepoint). Concedi all’utente l’autorizzazione di modifica per il foglio.

1. Apri il foglio di calcolo creato e rinomina il foglio predefinito in “shared-aem”.

   ![rinominare il foglio predefinito in “shared-default”](/help/edge/assets/rename-sheet-to-shared-default.png)

   >[!IMPORTANT]
   >
   >**Il foglio in cui è stato creato il modulo presenta restrizioni relative al nome. Solo `helix-default` e `shared-aem` possono essere utilizzati come nomi per il foglio.**

1. Per aggiungere i campi modulo, inserisci le righe e le intestazioni di colonna nel foglio “shared-aem”. Ogni riga deve rappresentare un [campo modulo](/help/edge/docs/forms/form-components.md#available-components), con intestazioni di colonna che definiscono il campo corrispondente [proprietà](/help/edge/docs/forms/form-components.md#components-properties).


   Per un avvio rapido, considera copiare il contenuto del [Foglio di calcolo interrogazione](/help/edge/assets/enquiry.xlsx) nel proprio foglio di calcolo. Dopo aver copiato il contenuto, salva il foglio di calcolo.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. Utilizza [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare l’anteprima del foglio.

   ![Utilizza AEM Sidekick per visualizzare l’anteprima del foglio](/help/edge/assets/preview-form.png)

   In anteprima, nelle nuove schede del browser il contenuto del foglio viene visualizzato in formato JSON. Assicurati di acquisire l’URL di anteprima, in quanto è necessario per il rendering del modulo nella sezione successiva. Il formato dell’URL è attualmente il seguente:


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form-path>/<form-file-name>.json
   ```

   - `<branch>` fa riferimento al ramo dell’archivio GitHub.
   - `<repository>` denota l’archivio GitHub.
   - `<owner>` fa riferimento al nome utente dell’account GitHub che ospita l’archivio GitHub.

   Ad esempio, se l’archivio del progetto è denominato “wefinance”, si trova sotto l’account “wkndform” e stai utilizzando il ramo “main”, l’URL avrà l’aspetto seguente:

`https://main--wefinance--wkndform.aem.page/enquiry.json`
&lt;!—(https://main--wefinance--wkndform.aem.page/enquiry.json)-->


+++

+++ Passaggio 2: visualizzare l’anteprima del modulo utilizzando la pagina Edge Delivery Services.


Finora è stata preparata la struttura del modulo. Ora, per visualizzare in anteprima il modulo:

1. Apri l’account Microsoft SharePoint o Google Drive e passa alla directory del progetto AEM Edge Delivery.



1. apri un file di documento (ad esempio un file index) per incorporare il modulo. In alternativa, puoi [creare un nuovo documento](/help/edge/assets/enquiry-form.docx).

1. Spostati nella posizione desiderata all’interno del documento in cui desideri aggiungere il modulo.

1. Creare un blocco del modulo per il rendering del modulo. Seleziona Inserisci > Tabella e crea una tabella a una colonna e due righe. Denomina la tabella “Modulo” e incolla l’URL di anteprima nella seconda riga. Accertati che l’URL sia formattato come collegamento ipertestuale, non come testo normale, come illustrato di seguito:

   | Modulo |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |


   ![Aggiungere un blocco di moduli adattivi alla pagina web](/help/edge/assets/enquiry-doc-to-embed-form.png)

   Questo blocco funge da segnaposto in cui è incorporato il modulo. Nella seconda riga del blocco, aggiungi l’URL di anteprima del file `<form>.json` come collegamento ipertestuale.

   >[!IMPORTANT]
   >
   >
   > Verifica che l’URL sia formattato come collegamento ipertestuale anziché essere visualizzato come testo normale.


1. Utilizza [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima il documento. Nella pagina viene ora visualizzato il modulo. Ad esempio, questo è il modulo basato sul [foglio di calcolo di richiesta](/help/edge/assets/enquiry-form.docx):


   [![Esempio di modulo EDS](/help/edge/assets/updated-form.png)](https://main--wefinance--wkndform.aem.page/enquiry-form)

   A questo punto, compila il modulo e fai clic sul pulsante Invia. Riscontrerai un errore simile al seguente, perché il foglio di calcolo non è ancora impostato per accettare i dati.

   ![errore durante l’invio del modulo](/help/edge/assets/form-error.png)

+++


## Passaggio successivo

[Preparare il foglio di calcolo](/help/edge/docs/forms/submit-forms.md) per iniziare ad accettare i dati al momento dell’invio del modulo.


