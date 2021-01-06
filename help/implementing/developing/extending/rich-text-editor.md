---
title: Configurate Editor Rich Text per creare contenuto in [!DNL Adobe Experience Manager] come Cloud Service.
description: Configurate Editor Rich Text per creare contenuto in [!DNL Adobe Experience Manager] come Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 739dde6f9a6a7f4fe773e27e53f23a395f2881dc
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 1%

---


# Configurare l&#39;Editor Rich Text {#configure-the-rich-text-editor}

L’editor Rich Text (RTE) offre agli autori un’ampia gamma di funzionalità per la modifica del contenuto di testo. Le icone, le caselle di selezione, la barra degli strumenti e i menu sono disponibili per un’esperienza di modifica del testo WYSIWYG. Gli amministratori configurano l’editor Rich Text per attivare, disattivare ed estendere le funzioni disponibili nei componenti di authoring. Scopri in che modo gli autori [utilizzano l&#39;editor Rich Text per creare contenuti Web](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md).

I concetti e i passaggi necessari per la configurazione dell’editor Rich Text sono elencati di seguito.

| Comprendere i concetti relativi all’editor Rich Text | Abilitare le funzioni richieste | Configurare le singole funzionalità |
|---|---|---|
| [Comprendere l&#39;interfaccia](#understand-rte-ui) | [Comprendere e impostare le posizioni di configurazione](#understand-the-configuration-paths-and-locations) | [Configurare i plug-in](#enable-rte-functionalities-by-activating-plug-ins) |
| [Tipi di modalità di modifica](#editingmodes) | [Attivare i plug-in](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Impostazione delle proprietà delle funzioni](#aboutplugins) |
| [Informazioni sui plug-in](#aboutplugins) | [Configurare le barre degli strumenti RTE](#dialogfullscreen) | [Configurare le modalità Incolla](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## Comprendere l&#39;interfaccia utente disponibile per gli autori {#understand-rte-ui}

L&#39;interfaccia RTE offre un [design reattivo](/help/sites-cloud/authoring/features/responsive-layout.md) per l&#39;ambiente di authoring. L&#39;interfaccia è progettata per essere utilizzata su dispositivi touch e desktop.

![Barra degli strumenti Editor Rich Text](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra degli strumenti Editor Rich Text con tutte le opzioni disponibili abilitate.*

La barra degli strumenti fornisce le opzioni per l’esperienza di authoring WYSIWYG. [!DNL Experience Manager] gli amministratori possono configurare le opzioni disponibili nella barra degli strumenti dell’interfaccia. Per impostazione predefinita, in [!DNL Experience Manager] è disponibile un set completo di opzioni di modifica. Gli sviluppatori possono personalizzare [!DNL Experience Manager] per aggiungere altre opzioni di modifica.

## Varie modalità di modifica {#editingmodes}

Gli autori possono creare e modificare contenuti testuali in [!DNL Experience Manager] utilizzando le diverse modalità di componenti. Le opzioni della barra degli strumenti per la creazione e formattazione di contenuti e l’esperienza utente dei componenti abilitati all’editor Rich Text in modalità di modifica diversa variano in base alle configurazioni dell’editor Rich Text.

| Modalità di modifica | Area di modifica | Funzioni consigliate da abilitare |
|--- |--- |--- |
| In linea | Modifica diretta per modifiche rapide e secondarie; Formato senza aprire una finestra di dialogo. | Funzioni RTE minime. |
| Schermo intero RTE | Copre l’intera pagina. | Tutte le funzioni RTE richieste. |
| Finestra di dialogo | Finestra di dialogo sopra al contenuto della pagina, ma non copre l’intera pagina. | Abilitare le funzionalità in modo appropriato. |
| Finestra di dialogo a schermo intero | Come modalità a schermo intero; contiene i campi della finestra di dialogo accanto a RTE. | Tutte le funzioni RTE richieste. |

>[!NOTE]
>
>La funzione di modifica sorgente non è disponibile in modalità di modifica in linea. Non è possibile trascinare le immagini in modalità schermo intero. Tutte le altre funzioni funzionano in tutte le modalità.

### Modifica in linea {#inline-editing}

Per modificare il contenuto di una pagina, aprite il contenuto con un doppio clic lento . Viene visualizzata una barra degli strumenti compatta con le opzioni di base.

![Modifica in linea con le opzioni di base nella barra degli strumenti](assets/inline-editing-mode-basic-options.png)

*Figura: Modifica in linea con le opzioni di base nella barra degli strumenti.*

### Modifica a tutto schermo {#full-screen-editing}

[!DNL Experience Manager] i componenti possono essere aperti nella visualizzazione a schermo intero che nasconde il contenuto della pagina e occupa la schermata disponibile. Considerate la possibilità di modificare a schermo intero una versione dettagliata dell&#39;editing in linea in quanto offre il maggior numero di opzioni di modifica. È possibile aprirlo facendo clic su ![Icona per aprire l&#39;editor Rich Text a schermo intero](assets/rte_fullscreen.png), dalla barra degli strumenti compatta quando si utilizza la modalità di modifica in linea.

Nella finestra di dialogo a schermo intero, insieme a una barra degli strumenti dettagliata dell’editor Rich Text, sono disponibili anche le opzioni e i componenti disponibili in una finestra di dialogo. È applicabile solo per una finestra di dialogo che contiene l’editor Rich Text insieme ad altri componenti.

![Barra degli strumenti RTE dettagliata durante la modifica in modalità a schermo intero](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra degli strumenti RTE dettagliata durante la modifica in modalità a schermo intero.*

### Modifica finestra di dialogo {#dialog-editing}

Quando si fa doppio clic su un componente, si apre una finestra di dialogo per la modifica del contenuto. Viene visualizzata la finestra di dialogo sopra la pagina esistente. In alcuni scenari specifici, la finestra di dialogo si apre come finestra a comparsa. Ad esempio, quando un componente Testo fa parte di una colonna in un layout di pagina con più colonne e l’area disponibile per la finestra di dialogo è minore.

![Modalità di modifica finestra di dialogo](assets/dialog_editing_modetouchui.png)

*Figura: Modalità di modifica finestra di dialogo.*

## Informazioni sui plug-in RTE e sulle funzionalità associate {#aboutplugins}

La funzionalità è disponibile tramite una serie di plug-in, ognuno dei quali è dotato di:

* Una proprietà `features`, ovvero

   * Utilizzato per attivare o disattivare le funzionalità di base di tale plug-in.
   * Configurato utilizzando una procedura standard.

* Se appropriato, più proprietà e opzioni richiedono una configurazione specializzata.

Le funzioni di base dell&#39;editor Rich Text sono attivate o disattivate dal valore della proprietà `features` su un nodo specifico del plug-in appropriato.

Nella tabella seguente sono elencati i plug-in correnti, che mostrano:

* ID plug-in con un collegamento alla documentazione API. L&#39;ID viene utilizzato come nome del nodo quando si attiva [un plug-in](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valori consentiti per la proprietà `features`.
* Una descrizione delle funzionalità fornite dal plug-in.

| ID plug-in | funzionalità | Descrizione |
|--- |--- |--- |
| modifica | `cut`,  `copy`,  `paste-default`,  `paste-plaintext`,  `paste-wordhtml` | [Tagliare, copiare e incollare le tre modalità](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles). |
| [punto](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | `find`, `replace` | Trova e sostituisci. |
| [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | `bold`, `italic`, `underline` | [Formattazione](configure-rich-text-editor-plug-ins.md#textstyles) di base del testo. |
| [immagine](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | `image` | Supporto per immagini di base (trascinate da Content Finder). A seconda del browser, il supporto ha diversi comportamenti per gli autori |
| [keys](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) | - | Per definire questo valore, vedere [dimensioni scheda](configure-rich-text-editor-plug-ins.md#tabsize). |
| [justify](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | `justifyleft`,  `justifycenter`,  `justifyright` | Allineamento del paragrafo. |
| [links](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | `modifylink`,  `unlink`,  `anchor` | [Collegamenti ipertestuali e ancoraggi](configure-rich-text-editor-plug-ins.md#linkstyles). |
| [list](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | `ordered`,  `unordered`,  `indent`,  `outdent` | Questo plug-in controlla sia il rientro [che gli elenchi](configure-rich-text-editor-plug-ins.md#indentmargin); inclusi gli elenchi nidificati. |
| [cattivi](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | `specialchars`,  `sourceedit` | Gli strumenti vari consentono agli autori di immettere [caratteri speciali](configure-rich-text-editor-plug-ins.md#spchar) o modificare l&#39;origine HTML. È inoltre possibile aggiungere un [intervallo di caratteri speciali](configure-rich-text-editor-plug-ins.md#definerangechar) se si desidera definire un proprio elenco. |
| Paraformat | `paraformat` | I formati di paragrafo predefiniti sono Paragrafo, Intestazione 1, Intestazione 2 e Intestazione 3 (`<p>`, `<h1>`, `<h2>` e `<h3>`). È possibile [aggiungere altri formati di paragrafo](configure-rich-text-editor-plug-ins.md#paraformats) o estendere l&#39;elenco. |
| controllo ortografia | `checktext` | [Controllo](configure-rich-text-editor-plug-ins.md#adddict) ortografia basato sulla lingua |
| stili | `styles` | Supporto per lo stile con una classe CSS. [Aggiungete un nuovo stile ](configure-rich-text-editor-plug-ins.md#textstyles) di testo se desiderate aggiungere (o estendere) un intervallo personalizzato di stili da usare con il testo. |
| pedice | `subscript`,  `superscript` | Estensioni nei formati di base, aggiunta di pedice e super-script. |
| tabella | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | Vedere [configurare gli stili di tabella](configure-rich-text-editor-plug-ins.md#tablestyles) per aggiungere stili personalizzati per intere tabelle o singole celle. |
| annulla | `undo`,  `redo` | Dimensione cronologia delle operazioni di annullamento e ripristino [annullamento e ripristino](configure-rich-text-editor-plug-ins.md#undohistory). |

>[!NOTE]
>
>Il plug-in a schermo intero non è supportato in modalità finestra di dialogo. Utilizzare l&#39;impostazione `dialogFullScreen` per configurare la barra degli strumenti per la modalità a schermo intero.

## Comprendere i percorsi e le posizioni di configurazione {#understand-the-configuration-paths-and-locations}

La [modalità di modifica dell&#39;editor Rich Text e l&#39;interfaccia](#editingmodes) fornita dagli autori determinano la posizione dei dettagli di configurazione quando si stanno attivando i plug-in dell&#39;editor Rich Text](configure-rich-text-editor-plug-ins.md#activateplugin). [ Le posizioni sono:

* Modalità in linea: `cq:editConfig/cq:inplaceEditing`.
* Modalità schermo intero: `cq:editConfig/cq:inplaceEditing`.
* Modalità finestra di dialogo: `cq:dialog`.
* Modalità finestra di dialogo a schermo intero: `cq:dialog`.

>[!NOTE]
>
>Non assegnare al nodo il nome `cq:inplaceEditing` come `config`. Sul nodo `cq:inplaceEditing`, definire le seguenti proprietà:
>
>* **Nome**: `configPath`
>* **Tipo**: `String`
>* **Valore**: percorso del nodo contenente la configurazione effettiva
>
>Non assegnare al nodo di configurazione RTE il nome `config`. In caso contrario, le configurazioni dell&#39;editor Rich Text hanno effetto solo per gli amministratori e non per gli utenti del gruppo `content-author`.

Configurare le seguenti proprietà che si applicano in modalità di modifica finestra di dialogo:

* `useFixedInlineToolbar`: È possibile impostare la barra degli strumenti dell’editor Rich Text in modo che sia fissa invece di essere mobile. Impostate questa proprietà booleana definita sul nodo RTE con sling:resourceType= `cq/gui/components/authoring/dialog/richtext` su `True`. Quando questa proprietà è impostata su `True`, la modifica RTF viene avviata sull&#39;evento `foundation-contentloaded`. Per evitare questo problema, impostare la proprietà `customStart` su `True` e attivare l&#39;evento `rte-start` per avviare la modifica dell&#39;editor Rich Text. Se questa proprietà è `true`, l&#39;editor Rich Text non inizia a fare clic e questo è il comportamento predefinito.

* `customStart`: Impostate questa proprietà booleana definita sul nodo dell&#39;editor Rich Text su  `True`, per controllare quando avviare l&#39;editor Rich Text attivando l&#39;evento  `rte-start`.

* `rte-start`: Attiva questo evento sull’ `contenteditable-div` editor Rich Text, quando avviare la modifica dell’editor Rich Text. Funziona solo se `customStart` è stato impostato su `true`.

Quando l&#39;editor Rich Text viene utilizzato nella finestra di dialogo con abilitazione touch, impostare la proprietà `useFixedInlineToolbar` su `true` per evitare problemi.

## Abilitare le funzionalità RTE attivando i plug-in {#enable-rte-functionalities-by-activating-plug-ins}

Le funzionalità RTE sono disponibili tramite una serie di plug-in, ognuno dei quali dispone della proprietà features. Potete configurare la proprietà features in modo da attivare o disattivare le varie funzioni di ciascun plug-in.

Per configurazioni dettagliate dei plug-in RTE, vedere [come attivare e configurare i plug-in RTE](configure-rich-text-editor-plug-ins.md).

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

Il componente di testo [Componenti di base](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) consente agli editor di modelli di configurare molti plug-in RTE utilizzando l&#39;interfaccia utente come criteri di contenuto, eliminando la necessità di una configurazione tecnica. I criteri di contenuto possono funzionare con le configurazioni dell’interfaccia utente RTE come descritto in questo documento. Per ulteriori informazioni, vedere [creare modelli di pagina](/help/sites-cloud/authoring/features/templates.md) e la [documentazione per gli sviluppatori di componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html).

>A scopo di riferimento, i componenti Testo predefiniti (forniti nell’ambito di un’installazione standard) sono disponibili all’indirizzo:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>Per creare un componente di testo personalizzato, copiate il componente sopra anziché modificarlo.

## Configura RTE, barra degli strumenti {#dialogfullscreen}

[!DNL Experience Manager] consente di configurare l’interfaccia per l’editor Rich Text in modo diverso per le diverse modalità di modifica. Le impostazioni predefinite sono fornite di seguito. Potete ignorare queste impostazioni predefinite in base alle vostre esigenze. Potete personalizzare solo le funzioni della barra degli strumenti che desiderate fornire agli autori. Non è necessario specificare tutte le configurazioni della barra degli strumenti.

Per configurare la barra degli strumenti per `dialogFullScreen`, utilizzate la seguente configurazione di esempio.

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

Per la modalità in linea e per la modalità a schermo intero vengono utilizzate diverse impostazioni dell&#39;interfaccia utente. La proprietà toolbar specifica l&#39;opzione della barra degli strumenti.

Ad esempio, se l&#39;opzione è essa stessa una funzione (ad esempio, `Bold`), viene specificata come `PluginName#FeatureName` (ad esempio, `links#modifylink`).

Se l&#39;opzione è un pop-over (contenente alcune caratteristiche di un plug-in), viene specificata come `#PluginName` (ad esempio, `#format`).

I separatori (`|`) tra un gruppo di opzioni possono essere specificati con `-`.

Il nodo a comparsa nella modalità in linea o a schermo intero contiene un elenco dei pop-up in uso. Ogni nodo secondario sotto il nodo `popovers` viene denominato in base al plug-in (ad esempio, formato). La proprietà &#39;items&#39; contiene un elenco delle funzioni del plug-in (ad esempio, format#bold).

## Impostazioni dell&#39;interfaccia utente RTE e criteri di contenuto {#rtecontentpolicies}

Gli amministratori possono controllare le opzioni dell&#39;editor Rich Text utilizzando criteri di contenuto, ad esempio anziché eseguire la configurazione come descritto in precedenza. I criteri di contenuto definiscono le proprietà di progettazione di un componente quando viene utilizzato come parte di un [modello modificabile](/help/sites-cloud/authoring/features/templates.md). Ad esempio, se un componente di testo che utilizza l’editor Rich Text viene utilizzato con un modello modificabile, il criterio del contenuto può definire la disponibilità dell’opzione grassetto e alcune opzioni di formattazione del paragrafo. I criteri di contenuto sono riutilizzabili e possono essere applicati a più modelli.

Le opzioni disponibili nell’editor Rich Text scorrono a valle dalle configurazioni dell’interfaccia utente ai criteri dei contenuti.

* Le impostazioni di configurazione dell&#39;interfaccia utente definiscono le opzioni disponibili per i criteri di contenuto.
* Se la configurazione dell&#39;interfaccia utente dell&#39;editor Rich Text è stata rimossa o non abilita un elemento, il criterio del contenuto non è in grado di configurarlo.
* Un autore ha accesso solo a tali funzionalità, rese disponibili dalle configurazioni dell&#39;interfaccia utente e dai criteri di contenuto.

Ad esempio, è possibile consultare la [Documentazione del componente di base di testo](https://docs.adobe.com/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## Personalizzare la mappatura tra icone della barra degli strumenti e comandi {#iconstoolbar}

È possibile personalizzare la mappatura tra le icone Corallo visualizzate sulla barra degli strumenti dell’editor Rich Text e i comandi disponibili. Non è possibile utilizzare altre icone oltre alle icone Corallo.

1. Create un nodo denominato `icons` in `uiSettings/cui`.

1. Creare nodi per le singole icone sottostanti.
1. Su ciascuno dei singoli nodi di icona, specificate un&#39;icona Corallo e un comando da associare all&#39;icona.

Segue uno snippet di esempio per mappare il comando `Bold` sull&#39;icona Corallo denominata `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## Limitazioni note {#known-limitations}

[!DNL Experience Manager] La funzionalità RTE presenta le seguenti limitazioni:

* Le funzionalità RTE sono supportate solo nelle finestre di dialogo dei componenti [!DNL Experience Manager]. L&#39;editor Rich Text non è supportato nelle procedure guidate o nei moduli di base.

* [!DNL Experience Manager] non funziona sui dispositivi ibridi.  <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* Non assegnare un nome al nodo di configurazione dell&#39;editor Rich Text `config`. In caso contrario, la configurazione dell&#39;editor Rich Text ha effetto solo per gli amministratori e non per gli utenti del gruppo `content-author`.

* L’editor Rich Text non supporta l’incorporazione di contenuto in una cornice in linea o in un iframe.

## Best practice e suggerimenti {#best-practices-and-tips}

* Per una finestra di dialogo mobile, abilitate solo i plug-in senza finestra di dialogo a comparsa. I plug-in senza pop-up sono di dimensioni più ridotte e sono più adatti per una finestra di dialogo mobile.
* Attivate i plug-in con un pop-up più grande, ad esempio il plug-in `Paste`, solo in modalità a schermo intero o a schermo intero. I plug-in con numerosi pop-up necessitano di maggiore spazio sullo schermo per offrire una buona esperienza di authoring.
* Se utilizzate plug-in personalizzati per l&#39;editor Rich Text CoralUI3, utilizzate la libreria `rte.coralui3`.

>[!MORELIKETHIS]
>
>* [Configurare i plug-in RTE](configure-rich-text-editor-plug-ins.md)
>* [Utilizzo dell’editor Rich Text per la creazione](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [Configurare l&#39;editor Rich Text per i siti con accesso facilitato](rte-accessible-content.md)
>* [Esempio di esercitazione per creare un componente multicampo composito](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

