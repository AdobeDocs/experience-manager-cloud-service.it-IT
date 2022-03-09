---
title: Panoramica dei test di Cloud Manager
description: Ottieni una panoramica dei tre tipi di test eseguiti automaticamente da Cloud Manager per garantire la qualità del codice personalizzato.
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 5%

---


# Panoramica dei test di Cloud Manager {#overview}

Cloud Manager supporta tre categorie di test per le pipeline dei Cloud Services.

1. [Test della qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md)

   * Il test della qualità del codice valuta la qualità del codice dell’applicazione.
   * La pipeline di qualità del codice viene eseguita immediatamente dopo il passaggio di compilazione in tutte le pipeline non di produzione e di produzione.
   * La [regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md) le esecuzioni di Cloud Manager vengono create in base alle best practice di AEM Engineering.

1. [Test funzionale](/help/implementing/cloud-manager/functional-testing.md)

   * Il test funzionale è una parte della fase di test della fase di una pipeline di produzione.

1. [Test di Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md)

   * Il test del controllo di audit di esperienza è abilitato in tutte le pipeline di produzione di Cloud Manager e non può essere ignorato.

Questi test possono essere:

* Scritto dal cliente
* scritto in Adobe
* Creato con strumenti open source

>[!NOTE]
>
> I test scritti dai clienti e i test scritti in Adobe vengono eseguiti in un&#39;infrastruttura containerizzata progettata per l&#39;esecuzione di tali test.
