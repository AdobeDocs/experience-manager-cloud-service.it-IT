---
title: Authoring dei contenuti con l’editor universale
description: Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 3922375b52ae64d08cdc64d475a95e8bd240a587
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 26%

---


# Authoring dei contenuti con l’editor universale {#authoring}

Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.

## Introduzione {#introduction}

L’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione in modo da offrire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.

A questo scopo, l’editor universale offre agli autori di contenuti un’interfaccia utente intuitiva che richiede una formazione minima per poter entrare e iniziare a modificare i contenuti. Questo documento descrive l’esperienza di authoring dell’editor universale.

>[!NOTE]
>
>In questo documento si presuppone che tu abbia già familiarità con le modalità di accesso e navigazione all’Editor universale. In caso contrario, vedere il documento [Accesso e navigazione nell&#39;editor universale.](/help/sites-cloud/authoring/universal-editor/navigation.md)

>[!TIP]
>
>Per un’introduzione più dettagliata all’editor universale, consulta il documento [Introduzione all’editor universale.](/help/implementing/universal-editor/introduction.md)

## Modifica del contenuto {#editing-content}

La modifica del contenuto è semplice e intuitiva. Quando passi il mouse sul contenuto nell’editor, il contenuto modificabile viene evidenziato con una casella blu.

![Il contenuto modificabile viene evidenziato da una casella blu](assets/editable-content.png)

>[!TIP]
>
>Per impostazione predefinita, tocca o fai clic sul contenuto per selezionarlo per la modifica. Se desideri esplorare il contenuto tramite i seguenti collegamenti, passa alla modalità di anteprima [.](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)

A seconda del contenuto selezionato, è possibile che siano disponibili diverse opzioni di modifica diretta e che siano disponibili ulteriori informazioni e opzioni per il contenuto nella barra delle proprietà di [.](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)

### Modifica del testo normale {#edit-plain-text}

Per modificare il testo nella posizione desiderata, fai doppio clic o tocca due volte il componente.

![Modifica del contenuto](assets/editing-content.png)

Per salvare le modifiche, premere Invio/Ritorna o selezionare all&#39;esterno della casella.

Quando selezioni il componente testo, i relativi dettagli vengono visualizzati nella barra delle proprietà [.](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail) È inoltre possibile modificare il testo nella barra.

![Modifica del testo nella barra delle proprietà](assets/ue-editing-text-component-rail.png)

Inoltre, i dettagli sul testo sono disponibili nella barra delle proprietà. Le modifiche vengono salvate automaticamente una volta che lo stato attivo lascia il campo modificato nella barra delle proprietà.

### Modifica del testo formattato {#edit-rich-text}

Per modificare il testo nella posizione desiderata, fai doppio clic o tocca due volte il componente.

![Modifica di un componente formato RTF](assets/rich-text-editing.png)

Per comodità, le opzioni di formattazione e i dettagli del testo sono disponibili in due posizioni.

* Il **menu di scelta rapida** si apre sopra il blocco di testo RTF e offre opzioni di formattazione di base nel contesto. A causa di limiti di spazio, alcune opzioni potrebbero essere nascoste dietro il pulsante con i puntini di sospensione.
* La barra delle proprietà **[](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)** mostra tutte le opzioni di formattazione disponibili insieme al testo.

Le modifiche vengono salvate automaticamente quando lo stato attivo lascia il campo modificato.

### Editing di file multimediali {#edit-media}

Puoi visualizzarne i dettagli nella barra delle proprietà [.](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)

![Modifica dei file multimediali](assets/ue-edit-media.png)

1. Tocca o fai clic sull’anteprima dell’immagine selezionata nella barra delle proprietà.
1. Viene visualizzata la finestra [selettore risorse](/help/assets/asset-selector.md#using-asset-selector) che consente di selezionare una risorsa.
1. Seleziona per selezionare una nuova risorsa.
1. Seleziona **Seleziona** per tornare alla barra delle proprietà in cui è stata sostituita la risorsa.

Le modifiche vengono salvate automaticamente nel contenuto.

### Modifica di frammenti di contenuto {#edit-content-fragment}

Se selezioni un [frammento di contenuto,](/help/sites-cloud/administering/content-fragments/overview.md) puoi modificarne i dettagli nella barra delle [proprietà.](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)

![Modifica di un frammento di contenuto](assets/ue-edit-cf.png)

I campi definiti nel modello di contenuto del frammento di contenuto selezionato vengono visualizzati e modificabili nella barra delle proprietà.

Se selezioni un campo correlato a un frammento di contenuto, il frammento di contenuto viene caricato nella barra dei componenti e il campo viene scorruto automaticamente in.

Le modifiche vengono salvate automaticamente una volta che lo stato attivo lascia il campo modificato nella barra delle proprietà.

Se invece desideri modificare il frammento di contenuto nell&#39;[Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md), fai clic sul [pulsante di modifica](/help/sites-cloud/authoring/universal-editor/navigation.md#edit) nella barra delle proprietà.

A seconda delle esigenze del flusso di lavoro, può essere utile modificare il frammento di contenuto nell’editor universale o direttamente nell’editor frammento di contenuto.

### Aggiunta di componenti ai contenitori {#adding-components}

1. Selezionare un componente contenitore nella [struttura contenuto](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) o nell&#39;editor.
1. Quindi seleziona l’icona Aggiungi nella barra delle proprietà.

   ![Selezione di un componente da aggiungere a un contenitore](assets/ue-add-component.png)

Il componente viene inserito nel contenitore e può essere modificato nell’editor.

>[!TIP]
>
>Utilizzare il tasto di scelta rapida `A` per aggiungere un componente al contenitore selezionato.

### Eliminazione di componenti dai contenitori {#deleting-components}

1. Selezionare un componente contenitore nella [struttura contenuto](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) o nell&#39;editor.
1. Seleziona l’icona della freccia del contenitore per espanderne il contenuto nella struttura del contenuto.
1. Quindi, nella struttura del contenuto, seleziona un componente all’interno del contenitore.
1. Seleziona l’icona Elimina nella barra delle proprietà.

   ![Eliminazione di un componente](assets/ue-delete-component.png)

Il componente selezionato è stato eliminato.

>[!TIP]
>
>Utilizzare il tasto di scelta rapida `Shift+Backspace` per eliminare il componente selezionato dal relativo contenitore.

### Riordinamento dei componenti nei contenitori {#reordering-components}

1. Se non è già in modalità [struttura contenuto,](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) passa alla struttura.
1. Seleziona un componente contenitore nella struttura del contenuto o nell’editor.
1. Seleziona l’icona della freccia del contenitore per espanderne il contenuto nella struttura del contenuto.
1. Trascina le icone delle maniglie accanto ai componenti all’interno del contenitore per mostrare che puoi riorganizzarli. Trascina i componenti per riordinarli all’interno del contenitore.

   ![Riordinamento dei componenti](assets/ue-reordering-components.png)

1. Il componente trascinato diventa grigio nella struttura del contenuto, mentre il punto di inserimento è rappresentato da una linea blu. Rilasciate il componente per posizionarlo nella nuova posizione.

I componenti vengono riordinati sia nella struttura del contenuto che nell’editor

## Anteprima del contenuto {#previewing-content}

Quando hai finito di modificare il contenuto, spesso desideri navigare in esso per vedere come si presenta nel contenuto di altre pagine. In [modalità anteprima](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode) puoi fare clic sui collegamenti per navigare nel contenuto come farebbe un lettore. Il contenuto viene riprodotto nell’editor così come verrebbe pubblicato.

In modalità anteprima, toccando o facendo clic sul contenuto si reagisce come se si trattasse di un normale lettore. Se si desidera selezionare il contenuto da modificare, uscire dalla modalità di anteprima [.](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)

## Risorse aggiuntive {#additional-resources}

Per informazioni su come pubblicare contenuti con l’editor universale, consulta questo documento.

* [Pubblicazione di contenuti con l&#39;editor universale](publishing.md) - Scopri come l&#39;editor universale pubblica i contenuti e come le app possono gestire i contenuti pubblicati.

Per ulteriori informazioni sui dettagli tecnici di Universal Editor, consulta questi documenti per gli sviluppatori.

* [Introduzione all’editor universale](/help/implementing/universal-editor/introduction.md): scopri come l’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Guida introduttiva all’editor universale in AEM](/help/implementing/universal-editor/getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](/help/implementing/universal-editor/architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](/help/implementing/universal-editor/attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](/help/implementing/universal-editor/authentication.md): scopri come l’editor universale effettua l’autenticazione.

## Modifica dell’ereditarietà dei componenti {#inheritance}

L’ereditarietà è il meccanismo in cui il contenuto può essere collegato in modo che la modifica di un elemento cambia automaticamente l’altro.

Utilizzando l’Editor universale, puoi annullare l’ereditarietà dei contenuti semplicemente aggiornandone il contenuto. L’editor disabilita automaticamente l’ereditarietà per tutte le modifiche apportate dagli autori sulla pagina, garantendo che il contenuto modificato venga mantenuto quando gli aggiornamenti vengono sincronizzati dalla blueprint.

Per ulteriori dettagli sul funzionamento dell&#39;ereditarietà con l&#39;Editor universale, vedere il documento [Ereditarietà contenuto nell&#39;Editor universale.](/help/sites-cloud/authoring/universal-editor/inheritance.md)
