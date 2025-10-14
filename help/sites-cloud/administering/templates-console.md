---
title: Console Modelli
description: Scopri come la console dei modelli funge da posizione centrale per visualizzare e gestire i modelli di pagina.
solution: Experience Manager Sites
feature: Administering
role: User
exl-id: d11d7176-dd35-4855-9dcd-dd40ff096510
source-git-commit: 3238b11cdd891cf18048199d4103397e3af75edf
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 2%

---

# Console Modelli {#templates-console}

Scopri come la console dei modelli funge da posizione centrale per visualizzare e gestire i modelli di pagina.

## Panoramica {#overview}

Durante la creazione di una pagina, devi selezionare un modello. Il modello di pagina viene utilizzato come base per la nuova pagina. [I modelli modificabili di AEM](/help/implementing/developing/components/templates.md) possono definire la struttura della pagina risultante, qualsiasi contenuto iniziale e i componenti che possono essere utilizzati (proprietà di progettazione).

Agli autori di contenuti viene presentata una selezione di modelli disponibili quando [creano nuove pagine nella console Sites](/help/sites-cloud/authoring/sites-console/creating-pages.md). I modelli possono essere utilizzati per creare pagine modificabili con:

* [Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md) o
* [L’editor universale](/help/sites-cloud/authoring/universal-editor/templates.md)

La console Modelli consente a un amministratore di visualizzare e gestire tutti i modelli di pagina da una posizione centrale.

## Accesso alla console Modelli {#accessing}

1. Accedi ad AEM as a Cloud Service.
1. Apri la navigazione globale e seleziona il pannello **Strumenti**, quindi **Generale** -> **Modelli**.

## Orientamento {#orientation}

La console Modelli è organizzata in cartelle con una cartella per [configurazione](/help/implementing/developing/introduction/configurations.md) in cui sono stati attivati modelli modificabili per la configurazione.

![Console Modelli](assets/templates-console/templates-console.png)

[La vista predefinita](/help/sites-cloud/authoring/quick-start.md) della console è la vista delle schede. Tocca o fai clic su una cartella per esplorarne il contenuto.

![Contenuto della cartella dei modelli nella console dei modelli](assets/templates-console/templates-console-templates.png)

Seleziona un modello per visualizzare le opzioni disponibili nella barra degli strumenti.

![Barra degli strumenti della console Modelli](assets/templates-console/templates-console-toolbar.png)

* [Modifica](#edit-edit)
* [Proprietà](#properties)
* [Disattiva/Abilita](#enable-disable)
* [Pubblicazione](#publish)
* [Copia](#copy)
* [Eliminare](#delete)

## Modifica {#edit}

La modifica di un modello apre l’editor utilizzato per creare il modello. Effettua una delle seguenti operazioni:

* [Editor modelli](/help/sites-cloud/authoring/page-editor/templates.md)
* [L’editor universale](/help/sites-cloud/authoring/universal-editor/templates.md)

Utilizzando l’editor appropriato, puoi apportare le modifiche necessarie al modello. La modifica di un modello in uso può avere effetti sugli autori.

* Per i modelli creati con l’Editor modelli, le modifiche apportate possono interessare le pagine live basate sul modello selezionato.
* Per i modelli creati con l’Editor universale, le modifiche apportate interessano solo le nuove pagine create dagli autori in base al modello selezionato.

Se un autore inizia a creare un modello con l’editor di modelli già abilitato, viene visualizzato un avviso.

>[!TIP]
>
>Dopo aver selezionato un modello nella console, utilizzare il tasto di scelta rapida `e` per modificare il modello selezionato.

## Proprietà {#properties}

È possibile modificare [le proprietà del modello](/help/sites-cloud/authoring/page-editor/templates.md) in modo analogo a [modificare le proprietà della pagina.Le proprietà del modello &#x200B;](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) includono:

* Titolo modello
* Descrizione
* Immagine

>[!TIP]
>
>Dopo aver selezionato un modello nella console, utilizzare il tasto di scelta rapida `p` per aprire le proprietà del modello selezionato.

## Abilitazione e disabilitazione {#enable-disable}

Un modello può avere uno dei tre stati seguenti:

* **Bozza** - Il modello è ancora in fase di creazione e non è disponibile per la creazione di nuove pagine.
* **Abilitato** - Il modello è completo e disponibile per la creazione di nuove pagine.
* **Disabilitato** - Il modello è completo ma non è disponibile per la creazione di nuove pagine.

Quando viene creato un modello, per impostazione predefinita si trova nello stato **Bozza** (per i modelli creati con [Editor modelli](/help/sites-cloud/authoring/page-editor/templates.md)) o **Abilitato** (per i modelli creati con [Editor universale](/help/sites-cloud/authoring/universal-editor/templates.md)).

Un modello deve essere abilitato prima di poter essere utilizzato dagli autori di contenuto per creare pagine. Se un modello non è più necessario, può essere disabilitato in modo che non venga più visualizzato nella procedura guidata di creazione della pagina.

* Selezionare il modello e fare clic su **Disattiva** per disabilitare il modello.
* Selezionare il modello e fare clic su **Abilita** per abilitarlo.

## Pubblicazione {#publish}

Un modello creato con l’editor di modelli può essere utilizzato solo dopo che è stato pubblicato. Seleziona il modello e fai clic su **Pubblica** per pubblicarlo.

Per poter essere utilizzati, i modelli creati con l’Editor universale non devono essere pubblicati.

## Copia in corso {#copy}

Se la struttura di alcune pagine è simile, è possibile utilizzare il pulsante **Copia** per creare l&#39;ambito di un modello e quindi modificare la copia in base alle proprie esigenze. Questa funzione è utile anche se si desidera utilizzare un modello in un altro sito.

1. Seleziona il modello e tocca o fai clic su **Copia** per creare una copia.
1. Passa alla posizione in cui desideri creare la copia.
1. Tocca o fai clic su **Incolla** nella barra degli strumenti.

Una volta incollato, puoi:

* [Modifica il modello](#edit) per modificarlo in base alle esigenze.
* [Utilizzare la finestra delle proprietà](#properties) per aggiornare il titolo del modello.
* [Abilitare il modello](#enable-disable) in modo che possa essere utilizzato per creare la pagina.
* [Pubblica il modello](#publish) se necessario.

>[!TIP]
>
>Dopo aver selezionato un modello nella console, utilizzare il tasto di scelta rapida `Command+c` o `ctrl+c` per copiare il modello selezionato.

## Eliminazione {#delete}

Se un modello non è più necessario, può essere eliminato purché non sia referenziato da alcuna pagina.

Seleziona il modello e tocca o fai clic su **Elimina** per eliminarlo.

>[!TIP]
>
>Dopo aver selezionato un modello nella console, utilizzare la scelta rapida `Backspace` per eliminare il modello selezionato.

## Creazione di modelli {#create}

Utilizza il pulsante **Crea** nella console per creare un nuovo modello nel percorso corrente. Per informazioni dettagliate sulla creazione di un modello, vedere il documento [Modelli per creare pagine modificabili con Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md).

Il pulsante **Crea** viene utilizzato solo per creare modelli modificabili con l&#39;Editor pagina. Per informazioni sulla creazione di modelli basati su pagine create con Universal Editor, vedere il documento [Modelli per creare pagine modificabili con Universal Editor](/help/sites-cloud/authoring/universal-editor/templates.md).
