---
title: Utilizzare le regole per aggiungere un comportamento dinamico a un modulo
description: Edge Delivery Services per AEM Forms è progettato per offrire prestazioni di picco, per semplificare e ottimizzare le esperienze di raccolta dati e coinvolgimento degli utenti. Utilizzare le regole per aggiungere un comportamento dinamico a un modulo.
feature: Edge Delivery Services
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 100%

---

# Utilizzare le regole per aggiungere un comportamento dinamico a un modulo

Una delle potenti funzionalità della creazione di moduli utilizzando un foglio di calcolo è la possibilità di utilizzare funzioni incorporate per creare regole, che consentono di visualizzare o nascondere in modo condizionale i campi modulo, automatizzare i calcoli in base agli input dell’utente e creare un’esperienza utente più dinamica.

Questo articolo illustra come utilizzare principalmente varie proprietà del blocco di modulo adattivo, principalmente le proprietà del foglio di calcolo [`Visible`](#visible-property), [`Visibility Expression`](#visible-expression-property) e [`Value Expression`](#value-expression-property) insieme a [funzioni del foglio di calcolo](#spreadsheet-functions-for-rules) per creare regole efficaci per i moduli. Esamineremo anche alcuni esempi per illustrare come queste regole possono essere implementate nella pratica.

## Informazioni sui costrutti di una regola

Le regole sono come istruzioni che ci dicono cosa fare in situazioni diverse. Una regola ha in genere i seguenti costrutti:

- Condizioni: specificano le circostanze in cui si applica la regola. Considerale come una domanda a cui bisogna rispondere (sì o no).

- Azioni: definiscono cosa accade quando la condizione viene soddisfatta (true) o non viene soddisfatta (false).


Ad esempio, per visualizzare una casella e-mail, quando è selezionata una casella di controllo:

- Condizione: la casella di controllo “Ti piacerebbe abbonarti a riviste e attività?” è selezionata. (Sì o no?). Questa condizione è impostata nella proprietà `Visible` del modulo.
- Azione (True): la casella e-mail è visibile. (Cosa succede se è sì). `Visibility Expression` utilizza la condizione definita in modo che la proprietà `visible` visualizzi dinamicamente i campi.
- Azione (False): la casella e-mail è nascosta. (Cosa succede se è no). `Visibility Expression` utilizza la condizione definita in modo che la proprietà `Value` nasconda dinamicamente i campi.

Per istruzioni dettagliate, consultare [mostra/nascondi campo e-mail in base a una condizione](#example-1-conditional-email-field)


## Informazioni sulle proprietà Valore, Visibile, Espressione di visibilità ed Espressione di valore

### Proprietà Visibile

Immagina un interruttore di luce per il campo modulo. La proprietà `Visible` è simile a tale interruttore, che controlla se il campo è inizialmente visibile nel modulo al primo caricamento.

- True (come se l’interruttore della luce fosse “on”): il campo viene visualizzato nel modulo.
- False (come se l’interruttore della luce fosse “off”): il campo è nascosto nel modulo.

È possibile utilizzare la formula del foglio di calcolo (incluso il tag = ) per scrivere una formula utilizzando una logica simile a quella del foglio di calcolo per determinare la visibilità del campo. In questa formula è possibile utilizzare i valori di altri campi del modulo. Ad esempio, se un utente seleziona “Individuo” in un campo di tipo registrazione, si può nascondere il campo e-mail utilizzando una formula che controlla tale valore.

### Proprietà Espressione visibile (mostrare/nascondere un campo)

La proprietà `Visible Expression` consente di utilizzare la regola aggiunta alla proprietà `Visible` per decidere se mostrare o nascondere il campo in base alle interazioni dell’utente.

Utilizza `=FORMULATEXT("Address of the corresponding Visible property)` per portare la formula indicata nella proprietà `Visible` come stringa per il campo `Visible Expression` al suo interno. Questa opzione è necessaria per mostrare/nascondere dinamicamente i campi in un modulo pubblicato.

![Forumaltext](/help/edge/assets/aem-forms-formulatext.png)

### Proprietà Valore (imposta i dati iniziali)

Immaginate un valore preimpostato su un interruttore dimmer per la luce di una stanza. La proprietà `Value` è simile e determina lo stato iniziale dei dati che utente visualizza nel campo.  Imposta o recupera i dati correnti visualizzati nel campo modulo.

Al primo caricamento del modulo, la proprietà `Value` determina ciò che l’utente vede nel campo prima di apportare qualsiasi modifica. A differenza delle proprietà `Visible` e `Visible Expression`, che controllano la visibilità, la proprietà Valore influisce direttamente sui dati stessi. Gli utenti possono modificare questo valore digitando, selezionando le opzioni (menu a discesa) o interagendo con il campo.

È possibile utilizzare la formula di Excel (incluso il tag = ) per scrivere una formula utilizzando una logica simile a quella del foglio di calcolo per determinare il valore visualizzato nel campo. In questa formula è possibile utilizzare i valori di altri campi del modulo. Ad esempio, è possibile calcolare automaticamente uno sconto in base all’importo dell’ordine inserito in un altro campo.


### Proprietà Espressione valore (calcola i valori da visualizzare in un campo)

Questa proprietà consente di controllare il valore visualizzato all’interno di un campo basato su una formula, simile all’Espressione visibile. Somiglia a una calcolatrice incorporata nel campo.

Utilizza `=FORMULATEXT("Address of the corresponding Value property)` per portare la formula indicata nella proprietà `Value` come stringa per il campo `Value Expression` al suo interno. Questa opzione è necessaria per calcolare e visualizzare in modo dinamico i valori calcolati in un modulo pubblicato.

![Forumaltext](/help/edge/assets/aem-forms-formulatext-value.png)

Di seguito è riportata un’analogia per consolidare questi concetti:

- Visibile: immagina una forma come una casa. La proprietà “Visible” è simile all’interruttore della luce per ogni stanza (campo). Decidi se la stanza è inizialmente illuminata (visibile) o scura (nascosta) quando qualcuno entra in casa (apre il modulo).
- Espressione visibile: simile a un interruttore della luce con sensore di movimento. La stanza (campo) potrebbe essere inizialmente scura (nascosta), ma una formula (sensore di movimento) può attivarla (mostrare il campo) se qualcuno passa accanto (modifica il valore in un altro campo).
- Valore: è come un interruttore dimmer preimpostato per la luce (dati iniziali nel campo). Gli utenti possono quindi regolare la luminosità (modificare il valore).
- Espressione valore: simile a una calcolatrice sofisticata incorporata nel cartellino del prezzo di un prodotto della casa (modulo). Il cartellino del prezzo (campo) mostra il prezzo finale basato su una formula (ad esempio, l’aggiunta di imposte al prezzo base) che utilizza altre informazioni analoghe (valore di un altro campo).

Combinando queste proprietà con [funzioni del foglio di calcolo](#spreadsheet-functions-for-rules), è possibile ottenere un’ampia gamma di comportamenti dinamici all’interno dei moduli.

## Funzioni del foglio di calcolo per le regole

Il Blocco moduli adattivi supporta diverse funzioni dei fogli di calcolo che possono essere utilizzate per creare regole. Di seguito sono riportate le funzioni disponibili come pronte all’uso:

### Funzioni logiche

- [NOT()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110): inverte lo stato logico (TRUE diventa FALSE e viceversa).
- [AND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND): restituisce TRUE solo se tutte le condizioni specificate sono TRUE.
- [OR()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR): restituisce TRUE se almeno una delle condizioni specificate è TRUE.

### Funzioni condizionali

- [IF()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110): valuta una condizione e restituisce un valore specifico se TRUE e un altro valore se FALSE.

### Funzioni matematiche

- [SUM()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM): aggiunge valori da un intervallo di celle specificato.
- [ROUND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND): arrotonda un numero a un numero specificato di cifre decimali.
- [MIN()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN): restituisce il valore più piccolo da un intervallo di celle specificato.

## Creazione di una regola

Approfondiamo alcuni esempi pratici per illustrare come le regole possono essere utilizzate per migliorare i moduli:

## Esempio 1: campo e-mail condizionale

Questo esempio mostra come la casella di controllo funge da condizione. Quando è selezionata (la condizione è true), viene visualizzata la casella e-mail (azione per true). Se non è selezionata (la condizione è false), la casella e-mail rimane nascosta (azione per false).

Creare un modulo con una casella di controllo e una casella e-mail, come illustrato nell’immagine seguente:

![Modulo e-mail condizionale](/help/edge/assets/aem-forms-conditional-email-form.png)


Di seguito viene illustrato come utilizzare una regola per visualizzare il campo e-mail alla selezione di una casella di controllo:

1. Imposta la proprietà `Value` del campo casella di controllo su `TRUE`.
1. Imposta la proprietà `Checked` del campo casella di controllo su `FALSE`. In questo modo, per impostazione predefinita, la casella di controllo non è selezionata.
1. Imposta la proprietà `Visible` del campo e-mail su `=[address of Checked property of the checkbox field] = true()`. Ad esempio `=Q11=TRUE()`. La formula verifica se la casella di controllo è selezionata o meno. Se la casella di controllo è selezionata, la formula restituisce TRUE. Se la casella di controllo non è selezionata, la formula restituisce FALSE.



   La funzione `TRUE()` restituisce il valore logico quando viene impostata per puntare alla proprietà `Checked`, se `checked = false` restituisce false. Se `checked=true`, restituisce `true`. In questo modo, per impostazione predefinita, il campo e-mail è nascosto.


1. Imposta la proprietà `Visible Expression` del campo casella di controllo su `=FORMULATEXT ((address of Visible property of the checkbox field))`. Ad esempio, `=FORMULATEXT((G12))`. La funzione FORMULATEXT() accetta una formula come input e restituisce la formula stessa come stringa di testo. Questo consente di utilizzare la formula nel modulo.

   ![Campo e-mail condizionale](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. Visualizzare in anteprima e pubblicare il modulo. Ora, quando si seleziona la casella di controllo, viene visualizzato il campo e-mail, e quando si deseleziona, il campo viene nascosto, offrendo un’esperienza utente dinamica.

   ![E-mail condizionale](/help/edge/assets/aem-forms-coditional-email.gif)


## Esempio 2: calcolo automatico

In questo esempio viene illustrato il modo in cui un modulo calcola automaticamente il costo stimato di un viaggio quando si selezionano le date del viaggio in un modulo.

Crea un modulo con un campo data, costo della stanza, i campi con costo stimato del viaggio come mostrato di seguito e una casella e-mail come illustrato nell’immagine seguente:

![Modulo e-mail condizionale](/help/edge/assets/aem-forms-automatic-calculations-form.png)

Di seguito viene descritto come utilizzare un calcolo automatico per visualizzare il costo stimato del viaggio:

1. Imposta la proprietà `Value` del campo `amount` su `=F6*DAYS(F3,F2)`. Questa formula calcola il numero di giorni da `Start Date` a `End Date`, moltiplica il numero di giorni per il costo della stanza e visualizza il risultato nel campo `Estimated Trip Cost`.

1. Imposta la proprietà `Value Expression` del campo `Estimated Trip Cost` su `=FORMULATEXT ((address of value property of the amount field))`. Ad esempio `=FORMULATEXT(F7)`. La funzione FORMULATEXT() accetta una formula come input e restituisce la formula stessa come stringa di testo. Questo consente di utilizzare la formula nel modulo.

1. Visualizzare in anteprima e pubblicare il modulo. Ora, specifica `Start Date`, `End Date` e il costo della stanza. Il `Estimated Trip Cost` viene calcolato automaticamente.

## Esempi di funzioni del foglio di calcolo


Di seguito sono riportati alcuni esempi di funzioni del foglio di calcolo comunemente utilizzate:

**Funzioni logiche:**

- **NOT():** inverte lo stato logico (TRUE diventa FALSE e viceversa).

  Esempio: se il campo e-mail viene lasciato vuoto, viene nascosto il campo “Conferma e-mail”.

   1. Imposta la proprietà `Visible` del campo “Conferma e-mail” su `=NOT(if('address of email field'=""))`.

      ![AEM Forms nasconde il campo di conferma e-mail](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. Imposta l’espressione visibile del campo “Conferma e-mail” su `=FORMULATEXT ((address of visible property of the Confirm Email field))`

      ![Formula per espressione visibile di AEM Forms](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


- AND(): restituisce TRUE solo se tutte le condizioni specificate sono TRUE.

   - Esempio: abilita un pulsante “Invia” solo se tutti i campi obbligatori sono compilati.

   1. Imposta la proprietà `Visible` del pulsante “Invia” su:



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      Ad esempio,

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. Imposta l’espressione visibile del campo “Conferma e-mail” su

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      Ad esempio,

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      Questa formula mostra il pulsante “invia” (TRUE) solo se tutti i campi (nome, e-mail, telefono) sono compilati (NOT() restituisce TRUE per ciascuno), altrimenti nasconde il pulsante (AND(più FALSES) = FALSE).

- OR(): restituisce TRUE se almeno una delle condizioni specificate è TRUE.

   - Esempio: l’applicazione di uno sconto se un utente inserisce uno qualsiasi dei codici dei coupon di sconto applicabili.

   1. Imposta la proprietà `Visible` del campo “importo finale” su:


  ```JavaScript
     =IF(OR(F14="BlackFridaySale", F14="NewYearDiscount"), (F6*DAYS(F3,F2)* 0.7) , (F6*DAYS(F3,F2)))
  ```

   1. Imposta l’espressione del valore del campo “Conferma e-mail” su

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      Ad esempio,

      ```JavaScript
      =FORMULATEXT(F7)
      ```

      Questa formula calcola uno sconto del 30%, se l’utente immette un codice coupon (couponCode = &quot;NewYearDiscount&quot;) OPPURE (couponCode = &quot;BlackFridaySale&quot;), altrimenti imposta lo sconto su 0.

**Funzioni testo:**

- IF(): valuta una condizione e restituisce un valore specifico se TRUE e un altro valore se FALSE.

   - Esempio: la visualizzazione di un messaggio personalizzato in base a una categoria di prodotto selezionata.

   1. Imposta la proprietà `Value` del campo `message` su `Only upto 7 kg check-in lagguage is allowed!`:

   1. Imposta la proprietà `Visible` del campo `message` su:


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      Ad esempio,

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. Imposta l’espressione del valore del campo `message` su

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      Ad esempio,

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      Questa formula visualizza il messaggio “È consentito il check-in per un bagaglio di un peso non superiore ai 7 kg!” se la classe scelta è “Economy”, altrimenti il campo del messaggio resta vuoto.

**Funzioni matematiche:**

- SUM(): aggiunge valori da un intervallo di celle specificato.

  Esempio: il calcolo del costo totale degli articoli in un carrello.

  Nell’espressione del valore del campo “costo totale”:
SUM(prezzo * quantità)

  Questa formula presuppone che siano presenti campi separati per “prezzo” e “quantità” di ciascun articolo. Li moltiplica e utilizza SUM() per sommare il costo totale di tutti gli articoli nel carrello.

- ROUND(): arrotonda un numero a un numero specificato di cifre decimali.

  Esempio: l’arrotondamento dell’importo calcolato di uno sconto a due cifre decimali.

  Nell’espressione del valore del campo “importo sconto” (supponendo che uno sconto venga calcolato altrove):
ROUND(sconto, 2)

  Questa formula arrotonda il valore dello sconto a due cifre decimali.

- MIN(): restituisce il valore più piccolo da un intervallo di celle specificato.

  Esempio: l’individuazione dell’età minima richiesta per un modulo di registrazione basato su un paese selezionato.

  Nell’espressione del valore di un campo “età minima”:
MIN(ageLimits[“USA”], ageLimits[“UK”], ageLimits[“Francia”])

  Questa formula presuppone che sia disponibile una tabella denominata “ageLimits” in cui sono memorizzati i requisiti di età minima per i diversi paesi. Utilizza MIN() per trovare il valore più basso di tutti.


Inoltre, il Blocco moduli adattivi consente di procedere alla redazione completa dei moduli creando [funzioni personalizzate](#creating-custom-functions). Le funzioni personalizzate permettono di definire regole e logiche personalizzate, offrendo un controllo completo sul funzionamento dei moduli.


## Creazione e distribuzione di funzioni personalizzate

Il Blocco moduli adattivi predefinito (OOTB) fornisce implementazioni per molte [funzioni comuni dei fogli di calcolo](#spreadsheet-functions-for-rules). Tuttavia, per un controllo più granulare sui moduli, puoi utilizzare una qualsiasi delle funzioni OOTB disponibili in Microsoft® Excel o Fogli Google all’interno dei Blocchi moduli adattivi. Il Blocco moduli adattivi non contiene l’implementazione per tutte le funzioni OOTB disponibili in Microsoft® Excel o in Fogli Google. Se hai bisogno di una di queste funzioni, puoi sviluppare una funzione personalizzata con una sintassi simile per ottenere la funzionalità fornita da Microsoft® Excel o Fogli Google. Ad esempio, puoi implementare la [funzione Anno() di Microsoft® Excel](https://support.microsoft.com/en-us/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#) per calcolare l’età dalla data di nascita.


### Creare una funzione personalizzata

Le funzioni personalizzate sono incluse nel file `[Adaptive form block]/functions.js`. Il processo di creazione prevede in genere i seguenti passaggi:

- Dichiarazione di funzione: definisce il nome della funzione e i relativi parametri (gli input accettati).
- Implementazione logica: scrive il codice che illustra i calcoli o le manipolazioni specifiche eseguiti dalla funzione.
- Funzione esportazione: rende la funzione accessibile all’interno delle tue regole esportandola dal file pertinente.

### Esempio: funzione Anno

In questo esempio vengono illustrate due funzioni personalizzate che imitano la funzione ANNO() di Microsoft® Excel per calcolare l’età:


```JavaScript
/**
 - Get the current date and time
 - @name now
 - @returns {Date} The current date and time as a Date object
 */
function now() {
  const today = new Date();
  return today;
}

/**
 - Get the year from a Date object
 - @name year
 - @param {Date} date The date object
 - @throws {TypeError} If the input is not a Date object
 - @returns {number} The year as a number
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

1. **Aggiungi la funzione**: includi la funzione personalizzata nel file `[Adaptive form block]/functions.js`. Ricordati di aggiungerla all’istruzione di esportazione all’interno del file.
1. **Distribuisci il file**: distribuisci il file `functions.js` aggiornato nel progetto GitHub e verifica la corretta compilazione.
1. **Utilizzo funzione**: accedi alla funzione all’interno del foglio di calcolo del modulo utilizzandole proprietà `Value`, `Value Expression`, `Visible` o `Visible Expression` simili a qualsiasi altra funzione OOTB di foglio di calcolo supportata.
1. **Visualizza l’anteprima del modulo**: utilizza AEM Sidekick per visualizzare l’anteprima del modulo con la nuova funzione implementata.

