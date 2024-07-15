---
title: Come si utilizza l’editor di regole per aggiungere regole ai campi modulo per aggiungere un comportamento dinamico e creare una logica complessa in un modulo adattivo basato su componenti core?
description: L’editor di regole di Forms adattivo consente di aggiungere un comportamento dinamico e di creare una logica complessa nei moduli senza codificare o scrivere script.
feature: Adaptive Forms, Core Components
role: User
level: Beginner, Intermediate
exl-id: 1292f729-c6eb-4e1b-b84c-c66c89dc53ae
source-git-commit: 46cd7d689c6cbc453720b5798ffb552da58f66e7
workflow-type: tm+mt
source-wordcount: '5627'
ht-degree: 1%

---


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service (Componenti core) | Questo articolo |
| AEM as a Cloud Service (Componenti di base) | [Fai clic qui](/help/forms/rule-editor.md) |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html) |

# Aggiungere regole a un modulo adattivo (componenti core) {#adaptive-forms-rule-editor}

La funzione dell’editor di regole consente agli utenti aziendali e agli sviluppatori di Forms di scrivere regole sugli oggetti Adaptive Form. Queste regole definiscono le azioni da attivare sugli oggetti modulo in base a condizioni preimpostate, input dell&#39;utente e azioni dell&#39;utente sul modulo. Consente di semplificare ulteriormente l’esperienza di compilazione dei moduli, garantendo precisione e velocità.

L’editor di regole fornisce un’interfaccia utente intuitiva e semplificata per scrivere regole. L’editor di regole offre un editor visivo per tutti gli utenti.<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. --> Alcune delle azioni chiave che è possibile eseguire sugli oggetti modulo adattivo utilizzando le regole sono:

* Mostrare o nascondere un oggetto
* Attivare o disattivare un oggetto
* Impostare un valore per un oggetto
* Convalidare il valore di un oggetto
* Eseguire funzioni per calcolare il valore di un oggetto
* Richiamare un modello dati del modulo (FDM) ed eseguire un’operazione
* Impostare la proprietà di un oggetto

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Gli utenti aggiunti al gruppo forms-power-users possono creare script e modificare quelli esistenti. Gli utenti del gruppo [!DNL forms-users] possono utilizzare gli script ma non crearli o modificarli.

## Differenza tra l’editor di regole nei componenti core e nei componenti di base

{{rule-editor-diff}}

>[!NOTE]
>
> Per informazioni dettagliate su come creare e utilizzare funzioni personalizzate, consulta l&#39;articolo [Funzioni personalizzate in Forms adattivo (componenti core)](/help/forms/create-and-use-custom-functions.md).

## Informazioni su una regola {#understanding-a-rule}

Una regola è una combinazione di azioni e condizioni. Nell’editor delle regole, le azioni includono attività quali nascondere, mostrare, abilitare, disabilitare o calcolare il valore di un oggetto in un modulo. Le condizioni sono espressioni booleane che vengono valutate eseguendo controlli e operazioni sullo stato, sul valore o sulla proprietà di un oggetto modulo. Le azioni vengono eseguite in base al valore ( `True` o `False`) restituito valutando una condizione.

L’editor di regole fornisce un set di tipi di regole predefiniti, ad esempio Quando, Mostra, Nascondi, Abilita, Disabilita, Imposta valore di e Convalida, per facilitare la scrittura delle regole. Ogni tipo di regola ti consente di definire condizioni e azioni in una regola. Il documento spiega ulteriormente ogni tipo di regola nei dettagli.

Una regola segue in genere uno dei seguenti costrutti:

**Condizione-Azione** In questo costrutto, una regola definisce innanzitutto una condizione seguita da un&#39;azione da attivare. Il costrutto è paragonabile all&#39;istruzione if-then nei linguaggi di programmazione.

Nell&#39;editor di regole, il tipo di regola **When** applica il costrutto condizione-azione.

**Action-Condition** In questo costrutto, una regola definisce innanzitutto un&#39;azione da attivare seguita da condizioni per la valutazione. Un’altra variante di questo costrutto è action-condition-alternate action, che definisce anche un’azione alternativa da attivare se la condizione restituisce False.

I tipi di regola Mostra, Nascondi, Abilita, Disabilita, Imposta valore di e Convalida nell&#39;editor di regole applicano il costrutto regola della condizione azione. Per impostazione predefinita, l&#39;azione alternativa per Mostra è Nascondi e per Abilita è Disabilita e viceversa. Non è possibile modificare l&#39;azione alternativa predefinita.

>[!NOTE]
>
>I tipi di regole disponibili, incluse le condizioni e le azioni definite nell&#39;editor di regole, dipendono anche dal tipo di oggetto modulo su cui si sta creando una regola. Nell&#39;editor delle regole vengono visualizzati solo i tipi di regole e le opzioni validi per la scrittura di istruzioni di condizione e azione per un particolare tipo di oggetto modulo. Ad esempio, non vengono visualizzati i tipi Convalida e Imposta valore di per un oggetto pannello.

Per ulteriori informazioni sui tipi di regole disponibili nell&#39;editor di regole, vedere [Tipi di regole disponibili nell&#39;editor di regole](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### Linee guida per la scelta di un costrutto regola {#guidelines-for-choosing-a-rule-construct}

