---
title: Creazione e gestione delle offerte (console Offerte)
description: Usa la console Offerte per creare offerte da utilizzare nelle esperienze Attività.
exl-id: 81d2fda2-06a9-48f6-820a-dd9e11d94fcc
source-git-commit: c27870c39da80d664f208d658994eec83a19589f
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 100%

---

# Creazione e gestione delle offerte (console Offerte) {#creating-and-managing-offers}

La console **Offerte** in futuro diventerà obsoleta. Da ora in poi:

* sarà disponibile solo per i clienti che dispongono di offerte *legacy* già definite (ovvero preesistenti);
* si consiglia di convertire tali offerte legacy in offerte basate su frammenti di esperienza;
   * non appena l’ultima offerta legacy sarà stata convertita o rimossa, la console **Offerte** non sarà più disponibile.

![Console di personalizzazione](/help/sites-cloud/authoring/assets/offers-consoles.png)

>[!NOTE]
>
>I clienti che dispongono di offerte legacy possono ancora utilizzare la console **Offerte** per visualizzare offerte legacy esistenti e crearne di nuove.
>
>I clienti che non dispongono di offerte legacy precedenti non visualizzeranno la console **Offerte**.
>
>Tutti i clienti possono utilizzare **Offerte con frammenti di esperienza** per creare e gestire le offerte.

## Conversione di un’offerta legacy in un frammento di esperienza {#convert-legacy-offer-to-experience-fragment}

L’opzione e flusso di lavoro **Converti in variante di frammento di esperienza** è stata implementata per aiutarti a convertire le offerte legacy in frammenti di esperienza:

>[!NOTE]
>
>Si tratta del flusso di lavoro consigliato per convertire le offerte legacy in frammenti di esperienza.

>[!NOTE]
>
>Puoi anche creare un nuovo frammento di esperienza, trasferire manualmente il contenuto dall’offerta legacy al frammento, quindi eliminare l’offerta legacy.

>[!CAUTION]
>
>L’opzione **Converti in variantei il frammento di esperienza** è disponibile per tutti i componenti core.
>
>Questa opzione non sarà supportata per i componenti personalizzati. Per tali componenti, devi convertire manualmente il contenuto in un frammento di esperienza.

>[!CAUTION]
>
>Non appena l’ultima offerta legacy sarà stata convertita o rimossa:
>
>* La console **Offerte** non sarà più disponibile.
>* L’icona Target nella barra degli strumenti di qualsiasi altro componente interessato non verrà più visualizzata.


1. Apri una pagina contenente l’offerta da modificare.

1. Passa alla modalità **Targeting** per tale pagina.

1. Fai clic su **Inizia impostazione destinazione**.

1. Seleziona il componente appropriato (di destinazione).

1. La barra degli strumenti del componente fornisce un’opzione per **convertire in variante di frammento di esperienza**:

   ![Conversione di offerte legacy in frammenti di esperienza](/help/sites-cloud/authoring/assets/offers-convert-legacy-icon.png)

1. Viene visualizzata una finestra di dialogo. Qui puoi selezionare l’**Azione** richiesta:

   * Crea un nuovo frammento esperienza
   * Aggiungi il contenuto a un frammento di esperienza esistente

   Per questo scenario, seleziona **Crea un nuovo frammento di esperienza**.

   ![Finestra di dialogo Converti in variante di frammento di esperienza](/help/sites-cloud/authoring/assets/offers-convert-dialog.png)

1. Compila i campi richiesti nella finestra di dialogo:

   * **Percorso principale**
Specifica il percorso principale del nuovo frammento di esperienza.
   * **Modello**
Seleziona il modello da utilizzare per creare il frammento di esperienza.
   * **Titolo frammento**
Specifica il titolo.
   * **Tag frammento**
Se necessario, aggiungi dei tag.

1. Conferma con **Fine**.

   Se ora passi alla console **Offerte con frammenti di esperienza**, il nuovo frammento di esperienza verrà visualizzato insieme alle relative varianti.

### Targeting con il modello di offerte {#targeting-offers-template}

