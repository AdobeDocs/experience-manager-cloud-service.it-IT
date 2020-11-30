---
title: Manutenzione di un connettore AEM
description: Manutenzione di un connettore AEM
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 20%

---


Manutenzione di un connettore AEM
============================

Questo articolo contiene informazioni sulla gestione di un connettore AEM e deve essere letto insieme agli altri relativi all’[implementazione](implement.md) e all’[invio](submit.md) di connettori.

Anche dopo l&#39;invio iniziale, potrebbero essere presenti motivi per cui un partner possa aggiornare il proprio connettore AEM, a causa di una nuova release di AEM o indipendente da tale operazione, ad esempio per aggiungere funzioni o correggere bug. Questo articolo descrive il processo per entrambi gli scenari e descrive anche il processo tipico di un cliente per la convalida dei connettori durante l&#39;aggiornamento dei AEM.

AEM come applicazioni di Cloud Service vengono aggiornate con AEM patch di manutenzione su base giornaliera, con modifiche maggiori attivate su base mensile durante il rilascio di una funzione. Sebbene AEM aggiornamenti siano destinati a essere compatibili con le versioni precedenti e quindi non interrompere le applicazioni, i partner fornitore sono invitati a convalidare regolarmente il funzionamento dei connettori come previsto. L&#39;accesso a un programma/ambiente AEM sarà determinato dal team partner.