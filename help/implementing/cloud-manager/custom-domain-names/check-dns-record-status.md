---
title: Verifica dello stato del record DNS
description: Scopri come determinare se la risoluzione delle impostazioni DNS avviene in modo corretto con Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 06e961febd7cb2ea1d8fca00cb3dee7f7ca893c9
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 60%

---


# Verifica dello stato del record DNS {#check-dns-record-status}

Scopri come determinare se la risoluzione delle impostazioni DNS avviene in modo corretto con Cloud Manager.

## Stato record DNS {#status}

Un nome di dominio personalizzato non può gestire il traffico in tempo reale finché il DNS non viene risolto correttamente. Cloud Manager consente di determinare se la risoluzione del nome di dominio avviene in modo corretto nel sito web di AEM as a Cloud Service.

## Requisiti {#requirements}

Prima di controllare lo stato di un record DNS tramite Cloud Manager, è necessario soddisfare questi requisiti.

* È necessario aver già configurato le impostazioni DNS per il nome di dominio personalizzato come descritto nel documento [Configurazione delle impostazioni DNS.](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)

## Controllare lo stato del record DNS {#how-to}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Fai clic su **Impostazioni dominio** nel pannello di navigazione a sinistra.

1. Fai clic sull’icona **Stato** del nome di dominio.

Cloud Manager esegue una ricerca DNS per il nome di dominio e lo visualizza [stato corrente.](#statuses)

Cloud Manager attiva automaticamente una ricerca DNS quando il nome di dominio personalizzato viene verificato e distribuito correttamente per la prima volta. Per i tentativi successivi, seleziona attivamente l’icona **Nuovo tentativo di risoluzione** accanto allo stato.

## Stati DNS in Cloud Manager {#statuses}

Un dominio personalizzato può avere uno dei seguenti stati in Cloud Manager.

* **Stato DNS non rilevato**: lo stato del DNS non viene rilevato fino alla completa verifica e distribuzione del nome di dominio personalizzato.

   * Questo stato viene osservato anche quando il nome di dominio personalizzato è in fase di eliminazione.

* **Risoluzione DNS errata**: indica che la risoluzione della configurazione dei record DNS non è avvenuta o è errata.

   * Consulta [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) per ulteriori informazioni.
   * Al termine dell’operazione, seleziona l’icona **Nuovo tentativo di risoluzione** accanto allo stato.

* **Risoluzione DNS in corso**: indica che la risoluzione è in corso.

   * In genere questo stato viene visualizzato dopo aver selezionato l’icona **Nuovo tentativo di risoluzione** accanto allo stato.

* **Risoluzione DNS corretta**: le impostazioni DNS sono configurate correttamente.

   * Il sito è disponibile per i visitatori e le visitatrici.

## Passaggi successivi {#next-steps}

Congratulazioni Il dominio personalizzato è stato configurato per l&#39;utilizzo con Cloud Manager. Per informazioni dettagliate su come gestire i nomi di dominio personalizzati con Cloud Manager, consulta il documento [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).
