---
title: Note sulla versione 2023.6.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2023.6.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 35%

---


# Note sulla versione 2023.6.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.6.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager versione 2023.6.0 in AEM as a Cloud Service è l’8 giugno 2023. La prossima versione è prevista per il 6 luglio 2023.

## Novità {#what-is-new}

* I clienti possono acquistare altre aree geografiche di pubblicazione secondarie oltre all’area principale, con conseguenti vantaggi in termini di latenza ridotta e maggiore disponibilità. Nota: possono essere applicate alcune restrizioni.
* Durante la creazione di un nuovo [programma o ambiente,](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) il nome ora può contenere solo caratteri alfanumerici e un set limitato di caratteri speciali.
* Quando si riprende una [pipeline di produzione,](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) al passaggio di approvazione viene ora visualizzata una finestra di dialogo di conferma.
* Per **[Test funzionali del cliente](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)** e **[Test dell’interfaccia utente personalizzati](/help/implementing/cloud-manager/ui-testing.md)** passaggi della pipeline, un nuovo `INCOMPLETE` Lo stato è ora possibile, il che indica che tali test non erano presenti e quindi non sono stati eseguiti.
   * In questi casi, la pipeline non ha esito negativo e procede al passaggio successivo.

## Correzioni di bug {#bug-fixes}

* Il [pipeline di configurazione a livello web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) non sono più abilitati in modo errato per i programmi solo Assets.
* È stata aggiunta una convalida più solida per evitare alcuni tipi di errori durante il provisioning dell’ambiente.
