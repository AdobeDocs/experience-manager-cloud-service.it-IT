---
title: Authoring dei frammenti di contenuto
description: Scopri come creare contenuti per i frammenti di contenuto, quindi creare varianti di tale contenuto in base allo scopo. Ciò offre maggiore flessibilità sia per la distribuzione headless che per l’authoring delle pagine.
feature: Content Fragments
role: User, Developer, Architect
source-git-commit: 2fa22bf2feb6b8697877b345bc29821e30b1c6a1
workflow-type: tm+mt
source-wordcount: '2227'
ht-degree: 4%

---


# Authoring dei frammenti di contenuto {#authoring-content-fragments}

L’authoring dei frammenti di contenuto si concentra sia sulla distribuzione headless che sull’authoring delle pagine.

Sono disponibili due editor per i frammenti di contenuto. L’editor descritto in questa sezione:

* è stato sviluppato per la distribuzione di contenuti headless (anche se può essere utilizzato per tutti gli scenari)
* è disponibile da **Frammenti di contenuto** console

Questo editor fornisce:

* [Salvataggio automatico](#saving-autosaving), per evitare la perdita accidentale di modifiche.
* [Caricamento in linea di risorse come riferimenti a contenuti](#reference-images), senza doverli caricare prima in Asset DAM.
* [Anteprima](#preview-content-fragment) dell’esperienza sottoposta a rendering fornita dal frammento di contenuto.
* Possibilità di [Pubblica](#publish-content-fragment) e [Annulla pubblicazione](#unpublish-content-fragment) dall’editor.
* Possibilità di [visualizzare e aprire le copie per lingua associate](#view-language-copies) nell’editor.
* Possibilità di [visualizza dettagli versione](#view-version-history) nell’editor.
   * Puoi anche ripristinare una versione selezionata.
* Possibilità di [visualizzare e aprire i riferimenti padre](#view-parent-references).
* Una visualizzazione gerarchica del frammento di contenuto e dei relativi riferimenti, utilizzando [Struttura ad albero](#structure-tree).

>[!CAUTION]
>
>L’editor descritto in questa sezione è *solo* disponibile in *online* Adobe Experience Manager (AEM) as a Cloud Service.

>[!CAUTION]
>
>Per modificare un frammento di contenuto è necessario [le autorizzazioni appropriate](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Se riscontri problemi, contatta l’amministratore del sistema.
> 
>Ad esempio, se non hai `edit` autorizzazioni l’editor sarà di sola lettura.

>[!NOTE]
>
>Consulta la documentazione di Assets per informazioni complete su [Editor frammento di contenuto originale](/help/assets/content-fragments/content-fragments-variations.md) - è disponibile presso **Risorse** e **Frammenti di contenuto** console.

>[!NOTE]
>
>Se necessario, il team del progetto può personalizzare l’editor. Consulta [Personalizzazione della console e dell’editor dei frammenti di contenuto](/help/implementing/developing/extending/content-fragments-console-and-editor.md) per ulteriori dettagli.

## Editor frammento di contenuto {#content-fragment-editor}

La prima volta che apri l’Editor frammento di contenuto vengono visualizzate quattro aree principali:

* barra degli strumenti superiore: per informazioni chiave e azioni
   * un collegamento alla Console Frammenti di contenuto (icona Home)
   * informazioni sul modello e sulla cartella
   * collegamenti a [Anteprima (se per il modello è configurato il Pattern URL di anteprima predefinito)](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-fragment-model-properties)
   * [Pubblica](#publish-content-fragment), e [Annulla pubblicazione](#unpublish-content-fragment) azioni
   * un&#39;opzione per mostrare tutto **Riferimenti padre** (icona collegamento)
   * il frammento **[Stato](/help/sites-cloud/administering/content-fragments/managing.md#statuses-content-fragments)**, e le ultime informazioni salvate
   * un pulsante per passare all’editor originale (basato su Assets)
* pannello a sinistra: mostra **[Varianti](#variations)** per il frammento di contenuto e i relativi **Campi**:
   * questi collegamenti possono essere utilizzati per [Navigare nella struttura dei frammenti di contenuto](#navigate-structure)
* pannello a destra: presenta le schede [visualizzazione delle proprietà (metadati) e dei tag](#view-properties-tags), informazioni su [cronologia delle versioni](#view-version-history), e informazioni relative a qualsiasi [copie per lingua](#view-language-copies)
   * nel **Proprietà** è possibile aggiornare la scheda **Titolo** e **Descrizione** per il frammento, oppure **Variante**
* pannello centrale: mostra i campi e il contenuto effettivi della variante selezionata
   * consente di modificare il contenuto
   * se **Segnaposto scheda** I campi sono definiti all’interno del modello che vengono visualizzati qui e possono essere utilizzati per la navigazione; verranno presentati in orizzontale o come elenco a discesa

![Editor frammenti di contenuto: panoramica](assets/cf-authoring-overview.png)

>[!CAUTION]
>
>Spesso un modello per frammenti di contenuto può definire campi di dati denominati **Titolo** e **Descrizione**. Se questi campi esistono, sono definiti dall&#39;utente e possono essere aggiornati nel *pannello centrale* durante la modifica del frammento.
>
>Il frammento di contenuto e le relative varianti dispongono anche di campi di metadati (proprietà variante) denominati **Titolo** e **Descrizione**. Questi campi sono parte integrante di qualsiasi frammento di contenuto e sono stati inizialmente definiti durante la creazione del frammento. Possono essere aggiornati nella sezione *pannello destro* durante la modifica del frammento.

## Navigare nella struttura dei frammenti di contenuto {#navigate-structure}

Un singolo frammento di contenuto;

* È costituito da due livelli:

   * **[Varianti](#variations)** del frammento di contenuto
   * **Campi** : definito dal modello per frammenti di contenuto e utilizzato da ogni variante

* Può contenere diversi riferimenti.

### Varianti e campi {#variations-and-fields}

Nel pannello a sinistra puoi vedere:

* l&#39;elenco di **[Varianti](#variations)** che sono stati creati per questo frammento:
   * **Principale** è la variante presente al momento della creazione del frammento di contenuto, che puoi aggiungere in un secondo momento
   * puoi selezionare e aprire una variante per la modifica
   * puoi anche [crea una variante](#create-variation)
* il **Campi** all’interno del frammento e relative varianti:
   * l’icona indica [Tipo di dati](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)
   * il testo è il nome del campo
   * insieme, forniscono un collegamento diretto al contenuto del campo nel pannello centrale (per la variante corrente)

### Segui collegamenti {#follow-links}

In varie parti dell’editor viene visualizzata l’icona del collegamento. Può essere utilizzato per aprire l’elemento visualizzato, ad esempio un Modello per frammento di contenuto, un Riferimento principale o un frammento a cui si fa riferimento:

![Editor frammento di contenuto - Icona collegamento](assets/cf-authoring-link-icon.png)

### Struttura ad albero {#structure-tree}

Apri **Struttura ad albero** dalla barra degli strumenti dell’editor per visualizzare la struttura gerarchica del frammento di contenuto e i relativi riferimenti. Utilizza le icone dei collegamenti per passare ai riferimenti.

![Editor frammento di contenuto - Struttura](assets/cf-authoring-structure-tree.png)

>[!NOTE]
>
>Consulta [Analisi della struttura dei frammenti di contenuto - Struttura](/help/sites-cloud/administering/content-fragments/analysis.md#structure-tree) per ulteriori dettagli.

## Salvataggio e salvataggio automatico {#saving-autosaving}

<!-- CHECK: cannot be saved, no undo, redo -->

Con ogni aggiornamento effettuato, il frammento di contenuto viene salvato automaticamente. L’ultimo salvataggio viene visualizzato nella barra degli strumenti superiore.

## Varianti {#variations}

[Varianti](/help/sites-cloud/administering/content-fragments/overview.md#main-and-variations) sono una funzione significativa dei frammenti di contenuto dell’AEM. Consentono di creare e modificare copie del **Principale** contenuti da utilizzare su canali e scenari specifici, per rendere ancora più flessibili la distribuzione di contenuti headless e l’authoring delle pagine.

Dall’editor è possibile:

* [Creare varianti](#create-variation) del **Principale** contenuto

* Seleziona la variante richiesta per la modifica del contenuto

* [Rinomina la variante](#rename-variation)

* [Eliminare una variante](#delete-variation)

### Crea una variante {#create-variation}

Per creare una variante del frammento di contenuto:

1. Nel pannello a sinistra, seleziona la **segno più** (**Crea variante**) a destra di **Varianti**.

   >[!NOTE]
   >
   >Dopo aver creato la prima variante, le varianti esistenti vengono elencate nello stesso pannello.

   ![Editor frammento di contenuto: creare la prima variante](assets/cf-authoring-create-variation-01.png)

1. Nella finestra di dialogo, immetti un **Titolo** per la variante, e una **Descrizione** se necessario:

   ![Editor frammento di contenuto - Finestra di dialogo Crea variante](assets/cf-authoring-create-variation-02.png)

1. **Crea** la variante. Viene visualizzato nell&#39;elenco.

### Rinominare una variante {#rename-variation}

Per rinominare un **Variante**:

1. Seleziona la variante desiderata.

1. Apri **Proprietà** nel pannello di destra.

1. Aggiornare la variante **Titolo**.

1. Premere **Ritorno** o spostarsi in un altro campo per salvare automaticamente la modifica. Il titolo viene aggiornato nel **Varianti** a sinistra.


### Eliminare una variante {#delete-variation}

Per eliminare una variante del frammento di contenuto:

>[!NOTE]
>
>Impossibile eliminare **Principale**.

1. Seleziona la Variante.

1. In **Variante** , seleziona l’icona Elimina (Cestino):

   ![Editor frammento di contenuto - Icona Elimina variante](assets/cf-authoring-delete-variation.png)

1. Viene visualizzata una finestra di dialogo. Seleziona **Elimina** per confermare l’azione.

## Modifica campi di testo su più righe - Testo normale o Markdown {#edit-multi-line-text-fields-plaintext-markdown}

**[Testo su più righe](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)** i campi possono avere uno dei tre formati seguenti:

* Testo normale
* [Markdown](/help/sites-cloud/administering/content-fragments/markdown.md)
* [Testo formattato](#edit-multi-line-text-fields-rich-text)

I campi definiti come Testo normale o Markdown hanno una casella di testo semplice, senza opzioni di formattazione (su schermo):

![Editor frammento di contenuto - Testo su più righe - Schermo intero](assets/cf-authoring-multilinetext-plaintext-markdown.png)

## Modifica campi di testo su più righe - Testo formattato {#edit-multi-line-text-fields-rich-text}

Per **[Testo su più righe](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)** campi definiti come **Rich Text** Sono disponibili varie funzioni:

* Modifica il contenuto:
   * Annulla/Ripeti
   * Incolla/Incolla come testo
   * Copiare
   * Seleziona formato paragrafo
   * Crea/gestisci tabella
   * Formato testo; grassetto, corsivo, sottolineato, colore
   * Imposta allineamento paragrafo
   * Crea/gestisci elenchi; puntati, numerati
   * Rientro testo; riduzione, aumento
   * Cancella formattazione corrente
   * Inserisci collegamenti
   * Selezionare e inserire riferimenti a risorse immagine
   * Aggiungi caratteri speciali
* [Editor a schermo intero](#full-screen-editor-rich-text) - alternare tra le modalità a schermo intero e in flusso
* [Statistiche](#statistics-rich-text)
* [Confronta e sincronizza](#compare-and-synchronize-rich-text)

Ad esempio:

![Editor frammento di contenuto - Testo su più righe - Attiva/Disattiva schermo intero](assets/cf-authoring-multilinetext-fullscreen-toggle.png)

>[!NOTE]
>
>I campi di testo su più righe sono inoltre contrassegnati dal simbolo [icona](#fields-datatypes-icons) nel **Campi** pannello.

### Editor a schermo intero - Rich Text {#full-screen-editor-rich-text}

L’editor a schermo intero offre le stesse opzioni di modifica disponibili durante il flusso, ma offre più spazio per il testo.

Ad esempio:

![Editor frammento di contenuto - Testo su più righe - Schermo intero](assets/cf-authoring-multilinetext-fullscreen.png)

### Statistiche - Rich Text {#statistics-rich-text}

L&#39;azione **Statistiche** visualizza un intervallo di informazioni sul testo in un campo Multiriga.

Ad esempio:

![Editor frammento di contenuto - Statistiche](assets/cf-authoring-multilinetext-statistics.png)

### Confronta e sincronizza - Testo formattato {#compare-and-synchronize-rich-text}

L&#39;azione **Confronta** è disponibile per i campi su più righe quando si dispone di un **Variante** apri.

Questo apre il campo Multiriga a schermo intero e:

* visualizza il contenuto di entrambi **Principale** e l&#39;attuale **Variante** in parallelo, con le eventuali differenze evidenziate

* le differenze sono indicate dal colore:

   * Il contenuto aggiunto alla variante è indicato in verde
   * II contenuto rimosso dalla variante è indicato in rosso
   * Il testo sostituito è indicato in blu.

* fornisce **Sincronizza** , che sincronizza il contenuto da **Principale** alla variante corrente

   * se **Principale** è stato aggiornato, queste modifiche verranno trasferite nella variante
   * se la variante è stata aggiornata, queste modifiche verranno sovrascritte dal contenuto di **Principale**

  >[!CAUTION]
  >
  >La sincronizzazione è disponibile solo per copiare le modifiche *da **Principale**alla variante*.
  >
  >Trasferimento delle modifiche *da una variante a **Principale*** non è disponibile come opzione.

Ad esempio, uno scenario in cui il contenuto della variante è stato completamente riscritto, in modo che una sincronizzazione sostituisca quel nuovo contenuto con il contenuto di **Principale**:

![Editor frammento di contenuto: confronto e sincronizzazione](assets/cf-authoring-multilinetext-compare.png)

## Gestisci riferimenti {#manage-references}

### Riferimenti ai frammenti {#fragment-references}

[Riferimenti frammento](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#fragment-reference-nested-fragments) può essere utilizzato per:

* [creare un riferimento a un frammento di contenuto esistente](#create-reference-existing-content-fragment)
* [creare un frammento di contenuto e quindi farvi riferimento](#create-reference-content-fragment)

#### Creare un riferimento a un frammento di contenuto esistente {#create-reference-existing-content-fragment}

Per creare un riferimento a un frammento di contenuto esistente:

1. Seleziona il campo.
1. Seleziona **Aggiungi frammento esistente**.
1. Seleziona il frammento richiesto dal selettore di frammenti.

   >[!NOTE]
   >
   >È possibile selezionare un solo frammento alla volta.

#### Creare un frammento di contenuto e un riferimento {#create-reference-content-fragment}

In alternativa, è possibile: [seleziona **Crea nuovo frammento** per aprire **Crea** finestra di dialogo](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment). Una volta creato, viene fatto riferimento a questo frammento.

### Riferimenti al contenuto {#content-references}

[Riferimenti contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-reference) sono utilizzati per fare riferimento ad altri tipi di contenuti AEM, come immagini, pagine e frammenti di esperienza.

#### Immagini di riferimento {#reference-images}

In entrata **Riferimento contenuto** campi è possibile:

* risorse di riferimento già esistenti nell’archivio
* caricarli direttamente nel campo; questo evita la necessità di utilizzare **Risorse** console da caricare

  >[!NOTE]
  >
  >Per caricare direttamente un&#39;immagine in **Riferimento contenuto** campo, it **deve**:
  >
  >* hanno un **Percorso directory principale** definito (nel [Modello per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-reference)). Specifica dove verrà memorizzata l&#39;immagine.
  >* include **Immagine** nell’elenco dei tipi di contenuto accettati

Per aggiungere una risorsa, puoi effettuare le seguenti operazioni:

* trascina e rilascia il nuovo file di risorse direttamente (ad esempio, dal file system) nella sezione **Riferimento contenuto** campo
* utilizzare il **Aggiungi risorsa** , quindi selezionare una delle seguenti opzioni **Sfoglia risorse** o **Carica** per aprire il selettore appropriato da utilizzare:

  ![Editor frammento di contenuto - Opzioni di aggiunta risorsa](assets/cf-authoring-add-asset-options.png)

#### Pagine di riferimento {#reference-pages}

Per aggiungere riferimenti a pagine AEM, frammenti di esperienza o altri tipi di contenuto:

1. Seleziona **Aggiungi percorso contenuto**.

1. Aggiungi il percorso richiesto nel campo di input.

1. Conferma con **Aggiungi**.

### Visualizza riferimenti padre {#view-parent-references}

Selezionando l’icona del collegamento nella barra degli strumenti superiore si apre un elenco di tutti i riferimenti principali.

Ad esempio:

![Editor frammento di contenuto - Mostra riferimenti](assets/cf-authoring-show-references-link.png)

Viene visualizzata una finestra in cui sono elencati tutti i riferimenti correlati. Per aprire un riferimento, selezionate il nome o il titolo o l&#39;icona del collegamento.

Ad esempio:

![Editor frammento di contenuto - Mostra riferimenti](assets/cf-authoring-show-references.png)

## Visualizza proprietà e tag {#view-properties-tags}

Nella scheda delle proprietà del pannello di destra, è possibile visualizzare le proprietà (metadati) e i tag. Le proprietà possono essere:

* per **Frammento di contenuto** - se **Principale** è attualmente selezionato
* per uno specifico **Variante**

![Editor frammento di contenuto - Proprietà](assets/cf-authoring-properties.png)

### Modifica proprietà e tag {#edit-properties-tags}

Nella scheda delle proprietà (pannello a destra) puoi anche modificare:

* **Titolo**
* **Descrizione**
* **Tag**: utilizzando il menu a discesa o la finestra di dialogo per selezione

  ![Editor frammento di contenuto - Gestisci tag](assets/cf-authoring-edit-tags.png)

### Aprire il modello per frammenti di contenuto {#open-content-fragment-model}

Quando hai **Principale** Se è selezionata, il nome del modello per frammenti di contenuto sottostante viene visualizzato nella sezione delle proprietà. Selezionando l’icona del collegamento, apre il modello in una scheda separata.

Ad esempio:

![Editor frammento di contenuto: apri modello per frammento di contenuto](assets/cf-authoring-open-model.png)

## Visualizzare la cronologia delle versioni {#view-version-history}

In **Cronologia versioni** nel pannello a destra vengono visualizzati i dettagli delle versioni corrente e precedente:

>[!NOTE]
>
>Al momento della pubblicazione del frammento di contenuto viene creata una nuova versione.

![Editor frammenti di contenuto: panoramica della cronologia delle versioni](assets/cf-authoring-version-history-overview.png)

### Ripristina una versione {#revert-version}

Puoi ripristinare qualsiasi versione.

Per ripristinare una versione specifica:

1. Seleziona l’icona dei tre punti accanto alla versione.

1. Seleziona **Ripristina**.

![Editor frammento di contenuto - Ripristino cronologia versioni](assets/cf-authoring-version-history-revert.png)

## Visualizzare le copie per lingua {#view-language-copies}

In **Proprietà lingua** vengono visualizzati i dettagli delle schede di eventuali copie per lingua correlate. Selezionando un’icona di collegamento, apre la copia in una scheda separata.

Ad esempio:

![Editor frammento di contenuto: apri copia per lingua](assets/cf-authoring-open-language-copies.png)

>[!NOTE]
>
>Per ulteriori dettagli sulla traduzione di un frammento di contenuto e sulla creazione di copie per lingua, vedi [Percorso di traduzione AEM headless](/help/journey-headless/translation/overview.md).


## Visualizzare l’anteprima del frammento {#preview-content-fragment}

L’editor dei frammenti di contenuto offre agli autori la possibilità di visualizzare in anteprima le modifiche apportate in un’applicazione front-end esterna.

Per utilizzare questa funzione, devi innanzitutto:

* Collabora con il tuo team IT per configurare l’applicazione front-end esterna che eseguirà il rendering del frammento di contenuto consumando il relativo output JSON.
* Una volta configurata l&#39;applicazione front-end esterna, **Pattern URL anteprima predefinito** deve essere definito come [proprietà del modello per frammenti di contenuto appropriato](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties).

Una volta definito l’URL, il **Anteprima** è attivo. Puoi selezionare questo pulsante per avviare l’applicazione esterna (in una scheda separata) per eseguire il rendering del frammento di contenuto.

## Pubblicare il frammento {#publish-content-fragment}

È possibile **Pubblica** il frammento su:

* Anteprima istanza
* Istanza Publish

Puoi pubblicare il frammento dall’editor o dalla console. Consulta [Pubblicazione e anteprima di un frammento](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment) per informazioni dettagliate.

## Annullare la pubblicazione del frammento {#unpublish-content-fragment}

È inoltre possibile **Annulla pubblicazione** frammento da:

* Anteprima istanza
* Istanza Publish

Puoi annullare la pubblicazione del frammento dall’editor o dalla console. Consulta [Annullamento della pubblicazione di un frammento](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment) per informazioni dettagliate.

## Campi, tipi di dati e icone {#fields-datatypes-icons}

Il **Campi** nel pannello sono elencati tutti i campi all’interno del frammento di contenuto. L’icona indica **[Tipo di dati](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)**:

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><p><b>Testo su riga singola</b></p> </td>
   <td><p> <img src="assets/cf-authoring-single-line-text-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Testo su più righe</b></p> </td>
   <td><p> <img src="assets/cf-authoring-multi-line-text-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Numero</b></p> </td>
   <td><p> <img src="assets/cf-authoring-number-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Booleano</b></p> </td>
   <td><p> <img src="assets/cf-authoring-boolean-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Data e ora</b></p> </td>
   <td><p> <img src="assets/cf-authoring-date-time-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Enumerazione</b></p> </td>
   <td><p> <img src="assets/cf-authoring-enumeration-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Tag</b></p> </td>
   <td><p> <img src="assets/cf-authoring-tags-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Riferimento contenuto</b></p> </td>
   <td><p> <img src="assets/cf-authoring-content-reference-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Riferimento frammento</b></p> </td>
   <td><p> <img src="assets/cf-authoring-fragment-reference-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Oggetto JSON</b></p> </td>
   <td><p> <img src="assets/cf-authoring-json-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Segnaposto scheda</b></p><p>Anche se non rappresentata da un'icona effettiva, una <b>Segnaposto scheda</b> è rappresentato nel pannello sinistro. <br>È anche rappresentato nel pannello centrale, orizzontalmente come mostrato, o in un elenco a discesa (quando ce ne sono troppi da mostrare orizzontalmente).</p> </td>
   <td><p> <img src="assets/cf-authoring-tab-icon.png"> </p></td>
  </tr>
 </tbody>
</table>
