---
title: Verifica dello stato del record DNS
description: Scopri come determinare se la risoluzione delle impostazioni DNS avviene in modo corretto con Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 96%

---

# Verifica dello stato del record DNS {#check-dns-record-status}

Cloud Manager consente di determinare se la risoluzione del nome di dominio avviene in modo corretto nel sito web di AEM as a Cloud Service.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Fai clic su **Impostazioni dominio** nel pannello di navigazione a sinistra.

1. Fai clic sull’icona **Stato** del nome di dominio.

Cloud Manager esegue una ricerca DNS per il nome di dominio e visualizza uno dei seguenti messaggi di stato.

* **Stato DNS non rilevato**: lo stato del DNS non viene rilevato fino alla completa verifica e distribuzione del nome di dominio personalizzato.

   * Questo stato viene riscontrato anche quando è in corso il processo di eliminazione del nome di dominio personalizzato.

* **Risoluzione DNS errata**: indica che la risoluzione della configurazione dei record DNS non è avvenuta o è errata.

   * Consulta [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) per ulteriori informazioni.
   * Al termine dell’operazione, seleziona l’icona **Nuovo tentativo di risoluzione** accanto allo stato.

* **Risoluzione DNS in corso**: indica che la risoluzione è in corso.

   * In genere questo stato viene visualizzato dopo aver selezionato l’icona **Nuovo tentativo di risoluzione** accanto allo stato.

* **Risoluzione DNS corretta**: le impostazioni DNS sono configurate correttamente.

   * Il sito è disponibile per i visitatori e le visitatrici.

Cloud Manager attiva automaticamente una ricerca DNS quando il nome di dominio personalizzato viene verificato e distribuito correttamente per la prima volta. Per i tentativi successivi, seleziona attivamente l’icona **Nuovo tentativo di risoluzione** accanto allo stato.
