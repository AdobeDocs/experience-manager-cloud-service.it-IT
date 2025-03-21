---
title: Gestire le raccolte di risorse digitali
description: Comprendere il concetto di raccolta in Adobe Experience Manager Assets. Scopri come gestire, modificare e raccogliere insieme ad altri utenti.
contentOwner: AG
mini-toc-levels: 1
feature: Collections, Asset Management
role: User
exl-id: b0798adc-56a4-4577-b4ee-8d1fca3bff09
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '2444'
ht-degree: 19%

---

# Gestire le raccolte {#manage-collections}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-collections.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Una raccolta è un insieme di risorse all’interno di Adobe Experience Manager Assets. Puoi utilizzare le raccolte per condividere le risorse tra i vari utenti. Il set può essere una raccolta statica o dinamica basata sui risultati della ricerca.

A differenza delle cartelle, una raccolta può includere risorse da posizioni diverse. Puoi condividere raccolte con vari utenti a cui sono assegnati livelli diversi di privilegi, tra cui visualizzazione, modifica e così via.

Puoi condividere più raccolte con un utente. Ogni raccolta contiene riferimenti alle risorse. L’integrità dei riferimenti alle risorse viene mantenuta tra le varie raccolte.

Le raccolte sono dei seguenti tipi, in base al modo in cui raccolgono le risorse:

* Una raccolta che contiene un elenco di riferimento statico di risorse, cartelle e altre raccolte.

* Una raccolta avanzata che include dinamicamente le risorse in base a un criterio di ricerca.

## Accedere alla console delle raccolte {#navigate-the-collections-console}

Per aprire la console **[!UICONTROL Raccolte]**:

Per aprire le **[!UICONTROL raccolte]**, seleziona il logo Experience Manager. Dalla pagina di navigazione, passa a **[!UICONTROL Assets]** > **[!UICONTROL Raccolte]**.

## Creare una raccolta {#create-a-collection}

