---
title: Configurazione della segmentazione con ContextHub
description: Scopri come configurare la segmentazione tramite ContextHub.
translation-type: tm+mt
source-git-commit: 82ad2cda70dd664ac9456a04f34e2d5831687fc1
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 2%

---


# Configurazione della segmentazione con ContextHub{#configuring-segmentation-with-contexthub}

La segmentazione è un concetto chiave per la creazione di una campagna. Consulta [Comprensione della segmentazione](segmentation.md) per informazioni sul funzionamento della segmentazione e sui termini chiave.

A seconda delle informazioni già raccolte sui visitatori del sito e degli obiettivi da raggiungere, dovrete definire i segmenti e le strategie necessari per il contenuto di destinazione.

Questi segmenti vengono quindi utilizzati per fornire a un visitatore contenuto con targeting specifico. [Le attività](activities.md) qui definite possono essere incluse in qualsiasi pagina e definire per quale segmento di visitatori si applica il contenuto specializzato.

AEM consente di personalizzare facilmente le esperienze degli utenti. Consente inoltre di verificare i risultati delle definizioni dei segmenti.

## Accesso ai segmenti {#accessing-segments}

La console [Audiences](audiences.md) viene utilizzata per gestire i segmenti per ContextHub e i tipi di pubblico per il vostro account Adobe Target . Questa documentazione descrive la gestione dei segmenti per ContextHub.

Per accedere ai tuoi segmenti, nella navigazione globale seleziona **Navigazione > Personalizzazione > Audience**.

