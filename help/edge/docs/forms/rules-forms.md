---
title: Utilizzare le regole per aggiungere un comportamento dinamico a un modulo
description: I Edge Delivery Services AEM Forms sono stati progettati per offrire prestazioni di picco, consentendoti di immaginare il futuro della raccolta dati semplificata e del coinvolgimento degli utenti. Utilizzare le regole per aggiungere un comportamento dinamico ai moduli.
feature: Edge Delivery Services
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '2216'
ht-degree: 0%

---

# Utilizzare le regole per aggiungere un comportamento dinamico ai moduli

Una delle potenti funzionalità della creazione di moduli utilizzando un foglio di calcolo è la possibilità di utilizzare funzioni incorporate per creare regole, che consentono di visualizzare o nascondere in modo condizionale i campi modulo, automatizzare i calcoli in base agli input dell&#39;utente e creare un&#39;esperienza utente più dinamica.

Questo articolo illustra come utilizzare principalmente varie proprietà del blocco di modulo adattivo [`Visible`](#visible-property), [`Visibility Expression`](#visible-expression-property) e [`Value Expression`](#value-expression-property) proprietà insieme a [funzioni del foglio di calcolo](#spreadsheet-functions-for-rules) per creare regole efficaci per i moduli. Esamineremo anche alcuni esempi per illustrare come queste regole possono essere implementate nella pratica.

## Informazioni sui costrutti di una regola

Le regole sono come istruzioni che ci dicono cosa fare in situazioni diverse. Una regola ha in genere i seguenti costrutti:

* Condizioni : specificano le circostanze in cui si applica la regola. Considerale come una domanda a cui bisogna rispondere (sì o no).

* Azioni: definiscono cosa accade quando la condizione viene soddisfatta (true) o non viene soddisfatta (false).


Ad esempio, per visualizzare una casella e-mail, quando è selezionata una casella di controllo:

* Condizione: &quot;Ti piace abbonarti a riviste e attività?&quot; è selezionata. (Sì o no?). Questa condizione è impostata in `Visible` proprietà del modulo.
* Azione (True): viene visualizzata la casella e-mail. (Cosa succede se sì). Il `Visibility Expression`  utilizza la condizione definita per `visible` per visualizzare dinamicamente i campi.
* Azione (False): la casella e-mail è nascosta. (Cosa succede se non lo è). Il `Visibility Expression`  utilizza la condizione definita per `Value` per nascondere dinamicamente i campi.

Per istruzioni dettagliate, vedere [mostra/nascondi campo e-mail in base a una condizione](#example-1-conditional-email-field)


## Informazioni sulle proprietà Espressione di valore, Visibile, Visibilità e Valore

### Visible, proprietà

Immagina un interruttore di luce per il campo modulo. Il `Visible` La proprietà è simile a tale opzione, che controlla se il campo è inizialmente visibile nella maschera al primo caricamento.

* True (come se l&#39;interruttore della luce fosse &quot;on&quot;): il campo viene visualizzato nel modulo.
* False (come se l&#39;interruttore della luce fosse &quot;off&quot;): il campo è nascosto nel modulo.

È possibile utilizzare la formula del foglio di calcolo (incluso il tag = ) per scrivere una formula utilizzando una logica simile a quella del foglio di calcolo per determinare la visibilità del campo. In questa formula è possibile utilizzare i valori di altri campi del modulo. Ad esempio, se un utente seleziona &quot;Individuale&quot; in un campo di tipo registrazione, puoi nascondere il campo e-mail utilizzando una formula che controlla tale valore.

### Proprietà espressione visibile (mostrare/nascondere un campo)

Il `Visible Expression` consente di utilizzare la regola aggiunta a `Visible` per decidere se mostrare o nascondere il campo in base alle interazioni dell&#39;utente.

Utilizza il `=FORMULATEXT("Address of the corresponding Visible property)` per portare la formula indicata nella `Visible` Proprietà come stringa per `Visible Expression` campo proprietà. Questa opzione è necessaria per mostrare/nascondere dinamicamente i campi in un modulo pubblicato.

![Testo Forumaltext](/help/edge/assets/aem-forms-formulatext.png)

### Proprietà Value (imposta i dati iniziali)

Immaginate un valore preimpostato su un interruttore dimmer per la luce di una stanza. Il `Value` è simile, determinando lo stato iniziale dei dati visualizzati nel campo.  Imposta o recupera i dati correnti visualizzati nel campo modulo.

Al primo caricamento del modulo, il `Value` determina ciò che l’utente vede nel campo prima di apportare qualsiasi modifica. A differenza di `Visible` e `Visible Expression` proprietà che controllano la visibilità, la proprietà Value influisce direttamente sui dati stessi. Gli utenti possono modificare questo valore digitando, selezionando le opzioni (menu a discesa) o interagendo con il campo.

È possibile utilizzare la formula di Excel (incluso il tag = ) per scrivere una formula utilizzando una logica simile a quella del foglio di calcolo per determinare il valore visualizzato nel campo. In questa formula è possibile utilizzare i valori di altri campi del modulo. Ad esempio, è possibile calcolare automaticamente uno sconto in base all&#39;importo dell&#39;ordine inserito in un altro campo.


### Proprietà espressione valore (calcolare i valori da visualizzare in un campo)

Questa proprietà consente di controllare il valore visualizzato all&#39;interno di un campo basato su una formula, simile all&#39;espressione visibile. Immagina una calcolatrice incorporata nel campo.

Utilizza il `=FORMULATEXT("Address of the corresponding Value property)` per portare la formula indicata nella `Value` Proprietà come stringa per `Value Expression` campo proprietà. Questa opzione è necessaria per calcolare e visualizzare in modo dinamico i valori calcolati in un modulo pubblicato.

![Testo Forumaltext](/help/edge/assets/aem-forms-formulatext-value.png)

Di seguito è riportata un&#39;analogia per consolidare questi concetti:

* Visibile: immagina una forma come una casa. La proprietà &quot;Visible&quot; è simile all&#39;interruttore della luce per ogni stanza (campo). Decidi se la stanza è inizialmente illuminata (visibile) o scura (nascosta) quando qualcuno entra in casa (apre il modulo).
* Espressione visibile: simile a un interruttore della luce del sensore di movimento. La stanza (campo) potrebbe essere inizialmente scura (nascosta), ma una formula (sensore di movimento) può attivarla (mostrare il campo) se qualcuno passa accanto (modifica il valore in un altro campo).
* Valore: è come un interruttore dimmer preimpostato per la luce (dati iniziali nel campo). Gli utenti possono quindi regolare la luminosità (modificare il valore).
* Espressione di valore: simile a una calcolatrice sofisticata incorporata nel tag prezzo di un prodotto della casa (modulo). Il tag prezzo (campo) mostra il prezzo finale basato su una formula (ad esempio, l&#39;aggiunta di imposte al prezzo base) che utilizza altre informazioni come il prezzo base (valore di un altro campo).

Combinando queste proprietà con [funzioni del foglio di calcolo](#spreadsheet-functions-for-rules), è possibile ottenere un&#39;ampia gamma di comportamenti dinamici all&#39;interno dei moduli.

## Funzioni del foglio di calcolo per le regole

Blocco Forms adattivo supporta diverse funzioni dei fogli di calcolo che possono essere utilizzate per creare regole. Di seguito sono riportate le funzioni disponibili come predefinite:

### Funzioni logiche

* [NOT()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110): inverte lo stato logico (TRUE diventa FALSE e viceversa).
* [AND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND): restituisce TRUE solo se tutte le condizioni specificate sono TRUE.
* [OR()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR): restituisce TRUE se almeno una delle condizioni specificate è TRUE.

### Funzioni condizionali

* [IF()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110): valuta una condizione e restituisce un valore specifico se TRUE e un altro valore se FALSE.

### Funzioni matematiche

* [SUM()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM): aggiunge valori da un intervallo di celle specificato.
* [ROUND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND): arrotonda un numero a un numero specificato di cifre decimali.
* [MIN()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN): restituisce il valore più piccolo da un intervallo di celle specificato.

## Creazione di una regola

Approfondiamo alcuni esempi pratici per illustrare come le regole possono essere utilizzate per migliorare i moduli:

## Esempio 1: campo e-mail condizionale

Questo esempio mostra come la casella di controllo funge da condizione. Quando è selezionata (la condizione è vera), viene visualizzata la casella e-mail (azione true). Se non è selezionata (la condizione è false), la casella e-mail rimane nascosta (azione per false).

Crea un modulo con una casella di controllo e una casella e-mail, come illustrato nell’immagine seguente:

![Modulo e-mail condizionale](/help/edge/assets/aem-forms-conditional-email-form.png)


Di seguito viene illustrato come utilizzare una regola per visualizzare il campo e-mail sulla selezione di una casella di controllo:

1. Imposta il `Value` proprietà del campo casella di controllo a `TRUE`.
1. Imposta il `Checked` proprietà del campo casella di controllo a `FALSE`. In questo modo, per impostazione predefinita, la casella di controllo non è selezionata.
1. Imposta il `Visible` proprietà del campo e-mail a `=[address of Checked property of the checkbox field] = true()`. Ad esempio `=Q11=TRUE()`. La formula valuta se la casella di controllo è selezionata o meno. Se la casella di controllo è selezionata, la formula restituisce TRUE. Se la casella di controllo non è selezionata, la formula restituisce FALSE.



   Il `TRUE()` , restituisce il valore logico quando lo si imposta su `Checked` proprietà, se `checked = false` restituisce false. Se `checked=true`, restituisce `true`. In questo modo, per impostazione predefinita, il campo e-mail è nascosto.


1. Imposta il `Visible Expression` proprietà del campo casella di controllo a `=FORMULATEXT ((address of Visible property of the checkbox field))`. Ad esempio: `=FORMULATEXT((G12))`. La funzione FORMULATEXT() accetta una formula come input e restituisce la formula stessa come stringa di testo. È utile utilizzare la formula nel modulo.

   ![Campo e-mail condizionale](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. Visualizzare in anteprima e pubblicare il modulo. Ora, quando si seleziona la casella di controllo, viene visualizzato il campo e-mail e, deselezionato, il campo viene nascosto, offrendo un’esperienza utente dinamica.

   ![E-mail condizionale](/help/edge/assets/aem-forms-coditional-email.gif)


## Esempio 2: calcolo automatico

In questo esempio viene illustrato il modo in cui una maschera calcola automaticamente il Costo viaggio stimato quando si selezionano le date del viaggio in una maschera.

Creare un modulo con un campo data, il budget della stanza, i campi Costo viaggio stimato come mostrato di seguito e una casella e-mail come illustrato nell&#39;immagine seguente:

![Modulo e-mail condizionale](/help/edge/assets/aem-forms-automatic-calculations-form.png)

Di seguito viene descritto come utilizzare un calcolo automatico per visualizzare il costo del viaggio stimato:

1. Imposta il `Value` proprietà del `amount` campo a `=F6*DAYS(F3,F2)`. Questa formula calcola il numero di giorni da `Start Date`  e `End Date`, numero multiplo di giorni con budget della stanza e visualizza il risultato in `Estimated Trip Cost` campo.

1. Imposta il `Value Expression` proprietà del `Estimated Trip Cost` campo a `=FORMULATEXT ((address of value property of the amount field))`. Ad esempio: `=FORMULATEXT(F7)`. La funzione FORMULATEXT() accetta una formula come input e restituisce la formula stessa come stringa di testo. È utile utilizzare la formula nel modulo.

1. Visualizzare in anteprima e pubblicare il modulo. Ora, quando si specifica una `Start Date`, `End Date`e il budget della camera. Il `Estimated Trip Cost` viene calcolato automaticamente.

## Esempi di funzioni del foglio di calcolo


Di seguito sono riportati alcuni esempi per le funzioni di foglio di calcolo comunemente utilizzate:

**Funzioni logiche:**

* **NOT():** Inverte lo stato logico (TRUE diventa FALSE e viceversa).

  Esempio: se il campo e-mail viene lasciato vuoto, viene nascosto il campo &quot;Conferma e-mail&quot;.

   1. Imposta il `Visible` del campo &quot;Conferma e-mail&quot; a `=NOT(if('address of email field'=""))`.

      ![Nascondi campo e-mail di conferma AEM Forms](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. Imposta l’espressione visibile del campo &quot;Conferma e-mail&quot; su `=FORMULATEXT ((address of visible property of the Confirm Email field))`

      ![Formula espressione visibile AEM Forms](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


* AND(): restituisce TRUE solo se tutte le condizioni specificate sono TRUE.

   * Esempio: abilitare un pulsante &quot;invia&quot; solo se tutti i campi obbligatori sono compilati.

   1. Imposta il `Visible` proprietà del pulsante &quot;invia&quot; a:



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      Ad esempio:

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. Imposta l’espressione visibile del campo &quot;Conferma e-mail&quot; su

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      Ad esempio:

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      Questa formula mostra il pulsante &quot;invia&quot; (VERO) solo se tutti i campi (nome, e-mail, telefono) sono compilati (NOT() restituisce VERO per ciascuno), altrimenti nasconde il pulsante (AND(multiple FALSES) = FALSO).

* OR(): restituisce TRUE se almeno una delle condizioni specificate è TRUE.

   * Esempio: applicazione di uno sconto se un utente inserisce uno qualsiasi dei codici coupon di sconto applicabili.

   1. Imposta il `Visible` proprietà del campo &quot;importo finale&quot; in:


  ```JavaScript
     =IF(OR(F14="BlackFridaySale", F14="NewYearDiscount"), (F6*DAYS(F3,F2)* 0.7) , (F6*DAYS(F3,F2)))
  ```

   1. Imposta l’espressione del valore del campo &quot;Confirm Email&quot; su

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      Ad esempio:

      ```JavaScript
      =FORMULATEXT(F7)
      ```

      Questa formula calcola uno sconto del 30%, se l&#39;utente immette un codice coupon (couponCode = &quot;NewYearDiscount&quot;) OPPURE (couponCode = &quot;BlackFridaySale&quot;), altrimenti imposta lo sconto su 0.

**Funzioni testo:**

* IF(): valuta una condizione e restituisce un valore specifico se TRUE e un altro valore se FALSE.

   * Esempio: visualizzazione di un messaggio personalizzato in base a una categoria di prodotto selezionata.

   1. Imposta il `Value` proprietà del `message` campo a `Only upto 7 kg check-in lagguage is allowed!`:

   1. Imposta il `Visible` proprietà del `message` campo a:


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      Ad esempio:

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. Imposta l’espressione del valore del `message` campo a

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      Ad esempio:

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      Questa formula visualizza il messaggio &quot;È consentito il check-in di un massimo di 7 kg di bagaglio!&quot; se la classe scelta è &quot;Economy&quot;, altrimenti lascia vuoto il campo del messaggio.

**Funzioni matematiche**

* SUM(): aggiunge valori da un intervallo di celle specificato.

  Esempio: calcolo del costo totale degli articoli in un carrello.

  Nell&#39;espressione valore del campo &quot;costo totale&quot;: SOMMA(prezzo * quantità)

  Questa formula presuppone che siano presenti campi separati per &quot;prezzo&quot; e &quot;quantità&quot; di ciascun articolo. Le moltiplica e utilizza SUM() per sommare il costo totale di tutti gli articoli nel carrello.

* ROUND(): arrotonda un numero a un numero specificato di cifre decimali.

  Esempio: arrotondamento di un importo di sconto calcolato a due posizioni decimali.

  Nell&#39;espressione di valore del campo &quot;importo sconto&quot; (supponendo che uno sconto venga calcolato altrove): ROUND(sconto, 2)

  Questa formula arrotonda il valore dello sconto a due posizioni decimali.

* MIN(): restituisce il valore più piccolo da un intervallo di celle specificato.

  Esempio: ricerca dell&#39;età minima richiesta per un modulo di abbonamento basato su un paese selezionato.

  Nell’espressione di valore di un campo &quot;età minima&quot;: MIN(ageLimits[&quot;US&quot;], ageLimits[&quot;UK&quot;], ageLimits[&quot;France&quot;])

  Questa formula presuppone che sia disponibile una tabella denominata &quot;ageLimits&quot; in cui sono memorizzati i requisiti di età minima per i diversi paesi. Utilizza MIN() per trovare il valore più piccolo tra questi.


Inoltre, Adaptive Forms Block consente di prendere tutte le redazioni dei moduli creando [funzioni personalizzate](#creating-custom-functions). Le funzioni personalizzate consentono di definire regole e logiche personalizzate, offrendo un controllo completo sul funzionamento dei moduli.


## Creazione e distribuzione di funzioni personalizzate

Il blocco Forms adattivo pronto all’uso (OOTB) fornisce implementazioni per molti [funzioni comuni dei fogli di calcolo](#spreadsheet-functions-for-rules). Tuttavia, per un controllo più granulare sui moduli, puoi utilizzare una qualsiasi delle funzioni OOTB disponibili in Microsoft® Excel o Google Sheets all’interno dei blocchi Forms adattivi. Il blocco Forms adattivo non contiene l’implementazione per tutte le funzioni OOTB disponibili in Microsoft® Excel o Google Sheets. Se hai bisogno di una di queste funzioni, puoi sviluppare una funzione personalizzata con una sintassi simile per ottenere la funzionalità fornita da Microsoft® Excel o Google Sheets. Ad esempio, puoi implementare [Funzione Year() di Microsoft® Excel](https://support.microsoft.com/en-us/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#) per calcolare l’età dalla data di nascita.


### Creare una funzione personalizzata

Le funzioni personalizzate risiedono nel `[Adaptive form block]/functions.js` file. Il processo di creazione prevede in genere i seguenti passaggi:

* Dichiarazione di funzione: consente di definire il nome della funzione e i relativi parametri, ovvero gli input accettati.
* Implementazione logica: scrivi il codice che illustra i calcoli o le manipolazioni specifici eseguiti dalla funzione.
* Esportazione funzione: rendi la funzione accessibile all’interno delle tue regole esportandola dal file pertinente.

### Esempio: funzione Year

In questo esempio vengono illustrate due funzioni personalizzate che imitano la funzione YEAR() di Microsoft® Excel per calcolare l&#39;età:


```JavaScript
/**
 * Get the current date and time
 * @name now
 * @returns {Date} The current date and time as a Date object
 */
function now() {
  const today = new Date();
  return today;
}

/**
 * Get the year from a Date object
 * @name year
 * @param {Date} date The date object
 * @throws {TypeError} If the input is not a Date object
 * @returns {number} The year as a number
 */
function year(date) {
  let inputDate = new Date(date)

  if (!(inputDate instanceof Date)) {
    throw new TypeError("Input must be a Date object");
  }

  const year = inputDate.getFullYear();

  return year;
}

// Make the function accessible for use in rules
export { now, year };
```

### Utilizzare una funzione personalizzata nel modulo

Per utilizzare la funzione personalizzata nel modulo:

1. **Aggiungi la funzione**: includi la funzione personalizzata nel `[Adaptive form block]/functions.js` file. Ricordati di aggiungerlo all’istruzione di esportazione all’interno del file.
1. **Distribuire il file**: distribuisci il file aggiornato `functions.js` nel progetto GitHub e verificare la corretta generazione.
1. **Utilizzo funzione**: consente di accedere alla funzione all&#39;interno del foglio di calcolo della maschera utilizzando `Value`, `Value Expression`, `Visible`, o `Visible Expression` simili a qualsiasi altra funzione di foglio di calcolo supportata OOTB.
1. **Visualizzare l’anteprima del modulo**: utilizza AEM Sidekick per visualizzare in anteprima il modulo con la nuova funzione implementata.

