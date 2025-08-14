---
title: Configurare l’annullamento della validità push per un sito Edge Delivery
description: Scopri come configurare l’annullamento della validità push per un sito Edge Delivery, per gestire in modo efficace l’aggiornamento dei contenuti e la memorizzazione in cache.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 7cded93c-325c-4a4b-8644-e6a2379d5179
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 100%

---

# Configurare l’annullamento della validità push

L’annullamento della validità push assicura che, al momento della pubblicazione, gli aggiornamenti dei contenuti effettuati dagli autori vengano rimossi automaticamente dalla rete per la consegna dei contenuti (CDN) gestita. In questo modo verranno forniti solo i contenuti più recenti.

Il sistema cancella i contenuti in base a specifici URL e tag o chiavi della cache, in modo che vengano eliminate le versioni obsolete.

Per abilitare l’annullamento della validità push, è necessario aggiungere proprietà specifiche al file di configurazione del progetto. Ad esempio, una cartella di lavoro di Microsoft Excel denominata `.helix/config.xlsx` in SharePoint o un foglio di Google denominato `.helix/config` in Google Drive.

Le seguenti proprietà di configurazione definiscono il nome dell’host di produzione e il tipo di gestione CDN:

| chiave | valore | commento |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | Nome host del sito di produzione. Esempio: `www.example.com`. |
| `cdn.prod.type` | gestito |   |

Dopo aver apportato modifiche al foglio di configurazione, gli utenti devono visualizzarle in anteprima e attivarle con lo strumento [Sidekick](https://www.aem.live/docs/sidekick) per applicare gli aggiornamenti.

Consulta anche [Informazioni sull’elenco attività di Edge Delivery in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list).
