---
title: Gestione dei frammenti di contenuto (risorse - frammenti di contenuto)
description: Scopri come utilizzare la console Assets per gestire i frammenti di contenuto AEM, che costituiscono la base dei contenuti headless.
exl-id: 333ad877-db2f-454a-a3e5-59a936455932
source-git-commit: 2a4538ad8b52615ffdee110393bfbc01f57694f4
workflow-type: tm+mt
source-wordcount: '1877'
ht-degree: 69%

---

# Gestione dei frammenti di contenuto {#managing-content-fragments}

Scopri come utilizzare la console Assets per gestire i frammenti di contenuto AEM, che costituiscono la base dei contenuti headless.

Dopo aver definito i [Modelli per frammenti di contenuto](#creating-a-content-model) puoi utilizzarli per [creare i tuoi frammenti di contenuto](#creating-a-content-fragment).

L’[Editor frammento di contenuto](#opening-the-fragment-editor) prevede svariate [modalità](#modes-in-the-content-fragment-editor) per consentirti di:

* [Modificare il contenuto](#editing-the-content-of-your-fragment) e [gestire le varianti](#creating-and-managing-variations-within-your-fragment)
* [Annotare il frammento](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Associare contenuto al frammento](#associating-content-with-your-fragment)
* [Configurare i metadati](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Visualizzare la struttura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Visualizzare un’anteprima della rappresentazione JSON](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>I frammenti di contenuto possono essere utilizzati:
>
>* quando si esegue l’authoring delle pagine; consulta [Authoring delle pagine con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* per la [distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

>[!NOTE]
>
>I frammenti di contenuto sono una funzione di Sites, ma vengono memorizzati come **Risorse**.
>
>Ora sono gestite principalmente con **[Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)** , anche se possono ancora essere gestite dalla **Risorse** console. Questa sezione riguarda la gestione da **Risorse** console.
>
>Sono disponibili due editor per l’authoring dei frammenti di contenuto. Questa sezione tratta l’editor originale, a cui si accede principalmente da **Risorse** console. Consulta la documentazione di Sites, [Frammenti di contenuto - Authoring](/help/sites-cloud/administering/content-fragments/authoring.md), per informazioni dettagliate sul nuovo editor (accessibile principalmente dal **Frammenti di contenuto** console). Entrambi gli editor dispongono di un interruttore nella barra degli strumenti superiore per consentire un accesso rapido all’altro editor.

## Creazione di frammenti di contenuto {#creating-content-fragments}

### Creazione di un modello di contenuto {#creating-a-content-model}

È possibile abilitare e creare i [modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) prima della creazione dei frammenti di contenuto con una struttura.

### Creazione di un frammento di contenuto {#creating-a-content-fragment}

Il metodo per creare un frammento di contenuto è:

1. Passa alla cartella **Risorse** in cui desideri creare il frammento.
1. Per aprire la procedura guidata, seleziona **Crea**, quindi **Frammento di contenuto**.
1. Il primo passaggio della procedura guidata richiede di specificare la base del nuovo frammento.

   * [Modello](/help/assets/content-fragments/content-fragments-models.md) : utilizzato per creare un frammento che richiede contenuto strutturato, ad esempio **Avventura** modello

      * Vengono visualizzati tutti i modelli disponibili.

   Dopo la selezione, utilizza **Successivo** per procedere.

   ![Seleziona modello di Frammento di contenuto](assets/cfm-managing-01.png)

1. Nel passaggio **Proprietà** specifica:

   * **Base**

      * **Titolo**

        Titolo del frammento.

        Obbligatorio.

      * **Descrizione**

      * **Tag**

   * **Avanzate**

      * **Nome**

        Il nome; viene utilizzato per formare l’URL.

        Obbligatorio; deriva automaticamente dal titolo, ma può essere aggiornato.

1. Seleziona **Crea** per completare l’azione, quindi **Apri** il frammento per la modifica oppure tornare alla console facendo clic su **Fine**.

   >[!NOTE]
   >In entrata **Elenco** della console è possibile aggiornare il **Impostazioni vista** per attivare **Modello per frammenti di contenuto** colonna.

## Azioni per un frammento di contenuto nella console Assets {#actions-for-a-content-fragment-assets-console}

In **Risorse** console è disponibile una serie di azioni per i frammenti di contenuto:

* Dalla barra degli strumenti; dopo aver selezionato il frammento, sono disponibili tutte le azioni appropriate.
* As [azioni rapide](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions); un sottoinsieme di azioni disponibile per le singole schede dei frammenti.

![Azioni nella barra degli strumenti](assets/cfm-managing-02.png)

Seleziona il frammento per visualizzare la barra degli strumenti con le azioni applicabili:

* **Rielabora risorse**
* **Crea**
* **Download**

   * Salva il frammento come file ZIP; puoi definire se includere elementi, varianti, metadati.

* **Pagamento**
* **Proprietà**

   * Consente di visualizzare, modificare o entrambi i metadati del frammento.

* **Modifica**

   * Consente di: [apri il frammento per la modifica del contenuto](/help/assets/content-fragments/content-fragments-variations.md) insieme ai relativi elementi, varianti, contenuti e metadati associati.

* **Pubblicazione rapida**
* **Gestisci pubblicazione**
* **Gestisci tag**
* **Alla raccolta**
* **Copia** (e **Incolla**)
* **Sposta**
* **Eliminare**

>[!NOTE]
>
>Molti di questi sono [azioni standard per Assets](/help/assets/manage-digital-assets.md) e/o [App desktop AEM](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=it).

## Apertura dell’Editor frammento {#opening-the-fragment-editor}

Per aprire la pagina per la modifica:

>[!CAUTION]
>
>Per modificare un frammento di contenuto sono necessarie [le autorizzazioni appropriate](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Se riscontri problemi, contatta l’amministratore del sistema.

1. Utilizza il **Risorse** per passare alla posizione del frammento di contenuto.
1. Apri il frammento per la modifica eseguendo una delle seguenti operazioni:

   * Tocca o fai clic sul collegamento del frammento o del frammento (a seconda della vista della console).
   * Selezionando il frammento, quindi **Modifica** dalla barra degli strumenti.

1. Viene aperto l’editor frammenti. Apporta le modifiche necessarie:

   ![Editor frammento](assets/cfm-managing-03.png)

1. Dopo aver apportato le modifiche, utilizza **Salva**, **Salva e chiudi** o **Chiudi** secondo la necessità.

   >[!NOTE]
   >
   >**Salva e chiudi** è disponibile tramite il menu a discesa **Salva**.

   >[!NOTE]
   >
   >Le azioni **Salva e chiudi** e **Chiudi** determinano l’uscita dall’editor. Per informazioni complete sul funzionamento delle varie opzioni dei frammenti di contenuto, consulta la sezione [Salva, chiudi e versioni](#save-close-and-versions).

## Modalità e azioni nell’Editor frammento di contenuto {#modes-actions-content-fragment-editor}

Nell’Editor frammento di contenuto sono disponibili varie modalità e azioni.

### Modalità nell’Editor frammento di contenuto {#modes-in-the-content-fragment-editor}

Naviga tra le varie modalità utilizzando le icone nel pannello laterale:

* Varianti: [Modifica del contenuto](#editing-the-content-of-your-fragment) e [Gestione delle varianti](#creating-and-managing-variations-within-your-fragment)

* [Annotazioni](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Contenuto associato](#associating-content-with-your-fragment)
* [Metadati](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Albero struttura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Anteprima](/help/assets/content-fragments/content-fragments-json-preview.md)

![Modalità nell’editor frammento di contenuto](assets/cfm-managing-04.png)

### Azioni barra degli strumenti nell’Editor frammento di contenuto {#toolbar-actions-in-the-content-fragment-editor}

Alcune funzioni nella barra degli strumenti superiore sono disponibili in diverse modalità:

![Azioni della barra degli strumenti disponibili in varie modalità](assets/cfm-managing-top-toolbar.png)

* Se in una pagina di contenuto è già presente un riferimento al frammento, viene visualizzato un messaggio. È possibile **chiudere** il messaggio.

* Il pannello laterale può essere nascosto o visualizzato utilizzando l’icona **Attiva/Disattiva pannello laterale**.

* Sotto il nome del frammento è possibile visualizzare il nome del [Modello per frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) utilizzato per creare il frammento corrente:

   * Il nome funge anche da collegamento per aprire l’editor modelli.

* Consulta lo stato del frammento; ad esempio, per informazioni su quando è stato creato, modificato o pubblicato. Lo stato viene inoltre codificato con un colore:

   * **Nuovo**: grigio
   * **Bozza**: blu
   * **Pubblicato**: verde
   * **Modificato**: arancione
   * **Disattivato**: rosso

* Un pulsante consente di: **Prova nuovo editor**, aprendo direttamente il *nuovo* [Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md) accessibile tramite [Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console).

  >[!WARNING]
  >
  >Il nuovo editor si aprirà nella stessa scheda. Si sconsiglia di aprire entrambi gli editor contemporaneamente.

* **Salva** fornisce accesso all’opzione **Salva e chiudi**.

* Il menu a discesa tre punti (**...**) fornisce accesso alle azioni aggiuntive:
   * **Aggiorna i riferimenti di pagina**
      * Questo aggiorna tutti i riferimenti di pagina.
   * **[Pubblicazione rapida](#publishing-and-referencing-a-fragment)**
   * **[Gestisci pubblicazione](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## Salva, chiudi e versioni {#save-close-and-versions}

>[!NOTE]
>
>Le versioni possono anche essere [create, confrontate e ripristinate dalla timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

L’editor dispone di diverse opzioni:

* **Salva** e **Salva e chiudi**

   * **Salva** salva le modifiche più recenti e rimane nell’editor.
   * **Salva e chiudi** salva le modifiche più recenti e chiude l’editor.

  >[!CAUTION]
  >
  >Per modificare un frammento di contenuto sono necessarie [le autorizzazioni appropriate](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Se riscontri problemi, contatta l’amministratore del sistema.

  >[!NOTE]
  >
  >È possibile rimanere nell’editor, apportando una serie di modifiche, prima di salvare.

  >[!CAUTION]
  >
  >Oltre al semplice salvataggio delle modifiche, le azioni aggiornano anche i riferimenti e garantiscono che il Dispatcher venga svuotato come richiesto. L’elaborazione di queste modifiche può richiedere del tempo. A causa di questo tempo, può esserci un impatto sulle prestazioni su un sistema di grandi dimensioni, complesso o con un carico elevato.
  >
  >Tieni presente questo processo quando utilizzi **Salva e chiudi** e quindi accedere di nuovo rapidamente all’editor frammenti per apportare e salvare altre modifiche.

* **Chiudi**

  Chiude l’editor senza salvare le modifiche più recenti, ovvero apportate dall’ultimo comando **Salva**.

Durante la modifica del frammento di contenuto, AEM crea automaticamente alcune versioni per garantire che il contenuto precedente possa essere ripristinato se si annullano le modifiche (utilizzando **Chiudi** senza salvare):

1. Quando un frammento di contenuto viene aperto per apportare modiche, AEM verifica l’esistenza del token basato su cookie che indica se esiste una *sessione di modifica*:

   1. Se il token viene trovato, il frammento viene considerato parte della sessione di modifica esistente.
   2. Se il token *non* è disponibile e l’utente inizia a modificare il contenuto, viene creata una versione e inviato al client un token per questa nuova sessione di modifica, che verrà salvato in un cookie.

2. Durante una sessione di modifica *attiva*, il contenuto in fase di modifica viene salvato automaticamente ogni 600 secondi (impostazione predefinita).

   >[!NOTE]
   >
   >L’intervallo di salvataggio automatico è configurabile utilizzando il comando `/conf`.
   >
   >Valore predefinito, vedi:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Se l’utente annulla la modifica, viene ripristinata la versione creata all’inizio della sessione di modifica e il token viene rimosso per terminare tale sessione.
4. Se l’utente **Salva** le modifiche, gli elementi/varianti aggiornate vengono rese permanenti e il token viene rimosso per terminare la sessione di modifica.

## Modifica del contenuto del frammento {#editing-the-content-of-your-fragment}

Dopo aver aperto il frammento, puoi utilizzare la scheda [Varianti](/help/assets/content-fragments/content-fragments-variations.md) per effettuare l’authoring dei contenuti.

## Creazione e gestione di varianti all’interno del frammento {#creating-and-managing-variations-within-your-fragment}

Dopo aver creato il contenuto primario, puoi creare e gestire le [Varianti](/help/assets/content-fragments/content-fragments-variations.md) di tale contenuto.

## Associazione di contenuto al frammento {#associating-content-with-your-fragment}

È inoltre possibile [associare il contenuto](/help/assets/content-fragments/content-fragments-assoc-content.md) a un frammento. In questo modo si fornisce una connessione in modo che le risorse (ad esempio le immagini) possano essere utilizzate (facoltativamente) con il frammento quando viene aggiunto a una pagina di contenuto.

## Visualizzazione e modifica dei metadati (proprietà) del frammento {#viewing-and-editing-the-metadata-properties-of-your-fragment}

Puoi visualizzare e modificare le proprietà di un frammento utilizzando la scheda [Metadati](/help/assets/content-fragments/content-fragments-metadata.md).

## Timeline per i frammenti di contenuto {#timeline-for-content-fragments}

Oltre alle opzioni standard, [Timeline](/help/assets/manage-digital-assets.md#timeline) fornisce sia informazioni che azioni specifiche relative ai frammenti di contenuto:

* Visualizza informazioni su versioni, commenti e annotazioni
* Azioni per le versioni

   * **[Ripristina questa versione](#reverting-to-a-version)** (seleziona un frammento esistente, quindi una versione specifica)

   * **[Confronta con corrente](#comparing-fragment-versions)** (seleziona un frammento esistente, quindi una versione specifica)

   * Aggiungi un’**Etichetta** e/o un **Commento** (seleziona un frammento esistente, quindi una versione specifica)

   * **Salva come versione** (seleziona un frammento esistente, quindi la freccia su nella parte inferiore della timeline)

* Azioni per le annotazioni

   * **Eliminare**

>[!NOTE]
>
I commenti sono:
>
* Funzionalità standard per tutte le risorse
* Effettuati nella timeline
* Correlati alla risorsa frammento
>
Le annotazioni (per i frammenti di contenuto) sono:
>
* Inserite nell’editor frammenti
* Specifiche per un segmento di testo selezionato all’interno del frammento
>

Esempio:

![Timeline](assets/cfm-managing-05.png)

## Confronto delle versioni dei frammenti {#comparing-fragment-versions}

L’azione **Confronta con corrente** è disponibile nella [Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) dopo aver selezionato una versione specifica.

Si aprirà:

* la versione **Corrente** (più recente) (a sinistra)

* la versione selezionata **v&lt;*x.y*>** (a destra)

Vengono visualizzati affiancati, dove:

* Eventuali differenze sono evidenziate

   * Testo eliminato: rosso
   * Testo inserito: verde
   * Testo sostituito: blu

* L’icona a schermo intero consente di aprire una versione da sola, quindi di tornare alla vista parallela
* È possibile **ritornare** alla versione specifica
* **Fine** riporta alla console

>[!NOTE]
>
Non è possibile modificare il contenuto del frammento nella modalità di confronto.

![Confronto delle varianti](assets/cfm-managing-06.png)

## Ripristino di una versione  {#reverting-to-a-version}

È possibile ripristinare una versione specifica del frammento:

* Direttamente dalla [timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

  Seleziona la versione richiesta, quindi l’azione **Ripristina questa versione**.

* Durante il [confronto di una versione con la versione corrente](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) è possibile **ritornare** alla versione selezionata.

## Pubblicazione e riferimento a un frammento {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
Se il frammento è basato su un modello, assicurati che il [modello sia stato pubblicato](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
>
Se pubblichi un frammento di contenuto per il quale il modello non è ancora stato pubblicato, ciò viene indicato in un elenco di selezione e il modello viene pubblicato con il frammento.

I frammenti di contenuto devono essere pubblicati per l’utilizzo nell’ambiente di pubblicazione. Questa operazione viene eseguita utilizzando la funzionalità standard di Assets:

* [Pubblicazione rapida](/help/assets/manage-publication.md#quick-publish)
* [Gestisci pubblicazione](/help/assets/manage-publication.md#manage-publication)

È possibile accedere a questa 

* Dopo la creazione; utilizzo [azioni disponibili nella console Assets](#actions-for-a-content-fragment-assets-console).
* Dall’[editor frammento di contenuto](#toolbar-actions-in-the-content-fragment-editor).

Inoltre, quando [pubblicare una pagina che utilizza il frammento](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing); il frammento è elencato nei riferimenti di pagina.

>[!CAUTION]
>
Dopo la pubblicazione e/o il riferimento a un frammento, AEM mostra un avviso quando un autore riapre il frammento per la modifica. L’avviso informa l’utente che le modifiche al frammento avranno effetto anche sulle pagine a cui si fa riferimento.

## Eliminazione di un frammento {#deleting-a-fragment}

Per eliminare un frammento:

1. Nella console **Risorse** passa alla posizione del frammento di contenuto.
2. Seleziona il frammento.

   >[!NOTE]
   >
   L’azione **Elimina** non è disponibile come azione rapida.

3. Seleziona **Elimina** dalla barra degli strumenti.
4. Conferma l’azione **Elimina**.

   >[!CAUTION]
   >
   Se in una pagina è già presente un riferimento al frammento, verrà visualizzato un messaggio di avviso e sarà necessario confermare che si desidera procedere con **Forza eliminazione**. Il frammento, insieme al relativo componente Frammento di contenuto, viene eliminato da tutte le pagine di contenuto.
