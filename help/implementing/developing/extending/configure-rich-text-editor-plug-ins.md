---
title: Configurare i plug-in dell'editor Rich Text in [!DNL Adobe Experience Manager].
description: Scopri come configurare  [!DNL Adobe Experience Manager] i plug-in dell'Editor Rich Text.
contentOwner: AG
mini-toc-levels: 1
exl-id: 91619662-e865-47d1-8bec-0739f402353a
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '4303'
ht-degree: 2%

---

# Configurare i plug-in dell’Editor Rich Text {#configure-the-rich-text-editor-plug-ins}

Le funzionalità dell’editor Rich Text sono disponibili tramite una serie di plug-in, ciascuno con la proprietà Features. È possibile configurare la proprietà features per attivare o disattivare una o più funzionalità dell’editor Rich Text. Questo articolo descrive come configurare in modo specifico i plug-in dell’editor Rich Text.

Per informazioni dettagliate sulle altre configurazioni dell&#39;editor RTF, vedere [configurare l&#39;editor RTF](/help/implementing/developing/extending/rich-text-editor.md).

>[!NOTE]
>
>Quando si lavora con CRXDE Lite, si consiglia di salvare le modifiche regolarmente utilizzando l&#39;opzione [!UICONTROL Salva tutto].

## Attivare un plug-in e configurare la proprietà features {#activateplugin}

Per attivare un plug-in, segui la procedura riportata di seguito. Alcuni passaggi sono necessari solo quando configuri un plug-in per la prima volta, in quanto i nodi corrispondenti non esistono.

Per impostazione predefinita, i plug-in `format`, `link`, `list`, `justify` e `control` e tutte le relative funzionalità sono abilitati nell&#39;editor Rich Text.

>[!NOTE]
>
>Il rispettivo nodo `rtePlugins` è indicato come `<rtePlugins-node>` per evitare duplicazioni in questo articolo.

