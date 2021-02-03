---
title: Modelli per frammenti di contenuto
description: I modelli di frammenti di contenuto vengono utilizzati per creare frammenti di contenuto con contenuto strutturato.
translation-type: tm+mt
source-git-commit: 3538c03a6a455cd22423ca5a4fd69c1fe57b3e5e
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 7%

---


# Modelli per frammenti di contenuto {#content-fragment-models}

I modelli di frammenti di contenuto definiscono la struttura del contenuto per i [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md).

Per utilizzare i modelli di frammenti di contenuto, effettuare le seguenti operazioni:

1. [Abilitare la funzionalità del modello di frammento di contenuto per l’istanza](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [Creare](#creating-a-content-fragment-model) e  [configurare](#defining-your-content-fragment-model) i modelli di frammenti di contenuto
1. [Abilitare i ](#enabling-disabling-a-content-fragment-model) modelli di frammenti di contenuto per la creazione di frammenti di contenuto da utilizzare durante la creazione di frammenti di contenuto
1. [Consenti modelli di frammenti di contenuto nelle ](#allowing-content-fragment-models-assets-folder) cartelle Risorse richieste configurando  **i criteri**.

## Creazione di un modello di frammento di contenuto {#creating-a-content-fragment-model}

1. Andate a **Strumenti**, **Risorse**, quindi aprite **Modelli di frammenti di contenuto**.
1. Andate alla cartella appropriata per la [configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md).
1. Utilizzare **Create** per aprire la procedura guidata.

   >[!CAUTION]
   >
   >Se l&#39;utilizzo di [modelli di frammento di contenuto non è stato abilitato](/help/assets/content-fragments/content-fragments-configuration-browser.md), l&#39;opzione **Crea** non sarà disponibile.

1. Specifica il **Titolo modello**. È inoltre possibile aggiungere **Tag**, una **Descrizione**, quindi selezionare **Abilita modello** per [abilitare il modello](#enabling-disabling-a-content-fragment-model), se necessario.

   ![titolo e descrizione](assets/cfm-models-02.png)

1. Utilizzare **Create** per salvare il modello vuoto. Un messaggio indica l&#39;esito positivo dell&#39;azione, è possibile selezionare **Apri** per modificare immediatamente il modello, oppure **Fine** per tornare alla console.

## Definizione del modello di frammento di contenuto {#defining-your-content-fragment-model}

Il modello di frammento di contenuto definisce in modo efficace la struttura dei frammenti di contenuto risultanti utilizzando una selezione di **[Tipi di dati](#data-types)**. Utilizzando l&#39;editor modelli è possibile aggiungere istanze dei tipi di dati, quindi configurarle per creare i campi richiesti:

>[!CAUTION]
>
>La modifica di un modello di frammento di contenuto esistente può avere un impatto sui frammenti dipendenti.

1. Andate a **Strumenti**, **Risorse**, quindi aprite **Modelli di frammenti di contenuto**.

1. Individuate la cartella che contiene il modello di frammento di contenuto.
1. Aprire il modello richiesto per **Edit**; utilizzare l&#39;azione rapida oppure selezionare il modello e quindi l&#39;azione dalla barra degli strumenti.

   Una volta aperto l&#39;editor modelli mostra:

   * left: campi già definiti
   * A destra: **Tipi di dati** disponibili per la creazione di campi, oltre alle **Proprietà** da utilizzare dopo la creazione.

   >[!NOTE]
   >
   >Quando un campo è **obbligatorio**, l’**Etichetta** indicata nel riquadro a sinistra sarà contrassegnata con un asterisco (*****).

   ![proprietà](assets/cfm-models-03.png)

1. **Aggiunta di un campo**

   * Trascinare un tipo di dati richiesto nella posizione desiderata per un campo:

      ![tipo di dati su campo](assets/cfm-models-04.png)

   * Una volta aggiunto un campo al modello, il pannello a destra mostrerà le **Proprietà** che possono essere definite per quel particolare tipo di dati. Qui è possibile definire i requisiti necessari per tale campo.

      * Molte proprietà sono autoesplicative, per ulteriori dettagli vedere [Proprietà](#properties).
      * Digitando una **etichetta campo** si completerà automaticamente il **nome proprietà**, se vuoto, e sarà possibile aggiornarlo manualmente in seguito.

      Esempio:

      ![proprietà del campo](assets/cfm-models-05.png)


1. **Rimozione di un campo**

   Selezionate il campo desiderato, quindi toccate o fate clic sull&#39;icona del cestino. Viene richiesto di confermare l’operazione.

   ![rimuovere](assets/cfm-models-06.png)

1. Aggiungete tutti i campi obbligatori e definite le relative proprietà, a seconda delle necessità. Esempio:

   ![save](assets/cfm-models-07.png)

1. Selezionare **Save** per mantenere la definizione.

## Tipi di dati {#data-types}

È disponibile una selezione di tipi di dati per definire il modello:

* **Testo su riga singola**
   * aggiungere uno o più campi di una singola riga di testo; la lunghezza massima può essere definita
* **Testo su più righe**
   * Un&#39;area di testo che può essere RTF, Testo normale o Marcatura
* **Numero**
   * Aggiungere uno o più campi numerici
* **Booleano**
   * Aggiungi una casella di controllo booleana
* **Data e ora**
   * Aggiungere una data e/o un’ora
* **Enumerazione**
   * Aggiungere un set di caselle di controllo, pulsanti di scelta o campi a discesa
* **Tag**
   * Consente agli autori dei frammenti di accedere e selezionare le aree dei tag
* **Riferimento contenuto**
   * riferimenti ad altri contenuti di qualsiasi tipo; può essere utilizzato per [creare contenuto nidificato](#using-references-to-form-nested-content)
* **Riferimento frammento**
   * Riferimenti ad altri frammenti di contenuto; può essere utilizzato per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Il tipo di dati può essere configurato per consentire agli autori dei frammenti di:
      * Modificare direttamente il frammento a cui viene fatto riferimento.
      * Creare un nuovo frammento di contenuto, in base al modello appropriato
* **Oggetto JSON**
   * Consente all&#39;autore del frammento di contenuto di immettere la sintassi JSON negli elementi corrispondenti di un frammento.
      * Per consentire AEM memorizzare JSON diretto che hai copiato/incollato da un altro servizio.
      * Il JSON verrà passato e inviato come JSON in GraphQL.
      * Include l&#39;evidenziazione della sintassi JSON, la compilazione automatica e l&#39;evidenziazione degli errori nell&#39;editor dei frammenti di contenuto.

## Proprietà {#properties}

Molte proprietà sono auto-esplicative, per alcune proprietà ulteriori dettagli sono di seguito:

* **Rendering**
con nome: varie opzioni per realizzare/eseguire il rendering del campo in un frammento. Spesso questo consente di definire se l’autore visualizzerà una singola istanza del campo o se potrà creare più istanze.

* **Etichetta**
campoImmissione di un 
**L&#39;** etichetta campo genererà automaticamente un nome **** proprietà, che potrà quindi essere aggiornato manualmente, se necessario.

* **La convalida**
ValidationBasic è disponibile tramite meccanismi quali la proprietà  **** Requiredproperty. Alcuni tipi di dati dispongono di campi di convalida aggiuntivi. Per ulteriori informazioni, vedere [Convalida](#validation).

* Per il tipo di dati **Testo su più righe** è possibile definire il **Tipo predefinito** come:

   * **Formato RTF**
   * **Markdown**
   * **Testo normale**

   Se non viene specificato, per questo campo viene utilizzato il valore predefinito **Rich Text**.

   La modifica del **Tipo predefinito** in un modello per frammenti di contenuto avrà effetto solo su un frammento esistente correlato, una volta che il frammento è stato aperto nell’editor e successivamente salvato.

* ****
UniqueContent (per il campo specifico) deve essere univoco in tutti i frammenti di contenuto creati dal modello corrente.

   Questo consente di impedire agli autori di contenuti di ripetere il contenuto già aggiunto in un altro frammento dello stesso modello.

   Ad esempio, un campo **Testo su riga singola** denominato `Country` nel modello di frammento di contenuto non può avere il valore `Japan` in due frammenti di contenuto dipendenti. Viene emesso un avviso quando si tenta di eseguire la seconda istanza.

   >[!NOTE]
   Uniquità garantita per radice lingua.

   >[!NOTE]
   Le varianti possono avere lo stesso valore *univoco* delle varianti dello stesso frammento, ma non lo stesso valore utilizzato in qualsiasi variante di altri frammenti.

* ****
TranslatableSelezionando la casella di controllo &quot;Translatable&quot; su un campo nell&#39;editor modelli CF

   * Assicurarsi che il nome della proprietà del campo sia aggiunto nella configurazione di traduzione, contesto `/content/dam/<tenant>`, se non è già presente.
   * Per GraphQL: impostare una proprietà `<translatable>` nel campo Frammento di contenuto su `yes`, per consentire il filtro query GraphQL per l&#39;output JSON con solo contenuto convertibile.

* Per ulteriori informazioni su tale tipo di dati specifico e sulle relative proprietà, vedere **[Riferimento frammento (frammenti nidificati)](#fragment-reference-nested-fragments)**.

## Convalida {#validation}

Diversi tipi di dati ora includono la possibilità di definire i requisiti di convalida per l&#39;immissione di contenuto nel frammento risultante:

* **Testo su riga singola**
   * Confrontate con un regex predefinito.
* **Numero**
   * Verificate la presenza di valori specifici.
* **Riferimento contenuto**
   * Eseguire il test per tipi specifici di contenuto.
   * È possibile fare riferimento solo alle risorse di dimensioni file specificate o inferiori.
   * È possibile fare riferimento solo alle immagini all’interno di un intervallo predefinito di larghezza e/o altezza (in pixel).
* **Riferimento frammento**
   * Eseguire il test per un modello di frammento di contenuto specifico.

<!--
  * Only predefined file types can be referenced.
  * No more than the predefined number of assets can be referenced. 
  * No more than the predefined number of fragments can be referenced.
-->

## Utilizzo dei riferimenti per il modulo Contenuto nidificato {#using-references-to-form-nested-content}

I frammenti di contenuto possono formare contenuto nidificato utilizzando uno dei seguenti tipi di dati:

* **[Riferimento contenuto](#content-reference)**
   * Fornisce un semplice riferimento ad altri contenuti; di qualsiasi tipo.
   * Può essere configurato per uno o più riferimenti (nel frammento risultante).

* **[Riferimento](#fragment-reference-nested-fragments)**  frammento (frammenti nidificati)
   * Fa riferimento ad altri frammenti, a seconda dei modelli specifici specificati.
   * Consente di includere/recuperare dati strutturati.

      >[!NOTE]
      Questo metodo è di particolare interesse in combinazione con [Distribuzione di contenuti headless con frammenti di contenuto con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).
   * Può essere configurato per uno o più riferimenti (nel frammento risultante).

>[!NOTE]
AEM dispone di una protezione di ricorrenza per:
* Riferimenti contenuto
Ciò impedisce all&#39;utente di aggiungere un riferimento al frammento corrente. Questo potrebbe causare la visualizzazione di una finestra di dialogo vuota del selettore Riferimento frammento.

* Riferimenti ai frammenti in GraphQL
Se create una query profonda che restituisce più frammenti di contenuto a cui fanno riferimento l’uno dall’altro, restituisce null alla prima occorrenza.


### Riferimento contenuto {#content-reference}

Content Reference (Riferimento contenuto) consente di eseguire il rendering del contenuto da un’altra origine; ad esempio, un frammento di immagine o di contenuto.

Oltre alle proprietà standard è possibile specificare:

* Il **percorso principale** per qualsiasi contenuto di riferimento.
* Tipi di contenuto a cui è possibile fare riferimento.
* Limitazioni per le dimensioni dei file.
* Restrizioni per l&#39;immagine.
   <!-- Check screenshot - might need update -->
   ![Riferimento contenuto](assets/cfm-content-reference.png)

### Riferimento frammento (frammenti nidificati) {#fragment-reference-nested-fragments}

Il riferimento al frammento fa riferimento a uno o più frammenti di contenuto. Questa funzione è particolarmente interessante per il recupero di contenuti da usare nell’app, in quanto consente di recuperare dati strutturati con più livelli.

Esempio:

* Un modello che definisce i dettagli per un dipendente; tra cui:
   * Un riferimento al modello che definisce il datore di lavoro (società)

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
Questo è di particolare interesse in combinazione con [Distribuzione di contenuti headless con frammenti di contenuto con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

Oltre alle proprietà standard è possibile definire:

* **Rendering come**:

   * **multicampo** : l’autore del frammento può creare più riferimenti, singoli o singoli

   * **riferimento a frammento** : consente all&#39;autore del frammento di selezionare un singolo riferimento a un frammento

* **Model**
TypeÈ possibile selezionare più modelli. Durante la creazione del frammento di contenuto, qualsiasi frammento a cui si fa riferimento deve essere stato creato utilizzando questi modelli.

* **Percorso**
radice: specifica un percorso principale per tutti i frammenti a cui viene fatto riferimento.

* **Consenti creazione di frammenti**

   Questo consente all&#39;autore del frammento di creare un nuovo frammento basato sul modello appropriato.

   * **fragmentreferencecomposite** : consente all&#39;autore del frammento di creare un composito, selezionando più frammenti

   <!-- Check screenshot - might need update -->
   ![Riferimento frammento](assets/cfm-fragment-reference.png)

>[!NOTE]
Esiste un meccanismo di protezione contro la ricorrenza. Non consente all&#39;utente di selezionare il frammento di contenuto corrente in Riferimento frammento. Questo potrebbe causare la visualizzazione di una finestra di dialogo vuota del selettore Riferimento frammento.
Esiste anche una protezione di ricorrenza per i riferimenti ai frammenti in GraphQL. Se si crea una query approfondita tra due frammenti di contenuto che si fanno riferimento l&#39;uno all&#39;altro, viene restituito null.

## Abilitazione o disattivazione di un modello di frammento di contenuto {#enabling-disabling-a-content-fragment-model}

Per il controllo completo sull’utilizzo dei modelli di frammenti di contenuto, è possibile impostare uno stato.

### Abilitazione di un modello di frammento di contenuto {#enabling-a-content-fragment-model}

Una volta creato, il modello deve essere abilitato in modo che:

* È disponibile per la selezione quando si crea un nuovo frammento di contenuto.
* È possibile fare riferimento all&#39;interno di un modello di frammento di contenuto.
* È disponibile per GraphQL; in modo che lo schema venga generato.

Per abilitare un modello contrassegnato come:

* **Bozza** : mew (mai attivato).
* **Disattivato** : è stato specificamente disabilitato.

È possibile utilizzare l&#39;opzione **Abilita** da:

* La barra degli strumenti superiore, quando è selezionato il modello richiesto.
* Azione rapida corrispondente (posizionamento del mouse sul modello richiesto).

![Abilita una bozza o un modello disattivato](assets/cfm-status-enable.png)

### Disattivazione di un modello di frammento di contenuto {#disabling-a-content-fragment-model}

È inoltre possibile disattivare un modello in modo che:

* Il modello non è più disponibile come base per la creazione di *nuovi frammenti di contenuto*.
* However:
   * Lo schema GraphQL continua a essere generato ed è ancora interrogabile (per evitare di influenzare l&#39;API JSON).
   * Eventuali frammenti di contenuto basati sul modello possono ancora essere interrogati e restituiti dall&#39;endpoint GraphQL.
* Non è più possibile fare riferimento al modello, ma i riferimenti esistenti vengono mantenuti invariati e possono comunque essere interrogati e restituiti dall&#39;endpoint GraphQL.

Per disabilitare un modello contrassegnato come **Abilitato**, utilizzare l&#39;opzione **Disattiva** da:

* La barra degli strumenti superiore, quando è selezionato il modello richiesto.
* Azione rapida corrispondente (posizionamento del mouse sul modello richiesto).

![Disattivazione di un modello abilitato](assets/cfm-status-disable.png)

## Consentire modelli di frammenti di contenuto nella cartella delle risorse {#allowing-content-fragment-models-assets-folder}

Per implementare la gestione dei contenuti, puoi configurare **Criteri** nella cartella Risorse per controllare quali modelli di frammenti di contenuto possono essere creati in tale cartella.

>[!NOTE]
Il meccanismo è simile a [consentendo modelli di pagina](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) per una pagina e i relativi elementi secondari, nelle proprietà avanzate di una pagina.

Per configurare i **criteri** per **modelli di frammenti di contenuto consentiti**:

1. Spostatevi e aprite **Proprietà** per la cartella Risorse richiesta.

1. Aprite la scheda **Criteri** in cui potete configurare:

   * **Ereditato da`<folder>`**

      I criteri vengono ereditati automaticamente quando si creano nuove cartelle figlie. il criterio può essere riconfigurato (e l&#39;ereditarietà interrotta) se le sottocartelle devono consentire modelli diversi dalla cartella principale.

   * **Modelli per frammenti di contenuto consentiti per percorso**

      Possono essere consentiti più modelli.

   * **Modelli di frammenti di contenuto consentiti per tag**

      Possono essere consentiti più modelli.
   ![Criterio modello frammento di contenuto](assets/cfm-model-policy-assets-folder.png)

1. **Salvare** le modifiche.

I modelli di frammento di contenuto consentiti per una cartella sono risolti come segue:
* **Criteri** per **Modelli di frammenti di contenuto consentiti**.
* Se vuoto, provare a determinare il criterio utilizzando le regole di ereditarietà.
* Se la catena di ereditarietà non fornisce un risultato, verificare la configurazione **Cloud Services** per quella cartella (anche prima direttamente e poi tramite ereditarietà).
* Se nessuno dei risultati di cui sopra fornisce alcun risultato, non ci sono modelli consentiti per quella cartella.

## Eliminazione di un modello di frammento di contenuto {#deleting-a-content-fragment-model}

>[!CAUTION]
L&#39;eliminazione di un modello di frammento di contenuto può avere un impatto sui frammenti dipendenti.

Per eliminare un modello di frammento di contenuto:

1. Andate a **Strumenti**, **Risorse**, quindi aprite **Modelli di frammenti di contenuto**.

1. Individuate la cartella che contiene il modello di frammento di contenuto.
1. Selezionare il modello, seguito da **Elimina** dalla barra degli strumenti.

   >[!NOTE]
   Se al modello viene fatto riferimento, verrà visualizzato un avviso. Adottare le misure appropriate.

## Pubblicazione di un modello di frammento di contenuto {#publishing-a-content-fragment-model}

I modelli di frammenti di contenuto devono essere pubblicati quando/prima che vengano pubblicati eventuali frammenti di contenuto dipendenti.

Per pubblicare un modello di frammento di contenuto:

1. Andate a **Strumenti**, **Risorse**, quindi aprite **Modelli di frammenti di contenuto**.

1. Individuate la cartella che contiene il modello di frammento di contenuto.
1. Selezionate il modello, seguito da **Pubblica** dalla barra degli strumenti.
Lo stato di pubblicazione verrà indicato nella console.

   >[!NOTE]
   Se si pubblica un frammento di contenuto per il quale il modello non è ancora stato pubblicato, verrà visualizzato un elenco di selezione e il modello verrà pubblicato insieme al frammento.

## Annullamento della pubblicazione di un modello di frammento di contenuto {#unpublishing-a-content-fragment-model}

È possibile annullare la pubblicazione dei modelli di frammento di contenuto se non vi fanno riferimento alcun frammento.

Per annullare la pubblicazione di un modello di frammento di contenuto:

1. Andate a **Strumenti**, **Risorse**, quindi aprite **Modelli di frammenti di contenuto**.

1. Individuate la cartella che contiene il modello di frammento di contenuto.
1. Selezionate il modello, seguito da **Annulla pubblicazione** dalla barra degli strumenti.
Lo stato di pubblicazione verrà indicato nella console.
