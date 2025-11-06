---
title: Riferimenti sviluppatore per  [!DNL Assets]
description: API [!DNL Assets] e contenuti di riferimento per sviluppatori consentono di gestire le risorse, inclusi file binari, metadati, rappresentazioni, commenti e  [!DNL Content Fragments].
contentOwner: AG
feature: Assets HTTP API
role: Developer, Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager Assets] casi d&#39;uso per sviluppatori, API e materiale di riferimento {#assets-cloud-service-apis}

L&#39;articolo contiene consigli, materiali di riferimento e risorse per gli sviluppatori di [!DNL Assets] come [!DNL Cloud Service]. Include un nuovo modulo di caricamento delle risorse, un riferimento API e informazioni sul supporto fornito nei flussi di lavoro di post-elaborazione.

## [!DNL Experience Manager Assets] API e operazioni {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service] fornisce diverse API per interagire in modo programmatico con le risorse digitali. Ogni API supporta casi d’uso specifici, come indicato nella tabella seguente. L&#39;interfaccia utente [!DNL Assets], l&#39;app desktop [!DNL Experience Manager] e [!DNL Adobe Asset Link] supportano tutte o alcune operazioni.

>[!CAUTION]
>
>Alcune API continuano a esistere ma non sono supportate attivamente (indicate con un ×). Per quanto possibile, non utilizzare queste API.

| Livello di supporto | Descrizione |
| ------------- | --------------------------- |
| ✓ | Funzione supportata |
| × | Non supportato. Non utilizzare. |
| - | Non disponibile |

