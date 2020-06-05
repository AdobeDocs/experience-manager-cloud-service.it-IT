---
title: Configurare i plug-in Editor Rich Text
description: Scoprite come configurare i plug-in Editor di testo RTF di AEM per abilitare singole funzionalità.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: b5af8cad55c8644ba613370cf65b6a04b3abf9ed
workflow-type: tm+mt
source-wordcount: '4348'
ht-degree: 3%

---


# Configurare i plug-in Editor Rich Text {#configure-the-rich-text-editor-plug-ins}

Le funzionalità RTE sono disponibili tramite una serie di plug-in, ognuno dei quali dispone della proprietà features. È possibile configurare la proprietà features per attivare o disattivare una o più funzioni RTE. Questo articolo descrive come configurare in modo specifico i plug-in RTE.

Per informazioni dettagliate sulle altre configurazioni dell’editor Rich Text, consultate [Configurare l’editor](/help/implementing/developing/extending/rich-text-editor.md)Rich Text.

>[!NOTE]
>
>Quando si lavora con CRXDE Lite, si consiglia di salvare regolarmente le modifiche utilizzando l&#39;opzione [!UICONTROL Salva tutto] .

## Attivare un plug-in e configurare la proprietà features {#activateplugin}

Per attivare un plug-in, effettuate le seguenti operazioni. Alcuni passaggi sono necessari solo quando configurate un plug-in per la prima volta, in quanto i nodi corrispondenti non esistono.

Per impostazione predefinita, `format`, `link`, `list`, `justify`e `control` i plug-in e tutte le relative funzioni sono abilitati nell’editor Rich Text.

>[!NOTE]
>
>Il rispettivo `rtePlugins` nodo è definito `<rtePlugins-node>` come per evitare duplicazioni in questo articolo.

1. Utilizzando CRXDE Lite, individuate il componente di testo per il progetto.
1. Crea il nodo padre di `<rtePlugins-node>` se non esiste, prima di configurare eventuali plug-in RTE:

   * A seconda del componente, i nodi principali sono:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * un nodo di configurazione alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * Sono di tipo: **jcr:PrimaryType** `cq:Widget`
   * Entrambe hanno la seguente proprietà:

      * **Nome** `name`
      * **Tipo** `String`
      * **Valore** `./text`


1. A seconda dell’interfaccia per la quale state configurando, create un nodo `<rtePlugins-node>`, se non esiste:

   * **Nome** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. Di seguito, create un nodo per ciascun plug-in che desiderate attivare:

   * **Tipo** `nt:unstructured`
   * **Denominate** l&#39;ID plug-in del plug-in richiesto

Dopo aver attivato un plug-in, attenetevi alle seguenti linee guida per configurare la `features` proprietà.

|  | Abilitare tutte le funzioni | Abilitare alcune funzionalità specifiche | Disattiva tutte le funzioni |
|---|---|---|---|
| Nome | funzionalità | funzionalità | funzionalità |
| Tipo | Stringa | String[] (multi-stringa; impostare Tipo su Stringa e fare clic su Più in CRXDE Lite) | Stringa |
| Valore | `*` (un asterisco) | impostare uno o più valori di feature | - |

## Comprendere il plug-in più recente {#findreplace}

Il `findreplace` plug-in non richiede alcuna configurazione. Funziona fuori dagli schemi.

Quando si utilizza la funzionalità replace, la stringa replace da sostituire deve essere immessa contemporaneamente alla stringa find. È comunque possibile fare clic su find per cercare la stringa prima di sostituirla. Se la stringa di sostituzione viene immessa dopo aver fatto clic su Trova, la ricerca viene reimpostata all’inizio del testo.

La finestra di dialogo Trova e sostituisci diventa trasparente quando si fa clic su Trova e diventa opaca quando si fa clic su Sostituisci. Questo consente all’autore di rivedere il testo che verrà sostituito dall’autore. Se gli utenti fanno clic su replace all (Sostituisci tutto), la finestra di dialogo viene chiusa e viene visualizzato il numero di sostituzioni effettuate.

## Configurare le modalità Incolla {#pastemodes}

Quando si utilizza l’editor Rich Text, gli autori possono incollare il contenuto in una delle tre modalità seguenti:

* **Modalità** browser: Incolla il testo utilizzando l&#39;implementazione Incolla predefinita del browser. Non è un metodo consigliato in quanto potrebbe introdurre markup indesiderati.

* **Modalità** testo normale: Incolla il contenuto degli Appunti come testo normale. Rimuove tutti gli elementi di stile e formattazione dal contenuto copiato prima di inserirlo nel componente AEM.

* **Modalità** MS Word: Incolla il testo, incluse le tabelle, con la formattazione durante la copia da MS Word. La copia e l&#39;incolla del testo da un&#39;altra origine, ad esempio una pagina Web o MS Excel, non è supportata e viene mantenuta solo la formattazione parziale.

### Configurare le opzioni Incolla disponibili nella barra degli strumenti dell’editor Rich Text  {#configure-paste-options-available-on-the-rte-toolbar}

Nella barra degli strumenti dell’editor Rich Text è possibile fornire agli autori alcune o nessuna di queste tre icone:

* **[!UICONTROL Incolla (Ctrl+V)]**: Può essere preconfigurata per corrispondere a una delle tre modalità Incolla elencate sopra.

* **[!UICONTROL Incolla come testo]**: Fornisce la funzionalità della modalità testo normale.

