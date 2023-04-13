---
title: Note sulla versione 2023.4.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2023.4.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: be39b09b609cccff916db462af9a84149d23a698
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 50%

---


# Note sulla versione 2023.4.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.4.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di rilascio della versione 2023.4.0 di Cloud Manager in AEM as a Cloud Service è il 13 aprile 2023. La prossima versione è prevista per il 11 maggio 2023.

## Novità {#what-is-new}

* [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) è stato aggiornato alla versione 41.

## Correzioni di bug {#bug-fixes}

* Quando un [certificato](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) scade, [nomi di dominio](/help/implementing/cloud-manager/custom-domain-names/introduction.md) e [ELENCHI CONSENTITI IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) associato al certificato non verrà più rimosso dalla rete CDN.  In questi casi, il sito continuerà ad essere raggiungibile.
* L’interfaccia utente di Cloud Manager fornisce avvisi anticipati più visibili relativi al [Certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) sta per scadere.
* È stata corretta una situazione rara in cui i clienti non potevano creare un nuovo ambiente o eliminare un ambiente.