| Caso d’uso | [aem-upload](https://github.com/adobe/aem-upload) | [API Java Experience Manager / Sling / JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | [Servizio Asset Compute](https://experienceleague.adobe.com/it/docs/asset-compute/using/extend/understand-extensibility) | [[!DNL Assets] API HTTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Servlet Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=it) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **File binario originale** |  |  |  |  |  |  |
| Crea originale | ✓ | × | - | × | × | - |
| Leggi originale | - | × | ✓ | ✓ | ✓ | - |
| Aggiorna originale | ✓ | × | ✓ | × | × | - |
| Elimina originale | - | ✓ | - | ✓ | ✓ | - |
| Copia originale | - | ✓ | - | ✓ | ✓ | - |
| Sposta originale | - | ✓ | - | ✓ | ✓ | - |
| **Metadati** |  |  |  |  |  |  |
| Creare i metadati | - | ✓ | ✓ | ✓ | ✓ | - |
| Leggi metadati | - | ✓ | - | ✓ | ✓ | - |
| Aggiornare i metadati | - | ✓ | ✓ | ✓ | ✓ | - |
| Elimina metadati | - | ✓ | ✓ | ✓ | ✓ | - |
| Copia metadati | - | ✓ | - | ✓ | ✓ | - |
| Sposta metadati | - | ✓ | - | ✓ | ✓ | - |
| **Frammenti di contenuto (CF)** |  |  |  |  |  |  |
| Crea CF | - | ✓ | - | ✓ | - | - |
| Lettura CF | - | ✓ | - | ✓ | - | ✓ |
| Aggiorna CF | - | ✓ | - | ✓ | - | - |
| Elimina CF | - | ✓ | - | ✓ | - | - |
| Copia CF | - | ✓ | - | ✓ | - | - |
| Sposta CF | - | ✓ | - | ✓ | - | - |
| **Versioni** |  |  |  |  |  |  |
| Crea versione | ✓ | ✓ | - | - | - | - |
| Versione di lettura | - | ✓ | - | - | - | - |
| Elimina versione | - | ✓ | - | - | - | - |
| **Cartelle** |  |  |  |  |  |  |
| Crea cartella | ✓ | ✓ | - | ✓ | - | - |
| Leggi cartella | - | ✓ | - | ✓ | - | - |
| Elimina cartella | ✓ | ✓ | - | ✓ | - | - |
| Copia cartella | ✓ | ✓ | - | ✓ | - | - |
| Sposta cartella | ✓ | ✓ | - | ✓ | - | - |

## Caricamento della risorsa {#asset-upload}

In [!DNL Experience Manager] come [!DNL Cloud Service], puoi caricare direttamente le risorse nell&#39;archiviazione cloud utilizzando l&#39;API HTTP. Di seguito sono riportati i passaggi per caricare un file binario. Eseguire questi passaggi in un&#39;applicazione esterna e non nella JVM [!DNL Experience Manager].

1. [Invia una richiesta HTTP](#initiate-upload). Indica a [!DNL Experience Manage] la distribuzione dell&#39;intento di caricare un nuovo binario.
1. [PUT il contenuto del file binario](#upload-binary) in uno o più URI forniti dalla richiesta di avvio.
1. [Inviare una richiesta HTTP](#complete-upload) per informare il server che il contenuto del binario è stato caricato correttamente.

![Panoramica del protocollo di caricamento binario diretto](assets/add-assets-technical.png)

>[!IMPORTANT]
>
>Eseguire i passaggi precedenti in un&#39;applicazione esterna e non nella JVM [!DNL Experience Manager].

L’approccio offre una gestione scalabile e più performante dei caricamenti di risorse. Le differenze rispetto a [!DNL Experience Manager] 6.5 sono:

* I file binari non passano attraverso [!DNL Experience Manager], che ora coordina semplicemente il processo di caricamento con l&#39;archiviazione cloud binaria configurata per la distribuzione.
* L’archiviazione cloud binaria funziona con una rete CDN (Content Delivery Network) o Edge. Una rete CDN seleziona un endpoint di caricamento più vicino a un client. Quando i dati vengono trasferiti a una distanza inferiore da un endpoint vicino, le prestazioni di caricamento e l’esperienza utente migliorano, in particolare per i team distribuiti geograficamente.

>[!NOTE]
>
>Consulta il codice client per implementare questo approccio nella [libreria aem-upload](https://github.com/adobe/aem-upload) open-source.
>
>[!IMPORTANT]
>
>In alcune circostanze, le modifiche potrebbero non propagarsi completamente tra le richieste ad Experience Manager a causa della natura infine coerente dello storage in Cloud Service. Questo porta a 404 risposte per avviare o completare chiamate di caricamento a causa della mancata propagazione delle creazioni della cartella richieste. I clienti devono aspettarsi risposte 404 e gestirle implementando un nuovo tentativo con una strategia di back-off.

### Avvia caricamento {#initiate-upload}

Invia una richiesta HTTP POST alla cartella desiderata. Assets vengono creati o aggiornati in questa cartella. Includere il selettore `.initiateUpload.json` per indicare che la richiesta deve avviare il caricamento di un file binario. Ad esempio, il percorso della cartella in cui deve essere creata la risorsa è `/assets/folder`. La richiesta POST è `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

Il tipo di contenuto del corpo della richiesta deve essere `application/x-www-form-urlencoded` dati modulo, contenenti i campi seguenti:

* `(string) fileName`: obbligatorio. Nome della risorsa visualizzato in [!DNL Experience Manager].
* `(number) fileSize`: obbligatorio. Dimensione file, in byte, della risorsa caricata.

È possibile utilizzare una singola richiesta per avviare caricamenti per più file binari, purché ogni file binario contenga i campi obbligatori. In caso di esito positivo, la richiesta risponde con un codice di stato `201` e un corpo contenente dati JSON nel seguente formato:

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` (stringa): chiama questo URI al termine del caricamento del binario. L’URI può essere assoluto o relativo e i client devono essere in grado di gestirlo. Il valore può essere `"https://[aem_server]:[port]/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"` Vedere [caricamento completo](#complete-upload).
* `folderPath` (stringa): percorso completo della cartella in cui viene caricato il file binario.
* `(files)` (array): elenco di elementi la cui lunghezza e ordine corrispondono alla lunghezza e all&#39;ordine dell&#39;elenco di informazioni binarie fornite nella richiesta di avvio.
* `fileName` (stringa): nome del file binario corrispondente, come specificato nella richiesta di avvio. Questo valore deve essere incluso nella richiesta completa.
* `mimeType` (stringa): tipo mime del binario corrispondente, come specificato nella richiesta di avvio. Questo valore deve essere incluso nella richiesta completa.
* `uploadToken` (stringa): token di caricamento per il file binario corrispondente. Questo valore deve essere incluso nella richiesta completa.
* `uploadURIs` (array): elenco di stringhe i cui valori sono URI completi in cui caricare il contenuto del binario (vedere [Carica binario](#upload-binary)).
* `minPartSize` (numero): la lunghezza minima, in byte, dei dati che possono essere forniti a uno qualsiasi dei `uploadURIs`, se sono presenti più URI.
* `maxPartSize` (numero): la lunghezza massima, in byte, dei dati che possono essere forniti a uno qualsiasi dei `uploadURIs`, se è presente più di un URI.

### Carica binario {#upload-binary}

L’output dell’avvio di un caricamento include uno o più valori URI di caricamento. Se viene fornito più di un URI, il client può suddividere il binario in parti ed effettuare richieste PUT di ciascuna parte agli URI di caricamento forniti, nell&#39;ordine. Se scegli di dividere il binario in parti, attieniti alle seguenti linee guida:

* Ogni parte, ad eccezione dell&#39;ultima, deve essere di dimensioni maggiori o uguali a `minPartSize`.
* Ogni parte deve essere di dimensione minore o uguale a `maxPartSize`.
* Se le dimensioni del file binario superano `maxPartSize`, dividere il file binario in parti per caricarlo.
* Non è necessario utilizzare tutti gli URI.

Se le dimensioni del file binario sono inferiori o uguali a `maxPartSize`, è possibile caricare l&#39;intero file binario in un unico URI di caricamento. Se viene fornito più di un URI di caricamento, utilizza il primo e ignora il resto. Non è necessario utilizzare tutti gli URI.

I nodi edge CDN consentono di accelerare il caricamento richiesto di dati binari.

Il modo più semplice per eseguire questa operazione consiste nell&#39;utilizzare il valore di `maxPartSize` come dimensione della parte. Il contratto API garantisce che siano presenti URI di caricamento sufficienti per caricare il file binario se utilizzi questo valore come dimensione della parte. A tale scopo, dividere il binario in parti di dimensione `maxPartSize`, utilizzando un URI per ogni parte, nell&#39;ordine. La parte finale può essere di qualsiasi dimensione minore o uguale a `maxPartSize`. Si supponga, ad esempio, che la dimensione totale del file binario sia 20.000 byte, che `minPartSize` sia 5.000 byte, che `maxPartSize` sia 8.000 byte e che il numero di URI di caricamento sia 5. Esegui i passaggi seguenti:

* Carica i primi 8.000 byte del file binario utilizzando l’URI del primo caricamento.
* Carica i secondi 8.000 byte del file binario utilizzando il secondo URI di caricamento.
* Carica gli ultimi 4.000 byte del file binario utilizzando il terzo URI di caricamento. Poiché questa è la parte finale, non deve essere maggiore di `minPartSize`.
* Non è necessario utilizzare gli ultimi due URI di caricamento. Puoi ignorarli.

Un errore comune consiste nel calcolare la dimensione della parte in base al numero di URI di caricamento forniti dall’API. Il contratto API non garantisce il corretto funzionamento di questo approccio e può determinare dimensioni delle parti non comprese nell&#39;intervallo tra `minPartSize` e `maxPartSize`. Questo può causare errori di caricamento binario.

Anche in questo caso, il modo più semplice e sicuro consiste nell&#39;utilizzare parti di dimensioni uguali a `maxPartSize`.

Se il caricamento ha esito positivo, il server risponde a ogni richiesta con un codice di stato `201`.

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;algoritmo di caricamento, consulta la [documentazione ufficiale sulle funzioni](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) e la [documentazione API](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) nel progetto Apache Jackrabbit Oak.

### Caricamento completo {#complete-upload}

Dopo aver caricato tutte le parti di un file binario, invia una richiesta HTTP POST all’URI completo fornito dai dati di avvio. Il tipo di contenuto del corpo della richiesta deve essere `application/x-www-form-urlencoded` dati modulo, contenenti i campi seguenti.

| Campi | Tipo | Obbligatorio o no | Descrizione |
|---|---|---|---|
| `fileName` | Stringa | Obbligatorio | Nome della risorsa, fornito dai dati di avvio. |
| `mimeType` | Stringa | Obbligatorio | Il tipo di contenuto HTTP del binario, fornito dai dati di avvio. |
| `uploadToken` | Stringa | Obbligatorio | Carica il token per il file binario, fornito dai dati di avvio. |
| `createVersion` | Booleano | Facoltativo | Se `True` e una risorsa con il nome specificato esistono, [!DNL Experience Manager] crea una nuova versione della risorsa. |
| `versionLabel` | Stringa | Facoltativo | Se viene creata una nuova versione, l’etichetta associata alla nuova versione di una risorsa. |
| `versionComment` | Stringa | Facoltativo | Se viene creata una nuova versione, i commenti associati alla versione. |
| `replace` | Booleano | Facoltativo | Se `True` e una risorsa con il nome specificato esistono, [!DNL Experience Manager] elimina la risorsa e la ricrea. |
| `uploadDuration` | Numero | Facoltativo | Tempo totale, in millisecondi, per il caricamento dell&#39;intero file. Se specificato, la durata del caricamento viene inclusa nei file di registro del sistema per l&#39;analisi della velocità di trasferimento. |
| `fileSize` | Numero | Facoltativo | Dimensione in byte del file. Se specificato, la dimensione del file viene inclusa nei file di registro del sistema per l&#39;analisi della velocità di trasferimento. |

>[!NOTE]
>
>Se la risorsa esiste e non è specificato né `createVersion` né `replace`, [!DNL Experience Manager] aggiorna la versione corrente della risorsa con il nuovo binario.

Analogamente al processo di avvio, i dati completi della richiesta possono contenere informazioni relative a più file.

Il processo di caricamento di un file binario non viene eseguito finché non viene richiamato l’URL completo del file. Una risorsa viene elaborata al termine del processo di caricamento. L’elaborazione non viene avviata anche se il file binario della risorsa è stato caricato completamente, ma il processo di caricamento non è stato completato. Se il caricamento ha esito positivo, il server risponde con un codice di stato `200`.

### Esempio di script della shell per caricare le risorse in AEM as a Cloud Service {#upload-assets-shell-script}

Il processo di caricamento a più passaggi per l&#39;accesso binario diretto all&#39;interno di AEM as a Cloud Service è illustrato nel seguente esempio di script shell `aem-upload.sh`:

```bash
#!/bin/bash

# Check if pv is installed
if ! command -v pv &> /dev/null; then
    echo "Error: 'pv' command not found. Please install it before running the script."
    exit 1
fi

# Check if jq is installed
if ! command -v jq &> /dev/null; then
    echo "Error: 'jq' command not found. Please install it before running the script."
    exit 1
fi

# Set DEBUG to true to enable debug statements
DEBUG=true

# Function for printing debug statements
function debug() {
    if [ "${DEBUG}" = true ]; then
        echo "[DEBUG] $1"
    fi
}

# Function to check if a file exists
function file_exists() {
    [ -e "$1" ]
}

# Function to check if a path is a directory
function is_directory() {
    [ -d "$1" ]
}

# Check if the required number of parameters are provided
if [ "$#" -ne 4 ]; then
    echo "Usage: $0 <aem-url> <asset-folder> <file-to-upload> <bearer-token>"
    exit 1
fi

AEM_URL="$1"
ASSET_FOLDER="$2"
FILE_TO_UPLOAD="$3"
BEARER_TOKEN="$4"

# Extracting file name or folder name from the file path
NAME=$(basename "${FILE_TO_UPLOAD}")

# Step 1: Check if "file-to-upload" is a folder
if is_directory "${FILE_TO_UPLOAD}"; then
    echo "Uploading files from the folder recursively..."
    
    # Recursively upload files in the folder
    find "${FILE_TO_UPLOAD}" -type f | while read -r FILE_PATH; do
        FILE_NAME=$(basename "${FILE_PATH}")
        debug "Uploading file: ${FILE_PATH}"
        
        # You can choose to initiate upload for each file here
        # For simplicity, let's assume you use the same ASSET_FOLDER for all files
        ./aem-upload.sh "${AEM_URL}" "${ASSET_FOLDER}" "${FILE_PATH}" "${BEARER_TOKEN}"
    done
else
    # "file-to-upload" is a single file
    FILE_NAME="${NAME}"

    # Step 2: Calculate File Size
    FILE_SIZE=$(stat -c %s "${FILE_TO_UPLOAD}")

    # Step 3: Initiate Upload
    INITIATE_UPLOAD_ENDPOINT="${AEM_URL}/content/dam/${ASSET_FOLDER}.initiateUpload.json"

    debug "Initiating upload..."
    debug "Initiate Upload Endpoint: ${INITIATE_UPLOAD_ENDPOINT}"
    debug "File Name: ${FILE_NAME}"
    debug "File Size: ${FILE_SIZE}"

    INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
        -d "fileName=${FILE_NAME}" \
        -d "fileSize=${FILE_SIZE}" \
        ${INITIATE_UPLOAD_ENDPOINT})

    # Continue with the rest of the script...
fi


# Check if the response body contains the specified HTML content for a 404 error
if echo "${INITIATE_UPLOAD_RESPONSE}" | grep -q "<title>404 Specified folder not found</title>"; then
    echo "Folder not found. Creating the folder..."

    # Attempt to create the folder
    CREATE_FOLDER_ENDPOINT="${AEM_URL}/api/assets/${ASSET_FOLDER}"

    debug "Creating folder..."
    debug "Create Folder Endpoint: ${CREATE_FOLDER_ENDPOINT}"

    CREATE_FOLDER_RESPONSE=$(curl -X POST \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -d '{"class":"'${ASSET_FOLDER}'","properties":{"title":"'${ASSET_FOLDER}'"}}' \
        ${CREATE_FOLDER_ENDPOINT})

    # Check the response code and inform the user accordingly
    STATUS_CODE_CREATE_FOLDER=$(echo "${CREATE_FOLDER_RESPONSE}" | jq -r '.properties."status.code"')
    case ${STATUS_CODE_CREATE_FOLDER} in
        201)
            echo "Folder created successfully. Initiating upload again..."

            # Retry Initiate Upload after creating the folder
            INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
                -H "Authorization: Bearer ${BEARER_TOKEN}" \
                -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
                -d "fileName=${FILE_NAME}" \
                -d "fileSize=${FILE_SIZE}" \
                ${INITIATE_UPLOAD_ENDPOINT})
            ;;
        409)
            echo "Error: Folder already exists."
            ;;
        412)
            echo "Error: Precondition failed. Root collection cannot be found or accessed."
            exit 1
            ;;
        500)
            echo "Error: Internal Server Error. Something went wrong."
            exit 1
            ;;
        *)
            echo "Error: Unexpected response code ${STATUS_CODE_CREATE_FOLDER}"
            exit 1
            ;;
    esac
fi

# Extracting values from the response
FOLDER_PATH=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.folderPath')
UPLOAD_URIS=($(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadURIs[]'))
UPLOAD_TOKEN=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadToken')
MIME_TYPE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].mimeType')
MIN_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].minPartSize')
MAX_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].maxPartSize')
COMPLETE_URI=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.completeURI')

# Extracting "Affinity-cookie" from the response headers
AFFINITY_COOKIE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | grep -i 'Affinity-cookie' | awk '{print $2}')

debug "Folder Path: ${FOLDER_PATH}"
debug "Upload Token: ${UPLOAD_TOKEN}"
debug "MIME Type: ${MIME_TYPE}"
debug "Min Part Size: ${MIN_PART_SIZE}"
debug "Max Part Size: ${MAX_PART_SIZE}"
debug "Complete URI: ${COMPLETE_URI}"
debug "Affinity Cookie: ${AFFINITY_COOKIE}"
if $DEBUG; then
    i=1
    for UPLOAD_URI in "${UPLOAD_URIS[@]}"; do
        debug "Upload URI $i: "$UPLOAD_URI
        i=$((i+1))
    done
fi


# Calculate the number of parts needed
NUM_PARTS=$(( (FILE_SIZE + MAX_PART_SIZE - 1) / MAX_PART_SIZE ))
debug "Number of Parts: $NUM_PARTS"

# Calculate the part size for the last chunk
LAST_PART_SIZE=$(( FILE_SIZE % MAX_PART_SIZE ))
if [ "${LAST_PART_SIZE}" -eq 0 ]; then
    LAST_PART_SIZE=${MAX_PART_SIZE}
fi

# Step 4: Upload binary to the blob store in parts
PART_NUMBER=1
for i in $(seq 1 $NUM_PARTS); do
    PART_SIZE=${MAX_PART_SIZE}
    if [ ${PART_NUMBER} -eq ${NUM_PARTS} ]; then
        PART_SIZE=${LAST_PART_SIZE}
        debug "Last part size: ${PART_SIZE}"
    fi

    PART_FILE="/tmp/${FILE_NAME}_part${PART_NUMBER}"

    # Creating part file 
    SKIP=$((PART_NUMBER - 1))
    SKIP=$((MAX_PART_SIZE * SKIP))
    dd if="${FILE_TO_UPLOAD}" of="${PART_FILE}"  bs="${PART_SIZE}" skip="${SKIP}" count="${PART_SIZE}" iflag=skip_bytes,count_bytes  > /dev/null 2>&1
    debug "Creating part file: ${PART_FILE} with size ${PART_SIZE}, skipping first ${SKIP} bytes."

    
    UPLOAD_URI=${UPLOAD_URIS[$PART_NUMBER-1]}

    debug "Uploading part ${PART_NUMBER}..."
    debug "Part Size: $PART_SIZE"
    debug "Part File: ${PART_FILE}"
    debug "Part File Size: $(stat -c %s "${PART_FILE}")"
    debug "Upload URI: ${UPLOAD_URI}"

    # Upload the part in the background
    if command -v pv &> /dev/null; then
        pv "${PART_FILE}" | curl --progress-bar -X PUT --data-binary "@-" "${UPLOAD_URI}" &
    else
        curl -# -X PUT --data-binary "@${PART_FILE}" "${UPLOAD_URI}" &
    fi

    PART_NUMBER=$((PART_NUMBER + 1))
done

# Wait for all background processes to finish
wait

# Step 5: Complete the upload in AEM
COMPLETE_UPLOAD_ENDPOINT="${AEM_URL}${COMPLETE_URI}"

debug "Completing the upload..."
debug "Complete Upload Endpoint: ${COMPLETE_UPLOAD_ENDPOINT}"

RESPONSE=$(curl -X POST \
    -H "Authorization: Bearer ${BEARER_TOKEN}" \
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
    -H "Affinity-cookie: ${AFFINITY_COOKIE}" \
    --data-urlencode "uploadToken=${UPLOAD_TOKEN}" \
    --data-urlencode "fileName=${FILE_NAME}" \
    --data-urlencode "mimeType=${MIME_TYPE}" \
    "${COMPLETE_UPLOAD_ENDPOINT}")
    
debug $RESPONSE

echo "File upload completed successfully."
```

### Libreria di caricamento open-source {#open-source-upload-library}

Per ulteriori informazioni sugli algoritmi di caricamento o per creare script e strumenti di caricamento, Adobe fornisce librerie e strumenti open source:

* [Libreria aem-upload open-source](https://github.com/adobe/aem-upload).
* [Strumento da riga di comando open-source](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
>
>La libreria di caricamento aem e lo strumento da riga di comando utilizzano entrambi la [libreria node-httptransfer](https://github.com/adobe/node-httptransfer/)

### API di caricamento risorse obsolete {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Il nuovo metodo di caricamento è supportato solo per [!DNL Adobe Experience Manager] come [!DNL Cloud Service]. Le API di [!DNL Adobe Experience Manager] 6.5 sono obsolete. I metodi relativi al caricamento o all’aggiornamento delle risorse o delle rappresentazioni (qualsiasi caricamento binario) sono obsoleti nelle seguenti API:

* [API HTTP EXPERIENCE MANAGER ASSETS](mac-api-assets.md)
* API Java `AssetManager`, come `AssetManager.createAsset(..)`, `AssetManager.createAssetForBinary(..)`, `AssetManager.getAssetForBinary(..)`, `AssetManager.removeAssetForBinary(..)`, `AssetManager.createOrUpdateAsset(..)`, `AssetManager.createOrReplaceAsset(..)`

>[!MORELIKETHIS]
>
>* [Libreria aem-upload open-source](https://github.com/adobe/aem-upload).
>* [Strumento da riga di comando open-source](https://github.com/adobe/aio-cli-plugin-aem).
>* [Documentazione di Apache Jackrabbit Oak per il caricamento diretto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).

## Flussi di lavoro di elaborazione e post-elaborazione delle risorse {#post-processing-workflows}

In [!DNL Experience Manager], l&#39;elaborazione delle risorse si basa sulla configurazione di **[!UICONTROL Profili elaborazione]** che utilizza [microservizi risorse](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). L’elaborazione non richiede estensioni per sviluppatori.

Per la configurazione del flusso di lavoro di post-elaborazione, utilizza i flussi di lavoro standard con estensioni e passaggi personalizzati.

## Supporto dei passaggi del flusso di lavoro nella post-elaborazione del flusso di lavoro {#post-processing-workflows-steps}

Se si esegue l&#39;aggiornamento da una versione precedente di [!DNL Experience Manager], è possibile utilizzare i microservizi delle risorse per elaborare le risorse. I microservizi per le risorse native per il cloud sono più semplici da configurare e utilizzare. Alcuni passaggi del flusso di lavoro utilizzati nel flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] nella versione precedente non sono supportati. Per ulteriori informazioni sulle classi supportate, vedere [Riferimento API Java o Java](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

I seguenti modelli di flusso di lavoro tecnico sono sostituiti dai microservizi per le risorse oppure il supporto non è disponibile:

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).