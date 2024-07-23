---
title: Come si utilizza l’editor di regole per aggiungere regole ai campi modulo per aggiungere un comportamento dinamico e creare una logica complessa in un modulo adattivo basato su componenti core?
description: L’editor di regole di Forms adattivo consente di aggiungere un comportamento dinamico e di creare una logica complessa nei moduli senza codificare o scrivere script.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 1292f729-c6eb-4e1b-b84c-c66c89dc53ae
source-git-commit: 780c68f0c21ef94ff6a73ce991370100b1a88db9
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 4%

---


# Introduzione all’editor di regole per moduli adattivi basati su componenti core

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service (Componenti core) | Questo articolo |
| AEM as a Cloud Service (Componenti di base) | [Fai clic qui](/help/forms/rule-editor.md) |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html) |

In un modulo adattivo basato su componenti core, la funzione dell’editor di regole consente sia agli utenti aziendali che agli sviluppatori di scrivere regole per gli oggetti del modulo adattivo. Queste regole definiscono le azioni da attivare sugli oggetti modulo in base a condizioni preimpostate, input dell&#39;utente e azioni dell&#39;utente sul modulo. Questa funzionalità consente di semplificare ulteriormente l&#39;esperienza di compilazione dei moduli, garantendo precisione e velocità.

L’editor di regole fornisce un’interfaccia utente intuitiva e semplificata per la scrittura di regole. Offre un editor visivo che soddisfa tutti gli utenti, consentendo loro di creare e gestire regole senza necessità di conoscenze tecniche approfondite. Questo approccio visivo consente agli utenti di comprendere e implementare più facilmente la logica desiderata all’interno dei moduli.

Alcune delle azioni chiave che è possibile eseguire sugli oggetti Modulo adattivo utilizzando le regole sono:

* Mostrare o nascondere un oggetto
* Attivare o disattivare un oggetto
* Impostare un valore per un oggetto
* Convalidare il valore di un oggetto
* Eseguire funzioni per calcolare il valore di un oggetto
* Richiamare un modello dati del modulo (FDM) ed eseguire un’operazione
* Impostare la proprietà di un oggetto

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Gli utenti aggiunti al gruppo `forms-power-users` possono creare script e modificare quelli esistenti. Gli utenti del gruppo [!DNL forms-users] possono utilizzare gli script ma non crearli o modificarli.

Per un confronto dettagliato, consulta l&#39;articolo [Differenza tra l&#39;editor di regole di Foundation e l&#39;editor di regole dei componenti core](/help/forms/rule-editor-core-components-difference-tables.md).

<!--
## Difference between Rule editor in Core Components and Rule Editor in Foundation Components

{{rule-editor-diff}}

>[!NOTE]
>
> To see how to create and use custom functions in detail, refer to [Custom functions in Adaptive Forms (Core Components)](/help/forms/create-and-use-custom-functions.md) article.

-->

## Informazioni su una regola {#understanding-a-rule}

Una regola è una combinazione di azioni e condizioni. Nell’editor delle regole, le azioni includono attività quali nascondere, mostrare, abilitare, disabilitare o calcolare il valore di un oggetto in un modulo. Le condizioni sono espressioni booleane che vengono valutate eseguendo controlli e operazioni sullo stato, sul valore o sulla proprietà di un oggetto modulo. Le azioni vengono eseguite in base al valore ( `True` o `False`) restituito valutando una condizione.

L’editor di regole fornisce un set di tipi di regole predefiniti, ad esempio Quando, Mostra, Nascondi, Abilita, Disabilita, Imposta valore di e Convalida, per facilitare la scrittura delle regole. Ogni tipo di regola ti consente di definire condizioni e azioni in una regola. Il documento spiega ulteriormente ogni tipo di regola nei dettagli.

Una regola segue in genere uno dei seguenti costrutti:

**Condizione-Azione** In questo costrutto, una regola definisce innanzitutto una condizione seguita da un&#39;azione da attivare. Il costrutto è paragonabile all’istruzione if-then nei linguaggi di programmazione.

Nell&#39;editor di regole, il tipo di regola **When** applica il costrutto condizione-azione.

**Action-Condition** In questo costrutto, una regola definisce innanzitutto un&#39;azione da attivare seguita da condizioni per la valutazione. Un’altra variante di questo costrutto è action-condition-alternate action, che definisce anche un’azione alternativa da attivare se la condizione restituisce False.

