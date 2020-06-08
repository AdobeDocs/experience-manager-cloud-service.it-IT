---
title: Struttura della gestione multisito per contenuti di destinazione
description: Un diagramma illustra il modo in cui è strutturato il supporto multisito per contenuti di destinazione
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 86%

---


# Struttura della gestione multisito per contenuti di destinazione {#how-multisite-management-for-targeted-content-is-structured}

Il diagramma seguente illustra il modo in cui è strutturato il supporto multisito per contenuti di destinazione.

Areas appear underneath **/content/campaigns/&lt;brand>** and by default each brand has a master area, which is created automatically. Ogni area contiene la propria serie di attività, esperienze e offerte.

![Struttura multisito](/help/sites-cloud/authoring/assets/multisite-structure.png)

Per cercare contenuti di destinazione, le pagine o i siti possono essere associati a un&#39;area. Se non è presente alcuna area configurata, AEM torna indietro all&#39;area master per questo marchio specifico.

Il diagramma seguente è un esempio di come funziona la logica per tre siti, denominati site1, site2 e site3.

![Struttura multisito tra siti](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1 cerca myarea1 per brand1 e otherarea2 per brand2 in base alla mappatura dell&#39;area.
* site2 cerca myarea1 per brand1 e l&#39;area master per brand2 perché è definita solo la mappatura dell&#39;area per brand1.
* site3 cerca l&#39;area master per brand1 e brand2 in quanto nessun&#39;altra area di mappatura è definita per questo sito.
