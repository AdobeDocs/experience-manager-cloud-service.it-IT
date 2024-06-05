---
title: Configurare l’Editor Rich Text per l’authoring dei contenuti in [!DNL Adobe Experience Manager] as a Cloud Service.
description: Configurare l’Editor Rich Text per l’authoring dei contenuti in [!DNL Adobe Experience Manager] as a Cloud Service.
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# Configurare l’editor Rich Text {#configure-the-rich-text-editor}

L’editor Rich Text offre agli autori un’ampia gamma di funzionalità per modificare il contenuto di testo. Sono disponibili icone, caselle di selezione, barre degli strumenti e menu per un&#39;esperienza di modifica del testo WYSIWYG. Gli amministratori configurano l’editor Rich Text per abilitare, disabilitare ed estendere le funzioni disponibili nei componenti di authoring. Scopri come gli autori [utilizzare l’editor Rich Text per l’authoring](/help/sites-cloud/authoring/page-editor/rich-text-editor.md) contenuto web.

Di seguito sono elencati i concetti e i passaggi necessari per la configurazione dell’editor Rich Text.

| Comprendere i concetti dell’editor Rich Text | Abilita funzioni richieste | Configurare singole funzionalità |
|---|---|---|
| [Interfaccia](#understand-rte-ui) | [Comprendere e impostare le posizioni di configurazione](#understand-the-configuration-paths-and-locations) | [Configurare i plug-in](#enable-rte-functionalities-by-activating-plug-ins) |
| [Tipi di modalità di modifica](#editingmodes) | [Attiva plug-in](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Impostare le proprietà della funzionalità](#aboutplugins) |
| [Informazioni sui plug-in](#aboutplugins) | [Configurare le barre degli strumenti dell’Editor Rich Text](#dialogfullscreen) | [Configurare le modalità Incolla](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## Interfaccia utente disponibile per gli autori {#understand-rte-ui}

L’interfaccia RTE offre [design responsive](/help/sites-cloud/authoring/page-editor/responsive-layout.md) per l’ambiente di authoring. L&#39;interfaccia è progettata per essere utilizzata su dispositivi touch e desktop.

![Barra degli strumenti dell’Editor Rich Text](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra degli strumenti dell’Editor Rich Text con tutte le opzioni disponibili abilitate.*

La barra degli strumenti fornisce le opzioni per l’esperienza di authoring WYSIWYG. [!DNL Experience Manager] gli amministratori possono configurare le opzioni disponibili nella barra degli strumenti dell’interfaccia di. Per impostazione predefinita, in è disponibile un set completo di opzioni di modifica [!DNL Experience Manager]. Gli sviluppatori possono personalizzare [!DNL Experience Manager] per aggiungere altre opzioni di modifica.

## Varie modalità di editing {#editingmodes}

Gli autori possono creare e modificare contenuti testuali in [!DNL Experience Manager] utilizzare le diverse modalità dei componenti. Le opzioni della barra degli strumenti per l’authoring e la formattazione dei contenuti e l’esperienza utente dei componenti abilitati per l’editor Rich Text in diverse modalità di modifica variano in base alle configurazioni dell’editor Rich Text.

| Modalità di modifica | Area di modifica | Funzioni consigliate da abilitare |
|--- |--- |--- |
| In linea | Modifica diretta per modifiche rapide e minori; Formatta senza aprire una finestra di dialogo. | Funzioni minime dell’editor Rich Text |
| Editor Rich Text a schermo intero | Copre l&#39;intera pagina. | Tutte le funzionalità richieste dell&#39;editor Rich Text. |
| Finestra di dialogo | Finestra di dialogo sopra il contenuto della pagina, ma non copre l’intera pagina. | Abilitare le funzionalità in modo giudizioso. |
| Finestra di dialogo a schermo intero | Come modalità a schermo intero; contiene campi della finestra di dialogo insieme all’editor Rich Text. | Tutte le funzionalità richieste dell&#39;editor Rich Text. |

>[!NOTE]
>
>La funzione di modifica dell’origine non è disponibile in modalità di modifica in linea. Non è possibile trascinare le immagini in modalità a schermo intero. Tutte le altre funzioni funzionano in tutte le modalità.

### Modifica in linea {#inline-editing}

Per modificare il contenuto di una pagina, apri il contenuto con un doppio clic lento . Viene visualizzata una barra degli strumenti compatta con opzioni di base.

![Modifica in linea con le opzioni di base nella barra degli strumenti](assets/inline-editing-mode-basic-options.png)

*Figura: Modifica in linea con le opzioni di base nella barra degli strumenti.*

### Modifica a tutto schermo {#full-screen-editing}

[!DNL Experience Manager] i componenti possono essere aperti in visualizzazione a schermo intero che nasconde il contenuto della pagina e occupa lo schermo disponibile. Prendi in considerazione la modifica a schermo intero di una versione dettagliata della modifica in linea, in quanto offre le opzioni di modifica più avanzate. Per aprirlo, fai clic su ![Icona per aprire l’editor Rich Text a schermo intero](assets/rte_fullscreen.png), dalla barra degli strumenti compatta quando si utilizza la modalità di modifica in linea.

Nella finestra di dialogo in modalità a tutto schermo, oltre a una barra degli strumenti dettagliata dell’editor Rich Text, sono disponibili anche le opzioni e i componenti disponibili in una finestra di dialogo. È applicabile solo a una finestra di dialogo che contiene l’editor Rich Text insieme ad altri componenti.

![Barra degli strumenti dettagliata dell’editor Rich Text in modalità a schermo intero](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra degli strumenti dettagliata dell’editor Rich Text in modalità a schermo intero.*

### Modifica finestre di dialogo {#dialog-editing}

Quando si fa doppio clic su un componente, viene visualizzata una finestra di dialogo per la modifica del contenuto. La finestra di dialogo viene visualizzata sopra la pagina esistente. In alcuni scenari specifici, la finestra di dialogo si apre come finestra pop-up. Ad esempio, quando un componente Testo fa parte di una colonna in un layout di pagina a più colonne e l’area disponibile per la finestra di dialogo è inferiore.

![Modalità di modifica finestra di dialogo](assets/dialog_editing_modetouchui.png)

*Figura: Modalità di modifica delle finestre di dialogo.*

## Informazioni sui plug-in dell’editor Rich Text e sulle funzioni associate {#aboutplugins}

Questa funzionalità è disponibile tramite una serie di plug-in, ciascuno con:

* A `features` proprietà che è,

   * Utilizzato per attivare o disattivare le funzionalità di base di quel plug-in.
   * Configurato utilizzando una procedura standard.

* Se appropriato, più proprietà e opzioni che richiedono una configurazione specializzata.

Le funzioni di base dell’editor Rich Text vengono attivate o disattivate dal valore `features` su un nodo specifico del plug-in appropriato.

Nella tabella seguente sono elencati i plug-in correnti:

* ID plug-in con collegamento alla documentazione API. ID viene utilizzato come nome del nodo quando [attivazione di un plug-in](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valori consentiti per `features` proprietà.
* Descrizione delle funzionalità fornite dal plug-in.

| ID plug-in | funzioni | Descrizione |
|--- |--- |--- |
| modifica | `cut`, `copy`, `paste-default`, `paste-plaintext`, `paste-wordhtml` | [Taglia, copia e, le tre modalità Incolla](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles). |
| findreplace | `find`, `replace` | Trova e sostituisci. |
| formato | `bold`, `italic`, `underline` | [Formattazione testo di base](configure-rich-text-editor-plug-ins.md#textstyles). |
| immagine | `image` | Supporto immagini di base (trascinamento dal contenuto o da Content Finder). A seconda del browser, il supporto presenta comportamenti diversi per gli autori |
| tasti | - | Per definire questo valore, consulta [dimensione scheda](configure-rich-text-editor-plug-ins.md#tabsize). |
| giustificare | `justifyleft`, `justifycenter`, `justifyright` | Allineamento paragrafo. |
| collegamenti | `modifylink`, `unlink`, `anchor` | [Collegamenti ipertestuali e ancoraggi](configure-rich-text-editor-plug-ins.md#linkstyles). |
| elenchi | `ordered`, `unordered`, `indent`, `outdent` | Questo plug-in controlla entrambi [rientro ed elenchi](configure-rich-text-editor-plug-ins.md#indentmargin), inclusi gli elenchi nidificati. |
| misctools | `specialchars`, `sourceedit` | Strumenti vari consentono agli autori di immettere [caratteri speciali](configure-rich-text-editor-plug-ins.md#spchar) o modificare il codice sorgente di HTML. Inoltre, puoi aggiungere una [intervallo di caratteri speciali](configure-rich-text-editor-plug-ins.md#definerangechar) se desideri definire un elenco personalizzato. |
| Paraformat | `paraformat` | I formati di paragrafo predefiniti sono Paragrafo, Titolo 1, Titolo 2 e Titolo 3 (`<p>`, `<h1>`, `<h2>`, e `<h3>`). È possibile [aggiungi altri formati di paragrafo](configure-rich-text-editor-plug-ins.md#paraformats) o estendere l&#39;elenco. |
| controllo ortografico | `checktext` | [Controllo ortografico in base alla lingua](configure-rich-text-editor-plug-ins.md#adddict). |
| stili | `styles` | Supporto per lo stile tramite una classe CSS. [Aggiungere nuovi stili di testo](configure-rich-text-editor-plug-ins.md#textstyles) se si desidera aggiungere o estendere un intervallo personalizzato di stili da utilizzare con il testo. |
| pedice | `subscript`, `superscript` | Estensioni ai formati di base, con l’aggiunta di pedice e pedice. |
| tabella | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | Consulta [configurare gli stili di tabella](configure-rich-text-editor-plug-ins.md#tablestyles) per aggiungere stili personalizzati per intere tabelle o singole celle. |
| annulla | `undo`, `redo` | Dimensione cronologia di [annulla e ripristina](configure-rich-text-editor-plug-ins.md#undohistory) operazioni. |

>[!NOTE]
>
>Il plug-in a schermo intero non è supportato nella modalità finestra di dialogo. Uso del `dialogFullScreen` impostazione per configurare la barra degli strumenti per la modalità a schermo intero.

## Comprendere i percorsi e le posizioni di configurazione {#understand-the-configuration-paths-and-locations}

Il [modalità di modifica dell’editor Rich Text e interfaccia](#editingmodes) che fornisci agli autori per decidere la posizione dei dettagli di configurazione quando sei [attivazione dei plug-in dell’editor Rich Text](configure-rich-text-editor-plug-ins.md#activateplugin). Le posizioni sono:

* Modalità in linea: `cq:editConfig/cq:inplaceEditing`.
* Modalità a tutto schermo: `cq:editConfig/cq:inplaceEditing`.
* Modalità finestra di dialogo `cq:dialog`.
* Modalità finestra di dialogo a schermo intero: `cq:dialog`.

>[!NOTE]
>
>Non denominare il nodo sotto `cq:inplaceEditing` as `config`. On `cq:inplaceEditing` , definire le seguenti proprietà:
>
>* **Nome**: `configPath`
>* **Tipo**: `String`
>* **Valore**: percorso del nodo contenente la configurazione effettiva
>
>Non denominare il nodo di configurazione dell’editor Rich Text come `config`. In caso contrario, le configurazioni dell’editor Rich Text hanno effetto solo per gli amministratori e non per gli utenti del gruppo `content-author`.

Configura le seguenti proprietà applicabili in modalità di modifica Finestra di dialogo:

* `useFixedInlineToolbar`: la barra degli strumenti dell’editor Rich Text può essere corretta invece di essere mobile. Imposta questa proprietà booleana definita sul nodo dell’editor Rich Text con sling:resourceType= `cq/gui/components/authoring/dialog/richtext` a `True`. Quando questa proprietà è impostata su `True`, la modifica in formato Rich Text viene avviata il `foundation-contentloaded` evento. Per evitare questo problema, imposta la proprietà `customStart` a `True` e attiva il `rte-start` per avviare la modifica dell’editor Rich Text. Quando questa proprietà è `true`, l’editor Rich Text non inizia quando si fa clic su e questo è il comportamento predefinito.

* `customStart`: imposta questa proprietà booleana definita nel nodo dell’editor Rich Text su `True`, per controllare quando avviare l’editor Rich Text attivando l’evento `rte-start`.

* `rte-start`: attiva questo evento sul `contenteditable-div` dell’editor Rich Text, quando iniziare a modificare l’editor Rich Text. Funziona solo se `customStart` è stato impostato su `true`.

Quando si utilizza l’editor Rich Text nella finestra di dialogo touch, imposta la proprietà `useFixedInlineToolbar` a `true` per evitare problemi.

## Abilitare le funzionalità dell’editor Rich Text attivando i plug-in {#enable-rte-functionalities-by-activating-plug-ins}

Le funzionalità dell’editor Rich Text sono disponibili tramite una serie di plug-in, ciascuno con la proprietà Features. Puoi configurare la proprietà features per abilitare o disabilitare le varie funzioni di ciascun plug-in.

Per configurazioni dettagliate dei plug-in dell’editor Rich Text, consulta [come attivare e configurare i plug-in dell’editor Rich Text](configure-rich-text-editor-plug-ins.md).

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

Il [Componente testo Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) consente agli editor di modelli di configurare molti plug-in dell’editor Rich Text utilizzando l’interfaccia utente come criteri per contenuti, eliminando la necessità di configurazione tecnica. I criteri dei contenuti possono funzionare con le configurazioni dell’interfaccia utente dell’editor Rich Text come descritto in questo documento. Per ulteriori informazioni, consulta [creare modelli di pagina](/help/sites-cloud/authoring/sites-console/templates.md) e [Documentazione per gli sviluppatori di Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>A scopo di riferimento, i componenti di testo predefiniti (forniti come parte di un’installazione standard) sono disponibili all’indirizzo:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>Per creare un componente testo personalizzato, copia il componente precedente invece di modificare questi componenti.

## Configurare la barra degli strumenti dell’editor Rich Text {#dialogfullscreen}

[!DNL Experience Manager] consente di configurare l’interfaccia per l’Editor Rich Text in modo diverso a seconda delle diverse modalità di modifica. Di seguito sono riportate le impostazioni predefinite. Puoi modificare questi valori predefiniti in base alle tue esigenze. Puoi personalizzare solo le funzioni della barra degli strumenti che desideri fornire agli autori. Non è necessario specificare tutte le configurazioni della barra degli strumenti.

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

Per le modalità in linea e a schermo intero vengono utilizzate diverse impostazioni dell’interfaccia utente. La proprietà toolbar specifica l’opzione della barra degli strumenti.

Ad esempio, se l&#39;opzione è essa stessa una feature (ad esempio, `Bold`), è specificato come `PluginName#FeatureName` (ad esempio, `links#modifylink`).

Se l&#39;opzione è a comparsa (contenente alcune caratteristiche di un plug-in), viene specificata come `#PluginName` (ad esempio, `#format`).

Separatori (`|`) tra un gruppo di opzioni può essere specificato con `-`.

Il nodo pop-up in modalità in linea o a schermo intero contiene un elenco dei pop-up utilizzati. Ogni nodo figlio sotto `popovers` Il nome del nodo deriva dal plug-in (ad esempio, formato). La proprietà &#39;items&#39; contiene un elenco di caratteristiche del plug-in (ad esempio, format#bold).

## Impostazioni dell’interfaccia utente e criteri dei contenuti dell’Editor Rich Text {#rtecontentpolicies}

Gli amministratori possono controllare le opzioni dell’editor Rich Text utilizzando i criteri del contenuto, ad esempio anziché eseguire la configurazione come descritto in precedenza. I criteri del contenuto definiscono le proprietà di progettazione di un componente quando viene utilizzato come parte di un [modello modificabile](/help/sites-cloud/authoring/sites-console/templates.md). Ad esempio, se un componente testo che utilizza l’editor Rich Text viene utilizzato con un modello modificabile, il criterio del contenuto può definire che l’opzione grassetto sia disponibile e che siano disponibili alcune opzioni di formattazione di paragrafo. I criteri per i contenuti sono riutilizzabili e possono essere applicati a più modelli.

Le opzioni disponibili nell’editor Rich Text scorrono a valle dalle configurazioni dell’interfaccia utente ai criteri dei contenuti.

* Le impostazioni di configurazione dell’interfaccia utente definiscono le opzioni disponibili per i criteri dei contenuti.
* Se la configurazione dell&#39;interfaccia utente dell&#39;editor Rich Text è stata rimossa o non consente un elemento, il criterio del contenuto non è in grado di configurarlo.
* Un autore ha accesso solo alle funzionalità rese disponibili dalle configurazioni dell’interfaccia utente e dai criteri dei contenuti.

Ad esempio, è possibile visualizzare [Documentazione dei componenti core testo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## Personalizzare la mappatura tra icone e comandi della barra degli strumenti {#iconstoolbar}

È possibile personalizzare la mappatura tra le icone Coral visualizzate sulla barra degli strumenti dell&#39;editor Rich Text e i comandi disponibili. Oltre alle icone Coral, non è possibile utilizzare altre icone.

1. Crea un nodo denominato `icons` in `uiSettings/cui`.

1. Crea nodi per le singole icone al di sotto di esso.
1. Su ciascuno dei singoli nodi delle icone, specificate un&#39;icona Coral e un comando da mappare sull&#39;icona.

Di seguito è riportato uno snippet di esempio per mappare il comando `Bold` all’icona Coral denominata `textItalic`.

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

* Le funzionalità dell’editor Rich Text sono supportate solo in [!DNL Experience Manager] finestre di dialogo dei componenti. L’editor Rich Text non è supportato nelle procedure guidate o nei moduli Foundation.

* [!DNL Experience Manager] non funziona sui dispositivi ibridi. <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* Non denominare il nodo di configurazione dell’editor Rich Text `config`. In caso contrario, la configurazione dell’editor Rich Text avrà effetto solo per gli amministratori e non per gli utenti del gruppo `content-author`.

* L’editor Rich Text non supporta l’incorporamento di contenuto in un frame in linea o in un iframe.

## Best practice e suggerimenti {#best-practices-and-tips}

* Per una finestra di dialogo mobile, abilita solo i plug-in senza una finestra di dialogo a comparsa. I plug-in senza pop-up sono di dimensioni ridotte e sono più adatti per una finestra di dialogo mobile.
* Abilita i plug-in con pop-up più grandi, ad esempio `Paste` plug-in, solo nella modalità di dialogo a schermo intero o in modalità a schermo intero. I plug-in con un pop-up di grandi dimensioni richiedono più spazio sullo schermo per fornire una buona esperienza di authoring.
* Se utilizzi plug-in personalizzati per CoralUI3 RTE, utilizza `rte.coralui3` libreria.

>[!MORELIKETHIS]
>
>* [Configurare i plug-in dell’editor Rich Text](configure-rich-text-editor-plug-ins.md)
>* [Utilizza l’editor Rich Text per l’authoring](/help/sites-cloud/authoring/page-editor/rich-text-editor.md)
>* [Configurare l’editor Rich Text per i siti accessibili](rte-accessible-content.md)
