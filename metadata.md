---
product: adobe experience manager
description: Documentazione di Cloud Service su Adobe Experience Manager .
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.it-IT
index: y
type: Documentation
solution: Experience Manager
version: Cloud Service
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 6%

---


# Metadati per uso interno

I metadati nel sistema di authoring GitHub sono gerarchici e vengono definiti i seguenti livelli crescenti di precedenti.

1. metadata.md
1. ToC
1. Articolo

I metadati definiti nel file metadata.md si applicano all&#39;intero repository, ma possono essere ignorati a livello di AC e di articolo. Qualsiasi override dei metadati deve essere eseguito al livello più basso possibile.

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

ToCs

* `sub-product`
* `user-guide-title`

Articolo

* `title`
* `description`
* `contentOwner` (solo sul contenuto delle risorse di base in  `/help/assets`)