Sebbene sia possibile ottenere la maggior parte dei casi d’uso utilizzando qualsiasi costrutto di regola, di seguito sono riportate alcune linee guida per scegliere un costrutto rispetto a un altro. Per ulteriori informazioni sulle regole disponibili nell&#39;editor di regole, vedere [Tipi di regole disponibili nell&#39;editor di regole](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* Una regola tipica del pollice durante la creazione di una regola è pensarla nel contesto dell&#39;oggetto su cui si sta scrivendo una regola. Si supponga di voler nascondere o visualizzare il campo B in base al valore specificato dall&#39;utente nel campo A. In questo caso, si sta valutando una condizione nel campo A e, in base al valore restituito, si sta attivando un&#39;azione nel campo B.

  Pertanto, se si sta scrivendo una regola nel campo B (l&#39;oggetto su cui si sta valutando una condizione), utilizzare il costrutto condizione-azione o il tipo di regola When. Allo stesso modo, utilizza il costrutto action-condition o il tipo di regola Show o Hide sul campo A.

* A volte, è necessario eseguire più azioni in base a una condizione. In questi casi, si consiglia di utilizzare il costrutto condizione-azione. In questo costrutto, puoi valutare una condizione una sola volta e specificare più istruzioni di azione.

  Ad esempio, per nascondere i campi B, C e D in base alla condizione che verifica il valore specificato dall&#39;utente nel campo A, scrivere una regola con il costrutto condizione-azione o il tipo di regola When nel campo A e specificare azioni per controllare la visibilità dei campi B, C e D. In caso contrario, sono necessarie tre regole separate per i campi B, C e D, in cui ogni regola controlla la condizione e mostra o nasconde il rispettivo campo. In questo esempio, è più efficiente scrivere il tipo di regola When su un oggetto anziché Show o Hide su tre oggetti.

* Per attivare un’azione in base a più condizioni, si consiglia di utilizzare il costrutto azione-condizione. Ad esempio, per mostrare e nascondere il campo A valutando le condizioni nei campi B, C e D, utilizzare Mostra o Nascondi tipo di regola nel campo A.
* Utilizza il costrutto condizione-azione o condizione azione se la regola contiene un’azione per una condizione.
* Se una regola verifica la presenza di una condizione ed esegue immediatamente un&#39;azione quando fornisce un valore in un campo o esce da un campo, si consiglia di scrivere una regola con il costrutto condizione-azione o il tipo di regola When nel campo in cui viene valutata la condizione.
* La condizione nella regola When viene valutata quando un utente modifica il valore dell&#39;oggetto su cui viene applicata la regola When. Tuttavia, se desideri che l’azione si attivi quando il valore cambia sul lato server, come per il prepopolamento del valore, è consigliabile scrivere una regola When che attivi l’azione quando il campo viene inizializzato.
* Quando si scrivono regole per gli oggetti menu a discesa, pulsanti di scelta o caselle di controllo, le opzioni o i valori di tali oggetti modulo nel modulo vengono precompilati nell’editor di regole.

## Tipi di operatori ed eventi disponibili nell’editor di regole {#available-operator-types-and-events-in-rule-editor}

L’editor di regole fornisce i seguenti operatori logici ed eventi utilizzando i quali è possibile creare regole.

* **È Uguale A**
* **È Diverso Da**
* **Inizia con**
* **Termina Con**
* **Contiene**
* **Non contiene**
* **È Vuoto**
* **Non È Vuoto**
* **Ha selezionato:** Restituisce true quando l&#39;utente seleziona un&#39;opzione particolare per una casella di controllo, un elenco a discesa o un pulsante di scelta.
* **È inizializzato (evento):** Restituisce true quando viene eseguito il rendering di un oggetto modulo nel browser.
* **È stato modificato (evento):** Restituisce true quando l&#39;utente modifica il valore immesso o l&#39;opzione selezionata per un oggetto modulo.

<!--
* **Navigation(event):** Returns true when the user clicks a navigation object. Navigation objects are used to move between panels. 
* **Step Completion(event):** Returns true when a step of a rule completes.
* **Successful Submission(event):** Returns true on successful submission of data to a form data model.
* **Error in Submission(event):**  Returns true on unsuccessful submission of data to a form data model. -->

## Tipi di regole disponibili nell’editor di regole {#available-rule-types-in-rule-editor}

L’editor di regole fornisce un set di tipi di regole predefiniti che è possibile utilizzare per scrivere regole. Esaminiamo in dettaglio ogni tipo di regola. Per ulteriori informazioni sulla scrittura di regole nell&#39;editor di regole, vedere [Scrivi regole](rule-editor.md#p-write-rules-p).

### [!UICONTROL Quando] {#whenruletype}

Il tipo di regola **[!UICONTROL When]** segue il costrutto della regola **condition-action-alternate action** oppure, a volte, solo il costrutto **condition-action**. In questo tipo di regola si specifica innanzitutto una condizione per la valutazione seguita da un&#39;azione da attivare se la condizione viene soddisfatta ( `True`). Durante l&#39;utilizzo del tipo di regola When, è possibile utilizzare più operatori AND e OR per creare [espressioni nidificate](#nestedexpressions).

Utilizzando il tipo di regola When, è possibile valutare una condizione in un oggetto modulo ed eseguire azioni su uno o più oggetti.

In parole semplici, una regola When tipica è strutturata come segue:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

`Action 2 on Object B;`
`AND`
&quot;Azione 3 sull’oggetto C;

`Else, do the following:`

`Action 2 on Object C;`
_

Quando si dispone di un componente con più valori, ad esempio pulsanti di scelta o elenco, durante la creazione di una regola per tale componente le opzioni vengono recuperate e rese disponibili automaticamente al creatore della regola. Non è necessario digitare nuovamente i valori delle opzioni.

Ad esempio, un elenco include quattro opzioni: Rosso, Blu, Verde e Giallo. Durante la creazione della regola, le opzioni (pulsanti di scelta) vengono recuperate automaticamente e rese disponibili al creatore della regola come segue:

![Più valori visualizza le opzioni](assets/multivaluefcdisplaysoptions.png)

Durante la scrittura di una regola When, puoi attivare l&#39;azione Cancella valore di. Cancella valore dell&#39;azione cancella il valore dell&#39;oggetto specificato. L&#39;opzione Clear Value (Cancella valore) nell&#39;istruzione When consente di creare condizioni complesse con più campi. È possibile aggiungere l&#39;istruzione Else per aggiungere ulteriori condizioni

![Cancella valore di](assets/clearvalueof.png)

>[!NOTE]
>
> Quando il tipo di regola supporta solo istruzioni then-else a livello singolo.

#### Più campi consentiti in [!UICONTROL When] {#allowed-multiple-fields}

Nella condizione **When** è possibile aggiungere altri campi oltre al campo a cui viene applicata la regola.

Ad esempio, utilizzando il tipo di regola When, è possibile valutare una condizione su diversi oggetti modulo ed eseguire l&#39;azione:

Quando:

(Oggetto A Condizione 1)

E/O

(Oggetto B Condizione 2)

Quindi, effettua le seguenti operazioni:

Azione 1 sull&#39;oggetto A

_

![Campi multipli consentiti in Quando](/help/forms/assets/allowed-multiple-field-when.png)

##### Considerazioni durante l&#39;utilizzo di Campi multipli consentiti nella funzione Quando condizione

* Assicurarsi che il [componente core sia impostato sulla versione 3.0.14 o successiva](https://github.com/adobe/aem-core-forms-components) per utilizzare questa funzione nell&#39;regola editor.
* Se le regole vengono applicate a campi diversi all&#39;interno della condizione Quando, il regola attiva lineare se viene modificato solo uno di tali campi.


<!--
* It is not possible to add multiple fields in the When condition while applying rules to a button.

##### To enable Allowed Multiple fields in When condition feature

Allowed Multiple fields in When condition feature is disabled by default. To enable this feature, add a custom property at the template policy:

1. Open the corresponding template associated with an Adaptive Form in the template editor.
1. Select the existing policy as **formcontainer-policy**.
1. Navigate to the **[!UICONTROL Structure]**  view and, from the **[!UICONTROL Allowed Components]** list, open the **[!UICONTROL Adaptive Forms Container]** policy.
1. Go to the **[!UICONTROL Custom Properties]** tab and to add a custom property, click **[!UICONTROL Add]**.
1. Specify the **Group Name** of your choice. For example, in our case, we added the group name as **allowedfeature**.
1. Add the **key** and **value** pair as follows:
   * key: fd:changeEventBehaviour
   * value: deps
1. Click **[!UICONTROL Done]**. -->

Se nella funzione Condizione When sono presenti più campi consentiti, segui i passaggi di risoluzione dei problemi descritti di seguito.

1. Apri il modulo in modalità di modifica.
1. Apri il browser Contenuti e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fai clic su Fine e salva di nuovo la finestra di dialogo.

**[!UICONTROL Nascondi]** Nasconde l&#39;oggetto specificato.

**[!UICONTROL Mostra]** mostra l&#39;oggetto specificato.

**[!UICONTROL Abilita]** Abilita l&#39;oggetto specificato.

**[!UICONTROL Disabilita]** Disabilita l&#39;oggetto specificato.

**[!UICONTROL Richiama servizio]** Richiama un servizio configurato in un modello dati modulo (FDM). Quando scegli l’operazione Richiama servizio, viene visualizzato un campo. Quando tocca il campo, vengono visualizzati tutti i servizi configurati in tutti i modelli di dati del modulo (FDM) nell&#39;istanza [!DNL Experience Manager]. Quando si sceglie un servizio Modello dati modulo, vengono visualizzati più campi in cui è possibile mappare gli oggetti modulo con i parametri di input e output per il servizio specificato. Vedi regola di esempio per richiamare i servizi del modello dati modulo (FDM).

Oltre al servizio Modello dati modulo, è possibile specificare un URL WSDL diretto per richiamare un servizio Web. Tuttavia, un servizio di modello dati modulo presenta molti vantaggi e l’approccio consigliato per richiamare un servizio.

Per ulteriori informazioni sulla configurazione dei servizi nel modello dati modulo, vedere [[!DNL Experience Manager Forms] Integrazione dati](data-integration.md).

**[!UICONTROL Imposta il valore di]** Calcola e imposta il valore dell&#39;oggetto specificato. È possibile impostare il valore dell&#39;oggetto su una stringa, il valore di un altro oggetto, il valore calcolato utilizzando un&#39;espressione matematica o una funzione, il valore di una proprietà di un oggetto o il valore di output di un servizio Form Data Model configurato. Quando si sceglie l&#39;opzione Servizio Web, vengono visualizzati tutti i servizi configurati in tutti i modelli di dati del modulo (FDM) nell&#39;istanza [!DNL Experience Manager]. Quando si sceglie un servizio Modello dati modulo, vengono visualizzati più campi in cui è possibile mappare gli oggetti modulo con i parametri di input e output per il servizio specificato.

Per ulteriori informazioni sulla configurazione dei servizi nel modello dati modulo, vedere [[!DNL Experience Manager Forms] Integrazione dati](data-integration.md).

Il tipo di regola **[!UICONTROL Imposta proprietà]** consente di impostare il valore di una proprietà dell&#39;oggetto specificato in base a un&#39;azione condizione. È possibile impostare la proprietà su una delle seguenti opzioni:
* visibile (booleano)
* label.value (Stringa)
* label.visible (booleano)
* description (String)
* abilitato (booleano)
* readOnly (booleano)
* obbligatorio (booleano)
* screenReaderText (stringa)
* valido (booleano)
* errorMessage (stringa)
* impostazione predefinita (numero, stringa, data)
* enumNames (Stringa[])
* chartType (String)

Ad esempio, consente di definire regole per visualizzare la casella di testo quando si fa clic su un pulsante. Per definire una regola è possibile utilizzare una funzione personalizzata, un oggetto modulo, una proprietà oggetto o un output di servizio.

![Imposta proprietà](assets/set_property_rule_new.png)

Per definire una regola basata su una funzione personalizzata, selezionare **[!UICONTROL Output funzione]** dall&#39;elenco a discesa e trascinare una funzione personalizzata dalla scheda **[!UICONTROL Funzioni]**. Se l&#39;azione della condizione viene soddisfatta, la casella di immissione testo diventa visibile.

Per definire una regola basata su un oggetto modulo, selezionare **[!UICONTROL Oggetto modulo]** dall&#39;elenco a discesa e trascinare un oggetto modulo dalla scheda **[!UICONTROL Oggetti modulo]**. Se l’azione della condizione viene soddisfatta, la casella di immissione testo diventa visibile nel modulo adattivo.

Una regola Imposta proprietà basata su una proprietà oggetto consente di rendere visibile la casella di input di testo in un modulo adattivo basato su un’altra proprietà oggetto inclusa nel modulo adattivo.

La figura seguente illustra un esempio di attivazione dinamica della casella di controllo in base al fatto che la casella di testo è nascosta o visualizzata in un modulo adattivo:

![Proprietà oggetto](assets/object_property_set_property_new.png)

**[!UICONTROL Cancella valore di]** Cancella il valore dell&#39;oggetto specificato.

**[!UICONTROL Imposta stato attivo]** Imposta lo stato attivo sull&#39;oggetto specificato.

**[!UICONTROL Invia modulo]** invia il modulo.

**[!UICONTROL Reimposta]** Reimposta il modulo o l&#39;oggetto specificato.

**[!UICONTROL Convalida]** convalida il modulo o l&#39;oggetto specificato.

**[!UICONTROL Aggiungi istanza]** Aggiunge un&#39;istanza del pannello o della riga di tabella ripetibile specificata.

**[!UICONTROL Rimuovi istanza]** Rimuove un&#39;istanza del pannello o della riga di tabella ripetibile specificata.

**[!UICONTROL Output funzione]** Definisce una regola basata su funzioni predefinite o personalizzate.

**[!UICONTROL Accedi a]** Consente di passare ad altri <!--Interactive Communications,--> Forms adattivi, ad altre risorse quali immagini o frammenti di documenti o a un URL esterno. <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

**[!UICONTROL Evento di invio]** Attiva azioni o comportamenti specifici in base a condizioni o eventi predefiniti.


### [!UICONTROL Imposta valore di] {#set-value-of}

Il tipo di regola **[!UICONTROL Imposta valore di]** consente di impostare il valore di un oggetto modulo a seconda che la condizione specificata sia soddisfatta o meno. Il valore può essere impostato sul valore di un altro oggetto, una stringa letterale, un valore derivato da un&#39;espressione matematica o una funzione, un valore di una proprietà di un altro oggetto o l&#39;output di un servizio del modello di dati modulo. Analogamente, è possibile verificare la presenza di una condizione su un componente, una stringa, una proprietà o valori derivati da una funzione o un&#39;espressione matematica.

Il tipo di regola **Imposta valore di** non è disponibile per tutti gli oggetti modulo, ad esempio pannelli e pulsanti della barra degli strumenti. Una regola Set Value Of standard ha la seguente struttura:

Impostare il valore dell&#39;oggetto A su:

(stringa ABC) O
(proprietà oggetto X dell&#39;oggetto C) O
(valore da una funzione) O
(valore da un&#39;espressione matematica) O
(valore di output di un servizio di modello dati);

Quando (facoltativo):

(Condizione 1 E Condizione 2 E Condizione 3) è VERO;

L&#39;esempio seguente seleziona il valore di `Question2` come `True` e imposta il valore di `Result` come `correct`.

![Set-value-web-service](assets/set-value-web-service.png)

Esempio di regola Imposta valore tramite il servizio Modello dati modulo.

### [!UICONTROL Mostra] {#show}

Utilizzando il tipo di regola **[!UICONTROL Mostra]**, è possibile scrivere una regola per mostrare o nascondere un oggetto modulo in base al soddisfacimento o meno di una condizione. Il tipo di regola Show attiva anche l&#39;azione Nascondi nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola Show tipica è strutturata come segue:

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

### [!UICONTROL Nascondi] {#hide}

Analogamente al tipo di regola Mostra, è possibile utilizzare il tipo di regola **[!UICONTROL Nascondi]** per mostrare o nascondere un oggetto modulo in base al soddisfacimento o meno di una condizione. Il tipo di regola Nascondi attiva anche l&#39;azione Mostra se la condizione non è soddisfatta o restituisce `False`.

Una tipica regola Nascondi è strutturata come segue:

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

### [!UICONTROL Abilita] {#enable}

Il tipo di regola **[!UICONTROL Enable]** consente di abilitare o disabilitare un oggetto modulo in base al soddisfacimento o meno di una condizione. Il tipo di regola Enable attiva anche l&#39;azione Disable nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola di abilitazione tipica è strutturata come segue:

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

### [!UICONTROL Disattiva] {#disable}

Analogamente al tipo di regola Abilita, il tipo di regola **[!UICONTROL Disabilita]** consente di abilitare o disabilitare un oggetto modulo a seconda che una condizione sia soddisfatta o meno. Il tipo di regola Disable attiva anche l&#39;azione Enable nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola di Disattivazione tipica è strutturata come segue:

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### [!UICONTROL Convalida] {#validate}

Il tipo di regola **[!UICONTROL Convalida]** convalida il valore in un campo utilizzando un&#39;espressione. È ad esempio possibile scrivere un&#39;espressione per verificare che la casella di testo per specificare il nome non contenga caratteri o numeri speciali.

Una regola di convalida tipica è strutturata come segue:

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Se il valore specificato non è conforme alla regola di convalida, è possibile visualizzare un messaggio di convalida per l&#39;utente. È possibile specificare il messaggio nel campo **[!UICONTROL Messaggio di convalida dello script]** nelle proprietà del componente nella barra laterale.

![Convalida script](assets/script-validation.png)

<!--
### [!UICONTROL Set Options Of] {#setoptionsof}

The **[!UICONTROL Set Options Of]** rule type enables you to define rules to add check boxes dynamically to the Adaptive Form. You can use a Form Data Model or a custom function to define the rule.

To define a rule based on a custom function, select **[!UICONTROL Function Output]** from the drop-down list, and drag-and-drop a custom function from the **[!UICONTROL Functions]** tab. The number of checkboxes defined in the custom function are added to the Adaptive Form.

![Custom Functions](assets/custom_functions_set_options_new.png)

To create a custom function, see [custom functions in rule editor](#custom-functions).

To define a rule based on a form data model:

1. Select **[!UICONTROL Service Output]** from the drop-down list.
1. Select the data model object.
1. Select a data model object property from the **[!UICONTROL Display Value]** drop-down list. The number of checkboxes in the Adaptive Form is derived from the number of instances defined for that property in the database.
1. Select a data model object property from the **[!UICONTROL Save Value]** drop-down list.

![FDM set options](assets/fdm_set_options_new.png) -->

## Interfaccia utente dell’editor di regole {#understanding-the-rule-editor-user-interface}

L’editor di regole fornisce un’interfaccia utente completa ma semplice per scrivere e gestire le regole. Puoi avviare l’interfaccia utente dell’editor di regole da un modulo adattivo in modalità di authoring.

Per avviare l’interfaccia utente dell’editor di regole:

1. Apri un modulo adattivo in modalità di authoring.
1. Selezionare l&#39;oggetto modulo per il quale si desidera scrivere una regola e nella barra degli strumenti del componente selezionare ![edit-rules](assets/edit-rules-icon.svg). Viene visualizzata l’interfaccia utente dell’editor di regole.

   ![create-rules](assets/create-rules.png)

   Tutte le regole esistenti sugli oggetti modulo selezionati sono elencate in questa visualizzazione. Per informazioni sulla gestione delle regole esistenti, vedere [Gestire le regole](rule-editor.md#p-manage-rules-p).

1. Seleziona **[!UICONTROL Crea]** per scrivere una nuova regola. L’editor visivo dell’interfaccia utente dell’editor di regole si apre per impostazione predefinita quando si avvia l’editor di regole la prima volta.

   ![Interfaccia utente editor regole](assets/rule-editor-ui.png)

Esaminiamo in dettaglio ogni componente dell’interfaccia utente dell’editor di regole.

### A. Visualizzazione delle regole dei componenti {#a-component-rule-display}

Visualizza il titolo dell&#39;oggetto modulo adattivo tramite il quale è stato avviato l&#39;editor di regole e il tipo di regola attualmente selezionato. Nell’esempio precedente, l’editor di regole viene avviato da un oggetto Modulo adattivo denominato Domanda 1 e il tipo di regola selezionato è Quando.

### B. Oggetti e funzioni del modulo {#b-form-objects-and-functions-br}

Il riquadro a sinistra nell&#39;interfaccia utente dell&#39;editor di regole include due schede: **[!UICONTROL Oggetti Forms]** e **[!UICONTROL Funzioni]**.

La scheda Oggetti modulo mostra una vista gerarchica di tutti gli oggetti contenuti nel modulo adattivo. Visualizza il titolo e il tipo degli oggetti. Durante la scrittura di una regola, è possibile trascinare gli oggetti modulo nell’editor di regole. Quando si trascina un oggetto o una funzione in un segnaposto durante la creazione o la modifica di una regola, il segnaposto assume automaticamente il tipo di valore appropriato.

Gli oggetti modulo a cui sono applicate una o più regole valide sono contrassegnati da un punto verde. Se una delle regole applicate a un oggetto modulo non è valida, l&#39;oggetto modulo viene contrassegnato con un punto giallo.

La scheda Funzioni include un set di funzioni incorporate, ad esempio Somma di, Min di, Max di, Media di, Numero di e Convalida modulo. È possibile utilizzare queste funzioni per calcolare i valori nei pannelli e nelle righe di tabella ripetibili e utilizzarli nelle istruzioni di azione e condizione durante la scrittura delle regole. Tuttavia, puoi anche creare funzioni personalizzate.

Nella figura sono illustrate alcune delle funzioni elencate di seguito:

![Scheda Funzioni](assets/functions.png)

>[!NOTE]
>
>È possibile eseguire la ricerca di testo su oggetti e funzioni, nomi e titoli nelle schede Oggetti e funzioni di Forms.

Nell&#39;albero sinistro degli oggetti modulo è possibile selezionare gli oggetti modulo per visualizzare le regole applicate a ciascuno degli oggetti. Non solo è possibile spostarsi tra le regole dei vari oggetti modulo, ma è anche possibile copiare e incollare le regole tra gli oggetti modulo. Per ulteriori informazioni, vedere [Copiare e incollare le regole](rule-editor.md#p-copy-paste-rules-p).

### C. Attivazione/disattivazione di funzioni e oggetti modulo {#c-form-objects-and-functions-toggle-br}

Quando viene toccato, questo pulsante attiva o disattiva il riquadro delle funzioni e degli oggetti del modulo.

### D. Editor di regole visive {#visual-rule-editor}

L’editor di regole visive è l’area in cui si scrivono le regole nella modalità editor visivo dell’interfaccia utente dell’editor di regole. Ti consente di selezionare un tipo di regola e di definire di conseguenza condizioni e azioni. Quando si definiscono condizioni e azioni in una regola, è possibile trascinare gli oggetti modulo e le funzioni dal riquadro Oggetti modulo e funzioni.

Per ulteriori informazioni sull&#39;utilizzo di regola editor visivi, vedere [Scrivere regole](rule-editor.md#p-write-rules-p).
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and conversely, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E. Pulsanti Fine e Annulla {#done-and-cancel-buttons}

Il **[!UICONTROL pulsante Fine]** viene utilizzato per salvare un regola. È possibile salvare un regola incompleto. Tuttavia, gli incompleti vengono non valido e non vengono eseguiti. Le regole salvate in un oggetto modulo vengono elencate quando si lanciare la regola editor successiva dallo stesso oggetto modulo. È possibile gestire regole esistenti in questa visualizzazione. Per ulteriori informazioni, vedere [Gestire le regole](rule-editor.md#p-manage-rules-p).

Il pulsante **[!UICONTROL Annulla]** elimina le modifiche apportate a una regola e chiude l&#39;editor di regole.

## Scrivi regole {#write-rules}

È possibile scrivere regole utilizzando l&#39;editor di regole visive <!-- or the code editor. When you launch the rule editor the first time, it opens in the visual editor mode. You can switch to the code editor mode and write rules. However, if you write or modify a rule in code editor, you cannot switch to the visual editor for that rule unless you clear the code editor. When you launch the rule editor next time, it opens in the mode that you used last to create rule. -->

Vediamo innanzitutto come scrivere regole utilizzando l’editor visivo.

### Utilizzo dell’editor visivo {#using-visual-editor}

Comprendiamo come creare una regola nell’editor visivo utilizzando il seguente modulo di esempio.

![Crea-regola-esempio](assets/create-rule-example.png)

La sezione Requisiti del prestito nell&#39;esempio di modulo di domanda di prestito richiede ai richiedenti di specificare il loro stato civile, lo stipendio e, in caso di matrimonio, lo stipendio del coniuge. In base agli input dell’utente, la regola calcola l’importo di idoneità al prestito e viene visualizzata nel campo Idoneità al prestito. Per implementare lo scenario, applica le seguenti regole:

* Il campo Stipendio coniuge viene visualizzato solo quando lo stato civile è sposato.
* L’importo di ammissibilità al prestito è pari al 50% dello stipendio totale.

Per scrivere le regole, effettua le seguenti operazioni:

1. Innanzitutto, scrivi la regola per controllare la visibilità del campo Stipendio coniuge in base all’opzione selezionata dall’utente per il pulsante di opzione Stato civile.

   Apri il modulo di richiesta di prestito in modalità di creazione. Selezionare il componente **[!UICONTROL Stato civile]** e selezionare ![edit-rules](assets/edit-rules-icon.svg). Quindi, seleziona **[!UICONTROL Crea]** per avviare l&#39;editor di regole.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1-cc.png)

   Quando si avvia l&#39;editor di regole, la regola When è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, Stato civile) da cui è stato avviato l&#39;editor di regole è specificato nell&#39;istruzione When.

   Sebbene non sia possibile modificare l&#39;oggetto selezionato, è possibile utilizzare l&#39;elenco a discesa delle regole, come illustrato di seguito, per selezionare un altro tipo di regola. Se desideri creare una regola su un altro oggetto, seleziona Annulla per uscire dall’editor di regole e riavviarlo dall’oggetto modulo desiderato.

1. Seleziona l&#39;elenco a discesa **[!UICONTROL Seleziona stato]** e seleziona **[!UICONTROL è uguale a]**. Viene visualizzato il campo **[!UICONTROL Enter a String]**.

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2-cc.png)

<!--  In the Marital Status radio button, **[!UICONTROL Married]** and **[!UICONTROL Single]** options are assigned **0** and **1** values, respectively. You can verify assigned values in the Title tab of the Edit radio button dialog as shown below.

   ![Radio button values from rule editor](assets/radio-button-values.png)-->

1. Nel campo **[!UICONTROL Immettere una stringa]** nella regola, selezionare **Sposato** dal menu a discesa.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4-cc.png)

   La condizione è stata definita come `When Marital Status is equal to Married`. Quindi, definisci l’azione da eseguire se questa condizione è True.

1. Nell&#39;istruzione Then, selezionare **[!UICONTROL Show]** dal menu a discesa **[!UICONTROL Select Action]**.

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5-cc.png)

1. Trascina il campo **[!UICONTROL Stipendio coniuge]** dalla scheda Oggetti modulo del campo **[!UICONTROL Rilascia oggetto o seleziona qui]**. In alternativa, selezionare il campo **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** e selezionare il campo **[!UICONTROL Stipendio coniuge]** dal menu a comparsa, che elenca tutti gli oggetti modulo nel modulo.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6-cc.png)

   Quindi, definisci l’azione da eseguire se questa condizione è False.
1. Fare clic su **[!UICONTROL Aggiungi sezione Else]** per aggiungere un&#39;altra condizione per il campo **[!UICONTROL Stipendio coniuge]**, nel caso in cui si selezioni Stato civile come singolo.

   ![when-else](assets/when-else.png)


1. Nell&#39;istruzione Else, selezionare **[!UICONTROL Nascondi]** dal menu a discesa **[!UICONTROL Seleziona azione]**.
   ![when-else](assets/when-else-1.png)

1. Trascina il campo **[!UICONTROL Stipendio coniuge]** dalla scheda Oggetti modulo del campo **[!UICONTROL Rilascia oggetto o seleziona qui]**. In alternativa, selezionare il campo **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** e selezionare il campo **[!UICONTROL Stipendio coniuge]** dal menu a comparsa, che elenca tutti gli oggetti modulo nel modulo.
   ![when-else](assets/when-else-2.png)

   La regola viene visualizzata come segue nell’editor di regole.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7-cc.png)



1. Seleziona **[!UICONTROL Fine]** per salvare la regola.

<!--
1. Repeat steps 1 through 5 to define another rule to hide the Spouse Salary field if the marital Status is Single. The rule appears as follows in the rule editor.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8-cc.png) -->

>[!NOTE]
>
> In alternativa, è possibile scrivere una regola Mostra nel campo Stipendio coniuge, anziché una regola Quando nel campo Stato civile, per implementare lo stesso comportamento.

![write-rules-visual-editor-9](assets/write-rules-visual-editor-9-cc.png)

1. Scrivere quindi una regola per calcolare l&#39;importo dell&#39;idoneità al prestito, che corrisponde al 50% dello stipendio totale, e visualizzarlo nel campo Idoneità al prestito. Per ottenere questo risultato, crea **[!UICONTROL Imposta il valore di]** regole nel campo Idoneità al prestito.

   In modalità creazione, seleziona il campo **[!UICONTROL Idoneità prestito]** e seleziona ![modifica-regole](assets/edit-rules-icon.svg). Quindi, seleziona **[!UICONTROL Crea]** per avviare l&#39;editor di regole.

1. Selezionare **[!UICONTROL Imposta valore di]** regola dal menu a discesa delle regole.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10-cc.png)

1. Seleziona **[!UICONTROL Seleziona opzione]** e seleziona **[!UICONTROL Espressione matematica]**. Viene aperto un campo per scrivere espressioni matematiche.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11-cc.png)

