---
title: Servizio di notifica Screens in Screens as a Cloud Service
description: Questa pagina descrive come configurare il servizio di notifica in Screens as a Cloud Service.
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
source-git-commit: 69798b1ac3758d37c4e2f480ccc23bae24d6a814
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 4%

---

# Servizio di notifica Screens {#notification-service}

## Introduzione {#introduction}

### Panoramica

Il servizio AEM Screens Notifications consente agli amministratori di ricevere un rapporto con un elenco di tutti i lettori AEM Screens che non hanno eseguito il ping per un periodo di tempo configurabile su un’e-mail.

### Come configurare

Su AEM Screens Cloud, i clienti possono richiedere un rapporto sullo stato di inattività del dispositivo creando un ticket di supporto con le seguenti informazioni:

* Nome cliente
* ID organizzazione IMS
* Frequenza pianificazione: specifica un’ora o una frequenza in ore (ad esempio, 1) in cui il monitoraggio deve inviare le e-mail.
* Timeout ping: specifica l&#39;intervallo in minuti dopo il quale un dispositivo deve essere considerato non raggiungibile.
* ID e-mail: ID e-mail a cui verrà inviato il report

>[!NOTE]
>Le e-mail faranno sì che il lettore venga segnalato solo se il dispositivo che non ha eseguito il ping per il timeout di ping specificato al momento della generazione dell’e-mail.

### Caso d’uso di esempio

Se imposti l’ora del rapporto sulle 5 e il timeout del ping su 1 ora, se il dispositivo Screens non esegue il ping tra le 4:00 e le 5:00, riceverai una notifica e-mail di conferma dell’inattività del dispositivo.
