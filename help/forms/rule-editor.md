---
title: Come si utilizza l’editor di regole per aggiungere regole ai campi del modulo per aggiungere un comportamento dinamico e creare una logica complessa in un modulo adattivo?
description: L’editor di regole di Forms adattivo consente di aggiungere un comportamento dinamico e di creare una logica complessa nei moduli senza codificare o scrivere script.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 6fd38e9e-435e-415f-83f6-3be177738c00
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '6649'
ht-degree: 3%

---

# Aggiungere regole a un modulo adattivo {#adaptive-forms-rule-editor}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service (componenti di base) | Questo articolo |
| AEM as a Cloud Service (componenti core) | [Fai clic qui](/help/forms/rule-editor-core-components.md) |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=it) |

## Panoramica {#overview}

La funzione dell’editor di regole consente agli utenti aziendali e agli sviluppatori di Forms di scrivere regole sugli oggetti Adaptive Form. Queste regole definiscono le azioni da attivare sugli oggetti modulo in base a condizioni preimpostate, input dell&#39;utente e azioni dell&#39;utente sul modulo. Consente di semplificare ulteriormente l’esperienza di compilazione dei moduli, garantendo precisione e velocità.

L’editor di regole fornisce un’interfaccia utente intuitiva e semplificata per scrivere regole. L’editor di regole offre un editor visivo per tutti gli utenti.<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. --> Alcune delle azioni chiave che è possibile eseguire sugli oggetti modulo adattivo utilizzando le regole sono:

* Mostrare o nascondere un oggetto
* Abilitare o disabilitare un oggetto
* Impostare un valore per un oggetto
* Convalidare il valore di un oggetto
* Eseguire funzioni per calcolare il valore di un oggetto
* Richiama un servizio del modello dati modulo ed esegui un’operazione
* Impostare la proprietà di un oggetto

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Gli utenti aggiunti al gruppo forms-power-users possono creare script e modificare quelli esistenti. Gli utenti del gruppo [!DNL forms-users] possono utilizzare gli script ma non crearli o modificarli.

## Differenza tra l’editor di regole nei componenti core e nei componenti di base

{{rule-editor-diff}}

## Informazioni sulle regole {#understanding-a-rule}

Una regola è una combinazione di azioni e condizioni. Nell’editor delle regole, le azioni includono attività quali nascondere, mostrare, abilitare, disabilitare o calcolare il valore di un oggetto in un modulo. Le condizioni sono espressioni booleane che vengono valutate eseguendo controlli e operazioni sullo stato, sul valore o sulla proprietà di un oggetto modulo. Le azioni vengono eseguite in base al valore ( `True` o `False`) restituito valutando una condizione.

L’editor di regole fornisce un set di tipi di regole predefiniti, ad esempio Quando, Mostra, Nascondi, Abilita, Disabilita, Imposta valore di e Convalida, per facilitare la scrittura delle regole. Ogni tipo di regola ti consente di definire condizioni e azioni in una regola. Il documento spiega ulteriormente ogni tipo di regola nei dettagli.

Una regola segue in genere uno dei seguenti costrutti:

**Condizione-Azione** In questo costrutto, una regola definisce innanzitutto una condizione seguita da un&#39;azione da attivare. Il costrutto è paragonabile all&#39;istruzione if-then nei linguaggi di programmazione.

Nell&#39;editor di regole, il tipo di regola **When** applica il costrutto condizione-azione.

**Action-Condition** In questo costrutto, una regola definisce innanzitutto un&#39;azione da attivare seguita da condizioni per la valutazione. Un’altra variante di questo costrutto è action-condition-alternate action, che definisce anche un’azione alternativa da attivare se la condizione restituisce False.

I tipi di regola Mostra, Nascondi, Abilita, Disabilita, Imposta valore di e Convalida nell&#39;editor di regole applicano il costrutto regola della condizione azione. Per impostazione predefinita, l&#39;azione alternativa per Mostra è Nascondi e per Abilita è Disabilita e viceversa. Non è possibile modificare l&#39;azione alternativa predefinita.

>[!NOTE]
>
>I tipi di regole disponibili, incluse le condizioni e le azioni definite nell&#39;editor di regole, dipendono anche dal tipo di oggetto modulo su cui si sta creando una regola. Nell&#39;editor delle regole vengono visualizzati solo i tipi di regole e le opzioni validi per la scrittura di istruzioni di condizione e azione per un particolare tipo di oggetto modulo. Ad esempio, per un oggetto pannello non vengono visualizzati i tipi di regole Convalida, Imposta valore di, Abilita e Disabilita.

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
* **È Vuoto**
* **Non È Vuoto**
* **Ha selezionato:** Restituisce true quando l&#39;utente seleziona un&#39;opzione particolare per una casella di controllo, un elenco a discesa o un pulsante di scelta.
* **È inizializzato (evento):** Restituisce true quando viene eseguito il rendering di un oggetto modulo nel browser.
* **È stato modificato (evento):** Restituisce true quando l&#39;utente modifica il valore immesso o l&#39;opzione selezionata per un oggetto modulo.
* **Navigazione(evento):** Restituisce true quando l&#39;utente fa clic su un oggetto di navigazione. Gli oggetti di navigazione vengono utilizzati per spostarsi tra i pannelli.
* **Completamento passaggio(evento):** Restituisce true al completamento di un passaggio di una regola.
* **Invio riuscito(evento):** Restituisce true in caso di invio corretto di dati a un modello dati del modulo.
* **Errore in Submission(event):** Restituisce true in caso di invio non riuscito di dati a un modello dati del modulo.

