---
title: Authoring dei contenuti con l’editor universale
description: Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: c6ab2d9b01a3f1abedb06d1d413e7eceb8b1c031
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 49%

---

# Authoring dei contenuti con l’editor universale {#authoring}

Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.

## Introduzione {#introduction}

Universal Editor consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione, in modo da poter fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.

A tal fine, l’Editor universale offre agli autori dei contenuti un’interfaccia utente intuitiva che richiede una formazione minima per essere in grado di accedere e iniziare semplicemente a modificare i contenuti.

>[!TIP]
>
>Per un’introduzione più dettagliata all’editor universale, consulta il documento [Introduzione all’editor universale.](introduction.md)

>[!NOTE]
>
>L’editor universale è ancora in fase di sviluppo e al momento non può modificare tutti i tipi di contenuto.

## Preparare l’app {#prepare-app}

Per creare contenuti per un’app tramite l’editor universale, l’app deve essere dotata di strumenti che consentano a uno sviluppatore di supportare l’editor.

>[!TIP]
>
>Consulta [Guida introduttiva all’Editor universale in AEM](getting-started.md) un esempio di come configurare un’app AEM per l’utilizzo con Universal Editor.

## Accedi {#sign-in}

Una volta che l’app è stata preparata per funzionare con l’editor universale, dovrai accedere all’editor universale. Sarà necessario un Adobe ID per accedere e [avere accesso all’editor universale.](getting-started.md#request-access)

Dopo aver effettuato l’accesso, immetti l’URL della pagina da modificare in [barra di posizione.](#location-bar) in modo da poter iniziare a modificare i contenuti, come [contenuto testo](#text-mode) o [contenuti multimediali.](#media-mode)

## Comprendere l’interfaccia utente {#ui}

L’interfaccia utente è divisa in cinque aree principali.

* [Intestazione di Experience Cloud](#experience-cloud-header)
* [Intestazione dell’editor universale](#universal-editor-header)
* [Barra modalità](#mode-rail)
* [L’editor](#editor)
* [Barra dei componenti](#component-rail)

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

Tocca o fai clic sul selettore delle soluzioni per passare rapidamente ad altre soluzioni di Experience Cloud.

![Selettore di soluzioni](assets/solutions.png)

#### Aiuto {#help}

L’icona dell’aiuto fornisce un accesso rapido alle risorse di apprendimento e supporto.

![Aiuto](assets/help.png)

#### Notifiche {#notifications}

Questa icona è contrassegnata con il numero di incompleti attualmente assegnati [notifiche.](/help/implementing/cloud-manager/notifications.md)

![Notifiche](assets/notifications.png)

#### Proprietà utente {#user-properties}

Tocca o fai clic sull’icona che rappresenta l’utente per accedere alle impostazioni utente. Se non hai configurato un’immagine utente, viene assegnata un’icona in modo casuale.

![Proprietà utente](assets/user-properties.png)

### Intestazione dell’editor universale {#universal-editor-header}

L’intestazione dell’editor universale è sempre presente nella parte superiore dello schermo immediatamente sotto [l’intestazione di Experience Cloud.](#experience-cloud-header) Ti consente di accedere rapidamente a un’altra pagina per modificare e pubblicare la pagina corrente.

![Intestazione dell’editor universale](assets/universal-editor-header.png)

#### Il menu hamburger {#hamburger-menu}

Il menu hamburger non è ancora implementato.

![Menu Hamburger](assets/hamburger-menu.png)

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

Tocca o fai clic sull’icona dell’emulazione per definire il rendering della pagina in Editor universale.

![Icona dell’emulatore](assets/emulator.png)

Toccando o facendo clic sull’icona dell’emulazione vengono visualizzate le opzioni.

![Opzioni di emulazione](assets/emulation-options.png)

Per impostazione predefinita, l’editor si apre in layout desktop, dove l’altezza e la larghezza vengono definite automaticamente dal browser.

Puoi anche scegliere di emulare un dispositivo mobile e nell’Editor universale:

* Definirne l’orientamento
* Definire la larghezza e l’altezza
* Modificare l’orientamento

#### Apri anteprima app {#open-app-preview}

Tocca o fai clic sull’icona di anteprima dell’app aperta per aprire la pagina che stai modificando nel browser, senza ricorrere all’editor per visualizzare in anteprima le modifiche.

![Apri anteprima app](assets/open-app-preview.png)

>[!TIP]
>
>Utilizza il tasto di scelta rapida `O` (la lettera O) per aprire l’anteprima dell’app.

#### Pubblicazione {#publish}

Tocca o fai clic sul pulsante Pubblica per pubblicare le modifiche al contenuto live per consentirne l’utilizzo da parte dei lettori.

![Pulsante pubblica](assets/publish.png)

>[!TIP]
>
>Consulta il documento [Pubblicazione di contenuti con l’editor visivo universale](publishing.md) per ulteriori informazioni sulla pubblicazione con l’editore universale.

### Barra modalità {#rail}

La barra delle modalità è sempre presente lungo il lato sinistro dell’editor. L&#39;editor può passare facilmente da una modalità di editing all&#39;altra.

![Barra modalità](assets/mode-rail.png)

#### Modalità Anteprima {#preview-mode}

In modalità anteprima, la pagina viene riprodotta nell’editor come verrebbe visualizzata sul servizio pubblicato. Questo consente all’autore del contenuto di navigare nel contenuto facendo clic sui collegamenti, ecc.

![Modalità anteprima](assets/preview-mode.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `P` per passare alla modalità anteprima.

#### Modalità testo {#text-mode}

In modalità testo, la pagina viene riprodotta nell’editor, ma l’autore del contenuto può fare clic per selezionare il contenuto di testo da modificare. Questa è la modalità predefinita dell’editor quando viene caricata una pagina.

![Modalità testo](assets/text-mode.png)

>[!TIP]
>
>Utilizza il tasto di scelta rapida `T` per passare alla modalità testo.

#### Modalità file multimediale {#media-mode}

In modalità multimediale, la pagina viene sottoposta a rendering nell’editor, ma l’autore di contenuto può fare clic per selezionare il contenuto multimediale da modificare.

![Modalità file multimediale](assets/media-mode.png)

>[!TIP]
>
>Utilizza il tasto di scelta rapida `M` per passare alla modalità multimediale.

#### Modalità componente {#component-mode}

In modalità componente, la pagina viene riprodotta nell’editor, ma l’autore di contenuto può fare clic su per selezionare i componenti della pagina.

![Modalità componente](assets/component-mode.png)

>[!TIP]
>
>Utilizza il tasto di scelta rapida `C` per passare alla modalità componente.

>[!NOTE]
>
>La modalità componente è ancora in fase di sviluppo ed è attualmente limitata alla selezione dei componenti.

### L’editor {#editor}

L’editor occupa la maggior parte della finestra ed è dove si trova la pagina specificata in [la barra della posizione](#location-bar) è sottoposto a rendering.

* Se l’editor è in modalità di modifica, ad esempio [modalità testo](#text-mode) o [modalità multimediale,](#media-mode) il contenuto sarà modificabile e non puoi seguire i collegamenti.
* Se l’editor è in [modalità anteprima,](#preview-mode) il contenuto sarà navigabile e potrai seguire i collegamenti, ma non puoi modificarlo.

![Editor](assets/editor.png)

### Barra dei componenti {#component-rail}

La barra dei componenti è sempre presente lungo il lato sinistro dell’editor. A seconda della modalità, può mostrare i dettagli di un componente selezionato nel contenuto o nella gerarchia del contenuto della pagina.

![Barra dei componenti](assets/component-rail.png)

#### Modalità Proprietà {#properties-mode}

In modalità proprietà, la barra mostra le proprietà del componente attualmente selezionato nell’editor. Questa è la modalità predefinita della barra dei componenti quando viene caricata una pagina.

![Modalità Proprietà](assets/properties-mode.png)

I dettagli del componente selezionato sono visualizzati nella barra. Non tutti i componenti hanno dettagli da mostrare.

![Dettagli componente](assets/component-details.png)

>[!TIP]
>
>Utilizza il tasto di scelta rapida `D` per passare alla modalità proprietà.

#### Modalità Struttura contenuto {#Content-tree-mode}

In modalità struttura contenuto, la barra mostra la gerarchia del contenuto della pagina.

![Modalità struttura contenuto](assets/content-tree-mode.png)

Quando si seleziona un elemento nella struttura del contenuto, l’editor scorre fino a quel contenuto e lo seleziona.

![Struttura contenuto](assets/content-tree.png)

>[!TIP]
>
>Utilizza il tasto di scelta rapida `F` per passare alla modalità struttura contenuto.


## Modifica del contenuto {#editing-content}

La modifica del contenuto è semplice e intuitiva. In modalità di modifica ([modalità testo](#text-mode), [modalità multimediale](#media-mode), e [modalità componente](#component-mode)), quando passi il mouse sul contenuto nell’editor, il contenuto modificabile viene evidenziato con una casella blu.

![Il contenuto modificabile viene evidenziato da una casella blu](assets/editable-content.png)

Tocca o fai clic sul contenuto nella casella blu per avviare un editor diretto per apportare le modifiche. Premi invio o indietro per salvare le modifiche.

![Modifica del contenuto](assets/editing-content.png)

In modalità modifica, toccando o facendo clic sul contenuto lo si seleziona per la modifica. Per navigare nel contenuto tramite i seguenti collegamenti, passa a [modalità anteprima.](#preview-mode)

A seconda della modalità in cui ti trovi e del contenuto selezionato, puoi avere opzioni di modifica locali diverse. Inoltre, puoi rivedere proprietà aggiuntive per il contenuto utilizzando [barra dei componenti.](#component-rail)

## Anteprima del contenuto {#previewing-content}

Quando hai finito di modificare il contenuto, spesso desideri navigare in esso per vedere come si presenta nel contenuto di altre pagine. In [modalità anteprima](#preview-mode) puoi fare clic sui collegamenti per navigare nel contenuto come farebbe un lettore. Il contenuto viene riprodotto nell’editor così come verrebbe pubblicato.

In modalità anteprima, toccando o facendo clic sul contenuto questo appare così come si presenterebbe a un lettore. Se desideri selezionare il contenuto da modificare, passa a una modalità di modifica come [modalità testo](#text-mode) o [modalità multimediale.](#media-mode)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md) - Scopri come Universal Editor consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione, per offrire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Pubblicazione di contenuto con l’editor universale](publishing.md): scopri in che modo l’editor visivo universale pubblica il contenuto e come le app possono gestire il contenuto pubblicato.
* [Guida introduttiva all’editor universale in AEM](getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](authentication.md): scopri come l’editor universale effettua l’autenticazione.