È possibile creare una raccolta con [riferimenti statici](#create-a-collection-with-static-references) o in base a un [filtro basato su criteri di ricerca](#create-a-smart-collection). Puoi anche creare una raccolta da un lightbox.

### Creare una raccolta con riferimenti statici {#create-a-collection-with-static-references}

Puoi creare una raccolta con riferimenti statici, ad esempio una raccolta con riferimenti a risorse, cartelle, raccolte, set 360 gradi e set di immagini.

1. Passa alla console **[!UICONTROL Raccolte]**.
1. Dalla barra degli strumenti, seleziona **[!UICONTROL Crea]**.
1. Nella pagina **[!UICONTROL Crea raccolta]** immettere un titolo e una descrizione facoltativa per la raccolta.
1. Aggiungi i membri alla raccolta e assegna le autorizzazioni appropriate. In alternativa, per consentire a tutti gli utenti di accedere alla raccolta, seleziona **[!UICONTROL Raccolta pubblica]**.

   >[!NOTE]
   >
   >Per consentire ai membri di condividere raccolte con altri utenti, fornire al gruppo `dam-users` le autorizzazioni di lettura nel percorso `home/users`. Concedere l&#39;autorizzazione agli utenti nella posizione `/content/dam/collections` per consentire agli utenti di visualizzare le raccolte negli elenchi popup. In alternativa, rendere l&#39;utente parte del gruppo `dam-users`.

1. (Facoltativo) Aggiungi una miniatura per la raccolta.
1. Seleziona **[!UICONTROL Crea]**, quindi seleziona **[!UICONTROL OK]** per chiudere la finestra di dialogo. Una raccolta con il titolo e le proprietà specificati viene aperta nella console Raccolte.

   >[!NOTE]
   >
   >In Experience Manager Assets è possibile creare attività di revisione per una raccolta in modo analogo a come si creano le attività di revisione per una cartella risorse.

   Per aggiungere risorse alla raccolta, passa all’interfaccia utente di Assets. Per ulteriori dettagli, vedere [Aggiungere risorse a una raccolta](#add-assets-to-a-collection).

### Creare raccolte tramite dropzone {#create-collections-using-dropzone}

Puoi trascinare le risorse dall’interfaccia utente di Assets a una raccolta. Puoi anche creare una copia di una raccolta e trascinarvi le risorse.

1. Dall’interfaccia utente di Assets, seleziona le risorse da aggiungere a una raccolta.
1. Trascina le risorse nella zona **[!UICONTROL Rilascia raccolta]**. In alternativa, seleziona l&#39;icona **[!UICONTROL Alla raccolta]** dalla barra degli strumenti.
1. Nella pagina **[!UICONTROL Aggiungi a raccolta]**, seleziona l&#39;icona **[!UICONTROL Crea raccolta]** dalla barra degli strumenti. Se desideri aggiungere le risorse a una raccolta esistente, selezionala dalla pagina, quindi seleziona **[!UICONTROL Aggiungi]**. Per impostazione predefinita, è selezionata la raccolta aggiornata più di recente.
1. Nella finestra di dialogo **[!UICONTROL Crea nuova raccolta]**, specifica un nome per la raccolta. Se vuoi che la raccolta sia accessibile a tutti gli utenti, seleziona **[!UICONTROL Raccolta pubblica]**.
1. Seleziona **[!UICONTROL Continua]** per creare la raccolta.

### Creare una raccolta avanzata {#create-a-smart-collection}

Una raccolta avanzata utilizza un criterio di ricerca per popolare dinamicamente le risorse. Puoi creare una raccolta avanzata utilizzando solo file e non cartelle o file e cartelle.

1. Passa all&#39;interfaccia utente di Assets e seleziona l&#39;icona **[!UICONTROL Cerca]**.
1. Immettere la parola chiave di ricerca nella casella Ricerca Omni e selezionare `Enter`. Seleziona l’icona GlobalNav per visualizzare il pannello Filtri e applicare un filtro di ricerca dal pannello Ricerca.
1. Dall&#39;elenco **[!UICONTROL File e cartelle]**, selezionare **[!UICONTROL File]**.
1. Seleziona **[!UICONTROL Salva raccolta avanzata]**.
1. Specifica un nome per la raccolta. Selezionare **[!UICONTROL Pubblico]** per aggiungere il gruppo Utenti DAM con il ruolo Visualizzatore alla raccolta avanzata.

   >[!NOTE]
   >
   >Se selezioni **[!UICONTROL Pubblico]**, la raccolta avanzata diventa disponibile per tutti coloro che hanno il ruolo di Proprietario dopo averla creata. Se si annulla l&#39;opzione **[!UICONTROL Public]**, il gruppo di utenti DAM non sarà più associato alla raccolta avanzata.

1. Seleziona **[!UICONTROL Salva]** per creare la raccolta avanzata, quindi chiudi la finestra di messaggio per completare il processo. La nuova raccolta avanzata viene aggiunta anche all&#39;elenco **[!UICONTROL Ricerche salvate]**.
L’etichetta del pulsante **[!UICONTROL Create Smart Selection (Crea selezione avanzata)]** diventa **[!UICONTROL Edit Smart Selection (Modifica selezione avanzata)]**. Per modificare le impostazioni della raccolta avanzata, seleziona **[!UICONTROL File]** dall’elenco **[!UICONTROL File e cartelle]**. Quindi, seleziona il pulsante **[!UICONTROL Modifica selezione avanzata]**.

## Aggiungere risorse a una raccolta {#add-assets-to-a-collection}

Puoi aggiungere risorse a una raccolta che contiene un elenco di risorse o cartelle a cui si fa riferimento.

>[!NOTE]
>
>Le raccolte avanzate utilizzano una query di ricerca per compilare le risorse. Pertanto, i riferimenti statici a risorse e cartelle non sono ad esse applicabili.

1. Nell’interfaccia utente di Assets, individua il percorso della risorsa da aggiungere a una raccolta.
1. Seleziona la risorsa e fai clic sull&#39;icona **[!UICONTROL A raccolta]** nella barra degli strumenti. In alternativa, puoi trascinare la risorsa nell&#39;area **[!UICONTROL Rilascia nella raccolta]**. Rilasciare il pulsante del mouse quando la zona di rilascio diventa attiva e la relativa etichetta diventa **[!UICONTROL Rilascia in Aggiungi]**.
1. Nella pagina **[!UICONTROL Aggiungi a raccolta]**, seleziona la raccolta a cui desideri aggiungere la risorsa.
1. Selezionare **[!UICONTROL Aggiungi]**, quindi chiudere il messaggio di conferma. La risorsa viene aggiunta alla raccolta.

## Modificare una raccolta avanzata {#edit-a-smart-collection}

Le raccolte avanzate vengono create salvando una ricerca in modo da modificarne il contenuto modificando i parametri di ricerca della [ricerca salvata](#saved-searches).

1. Nell&#39;interfaccia utente di Assets, seleziona l&#39;icona **[!UICONTROL Cerca]** dalla barra degli strumenti.
1. Con il cursore nella casella Omnisearch, selezionare il tasto `Enter`.
1. Seleziona l’icona GlobalNav per visualizzare il pannello Filtri.
1. Dall’elenco **[!UICONTROL Ricerche salvate]**, seleziona la raccolta avanzata da modificare. Nel pannello Ricerca sono visualizzati i filtri configurati per la ricerca salvata.
1. Dall&#39;elenco **[!UICONTROL File e cartelle]**, selezionare **[!UICONTROL File]**.
1. Modifica uno o più filtri, a seconda delle necessità. Seleziona **[!UICONTROL Modifica raccolta avanzata]**. Puoi anche modificare il nome della raccolta avanzata.
1. Seleziona **[!UICONTROL Salva]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica raccolta avanzata]**.
1. Seleziona **[!UICONTROL Sovrascrivi]** per sostituire la raccolta avanzata originale con la raccolta modificata. In alternativa, selezionare **[!UICONTROL Salva con nome]** per salvare separatamente la raccolta modificata.
1. Nella finestra di dialogo di conferma, seleziona **[!UICONTROL Salva]** per completare il processo.

## Visualizzare e modificare i metadati di una raccolta {#view-and-edit-collection-metadata}

I metadati della raccolta includono i dati sulla raccolta, inclusi eventuali tag aggiunti.

1. Dalla console Raccolte, seleziona una raccolta e l&#39;icona **[!UICONTROL Proprietà]** dalla barra degli strumenti.
1. Nella pagina **[!UICONTROL Metadati raccolta]**, seleziona le schede **[!UICONTROL Base]** e **Avanzate** per visualizzare i metadati della raccolta.
1. Modificare i metadati in base alle esigenze, quindi selezionare **[!UICONTROL Salva e chiudi]** nella barra degli strumenti per salvare le modifiche.

### Modificare in blocco i metadati di una raccolta {#edit-collection-metadata-in-bulk}

Puoi modificare i metadati di più raccolte contemporaneamente. Questa funzionalità consente di replicare rapidamente i metadati comuni in più raccolte.

1. Nella console Raccolte, seleziona due o più raccolte per le quali desideri modificare i metadati.
1. Dalla barra degli strumenti, seleziona l&#39;icona **[!UICONTROL Proprietà]**.
1. Nella pagina **[!UICONTROL Metadati raccolta]**, modifica i metadati nelle schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]**, secondo necessità.
1. Seleziona **[!UICONTROL Salva e chiudi]** dalla barra degli strumenti, quindi chiudi la finestra di dialogo di conferma per completare il processo.
1. Per aggiungere i nuovi metadati a quelli esistenti, seleziona **[!UICONTROL Modalità di aggiunta]**. Se non selezioni questa opzione, i nuovi metadati sostituiranno quelli già esistenti nei campi. Seleziona **[!UICONTROL Invia]**.

   >[!NOTE]
   >
   >La modalità di aggiunta funziona solo per i campi che possono contenere più valori. Per i campi che possono includere un solo valore, i nuovi metadati non vengono aggiunti al valore esistente del campo, anche se selezioni **[!UICONTROL Modalità di aggiunta]**.

## Ricerca {#searching}

La funzionalità di ricerca nelle raccolte supporta sia [Ricerca raccolte](#search-collections) che [Ricerca risorse in una raccolta](#search-within-collections).

### Cerca raccolte {#search-collections}

Puoi cercare le raccolte dalla console Raccolte. Quando si esegue una ricerca con parole chiave nella casella Omnisearch, [!DNL Experience Manager Assets] cerca i nomi delle raccolte, i metadati e i tag aggiunti alle raccolte.

Se cerchi raccolte dal livello superiore, nei risultati della ricerca vengono restituite solo singole raccolte. Sono escluse Assets o le cartelle all’interno delle raccolte. In tutti gli altri casi (ad esempio, all’interno di una singola raccolta o di una gerarchia di cartelle), vengono restituite tutte le risorse, le cartelle e le raccolte pertinenti.

### Cerca nelle raccolte {#search-within-collections}

Nella console Raccolte, seleziona una raccolta da aprire.

All&#39;interno di una raccolta, la ricerca di [!DNL Experience Manager] è limitata alle risorse (e ai relativi tag e metadati) all&#39;interno della raccolta che si sta visualizzando. Quando esegui una ricerca all’interno di una cartella, vengono restituite tutte le risorse e le cartelle secondarie corrispondenti nella cartella corrente. Quando esegui una ricerca all’interno di una raccolta, vengono restituite solo le risorse, le cartelle e le altre raccolte corrispondenti che sono membri diretti della raccolta.

## Modifica impostazioni raccolta {#edit-collection-settings}

È possibile modificare le impostazioni della raccolta, ad esempio titolo e descrizione, oppure aggiungere membri a una raccolta.

1. Selezionare una raccolta e l&#39;icona **[!UICONTROL Impostazioni]** nella barra degli strumenti. In alternativa, utilizza l&#39;azione rapida **[!UICONTROL Impostazioni]** dalla miniatura della raccolta.
1. Nella pagina **[!UICONTROL Impostazioni raccolta]**, puoi modificare le impostazioni della raccolta. Ad esempio, modifica il titolo della raccolta, le descrizioni, i membri e le autorizzazioni, in base a quanto descritto in [Aggiungi raccolta](#create-a-collection).
1. Seleziona **[!UICONTROL Salva]** per salvare le modifiche.

## Eliminare una raccolta {#delete-a-collection}

1. Dalla console Raccolte, seleziona una o più raccolte e fai clic sull’icona Elimina nella barra degli strumenti.
1. Nella finestra di dialogo, seleziona **[!UICONTROL Elimina]** per confermare l&#39;azione di eliminazione.

   >[!NOTE]
   >
   >Puoi anche eliminare le raccolte avanzate [elimina le ricerche salvate](#saved-searches).

## Scaricare una raccolta {#download-a-collection}

Quando si scarica una raccolta, viene scaricata l’intera gerarchia di risorse all’interno della raccolta, incluse le cartelle e le raccolte secondarie.

1. Dalla console Raccolte, seleziona una o più raccolte da scaricare.
1. Dalla barra degli strumenti, seleziona l’icona Scarica.
1. Nella finestra di dialogo **[!UICONTROL Scarica]**, seleziona **[!UICONTROL Scarica]**. Se vuoi scaricare le rappresentazioni delle risorse all&#39;interno della raccolta, seleziona **[!UICONTROL Rappresentazioni]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   Quando selezioni una raccolta da scaricare, viene scaricata l’intera gerarchia di cartelle sotto la raccolta. Per includere in una singola cartella ogni raccolta scaricata (incluse le risorse nelle raccolte secondarie nidificate nella raccolta padre), selezionare **[!UICONTROL Crea una cartella separata per ogni risorsa]**.

## Modificare le proprietà dei metadati di più raccolte {#editing-metadata-properties-of-multiple-collections}

Adobe Enterprise Manager Assets consente di modificare in blocco i metadati di molte raccolte. Utilizzare la pagina [!UICONTROL Proprietà] per eseguire modifiche ai metadati in più raccolte, ad esempio modificare le proprietà dei metadati in un valore comune oppure aggiungere o modificare tag.

Per personalizzare la pagina dei metadati [!UICONTROL Proprietà], incluse l&#39;aggiunta, la modifica e l&#39;eliminazione delle proprietà dei metadati, utilizzare l&#39;editor schema.

>[!NOTE]
>
>I metodi di modifica in blocco funzionano per le risorse disponibili in una raccolta. Per le risorse disponibili in più cartelle o che corrispondono a un criterio comune, è possibile [aggiornare in blocco i metadati dopo la ricerca](/help/assets/search-assets.md#metadata-updates).

1. Dalla console Raccolte, seleziona le raccolte da modificare.
1. Dalla barra degli strumenti, seleziona **[!UICONTROL Proprietà]** per aprire la pagina [!UICONTROL Proprietà] per le raccolte selezionate.
1. Modifica le proprietà dei metadati per le raccolte selezionate nelle varie schede.

   >[!NOTE]
   >
   >I metadati aggiunti per le raccolte selezionate sovrascrivono quelli precedenti per queste raccolte, ad eccezione dei tag. Tutti i tag aggiunti nel campo **[!UICONTROL Tag]** vengono aggiunti all&#39;elenco esistente di tag nei metadati.

1. Per visualizzare le proprietà dei metadati per una raccolta specifica, annulla la selezione delle raccolte rimanenti nell’elenco delle raccolte. I campi dell’editor di metadati vengono compilati con i metadati di una determinata raccolta.

   >[!NOTE]
   >
   >* Nella pagina delle proprietà della raccolta è possibile rimuovere le raccolte dall&#39;elenco annullando la selezione. Per impostazione predefinita, nell&#39;elenco delle raccolte sono selezionate tutte le raccolte. I metadati per le raccolte rimosse non vengono aggiornati.
   >* Nella parte superiore dell&#39;elenco, seleziona la casella di controllo accanto a **[!UICONTROL Titolo]** per scegliere tra la selezione delle raccolte e la cancellazione dell&#39;elenco.

1. Salva le modifiche.

## Creare raccolte nidificate {#create-nested-collections}

È possibile aggiungere una raccolta a un&#39;altra raccolta, creando così una raccolta nidificata.

1. Dalla console Raccolte, seleziona la raccolta o il gruppo di raccolte desiderato, quindi seleziona **[!UICONTROL Alla raccolta]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Aggiungi a raccolta]**, selezionare la raccolta in cui aggiungere la raccolta.

   >[!NOTE]
   >
   >La raccolta aggiornata più di recente è selezionata per impostazione predefinita nella pagina **[!UICONTROL Aggiungi alla raccolta]**.

1. Seleziona **[!UICONTROL Aggiungi]**. Un messaggio conferma che la raccolta viene aggiunta alla raccolta di destinazione nella pagina **[!UICONTROL Seleziona destinazione]**. Chiudi il messaggio per completare il processo.

>[!NOTE]
>
>Le raccolte avanzate non possono essere nidificate. In altre parole, le raccolte avanzate non possono contenere altri insiemi.

## Ricerche salvate {#saved-searches}

Nell’interfaccia utente Assets, puoi cercare o filtrare le risorse in base a determinate regole, criteri di ricerca o facet di ricerca personalizzata. Se salvi queste ricerche come **[!UICONTROL Ricerche salvate]**, puoi accedervi in un secondo momento dall’elenco **[!UICONTROL Ricerche salvate]** nel pannello Filtro. La creazione di una ricerca salvata genera anche una raccolta avanzata.

Le ricerche salvate vengono create quando generi una raccolta avanzata. Le raccolte avanzate vengono aggiunte automaticamente all’elenco **[!UICONTROL Ricerche salvate]**. La query delle Ricerche salvate per la raccolta viene salvata nella proprietà `dam:query` in CRXDE nella posizione relativa `/content/dam/collections/`. Non esistono limiti alle ricerche che è possibile salvare e alle ricerche salvate visualizzate nell&#39;elenco.

>[!NOTE]
>
>Puoi condividere le raccolte avanzate nello stesso modo in cui condividi le raccolte statiche.

La modifica delle ricerche salvate equivale alla modifica delle raccolte avanzate. Per ulteriori dettagli, vedere [Modificare una raccolta avanzata](#edit-a-smart-collection).

Per eliminare le ricerche salvate, eseguire la procedura seguente:

1. Nell’interfaccia utente di Assets, seleziona l’icona di ricerca nella barra degli strumenti.

1. Con il cursore nel campo Omnisearch, seleziona il tasto `Enter`.
1. Seleziona l’icona GlobalNav per visualizzare il pannello Filtri.
1. Dall&#39;elenco **[!UICONTROL Ricerche salvate]**, seleziona **[!UICONTROL Elimina]** accanto alla raccolta avanzata da eliminare.
1. Nella finestra di dialogo, seleziona **[!UICONTROL Elimina]** per eliminare la ricerca salvata.

## Eseguire un flusso di lavoro su una raccolta {#run-a-workflow-on-a-collection}

Puoi eseguire un flusso di lavoro per le risorse all’interno di una raccolta. Se la raccolta contiene raccolte nidificate, il flusso di lavoro viene eseguito anche sulle risorse all’interno delle raccolte nidificate. Tuttavia, se la raccolta e la raccolta nidificata contengono risorse duplicate, il flusso di lavoro viene eseguito una sola volta per tali risorse.

1. Dalla console Raccolte, seleziona una raccolta in cui desideri eseguire un flusso di lavoro.
1. Seleziona l&#39;icona GlobalNav e scegli **[!UICONTROL Timeline]** dall&#39;elenco.
1. Dalla timeline, seleziona l&#39;icona del cursore verso il basso, quindi seleziona **[!UICONTROL Avvia flusso di lavoro]**.
1. Nella sezione **[!UICONTROL Avvia flusso di lavoro]**, seleziona un modello di flusso di lavoro dall’elenco. Ad esempio, scegli il modello **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Immettere un titolo per il flusso di lavoro e selezionare **[!UICONTROL Inizio]**.
1. Nella finestra di dialogo, seleziona **[!UICONTROL Procedi]**. Il flusso di lavoro viene eseguito su tutte le risorse della raccolta.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Crea un&#39;attività di revisione per le raccolte](/help/assets/bulk-approval.md)
