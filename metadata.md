---
product: adobe experience manager
description: Documentazione di Adobe Experience Manager as a Cloud Service.
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.it-IT
index: y
type: Documentation
solution: Experience Manager, Experience Manager as a Cloud Service
feature-set: Experience Manager Assets, Experience Manager Sites, Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager, Experience Manager Screens
version: Cloud Service
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: d0e79edd83faafc1233b812019c877ec360e50c8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 51%

---


# Metadati per uso interno

I metadati nel sistema di authoring GitHub sono gerarchici e vengono definiti in base ai seguenti livelli crescenti di precedenza.

1. metadata.md
1. Sommario
1. Articolo

I metadati definiti nel file metadata.md si applicano all’intero archivio, ma possono essere ignorati a livello di sommario e articolo. Eventuali esclusioni dei metadati devono essere eseguite al livello più basso possibile.

I metadati nell’archivio experience-manager-cloud-service.en sono il minimo richiesto.

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

Sommario

* `sub-product`
* `user-guide-title`

Articolo

* `title`
* `description`
* `contentOwner` (solo sul contenuto della risorsa principale in `/help/assets`)