1. Con CRXDE Lite, individua il componente testo per il progetto.
1. Creare il nodo padre di `<rtePlugins-node>` se non esiste, prima di configurare qualsiasi plug-in dell&#39;editor Rich Text:

   * A seconda del componente, i nodi principali sono:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * un nodo di configurazione alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`

   * Sono di tipo: **jcr:primaryType** `cq:Widget`
   * Entrambi hanno la seguente proprietà:

      * **Nome** `name`
      * **Tipo** `String`
      * **Valore** `./text`

1. A seconda dell&#39;interfaccia per la quale si sta configurando, creare un nodo `<rtePlugins-node>`, se non esiste:

   * **Nome** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. Crea un nodo per ogni plug-in da attivare:

   * **Tipo** `nt:unstructured`
   * **Denomina** l&#39;ID del plug-in richiesto

Dopo aver attivato un plug-in, seguire queste linee guida per configurare la proprietà `features`.

| | Abilita tutte le funzioni | Abilita alcune funzioni specifiche. | Disattiva tutte le funzionalità. |
|---|---|---|---|
| Nome | funzioni | funzioni | funzioni |
| Tipo | Stringa | `String` (multistringa; impostare Type su `String` e fare clic su `Multi` in CRXDE Lite) | Stringa |
| Valore | `*` (un asterisco) | Impostate uno o più valori di feature. | - |

## Comprendere il plug-in Findreplace {#findreplace}

Il plug-in `findreplace` non richiede alcuna configurazione. Funziona immediatamente.

Quando si utilizza la funzionalità di sostituzione, la stringa sostitutiva deve essere immessa contemporaneamente alla stringa da trovare. Tuttavia, è ancora possibile fare clic su Trova per cercare la stringa prima di sostituirla. Se la stringa sostitutiva viene immessa dopo aver fatto clic su Trova, la ricerca riprende dall’inizio del testo.

La finestra di dialogo Trova e sostituisci diventa trasparente quando si fa clic su Trova e diventa opaca quando si fa clic su Sostituisci. Il comportamento consente all’autore di rivedere il testo da sostituire. Se si fa clic su Sostituisci tutto, la finestra di dialogo si chiude e viene visualizzato il numero di sostituzioni effettuate.

## Configurare le modalità Incolla {#pastemodes}

Quando si utilizza l’editor Rich Text, gli autori possono incollare il contenuto in una delle tre modalità seguenti:

* **Modalità browser**: incolla il testo utilizzando l&#39;implementazione Incolla predefinita del browser. Non è un metodo consigliato in quanto potrebbe introdurre markup indesiderati.

* **Modalità testo normale**: incolla il contenuto degli Appunti come testo normale. Elimina tutti gli elementi di stile e formattazione dal contenuto copiato prima di inserirli nel componente [!DNL Experience Manager].

* **Modalità MS Word**: incolla il testo, incluse le tabelle, con la formattazione durante la copia da MS Word. La copia e l’incolla di testo da un’altra origine, ad esempio una pagina web o MS Excel, non sono supportate e mantengono solo una formattazione parziale.

### Configurare le opzioni Incolla disponibili nella barra degli strumenti dell’editor Rich Text  {#configure-paste-options-available-on-the-rte-toolbar}

Nella barra degli strumenti dell’editor Rich Text è possibile fornire agli autori alcune o nessuna delle tre icone seguenti:

* **[!UICONTROL Incolla (Ctrl+V)]**: può essere preconfigurato per corrispondere a una delle tre modalità Incolla precedenti.

* **[!UICONTROL Incolla come testo]**: fornisce funzionalità in modalità testo normale.

* **[!UICONTROL Incolla da Word]**: fornisce funzionalità in modalità MS Word.

Per configurare l’editor Rich Text in modo da visualizzare le icone richieste, effettua le seguenti operazioni.

1. Passare al componente, ad esempio `/apps/<myProject>/components/text`.
1. Passare al nodo `rtePlugins/edit`. Se il nodo non esiste, vedere [attivare un plug-in](#activateplugin).
1. Creare la proprietà `features` nel nodo `edit` e aggiungere una o più funzionalità. Salva tutte le modifiche.

### Configurare il comportamento dell&#39;icona e della scelta rapida Incolla (Ctrl+V) {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Puoi preconfigurare il comportamento dell&#39;icona **[!UICONTROL Incolla (Ctrl+V)]** seguendo la procedura riportata di seguito. Questa configurazione definisce anche il comportamento della scelta rapida da tastiera Ctrl+V utilizzata dagli autori per incollare il contenuto.

La configurazione consente i tre tipi di casi di utilizzo seguenti:

* Incolla il testo utilizzando l’implementazione Incolla predefinita del browser. Non è un metodo consigliato in quanto potrebbe introdurre markup indesiderati. Configurato utilizzando `browser` di seguito.

* Incolla il contenuto degli Appunti come testo normale. Elimina tutti gli elementi di stile e formattazione dal contenuto copiato prima di inserirli nel componente [!DNL Experience Manager]. Configurato utilizzando `plaintext` di seguito.

* Incolla il testo, incluse le tabelle, con formattazione durante la copia da MS Word. La copia e l’incolla di testo da un’altra origine, ad esempio una pagina web o MS Excel, non sono supportate e mantengono solo una formattazione parziale. Configurato utilizzando `wordhtml` di seguito.

1. Nel componente, passa al nodo `<rtePlugins-node>/edit`. Creare i nodi se non esistono. Per ulteriori informazioni, vedere [attivare un plug-in](#activateplugin).
1. Nel nodo `edit` creare una proprietà utilizzando i dettagli seguenti:

   * **Nome** `defaultPasteMode`
   * **Tipo** `String`
   * **Il valore** è una delle modalità di incollamento richieste per `browser`, `plaintext` o `wordhtml`.

### Configurare i formati consentiti quando si incollano i contenuti {#pasteformats}

È possibile configurare ulteriormente la modalità Incolla come Microsoft Word (`paste-wordhtml`) in modo da consentire esplicitamente alcuni stili quando si incolla in [!DNL Experience Manager] da un altro programma, ad esempio [!DNL Microsoft Word].

Ad esempio, se solo i formati e gli elenchi in grassetto devono essere consentiti quando si incolla in [!DNL Experience Manager], è possibile filtrare gli altri formati. Questa operazione è denominata filtro di incollamento configurabile e può essere eseguita per entrambi:

* [Testo](#pastemodes)
* [Collegamenti](#linkstyles)

Per i collegamenti, puoi anche definire i protocolli che vengono accettati automaticamente.

Per configurare i formati consentiti quando si incolla testo in [!DNL Experience Manager] da un altro programma:

1. Nel componente, passa al nodo `<rtePlugins-node>/edit`. Crea i nodi se il nodo non esiste. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Crea un nodo sotto il nodo `edit` per contenere le regole di incollamento HTML:

   * **Nome** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Creare un nodo in `htmlPasteRules` per contenere i dettagli dei formati di base consentiti:

   * **Nome** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Per controllare i singoli formati accettati, creare una o più delle seguenti proprietà sul nodo `allowBasics`:

   * **Nome** `bold`
   * **Nome** `italic`
   * **Nome** `underline`
   * **Nome** `anchor` (sia per i collegamenti che per gli ancoraggi denominati)
   * **Nome** `image`

   Tutte le proprietà sono di tipo **Type** `Boolean`, quindi nel **Value** appropriato è possibile selezionare o rimuovere il segno di spunta per abilitare o disabilitare la funzionalità.

   >[!NOTE]
   >
   >Se non è definito in modo esplicito, viene utilizzato il valore predefinito true e il formato viene accettato.

1. Altri formati possono essere definiti utilizzando un intervallo di altre proprietà o nodi, applicati anche al nodo `htmlPasteRules`:

| Proprietà | Tipo | Descrizione |
|--- |--- |--- |
| `allowBlockTags` | `String` | Definisce l’elenco dei tag di blocco consentiti. Alcuni dei possibili tag di blocco includono titoli (h1, h2, h3), paragrafi (p), elenchi (ol, ul), tabelle (tabella). |
| `fallbackBlockTag` | `String` | Definisce il tag di blocco utilizzato per tutti i blocchi con un tag di blocco non incluso in `allowBlockTags`. In genere, `p` è sufficiente. |
| `table` | `nt:unstructured` | Definisce il comportamento quando si incollano le tabelle. Questo nodo deve avere la proprietà allow (tipo booleano) per definire se è consentito incollare tabelle. Se consenti è impostato su false, è necessario specificare la proprietà ignoreMode (tipo String) per definire la modalità di gestione del contenuto della tabella incollato. I valori validi per ignoreMode sono `remove` per rimuovere il contenuto della tabella e `paragraph` per trasformare le celle della tabella in paragrafi. |
| `list` | `nt:unstructured` | Definisce il comportamento quando si incollano gli elenchi. Deve avere la proprietà `allow` (tipo booleano) per definire se è consentito incollare gli elenchi. Se `allow` è impostato su `false`, specificare la proprietà `ignoreMode` (tipo `String`) per definire la modalità di gestione del contenuto dell&#39;elenco incollato. I valori validi per ignoreMode sono `remove` che rimuove il contenuto dell&#39;elenco e `paragraph` che trasforma le voci dell&#39;elenco in paragrafi. |

Di seguito è riportato un esempio di struttura `htmlPasteRules` valida:

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

1. Salva tutte le modifiche.

## Configurare gli stili di testo {#textstyles}

Gli autori possono applicare gli stili per modificare l&#39;aspetto di una parte di testo. Gli stili sono basati su classi CSS predefinite nel foglio di stile CSS. Il contenuto stilizzato è racchiuso tra tag `span` che utilizzano l&#39;attributo `class` per fare riferimento alla classe CSS. Ad esempio:

`<span class=monospaced>Monospaced Text Here</span>`

Quando il plug-in Stili viene attivato per la prima volta, non sono disponibili stili predefiniti. L&#39;elenco popup è vuoto. Per fornire agli autori stili, effettuare le seguenti operazioni:

* Abilita il selettore a discesa Stile.
* Specificare una o più posizioni dei fogli di stile.
* Specificate i singoli stili che possono essere selezionati dall&#39;elenco a comparsa degli stili.

Per le riconfigurazioni successive, per aggiungere altri stili, seguire solo le istruzioni per fare riferimento a un nuovo foglio di stile e specificare gli stili aggiuntivi.

>[!NOTE]
>
>È inoltre possibile definire gli stili per [tabelle o celle di tabella](configure-rich-text-editor-plug-ins.md#tablestyles). Queste configurazioni richiedono procedure separate.

### Abilitare l’elenco di selettori a discesa Stile {#styleselectorlist}

Questa operazione viene eseguita abilitando il plug-in stili.

1. Nel componente, passa al nodo `<rtePlugins-node>/styles`. Creare i nodi se non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Creare la proprietà `features` nel nodo `styles`:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valore** `*` (asterisco)

1. Salva tutte le modifiche.

>[!NOTE]
>
>Una volta attivato il plug-in Stili, l’elenco a discesa Stile viene visualizzato nella finestra di dialogo per modifica. Tuttavia, l’elenco è vuoto perché non è configurato alcuno stile.

### Specificare la posizione del foglio di stile {#locationofstylesheet}

Specificare quindi la posizione dei fogli di stile a cui si desidera fare riferimento:

1. Passare al nodo principale del componente di testo, ad esempio `/apps/<myProject>/components/text`.
1. Aggiungere la proprietà `externalStyleSheets` al nodo padre di `<rtePlugins-node>`:

   * **Nome** `externalStyleSheets`
   * **Tipo** `String[]` (multistringa; fare clic su **Multiplo** in CRXDE)
   * **Valori** Il percorso e il nome file di ogni foglio di stile che si desidera includere. Utilizza i percorsi dell’archivio.

   >[!NOTE]
   >
   >È possibile aggiungere riferimenti ad altri fogli di stile in qualsiasi momento successivo.

1. Salva tutte le modifiche.

Quando si utilizza l’editor Rich Text in una finestra di dialogo (interfaccia classica), è possibile specificare fogli di stile ottimizzati per la modifica di testo RTF. A causa di restrizioni tecniche, il contesto CSS viene perso nell’editor, quindi puoi emulare questo contesto per migliorare l’esperienza WYSIWYG.

L&#39;editor Rich Text utilizza un elemento DOM contenitore con un ID di `CQrte` che fornisce stili diversi per visualizzare e modificare:

```css
#CQ td {
// defines the style for viewing
 }