![Gestione dell&#39;audience](/help/sites-cloud/authoring/assets/contexthub-segmentation-audiences.png)

## Editor segmento {#segment-editor}

<!--The **Segment Editor** allows you to easily modify a segment. To edit a segment, select a segment in the [list of segments](/help/sites-administering/segmentation.md#accessing-segments) and click the **Edit** button.-->
L’Editor **** segmenti consente di modificare facilmente un segmento. Per modificare un segmento, seleziona un segmento nell’elenco dei segmenti e fai clic sul pulsante **Modifica** .

![Editor segmenti](/help/sites-cloud/authoring/assets/contexthub-segment-editor.png)

Utilizzando il Browser componenti è possibile aggiungere contenitori **AND** e **OR** per definire la logica del segmento, quindi aggiungere componenti aggiuntivi per confrontare proprietà e valori o script di riferimento e altri segmenti per definire i criteri di selezione (vedere [Creazione di un nuovo segmento](#creating-a-new-segment)) per definire lo scenario esatto per la selezione del segmento.

Quando l&#39;intera istruzione restituisce true, il segmento ha risolto. Se sono applicabili più segmenti, viene utilizzato anche il fattore **Incremento** . Consultate [Creazione di un nuovo segmento](#creating-a-new-segment) per informazioni dettagliate sul fattore di incremento.

>[!CAUTION]
>
>L&#39;editor segmenti non verifica la presenza di riferimenti circolari. Ad esempio, il segmento A fa riferimento a un altro segmento B, che a sua volta fa riferimento al segmento A. Devi accertarti che i tuoi segmenti non contengano riferimenti circolari.

### Containers {#containers}

I seguenti contenitori sono disponibili out-of-the-box e consentono di raggruppare confronti e riferimenti per la valutazione booleana. È possibile trascinarli dal Browser componenti all’editor. Per ulteriori informazioni, consulta la sezione [Utilizzo di AND e OR Containers](#using-and-and-or-containers) .

|  |  |
|---|---|
| Contenitore E | Operatore AND booleano |
| Contenitore O | Operatore OR booleano |

### Confronti {#comparisons}

Per valutare le proprietà del segmento sono disponibili i seguenti confronti out-of-the-box. È possibile trascinarli dal Browser componenti all’editor.

|  |  |
|---|---|
| Property-Value | Confronta una proprietà di uno store con un valore definito |
| Property-Property | Confronta una proprietà di uno store con un&#39;altra proprietà |
| Riferimento segmento proprietà | Confronta una proprietà di uno store con un altro segmento di riferimento |
| Riferimento script di proprietà | Confronta una proprietà di uno store con i risultati di uno script |
| Riferimento segmento-Riferimento script | Confronta un segmento di riferimento con i risultati di uno script |

>[!NOTE]
>
>Quando si confrontano i valori, se il tipo di dati del confronto non è impostato (ovvero impostato su auto detection), il motore di segmentazione di ContextHub confronterà semplicemente i valori come farebbe javascript. Non riporta i valori ai tipi previsti, il che può portare a risultati fuorvianti. Esempio:
>
>`null < 30 // will return true`
>
>Pertanto, quando [crei un segmento](#creating-a-new-segment), devi selezionare un tipo **di** dati ogni volta che sono noti i tipi di valori confrontati. Esempio:
>
>Quando si confronta la proprietà `profile/age`, è già noto che il tipo confrontato sarà **numerico**, quindi anche se non `profile/age` è impostato, un confronto `profile/age` inferiore a 30 restituirà **falso**, come previsto.

### Riferimenti {#references}

I seguenti riferimenti sono disponibili out-of-the-box per il collegamento diretto a uno script o a un altro segmento. È possibile trascinarli dal Browser componenti all’editor.

|  |  |
|---|---|
| Riferimento segmento | Valutazione del segmento a cui si fa riferimento |
| Riferimento script | Valutare lo script di riferimento. Per ulteriori informazioni, vedere la sezione [Utilizzo dei riferimenti](#using-script-references) di script riportata di seguito. |

## Creating a New Segment {#creating-a-new-segment}

Per definire il nuovo segmento:

1. Dopo aver [effettuato l’accesso ai segmenti](#accessing-segments), tocca o fai clic sul pulsante Crea e seleziona **Crea segmento** ContextHub.

   ![Aggiungi segmento](/help/sites-cloud/authoring/assets/contexthub-create-segment.png)

1. Nel **nuovo segmento** ContextHub, immetti un titolo per il segmento e un valore di incremento, se necessario, quindi tocca o fai clic su **Crea**.

   ![Nuovo segmento](/help/sites-cloud/authoring/assets/contexthub-new-segment.png)

   Ogni segmento ha un parametro di incremento che viene utilizzato come fattore di ponderazione. Un numero più alto indica che il segmento sarà selezionato in preferenza rispetto a un segmento con un numero inferiore nelle istanze in cui più segmenti sono validi.

   * Minimum value: `0`
   * Maximum value: `1000000`

1. Dalla console dei segmenti, modifica il segmento appena creato per aprirlo nell’editor segmenti.
1. Trascina un confronto o un riferimento all’editor segmenti che verrà visualizzato nel contenitore AND predefinito.
1. Tocca o fai doppio clic sull&#39;opzione di configurazione del nuovo riferimento o segmento per modificare i parametri specifici. In questo esempio, stiamo provando persone a Basilea.

   ![Test per le persone a Basilea](/help/sites-cloud/authoring/assets/contexthub-comparing-property-value.png)

   Imposta sempre un tipo **di** dati, se possibile, per garantire che i confronti vengano valutati correttamente. Per ulteriori informazioni, consulta [Confronti](#comparisons) .

1. Click **Done** to save your definition:
1. Aggiungi altri componenti in base alle esigenze. È possibile formulare espressioni booleane utilizzando i componenti contenitore per il confronto AND e OR (vedere [Uso di AND e O contenitori](#using-and-and-or-containers) di seguito). Con l&#39;editor segmenti è possibile eliminare i componenti non più necessari o trascinarli in nuove posizioni all&#39;interno dell&#39;istruzione.

### Utilizzo di AND e OR Containers {#using-and-and-or-containers}

I componenti AND e OR del contenitore consentono di creare segmenti complessi in AEM. A tal fine, è importante essere consapevoli di alcuni punti fondamentali:

* Il livello principale della definizione è sempre il contenitore AND creato inizialmente. Questo non può essere modificato, ma non ha un effetto sul resto della definizione del segmento.
* Verificare che la nidificazione del contenitore abbia senso. I contenitori possono essere visualizzati come parentesi dell&#39;espressione booleana.

L’esempio seguente è utilizzato per selezionare i visitatori che sono considerati nel nostro gruppo di destinazione svizzero:

```text
 People in Basel

 OR

 People in Zürich
```

Per iniziare, posizionate un componente contenitore OR all’interno del contenitore AND predefinito. All&#39;interno del contenitore OR è possibile aggiungere la proprietà o i componenti di riferimento.

![Segmento con operatore OR](/help/sites-cloud/authoring/assets/contexthub-or-operator.png)

Potete nidificare più operatori AND e OR come necessario.

### Utilizzo dei riferimenti di script {#using-script-references}

Utilizzando il componente Riferimento script, la valutazione di una proprietà del segmento può essere delegata a uno script esterno. Una volta configurato correttamente, lo script può essere utilizzato come qualsiasi altro componente di una condizione di segmento.

#### Definizione di uno script come riferimento {#defining-a-script-to-reference}

1. Aggiungi file a `contexthub.segment-engine.scripts` clientlib.
1. Implementare una funzione che restituisce un valore. Esempio:

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

1. Crea segmento ContextHub.
1. Aggiungere il componente Riferimento **** script nella posizione desiderata del segmento.
1. Aprire la finestra di dialogo di modifica del componente Riferimento **** script. Se configurato [](#defining-a-script-to-reference)correttamente, lo script dovrebbe essere disponibile nell&#39;elenco a discesa Nome **** script.

## Verifica dell’applicazione di un segmento {#testing-the-application-of-a-segment}

Una volta definito il segmento, i potenziali risultati possono essere testati con l&#39;aiuto di **[ContextHub](contexthub.md).**

1. Anteprima di una pagina
1. Fate clic sull’icona ContextHub per visualizzare la barra degli strumenti ContextHub
1. Selezionare una persona che corrisponda al segmento creato
1. ContextHub risolverà i segmenti applicabili alla persona selezionata

Ad esempio, la nostra definizione di segmento semplice per identificare gli utenti in Basilea è basata sulla posizione dell’utente. Quando si carica una persona specifica che soddisfa tali criteri, viene visualizzato se il segmento è stato risolto correttamente:

![Segmento che risolve](/help/sites-cloud/authoring/assets/contexthub-segment-resolve.png)

Oppure, se non è stato risolto:

![Segmento che non risolve](/help/sites-cloud/authoring/assets/contexthub-segment-doesnt-resolve.png)

>[!NOTE]
>
>Tutte le caratteristiche vengono risolte immediatamente, anche se la maggior parte delle modifiche apportate al ricaricamento della pagina.

Tali test possono essere eseguiti anche sulle pagine di contenuto e in combinazione con contenuti mirati e **attività** ed **esperienze** correlate.

Se avete impostato un&#39;attività e un&#39;esperienza, potete facilmente verificare il segmento con l&#39;attività. Per informazioni dettagliate sulla configurazione di un&#39;attività, consultate la [documentazione correlata sulla creazione di contenuto](targeted-content.md)mirato.

1. In modalità di modifica di una pagina in cui sono stati impostati contenuti mirati, potete vedere che il contenuto è indirizzato tramite l&#39;icona a forma di freccia sul contenuto.
1. Passate alla modalità di anteprima e utilizzate il context hub, passate a una persona che non corrisponde alla segmentazione configurata per l&#39;esperienza.
1. Passate a una persona che non corrisponde alla segmentazione configurata per l&#39;esperienza e controllate che l&#39;esperienza cambi di conseguenza.

## Utilizzo del segmento {#using-your-segment}

I segmenti vengono utilizzati per controllare il contenuto effettivo visualizzato da audience target specifiche. Consulta [Gestione dell&#39;audience](audiences.md) per ulteriori informazioni su audience e segmenti e [Creazione di contenuti](targeted-content.md) mirati sull&#39;utilizzo di audience e segmenti per il targeting dei contenuti.
