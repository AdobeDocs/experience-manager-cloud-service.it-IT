---
title: Panoramica del flusso di distribuzione dei contenuti
description: Ulteriori informazioni sul flusso di dati per la distribuzione dei contenuti e su come pubblicare i contenuti
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
feature: Dispatcher
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 87%

---

# Flusso di distribuzione dei contenuti {#content-delivery}

La pagina corrente descrive la consegna dei contenuti del servizio di pubblicazione in AEM as a Cloud Service. La consegna dei contenuti del servizio di pubblicazione include:

* CDN
* Dispatcher AEM
* Editore AEM

Il flusso di dati è il seguente:

1. L’URL viene aggiunto nel browser
1. Richiesta effettuata a CDN mappata in DNS a quel dominio
1. Se il contenuto è completamente memorizzato nella cache su CDN, quest’ultima lo trasmette al browser
1. Se il contenuto non è completamente memorizzato nella cache, la rete CDN si rivolge (proxy invertito) al Dispatcher
1. Se il contenuto è completamente memorizzato nella cache del Dispatcher, quest’ultimo lo distribuisce alla CDN
1. Se il contenuto non è completamente memorizzato nella cache, il Dispatcher si rivolge (proxy invertito) alla pubblicazione AEM
1. Il browser esegue il rendering sul contenuto, che può anche memorizzarlo nella cache, a seconda delle intestazioni

Per impostazione predefinita, il tipo di contenuto HTML/testo è impostato per scadere dopo 300 secondi (5 minuti) al livello del Dispatcher, una soglia rispettata sia dalla cache del Dispatcher che dalla CDN. Durante le ridistribuzioni del servizio di pubblicazione, la cache del Dispatcher viene svuotata e quindi subisce un processo di riscaldamento prima che i nuovi nodi di pubblicazione accettino il traffico.

Le sezioni seguenti forniscono ulteriori dettagli sulla distribuzione dei contenuti:

* [Configurazione CDN](/help/implementing/dispatcher/cdn.md)
* [Memorizzazione in cache](/help/implementing/dispatcher/caching.md)

Per informazioni sulla replica dal servizio di authoring al servizio di pubblicazione, vedere [Replica](/help/operations/replication.md).
