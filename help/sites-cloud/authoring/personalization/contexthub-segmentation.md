---
title: Configurazione della segmentazione con ContextHub
description: Scopri come configurare la segmentazione utilizzando ContextHub.
exl-id: fbc38611-dbee-426e-b823-df64b6730c45
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 5%

---

# Configurazione della segmentazione con ContextHub{#configuring-segmentation-with-contexthub}

La segmentazione è un concetto chiave per la creazione di una campagna. Vedi [Segmentazione](segmentation.md) per informazioni sul funzionamento della segmentazione e sui termini chiave.

A seconda delle informazioni già raccolte sui visitatori del sito e degli obiettivi che desideri raggiungere, dovrai definire i segmenti e le strategie necessarie per il contenuto di destinazione.

Questi segmenti vengono quindi utilizzati per fornire a un visitatore contenuti con targeting specifico. [Attività](activities.md) qui definito può essere incluso in qualsiasi pagina e definire per quale segmento di visitatori si applica il contenuto specializzato.

AEM ti consente di personalizzare facilmente le esperienze degli utenti. Consente inoltre di verificare i risultati delle definizioni dei segmenti.

## Accesso ai segmenti {#accessing-segments}

La [Tipi di pubblico](audiences.md) viene utilizzata per gestire i segmenti per ContextHub e i tipi di pubblico per il tuo account Adobe Target. Questa documentazione copre la gestione dei segmenti per ContextHub.

Per accedere ai segmenti, nella navigazione globale seleziona **Navigazione > Personalizzazione > Pubblico**.

![Gestione dei tipi di pubblico](../assets/contexthub-segmentation-audiences.png)

## Editor segmento {#segment-editor}

