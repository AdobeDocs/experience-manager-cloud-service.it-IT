---
title: Aree geografiche di pubblicazione aggiuntiva
description: Scopri in che modo AEM as a Cloud Service supporta ulteriori aree geografiche di pubblicazione per una maggiore disponibilità e una latenza ridotta.
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---


# Aree geografiche di pubblicazione aggiuntiva {#additional-publish-regions}

È possibile concedere in licenza e abilitare altre aree geografiche di pubblicazione nei programmi impostati con AEM Sites. Una volta configurata, il traffico negli ambienti di staging e produzione viene indirizzato a più farm di pubblicazione, il che offre i seguenti vantaggi:

* Latenza ridotta: le richieste che passano dalla rete CDN alle istanze di pubblicazione dell’AEM vengono indirizzate all’area di pubblicazione più vicina, il che è vantaggioso per i siti web e le applicazioni visitate da utenti in più aree geografiche.
* Disponibilità più elevata: se un’area non è disponibile, la rete CDN indirizza il traffico alle altre aree disponibili.

Le organizzazioni possono concedere licenze fino a tre ulteriori aree geografiche di pubblicazione.

>[!NOTE]
>
>Questa funzione è attualmente disponibile solo per AEM Sites. Inoltre, non può essere applicata ai programmi sandbox. Inoltre, tieni presente che per altre funzioni relative alle aree geografiche di pubblicazione è necessario aggiornare il programma alla versione AEM 12142 o successiva.

## Casi d’uso {#use-cases}

Di seguito sono riportati alcuni casi d’uso in cui le organizzazioni possono beneficiare della concessione di licenze per altre aree geografiche di pubblicazione.

1. Per le organizzazioni che ricevono traffico significativo o business-critical da utenti lontani dall’area principale, ulteriori aree geografiche di pubblicazione possono ridurre la latenza rilevata da tali visitatori.
1. Per le organizzazioni che potrebbero subire danni monetari o alla reputazione significativi quando un sito non è disponibile, questo può essere mitigato utilizzando ulteriori aree geografiche di pubblicazione per rendere il livello di pubblicazione dell’AEM più resiliente ai fallimenti regionali.
1. Per le organizzazioni i cui autori di contenuti si trovano in una posizione geografica distante dalla maggior parte dei visitatori del livello di pubblicazione, l’area principale può essere scelta accanto alla posizione degli autori di contenuti, mentre è possibile configurare altre aree di pubblicazione accanto al traffico lato pubblicazione, con entrambi i tipi di pubblico che beneficiano di un’esperienza ottimizzata.

## Abilitazione e configurazione {#enabling-and-configuring}

Dopo aver concesso in licenza un’ulteriore area geografica di pubblicazione, queste vengono configurate utilizzando Cloud Manager. Consulta la [Documentazione di Cloud Manager](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) per istruzioni dettagliate.

Aree geografiche di pubblicazione aggiuntive vengono applicate agli ambienti di staging e produzione, ma non agli ambienti RDE o di sviluppo.

## Considerazioni sulle reti avanzate {#advanced-networking-considerations}

Quando un’area di pubblicazione aggiuntiva è abilitata in un programma con rete avanzata già configurata, per impostazione predefinita il traffico nell’area di pubblicazione aggiuntiva che corrisponde alle regole di rete avanzate passerà attraverso l’area primaria. Per sfruttare la maggiore disponibilità, si consiglia di abilitare la rete avanzata nelle altre aree geografiche.

Consulta la [Configurazione di rete avanzata per aree di pubblicazione aggiuntive](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions) nella documentazione di Advanced Networking per informazioni dettagliate, tra cui come aggiungere configurazioni di rete avanzate ad altre aree geografiche senza causare la perdita di connettività.

## Limitazioni {#limitations}

Tieni presenti le seguenti limitazioni quando consideri di utilizzare aree di pubblicazione aggiuntive.

* È possibile aggiungere altre aree geografiche di pubblicazione solo ad AEM Sites. Altre aree geografiche di pubblicazione non si estendono ad altre soluzioni AEM o funzionalità correlate implementate nello stesso programma (ad esempio, AEM Forms o Adobe Learning Manager).
* È possibile aggiungere altre aree solo se i diritti associati sono disponibili e non utilizzati nel tenant.
* È possibile aggiungere fino a tre aree geografiche di pubblicazione a ogni singolo ambiente.
* Ulteriori aree geografiche sono disponibili solo nei programmi di produzione. Questa funzione non è disponibile nei programmi sandbox.
* Ulteriori aree geografiche di pubblicazione vengono applicate solo agli ambienti di staging e produzione, non agli ambienti RDE o di sviluppo.
* Altre aree geografiche richiedono l’aggiornamento del programma alla versione AEM 12142 o successiva.
