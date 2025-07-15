---
title: Come utilizzare l’editor di regole per applicare regole ai campi modulo, abilitando il comportamento dinamico e la logica complessa per i moduli creati con l’authoring WYSIWYG?
description: L’editor di regole nell’editor universale consente di aggiungere un comportamento dinamico e di creare una logica complessa nei moduli senza dover dover scrivere codice di programmazione o script.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: tm+mt
source-wordcount: '2216'
ht-degree: 97%

---


# Introduzione all’editor di regole nell’authoring WYSIWYG

<span class="preview"> Questa è una funzionalità pre-release disponibile tramite il nostro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features">canale pre-release</a>. </span>


È possibile aggiungere il comportamento di un modulo dinamico utilizzando l’editor di regole, che consente di creare regole. Queste regole abilitano la visibilità dei campi condizionali, automatizzano i calcoli in base a quanto immesso dall’utente e migliorano l’esperienza utente complessiva. Semplificando il processo di compilazione dei moduli, l’editor di regole favorisce sia l’accuratezza che l’efficienza.

L’editor di regole offre un’interfaccia visiva intuitiva per la creazione e la gestione delle regole. Il suo approccio semplice e intuitivo lo rende accessibile a tutti, anche a chi non dispone di competenze tecniche approfondite, consentendo loro di implementare facilmente elementi di logica all’interno dei moduli.

## Informazioni sulle regole

Le regole sono istruzioni che guidano l’utente in merito alle azioni da eseguire in condizioni specifiche.

* **Condizione**: una condizione è un controllo o una regola che valuta se qualcosa è vero o falso. Risponde alla domanda: “Soddisfa i requisiti?”

* **Azione**: un’azione è ciò che accade quando la condizione si verifica (vero). È l’attività o il comportamento che viene attivato in base alla valutazione della condizione.

Una regola segue in genere uno dei seguenti costrutti:

* **Condizione-Azione**: valuta se si verifica una condizione, quindi esegui un’azione. Nell’editor delle regole, il tipo di regola `When` applica il costrutto `condition-action`.
* **Azione-Condizione**: esegui un’azione, quindi valuta se si verifica una condizione. I tipi di regole `Set Value Of` e `Validate` nell’editor di regole impongono il costrutto `action-condition`.
* **Azione-Condizione-Azione alternativa**: esegui un’azione, valuta se si verifica una condizione, quindi esegui l’azione principale o un’azione alternativa in base alla condizione. Per impostazione predefinita, ad esempio, l’azione alternativa per `Show` è `Hide` e per `Enable` è `Disable`.

Ad esempio, nel caso di condizione che verifica se un utente ha immesso o meno un determinato valore in un campo, l’azione può consistere nel mostrare o nascondere un altro campo.
* **Condizione**: verifica se il reddito è superiore a 50.000 dollari.
* **Azione**: se l’esito della condizione è “vero”, visualizza il campo `Additional Deduction`. In caso contrario, esegui l’azione alternativa: nascondi il campo `Additional Deduction`.

Per istruzioni dettagliate, consulta [Aggiungere una regola condizionale](#2-add-a-conditional-rule).

## Come si abilita l’estensione dell’editor di regole?

Nell’editor universale, l’estensione editor di regole non è attivata per impostazione predefinita. Per abilitare l’estensione editor regole, scrivi all’indirizzo [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) dal tuo ID e-mail ufficiale.

Una volta che l’estensione dell’editor di regole sarà stata abilitata per il tuo ambiente, l’icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg) sarà visibile nell’angolo in alto a destra dell’editor.