<!--The **Segment Editor** allows you to easily modify a segment. To edit a segment, select a segment in the [list of segments](/help/sites-administering/segmentation.md#accessing-segments) and click the **Edit** button.-->
La **Editor segmenti** consente di modificare facilmente un segmento. Per modificare un segmento, selezionane uno nell’elenco dei segmenti e fai clic sul pulsante **Modifica** pulsante .

![Editor segmenti](../assets/contexthub-segment-editor.png)

Tramite il browser Componenti è possibile aggiungere **E** e **O** per definire la logica del segmento, quindi aggiungi altri componenti per confrontare proprietà e valori o script di riferimento e altri segmenti per definire i criteri di selezione (consulta [Creazione di un nuovo segmento](#creating-a-new-segment)) per definire lo scenario esatto per la selezione del segmento.

Quando l’intera istruzione restituisce true, il segmento è stato risolto. Nel caso in cui siano applicabili più segmenti, la variabile **Incremento** viene utilizzato anche il fattore . Vedi [Creazione di un nuovo segmento](#creating-a-new-segment) per informazioni dettagliate sul fattore di incremento.

>[!CAUTION]
>
>L’editor dei segmenti non verifica la presenza di riferimenti circolari. Ad esempio, il segmento A fa riferimento a un altro segmento B, che a sua volta fa riferimento al segmento A. È necessario assicurarsi che i segmenti non contengano riferimenti circolari.

### Contenitori {#containers}

I seguenti contenitori sono disponibili preconfigurati e consentono di raggruppare confronti e riferimenti per la valutazione booleana. Possono essere trascinati dal browser Componenti all’editor. Vedi la sezione seguente [Utilizzo dei contenitori AND e OR](#using-and-and-or-containers) per ulteriori informazioni.

|  |  |
|---|---|
| Contenitore E | Operatore AND booleano |
| Contenitore O | Operatore OR booleano |

### Confronti {#comparisons}

Per valutare le proprietà dei segmenti sono disponibili i seguenti confronti predefiniti dei segmenti. Possono essere trascinati dal browser Componenti all’editor.

|  |  |
|---|---|
| Property-Value | Confronta una proprietà di un archivio con un valore definito |
| Property-Property | Confronta una proprietà di un archivio con un&#39;altra proprietà |
| Riferimento a un segmento di proprietà | Confronta una proprietà di un archivio con un altro segmento di riferimento |
| Riferimento a script di proprietà | Confronta una proprietà di un archivio con i risultati di uno script |
| Riferimento al segmento-Script di riferimento | Confronta un segmento di riferimento ai risultati di uno script |

>[!NOTE]
>
>Quando si confrontano i valori, se il tipo di dati del confronto non è impostato (cioè è impostato su auto detect), il motore di segmentazione di ContextHub si limiterà a confrontare i valori come farebbe javascript. Non colloca i valori ai tipi previsti, il che può portare a risultati fuorvianti. Ad esempio:
>
>`null < 30 // will return true`
>
>Pertanto, quando [creazione di un segmento](#creating-a-new-segment), seleziona un **tipo di dati** ogni volta che i tipi di valori confrontati sono noti. Ad esempio:
>
>Quando si confronta la proprietà `profile/age`, sai già che il tipo confrontato sarà **numero**, anche se `profile/age` non è impostato, un confronto `profile/age` meno di 30 torneranno **false** come vi aspettereste.

### Riferimenti {#references}

Sono disponibili i seguenti riferimenti pronti all’uso per eseguire un collegamento diretto a uno script o a un altro segmento. Possono essere trascinati dal browser Componenti all’editor.

|  |  |
|---|---|
| Riferimento segmento | Valutare il segmento a cui si fa riferimento |
| Riferimento script | Valutare lo script a cui si fa riferimento. Vedi la sezione seguente [Utilizzo di riferimenti di script](#using-script-references) per ulteriori informazioni. |

## Creazione di un nuovo segmento {#creating-a-new-segment}

Per definire il nuovo segmento:

1. Dopo [accesso ai segmenti](#accessing-segments), [passa alla cartella](#organizing-segments) dove desideri creare il segmento o lasciarlo nella directory principale.

1. Tocca o fai clic sul pulsante **Crea** e seleziona **Creare un segmento ContextHub**.

   ![Aggiungi segmento](../assets/contexthub-create-segment.png)

1. In **Nuovo segmento ContextHub**, inserisci un titolo per il segmento e un valore di incremento se necessario, quindi tocca o fai clic su **Crea**.

   ![Nuovo segmento](../assets/contexthub-new-segment.png)

   Ogni segmento ha un parametro di incremento utilizzato come fattore di ponderazione. Un numero maggiore indica che il segmento verrà selezionato preferibilmente a un segmento con un numero inferiore nelle istanze in cui sono validi più segmenti.

   * Valore minimo: `0`
   * Valore massimo: `1000000`

1. Dalla console dei segmenti, modifica il segmento appena creato per aprirlo nell’editor segmenti.
1. Trascina un confronto o un riferimento all’editor di segmenti che verrà visualizzato nel contenitore AND predefinito.
1. Tocca o fai doppio clic sull’opzione di configurazione del nuovo riferimento o segmento per modificare i parametri specifici. In questo esempio, stiamo testando la gente a Basilea.

   ![Test per le persone a Basilea](../assets/contexthub-comparing-property-value.png)

   Imposta sempre un **Tipo di dati** se possibile, per garantire che i confronti siano valutati correttamente. Vedi [Confronti](#comparisons) per ulteriori informazioni.

1. Fai clic su **Fine** per salvare la definizione:
1. Aggiungi altri componenti in base alle esigenze. Puoi formulare espressioni booleane utilizzando i componenti contenitore per i confronti AND e OR (vedi [Utilizzo di AND e OR Containers](#using-and-and-or-containers) qui sotto). Con l’editor dei segmenti è possibile eliminare i componenti non più necessari o trascinarli in nuove posizioni all’interno dell’istruzione.

### Utilizzo dei contenitori AND e OR {#using-and-and-or-containers}

Utilizzando i componenti contenitore AND e OR , puoi creare segmenti complessi in AEM. In questo modo è utile tenere presenti alcuni punti fondamentali:

* Il livello principale della definizione è sempre il contenitore AND creato inizialmente. Questo non può essere modificato, ma non ha un effetto sul resto della definizione del segmento.
* Assicurati che la nidificazione del contenitore abbia senso. I contenitori possono essere visualizzati come parentesi dell’espressione booleana.

L’esempio seguente viene utilizzato per selezionare i visitatori considerati nel nostro gruppo di target svizzero:

```text
 People in Basel

 OR

 People in Zürich
```

Per iniziare, inserisci un componente contenitore OR all’interno del contenitore AND predefinito. All’interno del contenitore OR è possibile aggiungere la proprietà o i componenti di riferimento.

![Segmento con operatore OR](../assets/contexthub-or-operator.png)

È possibile nidificare più operatori AND e OR come necessario.

### Utilizzo di riferimenti di script {#using-script-references}

Utilizzando il componente Riferimento script, è possibile delegare la valutazione di una proprietà di segmento a uno script esterno. Una volta configurato correttamente lo script, può essere utilizzato come qualsiasi altro componente di una condizione di segmento.

#### Definizione di uno script da fare riferimento {#defining-a-script-to-reference}

1. Aggiungi file a `contexthub.segment-engine.scripts` clientlib.
1. Implementa una funzione che restituisce un valore. Ad esempio:

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
1. Aggiungi **Riferimento script** nella posizione desiderata del segmento.
1. Apri la finestra di dialogo di modifica del **Riferimento script** componente. Se [configurato correttamente](#defining-a-script-to-reference), lo script deve essere disponibile nel **Nome script** a discesa.

## Organizzazione dei segmenti {#organizing-segments}

Se hai molti segmenti, possono diventare difficili da gestire come elenco semplice. In questi casi, può essere utile creare cartelle per gestire i segmenti.

### Creare una nuova cartella {#create-folder}

1. Dopo [accesso ai segmenti](#accessing-segments), tocca o fai clic su **Crea** e seleziona **Cartella**.

   ![Aggiungi cartella](../assets/contexthub-create-segment.png)

1. Specifica il **titolo** e il **nome** da assegnare alla cartella.
   * Il **titolo** deve essere descrittivo.
   * Il **nome** diventerà il nome del nodo nell’archivio.
      * Viene generato automaticamente dal titolo, secondo le [convenzioni di denominazione di AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Se necessario è possibile modificarlo.

   ![Crea cartella](../assets/contexthub-create-folder.png)

1. Tocca o fai clic su **Crea**.

   ![Conferma cartella](../assets/contexthub-confirm-folder.png)

1. La cartella verrà visualizzata nell’elenco dei segmenti.
   * L’ordinamento delle colonne influisce sul punto in cui viene visualizzata la nuova cartella nell’elenco.
   * Per regolare l’ordinamento, tocca o fai clic sulle intestazioni di colonna.
      ![La nuova cartella](../assets/contexthub-folder.png)

### Modifica cartelle esistenti {#modify-folders}

1. Dopo [accesso ai segmenti](#accessing-segments), tocca o fai clic sulla cartella da modificare per selezionarla.

   ![Selezione cartella](../assets/contexthub-select-folder.png)

1. Tocca o fai clic su **Rinomina** nella barra degli strumenti per rinominare la cartella.

1. Fornisci un nuovo **Titolo cartella** e tocca o fai clic su **Salva**.

   ![Rinomina cartella](../assets/contexthub-rename-folder.png)

>[!NOTE]
>
>Quando si rinomina una cartella, è possibile modificare solo il titolo. Impossibile modificare il nome.

### Eliminare una cartella

1. Dopo [accesso ai segmenti](#accessing-segments), tocca o fai clic sulla cartella da modificare per selezionarla.

   ![Selezione cartella](../assets/contexthub-select-folder.png)

1. Tocca o fai clic su **Elimina** nella barra degli strumenti per eliminare la cartella.

1. Una finestra di dialogo presenta un elenco di cartelle selezionate per l’eliminazione.

   ![Conferma eliminazione](../assets/contexthub-confirm-segment-delete.png)

   * Tocca o fai clic su **Elimina** per confermare.
   * Tocca o fai clic su **Annulla** per interrompere.

1. Se una delle cartelle selezionate contiene sottocartelle o segmenti, l’eliminazione deve essere confermata.

   ![Conferma eliminazione di elementi figlio](../assets/contexthub-confirm-segment-child-delete.png)

   * Tocca o fai clic su **Forza eliminazione** per confermare.
   * Tocca o fai clic su **Annulla** per interrompere.

>[!NOTE]
>
> Non è possibile spostare un segmento da una cartella all’altra.

## Verifica dell’applicazione di un segmento {#testing-the-application-of-a-segment}

Una volta definito il segmento, è possibile testare i risultati potenziali con l’aiuto di **[ContextHub](contexthub.md).**

1. Visualizzare un’anteprima di una pagina
1. Fai clic sull’icona ContextHub per visualizzare la barra degli strumenti di ContextHub
1. Seleziona una persona che corrisponda al segmento creato
1. ContextHub risolverà i segmenti applicabili per la persona selezionata

Ad esempio, la nostra semplice definizione del segmento per identificare gli utenti a Basilea si basa sulla posizione dell’utente. Il caricamento di una persona specifica che corrisponde a tali criteri mostra se il segmento è stato risolto correttamente:

![Segmento che risolve](../assets/contexthub-segment-resolve.png)

Oppure se non è risolto:

![Segmento che non risolve](../assets/contexthub-segment-doesnt-resolve.png)

>[!NOTE]
>
>Tutte le caratteristiche vengono risolte immediatamente, anche se la maggior parte cambia solo al ricaricamento della pagina.

Tali test possono essere eseguiti anche sulle pagine di contenuto e in combinazione con contenuti mirati e correlati **Attività** e **Esperienze**.

Se hai impostato un’attività e un’esperienza, puoi facilmente testare il segmento con l’attività . Per informazioni dettagliate sulla configurazione di un’attività, consulta la relativa [documentazione sulla creazione di contenuti di destinazione](targeted-content.md).

1. In modalità di modifica di una pagina in cui hai impostato il contenuto di destinazione, puoi vedere che il contenuto è indirizzato tramite l’icona a forma di freccia sul contenuto.
1. Passa alla modalità anteprima e utilizza l’hub di contesto, passa a un utente tipo che non corrisponde alla segmentazione configurata per l’esperienza.
1. Passa a un utente tipo che non corrisponde alla segmentazione configurata per l’esperienza e osserva che l’esperienza cambia di conseguenza.

## Utilizzo del segmento {#using-your-segment}

I segmenti vengono utilizzati per controllare il contenuto effettivo visualizzato da tipi di pubblico specifici. Vedi [Gestione dei tipi di pubblico](audiences.md) per ulteriori informazioni su tipi di pubblico e segmenti e [Creazione di contenuti mirati](targeted-content.md) informazioni sull’utilizzo di tipi di pubblico e segmenti per eseguire il targeting del contenuto.
