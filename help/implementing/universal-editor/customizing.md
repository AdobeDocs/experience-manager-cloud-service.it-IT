---
title: Personalizzazione dell’interfaccia utente
description: Scopri i diversi punti di estensione che ti consentono di personalizzare l’interfaccia utente di Universal Editor per supportare le esigenze degli autori di contenuti.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---


# Personalizzazione dell’interfaccia utente {#customizing-ui}

Scopri i diversi punti di estensione che ti consentono di personalizzare l’interfaccia utente di Universal Editor per supportare le esigenze degli autori di contenuti.

## Disabilitazione della pubblicazione {#disable-publish}

Alcuni flussi di lavoro di authoring richiedono la revisione del contenuto prima della pubblicazione. In tali situazioni, l’opzione per pubblicare non deve essere disponibile per alcun autore.

Il **Pubblica** Il pulsante può quindi essere eliminato completamente in un’app aggiungendo i seguenti metadati.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```
