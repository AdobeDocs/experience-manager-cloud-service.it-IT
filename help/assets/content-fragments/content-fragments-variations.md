---
title: Varianti - Authoring dei contenuti di frammenti
description: Le varianti consentono di creare il contenuto per il frammento e quindi di crearne le varianti in base allo scopo (se necessario).
translation-type: tm+mt
source-git-commit: 0a60687eacf054675205d9a9466473e1f4996db1
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 19%

---


# Varianti - Authoring dei contenuti di frammenti{#variations-authoring-fragment-content}

<!--
>[!CAUTION]
>
>Certain features for Content Fragments will be released in early 2021.
>
>The related documentation is already available for preview purposes.
>
>Please see the [Release Notes](/help/release-notes/release-notes-cloud/release-notes-current.md) for further details.
-->

[Le ](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) varianti sono una caratteristica importante dei frammenti di contenuto, in quanto consentono di creare e modificare copie del contenuto principale da utilizzare su canali e/o scenari specifici.

Dalla scheda **Variazioni** è possibile:

* [Immettere il ](#authoring-your-content) contenuto del frammento,
* [Creare e gestire ](#managing-variations) le varianti del  **** contenuto principale,
* Vedere il nome del [modello di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) utilizzato per creare il frammento; nella barra degli strumenti superiore, sotto il nome del frammento.

Eseguire una serie di altre azioni in base al tipo di dati in corso di modifica; ad esempio:

* [Inserire risorse visive nel frammento](#inserting-assets-into-your-fragment)  (immagini)

* Selezionare tra [Rich Text](#rich-text), [Plain Text](#plain-text) e [Markdown](#markdown) per la modifica

* [Carica contenuto](#uploading-content)

* [Visualizzare le statistiche](#viewing-key-statistics)  chiave (informazioni sul testo su più righe)

* [Testo riepilogo](#summarizing-text)

* [Sincronizzare le varianti con il contenuto principale](#synchronizing-with-master)

>[!CAUTION]
>
>Dopo aver pubblicato e/o fatto riferimento a un frammento, AEM viene visualizzato un avviso quando un autore riapre il frammento per la modifica. In questo modo viene segnalato che le modifiche apportate al frammento avranno effetto anche sulle pagine di riferimento.

## Creazione di contenuti {#authoring-your-content}

Quando si apre il frammento di contenuto per la modifica, per impostazione predefinita viene aperta la scheda **Variazioni**. Qui potete creare il contenuto, per Master o qualsiasi altra variante disponibile. Il frammento strutturato contiene vari campi, di vari tipi di dati, definiti nel modello di contenuto.

Operazioni disponibili:

* apportare modifiche direttamente nella scheda **Variazioni**

   * ciascun tipo di dati fornisce diverse opzioni di modifica

* per i campi **Testo su più righe** è inoltre possibile aprire l&#39; [editor a schermo intero](#full-screen-editor) per:

   * selezionare [Format](#formats)
   * ulteriori opzioni di modifica (per il formato [Rich Text](#rich-text))
   * accedere a un intervallo di [azioni](#actions)

<!--
For example:

![full screen editor](assets/cfm-variations-02.png)
-->

### Editor a schermo intero {#full-screen-editor}

Quando si modifica un campo di testo a più righe, è possibile aprire l’editor a schermo intero; toccate o fate clic all&#39;interno del testo effettivo, quindi selezionate la seguente icona di azione:

![icona dell&#39;editor a schermo intero](assets/cfm-variations-03.png)

<!--
This will open the full screen text editor:

![full screen editor icon](assets/cfm-variations-fullscreentexteditor.png)
-->

L&#39;editor di testo a schermo intero fornisce:

* Accesso a varie [azioni](#actions)
* A seconda del [formato](#formats), opzioni di formattazione aggiuntive ([Rich Text](#rich-text))

### Azioni {#actions}

Sono inoltre disponibili le azioni seguenti (per tutti i formati [](#formats)) quando è aperto l&#39;editor a schermo intero (cioè testo su più righe):

* Selezionare il [formato](#formats) ([Rich Text](#rich-text), [Testo normale,](#plain-text) [Markdown](#markdown))

* [Caricare il contenuto](#uploading-content)

* [Mostra statistiche testo](#viewing-key-statistics)

* [Sincronizza con principale](#synchronizing-with-master)  (durante la modifica di una variante)

* [Testo riepilogo](#summarizing-text)

### Formati {#formats}

Le opzioni per la modifica del testo su più righe dipendono dal formato selezionato:

* [Formato RTF](#rich-text)
* [Testo normale](#plain-text)
* [Markdown](#markdown)

Il formato può essere selezionato quando si utilizza l&#39;editor a schermo intero.

### Formato RTF {#rich-text}

La modifica RTF consente di formattare:

* Grassetto
* Corsivo
* Sottolineato
* Allineamento: sinistra, centro, destra
* Elenco puntato
* Elenco numerato
* Rientro: aumento, diminuzione
* Creare/interrompere collegamenti ipertestuali
* Incolla testo/da Word
* Inserire una tabella
* Stile paragrafo: Paragrafo, Intestazione 1/2/3
* [Inserisci risorsa](#inserting-assets-into-your-fragment)
* Aprite l’editor a schermo intero, in cui sono disponibili le seguenti opzioni di formattazione:
   * Ricerca
   * Trova/Sostituisci
   * Controllo ortografia
   * [Annotazioni](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)

<!--
* [Insert Content Fragment](#inserting-content-fragment-into-your-fragment)
-->

Le [azioni](#actions) sono accessibili anche dall&#39;editor a schermo intero.

### Testo normale {#plain-text}

Testo semplice consente di inserire rapidamente il contenuto senza informazioni di formattazione o di marketing. È inoltre possibile aprire l&#39;editor a schermo intero per ulteriori [azioni](#actions).

>[!CAUTION]
>
>Se selezioni **Testo normale**, potresti perdere la formattazione, le marcature e/o le risorse inserite in **Rich Text** o **Markdown**.

### Markdown {#markdown}

>[!NOTE]
>
>Per informazioni complete, consulta la documentazione di [Markdown](/help/assets/content-fragments/content-fragments-markdown.md).

Questo consente di formattare il testo con la funzione di marketing. È possibile definire:

* Intestazioni
* Paragrafi e interruzioni di riga
* Collegamenti
* Immagini
* Virgolette a blocchi
* Elenchi
* Enfasi
* Blocchi di codice
* Estratti barra rovesciata

È inoltre possibile aprire l&#39;editor a schermo intero per ulteriori [azioni](#actions).

>[!CAUTION]
>
>Se passi da **Rich Text** a **Markdown**, potresti riscontrare effetti imprevisti con Block Quotes (Citazioni) e Code Blocks (Blocchi di codice), in quanto questi due formati possono presentare differenze nelle modalità di gestione.

<!--
### Fragment References {#fragment-references}

If the Content Fragment Model contains Fragment References, your fragment authors may have additional options:

* [Edit Content Fragment](#fragment-references-edit-content-fragment)
* [New Content Fragment](#fragment-references-new-content-fragment)

![Fragment References](assets/cfm-variations-12.png)

#### Edit Content Fragment {#fragment-references-edit-content-fragment}

The option **Edit Content Fragment** will open
a new browser tab, with the content fragment open in the content fragment editor.

#### New Content Fragment {#fragment-references-new-content-fragment}

The option **New Content Fragment** will allow you to create a completely new fragment. To achieve this a variation of the create content fragment wizard will open in the editor. 

You will then be able to create a new fragment by:

1. Navigating to, and selecting the required folder.
1. Selecting **Next**.
1. Specifying properties; for example **Title**.
1. Selecting **Create**.
1. Finally:
   1. **Done** will return (to the original fragment) and reference the new fragment.
   1. **Open** will reference the new fragment as well as opening the new fragment, for editing, in a new browser tab.
-->

### Visualizzazione delle statistiche chiave {#viewing-key-statistics}

Quando l’editor a schermo intero è aperto, l’azione **Statistiche testo** visualizzerà una serie di informazioni sul testo.

Esempio:

![statistica](assets/cfm-variations-04.png)

### Caricamento di contenuto {#uploading-content}

Per semplificare la creazione di frammenti di contenuto, è possibile caricare il testo, prepararlo in un editor esterno e aggiungerlo direttamente al frammento.

### Riepilogo testo {#summarizing-text}

Il testo di riepilogo è progettato per consentire agli utenti di ridurre la lunghezza del testo a un numero predefinito di parole, mantenendo al contempo i punti chiave e il significato complessivo.

>[!NOTE]
>
>A livello più tecnico, il sistema mantiene le frasi che considera come fornire il *miglior rapporto di densità delle informazioni e di unicità* in base a specifici algoritmi.

>[!CAUTION]
>
>Il frammento di contenuto deve avere come antenato una cartella di lingua valida (codice ISO); viene utilizzato per determinare il modello di lingua da utilizzare.
>
>Ad esempio, `en/` come nel percorso seguente:
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
L&#39;inglese è disponibile out-of-the-box.
Altre lingue sono disponibili come pacchetti di modelli di lingua da Package Share:
* [Francese (fr)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-fr)
* [Tedesco (de)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-de)
* [Italiano (it)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-it)
* [Spagnolo (es)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-es)



1. Selezionare **Master** o la variante richiesta.
1. Aprite l’editor a schermo intero.

1. Selezionare **Riepilogo testo** dalla barra degli strumenti.

   ![riepilogo](assets/cfm-variations-05.png)

1. Specificare il numero di parole di destinazione e selezionare **Start**:
1. Il testo originale viene visualizzato uno accanto all’altro con il riepilogo proposto:

   * Tutte le frasi da eliminare sono evidenziate in rosso, con lo sciopero.
   * Fate clic su una frase evidenziata per mantenerla nel contenuto riepilogato.
   * Fate clic su una frase non evidenziata per eliminarla.

1. Selezionare **Riepilogo** per confermare le modifiche.

<!--
1. The original text is displayed side-by-side with the proposed summarization:

    * Any sentences to be eliminated are highlighted in red, with strike-through.
    * Click on any highlighted sentence to keep it in the summarized content.
    * Click on any non-highlighted sentence to have it eliminated.

   ![summarization comparison](assets/cfm-variations-06.png)
-->

### Aggiunta di annotazioni a un frammento di contenuto {#annotating-a-content-fragment}

Per aggiungere annotazioni a un frammento:

1. Selezionare **Master** o la variante richiesta.
1. Aprite l’editor a schermo intero.
1. L&#39;icona **Annota** è disponibile nella barra degli strumenti superiore. Se necessario, potete selezionare del testo.

1. Viene aperta una finestra di dialogo. Consente di inserire l’annotazione.

   ![annotare](assets/cfm-variations-07a.png)

1. Selezionare **Applica** nella finestra di dialogo.

   ![annotare](assets/cfm-variations-annotations-apply-icon.png)

   Se l&#39;annotazione è stata applicata al testo selezionato, il testo rimarrà evidenziato.

   ![annotare](assets/cfm-variations-07b.png)

1. Se chiudete l’editor a schermo intero, le annotazioni restano evidenziate. Se questa opzione è selezionata, verrà visualizzata una finestra di dialogo che consente di modificare ulteriormente l’annotazione.

1. Seleziona **Salva**.

<!--
1. The **Annotate** icon is available in the top toolbar. You can seelect some text if required.

   ![annotate](assets/cfm-variations-07.png)
-->

<!--
1. Close the full-screen editor, annotations are still highlighted. If selected, a dialog will open so that you can edit the annotation further.

   ![annotate](assets/cfm-variations-07c.png)

-->

### Visualizzazione, modifica, eliminazione di annotazioni {#viewing-editing-deleting-annotations}

Annotazioni:

* Sono indicate dall’evidenziazione sul testo, sia a schermo intero che in modalità normale dell’editor. I dettagli completi di un’annotazione possono essere visualizzati, modificati e/o eliminati facendo clic sul testo evidenziato, che riaprirà la finestra di dialogo.

   >[!NOTE]
   Se a un elemento di testo sono state applicate più annotazioni, viene fornito un selettore a discesa.

* Quando eliminate l’intero testo a cui è stata applicata l’annotazione, viene eliminata anche quest’ultima.

* È possibile elencare ed eliminare i frammenti selezionando la scheda **Annotazioni** nell&#39;editor frammento.

* Può essere visualizzato ed eliminato in [Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) per il frammento selezionato.

<!--
* Can be listed, and deleted, by selecting the **Annotations** tab in the fragment editor.

  ![annotations](assets/cfm-variations-08.png)
-->

### Inserimento di risorse nel frammento {#inserting-assets-into-your-fragment}

Per semplificare la creazione di frammenti di contenuto, è possibile aggiungere [Risorse](/help/assets/manage-digital-assets.md) (immagini) direttamente al frammento.

Saranno aggiunti alla sequenza di paragrafi del frammento senza formattazione; la formattazione può essere eseguita quando il frammento [viene utilizzato/a cui viene fatto riferimento in una pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md).

>[!CAUTION]
Queste risorse non possono essere spostate o eliminate in una pagina che contiene il riferimento, bensì nell’editor frammento.
Tuttavia, la formattazione della risorsa (ad es. dimensione) deve essere eseguita nell&#39; [editor di pagina](/help/sites-cloud/authoring/fundamentals/content-fragments.md). La rappresentazione della risorsa nell’editor frammento è destinata esclusivamente alla creazione del flusso di contenuto.

>[!NOTE]
Esistono vari metodi per aggiungere [immagini](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al frammento e/o alla pagina.

1. Posiziona il cursore nel punto in cui vuoi aggiungere l’immagine.
1. Per aprire la finestra di dialogo di ricerca, utilizza l’icona **Inserisci risorsa**.

   ![inserire l&#39;icona della risorsa](assets/cfm-variations-09.png)

1. Nella finestra di dialogo potete:

   * passa alla risorsa richiesta in DAM
   * cercare la risorsa in DAM

   Una volta individuata la risorsa desiderata, selezionatela facendo clic sulla miniatura.

1. Utilizza **Seleziona** per aggiungere la risorsa al sistema paragrafo del frammento di contenuto nella posizione corrente.

   >[!CAUTION]
   Se, dopo aver aggiunto una risorsa, ne cambi il formato in:
   * **Testo normale**: la risorsa verrà persa completamente dal frammento.
   * **Markdown**: la risorsa non sarà visibile, ma lo tornerà a essere quando tornerai a **Rich Text**.


<!--
### Inserting a Content Fragment into your Fragment {#inserting-content-fragment-into-your-fragment}

To ease the process of authoring content fragments you can also add another Content Fragment to your fragment.

They will be added as a reference, in your current location in your fragment.
-->

<!--
>[!CAUTION]
>
>These assets cannot be moved or deleted on a referencing page, this must be done in the fragment editor.
>
>However, formatting of the asset (e.g. size) must be done in the [page editor](/help/sites-cloud/authoring/fundamentals/content-fragments.md). The representation of the asset in the fragment editor is purely for authoring the content flow.

>[!NOTE]
>
>There are various methods of adding [images](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) to the fragment and/or page.
-->

<!--
1. Position the cursor at the position you want to add the fragment.
1. Use the **Insert Content Fragment** icon to open the search dialog.

   ![insert Content Fragment icon](assets/cfm-variations-13.png)

1. In the dialog you can either:

    * navigate to the required fragment in the Assets folder
    * search for the fragment

   Once located, select the required fragment by clicking on the thumbnail.

1. Use **Select** to add a reference to the selected Content Fragment to your current content fragment (at the current location).

   >[!CAUTION]
   >
   >If, after adding an reference to another fragment, you change format to:
   >* **Plain Text**: the reference will be completely lost from the fragment.
   >* **Markdown**: the reference will remain.
-->

## Gestione delle varianti {#managing-variations}

### Creazione di una variante {#creating-a-variation}

Le varianti consentono di utilizzare il contenuto **Master** e di modificarlo in base allo scopo (se necessario).

Per creare una nuova variante:

1. Aprire il frammento e assicurarsi che il pannello laterale sia visibile.
1. Selezionate **Variazioni** dalla barra delle icone nel pannello laterale.
1. Selezionare **Crea variante**.
1. Viene aperta una finestra di dialogo in cui vengono specificati **Titolo** e **Descrizione** per la nuova variante.
1. Seleziona **Aggiungi**, il frammento **Master** verrà copiato nella nuova variante, che è ora aperta per la [modifica](#editing-a-variation).

   >[!NOTE]
   Quando si crea una nuova variante, viene sempre copiata la variante **Master**, non la variante attualmente aperta.

### Modifica di una variante {#editing-a-variation}

Puoi apportare modifiche al contenuto della variante dopo:

* [Creazione della variante](#creating-a-variation).
* Aprire un frammento esistente, quindi selezionare la variante desiderata dal pannello laterale.

![modifica di una variante](assets/cfm-variations-10.png)

### Ridenominazione di una variante {#renaming-a-variation}

Per rinominare una variante esistente:

1. Aprire il frammento e selezionare **Variazioni** dal pannello laterale.
1. Selezionate la variante desiderata.
1. Selezionare **Rinomina** dal menu a discesa **Azioni**.

1. Immetti il nuovo **Titolo** e/o **Descrizione** nella finestra di dialogo in questione.

1. Confermare l&#39;azione **Rinomina**.

>[!NOTE]
Questo incide solo sulla variante **Title**.

### Eliminazione di una variante {#deleting-a-variation}

Per eliminare una variante esistente:

1. Aprire il frammento e selezionare **Variazioni** dal pannello laterale.
1. Selezionate la variante desiderata.
1. Selezionare **Elimina** dal menu a discesa **Azioni**.

1. Confermate l&#39;azione **Elimina** nella finestra di dialogo.

>[!NOTE]
Non è possibile eliminare **Master**.

### Sincronizzazione con Master {#synchronizing-with-master}

**** Master è parte integrante di un frammento di contenuto e, per definizione, contiene la copia principale del contenuto, mentre le varianti contengono le singole versioni aggiornate e personalizzate di tale contenuto. Quando Master viene aggiornato, è possibile che tali modifiche siano pertinenti anche alle variazioni e, pertanto, debbano essere propagate ad esse.

Quando si modifica una variante, è possibile accedere all&#39;azione per sincronizzare l&#39;elemento corrente della variante con Master. Questo consente di copiare automaticamente le modifiche apportate alla variante desiderata in Master.

>[!CAUTION]
La sincronizzazione è disponibile solo per copiare le modifiche *da **Master**alla variante*.
Viene sincronizzato solo l’elemento corrente della variante.
La sincronizzazione funziona solo sul tipo di dati **Testo su più righe**.
Il trasferimento delle modifiche *da una variante a **Master*** non è disponibile come opzione.

1. Aprire il frammento di contenuto nell&#39;editor frammento. Assicurarsi che il **Master** sia stato modificato.
1. Selezionate una variante specifica, quindi l’azione di sincronizzazione appropriata da:

   * il selettore a discesa **Actions** - **Sincronizza elemento corrente con master**

   * la barra degli strumenti dell&#39;editor a schermo intero - **Sincronizza con master**

      ![sincronizzazione con master](assets/cfm-variations-11b.png)

1. Master e la variante verrà mostrata affiancata:

   * verde indica il contenuto aggiunto (alla variante)
   * il rosso indica che il contenuto è stato rimosso (dalla variante)
   * blu indica il testo sostituito

   ![sincronizzazione con master](assets/cfm-variations-11c.png)

1. Selezionare **Sincronizza**, la variante verrà aggiornata e visualizzata.

<!--
1. Select a specific variation, then the appropriate synchronization action from either:

   * the **Actions** drop down selector - **Sync current element with master**

      ![synchronizing with master](assets/cfm-variations-11a.png)

   * the toolbar of the full-screen editor - **Sync with master**

      ![synchronizing with master](assets/cfm-variations-11b.png)

1. Master and the variation will be shown side-by-side:

   * green indicates content added (to the variation)
   * red indicates content removed (from the variation)
   * blue indicates replaced text

   ![synchronizing with master](assets/cfm-variations-11c.png)

1. Select **Synchronize**, the variation will updated and shown.

-->