---
title: Selettore risorse per [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service]
description: Utilizza il Selettore risorse per cercare, trovare e recuperare i metadati e le rappresentazioni delle risorse all’interno dell’applicazione.
role: Admin, User
exl-id: 62b0b857-068f-45b7-9018-9c59fde01dc3
source-git-commit: 027922c304be9c36b600b04b264d571ea8ed60d4
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 34%

---

# Selettore risorse micro front-end {#Overview}

Il Selettore risorse micro front-end fornisce un’interfaccia utente che si integra facilmente con l’archivio di [!DNL Experience Manager Assets] in modo da poter sfogliare o cercare le risorse digitali disponibili nell’archivio e utilizzarle nell’esperienza di authoring dell’applicazione.

L’interfaccia utente micro front-end è resa disponibile nell’esperienza dell’applicazione utilizzando il pacchetto Selettore risorse. Eventuali aggiornamenti al pacchetto vengono importati automaticamente e l’ultimo Selettore risorse implementato viene caricato automaticamente all’interno dell’applicazione.

![Panoramica](assets/overview.png)

Il Selettore risorse offre molti vantaggi, tra cui:

* Semplicità di integrazione con le applicazioni [Adobe](/help/assets/integrate-asset-selector-adobe-app.md) o [non Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md) che utilizzano la libreria Vanilla JavaScript.
* Facile manutenzione poiché gli aggiornamenti al pacchetto Selettore risorse vengono automaticamente distribuiti nel selettore risorse disponibile per l’applicazione. Non sono necessari aggiornamenti all’interno dell’applicazione per caricare le modifiche più recenti.
* Facilità di personalizzazione grazie alle proprietà disponibili che controllano la visualizzazione del Selettore risorse all’interno dell’applicazione.
* Filtri di ricerca full-text, predefiniti e personalizzati per passare rapidamente alle risorse da utilizzare nell’esperienza di authoring.
* Possibilità di cambiare archivi all’interno di un’organizzazione IMS per la selezione delle risorse.
* Possibilità di ordinare le risorse per nome, dimensioni e dimensioni e di visualizzarle in visualizzazione Elenco, Griglia, Raccolta o Cascata.

<!--Perform the following tasks to integrate and use Asset Selector with your [!DNL Experience Manager Assets] repository:

1. [Install Asset Selector](#installation)
2. [Integrate Asset Selector using Vanilla JS](#integration-using-vanilla-js)
3. [Use Asset Selector](#using-asset-selector)
-->

<!--
## Setting up Asset Selector {#asset-selector-setup}

![Asset Selector set up](assets/asset-selector-prereqs.png)
-->

## Prerequisiti{#prereqs}

Devi accertarti di utilizzare i seguenti metodi di comunicazione:

* L&#39;applicazione è in esecuzione su HTTPS.
* L’URL dell’applicazione si trova nell’elenco Consentiti degli URL di reindirizzamento del client IMS.
* Il flusso di accesso IMS viene configurato e renderizzato utilizzando un pop-up sul browser web. Pertanto, i popup devono essere abilitati o consentiti nel browser di destinazione.

Se hai bisogno del flusso di lavoro di autenticazione IMS di Asset Selector, utilizza i prerequisiti precedenti. In alternativa, se sei già autenticato con il flusso di lavoro IMS, puoi aggiungere le informazioni IMS.

**Ulteriori informazioni**

* [Integrare Asset Selector (Selettore risorse) con un’app di Adobe](/help/assets/integrate-asset-selector-adobe-app.md)
* [Integrare il selettore risorse con un’app non basata su Adobi](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [Integrare le API Dynamic Media Open di Asset Selector](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!IMPORTANT]
>
> Questo archivio funge da documentazione supplementare che descrive le API disponibili e alcuni esempi di utilizzo per l’integrazione di Asset Selector. Prima di installare o utilizzare il Selettore risorse, assicurati che all’organizzazione sia stato fornito l’accesso al Selettore risorse come parte del profilo Experience Manager Assets as a Cloud Service. Se non è stato eseguito il provisioning di, non è possibile integrare o utilizzare questi componenti. Per richiedere il provisioning, l’amministratore del programma deve generare un ticket di supporto contrassegnato come P2 dall’Admin Console e includere le seguenti informazioni:
>
>* Nomi di dominio in cui è ospitata l’applicazione che integra.
>* Dopo il provisioning, all&#39;organizzazione verranno forniti `imsClientId`, `imsScope` e un `redirectUrl` corrispondenti agli ambienti richiesti che sono essenziali per la configurazione di Asset Selector. Senza tali proprietà valide, non è possibile eseguire i passaggi di installazione.

## Installazione {#installation}

Il selettore risorse è disponibile tramite CDN ESM (ad esempio, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) e versione [UMD](https://github.com/umdjs/umd).

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

## Utilizzo del Selettore risorse {#using-asset-selector}

Dopo aver configurato il Selettore risorse ed aver effettuato l’autenticazione per utilizzarlo con l’applicazione [!DNL Adobe Experience Manager] as a [!DNL Cloud Service], puoi selezionare le risorse o eseguire varie altre operazioni per cercare le risorse all’interno dell’archivio.

![using-asset-selector](assets/using-asset-selector.png)

* **A**: [Nascondi/Mostra pannello](#hide-show-panel)
* **B**: [Selettore archivio](#repository-switcher)
* **C**: [Risorse](#repository)
* **D**: [Filtri](#filters)
* **E**: [Barra di ricerca](#search-bar)
* **F**: [Ordinamento](#sorting)
* **G**: [Ordinamento crescente o decrescente](#sorting)
* **H**: [Visualizzazione](#types-of-view)

### Nascondi/Mostra pannello {#hide-show-panel}

Per nascondere le cartelle nel menu di navigazione a sinistra, fare clic sull&#39;icona **[!UICONTROL Nascondi cartelle]**. Per annullare le modifiche, fai di nuovo clic sull’icona **[!UICONTROL Nascondi cartelle]**.

### Selettore archivio {#repository-switcher}

Asset Selector consente inoltre di cambiare archivi per la selezione delle risorse. Puoi selezionare l’archivio desiderato dal menu a discesa disponibile nel pannello a sinistra. Le opzioni dell’archivio disponibili nell’elenco a discesa si basano sulla proprietà `repositoryId` definita nel file `index.html`. Si basa sull’ambiente dell’organizzazione IMS selezionata a cui accede l’utente connesso. I consumatori possono trasmettere un `repositoryID` preferito e, in tal caso, il Selettore risorse interrompe il rendering del selettore archivio ed esegue il rendering solo delle risorse dall’archivio specificato.

### Archivio risorse

Si tratta di una raccolta di cartelle di risorse che puoi utilizzare per eseguire le operazioni.

### Filtri predefiniti {#filters}

Il Selettore risorse fornisce anche opzioni di filtro predefinite per perfezionare i risultati della ricerca. Sono disponibili i seguenti filtri:

* **[!UICONTROL Stato]:** include lo stato corrente della risorsa tra `all`, `approved`, `rejected` o `no status`.
* **[!UICONTROL Il tipo di file]:** include `folder`, `file`, `images`, `documents` o `video`.
* **[!UICONTROL Stato scadenza]:** fa riferimento alle risorse in base alla relativa durata di scadenza. È possibile selezionare la casella di controllo `[!UICONTROL Expired]` per filtrare le risorse scadute oppure impostare `[!UICONTROL Expiration Duration]` per visualizzare le risorse in base alla loro durata di scadenza. Quando una risorsa è già scaduta o sta per scadere, viene visualizzato un badge che illustra la stessa situazione. Inoltre, puoi controllare se consentire l’utilizzo (o il trascinamento) di una risorsa scaduta. Ulteriori informazioni su [personalizzare le risorse scadute](/help/assets/asset-selector-customization.md#customize-expired-assets). Per impostazione predefinita, il badge **In scadenza** viene visualizzato per le risorse che scadono nei successivi 30 giorni. È tuttavia possibile configurare la scadenza utilizzando la proprietà `expirationDate`.

  >[!TIP]
  >
  > Se desideri visualizzare o filtrare le risorse in base alla loro data di scadenza futura, indica l&#39;intervallo di date futuro nel campo `[!UICONTROL Expiration Duration]`. Visualizza le risorse con il badge **in scadenza**.

* **[!UICONTROL Tipo MIME]:** include `JPG`, `GIF`, `PPTX`, `PNG`, `MP4`, `DOCX`, `TIFF`, `PDF`, `XLSX`.
* **[!UICONTROL Dimensioni immagine]:** include la larghezza minima/massima e l&#39;altezza minima/massima dell&#39;immagine.

  ![rail-view-example](assets/filters-asset-selector.png)

### Ricerca personalizzata

Oltre alla ricerca full-text, Asset Selector consente di cercare le risorse all’interno dei file utilizzando la ricerca personalizzata. Puoi utilizzare filtri di ricerca personalizzati sia nella vista modale che nella vista della barra.

![custom-search](assets/custom-search1.png)

È inoltre possibile creare un filtro di ricerca predefinito per salvare i campi che si desidera cercare di frequente e utilizzarli in un secondo momento. Per creare una ricerca personalizzata delle risorse, puoi utilizzare la proprietà `filterSchema`.

### Barra di ricerca {#search-bar}

Il selettore risorse consente di eseguire una ricerca full-text delle risorse all’interno dell’archivio selezionato. Ad esempio, se digiti la parola chiave `wave` nella barra di ricerca, vengono mostrate tutte le risorse con la parola chiave `wave` menzionata in una qualsiasi delle proprietà dei metadati.

### Ordinamento {#sorting}

Puoi ordinare le risorse all’interno selettore risorse per nome, dimensione o dimensione di una risorsa. Puoi anche ordinare le risorse in ordine crescente o decrescente.

### Tipi di visualizzazione {#types-of-view}

Il selettore risorse consente di visualizzare la risorsa in quattro diverse visualizzazioni:

* **![visualizzazione elenco](assets/do-not-localize/list-view.png) [!UICONTROL Visualizzazione elenco]** La visualizzazione elenco visualizza i file e le cartelle scorrevoli in un&#39;unica colonna.
* **![visualizzazione griglia](assets/do-not-localize/grid-view.png) [!UICONTROL Visualizzazione griglia]** La visualizzazione griglia visualizza i file e le cartelle scorrevoli in una griglia di righe e colonne.
* **![visualizzazione raccolta](assets/do-not-localize/gallery-view.png) [!UICONTROL Visualizzazione raccolta]** La visualizzazione raccolta visualizza i file o le cartelle in un elenco orizzontale con blocco centrale.
* **![vista a cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL vista a cascata]** La vista a cascata visualizza file o cartelle sotto forma di Bridge.

**Grafico Panoramica**


## Ulteriori informazioni sulle funzionalità chiave {#key-capabilities-asset-selector}

<table>
<tr>
    <td>
        <img src="assets/integrate-asset-selector.gif" width="70px" height="70px" alt="Grafico Integrare selettore risorse"><br/>
        <a href="integrate-asset-selector.md">Integrare il selettore risorse</a>
        <p>
        <em>Scopri diverse funzionalità per integrare Asset Selector con più applicazioni.
        </p>
     </td>
    <td>
        <img src="assets/with-adobe-app.gif" width="70px" height="70px" alt="Grafico Integrare Asset Selector con Adobe Applications"><br/>
        <a href="integrate-asset-selector.md">Integrare Asset Selector con le applicazioni Adobe</a>
        <p>
        <em>Scopri come integrare Asset Selector con varie applicazioni Adobe.</em>
        </p>
    </td>
    <td>
        <img src="assets/third-party-app.gif" width="70px" height="70px" alt="Grafico Integrare selettore risorse"><br/>
        <a href="integrate-asset-selector.md">Integrare Asset Selector con applicazioni di terze parti</a>
        <p>
        <em>Scopri le funzionalità per integrare Asset Selector con applicazioni non Adobe.</em>
        </p>
    </td>
    <td>
        <img src="assets/with-dynamic-media-open-api.gif" width="70px" height="70px" alt="Grafico Integrare selettore risorse"><br/>
        <a href="integrate-asset-selector.md">Integrare Asset Selector con le API aperte di Dynamic Medie</a>
        <p>
        <em>Informazioni su come integrare Asset Selector con le API aperte di Dynamic Medie.</em>
        </p>
     </td>
     <td>
        <img src="assets/asset-selector-examples.gif" width="70px" height="70px" alt="Grafico delle proprietà di Asset Selector"><br/>
        <a href="asset-selector-customization.md">Proprietà selettore risorse</a>
        <p>
        <em>Scopri le nozioni di base per personalizzare vari componenti di Asset Selector, ad esempio filtri, selezione di risorse, risorse scadute e molto altro. </em>
        </p>
    </td>
</tr>
<tr>
    <td>
        <img src="assets/asset-selector-properties.gif" width="70px" height="70px" alt="Grafico di esempio di Asset Selector"><br/>
        <a href="asset-selector-customization.md">Esempi di selettore risorse</a>
        <p>
        <em>Comprendere l'utilizzo delle proprietà in modo pratico. </em>
        </p>
    </td>
    <td>
        <img src="assets/customize-asset-selector.gif" width="70px" height="70px" alt="Grafico Personalizza selettore risorse"><br/>
        <a href="asset-selector-customization.md">Personalizzazioni selettore risorse</a>
        <p>
        <em>Configura e personalizza vari componenti di Asset Selector in base alla tua usabilità. </em>
        </p>
    </td>
    <td>
        <img src="assets/asset-selector-upload.gif" width="70px" height="70px" alt="Grafico caricamento selettore risorse"><br/>
        <a href="asset-selector-upload.md">Caricamento selettore risorse</a>
        <p>
        <em>Scopri come caricare file o cartelle in Asset Selector dal file system locale o di terze parti. </em>
        </p>
    </td>
     <td>
        <img src="assets/asset-selector-collections.gif" width="70px" height="70px" alt="Grafico delle raccolte di Asset Selector"><br/>
        <a href="asset-selector-collections.md">Raccolte selettori risorse</a>
        <p>
        <em>Scopri come utilizzare le raccolte all'interno di Asset Selector utilizzando l'archivio Experience Manager. </em>
        </p>
    </td>
    <td>
    </td>
</tr>
</table>

>[!MORELIKETHIS]
>
>* [Personalizzazioni di Asset Selector](/help/assets/asset-selector-customization.md)
>* [Integrare Asset Selector con varie applicazioni](/help/assets/integrate-asset-selector.md)
>* [Proprietà selettore risorse](/help/assets/asset-selector-properties.md)
>* [Integrare Asset Selector con Dynamic Medie con funzionalità OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
