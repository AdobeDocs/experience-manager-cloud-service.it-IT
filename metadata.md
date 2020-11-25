---
product: adobe experience manager
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.it-IT
index: y
type: Documentation
solution-title: Adobe Experience Manager as a Cloud Service
solution-hub-url: https://experienceleague.adobe.com/docs/experience-manager-cloud-service/landing/home.html
getting-started-title: Guida introduttiva
getting-started-url: https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/home.html
tutorials-title: Esercitazioni
tutorials-url: https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: 8832307a96160a3d45cc85942473a5ada288a74f
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 10%

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
