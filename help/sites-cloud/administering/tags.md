---
title: Amministrazione dei tag
description: Scopri come amministrare i tag in AEM per organizzare i contenuti.
exl-id: 42480699-b7a7-4678-a763-569a9b7573e2
solution: Experience Manager Sites
feature: Workflow
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2200'
ht-degree: 1%

---

# Amministrazione dei tag {#administering-tags}

I tag sono un metodo intuitivo per classificare il contenuto. Possono essere considerate come parole chiave o etichette (metadati) che consentono di trovare più rapidamente il contenuto.

In Adobe Experience Manager (AEM), un tag può essere una proprietà di:

* Un nodo di contenuto per una pagina
   * Per ulteriori informazioni, vedere il documento [Utilizzo dei tag](/help/sites-cloud/authoring/sites-console/tags.md).
* Un nodo di metadati per una risorsa
   * Per ulteriori informazioni, vedere il documento [Gestione dei metadati per Digital Assets](/help/assets/manage-metadata.md).

>[!TIP]
>
>È consigliabile ridurre al minimo il numero di tag relativi alle stesse idee. Ad esempio, se gestisci contenuti per un negozio di articoli all&#39;aperto, probabilmente non avrai bisogno di un tag per **scarpe** e **scarpe**.

## Funzioni tag {#tag-features}

I tag offrono funzioni affidabili per organizzare e gestire i contenuti.

* I tag possono essere raggruppati in vari spazi dei nomi.
   * Gli spazi dei nomi possono essere considerati gerarchie che consentono la creazione di tassonomie.
   * Queste tassonomie sono globali in tutta l&#39;AEM.
* I tag possono essere applicati dagli autori e utilizzati dai visitatori del sito.
* Indipendentemente dall’autore, tutte le forme di tag sono disponibili per la selezione, sia durante l’assegnazione a una pagina che durante la ricerca.
* I tag vengono utilizzati dal [componente Elenco](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html) per generare elenchi dinamici in base ai tag selezionati.

## Requisiti dei tag {#requirements}

Sono disponibili alcuni dettagli tecnici da tenere a mente durante la creazione e la gestione dei tag.

* I tag devono essere univoci all’interno di uno spazio dei nomi specifico.
* Il nome di un tag non può includere delimitatori di tag:
   * Due punti (`:`) - Delimita il tag dello spazio dei nomi
   * Barra (`/`) - Delimita i tag secondari
* Se il titolo di un tag include delimitatori di tag, questi verranno eliminati nell’interfaccia utente.
* I tag possono essere creati e la relativa tassonomia può essere modificata dai membri del gruppo `tag-administrators` e dai membri con diritti di modifica per `/content/cq:tags`.
   * Un tag che contiene tag figlio viene definito tag contenitore.
   * Un tag che non è un tag contenitore viene definito tag foglia.
   * Uno spazio dei nomi dei tag può essere un tag foglia o un tag contenitore.

Per ulteriori dettagli tecnici sul funzionamento dei tag, consulta [Framework di assegnazione tag AEM](/help/implementing/developing/introduction/tagging-framework.md).

## Console per assegnazione tag {#tagging-console}

La console dei tag consente di creare e gestire i tag e le relative tassonomie. Puoi utilizzare la console dei tag per gestire i tag:

* Raggruppandoli in spazi dei nomi.
* Analisi dell&#39;utilizzo dei tag esistenti prima di crearne di nuovi.
* Riorganizzazione dei tag senza disconnettere il tag dal contenuto a cui si fa attualmente riferimento.

Per accedere alla console dei tag:

1. Accedi a un ambiente di authoring con privilegi di amministratore.
1. Nel menu di navigazione globale selezionare **`Tools`** > **`General`** >
   **`Tagging`**.

![Console di assegnazione tag in AEM](/help/sites-cloud/administering/assets/tagging-console.png)

## Creazione di nuovi tag {#creating-new-tags}

Esistono diversi passaggi per creare e utilizzare i tag per organizzare i contenuti.

