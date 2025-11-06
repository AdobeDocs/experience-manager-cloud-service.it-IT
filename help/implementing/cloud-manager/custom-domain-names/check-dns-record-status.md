---
title: Verificare lo stato del record DNS
description: Scopri come determinare se le impostazioni DNS vengono risolte correttamente utilizzando Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 25%

---


# Verifica dello stato del record DNS {#check-dns-record-status}

Scopri come determinare se le impostazioni DNS vengono risolte correttamente utilizzando Cloud Manager.

## Stato dei record DNS {#status}

Un nome di dominio personalizzato non può gestire il traffico in tempo reale finché il DNS non viene risolto correttamente. In Cloud Manager, puoi determinare se la risoluzione del nome di dominio nel sito web di AEM as a Cloud Service è corretta.

## Requisiti {#requirements}

Rispetta questi requisiti prima di controllare lo stato di un record DNS tramite Cloud Manager.

È necessario aver già configurato le impostazioni DNS per il nome di dominio personalizzato come descritto in [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Verifica dello stato del record DNS {#how-to}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Fai clic su **Impostazioni dominio** nel menu a sinistra.

1. Fai clic sull’icona **Stato** del nome di dominio.

Cloud Manager esegue una ricerca DNS per il nome di dominio e lo visualizza [stato corrente](#statuses).

Cloud Manager attiva automaticamente una ricerca DNS quando il nome di dominio personalizzato viene verificato e distribuito correttamente per la prima volta. Per i tentativi successivi, seleziona attivamente l’icona **Nuovo tentativo di risoluzione** accanto allo stato.

## Stati DNS in Cloud Manager {#statuses}

Un dominio personalizzato può avere uno dei seguenti stati in Cloud Manager.

| Stato | Descrizione |
| --- | --- |
| Stato DNS non rilevato | Lo stato DNS viene rilevato solo dopo la corretta verifica e distribuzione del nome di dominio personalizzato. Questo stato viene osservato anche quando il nome di dominio personalizzato è in fase di eliminazione. |
| Il DNS si risolve in modo non corretto | Questo stato indica che la configurazione dei record DNS non è stata risolta o è errata. Per ulteriori informazioni, consulta [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).<br>Al termine dell&#39;operazione, è necessario selezionare l&#39;icona **Risolvi di nuovo** accanto allo stato. |
| Risoluzione DNS in corso | Risoluzione in corso. In genere questo stato viene visualizzato dopo aver selezionato l’icona **Nuovo tentativo di risoluzione** accanto allo stato. |
| Il DNS si risolve in modo corretto | Le impostazioni DNS sono configurate correttamente. Il sito è disponibile per i visitatori e le visitatrici. |

## Passaggi successivi {#next-steps}

Il dominio personalizzato è stato configurato per l&#39;utilizzo con Cloud Manager. Per informazioni dettagliate su come gestire i nomi di dominio personalizzati con Cloud Manager, consulta il documento [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).
