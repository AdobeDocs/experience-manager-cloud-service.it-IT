---
title: Configurazione della segmentazione con ContextHub
description: Scopri come configurare la segmentazione utilizzando ContextHub.
exl-id: fbc38611-dbee-426e-b823-df64b6730c45
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 87%

---

# Configurazione della segmentazione con ContextHub{#configuring-segmentation-with-contexthub}

La segmentazione è un concetto chiave per la creazione di una campagna. Consulta [Informazioni sulla segmentazione](segmentation.md) per saperne di più sul funzionamento della segmentazione e sui termini chiave.

Definisci i segmenti e le strategie necessari per i contenuti di destinazione in base alle informazioni già raccolte sui visitatori del tuo sito e agli obiettivi che desideri raggiungere.

Questi segmenti verranno poi utilizzati per fornire al visitatore i contenuti di destinazione più pertinenti. Le [Attività](activities.md) qui definite possono essere incluse in qualsiasi pagina e definiscono a quale segmento visitatore è applicabile il contenuto specifico.

L’AEM ti consente di personalizzare facilmente le esperienze degli utenti. Consente inoltre di verificare i risultati delle definizioni dei segmenti.

## Accesso ai segmenti {#accessing-segments}

La console [Tipi di pubblico](audiences.md) viene utilizzata sia per gestire i segmenti per ContextHub, sia i tipi di pubblico per il tuo account Adobe Target. La presente documentazione riguarda la gestione dei segmenti per ContextHub.

Per accedere ai segmenti, nella navigazione globale seleziona **Navigazione > Personalizzazione > Tipi di pubblico**. Seleziona la configurazione (ad esempio, Sito WKND) per visualizzare i segmenti:

![Gestione tipi di pubblico](../assets/contexthub-segmentation-audiences.png)

## Editor segmento {#segment-editor}

