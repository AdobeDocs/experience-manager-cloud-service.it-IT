---
title: Configurazione multi-store
description: Configurazione multi-store
translation-type: tm+mt
source-git-commit: 94c6abef36b6add300ba3b24855ebf3edf10e1ed
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# Configurazione multi-store {#multi-store}

I componenti core CIF AEM possono essere utilizzati su più strutture AEM sito e l&#39;implementazione client GraphQL sottostante può connettersi a diversi store Magenti/viste store. Questo consente ai progetti di implementare complesse impostazioni multi-store/multisito.

Una procedura dettagliata per i video che illustra le opzioni di integrazione di più visualizzazioni store Magenti con  Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

AEM funzioni di gestione multisito di Live Copy e di Language Copy sono utilizzate insieme a Commerce Integration Framework per gestire globalmente i siti tra le diverse aree geografiche e lingue.

Si consiglia di utilizzare una relazione 1:1 tra AEM visualizzazione del sito e dell&#39;archivio Magenti.

Per collegare un sito AEM e i componenti AEM CIF di base così come a una visualizzazione dedicata dello store, procedere come segue:

## Configurazione {#configuration}

1. Configurare più store e visualizzazioni store in base al pattern descritto in [Magento Siti Web, Negozi e Viste](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. Assicuratevi che la connessione tra AEM e Magento funzioni.

3. Create una configurazione figlio della configurazione del Cloud Service CIF seguendo la procedura seguente:

   * In AEM andare a Strumenti -> Generale -> Browser di configurazione
   * Seleziona la configurazione di base creata
   * Creare una nuova configurazione utilizzando i passaggi descritti al punto 2 precedente

   Questa nuova configurazione verrà creata come configurazione secondaria della base. È ora possibile accedere a Strumenti > Generali > Browser di configurazione e creare le impostazioni di configurazione.

4. Assegnazione della configurazione figlio a un sito AEM

   * Vai alla console AEM Sites
   * Andate alla directory principale della regione o della lingua della struttura del sito, ad esempio /content/venia/us _o_ /content/venia/us/it per la pagina di esempio di Venia
   * Selezionare la pagina e aprire le proprietà
   * Selezionate la scheda Avanzate
   * Nella `Configuration` sezione selezionare la configurazione creata al passaggio

## Risorse aggiuntive

* [Magento Siti Web, Negozi e Viste](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF Componenti di base - Configurazione multischermo/sito](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Utilizzo di Gestione multisito](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Riutilizzo del contenuto: Multi Site Manager e Live Copy](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/msm.html)
