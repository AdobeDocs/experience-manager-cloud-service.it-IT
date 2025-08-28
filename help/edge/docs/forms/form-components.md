---
title: Componenti del blocco modulo adattivo e relative proprietà
description: Questo documento fornisce una panoramica dei componenti del modulo e delle relative proprietà disponibili in Edge Delivery Service per AEM Forms.
feature: Edge Delivery Services
exl-id: 7d087d41-9313-482a-a905-8955b0999781
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '1007'
ht-degree: 100%

---

# Componenti del blocco modulo adattivo e relative proprietà

Edge Delivery Services per AEM Forms consente di creare moduli interattivi e di facile utilizzo utilizzando vari componenti. Questi componenti sono adatti a diversi tipi di raccolta dati e possono essere facilmente personalizzati in base a esigenze specifiche.


![Un foglio di calcolo di esempio con alcuni componenti e proprietà](/help/edge/assets/sample-form-in-spreadsheet.png)

Il blocco Forms adattivo genera per tutti i tipi di campo e i contenitori (pannelli) una [struttura HTML uniforme](/help/edge/docs/forms/style-theme-forms.md) che ne garantisce la coerenza. Questa struttura coerente facilita la personalizzazione dello [stile di un modulo](/help/edge/docs/forms/style-theme-forms.md).

## Componenti disponibili

Ecco una panoramica dei componenti disponibili:

### Campi di input

- Tutti i [tipi di input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) HTML5 validi e [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea). Ad esempio, pulsante, casella di controllo, colore, data, datetime-local, e-mail, file, nascosto, immagine, mese, numero, password, radio, intervallo, reimposta, invia, tel, testo, orario, url e settimana.

### Controlli selezione

- [Gruppi di caselle di controllo](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox): per selezionare più opzioni.
- [Gruppi di scelta](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio): per selezionare una singola opzione da un gruppo.
- [Menu a discesa](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select): per visualizzare un menu di opzioni. Ad esempio, casella a discesa.

### Contenitori

- Pannelli/contenitori: per raggruppare gli elementi del modulo correlati in modo da migliorarne l’organizzazione. Si tratta di una combinazione di [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) e [legend](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend).


## Proprietà dei componenti

Ogni componente del modulo include varie proprietà che consentono di controllarne il comportamento e l’aspetto. Qui trovi le proprietà supportate dai componenti di blocco Forms adattivo:


