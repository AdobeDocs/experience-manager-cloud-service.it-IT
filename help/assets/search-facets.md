---
title: Facet di ricerca
description: Questo articolo descrive come creare, modificare e utilizzare i facet di ricerca in AEM.
translation-type: tm+mt
source-git-commit: c978be66702b7f032f78a1509f2a11315d1ed89f
workflow-type: tm+mt
source-wordcount: '2387'
ht-degree: 22%

---


# Facet di ricerca {#search-facets}

Scoprite come creare, modificare e utilizzare i facet di ricerca in AEM.

L’implementazione a livello aziendale di Risorse Adobe Experience Manager (AEM) consente di archiviare molte risorse. A volte, trovare la risorsa giusta può essere difficile e richiede molto tempo se utilizzate solo le funzionalità di ricerca generiche di AEM.

Usate i facet di ricerca nel pannello Filtri per aggiungere maggiore granularità all’esperienza di ricerca e rendere più efficiente e versatile la funzionalità di ricerca. I facet di ricerca aggiungono più dimensioni (predicati) che consentono di eseguire ricerche più complesse. Il pannello Filtri include alcuni facet standard. Potete inoltre aggiungere facet di ricerca personalizzati.

In sintesi, i facet di ricerca consentono di cercare le risorse in più modi anziché in un unico ordine tassonomico predeterminato. Potete facilmente approfondire fino al livello di dettaglio desiderato per una ricerca più mirata.

Ad esempio, se cercate un’immagine, potete scegliere se un elemento bitmap o un’immagine vettoriale deve essere selezionato. È possibile ridurre ulteriormente l&#39;ambito della ricerca specificando il tipo MIME per l&#39;immagine. Allo stesso modo, quando cercate documenti, potete specificare il formato, ad esempio PDF o MS Word.

## Aggiungere un predicato {#adding-a-predicate}

I facet di ricerca visualizzati nel pannello Filtri sono definiti nel modulo di ricerca sottostante utilizzando i predicati. Per visualizzare più facet o facet diversi, è possibile aggiungere predicati al modulo predefinito oppure utilizzare un modulo personalizzato che includa facet di propria scelta.

Per le ricerche full-text, aggiungere il `Fulltext` predicato al modulo. Utilizzate il predicato Proprietà per cercare le risorse che corrispondono a una singola proprietà specificata. Utilizzate il predicato Opzioni per cercare le risorse che corrispondono a uno o più valori per una particolare proprietà. Aggiungi il predicato Intervallo date per cercare le risorse create entro un intervallo di date specificato.

1. Tocca/fai clic sul logo AEM, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Moduli di ricerca]**.
1. From the Search Forms page, select **[!UICONTROL Assets Admin Search Rail]**, then tap  **Edit** ![aemassets_edit](assets/aemassets_edit.png).

   ![Individua e seleziona la Barra di ricerca Amministratore risorse](assets/assets_admin_searchrail.png)

1. In the Edit Search Forms page, drag a predicate from the **[!UICONTROL Select Predicate]** tab to the main pane. Ad esempio, trascinare Predicato **[!UICONTROL proprietà]**.

   ![Trascinate un predicato per personalizzare i filtri di ricerca](assets/drag_predicate.png)

   Trascinate un predicato per personalizzare i filtri di ricerca

1. Nella scheda Impostazioni, inserite un&#39;etichetta di campo, un testo segnaposto e una descrizione per il predicato. Specificate un nome valido per la proprietà di metadati che desiderate associare al predicato.

   L&#39;etichetta dell&#39;intestazione nella scheda Impostazioni identifica il tipo di predicato selezionato.

   ![Utilizzate la scheda Impostazioni per fornire le opzioni richieste per un predicato](assets/settings.png)

   Utilizzate la scheda Impostazioni per fornire le opzioni richieste per un predicato

1. Nel campo **[!UICONTROL Nome proprietà]**, specifica un nome valido per la proprietà di metadati che vuoi associare al predicato. È il nome in base al quale viene eseguita la ricerca. Ad esempio, inserisci `jcr:content/metadata/dc:description` o `./jcr:content/metadata/dc:description`.

   È inoltre possibile selezionare un nodo esistente dalla finestra di dialogo di selezione.

   ![Associare una proprietà di metadati a un predicato nel campo Nome proprietà](assets/property_settings.png)

   Associare una proprietà di metadati a un predicato nel campo Nome proprietà

