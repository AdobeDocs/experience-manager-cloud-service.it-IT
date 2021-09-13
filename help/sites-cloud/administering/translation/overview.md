---
title: Traduzione di contenuti per siti multilingue
description: Ottieni una panoramica delle modalità di traduzione dei contenuti per siti multilingue.
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Traduzione di contenuti per siti multilingue {#translating-content-for-multilingual-sites}

Automatizza la traduzione di contenuti e risorse della pagina per creare e gestire siti web multilingue. Per automatizzare i flussi di lavoro di traduzione, è possibile integrare fornitori di servizi di traduzione con AEM e creare progetti per la traduzione dei contenuti in più lingue. AEM supporta flussi di lavoro di traduzione umana e automatica.

* **Traduzione umana:** il contenuto viene inviato al tuo fornitore di traduzioni e tradotto da traduttori professionisti. Una volta completato, il contenuto tradotto viene restituito e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.
* **Traduzione automatica:** il servizio di traduzione automatica traduce immediatamente il tuo contenuto.

>[!TIP]
>
>Se non hai esperienza nella traduzione dei contenuti, consulta il nostro [Percorso di traduzione dei siti,](/help/journey-sites/translation/overview.md) che è un percorso guidato attraverso la traduzione dei contenuti AEM Sites tramite i potenti strumenti di traduzione di AEM, ideale per chi non ha esperienza di AEM o traduzione.

La conversione del contenuto prevede i seguenti passaggi:

1. [Collega AEM al tuo ](integration-framework.md#connecting-to-a-translation-service-provider) provider di servizi di traduzione e  [crea configurazioni](integration-framework.md) del framework di integrazione della traduzione.
1. [Associa le pagine del tuo ](integration-framework.md#configuring-pages-for-translation) masterizzatore di linguaggio alle configurazioni del servizio di traduzione e del framework.
1. [Identifica il tipo di ](rules.md) contenuto da tradurre.
1. [Prepara il contenuto per la ](preparation.md) traduzione creando il master lingua e le pagine principali delle copie della lingua.
1. [Crea progetti di traduzione per ](managing-projects.md) raccogliere i contenuti da tradurre e preparare il processo di traduzione.
1. Utilizza i progetti di traduzione per [gestire il processo di traduzione dei contenuti](managing-projects.md).

Se il provider di servizi di traduzione non fornisce un connettore per l’integrazione con AEM, AEM supporta l’estrazione e il reinserimento manuali del contenuto di traduzione in formato XML.

>[!NOTE]
>
>Per utilizzare le funzioni Copia lingua, l’utente deve essere membro del gruppo `project-administrators` .

## Best practice   {#best-practices}

La pagina [Best practice per la traduzione](best-practices.md) contiene informazioni importanti sull’implementazione.