>[!CAUTION]
>
>Questa opzione è disponibile solo per i clienti che dispongono di offerte legacy precedenti.
>
>Come per la console **Offerte**, non sarà più disponibile nelle seguenti situazioni:
>
>* una volta convertita l’ultima offerta legacy in frammenti di esperienza;
>* quando le offerte legacy saranno diventate obsolete (in futuro).
>
>Pertanto, si consiglia di utilizzare l’opzione Frammenti di esperienza, non questa opzione.

Per i clienti che dispongono di offerte legacy preesistenti, le opzioni **Usa modello di offerta** saranno visibili quando si esegue il targeting di componenti che **non** sono frammenti di esperienza:

![Finestra di dialogo Converti in variante di frammento di esperienza](/help/sites-cloud/authoring/assets/offers-legacy-target-non-experience-fragment.png)

## Console Offerte {#offers-console}

>[!CAUTION]
>
>Questa console diventerà obsoleta in futuro, in quanto offre un modo legacy di personalizzare i contenuti.
>
>Hai ancora un po’ di tempo per prepararti. Scopri come [convertire le offerte legacy esistenti in offerte basate su frammenti di esperienza](#convert-legacy-offer-to-experience-fragment).

Usa la console Offerte per creare offerte da [utilizzare in più esperienze](/help/sites-cloud/authoring/personalization/targeted-content.md). La creazione di offerte nella console Offerte consente di risparmiare tempo nel caso in cui più esperienze richiedano la stessa offerta:

* Crea l’offerta una volta nella libreria e usala in più esperienze per le attività del tuo marchio.
* Se modifichi l’offerta nella libreria, la modifica viene applicata a tutte le esperienze che la utilizzano.

Nella console Offerte, le offerte sono organizzate per marchio. Ogni marchio contiene una libreria di offerte che possono essere utilizzate nelle diverse esperienze del marchio. Utilizza le cartelle per definire una struttura gerarchica e organizzare le offerte in ogni libreria. Una struttura logica delle cartelle consente agli autori di trovare facilmente le offerte navigando nella libreria. Anche gli strumenti di tagging e ricerca consentono agli autori di trovare le offerte.

### Aggiungi un marchio utilizzando la console Offerte {#add-a-brand-using-the-offers-console}

Crea un marchio a cui le offerte vengono associate. Apri un marchio nella console Offerte per accedere alla libreria delle offerte, dove puoi creare cartelle e offerte.

Quando crei un marchio utilizzando la console Offerte, questo viene visualizzato anche nella [console Attività](/help/sites-cloud/authoring/personalization/activities.md), dove puoi aggiungere e amministrare le attività per il marchio.

1. Fai clic o tocca **Personalizzazione** > **Offerte** nella console di navigazione.

   ![Navigazione alla console Offerte](/help/sites-cloud/authoring/assets/offers-navigation.png)

1. Tocca o fai clic su **Crea** e quindi su **Crea** **marchio**.
1. Seleziona il modello di marchio e tocca o fai clic su **Avanti**.
1. Digita un titolo per il marchio come desideri che appaia nelle console Offerte e Attività. Facoltativamente, digita o seleziona uno o più tag da associare al marchio.
1. Tocca o fai clic su **Crea**.

### Aggiunta di una cartella a una libreria di offerte {#add-a-folder-to-an-offer-library}

Consente di aggiungere una cartella alla libreria di offerte di un marchio per organizzare e salvare le offerte. Puoi creare una sottocartella sotto il marchio o altre cartelle.

1. Nella console Offerte, apri la posizione in cui desideri creare la cartella. Ad esempio, apri il marchio per creare una cartella di livello superiore o apri un&#39;altra cartella nella libreria.
1. Tocca o fai clic su **Crea** > **Crea cartella o offerta**.

   ![Creazione di una cartella di offerta](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Seleziona **Cartella** e fai clic su **Avanti**.
1. Digita un titolo per la cartella come desideri che appaia nella libreria dell&#39;offerta e digita o seleziona i tag.

   ![Definizione delle proprietà della cartella](/help/sites-cloud/authoring/assets/offers-folder-properties.png)

1. Tocca o fai clic su **Crea**.

### Aggiunta di un&#39;offerta a una libreria di offerte {#add-an-offer-to-an-offer-library}

Consente di aggiungere un&#39;offerta alla libreria delle offerte di un marchio in modo che possa essere aggiunta alle esperienze del marchio. Quando aggiungi un&#39;offerta devi inserire un titolo. Puoi anche associare l&#39;offerta con uno o più tag per migliorare la ricerca.

Dopo aver creato l&#39;offerta puoi aprirla per creare il contenuto.

1. Nella console Offerte, apri la posizione in cui desideri creare l&#39;offerta. Ad esempio, apri il marchio per creare un&#39;offerta di livello superiore o apri una cartella nella libreria.
1. Tocca o fai clic su **Crea** > **Crea cartella o offerta**.

   ![Creazione di una cartella di offerta](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Seleziona il modello **Pagina offerte** e tocca o fai clic su **Avanti**.
1. Digita un titolo per l&#39;offerta e, facoltativamente, seleziona o digita uno o più tag da associare all&#39;offerta, quindi tocca o fai clic su **Crea**.
1. Nella finestra di dialogo di conferma, per aprire l&#39;offerta di modifica tocca o fai clic su **Apri pagina**.

### Modifica di un&#39;offerta {#editing-an-offer}

Apri un&#39;offerta e modifica il contenuto come vuoi che appaia nelle esperienze che lo utilizzano. Quando modifichi un&#39;offerta che viene utilizzata in qualsiasi esperienza, le modifiche vengono visualizzate nelle esperienze.

Puoi aprire un&#39;offerta da una cartella in una libreria di offerte o dai risultati della ricerca. Puoi anche aprire un&#39;offerta da un&#39;esperienza che utilizza l&#39;offerta.

1. Nella console Offerte, tocca o fai clic sull&#39;icona accanto all&#39;offerta e tocca o fai clic su **Modifica**.
1. Aggiungi componenti all&#39;offerta e modifica il contenuto dei componenti come d&#39;abitudine.

### Eliminazione di un&#39;offerta {#deleting-an-offer}

Consente di eliminare un&#39;offerta quando non è più necessaria. Quando tenti di eliminare un&#39;offerta utilizzata in un&#39;esperienza, ti viene richiesto di confermare l&#39;eliminazione. Con la conferma viene eliminata l&#39;offerta e la rimuove dalle esperienze.

Puoi eliminare un&#39;offerta visualizzando il contenuto di una cartella in una libreria di offerte o i risultati della ricerca.

1. Nella console Offerte, tocca o fai clic sull&#39;icona accanto all&#39;offerta e tocca o fai clic su **Elimina**.

   Seleziona l&#39;offerta e tocca o fai clic su **Elimina**.

1. Nella finestra di dialogo visualizzata, tocca o fai clic su **Elimina** per confermare l&#39;eliminazione.
1. Se l&#39;offerta è usata in una o più esperienze, viene visualizzata una finestra di dialogo che indica che l&#39;offerta è referenziata:

   * Per eliminare l&#39;offerta e rimuoverla dalle esperienze, tocca o fai clic su **Forza eliminazione**.
   * Per mantenere l&#39;offerta, tocca o fai clic su **Annulla**.

### Ricerca delle offerte {#searching-for-offers}

Consente di cercare offerte di qualsiasi marchio utilizzando parole chiave per abbinare il titolo.

![Ricerca di un’offerta](/help/sites-cloud/authoring/assets/offers-search.png)

I criteri di ricerca attuali vengono visualizzati accanto ai risultati di ricerca. Puoi anche ordinare i risultati per colonna in ordine crescente o decrescente. Puoi eseguire una ricerca in qualsiasi cartella di qualsiasi libreria di offerte. I risultati della ricerca sono gli stessi, indipendentemente dalla cartella corrente.

Per cercare le offerte:

1. Nella parte superiore della console Offerte, tocca o fai clic sull&#39;icona della lente d&#39;ingrandimento. Per impostazione predefinita, la ricerca è limitata alle offerte.
1. Immetti la parola chiave per cercare le offerte. Seleziona un elemento dai risultati di ricerca.
