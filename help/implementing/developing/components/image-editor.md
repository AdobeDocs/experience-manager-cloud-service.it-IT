---
title: Editor immagine
description: L’Editor immagine è un elemento fondamentale di AEM e può essere sfruttato dai componenti per facilitare la manipolazione delle immagini da parte degli autori di contenuti.
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---


# Editor immagine {#image-editor}

L’Editor immagine è un elemento fondamentale di AEM e può essere sfruttato dai componenti per facilitare la manipolazione delle immagini da parte degli autori di contenuti.

## Unità relative per la mappa immagine {#relative-units-for-image-map}

L’Editor immagine persiste nelle aree delle mappe immagine sia come unità assolute che come unità relative. Le unità relative sono utili se fornite come attributi di dati per ridimensionare dinamicamente una mappa immagine (relativa alle dimensioni dell’immagine) sul lato client in un componente immagine reattivo.

### imageMap, proprietà {#imagemap-property}

Le coordinate della mappa immagine vengono memorizzate in JCR come `imageMap` proprietà dall’Editor immagine. Ha il seguente formato.

Le aree di mappa vengono memorizzate nel modo seguente:

`[area1][area2][...]`

Formato area:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Esempio:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Supporto per immagini SVG {#support-for-svg-images}

La grafica vettoriale scalabile (SVG) è supportata dall’Editor immagini.

* Sono supportati il trascinamento di una risorsa SVG da DAM e il caricamento di un file SVG da un file system locale.

## Abilitazione dei plug-in per tipo MIME {#enabling-plugins-by-mime-type}

In alcune situazioni le azioni di creazione devono essere limitate per alcuni tipi MIME, a causa della mancanza di supporto nell&#39;elaborazione sul lato server. Ad esempio, la modifica di immagini SVG potrebbe non essere consentita.

I plug-in nell’Editor immagine possono essere attivati selettivamente dal tipo MIME impostando una `supportedMimeTypes` proprietà sul nodo di configurazione del singolo plug-in.

### Esempio {#example}

Ad esempio, è possibile ritagliare solo le immagini GIF, JPEG, PNG, WEBP e TIFF.

La `supportedMimeTypes` proprietà deve quindi essere impostata come una stringa dei tipi MIME consentiti sul nodo di configurazione del plug-in sul `cq:editConfig` nodo del componente immagine.

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
