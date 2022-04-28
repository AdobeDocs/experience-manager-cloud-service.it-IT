---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.4.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.4.0
feature: Release Information
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 5%

---

# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.4.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione AEM as a Cloud Service 2022.4.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.28 è il 22 aprile 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e creare rapporti sull’utilizzo delle API di Asset Manager non supportate. Esistono quattro API che non sono più supportate in AEM as a Cloud Service. I clienti devono assicurarsi di non utilizzare più queste API e devono utilizzare il nuovo metodo di caricamento delle risorse.

* Possibilità di rilevare l’utilizzo di modelli di frammenti di contenuto. I modelli per frammenti di contenuto non sono più supportati per la creazione di nuovi frammenti di contenuto in AEM as a Cloud Service. Per sostituire i modelli di frammento di contenuto, i clienti dovranno creare modelli di frammento di contenuto.

* Possibilità di rilevare le risorse con più di 100 discendenti sotto il nodo di metadati della risorsa nell’archivio. È consigliabile rimuovere i nodi di metadati non necessari per migliorare le prestazioni durante il caricamento di cartelle costituite da tali risorse.

* Possibilità di rilevare e segnalare il tipo di archivio dati utilizzato.

* Pattern aggiornato per AEM Portale moduli.

### Correzioni di bug {#bug-fixes-bpa}

* BPA segnalava i risultati per i componenti core invece di generare rapporti solo per i componenti cliente. Questo problema è stato risolto.