1. Nel campo espressione:

   * Seleziona o trascina dalla scheda Oggetto Forms il campo **[!UICONTROL Stipendio]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   * Seleziona **[!UICONTROL Plus]** dal campo **[!UICONTROL Seleziona operatore]**.

   * Seleziona o trascina dalla scheda Oggetto Forms il campo **[!UICONTROL Stipendio coniuge]** nell&#39;altro campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. Quindi, seleziona nell&#39;area evidenziata intorno al campo espressione e seleziona **[!UICONTROL Estendi espressione]**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13-cc.png)

   Nel campo dell&#39;espressione estesa, selezionare **[!UICONTROL diviso per]** dal **[!UICONTROL campo Seleziona operatore]** e **[!UICONTROL Numero]** dal **[!UICONTROL campo Seleziona opzione]** . Quindi, specificare **[!UICONTROL 2]** nel campo numero.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14-cc.png)

   >[!NOTE]
   >
   >È possibile creare espressioni complesse utilizzando componenti, funzioni, espressioni matematiche e valori di proprietà dal campo Seleziona opzione.

   Quindi, crea una condizione, che quando restituisce True, l’espressione viene eseguita.

1. Selezionare **[!UICONTROL Aggiungi condizione]** per aggiungere un&#39;istruzione When.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15-cc.png)

   Nell&#39;istruzione When:

   * Seleziona o trascina dalla scheda Oggetto Forms il campo **[!UICONTROL Stato civile]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   * Selezionare **[!UICONTROL è uguale a]** dal campo **[!UICONTROL Seleziona operatore]**.

   * Seleziona Stringa nell&#39;altro **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo e specifica **[!UICONTROL Sposato]** nel campo **[!UICONTROL Immetti una stringa]**.

   La regola viene infine visualizzata come segue nell’editor di regole.  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16-cc.png)