1. Toccate o fate clic sull’ **[!UICONTROL anteprima]** ![Anteprima](assets/preview.png) per generare un’anteprima del pannello Filtri così come appare dopo l’aggiunta del predicato.
1. Esaminate il layout del predicato in modalità Anteprima.

   ![Visualizzare l&#39;anteprima del modulo di ricerca prima di inviare le modifiche](assets/preview-1.png)

   Visualizzare l&#39;anteprima del modulo di ricerca prima di inviare le modifiche

1. Per chiudere l’anteprima, toccate o fate clic su **[!UICONTROL Chiudi]** ![chiudi](assets/do-not-localize/close_icon.png) nell’angolo in alto a destra dell’anteprima.
1. Toccate **[!UICONTROL Fine]** per salvare le impostazioni.
1. Andate al pannello Ricerca nell’interfaccia utente Risorse. Il predicato Proprietà viene aggiunto al pannello.
1. Immettete una descrizione per la risorsa da cercare nella casella di testo. Ad esempio, immettete &quot;Adobe&quot;. Quando eseguite una ricerca, nei risultati della ricerca vengono elencate le risorse con la descrizione &quot;Adobe&quot;.

## Aggiunta di un predicato Opzioni {#adding-an-options-predicate}

Il predicato Opzioni consente di aggiungere più opzioni di ricerca nel pannello Filtri. Potete selezionare una o più di queste opzioni nel pannello Filtri per cercare le risorse. Ad esempio, per cercare le risorse in base al tipo di file, configurare le opzioni, quali Immagini, Multimedia, Documenti e Archivi, nel modulo di ricerca. Dopo aver configurato queste opzioni, la ricerca viene eseguita sulle risorse di tipo GIF, JPEG, PNG e così via, quando selezionate l’opzione Immagini nel pannello Filtri.

Per mappare le opzioni sulla rispettiva proprietà, create una struttura di nodi per le opzioni e fornite il percorso del nodo principale nella proprietà Nome proprietà del predicato Opzioni. Il nodo padre deve essere di tipo `sling`: `OrderedFolder`. Le opzioni devono essere di tipo `nt:unstructured`. I nodi di opzione devono avere le proprietà `jcr:title` e `value` configurate.

La `jcr:title` proprietà rappresenta un nome semplice per l&#39;opzione visualizzata nel pannello Filtri. Il `value` campo viene utilizzato nella query per corrispondere alla proprietà specificata.

Quando si seleziona un&#39;opzione, la ricerca viene eseguita in base alla `value` proprietà del nodo dell&#39;opzione e degli eventuali nodi secondari. L&#39;intera struttura sotto il nodo dell&#39;opzione viene attraversata e la `value` proprietà di ciascun nodo secondario viene combinata utilizzando un&#39;operazione OR per formare la query di ricerca.

Ad esempio, se selezioni “Immagini” per i tipi di file, la query di ricerca per le risorse viene creata combinando la proprietà `value` utilizzando un’operazione OR. Ad esempio, la query di ricerca per le immagini è realizzata unendo i risultati di corrispondenza per *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg* e *image/tiff* per la proprietà `jcr:content/metadata/dc:format` tramite un’operazione OR.

La proprietà Value di un tipo di file, come visualizzata in CRXDE, viene utilizzata per il funzionamento delle query di ricerca

Invece di creare manualmente una struttura di nodi per le opzioni nell’archivio CRX, puoi definire le opzioni in un file JSON, specificando le coppie corrispondenti di chiave-valore. Nel campo **[!UICONTROL Nome proprietà]**, specifica il percorso del file JSON. Ad esempio, puoi definire le coppie chiave-valore, `image/bmp`, `image/gif`, `image/jpeg`, `image/png` e specificarne i valori, come mostrato nel seguente file JSON di esempio. Nel campo **[!UICONTROL Nome proprietà]** puoi indicare il percorso CRX per il file.

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

Se si desidera utilizzare un nodo esistente, specificarlo utilizzando la finestra di dialogo di selezione.

>[!NOTE]
>
>Il predicato Options è un wrapper personalizzato che include i predicati delle proprietà per illustrare il comportamento descritto. Al momento non è disponibile alcun endpoint REST per supportare la funzionalità in modo nativo.

1. Tap the AEM logo, and then go to **[!UICONTROL Tools > General > Search Forms]**.
1. Dalla pagina **[!UICONTROL Moduli di ricerca]**, seleziona **[!UICONTROL Barra di ricerca amministrazione risorse]**, quindi tocca l’icona Modifica.
1. Nella pagina **[!UICONTROL Modifica modulo di ricerca]**, trascina **[!UICONTROL Predicato opzioni]** dalla scheda **[!UICONTROL Seleziona predicato]** al riquadro principale.
1. Nella scheda **[!UICONTROL Impostazioni]**, inserisci un’etichetta e un nome per la proprietà. Ad esempio, per cercare le risorse in base al loro formato, specifica un nome descrittivo per l’etichetta, ad esempio **[!UICONTROL Tipo file]**. Specifica la proprietà in base alla quale eseguire la ricerca nel campo apposito, ad esempio `jcr:content/metadata/dc:format.`
1. Effettua una delle operazioni seguenti:

   * In the **[!UICONTROL Property Name]** field, mention the path of the JSON file where you define the nodes for the options and specify corresponding key-value pairs.
   * Toccate ![](assets/do-not-localize/aem_assets_add_icon.png) accanto al campo Opzioni per specificare il testo di visualizzazione e il valore delle opzioni che desiderate fornire nel pannello Filtri. Per aggiungere un’altra opzione, toccate/fate clic ![](assets/do-not-localize/aem_assets_add_icon.png) e ripetete il passaggio.

1. Assicurati che l’opzione **[!UICONTROL Selezione singola]** sia deselezionata per consentire all’utente di scegliere più opzioni per volta per i tipi di file (ad esempio, Immagini, Documenti, Multimedia e Archivi). Se scegli **[!UICONTROL Selezione singola]**, l’utente può scegliere una sola opzione alla volta per i tipi di file.

   ![Campi disponibili nel predicato Opzioni](assets/options_predicate.png)

   Campi disponibili nel predicato Opzioni

1. Nel campo **Descrizione** , immettete una descrizione facoltativa e fate clic su **[!UICONTROL Fine]**.
1. Andate al pannello Ricerca. Il predicato Opzioni viene aggiunto al pannello **Ricerca** . Le opzioni per Tipo **[!UICONTROL di]** file sono visualizzate come caselle di controllo.

## Aggiungere un predicato proprietà multivalore {#adding-a-multi-value-property-predicate}

Il `Multi Value Property` predicato consente di cercare risorse per più valori. Considerate uno scenario in cui sono presenti immagini di più prodotti in Risorse AEM e i metadati di ciascuna immagine includono un numero SKU associato al prodotto. Potete usare questo predicato per cercare immagini di prodotto basate su più numeri SKU.

1. Fai clic sul logo AEM, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Moduli di ricerca]**.
1. Nella pagina Moduli di ricerca, seleziona Barra **[!UICONTROL di ricerca Amministratore]** risorse e tocca **Modifica** ![aemassets_edit](assets/aemassets_edit.png).
1. Nella pagina Modifica modulo di ricerca, trascina il predicato **[!UICONTROL Proprietà con più valori]** dalla scheda **[!UICONTROL Seleziona predicato]** al riquadro principale.
1. In the **[!UICONTROL Settings]** tab, enter a label and placeholder text for the predicate. Specify the property name based on which the search is to be performed in the property field, for example `jcr:content/metadata/dc:value`. È inoltre possibile utilizzare la finestra di dialogo di selezione per selezionare un nodo.
1. Assicurati di aver selezionato **[!UICONTROL Supporto delimitatore]**. Specifica i delimitatori per separare i singoli valori nel campo **[!UICONTROL Delimitatori di input]**. Per impostazione predefinita, la virgola è indicata come delimitatore. È possibile specificare un delimitatore diverso.
1. Nel campo **Descrizione** , immettete una descrizione facoltativa e toccate **[!UICONTROL Fine]**.
1. Nell’interfaccia utente Assets, vai al pannello Filtri. Al pannello viene aggiunto il predicato **[!UICONTROL Proprietà con più valori]**.
1. Specificate più valori nel campo Valore multiplo separati dai delimitatori ed eseguite la ricerca. Il predicato recupera una corrispondenza di testo esatta per i valori specificati.

