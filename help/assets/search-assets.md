---
title: Cercare risorse digitali e immagini in AEM
description: Scopri come trovare le risorse necessarie in AEM utilizzando il pannello Filtri e come utilizzare le risorse visualizzate nella ricerca.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: dfa9b099eaf7f0d155986bbab7d56901876d98f6

---


# Ricerca di risorse in AEM {#search-assets-in-aem}

Puoi ottenere una maggiore velocità dei contenuti utilizzando le opzioni di individuazione delle risorse intuitive di Experience Manager. I team possono ridurre i tempi di immissione sul mercato grazie a un’esperienza di ricerca intelligente e senza soluzione di continuità, grazie alla funzionalità e ai metodi personalizzati. La ricerca delle risorse è fondamentale per l’utilizzo di un sistema di gestione delle risorse digitali, sia per l’ulteriore utilizzo da parte dei creativi, per una gestione affidabile delle risorse da parte degli utenti aziendali e degli esperti di marketing, sia per l’amministrazione da parte degli amministratori DAM. Ricerche semplici, avanzate e personalizzate che puoi eseguire tramite l’interfaccia utente di AEM Assets o altre app e superfici consentono di soddisfare questi casi di utilizzo.

AEM supporta i seguenti casi di utilizzo e questo articolo descrive l’utilizzo, i concetti, le configurazioni, i limiti e la risoluzione di problemi per questi casi di utilizzo.

