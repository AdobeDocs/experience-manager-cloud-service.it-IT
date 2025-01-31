---
title: Come utilizzare l’editor di regole per applicare regole ai campi modulo, abilitando il comportamento dinamico e la logica complessa per i moduli creati con l’authoring WYSIWYG?
description: L’editor di regole nell’editor universale consente di aggiungere un comportamento dinamico e di creare una logica complessa nei moduli senza dover codificare o scrivere script.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: c27b8e413c060de601a72a669d86c4add2a4167d
workflow-type: tm+mt
source-wordcount: '2111'
ht-degree: 5%

---


# Introduzione all’editor di regole nell’editor universale

È possibile aggiungere il comportamento di un modulo dinamico utilizzando l&#39;Editor di regole, che consente di creare regole. Queste regole abilitano la visibilità dei campi condizionali, automatizzano i calcoli in base all’input dell’utente e migliorano l’esperienza utente complessiva. Semplificando il processo di compilazione dei moduli, l’Editor regole contribuisce a garantire sia precisione che efficienza.

L’editor di regole offre un’interfaccia visiva intuitiva per la creazione e la gestione delle regole. Il suo approccio semplice e intuitivo lo rende accessibile a tutti gli utenti, anche a quelli che non dispongono di competenze tecniche approfondite, consentendo loro di implementare la logica senza sforzo all’interno dei loro moduli.

## Informazioni su una regola

Le regole sono istruzioni che guidano gli utenti su quali azioni eseguire in condizioni specifiche.

* **Condizione**: una condizione è un controllo o una regola che valuta se qualcosa è vero o falso. Risponde alla domanda: &quot;Questo soddisfa i requisiti?&quot;

* **Azione**: un&#39;azione è ciò che accade quando la condizione è vera. È l’attività o il comportamento attivato in base alla valutazione della condizione.

Una regola segue in genere uno dei seguenti costrutti:

* **Condizione-Azione**: controlla prima una condizione, quindi esegui un&#39;azione. Nell&#39;editor delle regole, il tipo di regola `When` applica il costrutto `condition-action`.
* **Action-Condition**: esegui prima un&#39;azione, quindi verifica una condizione. I tipi di regole `Set Value Of` e `Validate` nell&#39;editor di regole impongono il costrutto `action-condition`.
* **Azione-Condizione-Azione alternativa**: eseguire un&#39;azione, controllare una condizione e quindi eseguire l&#39;azione principale o un&#39;azione alternativa in base alla condizione. Per impostazione predefinita, ad esempio, l&#39;azione alternativa per `Show` è `Hide` e per `Enable` è `Disable`.

Ad esempio, una condizione può verificare se un utente ha immesso un determinato valore in un campo e l’azione può consistere nel mostrare o nascondere un campo.
* **Condizione**: verifica se il reddito è superiore a 50.000 dollari.
* **Azione**: se la condizione è vera, visualizzare il campo `Additional Deduction`. In caso contrario, eseguire l&#39;azione alternativa: nascondere il campo `Additional Deduction`.

