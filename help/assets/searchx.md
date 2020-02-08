---
title: Ampliare le opzioni e le funzioni di ricerca in Risorse Adobe Experience Manager
description: Estendi le funzionalità di ricerca delle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Estendi ricerca risorse {#extend-assets-search}

Puoi estendere le funzionalità di ricerca di Risorse Adobe Experience Manager (AEM). Risorse AEM cerca automaticamente le risorse in base alle stringhe.

La ricerca viene eseguita tramite l&#39;interfaccia QueryBuilder, in modo da personalizzare la ricerca con diversi predicati. Potete sovrapporre il set predefinito di predicati nella seguente directory: `/apps/dam/content/search/searchpanel/facets`.

Puoi anche aggiungere altre schede al pannello di amministrazione di Risorse AEM.

## Sovrapposizione {#overlay}

Per sovrapporre i predicati preconfigurati, copiate il `facets` nodo da `/libs/dam/content/search/searchpanel` a `/apps/dam/content/search/searchpanel/` o specificate un&#39;altra `facetURL` proprietà nella configurazione del pannello di ricerca (l&#39;impostazione predefinita è `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

>[!NOTE]
>
>Per impostazione predefinita, la struttura di directory in `/apps` non esiste e deve essere creata. Assicurarsi che i tipi di nodo corrispondano a quelli in `/libs`.

### Aggiungi schede {#add-tabs}

Puoi aggiungere ulteriori schede di ricerca configurandole nell’amministratore di Risorse AEM. Per creare schede aggiuntive:

1. Create la struttura delle cartelle `/apps/wcm/core/content/damadmin/tabs,`se non esiste già, quindi copiate il `tabs` nodo da `/libs/wcm/core/content/damadmin` e incollatelo.
1. Create e configurate la seconda scheda, come desiderato.

   >[!NOTE]
   >
   >Quando si crea una seconda `siteadminsearchpanel`, assicurarsi di impostare una `id` proprietà per evitare conflitti tra i moduli.

### Creare predicati personalizzati {#create-custom-predicates}

Risorse AEM include un set di predicati predefiniti che possono essere utilizzati per personalizzare una pagina Condivisione risorse.
<!-- In addition to using pre-existing predicates, AEM developers can also create their own predicates using the [Query Builder API](/help/sites-developing/querybuilder-api.md). -->

La creazione di predicati personalizzati richiede conoscenze di base sul framework [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)Widget.

La procedura ottimale consiste nel copiare e regolare un predicato esistente. I predicati di esempio si trovano in **/libs/cq/search/components/predicates**.

#### Esempio: Creare un semplice predicato di proprietà {#example-build-a-simple-property-predicate}

Per creare un predicato di proprietà:

1. Create una cartella di componenti nella directory dei progetti, ad esempio **/apps/geometrixx/components/titlepredicate**.
1. Aggiungi **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Aggiungi `titlepredicate.jsp`.

   ```xml
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. Per rendere disponibile il componente, è necessario essere in grado di modificarlo. Per rendere modificabile un componente, in CRXDE aggiungete un nodo **cq:editConfig** di tipo principale **cq:EditConfig**. Per rimuovere i paragrafi, aggiungete una proprietà con più valori **cq:actions** con un singolo valore **CANC**.
1. Passate al browser e nella pagina di esempio (ad esempio, **press.html**) passate alla modalità di progettazione e attivate il nuovo componente per il sistema di paragrafi del predicato (ad esempio, **a sinistra**).

1. In modalità **Modifica** , il nuovo componente è ora disponibile nella barra laterale (nel gruppo **Ricerca** ). Inserite il componente nella colonna **Predicati** e digitate una parola di ricerca, ad esempio **Romboidale** , quindi fate clic sulla lente di ingrandimento per avviare la ricerca.

   >[!NOTE]
   >
   >Durante la ricerca, accertarsi di digitare esattamente il termine, compreso il caso corretto.

#### Esempio: Creare un semplice predicato di gruppo {#example-build-a-simple-group-predicate}

Per creare un predicato di gruppo:

1. Create una cartella di componenti nella directory dei progetti, ad esempio **/apps/geometrixx/components/picspredicate.**
1. Aggiungi **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Aggiungi **titlepredicate.jsp**:

   ```xml
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. Per rendere disponibile il componente, è necessario essere in grado di modificarlo. Per rendere modificabile un componente, in CRXDE aggiungete un nodo **cq:editConfig** di tipo principale **cq:EditConfig**. Per rimuovere i paragrafi, aggiungete una proprietà con più valori **cq:actions** con un singolo valore **CANC**.
1. Passate al browser e nella pagina di esempio (ad esempio, **press.html**) passate alla modalità di progettazione e attivate il nuovo componente per il sistema di paragrafi del predicato (ad esempio, **a sinistra**).
1. In modalità **Modifica** , il nuovo componente è ora disponibile nella barra laterale (nel gruppo **Ricerca** ). Inserite il componente nella colonna **Predicati** .

### Widget predicato installati {#installed-predicate-widgets}

I seguenti predicati sono disponibili come widget ExtJS preconfigurati.

#### FulltextPredicate {#fulltextpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Stringa</td>
   <td>Nome del predicato. Il valore predefinito è 'fulltext'</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>Funzione</td>
   <td>Callback per attivare la ricerca sull'evento "keyup". Impostazione predefinita su 'CQ.wcm.SiteAdmin.doSearch'</td>
  </tr>
 </tbody>
</table>

#### PropertyPredicate {#propertypredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Stringa</td>
   <td>Nome del predicato. Impostazione predefinita: 'proprietà'.</td>
  </tr>
  <tr>
   <td>propertyName</td>
   <td>Stringa </td>
   <td>Nome della proprietà JCR. Impostazione predefinita su 'jcr:title'</td>
  </tr>
  <tr>
   <td>defaultValue<br /> </td>
   <td>Stringa<br /> </td>
   <td>Valore predefinito precompilato.<br /> </td>
  </tr>
 </tbody>
</table>

#### PathPredicate {#pathpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Stringa</td>
   <td>Nome del predicato. Impostazioni predefinite su 'path'</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Stringa </td>
   <td>Percorso principale del predicato. Impostazione predefinita per '/content/dam'</td>
  </tr>
  <tr>
   <td>pathFieldPredicateName</td>
   <td>Stringa</td>
   <td>Impostazione predefinita su 'folder'</td>
  </tr>
  <tr>
   <td>showFlatOption</td>
   <td>Booleano</td>
   <td>Contrassegno per visualizzare la casella di controllo "Cerca nelle sottocartelle". Valori predefiniti per true.</td>
  </tr>
 </tbody>
</table>

#### DatePredicate {#datepredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Stringa</td>
   <td>Nome del predicato. Il valore predefinito è 'daterange'</td>
  </tr>
  <tr>
   <td>propertyName</td>
   <td>Stringa</td>
   <td>Nome della proprietà JCR. Impostazione predefinita su 'jcr:content/jcr:lastModified'</td>
  </tr>
  <tr>
   <td>defaultValue </td>
   <td>Stringa </td>
   <td>Valore predefinito precompilato </td>
  </tr>
 </tbody>
</table>

#### OptionsPredicate {#optionspredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>titolo </td>
   <td>Stringa </td>
   <td>Aggiunge un altro titolo superiore </td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Stringa</td>
   <td>Nome del predicato. Il valore predefinito è 'daterange'</td>
  </tr>
  <tr>
   <td>propertyName</td>
   <td>Stringa</td>
   <td>Nome della proprietà JCR. Impostazione predefinita su 'jcr:content/metadata/cq:tags'</td>
  </tr>
  <tr>
   <td>collassare</td>
   <td>Stringa</td>
   <td>Comprimi livello. Il valore predefinito è 'level1'</td>
  </tr>
  <tr>
   <td>triggerSearch</td>
   <td>Booleano </td>
   <td>Flag per l’attivazione della ricerca al momento della verifica. Il valore predefinito è false</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>Funzione</td>
   <td>Callback per attivare la ricerca. Il valore predefinito è 'CQ.wcm.SiteAdmin.doSearch'</td>
  </tr>
  <tr>
   <td>searchTimeoutTime</td>
   <td>Numero</td>
   <td>Timeout prima che searchCallback venga attivato. Il valore predefinito è 800 ms</td>
  </tr>
 </tbody>
</table>
