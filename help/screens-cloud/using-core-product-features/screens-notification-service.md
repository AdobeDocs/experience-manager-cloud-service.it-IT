---
title: Servizio di notifica Screens in Screens as a Cloud Service
description: Questa pagina descrive come configurare il servizio di notifica in Screens as a Cloud Service.
index: true
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 4%

---


# Servizio di notifica Screens {#notification-service}

## Introduzione {#introduction}

### Panoramica

Il servizio AEM Screens Notifications consente agli amministratori di ricevere un’e-mail se un lettore AEM screens non esegue il ping per un periodo di tempo configurabile.

### Come configurare

In AEM Screens Cloud, i clienti possono richiedere avvisi sullo stato di inattività del dispositivo creando un ticket di supporto con le seguenti informazioni:

* Nome cliente
* ID organizzazione IMS
* Frequenza pianificazione: specifica un’ora o una frequenza in ore (ad esempio, 1) in cui il monitoraggio deve inviare le e-mail.
* Timeout ping: specifica l&#39;intervallo in minuti dopo il quale un dispositivo deve essere considerato non raggiungibile.
* ID e-mail: ID e-mail a cui verrà inviato il report