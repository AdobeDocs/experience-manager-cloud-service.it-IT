---
title: Aggiungere sezioni ripetibili a un modulo
description: Aggiungere sezioni ripetibili a un modulo EDS
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: fd2e5df72e965ea6f9ad09b37983f815954f915c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Aggiungere sezioni ripetibili a un modulo

Il blocco di modulo adattivo consente di aggiungere o rendere ripetibile una sezione o un componente di un modulo.

Una sezione ripetibile è un componente di un modulo che viene duplicato o replicato più volte per raccogliere informazioni per più occorrenze di dati simili.

Si consideri, ad esempio, un modulo utilizzato per raccogliere informazioni sull&#39;esperienza lavorativa di una persona. È possibile che sia disponibile una sezione ripetibile per l&#39;acquisizione dei dettagli di ogni processo precedente. In genere, la sezione ripetibile contiene campi quali il nome dell&#39;azienda, la qualifica, le date di assunzione e le responsabilità lavorative. L’utente può aggiungere più istanze della sezione ripetibile per immettere informazioni su ogni processo che ha mantenuto.



Alla fine di questo articolo imparerai a:

* [Creare una sezione ripetibile in un modulo](#add-repeatable-sections-to-a-form)
* [Impostare il numero minimo o massimo di ripetizioni in un modulo](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## Creare una sezione ripetibile in un modulo

La creazione di una sezione ripetibile in un modulo consente agli utenti di immettere più istanze dello stesso insieme di dati, consentendo una raccolta efficiente di informazioni ripetitive. Per creare una sezione ripetibile in un modulo:

1. Vai alla cartella del progetto Edge Deliver in Microsoft SharePoint o Google Workspace e apri il foglio di calcolo. Ad esempio, apri un foglio di calcolo denominato `job-application.xlsx`.

1. Aggiungere un campo modulo con `type` proprietà impostata su `fieldset` e abilitare la ripetibilità impostando `repeatable` a `true`. Inoltre, specifica un valore `label` per il campo, in quanto funge da intestazione per la sezione ripetibile.

   Fare riferimento all&#39;immagine seguente per un&#39;illustrazione di una sezione della cronologia impiego all&#39;interno di un modulo di candidatura.

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. In `Fieldset` di tutti i campi da includere in una sezione ripetibile, specificare `Name` del set di campi corrispondente.

   Ad esempio, designa `experience` nella proprietà Fieldset di tutti i campi rilevanti da includere nel `employment history` sezione.

   ![](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima e pubblicare il foglio. La sezione ripetibile viene aggiunta al modulo.

   Sotto la sezione ripetibile, gli utenti possono trovare una **Aggiungi** semplificando l&#39;aggiunta di più sezioni.

   ![sezione ripetibile, trovare un **Aggiungi** per aggiungere più sezioni ](/help/edge/assets/repeatable-section-example.png)


## Imposta il numero minimo o massimo di ripetizioni per una sezione ripetibile

Nella progettazione dei moduli è utile impostare ripetizioni minime e massime per le sezioni ripetibili. In questo modo, puoi stabilire controllo e coerenza guidando al contempo gli utenti in modo efficace. Per impostare un numero minimo o massimo di ripetizioni:

1. Vai alla cartella del progetto Edge Deliver in Microsoft SharePoint o Google Workspace e apri il foglio di calcolo.

1. Imposta il `min` per specificare il numero minimo di ripetizioni della sezione.

   ![Impostare le proprietà min e max per specificare il numero di ripetizioni della sezione](/help/edge/assets/repeatable-section-set-min-max.png)

1. Imposta il `max` per specificare il numero massimo di ripetizioni della sezione.

1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima e pubblicare il foglio.

   Ora, quando si aggiungono sezioni ripetibili, gli utenti possono **Elimina** semplificando il processo di rimozione delle sezioni ripetibili. Una volta aggiunte, queste sezioni non possono essere ridotte a un numero di istanze inferiore a quello specificato da `min` proprietà. In questo modo si garantisce il rispetto dei requisiti minimi stabiliti per la compilazione del modulo.

<!--

For example, consider a form used to collect information from users applying for a loan. . You may have a repeatable section for capturing details of each co-applicant. The repeatable section would typically contain fields such as co-co-applicant

The form allows users to provide personal information, including details of the co-applicants. Users can enter details for co-applicants, with this section being repeatable.

![Repeatable sections in forms](/help/forms/assets/eds-repeatable.png)

## Prerequisites

The [Adaptive Form block is enabled](/help/edge/docs/forms/create-forms.md) for your Edge Delivery Service project. 

## Add a repeatable section to a form 

Let's take an example of a loan application form. The form enables users to submit personal information. You can include co-applicant details using repeatable sections, with the option to add a minimum and maximum of three co-applicant sections.

"_You can use a Microsoft Excel file on your SharePoint Site or Google Sheet file on Google Drive to develop a form. Examples in this document are based on a [Microsoft Excel file on your SharePoint Site](https://www.aem.live/docs/setup-customer-sharepoint)._" 


To add repeatable sections in Edge Delivery:

1. [Author a form using Microsoft Excel](#author-form)
2. [Preview and publish the form](#preview-form)

### Author a form using Microsoft Excel {#author-form}

1. Go to your Edge Deliver project folder on Microsoft SharePoint or Google Workspace and open your spreadsheet. For example, open an a spreadsheet named `loan-application.xlsx`.

1. Add a new columns labeled `Repeatable` to the sheet contaning your form fields. By default, the `shared-default` sheet contains the form fields.  

1. Add new columns labeled as `Repeatable`, `Min`, and `Max` in your Microsoft Excel file.
1. Specify the value for the `Repeatable` column as `True` for the fieldset that you want to make repeatable.
1. Specify the values for the `Min` and `Max` columns. The `Min` value represents the minimum number of occurrences for which the panel repeats, while the `Max` value represents the maximum number of occurrences for which the panel repeats.
1. Save your Microsoft Excel file.
     
>[!NOTE]
>
> Here is the [Loan application](/help/forms/assets/loan-application.xlsx) excel sheet for your reference. 

### Preview/Publish the form using your Edge Delivery Service

1. Open or create new document file in a Microsft SharePoint Site to embed the Excel sheet  in it using a `Form Block`. For example, open the `index` file and add a `Form Block`.
2. Open the command prompt, navigate to your AEM Edge Delivery project directory on your local machine, and execute the command as `aem up`.

The form is accessible at `https://localhost:3000`, where clicking the `Add` button adds new repeatable section for entering co-applicant details. You can also delete the the repeatable section by clicking the `Delete` button. 

>[!NOTE]
>
> If you encounter a "Page Not Found" error while accessing your form at localhost, add the directory name of the Microsoft SharePoint Site in front of the URL where your form is located. For example, `http://localhost:3000/<dir-name>/`

-->


## Vedi altro

* [Creare e visualizzare in anteprima un modulo](/help/edge/docs/forms/create-forms.md)
* [Abilita modulo per l’invio di dati](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare un modulo nella pagina Sites](/help/edge/docs/forms/publish-forms.md)
* [Aggiungere convalide ai campi modulo](/help/edge/docs/forms/validate-forms.md)
* [Modificare i temi e lo stile del modulo](/help/edge/docs/forms/style-theme-forms.md)
* [Componenti modulo e relative proprietà](/help/edge/docs/forms/form-components.md)