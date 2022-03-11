---
title: Manutenzione di un connettore AEM
description: Manutenzione di un connettore AEM
exl-id: 8122a8c8-6577-4907-8f6e-52711eed3970
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 20%

---

Manutenzione di un connettore AEM
============================

Questo articolo contiene informazioni sulla gestione di un connettore AEM e deve essere letto insieme agli altri relativi all’[implementazione](implement.md) e all’[invio](submit.md) di connettori.

Anche dopo l’invio iniziale, possono esserci motivi per cui un partner deve aggiornare il proprio connettore AEM, a causa di una nuova versione di AEM o indipendente da essa - ad esempio, per aggiungere funzionalità o per correggere bug. Questo articolo illustra il processo per entrambi gli scenari e descrive anche il processo tipico di un cliente per la convalida dei connettori durante l’aggiornamento dei AEM.

AEM applicazioni as a Cloud Service vengono aggiornate con patch di manutenzione AEM su base giornaliera, con modifiche più grandi attivate su base mensile durante il rilascio di una funzione. Sebbene gli aggiornamenti AEM siano destinati a essere compatibili con le versioni precedenti e quindi non interrompere le applicazioni, ai partner fornitori viene consigliato di verificare regolarmente che i connettori si comportino come previsto. L&#39;accesso a un programma/ambiente AEM sarà determinato dal team partner.
