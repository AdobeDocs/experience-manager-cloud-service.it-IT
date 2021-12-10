---
title: Come si utilizza l'editor di regole di Forms adattivo?
description: L’editor di regole Forms adattivo consente di aggiungere comportamenti dinamici e creare logiche complesse nei moduli senza codice o script. Inizia a comprendere una regola e le linee guida per la scelta di un costrutto di regole. Ulteriori informazioni sui tipi di operatori ed eventi disponibili nell'editor delle regole.
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
exl-id: 6fd38e9e-435e-415f-83f6-3be177738c00
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '6340'
ht-degree: 0%

---

# Aggiungere regole a un modulo adattivo {#adaptive-forms-rule-editor}

## Panoramica {#overview}

La funzione editor di regole consente agli utenti aziendali e agli sviluppatori di Forms di scrivere regole sugli oggetti modulo adattivo. Queste regole definiscono le azioni da eseguire sugli oggetti modulo in base a condizioni preimpostate, input dell’utente e azioni dell’utente sul modulo. Consente di semplificare ulteriormente l’esperienza di compilazione dei moduli, garantendo precisione e velocità.

L’editor di regole fornisce un’interfaccia utente intuitiva e semplificata per scrivere regole. L’editor delle regole offre un editor visivo per tutti gli utenti.<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. --> Alcune delle azioni chiave che è possibile eseguire sugli oggetti modulo adattivo utilizzando le regole sono:

* Mostrare o nascondere un oggetto
* Attivare o disattivare un oggetto
* Impostare un valore per un oggetto
* Convalida il valore di un oggetto
* Esegui funzioni per calcolare il valore di un oggetto
* Richiamare un servizio del modello dati modulo ed eseguire un’operazione
* Imposta la proprietà di un oggetto

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Gli utenti aggiunti al gruppo forms-power-users possono creare script e modificare quelli esistenti. Utenti nel [!DNL forms-users] Il gruppo può utilizzare gli script ma non creare o modificare gli script.

## Informazioni su una regola {#understanding-a-rule}

Una regola è una combinazione di azioni e condizioni. Nell’editor delle regole, le azioni includono attività quali nascondere, mostrare, abilitare, disabilitare o calcolare il valore di un oggetto in un modulo. Le condizioni sono espressioni booleane valutate effettuando controlli e operazioni sullo stato, il valore o la proprietà di un oggetto modulo. Le azioni vengono eseguite in base al valore ( `True` o `False`) restituita valutando una condizione.

L&#39;editor di regole fornisce un set di tipi di regole predefiniti, ad esempio When, Show, Hide, Enable, Disable, Set Value Of e Validate per facilitare la scrittura di regole. Ogni tipo di regola ti consente di definire condizioni e azioni in una regola. Il documento spiega ulteriormente ogni tipo di regola in dettaglio.

Una regola segue in genere uno dei seguenti costrutti:

**Azione condizione** In questo costrutto, una regola definisce innanzitutto una condizione seguita da un&#39;azione da attivare. La costruzione è paragonabile all&#39;istruzione if-then nei linguaggi di programmazione.

Nell’editor delle regole, il **Quando** tipo di regola applica il costrutto condizione-azione.

**Action-Condition** In questo costrutto, una regola definisce innanzitutto un&#39;azione da attivare seguita da condizioni di valutazione. Un&#39;altra variante di questo costrutto è action-condition-alternate action, che definisce anche un&#39;azione alternativa da attivare se la condizione restituisce False.

I tipi di regole Mostra, Nascondi, Abilita, Disabilita, Imposta valore di e Convalida nell&#39;editor delle regole impongono il costrutto della regola della condizione azione. Per impostazione predefinita, l&#39;azione alternativa Mostra è Nascondi e per Abilita è Disabilita e viene eseguita in modo opposto. Non è possibile modificare l&#39;azione alternativa predefinita.

>[!NOTE]
>
>I tipi di regole disponibili, comprese le condizioni e le azioni definite nell&#39;editor di regole, dipendono anche dal tipo di oggetto modulo da cui si sta creando una regola. L’editor di regole visualizza solo tipi di regole e opzioni validi per la scrittura di istruzioni di condizioni e azioni per un particolare tipo di oggetto modulo. Ad esempio, non vengono visualizzati i tipi di regole Convalida, Imposta valore di, Abilita e Disabilita per un oggetto pannello.

Per ulteriori informazioni sui tipi di regole disponibili nell&#39;editor di regole, vedi [Tipi di regole disponibili nell’editor delle regole](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### Linee guida per la scelta di un costrutto di regole {#guidelines-for-choosing-a-rule-construct}

