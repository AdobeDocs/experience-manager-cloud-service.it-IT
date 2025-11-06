---
title: Utilizzo di frammenti di contenuto con Adobe Journey Optimizer
description: Scopri come i frammenti di contenuto possono essere integrati e utilizzati con Adobe Journey Optimizer.
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: 4090ee41-80f1-4389-8961-e4af891f01ff
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 10%

---

# Frammenti di contenuto con Adobe Journey Optimizer {#content-fragments-with-journey-optimizer}

[Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started) ti aiuta a fornire ai tuoi clienti esperienze connesse, contestuali e personalizzate. Integrando Adobe Experience Manager (AEM) as a Cloud Service con Adobe Journey Optimizer (AJO), puoi riutilizzare i contenuti AEM nei canali in entrata AJO e nei canali in uscita AJO, inclusi web, SMS, e-mail e altri.

Ad esempio:

* incorpora perfettamente i [frammenti di contenuto AEM](/help/sites-cloud/administering/content-fragments/overview.md) nel contenuto di [e-mail Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/email-landing-page)
* visualizzare l’anteprima dell’esperienza AJO direttamente da AEM

La connessione tra Frammenti di contenuto e AJO semplifica il processo di accesso e utilizzo dei contenuti di AEM, consentendo la creazione di campagne e percorsi personalizzati e dinamici.

Per informazioni dettagliate, inizia con la documentazione di AJO:

* [Utilizzo di frammenti di contenuto in AJO](https://experienceleague.adobe.com/docs/journey-optimizer/using/integrations/aem-fragments.html#integrations)
* [Offerte di integrazione AJO con frammento di contenuto](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/managing-offers-in-the-offer-library/configure-offers/add-representations#urls)

## Configurazione Dispatcher {#dispatcher-configuration}

Per consentire ad AJO di accedere ai frammenti di contenuto di AEM tramite l&#39;[API di gestione dei frammenti di contenuto](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/), devi configurare Dispatcher:

* In `dispatcher/src/conf.dispatcher.d/filters/filters.any`:

* Aggiungi:

  ```xml
  # Allow Content Fragments API requests, required for integration with AJO 
  /200 {/type "allow" /url "/adobe/sites/cf/*" }
  ```

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consulta:

* L&#39;estensione [AJO External References](/help/sites-cloud/administering/content-fragments/extension-content-fragment-ajo-external-references.md)
