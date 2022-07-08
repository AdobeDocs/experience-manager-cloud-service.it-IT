---
title: Struttura della gestione multisito per contenuti di destinazione
description: Un diagramma illustra il modo in cui è strutturato il supporto multisito per contenuti di destinazione
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '181'
ht-degree: 100%

---

# Struttura della gestione multisito per contenuti di destinazione {#how-multisite-management-for-targeted-content-is-structured}

Il diagramma seguente illustra il modo in cui è strutturato il supporto multisito per contenuti di destinazione.

Le aree vengono visualizzate al di sotto di **/content/campaigns/&lt;brand>** e, per impostazione predefinita, ogni marchio ha un’area master che viene creata automaticamente. Ogni area contiene la propria serie di attività, esperienze e offerte.

![Struttura multisito](/help/sites-cloud/authoring/assets/multisite-structure.png)

Per cercare contenuti di destinazione, le pagine o i siti possono essere associati a un&#39;area. Se non è presente alcuna area configurata, AEM torna indietro all&#39;area master per questo marchio specifico.

Il diagramma seguente è un esempio di come funziona la logica per tre siti, denominati site1, site2 e site3.

![Struttura multisito tra siti diversi](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1 cerca myarea1 per brand1 e otherarea2 per brand2 in base alla mappatura dell&#39;area.
* site2 cerca myarea1 per brand1 e l&#39;area master per brand2 perché è definita solo la mappatura dell&#39;area per brand1.
* site3 cerca l&#39;area master per brand1 e brand2 in quanto nessun&#39;altra area di mappatura è definita per questo sito.
