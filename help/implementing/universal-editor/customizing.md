---
title: Personalizzazione dell’interfaccia utente
description: Scopri i diversi punti di estensione che ti consentono di personalizzare l’interfaccia utente di Universal Editor per supportare le esigenze degli autori di contenuti.
source-git-commit: 65893c0c0dee37bed8ecfbb06a12e7c093c4397c
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