| Proprietà | Componenti applicabili | Dettagli |
|--------------|------------------------------|----------------------------------------------------------------------|
| Tipo | Tutti | Specifica il tipo di componente. Questa proprietà determina il comportamento e l’aspetto del campo di input. Ad esempio, per gli input di testo, il tipo può essere “testo”, “e-mail” per gli input di e-mail, “password” per gli input di password. Blocco Forms adattivo supporta come tipo <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">tutti i tipi di input HTML5 validi</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, e <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>. |
| Nome | Tutti | Identifica il componente per l’invio del modulo. L’attributo name viene utilizzato quando i dati del modulo vengono inviati al server, associando l’input dell’utente a un campo specifico. |
| Etichetta | Tutti | Fornisce informazioni contestuali agli utenti. L’etichetta è il testo visualizzato accanto al componente, che fornisce agli utenti istruzioni su quali informazioni inserire. |
| Valore | Testo, password, e-mail, numero, intervallo, data e relative varianti (datetime-local, mese, settimana, ora), casella di controllo, scelta, nascosto, invia, pulsante | Specifica il valore iniziale del componente. Per gli input di testo e gli elementi textarea e select questo è il testo o l’opzione predefinita visualizzata. Per i componenti scelta e casella di controllo, si tratta del valore/dati inviati quando vengono selezionati. L’attributo value è facoltativo ma deve essere considerato obbligatorio per gli input casella di controllo e scelta. |
| Segnaposto | Testo, telefono, e-mail, password, data (e relative varianti come mese, settimana, ora, datetime-locale), numero, intervallo | Offre suggerimenti per l’input previsto. L’attributo segnaposto fornisce un breve suggerimento che descrive il valore previsto del campo di input. Scompare quando l’utente inizia a digitare. |
| Descrizione | Tutti | Fornisce informazioni aggiuntive sul componente e funge da testo di aiuto. Il campo di descrizione consente di spiegare ulteriormente lo scopo o le istruzioni per la compilazione del componente. Aiuta gli utenti a comprendere il contesto del campo di input. |
| Visibile | Tutti | Controlla la visibilità iniziale. L’attributo visible è una proprietà booleana che determina se il componente è inizialmente visibile o nascosto al caricamento del modulo. Se impostato su true, il campo viene visualizzato; in caso contrario, viene nascosto. |
| Obbligatorio | Testo, telefono, e-mail, password, data e relative varianti (datetime-local, mese, settimana, ora), numero, casella di controllo, scelta, file, select (a discesa), area di testo | Indica se il campo deve essere compilato prima dell’invio. L’attributo obbligatorio è una proprietà booleana utilizzata per specificare se l’utente deve fornire un input per il campo prima di inviare il modulo. |
| Min | Data (e relative varianti come mese, settimana, ora, datetime-locale), numero, intervallo | Specifica il valore minimo consentito. L’attributo min definisce il valore minimo che l’utente può immettere nel campo. Ad esempio, per gli input di numeri, definisce il numero più basso accettabile. |
| Max | Data (e relative varianti come mese, settimana, ora, datetime-locale), numero, intervallo | Specifica il valore massimo consentito. L’attributo max definisce il valore massimo che l’utente può immettere nel campo. Ad esempio, per gli input di date, definisce la data più alta accettabile. |
| Accetta | File | Definisce i tipi di file consentiti. L’attributo accept è un elenco separato da virgole di identificatori di tipi di file univoci che limita i tipi di file che gli utenti possono selezionare in un campo di input di file. |
| Varie | File | Consente selezioni multiple. L’attributo multiple è una proprietà booleana utilizzata con i campi di input dei file. Se impostata su true, consente agli utenti di selezionare più file. |
| Opzioni | A discesa | Specifica le scelte per i menu a discesa. La proprietà options è un elenco separato da virgole di scelte per i menu a discesa e definisce le opzioni selezionabili visualizzate dall’utente. |
| Selezionato | Casella di controllo, pulsante di scelta | Determina se il campo è selezionato per impostazione predefinita. L’attributo checked è una proprietà booleana utilizzata con gli input di caselle di controllo e pulsanti di scelta. Se impostato su true, indica che il campo è selezionato per impostazione predefinita al caricamento del modulo. |
| Fieldset | Tutti | Raggruppa i campi per creare sezioni visivamente distinte all’interno di un modulo. L’elemento fieldset raggruppa i campi correlati all’interno di un modulo, separandoli visivamente per migliorare l’organizzazione e l’esperienza utente. </br>Per organizzare un set di campi all’interno di un fieldset, utilizza semplicemente la proprietà `fieldset` specificandone l’attributo name. Nell’esempio seguente viene illustrato come i pulsanti di scelta sono racchiusi in un singolo fieldset per una migliore organizzazione. ![Esempio di fieldset](/help/edge/assets/fieldset-example.png) |
| Ripetibile | Tutti | Una proprietà booleana per `fieldset` che indica che un particolare fieldset può essere ripetuto per uno specifico numero `Min` e `Max` di volte. La proprietà `Min` deve essere impostata su 1 o maggiore, non impostare la proprietà `Min` su 0. |
| Espressione visible | Tutti | Un’espressione visible si riferisce a una formula del foglio di calcolo, identificata dal tag &#39;=&#39; e utilizzata per controllare la visibilità di un campo. In questa formula, è possibile utilizzare solo la proprietà value di altri campi, per una gestione semplice della visibilità dei campi all’interno del sistema. |
| Espressione value | Tutti | Un’espressione value si riferisce a una formula del foglio di calcolo, identificata dal tag &#39;=&#39;, utilizzata per controllare il valore di un campo. In questa formula, è possibile utilizzare solo la proprietà value di altri campi, per una gestione semplice del valore del campo all’interno del sistema. |
