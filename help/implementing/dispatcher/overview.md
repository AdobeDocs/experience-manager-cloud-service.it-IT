---
title: Panoramica del flusso di distribuzione dei contenuti
description: Ulteriori informazioni sul flusso di dati per la distribuzione dei contenuti e su come pubblicare i contenuti
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: d1da8559da856e028a5dcad1d0c0b2c00176af0c
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 45%

---

# Flusso di distribuzione dei contenuti {#content-delivery}

La pagina corrente descrive la consegna dei contenuti del servizio di pubblicazione in AEM as a Cloud Service. La consegna dei contenuti del servizio di pubblicazione include:

* CDN
* AEM Dispatcher
* Pubblicazione AEM

Il flusso di dati è il seguente:

1. L’URL viene aggiunto nel browser
1. Richiesta effettuata a CDN mappata in DNS a quel dominio
1. Se il contenuto è completamente memorizzato nella cache su CDN, quest’ultima lo trasmette al browser
1. Se il contenuto non è completamente memorizzato nella cache, la rete CDN viene richiamata (proxy inverso) in Dispatcher
1. Se il contenuto è completamente memorizzato nella cache in Dispatcher, Dispatcher lo trasmette alla rete CDN
1. Se il contenuto non è completamente memorizzato nella cache, Dispatcher invia una chiamata (proxy inverso) alla pubblicazione AEM
1. Il contenuto viene renderizzato dal browser, che può anche memorizzarlo nella cache, a seconda delle intestazioni

Per impostazione predefinita, il tipo di contenuto HTML/testo è impostato per scadere dopo 300 secondi (5 minuti) a livello di Dispatcher, una soglia rispettata sia dalla cache di Dispatcher che dalla rete CDN. Durante le ridistribuzioni del servizio di pubblicazione, la cache di Dispatcher viene cancellata e quindi riscaldata prima che i nuovi nodi di pubblicazione accettino il traffico.

Le sezioni seguenti forniscono maggiori dettagli sulla distribuzione dei contenuti:
* [Configurazione CDN](/help/implementing/dispatcher/cdn.md)
* [Memorizzazione in cache](/help/implementing/dispatcher/caching.md)


Sono disponibili informazioni sulla replica dal servizio di authoring al servizio di pubblicazione [qui](/help/operations/replication.md).
