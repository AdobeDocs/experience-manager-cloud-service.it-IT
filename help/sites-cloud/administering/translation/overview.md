---
title: Traduzione di contenuti per siti multilingue
description: Ottieni una panoramica delle modalità di traduzione dei contenuti per siti multilingue.
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 82%

---

# Traduzione di contenuti per siti multilingue {#translating-content-for-multilingual-sites}

Automatizza la traduzione di contenuti e risorse della pagina per creare e gestire siti Web multilingue. Per automatizzare i flussi di lavoro di traduzione, puoi integrare fornitori di servizi di traduzione con AEM e creare progetti per la traduzione dei contenuti in più lingue. AEM supporta flussi di lavoro di traduzione umana e automatica.

* **Traduzione umana:** il contenuto viene inviato al tuo provider di traduzioni e tradotto da professionisti. Una volta completato, il contenuto tradotto viene rinviato e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.
* **Traduzione automatica:** il servizio di traduzione automatica traduce immediatamente il contenuto.

>[!TIP]
>
>Se non hai ancora tradotto i contenuti, consulta [Percorso di traduzione siti](/help/journey-sites/translation/overview.md), per una guida attraverso la traduzione dei contenuti AEM Sites tramite i potenti strumenti di traduzione dell&#39;AEM, ideali per chi non ha esperienza di AEM o traduzione.

La traduzione del contenuto prevede i seguenti passaggi:

1. [Connetti AEM con il provider di servizi di traduzione](integration-framework.md#connecting-to-a-translation-service-provider) e [crea configurazioni del Translation Integration Framework](integration-framework.md).
1. [Associa le pagine della lingua master](integration-framework.md#configuring-pages-for-translation) con il servizio di traduzione e le configurazioni del framework.
1. [Identifica il tipo di contenuto](rules.md) da tradurre.
1. [Prepara il contenuto per la traduzione](preparation.md) creando la lingua master e le pagine root delle copie in lingua.
1. [Crea progetti di traduzione](managing-projects.md) per raccogliere il contenuto da tradurre e preparare il processo di traduzione.
1. Utilizza i progetti di traduzione per [gestire il processo di traduzione dei contenuti](managing-projects.md).

Se il provider di servizi di traduzione non fornisce un connettore per l’integrazione con AEM, AEM supporta l’estrazione e il reinserimento manuali del contenuto di traduzione in formato XML.

>[!NOTE]
>
>L&#39;utente deve essere membro del gruppo `project-administrators` per utilizzare le funzionalità Copia in lingua.

## Best practice   {#best-practices}

La pagina [Best practice per la traduzione](best-practices.md) contiene informazioni importanti sull’implementazione.