## Tipi di regole disponibili nell’editor di regole {#available-rule-types-in-rule-editor}

L’editor di regole fornisce un set di tipi di regole predefiniti che è possibile utilizzare per scrivere regole. Esaminiamo in dettaglio ogni tipo di regola. Per ulteriori informazioni sulla scrittura di regole nell&#39;editor di regole, vedere [Scrivi regole](rule-editor.md#p-write-rules-p).

### [!UICONTROL Quando] {#whenruletype}

Il tipo di regola **[!UICONTROL When]** segue il costrutto della regola **condition-action-alternate action** oppure, a volte, solo il costrutto **condition-action**. In questo tipo di regola si specifica innanzitutto una condizione per la valutazione seguita da un&#39;azione da attivare se la condizione viene soddisfatta ( `True`). Durante l&#39;utilizzo del tipo di regola When, è possibile utilizzare più operatori AND e OR per creare [espressioni nidificate](#nestedexpressions).

Utilizzando il tipo di regola When, è possibile valutare una condizione in un oggetto modulo ed eseguire azioni su uno o più oggetti.

In parole semplici, una regola When tipica è strutturata come segue:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

Azione 2 sull’oggetto B;
E
Azione 3 sull’oggetto C;

_

Quando si dispone di un componente con più valori, ad esempio pulsanti di scelta o elenco, durante la creazione di una regola per tale componente le opzioni vengono recuperate e rese disponibili automaticamente al creatore della regola. Non è necessario digitare nuovamente i valori delle opzioni.

Ad esempio, un elenco include quattro opzioni: Rosso, Blu, Verde e Giallo. Durante la creazione della regola, le opzioni (pulsanti di scelta) vengono recuperate automaticamente e rese disponibili al creatore della regola come segue:

![Più valori visualizza le opzioni](assets/multivaluefcdisplaysoptions1.png)

Durante la scrittura di una regola When, puoi attivare l&#39;azione Cancella valore di. Cancella valore dell&#39;azione cancella il valore dell&#39;oggetto specificato. L&#39;opzione Clear Value (Cancella valore) nell&#39;istruzione When consente di creare condizioni complesse con più campi.

![Cancella valore di](assets/clearvalueof1.png)

**[!UICONTROL Nascondi]** Nasconde l&#39;oggetto specificato.

**[!UICONTROL Mostra]** mostra l&#39;oggetto specificato.

**[!UICONTROL Abilita]** Abilita l&#39;oggetto specificato.

**[!UICONTROL Disabilita]** Disabilita l&#39;oggetto specificato.

**[!UICONTROL Richiama servizio]** Richiama un servizio configurato in un modello dati modulo (FDM). Quando scegli l’operazione Richiama servizio, viene visualizzato un campo. Quando tocca il campo, vengono visualizzati tutti i servizi configurati in tutti i modelli di dati del modulo (FDM) nell&#39;istanza [!DNL Experience Manager]. Quando si sceglie un servizio FDM (Form Data Model), vengono visualizzati più campi in cui è possibile mappare gli oggetti modulo con i parametri di input e output per il servizio specificato. Vedi regola di esempio per richiamare i servizi del modello dati modulo.

Oltre al servizio Modello dati modulo, è possibile specificare un URL WSDL diretto per richiamare un servizio Web. Tuttavia, un servizio di modello dati modulo presenta molti vantaggi e l’approccio consigliato per richiamare un servizio.

Per ulteriori informazioni sulla configurazione dei servizi nel modello dati modulo, vedere [[!DNL Experience Manager Forms] Integrazione dati](data-integration.md).

**[!UICONTROL Imposta il valore di]** Calcola e imposta il valore dell&#39;oggetto specificato. È possibile impostare il valore dell&#39;oggetto su una stringa, il valore di un altro oggetto, il valore calcolato utilizzando un&#39;espressione matematica o una funzione, il valore di una proprietà di un oggetto o il valore di output di un servizio Form Data Model configurato. Quando si sceglie l&#39;opzione Servizio Web, vengono visualizzati tutti i servizi configurati in tutti i modelli di dati del modulo (FDM) nell&#39;istanza [!DNL Experience Manager]. Quando si sceglie un servizio Modello dati modulo, vengono visualizzati più campi in cui è possibile mappare gli oggetti modulo con i parametri di input e output per il servizio specificato.

Per ulteriori informazioni sulla configurazione dei servizi nel modello dati modulo, vedere [[!DNL Experience Manager Forms] Integrazione dati](data-integration.md).

