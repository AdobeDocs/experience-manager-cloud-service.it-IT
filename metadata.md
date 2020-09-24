---
product: adobe experience manager
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.it-IT
index: y
solution-title: Adobe Experience Manager as a Cloud Service
solution-hub-url: https://docs.adobe.com/content/help/en/experience-manager-cloud-service/landing/home.html
getting-started-title: Guida introduttiva
getting-started-url: https://docs.adobe.com/content/help/en/experience-manager-cloud-service/overview/home.html
tutorials-title: Esercitazioni
tutorials-url: https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: 967d0993ba2114d0dd081724cf5e7754899b5c8e
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 20%

---


# Metadati per uso interno

I metadati nel sistema di creazione GitHub sono gerarchici ed è definito dai seguenti livelli crescenti di precedenti.

1. metadata.md
1. ToC
1. Articolo

I metadati definiti nel file metadata.md si applicano all’intero repo, ma possono essere sostituiti a livello di AC e di articolo. L&#39;eventuale sostituzione dei metadati deve essere eseguita al livello più basso possibile.

I metadati contenuti nel repo experience-manager-cloud-service.en sono il minimo richiesto.

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
* `contentOwner` (solo per il contenuto delle risorse di base in `/help/assets`)

Ulteriori informazioni sui metadati sono disponibili nella guida all’authoring [interna.](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/markdown/metadata.html#solution-metadata)
