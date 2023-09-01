---
title: Authoring dei contenuti con l’editor universale
description: Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: 4cf7d3692b53e5cb5baecd7d0ee93824d9186380
workflow-type: tm+mt
source-wordcount: '2267'
ht-degree: 57%

---


# Authoring dei contenuti con l’editor universale {#authoring}

Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.

## Introduzione {#introduction}

L’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione in modo da offrire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.

A questo scopo, l’editor universale offre agli autori di contenuti un’interfaccia utente intuitiva che richiede una formazione minima per poter entrare e iniziare a modificare i contenuti. Questo documento descrive l’esperienza di authoring dell’editor universale.

>[!TIP]
>
>Per un’introduzione più dettagliata all’editor universale, consulta il documento [Introduzione all’editor universale.](introduction.md)

>[!NOTE]
>
>L’editor universale è ancora in fase di sviluppo. Attualmente non è possibile modificare tutti i tipi di contenuto.

## Preparare l’app {#prepare-app}

Per creare contenuti per un’app utilizzando l’editor universale, l’app deve essere preparata da uno sviluppatore per supportare l’editor.

>[!TIP]
>
>Consulta il documento [Guida introduttiva all’editor universale in AEM](getting-started.md) per un esempio su come configurare un’app AEM per utilizzare l’editor universale.

## Accedi {#sign-in}