I tipi di regola Mostra, Nascondi, Abilita, Disabilita, Imposta valore di e Convalida nell&#39;editor di regole applicano il costrutto regola della condizione azione. Per impostazione predefinita, l&#39;azione alternativa per Mostra è Nascondi e per Abilita è Disabilita e viceversa. Non è possibile modificare l&#39;azione alternativa predefinita.

>[!NOTE]
>
>I tipi di regole disponibili, incluse le condizioni e le azioni definite nell&#39;editor di regole, dipendono anche dal tipo di oggetto modulo in base al quale si sta creando una regola. Nell&#39;editor delle regole vengono visualizzati solo i tipi di regole e le opzioni validi per la scrittura di istruzioni di condizione e azione per un particolare tipo di oggetto modulo. Ad esempio, non vengono visualizzati i tipi Convalida e Imposta valore di per un oggetto pannello.

Per ulteriori informazioni sui tipi di regole disponibili nell&#39;editor di regole, vedere [Tipi di regole disponibili nell&#39;editor di regole](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### Linee guida per la scelta di un costrutto regola {#guidelines-for-choosing-a-rule-construct}

Sebbene sia possibile ottenere la maggior parte dei casi d’uso utilizzando qualsiasi costrutto di regola, di seguito sono riportate alcune linee guida per scegliere un costrutto rispetto a un altro. Per ulteriori informazioni sulle regole disponibili nell&#39;editor di regole, vedere [Tipi di regole disponibili nell&#39;editor di regole](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* Una regola tipica del pollice durante la creazione di una regola è pensarla nel contesto dell&#39;oggetto su cui si sta scrivendo una regola. Si supponga di voler nascondere o visualizzare il campo B in base al valore specificato dall&#39;utente nel campo A. In questo caso, si sta valutando una condizione nel campo A e, in base al valore restituito, si sta attivando un&#39;azione nel campo B.

  Pertanto, se si sta scrivendo una regola nel campo B (l&#39;oggetto su cui si sta valutando una condizione), utilizzare il costrutto condizione-azione o il tipo di regola When. Allo stesso modo, utilizza il costrutto action-condition o il tipo di regola Show o Hide sul campo A.

* A volte, è necessario eseguire più azioni in base a una condizione. In questi casi, si consiglia di utilizzare il costrutto condizione-azione. In questo costrutto, puoi valutare una condizione una sola volta e specificare più istruzioni di azione.

  Ad esempio, per nascondere i campi B, C e D in base alla condizione che verifica il valore specificato dall&#39;utente nel campo A, scrivere una regola con il costrutto condizione-azione o il tipo di regola When nel campo A e specificare azioni per controllare la visibilità dei campi B, C e D. In caso contrario, sono necessarie tre regole separate per i campi B, C e D, in cui ogni regola controlla la condizione e mostra o nasconde il rispettivo campo. In questo esempio, è più efficiente scrivere il tipo di regola When su un oggetto anziché il tipo di regola Show o Hide su tre oggetti.

* Per attivare un’azione in base a più condizioni, si consiglia di utilizzare un costrutto azione-condizione. Ad esempio, per mostrare e nascondere il campo A valutando le condizioni nei campi B, C e D, utilizzare il tipo di regola Mostra o Nascondi nel campo A.
* Utilizza il costrutto condizione-azione o condizione azione se la regola contiene un’azione per una condizione.
* Se una regola verifica la presenza di una condizione ed esegue immediatamente un&#39;azione quando fornisce un valore in un campo o esce da un campo, si consiglia di scrivere una regola con un costrutto condizione-azione o il tipo di regola When nel campo in cui viene valutata la condizione.
* La condizione nella regola When viene valutata quando un utente modifica il valore dell&#39;oggetto su cui viene applicata la regola When. Tuttavia, se desideri che l’azione si attivi quando il valore cambia sul lato server, come per il prepopolamento del valore, è consigliabile scrivere una regola When che attivi l’azione quando il campo viene inizializzato.
* Quando si scrivono regole per gli oggetti menu a discesa, pulsanti di scelta o caselle di controllo, le opzioni o i valori di tali oggetti modulo nel modulo vengono precompilati nell’editor di regole.

## Passaggio successivo

Per informazioni su come utilizzare l&#39;interfaccia utente per scrivere e gestire regole in un editor di regole, consulta l&#39;articolo [Interfaccia utente dell&#39;editor di regole per Forms adattivo basato su Componenti core](/help/forms/rule-editor-core-components-user-interface.md).

## Consulta anche

{{see-also-rule-editor}}