---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.4.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.4.0
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
source-git-commit: 717b2c851a18ef5171d64a462509ce08fb87a59c
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