Il tipo di regola **[!UICONTROL Imposta proprietà]** consente di impostare il valore di una proprietà dell&#39;oggetto specificato in base a un&#39;azione condizione. È possibile impostare la proprietà su una delle seguenti opzioni:

* visibile (booleano)
* dorExclusion (booleano)
* chartType (String)
* title (Stringa)
* abilitato (booleano)
* obbligatorio (booleano)
* validationsDisabled (booleano)
* validateExpMessage (Stringa)
* valore (Numero, Stringa, Data)
* items (List)
* valido (booleano)
* errorMessage (stringa)

Ad esempio, consente di definire regole per aggiungere caselle di controllo in modo dinamico al modulo adattivo. È possibile utilizzare una funzione personalizzata, un oggetto modulo o una proprietà oggetto per definire una regola.

![Imposta proprietà](assets/set_property_rule_new1.png)

Per definire una regola basata su una funzione personalizzata, selezionare **[!UICONTROL Output funzione]** dall&#39;elenco a discesa e trascinare una funzione personalizzata dalla scheda **[!UICONTROL Funzioni]**. Se l’azione della condizione viene soddisfatta, il numero di caselle di controllo definite nella funzione personalizzata viene aggiunto al modulo adattivo.

Per definire una regola basata su un oggetto modulo, selezionare **[!UICONTROL Oggetto modulo]** dall&#39;elenco a discesa e trascinare un oggetto modulo dalla scheda **[!UICONTROL Oggetti modulo]**. Se l’azione della condizione viene soddisfatta, il numero di caselle di controllo definite nell’oggetto modulo viene aggiunto al modulo adattivo.

Una regola Imposta proprietà basata su una proprietà oggetto consente di aggiungere il numero di caselle di controllo in un modulo adattivo basato su un’altra proprietà oggetto inclusa nel modulo adattivo.

La figura seguente illustra un esempio di aggiunta dinamica di caselle di controllo in base al numero di elenchi a discesa nel modulo adattivo:

![Proprietà oggetto](assets/object_property_set_property_new1.png)

**[!UICONTROL Cancella valore di]** Cancella il valore dell&#39;oggetto specificato.

**[!UICONTROL Imposta stato attivo]** Imposta lo stato attivo sull&#39;oggetto specificato.

**[!UICONTROL Salva modulo]** salva il modulo.

**[!UICONTROL Invia Forms]** invia il modulo.

**[!UICONTROL Reimposta modulo]** Reimposta il modulo.

**[!UICONTROL Convalida modulo]** convalida il modulo.

**[!UICONTROL Aggiungi istanza]** Aggiunge un&#39;istanza del pannello o della riga di tabella ripetibile specificata.

**[!UICONTROL Rimuovi istanza]** Rimuove un&#39;istanza del pannello o della riga di tabella ripetibile specificata.

**[!UICONTROL Accedi a]** Consente di passare ad altri <!--Interactive Communications,--> Forms adattivi, ad altre risorse quali immagini o frammenti di documenti o a un URL esterno. <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

### [!UICONTROL Imposta valore di] {#set-value-of}

Il tipo di regola **[!UICONTROL Imposta valore di]** consente di impostare il valore di un oggetto modulo a seconda che la condizione specificata sia soddisfatta o meno. Il valore può essere impostato sul valore di un altro oggetto, una stringa letterale, un valore derivato da un&#39;espressione matematica o una funzione, un valore di una proprietà di un altro oggetto o l&#39;output di un servizio del modello di dati modulo. Analogamente, è possibile verificare la presenza di una condizione su un componente, una stringa, una proprietà o valori derivati da una funzione o un&#39;espressione matematica.

Il tipo di regola **Imposta valore di** non è disponibile per tutti gli oggetti modulo, ad esempio pannelli e pulsanti della barra degli strumenti. Una regola Set Value Of standard ha la seguente struttura:

Imposta il valore dell&#39;oggetto A su:

