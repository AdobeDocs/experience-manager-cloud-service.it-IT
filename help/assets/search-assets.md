---
title: Cercare risorse digitali e immagini in [!DNL Adobe Experience Manager].
description: Scoprite come trovare le risorse necessarie [!DNL Adobe Experience Manager] nel pannello Filtri e come utilizzare le risorse visualizzate nella ricerca.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 7f9384b08df70aac2f425b830337e97d711b709e
workflow-type: tm+mt
source-wordcount: '4743'
ht-degree: 5%

---


# Cercare risorse in [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] fornisce solidi metodi di individuazione delle risorse che consentono di ottenere una maggiore velocità del contenuto. I team possono ridurre i tempi di immissione sul mercato grazie a un’esperienza di ricerca intelligente e senza soluzione di continuità, grazie alla funzionalità e ai metodi personalizzati. La ricerca delle risorse è fondamentale per l’utilizzo di un sistema di gestione delle risorse digitali, sia per l’ulteriore utilizzo da parte dei creativi, per una gestione affidabile delle risorse da parte degli utenti aziendali e degli esperti di marketing, sia per l’amministrazione da parte degli amministratori DAM. Ricerche semplici, avanzate e personalizzate che potete eseguire tramite l&#39;interfaccia [!DNL Assets] utente o altre app e superfici aiutano a soddisfare questi casi di utilizzo.

[!DNL Experience Manager Assets] supporta i seguenti casi d’uso e questo articolo descrive l’utilizzo, i concetti, le configurazioni, i limiti e la risoluzione dei problemi per questi casi d’uso.

