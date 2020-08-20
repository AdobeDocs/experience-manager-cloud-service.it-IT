---
title: Panoramica sui risultati del test - Cloud Services
description: Panoramica sui risultati del test - Cloud Services
translation-type: tm+mt
source-git-commit: b3548e3920fed45f6d1de54a49801d3971aa6bba
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Panoramica {#overview}

Sono disponibili tre grandi categorie di test supportati da Cloud Manager per pipeline di Cloud Services:

1. [Verifica della qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md)

   Il test della qualità del codice valuta la qualità del codice dell’applicazione. La pipeline Code-Quality viene eseguita immediatamente dopo la fase di creazione in tutti i gasdotti non di produzione e produzione.

   Le regole [di qualità del codice](/help/implementing/cloud-manager/custom-code-quality-rules.md) personalizzate eseguite da Cloud Manager vengono create in base alle best practice AEM Engineering.

1. [Test funzionale](/help/implementing/cloud-manager/functional-testing.md)

   Il test funzionale fa parte della fase di test di una tubazione di produzione.

1. [Verifica del contenuto](/help/implementing/cloud-manager/content-audit-testing.md)

   Il controllo dei contenuti è abilitato in tutte le pipeline di produzione di Cloud Manager e non può essere ignorato.

Questi test possono essere:

* Scritto dal cliente
*  scritto in Adobe
* Open source, strumento

   >[!NOTE]
   > Sia i test scritti dal cliente che  test scritti dal Adobe vengono eseguiti in un&#39;infrastruttura containerizzata progettata per eseguire questi tipi di test.