## Aggiunta di un predicato Tag {#adding-a-tags-predicate}

Il `Tags` predicato consente di eseguire ricerche basate su tag per le risorse. Per impostazione predefinita, Risorse AEM cerca nelle risorse una o più corrispondenze di tag in base ai tag specificati. In altre parole, la query di ricerca esegue un&#39;operazione OR utilizzando i tag specificati. Tuttavia, potete usare l’opzione corrispondenza con tutti i tag per cercare le risorse che includono tutti i tag specificati.

1. Fai clic sul logo AEM, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Moduli di ricerca]**.
1. Dalla pagina Moduli di ricerca, seleziona Barra di ricerca **[!UICONTROL Amministratore]** risorse, quindi tocca **Modifica** ![aemassets_edit](assets/aemassets_edit.png).
1. In the Edit Search Form page, drag **[!UICONTROL Tags Predicate]** from the Select Predicate tab to the main pane.
1. Nella scheda Impostazioni, inserite un testo segnaposto per il predicato. Specify the property name based on which the search is to be performed in the property field, for example *jcr:content/metadata/cq:tags*. In alternativa, è possibile selezionare un nodo in CRXDE dalla finestra di dialogo di selezione.
1. Configurate la proprietà del percorso dei tag radice di questo predicate per popolare i vari tag nell&#39;elenco Tag.
1. Seleziona **[!UICONTROL Mostra opzione di corrispondenza con tutti i tag]** per cercare le risorse che includono tutti i tag specificati.

   ![Impostazioni tipiche del predicato Tag](assets/tags_predicate.png)

   Impostazioni tipiche del predicato Tag

