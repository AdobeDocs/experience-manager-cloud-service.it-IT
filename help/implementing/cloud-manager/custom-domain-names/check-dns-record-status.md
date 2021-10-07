---
title: Verifica dello stato del record DNS
description: Verifica dello stato del record DNS
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Verifica dello stato del record DNS {#check-dns-record-status}

Per determinare se il nome di dominio viene risolto correttamente nel sito Web AEM as a Cloud Service, fai clic sull’icona Stato del record DNS nella tabella Ambienti nella pagina Impostazioni dominio .

Cloud Manager attiva automaticamente una ricerca DNS quando il nome di dominio personalizzato viene verificato e distribuito correttamente per la prima volta. Per i tentativi successivi, è necessario selezionare attivamente l&#39;icona **risolvi nuovamente** accanto allo stato.

Cloud Manager esegue una ricerca DNS per il nome di dominio e visualizza uno dei seguenti messaggi di stato:

* **Lo stato DNS non**
rilevato. Lo stato DNS non verrà rilevato finché il nome di dominio personalizzato non sarà stato verificato e distribuito correttamente. Questo stato viene osservato anche quando il nome del dominio personalizzato è in fase di eliminazione.

* **Il DNS viene risolto**
in modo errato. Indica che la configurazione dei record DNS non è ancora stata risolta/puntata o è errata. Un rappresentante di Adobe verrà informato automaticamente.

   >[!NOTE]
   >È necessario configurare un `CNAME` o `A-record` seguendo le istruzioni corrispondenti. Per ulteriori informazioni, consulta Configurazione delle impostazioni DNS . Quando è pronto, è necessario selezionare nuovamente l&#39;icona **resolve** accanto allo stato.

* **Risoluzione DNS In**
corsoRisoluzione. Questo stato viene generalmente visualizzato dopo aver selezionato l’icona &quot;risolvi di nuovo&quot; accanto allo stato.

* **DNS viene risolto**
correttamenteLe impostazioni DNS sono configurate correttamente. Il tuo sito è al servizio dei visitatori.
