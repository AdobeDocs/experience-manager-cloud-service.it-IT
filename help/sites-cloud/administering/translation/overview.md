---
title: Traduzione di contenuti per siti multilingue
description: Ottieni una panoramica delle modalità di traduzione dei contenuti per siti multilingue.
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 4%

---

# Traduzione di contenuti per siti multilingue {#translating-content-for-multilingual-sites}

Automatizza la traduzione di contenuti e risorse della pagina per creare e gestire siti web multilingue. Per automatizzare i flussi di lavoro di traduzione, è possibile integrare fornitori di servizi di traduzione con AEM e creare progetti per la traduzione dei contenuti in più lingue. AEM supporta flussi di lavoro di traduzione umana e automatica.

* **Traduzione umana:** Il contenuto viene inviato al tuo provider di traduzioni e tradotto da traduttori professionisti. Una volta completato, il contenuto tradotto viene restituito e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.
* **Traduzione automatica:** Il servizio di traduzione automatica traduce immediatamente il contenuto.

>[!TIP]
>
>Se non hai ancora tradotto i contenuti, consulta la nostra [Percorso di traduzione dei siti,](/help/journey-sites/translation/overview.md) percorso guidato attraverso la traduzione dei contenuti AEM Sites tramite i potenti strumenti di traduzione di AEM, ideali per chi non ha esperienza di AEM o traduzione.

La conversione del contenuto prevede i seguenti passaggi:

1. [Connetti AEM con il provider di servizi di traduzione](integration-framework.md#connecting-to-a-translation-service-provider) e [creare configurazioni del framework di integrazione della traduzione](integration-framework.md).
1. [Associare le pagine del master lingua](integration-framework.md#configuring-pages-for-translation) con il servizio di traduzione e le configurazioni del framework.
1. [Identificare il tipo di contenuto](rules.md) di tradurre.
1. [Preparare il contenuto per la traduzione](preparation.md) creando il master lingua e le pagine principali delle copie per lingua.
1. [Creare progetti di traduzione](managing-projects.md) raccogliere il contenuto da tradurre e preparare il processo di traduzione.
1. Utilizzare i progetti di traduzione per [gestire il processo di traduzione dei contenuti](managing-projects.md).

Se il provider di servizi di traduzione non fornisce un connettore per l’integrazione con AEM, AEM supporta l’estrazione e il reinserimento manuali del contenuto di traduzione in formato XML.

>[!NOTE]
>
>Il tuo utente deve essere membro del `project-administrators` gruppo per utilizzare le funzioni Copia lingua.

## Best practice   {#best-practices}

La [Best practice per la traduzione](best-practices.md) contiene informazioni importanti sull’implementazione di .