```

```css
#CQrte td {
 // defines the style for editing
 }
```

### Specificare gli stili disponibili nell&#39;elenco a comparsa {#stylesindropdown}

1. Nella definizione del componente, passare al nodo `<rtePlugins-node>/styles`, come creato in [Abilitazione del selettore a discesa degli stili](#styleselectorlist).
1. Nel nodo `styles` creare un nodo (denominato anche `styles`) che contenga l&#39;elenco reso disponibile:

   * **Nome** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Crea un nodo sotto il nodo `styles` per rappresentare un singolo stile:

   * **Nome**, puoi specificare il nome, ma deve essere adatto allo stile
   * **Tipo** `nt:unstructured`

1. Aggiungere la proprietà `cssName` a questo nodo per fare riferimento alla classe CSS:

   * **Nome** `cssName`
   * **Tipo** `String`
   * **Valore** Il nome della classe CSS (senza un &#39;.&#39; precedente.; ad esempio, `cssClass` invece di `.cssClass`)

1. Aggiungere la proprietà `text` allo stesso nodo, che definisce il testo visualizzato nella casella di selezione:

   * **Nome** `text`
   * **Tipo** `String`
   * **Valore** Descrizione dello stile; viene visualizzato nella casella di selezione a discesa Stile.

1. Salva le modifiche.

   Ripeti i passaggi precedenti per ogni stile richiesto.

### Configurare l’editor Rich Text per interruzioni di parola ottimali in giapponese {#jpwordwrap}

Gli autori che utilizzano [!DNL Experience Manager] per l&#39;authoring di contenuti in lingua giapponese possono applicare uno stile ai caratteri per evitare interruzioni di riga laddove non è richiesta un&#39;interruzione. Questo consente agli autori di lasciare che le frasi si interrompano nella posizione desiderata. Lo stile di questa funzionalità si basa sulla classe CSS predefinita nel foglio di stile CSS.

Per creare lo stile che gli autori possono applicare al testo giapponese, effettuare le seguenti operazioni:

1. Crea un nodo sotto il nodo degli stili. Vedere [specificare uno stile](#stylesindropdown).
   * Nome: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Aggiungere la proprietà `cssName` al nodo per fare riferimento alla classe CSS. Questo nome di classe è un nome riservato per la funzione di ritorno a capo automatico giapponese.
   * Nome: `cssName`
   * Tipo: `String`
   * Valore: `jpn-word-wrap` (senza un precedente `.`)

1. Aggiungi il testo della proprietà allo stesso nodo. Il valore è il nome dello stile visualizzato dagli autori durante la selezione dello stile.
   * Nome: `text`
*Tipo: `String`
   * Valore: `Japanese word-wrap`

1. Creare un foglio di stile e specificarne il percorso. Vedere [specificare il percorso del foglio di stile](#locationofstylesheet). Aggiungere il contenuto seguente al foglio di stile. Modifica il colore di sfondo come desiderato.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Foglio di stile per rendere disponibile agli autori la funzionalità di ritorno a capo automatico in giapponese](assets/rte_jpwordwrap_stylesheet.jpg)

## Configurare i formati di paragrafo {#paraformats}

Qualsiasi testo creato nell&#39;editor Rich Text viene inserito all&#39;interno di un tag di blocco. Il valore predefinito è `<p>`. Attivando il plug-in `paraformat`, è possibile specificare ulteriori tag di blocco che possono essere assegnati ai paragrafi utilizzando un elenco a discesa. I formati di paragrafo determinano il tipo di paragrafo assegnando il tag di blocco corretto. L’autore può selezionarli e assegnarli utilizzando il selettore Formato. Gli esempi di tag di blocco includono, tra gli altri, il paragrafo standard &lt;p>, le intestazioni &lt;h1>, &lt;h2> e così via.

>[!CAUTION]
>
>Questo plug-in non è adatto per contenuti con struttura complessa, ad esempio elenchi o tabelle.

>[!NOTE]
>
>Se un tag di blocco, ad esempio un tag `<hr>`, non può essere assegnato a un paragrafo, non è un caso d&#39;uso valido per un plug-in `paraformat`.

Quando il plug-in Formati di paragrafo viene attivato per la prima volta, non sono disponibili formati di paragrafo predefiniti. L&#39;elenco popup è vuoto. Per fornire agli autori i formati di paragrafo, effettuare le seguenti operazioni:

* Abilita l&#39;elenco di selettori popup [!UICONTROL Formato].
* Specificate i tag di blocco che possono essere selezionati come formati di paragrafo dal menu a comparsa.

Per le riconfigurazioni successive, ad esempio per aggiungere altri formati, segui solo la parte pertinente delle istruzioni.

### Abilita il selettore a discesa Formato {#formatselectorlist}

Per abilitare il plug-in `paraformat`, eseguire la procedura seguente:

1. Nel componente, passa al nodo `<rtePlugins-node>/paraformat`. Creare i nodi se non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Creare la proprietà `features` nel nodo `paraformat`:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valore** `*` (asterisco)

>[!NOTE]
>
>Se il plug-in non è configurato ulteriormente, i formati predefiniti abilitati sono Paragrafo ( `<p>`), Intestazione 1 ( `<h1>`), Intestazione 2 ( `<h2>`), Intestazione 3 ( `<h3>`).

>[!CAUTION]
>
>Durante la configurazione dei formati di paragrafo dell’editor Rich Text, non rimuovere il tag di paragrafo &lt;p> come opzione di formattazione. Se il tag `<p>` viene rimosso, l&#39;autore del contenuto non può selezionare l&#39;opzione [!UICONTROL Formati paragrafo] anche se sono configurati altri formati.

### Specificare i formati di paragrafo disponibili {#paraformatsindropdown}

I formati di paragrafo possono essere selezionati da:

1. Nella definizione del componente, passare al nodo `<rtePlugins-node>/paraformat`, come creato in [Abilitazione del selettore a discesa del formato](#styleselectorlist).
1. Nel nodo `paraformat` creare un nodo, che contiene l&#39;elenco dei formati:

   * **Nome** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Crea un nodo sotto il nodo `formats`, contenente i dettagli per un singolo formato:

   * **Nome**, è possibile specificare il nome, ma deve essere appropriato per il formato (ad esempio, miaparagrafo, miaintestazione1).
   * **Tipo** `nt:unstructured`

1. A questo nodo, aggiungi la proprietà per definire il tag di blocco utilizzato:

   * **Nome** `tag`
   * **Tipo** `String`
   * **Valore** Il tag di blocco per il formato, ad esempio: p, h1, h2 e così via.

     Non è necessario inserire le parentesi angolari di delimitazione.

1. Per visualizzare il testo descrittivo nell’elenco a discesa, aggiungi un’altra proprietà allo stesso nodo:

   * **Nome** `description`
   * **Tipo** `String`
   * **Valore** Il testo descrittivo per questo formato, ad esempio Paragrafo, Intestazione 1, Intestazione 2 e così via. Questo testo viene visualizzato nell&#39;elenco di selezione Formato.

1. Salva le modifiche.

   Ripeti i passaggi per ogni formato richiesto.

>[!CAUTION]
>
Se si definiscono formati personalizzati, i formati predefiniti (`<p>`, `<h1>`, `<h2>` e `<h3>`) vengono rimossi. Ricreare il formato `<p>` come predefinito.

## Configurare caratteri speciali {#spchar}

In un&#39;installazione standard di [!DNL Experience Manager], quando il plug-in `misctools` è abilitato per i caratteri speciali (`specialchars`) è immediatamente disponibile una selezione predefinita da utilizzare, ad esempio i simboli di copyright e di marchio.

È possibile configurare l’editor Rich Text in modo da rendere disponibile la selezione di caratteri, definendo caratteri distinti o un’intera sequenza.

>[!CAUTION]
>
L’aggiunta di caratteri speciali sostituisce la selezione predefinita. Se necessario, ridefinisci questi caratteri nella selezione.

### Definisci un singolo carattere {#definesinglechar}

1. Nel componente, passa al nodo `<rtePlugins-node>/misctools`. Creare i nodi se non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Creare la proprietà `features` nel nodo `misctools`:

   * **Nome** `features`
   * **Tipo** `String[]`
   * **Valore** `specialchars`

         (o `String / *` se si applicano tutte le funzionalità per questo plug-in)

1. In `misctools` creare un nodo che contenga le configurazioni dei caratteri speciali:

   * **Nome** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. In `specialCharsConfig` creare un altro nodo che contenga l&#39;elenco dei caratteri:

   * **Nome** `chars`
   * **Tipo** `nt:unstructured`

1. In `chars` aggiungere un nodo che contenga la definizione di un singolo carattere:

   * **Nome** è possibile specificare il nome, ma deve riflettere il carattere, ad esempio metà.
   * **Tipo** `nt:unstructured`

1. A questo nodo aggiungi la seguente proprietà:

   * **Nome** `entity`
   * **Tipo** `String`
   * **Valore** la rappresentazione HTML del carattere richiesto, ad esempio `&189;` per la frazione metà.

1. Salva le modifiche.

In CRXDE, una volta salvata la proprietà, viene visualizzato il carattere rappresentato. Vedi sotto l&#39;esempio di mezzo. Ripeti i passaggi precedenti per rendere disponibili agli autori caratteri più speciali.

![In CRXDE aggiungere un singolo carattere da rendere disponibile nella barra degli strumenti dell&#39;editor Rich Text](assets/chlimage_1-106.png "In CRXDE aggiungere un singolo carattere da rendere disponibile nella barra degli strumenti dell&#39;editor Rich Text")

### Definire un intervallo di caratteri {#definerangechar}

1. Utilizzare i passaggi da 1 a 3 di [Definire un singolo carattere](#definesinglechar).
1. In `chars` aggiungere un nodo che contenga la definizione dell&#39;intervallo di caratteri:

   * **Nome** è possibile specificare il nome, ma deve riflettere l&#39;intervallo di caratteri, ad esempio le matite.
   * **Tipo** `nt:unstructured`

1. Sotto questo nodo (denominato in base all’intervallo di caratteri speciali) aggiungi le due proprietà seguenti:

   * **Nome** `rangeStart`
     **Tipo** `Long`
     **Valore** la rappresentazione [Unicode](https://unicode.org/) (decimale) del primo carattere dell&#39;intervallo

   * **Nome** `rangeEnd`
     **Tipo** `Long`
     **Valore** la rappresentazione [Unicode](https://unicode.org/) (decimale) dell&#39;ultimo carattere nell&#39;intervallo

1. Salva le modifiche.

   Ad esempio, definisci un intervallo da 9998 - 10000 fornisce i seguenti caratteri.

   ![In CRXDE, definire un intervallo di caratteri da rendere disponibili in RTE](assets/chlimage_1-107.png)

   *Figura: in CRXDE, definire un intervallo di caratteri da rendere disponibili in RTE*

   ![I caratteri speciali disponibili nell&#39;editor Rich Text vengono visualizzati agli autori in una finestra popup](assets/rtepencil.png "I caratteri speciali disponibili nell&#39;editor Rich Text vengono visualizzati agli autori in una finestra popup")

## Configurare gli stili di tabella {#tablestyles}

Gli stili vengono in genere applicati al testo, ma è possibile applicare un set separato di stili anche a una tabella o ad alcune celle di tabella. Tali stili sono disponibili per gli autori dalla casella del selettore Stile nella finestra di dialogo Proprietà cella o Proprietà tabella. Gli stili sono disponibili quando si modifica una tabella all’interno di un componente Testo (o derivata) e non nel componente Tabella standard.

>[!NOTE]
>
Puoi definire stili per tabelle e celle solo per l’interfaccia classica.

>[!NOTE]
>
Copiare e incollare tabelle nel componente Editor Rich Text o da esso dipende dal browser. Non è supportato per tutti i browser. Puoi ottenere risultati diversi a seconda della struttura della tabella e del browser. Ad esempio, quando copi e incolla una tabella in un componente Editor Rich Text in Mozilla Firefox nell’interfaccia classica e nell’interfaccia touch, il layout della tabella non viene mantenuto.

1. Nel componente passa al nodo `<rtePlugins-node>/table`. Creare i nodi se non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Creare la proprietà `features` nel nodo `table`:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valore** `*`

   >[!NOTE]
   >
   Se non si desidera abilitare tutte le funzionalità della tabella, è possibile creare la proprietà `features` come:
   >
   * **Tipo** `String[]`
   >
   * **Valore**(i) uno dei seguenti elementi o entrambi, come richiesto:
   * `table` per consentire la modifica delle proprietà della tabella, inclusi gli stili.
   * `cellprops` per consentire la modifica delle proprietà delle celle, inclusi gli stili.

1. Definisci la posizione dei fogli di stile CSS in modo che facciano riferimento a essi. Vedere [Specifica della posizione del foglio di stile](#locationofstylesheet), come quando si definiscono [stili per il testo](#textstyles). La posizione può essere definita se sono stati definiti altri stili.
1. Nel nodo `table` creare i nodi seguenti come richiesto:

   * Per definire gli stili per l&#39;intera tabella (disponibile in **[!UICONTROL Proprietà tabella]**):

      * **Nome** `tableStyles`
      * **Tipo** `cq:WidgetCollection`

   * Per definire gli stili per le singole celle (disponibili in **[!UICONTROL Proprietà cella]**):

      * **Nome** `cellStyles`
      * **Tipo** `cq:WidgetCollection`

1. Creare un nodo (sotto il nodo `tableStyles` o `cellStyles` come appropriato) per rappresentare un singolo stile

   * **Nome** è possibile specificare il nome, ma deve riflettere lo stile.
   * **Tipo** `nt:unstructured`

1. In questo nodo crea le proprietà:

   * Per definire lo stile CSS a cui si fa riferimento,

      * **Nome** `cssName`
      * **Tipo** `String`
      * **Valore** il nome della classe CSS (senza un `.` precedente, ad esempio, `cssClass` invece di `.cssClass`)

   * Per definire un testo descrittivo da visualizzare nel selettore a comparsa:

      * **Nome** `text`
      * **Tipo** `String`
      * **Valore** il testo da visualizzare nell&#39;elenco di selezione

1. Salva tutte le modifiche.

Ripeti i passaggi precedenti per ogni stile richiesto.

### Configurare le intestazioni nascoste nelle tabelle per l’accessibilità {#hiddenheader}

Talvolta è possibile creare tabelle di dati senza testo visivo in un&#39;intestazione di colonna presupponendo che lo scopo dell&#39;intestazione sia implicito dalla relazione visiva della colonna con altre colonne. In questo caso, è necessario fornire testo interno nascosto nella cella dell’intestazione per consentire agli assistenti vocali e altre tecnologie per aiutare i lettori con varie esigenze a comprendere lo scopo della colonna.

Per migliorare l’accessibilità in tali scenari, l’editor Rich Text supporta le celle di intestazione nascoste. Inoltre, fornisce le impostazioni di configurazione relative alle intestazioni nascoste nelle tabelle. Queste impostazioni consentono di applicare stili CSS alle intestazioni nascoste nelle modalità di modifica e anteprima. Per aiutare gli autori a identificare le intestazioni nascoste nella modalità di modifica, includi i seguenti parametri nel codice:

* `hiddenHeaderEditingCSS`: specifica il nome della classe CSS applicata alla cella dell&#39;intestazione nascosta quando viene modificato l&#39;editor Rich Text.
* `hiddenHeaderEditingStyle`: specifica una stringa di stile applicata alla cella di intestazione nascosta quando viene modificato l&#39;editor Rich Text.

Se nel codice specifichi sia CSS che la stringa di stile, la classe CSS ha la precedenza sulla stringa di stile e potrebbe sovrascrivere eventuali modifiche di configurazione apportate dalla stringa di stile.

Per consentire agli autori di applicare CSS sulle intestazioni nascoste nella modalità di anteprima, puoi includere i seguenti parametri nel codice:

* `hiddenHeaderClassName`: specifica il nome della classe CSS applicata alla cella di intestazione nascosta in modalità anteprima.
* `hiddenHeaderStyle`: specifica una stringa di stile applicata alla cella di intestazione nascosta in modalità anteprima.

Se nel codice specifichi sia CSS che la stringa di stile, la classe CSS ha la precedenza sulla stringa di stile e potrebbe sovrascrivere eventuali modifiche di configurazione apportate dalla stringa di stile.

## Aggiungere dizionari per il controllo ortografico {#adddict}

Quando il plug-in spellcheck è attivato, l&#39;editor Rich Text utilizza dizionari per ogni lingua appropriata. Questi vengono quindi selezionati in base alla lingua del sito web utilizzando la proprietà language della sottostruttura o estraendo la lingua dall’URL; ad esempio. il ramo `/en/` è selezionato come inglese, il ramo `/de/` come tedesco.

>[!NOTE]
>
Il messaggio &quot;Controllo ortografico non riuscito&quot;. viene visualizzato se si tenta di controllare una lingua non installata.

Un Experience Manager di installazione standard include i dizionari per:

* Inglese americano (en_us)
* Inglese britannico (en_gb)

>[!NOTE]
>
I dizionari standard si trovano in `/libs/cq/spellchecker/dictionaries`, insieme ai file ReadMe appropriati. Non modificare i file.

Per aggiungere altri dizionari, se necessario, eseguire la procedura seguente.

1. Passa alla pagina [https://extensions.openoffice.org/](https://extensions.openoffice.org/).
1. Seleziona la lingua richiesta e scarica il file ZIP con le definizioni di ortografia. Estrarre il contenuto dell&#39;archivio nel file system.

   >[!CAUTION]
   >
   Sono supportati solo i dizionari nel formato `MySpell` per OpenOffice.org v2.0.1 o versioni precedenti. Poiché i dizionari sono ora file di archivio, si consiglia di verificare l&#39;archivio dopo averlo scaricato.

1. Individua i file .aff e .dic. Mantieni il nome del file in minuscolo. Ad esempio, `de_de.aff` e `de_de.dic`.
1. Caricare i file .aff e .dic nell&#39;archivio in `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
>
Il controllo ortografico dell’editor Rich Text è disponibile su richiesta. Non viene eseguito automaticamente quando si inizia a digitare il testo.
>
Per eseguire il controllo ortografico, selezionare il pulsante Controllo ortografico nella barra degli strumenti. L’editor Rich Text controlla l’ortografia delle parole ed evidenzia le parole con un’ortografia errata.
>
Se si incorporano le modifiche suggerite dal correttore ortografico, lo stato del testo cambia e le parole digitate in modo errato non vengono più evidenziate. Per eseguire il controllo ortografico, selezionare nuovamente il pulsante Controllo ortografico.