1. [Crea uno spazio dei nomi per i tag](#creating-namespaces) (o scegline uno esistente da riutilizzare).
1. [Crea un nuovo tag](#creating-tags).
1. [Publish il tag](#publishing-tags).

### Creazione di spazi dei nomi {#creating-namespaces}

Per organizzare altri tag viene utilizzato uno spazio dei nomi. Può essere considerato come il tag di livello più basso e viene in genere utilizzato per raggruppare altri tag.

1. Per creare uno spazio dei nomi, apri la [console di assegnazione tag](#tagging-console) e seleziona il pulsante **Crea** nella barra degli strumenti, quindi **Crea spazio dei nomi**.

   ![Finestra di dialogo Aggiungi spazio dei nomi](/help/sites-cloud/administering/assets/add-namespace.png)

1. Fornisci le informazioni necessarie.

   * **Titolo** - Titolo per lo spazio dei nomi visualizzato nell&#39;interfaccia utente (facoltativo)
   * **Nome** - Se non viene specificato un nome, viene creato un nome di nodo valido dal **Titolo**. Per ulteriori informazioni, consulta il documento [Framework di assegnazione tag AEM](/help/implementing/developing/introduction/tagging-framework.md#tagid).
   * **Descrizione** - Descrizione dello spazio dei nomi (facoltativo)

1. Una volta immesse le informazioni richieste, seleziona **Crea**.

Viene creato lo spazio dei nomi. Nella console dei tag, gli spazi dei nomi si trovano al livello più basso (nella colonna all’estrema sinistra della console) e sono rappresentati da icone di cartelle, che riflettono la loro natura di &quot;contenitore&quot; o raggruppamento di altri tag.

Ora puoi [creare nuovi tag](#creating-tags) in questo spazio dei nomi o [gestire i tag esistenti](#managing-tags).

Uno spazio dei nomi non deve necessariamente contenere tag secondari. Poiché uno spazio dei nomi è di per sé un tag, può essere utilizzato per organizzare il contenuto come qualsiasi altro tag. Tuttavia, per continuare a creare una tassonomia dei tag strutturata, puoi [creare tag secondari](#creating-tags) all&#39;interno di tale spazio dei nomi in base ai requisiti del progetto.

### Creazione di tag {#creating-tags}

I tag vengono generalmente aggiunti agli spazi dei nomi.

1. Per creare un tag, apri la [console tag](#tagging-console).

1. Seleziona lo spazio dei nomi in cui desideri creare il tag. In alternativa, seleziona un altro tag per creare un tag secondario al di sotto di esso.

1. Selezionare il pulsante **Crea** sulla barra degli strumenti e quindi **Crea tag**.

1. Viene visualizzata la finestra di dialogo **Crea tag**. Fornisci le informazioni richieste per il nuovo tag.

   * **Titolo** - Titolo visualizzato per il tag (obbligatorio)
   * **Nome** - Nome del tag (obbligatorio). Se non viene specificato, verrà creato un nome di nodo valido dal **Titolo**. Vedi [TagID](/help/implementing/developing/introduction/tagging-framework.md#tagid).
   * **Descrizione** - Descrizione del tag
   * **Percorso tag**: lo spazio dei nomi (o tag) selezionato nella console di assegnazione tag viene impostato automaticamente. Per aggiornare manualmente questo valore, tocca o fai clic sull’icona del selettore del percorso.

   ![Finestra di dialogo Crea tag](assets/create-tag.png)

1. Seleziona **Invia**.

Il tag viene creato e la console viene aggiornata per mostrare il nuovo tag.

I tag consentono di creare in modo flessibile la propria tassonomia in base alle esigenze organizzative.

* Puoi creare tag secondari di tag esistenti selezionando il tag principale nella console prima di creare il nuovo tag.
* Se crei un tag senza selezionare uno spazio dei nomi o un altro tag, viene effettivamente creato uno spazio dei nomi.

### Pubblicazione dei tag {#publishing-tags}

Come per la creazione di qualsiasi altro contenuto in AEM, dopo aver creato un tag (o namespace), questo esiste solo nell’ambiente di authoring. Affinché i tag siano disponibili per gli utenti, devi pubblicarli.

1. Per pubblicare un tag, apri la [console tag](#tagging-console).

1. Selezionare il tag o i tag da pubblicare e nella barra degli strumenti selezionare **Publish**.

   ![Selezione di tag nella console](assets/select-tags.png)

1. La finestra di dialogo **Tag Publish** richiede una conferma per la pubblicazione dei tag selezionati. Seleziona **Pubblica**.

   ![Il modale di conferma del tag Publish](assets/publish-tag.png)

1. L&#39;azione di pubblicazione è confermata con una finestra di dialogo **Operazione riuscita**.

   ![Finestra di dialogo per il completamento del tag Publish](assets/publish-tag-success.png)

I tag selezionati sono in coda per la pubblicazione. Analogamente al contenuto della pagina, vengono pubblicati solo i tag selezionati, indipendentemente dal fatto che contengano o meno tag secondari.

Per pubblicare un&#39;intera tassonomia (uno spazio dei nomi e tag secondari), la procedura consigliata consiste nel creare un [pacchetto](/help/implementing/developing/tools/package-manager.md) dello spazio dei nomi (vedi [Nodo principale tassonomia](/help/implementing/developing/introduction/tagging-framework.md#taxonomy-root-node)).

<!--
Be sure to [apply permissions](#setting-tag-permissions) to the namespace before creating the package.
-->

## Gestione dei tag {#managing-tags}

Puoi eseguire diverse azioni sui tag e sugli spazi dei nomi esistenti per gestirli e organizzarli. È sufficiente selezionare un tag o uno spazio dei nomi nella [console di assegnazione tag](#tagging-console) per visualizzare nella barra degli strumenti le azioni disponibili.

* [Visualizza proprietà](#viewing-tag-properties)
* [Modifica](#editing-tags)
* [Annulla pubblicazione](#unpublishing-tags)
* [Riferimenti](#viewing-tag-references)
* [Spostare](#moving-tags)
* [Unisci](#merging-tags)
* [Elimina](#deleting-tags)

Quando lo spazio sulla barra degli strumenti è sufficiente, dietro l’icona con i puntini di sospensione sono disponibili opzioni aggiuntive.

### Visualizzazione delle proprietà dei tag {#viewing-tag-properties}

Quando nella console dei tag è selezionato un singolo tag, uno spazio dei nomi o un altro tag, i dettagli di base del tag selezionato, ad esempio l’ora dell’ultima modifica e dell’ultima pubblicazione, vengono visualizzati nella colonna a sinistra della colonna del tag.

![Colonna dettagli tag](assets/tag-details-column.png)

Per visualizzare ulteriori dettagli sul tag, tra cui chi l&#39;ha pubblicato per ultimo e quando, passa dalla console alla visualizzazione **Proprietà**.

1. Per visualizzare le proprietà di un tag, apri la [console tag](#tagging-console).

1. Seleziona il tag di cui desideri visualizzare le proprietà e nella barra a sinistra seleziona **Proprietà**.

   ![Selezione della visualizzazione delle proprietà](assets/view-tag-properties.png)

1. Le proprietà dettagliate del tag selezionato vengono visualizzate nella barra a sinistra.

   ![Visualizzazione delle proprietà dei tag](assets/tag-properties.png)

Per ulteriori dettagli sulla selezione delle modalità di visualizzazione e della barra, vedere [Operazioni di base](/help/sites-cloud/authoring/basic-handling.md#rail-selector).

### Modifica dei tag {#editing-tags}

I tag e gli spazi dei nomi possono essere modificati dopo la creazione.

1. Per modificare un tag, apri la [console tag](#tagging-console).

1. Seleziona il tag da modificare e nella barra degli strumenti seleziona **Modifica**.

1. Apporta le modifiche desiderate. È possibile modificare:

   * **Titolo**
   * **Descrizione**
   * [**Localizzazione**](#managing-tags-in-different-languages)

1. Dopo aver apportato le modifiche, selezionare **Invia**.

Per informazioni dettagliate sull&#39;aggiunta di traduzioni per lingua, vedere la sezione relativa a [Gestione dei tag in lingue diverse](#managing-tags-in-different-languages).

Se le modifiche apportate riguardano un tag già pubblicato, [ripubblicarlo](#publishing-tags).

### Annullamento della pubblicazione dei tag {#unpublishing-tags}

Per disattivare i tag nell’istanza di authoring e rimuoverli dall’istanza di pubblicazione, puoi annullarne la pubblicazione.

1. Per annullare la pubblicazione di un tag, apri la [console tag](#tagging-console).

1. Seleziona il tag o i tag da annullare la pubblicazione e nella barra degli strumenti seleziona **Annulla pubblicazione**.

   ![Selezione di tag nella console](assets/select-tags.png)

1. La finestra di dialogo **Annulla pubblicazione tag** richiede una conferma per la pubblicazione dei tag selezionati. Seleziona **Pubblica**.

   ![Il modale di conferma del tag Publish](assets/unpublish-tag.png)

1. L&#39;azione di annullamento della pubblicazione è confermata con una finestra di dialogo **Operazione riuscita**.

   ![Finestra di dialogo per il completamento del tag Publish](assets/unpublish-tag-success.png)

I tag selezionati sono in coda per l&#39;annullamento della pubblicazione. Se il tag selezionato è un tag contenitore, tutti i relativi tag figlio verranno disattivati nell’ambiente di authoring e rimossi dall’ambiente di pubblicazione.

### Visualizzazione dei riferimenti dei tag {#viewing-tag-references}

Può essere utile vedere a quale contenuto viene applicato un particolare tag. Puoi farlo utilizzando la visualizzazione **Riferimenti** nella console di assegnazione tag.

1. Per visualizzare i riferimenti di un tag, apri la [console tag](#tagging-console).

1. Seleziona il tag di cui desideri visualizzare i riferimenti e nella barra a sinistra seleziona **Riferimenti**.

   ![Selezione della visualizzazione delle proprietà](assets/view-tag-references.png)

1. Il numero totale di riferimenti per il tag selezionato viene visualizzato nella barra a sinistra.

   ![Visualizzazione dei riferimenti ai tag](assets/tag-references.png)

1. Seleziona il numero di riferimenti tag per visualizzare l’elenco dettagliato dei contenuti assegnati al tag.

   ![Visualizzazione dei dettagli dei riferimenti del tag](assets/tag-references-detail.png)

Passa il mouse o seleziona un contenuto con riferimento nell’elenco per visualizzare il percorso completo del contenuto.

Per ulteriori dettagli sulla selezione delle modalità di visualizzazione e della barra, vedere [Operazioni di base](/help/sites-cloud/authoring/basic-handling.md#rail-selector).

### Spostamento dei tag {#moving-tags}

Può essere necessario riorganizzare la tassonomia dei tag spostando un tag in una nuova posizione o rinominandolo.

>[!TIP]
>
>È consigliabile che solo gli amministratori possano spostare e rinominare i tag.

1. Per spostare o rinominare un tag, aprire la [console di assegnazione tag](#tagging-console).

1. Selezionare il tag da spostare o rinominare e selezionare **Sposta** nella barra degli strumenti.

1. Nella finestra di dialogo **Sposta tag**, specifica la proprietà da modificare.

   * **Rinomina in** - Nuovo nome da assegnare al tag
      * Questo campo viene precompilato con il nome corrente del tag.
      * Lascia invariato se desideri solo spostare il tag e non rinominarlo.
   * **Sposta in** - Posizione in cui spostare il tag
      * Questo campo viene precompilato con la posizione corrente del tag.
      * Lascia invariato se desideri rinominare solo il tag e non spostarlo.

   ![Sposta tag](assets/move-tag.png)

1. Seleziona **Invia**.

Il tag viene rinominato e/o spostato nella nuova posizione. Quando il tag selezionato è un tag contenitore, lo spostamento del tag comporta lo spostamento anche di tutti i tag figlio.

### Unione di tag {#merging-tags}

Se la tassonomia dei tag include duplicati o tag simili, può essere utile unirli. Quando il tag `A` viene unito al tag `B`, tutte le pagine contrassegnate con il tag `A` vengono contrassegnate con il tag `B` e il tag `A` non è più disponibile per gli autori.

1. Per unire due tag, apri la [console tag](#tagging-console).

1. Selezionare il tag da unire in un altro tag, quindi selezionare **Unisci** nella barra degli strumenti.

1. Nella finestra di dialogo **Unisci tag**, seleziona l&#39;icona **Sfoglia** del campo **Unisci in** per specificare in quale tag desideri unire il tag selezionato.

   ![Finestra di dialogo Unisci tag](assets/merge-tag.png)

1. Seleziona **Invia**.

Il tag selezionato nella console viene unito al tag specificato nella finestra di dialogo. Quando un tag di riferimento viene spostato o unito, il tag non viene fisicamente eliminato in modo tale da poter mantenere i riferimenti. Per ulteriori informazioni, vedere [Framework di assegnazione tag AEM](/help/implementing/developing/introduction/tagging-framework.md#moving-and-merging-tags).

### Eliminazione dei tag {#deleting-tags}

Se la tassonomia dei tag cambia e non è necessario specificare un tag o uno spazio dei nomi, è possibile eliminarlo.

1. Per eliminare un tag, apri la [console tag](#tagging-console).

1. Selezionare il tag da eliminare, quindi selezionare **Elimina** nella barra degli strumenti.

1. La finestra di dialogo **Elimina tag** richiede una conferma per eliminare i tag selezionati. Seleziona **Elimina**.

   ![Finestra modale di conferma eliminazione tag](assets/delete-tag.png)

1. L’AEM verifica che non sia presente alcun riferimento al tag.

   1. Se non viene trovato alcun riferimento, l&#39;AEM chiede la conferma finale per l&#39;eliminazione. Seleziona **Elimina**

      ![Nessun riferimento trovato](assets/no-references-found.png)

   1. Se vengono trovati dei riferimenti, l&#39;AEM li presenta e chiede una conferma finale per la loro cancellazione.

      ![Riferimenti trovati](assets/references-found.png)

I tag selezionati vengono eliminati e rimossi in modo permanente dall’ambiente di authoring. Se il tag è stato pubblicato, viene rimosso anche dall’ambiente di pubblicazione. Se il tag selezionato è un tag contenitore, vengono rimossi anche tutti i relativi tag figlio.

<!--

## Setting Tag Permissions {#setting-tag-permissions}

Tag permissions are ['secure (by default)'](/help/sites-administering/production-ready.md); a best practice for the publish environment that requires read permission to be explicitly allowed for tags. Bascially, this is done by creating a package of the Tag Namespace after permissions have been set on author, and installing the package on all publish instances.

* on author instance

    * sign in with administrative privileges
    * access the [Security Console](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

        * for example, browse to http://localhost:4502/useradmin

    * in the left pane, select the group (or user) for which [read permission](/help/sites-administering/security.md#permissions) is to be granted
    * in the right pane, locate the **Path **to the Tag Namespace

        * for example, `/content/cq:tags/mycommunity`

    * select the `checkbox`in the **Read** column
    * select **Save**

![Setting tag permissions](assets/chlimage_1-204.png)

* ensure all publish instances have same permissions

    * one approach is to [create a package](/help/sites-administering/package-manager.md#package-manager) of the namespace on author

        * on `Advanced` tab, for `AC Handling` select `Overwrite`

    * replicate the package

        * choose `Replicate` from package manager

-->

## Gestione dei tag in lingue diverse {#managing-tags-in-different-languages}

La proprietà `title` di un tag può essere tradotta in più lingue. Una volta tradotto, il titolo del tag appropriato può essere visualizzato in base all’utente o alla lingua del contenuto.

Supponiamo di avere un tag denominato `Animals` che vogliamo tradurre in tedesco e francese.

1. Apri la [console di assegnazione tag](#tagging-console).

1. Seleziona il tag da tradurre, quindi seleziona **Modifica** nella barra degli strumenti.

1. Nella finestra di dialogo **Modifica tag**, nella colonna **Localizzazione**, selezionare la lingua di destinazione, ad esempio il tedesco.

1. Nel campo **Tedesco** visualizzato, fornisci il titolo tradotto.

1. Ripeti i due passaggi precedenti per il francese.

   ![Traduzione titoli tag](assets/translate-tag.png)

1. Seleziona **Invia**.

Per le pagine di contenuto, la lingua scelta per il tag viene presa dalla lingua della pagina, se disponibile.

Tuttavia, nell’ambiente di authoring, AEM utilizza l’impostazione della lingua utente. Nella console dei tag, quindi, per il tag `Animals`, `Animaux` verrebbe visualizzato per un utente che imposta la lingua sul francese nelle proprietà utente.

Per aggiungere una nuova lingua alla finestra di dialogo, consulta il documento [Creazione di tag nelle applicazioni AEM](/help/implementing/developing/introduction/tagging-applications.md#adding-a-new-language-to-the-edit-tag-dialog)

>[!TIP]
>
>Per ulteriori informazioni sulle funzionalità di localizzazione dell&#39;AEM, vedere [Traduzione del contenuto per siti multilingue](/help/sites-cloud/administering/translation/overview.md).