1. Nel campo **[!UICONTROL Descrizione]** , immettete una descrizione facoltativa, quindi toccate o fate clic su **[!UICONTROL Fine]**.
1. Andate al pannello Ricerca. Il **[!UICONTROL predicato Tag]** viene aggiunto al pannello Ricerca.
1. Specificate i tag in base ai quali desiderate effettuare ricerche nelle risorse o selezionarli dall’elenco dei suggerimenti.
1. Select **[!UICONTROL Match all]** to search for matches that include all tags that you specify.

## Aggiunta di altri predicati {#adding-other-predicates}

Analogamente al modo in cui aggiungete un predicato Proprietà o un predicato Opzioni, potete aggiungere al pannello di ricerca i seguenti predicati aggiuntivi:

<table>
 <tbody>
  <tr>
   <td><p><strong>Nome predicato</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
   <td><p><strong>Proprietà</strong></p> </td>
  </tr>
  <tr>
   <td><p>Testo completo</p> </td>
   <td>Eseguire un predicato di ricerca per eseguire la ricerca full text su un intero nodo di risorsa. È mappato con <code>jcr</code>:<code>contains</code> operatore. Potete specificare un percorso relativo se desiderate eseguire una ricerca full text su una parte specifica del nodo della risorsa.</td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Segnaposto</li>
     <li>Nome proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Browser Percorsi</td>
   <td>Cerca predicato per cercare le risorse in cartelle e sottocartelle in un percorso radice preconfigurato</td>
   <td>
    <ul>
     <li>Segnaposto</li>
     <li>Percorso directory principale</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Percorso</p> </td>
   <td><p>Utilizzatelo per filtrare i risultati in base alla posizione. Potete specificare percorsi diversi come opzioni.</p> </td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Percorso</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Stato pubblicazione</p> </td>
   <td><p>Cercare il predicato per cercare le risorse in base al loro stato di pubblicazione</p> </td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Nome proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Data relativa</p> </td>
   <td><p>Consente di cercare le risorse in base alla data relativa della loro creazione. Ad esempio, potete configurare opzioni come 2 mesi fa, 3 settimane fa e così via. </p> </td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Nome proprietà</li>
     <li>Data relativa</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Intervallo</p> </td>
   <td><p>Cercare il predicato per cercare risorse che si trovano all’interno di un intervallo specificato. Nel pannello Ricerca, potete specificare i valori minimo e massimo per l’intervallo.</p> </td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Nome proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Intervallo date</p> </td>
   <td><p>Cerca predicato per cercare le risorse create all’interno di un intervallo specificato per una proprietà data. Nel pannello Ricerca, potete specificare le date di inizio e fine utilizzando i selettori data.</p> </td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Segnaposto</li>
     <li>Nome proprietà</li>
     <li>Testo intervallo (Da)</li>
     <li>Testo intervallo (A)</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p>Consente di eseguire una ricerca basata sul cursore delle risorse in base a una proprietà data.</p> </td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Nome proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dimensione file</p> </td>
   <td><p>Cercare un predicato per cercare le risorse in base alla loro dimensione. Si tratta di un predicato basato su silder in cui potete selezionare le opzioni del cursore da un nodo configurabile. Le opzioni predefinite sono definite in /libs/dam/options/predicates/filesize nel repository CRX. Le dimensioni del file sono espresse in byte.</p> </td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Nome proprietà</li>
     <li>Percorso</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ultima modifica risorsa</td>
   <td>Predicato di ricerca per cercare le risorse modificate di recente </td>
   <td>
    <ul>
     <li>Nome proprietà</li>
     <li>Valore proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Stato pubblicazione</td>
   <td>Cerca predicato per cercare le risorse in base al loro stato di pubblicazione </td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Nome proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Valutazione</td>
   <td>Cerca predicato per cercare le risorse in base alla loro valutazione media </td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Nome proprietà</li>
     <li>Percorso opzione</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Stato scadenza</td>
   <td>Cerca predicato per cercare le risorse in base al loro stato di scadenza </td>
   <td>
    <ul>
     <li>Etichetta</li>
     <li>Nome proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Nascosto</td>
   <td>predicato di ricerca che definisce una proprietà campo nascosta per la ricerca delle risorse</td>
   <td>
    <ul>
     <li>Nome proprietà</li>
     <li>Valore proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Ripristina facet di ricerca {#restoring-default-search-facets}

Per impostazione predefinita, l’icona Blocca viene visualizzata prima della Barra **[!UICONTROL di ricerca Amministratore]** risorse nella pagina **[!UICONTROL Moduli]** di ricerca. Se al modulo si aggiungono facet di ricerca per indicare che il modulo predefinito è stato modificato, l&#39;icona Blocca scompare.

L’icona Blocca rispetto a un’opzione nella pagina Moduli di ricerca indica che le impostazioni predefinite sono intatte e non sono personalizzate.

Per ripristinare il facet di ricerca predefinito, effettuare le seguenti operazioni:

1. Seleziona Barra di ricerca Amministratore **[!UICONTROL risorse]** nella pagina **[!UICONTROL Moduli]** di ricerca.
1. Toccate **[!UICONTROL Elimina]** icona ![](assets/do-not-localize/deleteoutline.png) Elimina nella barra degli strumenti.
1. Nella finestra di dialogo di conferma, toccate **[!UICONTROL Elimina]** per rimuovere le modifiche personalizzate.

   Dopo aver eliminato le modifiche personalizzate ai facet di ricerca, l’icona Blocca viene visualizzata nuovamente prima della **[!UICONTROL Barra di ricerca amministrazione risorse]** nella pagina **[!UICONTROL Moduli di ricerca]**.

## User permissions {#user-permissions}

Se non vi è stato assegnato un ruolo di amministratore, ecco un elenco di autorizzazioni necessarie per eseguire azioni di modifica, eliminazione e anteprima che coinvolgono facet di ricerca.

<table>
 <tbody>
  <tr>
   <td><strong>Azione</strong></td>
   <td><strong>Autorizzazioni </strong></td>
  </tr>
  <tr>
   <td>Modifica </td>
   <td>Autorizzazioni di lettura e scrittura sul <code>/apps</code> nodo in CRX<br /> </td>
  </tr>
  <tr>
   <td>Elimina</td>
   <td>Autorizzazioni di lettura, scrittura ed eliminazione sul <code>/apps</code> nodo in CRX</td>
  </tr>
  <tr>
   <td>Anteprima</td>
   <td>Autorizzazioni di lettura, scrittura ed eliminazione sul <code>/var/dam/content</code> nodo in CRX. Inoltre, le autorizzazioni di lettura e scrittura sul <code>/apps</code> nodo.</td>
  </tr>
 </tbody>
</table>

>[!MORELIKETHIS]
>
>* [Cercare risorse digitali](search-assets.md)