## Configurare la dimensione della cronologia per le azioni Annulla e Ripristina {#undohistory}

L’editor Rich Text consente agli autori di annullare o ripristinare alcune delle ultime modifiche. Per impostazione predefinita, nella cronologia vengono memorizzate 50 modifiche. Puoi configurare questo valore come richiesto.

1. Nel componente passa al nodo `<rtePlugins-node>/undo`. Crea questi nodi se non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Nel nodo `undo` creare la proprietà:

   * **Nome** `maxUndoSteps`
   * **Tipo** `Long`
   * **Valore** il numero di passaggi di annullamento che si desidera salvare nella cronologia. Il valore predefinito è 50. Utilizzare `0` per disabilitare completamente le operazioni Annulla/Ripristina.

1. Salva le modifiche.

## Configurare le dimensioni della scheda {#tabsize}

Quando il carattere di tabulazione viene premuto all&#39;interno di un testo, viene inserito un numero predefinito di spazi; per impostazione predefinita, si tratta di tre spazi unificatori e di uno spazio.

Per definire le dimensioni della scheda:

1. Nel componente, passa al nodo `<rtePlugins-node>/keys`. Creare i nodi se non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Nel nodo `keys` creare la proprietà:

   * **Nome** `tabSize`
   * **Tipo** `String`
   * **Valore** il numero di spazi da utilizzare per il tabulatore.

