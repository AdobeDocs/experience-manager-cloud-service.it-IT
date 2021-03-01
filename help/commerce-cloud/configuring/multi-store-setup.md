---
title: Configurazione di più store
description: Scopri come mappare più viste store da Magento ad AEM. Questo consente ai progetti di supportare casi d’uso multi-tenant e multilingue.
sub-product: Commerce
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
translation-type: tm+mt
source-git-commit: 95ac5e5f6c49d5a2d7aef5dcf30d8298fd459457
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 91%

---


# Configurazione di più store {#multi-store}

I componenti core CIF di AEM possono essere utilizzati su più strutture di siti AEM e l’implementazione client GraphQL sottostante può connettersi a diversi store o viste store di Magento. Ciò consente ai progetti di implementare complesse impostazioni per più store o siti.

Una procedura video dettagliata che illustra le opzioni di integrazione di più visualizzazioni store di Magento con Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Le funzioni Live Copy e Copia per lingua di AEM per la gestione di più siti sono utilizzate insieme a Commerce Integration Framework (CIF) per gestire globalmente i siti per diverse aree geografiche e lingue.

Si consiglia di utilizzare una relazione 1:1 tra AEM Sites e la vista Store di Magento.

Per collegare un sito AEM e i componenti core CIF di AEM a una visualizzazione dedicata dello store, procedi come segue:

## Configurazione {#configuration}

1. Configura più store e viste Store in base al pattern descritto in [Magento Websites, Stores &amp; Views](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html) (Siti web, store e viste di Magento).

2. Assicurati che la connessione tra AEM e Magento funzioni.

3. Crea una configurazione figlio della configurazione di Cloud Service CIF:

   * In AEM vai a Strumenti -> Generale -> [Browser di configurazione](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * Seleziona la configurazione di base creata.
   * Crea una nuova configurazione seguendo i passaggi descritti al punto 2 precedente.

   Questa nuova configurazione verrà creata come configurazione secondaria di quella di base. Ora passa a Strumenti > Generale > Browser di configurazione e crea le impostazioni di configurazione.

4. Assegnare la configurazione figlio a un sito AEM

   * Passa alla console di AEM Sites.
   * Passa alla directory principale dell’area geografica o della lingua della struttura del sito; ad esempio, per la pagina di esempio di Venia: /content/venia/us _oppure_ /content/venia/us/it
   * Seleziona la pagina e apri le proprietà della pagina.
   * Seleziona la scheda Avanzate.
   * Nella sezione `Configuration`, seleziona la configurazione creata al passaggio

## Risorse aggiuntive

* [Magento Website, Stores e Views](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [Componenti core CIF di AEM: configurazione di più store o siti](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Utilizzo di Multi-Site Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Riutilizzo del contenuto: Multi-Site Manager e Live Copy](/help/sites-cloud/administering/msm/overview.md)
