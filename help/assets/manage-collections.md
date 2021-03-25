---
title: Gestire le raccolte di risorse digitali
description: Comprendi il concetto di raccolta in Adobe Experience Manager Assets. Scopri come raccogliere, gestire, modificare e raccogliere con altri utenti.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: bd02261e62de28860c6c95794cd69e6529240b6d
workflow-type: tm+mt
source-wordcount: '2397'
ht-degree: 19%

---


# Gestire le raccolte {#manage-collections}

Una raccolta è un set di risorse all’interno di Adobe Experience Manager Assets. Utilizza le raccolte per condividere le risorse tra gli utenti. Il set può essere una raccolta statica o una raccolta dinamica basata sui risultati della ricerca.

A differenza delle cartelle, una raccolta può includere risorse da posizioni diverse. Puoi condividere raccolte con vari utenti a cui sono assegnati diversi livelli di privilegi, tra cui visualizzazione, modifica e così via.

Puoi condividere più raccolte con un utente. Ogni raccolta contiene riferimenti alle risorse. L’integrità referenziale delle risorse viene mantenuta tra le raccolte.

Le raccolte sono dei tipi seguenti, in base alla modalità di raccolta delle risorse:

* Una raccolta contenente un elenco di riferimento statico di risorse, cartelle e altre raccolte.

* Una raccolta avanzata che include in modo dinamico le risorse in base a un criterio di ricerca.

## Accedi alla console Raccolte {#navigate-the-collections-console}

Per aprire la console **[!UICONTROL Raccolte]**:

Per aprire le **[!UICONTROL Raccolte]**, tocca o fai clic sul logo di Experience Manager. Dalla pagina di navigazione, passa a **[!UICONTROL Risorse]** > **[!UICONTROL Raccolte]**.

## Creare una raccolta {#create-a-collection}