Per istruzioni dettagliate, vedere [aggiungere una regola condizionale](#2-add-a-conditional-rule).

## Come si abilita l’estensione Editor regole?

Nell’editor universale, l’editor di regole non è attivato per impostazione predefinita. Per abilitare l&#39;estensione Editor regole per il tuo ambiente, invia un&#39;e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con la tua richiesta.

Dopo aver abilitato l&#39;estensione Editor regole per l&#39;ambiente, l&#39;icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg) viene visualizzata nell&#39;angolo superiore destro dell&#39;editor.

![Editor regole dell&#39;editor universale](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

Selezionare l&#39;oggetto modulo per il quale si desidera scrivere una regola e fare clic sull&#39;icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Viene visualizzata l&#39;interfaccia utente dell&#39;editor di regole.

![Interfaccia utente dell&#39;editor di regole](/help/edge/docs/forms/assets/rule-editor-for-field.png)

Ora puoi iniziare a scrivere regole o regole business per il campo modulo selezionato utilizzando i [tipi di regole disponibili nell&#39;Editor regole](#available-rule-types-in-rule-editor).

## Interfaccia utente dell’editor di regole

L&#39;editor visivo dell&#39;editor di regole viene aperto quando si fa clic sull&#39;icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg):

![Interfaccia utente editor regole](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>Componente dell’editor di regole</th>
      <th>Descrizione</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. Visualizzazione delle regole dei componenti</td>
      <td>Visualizza il titolo dell'oggetto modulo tramite il quale è stato avviato l'Editor regole e il tipo di regola attualmente selezionato.</td>
    </tr>
    <tr>
      <td>2. Oggetti e funzioni del modulo</td>
      <td>La scheda <b>Oggetti Forms</b> mostra una visualizzazione gerarchica di tutti gli oggetti contenuti nel modulo. La scheda <b>Funzioni</b> include un set di funzioni incorporate.</td>
    </tr>
    <tr>
      <td>3. Attivazione/disattivazione di funzioni e oggetti modulo</td>
      <td>Quando viene toccato, questo pulsante attiva o disattiva il riquadro delle funzioni e degli oggetti del modulo.</td>
    </tr>
    <tr>
      <td>4. Editor di regole visive</td>
      <td>L'editor di regole visive è l'area in cui si scrivono le regole nella modalità editor visivo dell'interfaccia utente dell'editor di regole.</td>
    </tr>
    <tr>
      <td>5. Tasti Done e cancel</td>
      <td>Il pulsante <b>Fine</b> viene utilizzato per salvare una regola. Il pulsante <b>Annulla</b> elimina le modifiche apportate a una regola e chiude l'editor di regole.</td>
    </tr>
  </tbody>
</table>

Tutte le regole esistenti su un oggetto modulo vengono elencate quando si seleziona l&#39;oggetto. Puoi visualizzare il titolo e un’anteprima del riepilogo delle regole nell’editor di regole visivo. Inoltre, puoi modificare l’ordine delle regole, modificarle, abilitarle o disabilitarle o eliminarle.

![mostra le regole disponibili dell&#39;oggetto modulo](/help/edge/docs/forms/assets/rule-editor15.png)

## Tipi di regole disponibili

L&#39;Editor regole fornisce un insieme di tipi di regole predefiniti che è possibile utilizzare per scrivere regole, come illustrato nella tabella seguente:

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
      <td>Imposta il valore di un oggetto modulo a seconda che la condizione specificata sia soddisfatta o meno.</td>
    </tr>
    <tr>
      <td>Cancella valore</td>
      <td>Cancella il valore dell'oggetto specificato.</td>
    </tr>
    <tr>
      <td>Nascondi/Mostra</td>
      <td>Nasconde o mostra un oggetto modulo a seconda che una condizione sia soddisfatta o meno.</td>
    </tr>
    <tr>
      <td>Abilita/Disabilita</td>
      <td>Attiva o disattiva un oggetto modulo in base al soddisfacimento o meno di una condizione.</td>
    </tr>
    <tr>
      <td>Convalida</td>
      <td>Convalida il modulo o un oggetto specificato.</td>
    </tr>
    <tr>
      <td>Quando  </td>
      <td>Segue il costrutto della regola di azione <i>condition-action-alternate</i> o <i>condition-action</i>. Specifica una condizione per la valutazione seguita da un’azione da attivare se la condizione viene soddisfatta.</td>
    </tr>
    <tr>
      <td>Formato</td>
      <td>Formatta un oggetto modulo in base a una funzione o a un'espressione regolare.</td>
    </tr>
    <tr>
      <td>Avvia servizio</td>
      <td>Richiama un servizio configurato in un modello dati modulo (FDM).</td>
    </tr>
    <tr>
      <td>Imposta proprietà</td>
      <td>Imposta il valore di una proprietà dell'oggetto specificato in base a una condizione.</td>
    </tr>
    <tr>
      <td>Imposta Fuoco</td>
      <td>Imposta lo stato attivo sull'oggetto specificato.</td>
    </tr>
    <tr>
      <td>Modulo salva</td>
      <td>Salva il modulo.</td>
    </tr>
    <tr>
      <td>Invia/Reimposta modulo</td>
      <td>Invia o reimposta il modulo.</td>
    </tr>
    <tr>
      <td>Aggiungi/Rimuovi istanza</td>
      <td>Aggiunge o rimuove un'istanza del pannello o della riga di tabella ripetibile specificata.</td>
    </tr>
    <tr>
      <td>Accedi a</td>
      <td>Passa ad altri Forms adattivi, ad altre risorse come immagini o frammenti di documenti o a un URL esterno.</td>
    </tr>
    <tr>
      <td>Evento di invio</td>
      <td>Attiva azioni specifiche in base a condizioni o eventi predefiniti.</td>
    </tr>
    <tr>
      <td>Naviga tra i pannelli</td>
      <td>Consente di spostare lo stato attivo tra i diversi pannelli di un modulo.</td>
    </tr>
  </tbody>
</table>


Esaminiamo ora come [scrivere regole nell&#39;editor di regole](#write-rules).

## Scrivi regole

Per informazioni su come scrivere regole nell’Editor di regole visive, consideriamo un semplice esempio di modulo di calcolo delle imposte:

![Esempio di editor di regole](/help/edge/docs/forms/assets/rule-editor-1.png)

Nella forma descritta in precedenza, l&#39;utente immette lo stipendio lordo. In base a questo input, viene visualizzato il campo condizionale e viene calcolata l&#39;imposta a debito.

**Campi modulo:**
* Stipendio lordo (input utente)
* Detrazione aggiuntiva (campo condizionale)
* Reddito imponibile (campo calcolato)
* Imposta a debito (campo calcolato)

**Regola condizionale:**
* Condizione: stipendio lordo > 50.000
* Azione: mostrare il campo Detrazione aggiuntiva

**Regole di calcolo:**

* Reddito imponibile = Stipendio lordo - Detrazione aggiuntiva (se applicabile)
* Imposta dovuta = reddito imponibile * Aliquota (per semplicità, si supponga un&#39;aliquota fissa del 10%)

Per scrivere le regole, effettua le seguenti operazioni:

### 1. Creare un modulo

Per creare un modulo in Universal Editor:

1. Aprire un modulo in Universal Editor per la modifica.
1. Aggiungi i seguenti componenti modulo:
   * Modulo di calcolo imposta (titolo)
   * Stipendio lordo (immissione testo)
   * Detrazione aggiuntiva (immissione testo)
   * Reddito imponibile (input testo)
   * Imposta a debito (immissione testo)
   * Invia (pulsante Invia)
1. Nascondere il campo modulo `Additional Deduction` aprendo `Properties`.

   ![Esempio di editor di regole](/help/edge/docs/forms/assets/rule-editor2.png)

### 2. Aggiungere una regola condizionale per un campo modulo

Dopo aver creato il modulo, scrivere la prima regola per visualizzare il campo `Additional Deduction` solo se lo stipendio lordo supera i 50.000 dollari. Per aggiungere una regola condizionale:

1. Aprire un modulo in Universal Editor per la modifica.
1. Selezionare il componente **[!UICONTROL Stipendio lordo]** nella struttura contenuto e selezionare ![edit-rules](/help/forms/assets/edit-rules-icon.svg).
   ![Esempio di editor di regole1](/help/edge/docs/forms/assets/rule-editor3.png)
Viene visualizzata l&#39;interfaccia visiva dell&#39;Editor di regole.
1. Fai clic su **[!UICONTROL Crea]** per avviare l&#39;editor di regole.
   ![Esempio di editor di regole2](/help/edge/docs/forms/assets/rule-editor4.png)
Per impostazione predefinita, è selezionato il tipo di regola `Set Value Of`. Sebbene non sia possibile modificare l&#39;oggetto selezionato, è possibile utilizzare l&#39;elenco a discesa delle regole per selezionare un altro tipo di regola.\
   ![Esempio di editor di regole3](/help/edge/docs/forms/assets/rule-editor5.png)
1. Apri l&#39;elenco a discesa Tipo di regola e seleziona **[!UICONTROL Tipo di regola]**.
   ![Esempio di editor di regole4](/help/edge/docs/forms/assets/rule-editor6.png)
1. Seleziona l&#39;elenco a discesa **[!UICONTROL Seleziona stato]** e seleziona **[!UICONTROL è maggiore di]**. Viene visualizzato il campo **[!UICONTROL Immettere un numero]**.
   ![Esempio di editor di regole5](/help/edge/docs/forms/assets/rule-editor7.png)
1. Immettere `50000` nel campo **[!UICONTROL Immettere un numero]** nella regola.
   ![Esempio di editor di regole6](/help/edge/docs/forms/assets/rule-editor8.png)
La condizione è stata definita come `When Gross Salary is greater than 50000`. Definire quindi l&#39;azione da eseguire se la condizione è `True`.
1. Nell&#39;istruzione `Then`, selezionare **[!UICONTROL Mostra]** dal menu a discesa **[!UICONTROL Seleziona azione]**.
   ![Esempio di editor di regole7](/help/edge/docs/forms/assets/rule-editor9.png)
1. Trascina il campo **[!UICONTROL Detrazione aggiuntiva]** dalla scheda Oggetti modulo del campo **[!UICONTROL Rilascia oggetto o seleziona qui]**. In alternativa, selezionare il campo **[!UICONTROL Rilascia oggetto o seleziona qui]** e selezionare il campo **[!UICONTROL Detrazione aggiuntiva]** dal menu a comparsa, in cui sono elencati tutti gli oggetti modulo nel modulo.
   ![Esempio di editor di regole8](/help/edge/docs/forms/assets/rule-editor10.png)
1. Fare clic su **[!UICONTROL Aggiungi sezione Else]** per aggiungere un&#39;altra condizione per il campo **[!UICONTROL Stipendio lordo]**, nel caso in cui si immette uno stipendio inferiore a `50000`.
   ![Esempio di editor di regole9](/help/edge/docs/forms/assets/rule-editor11.png)
1. Selezionare **[!UICONTROL Nascondi]** dal menu a discesa **[!UICONTROL Seleziona azione]** nell&#39;istruzione `Else`.
   ![Esempio di editor di regole10](/help/edge/docs/forms/assets/rule-editor12.png)
1. Trascina il campo **[!UICONTROL Detrazione aggiuntiva]** dalla scheda Oggetti modulo del campo **[!UICONTROL Rilascia oggetto o seleziona qui]**. In alternativa, selezionare il campo **[!UICONTROL Rilascia oggetto o seleziona qui]** e selezionare il campo **[!UICONTROL Detrazione aggiuntiva]** dal menu a comparsa, in cui sono elencati tutti gli oggetti modulo nel modulo.
   ![Esempio di editor di regole11](/help/edge/docs/forms/assets/rule-editor13.png)
1. Seleziona **[!UICONTROL Fine]** per salvare la regola.
La regola viene visualizzata come segue nell’Editor regole.
   ![Esempio di editor di regole12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> In alternativa, è possibile scrivere una regola Mostra nel campo Detrazione aggiuntiva, anziché una regola Quando nel campo Stipendio lordo, per implementare lo stesso comportamento.

### 3. Aggiungere regole di calcolo per i campi modulo

Scrivere quindi una regola per calcolare `Taxable Income`, che è la differenza tra `Gross Salary` e `Additional Deduction` (se applicabile). Per aggiungere la regola di calcolo nel campo **[!UICONTROL Reddito imponibile]**, eseguire la procedura seguente:

1. In modalità creazione, seleziona il campo **[!UICONTROL Entrate tassabili]** e seleziona l&#39;icona ![modifica-regole](/help/forms/assets/edit-rules-icon.svg). Quindi, seleziona **[!UICONTROL Crea]** per avviare l&#39;editor di regole.
   ![Esempio di editor di regole13](/help/edge/docs/forms/assets/rule-editor16.png)
1. Seleziona **[!UICONTROL Seleziona opzione]** e seleziona **[!UICONTROL Espressione matematica]**. Viene aperto un campo per scrivere espressioni matematiche.
   ![Esempio di editor di regole14](/help/edge/docs/forms/assets/rule-editor17.png)

1. Nel campo espressione matematica:

   * Seleziona o trascina dalla scheda Oggetto Forms il campo **[!UICONTROL Stipendio lordo]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   * Seleziona **[!UICONTROL Meno]** dal campo **[!UICONTROL Seleziona operatore]**.

   * Seleziona o trascina dalla scheda Oggetto Forms il campo **[!UICONTROL Detrazione aggiuntiva]** nell&#39;altro campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.
     ![Esempio di editor di regole15](/help/edge/docs/forms/assets/rule-editor18.png)

1. Seleziona **[!UICONTROL Fine]** per salvare la regola.

   Aggiungere ora una regola per il campo `Tax Payable `, determinata moltiplicando il reddito imponibile per l&#39;aliquota fiscale. Per semplicità, si supponga un&#39;aliquota fissa di `10%`.

1. In modalità creazione, seleziona il campo **[!UICONTROL Imposta da pagare]** e seleziona l&#39;icona ![modifica-regole](/help/forms/assets/edit-rules-icon.svg). Quindi, seleziona **[!UICONTROL Crea]** per avviare l&#39;editor di regole.
   ![Esempio di editor di regole16](/help/edge/docs/forms/assets/rule-editor19.png)
1. Seleziona **[!UICONTROL Seleziona opzione]** e seleziona **[!UICONTROL Espressione matematica]**. Viene aperto un campo per scrivere espressioni matematiche.
   ![Esempio di editor di regole17](/help/edge/docs/forms/assets/rule-editor20.png)
1. Nel campo espressione matematica:

   * Seleziona o trascina dalla scheda Oggetto Forms il campo **[!UICONTROL Entrate tassabili]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   * Seleziona **[!UICONTROL Moltiplicato per]** dal campo **[!UICONTROL Seleziona operatore]**.

   * Selezionare **Numero** dal campo **[!UICONTROL Seleziona opzione]** e immettere il valore `10` nel campo **[!UICONTROL Immetti un numero]**.
     ![Esempio di editor di regole18](/help/edge/docs/forms/assets/rule-editor21.png)
1. Quindi, seleziona nell&#39;area evidenziata intorno al campo espressione e seleziona **[!UICONTROL Estendi espressione]**.
   ![Esempio di editor di regole19](/help/edge/docs/forms/assets/rule-editor22.png)
1. Nel campo espressione estesa, selezionare **[!UICONTROL diviso per]** dal campo **[!UICONTROL Seleziona operatore]** e **[!UICONTROL Numero]** dal campo **[!UICONTROL Seleziona opzione]**. Quindi, specificare `100` nel campo numerico.
   ![Esempio editor regole20](/help/edge/docs/forms/assets/rule-editor23.png)
1. Seleziona **[!UICONTROL Fine]** per salvare la regola.

### 4. Anteprima di un modulo

Ora, quando si visualizza l&#39;anteprima del modulo e si immette **Stipendio lordo** come `60,000`, viene visualizzato il campo **Detrazione aggiuntiva** e vengono calcolati di conseguenza **Reddito imponibile** e **Imposta pagabile**.

![Anteprima modulo](/help/edge/docs/forms/assets/rule-editor-form.png)

Oltre alle funzioni predefinite come Somma, Media elencate in Output funzioni, è possibile [scrivere funzioni personalizzate](#create-a-custom-function) per implementare logiche aziendali complesse.

## Funzione personalizzata nell’editor di regole

Edge Delivery Services Forms supporta funzioni personalizzate che consentono agli utenti di definire le funzioni JavaScript per l&#39;implementazione di regole aziendali complesse. Le funzioni personalizzate estendono le funzionalità dei moduli facilitando la manipolazione e l’elaborazione dei dati immessi per soddisfare requisiti specifici.

### Creare una funzione personalizzata

Per creare funzioni personalizzate, modificare il file `../[blocks]/form/functions.js`. Il processo di creazione prevede in genere i seguenti passaggi:

* **Dichiarazione di funzione**: definire il nome della funzione e i relativi parametri (gli input accettati).
* **Implementazione logica**: scrivere il codice che delinea i calcoli o le manipolazioni specifici eseguiti dalla funzione.
* **Esportazione funzione**: rendi la funzione accessibile all&#39;interno delle tue regole esportandola dal file rilevante.


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
![Aggiunta funzione personalizzata](/help/edge/docs/forms/assets/create-custom-function.png)

### Utilizzare una funzione personalizzata nell’editor di regole

Per utilizzare la funzione personalizzata nell’editor di regole:

1. **Aggiungi la funzione**: includi la funzione personalizzata nel file`../[blocks]/form/functions.js`. Ricordarsi di aggiungerlo all&#39;istruzione `export` nel file.
1. **Distribuisci il file**: distribuisci il file `functions.js` aggiornato nel progetto GitHub e verifica la corretta compilazione.
1. **Utilizzo funzione**: accedere alla funzione nell&#39;Editor regole del modulo selezionando l&#39;opzione `Function Output` nel campo **[!UICONTROL Seleziona azione]**.

   ![Funzione personalizzata nell&#39;editor di regole](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **Anteprima modulo**: visualizza l&#39;anteprima del modulo con la nuova funzione implementata.

## Articoli correlati

{{see-also-rule-editor}}

## Consulta anche

* [Guida introduttiva a Edge Delivery Services per AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Creare un modulo utilizzando Google Sheets o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Impostare i fogli di Google o i file di Microsoft Excel per iniziare ad accettare i dati](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare il modulo e iniziare a raccogliere i dati](/help/edge/docs/forms/publish-forms.md)
* [Personalizzare l’aspetto dei moduli](/help/edge/docs/forms/style-theme-forms.md)
* [Aggiungere sezioni ripetibili a un modulo](/help/edge/docs/forms/repeatable-forms.md)
* [Mostra un messaggio di ringraziamento personalizzato dopo l’invio del modulo](/help/edge/docs/forms/thank-you-page-form.md)
* [Componenti del blocco modulo adattivo e relative proprietà](/help/edge/docs/forms/form-components.md)
* [Monitoraggio dell’utilizzo reale](https://www.aem.live/developer/rum#authentication)
