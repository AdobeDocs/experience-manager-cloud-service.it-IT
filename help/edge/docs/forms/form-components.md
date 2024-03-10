---
title: Componenti e proprietà del modulo
description: Questo documento fornisce una panoramica dei componenti del modulo e delle relative proprietà disponibili in AEM Forms Edge Delivery Service.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 7d087d41-9313-482a-a905-8955b0999781
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# Componenti e proprietà del modulo: servizio di distribuzione Edge di AEM Forms

I servizi di distribuzione Edge di AEM Forms consentono di creare moduli interattivi e di facile utilizzo utilizzando vari componenti. Questi componenti sono adatti a diversi tipi di raccolta dati e possono essere facilmente personalizzati in base a esigenze specifiche.


![Un foglio di calcolo di esempio con alcuni componenti e proprietà](/help/edge/assets/sample-form-in-spreadsheet.png)

Il blocco Forms adattivo genera un [struttura uniforme dei HTML](/help/edge/docs/forms/style-theme-forms.md) per tutti i tipi di campo e i contenitori (pannelli) che ne garantiscono la coerenza. Questa struttura coerente consente di [assegnare uno stile a un modulo](/help/edge/docs/forms/style-theme-forms.md).

## Componenti disponibili

Ecco una panoramica dei componenti disponibili:

### Campi di input

- Tutti i HTML validi5 [tipi di input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) e [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea). Ad esempio, pulsante, casella di controllo, colore, data, datetime-local, e-mail, file, hidden, image, month, number, password, radio, range, reset, submit, tel, text, time, url e week.

### Controlli selezione

- [Gruppi di caselle di controllo](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox): per selezionare più opzioni.
- [Gruppi radio](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio): per selezionare una singola opzione da un gruppo.
- [Menu a discesa](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select): per visualizzare un menu di opzioni. Ad esempio, casella a discesa.

### Contenitori

- Pannelli/contenitori: per raggruppare gli elementi del modulo correlati in modo da migliorarne l’organizzazione. Si tratta di una combinazione di [set di campi](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) e [legenda](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend).






## Proprietà dei componenti

Ogni componente del modulo include varie proprietà che consentono di controllarne il comportamento e l’aspetto. Qui trovi le proprietà supportate dai componenti di blocco Forms adattivo:


