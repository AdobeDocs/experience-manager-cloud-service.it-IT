---
title: Modelli per frammenti di contenuto
description: Scopri come i modelli per frammenti di contenuto fungono da base per i frammenti di contenuto in AEM, consentendo di creare contenuti strutturati da utilizzare nella distribuzione headless o nell’authoring delle pagine.
feature: Content Fragments
role: User, Developer, Architect
exl-id: 8ab5b15f-cefc-45bf-a388-928e8cc8c603
solution: Experience Manager Sites
source-git-commit: 7adfe0ca7fbab1f8a5bd488e524a48be62584966
workflow-type: tm+mt
source-wordcount: '3209'
ht-degree: 54%

---

# Modelli per frammenti di contenuto {#content-fragment-models}

I modelli per frammenti di contenuto in Adobe Experience Manager (AEM as a Cloud Service) definiscono la struttura per il contenuto dei [frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md). Questi frammenti possono quindi essere utilizzati per l’authoring delle pagine o come base per i contenuti headless.

Per utilizzare i modelli di frammento di contenuto:

1. [Abilita la funzionalità modello Frammento di contenuto per un’istanza](/help/sites-cloud/administering/content-fragments/setup.md)
1. [Crea](#creating-a-content-fragment-model) e [configura](#defining-your-content-fragment-model) i modelli per frammenti di contenuto
1. [Abilitare i modelli di frammenti di contenuto](#enabling-disabling-a-content-fragment-model) da utilizzare per la creazione di frammenti di contenuto
1. [Consenti modelli di frammento di contenuto nelle cartelle Risorse richieste](#allowing-content-fragment-models-assets-folder) configurando i **Criteri**.

## Creazione di un modello di frammento di contenuto {#creating-a-content-fragment-model}

1. Passa a **Strumenti**, **Generale**, quindi apri **Modelli per frammenti di contenuto**.
1. Passa alla cartella appropriata per la configurazione [ o la configurazione secondaria](/help/sites-cloud/administering/content-fragments/setup.md).
1. Utilizza **Crea** per aprire la procedura guidata.

   >[!CAUTION]
   >
   >Se l&#39;utilizzo di [modelli per frammenti di contenuto non è stato abilitato](/help/sites-cloud/administering/content-fragments/setup.md), l&#39;opzione **Crea** non sarà disponibile.

1. Specifica il **titolo modello**.
Puoi anche definire varie proprietà; ad esempio, aggiungi **Tag**, **Descrizione**, seleziona **Abilita modello** per [abilitare il modello](#enabling-disabling-a-content-fragment-model) se necessario e definisci
   **Pattern URL anteprima predefinito**.

   >[!NOTE]
   >
   >Per informazioni dettagliate, consulta [Modello per frammenti di contenuto - Proprietà](#content-fragment-model-properties).

   ![Titolo e descrizione](assets/cf-cfmodels-create.png)

1. Utilizza **Crea** per salvare il modello vuoto. Un messaggio indica il successo dell&#39;azione. Puoi selezionare **Apri** per modificare immediatamente il modello, oppure **Fine** per tornare alla console.

>[!CAUTION]
>
>Se esegui una query su più frammenti a cui si fa riferimento, non è consigliabile che i vari modelli di frammenti abbiano nomi di campo con lo stesso nome, ma tipi diversi.
>
>Per ulteriori dettagli vedi [API GraphQL AEM per l&#39;utilizzo con frammenti di contenuto - Limitazioni](/help/headless/graphql-api/content-fragments.md#limitations)

### Modello per frammenti di contenuto - Proprietà {#content-fragment-model-properties}

Queste proprietà vengono definite al momento della creazione di un modello e possono essere modificate in un secondo momento con l&#39;opzione **Proprietà** per il modello per frammenti di contenuto:

* **Base**
   * **Titolo modello**
   * **Tag**
   * **Descrizione**
   * **Abilita modello**
   * **Pattern URL anteprima predefinito**
L&#39;editor frammento di contenuto consente agli autori di **visualizzare in anteprima** il contenuto in un&#39;applicazione front-end esterna. Una volta configurato il servizio **Anteprima**, aggiungere l&#39;URL per l&#39;applicazione front-end.

     L’URL di anteprima deve seguire questo pattern:
    `https://<preview_url>?param=${expression}`

     Le espressioni disponibili sono:

      * `${contentFragment.path}`
      * `${contentFragment.model.path}`
      * `${contentFragment.model.name}`
      * `${contentFragment.variation}`
      * `${contentFragment.id}`

   * **Carica immagine**

<!-- CHECK: currently under FT -->
<!--
* **GraphQL**
  Define names relevant for GraphQL.
  Changing the GraphQL API Name, or Query field names will impact client applications.
  * **API Name**
    Represents the GraphQL type and query field names in the GraphQL schema.
  * **Single Query Field Name**
    Represents the GraphQL single query field name in the GraphQL schema.
  * **Multiple Query Field Name**
    Represents the GraphQL multiple query field name in the GraphQL schema.
-->

## Definizione del modello per frammenti di contenuto {#defining-your-content-fragment-model}

Il modello per frammenti di contenuto definisce efficacemente la struttura dei frammenti di contenuto risultanti utilizzando una selezione di **[Tipi di dati](#data-types)**. Utilizzando l’editor modelli è possibile aggiungere istanze dei tipi di dati, quindi configurarle per creare i campi richiesti:

>[!CAUTION]
>
>La modifica di un modello già utilizzato da frammenti di contenuto esistenti può influire su tali frammenti dipendenti.

1. Passa a **Strumenti**, **Generale**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello Frammento di contenuto.
1. Apri il modello che desideri **modificare** utilizzando l’azione rapida oppure selezionando il modello e quindi l’azione dalla barra degli strumenti.

   Una volta aperto, l’editor modelli mostra:

   * a sinistra: campi già definiti
   * a destra: **Tipi di dati** disponibili per la creazione di campi, oltre alle **Proprietà** da utilizzare dopo la creazione

   >[!NOTE]
   >
   >Quando un campo è definito come **Obbligatorio**, l&#39;**Etichetta** indicata nel riquadro di sinistra è contrassegnata con un asterisco (**&#42;**).

![Proprietà](assets/cf-cfmodels-empty-model.png)

1. **Per aggiungere un campo**

   * Trascina un tipo di dati obbligatorio nella posizione desiderata per un campo:

     ![Trascina il tipo di dati per creare il campo](assets/cf-cfmodels-create-field.png)

   * Una volta aggiunto un campo al modello, il pannello di destra mostra le **Proprietà** che possono essere definite per quel particolare tipo di dati. Qui puoi definire ciò che è necessario per quel campo.

      * Molte proprietà sono auto-esplicative, per ulteriori dettagli vedi [Proprietà](#properties).
      * La digitazione di un **Etichetta campo** completa automaticamente il **Nome proprietà** - se vuoto, e può essere aggiornato manualmente in seguito.

        >[!CAUTION]
        >
        Quando si aggiorna manualmente la proprietà **Nome proprietà** per un tipo di dati, i nomi devono contenere *solo* caratteri A-Z, a-z, 0-9 e il carattere speciale di sottolineatura &quot;_&quot;.
        >
        Se i modelli creati in versioni precedenti di AEM contengono caratteri non validi, rimuovi o aggiorna tali caratteri.

     Ad esempio:

     ![Proprietà campo](assets/cf-cfmodels-field-properties.png)

1. **Per rimuovere un campo**

   Seleziona il campo richiesto, quindi seleziona l’icona del cestino. Viene richiesto di confermare l’azione.

   ![Rimuovi](assets/cf-cfmodels-remove-icon.png)

1. Aggiungi tutti i campi obbligatori e definisci le relative proprietà in base alle esigenze. Esempio:

   ![Salva](assets/cf-cfmodels-save.png)

1. Seleziona **Salva** per mantenere la definizione.

## Tipi di dati {#data-types}

Per definire il modello è disponibile una selezione di tipi di dati:

* **Testo su riga singola**
   * Aggiungi uno o più campi di una singola riga di testo; la lunghezza massima può essere definita
* **Testo su più righe**
   * Area di testo che può essere RTF, Testo normale o Markdown

  >[!NOTE]
  >
  Se l&#39;area di testo è RTF, Testo normale o Markdown, è definito nel modello dalla proprietà **Tipo predefinito**.
  >
  Questo formato non può essere modificato dall&#39;[Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md), ma solo dal modello.

* **Numero**
   * Aggiungi uno o più campi numerici
* **Booleano**
   * Aggiungi una casella di controllo booleana
* **Data e ora**
   * Aggiungi una data e/o un’ora
* **Enumerazione**
   * Aggiungere un set di campi casella di controllo, pulsante di scelta o elenco a discesa
* **Tag**
   * Consente agli autori di frammenti di accedere alle aree dei tag e di selezionarle
* **Riferimento contenuto**
   * I riferimenti ad altri contenuti di qualsiasi tipo possono essere utilizzati per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Se si fa riferimento a un’immagine, è possibile scegliere di mostrare una miniatura
* **Riferimento frammento**
   * I riferimenti ad altri frammenti di contenuto possono essere utilizzati per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Il tipo di dati può essere configurato in modo da consentire agli autori di frammenti di:
      * Modificare direttamente il frammento a cui si fa riferimento.
      * Creare un nuovo frammento di contenuto basato sul modello appropriato
* **Oggetto JSON**
   * Consente all’autore del frammento di contenuto di immettere la sintassi JSON negli elementi corrispondenti di un frammento.
      * Questo fa sì che AEM possa memorizzare direttamente JSON con copia e incolla da un altro servizio.
      * Il codice JSON viene trasmesso e riprodotto come codice JSON in GraphQL.
      * Include le funzioni di evidenziazione della sintassi JSON, completamento automatico ed evidenziazione degli errori nell’editor dei frammenti di contenuto.
* **Segnaposto scheda**
   * Consente l’introduzione di schede da utilizzare per la modifica del contenuto di Frammenti di contenuto.
      * Vengono visualizzati come divisori nell’editor modelli, separando le sezioni dell’elenco dei tipi di dati di contenuto. Ogni istanza rappresenta l’inizio di una nuova scheda.
      * Nell’editor frammenti ogni istanza viene visualizzata come una scheda.

     >[!NOTE]
     >
     Questo tipo di dati viene utilizzato esclusivamente per la formattazione e viene ignorato dallo schema GraphQL AEM.

## Proprietà {#properties}

Molte proprietà sono auto-esplicative, qui sotto ulteriori dettagli per alcune proprietà:

* **Nome proprietà**

  Quando aggiorni manualmente questa proprietà per un tipo di dati, i nomi **must** contengono *only* A-Z, a-z, 0-9 e il carattere speciale di sottolineatura &quot;_&quot;.

  >[!CAUTION]
  >
  Se i modelli creati in versioni precedenti di AEM contengono caratteri non validi, rimuovi o aggiorna tali caratteri.

* **Rendering come**

  Le varie opzioni per la realizzazione/il rendering del campo in un frammento. Spesso questo consente di definire se l’autore visualizzerà una singola istanza del campo o se potrà creare più istanze. Quando si utilizza **Campo multiplo** è possibile definire il numero minimo e massimo di elementi. Per ulteriori dettagli, vedere [Convalida](#validation).

* **Etichetta campo**
L&#39;immissione di un&#39;etichetta **Campo** genera automaticamente un **Nome proprietà**, che può essere aggiornato manualmente se necessario.

* **Convalida**
La convalida di base è disponibile tramite meccanismi quali la proprietà **Obbligatorio**. Alcuni tipi di dati dispongono di campi di convalida aggiuntivi. Vedi [Convalida](#validation) per ulteriori dettagli.

* Per il tipo di dati **Testo su più righe** è possibile definire il **Tipo predefinito** come:

   * **Formato RTF**
   * **Markdown**
   * **Testo normale**

  Se non viene specificato diversamente, per questo campo viene utilizzato il valore predefinito **Rich Text**.

  La modifica del **Tipo predefinito** in un modello per frammenti di contenuto avrà effetto solo su un frammento esistente correlato, dopo che il frammento è stato aperto nell&#39;editor e salvato.

* **Univoco**
Il contenuto (per il campo specifico) deve essere univoco in tutti i frammenti di contenuto creati dal modello corrente.

  Questo viene utilizzato per impedire agli autori di contenuti di ripetere contenuti già aggiunti in un altro frammento dello stesso modello.

  Ad esempio, un campo **Testo a riga singola** denominato `Country` nel modello per frammenti di contenuto non può avere il valore `Japan` in due frammenti di contenuto dipendenti. Viene visualizzato un avviso quando si tenta di eseguire la seconda istanza.

  >[!NOTE]
  >
  L’unicità è assicurata da directory principale lingua.

  >[!NOTE]
  >
  Le varianti possono avere lo stesso valore *unico* come varianti dello stesso frammento, ma non lo stesso valore utilizzato in qualsiasi variante di altri frammenti.

* Vedi **[Riferimento contenuto](#content-reference)** per ulteriori dettagli su quel tipo di dati specifico e sulle relative proprietà.

* Vedi **[Riferimento frammento (frammenti nidificati)](#fragment-reference-nested-fragments)** per ulteriori dettagli su quel tipo di dati specifico e sulle relative proprietà.

* **Traducibile**

  Selezionando la casella di controllo **Traducibile** in un campo dell’editor modelli di frammenti di contenuto:

   * Fa sì che il nome della proprietà del campo sia aggiunto alla configurazione di traduzione, al contesto `/content/dam/<sites-configuration>`, se non già presente.
   * Per GraphQL: impostare una proprietà `<translatable>` nel campo Frammento di contenuto su `yes`, per consentire al filtro query GraphQL di restituire output JSON con solo contenuto traducibile.

## Convalida {#validation}

Diversi tipi di dati includono ora la possibilità di definire requisiti di convalida per l’immissione di contenuto nel frammento risultante:

* **Testo su riga singola**
   * Confronta con un regex predefinito.
* **Numero**
   * Verifica la presenza di valori specifici.
* **Riferimento contenuto**
   * Controlla tipi specifici di contenuto.
   * È possibile fare riferimento solo alle risorse di dimensioni file specificate o inferiori.
   * È possibile fare riferimento solo alle immagini entro un intervallo di larghezza e/o altezza predefinito (in pixel).
* **Riferimento frammento**
   * Verifica un modello per frammenti di contenuto specifico.
* **Numero minimo di elementi** / **Numero massimo di elementi**

  I campi definiti come **Campo multiplo** (impostati con **Rendering come**) dispongono delle opzioni seguenti:

   * **Numero minimo di elementi**
   * **Numero massimo di elementi**

  Convalidati nell&#39;[Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md).

## Utilizzo di riferimenti per creare contenuti nidificati {#using-references-to-form-nested-content}

I frammenti di contenuto possono formare contenuto nidificato utilizzando uno dei seguenti tipi di dati:

* **[Riferimento contenuto](#content-reference)**
   * Fornisce un semplice riferimento ad altri contenuti; di qualsiasi tipo.
   * Può essere configurato per uno o più riferimenti (nel frammento risultante).

* **[Riferimento frammento](#fragment-reference-nested-fragments)** (frammenti nidificati)
   * Fa riferimento ad altri frammenti, a seconda dei modelli specifici indicati.
   * Consente di includere/recuperare dati strutturati.
     >[!NOTE]
     >
     Questo metodo è particolarmente interessante quando si utilizza [Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
   * Può essere configurato per uno o più riferimenti (nel frammento risultante).

>[!NOTE]
>
L’AEM ha una protezione da recidiva per:
>
* Riferimenti contenuto
In questo modo si impedisce all’utente di aggiungere un riferimento al frammento corrente e si potrebbe creare una finestra di dialogo di selezione Riferimento frammento vuota.
>
* Riferimenti frammento in GraphQL
Se crei una query approfondita che restituisce più frammenti di contenuto a cui si fa riferimento l’un l’altro, alla prima occorrenza restituisce null.

>[!CAUTION]
>
Se esegui una query su più frammenti a cui si fa riferimento, non è consigliabile che i vari modelli di frammenti abbiano nomi di campo con lo stesso nome, ma tipi diversi.
>
Per ulteriori dettagli vedi [API GraphQL AEM per l&#39;utilizzo con frammenti di contenuto - Limitazioni](/help/headless/graphql-api/content-fragments.md#limitations)

### Riferimento contenuto {#content-reference}

Il Riferimento contenuto consente di eseguire il rendering del contenuto da un’altra origine, ad esempio un’immagine, una pagina o un frammento di esperienza.

Oltre alle proprietà standard puoi specificare:

* Il **percorso principale**, che specifica dove memorizzare qualsiasi contenuto a cui si fa riferimento
  >[!NOTE]
  >
  Questo è obbligatorio se desideri caricare e fare riferimento direttamente alle immagini in questo campo quando utilizzi l’editor di frammenti di contenuto.
  >
  Per ulteriori dettagli, vedi [Immagini di riferimento](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images).

* I tipi di contenuto a cui è possibile fare riferimento
  >[!NOTE]
  >
  Devono includere **Immagine** se desideri caricare e fare riferimento direttamente alle immagini in questo campo quando utilizzi l&#39;editor di frammenti di contenuto.
  >
  Per ulteriori dettagli, vedi [Immagini di riferimento](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images).

* Le limitazioni per le dimensioni dei file
* Se si fa riferimento a un’immagine:
   * Mostra miniatura
   * Limiti di altezza e larghezza dell’immagine

![Riferimento contenuto](assets/cf-cfmodels-content-reference.png)

### Riferimento frammento (frammenti nidificati) {#fragment-reference-nested-fragments}

Il riferimento frammento fa riferimento a uno o più frammenti di contenuto. Questa funzione è particolarmente interessante per il recupero dei contenuti da utilizzare nell’app, in quanto consente di recuperare dati strutturati con più livelli.

Ad esempio:

* Un modello che definisce i dettagli di un dipendente, tra cui:
   * Un riferimento al modello che definisce il datore di lavoro (azienda)

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
>
I riferimenti ai frammenti sono di particolare interesse per la [distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).

Oltre alle proprietà standard puoi definire:

* **Rendering come**:

   * **multifield**: l’autore del frammento può creare più riferimenti individuali

   * **fragmentreference**: consente all’autore del frammento di selezionare un singolo riferimento a un frammento

* **Tipo di modello**
È possibile selezionare più modelli. Quando si aggiungono riferimenti a un frammento di contenuto, tutti i frammenti a cui si fa riferimento devono essere stati creati utilizzando questi modelli.

* **Percorso radice**

Specifica un percorso radice per tutti i frammenti a cui si fa riferimento.

* **Consenti creazione di frammenti**

  Questo consente all’autore del frammento di creare un frammento basato sul modello appropriato.

   * **fragmentreferencecomposite**: consente all’autore del frammento di creare un elemento composito selezionando più frammenti

  ![Riferimento frammento](assets/cf-cfmodels-fragment-reference.png)

>[!NOTE]
>
È presente un meccanismo di protezione per evitare le ricorrenze. Non consente all’utente di selezionare il frammento di contenuto corrente nel riferimento frammento e può causare una finestra di dialogo vuota per la selezione del riferimento frammento.
>
In GraphQL è inoltre disponibile una protezione di ricorrenza per i riferimenti di frammenti. Se crei una query approfondita tra due frammenti di contenuto che si riferiscono l’uno all’altro, restituisce null.

## Abilitazione o disabilitazione di un modello per frammenti di contenuto {#enabling-disabling-a-content-fragment-model}

Puoi **Abilitare** o **Disabilitare** i modelli per frammenti di contenuto per il controllo completo sul loro utilizzo.

### Abilitazione di un modello per frammenti di contenuto {#enabling-a-content-fragment-model}

Una volta creato, il modello deve essere abilitato in modo che:

* Può essere selezionato quando si crea un frammento di contenuto.
* Possibilità di utilizzarlo come riferimento all’interno di un modello per frammento di contenuto
* Possibilità di utilizzarlo in GraphQL, affinché venga generato lo schema

Per abilitare un modello contrassegnato come:

* **Bozza**: nuova (mai abilitata).
* **Disabilitato**: che è stato specificamente disabilitato

puoi utilizzare l’opzione **Abilita** dalle seguenti aree:

* Dalla barra degli strumenti superiore, quando è selezionato il modello richiesto.
* Con l’azione rapida corrispondente (passando il mouse sul modello richiesto).

![Abilitare un modello in stato Bozza o Disabilitato](assets/cf-cfmodels-status-enable.png)

### Disabilitazione di un modello per frammenti di contenuto {#disabling-a-content-fragment-model}

Un modello può anche essere disabilitato, con i seguenti risultati:

* Il modello non sarà più disponibile come base per la creazione di *nuovi* frammenti di contenuto.
* Tuttavia:
   * Lo schema GraphQL continua a essere generato ed è ancora interrogabile (per evitare di influenzare l’API JSON).
   * È comunque possibile eseguire query su qualsiasi frammento di contenuto basato sul modello e restituirlo dall’endpoint GraphQL.
* Non è più possibile fare riferimento al modello, ma i riferimenti esistenti vengono mantenuti intatti e possono ancora essere interrogati e restituiti dall’endpoint GraphQL.

Per disabilitare un modello contrassegnato come **Abilitato**, utilizzare l&#39;opzione **Disabilita** da:

* Dalla barra degli strumenti superiore, quando è selezionato il modello richiesto.
* Con l’azione rapida corrispondente (passando il mouse sul modello richiesto).

![Disattivare un modello abilitato](assets/cf-cfmodels-status-disable.png)

## Consentire modelli per frammenti di contenuto nella cartella delle risorse {#allowing-content-fragment-models-assets-folder}

Per implementare la governance dei contenuti, puoi configurare dei **Criteri** nella cartella Risorse per controllare quali modelli per frammenti di contenuto sono consentiti per la creazione di frammenti in tale cartella.

>[!NOTE]
>
Il meccanismo è simile a [consentire modelli di pagina](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author) per una pagina e i relativi elementi secondari, nelle proprietà avanzate di una pagina.

Per configurare i **Criteri** dei **Modelli per frammenti di contenuto consentiti**:

1. Naviga e apri **Proprietà** per la cartella Risorse desiderata.

1. Apri la scheda **Criteri**, dove puoi configurare:

   * **Ereditato da`<folder>`**

     I criteri vengono ereditati automaticamente durante la creazione di nuove cartelle secondarie; il criterio può essere riconfigurato (interrompendo l’ereditarietà) se le sottocartelle devono consentire modelli diversi dalla cartella principale.

   * **Modelli per frammenti di contenuto consentiti per percorso**

     Possono essere consentiti più modelli.

   * **Modelli per frammenti di contenuto consentiti per tag**

     Possono essere consentiti più modelli.

   ![Criterio del modello per frammento di contenuto](assets/cf-cfmodels-policy-assets-folder.png)

1. **Salva** eventuali modifiche.

I modelli per frammenti di contenuto consentiti per una cartella vengono risolti come segue:
* I **Criteri** dei **Modelli per frammenti di contenuto consentiti**.
* Se vuoto, prova a determinare il criterio utilizzando le regole di ereditarietà.
* Se la catena di ereditarietà non fornisce un risultato, consulta la sezione Configurazione di **Servizi cloud** per quella cartella (anche prima direttamente e poi tramite ereditarietà).
* Se nessuno dei risultati di cui sopra fornisce risultati, allora non ci sono modelli consentiti per quella cartella.

## Eliminazione di un modello per frammenti di contenuto {#deleting-a-content-fragment-model}

>[!CAUTION]
>
L’eliminazione di un modello per frammenti di contenuto può influire sui frammenti dipendenti.

Per eliminare un modello per frammenti di contenuto:

1. Passa a **Strumenti**, **Generale**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello Frammento di contenuto.
1. Seleziona il modello e poi **Elimina** dalla barra degli strumenti.

   >[!NOTE]
   >
   Se al modello viene fatto riferimento, viene visualizzato un avviso che consente di eseguire le azioni appropriate.

## Pubblicazione di un modello per frammenti di contenuto {#publishing-a-content-fragment-model}

I modelli per frammenti di contenuto devono essere pubblicati quando/prima della pubblicazione di qualsiasi frammento di contenuto dipendente.

Per pubblicare un modello per frammenti di contenuto:

1. Passa a **Strumenti**, **Generale**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello Frammento di contenuto.
1. Seleziona il modello e poi **Pubblica** dalla barra degli strumenti.
Lo stato di pubblicazione viene visualizzato nella console.

   >[!NOTE]
   >
   Se pubblichi un frammento di contenuto per il quale il modello non è ancora stato pubblicato, un elenco di selezione lo indicherà e il modello verrà pubblicato con il frammento.

## Annullamento della pubblicazione di un modello per frammenti di contenuto {#unpublishing-a-content-fragment-model}

È possibile annullare la pubblicazione dei modelli per frammenti di contenuto se nessun frammento vi fa riferimento.

Per annullare la pubblicazione di un modello per frammenti di contenuto:

1. Passa a **Strumenti**, **Generale**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello per frammenti di contenuto.
1. Seleziona il modello e poi **Annulla pubblicazione** dalla barra degli strumenti.
Lo stato di pubblicazione viene indicato nella console.

Se tenti di annullare la pubblicazione di un modello attualmente utilizzato da uno o più frammenti, viene visualizzato un avviso di errore. Ad esempio:

![Messaggio di errore di modello per frammenti di contenuto quando si annulla la pubblicazione di un modello in uso](assets/cf-cfmodels-unpublish-error.png)

Il messaggio suggerisce di controllare il pannello [Riferimenti](/help/sites-cloud/authoring/basic-handling.md#references) per approfondire l&#39;analisi:

![Modello per frammenti di contenuto nei riferimenti](assets/cf-cfmodels-references.png)

## Modelli per frammenti di contenuto bloccati (pubblicati) {#locked-published-content-fragment-models}

Questa funzione garantisce la governance dei modelli per frammenti di contenuto pubblicati.

### La sfida {#the-challenge}

* I modelli per frammenti di contenuto determinano lo schema per le query GraphQL in AEM.

   * Gli schemi GraphQL AEM vengono creati non appena viene creato un modello per frammenti di contenuto e possono esistere sia nell’ambiente di creazione che in quello di pubblicazione.

   * Gli schemi in fase di pubblicazione sono i più critici in quanto forniscono le basi per la consegna live di contenuti di frammenti di contenuto in formato JSON.

* Possono verificarsi problemi quando i modelli per frammenti di contenuto vengono modificati o in altre parole modificate. Ciò significa che lo schema cambia, e questo può di conseguenza influenzare le query GraphQL esistenti.

* L’aggiunta di nuovi campi a un modello per frammenti di contenuto non dovrebbe avere effetti negativi, in genere. Tuttavia, la modifica dei campi dati esistenti (ad esempio il nome) o l’eliminazione delle definizioni dei campi interromperà le query GraphQL esistenti quando richiedono questi campi.

### Requisiti {#the-requirements}

* Per sensibilizzare gli utenti sui rischi derivanti dalla modifica di modelli già utilizzati per la distribuzione di contenuti live, in altre parole, di modelli pubblicati.

* Inoltre, per evitare modifiche non desiderate.

Uno di questi criteri potrebbe interrompere le query se i modelli modificati vengono ripubblicati.

### Soluzione {#the-solution}

Per risolvere questi problemi, i modelli di frammento di contenuto sono *bloccati* in modalità di SOLA LETTURA su autore, non appena sono stati pubblicati. Questo stato è indicato da **Bloccato**:

![Scheda del modello per frammenti di contenuto bloccato](assets/cf-cfmodels-locked.png)

Quando il modello è **Bloccato** (in modalità di SOLA LETTURA), è possibile visualizzare il contenuto e la struttura dei modelli, ma non è possibile modificarli.

Puoi gestire i modelli **Bloccati** dalla console o dall’editor modelli:

* Console

  Dalla console, è possibile gestire la modalità SOLA LETTURA con le azioni **Sblocca** e **Blocca** nella barra degli strumenti:

  ![Barra degli strumenti del modello per frammenti di contenuto bloccato](assets/cf-cfmodels-locked.png)

   * È possibile **Sbloccare** un modello per abilitare le modifiche.

     Se selezioni **Sblocca** viene visualizzato un avviso ed è necessario confermare l&#39;azione **Sblocca**:
     ![Messaggio relativo allo sblocco del modello per frammenti di contenuto](assets/cf-cfmodels-unlock-message.png)

     Puoi quindi aprire il modello per la modifica.

   * Puoi anche **Bloccare** successivamente il modello.
   * La ripubblicazione del modello lo riporta immediatamente in modalità **Bloccato** (SOLA LETTURA).

* Editor modelli

   * Quando apri un modello bloccato, viene visualizzato un avviso e vengono presentate tre azioni: **Annulla**, **Visualizza sola lettura**, **Modifica**:

     ![Messaggio relativo alla visualizzazione di un modello per frammenti di contenuto bloccato](assets/cf-cfmodels-editor-lock-message.png)

   * Se si seleziona **Visualizza sola lettura**, è possibile visualizzare il contenuto e la struttura del modello:

     ![Visualizza solo lettura: modello per frammenti di contenuto bloccato](assets/cf-cfmodels-editor-locked-view-only.png)

   * Se selezioni **Modifica**, puoi modificare e salvare gli aggiornamenti:

     ![Modifica: modello per frammenti di contenuto bloccato](assets/cf-cfmodels-editor-locked-edit.png)

     >[!NOTE]
     >
     Potrebbe ancora essere presente un avviso nella parte superiore, ma si verifica quando il modello è già utilizzato da frammenti di contenuto esistenti.

   * **Annulla** ti riporta alla console.
