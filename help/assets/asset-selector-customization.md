---
title: Personalizzare l’applicazione Asset Selector
description: Utilizza le funzioni per personalizzare il selettore delle risorse all’interno dell’applicazione.
role: Admin, User
exl-id: 0fd0a9f7-8c7a-4c21-9578-7c49409df609
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 23%

---

# Personalizzazioni del Selettore risorse {#asset-selector-customization}

Asset Selector (Selettore risorse) consente di personalizzare vari componenti in base a preferenze, requisiti o esigenze funzionali. Puoi personalizzare i seguenti componenti [Selettore risorse micro-front-end](#overview-asset-selector.md):

* [Personalizzare il pannello dei filtri](#customize-filter-panel)
* [Personalizzare le informazioni nella vista modale](#customize-info-in-modal-view)
* [Attiva o disattiva la modalità di trascinamento della selezione](#enable-disable-drag-and-drop)
* [Selezione di Assets](#selection-of-assets)
* [Personalizzare le risorse scadute](#customize-expired-assets)
* [Filtro di chiamata contestuale](#contextual-invocation-filter)
* [dragOptions, proprietà](#drag-options-property)

È necessario definire i prerequisiti nel file **index.html** o in un file simile nell&#39;implementazione dell&#39;applicazione per definire i dettagli di autenticazione per accedere all&#39;archivio [!DNL Experience Manager Assets]. Al termine, puoi aggiungere snippet di codice in base alle tue esigenze.

## Personalizzare il pannello dei filtri {#customize-filter-panel}

È possibile aggiungere il seguente frammento di codice nell&#39;oggetto `assetSelectorProps` per personalizzare il pannello dei filtri:

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

## Personalizzare le informazioni nella vista modale {#customize-info-in-modal-view}

Puoi personalizzare la visualizzazione dei dettagli di una risorsa facendo clic sull&#39;icona ![info](assets/info-icon.svg). Esegui il codice seguente:

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path')
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

## Attiva o disattiva la modalità di trascinamento della selezione {#enable-disable-drag-and-drop}

Aggiungi le seguenti proprietà a `assetSelectorProp` per abilitare la modalità di trascinamento. Per disattivare il trascinamento, sostituire il parametro `true` con `false`.

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

## Selezione di Assets {#selection-of-assets}

Il tipo di risorsa selezionato è un array di oggetti che contiene le informazioni della risorsa quando si utilizzano le funzioni `handleSelection`, `handleAssetSelection`, e `onDrop`.

Per configurare la selezione di una o più risorse, effettua le seguenti operazioni:

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

**Sintassi dello schema**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'https://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

Nella tabella seguente vengono descritte alcune delle proprietà importanti dell’oggetto Risorsa selezionata.

| Proprietà | Tipo | Descrizione |
|---|---|---|
| *archivio:repositoryId* | stringa | Identificatore univoco dell’archivio in cui è memorizzata la risorsa. |
| *archivio:id* | stringa | Identificatore univoco della risorsa. |
| *archivio:assetClass* | stringa | La classificazione della risorsa (ad esempio immagine o video, documento). |
| *archivio:name* | stringa | Nome della risorsa, inclusa l’estensione del file. |
| *archivio:size* | numero | Dimensione della risorsa in byte. |
| *archivio:path* | stringa | Posizione della risorsa all’interno dell’archivio. |
| *archivio:ancestors* | `Array<string>` | Array di elementi predecessori per la risorsa nell’archivio. |
| *archivio:state* | stringa | Stato corrente della risorsa nell’archivio (ad esempio attiva, eliminata e così via). |
| *archivio:createdBy* | stringa | Utente o sistema che ha creato la risorsa. |
| *archivio:createDate* | stringa | La data e l’ora in cui è stata creata la risorsa. |
| *archivio:modifiedBy* | stringa | Utente o sistema che ha modificato per ultimo la risorsa. |
| *archivio:modifyDate* | stringa | La data e l’ora dell’ultima modifica apportata alla risorsa. |
| *dc:format* | stringa | Il formato della risorsa, ad esempio il tipo di file (ad esempio, JPEG, PNG e così via). |
| *tiff:imageWidth* | numero | Larghezza di una risorsa. |
| *tiff:imageLength* | numero | Altezza di una risorsa. |
| *computedMetadata* | `Record<string, any>` | Oggetto che rappresenta un bucket per tutti i metadati di tutti i tipi di risorsa (archivio, applicazione o metadati incorporati). |
| *_collegamenti* | `Record<string, any>` | Collegamenti ipermediali della risorsa associata. Include collegamenti a risorse quali metadati e rappresentazioni. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition>`* | `Array<Object>` | Array di oggetti contenenti informazioni sulle rappresentazioni della risorsa. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].href>`* | stringa | URI della rappresentazione. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].type>`* | stringa | Tipo MIME della rappresentazione. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].repo:size>`* | numero | Dimensione della rappresentazione in byte. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].width>`* | numero | Larghezza della rappresentazione. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].height>`* | numero | Altezza della rappresentazione. |

### Gestione della selezione di risorse tramite lo schema a oggetti {#handling-selection}

La proprietà `handleSelection` viene utilizzata per gestire selezioni singole o multiple di risorse nel Selettore risorse. L’esempio seguente indica la sintassi di utilizzo di `handleSelection`.

![handle-selection](assets/handling-selection.png)

### Disabilitazione della selezione di Assets {#disable-selection}

La funzione Disattiva selezione viene utilizzata per nascondere o disabilitare la selezione delle risorse o cartelle. La casella di controllo di selezione viene nascosta dalla scheda o dalla risorsa, che ne impedisce la selezione. Per utilizzare questa funzione, puoi dichiarare la posizione di una risorsa o cartella che desideri disabilitare in un array. Ad esempio, se vuoi disattivare la visualizzazione di una cartella in prima posizione, puoi aggiungere il seguente codice:
`disableSelection: [0]:folder`

Puoi fornire all’array un elenco di tipi mime (ad esempio immagine, cartella, file o altri tipi mime come immagine/jpeg) che desideri disabilitare. I tipi MIME dichiarati sono mappati negli attributi `data-card-type` e `data-card-mimetype` di una risorsa.

Inoltre, Assets con selezione disabilitata è trascinabile. Per disattivare il trascinamento di un particolare tipo di risorsa, puoi utilizzare la proprietà `dragOptions.allowList`.

La sintassi per disabilitare la selezione è la seguente:

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> Nel caso di una risorsa, la casella di controllo di selezione è nascosta, mentre nel caso di una cartella, la cartella non è selezionabile ma viene ancora visualizzata la navigazione della cartella indicata.

<!--For a complete list of properties and detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

## Personalizzare le risorse scadute {#customize-expired-assets}

Il selettore risorse consente di controllare l’utilizzo di una risorsa scaduta. Puoi personalizzare la risorsa scaduta con un distintivo **In scadenza** che ti aiuterà a conoscere in anticipo le risorse che scadranno entro 30 giorni dalla data corrente. Inoltre, questo può essere personalizzato in base al requisito. Puoi anche consentire la selezione di una risorsa scaduta nell’area di lavoro o viceversa. La personalizzazione di una risorsa scaduta può essere eseguita utilizzando alcuni snippet di codice in vari modi:

<!--{
    getExpiryStatus: function, // to control Expired/Expiring soon badges of the asset
    allowSelectionAndDrag: boolean, // set true to allow the selection of expired assets on canvas, set false, otherwise.
}-->

```
expiryOptions: {
    getExpiryStatus: getExpiryStatus;
}
```

### Selezione di una risorsa scaduta {#selection-of-expired-asset}

Puoi personalizzare l’utilizzo di una risorsa scaduta per renderla selezionabile o non selezionabile. Puoi personalizzare se desideri consentire o meno il trascinamento di una risorsa scaduta nell’area di lavoro del Selettore risorse. A questo scopo, utilizza i seguenti parametri per rendere una risorsa non selezionabile sull’area di lavoro:

```
expiryOptions:{
    allowSelectionAndDrop: false;
}
```

<!--
Additionally, To do this, navigate to **[!UICONTROL Disable default expiry behavior]** under the [!UICONTROL Controls] tab and set the boolean value to `true` or `false` as per the requirement. If `true` is selected, you can see the select box over the expired asset, otherwise it remains unselected. You can hover to the info icon of an asset to know the details of an expired asset. 

![Disable default expiry behavior](assets/disable-default-expiry-behavior.png)-->

### Impostazione della durata di una risorsa scaduta {#set-duration-of-expired-asset}

Il seguente frammento di codice ti aiuta a impostare il badge **In scadenza** per le risorse che scadranno nei prossimi cinque giorni: <!--The `expirationDate` property is used to set the expiration duration of an asset. Refer to the code snippet below:-->

```
/**
  const getExpiryStatus = async (asset) => {
  if (!asset.expirationDate) {
    return null;
  }
  const currentDate = new Date();
  const millisecondsInDay = 1000 * 60 * 60 * 24;
  const fiveDaysFromNow = new Date(value: currentDate.getTime() + 5 * millisecondsInDay);
  const expirationDate = new Date(asset.expirationDate);
  if (expirationDate.getTime() < currentDate.getTime()) {
    return 'EXPIRED';
  } else if (expirationDate.getTime() < fiveDaysFromNow.getTime()) {
    return 'EXPIRING_SOON';
  } else {
    return 'NOT_EXPIRED';
  }
};
```

<!--In the above code snippet, the `getExpiryStatus` function is used to show the **Expiring soon** badge that have expiration date stored in `customExpirationDate`. Additionally, it sets the expiration date of an asset to five days from the current date. The `millisecondsInDay` helps you set expiry of an asset by specifying the time range in milliseconds. You can replace milliseconds with hours directly or customize function as per the requirement. Whereas, the `getTime()` function returns the number of milliseconds for the mentioned date. See [properties](#asset-selector-properties) to know about `expirationDate` property.-->

Fai riferimento all’esempio seguente per comprendere come funziona la proprietà per recuperare la data e l’ora correnti:

```
const currentData = new Date();
currentData.getTime(),
```

restituisce `1718779013959` come nel formato di data 2024-06-19T06:36:53.959Z.

### Personalizzare il messaggio popup di una risorsa scaduta {#customize-toast-message}

La proprietà `showToast` viene utilizzata per personalizzare il messaggio popup da visualizzare su una risorsa scaduta.

Sintassi:

```
{
    type: 'ERROR', 'NEUTRAL', 'INFO', 'SUCCESS',
    message: '<message to be shown>',
    timeout: optional,
}
```

Il timeout predefinito è di 500 millisecondi. Mentre, è possibile modificarlo in base al requisito. Inoltre, se si passa il valore `timeout: 0`, l&#39;avviso popup rimane aperto fino a quando non si fa clic sul pulsante incrociato.

Di seguito è riportato un esempio per visualizzare un messaggio popup quando è necessario non consentire la selezione di una cartella e visualizzare un messaggio corrispondente:

```
const showToast = {
    type: 'ERROR',
    message: 'Folder cannot be selected',
    timeout: 5000,
}
```

Utilizza il seguente frammento di codice per visualizzare un messaggio popup per l’utilizzo di una risorsa scaduta:

```
(args) => {
    const [selectedAssets, setSelectedAssets] = useState([]);
    const [showToast, setShowToast] = React.useState(false);
    const handleAssetSelection = (assets) => {
        let directorySelectedFlag = false;
        const temp = assets.filter((asset) => {
            if (asset['repo:assetClass'] === 'directory') {
                directorySelectedFlag = true;
                setShowToast(true);
            }
            return !(asset['repo:assetClass'] === 'directory');
        });
        if (!directorySelectedFlag) {
            setShowToast(false);
        }
        setSelectedAssets(temp);
    };
    return (
        <ASDialogWrapper
            {...args}
            showToast={showToast ? args.showToast : null}
            selectedAssets={selectedAssets}
            handleAssetSelection={handleAssetSelection}
        />
    );
}
```

## Filtro di chiamata contestuale{#contextual-invocation-filter}

Il selettore risorse consente di aggiungere un filtro per la selezione dei tag. Supporta un gruppo di tag che combina tutti i tag pertinenti a un particolare gruppo di tag. Inoltre, ti consente di selezionare altri tag corrispondenti alla risorsa che stai cercando. Inoltre, puoi anche impostare i gruppi di tag predefiniti sotto il filtro di chiamata contestuale, che vengono utilizzati principalmente da te in modo che siano accessibili da te in movimento.

>
>
> * Per abilitare il filtro di assegnazione tag nella ricerca, è necessario aggiungere lo snippet di codice di chiamata contestuale.
> * È obbligatorio utilizzare la proprietà name corrispondente al tipo di gruppo di tag `(property=xcm:keywords.id=)`.

Sintassi:

```
const filterSchema=useMemo(() => {
    return: [
        {
            element: 'taggroup',
            name: 'property=xcm:keywords.id='
        },
    ];
}, []);
```

Per aggiungere gruppi di tag nel pannello filtri, è necessario aggiungere almeno un gruppo di tag come impostazione predefinita. Inoltre, utilizza lo snippet di codice seguente per aggiungere i tag predefiniti preselezionati dal gruppo di tag.

```
export const WithAssetTags = (props) = {
const [selectedTags, setSelectedTags] = useState (
new Set(['orientation', 'color', 'facebook', 'experience-fragments:', 'dam', 'monochrome'])
const handleSelectTags = (selected) => {
setSelectedTags (new Set (selected)) ;
};
const filterSchema = useMemo ((); => {
    return {
        schema: [
            ｛
                fields: [
                    {
                    element: 'checkbox', 
                    name: 'property=xcm:keywords=', 
                    defaultValue: Array. from(selectedTags), 
                    options: assetTags, 
                    orientation: 'vertical',
                    },
                ],
    header: 'Asset Tags', 
    groupkey: 'AssetTagsGroup',
        ],
    },
｝；
}, [selectedTags]);
```

![filtro gruppo tag](assets/tag-group.gif)

## Carica nel selettore risorse {#upload-in-asset-selector}

Puoi caricare file o cartelle in Asset Selector dal file system locale. Per caricare i file utilizzando il file system locale, in genere è necessario utilizzare una funzione di caricamento fornita da una micro applicazione front-end Asset Selector. `upload` Vari snippet di codice necessari per richiamare il caricamento nel selettore risorse includono:

* [Frammento di codice modulo caricamento di base](#basic-upload)
* [Carica configurazione](#upload-config)
* [Carica con metadati](#upload-with-metadata)
* [Caricamento personalizzato](#customized-upload)
* [Carica utilizzando origini di terze parti](#upload-using-third-party-source)

### Modulo di caricamento di base {#basic-upload}

```
import { AllInOneUpload } from '@assets/upload';
import { TextField, ContextualHelp } from '@adobe/react-spectrum';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

export const UploadExample = () => {
    return (
        <>
            <TextField
                marginStart="size-200"
                width="size-6000"
                isDisabled={true}
                label="Target Upload Path"
                value={targetUploadPath}
                contextualHelp={
                    <ContextualHelp>
                        <Content>Use Storybook Controls panel to change the default upload location</Content>
                    </ContextualHelp>
                }
            />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
            />
        <>
    )
}
```

### Carica configurazione {#upload-config}

```
uploadConfig: {
        onUploadStart: action('onUploadStart'),
        onUploadComplete: action('onUploadComplete'),
        metadataSchema: [
            {
                mapToProperty: 'dam:assetStatus',
                value: 'approved',
                element: 'hidden',
            },
        ],
        ... more properties
     }, 
```

*Altre proprietà includono `metadataSchema`, `onMetadataFormChange`, `targetUploadPath`, `hideUploadButton`, `onUploadStart`, `importSettings` `onUploadComplete`, `onFilesChange`,`uploadingPlaceholder`*. Per ulteriori informazioni, consulta [Proprietà selettore risorse](#asset-selector-properties.md).

### Carica con metadati {#upload-with-metadata}

```
import { AllInOneUpload } from '@assets/upload';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

/**
 * see https://git.corp.adobe.com/CQ/assets-upload/blob/main/packages/@assets/upload/stories/data/SampleMetadataSchemas.ts
 * for full schema shape used in rendered example below
 */
const metadataSchema = [
    {
        mapToProperty: 'gmo:lineofBusiness',
        label: 'Line of Business',
        placeholder: 'Select one',
        required: true,
        element: 'dropdown',
        dropdownOptions: [
            {
                id: 'corporate',
                name: 'Corporate',
            },
            {
                id: 'digital-media-dme',
                name: 'Digital Media (DMe)',
            },
            {
                id: 'digital-experience-dx',
                name: 'Digital Experience (DX)',
            },
            {
                id: 'business-solutions',
                name: 'Business Solutions',
            },
        ],
    },
    // ... see link above for full schema
    {
        mapToProperty: 'dam:assetStatus',
        value: 'approved',
        // hidden metadata element, this metadata will be applied to the asset without rendering UI for user input
        element: 'hidden',
    },
];

const handleMetadataFormChange = (event: MetadataChangeEvent) => {
    const { property, value } = event;

    console.log({ property, value });
}

const UploadExampleWithMetadataForm = () => {
    return (
        <AllInOneUpload
            repositoryId={repoId}
            apiToken={apiToken}
            targetUploadPath={targetUploadPath}
            metadataSchema={sampleMetadataSchema}
            onMetadataFormChange={handleMetadataFormChange}
        />
    )
}
```

### Caricamento personalizzato {#customized-upload}

```
const MultipleAllInOneUploadExample = () => {
    const mfeRef = React.useRef<{ iframeRef: { current: HTMLIFrameElement } }>(null);

    return (
        <>
            <Button
                onPress={() => UploadCoordinator.initiateUpload(mfeRef.current?.iframeRef?.current)}
            >
                External Initiate Upload
            </Button>
            <AllInOneUpload
                {...otherProps}
                ref={mfeRef}
            />
        <>
    );
}
```

### Carica utilizzando origini di terze parti {#upload-using-third-party-source}

```
import { useState, useRef } from 'react';
import { AllInOneUpload, UploadCoordinator } from '@assets/upload';
import { Button, Flex, Divider } from '@adobe/react-spectrum';
import { sampleMetadataSchema } from './SampleMetadataSchemas';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

const defaultFiles = [
    new File(['file-content'], 'Controlled File 1'),
    new File(['file-content-with-more'], 'Controlled File 2')
];

const ControlledUploadExample = () => {
    const [controlledFiles, setControlledFiles] = useState<File[]>(defaultFiles)
    const inputRef = React.useRef<HTMLInputElement>(null);

    const handleFileInputChange = useCallback((e: ChangeEvent<HTMLInputElement>) => {
        if (e.target.files) {
            setMyFiles([...e.target.files]);
        }
    }, []);

    return (
        <Flex height="100%" alignItems="center" direction="column">
            <Flex direction="row" alignItems="center" justifyContent="center">
                <Button
                    variant="accent"
                    onPress={() => UploadCoordinator.initiateUpload()}
                    isDisabled={files.length < 1}
                >
                    External Initiate Upload
                </Button>
                <Button
                    variant="secondary"
                    onPress={() => {
                        inputRef.current?.click();
                    }}
                >
                    External Browse files
                </Button>
            </Flex>
            <Divider size="M" marginTop="size-200" />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
                files={controlledFiles}
                onFilesChange={setControlledFiles}
                hideUploadButton={true}
                metadataSchema={sampleMetadataSchema}
            />
            <input
                ref={inputRef}
                type="file"
                style={{ display: 'none' }}
                onChange={handleFileInputChange}
                multiple={true}
            />
        </Flex>
    )
}
```

### dragOptions, proprietà {#drag-options-property}

```
dragOptions: {
            allowList: {
                '*': true,          // allow all types to be dragged
                'folder': false,    // except those explicitly set to disallow
                'image/jpeg': false // or those with specific mimeTypes
            },
         }
```

>[!MORELIKETHIS]
>
>* [Proprietà del Selettore risorse](/help/assets/asset-selector-properties.md)
>* [Integrare il Selettore risorse con varie applicazioni](/help/assets/integrate-asset-selector.md)
>* [Proprietà del Selettore risorse](/help/assets/asset-selector-properties.md)
>* [Integrare il Selettore risorse con Dynamic Media con funzionalità OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