![Editor di regole dell’editor universale](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

Seleziona il componente modulo per il quale desideri scrivere una regola e fai clic sull’icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Viene visualizzata l’interfaccia utente dell’editor di regole.

![Interfaccia utente dell’editor di regole](/help/edge/docs/forms/assets/rule-editor-for-field.png)

In questo articolo, `form object` e `form component` sono utilizzati in modo intercambiabile.

Ora puoi iniziare a scrivere regole o logica di business per il campo modulo selezionato utilizzando i [tipi di regole disponibili nell’editor di regole](#available-rule-types-in-rule-editor).

## Interfaccia utente dell’editor di regole

Quando fai clic sull’icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg), si apre l’editor dell’editor di regole:

![Interfaccia utente dell’editor di regole](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>Componente dell’editor di regole</th>
      <th>Descrizione</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. Titolo</td>
      <td>Mostra il titolo del componente modulo e il tipo di regola selezionato. Ad esempio, “Inserisci stipendio lordo” è un componente casella di testo per il quale è selezionato il tipo di regola “Quando”. </td>
    </tr>
    <tr>
      <td>2. Oggetti modulo e funzioni</td>
      <td>La scheda <b>Oggetti modulo</b> mostra una vista gerarchica di tutti gli oggetti contenuti nel modulo. La scheda <b>Funzioni</b> include un set di funzioni incorporate nell’editor di regole.</td>
    </tr>
    <tr>
      <td>3. Pulsante di attivazione/disattivazione Oggetti modulo e Funzioni</td>
      <td>Il pulsante di attivazione/disattivazione mostra o nasconde il riquadro Oggetti modulo o il riquadro Funzioni. </td>
    </tr>
    <tr>
      <td>4. Editor di regole visivo</td>
      <td>L’editor di regole visivo è l’interfaccia in cui puoi creare regole per i componenti del modulo.</td>
    </tr>
    <tr>
      <td>5. Tasti Fine e Annulla</td>
      <td>Il pulsante <b>Fine</b> viene utilizzato per salvare una regola. Il pulsante <b>Annulla</b> elimina le modifiche apportate a una regola e chiude l’editor di regole.</td>
    </tr>
  </tbody>
</table>

Tutte le regole esistenti su un componente modulo vengono elencate quando si seleziona il componente. Puoi visualizzare il titolo e un’anteprima del riepilogo delle regole nell’editor di regole. Inoltre, puoi modificare l’ordine delle regole, modificarle, abilitarle, disabilitarle o eliminarle.

![mostra le regole disponibili dell’oggetto modulo](/help/edge/docs/forms/assets/rule-editor15.png)

## Tipi di regole disponibili

L’editor di regole fornisce un insieme di tipi di regole predefinite che è possibile utilizzare per scrivere regole, come illustrato nella tabella seguente:

<table border="1">
  <thead>
    <tr>
      <th>Tipo di regola</th>
      <th>Descrizione</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Imposta valore di</td>
      <td>Imposta il valore di un componente modulo a seconda che la condizione specificata sia soddisfatta o meno.</td>
    </tr>
    <tr>
      <td>Cancella valore di</td>
      <td>Cancella il valore del componente modulo specificato.</td>
    </tr>
    <tr>
      <td>Nascondi/Mostra</td>
      <td>Nasconde o mostra un componente modulo a seconda che una condizione sia soddisfatta o meno.</td>
    </tr>
    <tr>
      <td>Abilita/Disabilita</td>
      <td>Attiva o disattiva un componente modulo a seconda che una condizione sia soddisfatta o meno.</td>
    </tr>
    <tr>
      <td>Convalida</td>
      <td>Verifica il componente modulo in base a una condizione e visualizza un errore se la condizione non è soddisfatta. </td>
    </tr>
    <tr>
      <td>Quando  </td>
      <td>Specifica una condizione per la valutazione seguita da un’azione da attivare se la condizione viene soddisfatta. Segue il costrutto della regola di azione <i>condition-action-alternate</i> o <i>condition-action</i>. </td>
    </tr>
    <tr>
      <td>Formato</td>
      <td> Modifica il valore visualizzato del componente modulo utilizzando l’espressione specificata quando cambia il relativo valore.</td>
    </tr>
    <tr>
      <td>Richiama servizio</td>
      <td>Richiama un servizio configurato utilizzando API esterne, un modello dati modulo o i servizi web RESTful.</td>
    </tr>
    <tr>
      <td>Imposta proprietà</td>
      <td>Imposta il valore di una proprietà del componente modulo specificato in base a una condizione.</td>
    </tr>
    <tr>
      <td>Imposta stato attivo</td>
      <td>Imposta lo stato attivo sul componente modulo specificato.</td>
    </tr>
    <tr>
      <td>Salva modulo</td>
      <td>Consente all’utente di salvare il modulo come bozza utilizzando il componente Portale Forms Bozze e invii. </td>
    </tr>
    <tr>
      <td>Invia modulo</td>
      <td>Invia il modulo.</td>
    </tr>
    <tr>
      <td>Reimposta modulo</td>
      <td>Reimposta il modulo.</td>
    </tr>
    <tr>
      <td>Aggiungi/Rimuovi istanza</td>
      <td>Aggiunge o rimuove un’istanza del pannello o della riga di tabella ripetibile specificata.</td>
    </tr>
    <tr>
      <td>Passa a</td>
      <td>Passa ad altri moduli adattivi, ad altre risorse come immagini o frammenti di documenti o a un URL esterno.</td>
    </tr>
    <tr>
      <td>Evento di invio</td>
      <td>Attiva azioni specifiche in base a condizioni o eventi predefiniti.</td>
    </tr>
    <tr>
      <td>Spostati tra i pannelli</td>
      <td>Consente di spostare lo stato attivo tra i diversi pannelli di un modulo.</td>
    </tr>
  </tbody>
</table>


Esaminiamo ora come [scrivere regole nell’editor di regole](#write-rules).

## Scrivere regole

Per informazioni su come scrivere regole nell’editor di regole visivo, prendiamo in considerazione un semplice esempio di modulo di calcolo delle imposte:

![Schermata dell&#39;interfaccia dell&#39;editor di regole che mostra la creazione di una regola condizionale con logica When-Then per la visibilità dei campi modulo](/help/edge/docs/forms/assets/rule-editor-1.png)

Nel modulo descritto in precedenza, l’utente immette lo stipendio lordo. In base a questo input, viene visualizzato il campo condizionale e viene calcolata l’imposta dovuta.

**Campi modulo:**
* Stipendio lordo (input utente)
* Detrazione aggiuntiva (campo condizionale)
* Reddito imponibile (campo calcolato)
* Imposta dovuta (campo calcolato)

**Regola condizionale:**
* Condizione: stipendio lordo > 50.000
* Azione: mostrare il campo Detrazione aggiuntiva

**Regole di calcolo:**

* Reddito imponibile = Stipendio lordo: detrazione aggiuntiva (se applicabile)
* Imposta dovuta = Reddito imponibile * Aliquota (per semplicità, supponiamo un’aliquota fissa del 10%)

Per scrivere regole, esegui i seguenti passaggi:

### &#x200B;1. Creare un modulo

Per creare un modulo nell’editor universale:

1. Apri un modulo nell’editor universale per la modifica.
1. Aggiungi i seguenti componenti modulo:
   * Modulo di calcolo imposta (titolo)
   * Stipendio lordo (immissione numero)
   * Detrazione aggiuntiva (immissione numero)
   * Reddito imponibile (immissione numero)
   * Imposta dovuta (immissione numero)
   * Invia (pulsante Invia)
1. Nascondi il campo modulo `Additional Deduction` aprendo `Properties`.

   ![Schermata di un modulo di calcolo delle imposte con campi di input per lo stipendio lordo, lo stato civile e i figli dipendenti, che illustra la struttura del modulo prima dell&#39;applicazione delle regole](/help/edge/docs/forms/assets/rule-editor2.png)

### &#x200B;2. Aggiungere una regola condizionale per un campo modulo

Dopo aver creato il modulo, scrivi la prima regola per visualizzare il campo `Additional Deduction` solo se lo stipendio lordo supera i 50.000 dollari. Per aggiungere una regola condizionale:

1. Apri un modulo nell’editor universale per la modifica e seleziona il campo **[!UICONTROL Stipendio lordo]** nella struttura contenuto, quindi seleziona ![edit-rules](/help/forms/assets/edit-rules-icon.svg). In alternativa, puoi selezionare il campo **[!UICONTROL Stipendio lordo]** direttamente dal riquadro **[!UICONTROL Oggetto Forms]**.
   ![Esempio di editor di regole1](/help/edge/docs/forms/assets/rule-editor3.png)
Viene visualizzata l’interfaccia dell’editor di regole visivo.
1. Fai clic su **[!UICONTROL Crea]** per creare le regole.
   ![Esempio di editor di regole2](/help/edge/docs/forms/assets/rule-editor4.png)
Per impostazione predefinita, è selezionato il tipo di regola `Set Value Of`. Sebbene non sia possibile cambiare o modificare l’oggetto selezionato, è possibile utilizzare l’elenco a discesa delle regole per selezionare un altro tipo di regola.\
   ![Esempio di editor di regole3](/help/edge/docs/forms/assets/rule-editor5.png)
1. Apri l’elenco a discesa Tipo di regola e seleziona il tipo di regola **[!UICONTROL Quando]**.
   ![Esempio di editor di regole4](/help/edge/docs/forms/assets/rule-editor6.png)
1. Seleziona l’elenco a discesa **[!UICONTROL Seleziona stato]** e seleziona **[!UICONTROL è maggiore di]**. Viene visualizzato il campo **[!UICONTROL Immetti un numero]**.
   ![Esempio di editor di regole5](/help/edge/docs/forms/assets/rule-editor7.png)
1. Immetti `50000` nel campo **[!UICONTROL Immetti un numero]** nella regola.
   ![Esempio di editor di regole6](/help/edge/docs/forms/assets/rule-editor8.png)
La condizione è stata definita come `When Gross Salary is greater than 50000`. Definisci quindi l’azione da eseguire se la condizione è `True`.
1. Nell’istruzione `Then`, seleziona **[!UICONTROL Mostra]** dal menu a discesa **[!UICONTROL Seleziona azione]**.
   ![Esempio di editor di regole7](/help/edge/docs/forms/assets/rule-editor9.png)
1. Trascina il campo **[!UICONTROL Detrazione aggiuntiva]** dalla scheda Oggetti modulo del campo **[!UICONTROL Rilascia oggetto o seleziona qui]**. In alternativa, seleziona il campo **[!UICONTROL Rilascia oggetto o seleziona qui]** e seleziona il campo **[!UICONTROL Detrazione aggiuntiva]** dal menu a comparsa, in cui sono elencati tutti gli oggetti modulo nel modulo.
   ![Esempio di editor di regole8](/help/edge/docs/forms/assets/rule-editor10.png)
1. Fai clic su **[!UICONTROL Aggiungi altra sezione]** per aggiungere un’altra condizione per il campo **[!UICONTROL Stipendio lordo]**, nel caso in cui sia immesso uno stipendio inferiore a `50000`.
   ![Esempio di editor di regole9](/help/edge/docs/forms/assets/rule-editor11.png)
1. Seleziona **[!UICONTROL Nascondi]** dal menu a discesa **[!UICONTROL Seleziona azione]** nell’istruzione `Else`.
   ![Esempio di editor di regole10](/help/edge/docs/forms/assets/rule-editor12.png)
1. Trascina il campo **[!UICONTROL Detrazione aggiuntiva]** dalla scheda Oggetti modulo nel campo **[!UICONTROL Rilascia oggetto o seleziona qui]**. In alternativa, seleziona il campo **[!UICONTROL Rilascia oggetto o seleziona qui]** e seleziona il campo **[!UICONTROL Detrazione aggiuntiva]** dal menu a comparsa, in cui sono elencati tutti gli oggetti modulo nel modulo.
   ![Editor di regole, esempio 11](/help/edge/docs/forms/assets/rule-editor13.png)
1. Per salvare la regola, fai clic su **[!UICONTROL Fine]**.
La regola viene visualizzata nell’editor di regole nel modo seguente.
   ![Editor di regole, esempio 12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> In alternativa, per implementare lo stesso comportamento, è possibile scrivere una regola Mostra nel campo Detrazione aggiuntiva, anziché una regola Quando nel campo Stipendio lordo.

### &#x200B;3. Aggiungere regole di calcolo per i campi modulo

Scrivi quindi una regola per calcolare il `Taxable Income`, che è la differenza tra `Gross Salary` e `Additional Deduction` (se applicabile). Per aggiungere la regola di calcolo nel campo **[!UICONTROL Reddito imponibile]**, esegui i seguenti passaggi:

1. In modalità di authoring, seleziona il campo **[!UICONTROL Reddito imponibile]** e quindi l’icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg). In alternativa, puoi selezionare il campo **[!UICONTROL Reddito imponibile]** direttamente dal riquadro **[!UICONTROL Oggetto Forms]**.
1. Quindi, seleziona **[!UICONTROL Crea]** per creare la regola.
   ![Editor di regole, esempio 13](/help/edge/docs/forms/assets/rule-editor16.png)
1. Seleziona **[!UICONTROL Seleziona opzione]** e scegli **[!UICONTROL Espressione matematica]**. Si apre un campo in cui scrivere espressioni matematiche.
   ![Editor di regole, esempio 14](/help/edge/docs/forms/assets/rule-editor17.png)

1. Nel campo per le espressioni matematiche:

   * Seleziona o trascina dalla scheda Oggetto modulo il campo **[!UICONTROL Stipendio lordo]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   * Seleziona **[!UICONTROL Meno]** dal campo **[!UICONTROL Seleziona operatore]**.

   * Seleziona o trascina dalla scheda Oggetto modulo il campo **[!UICONTROL Detrazione aggiuntiva]** nell’altro campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

     ![Editor di regole, esempio 15](/help/edge/docs/forms/assets/rule-editor18.png)

1. Per salvare la regola, fai clic su **[!UICONTROL Fine]**.

   Aggiungi ora una regola per il campo `Tax Payable `, determinata moltiplicando il reddito imponibile per l’aliquota fiscale. Per semplicità, supponiamo un’aliquota fissa di `10%`.

1. In modalità di authoring, seleziona il campo **[!UICONTROL Imposta dovuta]** e seleziona l’icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Successivamente, seleziona **[!UICONTROL Crea]** per creare le regole.
   ![Editor di regole, esempio 16](/help/edge/docs/forms/assets/rule-editor19.png)
1. Seleziona **[!UICONTROL Seleziona opzione]** e seleziona **[!UICONTROL Espressione matematica]**. Si apre un campo in cui scrivere espressioni matematiche.
   ![Editor di regole, esempio 17](/help/edge/docs/forms/assets/rule-editor20.png)
1. Nel campo per le espressioni matematiche:

   * Seleziona o trascina dalla scheda Oggetto modulo il campo **[!UICONTROL Reddito imponibile]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   * Seleziona **[!UICONTROL Moltiplicato per]** dal campo **[!UICONTROL Seleziona operatore]**.

   * Seleziona **Numero** dal campo **[!UICONTROL Seleziona opzione]** e immetti il valore `10` nel campo **[!UICONTROL Immetti un numero]**.

     ![Editor di regole, esempio 18](/help/edge/docs/forms/assets/rule-editor21.png)
1. Quindi, seleziona nell’area evidenziata intorno al campo espressione e seleziona **[!UICONTROL Estendi espressione]**.
   ![Editor di regole, esempio 19](/help/edge/docs/forms/assets/rule-editor22.png)
1. Nel campo espressione estesa, seleziona **[!UICONTROL diviso per]** dal campo **[!UICONTROL Seleziona operatore]** e **[!UICONTROL Numero]** dal campo **[!UICONTROL Seleziona opzione]**. Quindi, specifica `100` nel campo Numero.
   ![Editor di regole, esempio 20](/help/edge/docs/forms/assets/rule-editor23.png)
1. Per salvare la regola, seleziona **[!UICONTROL Fine]**.

### &#x200B;4. Visualizzare l’anteprima di un modulo

Ora, quando visualizzi l’anteprima del modulo e immetti come **Stipendio lordo** `60,000`, viene visualizzato il campo **Detrazione aggiuntiva** e vengono calcolati di conseguenza il **Reddito imponibile** e l’**Imposta dovuta**.

![Visualizzare l’anteprima di un modulo](/help/edge/docs/forms/assets/rule-editor-form.png)

Oltre alle funzioni predefinite come Somma, Media elencate in Output funzioni, è possibile [scrivere funzioni personalizzate](#create-a-custom-function) per implementare logiche aziendali complesse.

## Funzione personalizzata nell’editor di regole

I moduli di Edge Delivery Services supportano funzioni personalizzate che consentono agli utenti di definire funzioni JavaScript per l’implementazione di regole aziendali complesse. Le funzioni personalizzate estendono le funzionalità dei moduli facilitando la manipolazione e l’elaborazione dei dati immessi per soddisfare requisiti specifici.

### Creare una funzione personalizzata

Per creare funzioni personalizzate, modifica il file `../[blocks]/form/functions.js`. Il processo di creazione prevede in genere i seguenti passaggi:

* **Dichiarazione di funzione**: definisce il nome della funzione e i relativi parametri (gli input accettati).
* **Implementazione logica**: scrive il codice che illustra i calcoli o le manipolazioni specifiche eseguiti dalla funzione.
* **Esportazione funzione**: rende la funzione accessibile all’interno delle tue regole esportandola dal file pertinente.


In questo esempio vengono illustrate due funzioni personalizzate come `getFullName` e `days`:

```JavaScript
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in Stringformat
 * @param {string} lastname in Stringformat
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 * Calculate the number of days between two dates.
 * @param {*} endDate
 * @param {*} startDate
 * @name days Calculates the numebr of days between two dates
 * @returns {number} returns the number of days between two dates
 */
function days(endDate, startDate) {
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // return zero if dates are valid
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// eslint-disable-next-line import/prefer-default-export
export { getFullName, days };
```

![Aggiunta di una funzione personalizzata](/help/edge/docs/forms/assets/create-custom-function.png)

### Utilizzare una funzione personalizzata nell’editor di regole

Per utilizzare la funzione personalizzata nell’editor di regole:

1. **Aggiungi la funzione**: includi la funzione personalizzata nel file `../[blocks]/form/functions.js`. Ricordati di aggiungerla all’istruzione `export` all’interno del file.
1. **Distribuisci il file**: distribuisci il file `functions.js` aggiornato nel progetto GitHub e verifica la corretta compilazione.
1. **Utilizzo funzione**: accedi alla funzione nell’editor di regole del modulo selezionando l’opzione `Function Output` nel campo **[!UICONTROL Seleziona azione]**.

   ![Funzione personalizzata nell’editor di regole](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **Visualizza l’anteprima del modulo**: visualizza l’anteprima del modulo con la nuova funzione implementata.

## Informazioni aggiuntive

>[!NOTE]
>
> Nell’editor universale, le importazioni statiche e dinamiche non sono supportate negli script di funzione personalizzati. È necessario aggiungere il codice completo nel file `../[blocks]/form/functions.js`.

Questo articolo fornisce informazioni limitate sull’editor di regole disponibile nell’editor universale. Per ulteriori informazioni sull’editor di regole e sulle funzioni personalizzate, consulta i seguenti articoli:

{{see-also-rule-editor}}

## Consulta anche

{{universal-editor-see-also}}