1. Salva le modifiche.

## Imposta margine rientro {#indentmargin}

Quando il rientro è abilitato (impostazione predefinita), è possibile definire la dimensione del rientro:

>[!NOTE]
>
Questa dimensione di rientro viene applicata solo ai paragrafi (blocchi) di testo e non influisce sul rientro degli elenchi effettivi.

1. Nel componente passa al nodo `<rtePlugins-node>/lists`. Crea questi nodi se non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Nel nodo `lists` creare il parametro `identSize`:

   * **Nome**: `identSize`
   * **Tipo**: `Long`
   * **Valore**: numero di pixel necessari per il margine di rientro.

## Configurare l&#39;altezza dello spazio modificabile {#editablespace}

Potete definire l&#39;altezza dello spazio modificabile visualizzato nella finestra di dialogo del componente. La configurazione è applicabile solo quando si utilizza l’editor Rich Text in una finestra di dialogo. La configurazione non modifica l’altezza della finestra di dialogo.

1. Nel nodo `../items/text`, nella definizione della finestra di dialogo per il componente, crea una proprietà:

   * **Nome** `height`
   * **Tipo** `Long`
   * **Valore** l&#39;altezza dell&#39;area di modifica in pixel.

1. Salva le modifiche.

## Configurare stili e protocolli per i collegamenti {#linkstyles}

