---
title: Configurare l’editor Rich Text per creare pagine Web e siti con accesso facilitato.
description: Scopri come configurare l’editor Rich Text per creare siti con accesso facilitato in [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 96c59974a868779df6979818bea0d942060cf5bc
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---


# Configurare l’editor Rich Text per creare siti accessibili {#configure-rte-accessible-sites}

[!DNL Adobe Experience Manager] supporta funzioni di accessibilità standard, quali testo alternativo per le immagini e funzioni aggiuntive accessibili durante la creazione di contenuti. Gli autori dei contenuti utilizzano queste funzioni con componenti che utilizzano l’editor Rich Text (Rich Text Editor). Le funzioni includono l’aggiunta di testo alternativo, informazioni strutturali tra titoli, elementi di paragrafo e così via.

Per informazioni sulle configurazioni tipiche di RTE, vedere [configurare RTE](rich-text-editor.md) e [configurare i plug-in RTE per funzionalità specifiche](configure-rich-text-editor-plug-ins.md).

Utilizzate la configurazione dei plug-in RTE per configurare e personalizzare le funzioni relative all’accessibilità. Ad esempio, utilizzare `paraformat` per aggiungere elementi semantici a livello di blocco aggiuntivo, inclusa l&#39;estensione del numero di livelli di intestazione supportati oltre le `H1` di base `H2` e `H3` fornite per impostazione predefinita. La modifica RTF è possibile utilizzando molti componenti dell’interfaccia utente di authoring. I componenti più utilizzati sono testo, immagini, download e così via.

La funzionalità RTE può essere resa disponibile in molti componenti. Il componente principale è il componente `Text`.

Per il componente `Text` in [!DNL Experience Manager], la schermata seguente mostra l&#39;editor Rich Text con una serie di plug-in abilitati, tra cui `paraformat`:

![Componente Testo RTE in modalità a schermo intero](assets/rte-toolbar-full-screen-mode.png)

## Configurare le funzioni del plug-in {#configuring-the-plugin-features}

Per istruzioni su come configurare l&#39;editor Rich Text, vedere [configurare la pagina Editor Rich Text](rich-text-editor.md). L&#39;articolo riguarda:

* [Plug-in e relative funzioni](rich-text-editor.md#aboutplugins)
* [Posizioni di configurazione](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [Attivare un plug-in e configurare la proprietà features](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [Configurare altre funzionalità dell’editor Rich Text](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

Per attivare alcune o tutte le funzioni di un plug-in, configurate il plug-in all&#39;interno del sottoramo `rtePlugins` appropriato nel CRXDE Lite.

![CRXDE Lite che mostra un esempio rtePlugin](assets/example-rteplugin-crxde-lite.png)

### Esempio per specificare i formati di paragrafo disponibili nel campo di selezione dell&#39;editor Rich Text {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Nuovi formati di blocco semantico sono disponibili per la selezione.

1. A seconda dell&#39;editor Rich Text, determinare e passare alla [posizione di configurazione](rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Attivate il ](rich-text-editor.md) campo di selezione dei paragrafi  [attivando il plug-in](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Specificare i formati che si desidera rendere disponibili nel campo](rich-text-editor.md) di selezione dei paragrafi.
1. I formati di paragrafo sono quindi disponibili per l’autore del contenuto dai campi di selezione nell’editor Rich Text.

Con gli elementi strutturali disponibili nell’editor Rich Text tramite le opzioni del formato di paragrafo, [!DNL Experience Manager] fornisce una buona base per lo sviluppo di contenuto accessibile. Gli autori dei contenuti non possono utilizzare l’editor Rich Text per formattare la dimensione del font o i colori o altri attributi correlati, impedendo la creazione di formattazione in linea. Al contrario, gli autori possono selezionare gli elementi strutturali appropriati, ad esempio le intestazioni, e utilizzare gli stili globali scelti dall&#39;opzione Stili per garantire una marcatura pulita e opzioni più avanzate per gli utenti che sfogliano con i propri fogli di stile e il contenuto strutturato correttamente.

## Utilizzo della funzione di modifica sorgente {#use-of-the-source-edit-feature}

In alcuni casi, gli autori dei contenuti dovranno esaminare e regolare il codice sorgente HTML creato mediante l’editor Rich Text. Ad esempio, un contenuto creato all’interno dell’editor Rich Text potrebbe richiedere più markup per garantire la conformità a WCAG 2.0. Questo può essere fatto con l&#39;opzione [modifica sorgente](rich-text-editor.md#aboutplugins) dell&#39;editor Rich Text. È possibile specificare la funzione [`sourceedit` nel plug-in `misctools`](rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilizzate attentamente la funzione `sourceedit`. Eventuali errori di digitazione e le funzioni non supportate possono causare problemi.

<!--
TBD ENGREVIEW: Is this only applicable to Classic UI? 

## Adding Support for further HTML Elements and Attributes {#adding-support-for-additional-html-elements-and-attributes}

To further extend the accessibility features of [!DNL Experience Manager], it is possible to extend the existing components based on the RTE (such as the `Text` and `Table` components) with extra elements and attributes.

The following procedure illustrates how to extend the `Table` component with a `Caption` element that provides information about a data table to assistive technology users:

### Example: Add a caption to a table properties dialog {#example-adding-the-caption-to-the-table-properties-dialog}

In the constructor of the `TablePropertiesDialog`, add an extra text input field that is used for editing the caption. Set the `itemId` to `caption` (the DOM attribute’s name) to automatically handle its content.

In a `Table`, set the attribute to the DOM element or or remove it from the DOM element. The dialog in the `config` object passed the value. Set or remove the DOM attributes using the corresponding `CQ.form.rte.Common` methods (`com` is a shortcut for `CQ.form.rte.Common`). Using `CQ.form.rte.Common` methods avoids common pitfalls with browser implementations.

>[!NOTE]
>
>This procedure is only suitable for the classic UI.

### Step-by-step instructions {#step-by-step-instructions}

1. Start CRXDE Lite. For example: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`. Create intermediate folders if those do not exist.

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` file to edit.

1. In the `constructor` method, before the mention of `var dialogRef = this;`, add the following code:

   ```javascript
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` file.

1. Add the following code at the end of the `transferConfigToTable` method:

   ```javascript
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. To save your changes, click **[!UICONTROL Save All]**.

## Best practices and limitations {#best-practices-limitations-tips}

* A plain text field is not the only type of input allowed for the value of the caption element. You can use any ExtJS widget, that provides the caption’s value through its `getValue()` method.
* To add editing capabilities for more elements and attributes, ensure that:

  * The `itemId` property for each corresponding field is set to the name of the appropriate DOM attribute (`TablePropertiesDialog`).
  * The attribute is set and/or removed on the DOM element explicitly (`Table`).
-->

>[!MORELIKETHIS]
>
>* [Guida rapida agli standard WCAG](/help/onboarding/accessibility/quick-guide-wcag.md)
>* [Come creare contenuto accessibile in  Experience Manager](/help/sites-cloud/authoring/fundamentals/accessible-content.md)