| Cercare risorse | Configurazione e amministrazione | Utilizzo dei risultati di ricerca |
|--- |--- |--- |
| [Ricerche di base](#searchbasics) | [Indice di ricerca](#searchindex) | [Ordinare i risultati](#sort) |
| [Comprendere l’interfaccia di ricerca](#searchui) |  | [Verificare le proprietà e i metadati di una risorsa](#checkinfo) |
| [Suggerimenti per la ricerca](#searchsuggestions) | [Metadati obbligatori](#mandatorymetadata) | [Scarica](#download) |
| [Comprendere i risultati della ricerca e il comportamento](#searchbehavior) | [Modificare i facet di ricerca](#searchfacets) | [Aggiornamenti di massa dei metadati](#metadataupdates) |
| [Classificazione e incremento della ricerca](#searchrank) | [Estrazione del testo](#extracttextupload) | [Raccolte intelligenti](#collections) |
| [Ricerca avanzata: filtraggio e ambito di ricerca](#scope) | [predicati personalizzati](#custompredicates) | [Comprendere risultati](#unexpectedresults) imprevisti e [risolvere i problemi](#troubleshoot) |
| [Cerca da altre soluzioni e app](#beyondomnisearch): Collegamento <br />[risorse](#aal) app <br />[](#desktopapp) desktop <br />     Immagini [](#adobestock) Adobe Stock <br />     Risorse per contenuti multimediali [dinamici](#dynamicmedia) |  |  |
| [Selettore/selettore risorse](#assetselector) |  |  |
| [Limitazioni](#tips) e [suggerimenti](#limitations) |  |  |
| [Esempi illustrati](#samples) |  |  |

Cercate le risorse utilizzando il campo Omnisearch nella parte superiore dell’interfaccia Web di AEM. Vai a **[!UICONTROL Risorse]** > **[!UICONTROL File]** in AEM, fai clic su ![search_icon](assets/do-not-localize/search_icon.png) nella barra superiore, immetti la parola chiave di ricerca e premi Invio. In alternativa, usate la scelta rapida per le parole chiave `/` (barra) per aprire il campo di ricerca Omnisearch. `Location:Assets` è preselezionata per limitare le ricerche alle risorse DAM. Potete eseguire ricerche avanzate per aumentare o limitare l’ [ambito della ricerca](#scope).

Usate il pannello **[!UICONTROL Filtri]** per cercare risorse, cartelle, tag e metadati. Puoi filtrare i risultati di ricerca in base alle varie opzioni (predicati), come il tipo di file, la dimensione del file, la data dell’ultima modifica, lo stato della risorsa, i dati di approfondimento e le licenze di Adobe Stock. Potete personalizzare il pannello Filtri e aggiungere o rimuovere i predicati di ricerca utilizzando i facet [di](/help/assets/search-facets.md)ricerca.

La funzionalità di ricerca di AEM supporta la ricerca di raccolte e la ricerca di risorse all&#39;interno di una raccolta. Consultate [Cercare le raccolte](/help/assets/manage-collections.md).

## Comprendere l’interfaccia di ricerca {#searchui}

Acquisisci familiarità con l’interfaccia di ricerca e le azioni disponibili.

![](assets/aem_search_results.png) Informazioni sulle parti dell’interfaccia *dei risultati della ricerca Risorse* Figura: Informazioni sulle parti dell’interfaccia dei risultati di ricerca di Risorse

**** A. Salvate la ricerca come Smart Collection. **** B. Filtri (predicati) per limitare i risultati della ricerca. **C.** Visualizzare file, cartelle o entrambi nei risultati della ricerca. **** D. Fate clic su Filtri per aprire o chiudere la barra a sinistra. **** E. Il percorso di ricerca è DAM. ************ F. Campo di ricerca Omnisearch con la parola chiave di ricerca **G fornita dall&#39;utente. Casella di controllo per selezionare tutti i risultati di ricerca** H. Numero di risultati di ricerca visualizzati rispetto al totale dei risultati di ricerca **I. Chiudere la ricerca** J. Passaggio tra la vista a schede e quella a elenco

### Facet di ricerca dinamici {#dynamicfacets}

Dalla pagina dei risultati della ricerca potete individuare più rapidamente le risorse desiderate utilizzando il numero dinamico di risultati di ricerca previsti nei facet di ricerca. Il numero previsto di risorse viene aggiornato anche prima dell’applicazione del filtro di ricerca. La visualizzazione del conteggio previsto rispetto al filtro consente di navigare nei risultati di ricerca in modo rapido ed efficiente. Per ulteriori informazioni, consultate [Cercare risorse in AEM](/help/assets/search-assets.md).

![Visualizzate il numero approssimativo di risorse senza filtrare i risultati di ricerca nei facet di ricerca.](assets/asset_search_results_in_facets_filters.png)

Visualizzate il numero approssimativo di risorse senza filtrare i risultati di ricerca nei facet di ricerca.

## Search suggestions as you type {#searchsuggestions}

Quando iniziate a digitare una parola chiave, in AEM vengono suggerite le parole chiave o le frasi di ricerca possibili. I suggerimenti si basano sulle risorse in AEM. AEM indicizza tutti i campi di metadati per facilitare la ricerca. Per fornire suggerimenti per la ricerca, il sistema utilizza i valori dei seguenti campi di metadati. Per fornire suggerimenti per la ricerca, è consigliabile compilare i campi seguenti con le parole chiave appropriate:

* Tag risorsa. (mappe a `jcr:content/metadata/cq:tags`)
* Titolo risorsa. (mappe a `jcr:content/metadata/dc:title`)
* Descrizione della risorsa. (mappe a `jcr:content/metadata/dc:description`)
* Titolo nell’archivio JCR. Il valore può essere mappato sul titolo della risorsa. (mappe a `jcr:content/jcr:title`)
* Descrizione nell’archivio JCR. Il valore può essere mappato sulla descrizione della risorsa. (mappe a `jcr:content/jcr:description`)

## Comprendere i risultati della ricerca e il comportamento {#searchbehavior}

### Termini e risultati di ricerca di base {#searchbasics}

Potete eseguire ricerche per parole chiave dal campo OmniSearch. La ricerca per parola chiave non fa distinzione tra maiuscole e minuscole ed è una ricerca full-text (nei più comuni campi di metadati). Se vengono utilizzate più parole chiave, `AND` è l&#39;operatore predefinito tra le parole chiave. I risultati sono ordinati in base alla rilevanza, a partire da corrispondenze più simili. Per più parole chiave, i risultati più rilevanti sono le risorse che contengono entrambi i termini nei metadati. All’interno dei metadati, le parole chiave che appaiono come smart tag hanno una classificazione più alta rispetto alle parole chiave che appaiono in altri campi di metadati.

AEM consente di attribuire maggiore importanza a un particolare termine di ricerca. È inoltre possibile aumentare il rango di alcune risorse con targeting per termini di ricerca specifici. Gli amministratori di AEM possono eseguire queste configurazioni come descritto di seguito.

Per trovare rapidamente le risorse rilevanti, l’interfaccia avanzata offre meccanismi di filtraggio, ordinamento e selezione. Potete filtrare i risultati in base a più criteri e visualizzare il numero di risorse ricercate per vari filtri. In alternativa, potete eseguire nuovamente la ricerca modificando la query nel campo Omnisearch. Quando modificate i termini di ricerca o i filtri, gli altri filtri rimangono applicati per mantenere il contesto della ricerca.

In alcuni casi, nei risultati della ricerca potrebbero essere presenti risorse impreviste. Per ulteriori informazioni, consultate [risultati](#unexpectedresults)imprevisti.

AEM può cercare in molti formati di file e i filtri di ricerca possono essere personalizzati in base alle tue esigenze aziendali. Contatta i tuoi amministratori per sapere quali opzioni di ricerca rendere disponibili per l’archivio DAM e quali potrebbero essere le restrizioni per l’accesso.

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

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a qualsiasi termine di ricerca negli smart tag. Nell&#39;esempio precedente, l&#39;ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. Corrisponde `woman running` ai vari campi di metadati.
1. Corrisponde a `woman running` negli smart tag.
1. Corrisponde a `woman` o a `running` negli smart tag.

Potete migliorare la rilevanza delle parole chiave per risorse particolari per migliorare le ricerche in base alle parole chiave. In altre parole, le immagini per le quali vengono promosse parole chiave specifiche vengono visualizzate nella parte superiore dei risultati della ricerca quando si esegue una ricerca basata su tali parole chiave.

1. Dall’interfaccia utente Risorse, aprite la pagina delle proprietà della risorsa. Fate clic su **[!UICONTROL Avanzate]** e toccate o fate clic su **[!UICONTROL Aggiungi]** in **[!UICONTROL Elevate per cercare le parole chiave]**.
1. Nella casella **[!UICONTROL Search Promote (Promuovi]** ricerca), specificate una parola chiave per la quale desiderate incrementare la ricerca dell&#39;immagine e quindi fate clic o toccate **[!UICONTROL Aggiungi]**. Potete specificare più parole chiave nello stesso modo.
1. Tocca o fai clic su **[!UICONTROL Salva e chiudi]**. La risorsa promossa per questa parola chiave viene visualizzata tra i primi risultati della ricerca.

Potete usarlo a proprio vantaggio aumentando il livello di alcune risorse nei risultati della ricerca per la parola chiave di destinazione. Guardate il video di esempio riportato di seguito. Per informazioni dettagliate, consultate [Cercare in AEM](https://helpx.adobe.com/experience-manager/kt/help/assets/search-feature-video-use.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Come classificare i risultati della ricerca e come influenzarne la classificazione.*

## Advanced search {#scope}

In AEM sono disponibili vari metodi, come i filtri, che consentono di individuare più rapidamente le risorse ricercate. Di seguito sono descritti alcuni metodi di uso comune. Di seguito sono riportati alcuni esempi [](#samples) illustrati.

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

### Immagini Adobe Stock {#adobestock}

Dall’interfaccia utente di AEM, gli utenti possono effettuare ricerche nelle risorse [](/help/assets/aem-assets-adobe-stock.md) Adobe Stock e ottenere la licenza per le risorse richieste. Aggiungete `Location: Adobe Stock` nella barra di ricerca Omnisearch. Puoi anche usare il pannello Filtri per trovare tutte le risorse con o senza licenza o per cercare una risorsa specifica utilizzando il numero di file Adobe Stock.

### Risorse per file multimediali dinamici {#dmassets}

Per filtrare le immagini per gli elementi multimediali dinamici, selezionate Contenuti multimediali **[!UICONTROL dinamici > Set]** dal pannello **[!UICONTROL Filtri]** . Filtra e visualizza risorse come set di immagini, caroselli, set di file multimediali diversi e set 360 gradi.

### Ricerca utilizzando valori specifici nei campi di metadati {#gqlsearch}

Potete usare le risorse in base ai valori esatti di specifici campi di metadati, ad esempio titolo, descrizione e autore. La funzione di ricerca full-text GQL raccoglie solo le risorse il cui valore di metadati corrisponde esattamente alla query di ricerca. I nomi delle proprietà (ad esempio autore, titolo e così via) e i valori seguono la distinzione tra maiuscole e minuscole.

| Campo metadati | Valore e utilizzo dei facet |
|---|---|
| Titolo | title:John |
| Creatore | creatore:John |
| Dove si trova | posizione:NA |
| Descrizione | descrizione:&quot;Immagine campione&quot; |
| Strumento di creazione | strumento di creazione:&quot;Adobe Photoshop CC 2015&quot; |
| Proprietario copyright | copyrightowner: &quot;Adobe Systems&quot; |
| Collaboratore | collaboratore:John |
| Condizioni d&#39;uso | usageterms:&quot;CopyRights Reserved&quot; |
| Creato | create:YYYY-MM-DDTHH |
| Data scadenza | expires:AAAA-MM-DTHH |
| Ora di attivazione | ontime:AAAA-MM-DTHH |
| Ora di disattivazione | offtime:AAAA-MM-DTHH |
| Intervallo di tempo (data di scadenza, ora di disattivazione) | campo facet : in basso..upperbound |
| Percorso | /content/dam/&lt;nome cartella> |
| Titolo PDF | pdftitle:&quot;Documento Adobe&quot; |
| Oggetto | oggetto: &quot;Formazione&quot; |
| Tag | tags:&quot;Location And Travel&quot; |
| Tipo | type:&quot;image\png&quot; |
| Larghezza dell’immagine | width:lowerbound.upperbound |
| Altezza dell’immagine | height:lowerbound.upperbound |
| Person | persona:John |

Il percorso, il limite, la dimensione e l&#39;ordine delle proprietà non possono essere eseguiti in OR con altre proprietà.

La parola chiave per una proprietà generata dall&#39;utente è la relativa etichetta campo nell&#39;editor delle proprietà in lettere minuscole, con la rimozione degli spazi.

Di seguito sono riportati alcuni esempi di formati di ricerca per query complesse:

* Per visualizzare tutte le risorse con più campi facet (ad esempio: title=John Doe e strumento di creazione = Adobe Photoshop): `title:"John Doe" creatortool : Adobe*`
* Per visualizzare tutte le risorse quando il valore facet non è una singola parola ma una frase (ad esempio: title=Scott Reynolds): `title:"Scott Reynolds"`
* Per visualizzare le risorse con più valori di una singola proprietà (ad esempio: title=Scott Reynolds o John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Per visualizzare le risorse con valori di proprietà che iniziano con una stringa specifica (ad esempio: title is Scott Reynolds): `title:Scott*`
* Per visualizzare le risorse con valori di proprietà che terminano con una stringa specifica (ad esempio: title is Scott Reynolds): `title:*Reynolds`
* Per visualizzare le risorse con un valore di proprietà contenente una stringa specifica (ad esempio: title = Sala riunioni di Basilea): `title:*Meeting*`
* Per visualizzare le risorse che contengono una stringa particolare e hanno un valore di proprietà specifico (ad esempio: cercare la stringa Adobe nelle risorse con title=John Doe): `*Adobe* title:"John Doe"`

## Cercare risorse da altre offerte o interfacce AEM {#beyondomnisearch}

Adobe Experience Manager (AEM) collega l&#39;archivio DAM a diverse altre soluzioni AEM per fornire un accesso più rapido alle risorse digitali e semplificare i flussi di lavoro creativi. Qualsiasi individuazione di risorse inizia con ricerca o ricerca. Il comportamento di ricerca rimane in gran parte lo stesso sulle diverse superfici e soluzioni. Alcuni metodi di ricerca cambiano man mano che l’audience di destinazione, i casi di utilizzo e l’interfaccia utente variano tra le soluzioni AEM. I metodi specifici sono documentati per le singole soluzioni ai link seguenti. I suggerimenti e i comportamenti universalmente applicabili sono documentati in questo articolo.

### Cercare risorse dal pannello Collegamento risorse di Adobe {#aal}

Con Adobe Asset Link, i creativi professionisti possono ora accedere al contenuto memorizzato in AEM Assets, senza uscire dalle app Adobe Creative Cloud supportate. I creativi possono sfogliare, cercare, estrarre e archiviare facilmente le risorse utilizzando il pannello in-app nelle app Creative Cloud: Photoshop, Illustrator e InDesign. Collegamento risorsa consente anche agli utenti di effettuare ricerche con risultati visivamente simili. I risultati della visualizzazione della ricerca visiva sono basati sugli algoritmi di machine learning di Adobe Sensei e consentono agli utenti di trovare immagini esteticamente simili. Consultate [Cercare e sfogliare le risorse](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) tramite Adobe Asset Link.

### Cercare risorse nell’app desktop AEM {#desktopapp}

I professionisti creativi utilizzano l’app desktop per rendere le risorse AEM facilmente ricercabili e disponibili sul desktop locale (Win o Mac). Con i creativi è possibile visualizzare facilmente le risorse desiderate in Mac Finder o Esplora risorse, aperte nelle applicazioni desktop e modificate localmente; le modifiche vengono salvate in AEM con una nuova versione creata nell’archivio. L&#39;applicazione supporta le ricerche di base utilizzando una o più parole chiave, * e ? caratteri jolly e operatore AND. Consultate [Cercare, cercare e visualizzare in anteprima le risorse](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) nell’app desktop.

### Search assets in Brand Portal {#brandportal}

Gli utenti e i professionisti del settore della linea di business utilizzano Brand Portal per condividere in modo efficiente e sicuro le risorse digitali approvate con i team interni, i partner e i rivenditori estesi. See [search assets on Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Cercare immagini Adobe Stock {#adobestock-1}

Dall’interfaccia utente di AEM, gli utenti possono effettuare ricerche nelle risorse Adobe Stock e ottenere la licenza per le risorse richieste. Aggiungi `Location: Adobe Stock` nel campo Omnisearch. Puoi anche usare il pannello **[!UICONTROL Filtri]** per trovare tutte le risorse con o senza licenza oppure per cercare una risorsa specifica utilizzando il numero di file Adobe Stock. Consultate [Gestione delle immagini Adobe Stock in AEM](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Ricerca di risorse per file multimediali dinamici {#dynamicmedia}

Per filtrare le immagini per gli elementi multimediali dinamici, selezionate **[!UICONTROL Contenuti multimediali]** dinamici > **[!UICONTROL Set]** dal pannello **[!UICONTROL Filtri]** . Filtra e visualizza risorse come set di immagini, caroselli, set di file multimediali diversi e set 360 gradi. Durante la creazione di pagine Web, gli autori possono cercare i set direttamente da Content Finder. Un filtro per i set è disponibile in un menu a comparsa.

### Cercare risorse in Content Finder durante la creazione di pagine Web {#contentfinder}

Gli autori possono utilizzare Content Finder per ricercare nell&#39;archivio DAM le risorse pertinenti e utilizzare le risorse nelle pagine Web che creano.

<!-- Authors can also use the Connected Assets functionality to search for assets that are available on a remote AEM deployment. Authors can then use these assets in web pages on a local AEM deployment. See [use remote assets](use-assets-across-connected-assets-instances.md#use-remote-assets).
-->

### Cerca raccolte {#collections}

La funzionalità di ricerca di AEM supporta la ricerca di raccolte e la ricerca di risorse all&#39;interno di una raccolta. Consultate [Cercare le raccolte](/help/assets/manage-collections.md).

## Asset selector {#assetselector}

Il selettore delle risorse consente di cercare, filtrare e sfogliare le risorse DAM in modo speciale. Il selettore delle risorse è disponibile in `https://[aem_server]:[port]/aem/assetpicker.html`. Potete recuperare i metadati delle risorse selezionate mediante il selettore delle risorse. Potete avviarlo con i parametri di richiesta supportati, come il tipo di risorsa (immagine, video, testo) e la modalità di selezione (selezione singola o multipla). Questi parametri definiscono il contesto del selettore delle risorse per una particolare istanza di ricerca e rimangono intatti per tutta la selezione.

Il selettore delle risorse utilizza il messaggio HTML5 Window.postMessage per inviare al destinatario i dati per la risorsa selezionata. Il selettore delle risorse si basa sul vocabolario del selettore base di Granite. Per impostazione predefinita, il selettore delle risorse funziona in modalità Sfoglia.

Puoi trasmettere i seguenti parametri di richiesta in un URL per avviare il selettore risorse in un contesto particolare:

| Nome | Valori | Esempio | Scopo |
|---|---|---|---|
| suffisso risorsa (B) | Percorso della cartella come suffisso della risorsa nell’URL:[https://localhost:4502/aem/assetpicker.html/&lt;percorso_cartella>](https://localhost:4502/aem/assetpicker.html) | Per avviare il selettore risorse con una particolare cartella selezionata, ad esempio con la cartella /content/dam/we-retail/en/activity selezionata, l’URL deve essere del modulo: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | Se al momento dell’avvio del selettore delle risorse è necessario selezionare una determinata cartella, passatela come suffisso di risorsa. |
| mode | singolo, multiplo | [https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single) | In modalità multipla, potete selezionare più risorse contemporaneamente utilizzando il selettore delle risorse. |
| mimetype | tipo(i) mimetico(`/jcr:content/metadata/dc:format`) di una risorsa (supportato anche dai caratteri jolly) | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png)</li></ul> | Utilizzatelo per filtrare le risorse in base ai tipi MIME |
| finestra di dialogo | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Usate questi parametri per aprire il selettore delle risorse come finestra di dialogo Granite. Questa opzione è applicabile solo quando si avvia il selettore delle risorse tramite Granite Path Field e lo si configura come URL pickerSrc. |
| assettype (S) | immagini, documenti, contenuti multimediali, archivi | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | Utilizzate questa opzione per filtrare i tipi di risorse in base al valore passato. |
| root | &lt;percorso_cartella> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities) | Utilizzate questa opzione per specificare la cartella principale per il selettore di risorse. In questo caso, il selettore delle risorse consente di selezionare solo le risorse secondarie (dirette/indirette) sotto la cartella principale. |

Per accedere all’interfaccia del selettore delle risorse, passate a `https://[AEM server]:[port]/aem/assetpicker`. Individuate la cartella desiderata e selezionate una o più risorse. In alternativa, cercate la risorsa desiderata dalla casella di ricerca Omnico, applicate il filtro in base alle esigenze, quindi selezionatela.

![Sfogliare e selezionare la risorsa nel selettore risorse](assets/assetpicker.png)

Sfogliare e selezionare la risorsa nel selettore risorse

## Limiti {#limitations}

La funzionalità di ricerca in AEM Assets presenta i seguenti limiti:

* Non inserite uno spazio iniziale nella query di ricerca, altrimenti la ricerca non funziona.
* AEM potrebbe continuare a visualizzare il termine di ricerca dopo che sono state selezionate le proprietà di una risorsa dai risultati della ricerca e quindi annullate la ricerca (CQ-4273540).
* Durante la ricerca di cartelle, file e cartelle, i risultati della ricerca non possono essere ordinati in base ad alcun parametro.
* Se premete Invio senza digitare nulla nella barra di ricerca Omnisearch, AEM restituisce un elenco di soli file e non di cartelle. Se cercate specificamente delle cartelle senza utilizzare una parola chiave, AEM non restituisce alcun risultato.

La ricerca visiva o per similarità presenta le seguenti limitazioni:

* La ricerca visiva funziona meglio con archivi più grandi. Anche se non è richiesto un numero minimo di immagini per ottenere buoni risultati, la qualità delle corrispondenze con alcune immagini potrebbe non essere altrettanto buona di quella delle corrispondenze di un archivio di grandi dimensioni.
* Non potete modificare il modello o addestrare AEM per trovare immagini simili. Ad esempio, l&#39;aggiunta o la rimozione di smart tag ad alcune risorse non modifica il modello. Le risorse vengono escluse dai risultati di ricerca visivamente simili.

## Suggerimenti per la ricerca {#tips}

* Durante il monitoraggio dello stato di revisione delle risorse, utilizzate l&#39;opzione appropriata per individuare le risorse approvate o in attesa di approvazione.
* Utilizzate il predicato Insights per cercare le risorse supportate in base alle statistiche di utilizzo ottenute da diverse app Creative. I dati di utilizzo sono raggruppati in Valutazione utilizzo, Impressioni, Clic e Canali multimediali in cui le risorse appaiono categorie.
* Utilizzare la casella di controllo per selezionare tutti i risultati di ricerca o i risultati di ricerca filtrati da utilizzare sulla selezione. Seleziona tutte le risorse ricercate indipendentemente dal numero di risorse visualizzate nella visualizzazione utente corrente. Ad esempio, potete scaricare tutte le risorse selezionate, aggiornare le proprietà dei metadati in blocco per tutte le risorse selezionate o aggiungere le risorse selezionate a una raccolta.
* Per cercare risorse che non contengono metadati obbligatori, consultate Metadati [](#mandatorymetadata)obbligatori.
* La ricerca utilizza tutti i campi di metadati. Una ricerca generica, come la ricerca di 12, in genere restituisce molti risultati. Per risultati ottimali, utilizzate virgolette doppie (non singole) o assicuratevi che il numero sia contiguo a una parola senza un carattere speciale (ad esempio *shoe12*).
* La ricerca full text supporta operatori quali -, ^ e così via. Per cercare queste lettere come stringhe letterali, racchiudere l&#39;espressione di ricerca tra virgolette. Ad esempio, utilizzare &quot;Notebook - Bellezza&quot; invece di Notebook - Bellezza.
* Se i risultati della ricerca sono troppi, limita l’ [ambito della ricerca](#scope) a zero per le risorse desiderate. Questa funzione è particolarmente utile se avete qualche idea su come cercare meglio le risorse desiderate, ad esempio un tipo di file specifico, una posizione specifica, metadati specifici e così via.

* **Assegnazione tag**: I tag consentono di classificare le risorse che possono essere cercate e cercate in modo più efficiente. I tag consentono di estendere la tassonomia appropriata ad altri utenti e flussi di lavoro. AEM offre metodi per assegnare automaticamente i tag alle risorse utilizzando i servizi intelligenti di Adobe Sensei, che consentono di ottenere risultati ottimali con l’aggiunta di tag alle risorse mediante l’uso e la formazione. Quando ricercate le risorse, gli smart tag vengono inseriti se la funzione è attivata nel vostro account. Funziona insieme alla funzionalità di ricerca integrata. Consultate Comportamento [di](#searchbehavior)ricerca. Per ottimizzare l’ordine in cui vengono visualizzati i risultati della ricerca, potete [aumentare la classificazione](#searchrank) di alcune risorse selezionate.

* **Indicizzazione**: Nei risultati della ricerca vengono restituiti solo i metadati e le risorse indicizzati. Per una migliore copertura e migliori prestazioni, accertatevi che l&#39;indicizzazione sia corretta e seguite le best practice. Vedere [indicizzazione](#searchindex).

## Alcuni esempi che illustrano la ricerca {#samples}

Usate virgolette doppie intorno alle parole chiave per trovare le risorse che contengono la frase esatta nell’ordine esatto specificato dall’utente.

![Comportamento di ricerca con e senza virgolette](assets/search_with_quotes.gif)

Comportamento di ricerca con e senza virgolette

**Cerca con carattere jolly asterisco**: Per ampliare la ricerca, usate un asterisco prima o dopo la parola di ricerca per far corrispondere un numero qualsiasi di caratteri. Ad esempio, la ricerca di un&#39;esecuzione senza un asterisco non restituisce risorse contenenti variazioni della parola (anche nei metadati). Un asterisco sostituisce qualsiasi numero di caratteri. Esempio,

* `run` restituisce le risorse con la parola chiave run esatta
* `run*` restituisce le risorse in esecuzione, in esecuzione, in esecuzione e così via.
* `*run` restituisce un risultato negativo, un nuovo rendering e così via.
* `*run*` restituisce tutte le possibili combinazioni.

![Illustrazione dell’utilizzo di un carattere jolly asterisco nella ricerca di risorse tramite un esempio](assets/search_with_asterisk_run.gif)

Illustrazione dell’utilizzo di un carattere jolly asterisco nella ricerca di risorse tramite un esempio

**Cerca con il carattere jolly** punto interrogativo: Per ampliare la ricerca, utilizzare uno o più caratteri &#39;?&#39; caratteri per corrispondere al numero esatto di caratteri. Ad esempio, nell&#39;illustrazione seguente,

* `run???` la query non corrisponde ad alcuna risorsa.

* `run????` query restituisce la parola `running` con quattro caratteri dopo `run`.

* `??run` La query corrisponde alla parola `rerun` con due caratteri prima `run`.

![Illustrazione dell’uso del carattere jolly punto interrogativo nella ricerca di risorse tramite un esempio](assets/search_with_questionmark_run.gif)

Illustrazione dell’uso del carattere jolly punto interrogativo nella ricerca di risorse tramite un esempio

**Escludere una parola chiave**: Usate il trattino per cercare risorse che non contengono una parola chiave. Ad esempio, `running -shoe` la query restituisce risorse che contengono `running`, ma non `shoe`. Analogamente, `camp -night` query restituisce risorse che contengono `camp` ma non `night`. La `camp-night` query restituisce risorse contenenti sia `camp` che `night`.

![Utilizzo del trattino per cercare risorse non contenenti una parola chiave](assets/search_dash_exclude_keyword.gif)*Figura esclusa:Utilizzo del trattino per cercare risorse non contenenti una parola chiave esclusa*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).

### Sort on Name column {#sortbyname}

In list view, you can sort the search results just as you can sort assets in any folder. Sorting does not work on the `Name` column by default. To sort by the `Name` column, overlay `/libs/dam/gui/content/commons/availablecolumns` and change the value of sortable to `True`.

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses smart tagging and requires AEM 6.5.2.0 or later. After configuring smart tagging functionality, follow these steps.

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
1. Apply Smart Tags to the assets in your AEM repository. See [how to configure smart tags](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html).
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

<!-- Check with gklebus if this customization is possible in Cloud Service now

### Custom predicates to filter search results {#custompredicates}

Predicates are used to create facets. Administrators can customize the search facets in the Filters panel using pre-configured predicates. These predicates can be customized using overlays. See [create custom predicates](/help/assets/searchx.md).

You can search for digital assets based on one or more of the following properties. Filters that apply on some of these properties are available by default and some other filters can be custom-created to apply on the other properties.

| Search field | Search property values |
|---|---|
| MIME Types | Images, Documents, Multimedia, Archives, or Other. |
| Last Modified | Hour, Day, Week, Month, or Year. |
| File Size | Small, Medium, or Large. |
| Publish Status | Published or Unpublished. |
| Approved Status | Approved or Rejected. |
| Orientation | Horizontal, Vertical, or Square. |
| Style | Color, or Black & White. |
| Video Height | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Width | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Format | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Value is stored in the metadata of the source video and any renditions. |
| Video Codec | x264. Value is stored in the metadata of video renditions only. |
| Video Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Audio Codec | Libvorbis, Lame MP3, AAC Encoding. Value is stored in the metadata of video renditions only. |
| Audio Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |

-->

## Utilizzo dei risultati di ricerca delle risorse {#aftersearch}

Una volta visualizzate le risorse ricercate che corrispondono ai criteri specificati, potete effettuare le seguenti operazioni tipiche con i risultati di ricerca oppure effettuare le seguenti operazioni:

* Visualizzare le proprietà dei metadati e altre informazioni.
* Scaricate una o più risorse.
* Utilizzate Azioni desktop per aprire queste risorse nell&#39;app desktop.
* Creare raccolte intelligenti.

### Ordinare i risultati della ricerca {#sort}

L’ordinamento dei risultati di ricerca consente di individuare più rapidamente le risorse necessarie. L’ordinamento dei risultati della ricerca funziona nella vista a elenco e solo quando si seleziona **[!UICONTROL [File](#searchui)]**dal pannello**[!UICONTROL  Filtri ]**. Risorse AEM utilizza l’ordinamento lato server per ordinare rapidamente tutte le risorse (indipendentemente dal numero di risorse) all’interno di una cartella o dai risultati di una query di ricerca. L&#39;ordinamento lato server fornisce risultati più rapidi e precisi rispetto all&#39;ordinamento lato client.

Nella vista a elenco, potete ordinare i risultati della ricerca esattamente come potete ordinare le risorse in qualsiasi cartella. L&#39;ordinamento funziona su queste colonne: Titolo, Stato, Dimensioni, Dimensioni, Valutazione, Utilizzo, (Data) Modificata, (Data) Pubblicata, Flusso di lavoro e Estratta.

Consultate [Configurare l’ordinamento sulla colonna](#sortbyname)Nome. Per le limitazioni della funzionalità di ordinamento, consultate [Limitazioni](#limitations).

### Controllare informazioni dettagliate su una risorsa {#checkinfo}

Potete controllare informazioni dettagliate su una risorsa ricercata dalla pagina dei risultati della ricerca.

Per visualizzare tutti i metadati di una risorsa, selezionate la risorsa e fate clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.

Per controllare i commenti relativi a una risorsa o alla cronologia della versione di una risorsa, fate clic sulla risorsa per aprire l’anteprima di grandi dimensioni. Aprite la timeline nella barra a sinistra e selezionate **[!UICONTROL Commenti]** o **[!UICONTROL Versioni]**. Potete anche ordinare l&#39;attività della cronologia come commenti o versioni in ordine cronologico.

![Ordinare le voci della cronologia per una risorsa di ricerca](assets/sort_timeline_search_results.gif)

Ordinare le voci della cronologia per una risorsa di ricerca

### Scaricare le risorse ricercate {#download}

Potete scaricare le risorse ricercate e le relative rappresentazioni esattamente come potete scaricare le risorse normali dalle cartelle. Selezionate una o più risorse dai risultati della ricerca e fate clic su **[!UICONTROL Scarica]** dalla barra degli strumenti.

### Aggiornate in blocco le proprietà dei metadati {#metadataupdates}

È possibile eseguire aggiornamenti in blocco ai campi di metadati comuni di più risorse. Dai risultati della ricerca, selezionate una o più risorse. Fate clic su **[!UICONTROL Proprietà]** nella barra degli strumenti e aggiornate i metadati come necessario. Al termine, fate clic su **[!UICONTROL Salva e chiudi]** . I metadati esistenti in precedenza nei campi aggiornati vengono sovrascritti.

Per le risorse disponibili in una singola cartella o raccolta, è più semplice [aggiornare i metadati in massa](/help/assets/manage-metadata.md#manage-assets-metadata). Per le risorse disponibili in più cartelle o che corrispondono a criteri comuni, è più rapido aggiornare in massa i metadati tramite la ricerca.

### Raccolte intelligenti {#collections-1}

Una raccolta è un set ordinato di risorse che può includere risorse da posizioni diverse, perché le raccolte contengono solo riferimenti a tali risorse. Le raccolte sono dei due tipi seguenti:

* Un elenco di riferimento statico di risorse, cartelle e altre raccolte.
* Un elenco dinamico (raccolta avanzata) che popola le risorse nella raccolta in base a un criterio di ricerca.

Potete creare raccolte dinamiche in base ai criteri di ricerca. Dal pannello **[!UICONTROL Filtri]** , selezionate **[!UICONTROL File]** e fate clic su **[!UICONTROL Salva raccolta]** avanzata. Consultate [Gestione delle raccolte](/help/assets/manage-collections.md).

## Risultati di ricerca imprevisti {#unexpectedresults}

**Cerca metadati** mancanti: Quando si ricercano risorse per le quali mancano i metadati obbligatori, in AEM potrebbero essere visualizzate risorse con metadati validi. I metadati mancanti vengono rilevati e segnalati in base alle proprietà dei metadati indicizzati. Anche se i metadati della risorsa sono fissi, i metadati della risorsa continuano a essere visualizzati come metadati mancanti fino a quando non viene eseguita la reindicizzazione. Consultate Metadati [](/help/assets/metadata-schemas.md#defining-mandatory-metadata)obbligatori.

**Troppi risultati** di ricerca: Per evitare di ottenere troppi risultati di ricerca, è consigliabile limitare i risultati di ricerca. Ad esempio, per cercare risorse in DAM, selezionate `Location:Assets` nella barra di ricerca Omnice. Per ulteriori filtri di ricerca, vedere [ambito di ricerca](#scope).

<!-- Another reason to get more than expected search results can be use of smarts tags. See [search behavior with smart tags](#withsmarttags). 
-->

<!--
**Partially related or unrelated search results**: AEM may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

**Nessun suggerimento di completamento automatico per le risorse** appena caricate: I metadati (titoli, tag e così via) delle risorse caricate di recente non sono immediatamente disponibili come suggerimenti quando iniziate a digitare una parola chiave di ricerca nella barra di ricerca omonima. Risorse AEM attende la scadenza di un periodo di timeout (per impostazione predefinita, un’ora) prima di eseguire un processo in background per indicizzare i metadati per tutte le risorse caricate o aggiornate di recente e quindi aggiungere i metadati all’elenco dei suggerimenti.

**Nessun risultato** di ricerca: Se AEM e visualizza una pagina vuota per una query di ricerca, i motivi possono essere i seguenti:

* Nessuna risorsa corrispondente alla query.
* Prima della query di ricerca è possibile aggiungere uno spazio vuoto. È una limitazione [](#limitations)nota.

* Un campo di metadati non supportato contiene la parola chiave cercata. Non tutti i campi di metadati sono considerati per le ricerche. Vedere [ambito](#scope).
* L’ora di attivazione e disattivazione è configurata per la risorsa e la ricerca è stata eseguita durante il tempo di disattivazione della risorsa.

**Filtro/predicato di ricerca non disponibile**: Se una personalizzazione prevista per i filtri di ricerca non è disponibile nell’interfaccia utente, contattate l’amministratore per verificare se la personalizzazione è stata implementata per tutti gli autori e sul server di produzione in uso. È possibile che la configurazione non fosse corretta.

## Risoluzione dei problemi relativi alla ricerca {#troubleshoot}

Consulta i problemi e le possibili linee di azione di seguito:

* Se un filtro/predicato di ricerca previsto non è visibile, contattate l’amministratore.
* Quando si ricercano immagini visivamente simili, talvolta nei risultati della ricerca potrebbe mancare un’immagine prevista. Verificate che tali risorse siano indicizzate e con tag avanzati.
* Quando si ricercano immagini visivamente simili, talvolta nei risultati della ricerca può comparire un’immagine apparentemente irrilevante. AEM visualizza il maggior numero possibile di risorse potenzialmente rilevanti. Eventuali immagini meno rilevanti vengono aggiunte ai risultati, ma con una classificazione di ricerca più bassa. La qualità delle corrispondenze e la rilevanza delle risorse ricercate diminuiscono mano a mano che scorrete i risultati della ricerca.
