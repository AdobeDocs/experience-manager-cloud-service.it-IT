---
title: Authoring dei contenuti con l’editor universale
description: Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: fced4707e781242132a018d28d4dd121960469eb
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 22%

---


# Authoring dei contenuti con l’editor universale {#authoring}

Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.

## Introduzione {#introduction}

L’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione in modo da offrire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.

A questo scopo, l’editor universale offre agli autori di contenuti un’interfaccia utente intuitiva che richiede una formazione minima per poter entrare e iniziare a modificare i contenuti. Questo documento descrive l’esperienza di authoring dell’editor universale.

>[!NOTE]
>
>In questo documento si presuppone che tu abbia già familiarità con le modalità di accesso e navigazione all’Editor universale. In caso contrario, vedere [Accesso e navigazione nell&#39;editor universale](/help/sites-cloud/authoring/universal-editor/navigation.md).

>[!TIP]
>
>Per un&#39;introduzione più dettagliata all&#39;editor universale, vedere [Introduzione all&#39;editor universale](/help/implementing/universal-editor/introduction.md).

## Modifica del contenuto {#editing-content}

La modifica del contenuto è semplice e intuitiva. Quando passi il mouse sul contenuto nell’editor, il contenuto modificabile viene evidenziato con un sottile contorno blu.

![Il contenuto modificabile viene evidenziato da una casella blu](assets/editable-content.png)

>[!TIP]
>
>Per impostazione predefinita, tocca o fai clic sul contenuto per selezionarlo per la modifica. Se desideri esplorare il contenuto tramite i seguenti collegamenti, passa alla [modalità anteprima](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode).

A seconda del contenuto selezionato, è possibile che siano disponibili diverse opzioni di modifica diretta e che siano disponibili ulteriori informazioni e opzioni per il contenuto nel [pannello delle proprietà](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail).

### Modifica del testo normale {#edit-plain-text}

Per modificare il testo nella posizione desiderata, fai doppio clic o tocca due volte il componente.

![Modifica del contenuto](assets/editing-content.png)

Il contorno blu sottile si trasforma in un contorno blu pesante per indicare la selezione e viene visualizzato un cursore. Apportare le modifiche e premere Invio/Ritorna o selezionare all&#39;esterno della casella di testo per salvare le modifiche.

Quando selezioni il componente testo, i relativi dettagli vengono visualizzati nel [pannello delle proprietà](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail). Potete anche modificare il testo nel pannello.

![Modifica del testo nel pannello delle proprietà](assets/ue-editing-text-component-rail.png)

Inoltre, i dettagli sul testo sono disponibili nel pannello delle proprietà. Le modifiche vengono salvate automaticamente quando lo stato attivo lascia il campo modificato nel pannello delle proprietà.

### Modifica del testo formattato {#edit-rich-text}

Per modificare il testo nella posizione desiderata, fai doppio clic o tocca due volte il componente.

![Modifica di un componente formato RTF](assets/rich-text-editing.png)

Per comodità, le opzioni di formattazione e i dettagli del testo sono disponibili in due posizioni.

#### Menu di scelta rapida {#context-menu}

Il menu di scelta rapida si apre sopra il blocco di testo RTF e offre opzioni di formattazione di base nel contesto. A causa di limiti di spazio, alcune opzioni potrebbero essere nascoste dietro il pulsante con i puntini di sospensione.

![Menu di scelta rapida RTF](assets/rich-text-context-menu.png)

Le modifiche vengono salvate automaticamente quando lo stato attivo lascia il campo modificato.

#### Pannello Proprietà {#properties-rail}

Nel [pannello delle proprietà](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail) viene visualizzato un elemento per il testo selezionato. Tocca la voce per aprire una finestra di dialogo che presenta un’area di lavoro più grande per modificare il testo.

![Finestra di dialogo per la modifica di testo RTF](assets/rich-text-canvas.png)

Tocca o fai clic rispettivamente su **Annulla** o **Fine** per ignorare o salvare le modifiche.

### Editing di file multimediali {#edit-media}

Puoi visualizzarne i dettagli nel [pannello delle proprietà](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail).

![Modifica dei file multimediali](assets/ue-edit-media.png)

1. Tocca o fai clic sull’anteprima dell’immagine selezionata nel pannello proprietà.
1. Viene visualizzata la finestra [selettore risorse](/help/assets/overview-asset-selector.md#using-asset-selector) che consente di selezionare una risorsa.
1. Seleziona per selezionare una nuova risorsa.
1. Seleziona **Seleziona** per tornare al pannello delle proprietà in cui è stata sostituita la risorsa.

Le modifiche vengono salvate automaticamente nel contenuto.

### Modificare i frammenti di contenuto {#edit-content-fragment}

Se selezioni un [frammento di contenuto](/help/sites-cloud/administering/content-fragments/overview.md), puoi modificarne i dettagli nel [pannello delle proprietà](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail).

![Modifica di un frammento di contenuto](assets/ue-edit-cf.png)

I campi definiti nel modello di contenuto del frammento di contenuto selezionato vengono visualizzati e modificabili nel pannello delle proprietà.

Se selezioni un campo correlato a un frammento di contenuto, il frammento di contenuto viene caricato nel pannello dei componenti e il campo viene scorruto automaticamente in.

Le modifiche vengono salvate automaticamente quando lo stato attivo lascia il campo modificato nel pannello delle proprietà.

Se invece desideri modificare il frammento di contenuto nell&#39;[Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md), tocca o fai clic sul pulsante [**Apri nell&#39;editor CF**](/help/sites-cloud/authoring/universal-editor/navigation.md#edit) nel pannello delle proprietà.

>[!TIP]
>
>Utilizzare il tasto di scelta rapida `e` per modificare il frammento di contenuto selezionato nell&#39;editor frammenti di contenuto.

A seconda delle esigenze del flusso di lavoro, può essere utile modificare il frammento di contenuto nell’editor universale o direttamente nell’editor frammento di contenuto.

>[!NOTE]
>
>L&#39;editor universale [convalida i campi dei frammenti di contenuto in base ai relativi modelli](/help/assets/content-fragments/content-fragments-models.md#validation), consentendo di applicare le regole di integrità dei dati, ad esempio i pattern regex e i vincoli di univocità.
>
>In questo modo, il contenuto soddisfa i requisiti aziendali specifici prima della pubblicazione.

### Aggiunta di componenti ai contenitori {#adding-components}

1. Selezionare un componente contenitore nella [struttura contenuto](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) o nell&#39;editor.

   ![Selezione di un componente da aggiungere a un contenitore](assets/ue-add-component.png)

1. Quindi selezionate l&#39;icona Aggiungi nel pannello delle proprietà.

   ![Seleziona icona di aggiunta](assets/add-icon.png)

Il componente viene inserito nel contenitore e può essere modificato nell’editor.

>[!TIP]
>
>Utilizzare il tasto di scelta rapida `a` per aggiungere un componente al contenitore selezionato.

### Duplicazione di componenti nei contenitori {#duplicating-components}

1. Selezionare un componente in un contenitore utilizzando la [struttura contenuto](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) o l&#39;editor.
1. Quindi seleziona l&#39;icona **Duplica** nel pannello delle proprietà.

   ![Selezione di un componente da aggiungere a un contenitore](assets/ue-duplicate-component.png)
1. Il componente viene duplicato e inserito sotto il componente selezionato.

Il componente viene inserito nel contenitore e può essere modificato nell’editor.

### Eliminazione di componenti dai contenitori {#deleting-components}

1. Selezionare un componente contenitore nella [struttura contenuto](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) o nell&#39;editor.
1. Seleziona l’icona della freccia del contenitore per espanderne il contenuto nella struttura del contenuto.
1. Quindi, nella struttura del contenuto, seleziona un componente all’interno del contenitore.
1. Selezionate l&#39;icona Elimina nel pannello delle proprietà.

   ![Eliminazione di un componente](assets/ue-delete-component.png)

Il componente selezionato è stato eliminato.

>[!TIP]
>
>Utilizzare il tasto di scelta rapida `Shift+Backspace` per eliminare il componente selezionato dal relativo contenitore.

### Riordinamento dei componenti nei contenitori {#reordering-components}

1. Se non è già in [modalità struttura contenuto](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode), passare a tale modalità.
1. Seleziona un componente contenitore nella struttura del contenuto o nell’editor.
1. Seleziona l’icona della freccia del contenitore per espanderne il contenuto nella struttura del contenuto.
1. Trascina le icone delle maniglie accanto ai componenti all’interno del contenitore per mostrare che puoi riorganizzarli. Trascina i componenti per riordinarli all’interno del contenitore.

   ![Riordinamento dei componenti](assets/ue-reordering-components.png)

1. Il componente trascinato diventa grigio nella struttura del contenuto, mentre il punto di inserimento è rappresentato da una linea blu. Rilasciate il componente per posizionarlo nella nuova posizione.

I componenti vengono riordinati sia nella struttura del contenuto che nell’editor.

>[!NOTE]
>
>Impossibile spostare i componenti tra contenitori se è impostato un filtro [componente](/help/implementing/universal-editor/filtering.md) diverso tra i contenitori di origine e di destinazione.

### Creare varianti utilizzando GenAI con Genera varianti {#generate-variations-ai}

Utilizza le varianti generative per sfruttare l’intelligenza artificiale generativa per accelerare la creazione dei contenuti.

Apri l’editor universale per trovare il punto di ingresso per generare varianti.

Per ulteriori informazioni, consulta [Generate Variations - Integrated in AEM Editors](/help/generative-ai/generate-variations-integrated-editor.md).

## Anteprima del contenuto {#previewing-content}

Quando hai finito di modificare il contenuto, spesso desideri navigare in esso per vedere come si presenta nel contenuto di altre pagine. In [modalità anteprima](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode) puoi fare clic sui collegamenti per navigare nel contenuto come farebbe un lettore. Il contenuto viene riprodotto nell’editor così come verrebbe pubblicato.

In modalità anteprima, toccando o facendo clic sul contenuto si reagisce come se si trattasse di un normale lettore. Se si desidera selezionare il contenuto da modificare, uscire dalla [modalità anteprima](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode).

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

Per ulteriori dettagli sul funzionamento dell&#39;ereditarietà mediante l&#39;Editor universale, vedere [Ereditarietà contenuto nell&#39;Editor universale](/help/sites-cloud/authoring/universal-editor/inheritance.md).
