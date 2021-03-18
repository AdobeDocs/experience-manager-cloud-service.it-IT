---
title: Configura l’editor Rich Text per creare contenuti in [!DNL Adobe Experience Manager] come Cloud Service.
description: Configura l’editor Rich Text per creare contenuti in [!DNL Adobe Experience Manager] come Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 96aa0ef43613e6ae72bf4c454be46329abb19a0c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Configurare l’editor Rich Text {#configure-the-rich-text-editor}

L’Editor Rich Text offre agli autori numerose funzionalità per modificare il contenuto del testo. Icone, caselle di selezione, barra degli strumenti e menu sono disponibili per un’esperienza di modifica del testo WYSIWYG. Gli amministratori configurano l’editor Rich Text per abilitare, disabilitare ed estendere le funzioni disponibili nei componenti di authoring. Scopri in che modo gli autori [utilizzano l’editor Rich Text per creare contenuti web](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md).

Di seguito sono elencati i concetti e i passaggi necessari per la configurazione dell’editor Rich Text.

| Comprendere i concetti dell’editor Rich Text | Abilitare le funzioni richieste | Configurare singole funzionalità |
|---|---|---|
| [Comprendere l’interfaccia](#understand-rte-ui) | [Comprendere e impostare le posizioni di configurazione](#understand-the-configuration-paths-and-locations) | [Configurare i plug-in](#enable-rte-functionalities-by-activating-plug-ins) |
| [Tipi di modalità di modifica](#editingmodes) | [Attivare i plug-in](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Impostare le proprietà delle feature](#aboutplugins) |
| [Informazioni sui plug-in](#aboutplugins) | [Configurare le barre degli strumenti dell’Editor Rich Text](#dialogfullscreen) | [Configurare le modalità Incolla](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## Comprendere l’interfaccia utente disponibile per gli autori {#understand-rte-ui}

L’interfaccia RTE offre un [design reattivo](/help/sites-cloud/authoring/features/responsive-layout.md) per l’ambiente di authoring. L’interfaccia è progettata per l’utilizzo su dispositivi touch e desktop.

![Barra degli strumenti dell’Editor Rich Text](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra degli strumenti dell’Editor Rich Text con tutte le opzioni disponibili abilitate.*

La barra degli strumenti fornisce le opzioni per l’esperienza di authoring WYSIWYG. [!DNL Experience Manager] gli amministratori possono configurare le opzioni disponibili nella barra degli strumenti dell’interfaccia. Per impostazione predefinita, in [!DNL Experience Manager] è disponibile un set completo di opzioni di modifica. Gli sviluppatori possono personalizzare [!DNL Experience Manager] per aggiungere altre opzioni di modifica.

## Varie modalità di modifica {#editingmodes}

Gli autori possono creare e modificare il contenuto testuale in [!DNL Experience Manager] utilizzando le diverse modalità dei componenti. Le opzioni della barra degli strumenti per l’authoring e la formattazione dei contenuti e l’esperienza utente dei componenti abilitati per l’editor Rich Text in diverse modalità di modifica variano a seconda delle configurazioni dell’editor Rich Text.

| Modalità di modifica | Area di editing | Funzioni consigliate da abilitare |
|--- |--- |--- |
| In linea | Modifica diretta per modifiche rapide e minori; Formattare senza aprire una finestra di dialogo. | Funzioni RTE minime. |
| Schermo intero dell’Editor Rich Text | Copre l’intera pagina. | Tutte le funzioni RTE richieste. |
| Finestra di dialogo | La finestra di dialogo si trova sopra il contenuto della pagina, ma non copre l’intera pagina. | Abilitare le funzionalità in modo giudizioso. |
| Finestra di dialogo a schermo intero | come la modalità a schermo intero; contiene i campi della finestra di dialogo accanto a RTE. | Tutte le funzioni RTE richieste. |

>[!NOTE]
>
>La funzione di modifica sorgente non è disponibile in modalità di modifica in linea. Non è possibile trascinare immagini in modalità a schermo intero. Tutte le altre funzioni funzionano in tutte le modalità.

### Modifica in linea {#inline-editing}

Per modificare il contenuto di una pagina, apri il contenuto con un doppio clic lento . Viene presentata una barra degli strumenti compatta con le opzioni di base.

![Modifica in linea con le opzioni di base nella barra degli strumenti](assets/inline-editing-mode-basic-options.png)

*Figura: Modifica in linea con le opzioni di base nella barra degli strumenti.*

### Modifica a tutto schermo {#full-screen-editing}

[!DNL Experience Manager] i componenti possono essere aperti nella visualizzazione a schermo intero che nasconde il contenuto della pagina e occupa la schermata disponibile. Considera la modifica a schermo intero una versione dettagliata della modifica in linea in quanto offre il maggior numero di opzioni di modifica. Per aprirlo, fai clic su ![Icona per aprire l’Editor Rich Text a schermo intero](assets/rte_fullscreen.png) nella barra degli strumenti compatta quando utilizzi la modalità di editing in linea.

Nella finestra di dialogo a schermo intero, insieme a una barra degli strumenti dettagliata dell’Editor Rich Text, sono disponibili anche le opzioni e i componenti disponibili in una finestra di dialogo. È applicabile solo per una finestra di dialogo che contiene l’editor Rich Text e altri componenti.

![Barra degli strumenti dettagliata dell’editor Rich Text durante la modifica in modalità a schermo intero](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra degli strumenti dettagliata dell’Editor Rich Text durante la modifica in modalità a schermo intero.*

### Modifica finestra di dialogo {#dialog-editing}

Quando si fa doppio clic su un componente, viene visualizzata una finestra di dialogo per la modifica del contenuto. Viene visualizzata la finestra di dialogo sopra la pagina esistente. In alcuni scenari specifici, la finestra di dialogo si apre come finestra a comparsa. Ad esempio, quando un componente Testo fa parte di una colonna in un layout di pagina a più colonne e l’area disponibile per la finestra di dialogo è inferiore.

![Modalità di modifica finestra di dialogo](assets/dialog_editing_modetouchui.png)

*Figura: Modalità di modifica della finestra di dialogo.*

## Informazioni sui plug-in RTE e sulle funzioni associate {#aboutplugins}

La funzionalità è resa disponibile tramite una serie di plug-in, ciascuno con:

* Una proprietà `features` che è

   * Utilizzato per attivare o disattivare le funzionalità di base del plug-in.
   * Configurata utilizzando una procedura standard.

* Se appropriato, più proprietà e opzioni che richiedono una configurazione specializzata.

Le funzioni di base dell’editor Rich Text vengono attivate o disattivate dal valore della proprietà `features` su un nodo specifico del plug-in appropriato.

Nella tabella seguente sono elencati i plug-in correnti, che mostrano:

* ID dei plug-in con un collegamento alla documentazione API. L&#39;ID viene utilizzato come nome del nodo quando [si attiva un plug-in](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valori consentiti per la proprietà `features` .
* Una descrizione delle funzionalità fornite dal plug-in.

| ID plug-in | caratteristiche | Descrizione |
|--- |--- |--- |
| modifica | `cut`,  `copy`,  `paste-default`,  `paste-plaintext`,  `paste-wordhtml` | [Taglia, copia e incolla le tre modalità](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles). |
| [punto di arrivo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | `find`, `replace` | Trova e sostituisci. |
| [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | `bold`, `italic`, `underline` | [Formattazione](configure-rich-text-editor-plug-ins.md#textstyles) di base del testo. |
| [immagine](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | `image` | Supporto immagini di base (trascinamento da contenuto o Content Finder). A seconda del browser, il supporto offre diversi comportamenti per gli autori |
| [chiavi](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) | - | Per definire questo valore, vedere [dimensioni scheda](configure-rich-text-editor-plug-ins.md#tabsize). |
| [justify](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | `justifyleft`,  `justifycenter`,  `justifyright` | Allineamento paragrafo. |
| [collegamenti](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | `modifylink`,  `unlink`,  `anchor` | [Collegamenti ipertestuali ed ancoraggi](configure-rich-text-editor-plug-ins.md#linkstyles). |
| [elenchi](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | `ordered`,  `unordered`,  `indent`,  `outdent` | Questo plug-in controlla sia i rientri che gli elenchi](configure-rich-text-editor-plug-ins.md#indentmargin); inclusi gli elenchi nidificati.[ |
| [strumenti cattivi](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | `specialchars`,  `sourceedit` | Gli strumenti vari consentono agli autori di inserire [caratteri speciali](configure-rich-text-editor-plug-ins.md#spchar) o modificare l&#39;origine HTML. Inoltre, puoi aggiungere un [intervallo di caratteri speciali](configure-rich-text-editor-plug-ins.md#definerangechar) se desideri definire un tuo elenco. |
| Paraformato | `paraformat` | I formati di paragrafo predefiniti sono Paragrafo, Intestazione 1, Intestazione 2 e Intestazione 3 (`<p>`, `<h1>`, `<h2>` e `<h3>`). È possibile [aggiungere altri formati paragrafo](configure-rich-text-editor-plug-ins.md#paraformats) o estendere l&#39;elenco. |
| controllo ortografico | `checktext` | [Controllo ortografico basato sulla lingua](configure-rich-text-editor-plug-ins.md#adddict). |
| stili | `styles` | Supporto per lo stile utilizzando una classe CSS. [Aggiungi un nuovo stile ](configure-rich-text-editor-plug-ins.md#textstyles) di testo se desideri aggiungere (o estendere) un proprio intervallo di stili da utilizzare con il testo. |
| pedice | `subscript`,  `superscript` | Estensioni ai formati di base, aggiunta di script secondari e di script super. |
| tabella | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | Consultare [configurare gli stili di tabella](configure-rich-text-editor-plug-ins.md#tablestyles) per aggiungere stili personalizzati per intere tabelle o singole celle. |
| annulla | `undo`,  `redo` | Dimensione della cronologia delle operazioni [Annulla e Ripristina](configure-rich-text-editor-plug-ins.md#undohistory). |

>[!NOTE]
>
>Il plug-in a schermo intero non è supportato in modalità finestra di dialogo. Utilizzare l’impostazione `dialogFullScreen` per configurare la barra degli strumenti per la modalità a schermo intero.

## Comprendere i percorsi e le posizioni di configurazione {#understand-the-configuration-paths-and-locations}

La [modalità di modifica dell’editor Rich Text e l’interfaccia](#editingmodes) che fornisci agli autori decidono il percorso per i dettagli di configurazione quando si attivano i plug-in RTE](configure-rich-text-editor-plug-ins.md#activateplugin). [ Le posizioni sono:

* Modalità in linea: `cq:editConfig/cq:inplaceEditing`.
* Modalità schermo intero: `cq:editConfig/cq:inplaceEditing`.
* Modalità finestra di dialogo: `cq:dialog`.
* Modalità finestra di dialogo a schermo intero: `cq:dialog`.

>[!NOTE]
>
>Non denominare il nodo sotto `cq:inplaceEditing` come `config`. Sul nodo `cq:inplaceEditing`, definisci le seguenti proprietà:
>
>* **Nome**: `configPath`
>* **Tipo**: `String`
>* **Valore**: percorso del nodo contenente la configurazione effettiva

>
>
Non denominare il nodo di configurazione dell’editor Rich Text come `config`. In caso contrario, le configurazioni dell’editor Rich Text hanno effetto solo per gli amministratori e non per gli utenti del gruppo `content-author`.

Configura le seguenti proprietà da applicare in modalità di modifica della finestra di dialogo:

* `useFixedInlineToolbar`: È possibile impostare la barra degli strumenti dell’Editor Rich Text in modo che sia fissa invece di fluttuare. Imposta questa proprietà booleana definita sul nodo RTE con sling:resourceType= `cq/gui/components/authoring/dialog/richtext` su `True`. Quando questa proprietà è impostata su `True`, la modifica RTF viene avviata sull&#39;evento `foundation-contentloaded` . Per evitare questo problema, imposta la proprietà `customStart` su `True` e attiva l’evento `rte-start` per avviare la modifica dell’editor Rich Text. Quando questa proprietà è `true`, l’editor Rich Text non inizia a fare clic su e questo è il comportamento predefinito.

* `customStart`: Imposta questa proprietà booleana definita sul nodo dell’editor Rich Text su  `True`, per controllare quando avviare l’editor Rich Text attivando l’evento  `rte-start`.

* `rte-start`: Attiva questo evento sull’editor Rich Text  `contenteditable-div` , quando avviare la modifica dell’editor Rich Text. Funziona solo se `customStart` è stato impostato su `true`.

Quando l’editor Rich Text viene utilizzato nella finestra di dialogo touch, imposta la proprietà `useFixedInlineToolbar` su `true` per evitare problemi.

## Abilitare le funzionalità RTE attivando i plug-in {#enable-rte-functionalities-by-activating-plug-ins}

Le funzionalità dell’editor Rich Text sono disponibili tramite una serie di plug-in, ciascuno con proprietà features . Puoi configurare la proprietà features per attivare o disattivare le varie funzioni di ciascun plug-in.

Per configurazioni dettagliate dei plug-in RTE, consulta [come attivare e configurare i plug-in RTE](configure-rich-text-editor-plug-ins.md).

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

Il [componente di testo Componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) consente agli editor modelli di configurare molti plug-in RTE utilizzando l’interfaccia utente come criteri di contenuto, eliminando la necessità di configurazioni tecniche. I criteri dei contenuti possono funzionare con le configurazioni dell’interfaccia utente RTE come descritto in questo documento. Per ulteriori informazioni, consulta [creare modelli di pagina](/help/sites-cloud/authoring/features/templates.md) e la [documentazione per gli sviluppatori dei componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html).

>A scopo di riferimento, i componenti Testo predefiniti (forniti nell’ambito di un’installazione standard) sono disponibili all’indirizzo:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`

>
>
Per creare un componente di testo personalizzato, copia il componente di cui sopra invece di modificare questi componenti.

## Configurare la barra degli strumenti dell’editor Rich Text {#dialogfullscreen}

[!DNL Experience Manager] consente di configurare l’interfaccia per l’Editor Rich Text in modo diverso per le diverse modalità di modifica. Le impostazioni predefinite sono fornite di seguito. Puoi ignorare queste impostazioni predefinite in base alle tue esigenze. È possibile personalizzare solo le funzioni della barra degli strumenti che si desidera fornire agli autori. Non è necessario specificare tutte le configurazioni della barra degli strumenti.

Per configurare la barra degli strumenti per `dialogFullScreen`, utilizza la seguente configurazione di esempio.

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

Per la modalità in linea e la modalità a schermo intero vengono utilizzate diverse impostazioni dell’interfaccia utente. La proprietà della barra degli strumenti specifica l&#39;opzione della barra degli strumenti.

Ad esempio, se l’opzione è essa stessa una funzione (ad esempio, `Bold`), viene specificata come `PluginName#FeatureName` (ad esempio, `links#modifylink`).

Se l&#39;opzione è un pop-over (contenente alcune caratteristiche di un plug-in), viene specificata come `#PluginName` (ad esempio, `#format`).

È possibile specificare separatori (`|`) tra un gruppo di opzioni con `-`.

Il nodo a comparsa in modalità in linea o a schermo intero contiene un elenco dei pop-up in uso. Ogni nodo figlio sotto il nodo `popovers` prende il nome dal plug-in (ad esempio, formato). Ha una proprietà &quot;items&quot; contenente un elenco delle funzioni del plug-in (ad esempio, format#bold).

## Impostazioni dell’interfaccia utente e criteri dei contenuti dell’editor Rich Text {#rtecontentpolicies}

Gli amministratori possono controllare le opzioni dell’editor Rich Text utilizzando i criteri dei contenuti, ad esempio anziché eseguire la configurazione come descritto in precedenza. I criteri dei contenuti definiscono le proprietà di progettazione di un componente quando viene utilizzato come parte di un [modello modificabile](/help/sites-cloud/authoring/features/templates.md). Ad esempio, se un componente di testo che utilizza l’editor Rich Text viene utilizzato con un modello modificabile, i criteri per i contenuti possono definire che l’opzione in grassetto è disponibile e che sono disponibili alcune opzioni di formattazione dei paragrafi. I criteri del contenuto sono riutilizzabili e possono essere applicati a più modelli.

Le opzioni disponibili nell’editor Rich Text scorrono a valle dalle configurazioni dell’interfaccia utente ai criteri dei contenuti.

* Le impostazioni di configurazione dell’interfaccia utente definiscono quali opzioni sono disponibili per i criteri dei contenuti.
* Se la configurazione dell’interfaccia utente dell’editor Rich Text è stata rimossa o non abilita un elemento, il criterio del contenuto non è in grado di configurarlo.
* Un autore ha accesso solo alle funzionalità rese disponibili dalle configurazioni dell’interfaccia utente e dai criteri dei contenuti.

Ad esempio, puoi vedere la [documentazione sui componenti di base di testo](https://docs.adobe.com/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## Personalizzare la mappatura tra icone e comandi della barra degli strumenti {#iconstoolbar}

Puoi personalizzare la mappatura tra le icone Coral visualizzate sulla barra degli strumenti dell’Editor Rich Text e i comandi disponibili. Non è possibile utilizzare altre icone oltre alle icone Coral.

1. Crea un nodo denominato `icons` in `uiSettings/cui`.

1. Crea nodi per singole icone sotto di esso.
1. Su ciascuno dei singoli nodi icona, specifica un’icona Coral e un comando da mappare sull’icona.

Di seguito è riportato uno snippet di esempio per mappare il comando `Bold` all&#39;icona Coral denominata `textItalic`.

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

* Le funzionalità dell’editor Rich Text sono supportate solo nelle finestre di dialogo dei componenti [!DNL Experience Manager] . L’editor Rich Text non è supportato nelle procedure guidate o nei moduli di Foundation.

* [!DNL Experience Manager] non funziona su dispositivi ibridi.  <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* Non denominare il nodo di configurazione dell’editor Rich Text `config`. In caso contrario, la configurazione dell’editor Rich Text ha effetto solo per gli amministratori e non per gli utenti del gruppo `content-author`.

* L’editor Rich Text non supporta l’incorporazione di contenuto in un frame in linea o in un iframe.

## Best practice e suggerimenti {#best-practices-and-tips}

* Per una finestra di dialogo mobile, abilita solo i plug-in senza una finestra di dialogo a comparsa. I plug-in senza pop-up sono di dimensioni più piccole e sono più adatti per una finestra di dialogo mobile.
* Abilita i plug-in con pop-up più grandi, come il `Paste` plug-in, solo in modalità a schermo intero o in modalità a schermo intero. I plug-in con grandi pop-up necessitano di più spazio disponibile sullo schermo per fornire una buona esperienza di authoring.
* Se utilizzi plug-in personalizzati per l’editor Rich Text CoralUI3, utilizza la libreria `rte.coralui3` .

>[!MORELIKETHIS]
>
>* [Configurare i plug-in RTE](configure-rich-text-editor-plug-ins.md)
>* [Utilizza l’editor Rich Text per l’authoring](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [Configurare l’editor Rich Text per i siti accessibili](rte-accessible-content.md)

