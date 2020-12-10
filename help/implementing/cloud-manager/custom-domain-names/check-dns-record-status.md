---
title: Verifica dello stato del record DNS
description: Verifica dello stato del record DNS
translation-type: tm+mt
source-git-commit: b76a22469f248dde316dcaa514a906fe4361afd1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Verifica dello stato del record DNS {#check-dns-record-status}

È possibile determinare se il nome di dominio viene risolto correttamente nel AEM come sito Web di Cloud Service facendo clic sull&#39;icona Stato per il record DNS nella tabella in Ambienti della pagina Impostazioni di dominio.

Cloud Manager attiva automaticamente una ricerca DNS quando il nome di dominio personalizzato viene verificato e distribuito per la prima volta. Per i tentativi successivi, devi selezionare attivamente l&#39;icona **resolve again** accanto allo stato.

Cloud Manager esegue una ricerca DNS per il tuo nome di dominio e visualizza uno dei seguenti messaggi di stato:

* **Lo stato DNS non**
rilevatoLo stato DNS non verrà rilevato finché il nome di dominio personalizzato non sarà stato verificato e distribuito correttamente. Questo stato viene osservato anche quando il nome del dominio personalizzato è in fase di eliminazione.

* **Risoluzioni DNS**
errate: indica che la configurazione dei record DNS non è ancora stata risolta/puntata o è errata.  rappresentante del Adobe ne verrà informato automaticamente.

   >[!NOTE]
   >È necessario configurare `CNAME` o `A-record` seguendo le istruzioni corrispondenti. Per ulteriori informazioni, consulta Configurazione delle impostazioni DNS. Quando è pronto, è necessario selezionare l&#39;icona **resolve** accanto allo stato.

* **Risoluzione DNS in**
corsoRisoluzione. Questo stato viene generalmente visualizzato dopo che avete selezionato l’icona &quot;resolve again&quot; (Risolvi di nuovo) accanto allo stato.

* **DNS Risolve**
correttamenteLe impostazioni DNS sono configurate correttamente. Il sito è al servizio dei visitatori.
