---
title: Personalizzazione dell’authoring pagina
description: Scopri i meccanismi forniti da AEM as a Cloud Service per personalizzare la funzionalità di authoring delle pagine.
exl-id: 98d3c7ab-46d2-4e8d-b0da-5c8a7b398135
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 3%

---

# Personalizzazione dell’authoring pagina {#customizing-page-authoring}

Adobe Experience Manager as a Cloud Service offre meccanismi che ti consentono di personalizzare la funzionalità di authoring delle pagine (e le [console](/help/implementing/developing/extending/consoles.md)) della tua istanza di authoring.

## Clientlibs {#clientlibs}

Le clientlibs consentono di estendere l’implementazione predefinita per abilitare nuove funzionalità, riutilizzando le funzioni, gli oggetti e i metodi standard.

Durante la personalizzazione, puoi creare la tua libreria client in `/apps.`. La nuova libreria client deve:

* Dipende dalla libreria client di authoring `cq.authoring.editor.sites.page`.
* Appartenere alla categoria `cq.authoring.editor.sites.page.hook` appropriata.

Vedi [Utilizzo delle librerie lato client in AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md).

## Sovrapposizioni {#overlays}

Le sovrapposizioni si basano sulle definizioni dei nodi e consentono di sovrapporre la funzionalità standard in `/libs` con la funzionalità personalizzata in `/apps`.

Durante la creazione di una sovrapposizione, non è necessaria una copia 1:1 dell&#39;originale, in quanto [sling resource merger](/help/implementing/developing/introduction/sling-resource-merger.md) consente l&#39;ereditarietà.