1. Seleziona **[!UICONTROL Fine]**. Salva la regola.

1. Ripetere i passaggi da 7 a 14 per definire un&#39;altra regola per calcolare l&#39;idoneità al prestito se lo stato civile è Single. La regola viene visualizzata come segue nell’editor di regole.

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17-cc.png)

In alternativa, è possibile utilizzare la regola Imposta valore di per calcolare l&#39;idoneità al prestito nella regola Quando creata per mostrare-nascondere il campo Stipendio coniuge. La regola combinata risultante quando Stato civile è Singolo viene visualizzata come segue nell’editor delle regole.

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18-cc.png)

È possibile scrivere una regola combinata per controllare la visibilità del campo Stipendio coniuge e calcolare l&#39;idoneità al prestito quando lo stato civile è Sposato utilizzando la condizione Else.

![write-rules-visual-editor-19](assets/write-rules-visual-editor-19-cc.png)


<!-- ### Using code editor {#using-code-editor}

Users added to the forms-power-users group can use code editor. The rule editor auto generates the JavaScript code for any rule you create using visual editor. You can switch from visual editor to the code editor to view the generated code. However, if you modify the rule code in the code editor, you cannot switch back to the visual editor. If you prefer writing rules in code editor rather than visual editor, you can write rules afresh in the code editor. The visual-code editors switcher helps you switch between the two modes.

