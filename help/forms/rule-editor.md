---
title: Come si utilizza l’editor di regole di Forms adattivo?
description: L’editor di regole di Forms adattivo consente di aggiungere un comportamento dinamico e di creare una logica complessa nei moduli senza codificare o scrivere script. Introduzione alla comprensione di una regola e delle linee guida per la scelta di un costrutto regola. Ulteriori informazioni sui tipi di operatori e sugli eventi disponibili nell’editor di regole.
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
exl-id: 6fd38e9e-435e-415f-83f6-3be177738c00
source-git-commit: e64e15c9096f837daa7fff5c64b8394736297579
workflow-type: tm+mt
source-wordcount: '6346'
ht-degree: 0%

---

# Aggiungere regole a un modulo adattivo {#adaptive-forms-rule-editor}

## Panoramica {#overview}

La funzione dell’editor di regole consente agli utenti aziendali e agli sviluppatori di Forms di scrivere regole sugli oggetti Adaptive Form. Queste regole definiscono le azioni da attivare sugli oggetti modulo in base a condizioni preimpostate, input dell&#39;utente e azioni dell&#39;utente sul modulo. Consente di semplificare ulteriormente l’esperienza di compilazione dei moduli, garantendo precisione e velocità.

L’editor di regole fornisce un’interfaccia utente intuitiva e semplificata per scrivere regole. L’editor di regole offre un editor visivo per tutti gli utenti.<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. --> Alcune delle azioni chiave che è possibile eseguire sugli oggetti Modulo adattivo utilizzando le regole sono:

* Mostrare o nascondere un oggetto
* Attivare o disattivare un oggetto
* Imposta un valore per un oggetto
* Convalidare il valore di un oggetto
* Eseguire funzioni per calcolare il valore di un oggetto
* Richiama un servizio del modello dati modulo ed esegui un’operazione
* Impostare la proprietà di un oggetto

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Gli utenti aggiunti al gruppo forms-power-users possono creare script e modificare quelli esistenti. Utenti in [!DNL forms-users] Il gruppo può utilizzare gli script ma non crearli o modificarli.

## Informazioni su una regola {#understanding-a-rule}

Una regola è una combinazione di azioni e condizioni. Nell’editor delle regole, le azioni includono attività quali nascondere, mostrare, abilitare, disabilitare o calcolare il valore di un oggetto in un modulo. Le condizioni sono espressioni booleane che vengono valutate eseguendo controlli e operazioni sullo stato, sul valore o sulla proprietà di un oggetto modulo. Le azioni vengono eseguite in base al valore ( `True` o `False`) restituita valutando una condizione.

L’editor di regole fornisce un set di tipi di regole predefiniti, ad esempio Quando, Mostra, Nascondi, Abilita, Disabilita, Imposta valore di e Convalida, per facilitare la scrittura delle regole. Ogni tipo di regola ti consente di definire condizioni e azioni in una regola. Il documento spiega ulteriormente ogni tipo di regola nei dettagli.

Una regola segue in genere uno dei seguenti costrutti:

**Condizione-Azione** In questo costrutto, una regola definisce prima una condizione seguita da un’azione da attivare. Il costrutto è paragonabile all&#39;istruzione if-then nei linguaggi di programmazione.

Nell’editor delle regole, il **Quando** tipo di regola applica il costrutto condizione-azione.

**Action-Condition** In questo costrutto, una regola definisce prima un’azione da attivare seguita da condizioni per la valutazione. Un’altra variante di questo costrutto è action-condition-alternate action, che definisce anche un’azione alternativa da attivare se la condizione restituisce False.

I tipi di regola Mostra, Nascondi, Abilita, Disabilita, Imposta valore di e Convalida nell&#39;editor di regole applicano il costrutto regola della condizione azione. Per impostazione predefinita, l&#39;azione alternativa per Mostra è Nascondi e per Abilita è Disabilita e viceversa. Non è possibile modificare l&#39;azione alternativa predefinita.

>[!NOTE]
>
>I tipi di regole disponibili, incluse le condizioni e le azioni definite nell&#39;editor di regole, dipendono anche dal tipo di oggetto modulo su cui si sta creando una regola. Nell&#39;editor delle regole vengono visualizzati solo i tipi di regole e le opzioni validi per la scrittura di istruzioni di condizione e azione per un particolare tipo di oggetto modulo. Ad esempio, per un oggetto pannello non vengono visualizzati i tipi di regole Convalida, Imposta valore di, Abilita e Disabilita.

