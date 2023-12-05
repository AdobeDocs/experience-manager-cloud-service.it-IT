---
title: Configurazione di più store di Commerce
description: Scopri come mappare più visualizzazioni dello store da Adobe Commerce a Adobe Experience Manager. Questo consente ai progetti di supportare casi d’uso multi-tenant e multilingue.
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 15%

---

# Configurazione di più store di Commerce {#multi-store}

I componenti core CIF di Adobe Experience Manager (AEM) possono essere utilizzati su più strutture di siti AEM e l’implementazione client GraphQL sottostante può connettersi a diversi store o viste store di Adobe Commerce. Ciò consente ai progetti di implementare complesse impostazioni per più store o siti.

Una procedura video dettagliata che illustra le opzioni di integrazione di più visualizzazioni dello store di Adobe Commerce con Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Le funzioni di Live Copy e copia per lingua dell’AEM per la gestione multisito vengono utilizzate con Commerce Integration Framework per gestire globalmente i siti in aree geografiche e lingue diverse.

Si consiglia di utilizzare una relazione 1:1 tra il sito AEM e la vista Store di Adobe Commerce.

Per collegare un sito AEM e i componenti core CIF dell’AEM a una visualizzazione dedicata dello store, effettua le seguenti operazioni:

## Configurazione {#configuration}

1. Configura più store e viste store in base al pattern descritto in [Siti Web, store e visualizzazioni di Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)

2. Assicurati che la connessione tra AEM e Adobe Commerce funzioni.

3. Crea una configurazione figlio della configurazione di Cloud Service CIF:

   * In AEM vai a Strumenti > Generale > [Browser configurazioni](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * Seleziona la configurazione di base creata
   * Crea una configurazione seguendo i passaggi descritti al precedente punto 2

   Questa nuova configurazione viene creata come configurazione figlio di quella di base. Ora puoi passare a Strumenti > Generale > Browser configurazioni e creare le impostazioni di configurazione.

   >[!TIP]
   >
   > I cataloghi Commerce possono essere indirizzati utilizzando ID o UID. UID introdotti in Adobe Commerce 2.4.2. Abilita questa opzione solo se il backend di e-commerce supporta uno schema GraphQL della versione 2.4.2 o successiva.

4. Assegnare la configurazione figlio a un sito AEM

   * Passa alla console AEM Sites
   * Passa alla directory principale dell’area geografica o della lingua della struttura del sito. Ad esempio: `/content/venia/us _or_ /content/venia/us/en` per la pagina di esempio di Venia
   * Seleziona la pagina e apri le proprietà della pagina
   * Seleziona la scheda Avanzate.
   * In `Configuration` sezione, seleziona la configurazione creata al passaggio 3

## Risorse aggiuntive

* [Siti Web, store e visualizzazioni di Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)
* [Componenti core CIF di AEM: configurazione di più store o siti](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [Utilizzo di Multi-Site Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Riutilizzo del contenuto: Multi-Site Manager e Live Copy](/help/sites-cloud/administering/msm/overview.md)
