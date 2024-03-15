---
title: Componenti del blocco di modulo adattivo e relative proprietà
description: Questo documento fornisce una panoramica dei componenti del modulo e delle relative proprietà disponibili in AEM Forms Edge Delivery Service.
feature: Edge Delivery Services
exl-id: 7d087d41-9313-482a-a905-8955b0999781
source-git-commit: 703a48903c44678f6fe311de740b7c767c886ba5
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 3%

---

# Componenti del blocco di modulo adattivo e relative proprietà

I servizi di distribuzione Edge di AEM Forms consentono di creare moduli interattivi e di facile utilizzo utilizzando vari componenti. Questi componenti sono adatti a diversi tipi di raccolta dati e possono essere facilmente personalizzati in base a esigenze specifiche.


![Un foglio di calcolo di esempio con alcuni componenti e proprietà](/help/edge/assets/sample-form-in-spreadsheet.png)

Il blocco Forms adattivo genera un [struttura uniforme dei HTML](/help/edge/docs/forms/style-theme-forms.md) per tutti i tipi di campo e i contenitori (pannelli) che ne garantiscono la coerenza. Questa struttura coerente consente di [assegnare uno stile a un modulo](/help/edge/docs/forms/style-theme-forms.md).

## Componenti disponibili

Ecco una panoramica dei componenti disponibili:

### Campi di input

* Tutti i HTML validi5 [tipi di input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) e [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea). Ad esempio, pulsante, casella di controllo, colore, data, datetime-local, e-mail, file, hidden, image, month, number, password, radio, range, reset, submit, tel, text, time, url e week.

### Controlli selezione

* [Gruppi di caselle di controllo](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox): per selezionare più opzioni.
* [Gruppi radio](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio): per selezionare una singola opzione da un gruppo.
* [Menu a discesa](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select): per visualizzare un menu di opzioni. Ad esempio, casella a discesa.

### Contenitori

* Pannelli/contenitori: per raggruppare gli elementi del modulo correlati in modo da migliorarne l’organizzazione. Si tratta di una combinazione di [set di campi](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) e [legenda](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend).


## Proprietà dei componenti

Ogni componente del modulo include varie proprietà che consentono di controllarne il comportamento e l’aspetto. Qui trovi le proprietà supportate dai componenti di blocco Forms adattivo:


| Proprietà | Componenti applicabili | Dettagli |
|--------------|------------------------------|----------------------------------------------------------------------|
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
| Ripetibile | Tutti | Una proprietà booleana per `fieldset` che indica che un particolare set di campi può essere ripetuto per `Min` e `Max` numero di volte. Il `Min` deve essere impostato su 1 o maggiore, non impostare il valore `Min` proprietà su 0. |
| Espressione visibile | Tutti | Un&#39;espressione visibile si riferisce a una formula del foglio di calcolo, identificata dal tag &#39;=&#39;, utilizzata per controllare la visibilità di un campo. In questa formula, è possibile utilizzare solo la proprietà value di altri campi, consentendo una gestione semplice della visibilità dei campi all’interno del sistema. |
| Espressione valore | Tutti | Un&#39;espressione di valore si riferisce a una formula del foglio di calcolo, identificata dal tag &#39;=&#39;, utilizzata per controllare il valore di un campo. In questa formula, è possibile utilizzare solo la proprietà value di altri campi, consentendo una gestione semplice del valore del campo all’interno del sistema. |


## Consulta anche

{{see-more-forms-eds}}
