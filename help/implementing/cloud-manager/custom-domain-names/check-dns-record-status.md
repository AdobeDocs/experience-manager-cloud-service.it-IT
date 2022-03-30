---
title: Verifica dello stato del record DNS
description: Scopri come determinare se le impostazioni DNS vengono corrette utilizzando Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 2278abcf0c34fd34a7730242ee27814d37b7d4d0
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---

# Verifica dello stato del record DNS {#check-dns-record-status}

In Cloud Manager puoi determinare se il nome di dominio viene risolto correttamente nel sito web as a Cloud Service AEM.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.

1. Fai clic su **Impostazioni di dominio** nel pannello di navigazione a sinistra.

1. Fai clic sul pulsante **Stato** per il nome di dominio.

Cloud Manager esegue una ricerca DNS per il nome di dominio e visualizza uno dei seguenti messaggi di stato.

* **Stato DNS non rilevato** - Lo stato DNS non verrà rilevato finché il nome di dominio personalizzato non sarà stato verificato e distribuito correttamente.

   * Questo stato viene osservato anche quando il nome del dominio personalizzato è in fase di eliminazione.

* **Il DNS viene risolto in modo errato** - Indica che la configurazione dei record DNS non è stata risolta o è errata.

   * Consulta il documento [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) per saperne di più.
   * Quando è pronto, è necessario selezionare la **Risolvi di nuovo** accanto allo stato .

* **Risoluzione DNS in corso** - La risoluzione è in corso.

   * Questo stato viene generalmente visualizzato dopo aver selezionato **Risolvi di nuovo** accanto allo stato .

* **Il DNS viene risolto correttamente** - Le impostazioni DNS sono configurate correttamente.

   * Il tuo sito è al servizio dei visitatori.

Cloud Manager attiva automaticamente una ricerca DNS quando il nome di dominio personalizzato viene verificato e distribuito correttamente per la prima volta. Per i tentativi successivi, devi selezionare attivamente il **Risolvi di nuovo** accanto allo stato .