(stringa ABC) OPPURE
(proprietà dell&#39;oggetto X dell&#39;oggetto C) OPPURE
(valore da una funzione) OPPURE
(valore da un&#39;espressione matematica) OPPURE
(valore di output di un servizio di modello dati o di un servizio web);

Quando (facoltativo):

(Condizione 1 AND Condizione 2 AND Condizione 3) è TRUE;

Nell&#39;esempio seguente il valore nel campo `dependentid` viene utilizzato come input e il valore del campo `Relation` viene impostato sull&#39;output dell&#39;argomento `Relation` del servizio Modello dati modulo `getDependent`.

![Set-value-web-service](assets/set-value-web-service1.png)

Esempio di regola Imposta valore tramite il servizio Modello dati modulo

>[!NOTE]
>
>Inoltre, è possibile utilizzare Imposta valore della regola per compilare tutti i valori in un componente elenco a discesa dall’output di un servizio Modello dati modulo o di un servizio web. Verificare tuttavia che l&#39;argomento di output scelto sia di tipo matrice. Tutti i valori restituiti in un array diventano disponibili nell’elenco a discesa specificato.

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

### [!UICONTROL Imposta Opzioni Di] {#setoptionsof}

Il tipo di regola **[!UICONTROL Imposta opzioni di]** consente di definire regole per aggiungere caselle di controllo in modo dinamico al modulo adattivo. Per definire la regola è possibile utilizzare un modello dati modulo (FDM) o una funzione personalizzata.

Per definire una regola basata su una funzione personalizzata, selezionare **[!UICONTROL Output funzione]** dall&#39;elenco a discesa e trascinare una funzione personalizzata dalla scheda **[!UICONTROL Funzioni]**. Al modulo adattivo viene aggiunto il numero di caselle di controllo definite nella funzione personalizzata.

![Funzioni personalizzate](assets/custom_functions_set_options_new.png)

Per creare una funzione personalizzata, vedere [funzioni personalizzate nell&#39;editor di regole](#custom-functions).

Per definire una regola basata su un modello dati modulo (FDM):

1. Selezionare **[!UICONTROL Output servizio]** dall&#39;elenco a discesa.
1. Seleziona l’oggetto modello dati.
1. Selezionare una proprietà oggetto modello dati dall&#39;elenco a discesa **[!UICONTROL Valore visualizzato]**. Il numero di caselle di controllo nel modulo adattivo è derivato dal numero di istanze definite per tale proprietà nel database.
1. Selezionare una proprietà dell&#39;oggetto modello dati dall&#39;elenco a discesa **[!UICONTROL Salva valore]**.

![Opzioni set FDM](assets/fdm_set_options_new.png)

## Interfaccia utente dell’editor di regole {#understanding-the-rule-editor-user-interface}

L’editor di regole fornisce un’interfaccia utente completa ma semplice per scrivere e gestire le regole. Puoi avviare l’interfaccia utente dell’editor di regole da un modulo adattivo in modalità di authoring.

Per avviare l’interfaccia utente dell’editor di regole:

1. Apri un modulo adattivo in modalità di authoring.
1. Selezionare l&#39;oggetto modulo per il quale si desidera scrivere una regola e nella barra degli strumenti del componente selezionare ![edit-rules](assets/edit-rules-icon.svg). Viene visualizzata l’interfaccia utente dell’editor di regole.

   ![create-rules](assets/create-rules1.png)

   Tutte le regole esistenti sugli oggetti modulo selezionati sono elencate in questa visualizzazione. Per informazioni sulla gestione delle regole esistenti, vedere [Gestire le regole](rule-editor.md#p-manage-rules-p).

1. Seleziona **[!UICONTROL Crea]** per scrivere una nuova regola. L’editor visivo dell’interfaccia utente dell’editor di regole si apre per impostazione predefinita quando si avvia l’editor di regole la prima volta.

   ![Interfaccia utente editor regole](assets/rule-editor-ui1.png)

Esaminiamo in dettaglio ogni componente dell’interfaccia utente dell’editor di regole.

### A. Visualizzazione delle regole dei componenti {#a-component-rule-display}

Visualizza il titolo dell&#39;oggetto modulo adattivo tramite il quale è stato avviato l&#39;editor di regole e il tipo di regola attualmente selezionato. Nell’esempio precedente, l’editor di regole viene avviato da un oggetto Modulo adattivo denominato Stipendio e il tipo di regola selezionato è Quando.

### B. Oggetti e funzioni del modulo {#b-form-objects-and-functions-br}

Il riquadro a sinistra nell&#39;interfaccia utente dell&#39;editor di regole include due schede: **[!UICONTROL Oggetti Forms]** e **[!UICONTROL Funzioni]**.

La scheda Oggetti modulo mostra una vista gerarchica di tutti gli oggetti contenuti nel modulo adattivo. Visualizza il titolo e il tipo degli oggetti. Durante la scrittura di una regola, è possibile trascinare gli oggetti modulo nell’editor di regole. Quando si trascina un oggetto o una funzione in un segnaposto durante la creazione o la modifica di una regola, il segnaposto assume automaticamente il tipo di valore appropriato.

Gli oggetti modulo a cui sono applicate una o più regole valide sono contrassegnati da un punto verde. Se una delle regole applicate a un oggetto modulo non è valida, l&#39;oggetto modulo viene contrassegnato con un punto giallo.

La scheda Funzioni include un set di funzioni incorporate, ad esempio Somma di, Min di, Max di, Media di, Numero di e Convalida modulo. È possibile utilizzare queste funzioni per calcolare i valori nei pannelli e nelle righe di tabella ripetibili e utilizzarli nelle istruzioni di azione e condizione durante la scrittura delle regole. Tuttavia, puoi anche creare [funzioni personalizzate](#custom-functions).

![Scheda Funzioni](assets/functions1.png)

>[!NOTE]
>
>È possibile eseguire la ricerca di testo su oggetti e funzioni, nomi e titoli nelle schede Oggetti e funzioni di Forms.

Nell&#39;albero sinistro degli oggetti modulo è possibile selezionare gli oggetti modulo per visualizzare le regole applicate a ciascuno degli oggetti. Non solo è possibile spostarsi tra le regole dei vari oggetti modulo, ma è anche possibile copiare e incollare le regole tra gli oggetti modulo. Per ulteriori informazioni, vedere [Copiare e incollare le regole](rule-editor.md#p-copy-paste-rules-p).

### C. Attivazione/disattivazione di funzioni e oggetti modulo {#c-form-objects-and-functions-toggle-br}

Quando viene toccato questo pulsante di attivazione, diventa attivo il riquadro Oggetti modulo o il riquadro Funzioni.

### D. Editor di regole visive {#visual-rule-editor}

L’editor di regole visive è l’area in cui si scrivono le regole nella modalità editor visivo dell’interfaccia utente dell’editor di regole. Ti consente di selezionare un tipo di regola e di definire di conseguenza condizioni e azioni. Quando si definiscono condizioni e azioni in una regola, è possibile trascinare gli oggetti modulo e le funzioni dal riquadro Oggetti modulo e funzioni.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;editor di regole visive, vedere [Scrivere regole](rule-editor.md#p-write-rules-p).
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and conversely, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E. Tasti Done e cancel {#done-and-cancel-buttons}

Il pulsante **[!UICONTROL Fine]** viene utilizzato per salvare una regola. È possibile salvare una regola incompleta. Tuttavia, i dati incompleti non sono validi e non vengono eseguiti. Le regole salvate su un oggetto modulo vengono elencate quando si avvia l’editor di regole la prossima volta dallo stesso oggetto modulo. Puoi gestire le regole esistenti in tale vista. Per ulteriori informazioni, vedere [Gestione regole](rule-editor.md#p-manage-rules-p).

Il pulsante **[!UICONTROL Annulla]** elimina le modifiche apportate a una regola e chiude l&#39;editor di regole.

## Scrivi regole {#write-rules}

Puoi scrivere regole utilizzando l’editor di regole visive.

Vediamo innanzitutto come scrivere regole utilizzando l’editor visivo.

### Utilizzo dell’editor visivo {#using-visual-editor}

Comprendiamo come creare una regola nell’editor visivo utilizzando il seguente modulo di esempio.

![Crea-regola-esempio](assets/create-rule-example.png)

La sezione Requisiti del prestito nell&#39;esempio di modulo di domanda di prestito richiede ai richiedenti di specificare il loro stato civile, lo stipendio e, in caso di matrimonio, lo stipendio del coniuge. In base agli input dell’utente, la regola calcola l’importo di idoneità al prestito e viene visualizzata nel campo Idoneità al prestito. Per implementare lo scenario, applica le seguenti regole:

* Il campo Stipendio coniuge viene visualizzato solo quando lo stato civile è sposato.
* L’importo di ammissibilità al prestito è pari al 50% dello stipendio totale.

Per scrivere regole, esegui i seguenti passaggi:

1. Innanzitutto, scrivi la regola per controllare la visibilità del campo Stipendio coniuge in base all’opzione selezionata dall’utente per il pulsante di opzione Stato civile.

   Apri il modulo di richiesta di prestito in modalità di creazione. Selezionare il componente **[!UICONTROL Stato civile]** e selezionare ![edit-rules](assets/edit-rules-icon.svg). Quindi, seleziona **[!UICONTROL Crea]** per avviare l&#39;editor di regole.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   Quando si avvia l&#39;editor di regole, la regola When è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, Stato civile) da cui è stato avviato l&#39;editor di regole è specificato nell&#39;istruzione When.

   Sebbene non sia possibile modificare l&#39;oggetto selezionato, è possibile utilizzare l&#39;elenco a discesa delle regole, come illustrato di seguito, per selezionare un altro tipo di regola. Se desideri creare una regola su un altro oggetto, seleziona Annulla per uscire dall’editor di regole e riavviarlo dall’oggetto modulo desiderato.

1. Seleziona l&#39;elenco a discesa **[!UICONTROL Seleziona stato]** e seleziona **[!UICONTROL è uguale a]**. Viene visualizzato il campo **[!UICONTROL Enter a String]**.

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   Nel pulsante di opzione Stato civile, alle opzioni **[!UICONTROL Sposato]** e **[!UICONTROL Singolo]** sono assegnati rispettivamente i valori **0** e **1**. È possibile verificare i valori assegnati nella scheda Titolo della finestra di dialogo Modifica pulsante di opzione, come illustrato di seguito.

   ![Valori pulsante di opzione dall&#39;editor regole](assets/radio-button-values.png)

1. Nel campo **[!UICONTROL Immettere una stringa]** nella regola, specificare **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   La condizione è stata definita come `When Marital Status is equal to Married`. Quindi, definisci l’azione da eseguire se questa condizione è True.

1. Nell&#39;istruzione Then, selezionare **[!UICONTROL Show]** dal menu a discesa **[!UICONTROL Select Action]**.

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. Trascina il campo **[!UICONTROL Stipendio coniuge]** dalla scheda Oggetti modulo del campo **[!UICONTROL Rilascia oggetto o seleziona qui]**. In alternativa, selezionare il campo **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** e selezionare il campo **[!UICONTROL Stipendio coniuge]** dal menu a comparsa, che elenca tutti gli oggetti modulo nel modulo.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   La regola viene visualizzata come segue nell’editor di regole.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

1. Per salvare la regola, fai clic su **[!UICONTROL Fine]**.

1. Ripetere i passaggi da 1 a 5 per definire un&#39;altra regola per nascondere il campo Stipendio coniuge se lo stato civile è Singolo. La regola viene visualizzata come segue nell’editor di regole.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >In alternativa, è possibile scrivere una regola Mostra nel campo Stipendio coniuge, anziché due regole Quando nel campo Stato civile, per implementare lo stesso comportamento.

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. Scrivere quindi una regola per calcolare l&#39;importo dell&#39;idoneità al prestito, che corrisponde al 50% dello stipendio totale, e visualizzarlo nel campo Idoneità al prestito. Per ottenere questo risultato, crea **[!UICONTROL Imposta il valore di]** regole nel campo Idoneità al prestito.

   In modalità creazione, seleziona il campo **[!UICONTROL Idoneità prestito]** e seleziona ![modifica-regole](assets/edit-rules-icon.svg). Quindi, seleziona **[!UICONTROL Crea]** per avviare l&#39;editor di regole.

1. Selezionare **[!UICONTROL Imposta valore di]** regola dal menu a discesa delle regole.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. Seleziona **[!UICONTROL Seleziona opzione]** e scegli **[!UICONTROL Espressione matematica]**. Si apre un campo in cui scrivere espressioni matematiche.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. Nel campo espressione:

   * Seleziona o trascina dalla scheda Oggetto Forms il campo **[!UICONTROL Stipendio]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   * Seleziona **[!UICONTROL Plus]** dal campo **[!UICONTROL Seleziona operatore]**.

   * Seleziona o trascina dalla scheda Oggetto Forms il campo **[!UICONTROL Stipendio coniuge]** nell&#39;altro campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. Quindi, seleziona nell’area evidenziata intorno al campo espressione e seleziona **[!UICONTROL Estendi espressione]**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   Nel campo espressione estesa, seleziona **[!UICONTROL diviso per]** dal campo **[!UICONTROL Seleziona operatore]** e **[!UICONTROL Numero]** dal campo **[!UICONTROL Seleziona opzione]**. Specificare quindi **[!UICONTROL 2]** nel campo numerico.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >È possibile creare espressioni complesse utilizzando componenti, funzioni, espressioni matematiche e valori di proprietà dal campo Seleziona opzione.

   Quindi, crea una condizione, che quando restituisce True, l’espressione viene eseguita.

1. Selezionare **[!UICONTROL Aggiungi condizione]** per aggiungere un&#39;istruzione When.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   Nell&#39;istruzione When:

   * Seleziona o trascina dalla scheda Oggetto Forms il campo **[!UICONTROL Stato civile]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   * Selezionare **[!UICONTROL è uguale a]** dal campo **[!UICONTROL Seleziona operatore]**.

   * Seleziona Stringa nell&#39;altro **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo e specifica **[!UICONTROL Sposato]** nel campo **[!UICONTROL Immetti una stringa]**.

   La regola viene infine visualizzata come segue nell’editor di regole.  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

1. Seleziona **[!UICONTROL Fine]**. Salva la regola.

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

The code editor JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. These expressions return values of certain types. For the complete list of Adaptive Forms classes, events, objects, and public APIs, see [JavaScript Library API reference for Adaptive Forms](https://helpx.adobe.com/it/experience-manager/6-5/forms/javascript-api/index.html).

For more information about guidelines to write rules in the code editor, see [Adaptive Form Expressions](adaptive-form-expressions.md).

While writing JavaScript code in the rule editor, the following visual cues help you with the structure and syntax:

* Syntax highlights

* Auto Indentation

* Hints and suggestions for Form objects, functions, and their properties

* Auto completion of form component names and common JavaScript functions

![javascriptruleeditor](assets/javascriptruleeditor.png)
-->

#### Funzioni personalizzate nell’editor di regole {#custom-functions}

Oltre alle funzioni predefinite, come *Somma di*, elencate in Output funzioni, è possibile scrivere funzioni personalizzate di cui si ha spesso bisogno. Assicurarsi che la funzione scritta sia accompagnata dal `jsdoc` sopra di essa.

`jsdoc` di accompagnamento è obbligatorio:

* Se desideri una configurazione e una descrizione personalizzate
* Poiché esistono diversi modi per dichiarare una funzione in `JavaScript,` e i commenti consentono di tenere traccia delle funzioni.

L’editor di regole supporta la sintassi JavaScript ES5 per gli script e le funzioni personalizzate.
Per ulteriori informazioni, vedere [jsdoc.app](https://jsdoc.app/).

`jsdoc` tag supportati:

* **Privato**
Sintassi: `@private`
Una funzione privata non è inclusa come funzione personalizzata.

* **Nome**
Sintassi: `@name funcName <Function Name>`
In alternativa `,` puoi utilizzare: `@function funcName <Function Name>` **or** `@func` `funcName <Function Name>`.
  `funcName` è il nome della funzione (non sono consentiti spazi).
  `<Function Name>` è il nome visualizzato della funzione.

* **Membro**
Sintassi: `@memberof namespace`
Associa uno spazio dei nomi alla funzione.

* **Parametro**
Sintassi: `@param {type} name <Parameter Description>`
In alternativa, è possibile utilizzare: `@argument` `{type} name <Parameter Description>` **or** `@arg` `{type}` `name <Parameter Description>`.
Mostra i parametri utilizzati dalla funzione. Una funzione può avere più tag di parametri, uno per ogni parametro in ordine di occorrenza.
  `{type}` rappresenta il tipo di parametro. I tipi di parametri consentiti sono:

   1. stringa
   1. numero
   1. booleano
   1. ambito

  L’ambito fa riferimento ai campi di un modulo adattivo. Quando un modulo utilizza il caricamento lento, è possibile utilizzare `scope` per accedere ai relativi campi. È possibile accedere ai campi quando sono caricati o se sono contrassegnati come globali.

  Tutti i tipi di parametri sono classificati in una delle categorie precedenti. Nessuno non è supportato. Accertati di selezionare uno dei tipi riportati sopra. I tipi non fanno distinzione tra maiuscole e minuscole. Spazi non consentiti nel parametro `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Tipo restituito**
Sintassi: `@return {type}`
In alternativa, è possibile utilizzare `@returns {type}`.
Aggiunge informazioni sulla funzione, ad esempio l&#39;obiettivo.
  {type} rappresenta il tipo restituito della funzione. I tipi restituiti consentiti sono:

   1. stringa
   1. numero
   1. booleano

  Tutti gli altri tipi di reso sono classificati in una delle categorie precedenti. Nessuno non è supportato. Accertati di selezionare uno dei tipi riportati sopra. I tipi restituiti non fanno distinzione tra maiuscole e minuscole.

   * **Questo**
Sintassi: `@this currentComponent`

  Utilizza @this per fare riferimento al componente Modulo adattivo su cui è scritta la regola.

  L’esempio seguente è basato sul valore del campo. Nell&#39;esempio seguente, la regola nasconde un campo nel modulo. La parte `this` di `this.value` fa riferimento al componente del modulo adattivo sottostante, sul quale viene scritta la regola.

  ```
     /**
     * @function myTestFunction
     * @this currentComponent
     * @param {scope} scope in which code inside function is run.
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

1. Crea una libreria client. Per ulteriori informazioni, vedere [Utilizzo di librerie lato client](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=it#developing).
1. In CRXDE, aggiungere una proprietà `categories` con il valore del tipo di stringa `customfunction` alla cartella `clientlib`.

   >[!NOTE]
   >
   >`customfunction` è una categoria di esempio. È possibile scegliere qualsiasi nome per la categoria creata nella cartella `clientlib`.

Dopo aver aggiunto la libreria client nell’archivio CRX, utilizzala nel modulo adattivo. Ti consente di utilizzare la funzione personalizzata come regola nel modulo. Per aggiungere la libreria client nel modulo adattivo, effettua le seguenti operazioni:

1. Apri il modulo in modalità di modifica.
Per aprire un modulo in modalità di modifica, selezionare un modulo e selezionare **[!UICONTROL Apri]**.
1. In modalità di modifica, seleziona un componente, quindi seleziona ![livello campo](assets/select_parent_icon.svg) > **[!UICONTROL Contenitore modulo adattivo]**, quindi seleziona ![cmppr](assets/configure-icon.svg).
1. Nella barra laterale, in Nome della libreria client, aggiungi la libreria client. ( `customfunction` nell&#39;esempio.)

   ![Aggiunta della libreria client della funzione personalizzata](assets/clientlib.png)

1. Selezionare la casella numerica di input e selezionare ![edit-rules](assets/edit-rules-icon.svg) per aprire l&#39;editor di regole.
1. Seleziona **[!UICONTROL Crea regola]**. Utilizzando le opzioni illustrate di seguito, creare una regola per salvare il valore al quadrato dell&#39;input nel campo Output del modulo.

   [![Utilizzo di funzioni personalizzate per creare una regola](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)

1. Seleziona **[!UICONTROL Fine]**. Viene aggiunta la funzione personalizzata.

   >[!NOTE]
   >
   > Per richiamare un modello di dati modulo dall&#39;editor di regole utilizzando funzioni personalizzate, [consulta qui](/help/forms/using-form-data-model.md#invoke-services-in-adaptive-forms-using-rules-invoke-services).

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

**Espressione funzione e istruzione**

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
>Assicurarsi di utilizzare `jsdoc` per ogni funzione personalizzata. Anche se `jsdoc` commenti sono incoraggiati, includi un `jsdoc` commento vuoto per contrassegnare la tua funzione come funzione personalizzata. Consente la gestione predefinita della funzione personalizzata.

### Supporto di funzioni personalizzate nelle espressioni di convalida {#supporting-custom-functions-in-validation-expressions-br}

A volte, se sono presenti **regole di convalida complesse**, lo script di convalida esatto risiede nelle funzioni personalizzate e l&#39;autore chiama tali funzioni personalizzate dall&#39;espressione di convalida del campo. Per rendere nota e disponibile questa libreria di funzioni personalizzata durante l&#39;esecuzione delle convalide lato server, l&#39;autore del modulo può configurare il nome della libreria client di AEM nella scheda **[!UICONTROL Base]** delle proprietà del contenitore di moduli adattivi, come illustrato di seguito.

![Supporto di funzioni personalizzate nelle espressioni di convalida](assets/clientlib-cat.png)

Supporto di funzioni personalizzate nelle espressioni di convalida

L’autore può configurare una libreria JavaScript personalizzata per modulo adattivo. Si consiglia di mantenere solo le funzioni riutilizzabili nella libreria, che dipendono dalle librerie di terze parti jquery e underscore.js.

## Gestione degli errori nell’azione di invio {#error-handling-on-submit-action}

Come parte delle linee guida sulla sicurezza e l’irrigidimento di AEM, configura pagine di errore personalizzate come 400.jsp, 404.jsp e 500.jsp. Questi gestori vengono chiamati quando all’invio di un modulo vengono visualizzati errori 400, 404 o 500. Gli handler vengono chiamati anche quando questi codici di errore vengono attivati sul nodo Publish. Puoi anche creare pagine JSP per altri codici di errore HTTP.

Quando si precompila un modello di dati modulo (FDM) o un modulo adattivo basato su schema con dati XML o JSON a uno schema che non contiene tag `<afData>`, `<afBoundData>` e `</afUnboundData>`, i dati dei campi non limitati del modulo adattivo andranno persi. Lo schema può essere uno schema XML, uno schema JSON o un modello dati modulo (FDM). I campi non limitati sono campi modulo adattivo senza la proprietà `bindref`.

## Gestisci regole {#manage-rules}

Tutte le regole esistenti in un oggetto modulo vengono elencate quando si seleziona l&#39;oggetto e si seleziona ![edit-rules1](assets/edit-rules-icon.svg). Puoi visualizzare il titolo e un’anteprima del riepilogo delle regole. Inoltre, l’interfaccia utente consente di espandere e visualizzare il riepilogo completo delle regole, modificarne l’ordine, modificarne le regole ed eliminarle.

![Regole elenco](assets/list-rules.png)

Puoi eseguire le seguenti azioni sulle regole:

* **Espandi/comprimi**: la colonna Contenuto nell&#39;elenco delle regole visualizza il contenuto della regola. Se l&#39;intero contenuto della regola non è visibile nella visualizzazione predefinita, selezionare ![expand-rule-content](assets/Smock_ChevronDown.svg) per espanderlo.

* **Riordina**: tutte le nuove regole create sono sovrapposte nella parte inferiore dell&#39;elenco di regole. Le regole vengono eseguite dall&#39;alto verso il basso. La regola in alto viene eseguita per prima, seguita da altre regole dello stesso tipo. Ad esempio, se disponi di regole When, Show, Enable e When rispettivamente in prima, seconda, terza e quarta posizione dall&#39;alto, la regola When nella parte superiore viene eseguita per prima seguita dalla regola When nella quarta posizione. Vengono quindi eseguite le regole Mostra e Abilita.
È possibile modificare l&#39;ordine di una regola toccando ![sort-rules](assets/sort-rules.svg) o trascinandola nell&#39;ordine desiderato nell&#39;elenco.

* **Modifica**: per modificare una regola, selezionare la casella di controllo accanto al titolo della regola. Vengono visualizzate le opzioni per modificare ed eliminare la regola. Seleziona **[!UICONTROL Modifica]** per aprire la regola selezionata nell&#39;editor regole <!-- in visual  or code editor mode depending on the mode used to create the rule -->.

* **Elimina**: per eliminare una regola, selezionarla e selezionare **[!UICONTROL Elimina]**.

* **Attiva/Disattiva**: quando è necessario sospendere temporaneamente l&#39;utilizzo di una regola, è possibile selezionare una o più regole e selezionare **[!UICONTROL Disattiva]** nella barra degli strumenti Azioni per disattivarle. Se una regola è disabilitata, non viene eseguita in fase di esecuzione. Per abilitare una regola disabilitata, selezionala e seleziona Abilita nella barra degli strumenti delle azioni. La colonna di stato della regola indica se la regola è abilitata o disabilitata.

![Disabilita regola](assets/disablerule.png)

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

1. Per salvare la regola, fai clic su **[!UICONTROL Fine]**.

## Espressioni nidificate {#nestedexpressions}

L’editor di regole consente di utilizzare più operatori AND e OR per creare regole nidificate. È possibile combinare più operatori AND e OR nelle regole.

Di seguito è riportato un esempio di regola nidificata che visualizza un messaggio per l’utente sull’idoneità per la custodia di un bambino quando vengono soddisfatte le condizioni richieste.

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

* Un pulsante di scelta, **[!UICONTROL Sei un cliente Geometrixx esistente?]**, che fornisce [!UICONTROL Sì] e [!UICONTROL No] opzioni. Il valore per Sì è **0** e No è **1**.

* Campo di testo, **[!UICONTROL ID cliente Geometrixx]**, per specificare l&#39;ID cliente.

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

Regola nell’editor visivo

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->