* **[!UICONTROL Incolla da Word]**: Fornisce la funzionalità della modalità MS Word.

Per configurare l’editor Rich Text in modo da visualizzare le icone richieste, attenetevi alla seguente procedura.

1. Andate al componente, ad esempio `/apps/<myProject>/components/text`.
1. Individuare il nodo `rtePlugins/edit`. Se il nodo non esiste, vedi [attivare un plug-in](#activateplugin) .
1. Create la `features` proprietà sul `edit` nodo e aggiungete una o più funzioni. Salvate tutte le modifiche.

### Configurare il comportamento dell&#39;icona Incolla (Ctrl+V) e della scelta rapida {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Per preconfigurare il comportamento dell&#39;icona **[!UICONTROL Incolla (Ctrl+V)]** , effettuate le seguenti operazioni. Questa configurazione definisce anche il comportamento della scelta rapida da tastiera Ctrl+V che verrà utilizzata dagli autori per incollare il contenuto.

La configurazione consente tre tipi di casi di utilizzo:

* Incolla il testo utilizzando l&#39;implementazione Incolla predefinita del browser. Non è un metodo consigliato in quanto potrebbe introdurre markup indesiderati. Configurato utilizzando `browser` di seguito.

* Incolla il contenuto degli Appunti come testo normale. Rimuove tutti gli elementi di stile e formattazione dal contenuto copiato prima di inserirlo nel componente AEM. Configurato utilizzando `plaintext` di seguito.

* Incolla il testo, incluse le tabelle, con la formattazione durante la copia da MS Word. La copia e l&#39;incolla del testo da un&#39;altra origine, ad esempio una pagina Web o MS Excel, non è supportata e viene mantenuta solo la formattazione parziale. Configurato utilizzando `wordhtml` di seguito.

1. Nel componente, passa al `<rtePlugins-node>/edit` nodo. Creare i nodi se questi non esistono. Per ulteriori informazioni, consultate [Attivare un plug-in](#activateplugin).
1. Nel `edit` nodo create una proprietà utilizzando i seguenti dettagli:

   * **Nome** `defaultPasteMode`
   * **Tipo** `String`
   * **Valore** Una delle modalità Incolla `browser`, `plaintext`o `wordhtml`.

### Configurare i formati consentiti per incollare il contenuto {#pasteformats}

È possibile configurare ulteriormente la modalità Incolla come Microsoft Word (`paste-wordhtml`) in modo da definire in modo esplicito gli stili consentiti quando si incolla in AEM da un altro programma, ad esempio Microsoft Word.

Ad esempio, se per incollare in AEM solo i formati grassetto e gli elenchi devono essere consentiti, potete filtrare gli altri formati. Questa operazione è denominata filtro Incolla configurabile, che può essere eseguita per entrambi:

* [Testo](#pastemodes)
* [Collegamenti](#linkstyles)

Per i collegamenti è inoltre possibile definire i protocolli accettati automaticamente.

Per configurare quali formati sono consentiti quando si incolla del testo in AEM da un altro programma:

1. Nel componente, andate al nodo `<rtePlugins-node>/edit`. Creare i nodi se questi non esistono. Per ulteriori dettagli, consultate [Attivare un plug-in](#activateplugin).
1. Create un nodo sotto il `edit` nodo per mantenere le regole di incolla HTML:

   * **Nome** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Create un nodo in `htmlPasteRules`, per mantenere i dettagli dei formati di base consentiti:

   * **Nome** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Per controllare i singoli formati accettati, creare una o più delle seguenti proprietà sul `allowBasics` nodo:

   * **Nome** `bold`
   * **Nome** `italic`
   * **Nome** `underline`
   * **Nome** `anchor` (per collegamenti e ancoraggi denominati)
   * **Nome** `image`

   Tutte le proprietà sono di **tipo** `Boolean`, quindi in **Valore** appropriato è possibile selezionare o rimuovere il segno di spunta per abilitare o disabilitare la funzionalità.

   >[!NOTE]
   >
   >Se non viene definito in modo esplicito, viene utilizzato il valore predefinito true e il formato viene accettato.

1. Altri formati possono essere definiti anche utilizzando un intervallo di altre proprietà o nodi, applicati anche al `htmlPasteRules` nodo:

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>allowBlockTags</td>
   <td>Stringa[]</td>
   <td><p>Definisce l'elenco dei tag di blocco consentiti.</p> <p>Alcuni possibili tag di blocco:</p>
    <ul>
     <li>titoli (h1, h2, h3)</li>
     <li>paragrafo p)</li>
     <li>lists (ol, ul)</li>
     <li>tabelle (tabella)</li>
    </ul> </td>
  </tr>
  <tr>
   <td>fallbackBlockTag</td>
   <td>Stringa</td>
   <td><p>Definisce il tag blocco utilizzato per tutti i blocchi con un tag blocco non incluso in allowBlockTags.</p> <p> Nella maggior parte dei casi è sufficiente.</p> </td>
  </tr>
  <tr>
   <td>tabella</td>
   <td>nt:unstructured</td>
   <td><p>Definisce il comportamento da applicare quando si incollano le tabelle.<br /> </p> <p>Questo nodo deve avere la proprietà <code>allow</code> (tipo <code>Boolean</code>) per definire se è consentito incollare tabelle.</p> <p>Se <code>allow</code> è impostato su <code>false</code>, è necessario specificare la proprietà <code>ignoreMode</code> (type<code> String</code>) per definire il modo in cui viene gestito il contenuto della tabella incollato. I valori validi per <code>ignoreMode</code> sono:</p>
    <ul>
     <li><code>remove</code>: Rimuove il contenuto della tabella.</li>
     <li><code>paragraph</code>: Trasforma le celle di tabella in paragrafi.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>elenco</td>
   <td>nt:unstructured</td>
   <td><p>Definisce il comportamento da applicare agli elenchi.<br /> </p> <p>Deve avere la proprietà <code>allow</code> (tipo <code>Boolean</code>) per definire se è consentito incollare elenchi.</p> <p>Se <code>allow</code> è impostato su <code>false</code>, è necessario specificare la proprietà <code>ignoreMode</code> (tipo <code>String</code>) per definire la gestione del contenuto dell'elenco incollato. I valori validi per <code>ignoreMode</code> sono:</p>
    <ul>
     <li><code>remove</code>: Rimuove il contenuto dell'elenco.</li>
     <li><code>paragraph</code>: Trasforma le voci di elenco in paragrafi.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Esempio di una `htmlPasteRules` struttura valida:

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

1. Salvate tutte le modifiche.

## Configurare gli stili di testo {#textstyles}

Gli autori possono applicare Stili per modificare l’aspetto di una parte del testo. Gli stili sono basati sulle classi CSS che avete precedentemente definito nel foglio di stile CSS. Il contenuto formattato è racchiuso in `span` tag che utilizzano l&#39; `class` attributo per fare riferimento alla classe CSS. Ad esempio:

`<span class=monospaced>Monospaced Text Here</span>`

Quando il plug-in Stili è attivato per la prima volta, non è disponibile alcun Stili predefinito. L&#39;elenco a comparsa è vuoto. Per fornire agli autori Stili, effettuate le seguenti operazioni:

* Attiva il selettore a discesa Stile.
* Specificare le posizioni dei fogli di stile.
* Specificare i singoli stili che è possibile selezionare dall&#39;elenco a discesa Stile.

Per configurazioni successive (ri)aggiungere altri stili, seguire solo le istruzioni per fare riferimento a un nuovo foglio di stile e specificare gli stili aggiuntivi.

>[!NOTE]
>
>È inoltre possibile definire stili per [tabelle o celle](configure-rich-text-editor-plug-ins.md#tablestyles)di tabella. Queste configurazioni richiedono procedure separate.

### Attiva l&#39;elenco a discesa Stile {#styleselectorlist}

Questa operazione viene eseguita attivando il plug-in per gli stili.

1. Nel componente, andate al nodo `<rtePlugins-node>/styles`. Creare i nodi se questi non esistono. Per ulteriori dettagli, consultate [Attivare un plug-in](#activateplugin).
1. Creare la `features` proprietà sul `styles` nodo:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valore** `*` (asterisco)

1. Salvate tutte le modifiche.

>[!NOTE]
>
>Una volta abilitato il plug-in Stili, l&#39;elenco a discesa Stile viene visualizzato nella finestra di dialogo di modifica. Tuttavia, l&#39;elenco è vuoto in quanto non è configurato alcun stile.

### Specificare la posizione del foglio di stile {#locationofstylesheet}

Quindi, specificare le posizioni dei fogli di stile a cui si desidera fare riferimento:

1. Individuate, ad esempio, il nodo principale del componente di testo `/apps/<myProject>/components/text`.
1. Aggiungete la proprietà `externalStyleSheets` al nodo padre di `<rtePlugins-node>`:

   * **Nome** `externalStyleSheets`
   * **Type** `String[]` (multi-stringa; fate clic su **Multi** in CRXDE)
   * **Valore(i)** Percorso e nome del file di ogni foglio di stile da includere. Utilizzare i percorsi dell&#39;archivio.

   >[!NOTE]
   >
   >È possibile aggiungere riferimenti a fogli di stile aggiuntivi in qualsiasi momento successivo.

1. Salvate tutte le modifiche.

>[!NOTE]
>
>Quando si utilizza l&#39;editor Rich Text in una finestra di dialogo (interfaccia classica) È possibile specificare fogli di stile ottimizzati per la modifica RTF. A causa di restrizioni tecniche, il contesto CSS viene perso nell&#39;editor, quindi potrebbe essere utile emulare questo contesto per migliorare l&#39;esperienza WYSIWYG.
>
>L’Editor Rich Text utilizza un elemento DOM contenitore con un ID `CQrte` che può essere utilizzato per fornire stili diversi per la visualizzazione e la modifica:
>
>
```
>#CQ td {
> // defines the style for viewing
> }
>```
>
>
```
>#CQrte td {
> // defines the style for editing
> }
>```

### Specificare gli stili disponibili nell&#39;elenco a comparsa {#stylesindropdown}

1. Nella definizione del componente, andate al nodo `<rtePlugins-node>/styles`, come creato in [Abilitazione del selettore](#styleselectorlist)a discesa Stile.
1. Sotto il nodo `styles`, creare un nuovo nodo (detto anche `styles`) per rendere disponibile l’elenco:

   * **Nome** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Create un nuovo nodo sotto il `styles` nodo per rappresentare un singolo stile:

   * **Nome**, è possibile specificare il nome, ma deve essere adatto allo stile
   * **Tipo** `nt:unstructured`

1. Aggiungete la proprietà `cssName` a questo nodo per fare riferimento alla classe CSS:

   * **Nome** `cssName`
   * **Tipo** `String`
   * **Valore** Il nome della classe CSS (senza un &#39;.&#39; precedente.; for example, `cssClass` instead of `.cssClass`)

1. Aggiungere la proprietà `text` allo stesso nodo; definisce il testo visualizzato nella casella di selezione:

   * **Nome** `text`
   * **Tipo** `String`
   * **Valore** Descrizione dello stile; viene visualizzata nella casella di selezione a discesa Stile.

1. Salva le modifiche.

   Ripetere i passaggi indicati sopra per ogni stile richiesto.

### Configurare l&#39;editor Rich Text per interruzioni di parole ottimali in giapponese {#jpwordwrap}

Gli autori che utilizzano AEM per creare contenuti in lingua giapponese possono applicare uno stile ai caratteri per evitare interruzioni di riga nei casi in cui non è richiesta un’interruzione. Questo permette agli autori di lasciare le frasi rompere nella posizione desiderata. Lo stile di questa funzionalità è basato sulla classe CSS predefinita nel foglio di stile CSS.

>[!NOTE]
>
>Questa funzione richiede almeno AEM 6.5 Service Pack 1.

Per creare lo stile che gli autori possono applicare al testo giapponese, effettuate le seguenti operazioni:

1. Crea un nuovo nodo sotto il nodo stili. Vedere [specificare un nuovo stile](#stylesindropdown).
   * Nome: `jpn-word-wrap`
   * Tipo: `nt:unstructure

1. Aggiungete la proprietà `cssName` al nodo per fare riferimento alla classe CSS. Questo nome di classe è un nome riservato per la funzione di ritorno a capo automatico in giapponese.
   * Nome: `cssName`
   * Tipo: `String`
   * Valore: `jpn-word-wrap` (senza un precedente `.`)

1. Aggiungere il testo della proprietà allo stesso nodo. Il valore è il nome dello stile che gli autori vedono quando selezionano lo stile.
   * Nome: `text`
*Tipo: `String`
Valore: `Japanese word-wrap`
   * Creare un foglio di stile e specificarne il percorso. Vedere [specificare la posizione del foglio di stile](#locationofstylesheet). Aggiungere il contenuto seguente al foglio di stile. Modificate il colore di sfondo come desiderato.

1. ![Foglio di stile per rendere disponibile agli autori la funzione di ritorno a capo automatico in giapponese](assets/rte_jpwordwrap_stylesheet.jpg)

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   Configurare i formati dei paragrafi {#paraformats}](assets/rte_jpwordwrap_stylesheet.jpg)

## Qualsiasi testo creato nell’editor Rich Text viene inserito all’interno di un tag blocco, con l’impostazione predefinita `<p>`. Attivando il `paraformat` plug-in, è possibile specificare tag di blocco aggiuntivi da assegnare ai paragrafi tramite un elenco a discesa di selezione. I formati di paragrafo determinano il tipo di paragrafo assegnando il tag blocco corretto. L&#39;autore può selezionarli e assegnarli mediante il selettore Formato. I tag blocco di esempio includono, tra l&#39;altro, il paragrafo standard &lt;p>, i titoli &lt;h1>, &lt;h2> e così via.

[!CAUTION]`paraformat`

>[!CAUTION]Questo plug-in non è adatto per contenuti con struttura complessa, come elenchi o tabelle.
>
>[!NOTE]

>[!NOTE]Se un tag blocco, ad esempio un tag &lt;hr>, non può essere assegnato a un paragrafo, non è un caso d&#39;uso valido per un plug-in in paraformat.
>
>Quando il plug-in Formati paragrafo è attivato per la prima volta, non sono disponibili formati paragrafo predefiniti. L&#39;elenco a comparsa è vuoto. Per fornire agli autori i formati di paragrafo, effettuate le seguenti operazioni:

Attiva l&#39;elenco a discesa Formato.

* Specificate i tag di blocco che possono essere selezionati come formati di paragrafo dall&#39;elenco a discesa.
* Per configurazioni successive (ri)aggiungete altri formati, seguite solo la parte pertinente delle istruzioni.

Attiva il selettore a discesa Formato {#formatselectorlist}

### Innanzitutto, attivate il plug-in paraformat:{#formatselectorlist}

Nel componente, andate al nodo `<rtePlugins-node>/paraformat`. Creare i nodi se questi non esistono. Per ulteriori dettagli, consultate [Attivare un plug-in](#activateplugin).

1. Creare la `features` proprietà sul `paraformat` nodo:](#activateplugin)
1. **Nome** `features`

   * **Tipo** `String`
   * **Valore** `*` (asterisco)
   * [!NOTE]**`*`

>[!NOTE]Se il plug-in non è configurato ulteriormente, vengono attivati i seguenti formati predefiniti:
Paragrafo ( `<p>`)
* Intestazione 1 ( `<h1>`)
* Intestazione 2 ( `<h2>`)
* Intestazione 3 ( `<h3>`)
* [!CAUTION]



>Durante la configurazione dei formati di paragrafo dell’editor Rich Text, non rimuovere il tag di paragrafo &lt;p> come opzione di formattazione. Se il `<p>` tag viene rimosso, l’autore del contenuto non può selezionare l’opzione Formati **di** paragrafo anche se sono configurati formati aggiuntivi.
Specificare i formati di paragrafo disponibili {#paraformatsindropdown}****

### I formati dei paragrafi possono essere resi disponibili per la selezione tramite:{#paraformatsindropdown}

Nella definizione del componente, andate al nodo `<rtePlugins-node>/paraformat`, come creato in [Abilitazione del selettore](#styleselectorlist)a discesa del formato.

1. Sotto il `paraformat` nodo creare un nuovo nodo, per contenere l&#39;elenco dei formati:[](#styleselectorlist)
1. **Nome** `formats`

   * **Tipo** `cq:WidgetCollection`
   * Crea un nuovo nodo sotto il `formats` nodo, che contiene i dettagli per un singolo formato:**`cq:WidgetCollection`

1. **Nome**, è possibile specificare il nome, ma deve essere adatto al formato (ad esempio, myparagraph, myheading1).

   * **Tipo** `nt:unstructured`
   * **A questo nodo, aggiungere la proprietà per definire il tag blocco utilizzato:**`nt:unstructured`

1. **Nome** `tag`

   * **Tipo** `String`
   * **Valore** Il tag block per il formato; ad esempio: p, h1, h2, ecc.`String`
   * **Non è necessario inserire le parentesi angolari di delimitazione.**

      Per visualizzare il testo descrittivo nell&#39;elenco a discesa, aggiungere un&#39;altra proprietà allo stesso nodo:

1. **Nome** `description`

   * **Tipo** `String`
   * **Valore** Il testo descrittivo per questo formato; ad esempio, Paragrafo, Intestazione 1, Intestazione 2 e così via. Questo testo viene visualizzato nell&#39;elenco di selezione Formato.`String`
   * **Salva le modifiche.**

1. Ripetere i passaggi per ciascun formato richiesto.

   [!CAUTION]

>Se si definiscono formati personalizzati, i formati predefiniti (`<p>`, `<h1>`, `<h2>`e `<h3>`) vengono rimossi. Create nuovamente `<p>` il formato predefinito.
Configurare i caratteri speciali {#spchar}`<h1>``<h2>``<h3>``<p>`

## In un’installazione standard di AEM, quando il `misctools` plug-in è abilitato per caratteri speciali (`specialchars`) è immediatamente disponibile per l’uso una selezione predefinita; ad esempio, i simboli di copyright e marchio.

È possibile configurare l’editor Rich Text per rendere disponibile la propria selezione di caratteri; mediante la definizione di caratteri distinti o di un&#39;intera sequenza.`misctools``specialchars`

[!CAUTION]

>[!CAUTION]Se si aggiungono caratteri speciali, la selezione predefinita viene ignorata. Se necessario, (ri)definite questi caratteri nella vostra selezione.
Definire un singolo carattere {#definesinglechar}

### Nel componente, andate al nodo `<rtePlugins-node>/misctools`. Creare i nodi se questi non esistono. Per ulteriori dettagli, consultate [Attivare un plug-in](#activateplugin).

1. Creare la `features` proprietà sul `misctools` nodo:](#activateplugin)
1. **Nome** `features`

   * **Tipo** `String[]`
   * **Valore** `specialchars`
   *     (o `String / *` se si applicano tutte le funzioni per questo plug-in)**`specialchars`

      In `misctools` Crea un nodo per contenere le configurazioni di caratteri speciali:

1. **Nome** `specialCharsConfig`

   * **Tipo** `nt:unstructured`
   * In `specialCharsConfig` Crea un altro nodo per contenere l’elenco di caratteri:**`nt:unstructured`

1. **Nome** `chars`

   * **Tipo** `nt:unstructured`
   * In `chars` Aggiungi un nuovo nodo per contenere una singola definizione di carattere:**`nt:unstructured`

1. **Il nome** può essere specificato, ma deve riflettere il carattere; ad esempio, metà.

   * **Tipo** `nt:unstructured`
   * **A questo nodo aggiungere la seguente proprietà:**`nt:unstructured`

1. **Nome** `entity`

   * **Tipo** `String`
   * **Valutare** la rappresentazione HTML del carattere richiesto; ad esempio, `&189;` per la frazione di una metà.
   * **Salva le modifiche.**`&189;`

1. In CRXDE, una volta salvata la proprietà, viene visualizzato il carattere rappresentato. Vedi sotto l&#39;esempio della metà. Ripetete i passaggi indicati sopra per rendere disponibili agli autori altri caratteri speciali.

![In CRXDE, aggiungere un singolo carattere da rendere disponibile nella](assets/chlimage_1-106.png "barra degli strumenti dell’editor Rich TextIn CRXDE, aggiungere un singolo carattere da rendere disponibile nella barra degli strumenti dell’editor Rich Text")

Definire un intervallo di caratteri {#definerangechar}](assets/chlimage_1-106.png "")

### Utilizzate i passaggi da 1 a 3 della sezione [Definizione di un singolo carattere](#definingasinglecharacter).

1. In `chars` Aggiungi un nuovo nodo per contenere la definizione dell&#39;intervallo di caratteri:](#definingasinglecharacter)
1. **Il nome** può essere specificato, ma deve riflettere l’intervallo di caratteri; ad esempio, matite.

   * **Tipo** `nt:unstructured`
   * **Sotto questo nodo (denominato in base all&#39;intervallo di caratteri speciale) aggiungere le due seguenti proprietà:**`nt:unstructured`

1. **Nome** `rangeStart`


   * **Tipo** `Long`
      **Valore** della rappresentazione [Unicode[#$tu253] (decimale) del primo carattere dell&#39;intervallo      

   * **Tipo** `Long`
      **Valore** della rappresentazione [Unicode[#$tu257] (decimale) dell&#39;ultimo carattere dell&#39;intervallo      

1. Ad esempio, definire un intervallo compreso tra 9998 e 10000 contiene i seguenti caratteri.

   ![In CRXDE, definire un intervallo di caratteri da rendere disponibili in RTE](assets/chlimage_1-107.png)

   *Figura: In CRXDE, definire un intervallo di caratteri da rendere disponibili in RTE*

   ![I caratteri speciali disponibili nell’editor Rich Text vengono visualizzati dagli autori in una](assets/rtepencil.png "finestra a comparsaI caratteri speciali disponibili nell’editor Rich Text vengono visualizzati dagli autori in una finestra a comparsa")

   Configurare gli stili di tabella {#tablestyles}](assets/rtepencil.png "")

## Gli stili vengono in genere applicati al testo, ma su una tabella o su alcune celle di tabella è possibile applicare un set separato di stili. Tali stili sono disponibili per gli autori dalla casella di selezione Stile della finestra di dialogo Proprietà cella o Proprietà tabella. Gli stili sono disponibili quando si modifica una tabella all’interno di un componente Testo (o derivato) e non nel componente Tabella standard.{#tablestyles}

[!NOTE]

>[!NOTE]È possibile definire stili per tabelle e celle solo per l&#39;interfaccia classica.
[!NOTE]

>[!NOTE]Copiare e incollare tabelle in o dal componente RTE dipende dal browser. Non è supportato out-of-box per tutti i browser. È possibile ottenere risultati variabili a seconda della struttura della tabella e del browser. Ad esempio, quando copiate e incollate una tabella in un componente RTE in Mozilla Firefox nell’interfaccia classica e Touch, il layout della tabella non viene mantenuto.
All’interno del componente, andate al nodo `<rtePlugins-node>/table`. Creare i nodi se questi non esistono. Per ulteriori dettagli, consultate [Attivare un plug-in](#activateplugin).

1. Creare la `features` proprietà sul `table` nodo:](#activateplugin)
1. **Nome** `features`

   * **Tipo** `String`
   * **Valore** `*`
   * [!NOTE]**`*`

   >Se non si desidera abilitare tutte le funzionalità della tabella, è possibile creare la `features` proprietà come:
   **Tipo** `String[]`
   * **Valore** uno o entrambi dei valori seguenti, a seconda delle necessità:`String[]`

   * `table` consentire la modifica delle proprietà della tabella; inclusi gli stili.**
      * `cellprops` per consentire la modifica delle proprietà delle celle, inclusi gli stili.
      * Definire la posizione dei fogli di stile CSS per farvi riferimento. Vedere [Specifica della posizione del foglio](#locationofstylesheet) di stile, identica a quella utilizzata per definire [gli stili per il testo](#textstyles). La posizione può essere definita se avete definito altri stili.


1. Sotto il `table` nodo creare i seguenti nuovi nodi (come richiesto):](#locationofstylesheet)[](#textstyles)
1. Per definire gli stili per l&#39;intera tabella (disponibili in Proprietà **** tabella):

   * **Nome** `tableStyles`

      * **Tipo** `cq:WidgetCollection`
      * Per definire gli stili per le singole celle (disponibili in Proprietà **** cella):`cq:WidgetCollection`
   * **Nome** `cellStyles`

      * **Tipo** `cq:WidgetCollection`
      * Create un nuovo nodo (sotto il nodo `tableStyles` o `cellStyles` secondo quanto appropriato) per rappresentare un singolo stile:`cq:WidgetCollection`


1. **Il nome** può essere specificato, ma deve riflettere lo stile.

   * **Tipo** `nt:unstructured`
   * **In questo nodo creare le proprietà:**`nt:unstructured`

1. Definizione dello stile CSS a cui fare riferimento

   * **Nome** `cssName`

      * **Tipo** `String`
      * **Valore** del nome della classe CSS (senza un precedente, `.`ad esempio, `cssClass` anziché `.cssClass`)
      * **Definizione di un testo descrittivo da visualizzare nel selettore a discesa**`.``cssClass``.cssClass`
   * **Nome** `text`

      * **Tipo** `String`
      * **Valutare** il testo da visualizzare nell&#39;elenco di selezione`String`
      * **Salvate tutte le modifiche.**


1. Ripetere i passaggi indicati sopra per ogni stile richiesto.

Configurare le intestazioni nascoste nelle tabelle per l&#39;accessibilità {#hiddenheader}

### A volte è possibile creare tabelle di dati senza testo visivo in un&#39;intestazione di colonna, partendo dal presupposto che lo scopo dell&#39;intestazione sia determinato dalla relazione visiva della colonna con altre colonne. In questo caso, è necessario fornire testo interno nascosto all&#39;interno della cella nella cella di intestazione per consentire agli assistenti vocali e altre tecnologie di assistenza di aiutare i lettori con varie esigenze a comprendere lo scopo della colonna.{#hiddenheader}

Per migliorare l’accessibilità in tali scenari, l’editor Rich Text supporta le celle di intestazione nascoste. Inoltre, fornisce le impostazioni di configurazione relative alle intestazioni nascoste nelle tabelle. Queste impostazioni consentono di applicare stili CSS alle intestazioni nascoste nelle modalità di modifica e anteprima. Per aiutare gli autori a identificare le intestazioni nascoste nella modalità di modifica, includete nel codice i seguenti parametri:

`hiddenHeaderEditingCSS`: Specifica il nome della classe CSS applicata alla cella di intestazione nascosta quando viene modificato l&#39;editor Rich Text.

* `hiddenHeaderEditingStyle`: Specifica una stringa di stile applicata alla cella di intestazione nascosta quando viene modificato l&#39;editor Rich Text.
* `hiddenHeaderEditingStyle`Se specificate sia il CSS che la stringa Stile nel codice, la classe CSS ha la precedenza sulla stringa di stile e potrebbe sovrascrivere eventuali modifiche alla configurazione apportate dalla stringa Stile.

Per aiutare gli autori ad applicare CSS sulle intestazioni nascoste nella modalità di anteprima, potete includere nel codice i seguenti parametri:

`hiddenHeaderClassName`: Specifica il nome della classe CSS applicata alla cella di intestazione nascosta in modalità di anteprima.

* `hiddenHeaderStyle`: Specifica una stringa di stile applicata alla cella di intestazione nascosta in modalità di anteprima.
* `hiddenHeaderStyle`Se specificate sia il CSS che la stringa Stile nel codice, la classe CSS ha la precedenza sulla stringa di stile e potrebbe sovrascrivere eventuali modifiche alla configurazione apportate dalla stringa Stile.

Aggiunta di dizionari per il controllo ortografia {#adddict}

## Quando il plug-in per il controllo ortografia è attivato, l&#39;editor Rich Text utilizza i dizionari per ciascuna lingua appropriata. Questi vengono quindi selezionati in base alla lingua del sito Web, ottenendo la proprietà language della struttura ad albero secondaria o estraendo la lingua dall’URL; ad esempio. il `/en/` ramo è controllato come inglese, il `/de/` ramo come tedesco.

[!NOTE]`/de/`

>[!NOTE]Messaggio &quot;Controllo ortografia non riuscito&quot;. viene visualizzato se viene provato un controllo per una lingua non installata.
Un’installazione standard di AEM include dizionari per:

Inglese americano (en_us)

* Inglese britannico (en_gb)
* [!NOTE]

>I dizionari standard si trovano in `/libs/cq/spellchecker/dictionaries`, insieme ai file Leggimi appropriati. Non modificate i file.
Per aggiungere altri dizionari, se necessario, procedere come segue.`/libs/cq/spellchecker/dictionaries`

Passate alla pagina [https://extensions.openoffice.org/[#$tu323].

1. 
1. [!CAUTION]

   >Sono supportati solo i dizionari nel `MySpell` formato per OpenOffice.org v2.0.1 o versioni precedenti. Poiché i dizionari ora sono file di archivio, si consiglia di verificare l&#39;archivio dopo il download.
   Individuate i file .aff e .dic. Mantieni il nome del file in lettere minuscole. Ad esempio `de_de.aff` e `de_de.dic`.

1. Caricate i file .aff e .dic nella directory archivio `/apps/cq/spellchecker/dictionaries`.`de_de.dic`
1. [!NOTE]

>[!NOTE]Il controllo ortografia RTE è disponibile su richiesta. Non viene eseguito automaticamente quando si inizia a digitare del testo.
Per eseguire il controllo ortografia, toccate o fate clic sul pulsante Controllo ortografia nella barra degli strumenti. L’editor Rich Text controlla l’ortografia delle parole e evidenzia le parole con errori di ortografia.
Se si incorporano modifiche suggerite dal controllo ortografia, lo stato del testo cambia e le parole con errori di ortografia non vengono più evidenziate. Per eseguire il controllo ortografia, toccate o fate di nuovo clic sul pulsante Controllo ortografia.
Configurare la dimensione della cronologia per le azioni di annullamento e ripristino {#undohistory}

## L’editor Rich Text consente agli autori di annullare o ripristinare alcune ultime modifiche. Per impostazione predefinita, nella cronologia sono memorizzate 50 modifiche. Puoi configurare questo valore come necessario.{#undohistory}

All’interno del componente, andate al nodo `<rtePlugins-node>/undo`. Creare questi nodi se non esistono. Per ulteriori dettagli, consultate [Attivare un plug-in](#activateplugin).

1. Sul `undo` nodo creare la proprietà:[](#activateplugin)
1. **Nome** `maxUndoSteps`

   * **Tipo** `Long`
   * **Valore** del numero di passaggi di annullamento da salvare nella cronologia. Il valore predefinito è 50. Utilizzare `0` per disattivare completamente Annulla/Ripristina.
   * **Salva le modifiche.**`0`

1. Configurare le dimensioni della scheda {#tabsize}

## Quando il carattere di tabulazione viene premuto all&#39;interno di un testo, viene inserito un numero predefinito di spazi; per impostazione predefinita si tratta di tre spazi unificatori e uno spazio.{#tabsize}

Per definire la dimensione della scheda:

Nel componente, andate al nodo `<rtePlugins-node>/keys`. Creare i nodi se questi non esistono. Per ulteriori dettagli, consultate [Attivare un plug-in](#activateplugin).

1. Sul `keys` nodo creare la proprietà:[](#activateplugin)
1. **Nome** `tabSize`

   * **Tipo** `String`
   * **Valore** il numero di caratteri di spazio da utilizzare per la tabulazione.`String`
   * **Salva le modifiche.**

1. Imposta margine rientro {#indentmargin}

## Quando il rientro è abilitato (impostazione predefinita), puoi definire la dimensione del rientro:{#indentmargin}

[!NOTE]

>[!NOTE]Questa dimensione del rientro è applicata solo ai paragrafi (blocchi) di testo; non incide sul rientro degli elenchi effettivi.
All’interno del componente, andate al nodo `<rtePlugins-node>/lists`. Creare questi nodi se non esistono. Per ulteriori dettagli, consultate [Attivare un plug-in](#activateplugin).

1. Sul `lists` nodo create il `identSize` parametro:](#activateplugin)
1. **Nome**: `identSize`

   * **Tipo**: `Long`
   * **Valore**: numero di pixel necessari per il margine di rientro.`Long`
   * Configurare l&#39;altezza dello spazio modificabile {#editablespace}**

## [!NOTE]

>[!NOTE]Questo è applicabile solo quando si utilizza l’editor Rich Text in una finestra di dialogo (non durante la modifica locale nell’interfaccia classica).
È possibile definire l’altezza dello spazio modificabile visualizzato nella finestra di dialogo del componente:

Sul `../items/text` nodo nella definizione della finestra di dialogo per il componente, create una nuova proprietà:

1. **Nome** `height`

   * **Tipo** `Long`
   * **Specificate** l’altezza del quadro di modifica in pixel.`Long`
   * [!NOTE]**

   >[!NOTE]L&#39;altezza della finestra di dialogo non viene modificata.
   Salva le modifiche.

1. Configurare stili e protocolli per i collegamenti {#linkstyles}

## Quando aggiungete collegamenti in AEM, potete definire:{#linkstyles}

Stili CSS da utilizzare

* I protocolli automaticamente accettati
* Per configurare la modalità in cui i collegamenti vengono aggiunti in AEM da un altro programma, definite le regole HTML.

Utilizzando CRXDE Lite, individuate il componente di testo per il progetto.

1. Crea un nuovo nodo allo stesso livello `<rtePlugins-node>`, ovvero crea il nodo sotto il nodo principale di `<rtePlugins-node>`:
1. **Nome** `htmlRules`

   * **Tipo** `nt:unstructured`
   * [!NOTE]**`nt:unstructured`

   >Il `../items/text` nodo ha la proprietà:
   **Nome** `xtype`
   * **Tipo** `String`
   * **Valore** `richtext`
   * La posizione del `../items/text` nodo può variare, a seconda della struttura del dialogo; due esempi:**`richtext`

   `/apps/myProject>/components/text/dialog/items/text`
   * `/apps/<myProject>/components/text/dialog/items/panel/items/text`
   * In `htmlRules`, creare un nuovo nodo.


1. **Nome** `links`

   * **Tipo** `nt:unstructured`
   * Sotto il `links` nodo definire le proprietà come richiesto:**`nt:unstructured`

1. Stile CSS per collegamenti interni:`links`

   * **Nome** `cssInternal`

      * **Tipo** `String`
      * **Valore** il nome della classe CSS (senza un &#39;.&#39; precedente.; for example, `cssClass` instead of `.cssClass`)
      * **Stile CSS per collegamenti esterni**`cssClass``.cssClass`
   * **Nome** `cssExternal`

      * **Tipo** `String`
      * **Valore** il nome della classe CSS (senza un &#39;.&#39; precedente.; for example, `cssClass` instead of `.cssClass`)
      * Array di **protocolli** validi (tra cui https://, https:// file://, mailto:, ecc.)`cssClass``.cssClass`
   * **Nome** `protocols`

      * **Tipo** `String[]`
      * **Valori** uno o più protocolli`String[]`
      * **defaultProtocol** (proprietà di tipo **String**): Protocollo da utilizzare se l&#39;utente non ne ha specificato uno in modo esplicito.
   * **Nome** `defaultProtocol`**

      * **Tipo** `String`
      * **Valori** uno o più protocolli predefiniti`String`
      * **Definizione di come gestire l&#39;attributo target di un collegamento. Crea un nuovo nodo:**
   * **Nome** `targetConfig`

      * **Tipo** `nt:unstructured`
      * Sul nodo `targetConfig`: definire le proprietà richieste:**`nt:unstructured`

      Specificate la modalità di destinazione:`targetConfig`

      * **Nome** `mode`

         * **Tipo** `String`)
         * **Valore**:`String`
         * `auto`: indica che è selezionata una destinazione automatica**

            * (specificata dalla `targetExternal` proprietà per i collegamenti esterni o `targetInternal` per i collegamenti interni).

               `manual`: non applicabile in questo contesto`targetInternal`

            * `blank`: non applicabile in questo contesto
            * `blank`Destinazione dei collegamenti interni:
      * **Nome** `targetInternal`

         * **Tipo** `String`
         * **Valore** della destinazione per i collegamenti interni (utilizzare solo quando &quot;mode is `auto`&quot;)
         * **Destinazione per i collegamenti esterni:**`auto`
      * **Nome** `targetExternal`

         * **Tipo** `String`
         * **Valutare** la destinazione per i collegamenti esterni (utilizzata solo quando la modalità è `auto`).
         * **Salvate tutte le modifiche.**`auto`








1. Save all changes.
