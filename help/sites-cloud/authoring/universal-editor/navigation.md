---
title: Accesso e navigazione nell’editor universale
description: Scopri le nozioni di base sull’accesso e la navigazione nell’Editor universale.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 58c58243dc98a21161afe0976da4dcdc235da0d3
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 40%

---


# Accesso e navigazione nell’editor universale {#navigating}

Scopri le nozioni di base sull’accesso e la navigazione nell’Editor universale.

## Introduzione {#introduction}

L’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione in modo da offrire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.

A questo scopo, l’editor universale offre agli autori di contenuti un’interfaccia utente intuitiva che richiede una formazione minima per poter entrare e iniziare a modificare i contenuti. Questo documento descrive come spostarsi nell’Editor universale.

>[!TIP]
>
>* Per informazioni dettagliate sull&#39;authoring mediante l&#39;editor universale, vedere il documento [Authoring dei contenuti con l&#39;editor universale.](/help/sites-cloud/authoring/universal-editor/authoring.md)
>* Per un’introduzione più dettagliata all’editor universale, consulta il documento [Introduzione all’editor universale.](/help/implementing/universal-editor/introduction.md)

## Preparare l’app {#prepare-app}

Per creare contenuti per un’app utilizzando l’editor universale, l’app deve essere preparata da uno sviluppatore per supportare l’editor.

>[!TIP]
>
>Consulta il documento [Guida introduttiva all’editor universale in AEM](/help/implementing/universal-editor/getting-started.md) per un esempio su come configurare un’app AEM per utilizzare l’editor universale.

## Accesso all’editor universale {#accessing}

Una volta che l’app è dotata di strumenti per funzionare con l’editor universale, questo può essere accessibile sia all’interno di AEM as a Cloud Service che direttamente senza accedere all’AEM.

### Accesso in AEM as a Cloud Service {#accessing-aem}

1. Accedi all’istanza di authoring di AEM as a Cloud Service.
1. Utilizzare la console [**Sites**](/help/sites-cloud/authoring/sites-console/introduction.md) per passare alla pagina creata per l&#39;utilizzo con l&#39;editor universale che si desidera modificare.
1. Modifica la pagina.
1. Viene aperto Universal Editor per modificare la pagina selezionata.

>[!NOTE]
>
>Durante la modifica di una pagina nella console [**Sites**,](/help/sites-cloud/authoring/sites-console/introduction.md) la console aprirà l&#39;editor appropriato per il modello [ della pagina:](/help/sites-cloud/authoring/sites-console/templates.md) o l&#39;editor universale descritto in questo documento o l&#39;editor di [ pagine.](/help/sites-cloud/authoring/page-editor/introduction.md)

### Accesso diretto {#accessing-directly}

