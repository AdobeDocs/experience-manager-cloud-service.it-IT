---
title: Creazione e gestione delle offerte (console Offerte)
description: Usa la console Offerte per creare offerte da utilizzare nelle esperienze Attività.
exl-id: 81d2fda2-06a9-48f6-820a-dd9e11d94fcc
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 96%

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
>Puoi anche creare un frammento di esperienza, trasferire manualmente il contenuto dall’offerta legacy al frammento, quindi eliminare l’offerta legacy.

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

   Se ora passi a **Offerte con frammenti di esperienza** nella console, puoi visualizzare il nuovo frammento di esperienza e le relative varianti.

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

Per i clienti che dispongono di offerte legacy preesistenti, le opzioni **Usa modello di offerta** sono visibili quando si esegue il targeting di componenti che **non** sono frammenti di esperienza:

![Finestra di dialogo Converti in variante di frammento di esperienza](/help/sites-cloud/authoring/assets/offers-legacy-target-non-experience-fragment.png)

## Console Offerte {#offers-console}

>[!CAUTION]
>
>Questa console diventerà obsoleta in futuro, in quanto offre un modo legacy di personalizzare i contenuti.
>
>Hai ancora un po’ di tempo per prepararti. Scopri come [convertire le offerte legacy esistenti in offerte basate su frammenti di esperienza](#convert-legacy-offer-to-experience-fragment).

Usa la console Offerte per creare offerte da [utilizzare in più esperienze](/help/sites-cloud/authoring/personalization/targeted-content.md). La creazione di offerte nella console Offerte consente di risparmiare tempo quando più esperienze richiedono la stessa offerta:

* Crea l’offerta una volta nella libreria e usala in più esperienze per le attività del tuo marchio.
* Modifica l’offerta nella libreria e la modifica interesserà tutte le esperienze che la utilizzano.

Nella console Offerte, le offerte sono organizzate per marchio. Ogni marchio contiene una libreria di offerte che possono essere utilizzate nelle diverse esperienze del marchio. Utilizza le cartelle per definire una struttura gerarchica e organizzare le offerte in ogni libreria. Una struttura logica delle cartelle consente agli autori di trovare facilmente le offerte navigando nella libreria. Gli strumenti di assegnazione tag e ricerca consentono inoltre agli autori di trovare le offerte.

### Aggiunta di un marchio utilizzando la console Offerte {#add-a-brand-using-the-offers-console}

Crea un marchio a cui sono associate le offerte. Apri un marchio nella console Offerte per accedere alla libreria delle offerte, dove puoi creare cartelle e offerte.

Quando crei un marchio utilizzando la console Offerte, questo viene visualizzato anche nella [Console Attività](/help/sites-cloud/authoring/personalization/activities.md) dove puoi aggiungere e amministrare attività per il marchio.

1. Fai clic o tocca **Personalizzazione** > **Offerte** nella console di navigazione.

   ![Navigazione alla console Offerte](/help/sites-cloud/authoring/assets/offers-navigation.png)

1. Tocca o fai clic su **Crea** e quindi su **Crea** **marchio**.
1. Seleziona il modello di marchio e tocca o fai clic su **Avanti**.
1. Digita un titolo per il marchio in base a come desideri che appaia nelle console Offerte e Attività. Facoltativamente, digita o seleziona uno o più tag da associare al marchio.
1. Tocca o fai clic su **Crea**.

### Aggiunta di una cartella a una libreria di offerte {#add-a-folder-to-an-offer-library}

Aggiungi una cartella alla libreria di offerte di un marchio per organizzare e archiviare le offerte. Puoi creare una cartella sotto il marchio o sotto altre cartelle.

1. Nella console Offerte, apri il percorso in cui desideri creare la cartella. Ad esempio, apri il marchio per creare una cartella di livello superiore o apri un’altra cartella nella libreria.
1. Tocca o fai clic su **Crea** > **Crea cartella o offerta**.

   ![Creazione di una cartella di offerta](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Seleziona **Cartella** e fai clic su **Avanti**.
1. Digita un titolo per la cartella come desideri che appaia nella libreria dell&#39;offerta e digita o seleziona i tag.

   ![Definizione delle proprietà della cartella](/help/sites-cloud/authoring/assets/offers-folder-properties.png)

1. Tocca o fai clic su **Crea**.

### Aggiungere un’offerta a una libreria di offerte {#add-an-offer-to-an-offer-library}

Aggiungi un’offerta alla libreria di offerte di un marchio in modo che possa essere aggiunta alle esperienze del marchio. Quando aggiungi un’offerta, fornisci un titolo. Puoi anche associare l’offerta a uno o più tag per migliorare la ricerca.

Dopo aver creato l’offerta, puoi aprirla per eseguire l’authoring del contenuto.

1. Nella console Offerte, apri la posizione in cui desideri creare l’offerta. Ad esempio, apri il marchio per creare un’offerta di livello superiore o apri una cartella nella libreria.
1. Tocca o fai clic su **Crea** > **Crea cartella o offerta**.

   ![Creazione di una cartella di offerta](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Seleziona il modello **Pagina offerte** e tocca o fai clic su **Avanti**.
1. Digita un titolo per l’offerta e facoltativamente seleziona o digita uno o più tag da associare all’offerta, quindi tocca o fai clic su **Crea**.
1. Nella finestra di dialogo di conferma, per aprire l&#39;offerta di modifica tocca o fai clic su **Apri pagina**.

### Modifica di un’offerta {#editing-an-offer}

Apri un’offerta e modifica il contenuto in base a come desideri che appaia nelle esperienze che la utilizzano. Quando modifichi un’offerta utilizzata in una qualsiasi esperienza, le modifiche vengono visualizzate nelle esperienze.

Puoi aprire un’offerta da una cartella in una libreria di offerte o dai risultati della ricerca. Puoi anche aprire un’offerta da un’esperienza che utilizza l’offerta.

1. Nella console Offerte, tocca o fai clic sull’icona accanto all’offerta e tocca o fai clic su **Modifica**.
1. Aggiungi componenti all’offerta e modifica normalmente il contenuto dei componenti.

### Eliminazione di un’offerta {#deleting-an-offer}

Elimina un’offerta quando non è più necessaria. Quando tenti di eliminare un’offerta utilizzata in un’esperienza, ti viene richiesto di confermare l’eliminazione. La conferma comporta l’eliminazione dell’offerta e la sua rimozione dalle esperienze.

Puoi eliminare un’offerta quando visualizzi il contenuto di una cartella in una libreria di offerte o nei risultati della ricerca.

1. Nella console Offerte, tocca o fai clic sull’icona accanto all’offerta e tocca o fai clic su **Elimina**.

   Seleziona l’offerta e tocca o fai clic su **Elimina**.

1. Nella finestra di dialogo visualizzata, tocca o fai clic su **Elimina** per confermare l’eliminazione.
1. Se l’offerta viene utilizzata in una o più esperienze, viene visualizzata una finestra di dialogo per indicare che si fa riferimento all’offerta:

   * Per eliminare l’offerta e rimuoverla dalle esperienze, tocca o fai clic su **Forza eliminazione**.
   * Per mantenere l’offerta, tocca o fai clic su **Annulla**.

### Ricerca di offerte {#searching-for-offers}

Cerca le offerte di qualsiasi marchio utilizzando parole chiave che corrispondano al titolo.

![Ricerca di un’offerta](/help/sites-cloud/authoring/assets/offers-search.png)

I criteri di ricerca correnti vengono visualizzati accanto ai risultati della ricerca. Puoi anche ordinare i risultati per colonna in ordine crescente o decrescente. Puoi eseguire una ricerca in qualsiasi cartella di qualsiasi libreria di offerte. I risultati della ricerca sono gli stessi, indipendentemente dalla cartella corrente.

Per cercare le offerte:

1. Nella parte superiore della console Offerte, tocca o fai clic sull&#39;icona della lente d&#39;ingrandimento. Per impostazione predefinita, la ricerca è limitata alle offerte.
1. Immetti la parola chiave per cercare le offerte. Seleziona un elemento dai risultati di ricerca.