<!--The **Segment Editor** lets you easily modify a segment. To edit a segment, select a segment in the [list of segments](/help/sites-administering/segmentation.md#accessing-segments) and click the **Edit** button.-->
Il **Editor segmento** consente di modificare facilmente un segmento. Per modificare un segmento, selezionalo dall’elenco dei segmenti e fai clic sul pulsante **Modifica**.

![Editor segmento](../assets/contexthub-segment-editor.png)

Tramite il browser Componenti puoi aggiungere i contenitori **AND** e **OR** per definire la logica del segmento. In seguito puoi aggiungere altri componenti per confrontare proprietà e valori o script di riferimento e altri segmenti per definire i criteri di selezione (consulta [Creazione di un nuovo segmento](#creating-a-new-segment)) per definire lo scenario esatto per la selezione del segmento.

Quando l’intera istruzione restituisce “True”, significa che il segmento è stato risolto. Nel caso in cui siano applicabili più segmenti, viene utilizzato anche il fattore **Incremento**. Per informazioni dettagliate sul fattore di incremento, consulta [Creazione di un nuovo segmento](#creating-a-new-segment).

>[!CAUTION]
>
>L’editor segmento non verifica la presenza di riferimenti circolari. Ad esempio, il segmento A fa riferimento a un altro segmento B, che a sua volta fa riferimento al segmento A. È necessario assicurarsi che i segmenti non contengano riferimenti circolari.

### Contenitori {#containers}

I seguenti contenitori sono predefiniti e consentono di raggruppare confronti e riferimenti per la valutazione boolean. Possono essere trascinati dal browser Componenti all’editor. Per ulteriori informazioni, consulta la sezione seguente [Utilizzo dei contenitori AND e OR](#using-and-and-or-containers).

|  |  |
|---|---|
| Contenitore AND | Operatore AND boolean |
| Contenitore OR | Operatore OR boolean |

### Confronti {#comparisons}

Per valutare le proprietà dei segmenti sono disponibili i seguenti confronti di segmenti predefiniti. Possono essere trascinati dal browser Componenti all’editor.

|  |  |
|---|---|
| Property-Value (Proprietà-Valore) | Confronta una proprietà di un archivio con un valore definito |
| Property-Property (Proprietà-Proprietà) | Confronta una proprietà di un archivio con un’altra proprietà |
| Riferimento Property-Segment (Proprietà-Segmento) | Confronta una proprietà di un archivio con un altro segmento di riferimento |
| Riferimento Property-Script (Proprietà-Script) | Confronta una proprietà di un archivio con i risultati di uno script |
| Segment Reference-Script Reference (Riferimento segmento-Riferimento script) | Confronta un segmento di riferimento ai risultati di uno script |

>[!NOTE]
>
>Quando si confrontano i valori, se il tipo di dati del confronto non è impostato (cioè è impostato sul rilevamento automatico), il motore di segmentazione di ContextHub si limiterà a confrontare i valori allo stesso modo di Javascript. Non effettua l’assegnazione dei valori ai tipi previsti, il che può portare a risultati fuorvianti. Esempio:
>
>`null < 30 // will return true`
>
>Pertanto quando procedi alla [creazione di un segmento](#creating-a-new-segment) devi selezionare un **tipo di dati** ogni volta che sono noti i tipi di valori confrontati. Esempio:
>
>Quando confronti la proprietà `profile/age`, sai già che il tipo confrontato sarà un **numero**, perciò anche se `profile/age` non è impostato, un confronto `profile/age` minore di 30 restituirà **False (Falso)**, come prevedibile.

### Riferimenti {#references}

Sono disponibili i seguenti riferimenti predefiniti per eseguire un collegamento diretto a uno script o a un altro segmento. Possono essere trascinati dal browser Componenti all’editor.

|  |  |
|---|---|
| Riferimento segmento | Valuta il segmento di riferimento |
| Riferimento script | Valuta lo script di riferimento. Per ulteriori informazioni, consulta la sezione seguente [Utilizzo di riferimenti a script](#using-script-references). |

## Creazione di un nuovo segmento {#creating-a-new-segment}

Per definire il nuovo segmento:

1. Dopo l’[accesso ai segmenti](#accessing-segments), [passa alla cartella](#organizing-segments) in cui desideri creare il segmento.

1. Seleziona la **Crea** e seleziona **Crea segmento ContextHub**.

   ![Aggiungi segmento](../assets/contexthub-create-segment.png)

1. In **Nuovo segmento ContextHub**, immetti un titolo per il segmento e un valore di incremento, se necessario, quindi seleziona **Crea**.

   ![Nuovo segmento](../assets/contexthub-new-segment.png)

   Ogni segmento ha un parametro di incremento utilizzato come fattore di ponderazione. Un valore più elevato determina la selezione del segmento, preferendolo a un segmento con un valore inferiore nelle istanze in cui sono validi più segmenti.

   * Valore minimo: `0`
   * Valore massimo: `1000000`

1. Dalla console dei segmenti, modifica il segmento creato per aprirlo nell’editor segmento.
1. Trascina un confronto o un riferimento nell’editor segmento per visualizzarlo nel contenitore AND predefinito.
1. Selezionate due volte l&#39;opzione di configurazione del nuovo riferimento o segmento per modificare i parametri specifici. In questo esempio, effettuiamo i test per le persone a Basilea.

   ![Test per le persone a Basilea](../assets/contexthub-comparing-property-value.png)

   Imposta sempre un **Tipo di dati** se possibile, per garantire che i confronti siano valutati correttamente. Per ulteriori informazioni, consulta [Confronti](#comparisons).

1. Fai clic su **Fine** per salvare la definizione:
1. Aggiungi altri componenti in base alle esigenze. Puoi formulare espressioni boolean utilizzando i componenti contenitore per i confronti AND e OR (vedi di seguito [Utilizzo dei contenitori AND e OR](#using-and-and-or-containers)). Con l’editor segmento è possibile eliminare i componenti non più necessari o trascinarli in nuove posizioni all’interno dell’istruzione.

### Utilizzo dei contenitori AND e OR {#using-and-and-or-containers}

Utilizzando i componenti contenitore AND e OR, puoi costruire segmenti complessi in AEM. Questa operazione richiede di tenere presenti alcuni punti fondamentali:

* Il livello principale della definizione è sempre il contenitore AND creato inizialmente. Questo non può essere modificato, ma non ha effetti sul resto della definizione del segmento.
* Assicurati che la nidificazione del contenitore abbia una logica. I contenitori possono essere visualizzati come parentesi dell’espressione boolean.

L’esempio seguente viene utilizzato per selezionare i visitatori considerati nel nostro gruppo target in Svizzera:

```text
 People in Basel

 OR

 People in Zürich
```

Per iniziare, inserisci un componente contenitore OR all’interno del contenitore AND predefinito. All’interno del contenitore OR puoi aggiungere la proprietà o i componenti di riferimento.

![Segmento con operatore OR](../assets/contexthub-or-operator.png)

È possibile nidificare più operatori AND e OR, a seconda delle necessità.

### Utilizzo di riferimenti a script {#using-script-references}

Utilizzando il componente Riferimento script, è possibile delegare la valutazione di una proprietà di segmento a uno script esterno. Una volta configurato correttamente lo script, può essere utilizzato come qualsiasi altro componente di una condizione di segmento.

#### Definizione di uno script a cui fare riferimento {#defining-a-script-to-reference}

1. Aggiungi file alla libreria client `contexthub.segment-engine.scripts`.
1. Implementa una funzione che restituisca un valore. Esempio:

   ```javascript
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. Registra lo script con `ContextHub.SegmentEngine.ScriptManager.register`.

Se lo script dipende da proprietà aggiuntive, lo script deve chiamare `this.dependOn()`. Ad esempio, se lo script dipende da `profile/age`:

```javascript
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### Riferimento a uno script {#referencing-a-script}

1. Crea un segmento ContextHub.
1. Aggiungi il componente **Riferimento script** nella posizione desiderata del segmento.
1. Apri la finestra di dialogo di modifica del componente **Riferimento script**. Se [configurato correttamente](#defining-a-script-to-reference), lo script deve essere disponibile nell’elenco a discesa **Nome script**.

## Organizzazione dei segmenti {#organizing-segments}

Se disponi di molti segmenti, la gestione in un elenco semplice può essere complicata. In questi casi, può essere utile creare alcune cartelle per gestire i tuoi segmenti.

### Crea una nuova cartella,  {#create-folder}

1. Dopo [accesso ai segmenti](#accessing-segments), seleziona la **Crea** e seleziona **Cartella**.

   ![Aggiungi cartella](../assets/contexthub-create-segment.png)

1. Specifica il **titolo** e il **nome** da assegnare alla cartella.
   * Il **titolo** deve essere descrittivo.
   * Il **nome** diventa il nome del nodo nell’archivio.
      * Viene generato automaticamente dal titolo, secondo le [convenzioni di denominazione di AEM](/help/implementing/developing/introduction/naming-conventions.md).
      * Se necessario è possibile modificarlo.

   ![Crea cartella](../assets/contexthub-create-folder.png)

1. Seleziona **Crea**.

   ![Conferma cartella](../assets/contexthub-confirm-folder.png)

1. La cartella verrà visualizzata nell’elenco dei segmenti.
   * L’ordinamento delle colonne incide sulla posizione di visualizzazione della nuova cartella nell’elenco.
   * È possibile selezionare le intestazioni di colonna per modificare l&#39;ordinamento.
     ![La nuova cartella](../assets/contexthub-folder.png)

### Modificare le cartelle esistenti {#modify-folders}

1. Dopo [accesso ai segmenti](#accessing-segments), seleziona la cartella da modificare per selezionarla.

   ![Selezione cartella](../assets/contexthub-select-folder.png)

1. Seleziona **Rinomina** nella barra degli strumenti per rinominare la cartella.

1. Fornisci un nuovo **Titolo cartella** e seleziona **Salva**.

   ![Rinomina cartella](../assets/contexthub-rename-folder.png)

>[!NOTE]
>
>Quando rinomini una cartella, è possibile modificare solo il titolo. Il nome non può essere modificato.

### Eliminare una cartella

1. Dopo [accesso ai segmenti](#accessing-segments), seleziona la cartella da modificare per selezionarla.

   ![Selezione cartella](../assets/contexthub-select-folder.png)

1. Seleziona **Elimina** nella barra degli strumenti per eliminare la cartella.

1. Una finestra di dialogo riporta un elenco di cartelle selezionate per l’eliminazione.

   ![Conferma eliminazione](../assets/contexthub-confirm-segment-delete.png)

   * Seleziona **Elimina** per confermare.
   * Seleziona **Annulla** per interrompere.

1. Se una delle cartelle selezionate contiene sottocartelle o segmenti, devi confermarne l’eliminazione.

   ![Conferma l’eliminazione degli elementi figlio](../assets/contexthub-confirm-segment-child-delete.png)

   * Seleziona **Forza eliminazione** per confermare.
   * Seleziona **Annulla** per interrompere.

>[!NOTE]
>
> Non è possibile spostare un segmento da una cartella all’altra.

## Test dell’applicazione di un segmento {#testing-the-application-of-a-segment}

Una volta definito il segmento, è possibile testare i risultati potenziali con l’ausilio di **[ContextHub](contexthub.md).**

1. Visualizza l’anteprima di una pagina
1. Fai clic sull’icona ContextHub per visualizzare la barra degli strumenti di ContextHub
1. Seleziona un utente che corrisponda al segmento creato
1. ContextHub risolverà i segmenti applicabili per l’utente tipo selezionato

Ad esempio, la definizione del segmento semplice per identificare gli utenti a Basilea si basa sulla posizione dell’utente. Il caricamento di un utente tipo specifico che corrisponde a tali criteri mostra se il segmento è stato risolto correttamente:

![Segmento che risolve](../assets/contexthub-segment-resolve.png)

Oppure, se non è risolto:

![Segmento che non risolve](../assets/contexthub-segment-doesnt-resolve.png)

>[!NOTE]
>
>Tutte le caratteristiche vengono risolte immediatamente, anche se la maggior parte si modifica solamente quando la pagina viene ricaricata.

Tali test possono essere eseguiti anche sulle pagine di contenuto e in combinazione con contenuti mirati e **Attività** ed **Esperienze** correlate.

Se hai impostato un’attività e un’esperienza, puoi testare facilmente il segmento con l’attività. Per informazioni dettagliate sulla configurazione di un’attività, consulta la [documentazione sull’authoring di contenuti di destinazione](targeted-content.md).

1. In modalità di modifica di una pagina in cui hai impostato il contenuto di destinazione, è possibile vedere che il contenuto è indirizzato tramite l’icona a forma di freccia su di esso.
1. Passa alla modalità anteprima e utilizza ContextHub, passa a un utente tipo che non corrisponde alla segmentazione configurata per l’esperienza.
1. Passa a un utente tipo che non corrisponde alla segmentazione configurata per l’esperienza e osserva che l’esperienza cambia di conseguenza.

## Utilizzo del segmento {#using-your-segment}

I segmenti vengono utilizzati per controllare il contenuto effettivo visualizzato da un pubblico specifico. Consulta [Gestione dei tipi di pubblico](audiences.md) per ulteriori informazioni su tipi di pubblico e di segmenti e [Authoring di contenuti di destinazione](targeted-content.md) per informazioni sull’utilizzo di tipi di pubblico e di segmenti per eseguire il targeting del contenuto.
