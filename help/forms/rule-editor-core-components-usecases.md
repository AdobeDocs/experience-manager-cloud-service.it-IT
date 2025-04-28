---
title: Questo articolo illustra vari casi d’uso per un editor di regole in un modulo adattivo basato su componenti core.
description: L’articolo delinea vari casi d’uso per un editor di regole in un modulo adattivo basato su componenti core.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 8191e113-f768-4b1e-a191-e3c722f19054
source-git-commit: e10451553692b6ad957421783e176409b36b642b
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 0%

---

# Diversi casi d’uso dell’editor di regole

L’articolo fornisce esempi dettagliati di editor di regole per un modulo adattivo basato su componenti core, fornendo informazioni sulla sua corretta implementazione per scenari diversi. L’editor di regole consente agli sviluppatori di definire e gestire la logica che controlla il comportamento dei moduli.
Ora, parliamo delle diverse implementazioni per un editor di regole.

## Imposta lo stato attivo su un altro pannello al clic del pulsante, se il primo pannello è valido

<span class="preview"> Si tratta di una funzionalità pre-release accessibile tramite il [canale pre-release](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features). </span>

L’editor di regole consente di convalidare i layout di un pannello, ad esempio Schede orizzontali, Schede verticali, Accordi o Procedura guidata al clic del pulsante e di impostare lo stato attivo su un oggetto modulo in un altro pannello. Puoi utilizzare questa funzionalità per migliorare la navigazione nei moduli e l’esperienza utente.

Immaginare un modulo applicativo in più passaggi utilizzando un layout della procedura guidata. È necessario completare il pannello `Personal Information` prima di passare a `Employment Details`. Quando fai clic sul pulsante `Next`, l&#39;editor di regole convalida il pannello `Personal Information`. Se tutti i campi obbligatori sono compilati correttamente, il modulo sposta automaticamente lo stato attivo sul pannello `Employment Details`. In caso contrario, viene visualizzato un messaggio di errore in cui si richiede agli utenti di completare i campi mancanti.

È possibile creare una regola sul pulsante `Next` per convalidare il primo pannello:

![Regola per pulsante Avanti](/help/forms/assets/next-rule.png){width=50%}

Quando fai clic sul pulsante **Avanti**, il pannello **Informazioni personali** viene convalidato. Se i dettagli immessi sono corretti, lo stato attivo viene spostato sul pannello **Sicurezza account**. In caso contrario, verrà visualizzato un messaggio di errore in cui si richiede di specificare i dettagli mancanti.