| Proprietà | Componenti applicabili | Dettagli |
|--------------|------------------------------|----------------------------------------------------------------------|
| Tipo | Tutti i bundle  | Specifica il tipo di componente. Questa proprietà determina il comportamento e l&#39;aspetto del campo di input. Ad esempio, per gli input di testo, il tipo può essere &quot;text&quot;, &quot;email&quot; per gli input di e-mail, &quot;password&quot; per gli input di password. Blocco Forms adattivo supportato  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">tutti i tipi di input HTML5 validi</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">seleziona</a>, e <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">set di campi</a> come tipo. |
| Tipo | Tutti i bundle  | Specifica il tipo di componente. Questa proprietà determina il comportamento e l&#39;aspetto del campo di input. Ad esempio, per gli input di testo, il tipo può essere &quot;text&quot;, &quot;email&quot; per gli input di e-mail, &quot;password&quot; per gli input di password. Blocco Forms adattivo supportato  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">tutti i tipi di input HTML5 validi</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">seleziona</a>, e <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">set di campi</a> come tipo. |
| Nome | Tutti | Identifica il componente per l’invio del modulo. L&#39;attributo name viene utilizzato quando i dati del modulo vengono inviati al server, associando l&#39;input dell&#39;utente a un campo specifico. |
| Etichetta | Tutti | Fornisce informazioni contestuali agli utenti. L’etichetta è il testo visualizzato accanto al componente, che fornisce agli utenti istruzioni su quali informazioni inserire. |
| Valore | Testo, password, e-mail, numero, intervallo, data e relative varianti (datetime-local, mese, settimana, ora), casella di controllo, radio, nascosto, invia, pulsante | Specifica il valore iniziale del componente. Per gli input di testo, l&#39;area di testo e gli elementi di selezione, questo è il testo o l&#39;opzione di default visualizzata. Per i componenti radio e casella di controllo, si tratta del valore/dati inviati quando vengono selezionati. L’attributo value è facoltativo ma deve essere considerato obbligatorio per gli input di caselle di controllo e radio. |
| Segnaposto | Testo, telefono, e-mail, password, data (e relative varianti come mese, settimana, ora, datetime-locale), numero, intervallo | Offre suggerimenti per l’input previsto. L&#39;attributo segnaposto fornisce un breve suggerimento che descrive il valore previsto del campo di input. Scompare quando l’utente inizia a digitare. |
| Descrizione | Tutti | Fornisce informazioni aggiuntive sul componente e funge da testo della guida. Il campo di descrizione consente di spiegare ulteriormente lo scopo o le istruzioni per la compilazione del componente. Aiuta gli utenti a comprendere il contesto del campo di input. |
| Visibile | Tutti | Controlla la visibilità iniziale. L’attributo visible è una proprietà booleana che determina se il componente è inizialmente visibile o nascosto al caricamento del modulo. Se impostato su true, il campo viene visualizzato; in caso contrario, viene nascosto. |
| Obbligatorio | Testo, telefono, e-mail, password, data e relative varianti (datetime-local, mese, settimana, ora), numero, casella di controllo, radio, file, seleziona (a discesa), area di testo | Indica se il campo deve essere compilato prima dell’invio. L’attributo obbligatorio è una proprietà booleana utilizzata per specificare se l’utente deve fornire un input per il campo prima di inviare il modulo. |
| Min | Data (e relative varianti come mese, settimana, ora, datetime-locale), numero, intervallo | Specifica il valore minimo consentito. L&#39;attributo min imposta il valore minimo che l&#39;utente può immettere nel campo. Ad esempio, per gli input di numeri, definisce il numero più basso accettabile. |
| Max | Data (e relative varianti come mese, settimana, ora, datetime-locale), numero, intervallo | Specifica il valore massimo consentito. L’attributo max imposta il valore massimo che l’utente può immettere nel campo. Ad esempio, per gli input di date, definisce la data più alta accettabile. |
| Accetta | File | Definisce i tipi di file consentiti. L&#39;attributo accept è un elenco separato da virgole di identificatori di tipi di file univoci che limita i tipi di file che gli utenti possono selezionare in un campo di input di file. |
| Varie | File | Consente selezioni multiple. L’attributo multiple è una proprietà booleana utilizzata con i campi di input dei file. Se impostata su true, consente agli utenti di selezionare più file. |
| Opzioni | A discesa | Specifica le scelte per i menu a discesa. La proprietà options è un elenco di scelte per i menu a discesa separato da virgole che definisce le opzioni selezionabili visualizzate dall&#39;utente. |
| Selezionato | Casella di selezione, Radio | Determina se il campo è selezionato per impostazione predefinita. L’attributo selected è una proprietà booleana utilizzata con gli input di caselle di controllo e radio. Se impostato su true, indica che il campo è selezionato per impostazione predefinita al caricamento del modulo. |
| Set di campi | Tutti | Raggruppa i campi per creare sezioni visivamente distinte all’interno di un modulo. L’elemento set di campi raggruppa i campi correlati all’interno di un modulo, separandoli visivamente per migliorare l’organizzazione e l’esperienza utente. </br> Per organizzare un set di campi all’interno di un set di campi, utilizza semplicemente `fieldset` e specificarne l’attributo name. Nell’esempio seguente viene illustrato come i pulsanti di scelta sono racchiusi in un singolo set di campi per una migliore organizzazione. ![Esempio di set di campi](/help/edge/assets/fieldset-example.png) |



<!--

## Supported HTML 5 input types in Adaptive Forms Block