Una volta che l’app è stata preparata per funzionare con l’editor universale, dovrai accedere all’editor universale. Sarà necessario un Adobe ID per accedere e [avere accesso all’editor universale.](getting-started.md#request-access)

Dopo aver effettuato l’accesso, immetti l’URL della pagina da modificare nella [barra degli indirizzi.](#location-bar) in modo da poter iniziare a modificare i contenuti, come [contenuto testo](#text-mode) o il [contenuto multimediale.](#media-mode)

## Comprendere l’interfaccia utente {#ui}

L’interfaccia utente è divisa in cinque aree principali.

* [Intestazione di Experience Cloud](#experience-cloud-header)
* [Intestazione dell’editor universale](#universal-editor-header)
* [La barra modalità](#mode-rail)
* [L’editor](#editor)
* [La barra dei componenti](#component-rail)

![Interfaccia utente dell’editor universale](assets/ui.png)

### Intestazione di Experience Cloud {#experience-cloud-header}

L’intestazione di Experience Cloud è sempre presente nella parte superiore dello schermo. È un ancoraggio che indica dove ti trovi all’interno di Experience Cloud e ti aiuta a passare ad altre app di Experience Cloud.

![Intestazione di Experience Cloud](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

Seleziona il collegamento Adobe Experience Cloud a sinistra dell’intestazione per passare alla directory principale della soluzione Experience Manager e accedere a strumenti come [Cloud Manager,](/help/onboarding/cloud-manager-introduction.md) [Cloud Acceleration Manager,](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) e [Distribuzione di software.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=it)

![Pulsante di navigazione globale](assets/global-navigation.png)

#### Organizzazione {#organization}

Viene visualizzata l’organizzazione in cui hai effettuato l’accesso. Tocca o fai clic per passare a un’altra organizzazione se il tuo Adobe ID è associato a più di una.

![Indicatore dell’organizzazione](assets/organization.png)

#### Soluzioni {#solutions}

Toccando o facendo clic sul selettore delle soluzioni puoi passare rapidamente ad altre soluzioni di Experience Cloud.

![Selettore di soluzioni](assets/solutions.png)

#### Aiuto {#help}

L’icona dell’aiuto fornisce un accesso rapido alle risorse di apprendimento e supporto.

![Aiuto](assets/help.png)

#### Notifiche {#notifications}

Questa icona viene contrassegnata con il numero di [notifiche](/help/implementing/cloud-manager/notifications.md) incomplete attualmente assegnate.

![Notifiche](assets/notifications.png)

#### Proprietà utente {#user-properties}

Tocca o fai clic sull’icona che rappresenta l’utente per accedere alle impostazioni utente. Se non hai configurato un’immagine utente, viene assegnata un’icona in modo casuale.

![Proprietà utente](assets/user-properties.png)

### Intestazione dell’editor universale {#universal-editor-header}

L’intestazione dell’editor universale è sempre presente nella parte superiore dello schermo immediatamente sotto [l’intestazione di Experience Cloud.](#experience-cloud-header) Consente un accesso rapido per passare a un’altra pagina di modifica e di pubblicazione della pagina corrente.

![Intestazione dell’editor universale](assets/universal-editor-header.png)

#### Il menu hamburger {#hamburger-menu}

Il menu hamburger non è ancora implementato.

![Menu hamburger](assets/hamburger-menu.png)

#### Barra della posizione {#location-bar}

La barra della posizione mostra l’indirizzo della pagina che stai modificando. Tocca o fai clic per inserire l’indirizzo di un’altra pagina da modificare.

![Barra della posizione](assets/location-bar.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `L` per aprire la barra degli indirizzi.

>[!NOTE]
>
>Qualsiasi pagina da modificare con l’editor universale deve essere [abilitata per supportare l’editor universale.](getting-started.md)

#### Impostazioni emulatore {#emulator}

Tocca o fai clic sull’icona dell’emulatore per definire il rendering della pagina nell’editor universale.

![Icona dell’emulatore](assets/emulator.png)

Toccando o facendo clic sull’icona dell’emulatore vengono visualizzate le opzioni.

![Opzioni di emulazione](assets/emulation-options.png)

Per impostazione predefinita, l’editor si apre in layout desktop, dove l’altezza e la larghezza vengono definite automaticamente dal browser.

Puoi anche scegliere di emulare un dispositivo mobile e nell’editor universale:

* Definirne l’orientamento
* Definire la larghezza e l’altezza
* Modificare l’orientamento

#### Apri anteprima app {#open-app-preview}

Tocca o fai clic sull’icona di anteprima dell’app per aprire la pagina che stai modificando nella scheda del browser corrispondente, senza che sia necessario l’editor per visualizzare l’anteprima del contenuto.

![Apri anteprima app](assets/open-app-preview.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `O` (la lettera O) per aprire l’anteprima dell’app.

#### Pubblicazione {#publish}

Tocca o fai clic sul pulsante Pubblica per poter pubblicare le modifiche al contenuto utilizzabile dai lettori in tempo reale.

![Pulsante pubblica](assets/publish.png)

>[!TIP]
>
>Consulta il documento [Pubblicazione di contenuti con l’editor visivo universale](publishing.md) per ulteriori informazioni sulla pubblicazione con l’editore universale.

### La barra modalità {#rail}

La barra modalità è sempre presente sul lato sinistro dell’editor. Consente all’editor di passare facilmente da una modalità di modifica all’altra.

![La barra modalità](assets/mode-rail.png)

#### Modalità Anteprima {#preview-mode}

In modalità anteprima, la pagina viene riprodotta nell’editor come verrebbe visualizzata sul servizio pubblicato. Questo consente all’autore del contenuto di navigare nel contenuto facendo clic sui collegamenti, ecc.

![Modalità anteprima](assets/preview-mode.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `P` per passare alla modalità anteprima.

#### Modalità testo {#text-mode}

In modalità testo, l’autore del contenuto può fare clic per selezionare il contenuto di testo.

![Modalità testo](assets/text-mode.png)

* È possibile [modifica testo normale](#editing-content) sul posto.
* È inoltre possibile [modifica testo formattato](#editing-rich-text) nella barra dei componenti sono presenti ulteriori opzioni di formattazione.

>[!TIP]
>
>Usa il tasto di scelta rapida `T` per passare alla modalità testo.

#### Modalità contenuto multimediale {#media-mode}

In modalità multimediale, l’autore di contenuto può fare clic per selezionare il contenuto multimediale.

![Modalità contenuto multimediale](assets/media-mode.png)

I dettagli del contenuto vengono visualizzati nella barra dei componenti, che consente anche all’autore di [modificare il contenuto multimediale.](#editing-media)

>[!TIP]
>
>Usa il tasto di scelta rapida `M` per passare alla modalità contenuto multimediale.

#### Modalità componente {#component-mode}

In modalità componente, l’autore di contenuto può fare clic per selezionare [Frammenti di contenuto.](/help/assets/content-fragments/content-fragments.md)

![Modalità componente](assets/component-mode.png)

Quando selezioni un frammento di contenuto, i relativi dettagli vengono visualizzati nella barra dei componenti, dove puoi [modificare il frammento di contenuto.](#edit-content-fragment)

>[!TIP]
>
>Usa il tasto di scelta rapida `C` per passare alla modalità componente.

### L’editor {#editor}

L’editor occupa la maggior parte della finestra ed è l’area in cui viene eseguito il rendering della pagina specificata nella [barra della posizione](#location-bar).

* Se l’editor è in modalità di modifica, ad esempio [modalità testo](#text-mode) o [modalità multimediale,](#media-mode) il contenuto sarà modificabile, ma non puoi seguire i collegamenti.
* Se l’editor è in [modalità anteprima,](#preview-mode) il contenuto sarà navigabile e potrai seguire i collegamenti, ma non puoi modificarlo.

![Editor](assets/editor.png)

### Barra dei componenti {#component-rail}

La barra dei componenti è sempre presente lungo il lato destro dell’editor. A seconda della modalità, può mostrare i dettagli di un componente selezionato nel contenuto o la gerarchia dei contenuti della pagina.

![La barra dei componenti](assets/component-rail.png)

#### Modalità proprietà {#properties-mode}

In modalità proprietà, la barra mostra le proprietà del componente attualmente selezionato nell’editor. Questa è la modalità predefinita della barra dei componenti quando viene caricata una pagina.

![Modalità proprietà](assets/properties-mode.png)

A seconda del tipo di componente selezionato, i dettagli possono essere visualizzati e modificati nella barra delle proprietà.

![Dettagli dei componenti](assets/component-details.png)

Nota che non tutti i componenti hanno dettagli che possono essere visualizzati e/o modificati.

>[!TIP]
>
>Usa il tasto di scelta rapida `D` per passare alla modalità proprietà.

#### Modalità struttura contenuto {#content-tree-mode}

In modalità struttura contenuto, la barra mostra la gerarchia del contenuto della pagina.

![Modalità struttura contenuto](assets/content-tree-mode.png)

Quando si seleziona un elemento nella struttura del contenuto, l’editor scorre fino a quel contenuto e lo seleziona.

![Struttura contenuto](assets/content-tree.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `F` per passare alla modalità struttura contenuto.

#### Modifica {#edit}

In [modalità componente,](#component-mode) se si seleziona un [Frammento di contenuto,](/help/assets/content-fragments/content-fragments.md) l’opzione modifica viene visualizzata nella barra dei componenti.

![Icona Modifica](assets/edit.png)

Toccando o facendo clic sul pulsante di modifica si apre [Editor frammento di contenuto](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor) in una nuova scheda, che consente di accedere a tutte le funzioni dell’Editor frammento di contenuto.

Puoi anche modificare i dettagli del Frammento di contenuto all’interno della barra dei componenti in base alle esigenze del flusso di lavoro.

>[!TIP]
>
>Utilizza il tasto di scelta rapida `E` per modificare un componente selezionato.

#### Aggiungi {#add}

Se selezioni un componente contenitore nella struttura del contenuto o nell’editor, l’opzione aggiungi viene visualizzata nella barra dei componenti.

![Icona Aggiungi](assets/ue-add-component-icon.png)

Toccando o facendo clic sul pulsante Aggiungi si apre un menu a discesa dei componenti disponibili per [aggiungi al contenitore selezionato.](#adding-components)

>[!TIP]
>
>Utilizza il tasto di scelta rapida `A` per aggiungere un componente a un componente contenitore selezionato.

#### Eliminare {#delete}

Se selezioni un componente all’interno di un componente contenitore nella struttura del contenuto o nell’editor, l’opzione Elimina viene visualizzata nella barra dei componenti.

![Icona Elimina](assets/ue-delete-component-icon.png)

Toccando o facendo clic sul pulsante Elimina [elimina il componente.](#deleting-components)

>[!TIP]
>
>Utilizza il tasto di scelta rapida `Shift+Backspace` per eliminare un componente selezionato da un contenitore.

## Modifica del contenuto {#editing-content}

La modifica del contenuto è semplice e intuitiva. In modalità di modifica ([modalità testo](#text-mode), [modalità contenuto multimediale](#media-mode), e [modalità componente](#component-mode)), quando passi il mouse sul contenuto nell’editor, il contenuto modificabile viene evidenziato con una casella blu.

![Il contenuto modificabile viene evidenziato da una casella blu](assets/editable-content.png)

In modalità modifica, toccando o facendo clic sul contenuto lo si seleziona per la modifica. Per navigare nel contenuto tramite i seguenti collegamenti, passa a [modalità anteprima.](#preview-mode)

A seconda della [modalità](#mode-rail) in e nel contenuto selezionato, possono essere disponibili opzioni di modifica locali diverse e puoi rivedere proprietà aggiuntive per il contenuto utilizzando [barra dei componenti.](#component-rail)

### Modifica del testo normale {#edit-plain-text}

Se ti trovi in [modalità testo](#text-mode) e selezionare un componente testo normale, è possibile modificare il testo nella posizione desiderata.

![Modifica del contenuto](assets/editing-content.png)

È sufficiente digitare per aggiornare il contenuto. Premi Invio/Ritorna o tocca o fai clic all’esterno della casella di testo per salvare le modifiche.

### Modifica del testo formattato {#edit-rich-text}

Se ti trovi in [modalità testo](#text-mode) e selezionare un componente testo RTF, puoi modificare il testo nella posizione desiderata.

È sufficiente digitare per aggiornare il contenuto. Premi Invio/Ritorna o tocca o fai clic all’esterno della casella di testo per salvare le modifiche.

Inoltre, le opzioni di formattazione e i dettagli sul testo sono disponibili nella barra dei componenti.

![Modifica di un componente formato RTF](assets/rich-text-editing.png)

Le modifiche di formattazione vengono salvate automaticamente nel contenuto.

### Editing di file multimediali {#edit-media}

Se ti trovi in [modalità multimediale](#media-mode) quando selezioni un’immagine puoi visualizzarne i dettagli nella barra dei componenti.

![Editing di file multimediali](assets/ue-edit-media.png)

Tocca o fai clic su **Sostituisci** sotto l’anteprima dell’immagine selezionata nella barra dei componenti, per sostituirla con un’altra immagine della libreria di risorse.

1. Il [selettore risorse](/help/assets/asset-selector.md#using-asset-selector) viene visualizzata una finestra che consente di selezionare una risorsa.
1. Tocca o fai clic su per selezionare una nuova risorsa.
1. Tocca o fai clic su **Seleziona** per tornare alla barra dei componenti in cui la risorsa è stata sostituita.

Le modifiche vengono salvate automaticamente nel contenuto.

>[!TIP]
>
>Utilizza il tasto di scelta rapida `R` per aprire il selettore risorse e sostituire l’immagine selezionata.

### Modifica di frammenti di contenuto {#edit-content-fragment}

Se ti trovi in [modalità componente](#component-mode) e selezioni una [Frammento di contenuto,](/help/sites-cloud/administering/content-fragments/overview.md) puoi modificarne i dettagli nella barra dei componenti.

![Modifica di un frammento di contenuto](assets/ue-edit-cf.png)

I campi definiti nel modello di contenuto del frammento di contenuto selezionato sono visualizzati e modificabili nella barra dei componenti.

Le modifiche vengono salvate automaticamente nel contenuto.

Se desideri modificare il frammento di contenuto in [Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md) invece, fai clic su [pulsante modifica](#edit) nella barra delle modalità.

### Aggiunta di componenti ai contenitori {#adding-components}

1. Seleziona un componente contenitore nella struttura del contenuto o nell’editor.
1. Quindi tocca o fai clic sull’icona Aggiungi nella barra dei componenti.

   ![Selezione di un componente da aggiungere a un contenitore](assets/ue-add-component.png)

Il componente viene inserito nel contenitore e può essere modificato nell’editor.

### Eliminazione di componenti dai contenitori {#deleting-components}

1. Seleziona un componente contenitore nella struttura del contenuto o nell’editor.
1. Tocca o fai clic sulla freccia del contenitore per espanderne il contenuto nella struttura del contenuto.
1. Quindi, nella struttura del contenuto, seleziona un componente all’interno del contenitore.
1. Tocca o fai clic sull’icona Elimina nella barra dei componenti.

   ![Eliminazione di un componente](assets/ue-delete-component.png)

Il componente selezionato è stato eliminato.

### Riordinamento dei componenti nei contenitori {#reordering-components}

1. Seleziona un componente contenitore nella struttura del contenuto o nell’editor.
1. Se non è già in [modalità struttura contenuto,](#content-tree-mode) passa ad esso.
1. Tocca o fai clic sulla freccia del contenitore per espanderne il contenuto nella struttura del contenuto.
1. Trascina le icone delle maniglie accanto ai componenti all’interno del contenitore per mostrare che puoi riorganizzarli. Trascina i componenti per riordinarli all’interno del contenitore.

   ![Riordinamento dei componenti](assets/ue-reordering-components.png)
1. Il componente trascinato diventa grigio nell’albero dei componenti, mentre il punto di inserimento è rappresentato da una linea blu. Rilasciate il componente per posizionarlo nella nuova posizione.

I componenti vengono riordinati sia nella struttura del contenuto che nell’editor

## Anteprima del contenuto {#previewing-content}

Quando hai finito di modificare il contenuto, spesso desideri navigare in esso per vedere come si presenta nel contenuto di altre pagine. In [modalità anteprima](#preview-mode) puoi fare clic sui collegamenti per navigare nel contenuto come farebbe un lettore. Il contenuto viene riprodotto nell’editor così come verrebbe pubblicato.

In modalità anteprima, toccando o facendo clic sul contenuto questo appare così come si presenterebbe a un lettore. Se desideri selezionare il contenuto da modificare, passa a una modalità di modifica come [modalità testo](#text-mode) o [modalità contenuto multimediale.](#media-mode)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md): scopri come l’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione in modo da fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Pubblicazione di contenuto con l’editor universale](publishing.md): scopri in che modo l’editor visivo universale pubblica il contenuto e come le app possono gestire il contenuto pubblicato.
* [Guida introduttiva all’editor universale in AEM](getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](authentication.md): scopri come l’editor universale effettua l’autenticazione.
