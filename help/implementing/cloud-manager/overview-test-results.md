---
title: Panoramica sui risultati del test - Cloud Services
description: Panoramica sui risultati del test - Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 16%

---


# Panoramica {#overview}

Le esecuzioni della pipeline di Cloud Manager per Cloud Services supportano l’esecuzione di test sull’ambiente stage. Ciò è in contrasto con i test eseguiti durante il passaggio Build e Unit Testing che vengono eseguiti offline, senza l&#39;accesso ad alcun ambiente AEM in esecuzione.

Sono disponibili tre grandi categorie di test supportati da Cloud Manager per pipeline di Cloud Services:

1. [Verifica della qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md)
1. [Test funzionale](/help/implementing/cloud-manager/functional-testing.md)
1. [Verifica del contenuto](/help/implementing/cloud-manager/content-audit-testing.md)

Questi test possono essere:

* Scritto dal cliente
*  scritto in Adobe
* Strumento open source (alimentato da faro di Google)

   >[!NOTE]
   > Sia i test scritti dal cliente che  test scritti dal Adobe vengono eseguiti in un&#39;infrastruttura containerizzata progettata per eseguire questi tipi di test.

