---
title: Definizione dei modelli per frammenti di contenuto
description: Scopri come i modelli per frammenti di contenuto fungono da base per i frammenti di contenuto in AEM, consentendo di creare contenuti strutturati da utilizzare nella distribuzione headless o nell’authoring delle pagine.
feature: Content Fragments
role: User, Developer, Architect
exl-id: 8ab5b15f-cefc-45bf-a388-928e8cc8c603
solution: Experience Manager Sites
source-git-commit: 416cb98fbf48885688ee70d63e606e3f7c90f9f8
workflow-type: tm+mt
source-wordcount: '2201'
ht-degree: 31%

---

# Definizione dei modelli per frammenti di contenuto {#defining-content-fragment-models}

I modelli per frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service definiscono la struttura per il contenuto dei [frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md). Questi frammenti possono quindi essere utilizzati per l’authoring delle pagine o come base per i contenuti headless.

Questa pagina illustra come definire il modello per frammenti di contenuto utilizzando l’editor dedicato. Consulta [Gestione dei modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) per ulteriori attività e opzioni disponibili dopo la creazione dei frammenti, tra cui [azioni disponibili nella Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#actions), [autorizzazione del modello nella cartella](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder) e [pubblicazione del modello](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model).

>[!CAUTION]
>
>Se esegui una query su più frammenti a cui si fa riferimento, non è consigliabile che i vari modelli di frammenti abbiano nomi di campo con lo stesso nome, ma tipi diversi.
>
>Per ulteriori dettagli vedi [API GraphQL di AEM per l&#39;utilizzo con Frammenti di contenuto - Limitazioni](/help/headless/graphql-api/content-fragments.md#limitations)

>[!NOTE]
>
>Se crei un modello con questo nuovo editor, utilizza sempre questo editor per quel modello.
>
>Se poi apri il modello con [editor modelli originale](/help/assets/content-fragments/content-fragments-models.md), verrà visualizzato il messaggio:
>
>* &quot;Questo modello ha uno schema di interfaccia utente personalizzato configurato. L’ordine dei campi visualizzati in questa interfaccia utente potrebbe non corrispondere allo schema dell’interfaccia utente. Per visualizzare i campi allineati con lo schema dell’interfaccia utente, devi passare al nuovo Editor frammento di contenuto.&quot;

## Definizione del modello per frammenti di contenuto {#defining-your-content-fragment-model}

Il modello per frammenti di contenuto definisce efficacemente la struttura dei frammenti di contenuto risultanti utilizzando una selezione di **[Tipi di dati](#data-types)**. Utilizzando l’editor modelli è possibile aggiungere istanze dei tipi di dati, quindi configurarle per creare i campi richiesti:

>[!CAUTION]
>
>La modifica di un modello già utilizzato da frammenti di contenuto esistenti può influire su tali frammenti dipendenti.

1. Nella Console Frammenti di contenuto, seleziona il pannello per [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#basic-structure-handling-content-fragment-models-console) e passa alla cartella contenente il modello per frammenti di contenuto.

   >[!NOTE]
   >
   >Puoi anche aprire un modello direttamente dopo [averlo creato](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#creating-a-content-fragment-model).

1. Apri il modello richiesto per **Modifica**. Utilizza uno dei collegamenti di azione rapida oppure seleziona il modello e quindi l&#39;azione dalla barra degli strumenti.


   ![Proprietà](assets/cf-cfmodels-empty-model.png)

   Una volta aperto, l’editor modelli mostra:

   * superiore:
      * Icona **Home**
      * opzione per passare da [original](/help/assets/content-fragments/content-fragments-models.md) al nuovo editor
      * **Annulla**
      * **Salva**

   * a sinistra: **Tipi di dati** disponibili per la creazione di campi

   * middle: campi già definiti insieme all&#39;opzione **Aggiungi**

   * a destra: utilizzando le icone all’estrema destra puoi scegliere tra:

      * **Proprietà**: definire e visualizzare le proprietà per il campo selezionato
      * **Dettagli modello**: mostra lo stato **Enabled**, **Titolo modello**, **Tag**, **Descrizione** e **URL anteprima**

1. **Per aggiungere un campo**

   * Effettua una delle seguenti operazioni:

      * Trascina un tipo di dati dal pannello di sinistra alla posizione desiderata per un campo nel pannello centrale.
      * Selezionare l&#39;icona **+** per un tipo di dati per aggiungerla alla fine dell&#39;elenco dei campi.
      * Seleziona **Aggiungi** nel pannello centrale e quindi il tipo di dati richiesto dall&#39;elenco a discesa risultante per aggiungere un campo alla fine dell&#39;elenco.

     >[!NOTE]
     >
     >**I campi segnaposto scheda** devono essere sempre visualizzati sopra i campi esistenti.

   * Puoi riposizionare un campo utilizzando la formazione di punti a sinistra della casella del campo:

     ![Sposta campo](assets/cf-cfmodels-move-field-icon.png)

   * Una volta aggiunto un campo al modello (e selezionato), il pannello di destra mostra le **Proprietà** che possono essere definite per quel particolare tipo di dati. Qui puoi definire cosa è necessario per il
campo.

      * Molte proprietà sono auto-esplicative. Per ulteriori dettagli, vedere [Proprietà (tipi di dati)](#properties).
      * La digitazione di un **Etichetta campo** completa automaticamente il **Nome proprietà** - se vuoto, e può essere aggiornato manualmente in seguito.

        >[!CAUTION]
        >
        >Quando si aggiorna manualmente la proprietà **Nome proprietà** per un tipo di dati, i nomi devono contenere *solo* caratteri A-Z, a-z, 0-9 e il carattere speciale di sottolineatura &quot;_&quot;.
        >
        >Se i modelli creati in versioni precedenti di AEM contengono caratteri non validi, rimuovi o aggiorna tali caratteri.

     Ad esempio:

     ![Proprietà campo](assets/cf-cfmodels-field-properties.png)

     >[!NOTE]
     >
     >Quando un campo è definito come **Obbligatorio**, l&#39;**Etichetta** indicata nel riquadro centrale è contrassegnata con un asterisco (**&#42;**).

1. **Per rimuovere un campo**

   Seleziona l’icona cestino per il campo appropriato nel pannello centrale.

   ![Rimuovi](assets/cf-cfmodels-remove-icon.png)

1. Aggiungi tutti i campi obbligatori e definisci le relative proprietà in base alle esigenze.

1. Seleziona **Salva** per mantenere la definizione.

## Tipi di dati {#data-types}

Per definire il modello è disponibile una selezione di tipi di dati:

* **Testo su riga singola**
   * Aggiungi un campo per una singola riga di testo; è possibile definire la lunghezza massima
   * Il campo può essere configurato per consentire agli autori di frammenti di creare nuove istanze del campo

* **Testo su più righe**
   * Area di testo che può essere RTF, Testo normale o Markdown
   * Il campo può essere configurato per consentire agli autori di frammenti di creare nuove istanze del campo

  >[!NOTE]
  >
  >Se l&#39;area di testo è RTF, Testo normale o Markdown, è definito nel modello dalla proprietà **Tipo predefinito**.
  >
  >Questo formato non può essere modificato dall&#39;[Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md), ma solo dal modello.

* **Numero**
   * Aggiungere un campo numerico
   * Il campo può essere configurato per consentire agli autori di frammenti di creare nuove istanze del campo

* **Booleano**
   * Aggiungi una casella di controllo booleana

* **Data e ora**
   * Aggiungere un campo data e/o ora

* **Enumerazione**
   * Aggiungere un set di campi Casella di controllo, Pulsante di scelta o A discesa
      * Puoi specificare le opzioni disponibili per l’autore del frammento

* **Tag**
   * Consente agli autori di frammenti di accedere alle aree dei tag e di selezionarle

* **Riferimento frammento**
   * I riferimenti ad altri frammenti di contenuto possono essere utilizzati per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Il tipo di dati può essere configurato in modo da consentire agli autori di frammenti di:
      * Modificare direttamente il frammento a cui si fa riferimento.
      * Creare un nuovo frammento di contenuto basato sul modello appropriato
      * Crea nuove istanze del campo
   * Il riferimento specifica il percorso della risorsa di riferimento, ad esempio `/content/dam/path/to/resource`

     <!--
    * Internally the reference is held as a universally unique ID (UUID) that references the resource
    * You do not need to know the UUID; in the fragment editor you can browse to the required fragment.
    -->

  <!--
  >[!NOTE]
  >
  >The UUIDs are repository specific. If you use the [Content Copy Tool](/help/implementing/developing/tools/content-copy.md) to copy Content Fragments, the UUIDs will be recalculated in the target environment.
  -->

* **Riferimento contenuto**
   * I riferimenti ad altri contenuti di qualsiasi tipo possono essere utilizzati per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Se si fa riferimento a un’immagine, è possibile scegliere di mostrare una miniatura
   * Il campo può essere configurato per consentire agli autori di frammenti di creare nuove istanze del campo
   * Il riferimento specifica il percorso della risorsa di riferimento, ad esempio `/content/dam/path/to/resource`

     <!--
    * Internally the reference is held as a universally unique ID (UUID) that references the resource
    * You do not need to know the UUID; in the fragment editor you can browse to the required asset resource
    -->

  <!--
  >[!NOTE]
  >
  >The UUIDs are repository specific. If you use the [Content Copy Tool](/help/implementing/developing/tools/content-copy.md) to copy Content Fragments, the UUIDs will be recalculated in the target environment.
  -->

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
     >Questo tipo di dati viene utilizzato esclusivamente per la formattazione e viene ignorato dallo schema GraphQL AEM.
     >
     >**I campi segnaposto scheda** devono essere sempre visualizzati sopra i campi esistenti.

## Proprietà (tipi di dati) {#properties}

Molte proprietà sono auto-esplicative, qui sotto ulteriori dettagli per alcune proprietà:

* **Nome proprietà**

  Quando aggiorni manualmente questa proprietà per un tipo di dati, i nomi **must** contengono *only* A-Z, a-z, 0-9 e il carattere speciale di sottolineatura &quot;_&quot;.

  >[!CAUTION]
  >
  >Se i modelli creati in versioni precedenti di AEM contengono caratteri non validi, rimuovi o aggiorna tali caratteri.

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
  >L’unicità è assicurata da directory principale lingua.

  >[!NOTE]
  >
  >Le varianti possono avere lo stesso valore *unico* come varianti dello stesso frammento, ma non lo stesso valore utilizzato in qualsiasi variante di altri frammenti.

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

* [Riferimento contenuto](#content-reference)
   * Fornisce un semplice riferimento ad altri contenuti; di qualsiasi tipo.
   * Fornito dal tipo di dati **Riferimento contenuto**
   * Può essere configurato per uno o più riferimenti (nel frammento risultante).

* [Riferimento frammento](#fragment-reference-nested-fragments) (frammenti nidificati)
   * Fa riferimento ad altri frammenti, a seconda dei modelli specifici indicati.
   * Fornito dal tipo di dati **Riferimento frammento**
   * Consente di includere/recuperare dati strutturati.

     >[!NOTE]
     >
     >Questo metodo è particolarmente interessante quando si utilizza [Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
   * Può essere configurato per uno o più riferimenti (nel frammento risultante).

<!--
>[!NOTE]
>
>See [Upgrade your Content Fragments for UUID References](/help/headless/graphql-api/uuid-reference-upgrade.md) for further information about Content/Fragment Reference and Content/Fragment Reference (UUID), and upgrading to the UUID-based data types.
-->

>[!NOTE]
>
>AEM dispone di protezione di ricorrenza per:
>
>* Riferimenti al contenuto
>  &#x200B;>  In questo modo si impedisce all’utente di aggiungere un riferimento al frammento corrente e si potrebbe creare una finestra di dialogo di selezione Riferimento frammento vuota.
>
>* Riferimenti frammento in GraphQL
>  &#x200B;>  Se crei una query approfondita che restituisce più frammenti di contenuto a cui si fa riferimento l’un l’altro, alla prima occorrenza restituisce null.

>[!CAUTION]
>
>Se esegui una query su più frammenti a cui si fa riferimento, non è consigliabile che i vari modelli di frammenti abbiano nomi di campo con lo stesso nome, ma tipi diversi.
>
>Per ulteriori dettagli vedi [API GraphQL di AEM per l&#39;utilizzo con Frammenti di contenuto - Limitazioni](/help/headless/graphql-api/content-fragments.md#limitations)

### Riferimento contenuto {#content-reference}

Il tipo di dati **Riferimento contenuto** consente di eseguire il rendering del contenuto da un&#39;altra origine, ad esempio immagine, pagina o frammento di esperienza.

Oltre alle proprietà standard puoi specificare:

* **Percorso principale**, che specifica o rappresenta la posizione in cui archiviare il contenuto a cui si fa riferimento
  >[!NOTE]
  >
  >Questo è obbligatorio se desideri caricare e fare riferimento direttamente alle immagini in questo campo quando utilizzi l’editor di frammenti di contenuto.
  >
  >Per ulteriori dettagli, vedi [Immagini di riferimento](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images).

* I tipi di contenuto a cui è possibile fare riferimento
  >[!NOTE]
  >
  >Devono includere **Immagine** se desideri caricare e fare riferimento direttamente alle immagini in questo campo quando utilizzi l&#39;editor di frammenti di contenuto.
  >
  >Per ulteriori dettagli, vedi [Immagini di riferimento](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images).

* Le limitazioni per le dimensioni dei file
* Se si fa riferimento a un’immagine:
   * Mostra miniatura
   * Limiti di altezza e larghezza dell’immagine

![Riferimento contenuto](assets/cf-cfmodels-content-reference.png)

### Riferimento frammento (frammenti nidificati) {#fragment-reference-nested-fragments}

Il tipo di dati **Riferimento frammento** può fare riferimento a uno o più frammenti di contenuto. Questa funzione è particolarmente interessante per il recupero dei contenuti da utilizzare nell’app, in quanto consente di recuperare dati strutturati con più livelli.

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
>I riferimenti ai frammenti sono di particolare interesse per la [distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).

Oltre alle proprietà standard puoi definire:

* **Rendering come**:

   * **multifield**: l’autore del frammento può creare più riferimenti individuali

   * **fragmentreference**: consente all’autore del frammento di selezionare un singolo riferimento a un frammento

* **Tipo di modello**
È possibile selezionare più modelli. Quando si aggiungono riferimenti a un frammento di contenuto, tutti i frammenti a cui si fa riferimento devono essere stati creati utilizzando questi modelli.

* **Percorso principale**
Specifica o rappresenta un percorso principale per tutti i frammenti a cui si fa riferimento.

* **Consenti creazione di frammenti**

  Questo consente all’autore del frammento di creare un frammento basato sul modello appropriato.

   * **fragmentreferencecomposite**: consente all’autore del frammento di creare un elemento composito selezionando più frammenti

  ![Riferimento frammento](assets/cf-cfmodels-fragment-reference.png)

>[!NOTE]
>
>È presente un meccanismo di protezione per evitare le ricorrenze. Non consente all’utente di selezionare il frammento di contenuto corrente nel riferimento frammento e può causare una finestra di dialogo vuota per la selezione del riferimento frammento.
>
>In GraphQL è inoltre disponibile una protezione di ricorrenza per i riferimenti di frammenti. Se crei una query approfondita tra due frammenti di contenuto che si riferiscono l’uno all’altro, restituisce null.