1. Accedi all’editor universale. Per accedere è necessario un Adobe ID e [accedere all&#39;editor universale.](/help/implementing/universal-editor/getting-started.md#request-access)

1. Dopo aver effettuato l’accesso, immetti l’URL della pagina da modificare nella [barra degli indirizzi.](#location-bar) in modo da poter iniziare a modificare i contenuti, come [contenuto testo](#text-mode) o il [contenuto multimediale.](#media-mode)

## Comprendere l’interfaccia utente {#ui}

L’interfaccia utente è divisa in queste aree principali.

* [Intestazione di Experience Cloud](#experience-cloud-header)
* [Barra degli strumenti Editor universale](#universal-editor-toolbar)
* [L’editor](#editor)
* [Barra delle proprietà](#properties-rail)

![Interfaccia utente dell’editor universale](assets/ui.png)

### Intestazione di Experience Cloud {#experience-cloud-header}

L’intestazione di Experience Cloud è sempre presente nella parte superiore dello schermo. È un ancoraggio che indica dove ti trovi all’interno di Experience Cloud e ti aiuta a passare ad altre app di Experience Cloud.

![Intestazione di Experience Cloud](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

Seleziona il collegamento Adobe Experience Cloud a sinistra dell’intestazione per passare alla directory principale della soluzione Experience Manager e accedere a strumenti come [Cloud Manager,](/help/onboarding/cloud-manager-introduction.md) [Cloud Acceleration Manager,](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) e [Distribuzione di software.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=it)

![Pulsante di navigazione globale](assets/global-navigation.png)

#### Organizzazione {#organization}

Viene visualizzata l’organizzazione in cui hai effettuato l’accesso. Seleziona questa opzione per passare a un’altra organizzazione se l’Adobe ID è associata a più.

![Indicatore dell’organizzazione](assets/organization.png)

#### Soluzioni {#solutions}

Tocca o fai clic sul selettore delle soluzioni per passare rapidamente ad altre soluzioni di Experience Cloud.

![Selettore di soluzioni](assets/solutions.png)

#### Aiuto {#help}

L’icona dell’aiuto fornisce un accesso rapido alle risorse di apprendimento e supporto.

![Aiuto](assets/help.png)

#### Notifiche {#notifications}

Questa icona viene contrassegnata con il numero di [notifiche](/help/implementing/cloud-manager/notifications.md) incomplete attualmente assegnate.

![Notifiche](assets/notifications.png)

#### Proprietà utente {#user-properties}

Seleziona l’icona che rappresenta l’utente per accedere alle impostazioni utente. Se non hai configurato un’immagine utente, viene assegnata un’icona in modo casuale.

![Proprietà utente](assets/user-properties.png)

### Barra degli strumenti Editor universale {#universal-editor-toolbar}

La barra degli strumenti di Universal Editor è sempre presente nella parte superiore dello schermo immediatamente sotto [ l&#39;intestazione dell&#39;Experience Cloud.](#experience-cloud-header) Consente un accesso rapido per passare a un’altra pagina di modifica e di pubblicazione della pagina corrente.

![Barra degli strumenti di Universal Editor](assets/universal-editor-toolbar.png)

#### Pulsante Home {#home-button}

Il pulsante Home consente di tornare alla pagina iniziale di Universal Editor

![Menu hamburger](assets/home-button.png)

Nella pagina iniziale è possibile immettere l&#39;URL del sito che si desidera modificare con l&#39;editor universale.

![Pagina iniziale](assets/start-page.png)

>[!NOTE]
>
>Qualsiasi pagina che si desidera modificare con l&#39;editor universale deve essere [dotata di strumenti per supportare l&#39;editor universale.](/help/implementing/universal-editor/getting-started.md)

#### Barra della posizione {#location-bar}

La barra della posizione mostra l’indirizzo della pagina che stai modificando. Selezionare questa opzione per immettere l&#39;indirizzo di un&#39;altra pagina da modificare.

![Barra della posizione](assets/location-bar.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `L` per aprire la barra degli indirizzi.

>[!NOTE]
>
>Qualsiasi pagina che si desidera modificare con l&#39;editor universale deve essere [dotata di strumenti per supportare l&#39;editor universale.](/help/implementing/universal-editor/getting-started.md)

#### Impostazioni intestazione autenticazione {#authentication-settings}

Se devi [impostare un&#39;intestazione di autenticazione personalizzata a scopo di sviluppo locale, seleziona l&#39;icona delle impostazioni dell&#39;intestazione di autenticazione.](/help/implementing/universal-editor/developer-overview.md#auth-header)

![Pulsante Impostazioni intestazione autenticazione](assets/authentication-header-settings.png)

#### Impostazioni emulatore {#emulator}

Seleziona l’icona di emulazione per definire il rendering della pagina in Editor universale.

![Icona dell’emulatore](assets/emulator.png)

Toccando o facendo clic sull’icona dell’emulatore vengono visualizzate le opzioni.

![Opzioni di emulazione](assets/emulation-options.png)

Per impostazione predefinita, l’editor si apre in layout desktop, dove l’altezza e la larghezza vengono definite automaticamente dal browser.

Puoi anche scegliere di emulare un dispositivo mobile e nell’editor universale:

* Definirne l’orientamento
* Definire la larghezza e l’altezza
* Modificare l’orientamento

#### Modalità Anteprima {#preview-mode}

In modalità anteprima, la pagina viene riprodotta nell’editor come verrebbe visualizzata sul servizio pubblicato. Questo consente all’autore di contenuto di navigare nel contenuto facendo clic sui collegamenti e così via.

![Modalità anteprima](assets/preview-mode.png)

>[!TIP]
>
>Utilizzare il tasto di scelta rapida `P` per passare alla modalità anteprima e viceversa.

#### Apri anteprima app {#open-app-preview}

Seleziona l’icona di anteprima dell’app aperta per aprire la pagina che stai modificando nella scheda del browser corrispondente, senza dover accedere all’editor per visualizzare l’anteprima dei contenuti.

![Apri anteprima app](assets/open-app-preview.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `O` (la lettera O) per aprire l’anteprima dell’app.

#### Pubblicazione {#publish}

Seleziona il pulsante Pubblica per pubblicare le modifiche al contenuto live per consentirne l’utilizzo da parte dei lettori.

![Pulsante pubblica](assets/publish.png)

>[!TIP]
>
>Per ulteriori informazioni sulla pubblicazione con Universal Editor, vedere il documento [Pubblicazione di contenuti con Universal Editor](publishing.md).

#### Pulsanti aggiuntivi {#additional-toolbar-buttons}

Universal Editor offre un&#39;esperienza di authoring personalizzabile ed estensibile. Se nella barra degli strumenti sono presenti pulsanti aggiuntivi, l’editor universale è stato esteso.

* Per informazioni dettagliate sulle possibilità di estensione, vedere [Personalizzazione ed estensione dell&#39;editor universale.](/help/implementing/universal-editor/customizing.md)
* Per informazioni dettagliate sul funzionamento di una singola estensione, consulta la [documentazione di Extension Manager.](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/)

### L’editor {#editor}

L’editor occupa la maggior parte della finestra ed è l’area in cui viene eseguito il rendering della pagina specificata nella [barra della posizione](#location-bar).

![Editor](assets/editor.png)

Se l&#39;editor è in modalità [anteprima,](#preview-mode) il contenuto sarà navigabile e puoi seguire i collegamenti, ma non puoi modificarlo.

### Barra delle proprietà {#properties-rail}

La barra delle proprietà è sempre presente lungo il lato destro dell’editor. A seconda della modalità, può mostrare i dettagli di un componente selezionato nel contenuto o la gerarchia dei contenuti della pagina.

![Barra delle proprietà](assets/component-rail.png)

#### Modalità proprietà {#properties-mode}

In modalità proprietà, la barra mostra le proprietà del componente attualmente selezionato nell’editor. Questa è la modalità predefinita della barra delle proprietà quando viene caricata una pagina.

![Modalità proprietà](assets/properties-mode.png)

A seconda del tipo di componente selezionato, i dettagli possono essere visualizzati e modificati nella barra delle proprietà.

![Dettagli dei componenti](assets/component-details.png)

Non tutti i componenti hanno dettagli che possono essere visualizzati e/o modificati.

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

##### Modifica {#edit}

Durante la modifica, le opzioni per il componente selezionato vengono visualizzate nella barra delle proprietà, dove è possibile modificarlo. Se il componente selezionato è un frammento di contenuto, puoi anche selezionare il pulsante Modifica.

![Icona Modifica](assets/edit.png)

Toccando o facendo clic sul pulsante Modifica si apre l&#39;[Editor frammento di contenuto](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor) in una nuova scheda. Questo consente di accedere a tutte le funzionalità dell’Editor frammento di contenuto per modificare il frammento di contenuto associato.

A seconda delle esigenze del flusso di lavoro, può essere utile modificare il frammento di contenuto nell’editor universale o direttamente nell’editor frammento di contenuto.

>[!TIP]
>
>Utilizza il tasto di scelta rapida `E` per modificare un componente selezionato.

##### Aggiungi {#add}

Se selezioni un componente contenitore nella struttura del contenuto o nell’editor, l’opzione aggiungi viene visualizzata nella barra delle proprietà.

![Icona Aggiungi](assets/ue-add-component-icon.png)

Toccando o facendo clic sul pulsante Aggiungi si apre un menu a discesa dei componenti disponibili per [aggiungere al contenitore selezionato.](#adding-components)

![Aggiungi menu di scelta rapida](assets/add-context-menu.png)

>[!TIP]
>
>Utilizzare il tasto di scelta rapida `A` per aggiungere un componente a un componente contenitore selezionato.

##### Elimina {#delete}

Se selezioni un componente all’interno di un componente contenitore nella struttura del contenuto o nell’editor, l’opzione Elimina viene visualizzata nella barra delle proprietà.

![Icona Elimina](assets/ue-delete-component-icon.png)

Toccando o facendo clic sul pulsante Elimina [il componente viene eliminato.](#deleting-components)

>[!TIP]
>
>Utilizzare il tasto di scelta rapida `Shift+Backspace` per eliminare un componente selezionato da un contenitore.

#### Pulsanti aggiuntivi {#additional-properties-rail-buttons}

Universal Editor offre un&#39;esperienza di authoring personalizzabile ed estensibile. Se trovi pulsanti aggiuntivi nella barra delle proprietà, l’Editor universale è stato esteso.

* Per informazioni dettagliate sulle possibilità di estensione, vedere [Personalizzazione ed estensione dell&#39;editor universale.](/help/implementing/universal-editor/customizing.md)
* Per informazioni dettagliate sul funzionamento di una singola estensione, consulta la [documentazione di Extension Manager.](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/)

## Passaggi successivi {#next-steps}

Ora che sai come accedere e navigare nell&#39;Editor universale, puoi [creare contenuti utilizzandolo.](/help/sites-cloud/authoring/universal-editor/authoring.md)