The Adaptive Forms Block supports a range of HTML 5 input types, and it also seamlessly renders forms created with AEM core components.
Here is the table which outlines how core components correspond to their HTML-5 input types in Edge Delivery:
<table>
 <tbody>
  <tr>
   <td><b>Core Components</b> </td>
   <td><b>HTML 5 input type</b> </td>
   <td><b>Details</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Form Container</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">form </td>
   <td> Create a form to capture user inputs.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Text Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Defines a single-line text input field. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Number Input</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">number</a></td>
   <td>Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Initially, the input field is displayed as a number input. If a user applies a display pattern, it changes to text to allow the author to apply number formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing numbers.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Date Picker</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">date </a></td>
   <td> Create an input field for entering a date. You have the option to input the date either through a text box, which validates the entry, or through a dedicated date picker interface. Initially, the native date input field is displayed. If a user applies a display pattern, it changes to text to allow the user to apply formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing a date.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">File Attachment</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">file</a></td>
   <td> Allows user to choose one or more files from the device storage. It supports enhanced file input validations, such as accepted file types, file size restrictions, and minimum/maximum file selection limits. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Dropdown List</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a></td>
   <td> Allows users to select one or more options from a list of predefined options. The options can be of type String, Number, or Boolean.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Checkbox Group</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">multiple checkbox</a></td>
   <td> Allow users to select one or more options from a list. Multiple checkboxes are generated with identical names, each corresponding to an item in the enum. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Radio Button Group</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">multiple radio</a></td>
   <td> Allows a user to select one option from a group of related options. Multiple radio buttons are generated with identical names, each corresponding to an item in the enum.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">button</a></td>
   <td>A UI element that allows users to trigger an action when clicked. </td>
  </tr>
  <tr>
   <td><a href =""https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Panel</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset with legend</a></td>
   <td> Group sections within a form, where a nested *legend* element adds a caption for the form.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html">Wizard</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>Groups related sections within a form. It also controls the arrangement, supporting display options for positioning them at the top or at the left side. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Text</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>A p tag marks a paragraph. In visual content, paragraphs are chunks of text separated by blank lines or an indented first line</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Submit button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">submit</a></td>
   <td> A UI element that enables users to submit a form to the server upon clicking. If a user adds a submit rule to a button, it functions as the submit button. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Reset button</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">reset</a></td>
   <td>A UI element that resets a form upon clicking. If a user adds a reset rule to a button, it functions as the reset button. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">Email Input</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">email</a></td>
   <td> Allows the user to enter and edit an email address. If the user adds the multiple attributes, a list of email addresses can be added or edited.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Telephone Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Allows user to enter and edit a telephone number.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Header</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> header</a></td>
   <td>It includes introductory content, typically a group of introductory or navigational aids. It is supported outside Form container. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Footer</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">footer</a></td>
   <td> Contains information such as copyright data or links to related documents. It is supported outside Form container.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html">Accordion<a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Allows user to create expandable and collapsible sections in a form. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html">Horizontal tabs</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td>Organizes multiple sections of a form into separate tabs which are displayed horizontally.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Image</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Allows user to include images in a form.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Title</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Refers to the text that appears at the top of the form. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Switch</td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> A two-state toggle that allows user to select between two states such as enabling or disabling a feature, setting, or functionality.</td>
  </tr>
 </tbody>
</table> -->

## Vedi altro

- [Creare e visualizzare in anteprima un modulo](/help/edge/docs/forms/create-forms.md)
- [Abilita modulo per l’invio di dati](/help/edge/docs/forms/submit-forms.md)
- [Pubblicare un modulo nella pagina Sites](/help/edge/docs/forms/publish-forms.md)
- [Aggiungere convalide ai campi modulo](/help/edge/docs/forms/validate-forms.md)
- [Modificare i temi e lo stile del modulo](/help/edge/docs/forms/style-theme-forms.md)
