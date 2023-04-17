---
title: Panoramica dei test di Cloud Manager
description: Ottieni una panoramica dei tre tipi di test eseguiti automaticamente da Cloud Manager per garantire la qualità del codice personalizzato.
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: 94f818b7622e0f878d15ba30e2f07a169bd114c3
workflow-type: ht
source-wordcount: '164'
ht-degree: 100%

---


# Panoramica dei test di Cloud Manager {#overview}

Cloud Manager supporta tre categorie di test per le pipeline di Cloud Service.

1. [Test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md)

   * Il test di qualità del codice valuta la qualità del codice dell’applicazione.
   * La pipeline di qualità del codice viene eseguita immediatamente dopo la fase di build in tutte le pipeline non di produzione e di produzione.
   * Le [regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md) eseguite da Cloud Manager vengono create in base alle best practice indicate dal team ingegneristico di AEM.

1. [Test funzionali](/help/implementing/cloud-manager/functional-testing.md)

   * Il test funzionale fa parte della fase di test nell’ambiente di staging di una [pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) ed eventualmente fa parte della fase di test di una [pipeline non di produzione.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

1. [Test dell’audit dell’esperienza](/help/implementing/cloud-manager/experience-audit-testing.md)

   * I test dell’audit dell’esperienza sono abilitati in tutte le pipeline di produzione di Cloud Manager e non possono essere ignorati.

I test possono essere:

* Scritti dal cliente
* Scritti da Adobe
* Creati con strumenti open source

>[!NOTE]
>
> I test scritti dal cliente e da Adobe vengono eseguiti in un’infrastruttura in contenitori progettata per l’esecuzione di tali test.