Per ulteriori informazioni sui tipi di regole disponibili nell’editor di regole, consulta [Tipi di regole disponibili nell’editor di regole](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### Linee guida per la scelta di un costrutto regola {#guidelines-for-choosing-a-rule-construct}

Sebbene sia possibile ottenere la maggior parte dei casi d’uso utilizzando qualsiasi costrutto di regola, di seguito sono riportate alcune linee guida per scegliere un costrutto rispetto a un altro. Per ulteriori informazioni sulle regole disponibili nell’editor di regole, consulta [Tipi di regole disponibili nell’editor di regole](rule-editor.md#p-available-rule-types-in-rule-editor-p).

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

* **È uguale a**
* **Non è uguale a**
* **Inizia con**
* **Termina con**
* **Contiene**
* **È vuoto**
* **Non è vuoto**
* **Ha selezionato:** Restituisce true quando l’utente seleziona una particolare opzione per una casella di controllo, un elenco a discesa o un pulsante di scelta.
* **È inizializzato (evento):** Restituisce true quando viene eseguito il rendering di un oggetto modulo nel browser.
* **Viene modificato (evento):** Restituisce true quando l&#39;utente modifica il valore immesso o l&#39;opzione selezionata per un oggetto modulo.
* **Navigazione (evento):** Restituisce true quando l&#39;utente fa clic su un oggetto di spostamento. Gli oggetti di navigazione vengono utilizzati per spostarsi tra i pannelli.
* **Completamento fase (evento):** Restituisce true al completamento di un passaggio di una regola.
* **Invio riuscito (evento):** Restituisce true in caso di invio corretto di dati a un modello dati del modulo.
* **Errore nell’invio (evento):**  Restituisce true in caso di invio non riuscito di dati a un modello dati del modulo.

## Tipi di regole disponibili nell’editor di regole {#available-rule-types-in-rule-editor}

L’editor di regole fornisce un set di tipi di regole predefiniti che è possibile utilizzare per scrivere regole. Esaminiamo in dettaglio ogni tipo di regola. Per ulteriori informazioni sulla scrittura di regole nell’editor di regole, consulta [Scrivi regole](rule-editor.md#p-write-rules-p).

### [!UICONTROL Quando  ] {#whenruletype}

Il **[!UICONTROL Quando]** il tipo di regola segue **condizione-azione-azione-azione alternativa** costrutto della regola o, a volte, solo **condizione-azione** costruzione. In questo tipo di regola, devi innanzitutto specificare una condizione per la valutazione seguita da un&#39;azione da attivare se la condizione viene soddisfatta ( `True`). Quando si utilizza il tipo di regola When, è possibile utilizzare più operatori AND e OR per creare [espressioni nidificate](#nestedexpressions).

Utilizzando il tipo di regola When, è possibile valutare una condizione in un oggetto modulo ed eseguire azioni su uno o più oggetti.

In parole semplici, una regola When tipica è strutturata come segue:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

Azione 2 sull&#39;oggetto B; e Azione 3 sull&#39;oggetto C;

_

Quando si dispone di un componente con più valori, ad esempio pulsanti di scelta o elenco, durante la creazione di una regola per tale componente le opzioni vengono recuperate e rese disponibili automaticamente al creatore della regola. Non è necessario digitare nuovamente i valori delle opzioni.

Ad esempio, un elenco include quattro opzioni: Rosso, Blu, Verde e Giallo. Durante la creazione della regola, le opzioni (pulsanti di scelta) vengono recuperate automaticamente e rese disponibili al creatore della regola come segue:

![Opzioni per la visualizzazione di più valori](assets/multivaluefcdisplaysoptions.png)

Durante la scrittura di una regola When, puoi attivare l&#39;azione Cancella valore di. Cancella valore dell&#39;azione cancella il valore dell&#39;oggetto specificato. L&#39;opzione Clear Value (Cancella valore) nell&#39;istruzione When consente di creare condizioni complesse con più campi.

![Cancella valore](assets/clearvalueof.png)

**[!UICONTROL Nascondi]** Nasconde l&#39;oggetto specificato.

**[!UICONTROL Spettacolo]** Mostra l&#39;oggetto specificato.

**[!UICONTROL Abilita]** Attiva l&#39;oggetto specificato.

**[!UICONTROL Disattiva]** Disattiva l&#39;oggetto specificato.

**[!UICONTROL Richiama servizio]** Richiama un servizio configurato in un modello dati modulo. Quando scegli l’operazione Richiama servizio, viene visualizzato un campo. Quando tocca il campo, vengono visualizzati tutti i servizi configurati in tutti i modelli di dati del modulo sul [!DNL Experience Manager] dell&#39;istanza. Quando si sceglie un servizio Modello dati modulo, vengono visualizzati più campi in cui è possibile mappare gli oggetti modulo con i parametri di input e output per il servizio specificato. Vedi regola di esempio per richiamare i servizi del modello dati modulo.

Oltre al servizio Modello dati modulo, è possibile specificare un URL WSDL diretto per richiamare un servizio Web. Tuttavia, un servizio di modello dati modulo presenta molti vantaggi e l’approccio consigliato per richiamare un servizio.

Per ulteriori informazioni sulla configurazione dei servizi nel modello dati modulo, vedi [[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md).

**[!UICONTROL Imposta valore di]** Calcola e imposta il valore dell&#39;oggetto specificato. È possibile impostare il valore dell&#39;oggetto su una stringa, il valore di un altro oggetto, il valore calcolato utilizzando un&#39;espressione matematica o una funzione, il valore di una proprietà di un oggetto o il valore di output di un servizio Form Data Model configurato. Quando si sceglie l&#39;opzione Servizio Web, vengono visualizzati tutti i servizi configurati in tutti i modelli di dati del modulo sul [!DNL Experience Manager] dell&#39;istanza. Quando si sceglie un servizio Modello dati modulo, vengono visualizzati più campi in cui è possibile mappare gli oggetti modulo con i parametri di input e output per il servizio specificato.

Per ulteriori informazioni sulla configurazione dei servizi nel modello dati modulo, vedi [[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md).

Il **[!UICONTROL Imposta proprietà]** tipo di regola consente di impostare il valore di una proprietà dell&#39;oggetto specificato in base a un&#39;azione condizione.

Consente di definire regole per aggiungere caselle di controllo in modo dinamico al modulo adattivo. È possibile utilizzare una funzione personalizzata, un oggetto modulo o una proprietà oggetto per definire una regola.

![Imposta proprietà](assets/set_property_rule_new.png)

Per definire una regola basata su una funzione personalizzata, seleziona **[!UICONTROL Uscita funzione]** dall&#39;elenco a discesa e trascinare una funzione personalizzata dall&#39;elenco **[!UICONTROL Funzioni]** scheda. Se l’azione della condizione viene soddisfatta, il numero di caselle di controllo definite nella funzione personalizzata viene aggiunto al modulo adattivo.

Per definire una regola basata su un oggetto modulo, selezionare **[!UICONTROL Oggetto modulo]** dall&#39;elenco a discesa e trascinare un oggetto modulo dal **[!UICONTROL Oggetti modulo]** scheda. Se l’azione della condizione viene soddisfatta, il numero di caselle di controllo definite nell’oggetto modulo viene aggiunto al modulo adattivo.

Una regola Imposta proprietà basata su una proprietà oggetto consente di aggiungere il numero di caselle di controllo in un modulo adattivo basato su un’altra proprietà oggetto inclusa nel modulo adattivo.

La figura seguente illustra un esempio di aggiunta dinamica di caselle di controllo in base al numero di elenchi a discesa nel modulo adattivo:

![Proprietà oggetto](assets/object_property_set_property_new.png)

**[!UICONTROL Cancella valore di]** Cancella il valore dell&#39;oggetto specificato.

**[!UICONTROL Imposta Fuoco]** Imposta lo stato attivo sull&#39;oggetto specificato.

**[!UICONTROL Salva modulo]** Salva il modulo.

**[!UICONTROL Invia Forms]** Invia il modulo.

**[!UICONTROL Reimposta modulo]** Reimposta il modulo.

**[!UICONTROL Convalida modulo]** Convalida il modulo.

**[!UICONTROL Aggiungi istanza]** Aggiunge un&#39;istanza del pannello o della riga di tabella ripetibile specificata.

**[!UICONTROL Rimuovi istanza]** Rimuove un&#39;istanza del pannello o della riga di tabella ripetibile specificata.

**[!UICONTROL Accedi a]** Passa ad altro <!--Interactive Communications,--> Forms adattivo, altre risorse come immagini o frammenti di documento o un URL esterno. <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

### [!UICONTROL Imposta valore di] {#set-value-of}

Il **[!UICONTROL Imposta valore di]** tipo di regola consente di impostare il valore di un oggetto modulo a seconda che la condizione specificata sia soddisfatta o meno. Il valore può essere impostato sul valore di un altro oggetto, una stringa letterale, un valore derivato da un&#39;espressione matematica o una funzione, un valore di una proprietà di un altro oggetto o l&#39;output di un servizio del modello di dati modulo. Analogamente, è possibile verificare la presenza di una condizione su un componente, una stringa, una proprietà o valori derivati da una funzione o un&#39;espressione matematica.

Il **Imposta valore di** il tipo di regola non è disponibile per tutti gli oggetti modulo, ad esempio pannelli e pulsanti della barra degli strumenti. Una regola Set Value Of standard ha la seguente struttura:

Imposta il valore dell&#39;oggetto A su:

(stringa ABC) OR (proprietà dell&#39;oggetto X dell&#39;oggetto C) OR (valore di una funzione) OR (valore di un&#39;espressione matematica) OR (valore di output di un servizio di modello dati o di un servizio Web);

Quando (facoltativo):

(Condizione 1 AND Condizione 2 AND Condizione 3) è TRUE;

L’esempio seguente utilizza il valore in `dependentid` come input e imposta il valore del campo `Relation` campo all&#39;output del `Relation` argomento della `getDependent` Servizio modello dati modulo.

![Set-value-web-service](assets/set-value-web-service.png)

Esempio di regola Imposta valore tramite il servizio Modello dati modulo

>[!NOTE]
>
>Inoltre, è possibile utilizzare Imposta valore della regola per compilare tutti i valori in un componente elenco a discesa dall’output di un servizio Modello dati modulo o di un servizio web. Verificare tuttavia che l&#39;argomento di output scelto sia di tipo matrice. Tutti i valori restituiti in un array diventano disponibili nell’elenco a discesa specificato.

### [!UICONTROL Mostra] {#show}

Utilizzo di **[!UICONTROL Spettacolo]** tipo di regola, è possibile scrivere una regola per mostrare o nascondere un oggetto modulo a seconda che una condizione sia soddisfatta o meno. Il tipo di regola Mostra attiva anche l’azione Nascondi se la condizione non viene soddisfatta o restituisce `False`.

Una regola Show tipica è strutturata come segue:

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

### [!UICONTROL Nascondi] {#hide}

Simile al tipo di regola Mostra, puoi utilizzare **[!UICONTROL Nascondi]** tipo di regola per mostrare o nascondere un oggetto modulo in base al soddisfacimento o meno di una condizione. Il tipo di regola Nascondi attiva anche l&#39;azione Mostra nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una tipica regola Nascondi è strutturata come segue:

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

### [!UICONTROL Attiva] {#enable}

Il **[!UICONTROL Abilita]** tipo di regola consente di abilitare o disabilitare un oggetto modulo a seconda che una condizione sia soddisfatta o meno. Il tipo di regola Enable attiva anche l&#39;azione Disable nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola di abilitazione tipica è strutturata come segue:

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

### [!UICONTROL Disattiva] {#disable}

Simile al tipo di regola Abilita, il **[!UICONTROL Disattiva]** tipo di regola consente di abilitare o disabilitare un oggetto modulo a seconda che una condizione sia soddisfatta o meno. Il tipo di regola Disable attiva anche l’azione Enable nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola di Disattivazione tipica è strutturata come segue:

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### [!UICONTROL Convalida] {#validate}

Il **[!UICONTROL Convalida]** tipo di regola convalida il valore in un campo utilizzando un&#39;espressione. È ad esempio possibile scrivere un&#39;espressione per verificare che la casella di testo per specificare il nome non contenga caratteri o numeri speciali.

Una regola di convalida tipica è strutturata come segue:

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Se il valore specificato non è conforme alla regola di convalida, è possibile visualizzare un messaggio di convalida. Puoi specificare il messaggio nel **[!UICONTROL Messaggio di convalida script]** nelle proprietà del componente nella barra laterale.

![Convalida script](assets/script-validation.png)

### [!UICONTROL Imposta opzioni di] {#setoptionsof}

Il **[!UICONTROL Imposta opzioni di]** tipo di regola consente di definire regole per aggiungere caselle di controllo in modo dinamico al modulo adattivo. Puoi utilizzare un modello dati modulo o una funzione personalizzata per definire la regola.

Per definire una regola basata su una funzione personalizzata, seleziona **[!UICONTROL Uscita funzione]** dall&#39;elenco a discesa e trascinare una funzione personalizzata dall&#39;elenco **[!UICONTROL Funzioni]** scheda. Al modulo adattivo viene aggiunto il numero di caselle di controllo definite nella funzione personalizzata.

![Funzioni personalizzate](assets/custom_functions_set_options_new.png)

Per creare una funzione personalizzata, vedi [funzioni personalizzate nell’editor di regole](#custom-functions).

Per definire una regola basata su un modello dati modulo:

1. Seleziona **[!UICONTROL Output del servizio]** dall’elenco a discesa.
1. Seleziona l’oggetto modello dati.
1. Selezionare una proprietà dell’oggetto modello dati dal menu **[!UICONTROL Visualizza valore]** elenco a discesa. Il numero di caselle di controllo nel modulo adattivo è derivato dal numero di istanze definite per tale proprietà nel database.
1. Selezionare una proprietà dell’oggetto modello dati dal menu **[!UICONTROL Salva valore]** elenco a discesa.

![Opzioni set FDM](assets/fdm_set_options_new.png)

## Interfaccia utente dell’editor di regole {#understanding-the-rule-editor-user-interface}

L’editor di regole fornisce un’interfaccia utente completa ma semplice per scrivere e gestire le regole. Puoi avviare l’interfaccia utente dell’editor di regole da un modulo adattivo in modalità di authoring.

Per avviare l’interfaccia utente dell’editor di regole:

1. Apri un modulo adattivo in modalità di authoring.
1. Toccare l’oggetto modulo per il quale si desidera scrivere una regola, quindi nella barra degli strumenti del componente toccare ![edit-rules](assets/edit-rules-icon.svg). Viene visualizzata l’interfaccia utente dell’editor di regole.

   ![create-rules](assets/create-rules.png)

   Tutte le regole esistenti sugli oggetti modulo selezionati sono elencate in questa visualizzazione. Per informazioni sulla gestione delle regole esistenti, consulta [Gestisci regole](rule-editor.md#p-manage-rules-p).

1. Tocca **[!UICONTROL Crea]** per scrivere una nuova regola. L’editor visivo dell’interfaccia utente dell’editor di regole si apre per impostazione predefinita quando si avvia l’editor di regole la prima volta.

   ![Interfaccia utente dell’editor delle regole](assets/rule-editor-ui.png)

Esaminiamo in dettaglio ogni componente dell’interfaccia utente dell’editor di regole.

### A. Visualizzazione delle regole dei componenti {#a-component-rule-display}

Visualizza il titolo dell&#39;oggetto modulo adattivo tramite il quale è stato avviato l&#39;editor di regole e il tipo di regola attualmente selezionato. Nell’esempio precedente, l’editor di regole viene avviato da un oggetto Modulo adattivo denominato Stipendio e il tipo di regola selezionato è Quando.

### B. Oggetti e funzioni del modulo {#b-form-objects-and-functions-br}

Il riquadro a sinistra nell’interfaccia utente dell’editor di regole include due schede: **[!UICONTROL Oggetti Forms]** e **[!UICONTROL Funzioni]**.

La scheda Oggetti modulo mostra una vista gerarchica di tutti gli oggetti contenuti nel modulo adattivo. Visualizza il titolo e il tipo degli oggetti. Durante la scrittura di una regola, è possibile trascinare gli oggetti modulo nell’editor di regole. Quando si trascina un oggetto o una funzione in un segnaposto durante la creazione o la modifica di una regola, il segnaposto assume automaticamente il tipo di valore appropriato.

Gli oggetti modulo a cui sono applicate una o più regole valide sono contrassegnati da un punto verde. Se una delle regole applicate a un oggetto modulo non è valida, l&#39;oggetto modulo viene contrassegnato con un punto giallo.

La scheda Funzioni include un set di funzioni incorporate, ad esempio Somma di, Min di, Max di, Media di, Numero di e Convalida modulo. È possibile utilizzare queste funzioni per calcolare i valori nei pannelli e nelle righe di tabella ripetibili e utilizzarli nelle istruzioni di azione e condizione durante la scrittura delle regole. Tuttavia, puoi creare [funzioni personalizzate](#custom-functions) anche.

![Scheda Funzioni](assets/functions.png)

>[!NOTE]
>
>È possibile eseguire la ricerca di testo su oggetti e funzioni, nomi e titoli nelle schede Oggetti e funzioni di Forms.

Nell&#39;albero sinistro degli oggetti modulo è possibile toccare gli oggetti modulo per visualizzare le regole applicate a ciascuno degli oggetti. Non solo è possibile spostarsi tra le regole dei vari oggetti modulo, ma è anche possibile copiare e incollare le regole tra gli oggetti modulo. Per ulteriori informazioni, consulta [Regole di copia e incolla](rule-editor.md#p-copy-paste-rules-p).

### C. Attivazione/disattivazione di funzioni e oggetti modulo {#c-form-objects-and-functions-toggle-br}

Quando viene toccato, questo pulsante attiva o disattiva il riquadro delle funzioni e degli oggetti del modulo.

### D. Editor di regole visive {#visual-rule-editor}

L’editor di regole visive è l’area in cui si scrivono le regole nella modalità editor visivo dell’interfaccia utente dell’editor di regole. Consente di selezionare un tipo di regola e di conseguenza di definire condizioni e azioni. Quando si definiscono condizioni e azioni in una regola, è possibile trascinare gli oggetti modulo e le funzioni dal riquadro Oggetti modulo e funzioni.

Per ulteriori informazioni sull’utilizzo dell’editor di regole visive, consulta [Scrivi regole](rule-editor.md#p-write-rules-p).
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and vice versa, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E. Tasti Done e cancel {#done-and-cancel-buttons}

Il **[!UICONTROL Fine]** per salvare una regola. È possibile salvare una regola incompleta. Tuttavia, i dati incompleti non sono validi e non vengono eseguiti. Le regole salvate su un oggetto modulo vengono elencate quando si avvia l’editor di regole la prossima volta dallo stesso oggetto modulo. Puoi gestire le regole esistenti in tale vista. Per ulteriori informazioni, consulta [Gestisci regole](rule-editor.md#p-manage-rules-p).

Il **[!UICONTROL Annulla]** il pulsante elimina tutte le modifiche apportate a una regola e chiude l’editor di regole.

## Scrivi regole {#write-rules}

Puoi scrivere regole utilizzando l’editor di regole visive &lt;!>— o l&#39;editor di codice>. Quando avvii l’editor di regole la prima volta, si apre in modalità editor visivo. Puoi passare alla modalità editor di codice e scrivere regole. Tuttavia, se scrivi o modifichi una regola nell’editor di codice, non puoi passare all’editor visivo per tale regola a meno che non annulli l’editor di codice. La prossima volta che avvii l’editor di regole, questo si apre nella modalità utilizzata per ultima per creare la regola.

Vediamo innanzitutto come scrivere regole utilizzando l’editor visivo.

### Utilizzo dell’editor visivo {#using-visual-editor}

Comprendiamo come creare una regola nell’editor visivo utilizzando il seguente modulo di esempio.

![Create-rule-example](assets/create-rule-example.png)

La sezione Requisiti del prestito nell&#39;esempio di modulo di domanda di prestito richiede ai richiedenti di specificare il loro stato civile, lo stipendio e, in caso di matrimonio, lo stipendio del coniuge. In base agli input dell’utente, la regola calcola l’importo di idoneità al prestito e viene visualizzata nel campo Idoneità al prestito. Per implementare lo scenario, applica le seguenti regole:

* Il campo Stipendio coniuge viene visualizzato solo quando lo stato civile è sposato.
* L’importo di ammissibilità al prestito è pari al 50% dello stipendio totale.

Per scrivere le regole, effettua le seguenti operazioni:

1. Innanzitutto, scrivi la regola per controllare la visibilità del campo Stipendio coniuge in base all’opzione selezionata dall’utente per il pulsante di opzione Stato civile.

   Apri il modulo di richiesta di prestito in modalità di creazione. Tocca il **[!UICONTROL Stato civile]** componente e tocca ![edit-rules](assets/edit-rules-icon.svg). Quindi tocca **[!UICONTROL Crea]** per avviare l’editor di regole.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   Quando si avvia l&#39;editor di regole, la regola When è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, Stato civile) da cui è stato avviato l&#39;editor di regole è specificato nell&#39;istruzione When.

   Sebbene non sia possibile modificare l&#39;oggetto selezionato, è possibile utilizzare l&#39;elenco a discesa delle regole, come illustrato di seguito, per selezionare un altro tipo di regola. Se desideri creare una regola su un altro oggetto, tocca Annulla per uscire dall’editor di regole e riavviarlo dall’oggetto modulo desiderato.

1. Tocca **[!UICONTROL Seleziona stato]** a discesa e selezionare **[!UICONTROL è uguale a]**. Il **[!UICONTROL Inserisci una stringa]** viene visualizzato.

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   Nel pulsante di opzione Stato civile, **[!UICONTROL Coniugato]** e **[!UICONTROL Singolo]** opzioni assegnate **0** e **1** rispettivamente. È possibile verificare i valori assegnati nella scheda Titolo della finestra di dialogo Modifica pulsante di opzione, come illustrato di seguito.

   ![Valori dei pulsanti di scelta dall’editor di regole](assets/radio-button-values.png)

1. In **[!UICONTROL Inserisci una stringa]** nella regola, specifica **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   La condizione è stata definita come `When Marital Status is equal to Married`. Quindi, definisci l’azione da eseguire se questa condizione è True.

1. Nell&#39;istruzione Then, selezionare **[!UICONTROL Spettacolo]** dal **[!UICONTROL Seleziona azione]** a discesa.

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. Trascina la selezione **[!UICONTROL Stipendio coniuge]** dalla scheda Oggetti modulo nella **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo. In alternativa, tocca il **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** e selezionare il **[!UICONTROL Stipendio coniuge]** dal menu a comparsa, che elenca tutti gli oggetti modulo del modulo.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   La regola viene visualizzata come segue nell’editor di regole.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

1. Tocca **[!UICONTROL Fine]** per salvare la regola.

1. Ripetere i passaggi da 1 a 5 per definire un&#39;altra regola per nascondere il campo Stipendio coniuge se lo stato civile è Singolo. La regola viene visualizzata come segue nell’editor di regole.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >In alternativa, è possibile scrivere una regola Mostra nel campo Stipendio coniuge, anziché due regole Quando nel campo Stato civile, per implementare lo stesso comportamento.

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. Scrivere quindi una regola per calcolare l&#39;importo dell&#39;idoneità al prestito, che corrisponde al 50% dello stipendio totale, e visualizzarlo nel campo Idoneità al prestito. Per ottenere questo risultato, crea **[!UICONTROL Imposta valore di]** regole sul campo Ammissibilità al prestito.

   In modalità authoring, tocca il **[!UICONTROL Ammissibilità al prestito]** campo e tocco ![edit-rules](assets/edit-rules-icon.svg). Quindi tocca **[!UICONTROL Crea]** per avviare l’editor di regole.

1. Seleziona **[!UICONTROL Imposta valore di]** regola dal menu a discesa regola.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. Tocca **[!UICONTROL Seleziona opzione]** e seleziona **[!UICONTROL Espressione matematica]**. Viene aperto un campo per scrivere espressioni matematiche.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. Nel campo espressione:

   * Seleziona o trascina dalla scheda Oggetto Forms il **[!UICONTROL Salario]** campo nel primo **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo.

   * Seleziona **[!UICONTROL Più]** dal **[!UICONTROL Seleziona operatore]** campo.

   * Seleziona o trascina dalla scheda Oggetto Forms il **[!UICONTROL Stipendio coniuge]** campo nell&#39;altro **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo.

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. Quindi tocca nell’area evidenziata intorno al campo dell’espressione e tocca **[!UICONTROL Estendi estensione]**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   Nel campo espressione estesa, seleziona **[!UICONTROL diviso per]** dal **[!UICONTROL Seleziona operatore]** campo e **[!UICONTROL Numero]** dal **[!UICONTROL Seleziona opzione]** campo. Quindi, specifica **[!UICONTROL 2]** nel campo numerico.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >È possibile creare espressioni complesse utilizzando componenti, funzioni, espressioni matematiche e valori di proprietà dal campo Seleziona opzione.

   Quindi, crea una condizione, che quando restituisce True, l’espressione viene eseguita.

1. Tocca **[!UICONTROL Aggiungi condizione]** per aggiungere un&#39;istruzione When.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   Nell&#39;istruzione When:

   * Seleziona o trascina dalla scheda Oggetto Forms il **[!UICONTROL Stato civile]** campo nel primo **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo.

   * Seleziona **[!UICONTROL è uguale a]** dal **[!UICONTROL Seleziona operatore]** campo.

   * Seleziona stringa nell’altro **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** e specificare **[!UICONTROL Coniugato]** nel **[!UICONTROL Inserisci una stringa]** campo.

   La regola viene infine visualizzata come segue nell’editor di regole.  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

1. Toccate **[!UICONTROL Chiudi]**. Salva la regola.

1. Ripetere i passaggi da 7 a 14 per definire un&#39;altra regola per calcolare l&#39;idoneità al prestito se lo stato civile è Single. La regola viene visualizzata come segue nell’editor di regole.

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>In alternativa, è possibile utilizzare la regola Imposta valore di per calcolare l&#39;idoneità al prestito nella regola Quando creata per mostrare-nascondere il campo Stipendio coniuge. La regola combinata risultante quando Stato civile è Singolo viene visualizzata come segue nell’editor delle regole.
>
>Analogamente, è possibile scrivere una regola combinata per controllare la visibilità del campo Stipendio coniuge e calcolare l&#39;idoneità al prestito quando lo stato civile è Coniugato.

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

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

Oltre alle funzioni predefinite, come *Somma di* elencate in Output funzioni, è possibile scrivere funzioni personalizzate che sono spesso necessarie. Assicurati che la funzione che scrivi sia accompagnata dal `jsdoc` sopra di esso.

Accompagnamento `jsdoc` è obbligatorio:

* Se desideri una configurazione e una descrizione personalizzate
* Perché esistono diversi modi per dichiarare una funzione in `JavaScript,` I commenti e consentono di tenere traccia delle funzioni.

L’editor di regole supporta la sintassi JavaScript ES2015 per script e funzioni personalizzate.
Per ulteriori informazioni, consulta [jsdoc.app](https://jsdoc.app/).

Supportato `jsdoc` tag:

* **Privato**
Sintassi: una funzione privata non è inclusa come funzione personalizzata.`@private`
Una funzione privata non è inclusa come funzione personalizzata.

* **Nome**
Sintassi: in alternativa `@name funcName <Function Name>`
In alternativa `,` puoi utilizzare: `@function funcName <Function Name>` **o** `@func` `funcName <Function Name>`.
   `funcName` è il nome della funzione (non sono consentiti spazi).
   `<Function Name>` è il nome visualizzato della funzione.

* **Membro**
Sintassi: associa uno spazio dei nomi alla funzione.`@memberof namespace`
Associa uno spazio dei nomi alla funzione.

* **Parametro**
Sintassi: in alternativa, puoi utilizzare: `@param {type} name <Parameter Description>`
In alternativa, puoi utilizzare: `@argument` `{type} name <Parameter Description>` **o** `@arg` `{type}` `name <Parameter Description>`.
Mostra i parametri utilizzati dalla funzione. Una funzione può avere più tag di parametri, uno per ogni parametro in ordine di occorrenza.
   `{type}` rappresenta il tipo di parametro. I tipi di parametri consentiti sono:

   1. stringa
   1. numero
   1. booleano
   1. scope

   L’ambito fa riferimento ai campi di un modulo adattivo. Quando un modulo utilizza il caricamento lento, è possibile utilizzare `scope` per accedere ai relativi campi. È possibile accedere ai campi quando sono caricati o se sono contrassegnati come globali.

   Tutti i tipi di parametri sono classificati in una delle categorie precedenti. Nessuno non è supportato. Accertati di selezionare uno dei tipi riportati sopra. I tipi non fanno distinzione tra maiuscole e minuscole. Il parametro non può contenere spazi `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Tipo restituito**
Sintassi: in alternativa, puoi utilizzare `@return {type}`
In alternativa, puoi utilizzare `@returns {type}`.
Aggiunge informazioni sulla funzione, ad esempio l&#39;obiettivo.
{type} rappresenta il tipo restituito della funzione. I tipi restituiti consentiti sono:

   1. stringa
   1. numero
   1. booleano

   Tutti gli altri tipi di reso sono classificati in una delle categorie precedenti. Nessuno non è supportato. Accertati di selezionare uno dei tipi riportati sopra. I tipi restituiti non fanno distinzione tra maiuscole e minuscole.

   * **Questo**
Sintassi: 
`@this currentComponent`
   Utilizza @this per fare riferimento al componente Modulo adattivo su cui è scritta la regola.

   L’esempio seguente è basato sul valore del campo. Nell&#39;esempio seguente, la regola nasconde un campo nel modulo. Il `this` parte di `this.value` fa riferimento al componente modulo adattivo sottostante, su cui viene scritta la regola.

   ```
      /**
      * @function myTestFunction
      * @this currentComponent
      * @param {scope} scope in which code inside function will be executed.
      */
      myTestFunction = function (scope) {
         if(this.value == "O"){
               scope.age.visible = true;
         } else {
            scope.age.visible = false;
         }
      }
   ```

   >[!NOTE]
   >
   >I commenti prima della funzione personalizzata vengono utilizzati per il riepilogo. Il riepilogo può estendersi su più righe fino a quando non viene rilevato un tag. Limita le dimensioni a un singolo per una descrizione concisa nel generatore di regole.

**Aggiunta di una funzione personalizzata**

Ad esempio, si desidera aggiungere una funzione personalizzata che calcola l&#39;area di un quadrato. La lunghezza laterale è l’input dell’utente per la funzione personalizzata, che viene accettata utilizzando una casella numerica nel modulo. L&#39;output calcolato viene visualizzato in un&#39;altra casella numerica del modulo. Per aggiungere una funzione personalizzata, devi innanzitutto creare una libreria client e quindi aggiungerla all’archivio CRX.

Per creare una libreria client e aggiungerla all’archivio CRX, effettua le seguenti operazioni:

1. Creare un clientEffettuare le seguenti operazioni nella libreria. Per ulteriori informazioni, consulta [Utilizzo delle librerie lato client](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).
1. In CRXDE, aggiungi una proprietà `categories`con valore di tipo stringa come `customfunction` al `clientlib` cartella.

   >[!NOTE]
   >
   >`customfunction`è una categoria di esempio. È possibile scegliere qualsiasi nome per la categoria creata in `clientlib`cartella.

Dopo aver aggiunto la libreria client nell’archivio CRX, utilizzala nel modulo adattivo. Ti consente di utilizzare la funzione personalizzata come regola nel modulo. Per aggiungere la libreria client nel modulo adattivo, effettua le seguenti operazioni:

1. Apri il modulo in modalità di modifica.
Per aprire un modulo in modalità di modifica, seleziona un modulo e tocca **[!UICONTROL Apri]**.
1. In modalità di modifica, seleziona un componente, quindi tocca ![a livello di campo](assets/select_parent_icon.svg) > **[!UICONTROL Contenitore modulo adattivo]**, quindi tocca ![cmppr](assets/configure-icon.svg).
1. Nella barra laterale, in Nome della libreria client, aggiungi la libreria client. ( `customfunction` nell&#39;esempio.)

   ![Aggiunta della libreria client della funzione personalizzata](assets/clientlib.png)

1. Seleziona la casella numerica di input e tocca ![edit-rules](assets/edit-rules-icon.svg) per aprire l’editor di regole.
1. Tocca **[!UICONTROL Crea regola]**. Utilizzando le opzioni illustrate di seguito, creare una regola per salvare il valore al quadrato dell&#39;input nel campo Output del modulo.

   [![Utilizzo di funzioni personalizzate per creare una regola](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)

1. Toccate **[!UICONTROL Chiudi]**. Viene aggiunta la funzione personalizzata.

#### Tipi supportati da dichiarazione di funzione {#function-declaration-supported-types}

**Istruzione Function**

```javascript
function area(len) {
    return len*len;
}
```

Questa funzione è inclusa senza `jsdoc` commenti.

**Espressione funzione**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Espressione di funzione e istruzione**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Dichiarazione di funzione come variabile**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitazione: la funzione personalizzata seleziona solo la prima dichiarazione di funzione dall’elenco delle variabili, se presente insieme. È possibile utilizzare l&#39;espressione di funzione per ogni funzione dichiarata.

**Dichiarazione di funzione come oggetto**

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
>Assicurati di utilizzare `jsdoc` per ogni funzione personalizzata. Anche se `jsdoc`i commenti sono incoraggiati, includi un `jsdoc`commento per contrassegnare la funzione come funzione personalizzata. Consente la gestione predefinita della funzione personalizzata.

## Gestisci regole {#manage-rules}

Tutte le regole esistenti su un oggetto modulo vengono elencate quando tocchi l’oggetto e tocca ![edit-rules1](assets/edit-rules-icon.svg). Puoi visualizzare il titolo e un’anteprima del riepilogo delle regole. Inoltre, l’interfaccia utente consente di espandere e visualizzare il riepilogo completo delle regole, modificarne l’ordine, modificarne le regole ed eliminarle.

![Regole elenco](assets/list-rules.png)

Puoi eseguire le seguenti azioni sulle regole:

* **Espandi/Comprimi**: la colonna Contenuto nell’elenco delle regole visualizza il contenuto della regola. Se l’intero contenuto della regola non è visibile nella visualizzazione predefinita, tocca ![expand-rule-content](assets/Smock_ChevronDown.svg) per espanderlo.

* **Riordina**: tutte le nuove regole create vengono impilate nella parte inferiore dell’elenco di regole. Le regole vengono eseguite dall&#39;alto verso il basso. La regola in alto viene eseguita per prima, seguita da altre regole dello stesso tipo. Ad esempio, se disponi di regole When, Show, Enable e When rispettivamente in prima, seconda, terza e quarta posizione dall&#39;alto, la regola When nella parte superiore viene eseguita per prima seguita dalla regola When nella quarta posizione. Vengono quindi eseguite le regole Mostra e Abilita.
Per modificare l’ordine di una regola, tocca ![sort-rules](assets/sort-rules.svg) o trascinarlo nell&#39;ordine desiderato nell&#39;elenco.

* **Modifica**: per modificare una regola, seleziona la casella di controllo accanto al titolo della regola. Vengono visualizzate le opzioni per modificare ed eliminare la regola. Tocca **[!UICONTROL Modifica]** per aprire la regola selezionata nell’editor di regole <!-- in visual  or code editor mode depending on the mode used to create the rule -->.

* **Elimina**: per eliminare una regola, selezionala e tocca **[!UICONTROL Elimina]**.

* **Attiva/Disattiva**: quando devi sospendere temporaneamente l’utilizzo di una regola, puoi selezionare una o più regole e toccare **[!UICONTROL Disattiva]** nella barra degli strumenti Azioni per disattivarli. Se una regola è disabilitata, non viene eseguita in fase di esecuzione. Per abilitare una regola disabilitata, selezionala e tocca Abilita nella barra degli strumenti delle azioni. La colonna di stato della regola indica se la regola è abilitata o disabilitata.

![Disattiva regola](assets/disablerule.png)

## Regole di copia e incolla {#copy-paste-rules}

Per risparmiare tempo, puoi copiare e incollare una regola da un campo ad altri campi simili.

Per copiare e incollare le regole, effettuare le seguenti operazioni:

1. Tocca l’oggetto modulo da cui desideri copiare una regola, quindi nella barra degli strumenti del componente tocca ![modifica regola](assets/edit-rules-icon.svg). Viene visualizzata l’interfaccia utente dell’editor di regole con l’oggetto modulo selezionato e le regole esistenti.

   ![copia regola](assets/copyrule.png)

   Per informazioni sulla gestione delle regole esistenti, consulta [Gestisci regole](rule-editor.md#p-manage-rules-p).

1. Selezionare la casella di controllo accanto al titolo della regola per visualizzare le opzioni per la gestione della regola. Tocca **[!UICONTROL Copia]**.

   ![copyrule2](assets/copyrule2.png)

1. Seleziona un altro oggetto modulo in cui desideri incollare la regola e tocca **[!UICONTROL Incolla]**. Inoltre, puoi modificare la regola per apportarvi modifiche.

   >[!NOTE]
   >
   >È possibile incollare una regola in un altro oggetto modulo solo se tale oggetto supporta l&#39;evento della regola copiata. Ad esempio, un pulsante supporta l’evento clic. È possibile incollare una regola con un evento clic su un pulsante ma non su una casella di controllo.

1. Tocca **[!UICONTROL Fine]** per salvare la regola.

## Espressioni nidificate {#nestedexpressions}

L’editor di regole consente di utilizzare più operatori AND e OR per creare regole nidificate. È possibile combinare più operatori AND e OR nelle regole.

Di seguito è riportato un esempio di regola nidificata che visualizza un messaggio per l’utente sull’idoneità per la custodia di un bambino quando vengono soddisfatte le condizioni richieste.

![Espressione complessa](assets/complexexpression.png)

Puoi anche trascinare le condizioni all’interno di una regola per modificarla. Tocca e passa il puntatore sull&#39;handle ( ![maniglia](assets/drag-handle.svg)) prima di una condizione. Una volta che il puntatore si trasforma nel simbolo della mano, come illustrato di seguito, trascinare e rilasciare la condizione in qualsiasi punto della regola. La struttura della regola cambia.

![Trascinamento della selezione](assets/drag-and-drop.png)

## Condizioni di espressione data {#dateexpression}

L’editor di regole consente di utilizzare i confronti tra date per creare le condizioni.

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

![È richiesta un’altra bozza](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

## Regole di esempio {#example}

### Richiama servizio modello dati modulo {#invoke}

Considerare un servizio Web `GetInterestRates` che prende l&#39;importo del prestito, la locazione e il punteggio di credito del richiedente come input e restituisce un piano di prestito che include l&#39;importo dell&#39;IME e il tasso di interesse. Puoi creare un modello dati modulo utilizzando il servizio web come origine dati. Si aggiungono oggetti modello dati e un `get` servizio al modello di modulo. Il servizio viene visualizzato nella scheda Servizi del modello dati del modulo. Quindi, crea un modulo adattivo che includa i campi dagli oggetti modello dati per acquisire gli input dell’utente per l’importo del prestito, la durata e il punteggio di credito. Aggiungi un pulsante che attiva il servizio web per recuperare i dettagli del piano. L’output viene compilato nei campi appropriati.

La regola seguente mostra come configurare l’azione Richiama servizio per eseguire lo scenario di esempio.

![Example-invoke-services](assets/example-invoke-services.png)

Richiama il servizio del modello di dati modulo utilizzando la regola del modulo adattivo

### Attivazione di più azioni tramite la regola When {#triggering-multiple-actions-using-the-when-rule}

In un modulo di richiesta di prestito, si desidera stabilire se il richiedente è un cliente esistente o meno. In base alle informazioni fornite dall&#39;utente, il campo ID cliente deve essere visualizzato o nascosto. Inoltre, se l’utente è un cliente esistente, imposta il campo ID cliente come elemento attivo. Il modulo di richiesta di prestito presenta le seguenti componenti:

* Un pulsante di opzione, **[!UICONTROL Sei già un cliente del Geometrixx?]**, che fornisce [!UICONTROL Sì] e [!UICONTROL No] opzioni. Il valore di Sì è **0** e No è **1**.

* Un campo di testo, **[!UICONTROL ID cliente Geometrixx]**, per specificare l&#39;ID cliente.

Quando scrivi una regola When sul pulsante di scelta per implementare questo comportamento, la regola viene visualizzata come segue nell’editor di regole visive.

![When-rule-example](assets/when-rule-example.png)

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

**R.** Riga 1 **B.** Quantità **C.** Quantità totale

Ora si desidera aggiungere le quantità specificate nella colonna Quantità prodotto per tutti i prodotti e visualizzare la somma nella cella Quantità totale. È possibile ottenere tale somma scrivendo una regola Imposta valore di nella cella Quantità totale come illustrato di seguito.

![Esempio-funzione-output](assets/example-function-output.png)

Regola nell’editor visivo

<!-- he rule appears as follows in the code editor.

![example-function-output-code](assets/example-function-output-code.png)

Rule in the code editor -->

### Convalida di un valore di campo tramite espressione {#validating-a-field-value-using-expression}

Nel modulo dell&#39;ordine di acquisto illustrato nell&#39;esempio precedente, si desidera impedire agli utenti di ordinare più di una quantità di qualsiasi prodotto il cui prezzo sia superiore a 10000. Per eseguire questa convalida, è possibile scrivere una regola di convalida come illustrato di seguito.

![Esempio di convalida](assets/example-validate.png)

Regola nell’editor visivo

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->
