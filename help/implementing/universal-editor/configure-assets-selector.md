---
title: Configurazione del selettore Assets per l’editor universale
description: Scopri come configurare il selettore delle risorse da utilizzare con l’Editor universale.
feature: Developing
role: Admin, Developer
source-git-commit: 0ed57393afaf9af3258dacdcb043487f4a098e03
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 1%

---


# Configurazione del selettore Assets per l’editor universale {#configure-assets-selector}

Scopri come configurare il selettore delle risorse da utilizzare con l’Editor universale.

## Panoramica {#overview}

L&#39;editor universale utilizza [il selettore risorse](/help/assets/overview-asset-selector.md#using-asset-selector) per consentire agli autori di sfogliare e selezionare le risorse da inserire nel contenuto.

Il selettore delle risorse può essere configurato nell&#39;Editor universale utilizzando i filtri dei componenti [.](/help/implementing/universal-editor/filtering.md) Questo documento descrive le opzioni di configurazione disponibili.

>[!NOTE]
>
>Quando avvii un progetto Universal Editor, non sono presenti filtri per il selettore delle risorse. Gli autori avranno accesso a tutte le risorse normalmente consentite dalle autorizzazioni utente.

## Definizione filtro {#filter-definition}

La definizione del filtro per il selettore delle risorse ha una struttura semplice.

```json
[
  {
    "id": "assets-filter",
    "assets": {...}
   }
]
```

## Opzioni filtro {#filter-options}

Il filtro `assets` può avere le seguenti opzioni.

* `deliveryTier?`: - Definisce quale dei seguenti livelli di consegna utilizzare:
   * `dm`: elemento multimediale dinamico (preferito) con fallback a `publish` se necessario
   * `publish`: istanza di pubblicazione AEM
* `repoNames?`: Stringa - Elenco di archivi AEM che possono essere utilizzati per selezionare le immagini.
   * Predefinito: tutti i repository di consegna
* `selectionTier?`: Stringa - Livelli AEM da cui selezionare le risorse
   * Predefinito: `["author", "delivery"]`
* `disableRemote?`: booleano - Disabilita supporto archivio remoto
* `preselectedTypes?`: Stringa - Tipi di file preselezionati da applicare come filtro predefinito nel selettore risorse
* `minMaxDimensions?`: oggetto - Fornisce dimensioni minime e/o massime (in pixel) da applicare come filtro predefinito nel selettore risorse
   * `widthMin?`: Numero - Larghezza minima
   * `widthMax?`: Numero - Larghezza massima
   * `heightMin?`: Numero - Altezza minima
   * `heightMax?`: Numero - Altezza massima
* `minMaxFileSize?`: oggetto - Specificare la dimensione file minima e/o massima (in byte) da applicare come filtro predefinito nel selettore risorse
   * `min?`: Numero - Dimensione minima file
   * `max?`: numero - Dimensione massima file
* `customFileTypeFilters?`: oggetto - Fornisce filtri del tipo di file personalizzati da visualizzare nel selettore risorse
   * `label`: Stringa - Etichetta da visualizzare nell&#39;interfaccia utente di selezione delle risorse
   * `value`: Stringa - Valore del tipo di file da filtrare
* `displayFilters?`: booleano: utilizzato per disabilitare l’interfaccia utente dei filtri nel selettore risorse; true per impostazione predefinita

## Esempio {#example}

L&#39;esempio seguente contiene la maggior parte delle opzioni a scopo illustrativo.

```json
[
  {
    "id": "assets-filter",
    "assets": {
      "deliveryTier": "dm",
      "repoNames": ["thisRepo", "thatRepo"],
      "selectionTier": ["author", "delivery"],
      "disableRemote": true,
      "preselectedTypes": ["png", "svg", "jpg", "gif"],
      "minMaxDimensions": {
        "widthMin": 640,
        "widthMax": 640,
        "heightMin": 480,
        "heightMax": 480
      },
      "minMaxFileSize": {
        "min": 1024,
        "max": 1024
      }
    }
   }
]
```

## Risorse aggiuntive {#additional-resources}

Per informazioni dettagliate sul selettore risorse, consulta il documento [Selettore risorse micro-front-end](/help/assets/overview-asset-selector.md#using-asset-selector) nella documentazione delle risorse.
