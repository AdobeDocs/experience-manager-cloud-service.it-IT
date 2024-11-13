---
title: Imposta annullamento validità push
description: Scopri come configurare l’invalidazione push per creare una tua CDN di produzione.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 7cded93c-325c-4a4b-8644-e6a2379d5179
source-git-commit: 0ac6856e8f3e664fcc7e3c08faac4c4f5c16af18
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 2%

---

# Impostare l’annullamento della validità push

L’annullamento della validità push assicura che gli aggiornamenti di contenuto effettuati dagli autori vengano rimossi automaticamente dalla rete CDN (Content Delivery Network) gestita al momento della pubblicazione. In questo modo viene fornito solo il contenuto più recente.

Il sistema cancella il contenuto in base a URL specifici e memorizza nella cache tag o chiavi, garantendo l’eliminazione delle versioni obsolete.

Per abilitare l’invalidazione push, è necessario aggiungere proprietà specifiche al file di configurazione del progetto. Ad esempio, una cartella di lavoro di Microsoft Excel denominata `.helix/config.xlsx` in SharePoint o il nome di un foglio di Google `.helix/config` in Google Drive.

Le seguenti proprietà di configurazione definiscono il nome dell’host di produzione e il tipo di gestione CDN:

| chiave | valore | commento |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | Nome host del sito di produzione. Esempio: `www.example.com`. |
| `cdn.prod.type` | gestito |   |

Dopo aver apportato modifiche al foglio di configurazione, gli utenti devono visualizzarle in anteprima e attivarle con lo strumento [Sidekick](/help/edge/docs/sidekick.md) per applicare gli aggiornamenti.

Vedere anche [Informazioni sull&#39;elenco attività di Edge Delivery in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list).