È possibile creare una raccolta con [riferimenti statici](#create-a-collection-with-static-references) o in base a un [filtro basato su criteri di ricerca](#create-a-smart-collection). Puoi anche creare una raccolta da una Lightbox.

### Creare una raccolta con riferimenti statici {#create-a-collection-with-static-references}

Puoi creare una raccolta con riferimenti statici, ad esempio una raccolta con riferimenti a risorse, cartelle, raccolte, set 360 gradi e set di immagini.

1. Passa alla console **[!UICONTROL Raccolte]** .
1. Dalla barra degli strumenti, tocca o fai clic su **[!UICONTROL Crea]**.
1. Nella pagina **[!UICONTROL Crea raccolta]**, immetti un titolo e una descrizione facoltativa per la raccolta.
1. Aggiungi i membri alla raccolta e assegna le autorizzazioni appropriate. In alternativa, per consentire a tutti gli utenti di accedere alla raccolta, seleziona **[!UICONTROL Raccolta pubblica]**.

   >[!NOTE]
   >
   >Per consentire ai membri di condividere le raccolte con altri utenti, fornisci al gruppo `dam-users` le autorizzazioni di lettura nel percorso `home/users`. Concedi l&#39;autorizzazione agli utenti nella posizione `/content/dam/collections` per consentire agli utenti di visualizzare le raccolte negli elenchi a comparsa. In alternativa, imposta l’utente come parte del gruppo `dam-users` .

1. (Facoltativo) Aggiungi una miniatura per la raccolta.
1. Tocca o fai clic su **[!UICONTROL Crea]**, quindi tocca o fai clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo. Una raccolta con il titolo e le proprietà specificati viene aperta nella console Raccolte.

   >[!NOTE]
   >
   >Risorse di Experience Manager consente di creare attività di revisione per una raccolta, in modo analogo a come si creano le attività di revisione per una cartella di risorse.

   Per aggiungere risorse alla raccolta, passa all’interfaccia utente Assets. Per informazioni dettagliate, consulta [Aggiungere risorse a una raccolta](#add-assets-to-a-collection).

### Creare raccolte utilizzando la zona di rilascio {#create-collections-using-dropzone}

Puoi trascinare le risorse dall’interfaccia utente di Assets in una raccolta. Puoi anche creare una copia di una raccolta e trascinarvi le risorse.

1. Dall’interfaccia utente Assets, seleziona le risorse da aggiungere a una raccolta.
1. Trascina le risorse nella zona **[!UICONTROL Rilascia raccolta]** . In alternativa, tocca o fai clic sull&#39;icona **[!UICONTROL To Collection]** nella barra degli strumenti.
1. Nella pagina **[!UICONTROL Aggiungi a raccolta]**, tocca o fai clic sull’icona **[!UICONTROL Crea raccolta]** dalla barra degli strumenti. Se vuoi aggiungere le risorse a una raccolta esistente, selezionala dalla pagina, quindi tocca o fai clic su **[!UICONTROL Aggiungi]**. Per impostazione predefinita, è selezionata la raccolta aggiornata più di recente.
1. Nella finestra di dialogo **[!UICONTROL Crea nuova raccolta]**, specifica un nome per la raccolta. Se vuoi che la raccolta sia accessibile a tutti gli utenti, seleziona **[!UICONTROL Raccolta pubblica]**.
1. Tocca o fai clic su **[!UICONTROL Continua]** per creare la raccolta.

### Creare una raccolta avanzata {#create-a-smart-collection}

Una raccolta avanzata utilizza un criterio di ricerca per popolare dinamicamente le risorse. È possibile creare una raccolta avanzata utilizzando solo file e non cartelle o file e cartelle.

1. Passa all’interfaccia utente Assets e tocca o fai clic sull’icona **[!UICONTROL Ricerca]**.
1. Immetti la parola chiave di ricerca nella casella Ricerca Omni e seleziona `Enter`. Tocca o fai clic sull’icona Navigazione globale per visualizzare il pannello Filtri e applicare un filtro di ricerca dal pannello Ricerca.
1. Dall&#39;elenco **[!UICONTROL File e cartelle]**, selezionare **[!UICONTROL File]**.
1. Tocca o fai clic su **[!UICONTROL Salva raccolta avanzata]**.
1. Specifica un nome per la raccolta. Seleziona **[!UICONTROL Public]** per aggiungere il gruppo DAM Users con il ruolo Visualizzatore alla raccolta avanzata.

   >[!NOTE]
   >
   >Se selezioni **[!UICONTROL Pubblico]**, la raccolta avanzata diventa disponibile a tutti coloro che dispongono del ruolo Proprietario dopo la creazione. Se annulli l’opzione **[!UICONTROL Public]** , il gruppo di utenti DAM non è più associato alla raccolta avanzata.

1. Per creare la raccolta avanzata, tocca/fai clic su **[!UICONTROL Salva]**, quindi chiudi la finestra messaggio per completare il processo. La nuova raccolta avanzata viene aggiunta anche all’elenco **[!UICONTROL Saved Searches (Ricerche salvate)]**.
L’etichetta del pulsante **[!UICONTROL Create Smart Selection (Crea selezione avanzata)]** diventa **[!UICONTROL Edit Smart Selection (Modifica selezione avanzata)]**. Per modificare le impostazioni della raccolta avanzata, seleziona **[!UICONTROL File]** dall’elenco **[!UICONTROL File e cartelle]**. Quindi tocca o fai clic sul pulsante **[!UICONTROL Edit Smart Selection (Modifica selezione avanzata)]**.

## Aggiungere risorse a una raccolta {#add-assets-to-a-collection}

Puoi aggiungere risorse a una raccolta contenente un elenco di risorse o cartelle a cui si fa riferimento.

>[!NOTE]
>
>Le raccolte avanzate utilizzano una query di ricerca per popolare le risorse. Pertanto, i riferimenti statici a risorse e cartelle non sono applicabili a tali risorse.

1. Nell’interfaccia utente Assets, individua la posizione della risorsa da aggiungere a una raccolta.
1. Seleziona la risorsa e tocca o fai clic sull&#39;icona **[!UICONTROL To Collection]** nella barra degli strumenti. In alternativa, puoi trascinare la risorsa nella zona **[!UICONTROL Rilascia raccolta]** . Rilasciare il pulsante del mouse quando la zona di rilascio diventa attiva e l&#39;etichetta diventa **[!UICONTROL Rilascia per aggiungere]**.
1. Nella pagina **[!UICONTROL Aggiungi alla raccolta]** , seleziona la raccolta alla quale desideri aggiungere la risorsa.
1. Tocca o fai clic su **[!UICONTROL Aggiungi]**, quindi chiudi il messaggio di conferma. La risorsa viene aggiunta alla raccolta.

## Modificare una raccolta avanzata {#edit-a-smart-collection}

Le raccolte avanzate vengono create salvando una ricerca in modo da poter modificare il loro contenuto modificando i parametri di ricerca della [ricerca salvata](#saved-searches).

1. Nell’interfaccia utente Assets, tocca o fai clic sull’icona **[!UICONTROL Cerca]** nella barra degli strumenti.
1. Con il cursore nella casella Omnisearch, selezionare il tasto `Enter`.
1. Tocca o fai clic sull’icona Navigazione globale per visualizzare il pannello Filtri .
1. Dall’elenco **[!UICONTROL Ricerche salvate]**, seleziona la raccolta avanzata da modificare. Nel pannello Ricerca sono visualizzati i filtri configurati per la ricerca salvata.
1. Dall&#39;elenco **[!UICONTROL File e cartelle]**, selezionare **[!UICONTROL File]**.
1. Se necessario, modifica uno o più filtri. Tocca o fai clic su **[!UICONTROL Modifica raccolta avanzata]**. Puoi anche modificare il nome della raccolta avanzata.
1. Tocca o fai clic su **[!UICONTROL Salva]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica raccolta avanzata]**.
1. Tocca o fai clic su **[!UICONTROL Sovrascrivi]** per sostituire la raccolta avanzata originale con la raccolta modificata. In alternativa, selezionare **[!UICONTROL Salva con nome]** per salvare separatamente la raccolta modificata.
1. Nella finestra di dialogo di conferma, tocca o fai clic su **[!UICONTROL Salva]** per completare il processo.

## Visualizzare e modificare i metadati della raccolta {#view-and-edit-collection-metadata}

I metadati della raccolta includono dati sulla raccolta, compresi eventuali tag aggiunti.

1. Dalla console Raccolte, seleziona una raccolta e tocca o fai clic sull’icona **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Nella pagina **[!UICONTROL Metadati raccolta]**, seleziona le schede **[!UICONTROL Base]** e **Avanzate** per visualizzare i metadati della raccolta.
1. Modifica i metadati, se necessario, quindi tocca o fai clic su **[!UICONTROL Salva e chiudi]** nella barra degli strumenti per salvare le modifiche.

### Modifica i metadati della raccolta in blocco {#edit-collection-metadata-in-bulk}

Puoi modificare i metadati di più raccolte contemporaneamente. Questa funzionalità consente di replicare rapidamente i metadati comuni in più raccolte.

1. Nella console Raccolte , seleziona una o più raccolte di cui desideri modificare i metadati.
1. Dalla barra degli strumenti, tocca o fai clic sull&#39;icona **[!UICONTROL Proprietà]** .
1. Nella pagina **[!UICONTROL Metadati raccolta]**, modifica i metadati nelle schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]**, secondo necessità.
1. Tocca o fai clic su **[!UICONTROL Salva e chiudi]** nella barra degli strumenti, quindi chiudi la finestra di dialogo di conferma per completare il processo.
1. Per aggiungere i nuovi metadati a quelli esistenti, seleziona **[!UICONTROL Modalità di aggiunta]**. Se non selezioni questa opzione, i nuovi metadati sostituiranno quelli già esistenti nei campi. Tocca o fai clic su **[!UICONTROL Invia]**.

   >[!NOTE]
   >
   >La modalità di aggiunta funziona solo per i campi che possono contenere più valori. Per i campi che possono includere un solo valore, i nuovi metadati non vengono aggiunti al valore esistente del campo, anche se selezioni **[!UICONTROL Modalità di aggiunta]**.

## Ricerca {#searching}

La funzione Ricerca nelle raccolte supporta sia [Ricerca di raccolte](#search-collections) che [Ricerca di risorse all&#39;interno di una raccolta](#search-within-collections).

### Raccolte di ricerca {#search-collections}

Puoi cercare le raccolte dalla console Raccolte . Quando esegui una ricerca con parole chiave nella casella Omnisearch, [!DNL Experience Manager Assets] cerca i nomi delle raccolte, i metadati e i tag aggiunti alle raccolte.

Se cerchi raccolte dal livello principale, nei risultati della ricerca vengono restituite solo singole raccolte. Le risorse o le cartelle all’interno delle raccolte sono escluse. In tutti gli altri casi (ad esempio, all’interno di una singola raccolta o in una gerarchia di cartelle), vengono restituite tutte le risorse, le cartelle e le raccolte pertinenti.

### Ricerca nelle raccolte {#search-within-collections}

Nella console Raccolte, tocca o fai clic su una raccolta per aprirla.

All&#39;interno di una raccolta, la ricerca [!DNL Experience Manager] è limitata alle risorse (e ai relativi tag e metadati) all&#39;interno della raccolta che stai visualizzando. Quando esegui una ricerca all’interno di una cartella, vengono restituite tutte le risorse e le cartelle secondarie corrispondenti all’interno della cartella corrente. Quando esegui una ricerca all’interno di una raccolta, vengono restituite solo le risorse, le cartelle e le altre raccolte corrispondenti ai membri diretti della raccolta.

## Modifica impostazioni raccolta {#edit-collection-settings}

È possibile modificare le impostazioni della raccolta, ad esempio titolo e descrizione, o aggiungere membri a una raccolta.

1. Seleziona una raccolta e tocca o fai clic sull&#39;icona **[!UICONTROL Impostazioni]** nella barra degli strumenti. In alternativa, utilizza l&#39;azione rapida **[!UICONTROL Impostazioni]** dalla miniatura della raccolta.
1. Nella pagina **[!UICONTROL Impostazioni raccolta]**, puoi modificare le impostazioni della raccolta. Ad esempio, modifica il titolo della raccolta, le descrizioni, i membri e le autorizzazioni, in base a quanto descritto in [Aggiungi raccolta](#create-a-collection).
1. Tocca o fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

## Eliminare una raccolta {#delete-a-collection}

1. Dalla console Raccolte , seleziona una o più raccolte e tocca o fai clic sull’icona Elimina nella barra degli strumenti.
1. Nella finestra di dialogo, tocca o fai clic su **[!UICONTROL Elimina]** per confermare l’eliminazione.

   >[!NOTE]
   >
   >È inoltre possibile eliminare le raccolte avanzate [eliminando le ricerche salvate](#saved-searches).

## Scarica una raccolta {#download-a-collection}

Quando scarichi una raccolta, viene scaricata l’intera gerarchia delle risorse all’interno della raccolta, incluse le cartelle e le raccolte secondarie.

1. Dalla console Raccolte , seleziona una o più raccolte da scaricare.
1. Dalla barra degli strumenti, tocca o fai clic sull’icona di download.
1. Nella finestra di dialogo **[!UICONTROL Scarica]**, tocca o fai clic su **[!UICONTROL Scarica]**. Se desideri scaricare i rendering delle risorse all&#39;interno della raccolta, seleziona **[!UICONTROL Rendering]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   Quando selezioni una raccolta da scaricare, viene scaricata la gerarchia completa delle cartelle sotto la raccolta. Per includere ogni raccolta scaricata (incluse le risorse nelle raccolte secondarie nidificate sotto la raccolta principale) in una singola cartella, seleziona **[!UICONTROL Crea una cartella separata per ogni risorsa]**.

## Modifica le proprietà dei metadati di più raccolte {#editing-metadata-properties-of-multiple-collections}

Adobe Enterprise Manager Assets consente di modificare i metadati di molte raccolte in blocco. Utilizza la pagina [!UICONTROL Proprietà] per eseguire modifiche ai metadati su più raccolte, ad esempio, modifica le proprietà dei metadati in un valore comune o aggiungi o modifica tag.

Per personalizzare la pagina dei metadati [!UICONTROL Proprietà], inclusa l&#39;aggiunta, la modifica, l&#39;eliminazione delle proprietà dei metadati, utilizza l&#39;editor schema.

>[!NOTE]
>
>I metodi di modifica collettiva funzionano per le risorse disponibili in una raccolta. Per le risorse disponibili nelle cartelle o che corrispondono a un criterio comune, è possibile [aggiornare in blocco i metadati dopo la ricerca](/help/assets/search-assets.md#metadata-updates).

1. Dalla console Raccolte, seleziona le raccolte da modificare.
1. Dalla barra degli strumenti, tocca o fai clic su **[!UICONTROL Proprietà]** per aprire la pagina [!UICONTROL Proprietà] per le raccolte selezionate.
1. Modifica le proprietà dei metadati per le raccolte selezionate nelle varie schede.

   >[!NOTE]
   >
   >I metadati aggiunti per le raccolte selezionate sovrascrivono i metadati precedenti per queste raccolte, ad eccezione dei tag. Tutti i tag aggiunti nel campo **[!UICONTROL Tag]** vengono aggiunti all’elenco esistente di tag nei metadati.

1. Per visualizzare le proprietà dei metadati per una raccolta specifica, annullare la selezione delle raccolte rimanenti nell&#39;elenco delle raccolte. I campi dell’editor di metadati sono compilati con i metadati per la raccolta specifica.

   >[!NOTE]
   >
   >* Nella pagina delle proprietà della raccolta, puoi rimuovere le raccolte dall’elenco delle raccolte annullando la selezione. Nell’elenco delle raccolte sono selezionate tutte le raccolte per impostazione predefinita. I metadati per le raccolte rimosse non vengono aggiornati.
   >* Nella parte superiore dell’elenco, seleziona la casella di controllo accanto a **[!UICONTROL Titolo]** per passare dalla selezione delle raccolte alla cancellazione dell’elenco.


1. Salva le modifiche.

## Creare raccolte nidificate {#create-nested-collections}

È possibile aggiungere una raccolta a un&#39;altra raccolta, creando in tal modo una raccolta nidificata.

1. Dalla console Raccolte, seleziona la raccolta o il gruppo di raccolte desiderato, quindi tocca o fai clic su **[!UICONTROL To Collection]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Aggiungi alla raccolta]**, seleziona la raccolta in cui aggiungere la raccolta.

   >[!NOTE]
   >
   >La raccolta aggiornata più di recente è selezionata per impostazione predefinita nella pagina **[!UICONTROL Aggiungi alla raccolta]** .

1. Tocca o fai clic su **[!UICONTROL Aggiungi]**. Un messaggio conferma che la raccolta viene aggiunta alla raccolta di destinazione nella pagina **[!UICONTROL Seleziona destinazione]** . Chiudi il messaggio per completare il processo.

>[!NOTE]
>
>Le raccolte avanzate non possono essere nidificate. In altre parole, le raccolte avanzate non possono contenere altre raccolte.

## Ricerche salvate {#saved-searches}

Nell’interfaccia utente Assets, puoi cercare o filtrare le risorse in base a determinate regole, criteri di ricerca o facet di ricerca personalizzata. Se salvi queste ricerche come **[!UICONTROL Ricerche salvate]**, puoi accedervi in un secondo momento dall’elenco **[!UICONTROL Ricerche salvate]** nel pannello Filtro. La creazione di una ricerca salvata genera anche una raccolta avanzata.

Le ricerche salvate vengono create quando generi una raccolta avanzata. Le raccolte avanzate vengono aggiunte automaticamente all’elenco **[!UICONTROL Ricerche salvate]**. La query delle Ricerche salvate per la raccolta viene salvata nella posizione relativa nella proprietà `dam:query` di CRXDE `/content/dam/collections/`. Non ci sono limiti alle ricerche che puoi salvare e alle ricerche salvate visualizzate nell’elenco.

>[!NOTE]
>
>Puoi condividere le raccolte avanzate nello stesso modo in cui condividi le raccolte statiche.

La modifica delle ricerche salvate equivale alla modifica delle raccolte avanzate. Per informazioni dettagliate, consulta [Modificare una raccolta avanzata](#edit-a-smart-collection).

Per eliminare le ricerche salvate, effettua le seguenti operazioni:

1. Nell’interfaccia utente Assets, tocca o fai clic sull’icona di ricerca nella barra degli strumenti.

1. Con il cursore nel campo Omnisearch , seleziona il tasto `Enter` .
1. Tocca o fai clic sull’icona Navigazione globale per visualizzare il pannello Filtri .
1. Nell’elenco **[!UICONTROL Ricerche salvate]**, tocca o fai clic su **[!UICONTROL Elimina]** accanto alla raccolta avanzata da eliminare.
1. Nella finestra di dialogo, tocca o fai clic su **[!UICONTROL Elimina]** per eliminare la ricerca salvata.

## Eseguire un flusso di lavoro su una raccolta {#run-a-workflow-on-a-collection}

Puoi eseguire un flusso di lavoro per le risorse all’interno di una raccolta. Se la raccolta contiene raccolte nidificate, il flusso di lavoro viene eseguito anche sulle risorse all’interno delle raccolte nidificate. Tuttavia, se la raccolta e la raccolta nidificata contengono risorse duplicate, il flusso di lavoro viene eseguito una sola volta per tali risorse.

1. Dalla console Raccolte , seleziona una raccolta in cui desideri eseguire un flusso di lavoro.
1. Tocca o fai clic sull&#39;icona di navigazione globale e scegli **[!UICONTROL Timeline]** dall&#39;elenco.
1. Dalla timeline, seleziona o tocca l’icona del cursore verso il basso, quindi tocca o fai clic su **[!UICONTROL Avvia flusso di lavoro]**.
1. Nella sezione **[!UICONTROL Avvia flusso di lavoro]**, seleziona un modello di flusso di lavoro dall’elenco. Ad esempio, scegli il modello **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Inserisci un titolo per il flusso di lavoro e tocca o fai clic su **[!UICONTROL Avvia]**.
1. Nella finestra di dialogo, tocca o fai clic su **[!UICONTROL Procedi]**. Il flusso di lavoro viene eseguito su tutte le risorse della raccolta.

>[!MORELIKETHIS]
>
>* [Creare un&#39;attività di revisione per le raccolte](/help/assets/bulk-approval.md)

