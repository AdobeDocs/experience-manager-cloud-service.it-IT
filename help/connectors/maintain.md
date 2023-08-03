---
title: Manutenzione di un connettore AEM
description: Scopri come aggiornare il connettore AEM dopo l’invio iniziale.
exl-id: 8122a8c8-6577-4907-8f6e-52711eed3970
source-git-commit: f7ffe727ecc7f1331c1c72229a5d7f940070c011
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 86%

---

Manutenzione di un connettore AEM
============================

Questo articolo contiene informazioni sulla gestione di un connettore AEM e deve essere letto insieme agli altri relativi all’[implementazione](implement.md) e all’[invio](submit.md) di connettori.

Anche dopo l’invio iniziale, possono esserci motivi per cui un partner deve aggiornare il proprio connettore AEM, a causa di una nuova versione di AEM o indipendentemente da essa, ad esempio, per aggiungere funzionalità o per correggere bug. Questo articolo illustra il processo per entrambi gli scenari e descrive anche il processo tipico di un cliente per la convalida dei connettori durante l’aggiornamento di AEM.

Le applicazioni AEM as a Cloud Service vengono aggiornate con patch di manutenzione AEM su base giornaliera, con modifiche più grandi attivate su base mensile durante il rilascio di una funzione. Sebbene gli aggiornamenti AEM siano destinati a essere compatibili con le versioni precedenti in modo da non interrompere le applicazioni, ai partner fornitori viene consigliato di verificare regolarmente che i connettori si comportino come previsto. L’accesso a un programma/ambiente AEM è determinato dal team partner.
