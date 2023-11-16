---
title: Note sulla versione 2022.4.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2022.4.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 5%

---

# Note sulla versione 2022.4.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2022.4.0 degli strumenti di migrazione in AEM as a Cloud Service.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.28 è il 22 aprile 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e segnalare l’utilizzo di API di Asset Manager non supportate. Quattro API non sono più supportate in AEM as a Cloud Service. I clienti devono assicurarsi di non utilizzare più queste API e di utilizzare il nuovo metodo di caricamento delle risorse.

* Possibilità di rilevare l’utilizzo di modelli per frammenti di contenuto. I modelli per frammenti di contenuto non sono più supportati per la creazione di nuovi frammenti di contenuto su AEM as a Cloud Service. I clienti devono creare modelli per frammenti di contenuto in sostituzione dei modelli per frammenti di contenuto.

* Possibilità di rilevare le risorse con più di 100 discendenti sotto il nodo di metadati della risorsa nell’archivio. Si consiglia di rimuovere i nodi di metadati che non sono necessari per migliorare le prestazioni durante il caricamento di cartelle contenenti tali risorse.

* Possibilità di rilevare e segnalare il tipo di Archivio dati utilizzato.

* Pattern aggiornato per AEM Form Portal.

### Correzioni di bug {#bug-fixes-bpa}

* BPA riportava i risultati per i componenti core invece di riferire solo sui componenti del cliente. Questo problema è stato risolto.
