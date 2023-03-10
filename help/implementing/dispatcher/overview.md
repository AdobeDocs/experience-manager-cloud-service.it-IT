---
title: Panoramica del flusso di distribuzione dei contenuti
description: Panoramica del flusso di distribuzione dei contenuti
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: 60fc1b8f93c93ca427507dbe56511342f285e6bc
workflow-type: ht
source-wordcount: '207'
ht-degree: 100%

---

# Flusso di distribuzione dei contenuti {#content-delivery}

La pagina corrente descrive la consegna dei contenuti del servizio di pubblicazione in AEM as a Cloud Service. La consegna dei contenuti del servizio di pubblicazione include:

* CDN
* Dispatcher AEM
* Pubblicazione AEM

Il flusso di dati è il seguente:

1. L’URL viene aggiunto nel browser
1. Richiesta effettuata a CDN mappata in DNS a quel dominio
1. Se il contenuto è completamente memorizzato nella cache su CDN, quest’ultima lo trasmette al browser
1. Se il contenuto non è completamente memorizzato nella cache, la rete CDN si rivolge (proxy invertito) al dispatcher
1. Se il contenuto è completamente memorizzato nella cache del dispatcher, quest’ultimo lo distribuisce alla CDN
1. Se il contenuto non è completamente memorizzato nella cache, il dispatcher si rivolge (proxy invertito) a AEM Publish
1. Il contenuto viene renderizzato dal browser, che può anche memorizzarlo nella cache, a seconda delle intestazioni

Per impostazione predefinita, il tipo di contenuto HTML/testo è impostato per scadere dopo 300 secondi (5 minuti) al livello del dispatcher, una soglia rispettata sia dalla cache del dispatcher che dalla CDN. Durante le ridistribuzioni del servizio di pubblicazione, la cache del dispatcher viene svuotata e successivamente subisce un processo di riscaldamento prima che i nuovi nodi di pubblicazione accettino il traffico.

Le sezioni seguenti forniscono ulteriori dettagli sulla distribuzione dei contenuti:
* [Configurazione CDN](/help/implementing/dispatcher/cdn.md)
* [Memorizzazione in cache](/help/implementing/dispatcher/caching.md)


Sono disponibili informazioni sulla replica dal servizio di authoring al servizio di pubblicazione [qui](/help/operations/replication.md).