Sebbene sia possibile ottenere la maggior parte dei casi di utilizzo utilizzando qualsiasi costrutto di regole, di seguito sono riportate alcune linee guida per scegliere un costrutto più un altro. Per ulteriori informazioni sulle regole disponibili nell&#39;editor delle regole, vedi [Tipi di regole disponibili nell’editor delle regole](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* Una regola tipica del pollice durante la creazione di una regola consiste nel pensarla nel contesto dell&#39;oggetto su cui si sta scrivendo una regola. Tenere presente che si desidera nascondere o mostrare il campo B in base al valore specificato dall&#39;utente nel campo A. In questo caso si sta valutando una condizione nel campo A e, in base al valore restituito, si sta attivando un&#39;azione nel campo B.

   Pertanto, se scrivi una regola sul campo B (l&#39;oggetto su cui stai valutando una condizione), utilizza il costrutto condizione-azione o il tipo di regola When. Allo stesso modo, utilizza il costrutto della condizione azione o il tipo di regola Mostra o Nascondi sul campo A.

* A volte, è necessario eseguire più azioni in base a una condizione. In questi casi, si consiglia di utilizzare il costrutto condizione-azione . In questo costrutto è possibile valutare una condizione una volta e specificare più istruzioni di azione.

   Ad esempio, per nascondere i campi B, C e D in base alla condizione che verifica il valore specificato da un utente nel campo A, scrivere una regola con il costrutto condizione-azione o quando il tipo di regola sul campo A e specificare le azioni per controllare la visibilità dei campi B, C e D. In caso contrario, sono necessarie tre regole separate sui campi B, C e D, dove ogni regola controlla la condizione e mostra o nasconde il rispettivo campo. In questo esempio, è più efficiente scrivere il tipo di regola When su un oggetto anziché il tipo di regola Show o Hide su tre oggetti.

* Per attivare un&#39;azione basata su più condizioni, si consiglia di utilizzare il costrutto a condizione di azione. Ad esempio, per visualizzare e nascondere il campo A valutando le condizioni nei campi B, C e D, utilizzare Mostra o Nascondi tipo di regola nel campo A.
* Utilizza il costrutto condizione-azione o condizione azione se la regola contiene un&#39;azione per una condizione.
* Se una regola verifica una condizione ed esegue immediatamente un&#39;azione quando fornisce un valore in un campo o esce da un campo, si consiglia di scrivere una regola con il costrutto condizione-azione o il tipo di regola Quando sul campo in cui viene valutata la condizione.
* La condizione nella regola When viene valutata quando un utente modifica il valore dell&#39;oggetto in cui viene applicata la regola When. Tuttavia, se si desidera che l&#39;azione si attivi quando il valore cambia sul lato server, come per la precompilazione del valore, è consigliabile scrivere una regola When che attivi l&#39;azione quando il campo viene inizializzato.
* Quando si scrivono regole per oggetti a discesa, pulsanti di scelta o caselle di controllo, le opzioni o i valori di questi oggetti modulo sono precompilati nell’editor di regole.

## Tipi ed eventi di operatori disponibili nell&#39;editor delle regole {#available-operator-types-and-events-in-rule-editor}

L&#39;editor di regole fornisce i seguenti operatori logici ed eventi utilizzando i quali puoi creare regole.

* **È uguale a**
* **È diverso da**
* **Inizia con**
* **Termina con**
* **Contiene**
* **È vuoto**
* **Non è vuoto**
* **Selezionato:** Restituisce true quando l’utente seleziona una particolare opzione per un pulsante di scelta casella, elenco a discesa e un pulsante di scelta.
* **È inizializzato (evento):** Restituisce true quando viene eseguito il rendering di un oggetto modulo nel browser.
* **È modificato (evento):** Restituisce true quando l’utente modifica il valore immesso o l’opzione selezionata per un oggetto modulo.
* **Navigation(event):** Restituisce true quando l&#39;utente fa clic su un oggetto di navigazione. Gli oggetti di navigazione vengono utilizzati per spostarsi tra i pannelli.
* **Completamento passaggio (evento):** Restituisce true al completamento di un passaggio di una regola.
* **Invio (evento) riuscito:** Restituisce true se i dati vengono inviati correttamente a un modello dati del modulo.
* **Errore in Submission(event):**  Restituisce true in caso di invio non riuscito di dati a un modello dati del modulo.

## Tipi di regole disponibili nell’editor delle regole {#available-rule-types-in-rule-editor}

L&#39;editor di regole fornisce un set di tipi di regole predefiniti che è possibile utilizzare per scrivere regole. Esaminiamo ogni tipo di regola in dettaglio. Per ulteriori informazioni sulla scrittura di regole nell&#39;editor di regole, vedi [Regole di scrittura](rule-editor.md#p-write-rules-p).

### [!UICONTROL Quando  ] {#whenruletype}

La **[!UICONTROL Quando]** il tipo di regola segue **azione alternata condizione-azione** costrutto di regole, o a volte solo **condizione-azione** costruzione. In questo tipo di regola, devi prima specificare una condizione per la valutazione seguita da un&#39;azione da attivare se la condizione è soddisfatta ( `True`). Quando utilizzi il tipo di regola When, puoi utilizzare più operatori AND e OR per creare [espressioni nidificate](#nestedexpressions).

Utilizzando il tipo di regola When, è possibile valutare una condizione di un oggetto modulo ed eseguire azioni su uno o più oggetti.

In parole semplici, una regola Quando tipica è strutturata come segue:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

Azione 2 sull&#39;oggetto B; E l&#39;azione 3 sull&#39;oggetto C;

_

Quando si dispone di un componente con più valori, ad esempio pulsanti di scelta o elenco, durante la creazione di una regola per quel componente le opzioni vengono recuperate automaticamente e rese disponibili al creatore di regole. Non è necessario digitare nuovamente i valori delle opzioni.

Ad esempio, un elenco include quattro opzioni: Rosso, Blu, Verde e Giallo. Durante la creazione della regola, le opzioni (pulsanti di scelta) vengono recuperate automaticamente e rese disponibili al creatore della regola come segue:

![Opzioni visualizzate da più valori](assets/multivaluefcdisplaysoptions.png)

Quando scrivi una regola When, puoi attivare l&#39;azione Clear Value Of (Cancella valore dell&#39;azione). Cancella valore dell&#39;azione cancella il valore dell&#39;oggetto specificato. L’opzione Cancella valore di come opzione nell’istruzione When consente di creare condizioni complesse con più campi.

![Cancella valore](assets/clearvalueof.png)

**[!UICONTROL Nascondi]** Nasconde l&#39;oggetto specificato.

**[!UICONTROL Mostra]** Mostra l’oggetto specificato.

**[!UICONTROL Abilita]** Abilita l’oggetto specificato.

**[!UICONTROL Disattiva]** Disattiva l’oggetto specificato.

**[!UICONTROL Richiamare il servizio]** Richiama un servizio configurato in un modello dati del modulo. Quando si sceglie l&#39;operazione Invoke Service, viene visualizzato un campo. Toccando il campo, vengono visualizzati tutti i servizi configurati in tutti i modelli di dati modulo sul [!DNL Experience Manager] istanza. Quando si sceglie un servizio Modello dati modulo, vengono visualizzati più campi in cui è possibile mappare gli oggetti modulo con i parametri di input e output per il servizio specificato. Vedere la regola di esempio per richiamare i servizi Form Data Model.

Oltre al servizio Modello dati modulo, è possibile specificare un URL WSDL diretto per richiamare un servizio Web. Tuttavia, un servizio Form Data Model presenta molti vantaggi e l&#39;approccio consigliato per richiamare un servizio.

Per ulteriori informazioni sulla configurazione dei servizi nel modello dati modulo, consulta [[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md).

**[!UICONTROL Imposta valore di]** Calcola e imposta il valore dell&#39;oggetto specificato. È possibile impostare il valore dell&#39;oggetto su una stringa, il valore di un altro oggetto, il valore calcolato utilizzando l&#39;espressione o la funzione matematica, il valore di una proprietà di un oggetto o il valore di output da un servizio Form Data Model configurato. Quando scegli l’opzione del servizio Web, vengono visualizzati tutti i servizi configurati in tutti i modelli di dati modulo sul [!DNL Experience Manager] istanza. Quando si sceglie un servizio Modello dati modulo, vengono visualizzati più campi in cui è possibile mappare gli oggetti modulo con i parametri di input e output per il servizio specificato.

Per ulteriori informazioni sulla configurazione dei servizi nel modello dati modulo, consulta [[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md).

La **[!UICONTROL Imposta proprietà]** Il tipo di regola consente di impostare il valore di una proprietà dell&#39;oggetto specificato in base a un&#39;azione condizione.

Consente di definire regole per aggiungere le caselle di controllo in modo dinamico al modulo adattivo. È possibile utilizzare una funzione personalizzata, un oggetto modulo o una proprietà oggetto per definire una regola.

![Imposta proprietà](assets/set_property_rule_new.png)

Per definire una regola basata su una funzione personalizzata, seleziona **[!UICONTROL Uscita funzione]** dall’elenco a discesa e trascina una funzione personalizzata dal **[!UICONTROL Funzioni]** scheda . Se l’azione della condizione viene soddisfatta, al Modulo adattivo viene aggiunto il numero di caselle di controllo definite nella funzione personalizzata.

Per definire una regola basata su un oggetto modulo, selezionare **[!UICONTROL Oggetto modulo]** dall’elenco a discesa e trascinare un oggetto modulo dal **[!UICONTROL Oggetti modulo]** scheda . Se l’azione della condizione viene soddisfatta, al modulo adattivo viene aggiunto il numero di caselle di controllo definite nell’oggetto modulo.

Una regola Imposta proprietà basata su una proprietà oggetto consente di aggiungere il numero di caselle di controllo in un modulo adattivo basato su un&#39;altra proprietà oggetto inclusa nel modulo adattivo.

Nella figura seguente viene illustrato un esempio di aggiunta dinamica di caselle di controllo in base al numero di elenchi a discesa nel modulo adattivo:

![Proprietà oggetto](assets/object_property_set_property_new.png)

**[!UICONTROL Cancella Valore Di]** Cancella il valore dell&#39;oggetto specificato.

**[!UICONTROL Imposta messa a fuoco]** Imposta lo stato attivo sull&#39;oggetto specificato.

**[!UICONTROL Salva modulo]** Salva il modulo.

**[!UICONTROL Invia Forms]** Invia il modulo.

**[!UICONTROL Ripristina modulo]** Reimposta il modulo.

**[!UICONTROL Convalida modulo]** Convalida il modulo.

**[!UICONTROL Aggiungi istanza]** Aggiunge un&#39;istanza del pannello o della riga di tabella ripetibili specificati.

**[!UICONTROL Rimuovi istanza]** Rimuove un&#39;istanza del pannello o della riga di tabella ripetibili specificati.

**[!UICONTROL Passa a]** Passa ad altri <!--Interactive Communications,--> Forms adattivo, altre risorse come immagini o frammenti di documento, o un URL esterno. <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

### [!UICONTROL Imposta valore di] {#set-value-of}

La **[!UICONTROL Imposta valore di]** il tipo di regola consente di impostare il valore di un oggetto modulo a seconda che la condizione specificata sia soddisfatta o meno. Il valore può essere impostato su un valore di un altro oggetto, una stringa letterale, un valore derivato da un&#39;espressione matematica o da una funzione, un valore di una proprietà di un altro oggetto o l&#39;output di un servizio Form Data Model. Allo stesso modo, è possibile verificare la presenza di una condizione su un componente, una stringa, una proprietà o valori derivati da una funzione o un&#39;espressione matematica.

La **Imposta valore di** il tipo di regola non è disponibile per tutti gli oggetti modulo, ad esempio pannelli e pulsanti della barra degli strumenti. Una regola Set Value Of standard ha la seguente struttura:

Imposta il valore dell&#39;oggetto A su:

(stringa ABC) OR (proprietà dell&#39;oggetto X dell&#39;oggetto C) OR (valore da una funzione) OR (valore da un&#39;espressione matematica) OR (valore di output di un servizio del modello dati o di un servizio Web);

Quando (facoltativo):

(Condizione 1 E condizione 2 E condizione 3) è TRUE;

Nell&#39;esempio seguente il valore viene inserito in `dependentid` come input e imposta il valore del `Relation` all&#39;output del `Relation` argomento `getDependent` Servizio Modello dati modulo .

![Set-value-web-service](assets/set-value-web-service.png)

Esempio di regola Imposta valore tramite il servizio Modello dati modulo

>[!NOTE]
>
>Inoltre, è possibile utilizzare Imposta valore della regola per compilare tutti i valori di un componente elenco a discesa dall’output di un servizio Form Data Model o di un servizio Web. Assicurati tuttavia che l&#39;argomento di output scelto sia di tipo matrice. Tutti i valori restituiti in una matrice diventano disponibili nell&#39;elenco a discesa specificato.

### [!UICONTROL Mostra] {#show}

Utilizzo della **[!UICONTROL Mostra]** tipo di regola, è possibile scrivere una regola per mostrare o nascondere un oggetto modulo in base al fatto che una condizione sia soddisfatta o meno. Il tipo di regola Mostra attiva anche l&#39;azione Nascondi nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola Show tipica è strutturata come segue:

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

### [!UICONTROL Nascondi] {#hide}

Simile al tipo di regola Mostra, puoi utilizzare la **[!UICONTROL Nascondi]** tipo di regola per mostrare o nascondere un oggetto modulo in base al soddisfacimento o meno di una condizione. Il tipo di regola Nascondi attiva anche l&#39;azione Mostra nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola Nascondi tipica è strutturata come segue:

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

### [!UICONTROL Attiva] {#enable}

La **[!UICONTROL Abilita]** Il tipo di regola consente di abilitare o disabilitare un oggetto modulo in base al fatto che una condizione sia soddisfatta o meno. Il tipo di regola Abilita attiva inoltre attiva l&#39;azione Disabilita nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola di abilitazione tipica è strutturata come segue:

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

### [!UICONTROL Disattiva] {#disable}

Simile al tipo di regola Abilita, la **[!UICONTROL Disattiva]** il tipo di regola consente di abilitare o disabilitare un oggetto modulo in base al fatto che una condizione sia soddisfatta o meno. Il tipo di regola Disattiva attiva anche l&#39;azione Abilita nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola Disabilita tipica è strutturata come segue:

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### [!UICONTROL Convalida] {#validate}

La **[!UICONTROL Convalida]** il tipo di regola convalida il valore in un campo utilizzando un&#39;espressione. Ad esempio, è possibile scrivere un&#39;espressione per verificare che la casella di testo per specificare il nome non contenga caratteri o numeri speciali.

Una regola Convalida tipica è strutturata come segue:

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Se il valore specificato non è conforme alla regola Validate, è possibile visualizzare un messaggio di convalida all&#39;utente. Puoi specificare il messaggio nella **[!UICONTROL Messaggio di convalida script]** nelle proprietà del componente nella barra laterale.

![Convalida script](assets/script-validation.png)

### [!UICONTROL Imposta Le Opzioni Di] {#setoptionsof}

La **[!UICONTROL Imposta Le Opzioni Di]** Il tipo di regola consente di definire regole per aggiungere le caselle di controllo in modo dinamico al modulo adattivo. È possibile utilizzare un modello dati modulo o una funzione personalizzata per definire la regola.

Per definire una regola basata su una funzione personalizzata, seleziona **[!UICONTROL Uscita funzione]** dall’elenco a discesa e trascina una funzione personalizzata dal **[!UICONTROL Funzioni]** scheda . Il numero di caselle di controllo definite nella funzione personalizzata viene aggiunto al Modulo adattivo.

![Funzioni personalizzate](assets/custom_functions_set_options_new.png)

Per creare una funzione personalizzata, vedi [funzioni personalizzate nell’editor di regole](#custom-functions).

Per definire una regola basata su un modello dati modulo:

1. Seleziona **[!UICONTROL Uscita servizio]** dall’elenco a discesa.
1. Selezionare l&#39;oggetto modello dati.
1. Selezionare una proprietà dell&#39;oggetto modello dati dal **[!UICONTROL Valore visualizzato]** elenco a discesa. Il numero di caselle nel modulo adattivo deriva dal numero di istanze definite per tale proprietà nel database.
1. Selezionare una proprietà dell&#39;oggetto modello dati dal **[!UICONTROL Salva valore]** elenco a discesa.

![Opzioni di impostazione FDM](assets/fdm_set_options_new.png)

## Interfaccia utente dell’editor di regole {#understanding-the-rule-editor-user-interface}

L’editor delle regole fornisce un’interfaccia utente completa ma semplice per scrivere e gestire le regole. Puoi avviare l’interfaccia utente dell’editor di regole da un modulo adattivo in modalità di creazione.

Per avviare l&#39;interfaccia utente dell&#39;editor di regole:

1. Aprire un modulo adattivo in modalità di creazione.
1. Toccare l’oggetto modulo per il quale si desidera scrivere una regola e nella barra degli strumenti del componente toccare ![edit-rules](assets/edit-rules-icon.svg). Viene visualizzata l’interfaccia utente dell’editor di regole.

   ![create-rules](assets/create-rules.png)

   In questa visualizzazione sono elencate tutte le regole esistenti sugli oggetti modulo selezionati. Per informazioni sulla gestione delle regole esistenti, consulta [Gestire le regole](rule-editor.md#p-manage-rules-p).

1. Tocca **[!UICONTROL Crea]** per scrivere una nuova regola. L’editor visivo dell’interfaccia utente dell’editor di regole si apre per impostazione predefinita quando si avvia l’editor di regole la prima volta.

   ![Interfaccia utente dell’editor delle regole](assets/rule-editor-ui.png)

Diamo un’occhiata dettagliata a ciascun componente dell’interfaccia utente dell’editor di regole.

### A. Visualizzazione della regola del componente {#a-component-rule-display}

Visualizza il titolo dell’oggetto Modulo adattivo tramite il quale è stato avviato l’editor di regole e il tipo di regola attualmente selezionato. Nell’esempio precedente, l’editor di regole viene avviato da un oggetto Modulo adattivo denominato Salario e il tipo di regola selezionato è Quando.

### B. Oggetti e funzioni del modulo {#b-form-objects-and-functions-br}

Il riquadro a sinistra nell’interfaccia utente dell’editor di regole include due schede: **[!UICONTROL Oggetti Forms]** e **[!UICONTROL Funzioni]**.

La scheda Oggetti modulo mostra una visualizzazione gerarchica di tutti gli oggetti contenuti nel modulo adattivo. Visualizza il titolo e il tipo degli oggetti. Quando si scrive una regola, è possibile trascinare gli oggetti modulo nell’editor di regole. Durante la creazione o la modifica di una regola quando si trascina un oggetto o una funzione in un segnaposto, il segnaposto assume automaticamente il tipo di valore appropriato.

Gli oggetti modulo a cui è stata applicata una o più regole valide sono contrassegnati con un punto verde. Se una delle regole applicate a un oggetto modulo non è valida, l’oggetto modulo è contrassegnato da un punto giallo.

La scheda Funzioni include un set di funzioni integrate quali Somma di, Min di, Max di, Media di, Numero di e Convalida del modulo. È possibile utilizzare queste funzioni per calcolare i valori in pannelli e righe di tabella ripetibili e utilizzarli nelle istruzioni di azione e condizione durante la scrittura delle regole. Tuttavia, puoi creare [funzioni personalizzate](#custom-functions) anche.

![Scheda Funzioni](assets/functions.png)

>[!NOTE]
>
>È possibile eseguire la ricerca del testo sui nomi e i titoli di oggetti e funzioni nelle schede Oggetti e Funzioni di Forms.

Nella struttura ad albero a sinistra degli oggetti modulo è possibile toccare gli oggetti modulo per visualizzare le regole applicate a ciascuno di essi. Non solo è possibile spostarsi tra le regole dei vari oggetti modulo, ma è anche possibile copiare e incollare le regole tra gli oggetti modulo. Per ulteriori informazioni, consulta [Copiare e incollare le regole](rule-editor.md#p-copy-paste-rules-p).

### C. Attiva/disattiva oggetti e funzioni modulo {#c-form-objects-and-functions-toggle-br}

Quando viene toccato, il pulsante di attivazione/disattivazione attiva il riquadro oggetti modulo e funzioni.

### D. Editor di regole visive {#visual-rule-editor}

L’editor di regole visive è l’area in modalità editor visivo dell’interfaccia utente dell’editor di regole in cui si scrivono le regole. Ti consente di selezionare un tipo di regola e di conseguenza di definire condizioni e azioni. Quando si definiscono condizioni e azioni in una regola, è possibile trascinare oggetti e funzioni modulo dal riquadro Oggetti modulo e funzioni.

Per ulteriori informazioni sull’utilizzo dell’editor di regole visive, consulta [Regole di scrittura](rule-editor.md#p-write-rules-p).
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and vice versa, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E. Pulsanti Fine e Annulla {#done-and-cancel-buttons}

La **[!UICONTROL Fine]** viene utilizzato per salvare una regola. È possibile salvare una regola incompleta. Tuttavia, incomplete non sono valide e non vengono eseguite. Le regole salvate in un oggetto modulo vengono elencate quando si avvia l&#39;editor di regole la prossima volta dallo stesso oggetto modulo. In questa visualizzazione puoi gestire le regole esistenti. Per ulteriori informazioni, consulta [Gestire le regole](rule-editor.md#p-manage-rules-p).

La **[!UICONTROL Annulla]** elimina le modifiche apportate a una regola e chiude l’editor di regole.

## Regole di scrittura {#write-rules}

Puoi scrivere regole utilizzando l’editor di regole visive &lt;!>— o l&#39;editor di codice>. Quando avvii l’editor di regole la prima volta, questo viene aperto in modalità editor visivo. Puoi passare alla modalità editor di codice e alle regole di scrittura. Tuttavia, se scrivi o modifichi una regola nell&#39;editor di codice, non puoi passare all&#39;editor visivo per quella regola a meno che non cancelli l&#39;editor di codice. Quando si avvia l&#39;editor di regole la prossima volta, questo si apre nella modalità utilizzata l&#39;ultima volta per creare la regola.

Per prima cosa, vediamo come scrivere regole utilizzando l’editor visivo.

### Utilizzo dell’editor visivo {#using-visual-editor}

Comprendiamo come creare una regola nell’editor visivo utilizzando il seguente modulo di esempio.

![Crea un esempio di regola](assets/create-rule-example.png)

La sezione Requisiti del prestito nel modulo di domanda di prestito di esempio richiede ai richiedenti di specificare lo stato civile, lo stipendio e, se coniugati, lo stipendio del coniuge. In base agli input dell&#39;utente, la regola calcola l&#39;importo di idoneità del prestito e viene visualizzata nel campo Idoneità del prestito . Per implementare lo scenario, applica le seguenti regole:

* Il campo Stipendio del coniuge viene visualizzato solo quando lo Stato civile è sposato.
* L&#39;importo di ammissibilità al prestito è pari al 50% dello stipendio totale.

Per scrivere le regole, esegui le seguenti operazioni:

1. Innanzitutto, scrivi la regola per controllare la visibilità del campo Stipendio coniuge in base all&#39;opzione selezionata dall&#39;utente per il pulsante di opzione Stato civile.

   Aprire il modulo di richiesta di prestito in modalità di authoring. Tocca **[!UICONTROL Stato civile]** componente e tocco ![edit-rules](assets/edit-rules-icon.svg). Avanti, tocca **[!UICONTROL Crea]** per avviare l&#39;editor di regole.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   Quando si avvia l&#39;editor di regole, la regola When è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, Stato civile) dal quale è stato avviato l&#39;editor di regole viene specificato nell&#39;istruzione When.

   Sebbene non sia possibile modificare o modificare l’oggetto selezionato, è possibile utilizzare l’elenco a discesa della regola, come illustrato di seguito, per selezionare un altro tipo di regola. Per creare una regola su un altro oggetto, tocca Annulla per uscire dall’editor di regole e avviarla nuovamente dall’oggetto modulo desiderato.

1. Tocca **[!UICONTROL Seleziona stato]** a discesa e seleziona **[!UICONTROL è uguale a]**. La **[!UICONTROL Immettere una stringa]** viene visualizzato il campo .

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   Nel pulsante di opzione Stato civile, **[!UICONTROL Sposato]** e **[!UICONTROL Singolo]** opzioni assegnate **0** e **1** rispettivamente. È possibile verificare i valori assegnati nella scheda Titolo della finestra di dialogo del pulsante di scelta Modifica , come illustrato di seguito.

   ![Valori dei pulsanti di scelta dall’editor di regole](assets/radio-button-values.png)

1. In **[!UICONTROL Immettere una stringa]** campo nella regola, specifica **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   La condizione è stata definita come `When Marital Status is equal to Married`. Quindi, definire l&#39;azione da eseguire se questa condizione è True.

1. Nell’istruzione Then, seleziona **[!UICONTROL Mostra]** dal **[!UICONTROL Seleziona azione]** a discesa.

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. Trascina la **[!UICONTROL Stipendio del coniuge]** dalla scheda Oggetti modulo **[!UICONTROL Rilascia oggetto o seleziona qui]** campo . In alternativa, tocca **[!UICONTROL Rilascia oggetto o seleziona qui]** e seleziona il **[!UICONTROL Stipendio del coniuge]** dal menu a comparsa, in cui sono elencati tutti gli oggetti modulo.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   La regola viene visualizzata come segue nell&#39;editor di regole.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

1. Tocca **[!UICONTROL Fine]** per salvare la regola.

1. Ripetere i passaggi da 1 a 5 per definire un&#39;altra regola per nascondere il campo Stipendio coniuge se lo Stato coniugale è Singolo. La regola viene visualizzata come segue nell&#39;editor di regole.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >In alternativa, è possibile scrivere una regola Show sul campo Stipendio coniuge, invece di due regole When sul campo Stato coniugale, per implementare lo stesso comportamento.

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. Successivamente, scrivere una regola per calcolare l&#39;importo di idoneità del prestito, che corrisponde al 50% dello stipendio totale, e visualizzarlo nel campo Idoneità del prestito. Per ottenere questo risultato, crea **[!UICONTROL Imposta valore di]** regole sul campo Idoneità al prestito .

   In modalità di authoring, tocca il pulsante **[!UICONTROL Idoneità al prestito]** campo e tocco ![edit-rules](assets/edit-rules-icon.svg). Avanti, tocca **[!UICONTROL Crea]** per avviare l&#39;editor di regole.

1. Seleziona **[!UICONTROL Imposta valore di]** regola dal menu a discesa regola.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. Tocca **[!UICONTROL Seleziona opzione]** e seleziona **[!UICONTROL Espressione matematica]**. Si apre un campo per scrivere un’espressione matematica.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. Nel campo espressione:

   * Seleziona o trascina la selezione dalla scheda Oggetto Forms **[!UICONTROL Salario]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]** campo .

   * Seleziona **[!UICONTROL Plus]** dal **[!UICONTROL Seleziona operatore]** campo .

   * Seleziona o trascina la selezione dalla scheda Oggetto Forms **[!UICONTROL Stipendio del coniuge]** campo dell&#39;altro **[!UICONTROL Rilascia oggetto o seleziona qui]** campo .

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. Quindi, tocca l’area evidenziata intorno al campo espressione e tocca **[!UICONTROL Estendi espressione]**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   Nel campo espressione estesa, seleziona **[!UICONTROL diviso per]** dal **[!UICONTROL Seleziona operatore]** campo e **[!UICONTROL Numero]** dal **[!UICONTROL Seleziona opzione]** campo . Quindi, specifica **[!UICONTROL 2]** nel campo numero.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >È possibile creare espressioni complesse utilizzando componenti, funzioni, espressioni matematiche e valori di proprietà dal campo Seleziona opzione .

   Quindi, creare una condizione, che quando restituisce True, viene eseguita dall&#39;espressione.

1. Tocca **[!UICONTROL Aggiungi condizione]** per aggiungere un’istruzione When.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   Nell’istruzione When:

   * Seleziona o trascina la selezione dalla scheda Oggetto Forms **[!UICONTROL Stato civile]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]** campo .

   * Seleziona **[!UICONTROL è uguale a]** dal **[!UICONTROL Seleziona operatore]** campo .

   * Seleziona Stringa nell’altro **[!UICONTROL Rilascia oggetto o seleziona qui]** campo e specifica **[!UICONTROL Sposato]** in **[!UICONTROL Immettere una stringa]** campo .

   La regola viene finalmente visualizzata come segue nell&#39;editor di regole.  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

1. Toccate **[!UICONTROL Chiudi]**. Salva la regola.

1. Ripetere i passaggi da 7 a 14 per definire un&#39;altra regola per calcolare l&#39;idoneità del prestito se lo stato civile è Single. La regola viene visualizzata come segue nell&#39;editor di regole.

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>In alternativa, è possibile utilizzare la regola Imposta valore di per calcolare l&#39;idoneità del prestito nella regola Quando creata per mostrare e nascondere il campo Stipendio del coniuge. La regola combinata risultante quando lo stato civile è Single viene visualizzata come segue nell&#39;editor di regole.
>
>Allo stesso modo, è possibile scrivere una regola combinata per controllare la visibilità del campo Stipendio coniuge e calcolare l&#39;idoneità del prestito quando lo Stato del matrimonio è sposato.

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

Oltre alle funzioni preconfigurate come *Somma di* che sono elencati in Output funzioni, è possibile scrivere funzioni personalizzate di cui si ha spesso bisogno. Assicurati che la funzione che scrivi sia accompagnata dal `jsdoc` sopra.

Accompagnato `jsdoc` è richiesto:

* Se desideri una configurazione e una descrizione personalizzate
* Poiché esistono diversi modi per dichiarare una funzione in `JavaScript,` e i commenti consentono di tenere traccia delle funzioni.

Per ulteriori informazioni, consulta [jsdoc.app](https://jsdoc.app/).

Supportato `jsdoc` tag:

* **Privato**
Sintassi: Una funzione privata non è inclusa come funzione personalizzata.`@private`
Una funzione privata non è inclusa come funzione personalizzata.

* **Nome**
Sintassi: Alternativa `@name funcName <Function Name>`
Alternativa `,` puoi utilizzare: `@function funcName <Function Name>` **o** `@func` `funcName <Function Name>`.
   `funcName` è il nome della funzione (non sono consentiti spazi).
   `<Function Name>` è il nome visualizzato della funzione.

* **Membro**
Sintassi: Associa uno spazio dei nomi alla funzione .`@memberof namespace`
Associa uno spazio dei nomi alla funzione .

* **Parametro**
Sintassi: In alternativa, puoi utilizzare: `@param {type} name <Parameter Description>`
In alternativa, puoi utilizzare: `@argument` `{type} name <Parameter Description>` **o** `@arg` `{type}` `name <Parameter Description>`.
Mostra i parametri utilizzati dalla funzione . Una funzione può avere più tag di parametro, un tag per ogni parametro nell&#39;ordine di occorrenza.
   `{type}` rappresenta il tipo di parametro. I tipi di parametri consentiti sono:

   1. stringa
   1. numero
   1. booleano
   1. scope

   L’ambito si riferisce ai campi di un modulo adattivo. Quando un modulo utilizza il caricamento lento, è possibile utilizzare `scope` per accedere ai relativi campi. È possibile accedere ai campi sia quando i campi sono caricati sia se i campi sono contrassegnati come globali.

   Tutti i tipi di parametri sono organizzati in una delle categorie precedenti. Nessuno non supportato. Assicurati di selezionare uno dei tipi indicati sopra. I tipi non sono sensibili all’uso di maiuscole e minuscole. Gli spazi non sono consentiti nel parametro `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Tipo di ritorno**
Sintassi: In alternativa, puoi utilizzare `@return {type}`
In alternativa, puoi utilizzare `@returns {type}`.
Aggiunge informazioni sulla funzione, ad esempio la sua finalità.
{type} rappresenta il tipo restituito dalla funzione. I tipi di restituzione consentiti sono:

   1. stringa
   1. numero
   1. booleano

   Tutti gli altri tipi di restituzione sono classificati in una delle situazioni precedenti. Nessuno non supportato. Assicurati di selezionare uno dei tipi indicati sopra. I tipi restituiti non fanno distinzione tra maiuscole e minuscole.

   * **Questo**
Sintassi: 
`@this currentComponent`
   Utilizza @this per fare riferimento al componente Modulo adattivo su cui viene scritta la regola.

   L&#39;esempio seguente è basato sul valore del campo. Nell’esempio seguente, la regola nasconde un campo nel modulo. La `this` porzione di `this.value` si riferisce al componente Modulo adattivo sottostante, su cui viene scritta la regola.

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
   >I commenti prima della funzione personalizzata vengono utilizzati per il riepilogo. Il riepilogo può estendersi a più righe finché non viene rilevato un tag . Limita la dimensione a un singolo per una descrizione concisa nel generatore di regole.

**Aggiunta di una funzione personalizzata**

Ad esempio, si desidera aggiungere una funzione personalizzata che calcoli l&#39;area di un quadrato. La lunghezza laterale è l’input dell’utente alla funzione personalizzata, che viene accettata utilizzando una casella numerica del modulo. L’output calcolato viene visualizzato in un’altra casella numerica del modulo. Per aggiungere una funzione personalizzata, devi prima creare una libreria client e poi aggiungerla all&#39;archivio CRX.

Per creare una libreria client e aggiungerla nell&#39;archivio CRX, esegui i seguenti passaggi:

1. Crea un clientEsegui i seguenti passaggi alla libreria. Per ulteriori informazioni, consulta [Utilizzo delle librerie lato client](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).
1. In CRXDE, aggiungi una proprietà `categories`con valore di tipo stringa come `customfunction` al `clientlib` cartella.

   >[!NOTE]
   >
   >`customfunction`è una categoria di esempio. Puoi scegliere qualsiasi nome per la categoria creata nella `clientlib`cartella.

Dopo aver aggiunto la libreria client nell’archivio CRX, utilizzala nel modulo adattivo. Consente di utilizzare la funzione personalizzata come regola nel modulo. Per aggiungere la libreria client nel modulo adattivo, effettua le seguenti operazioni:

1. Apri il modulo in modalità di modifica.
Per aprire un modulo in modalità di modifica, selezionalo e tocca **[!UICONTROL Apri]**.
1. In modalità di modifica, seleziona un componente, quindi tocca ![a livello di campo](assets/select_parent_icon.svg) > **[!UICONTROL Contenitore di moduli adattivi]**, quindi tocca ![cmppr](assets/configure-icon.svg).
1. Nella barra laterale, in Nome libreria client , aggiungi la libreria client. ( `customfunction` nell&#39;esempio.)

   ![Aggiunta della libreria client di funzioni personalizzata](assets/clientlib.png)

1. Seleziona la casella numerica di input e tocca ![edit-rules](assets/edit-rules-icon.svg) per aprire l’editor di regole.
1. Tocca **[!UICONTROL Crea regola]**. Utilizzando le opzioni visualizzate di seguito, creare una regola per salvare il valore al quadrato dell&#39;input nel campo Output del modulo.

[![Utilizzo di funzioni personalizzate per creare una regola](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)

1. Toccate **[!UICONTROL Chiudi]**. Viene aggiunta la funzione personalizzata .

#### Tipi supportati per la dichiarazione della funzione {#function-declaration-supported-types}

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

**Espressione e istruzione della funzione**

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

Limitazione: funzione personalizzata seleziona solo la prima dichiarazione di funzione dall&#39;elenco delle variabili, se insieme. È possibile utilizzare l&#39;espressione di funzione per ogni funzione dichiarata.

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
>Assicurati di utilizzare `jsdoc` per ogni funzione personalizzata. Nonostante `jsdoc`commenti incoraggiati, includi un `jsdoc`commento per contrassegnare la funzione come funzione personalizzata. Abilita la gestione predefinita della funzione personalizzata.

## Gestire le regole {#manage-rules}

Tutte le regole esistenti in un oggetto modulo vengono elencate quando si tocca l’oggetto e si tocca ![edit-rules1](assets/edit-rules-icon.svg). Puoi visualizzare il titolo e un&#39;anteprima del riepilogo della regola. Inoltre, l’interfaccia utente ti consente di espandere e visualizzare il riepilogo completo delle regole, modificare l’ordine delle regole, modificare le regole ed eliminare le regole.

![Regole elenco](assets/list-rules.png)

È possibile eseguire le azioni seguenti sulle regole:

* **Espandi/Comprimi**: La colonna Contenuto nell’elenco delle regole visualizza il contenuto della regola. Se l’intero contenuto della regola non è visibile nella visualizzazione predefinita, tocca ![contenuto di expand-rule](assets/Smock_ChevronDown.svg) per espanderlo.

* **Riordina**: Qualsiasi nuova regola creata viene impilata in fondo all&#39;elenco delle regole. Le regole vengono eseguite dall’alto verso il basso. La regola nella parte superiore viene eseguita per prima, seguita da altre regole dello stesso tipo. Ad esempio, se le regole When, Show, Enable e When si trovano rispettivamente in prima, seconda, terza e quarta posizione dall&#39;alto, la regola When nella parte superiore viene eseguita per prima seguita dalla regola When nella quarta posizione. Vengono quindi eseguite le regole Mostra e Abilita .
Per modificare l’ordine di una regola, tocca ![regole di ordinamento](assets/sort-rules.svg) oppure trascinalo nell’ordine desiderato nell’elenco.

* **Modifica**: Per modificare una regola, seleziona la casella di controllo accanto al titolo della regola. Vengono visualizzate le opzioni per modificare ed eliminare la regola. Tocca **[!UICONTROL Modifica]** per aprire la regola selezionata nell’editor di regole <!-- in visual  or code editor mode depending on the mode used to create the rule -->.

* **Elimina**: Per eliminare una regola, selezionala e tocca **[!UICONTROL Elimina]**.

* **Attiva/Disattiva**: Quando devi sospendere temporaneamente l’utilizzo di una regola, puoi selezionare una o più regole e toccare **[!UICONTROL Disattiva]** nella barra degli strumenti Azioni per disattivarle. Se una regola è disabilitata, non viene eseguita in fase di runtime. Per abilitare una regola disabilitata, puoi selezionarla e toccare Abilita nella barra degli strumenti delle azioni. Nella colonna dello stato della regola viene visualizzato se la regola è abilitata o disabilitata.

![Disattiva regola](assets/disablerule.png)

## Copiare e incollare le regole {#copy-paste-rules}

Puoi copiare e incollare una regola da un campo ad altri campi simili per risparmiare tempo.

Per copiare e incollare le regole, procedi come segue:

1. Toccare l’oggetto modulo da cui si desidera copiare una regola e, nella barra degli strumenti del componente, toccare ![modifica regola](assets/edit-rules-icon.svg). Viene visualizzata l’interfaccia utente dell’editor di regole con l’oggetto modulo selezionato e vengono visualizzate le regole esistenti.

   ![copia regola](assets/copyrule.png)

   Per informazioni sulla gestione delle regole esistenti, consulta [Gestire le regole](rule-editor.md#p-manage-rules-p).

1. Seleziona la casella di controllo accanto al titolo della regola. Vengono visualizzate le opzioni per gestire la regola. Tocca **[!UICONTROL Copia]**.

   ![copyrule2](assets/copyrule2.png)

1. Selezionare un altro oggetto modulo al quale si desidera incollare la regola e toccare **[!UICONTROL Incolla]**. Inoltre, puoi modificare la regola per apportare modifiche.

   >[!NOTE]
   >
   >È possibile incollare una regola in un altro oggetto modulo solo se tale oggetto supporta l&#39;evento della regola copiata. Ad esempio, un pulsante supporta l’evento clic. È possibile incollare una regola con un evento clic su un pulsante ma non su una casella di controllo.

1. Tocca **[!UICONTROL Fine]** per salvare la regola.

## Espressioni nidificate {#nestedexpressions}

L’editor di regole consente di utilizzare più operatori AND e OR per creare regole nidificate. È possibile combinare più operatori AND e OR nelle regole.

Di seguito è riportato un esempio di una regola nidificata che visualizza un messaggio all&#39;utente sull&#39;idoneità per la custodia di un figlio quando vengono soddisfatte le condizioni richieste.

![Espressione complessa](assets/complexexpression.png)

Puoi anche trascinare le condizioni all’interno di una regola per modificarla. Tocca e passa il puntatore del mouse sulla maniglia ( ![impugnatura](assets/drag-handle.svg)) prima di una condizione. Una volta che il puntatore si trasforma in un simbolo a mano come mostrato di seguito, trascina e rilascia la condizione in qualsiasi punto della regola. La struttura delle regole cambia.

![Trascinamento della selezione](assets/drag-and-drop.png)

## Condizioni di espressione della data {#dateexpression}

L’editor di regole consente di utilizzare confronti di date per creare condizioni.

Di seguito è riportato un esempio di condizione che visualizza un oggetto di testo statico se l&#39;ipoteca sulla casa è già stata acquisita, che l&#39;utente indica compilando il campo data.

Quando la data del mutuo della proprietà compilata dall’utente è passata, nel Modulo adattivo viene visualizzata una nota relativa al calcolo del reddito. La regola seguente confronta la data compilata dall’utente con la data corrente e, se la data compilata dall’utente è precedente alla data corrente, nel modulo viene visualizzato il messaggio di testo (denominato Entrate).

![Condizione di espressione data](assets/dateexpressioncondition.png)

Quando la data di compilazione è precedente alla data corrente, nel modulo viene visualizzato il messaggio di testo (Entrate) come segue:

![Condizione di espressione data soddisfatta](assets/dateexpressionconditionmet.png)

## Condizioni di confronto dei numeri {#number-comparison-conditions}

L’editor delle regole ti consente di creare condizioni che confrontano due numeri.

Di seguito è riportato un esempio di condizione che visualizza un oggetto di testo statico se il numero di mesi in cui un richiedente risiede all&#39;indirizzo corrente è inferiore a 36.

![Condizione di confronto dei numeri](assets/numbercomparisoncondition.png)

Se l&#39;utente indica di vivere all&#39;indirizzo residenziale attuale per meno di 36 mesi, il modulo visualizza una notifica che può essere richiesta una maggiore prova di residenza.

![Altre prove richieste](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

## Regole di esempio {#example}

### Richiama del servizio Modello dati modulo {#invoke}

Considera un servizio Web `GetInterestRates` che prende l&#39;importo del prestito, la durata e il punteggio di credito del richiedente come input e restituisce un piano di prestito che include l&#39;ammontare e il tasso di interesse dell&#39;IME. È possibile creare un modello dati modulo utilizzando il servizio Web come origine dati. È possibile aggiungere oggetti del modello dati e un `get` al modello di modulo. Il servizio viene visualizzato nella scheda Servizi del modello dati del modulo. Quindi, creare un Modulo adattivo che includa i campi degli oggetti del modello dati per acquisire gli input degli utenti per l’importo del prestito, la durata e il punteggio di credito. Aggiungi un pulsante che attiva il servizio Web per recuperare i dettagli del piano. L’output viene compilato nei campi appropriati.

La regola seguente mostra come configurare l&#39;azione del servizio Invoke per eseguire lo scenario di esempio.

![Esempio-invoke-services](assets/example-invoke-services.png)

Richiamare il servizio del modello dati modulo utilizzando la regola del modulo adattivo

### Attivazione di più azioni tramite la regola When {#triggering-multiple-actions-using-the-when-rule}

In un modulo di domanda di prestito, si desidera acquisire se il richiedente è un cliente esistente o meno. In base alle informazioni fornite dall’utente, il campo ID cliente deve essere visualizzato o nascosto. Inoltre, se l&#39;utente è un cliente esistente, imposta lo stato attivo sul campo ID cliente . Il modulo di domanda di prestito presenta le seguenti componenti:

* Un pulsante di scelta, **[!UICONTROL Sei un cliente Geometrixx esistente?]**, che prevede [!UICONTROL Sì] e [!UICONTROL No] opzioni. Il valore per Sì è **0** e No **1**.

* Un campo di testo, **[!UICONTROL ID cliente Geometrixx]**, per specificare l&#39;ID cliente.

Quando scrivi una regola When sul pulsante di scelta per implementare questo comportamento, la regola viene visualizzata come segue nell’editor di regole visive.

![When-rule-example](assets/when-rule-example.png)

Regola nell’editor visivo

Nella regola di esempio, l&#39;istruzione nella sezione When è la condizione che, quando restituisce True, esegue le azioni specificate nella sezione Then.

<!-- The rule appears as follows in the code editor.

![when-rule-example-code](assets/when-rule-example-code.png) 

Rule in the code editor -->

### Utilizzo di un output di funzione in una regola {#using-a-function-output-in-a-rule}

In un modulo di ordine di acquisto è disponibile la tabella seguente, in cui gli utenti compilano gli ordini. In questa tabella:

* La prima riga è ripetibile, in modo che gli utenti possano ordinare più prodotti e specificare quantità diverse. Il nome dell’elemento è `Row1`.
* Il titolo della cella nella colonna Quantità prodotto della riga ripetibile è Quantità. Il nome dell’elemento per questa cella è `productquantity`.
* La seconda riga della tabella non è ripetibile e il titolo della cella nella colonna Quantità prodotto in questa riga è Quantità totale.

![Esempio di tabella delle funzioni](assets/example-function-table.png)

**A.** Riga1 **B.** Quantità **C.** Quantità totale

A questo punto, è necessario aggiungere quantità specificate nella colonna Quantità prodotto per tutti i prodotti e visualizzare la somma nella cella Quantità totale. È possibile ottenere questa somma scrivendo una regola Imposta valore di sulla cella Quantità totale come illustrato di seguito.

![Esempio di funzione-uscita](assets/example-function-output.png)

Regola nell’editor visivo

<!-- he rule appears as follows in the code editor.

![example-function-output-code](assets/example-function-output-code.png)

Rule in the code editor -->

### Convalida di un valore di campo utilizzando un’espressione {#validating-a-field-value-using-expression}

Nel modulo di ordine di acquisto illustrato nell&#39;esempio precedente, si desidera impedire all&#39;utente di ordinare più di una quantità di qualsiasi prodotto il cui prezzo è superiore a 10000. Per eseguire questa convalida, puoi scrivere una regola di convalida come mostrato di seguito.

![Esempio di convalida](assets/example-validate.png)

Regola nell’editor visivo

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->