| Cercare risorse | Configurazione e amministrazione | Utilizzo dei risultati di ricerca |
|---|---|---|
| [Ricerche di base](#searchbasics) | [Indice di ricerca](#searchindex) | [Ordinare i risultati](#sort) |
| [Comprendere l’interfaccia di ricerca](#searchui) |  | [Verificare le proprietà e i metadati di una risorsa](#checkinfo) |
| [Suggerimenti per la ricerca](#searchsuggestions) | [Metadati obbligatori](#mandatorymetadata) | [Scarica](#download) |
| [Comprendere i risultati della ricerca e il comportamento](#searchbehavior) | [Modificare i facet di ricerca](#searchfacets) | [Aggiornamenti di massa dei metadati](#metadataupdates) |
| [Classificazione e incremento della ricerca](#searchrank) | [Estrazione del testo](#extracttextupload) | [Raccolte intelligenti](#collections) |
| [Ricerca avanzata: filtraggio e ambito di ricerca](#scope) | [predicati personalizzati](#custompredicates) | [Comprendere e risolvere problemi relativi a risultati imprevisti](#unexpectedresults) |
| [Cerca da altre soluzioni e app](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[app desktop Experience Manager](#desktopapp)</li><li>[immagini Adobe Stock](#adobestock)</li><li>[Risorse per file multimediali dinamici](#dynamicmedia)</li></ul> |  |  |
| [Selettore risorse](#assetselector) |  |  |
| [Limitazioni](#tips) e [suggerimenti](#limitations) |  |  |
| [Esempi illustrati](#samples) |  |  |

Cercate le risorse utilizzando il campo Omnisearch nella parte superiore dell’interfaccia [!DNL Experience Manager] Web. Vai a **[!UICONTROL Risorse]** > **[!UICONTROL File]** in [!DNL Experience Manager], fai clic su ![search_icon](assets/do-not-localize/search_icon.png) nella barra superiore, immetti la parola chiave di ricerca e premi Invio. In alternativa, usate la scelta rapida per le parole chiave `/` (barra) per aprire il campo di ricerca Omnisearch. `Location:Assets` è preselezionata per limitare le ricerche alle risorse DAM. [!DNL Experience Manager] fornisce suggerimenti durante la digitazione iniziale di una parola chiave di ricerca.

Usate il pannello **[!UICONTROL Filtri]** per cercare risorse, cartelle, tag e metadati. Potete filtrare i risultati di ricerca in base alle varie opzioni (predicati), come il tipo di file, la dimensione del file, la data dell&#39;ultima modifica, lo stato della risorsa, i dati di approfondimento e  licenza Adobe Stock. Potete personalizzare il pannello Filtri e aggiungere o rimuovere i predicati di ricerca utilizzando i facet [di](/help/assets/search-facets.md)ricerca. Il filtro Tipo [!UICONTROL di] file nel pannello [!UICONTROL Filtri] dispone di caselle di controllo con più stati. Pertanto, a meno che non si selezionino tutti i predicati (o i formati) nidificati, le caselle di controllo di primo livello sono selezionate parzialmente.

[!DNL Experience Manager] la funzionalità di ricerca supporta la ricerca di raccolte e la ricerca di risorse all&#39;interno di una raccolta. Consultate [Cercare le raccolte](/help/assets/manage-collections.md).

## Comprendere l’interfaccia di ricerca {#searchui}

Acquisisci familiarità con l’interfaccia di ricerca e le azioni disponibili.

![Comprendere  Experience Manager Interfaccia dei risultati della ricerca Risorse](assets/aem_search_results.png)

*Figura: Comprendere l’interfaccia dei risultati della [!DNL Experience Manager Assets] ricerca.*

**A.** Salvate la ricerca come raccolta avanzata. **B.** Filtri o predicati per limitare i risultati della ricerca. **C.** Visualizzare file, cartelle o entrambi. **D.** Fai clic su Filtri per aprire o chiudere la barra a sinistra. **E.** Il percorso di ricerca è DAM. **F.** Campo di ricerca Omnisearch con parola chiave di ricerca fornita dall’utente. **G.** Selezionare i risultati di ricerca caricati. **H.** Numero di risultati della ricerca visualizzati rispetto al totale dei risultati della ricerca. **I.** Chiudi la ricerca. **J.** Passa dalla vista a scheda a quella a elenco.

### Facet di ricerca dinamici {#dynamicfacets}

Dalla pagina dei risultati della ricerca potete individuare più rapidamente le risorse desiderate utilizzando il numero dinamico di risultati di ricerca previsti nei facet di ricerca. Il numero previsto di risorse viene aggiornato anche prima dell’applicazione del filtro di ricerca. La visualizzazione del conteggio previsto rispetto al filtro consente di navigare nei risultati di ricerca in modo rapido ed efficiente.

![Visualizzate il numero approssimativo di risorse senza filtrare i risultati di ricerca nei facet di ricerca.](assets/asset_search_results_in_facets_filters.png)

*Figura: Visualizzate il numero approssimativo di risorse senza filtrare i risultati di ricerca nei facet di ricerca.*

## Search suggestions as you type {#searchsuggestions}

Quando si inizia a digitare una parola chiave, AEM suggerisce le parole chiave o frasi possibili da cercare. I suggerimenti si basano sulle risorse in AEM. AEM indicizza tutti i campi di metadati per facilitare la ricerca. Per fornire suggerimenti per la ricerca, il sistema utilizza i valori dei seguenti campi di metadati. Per fornire suggerimenti per la ricerca, è consigliabile compilare i campi seguenti con le parole chiave appropriate:

* Tag risorsa. (mappe a `jcr:content/metadata/cq:tags`)
* Titolo risorsa. (mappe a `jcr:content/metadata/dc:title`)
* Descrizione della risorsa. (mappe a `jcr:content/metadata/dc:description`)
* Titolo nell’archivio JCR. Il valore può essere mappato sul titolo della risorsa. (mappe a `jcr:content/jcr:title`)
* Descrizione nell’archivio JCR. Il valore può essere mappato sulla descrizione della risorsa. (mappe a `jcr:content/jcr:description`)

## Comprendere i risultati della ricerca e il comportamento {#searchbehavior}

### Termini e risultati di ricerca di base {#searchbasics}

Potete eseguire ricerche per parole chiave dal campo OmniSearch. La ricerca per parola chiave non fa distinzione tra maiuscole e minuscole ed è una ricerca full-text (nei più comuni campi di metadati). Se vengono utilizzate più parole chiave, `AND` è l&#39;operatore predefinito tra le parole chiave.

I risultati sono ordinati in base alla rilevanza, a partire da corrispondenze più simili. Per più parole chiave, i risultati più rilevanti sono le risorse che contengono entrambi i termini nei metadati. All’interno dei metadati, le parole chiave che appaiono come smart tag hanno una classificazione più alta rispetto alle parole chiave che vengono visualizzate in altri campi di metadati. [!DNL Experience Manager] consente di assegnare a un particolare termine di ricerca maggiore peso. Inoltre, è possibile [aumentare il rango](#searchrank) di alcune risorse con targeting per termini di ricerca specifici.

Per trovare rapidamente le risorse rilevanti, l’interfaccia avanzata offre meccanismi di filtraggio, ordinamento e selezione. Potete filtrare i risultati in base a più criteri e visualizzare il numero di risorse ricercate per vari filtri. In alternativa, potete eseguire nuovamente la ricerca modificando la query nel campo Omnisearch. Quando modificate i termini di ricerca o i filtri, gli altri filtri rimangono applicati per mantenere il contesto della ricerca.

Quando i risultati sono molte risorse, [!DNL Experience Manager] visualizza le prime 100 nella vista a schede e 200 nella vista a elenco. Quando gli utenti scorrono, vengono caricate più risorse. Questo per migliorare le prestazioni. Guardate un video dimostrativo del [numero di risorse visualizzate](https://www.youtube.com/watch?v=LcrGPDLDf4o).

In alcuni casi, nei risultati della ricerca potrebbero essere presenti risorse impreviste. Per ulteriori informazioni, consultate [risultati](#unexpectedresults)imprevisti.

AEM cercare in molti formati di file e i filtri di ricerca possono essere personalizzati in base alle esigenze aziendali. Contatta i tuoi amministratori per sapere quali opzioni di ricerca rendere disponibili per l’archivio DAM e quali potrebbero essere le restrizioni per l’accesso.

<!-- 
### Results with and without Enhanced Smart Tags {#withsmarttags}

By default, AEM search combines the search terms with an AND clause. For example, consider searching for keywords woman running. Only the assets with both woman and running keywords in the metadata appear in the search results by default. The same behavior is retained when special characters (periods, underscores, or dashes) are used with the keywords. The following search queries return the same results:

* `woman running`
* `woman.running`
* `woman-running`

However, the query `woman -running` returns assets without `running` in their metadata.
Using smart tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. So the search results are a combination of,

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Assets smart tagged with either of the keywords (Smart Tags behavior).
-->

### Classificazione e incremento della ricerca {#searchrank}

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a uno qualsiasi dei termini di ricerca negli smart tag. Nell&#39;esempio precedente, l&#39;ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. Corrisponde `woman running` ai vari campi di metadati.
1. Corrisponde a `woman running` negli smart tag.
1. Corrispondenza di `woman` o di `running` in smart tag.

Potete migliorare la rilevanza delle parole chiave per risorse particolari per migliorare le ricerche in base alle parole chiave. In altre parole, le immagini per le quali vengono promosse parole chiave specifiche vengono visualizzate nella parte superiore dei risultati della ricerca quando si esegue una ricerca basata su tali parole chiave.

1. From the [!DNL Assets] user interface, open the properties page for the asset. Click **[!UICONTROL Advanced]** and click **[!UICONTROL Add]** under **[!UICONTROL Elevate for search keywords]**.
1. Nella casella **[!UICONTROL Search Promote (Promuovi]** ricerca), specificate una parola chiave per la quale desiderate incrementare la ricerca dell&#39;immagine e fate clic su **[!UICONTROL Add (Aggiungi)]**. Potete specificare più parole chiave nello stesso modo.
1. Fai clic su **[!UICONTROL Salva e chiudi]**. La risorsa promossa per questa parola chiave viene visualizzata tra i primi risultati della ricerca.

Potete usarlo a proprio vantaggio aumentando il livello di alcune risorse nei risultati della ricerca per la parola chiave di destinazione. Guardate il video di esempio riportato di seguito. Per informazioni dettagliate, consultate [cercare in  Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Video: Come classificare i risultati della ricerca e come influenzarne la classificazione.*

## Advanced search {#scope}

AEM fornisce vari metodi, come i filtri applicabili alle risorse ricercate, per individuare più rapidamente le risorse desiderate. Di seguito sono descritti alcuni metodi di uso comune. Di seguito sono riportati alcuni esempi [](#samples) illustrati.

**Cercare file o cartelle**: Nei risultati della ricerca, consultate file, cartelle o entrambi. Dal pannello **[!UICONTROL Filtri]** , potete selezionare l’opzione appropriata. Consultate Interfaccia [di](#searchui)ricerca.

**Cercare risorse all’interno di una cartella**: Potete limitare la ricerca a una cartella specifica. Nel pannello **[!UICONTROL Filtri]** , aggiungete il percorso di una cartella. Potete selezionare una sola cartella alla volta.

![Limitare i risultati di ricerca in una cartella aggiungendo un percorso di cartella nel pannello Filtri](assets/search_folder_select.gif)

Limitare i risultati di ricerca in una cartella aggiungendo un percorso di cartella nel pannello Filtri

<!--
### Find similar images {#visualsearch}

To find images that are visually similar to a user-selected image, click **[!UICONTROL Find Similar]** option from the card view of an image or from the toolbar. AEM displays the smart tagged images from the DAM repository that are similar to a user-selected image. See [how to configure similarity search](#configvisualsearch).

![Find similar images using the option in the card view](assets/search_find_similar.png)
*Figure: Find similar images using the option in the card view*
-->

###  immagini Adobe Stock {#adobestock}

Dall’interfaccia utente AEM, gli utenti possono effettuare ricerche [risorse](/help/assets/aem-assets-adobe-stock.md) Adobe Stock e ottenere la licenza per le risorse necessarie. Aggiungete `Location: Adobe Stock` nella barra di ricerca Omnisearch. Potete anche usare il pannello Filtri per trovare tutte le risorse con o senza licenza o per cercare una risorsa specifica usando  numero di file Adobe Stock.

### Risorse per file multimediali dinamici {#dmassets}

Per filtrare le immagini in base a Dynamic Media, dal pannello **[!UICONTROL Filtri seleziona Dynamic Media]** > **[!UICONTROL Set]**. Filtra e visualizza le risorse come set di immagini, caroselli, set di file multimediali diversi e set 360 gradi.

### Ricerca utilizzando valori specifici nei campi di metadati {#gqlsearch}

Potete usare le risorse in base ai valori esatti di specifici campi di metadati, ad esempio titolo, descrizione e autore. La funzione di ricerca full-text GQL raccoglie solo le risorse il cui valore di metadati corrisponde esattamente alla query di ricerca. I nomi delle proprietà (ad esempio autore, titolo e così via) e i valori seguono la distinzione tra maiuscole e minuscole.

| Campo metadati | Valore e utilizzo dei facet |
|---|---|
| Titolo | title:John |
| Creatore | creatore:John |
| Dove si trova | posizione:NA |
| Descrizione | descrizione:&quot;Immagine campione&quot; |
| Strumento di creazione | creatortool:&quot;Adobe Photoshop CC 2015&quot; |
| Proprietario copyright | copyrightowner:&quot; Adobe Systems&quot; |
| Collaboratore | collaboratore:John |
| Condizioni d&#39;uso | usageterms:&quot;CopyRights Reserved&quot; |
| Creato | create:YYYY-MM-DDTHH |
| Data scadenza | expires:AAAA-MM-DTHH |
| Ora di attivazione | ontime:YYYY-MM-DTHH |
| Ora di disattivazione | offtime:AAAA-MM-DTHH |
| Intervallo di tempo (data di scadenza, ora di disattivazione) | campo facet : in basso..upperbound |
| Percorso | /content/dam/&lt;nome cartella> |
| Titolo PDF | pdftitle:&quot;Documento  Adobe&quot; |
| Oggetto | oggetto: &quot;Formazione&quot; |
| Tag | tags:&quot;Location And Travel&quot; |
| Tipo | type:&quot;image\png&quot; |
| Larghezza dell’immagine | width:lowerbound.upperbound |
| Altezza dell’immagine | height:lowerbound.upperbound |
| Person | persona:John |

Il percorso, il limite, la dimensione e l&#39;ordine delle proprietà non possono essere eseguiti in OR con altre proprietà.

La parola chiave per una proprietà generata dall&#39;utente è la relativa etichetta campo nell&#39;editor delle proprietà in lettere minuscole, con la rimozione degli spazi.

Di seguito sono riportati alcuni esempi di formati di ricerca per query complesse:

* Per visualizzare tutte le risorse con più campi facet (ad esempio: title=John Doe e strumento di creazione =  Adobe Photoshop): `title:"John Doe" creatortool : Adobe*`
* Per visualizzare tutte le risorse quando il valore dei facet non è una singola parola ma una frase (ad esempio: title=Scott Reynolds): `title:"Scott Reynolds"`
* Per visualizzare le risorse con più valori di una singola proprietà (ad esempio: title=Scott Reynolds o John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Per visualizzare le risorse con valori di proprietà che iniziano con una stringa specifica (ad esempio: title is Scott Reynolds): `title:Scott*`
* Per visualizzare le risorse con valori di proprietà che terminano con una stringa specifica (ad esempio: title is Scott Reynolds): `title:*Reynolds`
* Per visualizzare le risorse con un valore di proprietà contenente una stringa specifica (ad esempio: title = Sala riunioni di Basilea): `title:*Meeting*`
* Per visualizzare le risorse che contengono una stringa particolare e hanno un valore di proprietà specifico (ad esempio: cercare una stringa  Adobe nelle risorse con title=John Doe): `*Adobe* title:"John Doe"`

## Cercare risorse da altre offerte AEM o interfacce {#beyondomnisearch}

Adobe Experience Manager (AEM) collega l&#39;archivio DAM a varie altre soluzioni AEM per fornire un accesso più rapido alle risorse digitali e semplificare i flussi di lavoro creativi. Qualsiasi individuazione di risorse inizia con ricerca o ricerca. Il comportamento di ricerca rimane in gran parte lo stesso per le diverse superfici e soluzioni. Alcuni metodi di ricerca cambiano man mano che l&#39;audience di destinazione, i casi di utilizzo e l&#39;interfaccia utente variano tra le soluzioni AEM. I metodi specifici sono documentati per le singole soluzioni ai link seguenti. I suggerimenti e i comportamenti universalmente applicabili sono documentati in questo articolo.

### Cercare risorse dal pannello Collegamento risorse  Adobe {#aal}

Utilizzando  collegamento risorse di Adobe, i creativi professionisti ora possono accedere al contenuto memorizzato in  AEM Assets, senza uscire dalle app Adobe Creative Cloud supportate. I creativi possono sfogliare, cercare, estrarre e archiviare facilmente le risorse utilizzando il pannello in-app nelle app di Creative Cloud: Photoshop,  Illustrator e  InDesign. Collegamento risorsa consente anche agli utenti di effettuare ricerche con risultati visivamente simili. I risultati della visualizzazione della ricerca visiva sono basati  algoritmi di machine learning Adobe Sensei e consentono agli utenti di trovare immagini esteticamente simili. Consultate [Cercare e sfogliare le risorse](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) mediante  collegamento alla risorsa Adobe.

### Cercare risorse nell&#39;app AEM desktop {#desktopapp}

I professionisti creativi utilizzano l’app desktop per rendere l’AEM Assets  facilmente ricercabile e disponibile sul desktop locale (Win o Mac). Creative può facilmente rivelare le risorse desiderate in Mac Finder o Windows Explorer, aperte nelle applicazioni desktop e modificate localmente - le modifiche vengono salvate in AEM con una nuova versione creata nel repository. L&#39;applicazione supporta le ricerche di base utilizzando una o più parole chiave, * e ? caratteri jolly e operatore AND. Consultate [Cercare, cercare e visualizzare in anteprima le risorse](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) nell’app desktop.

### Search assets in Brand Portal {#brandportal}

Gli utenti e i professionisti del settore della linea di business utilizzano Brand Portal per condividere in modo efficiente e sicuro le risorse digitali approvate con i team interni, i partner e i rivenditori estesi. See [search assets on Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Ricerca  immagini Adobe Stock {#adobestock-1}

Dall’interfaccia utente AEM, gli utenti possono effettuare ricerche  risorse Adobe Stock e ottenere la licenza per le risorse necessarie. Aggiungi `Location: Adobe Stock` nel campo Omnisearch. Potete anche usare il pannello **[!UICONTROL Filtri]** per trovare tutte le risorse con o senza licenza oppure per cercare una risorsa specifica usando  numero di file Adobe Stock. Consultate [gestire  immagini Adobe Stock in AEM](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Ricerca di risorse per file multimediali dinamici {#dynamicmedia}

Per filtrare le immagini in base a Dynamic Media, dal pannello **[!UICONTROL Filtri]** seleziona **[!UICONTROL Dynamic Media]** > **[!UICONTROL Set]**. Filtra e visualizza le risorse come set di immagini, caroselli, set di file multimediali diversi e set 360 gradi. Durante la creazione di pagine web, gli autori possono cercare i set direttamente da Content Finder. Nel menu pop-up è disponibile un filtro per i set.

### Cercare risorse in Content Finder durante la creazione di pagine Web {#contentfinder}

Gli autori possono utilizzare Content Finder per ricercare nell&#39;archivio DAM le risorse pertinenti e utilizzare le risorse nelle pagine Web che creano.

<!-- Authors can also use the Connected Assets functionality to search for assets that are available on a remote AEM deployment. Authors can then use these assets in web pages on a local AEM deployment. See [use remote assets](use-assets-across-connected-assets-instances.md#use-remote-assets).
-->

### Cerca raccolte {#collections}

AEM funzionalità di ricerca supporta la ricerca di raccolte e la ricerca di risorse all&#39;interno di una raccolta. Consultate [Cercare le raccolte](/help/assets/manage-collections.md).

## Asset selector {#assetselector}

Il selettore delle risorse consente di cercare, filtrare e sfogliare le risorse DAM in modo speciale. Il selettore delle risorse è disponibile in `https://[aem_server]:[port]/aem/assetpicker.html`. Potete recuperare i metadati delle risorse selezionate mediante il selettore delle risorse. Potete avviarlo con i parametri di richiesta supportati, come il tipo di risorsa (immagine, video, testo) e la modalità di selezione (selezione singola o multipla). Questi parametri definiscono il contesto del selettore delle risorse per una particolare istanza di ricerca e rimangono intatti per tutta la selezione.

Il selettore delle risorse utilizza il messaggio HTML5 `Window.postMessage` per inviare al destinatario i dati per la risorsa selezionata. Il selettore delle risorse si basa sul vocabolario del selettore base di Granite. Per impostazione predefinita, il selettore delle risorse funziona in modalità Sfoglia.

Puoi trasmettere i seguenti parametri di richiesta in un URL per avviare il selettore risorse in un contesto particolare:

| Nome | Valori | Esempio | Scopo |
|---|---|---|---|
| suffisso risorsa (B) | Percorso della cartella come suffisso della risorsa nell’URL:[https://localhost:4502/aem/assetpicker.html/&lt;percorso_cartella>](https://localhost:4502/aem/assetpicker.html) | Per avviare il selettore risorse con una particolare cartella selezionata, ad esempio con la cartella /content/dam/we-retail/en/activity selezionata, l’URL deve essere del modulo: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | Se al momento dell’avvio del selettore delle risorse è necessario selezionare una determinata cartella, passatela come suffisso di risorsa. |
| mode | singolo, multiplo | [https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single) | In modalità multipla, potete selezionare più risorse contemporaneamente utilizzando il selettore delle risorse. |
| mimetype | tipo(i) mimetico(`/jcr:content/metadata/dc:format`) di una risorsa (supportato anche dai caratteri jolly) | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png)</li></ul> | Utilizzatelo per filtrare le risorse in base ai tipi MIME |
| finestra di dialogo | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Usate questi parametri per aprire il selettore delle risorse come finestra di dialogo Granite. Questa opzione è applicabile solo quando si avvia il selettore delle risorse tramite Granite Path Field e lo si configura come URL pickerSrc. |
| assettype (S) | immagini, documenti, contenuti multimediali, archivi | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | Utilizzate questa opzione per filtrare i tipi di risorse in base al valore passato. |
| root | &lt;percorso_cartella> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | Utilizzate questa opzione per specificare la cartella principale per il selettore di risorse. In questo caso, il selettore delle risorse consente di selezionare solo le risorse secondarie (dirette/indirette) sotto la cartella principale. |

Per accedere all’interfaccia del selettore delle risorse, passate a `https://[aem_server]:[port]/aem/assetpicker`. Individuate la cartella desiderata e selezionate una o più risorse. In alternativa, cercate la risorsa desiderata dalla casella di ricerca Omnico, applicate il filtro in base alle vostre esigenze, quindi selezionatela.

![Sfogliare e selezionare la risorsa nel selettore delle risorse](assets/assetpicker.png)

*Figura: Sfoglia e seleziona la risorsa nel selettore delle risorse.*

## Limitazioni  {#limitations}

La funzionalità di ricerca in [!DNL Experience Manager Assets] presenta le seguenti limitazioni:

* Non inserite uno spazio iniziale nella query di ricerca, altrimenti la ricerca non funziona.
* [!DNL Experience Manager] può continuare a visualizzare il termine di ricerca dopo che hai selezionato le proprietà di una risorsa dai risultati della ricerca e quindi hai annullato la ricerca. <!-- (CQ-4273540) -->
* Durante la ricerca di cartelle, file e cartelle, i risultati della ricerca non possono essere ordinati in base ad alcun parametro.
* Se premete Invio senza digitare nella barra di ricerca Omnico, [!DNL Experience Manager] restituisce un elenco di soli file e non di cartelle. Se cercate in modo specifico le cartelle senza utilizzare una parola chiave, [!DNL Experience Manager] non restituisce alcun risultato.

La ricerca visiva o la ricerca per similarità presenta le seguenti limitazioni:

* La ricerca visiva funziona meglio con archivi più grandi. Anche se non è richiesto un numero minimo di immagini per ottenere buoni risultati, la qualità delle corrispondenze con alcune immagini potrebbe non essere altrettanto buona di quella delle corrispondenze di un archivio di grandi dimensioni.
* Non è possibile modificare il modello o il treno [!DNL Experience Manager] per trovare immagini simili. Ad esempio, l&#39;aggiunta o la rimozione di smart tag ad alcune risorse non modifica il modello. Le risorse vengono effettivamente escluse dai risultati di ricerca visivamente simili.

La funzionalità di ricerca può presentare dei limiti di prestazioni nei seguenti scenari:

* Rispetto alla visualizzazione a elenco, la visualizzazione a schede presenta un tempo di caricamento più rapido per visualizzare i risultati della ricerca.

## Suggerimenti per la ricerca {#tips}

* Durante il monitoraggio dello stato di revisione delle risorse, utilizzate l&#39;opzione appropriata per individuare le risorse approvate o in attesa di approvazione.
* Utilizzate il predicato Insights per cercare le risorse supportate in base alle statistiche di utilizzo ottenute da diverse app Creative. I dati di utilizzo sono raggruppati in Valutazione utilizzo, Impressioni, Clic e Canali multimediali in cui le risorse appaiono categorie.
* Per selezionare le risorse ricercate, usate la casella di controllo **[!UICONTROL Seleziona tutto]** . [!DNL Experience Manager] inizialmente visualizza 100 risorse nella vista a schede e 200 risorse nella vista a elenco. Quando scorrete i risultati della ricerca, vengono caricate più risorse. Potete selezionare più risorse rispetto alle risorse caricate. Il conteggio delle risorse selezionate viene visualizzato nell’angolo superiore destro della pagina dei risultati della ricerca. Potete gestire la selezione, ad esempio scaricare le risorse selezionate, aggiornare le proprietà dei metadati in blocco per le risorse selezionate o aggiungere le risorse selezionate a una raccolta. Quando più risorse sono selezionate rispetto a quelle visualizzate, un’azione viene applicata a tutte le risorse selezionate oppure viene visualizzata una finestra di dialogo con il numero di risorse a cui sono applicate. Per applicare un’azione alle risorse non caricate, accertatevi che tutte le risorse siano selezionate in modo esplicito.
* Per cercare risorse che non contengono metadati obbligatori, consultate Metadati [](#mandatorymetadata)obbligatori.
* La ricerca utilizza tutti i campi di metadati. Una ricerca generica, come la ricerca di 12, in genere restituisce molti risultati. Per risultati ottimali, utilizzate virgolette doppie (non singole) o assicuratevi che il numero sia contiguo a una parola senza un carattere speciale (ad esempio `shoe12`).
* La ricerca full-text supporta operatori quali `-` e `^`. Per cercare queste lettere come stringhe letterali, racchiudere l&#39;espressione di ricerca tra virgolette. Ad esempio, utilizzate `"Notebook - Beauty"` anziché `Notebook - Beauty`.
* Se i risultati della ricerca sono troppi, limita l’ [ambito della ricerca](#scope) a zero per le risorse desiderate. Questa funzione è particolarmente utile se avete qualche idea su come cercare meglio le risorse desiderate, ad esempio un tipo di file specifico, una posizione specifica, metadati specifici e così via.

* **Assegnazione tag**: I tag consentono di classificare le risorse che possono essere cercate e cercate in modo più efficiente. I tag consentono di estendere la tassonomia appropriata ad altri utenti e flussi di lavoro. [!DNL Experience Manager] offre metodi per assegnare automaticamente tag alle risorse utilizzando  servizi intelligenti di Adobe Sensei che consentono di aggiungere tag con utilizzo e formazione sempre più avanzati alle risorse. Quando ricercate le risorse, gli smart tag vengono inseriti se la funzione è attivata nel vostro account. Funziona insieme alla funzionalità di ricerca integrata. Consultate Comportamento [di](#searchbehavior)ricerca. Per ottimizzare l’ordine in cui vengono visualizzati i risultati della ricerca, potete [aumentare la classifica](#searchrank) di ricerca di alcune risorse selezionate.

* **Indicizzazione**: Nei risultati della ricerca vengono restituiti solo i metadati e le risorse indicizzati. Per una migliore copertura e migliori prestazioni, accertatevi che l&#39;indicizzazione sia corretta e seguite le best practice. Vedere [indicizzazione](#searchindex).

## Alcuni esempi che illustrano la ricerca {#samples}

Usate virgolette doppie intorno alle parole chiave per trovare le risorse che contengono la frase esatta nell’ordine esatto specificato dall’utente.

![Comportamento di ricerca con e senza virgolette](assets/search_with_quotes.gif)

*Figura: Funzionamento della ricerca con e senza virgolette.*

**Cerca con carattere jolly asterisco**: Per ampliare la ricerca, usate un asterisco prima o dopo la parola di ricerca per far corrispondere un numero qualsiasi di caratteri. Ad esempio, la ricerca di un&#39;esecuzione senza un asterisco non restituisce risorse contenenti variazioni della parola (anche nei metadati). Un asterisco sostituisce qualsiasi numero di caratteri. Esempio,

* `run` restituisce le risorse con la parola chiave run esatta
* `run*` restituisce le risorse in esecuzione, in esecuzione, in esecuzione e così via.
* `*run` restituisce un risultato negativo, un nuovo rendering e così via.
* `*run*` restituisce tutte le possibili combinazioni.

![Illustrazione dell’utilizzo di un carattere jolly asterisco nella ricerca di risorse tramite un esempio](assets/search_with_asterisk_run.gif)

*Figura: Illustrazione dell’utilizzo del carattere jolly asterisco nella ricerca delle risorse tramite un esempio.*

**Cerca con il carattere jolly** punto interrogativo: Per ampliare la ricerca, utilizzare uno o più caratteri &#39;?&#39; caratteri per corrispondere al numero esatto di caratteri. Ad esempio, nell&#39;illustrazione seguente,

* `run???` la query non corrisponde ad alcuna risorsa.

* `run????` query restituisce la parola `running` con quattro caratteri dopo `run`.

* `??run` La query corrisponde alla parola `rerun` con due caratteri prima `run`.

![Illustrazione dell’uso del carattere jolly punto interrogativo nella ricerca di risorse tramite un esempio](assets/search_with_questionmark_run.gif)

*Figura: Illustrazione dell’uso del carattere jolly punto interrogativo nella ricerca di risorse tramite un esempio.*

**Escludere una parola chiave**: Usate il trattino per cercare risorse che non contengono una parola chiave. Ad esempio, `running -shoe` la query restituisce risorse che contengono `running`, ma non `shoe`. Analogamente, `camp -night` query restituisce risorse che contengono `camp` ma non `night`. La query `camp-night` restituisce risorse contenenti sia `camp` che `night`.

![Utilizzo del trattino per cercare risorse non contenenti una parola chiave esclusa](assets/search_dash_exclude_keyword.gif)

*Figura: Utilizzo del trattino per cercare risorse non contenenti una parola chiave esclusa.*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).
-->

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses smart tags. After configuring smart tagging functionality, follow these steps.

1. In AEM CRXDE, in `/oak:index/lucene` node, add the following properties and values and save the changes.

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
1. Apply Smart Tags to the assets in your AEM repository. See [how to configure smart tags](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html?lang=en#configuring).
1. In CRXDE, in `/oak-index/damAssetLucene` node, set the `reindex` property to `true`. Save the changes.
1. (Optional) If you have customized search form then copy the `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` node to `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Save all the changes.

For related information, see [understand smart tags in AEM](https://helpx.adobe.com/experience-manager/kt/help/assets/smart-tags-feature-video-understand.html) and [how to manage smart tags](/help/assets/smart-tags.md).
-->

<!--
### Mandatory metadata {#mandatorymetadata}

Business users, administrators, or DAM librarians can define some metadata as mandatory metadata that is a must for the business processes to work. For various reasons, some assets may be missing this metadata, such as legacy assets or assets migrated in bulk. Assets with missing or invalid metadata are detected and reported based on the indexed metadata property. To configure it, see [mandatory metadata](/help/assets/metadata-schemas.md#defining-mandatory-metadata).

### Modify search facets {#searchfacets}

To improve the speed of discovery, AEM Assets offers search facets using which you can filter the search results. The Filters panel includes a few standard facets by default. Administrators can customize the Filters panel to modify the default facets using the in-built predicates. AEM provides a good collection of in-built predicates and an editor to customize the facets. See [search facets](/help/assets/search-facets.md).

### Extract text when uploading assets {#extracttextupload}

You can configure AEM to extract the text from the assets when users upload assets, such as PSD or PDF files. AEM indexes the extracted text and helps users search these assets based on the extracted text. See [upload assets](/help/assets/manage-digital-assets.md#uploading-assets).
-->

<!-- TBD: Check with gklebus and engineering if these customization are possible in CS.

### Custom predicates to filter search results {#custompredicates}

Predicates are used to create facets. Administrators can customize the search facets in the Filters panel using pre-configured predicates. These predicates can be customized using overlays. See [create custom predicates](/help/assets/searchx.md).

You can search for digital assets based on one or more of the following properties. Filters that apply on some of these properties are available by default and some other filters can be custom-created to apply on the other properties.

| Search field | Search property values |
|---|---|
| Approved Status | Approved or Rejected. |
| Audio Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Audio Codec | Libvorbis, Lame MP3, AAC Encoding. Value is stored in the metadata of video renditions only. |
| File Size | Small, Medium, or Large. |
| Last Modified | Hour, Day, Week, Month, or Year. |
| MIME Types | Images, Documents, Multimedia, Archives, or Other. |
| Orientation | Horizontal, Vertical, or Square. |
| Publish Status | Published or Unpublished. |
| Style | Color, or Black & White. |
| Video Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Codec | x264. Value is stored in the metadata of video renditions only. |
| Video Format | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Value is stored in the metadata of the source video and any renditions. |
| Video Height | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Width | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |

-->

## Utilizzo dei risultati di ricerca delle risorse {#aftersearch}

Con le risorse per le quali hai effettuato la ricerca potete effettuare le seguenti operazioni [!DNL Experience Manager]:

* Visualizzare le proprietà dei metadati e altre informazioni.
* Scaricate una o più risorse.
* Utilizzate Azioni desktop per aprire queste risorse nell&#39;app desktop.
* Creare raccolte intelligenti.

### Ordinare i risultati della ricerca {#sort}

Ordinate i risultati della ricerca per individuare più rapidamente le risorse necessarie. You can sort the search results in list view and only when you select **[[!UICONTROL Files]](#searchui)** from the **[!UICONTROL Filters]** panel. [!DNL Assets] utilizza l’ordinamento lato server per ordinare rapidamente tutte le risorse all’interno di una cartella o nei risultati di una query di ricerca, indipendentemente dal numero. L’ordinamento lato server fornisce risultati più rapidi e precisi rispetto all’ordinamento lato client.

Nella vista a elenco, potete ordinare i risultati della ricerca esattamente come potete ordinare le risorse in qualsiasi cartella. L&#39;ordinamento funziona su queste colonne: Nome, Titolo, Stato, Dimension, Dimensioni, Valutazione, Utilizzo, (Data) Creata, (Data) Modificata, (Data) Pubblicata, Flusso di lavoro e Estratta.

Per le limitazioni della funzionalità di ordinamento, consultate [Limitazioni](#limitations).

### Controllare informazioni dettagliate su una risorsa {#checkinfo}

Potete controllare informazioni dettagliate su una risorsa ricercata dalla pagina dei risultati della ricerca.

Per visualizzare tutti i metadati di una risorsa, selezionate la risorsa e fate clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.

Per controllare i commenti relativi a una risorsa o alla sua cronologia della versione, fai clic sulla risorsa per aprirne l’anteprima di grandi dimensioni. Apri la timeline nella barra a sinistra e seleziona **[!UICONTROL Commenti]** o **[!UICONTROL Versioni]**. Puoi anche ordinare l’attività della timeline come commenti o versioni in ordine cronologico.

![Ordinare le voci della cronologia per una risorsa di ricerca](assets/sort_timeline_search_results.gif)

*Figura: Ordinare le voci della cronologia per una risorsa di ricerca.*

### Scaricare le risorse ricercate {#download}

Potete scaricare le risorse ricercate e le relative rappresentazioni esattamente come potete scaricare le risorse normali dalle cartelle. Selezionate una o più risorse dai risultati della ricerca e fate clic su **[!UICONTROL Scarica]** dalla barra degli strumenti.

### Aggiornate in blocco le proprietà dei metadati {#metadataupdates}

È possibile eseguire aggiornamenti in blocco ai campi di metadati comuni di più risorse. Dai risultati della ricerca, selezionate una o più risorse. Fate clic su **[!UICONTROL Proprietà]** nella barra degli strumenti e aggiornate i metadati come necessario. Al termine, fate clic su **[!UICONTROL Salva e chiudi]** . I metadati esistenti in precedenza nei campi aggiornati vengono sovrascritti.

Per le risorse disponibili in una singola cartella o raccolta, è più semplice [aggiornare i metadati in blocco](/help/assets/manage-metadata.md#manage-assets-metadata) senza utilizzare la funzionalità di ricerca. Per le risorse disponibili in più cartelle o che corrispondono a criteri comuni, è più rapido aggiornare in massa i metadati tramite la ricerca.

### Raccolte intelligenti {#collections-1}

Una raccolta è un set ordinato di risorse che può includere risorse da posizioni diverse, perché le raccolte contengono solo riferimenti a tali risorse. Le raccolte sono dei due tipi seguenti:

* Un elenco di riferimento statico di risorse, cartelle e altre raccolte.
* Un elenco dinamico (raccolta avanzata) che popola le risorse nella raccolta in base a un criterio di ricerca.

Puoi creare raccolte avanzate in base ai criteri di ricerca. Dal pannello **[!UICONTROL Filtri]**, seleziona **[!UICONTROL File]** e fai clic su **[!UICONTROL Salva raccolta avanzata]**. Consulta la sezione [Gestisci raccolte](/help/assets/manage-collections.md).

## Risultati e problemi della ricerca imprevisti {#unexpectedresults}

<!--
**Partially related or unrelated search results**: AEM may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

| Errore, problemi, sintomi | Possibile motivo | Possibile correzione o comprensione del problema |
|---|---|---|
| Risultati errati durante la ricerca di risorse con metadati mancanti. | Quando si ricercano risorse per le quali mancano i metadati obbligatori, [!DNL Experience Manager] è possibile che vengano visualizzate risorse con metadati validi. I risultati si basano sulle proprietà dei metadati indicizzati. | Una volta aggiornati i metadati, è necessario reindicizzarli per riflettere lo stato corretto dei metadati delle risorse. Consultate Metadati [](metadata-schemas.md#define-mandatory-metadata)obbligatori. |
| Troppi risultati di ricerca. | Parametro di ricerca ampio. | Considerate la limitazione dell&#39; [ambito di ricerca](#scope). Gli smart tag consentono di ottenere più risultati di quanto previsto. Consultate Comportamento di [ricerca con gli smart tag](#withsmarttags). |
| Risultati di ricerca non correlati o in parte correlati. | Il comportamento di ricerca cambia con l’assegnazione di smart tag. | Scoprite [come cambia la ricerca dopo l’assegnazione di tag](#withsmarttags)avanzati. |
| Nessun suggerimento di completamento automatico per le risorse. | Le risorse appena caricate non sono ancora indicizzate. I metadati non sono immediatamente disponibili come suggerimenti quando iniziate a digitare una parola chiave di ricerca nella barra di ricerca Omnyser. | [!DNL Assets] attende la scadenza di un periodo di timeout (per impostazione predefinita, un’ora) prima di eseguire un processo in background per indicizzare i metadati per tutte le risorse caricate o aggiornate di recente e quindi aggiungere i metadati all’elenco dei suggerimenti. |
| Nessun risultato di ricerca. | <ul><li>Le risorse corrispondenti alla query non esistono. </li><li> Spazi bianchi aggiunti prima della query di ricerca. </li><li> Il campo di metadati non supportato contiene la parola chiave cercata.</li><li> Ricerca eseguita durante la disattivazione di una risorsa. </li></ul> | <ul><li>Effettuate ricerche utilizzando un&#39;altra parola chiave. In alternativa, potete usare tag avanzati o ricerche per similarità per migliorare i risultati della ricerca. </li><li>[Limitazione](#limitations)nota.</li><li>Non tutti i campi di metadati sono considerati come ricerche. Vedere [ambito](#scope).</li><li>Effettuate ricerche in un secondo momento o modificate i tempi di attivazione e disattivazione delle risorse richieste.</li></ul> |
| Filtro di ricerca o predicato non disponibile. | <ul><li>Il filtro di ricerca non è configurato.</li><li>Non è disponibile per l&#39;accesso.</li><li>(Meno probabile) Le opzioni di ricerca non vengono personalizzate sulla distribuzione in uso.</li></ul> | <ul><li>Contattate l’amministratore per verificare se le personalizzazioni della ricerca sono disponibili o meno.</li><li>Contattate l’amministratore per verificare se l’account dispone dei privilegi o delle autorizzazioni necessari per utilizzare la personalizzazione.</li><li>Contattate l’amministratore e controllate le personalizzazioni disponibili per la [!DNL Assets] distribuzione in uso.</li></ul> |
| Quando si ricercano immagini visivamente simili, manca un&#39;immagine prevista. | <ul><li>L&#39;immagine non è disponibile in [!DNL Experience Manager].</li><li>L&#39;immagine non è indicizzata. In genere, quando viene caricato di recente.</li><li>L&#39;immagine non è dotata di smart tag.</li></ul> | <ul><li>Aggiungete l’immagine a [!DNL Assets].</li><li>Contattate l’amministratore per reindirizzare la directory archivio. Inoltre, accertatevi di utilizzare l&#39;indice appropriato.</li><li>Contattate l’amministratore per assegnare tag avanzati alle risorse pertinenti.</li></ul> |
| Quando si ricercano immagini visivamente simili, viene visualizzata un’immagine irrilevante. | Comportamento di ricerca visiva. | [!DNL Experience Manager] visualizza il maggior numero possibile di risorse potenzialmente rilevanti. Eventuali immagini meno rilevanti vengono aggiunte ai risultati, ma con una classificazione di ricerca più bassa. La qualità delle corrispondenze e la rilevanza delle risorse ricercate diminuiscono mano a mano che scorrete i risultati della ricerca. |
| Quando si selezionano e si utilizzano i risultati della ricerca, non vengono utilizzate tutte le risorse ricercate. | L&#39;opzione [!UICONTROL Seleziona tutto] seleziona solo i primi 100 risultati di ricerca nella vista a schede e i primi 200 risultati di ricerca nella vista a elenco. |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] guida all&#39;implementazione della ricerca](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Configurazione avanzata per migliorare i risultati della ricerca](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [Configurare la ricerca per la traduzione intelligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

