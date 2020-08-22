---
title: Modifiche di rilievo apportate ad AEM Commerce as a Cloud Service
description: Modifiche di rilievo apportate ad AEM Commerce as a Cloud Service rispetto ad Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 5a90db8791dd92cceb811b9ed2beda3ecb4a974d
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 100%

---


# Modifiche di rilievo apportate ad AEM Commerce as a Cloud Service {#notable-changes}

Adobe Experience Manager as a Cloud Service offre nuove funzionalità e possibilità per gestire i progetti AEM. Questo documento evidenzia le differenze di rilievo per le funzionalità Commerce tra Commerce Integration Framework (CIF) per on-premise, Adobe Managed Service ed Experience Manager as a Cloud Service. Per altre modifiche, consulta le [modifiche generiche di Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Le principali differenze rispetto a Experience Manager 6.5 riguardano i seguenti aspetti:
* [Supporto per CIF Classic](#cif-classic)
* [Implementazione degli strumenti CIF per l’authoring dei contenuti](#cif-tools)
* [Passaggio da on-premise e Adobe Managed Service](#moving-cif-cs)

## Supporto per CIF Classic/Quickstart su Experience Manager as a Cloud Service {#cif-classic}

Classic Commerce Integration Framework, che comprendeva un importatore di prodotti per importare e archiviare cataloghi di prodotti in Experience Manager, non è più disponibile in Experience Manager as a Cloud Service. L’utilizzo di Classic CIF non è supportato da Experience Manager as a Cloud Service e nei progetti basati su Classic CIF è necessario sostituire l’implementazione Classic CIF con la versione supportata, come descritto in [CIF in Experience Manager as a Cloud Service](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/cif/help/commerce-cloud/architecture.md).

## Implementazione di CIF {#deployment}

Di seguito sono riportati i diversi modelli di implementazione di Commerce Integration Framework per le diverse offerte di AEM:

|  | AEM on-premise | AEM Managed Services | AEM Cloud Service |
|-------------     |-----------|-----------|-----------|
| Come implementare gli strumenti CIF per l’authoring di contenuti per il back-end di Magento | [Fai riferimento al connettore CIF](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) supportato in AEM 6.5 | [Fai riferimento al connettore CIF](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) supportato in AEM 6.5 | AEM as a Cloud Service deve essere fornito con il componente aggiuntivo CIF. Per maggiori informazioni, contatta il tuo rappresentante commerciale |
| Come implementare [CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) | Pacchetto di installazione di AEM | Implementazione eseguita tramite [Cloud Manager](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) | Il progetto è stato spostato nell’[archivio Git di Cloud Manager Git](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) e implementato tramite [Cloud Manager](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/deploying/overview.html) |

>[!NOTE]
>
>La versione CIF Classic/Quickstart di Commerce Integration Framework può essere utilizzata nell’offerta on-premise di AEM per casi di utilizzo molto limitati. Tuttavia, questa non è la soluzione consigliata.

## Passaggio ad AEM Commerce as a Cloud Service da on-premise e Managed Services {#moving-cif-cs}

I clienti che passano da un’installazione AEM on-premise o Managed Services ad AEM as a Cloud Service devono effettuare alcune piccole regolazioni del progetto AEM.

La prima regolazione, come descritto sopra, è necessaria per il connettore CIF. Il connettore CIF è sostituito dal componente aggiuntivo CIF, distribuito da Adobe. Pertanto, non installare il connettore CIF in AEM as a Cloud Service. Inoltre, l’utilizzo con l’SDK di AEM Cloud locale non è supportato, Adobe fornisce il componente aggiuntivo CIF anche per lo [sviluppo locale](develop.md).

In secondo luogo, occorre comprendere la [struttura del progetto AEM ](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) e le caratteristiche di AEM as a Cloud Service. Adatta la configurazione del progetto al layout di AEM as a Cloud Service.
Le principali differenze sono:

* Il bundle OSGI client GraphQL **non deve** più essere incluso nel progetto AEM, ma viene distribuito tramite il componente aggiuntivo CIF.
* Le configurazioni OSGI per il client GraphQL e Graphql Data Service **non devono** più essere incluse nel progetto AEM.

>[!TIP]
>
>Controlla il progetto [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) su GitHub. Questo progetto fornisce profili Maven per implementazioni AEM as a Cloud Service e on-premise che tengono conto delle diverse condizioni di framework.
