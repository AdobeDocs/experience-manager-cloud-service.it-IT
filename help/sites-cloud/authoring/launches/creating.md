---
title: Creazione dei lanci
description: Puoi creare un lancio per abilitare l’aggiornamento di una nuova versione di pagine web esistenti da attivare in futuro.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Creazione dei lanci {#creating-launches}

Puoi creare un lancio per abilitare l’aggiornamento di una nuova versione di pagine web esistenti da attivare in futuro. Per creare un lancio, è necessario specificare un titolo e la pagina di origine:

* The title appears in the [References](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) rail, from where authors can access them to work on them.
* Per impostazione predefinita nel lancio vengono incluse le pagine figlie della pagina di origine. Se necessario, potete comunque usare anche solo la pagina sorgente.
* Per impostazione predefinita, Live Copy aggiorna automaticamente le pagine di lancio mano a mano che vengono modificate le pagine sorgente. Per evitare che vengano apportate tali modifiche automatiche, puoi specificare che venga creata una copia statica. <!--By default, [Live Copy](/help/sites-administering/msm.md) automatically updates the launch pages as the source pages change. You can specify that a static copy is created to prevent automatic changes.-->

Facoltativamente, puoi specificare **la data (e l’ora) di lancio** per definire quando promuovere e attivare le pagine di lancio. However the **Launch Date** only operates in combination with the **Production Ready** flag (see [Editing a Launch Configuration](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration)); for the actions to actually occur automatically, both must be set.

## Creazione di un lancio {#creating-a-launch}

Puoi creare un lancio da Sites o dalla console Lanci:

1. Apri la console **Sites** o **Lanci**.

   >[!NOTE]
   >
   >Quando usi la console **Sites** solitamente si accede alla posizione della pagina sorgente, ma non è obbligatorio, perché puoi accedervi quando selezioni l’**Origine del lancio** nella procedura guidata.

1. A seconda della console utilizzata:
   * **Lanci**:
      1. Seleziona **Crea lancio** dalla barra degli strumenti per aprire la procedura guidata.
   * **Sites**:
      1. Seleziona **Crea** nella barra degli strumenti per aprire la casella di selezione.
      1. Da qui seleziona **Crea lancio** per aprire la procedura guidata.
   >[!NOTE]
   >
   >Nella console **Sites** puoi anche usare la [modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) per selezionare una pagina prima di selezionare **Crea**.
   >
   >La pagina selezionata verrà così utilizzata come pagina sorgente iniziale.

1. Nel passaggio **Seleziona origine** è necessario usare la funzione **Aggiungi pagine**. Puoi selezionare più pagine, specificando il percorso per ciascuna:
   * Passa alla posizione desiderata.
   * Selezionate le pagine di origine e confermate (segno di spunta).
   Ripeti in base alle esigenze.  

   ![Seleziona origine lancio](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >Per aggiungere pagine e/o rami a un lancio, questi devono essere all’interno di un sito; in altre parole, in una directory comune di primo livello.
   >
   >Se un sito contiene directory principali per lingue inferiori al primo livello, le pagine e i rami di un lancio devono essere in una directory principale per lingua comune.

1. Per ogni voce puoi specificare le seguenti opzioni:

   * **Includi le pagine secondarie**:

      * Specifica se creare il lancio con o senza pagine figlie.  Per impostazione predefinita, le pagine secondarie sono incluse.
   Procedi con **Successivo**.

   ![Seleziona origine lancio](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. Nel passaggio **Proprietà** della procedura guidata puoi specificare:

   * **Titolo lancio**: nome del lancio. Scegli un nome che possa essere facilmente riconosciuto dagli autori.
   * **con contenuto esistente**: il contenuto originale verrà utilizzato per creare il lancio.
   * **con un nuovo modello per sostituire la pagina**: per ulteriori dettagli, vedi [Creare un lancio con un nuovo modello](#create-launch-with-new-template).
   * **Eredita i dati live della pagina di origine**: seleziona questa opzione per aggiornare automaticamente il contenuto delle pagine di lancio quando cambiano le pagine di origine. Questa opzione consente di ottenere questo risultato rendendo il lancio una copia dal vivo. Per impostazione predefinita, questa opzione è selezionata.<!--Select this option to automatically update the content of launch pages when the source pages change. This option achieves this by making the launch a [live copy](/help/sites-administering/msm.md). By default, this option is selected.-->
   * **Data lancio**: la data e l&#39;ora in cui la copia del lancio deve essere attivata (in base alla segnalazione **Produzione pronta**; consulta [Lanci: l&#39;ordine degli eventi](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)).
   ![Proprietà di avvio](/help/sites-cloud/authoring/assets/launches-properties.png)

1. Tocca o fai clic su **Crea** per completare il processo e creare il nuovo lancio. La finestra di dialogo di conferma chiederà se desideri aprire il lancio immediatamente.

   Se torni alla console (con **Fine**), puoi visualizzare il lancio (e accedervi) in uno dei due modi seguenti:

   * The [**Launches **console](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * The [**References **in the** Sites **console](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### Creare un lancio con un nuovo modello {#create-launch-with-new-template}

Quando creai un lancio puoi utilizzare un nuovo modello scegliendo la seguente opzione:

>[!NOTE]
>
>Questa opzione è disponibile solo quando crei un lancio dalla console **Sites**. Non è disponibile quando crei un lancio dalla console **Lanci**.

![Creazione di un lancio con un nuovo modello](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

Quando selezioni questa opzione:

* Aggiornare le altre opzioni disponibili,
* Includete un nuovo passaggio in cui potete selezionare il modello richiesto.

![Selezione di un nuovo modello](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>Quando utilizzi un modello diverso, la nuova pagina sarà vuota. A causa della diversa struttura della pagina, non verrà copiato alcun contenuto.
>
>Questo metodo può essere utilizzato per modificare il modello di una [pagina esistente](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page); tuttavia, deve essere tenuta in considerazione la perdita di contenuto.

### Creazione di un lancio nidificato {#creating-a-nested-launch}

Un lancio nidificato (lancio all’interno di un altro lancio) dà la possibilità di creare un lancio da un lancio esistente in modo che gli autori possano sfruttare le modifiche già apportate, anziché doverle apportare più volte per ogni lancio.

>[!NOTE]
>
>Vedi anche [Promozione di un lancio nidificato](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch).

#### Creazione di un lancio nidificato: console Lanci {#creating-a-nested-launch-launches-console}

Creating a nested launch from the **Launches** console is basically the same as creating any other form of launch, with the exception that you need to navigate to the launches branch `/content/launches`:

1. Nella console **Lanci** seleziona **Crea**.
1. Select **Add Pages**, then navigate to the launches branch by specifying `/content/launches` in the filter. Seleziona il lancio richiesto e conferma con **Seleziona**:

   ![Creazione di un lancio nidificato](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. Procedi con **Successivo** e imposta le **Proprietà** come per un qualsiasi altro lancio.

   ![Seleziona origine per il lancio nidificato](/help/sites-cloud/authoring/assets/launches-create-nested-select.png)

#### Creazione di un lancio nidificato: console Sites {#creating-a-nested-launch-sites-console}

Per creare un lancio nidificato dalla console **Sites**, basato su un lancio esistente:

1. Accedi a [Lancio da Riferimenti (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) per visualizzare le azioni disponibili.
1. Seleziona **Crea lancio** per aprire la procedura guidata (poiché la sorgente è già stata selezionata, verrà saltato il passaggio **Seleziona origine**).
1. Immetti il **Titolo lancio** e tutti gli altri dettagli richiesti (come con un normale lancio).
1. Tocca o fai clic su **Crea** per completare il processo e creare il nuovo lancio. La finestra di dialogo di conferma chiederà se desideri aprire il lancio immediatamente.

If you select **Done**, you are returned to the **References** rail of the **Sites** console, if you select the appropriate page your new launch is shown.

### Eliminazione di un lancio {#deleting-a-launch}

Puoi eliminare un lancio dalla [console Lanci](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):

* Seleziona il lancio, toccando o facendo clic sulla miniatura.
* Viene visualizzata la barra degli strumenti: scegli Elimina.
* Conferma l’azione.

>[!CAUTION]
>
>L’eliminazione del lancio rimuove il lancio stesso e tutti i lanci nidificati discendenti.
