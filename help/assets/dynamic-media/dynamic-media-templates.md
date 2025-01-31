---
title: Come gestire i modelli di Dynamic Media?
description: Scopri come creare modelli Dynamic Media utilizzando un editor di modelli WYSIWYG e includere più immagini e livelli di testo per creare rapidamente banner e volantini e utilizzarli nelle applicazioni a valle.
hide: true
role: User
source-git-commit: ada339567716a126d3288246c148c551dff298f4
workflow-type: tm+mt
source-wordcount: '2592'
ht-degree: 0%

---

# Modelli Dynamic Media{#dynamic-media-templates}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|-----|

Creare modelli Dynamic Media utilizzando un editor di modelli WYSIWYG e includere più immagini e livelli di testo per creare rapidamente banner e volantini e utilizzarli nelle applicazioni a valle. Puoi anche aggiungere parametri alle immagini e ai livelli di testo inclusi nel modello e utilizzare [URL Dynamic Media](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media) per aggiornare i valori di tali livelli in tempo reale.

Alcune delle caratteristiche principali includono:

* **Editor modelli di Dynamic Media WYSIWYG:** creare banner personalizzabili con livelli immagine e testo.
* **Parametrizzazione livello:** Definisci coppie chiave-valore dinamiche per i livelli per abilitare gli aggiornamenti in tempo reale.
* **Supporto URL Dynamic Media:** Utilizza gli URL di Dynamic Media per i modelli, integrando valori personalizzati da applicazioni di prima parte o di terze parti.
* **Controllo visibilità livello:** nascondere o mostrare dinamicamente i livelli in base alle esigenze.
* **Ridimensionamento automatico del testo:** Adatta automaticamente le dimensioni del testo alle aree designate.

Alcuni dei vantaggi principali dei modelli di Dynamic Media includono:

* **Ottimizza Personalization 1:1:** Personalizza il contenuto per i segnali dei clienti in tempo reale.
* **Riduzione dello sforzo manuale:** Automatizzazione e accelerazione della creazione e della gestione dei contenuti.
* **Assicurare Esperienze omnicanale coerenti:** Mantenere la coerenza del brand tra i canali.
* **Riutilizzare il contenuto in modo efficace:** evitare contenuti monouso e scalare con modelli dinamici con parametri.
* **Riduci rischi:** Aggiorna prezzi, sconti e collegamenti in tempo reale.
* **Migliora il coinvolgimento dei clienti:** esperienze interattive e contestualmente rilevanti.

>[!NOTE]
>
>I clienti con abbonamenti allo SKU Sicurezza avanzata non possono utilizzare alcuna funzionalità di Dynamic Media, inclusi i modelli di Dynamic Media, in tale programma di Cloud Service.

## Prima di iniziare{#prerequisites-for-dynamic-media-wysiwyg-template}

Per creare un modello di Dynamic Media, è necessario disporre di:

1. Accesso a Dynamic Media.
1. [Ha sincronizzato le immagini disponibili nell&#39;istanza AEM Assets con Dynamic Media per utilizzarle per la creazione del modello](/help/assets/dynamic-media/config-dm.md).

## Crea modello WYSIWYG di Dynamic Media{#how-to-create-dynamic-media-wysiwyg-template}

Per creare un modello DM, effettuare le seguenti operazioni:

1. [Creare un’area di lavoro vuota](#create-a-canvas)
1. [Aggiungere immagini all’area di lavoro](#add-images-to-the-canvas)
1. [Aggiungere livelli di testo all&#39;area di lavoro](#add-text-to-the-canvas)
1. [Modificare o eliminare un livello](#edit-or-delete-a-layer)
1. [Livelli parametrizzati](#parameterise-a-layer)


### Creare un’area di lavoro vuota{#create-a-canvas}

Per creare un’area di lavoro vuota, effettua le seguenti operazioni:

1. Passa alla visualizzazione Assets e fai clic su **Dynamic Media Assets** disponibile nel pannello a sinistra.

   ![](/help/assets/assets/dm-templates/DM-Assets1.png)

1. Fai clic su **Crea modello** per salvare il modello in Dynamic Media Assets oppure passa a una cartella e fai clic su **Crea modello** per salvare il modello in tale cartella. Viene visualizzata la finestra di dialogo **Nuovo modello**.
   ![](/help/assets/assets/dm-templates/new-template.png)
Per [creare una cartella](/help/assets/add-delete-assets-view.md) in **Dynamic Media Assets**, creare una cartella in **Assets**. La struttura di cartelle in **Assets** viene replicata in **Dynamic Media Assets**.
1. Specifica un nome di modello, definisci la larghezza e l&#39;altezza dell&#39;area di lavoro e fai clic su **Crea**. Viene visualizzata un&#39;area di lavoro vuota con opzioni di menu su entrambi i lati da utilizzare per la creazione del modello. Passa il puntatore del mouse sulle opzioni del menu per visualizzarne la descrizione comando.
   ![](/help/assets/assets/dm-templates/blank-canvas-page.png)

>[!NOTE]
>
> L&#39;intervallo consentito di larghezza e altezza è compreso tra 50 e 5000.

**Opzioni di menu nel riquadro di destra:** Utilizzare queste opzioni per aggiungere all&#39;area di lavoro le immagini e i livelli di testo necessari.

* ![](/help/assets/assets/dm-templates/add-image.svg): fare clic per aggiungere immagini all&#39;area di lavoro.
* ![](/help/assets/assets/dm-templates/add-text.svg): fare clic per aggiungere testi all&#39;area di lavoro.
* ![](/help/assets/assets/dm-templates/show-layers-list.svg): fare clic per visualizzare l&#39;elenco di tutti i livelli (immagine e testo) nell&#39;area di lavoro. Ogni immagine e testo aggiunti all’area di lavoro viene rappresentato come un livello separato.

**Opzioni di menu nel riquadro a sinistra:** Utilizzare queste opzioni per le azioni comuni dell&#39;editor come indicato di seguito.

* ![](/help/assets/assets/dm-templates/layer-selector.svg): selezionare un livello.
* ![](/help/assets/assets/dm-templates/bring-forward.svg): fare clic per portare avanti un livello selezionato o premere **Ctrl** + **]** (Windows) o **Cmd** + **]** (Mac).
* ![](/help/assets/assets/dm-templates/send-backward.svg): fare clic per inviare indietro un livello selezionato o premere **Ctrl** + **[** (Windows) o **Cmd** + **[** (Mac).
* ![](/help/assets/assets/dm-templates/undo.svg): fare clic per annullare l&#39;ultima azione o premere **Ctrl** + **Z** (Windows) o **Cmd** + **Z** (Mac).
* ![](/help/assets/assets/dm-templates/redo.svg): fare clic per ripetere l&#39;ultima azione o premere **Ctrl** + **Y** (Windows) o **Cmd** + **Y** (Mac).
* ![](/help/assets/assets/dm-templates/zoomin.svg): fare clic per ingrandire l&#39;area di lavoro o premere **Ctrl** + **+** (Windows) o Cmd + **+** (Mac).
* ![](/help/assets/assets/dm-templates/zoomout.svg): fare clic per ridurre l&#39;area di lavoro o premere **Ctrl** + **-** (Windows) o **Cmd** + **-** (Mac).
* Premi **Backspace** o **delete** per eliminare il livello selezionato se non si sta modificando testo o proprietà.

Fare clic su ![](/help/assets/assets/dm-templates/show-layers-list.svg) e altre opzioni (![](/help/assets/assets/dm-templates/three-dots.svg)) sul livello Area di lavoro per modificare le dimensioni dell&#39;area di lavoro in qualsiasi momento durante la creazione del modello.
![](/help/assets/assets/dm-templates/edit-canvas1.png)

>[!NOTE]
>
> I modelli consentono un massimo di 20 livelli, incluso Canvas.

### Aggiungere immagini all’area di lavoro{#add-images-to-the-canvas}

Per aggiungere immagini all’area di lavoro, effettua le seguenti operazioni:

1. Fai clic su ![](/help/assets/assets/dm-templates/add-image.svg) per visualizzare il pannello [Selettore risorse](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector). Il pannello mostra le immagini dell’istanza di AEM Assets che sono sincronizzate con Dynamic Media.
1. Sfoglia il pannello o usa le parole chiave nella barra di ricerca per trovare un’immagine specifica.
1. Trascina e rilascia un’immagine nell’area di lavoro per utilizzarla. Vedere il [pannello Proprietà](#4) per ridimensionare o riposizionare un livello nell&#39;area di lavoro.
   ![](/help/assets/assets/dm-templates/add-image-to-canvas.png)

### Aggiungere livelli di testo all&#39;area di lavoro{#add-text-to-the-canvas}

Per aggiungere livelli di testo all’area di lavoro, effettua le seguenti operazioni:

1. Fare clic su ![](/help/assets/assets/dm-templates/add-text.svg) per aggiungere un livello di testo all&#39;area di lavoro e aprire il pannello Proprietà.
1. Selezionate il livello e fate clic sul testo per aggiornarlo.
1. Abilitare **Ridimensionamento avanzato del testo** nel pannello Proprietà per regolare automaticamente la lunghezza del testo e la dimensione del font in modo che si adattino in modo ottimale all&#39;area designata.
   ![](/help/assets/assets/dm-templates/add-text-layer.png)

Vedere il [pannello Proprietà](#4) per riposizionare, ridimensionare, ruotare o eliminare il livello. Formatta il testo con il carattere, le dimensioni, il colore, lo stile e l&#39;allineamento desiderati (nel livello) modificandone i valori nei rispettivi campi nella sezione **Testo** del pannello.

>[!NOTE]
>
> Per utilizzare un tipo di carattere diverso da quello predefinito della famiglia di caratteri Adobe Sans F2, è necessario caricare e pubblicare il file dei caratteri in AEM Assets e Dynamic Media. Se nell&#39;istanza sono presenti caratteri obsoleti, assicurati di [rielaborare](/help/assets/reprocessing-assets-view.md) per visualizzarli nell&#39;editor modelli.

### Modificare o eliminare un livello {#edit-or-delete-a-layer}

Per modificare o eliminare un livello area di lavoro, esegui la procedura seguente:

1. Fare clic su ![](/help/assets/assets/dm-templates/show-layers-list.svg) e selezionare il livello nell&#39;area di lavoro o nell&#39;elenco Livelli.
1. Fai clic su **altre opzioni** (![](/help/assets/assets/dm-templates/three-dots.svg)) per modificare o eliminare il livello.
1. Fai clic su **Elimina** per eliminare il livello.
1. Fai clic su **Modifica** per modificare il livello utilizzando il [pannello Proprietà](#4).
   ![](/help/assets/assets/dm-templates/edit-delete-layer.png)

### Pannello Proprietà{#properties-panel}

Per passare al pannello delle proprietà di un livello:

1. Fai clic su ![](/help/assets/assets/dm-templates/show-layers-list.svg).
1. Selezionate il livello dall&#39;elenco.

In questo pannello viene visualizzata la posizione del punto centrale del livello sul piano dell&#39;area di lavoro (valori X e Y) e le dimensioni del livello (larghezza e altezza) insieme alle opzioni di formattazione del testo.

![](/help/assets/assets/dm-templates/properties-panel.png)

Dal pannello delle proprietà di un livello, selezionate un altro livello nell&#39;area di lavoro per passare al relativo pannello delle proprietà.
<a id="4"></a>

#### Riposizionare, ridimensionare, ruotare o eliminare un livello{#reposition-resize-delete-a-layer}

Per modificare un livello testo o immagine, consulta le seguenti azioni di modifica dei livelli comuni:

* **Riposizionare il livello:** Trascinare il livello per spostarlo in qualsiasi punto dell&#39;area di lavoro. Questa azione aggiorna i valori X e Y nel pannello delle proprietà.
* **Ridimensiona il livello:** Seleziona il livello e trascina i relativi quadratini di ridimensionamento per ridimensionarlo. Questa azione aggiorna i valori W (larghezza) e H (altezza) nel pannello delle proprietà.
* **Ruotare il livello:** Trascinare la maniglia quadrata posizionata verticalmente sopra il livello per ruotarlo intorno al centro. Questa azione aggiorna i valori degli angoli nel pannello delle proprietà.
* **Eliminare il livello:** Premere **Backspace** o **delete** e quindi fare clic su **Confirm** per eliminare il livello selezionato.

#### Opzioni di formattazione del testo{#text-formatting-options-on-properties-panel}

Formatta il testo con il carattere, le dimensioni, il colore, lo stile e l&#39;allineamento desiderati (nel livello) modificandone i valori nei rispettivi campi nella sezione **Testo** del pannello.

**Ridimensionamento automatico del testo:** Assicurarsi di includere **Ridimensionamento automatico del testo** ([Adattamento al testo](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting)) per adattarlo in modo ottimale a qualsiasi testo nell&#39;area designata, modificandone in modo intelligente la dimensione e la lunghezza del carattere. Questa funzionalità impedisce l&#39;overflow del testo o riduce al minimo gli spazi in eccesso nella parte inferiore.
![](/help/assets/assets/dm-templates/smart-text-resize.png)

### Livelli parametrizzati {#parameterise-a-layer}

Dopo aver creato un modello con più livelli di immagini e testi, impostate i parametri per i livelli selezionati. Quando un livello o la relativa proprietà sono parametrizzati, ottiene una coppia chiave-valore (detta anche parametro). Questo parametro può essere incluso nell’URL del modello per aggiornare la posizione, le dimensioni o il contenuto del livello in tempo reale, con conseguente personalizzazione del modello in un attimo.

Per parametrizzare un livello: <a id="1"></a>

1. fare clic su ![](/help/assets/assets/dm-templates/show-layers-list.svg), selezionare un livello e fare clic su **Parametri**. Viene visualizzato il pannello **Parametri**.
1. Attiva **Includi parametro** per parametrizzare una proprietà. Vedi [questo](#parameterisation-options-or-allowed-parameters) per conoscere il comportamento della proprietà dopo la parametrizzazione.
1. **Facoltativo:** Rinominare il nome del parametro. Il nome di un parametro è seguito da un suffisso. Per un livello selezionato, tutte le relative proprietà con parametri condividono lo stesso nome di livello seguito da un suffisso variabile. Rinominate il nome del livello seguendo la convenzione di denominazione semantica in modo che, quando includete il parametro nell&#39;URL, il nome del parametro spieghi da solo il contenuto o lo scopo del livello.
1. Fai clic su **Salva**.
   ![](/help/assets/assets/dm-templates/parameterise-a-layer.png)
Per passare dal pannello Parametri di un&#39;immagine al livello testo, selezionare il livello nell&#39;area di lavoro e fare clic su **Parametri**.

#### Opzione del pannello Parametri {#parameterisation-options-or-allowed-parameters}

Le proprietà con parametri possono essere incluse come parametri URL nell’URL del modello per modificare il modello in tempo reale utilizzando l’URL.

**Parametri immagine:**

**X:** includere per spostare il livello orizzontalmente lungo la sua linea centrale, parallelamente all&#39;asse X del piano del modello, modificando il valore del parametro nell&#39;URL.
**Y:** includere per spostare il livello verticalmente lungo la linea centrale, parallelamente all&#39;asse Y del piano del modello, modificando il valore del parametro nell&#39;URL.
**Larghezza:** Includere per regolare la larghezza del livello modificando il valore del parametro nell&#39;URL.
**Altezza:** Includere per regolare l&#39;altezza del livello modificando il valore del parametro nell&#39;URL.
**Nascondi:** Includi per nascondere o mostrare il livello nel modello utilizzando 0 (mostra) e 1 (nascondi).
**Source:** Includi per sostituire l&#39;immagine del livello con una nuova immagine modificando il percorso dell&#39;immagine nel valore del parametro nell&#39;URL.

**Parametri di formattazione del testo:**

Includi i seguenti parametri per modificare il testo, il relativo font, colore e dimensione, dall’URL aggiornando i valori dei parametri nell’URL.

**Testo:** Includere per aggiornare il testo dall&#39;URL.
**Famiglia font:** Includere per aggiornare il font del testo dall&#39;URL.
**Dimensione carattere:** Includere per aggiornare la dimensione del carattere del testo dall&#39;URL.
**Colore testo:** Includere per aggiornare il colore del carattere del testo dall&#39;URL.

### Raggruppare i livelli per controllarne contemporaneamente la visibilità{#group-layers}

Un altro modo per mantenere flessibili i modelli consiste nell&#39;utilizzare un singolo nome di parametro per controllare più livelli. Questa strategia è utile per il parametro di visibilità (nascondi o mostra livelli), per aggiornare la progettazione o gli elementi grafici da un singolo modello.

Seguire questi passaggi per assegnare lo stesso nome ai parametri nascosti (![](/help/assets/assets/dm-templates/Visibility-icon.svg)) di più livelli, consentendo di nasconderli o visualizzarli contemporaneamente.

1. Passa al [pannello Parametri](#1) di un livello.
1. Attiva/disattiva il parametro **Nascondi** se non è già stato impostato in precedenza come parametro.
1. **Facoltativo:** rinominare il parametro Nascondi.
1. Copia il nome del parametro Nascondi.
1. Passa al pannello Parametri degli altri livelli selezionandoli dall&#39;area di lavoro e, se non sono parametrizzati, imposta il parametro **Nascondi**.
1. Sostituisci il nome del parametro **** Hide con il nome copiato.
1. Fai clic su **Salva** per raggruppare i livelli.
1. Eseguire i passaggi 3 e 4 nella sezione [Anteprima e Publish](#2) per visualizzare le modifiche.

## Anteprima e pubblicazione del modello per copiare l’URL di consegna{#preview-and-publish-template-and-copy-template-deliver-url}

Per visualizzare in anteprima e pubblicare il modello e copiare l’URL di consegna, effettua le seguenti operazioni:

1. Nella pagina dell&#39;area di lavoro fare clic su **Anteprima**. Puoi anche passare a **Vista Assets > Dynamic Media Assets >** Trova e seleziona il modello **>** fai clic su **Modifica modello >** fai clic su **Anteprima**. Nella pagina di anteprima vengono visualizzati il modello, i relativi parametri (livelli e proprietà con parametri), lo stato di pubblicazione e l&#39;opzione **Publish**. <a id="3"></a>
1. Seleziona i parametri dal pannello **Parametri modello** per modificarne i valori e aggiornare immediatamente il contenuto, le dimensioni, la posizione o la formattazione del testo del livello del modello corrispondente nell&#39;anteprima. Ad esempio:
   1. Selezionare un livello di testo e modificarne il testo oppure
   1. Seleziona un livello immagine, fai clic su ![](/help/assets/assets/dm-templates/add-image.svg), seleziona un&#39;immagine dal selettore risorse, quindi fai clic su **Aggiorna**.

   Il modello viene aggiornato immediatamente, visualizzando il testo modificato e sostituendo l’immagine precedente con quella nuova. Inoltre, il valore del parametro immagine riflette il nuovo percorso immagine. Analogamente, potete ridimensionare un livello regolandone i valori e le modifiche vengono applicate al modello in tempo reale. <a id="2"></a>
1. Selezionare dall&#39;elenco il parametro Nascondi per [livelli raggruppati](#group-layers) per visualizzarli o nasconderli nel modello.
1. **Facoltativo:** Modificare il valore del **Nascondi parametro** tra 0 e 1 e fare clic su **Aggiorna** per visualizzare le modifiche. I livelli con lo stesso parametro Nascondi (Hide) vengono nascosti o visualizzati insieme. Allo stesso modo, potete controllare la visibilità dei livelli dall&#39;URL.

   ![](/help/assets/assets/dm-templates-publish-status.png)
Puoi anche attivare **Includi tutti i parametri** per modificare tutti i valori dei parametri visualizzati e visualizzare gli aggiornamenti nell&#39;anteprima del modello.
   <br>
1. Per pubblicare il modello nella pagina di anteprima, fare clic su **Publish** e confermare la pubblicazione. Viene visualizzato il messaggio Publish Complete e lo stato di pubblicazione viene aggiornato su Pubblicato.

>[!NOTE]
>
>La pubblicazione del modello richiede prima la pubblicazione delle immagini del modello.

### Copiare l’URL di consegna

I parametri selezionati nella pagina **Anteprima** diventano i parametri URL nell&#39;URL del modello.

Per copiare l’URL del modello pubblicato visualizzato nell’anteprima:

1. Fare clic su **Copia URL**. Viene visualizzata la finestra di dialogo **Copia URL**. Seleziona e copia l’URL visualizzato. Il primo parametro nell&#39;URL inizia dopo un punto interrogativo **(?)** e una coppia chiave-valore iniziano con **$** e terminano con **&amp;**. La chiave e il valore sono separati da un segno di uguale **(=)**, con la chiave a sinistra e il valore a destra.
1. Incolla questo URL nella scheda del browser e visualizza il modello live. Personalizza il modello in tempo reale aggiornando il valore del parametro richiesto (valore della chiave) nell&#39;URL direttamente come mostrato nel [passaggio 2](#3) della **sezione Anteprima e Publish**.
1. Utilizza questo URL per accelerare il merchandising dei tuoi prodotti o servizi. Puoi condividere questo URL con i clienti o integrarlo nel tuo sito web o in qualsiasi applicazione di terze parti a valle per visualizzare il banner e aggiornarlo in tempo reale per riflettere le offerte in corso.

Scopri come creare un modello di Dynamic Media passo dopo passo in questo video.
>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## Aggiornamenti in tempo reale al modello dall’URL{#update-the-template-from-the-url}

Modificare i parametri direttamente nell’URL può essere noioso. Per semplificare:

1. Copia l’URL e incollalo in un blocco note.
1. Utilizzare Cmd+F (Mac) o Ctrl+F (Windows) per trovare e modificare i valori dei parametri. Ad esempio:
   * Sostituite i percorsi immagine per i livelli immagine.
   * Regolare le dimensioni e le posizioni dei livelli (se [con parametri](#parameterise-a-layer)).
   * Modificare testo, font, colore, dimensione o allineamento per i livelli di testo.
   * Modificate i valori di visibilità compresi tra 0 e 1.

Incolla questo URL aggiornato nel browser per visualizzare le modifiche.

## Modifica il modello{#edit-the-template}

Modifica il modello seguendo questi passaggi:

1. Nella visualizzazione Assets, fare clic su **Dynamic Media Assets**.
2. Passa alla posizione del modello.
3. Seleziona il modello.
4. Fare clic su **Modifica modello**. Nell&#39;area di lavoro del modello vengono visualizzati il modello e l&#39;elenco di tutti i relativi livelli nel pannello Livelli. Inizia a modificare il modello in base ai requisiti.

## Punti importanti da notare {#important-points-to-note}

* Dopo aver creato un modello con livelli immagine con parametri per gli aggiornamenti dinamici, assicuratevi che le immagini destinate agli aggiornamenti futuri condividano le stesse dimensioni delle immagini con parametri. In questo modo le immagini si adattano perfettamente ai livelli senza traboccare o lasciare spazi vuoti. Attualmente, il modello non supporta le regolazioni automatiche delle quote per adattare le immagini ai livelli.
* Non è disponibile alcun supporto per sottostringhe in un livello di testo. L&#39;utente non può applicare proprietà font diverse alla sottostringa di un livello di testo.
* Il supporto di più società Dynamic Media non è attualmente disponibile con i modelli Dynamic Media.
* In caso di copia o spostamento, il selettore di destinazione mostra tutte le cartelle (incluse le cartelle non sincronizzate con Dynamic Media). Inoltre, al momento non mostra le risorse Modello Dynamic Media (entrambe queste sono limitazioni del selettore di destinazione).
* Qualsiasi operazione di aggiornamento su una cartella (ad esempio, Publish o Elimina) dalla sezione Assets ha effetto sui modelli di Dynamic Media disponibili all’interno di tale cartella.
* Il cestino non funziona per i modelli Dynamic Media. Se una risorsa viene spostata nel cestino e quindi ripristinata, viene ripristinata nell’AEM ma non in Dynamic Media. Lo stesso vale per i modelli di Dynamic Media.

## Consulta anche

1. Esplora [Dynamic Media e le sue funzionalità](/help/assets/dynamic-media/dynamic-media.md)
1. Esplora [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md)