The code editor JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. These expressions return values of certain types. For the complete list of Adaptive Forms classes, events, objects, and public APIs, see [JavaScript Library API reference for Adaptive Forms](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

For more information about guidelines to write rules in the code editor, see [Adaptive Form Expressions](adaptive-form-expressions.md).

While writing JavaScript code in the rule editor, the following visual cues help you with the structure and syntax:

* Syntax highlights

* Auto Indentation

* Hints and suggestions for Form objects, functions, and their properties

* Auto completion of form component names and common JavaScript functions

![javascriptruleeditor](assets/javascriptruleeditor.png)
-->

#### Funzioni personalizzate nell’editor di regole {#custom-functions}

Oltre alle funzioni predefinite, come *Somma di*, elencate in **Output funzioni**, è possibile utilizzare anche funzioni personalizzate nell&#39;editor di regole. L’editor di regole supporta la sintassi JavaScript ECMAScript 2019 per gli script e le funzioni personalizzate. Per istruzioni sulla creazione di funzioni personalizzate, consulta l&#39;articolo [Funzioni personalizzate in Forms adattivo](/help/forms/create-and-use-custom-functions.md).

<!--

Ensure that the function you write is accompanied by the `jsdoc` above it. Adaptive Form supports the various [JavaScript annotations for custom functions](/help/forms/create-and-use-custom-functions.md#js-annotations).

For more information, see [jsdoc.app](https://jsdoc.app/).

Accompanying `jsdoc` is required:

* If you want custom configuration and description
* Because there are multiple ways to declare a function in `JavaScript,` and comments let you keep a track of the functions.

Supported `jsdoc` tags:

* **Private**
  Syntax: `@private`
  A private function is not included as a custom function.

* **Name**
  Syntax: `@name funcName <Function Name>`
  Alternatively `,` you can use: `@function funcName <Function Name>` **or** `@func` `funcName <Function Name>`.
  `funcName` is the name of the function (no spaces allowed).
  `<Function Name>` is the display name of the function.

* **Parameter**
  Syntax: `@param {type} name <Parameter Description>`
  Alternatively, you can use: `@argument` `{type} name <Parameter Description>` **or** `@arg` `{type}` `name <Parameter Description>`.
  Shows parameters used by the function. A function can have multiple parameter tags, one tag for each parameter in the order of occurrence.
  `{type}` represents parameter type. Allowed parameter types are:

    1. string
    2. number
    3. boolean
    4. scope
    5. string[]
    6. number[]
    7. boolean[]
    8. date
    9. date[]
    10. array
    11. object

   `scope` refers to a special globals object which is provided by forms runtime. It must be the last parameter and is not be visible to the user in the rule editor. You can use scope to access readable form and field proxy object to read properties, event which triggered the rule and a set of functions to manipulate the form.

   `object` type is used to pass readable field object in parameter to a custom function instead of passing the value.

   All parameter types are categorized under one of the above. None is not supported. Ensure that you select one of the types above. Types are not case-sensitive. Spaces are not allowed in the parameter name.  Parameter description can have multiple words.

* **Optional Parameter**
Syntax: `@param {type=} name <Parameter Description>` 
Alternatively, you can use: `@param {type} [name] <Parameter Description>`
By default all parameters are mandatory. You can mark a parameter optional by adding `=` in type of the parameter or by putting param name in square brackets.
   
   For example, let us declare `Input1` as optional parameter:
    * `@param {type=} Input1`
    * `@param {type} [Input1]`

* **Return Type**
  Syntax: `@return {type}`
  Alternatively, you can use `@returns {type}`.
  Adds information about the function, such as its objective.
  {type} represents the return type of the function. Allowed return types are:

    1. string
    2. number
    3. boolean
    4. string[]
    5. number[]
    6. boolean[]
    7. date
    8. date[]
    9. array
    10. object

  All other return types are categorized under one of the above. None is not supported. Ensure that you select one of the types above. Return types are not case-sensitive.

**Adding a custom function**

For example, you want to add a custom function which calculates area of a square. Side length is the user input to the custom function, which is accepted using a numeric box in your form. The calculated output is displayed in another numeric box in your form. To add a custom function, you have to first create a client library, and then add it to the CRX repository.

To create a client library and add it in the CRX repository, perform the following steps:

1. Create a client library. For more information, see [Using Client-Side Libraries](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).
2. In CRXDE, add a property `categories`with string type value as `customfunction` to the `clientlib` folder.

   >[!NOTE]
   >
   >`customfunction`is an example category. You can choose any name for the category you create in the `clientlib`folder.

After you have added your client library in the CRX repository, use it in your Adaptive Form. It lets you use your custom function as a rule in your form. To add the client library in your Adaptive Form, perform the following steps:

1. Open your form in edit mode.
   To open a form in edit mode, select a form and select **[!UICONTROL Open]**.
1. In the edit mode, select a component, then select ![field-level](assets/select_parent_icon.svg) &gt; **[!UICONTROL Adaptive Form Container]**, and then select ![cmppr](assets/configure-icon.svg).
1. In the sidebar, under Name of Client Library, add your client library. ( `customfunction` in the example.)

   ![Adding the custom function client library](assets/clientlib.png)

1. Select the input numeric box, and select ![edit-rules](assets/edit-rules-icon.svg) to open the rule editor.
1. Select **[!UICONTROL Create Rule]**. Using options shown below, create a rule to save the squared value of the input in the Output field of your form.

   [![Using custom functions to create a rule](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)
  
1. Select **[!UICONTROL Done]**. Your custom function is added.

   >[!NOTE]
   >
   > To invoke a form data model from rule editor using custom functions, [see here](/help/forms/using-form-data-model.md#invoke-services-in-adaptive-forms-using-rules-invoke-services). 

#### Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>Ensure that you use `jsdoc` for every custom function. Although `jsdoc`comments are encouraged, include an empty `jsdoc`comment to mark your function as custom function. It enables default handling of your custom function.
-->

## Gestisci regole {#manage-rules}

Tutte le regole esistenti in un oggetto modulo vengono elencate quando si seleziona l&#39;oggetto e si seleziona ![edit-rules1](assets/edit-rules-icon.svg). Puoi visualizzare il titolo e un’anteprima del riepilogo delle regole. Inoltre, l’interfaccia utente consente di espandere e visualizzare il riepilogo completo delle regole, modificarne l’ordine, modificarne le regole ed eliminarle.

![Regole elenco](assets/list-rules-cc.png)

Puoi eseguire le seguenti azioni sulle regole:

* **Espandi/comprimi**: la colonna Contenuto nell&#39;elenco delle regole visualizza il contenuto della regola. Se l&#39;intero contenuto della regola non è visibile nella visualizzazione predefinita, selezionare ![expand-rule-content](assets/Smock_ChevronDown.svg) per espanderlo.

* **Riordina**: tutte le nuove regole create sono sovrapposte nella parte inferiore dell&#39;elenco di regole. Le regole vengono eseguite dall&#39;alto verso il basso. La regola in alto viene eseguita per prima, seguita da altre regole dello stesso tipo. Ad esempio, se disponi di regole When, Show, Enable e When rispettivamente in prima, seconda, terza e quarta posizione dall&#39;alto, la regola When nella parte superiore viene eseguita per prima seguita dalla regola When nella quarta posizione. Vengono quindi eseguite le regole Mostra e Abilita.
È possibile modificare l&#39;ordine di una regola toccando ![sort-rules](assets/sort-rules.svg) o trascinandola nell&#39;ordine desiderato nell&#39;elenco.

* **Modifica**: per modificare una regola, selezionare la casella di controllo accanto al titolo della regola. Vengono visualizzate le opzioni per modificare ed eliminare la regola. Seleziona **[!UICONTROL Modifica]** per aprire la regola selezionata nell&#39;editor regole <!-- in visual  or code editor mode depending on the mode used to create the rule -->.

* **Elimina**: per eliminare una regola, selezionarla e selezionare **[!UICONTROL Elimina]**.

* **Attiva/Disattiva**: quando è necessario sospendere temporaneamente l&#39;utilizzo di una regola, è possibile selezionare una o più regole e selezionare **[!UICONTROL Disattiva]** nella barra degli strumenti Azioni per disattivarle. Se una regola è disabilitata, non viene eseguita in fase di esecuzione. Per abilitare una regola disabilitata, selezionala e seleziona Abilita nella barra degli strumenti delle azioni. La colonna di stato della regola indica se la regola è abilitata o disabilitata.

![Disabilita regola](assets/disablerule-cc.png)

## Regole di copia e incolla {#copy-paste-rules}

Per risparmiare tempo, puoi copiare e incollare una regola da un campo ad altri campi simili.

Per copiare e incollare le regole, effettuare le seguenti operazioni:

1. Selezionare l&#39;oggetto modulo da cui si desidera copiare una regola e nella barra degli strumenti del componente selezionare ![modifica regola](assets/edit-rules-icon.svg). Viene visualizzata l’interfaccia utente dell’editor di regole con l’oggetto modulo selezionato e le regole esistenti.

   ![copia regola](assets/copyrule.png)

   Per informazioni sulla gestione delle regole esistenti, vedere [Gestire le regole](rule-editor.md#p-manage-rules-p).

1. Selezionare la casella di controllo accanto al titolo della regola per visualizzare le opzioni per la gestione della regola. Seleziona **[!UICONTROL Copia]**.

   ![copyrule2](assets/copyrule2.png)

1. Selezionare un altro oggetto modulo in cui incollare la regola e selezionare **[!UICONTROL Incolla]**. Inoltre, puoi modificare la regola per apportarvi modifiche.

   >[!NOTE]
   >
   >È possibile incollare una regola in un altro oggetto modulo solo se tale oggetto supporta l&#39;evento della regola copiata. Ad esempio, un pulsante supporta l’evento clic. È possibile incollare una regola con un evento clic su un pulsante ma non su una casella di controllo.

1. Seleziona **[!UICONTROL Fine]** per salvare la regola.

## Espressioni nidificate {#nestedexpressions}

L’editor di regole consente di utilizzare più operatori AND e OR per creare regole nidificate. È possibile combinare più operatori AND e OR nelle regole.

Di seguito è riportato un esempio di regola nidificata che visualizza un messaggio per l’utente sull’idoneità per la custodia di un bambino quando vengono soddisfatte le condizioni richieste.

![Espressione complessa](assets/complexexpression.png)

Puoi anche trascinare le condizioni all’interno di una regola per modificarla. Seleziona e passa il puntatore del mouse sull&#39;handle ( ![handle](assets/drag-handle.svg)) prima di una condizione. Una volta che il puntatore diventa il simbolo della mano, come mostrato di seguito, trascinare la condizione in un punto qualsiasi della regola. La struttura regola cambia.

![Trascinamento della selezione](assets/drag-and-drop.png)

## Condizioni dell&#39;espressione data {#dateexpression}

La regola editor consente di utilizzare i confronti di date per creare condizioni.

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

## Regole di esempio {#example}

### Richiama servizio modello dati modulo {#invoke}

Si consideri un servizio Web `GetInterestRates` che accetta come input l&#39;importo del prestito, la locazione e il punteggio di credito del richiedente e restituisce un piano di prestito che include l&#39;importo dell&#39;IME e il tasso di interesse. È possibile creare un modello dati modulo (FDM) utilizzando il servizio Web come origine dati. Gli oggetti modello dati e un servizio `get` vengono aggiunti al modello di modulo. Il servizio viene visualizzato nella scheda Servizi del modello dati del modulo (FDM). Quindi, crea un modulo adattivo che includa i campi dagli oggetti modello dati per acquisire gli input dell’utente per l’importo del prestito, la durata e il punteggio di credito. Aggiungi un pulsante che attiva il servizio web per recuperare i dettagli del piano. L’output viene compilato nei campi appropriati.

La regola seguente mostra come configurare l’azione Richiama servizio per eseguire lo scenario di esempio.

![Esempio-invoke-services](assets/example-invoke-services.png)

>[!NOTE]
>
>Se l’input è di tipo array, i campi che supportano gli array sono visibili nella sezione a discesa Output.

### Attivazione di più azioni tramite la regola When {#triggering-multiple-actions-using-the-when-rule}

In un modulo di richiesta di prestito, si desidera stabilire se il richiedente è un cliente esistente o meno. In base alle informazioni fornite dall&#39;utente, il campo ID cliente deve essere visualizzato o nascosto. Inoltre, se l’utente è un cliente esistente, imposta il campo ID cliente come elemento attivo. Il modulo di richiesta di prestito presenta le seguenti componenti:

* Un pulsante di scelta, **[!UICONTROL Sei già un cliente del Geometrixx?]**, che fornisce [!UICONTROL Sì] e [!UICONTROL No] opzioni. Il valore per Sì è **0** e No è **1**.

* Un campo di testo, **[!UICONTROL ID cliente Geometrixx]**, per specificare l&#39;ID cliente.

Quando scrivi una regola When sul pulsante di scelta per implementare questo comportamento, la regola viene visualizzata come segue nell’editor di regole visive.

![Esempio-regola-quando](assets/when-rule-example.png)

Regola nell’editor visivo

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

Regola nell’editor visivo

<!-- he rule appears as follows in the code editor.

![example-function-output-code](assets/example-function-output-code.png)

Rule in the code editor -->

### Convalida di un valore di campo tramite espressione {#validating-a-field-value-using-expression}

Nel modulo dell&#39;ordine di acquisto illustrato nell&#39;esempio precedente, si desidera impedire agli utenti di ordinare più di una quantità di qualsiasi prodotto il cui prezzo sia superiore a 10000. Per eseguire questa convalida, è possibile scrivere una regola di convalida come illustrato di seguito.

![Esempio-convalida](assets/example-validate.png)

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->
