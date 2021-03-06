---
title: Cercare risorse digitali e immagini in [!DNL Adobe Experience Manager]
description: Scopri come trovare le risorse richieste in [!DNL Adobe Experience Manager] mediante il pannello Filtri e le modalità di utilizzo delle risorse visualizzate nella ricerca.
contentOwner: AG
mini-toc-levels: 1
feature: Search,Metadata,Asset Distribution
role: User,Admin
exl-id: 68bdaf25-cbd4-47b3-8e19-547c32555730
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '4897'
ht-degree: 6%

---

# Cercare risorse in [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] fornisce solidi metodi di individuazione delle risorse che consentono di raggiungere una maggiore velocità dei contenuti. I team possono ridurre i tempi di commercializzazione grazie a un’esperienza di ricerca intelligente e continua, utilizzando funzionalità predefinite e metodi personalizzati. La ricerca delle risorse è fondamentale per l’utilizzo di un sistema di gestione delle risorse digitali, sia per l’ulteriore utilizzo da parte dei creativi, per una gestione affidabile delle risorse da parte degli utenti aziendali e dei professionisti del marketing, sia per l’amministrazione da parte degli amministratori DAM. Ricerche semplici, avanzate e personalizzate che puoi eseguire tramite [!DNL Assets] l&#39;interfaccia utente o altre app e superfici aiutano a soddisfare questi casi d&#39;uso.

[!DNL Experience Manager Assets] supporta i seguenti casi d’uso e questo articolo descrive l’utilizzo, i concetti, le configurazioni, le limitazioni e la risoluzione dei problemi relativi a questi casi d’uso.