>[!VIDEO](https://video.tv.adobe.com/v/3457767)


## Navigazione tra i pannelli utilizzando il pulsante

L’editor di regole consente di aggiungere pulsanti di navigazione ai layout del pannello, ad esempio Schede orizzontali, Schede verticali, Pannello a soffietto o Procedura guidata. Questi pulsanti migliorano l’esperienza utente semplificando le transizioni tra i diversi pannelli di un modulo, spostando lo stato attivo sul pannello selezionato.

Immagina di interagire con la sezione delle impostazioni di profilo di un’applicazione, in cui la navigazione è facilitata da pulsanti anziché schede. Quando si immettono le impostazioni del profilo dal dashboard principale, si incontrano una serie di pannelli dedicati a diversi aspetti del loro profilo: **Informazioni personali**, **Sicurezza account** e **Preferenze di notifica**.

Ogni pannello contiene campi e opzioni pertinenti per l’aggiornamento di informazioni specifiche. I pulsanti di spostamento, ad esempio `Next` e `Back`, sono posizionati in modo evidente e consentono di spostarsi tra questi pannelli. Fai clic su `Next` per portare l&#39;utente al pannello **Sicurezza account** e fai clic su `Back` per tornare al pannello **Informazioni personali**. Questo metodo di navigazione garantisce una transizione fluida tra le sezioni senza perdere contesto, fornendo un’esperienza utente fluida e intuitiva. L’utilizzo dei pulsanti di navigazione semplifica il processo di gestione delle impostazioni del profilo, rendendo l’interazione più organizzata e di facile utilizzo.

È possibile utilizzare la regola `Navigate among the panels` per creare regole di navigazione per i pulsanti che consentono il passaggio tra pannelli diversi.  Selezionare l&#39;attributo `Shift focus to the next item` per spostare lo stato attivo sul pannello successivo nel layout.

![Regola pannello successivo](/help/forms/assets/rule-editor-navigate-in-panel-next.png){width=50%}

Quando si fa clic sul pulsante `Next`, lo stato attivo si sposta sul pannello successivo nel layout.

![Pulsante Avanti per spostarsi nel pannello](/help/forms/assets/navigate-in-panel.gif)

Analogamente, è possibile creare una regola per il pulsante `Previous` per spostare lo stato attivo sul pannello precedente.

![Regola pannello precedente](/help/forms/assets/rule-editor-navigate-in-panel-previous.png){width=50%}

## Semplificare i calcoli complessi in pannelli ripetibili con le funzioni

L’editor di regole ti consente di utilizzare funzioni predefinite come Somma, Min, Max e Unisci direttamente sui campi all’interno di pannelli ripetibili. Puoi anche passare un valore di campo del pannello ripetibile alla funzione che accetta array di numeri, array di stringhe, array booleano, ecc. Ciò consente una potente automazione, che consente di implementare una logica di business complessa senza codice personalizzato.

Immaginate un modulo con un pannello ripetibile in cui ogni istanza del pannello raccoglie informazioni sul valore dichiarato delle risorse.

![Modulo ripetibile](/help/forms/assets/ootb-function-support-repeatable-panel-form.png)

È possibile utilizzare la funzione `Sum` per calcolare automaticamente il valore totale delle risorse in tutti i pannelli, eliminando la necessità di calcoli manuali e riducendo la possibilità di errori.

![Supporto dei campi del pannello ripetibili nelle funzioni OOTB](/help/forms/assets/ootb-function-support-repeatable-panel.png)

Quando si compila un modulo, aggiungendo istanze per dichiarare i valori delle risorse, il pulsante `Calculate Asset Value` calcola la somma totale di tutti i valori delle risorse dichiarate e visualizza il risultato nella casella di testo `assetvalue`.

![Supporto dei campi del pannello ripetibili nelle funzioni OOTB](/help/forms/assets/ootb-function-support-repeatable-panel-form-preview.png)

>[!NOTE]
>
> Se il valore del campo del pannello ripetibile viene passato a una funzione che non accetta un array, il valore del campo dell’ultima istanza del pannello ripetibile viene passato alla funzione.

Questo è solo un esempio! Esplora le [funzioni](#b-form-objects-and-functions-br) disponibili per semplificare i flussi di lavoro e migliorare la precisione dei dati nei moduli.

## Espressioni nidificate {#nestedexpressions}

L’editor di regole consente di utilizzare più operatori AND e OR per creare regole nidificate. È possibile combinare più operatori AND e OR nelle regole.

Di seguito è riportato un esempio di regola nidificata che visualizza un messaggio all&#39;utente sull&#39;idoneità per la custodia di un figlio quando vengono soddisfatte le condizioni richieste.

![Espressione complessa](assets/complexexpression.png)

Puoi anche trascinare le condizioni all’interno di una regola per modificarla. Seleziona e passa il puntatore del mouse sull&#39;handle ( ![handle](assets/drag-handle.svg)) prima di una condizione. Una volta che il puntatore si trasforma nel simbolo della mano, come illustrato di seguito, trascinare e rilasciare la condizione in qualsiasi punto della regola. La struttura della regola cambia.

![Trascinare](assets/drag-and-drop.png)

## Condizioni di espressione data {#dateexpression}

L’editor di regole consente di utilizzare i confronti tra date per creare condizioni.

Di seguito è riportata una condizione di esempio che visualizza un oggetto di testo statico se l’ipoteca sulla casa è già stata accettata, che l’utente indica compilando il campo data.

Quando la data del mutuo dell’immobile compilata dall’utente è nel passato, il modulo adattivo visualizza una nota relativa al calcolo del reddito. La regola seguente confronta la data compilata dall&#39;utente con la data corrente. Se la data compilata dall&#39;utente è precedente alla data corrente, nel modulo viene visualizzato il messaggio di testo Income.

![Condizione espressione data](assets/dateexpressioncondition.png)

Quando la data di compilazione è precedente alla data corrente, nel modulo viene visualizzato il messaggio di testo (Entrate) nel modo seguente:

![Condizione espressione data soddisfatta](assets/dateexpressionconditionmet.png)

## Condizioni di confronto dei numeri {#number-comparison-conditions}

L’editor di regole consente di creare condizioni che confrontano due numeri.

Di seguito è riportata una condizione di esempio che visualizza un oggetto di testo statico se il numero di mesi in cui un candidato rimane all&#39;indirizzo corrente è inferiore a 36.

![Condizione di confronto dei numeri](assets/numbercomparisoncondition.png)

Quando l’utente indica di vivere all’attuale indirizzo residenziale per meno di 36 mesi, il modulo mostra una notifica che indica che è possibile richiedere più prove di residenza.

![È stata richiesta un&#39;altra bozza](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

### Richiama servizio modello dati modulo {#invoke}

Si consideri un servizio Web `GetInterestRates` che accetta come input l&#39;importo del prestito, la locazione e il punteggio di credito del richiedente e restituisce un piano di prestito che include l&#39;importo dell&#39;IME e il tasso di interesse. È possibile creare un modello dati modulo (FDM) utilizzando il servizio Web come origine dati. Gli oggetti modello dati e un servizio `get` vengono aggiunti al modello di modulo. Il servizio viene visualizzato nella scheda Servizi del modello dati del modulo (FDM). Quindi, crea un modulo adattivo che includa i campi dagli oggetti modello dati per acquisire gli input dell’utente per l’importo del prestito, la durata e il punteggio di credito. Aggiungi un pulsante che attiva il servizio web per recuperare i dettagli del piano. L’output viene compilato nei campi appropriati.

La regola seguente mostra come configurare l’azione Richiama servizio per eseguire lo scenario di esempio.

![Esempio-invoke-services](assets/example-invoke-services.png)

>[!NOTE]
>
>Se l’input è di tipo array, i campi che supportano gli array sono visibili nella sezione a discesa Output.

### Attivazione di più azioni tramite la regola When {#triggering-multiple-actions-using-the-when-rule}

In un modulo di richiesta di prestito, si desidera stabilire se il richiedente è un cliente esistente o meno. In base alle informazioni fornite dall’utente, il campo ID cliente deve essere visualizzato o nascosto. Inoltre, se l’utente è un cliente esistente, imposta il campo ID cliente come elemento attivo. Il modulo di richiesta di prestito presenta le seguenti componenti:

* Un pulsante di scelta, **[!UICONTROL Sei un cliente Geometrixx esistente?]**, che fornisce [!UICONTROL Sì] e [!UICONTROL No] opzioni. Il valore per Sì è **0** e No è **1**.

* Campo di testo, **[!UICONTROL ID cliente Geometrixx]**, per specificare l&#39;ID cliente.

Quando scrivi una regola When sul pulsante di scelta per implementare questo comportamento, la regola viene visualizzata come segue nell’editor di regole visive.

![Esempio-regola-quando](assets/when-rule-example.png)

Nella regola di esempio, l&#39;istruzione nella sezione When è la condizione che, quando restituisce True, esegue le azioni specificate nella sezione Then.

<!-- The rule appears as follows in the code editor.

![when-rule-example-code](assets/when-rule-example-code.png) 

Rule in the code editor -->

### Utilizzo di un output di funzione in una regola {#using-a-function-output-in-a-rule}

In un modulo ordine fornitore è disponibile la tabella seguente, in cui gli utenti compilano i propri ordini. In questa tabella:

* La prima riga è ripetibile, in modo che gli utenti possano ordinare più prodotti e specificare quantità diverse. Il nome elemento è `Row1`.
* Il titolo della cella nella colonna Quantità prodotto della riga ripetibile è Quantità. Il nome elemento per questa cella è `productquantity`.
* La seconda riga della tabella non è ripetibile e il titolo della cella nella colonna Quantità prodotto di questa riga è Quantità totale.

![Esempio-tabella-funzione](assets/example-function-table.png)

**A.** Riga1 **B.** Quantità **C.** Quantità Totale

Ora si desidera aggiungere le quantità specificate nella colonna Quantità prodotto per tutti i prodotti e visualizzare la somma nella cella Quantità totale. È possibile ottenere tale somma scrivendo una regola Imposta valore di nella cella Quantità totale come illustrato di seguito.

![Esempio-funzione-output](assets/example-function-output.png)

### Convalida di un valore di campo tramite espressione {#validating-a-field-value-using-expression}

Nel modulo dell&#39;ordine di acquisto illustrato nell&#39;esempio precedente, si desidera impedire all&#39;utente di ordinare più di una quantità di qualsiasi prodotto il cui prezzo sia superiore a 10000. Per eseguire questa convalida, è possibile scrivere una regola di convalida come illustrato di seguito.

![Esempio-convalida](assets/example-validate.png)

## Consulta anche

{{see-also-rule-editor}}
