---
title: Configurare l’editor Rich Text per creare pagine Web e siti con accesso facilitato.
description: Scopri come configurare l’editor Rich Text per creare siti con accesso facilitato in Adobe Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 165dc4af656ce1bc431d2f921775ebda4cf4de9f
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Configure RTE to create accessible sites {#configure-rte-accessible-sites}

Adobe Experience Manager supporta funzioni di accessibilità standard, ad esempio testo alternativo per le immagini e funzioni aggiuntive accessibili al momento della creazione dei contenuti. Gli autori dei contenuti utilizzano queste funzioni con componenti che utilizzano l’editor Rich Text (Rich Text Editor). Ciò include l&#39;aggiunta di testo alt, informazioni strutturali tra titoli ed elementi di paragrafo e così via.

Per informazioni sulle configurazioni tipiche dell’editor Rich Text, consulta [Configurare l’editor Rich Text](rich-text-editor.md) e [configurare i plug-in dell’editor Rich Text per funzionalità](configure-rich-text-editor-plug-ins.md)specifiche.

Utilizzate la configurazione dei plug-in RTE per configurare e personalizzare le funzioni relative all’accessibilità. Ad esempio, utilizzare `paraformat` per aggiungere altri elementi semantici a livello di blocco, inclusa l&#39;estensione del numero di livelli di intestazione supportati oltre il livello di base `H1`e `H2` `H3` forniti per impostazione predefinita. La modifica RTF è possibile utilizzando molti componenti dell’interfaccia utente di authoring. I componenti più utilizzati sono testo, immagini, download e così via.

La funzionalità RTE può essere resa disponibile in molti componenti. Il componente principale è il `Text` componente.

Per il `Text` componente in Experience Manager, la schermata seguente mostra l’editor Rich Text con una serie di plug-in abilitati, tra cui `paraformat`:

![Componente Testo RTE in modalità a schermo intero](assets/rte-toolbar-full-screen-mode.png)

## Configurare le funzioni del plug-in {#configuring-the-plugin-features}

Per istruzioni su come configurare l’editor Rich Text, consultate [configurare la pagina Editor](rich-text-editor.md) Rich Text. L&#39;articolo riguarda:

* [Plugin e relative funzioni](rich-text-editor.md#aboutplugins)
* [Posizioni di configurazione](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [Attivare un plug-in e configurare la proprietà features](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [Configurare altre funzionalità dell’editor Rich Text](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

Per attivare alcune o tutte le funzioni di un plugin, configurare il plug-in all&#39;interno del `rtePlugins` sottoramo appropriato in CRXDE Lite.

![CRXDE Lite che mostra un esempio rtePlugin.](assets/chlimage_1-208.png)

### Esempio: specifica dei formati di paragrafo disponibili nel campo di selezione dell&#39;editor Rich Text {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Nuovi formati di blocco semantico possono essere resi disponibili per la selezione tramite:

1. A seconda dell’editor Rich Text, determina e passa al percorso [di](rich-text-editor.md#understand-the-configuration-paths-and-locations)configurazione.
1. [Attivate il campo](rich-text-editor.md) di selezione dei paragrafi [attivando il plug-in](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Specificare i formati che si desidera rendere disponibili nel campo](rich-text-editor.md)di selezione dei paragrafi.
1. I formati di paragrafo sono quindi disponibili per l’autore del contenuto dai campi di selezione nell’editor Rich Text.

Con gli elementi strutturali disponibili nell’editor Rich Text tramite le opzioni del formato di paragrafo, Experience Manager offre una buona base per lo sviluppo di contenuti accessibili. Gli autori dei contenuti non possono utilizzare l’editor Rich Text per formattare la dimensione del font o i colori o altri attributi correlati, impedendo la creazione di formattazione in linea. Devono invece selezionare gli elementi strutturali appropriati, ad esempio le intestazioni, e utilizzare gli stili globali scelti dall&#39;opzione Stili. In questo modo, gli utenti che sfogliano con i propri fogli di stile e con contenuti strutturati correttamente possono usufruire di una marcatura pulita e di opzioni maggiori.

## Utilizzo della funzione di modifica sorgente {#use-of-the-source-edit-feature}

In alcuni casi, gli autori dei contenuti dovranno esaminare e regolare il codice sorgente HTML creato mediante l’editor Rich Text. Ad esempio, un contenuto creato all’interno dell’editor Rich Text potrebbe richiedere una marcatura aggiuntiva per garantire la conformità a WCAG 2.0. Questa operazione può essere eseguita con l’opzione di modifica [](rich-text-editor.md#aboutplugins) sorgente dell’editor Rich Text. Potete specificare la [`sourceedit` funzione sul `misctools` plug-in](rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilizzate la `sourceedit` funzione con attenzione. Gli errori di digitazione e/o le funzioni non supportate possono causare altri problemi.

<!--
TBD ENGREVIEW: Is this only applicable to Classic UI? 

## Adding Support for Additional HTML Elements and Attributes {#adding-support-for-additional-html-elements-and-attributes}

To further extend the accessibility features of Experience Manager, it is possible to extend the existing components based on the RTE (such as the `Text` and `Table` components) with additional elements and attributes.

The following procedure illustrates how to extend the `Table` component with a `Caption` element that provides information about a data table to assistive technology users:

### Example: Add a caption to a table properties dialog {#example-adding-the-caption-to-the-table-properties-dialog}

In the constructor of the `TablePropertiesDialog`, add an additional text input field that is used for editing the caption. Set the `itemId` to `caption` (the DOM attribute’s name) to automatically handle its content.

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
* To add editing capabilities for further additional elements and attributes, ensure that:

  * The `itemId` property for each corresponding field is set to the name of the appropriate DOM attribute (`TablePropertiesDialog`).
  * The attribute is set and/or removed on the DOM element explicitly (`Table`).
-->

>[!MORELIKETHIS]
>
>* [Guida rapida agli standard WCAG](/help/onboarding/accessibility/quick-guide-wcag.md)