| Cercare risorse | Configurare e amministrare la funzionalità di ricerca | Utilizzare i risultati di ricerca |
|---|---|---|
| [Ricerche di base](#searchbasics) | [Indice di ricerca](#searchindex) | [Ordinare i risultati](#sort) |
| [Comprendere l’interfaccia utente di ricerca](#searchui) | [Estrazione di testo](#extracttextupload) | [Controllare le proprietà e i metadati di una risorsa](#checkinfo) |
| [Suggerimenti per la ricerca](#searchsuggestions) | [Metadati obbligatori](#mandatorymetadata) | [Scarica](#download) |
| [Comprendere i risultati e il comportamento della ricerca](#searchbehavior) | [Modificare i facet di ricerca](#searchfacets) | [Aggiornamenti in blocco dei metadati](#metadata-updates) |
| [Grado di ricerca e incremento](#searchrank) | [Predicati personalizzati](#custompredicates) | [Raccolte intelligenti](#collections) |
| [Ricerca avanzata: filtraggio e ambito di ricerca](#scope) |  | [Comprendere e risolvere i problemi di risultati imprevisti](#unexpected-results) |
| [Ricerca da altre soluzioni e app](#search-assets-other-surfaces):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[app desktop Experience Manager](#desktop-app)</li><li>[Immagini Adobe Stock](#adobe-stock)</li><li>[Risorse Dynamic Media](#search-dynamic-media-assets)</li></ul> |  |  |
| [Selettore risorse](#asset-picker) |  |  |
| [Limitazioni](#limitations) e [Suggerimenti](#tips) |  |  |
| [Esempi illustrati](#samples) |  |  |

Cerca le risorse utilizzando il campo Omnisearch nella parte superiore della [!DNL Experience Manager] interfaccia web. Vai a **[!UICONTROL Risorse]** > **[!UICONTROL File]** in [!DNL Experience Manager], fai clic su ![search_icon](assets/do-not-localize/search_icon.png) nella barra superiore, immetti parola chiave di ricerca e seleziona `Return`. In alternativa, utilizza la scelta rapida per parole chiave `/` (barra) per aprire il campo Omnisearch. `Location:Assets` è preselezionato per limitare le ricerche alle risorse DAM. [!DNL Experience Manager] fornisce suggerimenti durante la digitazione di una parola chiave di ricerca.

Utilizza la **[!UICONTROL Filtri]** per cercare risorse, cartelle, tag e metadati. Puoi filtrare i risultati della ricerca in base alle varie opzioni (predicati), ad esempio tipo di file, dimensione del file, data dell’ultima modifica, stato della risorsa, dati insights e licenze Adobe Stock. Puoi personalizzare il pannello Filtri e aggiungere o rimuovere i predicati di ricerca utilizzando [facet di ricerca](/help/assets/search-facets.md). La [!UICONTROL Tipo di file] nella [!UICONTROL Filtri] il pannello presenta caselle di controllo con stato misto. Pertanto, a meno che non si selezionino tutti i predicati (o formati) nidificati, le caselle di controllo di primo livello non vengono selezionate in parte.

[!DNL Experience Manager] La funzionalità di ricerca supporta la ricerca di raccolte e la ricerca di risorse all’interno di una raccolta. Vedi [raccolte di ricerca](/help/assets/manage-collections.md).

## Comprendere l’interfaccia di ricerca {#searchui}

Acquisisci familiarità con l’interfaccia di ricerca e le azioni disponibili.

![Interfaccia dei risultati di ricerca Experience Manager Assets](assets/aem_search_results.png)

*Figura: Comprendere [!DNL Experience Manager Assets] interfaccia dei risultati della ricerca.*

**A.** Salva la ricerca come raccolta avanzata. **B.** Filtri o predicati per limitare i risultati della ricerca. **C.** Visualizza file, cartelle o entrambi. **D.** Fai clic su Filtri per aprire o chiudere la barra a sinistra. **E.** Il percorso di ricerca è DAM. **F.** Campo di ricerca Omnisearch con la parola chiave di ricerca fornita dall’utente. **G.** Selezionare i risultati della ricerca caricata. **H.** Numero di risultati della ricerca visualizzati rispetto al totale dei risultati della ricerca. **I.** Chiudi la ricerca. **J.** Passa dalla vista a schede alla vista a elenco.

### Facet di ricerca dinamica {#dynamicfacets}

Puoi individuare più rapidamente le risorse desiderate dalla pagina dei risultati della ricerca utilizzando il numero dinamico aggiornato di risultati di ricerca previsti nei facet di ricerca. Il numero previsto di risorse viene aggiornato anche prima dell’applicazione del filtro di ricerca. La visualizzazione del conteggio previsto per il filtro consente di navigare nei risultati di ricerca in modo rapido ed efficiente.

![Visualizzare il numero approssimativo di risorse senza filtrare i risultati di ricerca nei facet di ricerca.](assets/asset_search_results_in_facets_filters.png)

*Figura: Visualizzare il numero approssimativo di risorse senza filtrare i risultati di ricerca nei facet di ricerca.*

## Ricerca suggerimenti durante la digitazione {#searchsuggestions}

Quando si inizia a digitare una parola chiave, in Experience Manager vengono suggerite le parole chiave o le frasi di ricerca possibili. I suggerimenti si basano sulle risorse nell’Experience Manager. L’Experience Manager indicizza tutti i campi di metadati per facilitarne la ricerca. Per fornire suggerimenti di ricerca, il sistema utilizza i valori dei seguenti pochi campi di metadati. Per fornire suggerimenti di ricerca, è consigliabile compilare i campi seguenti con le parole chiave appropriate:

* Tag delle risorse. (mappe a `jcr:content/metadata/cq:tags`)
* Titolo della risorsa. (mappe a `jcr:content/metadata/dc:title`)
* Descrizione della risorsa. (mappe a `jcr:content/metadata/dc:description`)
* Titolo nell’archivio JCR. Il valore può essere mappato sul titolo della risorsa. (mappe a `jcr:content/jcr:title`)
* Descrizione nell’archivio JCR. Il valore può essere mappato sulla descrizione della risorsa. (mappe a `jcr:content/jcr:description`)

## Comprendere i risultati e il comportamento della ricerca {#searchbehavior}

### Termini e risultati di ricerca di base {#searchbasics}

Puoi eseguire ricerche per parole chiave dal campo OmniSearch. La ricerca per parola chiave non distingue tra maiuscole e minuscole ed è una ricerca full-text (nei campi di metadati più comuni). Se vengono utilizzate più parole chiave, `AND` è l’operatore predefinito tra le parole chiave.

I risultati sono ordinati in base alla rilevanza, a partire dalle corrispondenze più vicine. Per più parole chiave, i risultati più rilevanti sono le risorse che contengono entrambi i termini nei relativi metadati. All’interno dei metadati, le parole chiave che compaiono come tag avanzati sono classificate più in alto rispetto alle parole chiave che compaiono in altri campi di metadati. [!DNL Experience Manager] consente di attribuire a un particolare termine di ricerca un peso maggiore. Inoltre, è possibile [aumentare il rango](#searchrank) di alcune risorse mirate per termini di ricerca specifici.

Per trovare rapidamente le risorse rilevanti, l’interfaccia avanzata fornisce meccanismi di filtraggio, ordinamento e selezione. Puoi filtrare i risultati in base a più criteri e visualizzare il numero di risorse ricercate per vari filtri. In alternativa, è possibile eseguire nuovamente la ricerca modificando la query nel campo Omnisearch . Quando modifichi i termini o i filtri di ricerca, gli altri filtri rimangono applicati per preservare il contesto della ricerca.

Quando i risultati sono molte risorse, [!DNL Experience Manager] visualizza i primi 100 nella vista a schede e i 200 nella vista a elenco. Quando gli utenti scorrono, vengono caricate più risorse. Questo per migliorare le prestazioni. Guarda una dimostrazione video della [numero di risorse visualizzate](https://www.youtube.com/watch?v=LcrGPDLDf4o).

A volte, nei risultati della ricerca potrebbero essere presenti alcune risorse impreviste. Per ulteriori informazioni, consulta [risultati imprevisti](#unexpected-results).

[!DNL Experience Manager] può cercare in molti formati di file e i filtri di ricerca possono essere personalizzati in base alle tue esigenze aziendali. Contatta l’amministratore per sapere quali opzioni di ricerca sono disponibili per l’archivio DAM e quali restrizioni ha l’account.

<!-- 
### Results with and without enhanced Smart Tags {#withsmarttags}

By default, [!DNL Experience Manager] search combines the search terms with an AND clause. For example, consider searching for keywords woman running. Only the assets with both woman and running keywords in the metadata appear in the search results by default. The same behavior is retained when special characters (periods, underscores, or dashes) are used with the keywords. The following search queries return the same results:

* `woman running`
* `woman.running`
* `woman-running`

However, the query `woman -running` returns assets without `running` in their metadata.
Using Smart Tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. So the search results are a combination of,

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Assets smart tagged with either of the keywords (Smart Tags behavior).
-->

### Classificazione e incremento della ricerca {#searchrank}

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a qualsiasi termine di ricerca negli smart tag. Nell’esempio precedente, l’ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. Corrisponde a `woman running` nei vari campi di metadati.
1. Corrisponde a `woman running` in smart tag.
1. Corrisponde a `woman` o `running` in smart tag.

Puoi migliorare la pertinenza delle parole chiave per particolari risorse per migliorare le ricerche in base alle parole chiave. In altre parole, le immagini per le quali promuovi parole chiave specifiche vengono visualizzate nella parte superiore dei risultati della ricerca quando esegui una ricerca in base a queste parole chiave.

1. Da [!DNL Assets] interfaccia utente, apri la pagina delle proprietà della risorsa. Fai clic su **[!UICONTROL Avanzate]** e fai clic su **[!UICONTROL Aggiungi]** sotto **[!UICONTROL Elevare per parole chiave di ricerca]**.
1. In **[!UICONTROL Search Promote]** specificare una parola chiave per la quale si desidera incrementare la ricerca dell&#39;immagine, quindi fare clic su **[!UICONTROL Aggiungi]**. È possibile specificare più parole chiave nello stesso modo.
1. Fai clic su **[!UICONTROL Salva e chiudi]**. La risorsa promossa per questa parola chiave viene visualizzata tra i primi risultati della ricerca.

Puoi usarlo a tuo vantaggio aumentando il rango di alcune risorse nei risultati della ricerca per la parola chiave target. Vedi il video di esempio qui sotto. Per informazioni dettagliate, consulta [cerca [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Video: Comprendere la classificazione dei risultati della ricerca e come influenzarli.*

## Ricerca avanzata {#scope}

[!DNL Experience Manager] fornisce vari metodi, come i filtri, applicabili alle risorse ricercate, per individuare più rapidamente le risorse desiderate. Di seguito sono descritti alcuni metodi comunemente utilizzati. Alcuni [esempi illustrati](#samples) sono condivisi di seguito.

**Cercare file o cartelle**: Nei risultati della ricerca, vedere file, cartelle o entrambi. Da **[!UICONTROL Filtri]** seleziona l’opzione appropriata. Vedi [interfaccia di ricerca](#searchui).

**Cercare risorse all’interno di una cartella**: È possibile limitare la ricerca a una cartella specifica. In **[!UICONTROL Filtri]** , aggiungi il percorso di una cartella. È possibile selezionare una sola cartella alla volta.

![Limitare i risultati della ricerca in una cartella aggiungendo un percorso della cartella nel pannello Filtri](assets/search_folder_select.gif)

*Figura: Limita i risultati della ricerca a una cartella aggiungendo un percorso di cartella nel pannello Filtri .*

### Trova immagini simili {#visualsearch}

Per trovare immagini visivamente simili a quelle selezionate dall’utente, fai clic su **[!UICONTROL Trova simili]** nella vista a schede di un’immagine o nella barra degli strumenti. [!DNL Experience Manager]Dall’archivio DAM,  visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. 

![Trova immagini simili utilizzando l’opzione nella vista a schede](assets/search_find_similar.png)

*Figura: Trova immagini simili utilizzando l’opzione nella vista a schede.*

### Immagini Adobe Stock {#adobe-stock}

Da all’interno di [!DNL Experience Manager] interfaccia utente, gli utenti possono cercare [Risorse Adobe Stock](/help/assets/aem-assets-adobe-stock.md) e concedere in licenza le risorse necessarie. Aggiungi `Location: Adobe Stock` nella barra Omnisearch. Puoi anche usare il pannello Filtri per trovare tutte le risorse con o senza licenza o per cercare una specifica risorsa utilizzando il numero di file Adobe Stock.

### Risorse Dynamic Media {#dmassets}

Per filtrare le immagini in base a Dynamic Media, dal pannello **[!UICONTROL Filtri]** seleziona **[!UICONTROL Dynamic Media]** > **[!UICONTROL Set]**. Filtra e visualizza le risorse come set di immagini, caroselli, set di file multimediali diversi e set 360 gradi.

### Ricerca GQL utilizzando valori specifici nei campi di metadati {#gql-search}

Puoi cercare le risorse in base ai valori esatti dei campi di metadati, ad esempio titolo, descrizione e creatore. La funzione di ricerca full-text GQL recupera solo le risorse il cui valore di metadati corrisponde esattamente alla query di ricerca. I nomi delle proprietà (Creatore, Titolo e così via) e dei valori sono sensibili all’uso di maiuscole e minuscole.

| Campo metadati | Valore e utilizzo dei facet |
|---|---|
| Titolo | title:John |
| Creatore | creatore:John |
| Dove si trova | posizione:NA |
| Descrizione | descrizione:&quot;Immagine campione&quot; |
| Strumento di creazione | creatortool: &quot;Adobe Photoshop&quot; |
| Proprietario copyright | copyrightowner: &quot;Adobe Systems&quot; |
| Collaboratore | collaboratore:John |
| Condizioni d&#39;uso | usageterms:&quot;CopyRights riservati&quot; |
| Creato | creato:AAAA-MM-DDTHH |
| Data di scadenza | scadenza:AAAA-MM-DDTHH |
| Ora di attivazione | ontime:YYYY-MM-DDTHH |
| Ora di disattivazione | tempo libero:AAAA-MM-DDTHH |
| Intervallo di tempo (dateontime di scadenza, offtime) | campo facet : in basso..superiore |
| Percorso | /content/dam/&lt;folder name=&quot;&quot;> |
| Titolo PDF | pdftitle:&quot;Documento di Adobe&quot; |
| Oggetto | oggetto: &quot;Formazione&quot; |
| Tag | tags:&quot;Località E Viaggi&quot; |
| Tipo | tipo:&quot;image\png&quot; |
| Larghezza immagine | larghezza:in basso.superiore |
| Altezza dell&#39;immagine | altezza:in basso.superiore |
| Utente | persona:John |

Proprietà `path`, `limit`, `size`e `orderby` non può essere combinato utilizzando `OR` con qualsiasi altra proprietà.

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

La parola chiave per una proprietà generata dall’utente è l’etichetta del relativo campo nell’editor delle proprietà in minuscolo, con gli spazi rimossi.

Di seguito sono riportati alcuni esempi di formati di ricerca per query complesse:

* Per visualizzare tutte le risorse con più campi facet (ad esempio: title=John Doe strumento creatore = Adobe Photoshop): `title:"John Doe" creatortool:Adobe*`
* Per visualizzare tutte le risorse quando il valore dei facet non è una singola parola ma una frase (ad esempio: title=Scott Reynolds): `title:"Scott Reynolds"`
* Per visualizzare le risorse con più valori di una singola proprietà (ad esempio: title=Scott Reynolds o John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Per visualizzare le risorse con valori di proprietà che iniziano con una stringa specifica (ad esempio: il titolo è Scott Reynolds): `title:Scott*`
* Per visualizzare le risorse con valori di proprietà che terminano con una stringa specifica (ad esempio: il titolo è Scott Reynolds): `title:*Reynolds`
* Per visualizzare le risorse con un valore di proprietà contenente una stringa specifica (ad esempio: title = Sala riunioni di Basilea): `title:*Meeting*`
* Per visualizzare le risorse che contengono una stringa particolare e hanno un valore di proprietà specifico (ad esempio: cerca Adobe stringa nelle risorse con title=John Doe): `*Adobe* title:"John Doe"`

## Cercare risorse da altri [!DNL Experience Manager] offerte o interfacce {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager] collega l’archivio DAM a varie altre [!DNL Experience Manager] soluzioni per fornire un accesso più rapido alle risorse digitali e semplificare i flussi di lavoro creativi. L’individuazione delle risorse inizia con ricerca o ricerca. Il comportamento di ricerca rimane sostanzialmente lo stesso tra le varie superfici e soluzioni. Alcuni metodi di ricerca cambiano a seconda del pubblico di destinazione, dei casi d’uso e dell’interfaccia utente [!DNL Experience Manager] soluzioni. I metodi specifici sono documentati per le singole soluzioni ai link seguenti. I suggerimenti e i comportamenti universalmente applicabili sono documentati in questo articolo.

### Cercare risorse dal pannello Asset Link di Adobe {#aal}

Utilizzando Adobe Asset Link, i creativi possono ora accedere ai contenuti archiviati in [!DNL Experience Manager Assets], senza uscire dalle app Adobe Creative Cloud supportate. I creativi possono sfogliare, cercare, estrarre e archiviare facilmente le risorse utilizzando il pannello in-app nella sezione [!DNL Adobe Creative Cloud] app: [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign]. Asset Link consente inoltre di cercare risultati visivamente simili. I risultati della ricerca visiva sono basati su algoritmi di apprendimento automatico di Adobe Sensei e consentono agli utenti di trovare immagini esteticamente simili. Vedi [cercare e sfogliare le risorse](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) utilizzo di Adobe Asset Link.

### Cercare risorse in [!DNL Experience Manager] app desktop {#desktop-app}

I creativi professionisti utilizzano l’app desktop per [!DNL Experience Manager Assets] facilmente ricercabili e disponibili sul desktop locale (Win o Mac). I creativi possono facilmente rivelare le risorse desiderate in Mac Finder o Esplora risorse, aperte nelle applicazioni desktop e modificate localmente - le modifiche vengono salvate in [!DNL Experience Manager] con una nuova versione creata nell’archivio. L&#39;applicazione supporta ricerche di base utilizzando una o più parole chiave, `*` e `?` caratteri jolly, e `AND` operatore. Vedi [sfogliare, cercare e visualizzare in anteprima le risorse](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) nell’app desktop.

### Cercare risorse in [!DNL Brand Portal] {#brand-portal}

Gli utenti e i professionisti del marketing del settore utilizzano Brand Portal per condividere in modo efficiente e sicuro le risorse digitali approvate con i team interni, i partner e i rivenditori estesi. Vedi [cercare risorse in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Ricerca [!DNL Adobe Stock] immagini {#adobe-stock1}

Da all’interno di [!DNL Experience Manager] nell’interfaccia utente, gli utenti possono cercare le risorse Adobe Stock e concedere in licenza le risorse richieste. Aggiungi `Location: Adobe Stock` nel campo Omnisearch. È inoltre possibile utilizzare **[!UICONTROL Filtri]** per trovare tutte le risorse con o senza licenza o per cercare una specifica risorsa utilizzando il numero di file Adobe Stock. Vedi [gestire [!DNL Adobe Stock] immagini in [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Ricerca [!DNL Dynamic Media] assets {#search-dynamic-media-assets}

Per filtrare le immagini in base a Dynamic Media, dal pannello **[!UICONTROL Filtri]** seleziona **[!UICONTROL Dynamic Media]** > **[!UICONTROL Set]**. Filtra e visualizza le risorse come set di immagini, caroselli, set di file multimediali diversi e set 360 gradi. Durante la creazione di pagine web, gli autori possono cercare i set direttamente da Content Finder. Nel menu pop-up è disponibile un filtro per i set.

### Cercare le risorse in Content Finder durante la creazione di pagine web {#content-finder}

Gli autori possono utilizzare Content Finder per cercare nell’archivio DAM le risorse pertinenti e utilizzarle nelle pagine web create. Gli autori possono inoltre utilizzare la funzionalità Risorse collegate per cercare le risorse disponibili in un sito remoto [!DNL Experience Manager] distribuzione. Gli autori possono quindi utilizzare queste risorse nelle pagine web di un sito locale [!DNL Experience Manager] distribuzione. Vedi [utilizzare risorse remote](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Raccolte di ricerca {#collections}

[!DNL Experience Manager] La funzionalità di ricerca supporta la ricerca di raccolte e la ricerca di risorse all’interno di una raccolta. Vedi [raccolte di ricerca](/help/assets/manage-collections.md).

## Selettore risorse {#asset-picker}

Selettore risorse (detto selettore risorse nelle versioni precedenti di [!DNL Adobe Experience Manager]) consente di cercare, filtrare e sfogliare le risorse DAM in modo speciale. Il selettore delle risorse è disponibile in `https://[aem_server]:[port]/aem/assetpicker.html`. Puoi recuperare i metadati delle risorse selezionate utilizzando il selettore delle risorse. Puoi avviarlo con i parametri di richiesta supportati, ad esempio il tipo di risorsa (immagine, video, testo) e la modalità di selezione (selezione singola o multipla). Questi parametri impostano il contesto del selettore delle risorse per una particolare istanza di ricerca e rimangono intatti per tutta la selezione.

Il selettore delle risorse utilizza HTML5 `Window.postMessage` messaggio per inviare i dati della risorsa selezionata al destinatario. Funziona solo in modalità Sfoglia e solo con la pagina dei risultati Omnisearch.

Passa i seguenti parametri di richiesta in un URL per avviare il selettore risorse in un particolare contesto:

| Nome | Valori | Esempio | Scopo |
|---|---|---|---|
| suffisso risorsa (B) | Percorso cartella come suffisso di risorsa nell’URL: [https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | Per avviare il selettore risorse con una particolare cartella selezionata, ad esempio con la cartella `/content/dam/we-retail/en/activities` selezionato, l’URL deve essere del modulo: `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | Se devi selezionare una particolare cartella all’avvio del selettore delle risorse, passala come suffisso di risorsa. |
| `mode` | singolo, multiplo | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | In modalità multipla, puoi selezionare più risorse contemporaneamente utilizzando il selettore delle risorse. |
| `dialog` | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Utilizza questi parametri per aprire il selettore delle risorse come finestra di dialogo Granite. Questa opzione è applicabile solo quando si avvia il selettore risorse tramite il campo del percorso Granite e lo si configura come URL pickerSrc. |
| `root` | &lt;folder_path> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | Utilizza questa opzione per specificare la cartella principale per il selettore di risorse. In questo caso, il selettore delle risorse consente di selezionare solo le risorse secondarie (dirette/indirette) sotto la cartella principale. |
| `viewmode` | ricerca |  | Per avviare il selettore delle risorse in modalità di ricerca, con `assettype` e `mimetype` Parametri. |
| `assettype` | Immagini, documenti, file multimediali, archivi. | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | Utilizza l’opzione per filtrare i tipi di risorse in base al valore fornito. |
| `mimetype` | Tipo MIME (`/jcr:content/metadata/dc:format`) di una risorsa (supportato anche dai caratteri jolly). | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | Utilizzalo per filtrare le risorse in base al tipo MIME. |

Per accedere all’interfaccia del selettore risorse, vai a `https://[aem_server]:[port]/aem/assetpicker`. Individua la cartella desiderata e seleziona una o più risorse. In alternativa, cerca la risorsa desiderata dalla casella Omnisearch, applica il filtro richiesto, quindi selezionalo.

![Sfoglia e seleziona la risorsa nel selettore risorse](assets/assetpicker.png)

*Figura: Sfoglia e seleziona la risorsa nel selettore delle risorse.*

## Limitazioni  {#limitations}

La funzionalità di ricerca in [!DNL Experience Manager Assets] presenta le seguenti limitazioni:

* Non inserire uno spazio iniziale nella query di ricerca, altrimenti la ricerca non funziona.
* [!DNL Experience Manager] potrebbe continuare a mostrare il termine di ricerca dopo aver selezionato le proprietà di una risorsa dai risultati della ricerca e quindi annullato la ricerca. <!-- (CQ-4273540) -->
* Durante la ricerca di cartelle, file e cartelle, i risultati della ricerca non possono essere ordinati su alcun parametro.
* Se si seleziona `Return` senza digitare nella barra omnisearch, [!DNL Experience Manager] restituisce un elenco di solo file e non cartelle. Se si cerca in modo specifico le cartelle senza utilizzare una parola chiave, [!DNL Experience Manager] non restituisce alcun risultato.
* È possibile eseguire ricerche full-text nelle cartelle. Specifica un termine di ricerca per il funzionamento della ricerca.

La ricerca visiva o la ricerca per similarità presenta le seguenti limitazioni:

* La ricerca visiva funziona meglio con un archivio di grandi dimensioni. Sebbene non vi sia un numero minimo di immagini necessarie per buoni risultati, la qualità delle corrispondenze con alcune immagini non è buona come le corrispondenze da un archivio di grandi dimensioni.
* Non è possibile modificare il modello o il treno [!DNL Experience Manager] per trovare immagini simili. Ad esempio, l’aggiunta o la rimozione di tag avanzati ad alcune risorse non modifica il modello. Le risorse vengono escluse dai risultati di ricerca visivamente simili.

La funzionalità di ricerca può presentare limitazioni delle prestazioni nei seguenti scenari:

* La vista a schede presenta un tempo di caricamento più veloce rispetto alla vista a elenco per visualizzare i risultati della ricerca.

## Suggerimenti per la ricerca {#tips}

* Quando monitori lo stato di revisione delle risorse, utilizza l’opzione appropriata per individuare le risorse approvate o quelle in attesa di approvazione.
* Utilizza il predicato Insights per cercare le risorse supportate in base alle statistiche di utilizzo ottenute da varie app Creative. I dati di utilizzo sono raggruppati in Punteggio di utilizzo, Impressioni, Clic e Canali multimediali in cui le risorse appaiono come categorie.
* Utilizza la **[!UICONTROL Seleziona tutto]** per selezionare le risorse ricercate. [!DNL Experience Manager] inizialmente visualizza 100 risorse nella vista a schede e 200 risorse nella vista a elenco. Quando scorri i risultati della ricerca, vengono caricate più risorse. Puoi selezionare più risorse rispetto alle risorse caricate. Il conteggio delle risorse selezionate viene visualizzato nell’angolo in alto a destra della pagina dei risultati della ricerca. Puoi utilizzare la selezione, ad esempio scaricare le risorse selezionate, aggiornare in blocco le proprietà dei metadati per le risorse selezionate o aggiungere le risorse selezionate a una raccolta. Quando selezioni più risorse rispetto alla visualizzazione, un’azione viene applicata a tutte le risorse selezionate oppure una finestra di dialogo visualizza il numero di risorse a cui viene applicata. Per applicare un’azione alle risorse che non sono state caricate, accertati che tutte le risorse siano selezionate in modo esplicito.
* Per cercare risorse che non contengono metadati obbligatori, consulta [metadati obbligatori](#mandatorymetadata).
* La ricerca utilizza tutti i campi di metadati. Una ricerca generica, ad esempio la ricerca di 12, in genere restituisce molti risultati. Per risultati migliori, utilizza virgolette doppie (non singole) o accertati che il numero sia contiguo a una parola senza un carattere speciale (ad esempio `shoe12`).
* La ricerca full-text supporta operatori quali `-` e `^`. Per cercare queste lettere come stringhe letterali, racchiudere l&#39;espressione di ricerca tra virgolette doppie. Ad esempio, utilizza `"Notebook - Beauty"` anziché `Notebook - Beauty`.
* Se i risultati della ricerca sono troppi, limita la [ambito di ricerca](#scope) a zero sulle risorse desiderate. Funziona meglio se hai qualche idea su come cercare meglio le risorse desiderate, ad esempio un tipo di file specifico, una posizione specifica, metadati specifici e così via.

* **Assegnazione tag**: I tag consentono di classificare le risorse che possono essere cercate e cercate in modo più efficiente. I tag consentono di propagare la tassonomia appropriata ad altri utenti e flussi di lavoro. [!DNL Experience Manager] offre metodi per assegnare automaticamente tag alle risorse utilizzando i servizi intelligenti artificialmente di Adobe Sensei, che consentono di assegnare tag sempre migliori alle risorse in base all’utilizzo e alla formazione. Quando cerchi delle risorse, i tag avanzati vengono inseriti nei factoring. Funziona insieme alla funzionalità di ricerca incorporata. Vedi [comportamento di ricerca](#searchbehavior). Per ottimizzare l’ordine in cui vengono visualizzati i risultati della ricerca, puoi [aumentare la classificazione di ricerca](#searchrank) di alcune risorse selezionate.

* **Indicizzazione**: Nei risultati della ricerca vengono restituiti solo i metadati e le risorse indicizzate. Per una migliore copertura e prestazioni, assicurati un’indicizzazione adeguata e segui le best practice. Vedi [indicizzazione](#searchindex).

## Alcuni esempi che illustrano la ricerca {#samples}

Utilizza virgolette doppie intorno alle parole chiave per trovare le risorse che contengono la frase esatta nell’ordine esatto specificato dall’utente.

![Comportamento di ricerca con e senza virgolette](assets/search_with_quotes.gif)

*Figura: Comportamento della ricerca con e senza virgolette.*

**Ricerca con carattere jolly asterisco**: Per ampliare la ricerca, utilizzare un asterisco prima o dopo la parola di ricerca per abbinare qualsiasi numero di caratteri. Ad esempio, la ricerca di un&#39;esecuzione senza asterisco non restituisce risorse contenenti varianti della parola (inclusi nei metadati). Un asterisco sostituisce qualsiasi numero di caratteri. Ad esempio:

* `run` restituisce le risorse con la parola chiave run esattamente
* `run*` restituisce le risorse con `running`, `run`, `runaway`e così via.
* `*run` restituisce le risorse con `outrun`, `rerun`e così via.
* `*run*` restituisce tutte le combinazioni possibili.

![Illustrazione dell’uso del carattere jolly asterisco nella ricerca delle risorse utilizzando un esempio](assets/search_with_asterisk_run.gif)

*Figura: Illustrazione dell’uso del carattere jolly asterisco nella ricerca delle risorse utilizzando un esempio.*

**Ricerca con carattere jolly punto interrogativo**: Per ampliare la ricerca, utilizza uno o più &#39;?&#39; caratteri che corrispondono al numero esatto di caratteri. Ad esempio, nell’illustrazione seguente,

* `run???` la query non corrisponde ad alcuna risorsa.

* `run????` la query corrisponde alla parola `running` con quattro caratteri dopo `run`.

* `??run` la query corrisponde alla parola `rerun` con due caratteri prima `run`.

![Illustrazione dell’uso del carattere jolly del punto interrogativo nella ricerca delle risorse utilizzando un esempio](assets/search_with_questionmark_run.gif)

*Figura: Illustrazione dell’uso del carattere jolly del punto interrogativo nella ricerca delle risorse utilizzando un esempio.*

**Escludere una parola chiave**: Usa il trattino per cercare le risorse che non contengono una parola chiave. Ad esempio: `running -shoe` la query restituisce le risorse che contengono `running`, ma non `shoe`. Analogamente, `camp -night` la query restituisce le risorse che contengono `camp` ma non `night`. Query `camp-night` restituisce le risorse che contengono entrambe `camp` e `night`.

![Utilizzo del trattino per cercare risorse non contenenti una parola chiave esclusa](assets/search_dash_exclude_keyword.gif)

*Figura: Utilizzo del trattino per cercare le risorse che non contengono una parola chiave esclusa.*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).
-->

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses Smart Tags. After configuring smart tagging functionality, follow these steps.

1. In [!DNL Experience Manager] CRXDE, in `/oak:index/lucene` node, add the following properties and values and save the changes.

    * `costPerEntry` property of type `Double` with the value `10`.

    * `costPerExecution` property of type `Double` with the value `2`.

    * `refresh` property of type `Boolean` with the value `true`.

   This configuration allows searches from the appropriate index.

1. To create Lucene index, in CRXDE, at `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, create node named `imageFeatures` of type `nt-unstructured`. In `imageFeatures` node,

    * Add `name` property of type `String` with the value `jcr:content/metadata/imageFeatures/haystack0`.

    * Add `nodeScopeIndex` property of type `Boolean` with the value of `true`.

    * Add `propertyIndex` property of type `Boolean` with the value of `true`.

    * Add `useInSimilarity` property of type `Boolean` with the value `true`.

   Save the changes.

1. Access `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` and add `similarityTags` property of type `Boolean` with the value of `true`.
1. Apply Smart Tags to the assets in your [!DNL Experience Manager] repository. See [how to configure smart tags](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html#configuring).
1. In CRXDE, in `/oak-index/damAssetLucene` node, set the `reindex` property to `true`. Save the changes.
1. (Optional) If you have customized search form then copy the `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` node to `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Save the changes.

For related information, see [understand smart tags in Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) and [how to manage smart tags](/help/assets/smart-tags.md).
-->

<!--
### Mandatory metadata {#mandatorymetadata}

Business users, administrators, or DAM librarians can define some metadata as mandatory metadata that is a must for the business processes to work. For various reasons, some assets may be missing this metadata, such as legacy assets or assets migrated in bulk. Assets with missing or invalid metadata are detected and reported based on the indexed metadata property. To configure it, see [mandatory metadata](/help/assets/metadata-schemas.md#defining-mandatory-metadata).

### Modify search facets {#searchfacets}

To improve the speed of discovery, [!DNL Experience Manager Assets] offers search facets using which you can filter the search results. The Filters panel includes a few standard facets by default. Administrators can customize the Filters panel to modify the default facets using the in-built predicates. [!DNL Experience Manager] provides a good collection of in-built predicates and an editor to customize the facets. See [search facets](/help/assets/search-facets.md).

### Extract text when uploading assets {#extracttextupload}

You can configure [!DNL Experience Manager] to extract the text from the assets when users upload assets, such as PSD or PDF files. [!DNL Experience Manager] indexes the extracted text and helps users search these assets based on the extracted text. See [upload assets](/help/assets/manage-digital-assets.md#uploading-assets).
-->

### Predicati personalizzati per filtrare i risultati della ricerca {#custompredicates}

I predicati vengono utilizzati per creare facet. Gli amministratori possono personalizzare i facet di ricerca nel pannello Filtri utilizzando predicati preconfigurati. Questi predicati possono essere personalizzati utilizzando le sovrapposizioni. Vedi [creare predicati personalizzati](/help/assets/search-facets.md).

Puoi cercare le risorse digitali in base a una o più delle seguenti proprietà. I filtri applicati ad alcune di queste proprietà sono disponibili per impostazione predefinita; altri filtri possono essere creati in modo personalizzato per essere applicati alle altre proprietà.

| Campo di ricerca | Valori delle proprietà di ricerca |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Tipi MIME | Immagini, Documenti, Multimedia, Archivi o Altro. |
| Ultima modifica | Ora, giorno, settimana, mese o anno. |
| Dimensione file | Piccolo, Medio o Grande. |
| Stato pubblicazione | Pubblicato o Non pubblicato. |
| Stato approvato | Approvato o rifiutato. |
| Orientamento | Orizzontale, Verticale o Quadrato. |
| Stile | Colore o Bianco e nero. |
| Altezza video | Specificato come valore minimo e massimo. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |
| Larghezza video | Specificato come valore minimo e massimo. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |
| Formato video | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Il valore viene memorizzato nei metadati del video sorgente e delle rappresentazioni. |
| Codec video | x264. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |
| Bitrate video | Specificato come valore minimo e massimo. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |
| Codec audio | Libvorbis, Lame MP3, Codifica AAC. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |
| Bitrate audio | Specificato come valore minimo e massimo. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |

## Utilizzare i risultati di ricerca delle risorse {#aftersearch}

Puoi effettuare le seguenti operazioni con le risorse che hai cercato [!DNL Experience Manager]:

* Visualizza le proprietà dei metadati e altre informazioni.
* Scarica una o più risorse.
* Utilizza Azioni desktop per aprire queste risorse nell’app desktop.
* Creare raccolte avanzate.

### Ordinare i risultati della ricerca {#sort}

Ordina i risultati della ricerca per individuare più rapidamente le risorse necessarie. Puoi ordinare i risultati della ricerca nella vista a elenco e solo quando selezioni **[[!UICONTROL File]](#searchui)** dal **[!UICONTROL Filtri]** pannello. [!DNL Assets] utilizza l’ordinamento lato server per ordinare rapidamente tutte le risorse all’interno di una cartella o nei risultati di una query di ricerca, indipendentemente dal numero. L’ordinamento lato server fornisce risultati più rapidi e precisi rispetto all’ordinamento lato client.

Nella vista a elenco, è possibile ordinare i risultati della ricerca in modo analogo all’ordinamento delle risorse in qualsiasi cartella. L’ordinamento funziona su queste colonne: Nome, Titolo, Stato, Dimension, Dimensioni, Valutazione, Utilizzo, Data creazione, Data modifica, Data pubblicazione, Flusso di lavoro e Estratto.

Per informazioni sulle limitazioni della funzionalità di ordinamento, consulta [limitazioni](#limitations).

### Controllare informazioni dettagliate su una risorsa {#checkinfo}

Puoi controllare informazioni dettagliate sulle risorse ricercate nella pagina dei risultati della ricerca.

Per visualizzare tutti i metadati di una risorsa, selezionala e fai clic su **[!UICONTROL proprietà]** dalla barra degli strumenti.

Per controllare i commenti relativi a una risorsa o alla sua cronologia della versione, fai clic sulla risorsa per aprirne l’anteprima di grandi dimensioni. Apri la timeline nella barra a sinistra e seleziona **[!UICONTROL Commenti]** o **[!UICONTROL Versioni]**. Puoi anche ordinare l’attività della timeline come commenti o versioni in ordine cronologico.

![Ordinare le voci della timeline per una risorsa di ricerca](assets/sort_timeline_search_results.gif)

*Figura: Ordina le voci della timeline per una risorsa di ricerca.*

### Scaricare le risorse cercate {#download}

Puoi scaricare le risorse cercate e i relativi rendering così come puoi scaricare le risorse normali dalle cartelle. Seleziona una o più risorse dai risultati della ricerca e fai clic su **[!UICONTROL Scarica]** dalla barra degli strumenti.

### Aggiornare in blocco le proprietà dei metadati {#metadata-updates}

È possibile eseguire aggiornamenti in blocco ai campi di metadati comuni di più risorse. Dai risultati della ricerca, seleziona una o più risorse. Fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti e aggiorna i metadati in base alle esigenze. Fai clic su **[!UICONTROL Salva e chiudi]** al termine. I metadati esistenti in precedenza nei campi aggiornati vengono sovrascritti.

Per le risorse disponibili in una singola cartella o raccolta, è più semplice [aggiornare i metadati in blocco](/help/assets/manage-metadata.md#manage-assets-metadata) senza utilizzare la funzionalità di ricerca. Per le risorse disponibili tra le cartelle o che corrispondono a un criterio comune, è più veloce aggiornare in massa i metadati tramite la ricerca.

### Raccolte intelligenti {#smart-collections}

Una raccolta è un set ordinato di risorse che possono includere risorse da posizioni diverse, perché le raccolte contengono solo riferimenti a tali risorse. Le raccolte sono di due tipi:

* Un elenco di riferimenti statici di risorse, cartelle e altre raccolte.
* Un elenco dinamico (raccolta avanzata) che popola le risorse nella raccolta in base a un criterio di ricerca.

Puoi creare raccolte avanzate in base ai criteri di ricerca. Dal pannello **[!UICONTROL Filtri]**, seleziona **[!UICONTROL File]** e fai clic su **[!UICONTROL Salva raccolta avanzata]**. Consulta la sezione [Gestisci raccolte](/help/assets/manage-collections.md).

## Risultati e problemi della ricerca imprevisti {#unexpected-results}

<!--
**Partially related or unrelated search results**: Experience Manager may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

| Errore, problemi, sintomi | Possibile motivo | Possibile correzione o comprensione del problema |
|---|---|---|
| Risultati errati durante la ricerca di risorse con metadati mancanti. | Durante la ricerca di risorse per le quali mancano i metadati obbligatori, [!DNL Experience Manager] potrebbero visualizzare alcune risorse con metadati validi. I risultati si basano sulla proprietà dei metadati indicizzati. | Dopo l’aggiornamento dei metadati, la reindicizzazione è necessaria per riflettere lo stato corretto dei metadati delle risorse. Vedi [metadati obbligatori](metadata-schemas.md#define-mandatory-metadata). |
| Troppi risultati di ricerca. | Parametro di ricerca ampio. | Considera la limitazione della [ambito di ricerca](#scope). L’utilizzo di smart tag può fornire più risultati di quanto previsto. Vedi [comportamento di ricerca con gli smart tag](#withsmarttags). |
| Risultati di ricerca non correlati o parzialmente correlati. | Il comportamento di ricerca cambia con l’assegnazione tag avanzati. | Comprendere [modifica della ricerca dopo l’assegnazione tag avanzati](#withsmarttags). |
| Nessun suggerimento di completamento automatico per le risorse. | Le nuove risorse caricate non sono ancora indicizzate. I metadati non sono immediatamente disponibili come suggerimenti quando si inizia a digitare una parola chiave di ricerca nella barra di Omnisearch. | [!DNL Experience Manager] attende la scadenza di un periodo di timeout (un’ora per impostazione predefinita) prima di eseguire un processo in background per indicizzare i metadati per tutte le risorse appena caricate o aggiornate e quindi aggiunge i metadati all’elenco dei suggerimenti. |
| Nessun risultato di ricerca. | <ul><li>Le risorse corrispondenti alla query non esistono. </li><li> Spazio vuoto aggiunto prima della query di ricerca. </li><li> Il campo di metadati non supportato contiene la parola chiave cercata.</li><li> Ricerca effettuata durante lo spegnimento di una risorsa. </li></ul> | <ul><li>Cerca utilizzando una parola chiave diversa. In alternativa, utilizza l’assegnazione tag avanzati o la ricerca per similarità per migliorare i risultati della ricerca. </li><li>[Limitazione nota](#limitations).</li><li>Tutti i campi di metadati non vengono considerati per le ricerche. Vedi [scope](#scope).</li><li>Puoi cercare in un secondo momento o modificare il tempo di attivazione e disattivazione delle risorse richieste.</li></ul> |
| Filtro di ricerca o predicato non disponibile. | <ul><li>Il filtro di ricerca non è configurato.</li><li>Non è disponibile per il tuo accesso.</li><li>(Meno probabile) Le opzioni di ricerca non vengono personalizzate sulla distribuzione in uso.</li></ul> | <ul><li>Contatta l’amministratore per verificare se le personalizzazioni della ricerca sono disponibili o meno.</li><li>Contatta l’amministratore per verificare se il tuo account dispone dei privilegi/delle autorizzazioni per utilizzare la personalizzazione.</li><li>Contatta l’amministratore e controlla le personalizzazioni disponibili per [!DNL Assets] distribuzione in uso.</li></ul> |
| Quando si cercano immagini visivamente simili, manca un’immagine prevista. | <ul><li>L&#39;immagine non è disponibile in [!DNL Experience Manager].</li><li>L&#39;immagine non è indicizzata. In genere, quando viene caricato di recente.</li><li>L&#39;immagine non è con tag avanzati.</li></ul> | <ul><li>Aggiungi l’immagine a [!DNL Assets].</li><li>Contattare l&#39;amministratore per reindicizzare il repository. Inoltre, assicurati di utilizzare l&#39;indice appropriato.</li><li>Contatta l’amministratore per assegnare tag avanzati alle risorse pertinenti.</li></ul> |
| Quando si cercano immagini visivamente simili, viene visualizzata un&#39;immagine irrilevante. | Comportamento della ricerca visiva. | [!DNL Experience Manager] visualizza il maggior numero possibile di risorse potenzialmente rilevanti. Eventuali immagini meno rilevanti vengono aggiunte ai risultati ma con una classificazione di ricerca più bassa. La qualità delle corrispondenze e la rilevanza delle risorse ricercate diminuiscono quando scorri verso il basso i risultati della ricerca. |
| Quando selezioni e operi sui risultati della ricerca, non vengono utilizzate tutte le risorse ricercate. | La [!UICONTROL Seleziona tutto] seleziona solo i primi 100 risultati di ricerca nella vista a schede e i primi 200 risultati di ricerca nella vista a elenco. |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] guida all’implementazione di ricerca](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Configurazione avanzata per migliorare i risultati della ricerca](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [Configurare la ricerca per la traduzione intelligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

