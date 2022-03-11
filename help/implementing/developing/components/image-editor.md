---
title: Editor immagine
description: L’editor di immagini è una parte fondamentale della AEM e può essere sfruttato dai componenti per facilitare la manipolazione delle immagini da parte degli autori di contenuti.
exl-id: c8ae4f59-75b1-49b4-8dd4-957d2e33000b
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 10%

---

# Editor immagine {#image-editor}

L’editor di immagini è una parte fondamentale della AEM e può essere sfruttato dai componenti per facilitare la manipolazione delle immagini da parte degli autori di contenuti.

## Unità relative per la mappa immagine {#relative-units-for-image-map}

L’Editor immagini persiste nelle aree della mappa immagine come unità assolute e relative. Le unità relative sono utili se fornite come attributi di dati per ridimensionare dinamicamente una mappa immagine (rispetto alle dimensioni dell’immagine) sul lato client in un componente immagine reattiva.

### imageMap, proprietà {#imagemap-property}

Le coordinate della mappa immagine vengono mantenute nel JCR come `imageMap` di Image Editor. Ha il seguente formato.

La proprietà memorizza le aree mappa come segue:

`[area1][area2][...]`

Formato area:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Esempio:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Supporto per le immagini di SVG {#support-for-svg-images}

La grafica vettoriale scalabile (SVG) è supportata dall’Editor immagini.

* Il trascinamento e rilascio di una risorsa SVG da DAM e il caricamento di un file SVG da un file system locale sono entrambi supportati.

## Abilitazione dei plug-in per tipo MIME {#enabling-plugins-by-mime-type}

In alcune situazioni le azioni di authoring devono essere limitate per alcuni tipi MIME, a causa della mancanza di supporto nell’elaborazione sul lato server. Ad esempio, la modifica di immagini SVG potrebbe non essere consentita.

I plug-in nell’Editor immagini possono essere attivati selettivamente dal tipo MIME impostando un `supportedMimeTypes` sul nodo di configurazione del singolo plug-in.

### Esempio {#example}

Ad esempio, supponiamo che la possibilità di ritagliare sia consentita solo per le immagini GIF, JPEG, PNG, WEBP e TIFF.

La `supportedMimeTypes` la proprietà deve quindi essere impostata come stringa dei tipi MIME consentiti sul nodo di configurazione del plug-in nel `cq:editConfig` nodo del componente immagine.

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
