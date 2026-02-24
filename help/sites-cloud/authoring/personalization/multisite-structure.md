---
title: Struttura della gestione multisito per contenuti di destinazione
description: Un diagramma mostra come è strutturato il supporto multisito per contenuti mirati
badgeSaas: label="AEM Sites" type="Positive" tooltip="Si applica ad AEM Sites)."
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 39%

---

# Struttura della gestione multisito per contenuti di destinazione {#how-multisite-management-for-targeted-content-is-structured}

Il diagramma seguente mostra come è strutturato il supporto multisito per contenuti di destinazione.

Le aree vengono visualizzate al di sotto di **/content/campaigns/&lt;brand>** e, per impostazione predefinita, ogni marchio ha un’area master che viene creata automaticamente. Ogni area contiene la propria serie di attività, esperienze e offerte.

![Struttura multisito](/help/sites-cloud/authoring/assets/multisite-structure.png)

Per cercare contenuti mirati, le pagine o i siti possono essere mappati su un’area. Se non è configurata alcuna area, AEM torna all’area master per questo marchio specifico.

Il diagramma seguente è un esempio di come funziona la logica per tre siti, denominati site1, site2 e site3.

![Struttura multisito tra siti diversi](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1 cerca myarea1 per brand1 e otherarea2 per brand2 in base alla mappatura dell’area.
* site2 cerca myarea1 per brand1 e master area per brand2 in quanto viene definita solo la mappatura di area per brand1.
* site3 cerca l’area master per brand1 e brand2 in quanto per questo sito non è definita alcuna altra mappatura di area.
