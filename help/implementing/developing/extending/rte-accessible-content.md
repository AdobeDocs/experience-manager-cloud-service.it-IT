---
title: Configura l’editor Rich Text per creare pagine web e siti accessibili.
description: Scopri come configurare l’editor Rich Text per creare siti accessibili in [!DNL Adobe Experience Manager].
contentOwner: AG
exl-id: 54050fc9-0348-4033-8e2b-b3897588cb62
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---

# Configurare l’editor Rich Text per creare siti accessibili {#configure-rte-accessible-sites}

[!DNL Adobe Experience Manager] supporta funzioni di accessibilità standard, ad esempio testo alternativo per le immagini, e funzioni aggiuntive accessibili durante la creazione di contenuti. Gli autori di contenuti utilizzano queste funzioni con componenti che utilizzano l’editor Rich Text. Le funzioni includono l’aggiunta di testo alternativo, informazioni strutturali tramite intestazioni, elementi di paragrafo e così via.

Per informazioni sulle configurazioni tipiche dell’editor Rich Text, consulta [configurare RTE](rich-text-editor.md) e [configurare i plug-in RTE per funzionalità specifiche](configure-rich-text-editor-plug-ins.md).

Utilizza la configurazione dei plug-in RTE per configurare e personalizzare le funzioni relative all’accessibilità. Ad esempio, utilizza `paraformat` per aggiungere elementi semantici a livello di blocco extra, compreso l’estensione del numero di livelli di intestazione supportati oltre il livello di base `H1`, `H2` e `H3` fornito per impostazione predefinita. La modifica avanzata del testo è possibile utilizzando molti componenti dell’interfaccia utente di authoring. I componenti comunemente utilizzati sono testo, immagine, download e così via.

La funzionalità RTE può essere resa disponibile in molti componenti. Il componente principale è il `Text` componente.

Per `Text` componente in [!DNL Experience Manager], la schermata seguente visualizza l’editor Rich Text con una serie di plug-in abilitati, tra cui `paraformat`:

![Componente Testo RTE in modalità a schermo intero](assets/rte-toolbar-full-screen-mode.png)

## Configurare le funzioni del plug-in {#configuring-the-plugin-features}

Per istruzioni su come configurare l’editor Rich Text, consulta [configurare l’editor Rich Text](rich-text-editor.md) pagina. L&#39;articolo riguarda:

* [Plug-in e relative funzioni](rich-text-editor.md#aboutplugins)
* [Posizioni di configurazione](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [Attivare un plug-in e configurare la proprietà features](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [Configurare altre funzionalità dell’editor Rich Text](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

Per attivare alcune o tutte le funzioni di un plug-in, configura il plug-in all’interno dei `rtePlugins` in CRXDE Lite.

![CRXDE Lite mostra un esempio di rtePlugin](assets/example-rteplugin-crxde-lite.png)

### Esempio per specificare i formati paragrafo disponibili nel campo di selezione dell’editor Rich Text {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Nuovi formati di blocchi semantici sono disponibili per la selezione.

1. A seconda dell’editor Rich Text, determina e naviga fino al [percorso di configurazione](rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Attiva il campo di selezione dei paragrafi](rich-text-editor.md) da [attivazione del plug-in](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Specificare i formati che si desidera rendere disponibili nel campo di selezione dei paragrafi](rich-text-editor.md).
1. I formati di paragrafo sono quindi disponibili per l’autore del contenuto dai campi di selezione nell’editor Rich Text.

Con gli elementi strutturali disponibili nell’editor Rich Text tramite le opzioni del formato paragrafo, [!DNL Experience Manager] fornisce una buona base per lo sviluppo di contenuti accessibili. Gli autori di contenuti non possono utilizzare l’editor Rich Text per formattare la dimensione del font o i colori o altri attributi correlati, impedendo la creazione di formattazione in linea. Al contrario, gli autori possono selezionare gli elementi strutturali appropriati, come le intestazioni e utilizzare gli stili globali selezionati dall’opzione Stili per garantire un markup pulito e opzioni più avanzate per gli utenti che navigano con i propri fogli di stile e contenuti strutturati correttamente.

## Utilizzo della funzione Modifica origine {#use-of-the-source-edit-feature}

In alcuni casi, gli autori di contenuti dovranno esaminare e regolare il codice sorgente HTML creato utilizzando l’editor Rich Text. Ad esempio, per garantire la conformità alle linee guida WCAG 2.0, un contenuto creato all’interno dell’editor Rich Text può richiedere più markup. Questo può essere fatto con le [modifica sorgente](rich-text-editor.md#aboutplugins) opzione dell’editor Rich Text. Puoi specificare la [`sourceedit` sulla `misctools` plug-in](rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilizza la `sourceedit` con attenzione. Eventuali errori di digitazione e le funzioni non supportate possono causare problemi.

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
>* [Guida rapida agli standard WCAG](/help/compliance/accessibility/quick-guide-wcag.md)
>* [Come creare contenuto accessibile in Experience Manager](/help/sites-cloud/authoring/fundamentals/accessible-content.md)

