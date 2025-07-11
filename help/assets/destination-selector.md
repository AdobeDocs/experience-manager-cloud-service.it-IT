---
title: Selettore di destinazione per AEM as a Cloud Service
description: Utilizza il Selettore di destinazione di AEM per mostrare e selezionare le risorse da utilizzare come copia della risorsa originale.
contentOwner: Adobe
role: Admin, User
exl-id: 7e7bc1ee-d580-4c88-b550-273e8b0620ba
feature: Selectors
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 35%

---

# Selettore di destinazione micro front-end {#Overview}

Il selettore di destinazione Microsoft-Frontend fornisce all&#39;interno dell&#39;applicazione un&#39;interfaccia utente che si integra facilmente con l&#39;archivio [!DNL Experience Manager Assets as a Cloud Service]. È possibile cercare o sfogliare la cartella appropriata all&#39;interno dell&#39;archivio [!DNL Experience Manager Assets as a Cloud Service] e caricare le risorse dall&#39;applicazione.

L’interfaccia utente di Micro-Frontend è resa disponibile nell’esperienza dell’applicazione utilizzando il pacchetto Selettore di destinazione. Eventuali aggiornamenti al pacchetto vengono importati automaticamente e l’ultimo selettore di destinazione distribuito viene caricato automaticamente all’interno dell’applicazione.

![Panoramica](assets/overview-destination-selector.png)

Il selettore delle destinazioni offre molti vantaggi, ad esempio:

* Facilità di integrazione con qualsiasi applicazione Adobe o non Adobe utilizzando la libreria JavaScript Vanilla.
* Manutenzione semplice: gli aggiornamenti al pacchetto Selettore di destinazione vengono automaticamente distribuiti nel selettore di destinazione disponibile per l’applicazione. Non sono necessari aggiornamenti all’interno dell’applicazione per caricare le modifiche più recenti.
* Possibilità di personalizzazione grazie alle proprietà disponibili che controllano la visualizzazione del selettore di destinazione all&#39;interno dell&#39;applicazione.
* Ricerca testuale per passare rapidamente alle cartelle e caricare le risorse dall’applicazione.
* Possibilità di creare cartelle, ordinare le cartelle in ordine crescente o decrescente e visualizzarle in visualizzazione Elenco, Griglia, Raccolta o Cascata.

L&#39;ambito di questo articolo consiste nel dimostrare come utilizzare il selettore di destinazione con un&#39;applicazione [!DNL Adobe] in Unified Shell o quando si dispone già di un imsToken generato per l&#39;autenticazione. In questo articolo, questi flussi di lavoro sono denominati flussi non-SUSI.

Per integrare e utilizzare il selettore di destinazione con l&#39;archivio [!DNL Experience Manager Assets as a Cloud Service], eseguire le attività seguenti:

* [Integrare il selettore di destinazione utilizzando Vanilla JS](#integration-with-vanilla-js)
* [Definire le proprietà di visualizzazione del selettore di destinazione](#destination-selector-properties)
* [Usa selettore di destinazione](#using-destination-selector)

## Integrare il selettore di destinazione utilizzando Vanilla JS {#integration-with-vanilla-js}

È possibile integrare qualsiasi [!DNL Adobe] o applicazioni non Adobe nell’archivio [!DNL Experience Manager Assets] as a [!DNL Cloud Service] e selezionare le risorse dall’interno dell’applicazione.

L’integrazione viene eseguita importando il pacchetto Selettore di destinazione e collegandosi all’as a Cloud Service di Assets utilizzando la libreria JavaScript di Vanilla. È necessario modificare un file `index.html` o qualsiasi file appropriato all&#39;interno dell&#39;applicazione in -

* Definire i dettagli di autenticazione
* Accedere all’archivio Assets as a Cloud Service
* Configurare le proprietà di visualizzazione del Selettore di destinazione

Puoi eseguire l’autenticazione senza definire alcune delle proprietà IMS se:

* Stai integrando un’applicazione [!DNL Adobe] su [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=it).
* Hai già generato un token IMS per l’autenticazione.

## Prerequisiti {#prerequisites}

Definisci i prerequisiti in un file `index.html` o simile nell’implementazione dell’applicazione per definire i dettagli di autenticazione per accedere all’archivio di [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. I prerequisiti includono:

* imsOrg
* imsToken
* apikey

## Installazione {#installation}

Il selettore di destinazione è disponibile sia tramite CDN ESM (ad esempio, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) che tramite la versione [UMD](https://github.com/umdjs/umd).

Nei browser che utilizzano la **versione UMD** (scelta consigliata):

Nei browser che utilizzano la **versione UMD** (scelta consigliata):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

Nei browser con supporto di `import maps` che utilizzano la **versione ESM CDN**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

Nella federazione di moduli Deno/Webpack utilizzando la **versione ESM CDN**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

### Destinazione selezionata {#selected-destination}

Il selettore di destinazione riceve un callback da `onItemSelect`, `onTreeToggleItem` o `onTreeSelectionChange` con la directory selezionata che contiene l&#39;oggetto (directory, immagine e così via).

**Sintassi dello schema**

```
interface SelectedDestination {
  id: string;
  children: SelectedDestination[];
  'repo:repositoryId': string;
  'dc:format': string;
  'repo:assetClass': string;
  'storage:directoryType': string;
  'storage:region': string;
  'repo:name': string;
  'repo:path': string;
  'repo:ancestors': string[];
  'repo:createDate': string;
  'storage:assignee':

  { type: string; id: string; }
  ;
  'repo:assetId': string;
  'aem:published': boolean;
  'repo:createdBy': string;
  'repo:state': string;
  'repo:id': string;
  'repo:modifyDate': string;
  _page:

  { orderBy: string; count: number; };
}
```

Nella tabella seguente vengono descritte alcune delle proprietà importanti della destinazione selezionata.

| Proprietà | Tipo | Spiegazione |
|---|---|---|
| *repo:repositoryId* | stringa | Identificatore univoco dell’archivio in cui è memorizzata la risorsa. |
| *repo:id* | stringa | Identificatore univoco della risorsa. |
| *repo:assetClass* | stringa | La classificazione della risorsa (ad esempio immagine o video, documento). |
| *repo:name* | stringa | Nome della risorsa, inclusa l’estensione del file. |
| *repo:size* | numero | Dimensione della risorsa in byte. |
| *repo:path* | stringa | Posizione della risorsa all’interno dell’archivio. |
| *repo:ancestors* | `Array<string>` | Array di elementi predecessori per la risorsa nell’archivio. |
| *repo:state* | stringa | Stato corrente della risorsa nell’archivio (ad esempio attiva, eliminata e così via). |
| *repo:createdBy* | stringa | Utente o sistema che ha creato la risorsa. |
| *repo:createDate* | stringa | La data e l’ora in cui è stata creata la risorsa. |
| *repo:modifiedBy* | stringa | Utente o sistema che ha modificato per ultimo la risorsa. |
| *repo:modifyDate* | stringa | La data e l’ora dell’ultima modifica apportata alla risorsa. |
| *dc:format* | stringa | Formato della risorsa. |
| *_pagina* | orderBy: string; count: number; | Include il numero di pagina del documento. |

Per un elenco completo delle proprietà e un esempio dettagliato, visita [Esempio di codice del selettore di destinazione](https://github.com/adobe/aem-assets-selectors-mfe-examples).

### Esempio di flusso non-SUSI {#non-ims-vanilla}

In questo esempio viene illustrato come utilizzare il selettore di destinazione con un flusso non SUSI durante l&#39;esecuzione di un&#39;applicazione [!DNL Adobe] in Unified Shell o quando è già stato generato `imsToken` per l&#39;autenticazione.

Includi il pacchetto Selettore di destinazione nel codice utilizzando il tag `script`, come mostrato nelle _righe 6-15_ dell&#39;esempio seguente. Dopo il caricamento dello script, la variabile globale `PureJSSelectors` è disponibile per l&#39;utilizzo. Definisci il selettore di destinazione [proprietà](#destination-selector-properties) come mostrato nelle _righe 16-23_. In un flusso non-SUSI, entrambe le proprietà `imsOrg` e `imsToken` sono necessarie per l’autenticazione. La proprietà `handleSelection` è utilizzata per gestire le risorse selezionate. Per eseguire il rendering del selettore di destinazione, chiamare la funzione `renderDestinationSelector` come indicato nella _riga 17_. Il selettore di destinazione viene visualizzato nell&#39;elemento contenitore `<div>`, come mostrato nelle _righe 21 e 22_.

Seguendo questi passaggi, è possibile utilizzare il selettore di destinazione con un flusso non SUSI nell&#39;applicazione [!DNL Adobe].

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Destination Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the DestinationSelector component
        const container = document.getElementById('destination-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
        const destinationSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderDestinationSelector` available in PureJSSelectors globals to render DestinationSelector
        PureJSSelectors.renderDestinationSelector(container, destinationselectorprops);
    </script>
</head>

<body>
    <div id="destination-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

Ad esempio, visita [Esempio di codice del selettore di destinazione](https://github.com/adobe/aem-assets-selectors-mfe-examples).

## Utilizzare le proprietà del selettore di destinazione {#destination-selector-properties}

Puoi utilizzare le proprietà del Selettore di destinazione per personalizzare il rendering del Selettore di destinazione. Nella tabella seguente sono elencate le proprietà che è possibile utilizzare per personalizzare e utilizzare il selettore di destinazione:

| Proprietà | Tipo | Obbligatorio | Predefiniti | Descrizione |
|---|---|---|---|---|
| *imsOrg* | stringa | Sì | | L’ID di Adobe Identity Management System (IMS) assegnato durante il provisioning di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] per l’organizzazione. La chiave `imsOrg` è necessaria per autenticare se l&#39;organizzazione a cui si accede è in Adobe IMS o meno. |
| *imsToken* | stringa | No | | Token di connessione IMS utilizzato per l’autenticazione. `imsToken` non è richiesto se si utilizza il flusso SUSI. Tuttavia, è necessario se si utilizza il flusso non SUSI. |
| *apiKey* | stringa | No | | Chiave API utilizzata per accedere al servizio di individuazione AEM. `apiKey` non è richiesto se si utilizza il flusso SUSI. Tuttavia, è richiesto nel flusso non SUSI. |
| *rootPath* | stringa | No | /content/dam/ | Percorso della cartella da cui il Selettore di destinazione visualizza le risorse. `rootPath` può essere utilizzato anche sotto forma di incapsulamento. Ad esempio, dato il seguente percorso, `/content/dam/marketing/subfolder/`, il selettore di destinazione non consente di scorrere tra le cartelle principali, ma visualizza solo le cartelle secondarie. |
| *hasMore* | booleano | No | | Quando l’applicazione ha più contenuto da visualizzare, puoi utilizzare questa proprietà per aggiungere un caricatore che carica il contenuto per renderlo visibile nell’applicazione. È un indicatore che indica che il caricamento del contenuto è in corso. |
| *nomeOrganizzazione* | booleano | No | | È il nome dell’organizzazione (probabilmente orgID) associata ad AEM |
| *initRepoID* | stringa | No | | Si tratta del percorso dell’archivio delle risorse che desideri utilizzare in una visualizzazione iniziale predefinita |
| *suCreaCartella* | stringa | No | | La proprietà `onCreateFolder` consente di aggiungere un&#39;icona che aggiunge una nuova cartella nell&#39;applicazione. |
| *onConfirm* | stringa | No | | Si tratta di un callback quando si preme il pulsante di conferma. |
| *confirmDisabled* | stringa | No | | Questa proprietà controlla l’interruttore del pulsante di conferma. |
| *viewType* | stringa | No | | La proprietà `viewType` viene utilizzata per specificare le visualizzazioni utilizzate per visualizzare le risorse. |
| *viewTypeOptions* | stringa | No | | Questa proprietà è correlata alla proprietà `viewType`. puoi specificare una o più viste per visualizzare le risorse. Sono disponibili le seguenti opzioni viewTypeOptions: List view, Grid view, Gallery view, Waterfall view e Tree view. |
| *itemNameFormatter* | stringa | No | | Questa proprietà consente di formattare il nome dell&#39;elemento |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | No |  | Se le traduzioni OOTB non sono sufficienti per le esigenze dell’applicazione, puoi esporre un’interfaccia tramite la quale puoi trasmettere valori localizzati personalizzati tramite la proprietà `i18nSymbols`. Il passaggio di un valore tramite questa interfaccia sostituisce le traduzioni predefinite fornite e utilizza le tue.  Per eseguire la sostituzione, è necessario passare un oggetto valido del [Descrittore del messaggio](https://formatjs.io/docs/react-intl/api/#message-descriptor) alla chiave di `i18nSymbols` che desideri sostituire. |
| *installazioneAvvisiInLinea* | stringa | No | | Aggiunge un messaggio di avviso che si desidera trasmettere nell&#39;applicazione. Ad esempio, l&#39;aggiunta di un messaggio di avviso per segnalare che non si dispone dell&#39;autorizzazione per accedere alla cartella. |
| *intl* | Oggetto | No | | Il selettore di destinazione fornisce le traduzioni predefinite OOTB. È possibile selezionare la lingua di traduzione fornendo una stringa di lingua valida attraverso la proprietà `intl.locale`. Ad esempio: `intl={{ locale: "es-es" }}` </br></br> Le stringhe di lingua supportate seguono i [Codici - ISO 639](https://www.iso.org/iso-639-language-codes.html) per la rappresentazione di nomi di lingue standard. </br></br> Elenco delle lingue supportate: Inglese - ‘en-us’ (impostazione predefinita) Spagnolo - ‘es-es’ Tedesco - ‘de-de’ Francese - ‘fr-fr’ Italiano - ‘it-it’ Giapponese - ‘ja-jp’ Coreano - ‘ko-kr’ Portoghese - ‘pt-br’ cinese (tradizionale) - ‘zh-cn’ Cinese (Taiwan) - ‘zh-tw’ |

## Esempi per utilizzare le proprietà del Selettore di destinazione {#usage-examples}

Puoi definire il selettore di destinazione [proprietà](#destination-selector-properties) nel file `index.html` per personalizzare la visualizzazione del selettore di destinazione all&#39;interno dell&#39;applicazione.

### Esempio 1: creare una cartella nel selettore di destinazione

Il selettore di destinazione consente di creare una cartella per caricare, spostare o copiare le risorse nella posizione specifica.

![create-folder-destination-selector](assets/create-folder-destination-selector.png)

### Esempio 2: specificare il tipo di visualizzazione del selettore di destinazione

Il selettore delle destinazioni mostra un’ampia gamma di risorse in quattro diverse viste, tra cui Vista a elenco, Vista griglia, Vista galleria e Vista cascata. Per specificare il tipo di visualizzazione predefinito, è possibile utilizzare la proprietà `viewType`. La proprietà `viewTypeOptions` viene utilizzata insieme alla proprietà `viewType` per definire altri tipi di visualizzazione in modo che le altre opzioni dei tipi di visualizzazione possano essere visualizzate in un elenco a discesa. Un singolo argomento può essere utilizzato nel caso in cui si desideri visualizzare una sola opzione.

![viewtype-destination-selector](assets/viewtype-destination-selector.png)

### Esempio 3: inizializzare il percorso della cartella Assets

Utilizzare la proprietà `path` per definire il nome della cartella visualizzato automaticamente quando viene eseguito il rendering del selettore di destinazione.

![initialize-folder-path](assets/initialize-folder-path.png)

## Utilizzo del selettore di destinazione {#using-destination-selector}

Dopo aver configurato il selettore di destinazione e aver eseguito l&#39;autenticazione per utilizzare il selettore di destinazione con [!DNL Adobe Experience Manager] come applicazione [!DNL Cloud Service], è possibile selezionare le risorse o eseguire varie altre operazioni per cercare le risorse all&#39;interno dell&#39;archivio.

![using-destination-selector](assets/using-destination-selector.png)

* **A**: [Barra di ricerca](#search-bar)
* **B**: [Ordinamento](#sorting)
* **C**: [Risorse](#assets-repo)
* **D**: [Aggiungi suffisso o prefisso](#add-suffix-or-prefix)
* **E**: [Crea nuova cartella](#create-new-folder)
* **F**: [Visualizza](#types-of-view)
* **G**: [Informazioni](#info)
* **H**: [Seleziona cartella](#select-folder)

### Barra di ricerca {#search-bar}

Il selettore di destinazione consente di eseguire una ricerca full-text delle risorse all’interno dell’archivio selezionato. Ad esempio, se digiti la parola chiave `wave` nella barra di ricerca, vengono mostrate tutte le risorse con la parola chiave `wave` menzionata in una qualsiasi delle proprietà dei metadati.

### Ordinamento {#sorting}

Puoi ordinare le risorse in Selettore destinazione per nome, dimensione o dimensione di una risorsa. Puoi anche ordinare le risorse in ordine crescente o decrescente.

### Archivio Assets {#assets-repo}

Il selettore delle destinazioni consente inoltre di visualizzare i dati dell’archivio scelto disponibili nell’applicazione AEM. È possibile utilizzare la proprietà `repositoryID` per inizializzare il percorso della cartella di destinazione da visualizzare nella prima istanza del selettore di destinazione.

### Aggiungi suffisso o prefisso {#add-suffix-or-prefix}

È un esempio della proprietà `optionsFormSetup`. È possibile utilizzarlo per confermare la selezione, che viene passata all&#39;evento `onConfirm`.

### Crea una cartella {#create-new-folder}

Ti consente di creare una cartella nella cartella di destinazione di [!DNL Adobe Experience Manager] come [!DNL Cloud Service].

### Tipi di visualizzazione {#types-of-view}

Il selettore delle destinazioni consente di visualizzare la risorsa in quattro diverse visualizzazioni:

* ![Vista a elenco](assets/do-not-localize/list-view.png) [!UICONTROL **Vista a elenco**]: la vista a elenco mostra i file e le cartelle in modo scorrevole in una singola colonna.
* ![vista griglia](assets/do-not-localize/grid-view.png) [!UICONTROL **Vista griglia**]: la vista griglia mostra i file e le cartelle in modo scorrevole in una griglia di righe e colonne.
* ![vista galleria](assets/do-not-localize/gallery-view.png) [!UICONTROL **Vista galleria**]: la vista galleria mostra i file o le cartelle in un elenco orizzontale bloccato al centro.
* ![vista a cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL **Vista a cascata**]: la vista a cascata mostra file o cartelle sotto forma di un Bridge.

### Info {#info}

L’icona delle informazioni o info consente di visualizzare i metadati della risorsa selezionata. Include vari dettagli come dimensioni, dimensioni, descrizione, percorso, data di modifica e data di creazione. Le informazioni sui metadati vengono fornite durante il caricamento, la copia o la creazione di una risorsa.

### Selezione cartella {#select-folder}

Il pulsante Seleziona cartella consente di selezionare le risorse per eseguire varie operazioni associate a [proprietà](#destination-selector-properties) nel selettore di destinazione.
