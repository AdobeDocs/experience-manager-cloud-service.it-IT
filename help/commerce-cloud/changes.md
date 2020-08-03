---
title: Notevoli modifiche a AEM Commerce come Cloud Service
description: Notevoli modifiche AEM Commerce come Cloud Service rispetto a  Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: df6f679b70a7cc70e4f76612c0a72a31443cd1b8
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 6%

---


# Notable changes to AEM Commerce as a Cloud Service {#notable-changes}

 Adobe Experience Manager come Cloud Service offre molte nuove funzionalità e possibilità per gestire i progetti AEM. Questo documento evidenzia le importanti differenze per le funzionalità Commerce tra Commerce Integration Framework (CIF) per i servizi gestiti in sede,  Adobe e  Experience Manager come Cloud Service. Per altre modifiche, consultate le [modifiche generiche al Experience Manager  come Cloud Service](/help/release-notes/aem-cloud-changes.md).

Le principali differenze rispetto  Experience Manager 6.5 riguardano i seguenti settori:
* [Supporto per CIF Classic](#cif-classic)
* [Distribuzione di strumenti di authoring CIF](#cif-tools)
* [Passaggio da un servizio gestito locale e  Adobe](#moving-cif-cs)

## Supporto per CIF Classic/Quickstart su  Experience Manager come Cloud Service {#cif-classic}

Classic Commerce Integration Framework, che comprendeva un Importatore di prodotti per importare e archiviare cataloghi di prodotti in  Experience Manager, non è più disponibile  Experience Manager come Cloud Service. L&#39;utilizzo di Classic CIF non è supportato  Experience Manager come Cloud Service e i progetti che utilizzano Classic CIF dovranno sostituire l&#39;implementazione Classic CIF con la versione supportata, come descritto in [CIF su Experience Manager Cloud Service come](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/cif/help/commerce-cloud/architecture.md)

## Distribuzione di CIF {#deployment}

Di seguito sono riportati i diversi modelli di implementazione di Commerce Integration Framework per le diverse offerte di AEM:

|  | AEM locale | AEM Managed Services | Cloud Service AEM |
|-------------     |-----------|-----------|-----------|
| Come implementare gli strumenti di authoring CIF per il back-end Magento | [Fare riferimento al connettore](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) CIF supportato su AEM 6.5 | [Fare riferimento al connettore](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) CIF supportato su AEM 6.5 | AEM come Cloud Service deve essere fornito con il componente aggiuntivo CIF. Per maggiori informazioni, contattate il vostro rappresentante commerciale |
| Come implementare il progetto [CIF Venia](https://github.com/adobe/aem-cif-guides-venia) | AEM pacchetto di installazione | Distribuzione eseguita tramite [Cloud Manager](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) | Il progetto è stato spostato nell&#39;archivio [Git di](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) Cloud Manager e implementato tramite [Cloud Manager](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/deploying/overview.html) |

>[!Note]
>
>CIF la versione Classic/Quickstart di Commerce Integration Framework può essere utilizzata AEM offerta locale per casi di utilizzo molto limitati. Tuttavia, questa non è la soluzione consigliata.

## Passaggio a AEM Commerce come Cloud Service da On-premise e Managed Services {#moving-cif-cs}

I clienti che si spostano da un&#39;installazione AEM locale o Managed Services a AEM come Cloud Service devono effettuare alcuni piccoli aggiustamenti sul progetto AEM.

La prima regolazione, come descritto sopra, è necessaria per il connettore CIF. Il connettore CIF è sostituito dal componente aggiuntivo CIF distribuito dal Adobe . Pertanto, non installate il connettore CIF su AEM come Cloud Service. Inoltre, l’utilizzo con l’SDK AEM Cloud locale non è supportato,  Adobe fornisce il componente aggiuntivo CIF anche per lo sviluppo [](develop.md)locale.

In secondo luogo, comprendere la [AEM struttura](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) del progetto e le caratteristiche di AEM come Cloud Service. Adattare la configurazione del progetto al AEM come layout di Cloud Service.
Le principali differenze sono:

* Il bundle OSGI client GraphQL non **deve più** essere incluso nel progetto AEM, viene distribuito tramite il componente aggiuntivo CIF
* Le configurazioni OSGI per il client GraphQL e il servizio di dati grafico non **devono più** essere incluse nel progetto AEM

>[!Tip]
>
>Scopri il progetto [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) su GitHub. Questo progetto fornisce profili Maven per AEM come Cloud Service e distribuzioni locali che tengono conto delle diverse condizioni quadro.