Per ulteriori informazioni, vedere la [documentazione JS ](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Per ulteriori informazioni sulle sovrapposizioni, vedere [Sovrapposizioni per Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Aggiungi nuovo livello (modalità) {#add-new-layer-mode}

Quando modifichi una pagina, sono disponibili varie [modalità](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes). Queste modalità sono implementate utilizzando [livelli](/help/implementing/developing/introduction/ui-structure.md#layer). Consentono di accedere a diversi tipi di funzionalità per lo stesso contenuto della pagina. Le modalità standard di AEM includono Modifica, Layout, Sviluppatore, Timewarp, Stato Live Copy e Targeting.

### Esempio di livello: stato Live Copy {#layer-example-live-copy-status}

Un’istanza AEM standard fornisce il livello MSM. Consente di accedere ai dati relativi alla [gestione multisito](/help/sites-cloud/administering/msm/overview.md) e di evidenziarli nel livello.

Per vederlo in azione, puoi modificare qualsiasi copia per lingua nel [contenuto di esempio WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) e selezionare la modalità **Stato Live Copy**.

Puoi trovare la definizione del livello MSM (per riferimento) in:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Esempio di codice {#code-sample}

Questo è un pacchetto di esempio che mostra come creare un livello (modalità) per la vista MSM.

Puoi trovare il codice di questa pagina in [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode).

## Aggiungi nuova categoria selezione al browser risorse {#add-new-selection-category-to-asset-browser}

Il browser Risorse mostra risorse di vari tipi/categorie (ad esempio, immagini e documenti). Le risorse possono essere filtrate anche in base a queste categorie di risorse.

### Esempio di codice {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` è un pacchetto di esempio che mostra come aggiungere un gruppo a Asset Finder. Questo esempio si connette al flusso pubblico di [Flickr](https://www.flickr.com) e lo mostra nel pannello laterale.

Puoi trovare il codice di questa pagina in [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr).

## Filtrare le risorse {#filtering-resources}

Durante l’authoring delle pagine, l’utente deve spesso selezionare tra le risorse di un elenco.

Per mantenere l’elenco a una dimensione ragionevole e pertinente al caso d’uso, un filtro può essere implementato sotto forma di predicato personalizzato. Ad esempio, se il componente Granite `pathbrowser` viene utilizzato per consentire all&#39;utente di selezionare il percorso di una particolare risorsa, i percorsi presentati possono essere filtrati nel modo seguente:

* Implementare il predicato personalizzato implementando l&#39;interfaccia [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html).
* Specificare un nome per il predicato e fare riferimento a tale nome quando si utilizza `pathbrowser`.

Per ulteriori dettagli sulla creazione di un predicato personalizzato, vedi [questo articolo](/help/implementing/developing/introduction/query-builder-custom-predicate.md).

## Aggiungere una nuova azione alla barra degli strumenti di un componente {#add-new-action-to-a-component-toolbar}

Ogni componente dispone in genere di una barra degli strumenti che consente di accedere a una serie di azioni che possono essere eseguite su quel componente.

### Esempio di codice {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` è un pacchetto di esempio che mostra come creare un&#39;azione della barra degli strumenti personalizzata per eseguire il rendering dei componenti.

Puoi trovare il codice di questa pagina in [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot).

## Aggiungi nuovo editor locale {#add-new-in-place-editor}

### Editor locale standard {#standard-in-place-editor}

In un’installazione standard di AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` contiene le definizioni dei vari editor disponibili.

1. Esiste una connessione tra l’editor e ogni tipo di risorsa (come nel componente) che può utilizzarla:

   * `cq:inplaceEditing`

     ad esempio:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * proprietà: `editorType`

           Definisce il tipo di editor in linea utilizzato quando viene attivata la modifica diretta per quel componente, ad esempio `text`, `textimage`, `image`, `title`.

1. È possibile configurare ulteriori dettagli di configurazione dell&#39;editor utilizzando un nodo `config` contenente configurazioni e un nodo `plugin` per contenere i dettagli di configurazione del plug-in necessari.


Di seguito è riportato un esempio di definizione delle proporzioni per il plug-in di ritaglio immagine del componente immagine.

```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
```

>[!NOTE]
>
>I rapporti di ritaglio di AEM, impostati dalla proprietà `ratio`, sono definiti come **altezza/larghezza**. Ciò differisce dalla definizione tradizionale di larghezza/altezza e viene fatto per ragioni di compatibilità con le versioni precedenti. Gli utenti che creano i file non noteranno alcuna differenza, a condizione che tu definisca chiaramente la proprietà `name`, in quanto questo è ciò che viene visualizzato nell&#39;interfaccia utente.

#### Creazione di un nuovo editor locale {#creating-a-new-in-place-editor}

Per implementare un nuovo editor locale (nella libreria client):

1. Implementare:

   * `setUp`
   * `tearDown`

1. Registra l’editor (include il costruttore):

   * `editor.register`

1. Fornisci la connessione tra l’editor e ogni tipo di risorsa (come nel componente) che può utilizzarlo.

#### Esempio di codice per la creazione di un nuovo editor locale {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` è un pacchetto di esempio che mostra come creare un editor locale in AEM.

Puoi trovare il codice di questa pagina in [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor).

## Aggiungi un&#39;azione Nuova pagina {#add-a-new-page-action}

Per aggiungere una nuova azione di pagina alla barra degli strumenti della pagina, ad esempio, **Torna a Sites** (console).

### Esempio di codice {#code-sample-3}

`aem-authoring-extension-header-backtosites` è un pacchetto di esempio che mostra come creare un&#39;azione personalizzata della barra di intestazione per tornare alla console Sites.

Puoi trovare il codice di questa pagina in [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites).

## Personalizzazione del flusso di lavoro Richiesta attivazione {#customizing-the-request-for-activation-workflow}

Flusso di lavoro predefinito, **Richiesta di attivazione**:

* Verrà visualizzato automaticamente nel menu appropriato quando un autore di contenuti **non dispone** dei diritti di replica appropriati, ma **non dispone di** appartenenze a DAM-Users e Author.

* In caso contrario, non viene visualizzato nulla, poiché i diritti di replica sono stati rimossi.

Per personalizzare il comportamento di questa attivazione, puoi sovrapporre il flusso di lavoro **Richiesta di attivazione**:

1. In `/apps` sovrapporre la procedura guidata **di** Sites`/libs/wcm/core/content/common/managepublicationwizard`

   * Questa azione esegue l&#39;override dell&#39;istanza comune di `/libs/cq/gui/content/common/managepublicationwizard`.

1. Se necessario, aggiorna il modello del flusso di lavoro e le configurazioni/script correlati.
1. Rimuovere il diritto all&#39;azione `replicate` da tutti gli utenti appropriati per tutte le pagine rilevanti. Per attivare questo flusso di lavoro come azione predefinita quando uno qualsiasi degli utenti, prova a pubblicare (o replicare) una pagina.
