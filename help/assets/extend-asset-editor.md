---
title: Estensione dell’editor di risorse
description: Scoprite come estendere le funzionalità dell'editor di risorse utilizzando componenti personalizzati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c978be66702b7f032f78a1509f2a11315d1ed89f
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 13%

---


# Estensione dell’Editor risorse {#extending-asset-editor}

Editor risorse è la pagina che si apre quando si fa clic su una risorsa reperibile tramite Condivisione risorse per consentire all’utente di modificare tali aspetti della risorsa come metadati, miniature, titoli e tag.

La configurazione dell’editor mediante i componenti di modifica predefiniti è descritta in [Creazione e configurazione di una pagina](https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-finder-editor.html)Editor risorse.

Oltre a utilizzare componenti dell’editor preesistenti, gli sviluppatori Adobe Experience Manager (AEM) possono anche creare i propri componenti.

## Creazione di un modello di Editor risorse {#creating-an-asset-editor-template}

In geometrixx sono incluse le seguenti pagine di esempio:

* Pagina campione Geometrixx: `/content/geometrixx/en/press/asseteditor.html`
* Modello di esempio: `/apps/geometrixx/templates/asseteditor`
* Esempio di componente pagina: `/apps/geometrixx/components/asseteditor`

### Configurazione di Clientlib {#configuring-clientlib}

I componenti AEM Assets utilizzano un&#39;estensione della clientlib di modifica WCM. I clientlibs solitamente sono caricati in `init.jsp`.

Rispetto al caricamento clientlib predefinito (nei core `init.jsp`), un modello di Risorse AEM deve avere i seguenti elementi:

* Il modello deve includere la `cq.dam.edit` clientlib (invece di `cq.wcm.edit`).

* Per poter eseguire il rendering di predicati, azioni e obiettivi, clientlib deve essere incluso anche in modalità WCM disabilitata (ad esempio, caricata **al momento della pubblicazione**).

Nella maggior parte dei casi, la copia del campione esistente `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`) deve soddisfare tali esigenze.

### Configurazione delle azioni JS {#configuring-js-actions}

Alcuni dei componenti di AEM Assets richiedono funzioni JS definite in `component.js`. Copiate questo file nella directory dei componenti e collegatelo.

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

L&#39;esempio carica questa origine javascript in `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### Fogli di stile aggiuntivi {#additional-style-sheets}

Alcuni dei componenti di Risorse AEM utilizzano la libreria widget di AEM. Per poter eseguire correttamente il rendering nel contesto del contenuto, è necessario caricare un foglio di stile aggiuntivo. Il componente azione tag richiede un altro componente.

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Foglio di stile Geometrixx {#geometrixx-style-sheet}

I componenti della pagina di esempio richiedono che tutti i selettori inizino con `.asseteditor` il `static.css` (`/etc/designs/geometrixx/static.css`). Procedura consigliata: Copiare tutti `.asseteditor` i selettori nel foglio di stile e regolare le regole come desiderato.

### FormChooser: Adeguamenti delle risorse eventualmente caricate {#formchooser-adjustments-for-eventually-loaded-resources}

L’Editor risorse utilizza il Selettore moduli, che consente di modificare le risorse, in questo caso le risorse, nella stessa pagina del modulo semplicemente aggiungendo all’URL della risorsa un selettore di modulo e il percorso del modulo.

Ad esempio:

* Pagina modulo semplice: [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* Risorsa caricata nella pagina del modulo: [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

Le maniglie del campione in `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) eseguono le seguenti operazioni:

* Rilevano se una risorsa è caricata o se è necessario visualizzare il modulo normale.
* Se una risorsa viene caricata, questa disattiva la modalità WCM come parsys e può essere modificata solo in una pagina di modulo normale.
* Se una risorsa viene caricata, utilizza il titolo invece di quello nella pagina del modulo.

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

Nella parte HTML, utilizzate il set di titoli precedente (risorsa o titolo della pagina):

```html
<title><%= title %></title>
```

## Creazione di un componente campo modulo semplice {#creating-a-simple-form-field-component}

Questo esempio descrive come creare un componente che mostri e visualizzi i metadati di una risorsa caricata.

1. Create una cartella di componenti nella directory dei progetti, ad esempio `/apps/geometrixx/components/samplemeta`.
1. Aggiungi `content.xml` con il seguente snippet:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. Aggiungi `samplemeta.jsp` con il seguente snippet:

   ```javascript
   <%--
   
     Sample metadata field comopnent
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource will be the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. Per rendere disponibile il componente, devi essere in grado di modificarlo. To make a component editable, in CRXDE Lite, add a node `cq:editConfig` of primary type `cq:EditConfig`. Per rimuovere i paragrafi, aggiungi una proprietà con più valori `cq:actions` che presenta un singolo valore `DELETE`.

1. Passate al browser e sulla pagina di esempio (ad esempio, `asseteditor.html`) passate alla modalità di progettazione e attivate il nuovo componente per il sistema di paragrafi.

1. Nella modalità **Modifica**, il nuovo componente, ad esempio, **Metadati campione**, è ora disponibile nella barra laterale (gruppo **Editor risorse**). Inserisci il componente. Per memorizzare i metadati, è necessario aggiungerli al modulo relativo.

## Modifica delle opzioni dei metadati {#modifying-metadata-options}

È possibile modificare gli spazi dei nomi disponibili nel modulo [di](https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-finder-editor.html)metadati.

I metadati attualmente disponibili sono definiti in `/libs/dam/options/metadata`:

* Il primo livello all&#39;interno di questa directory contiene gli spazi dei nomi.
* Gli elementi all&#39;interno di ogni namespace rappresentano un metadati, ad esempio un elemento parte locale.
* Il contenuto dei metadati contiene le informazioni relative al tipo e alle opzioni multivalore.

Le opzioni possono essere sovrascritte in `/apps/dam/options/metadata`:

1. Copiate la directory da `/libs` a `/apps`.

1. Rimuovere, modificare o aggiungere elementi.

>[!NOTE]
>
>Se si aggiungono nuovi spazi dei nomi, questi devono essere registrati nella directory archivio/CRX. In caso contrario, l&#39;invio del modulo di metadati causerà un errore.