Quando si aggiungono collegamenti in [!DNL Experience Manager], è possibile definire gli stili CSS da utilizzare e i protocolli da accettare automaticamente. Per configurare la modalità di aggiunta dei collegamenti in [!DNL Experience Manager] da un altro programma, definire le regole di HTML.

1. Con CRXDE Lite, individua il componente testo per il progetto.
1. Creare un nodo allo stesso livello di `<rtePlugins-node>`, ovvero creare il nodo sotto il nodo padre di `<rtePlugins-node>`:

   * **Nome** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   >
   Il nodo `../items/text` ha la proprietà:
   >
   * **Nome** `xtype`
   * **Tipo** `String`
   * **Valore** `richtext`
   >
   La posizione del nodo `../items/text` può variare a seconda della struttura della finestra di dialogo. Due esempi sono `/apps/myProject>/components/text/dialog/items/text` e `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. In `htmlRules` creare un nodo.

   * **Nome** `links`
   * **Tipo** `nt:unstructured`

1. Nel nodo `links` definisci le proprietà come richiesto:

   * Stile CSS per collegamenti interni:

      * **Nome** `cssInternal`
      * **Tipo** `String`
      * **Valore** il nome della classe CSS (senza un &#39;.&#39; precedente; ad esempio, `cssClass` invece di `.cssClass`)

   * Stile CSS per collegamenti esterni

      * **Nome** `cssExternal`
      * **Tipo** `String`
      * **Valore** il nome della classe CSS (senza un &#39;.&#39; precedente; ad esempio, `cssClass` invece di `.cssClass`)

   * Array di **[!UICONTROL protocolli]** validi, inclusi `https://`, `https://`, `file://`, `mailto:` e altri,

      * **Nome** `protocols`
      * **Tipo** `String[]`
      * **Valore** uno o più protocolli

   * **defaultProtocol** (proprietà di tipo **String**): protocollo da utilizzare se l&#39;utente non ne ha specificato esplicitamente uno.

      * **Nome** `defaultProtocol`
      * **Tipo** `String`
      * **Valore** uno o più protocolli predefiniti

   * Definizione di come gestire l’attributo target di un collegamento. Crea un nodo:

      * **Nome** `targetConfig`
      * **Tipo** `nt:unstructured`

     Nel nodo `targetConfig`: definire le proprietà richieste:

      * Specifica la modalità di destinazione:

         * **Nome** `mode`
         * **Tipo** `String`)
         * **Valore**:

            * `auto`: indica che è stata scelta una destinazione automatica

              (specificato dalla proprietà `targetExternal` per i collegamenti esterni o `targetInternal` per i collegamenti interni).

            * `manual`: non applicabile in questo contesto
            * `blank`: non applicabile in questo contesto

      * Destinazione dei collegamenti interni:

         * **Nome** `targetInternal`
         * **Tipo** `String`
         * **Valore** la destinazione per i collegamenti interni (da utilizzare solo quando la modalità è `auto`)

      * Destinazione per i collegamenti esterni:

         * **Nome** `targetExternal`
         * **Tipo** `String`
         * **Valore** la destinazione per i collegamenti esterni (utilizzato solo quando la modalità è `auto`).

1. Salva tutte le modifiche.
