---
title: Panoramica sul flusso di distribuzione dei contenuti
description: Panoramica sul flusso di distribuzione dei contenuti
translation-type: tm+mt
source-git-commit: 0080ace746f4a7212180d2404b356176d5f2d72c
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Flusso di distribuzione dei contenuti {#content-delivery}

I dettagli della pagina corrente consentono di pubblicare il contenuto del servizio in AEM come servizio cloud. La distribuzione dei contenuti del servizio di pubblicazione include:

* CDN
* dispatcher AEM
* Pubblicazione AEM

Il flusso di dati è il seguente:

1. L’URL viene aggiunto nel browser
1. Richiesta effettuata alla CDN mappata in DNS a tale dominio
1. Se il contenuto è completamente memorizzato nella cache su CDN, CDN lo trasmette al browser
1. Se il contenuto non è completamente memorizzato nella cache, la rete CDN richiama (proxy inverso) al dispatcher
1. Se il contenuto è completamente memorizzato nella cache del dispatcher, il dispatcher lo invia alla CDN
1. Se il contenuto non è completamente memorizzato nella cache, il dispatcher richiama (proxy inverso) alla pubblicazione AEM
1. Il contenuto viene rappresentato dal browser, che potrebbe anche memorizzarlo nella cache, a seconda delle intestazioni

Per impostazione predefinita, il tipo di contenuto HTML/testo è impostato per scadere dopo 300 (5 minuti) al livello dispatcher, una soglia rispettata sia dalla cache dispatcher che dalla CDN. Durante le ridistribuzioni del servizio di pubblicazione, la cache del dispatcher viene svuotata e successivamente riscaldata prima che i nuovi nodi di pubblicazione accettino il traffico.

Le sezioni seguenti forniscono maggiori dettagli sulla distribuzione dei contenuti, inclusa la configurazione CDN e il caching.

Le informazioni sulla replica dal servizio di creazione al servizio di pubblicazione sono disponibili [qui](/help/operations/replication.md).
