---
title: Aree geografiche di pubblicazione aggiuntiva
description: Scopri in che modo AEM as a Cloud Service supporta ulteriori aree geografiche di pubblicazione aggiuntiva per una maggiore disponibilità e una latenza ridotta.
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '542'
ht-degree: 100%

---


# Aree geografiche di pubblicazione aggiuntiva {#additional-publish-regions}

Nei programmi impostati con AEM Sites è possibile concedere in licenza e abilitare aree geografiche di pubblicazione aggiuntiva. Una volta configurata, il traffico negli ambienti di staging e produzione viene indirizzato a più farm di pubblicazione, offrendo i seguenti vantaggi:

* Latenza ridotta: le richieste che passano dalla rete CDN alle istanze di pubblicazione di AEM vengono indirizzate all’area geografica di pubblicazione più vicina, costituendo un vantaggio per i siti web e le applicazioni visitate da utenti in più aree geografiche.
* Disponibilità più elevata: se un’area geografica non è disponibile, la rete CDN indirizza il traffico sulle altre aree geografiche disponibili.

Le organizzazioni possono concedere licenze fino a tre aree geografiche di pubblicazione aggiuntiva.

>[!NOTE]
>
>Questa funzione è attualmente disponibile solo per AEM Sites. Inoltre, non può essere applicata a programmi sandbox. Tieni anche presente che per ulteriori funzioni relative alle aree geografiche di pubblicazione aggiuntiva è necessario aggiornare il programma alla versione AEM 12142 o successiva.

## Casi d’uso {#use-cases}

Di seguito sono riportati alcuni casi d’uso in cui le organizzazioni possono usufruire della concessione di licenze per aree geografiche di pubblicazione aggiuntiva.

1. Per le organizzazioni che ricevono traffico significativo o essenziale per l’azienda da utenti lontani dall’area geografica primaria, le aree geografiche di pubblicazione aggiuntiva possono ridurre la latenza rilevata da tali visitatori.
1. Per le organizzazioni che potrebbero subire danni monetari o alla reputazione significativi quando un sito non è disponibile, tali rischi possono essere mitigati utilizzando aree geografiche di pubblicazione aggiuntiva per rendere il livello di pubblicazione di AEM più resiliente rispetto agli errori.
1. Per le organizzazioni i cui autori di contenuti si trovano in una posizione geografica distante dalla maggior parte dei visitatori del livello di pubblicazione, accanto alla posizione degli autori di contenuti è possibile scegliere l’area geografica primaria, mentre accanto al traffico lato pubblicazione è possibile configurare aree di pubblicazione aggiuntiva, con entrambi i tipi di pubblico che usufruiscono di un’esperienza ottimizzata.

## Abilitazione e configurazione {#enabling-and-configuring}

Dopo aver concesso in licenza un’area geografica di pubblicazione aggiuntiva, le aree geografiche vengono configurate utilizzando Cloud Manager. Consulta la [Documentazione di Cloud Manager](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) per istruzioni dettagliate.

Le aree geografiche di pubblicazione aggiuntiva vengono applicate agli ambienti di staging e produzione, ma non agli ambienti RDE o di sviluppo.

## Considerazioni sulle reti avanzate {#advanced-networking-considerations}

Quando un’area geografica di pubblicazione aggiuntiva è abilitata in un programma con rete avanzata già configurata, per impostazione predefinita il traffico nell’area geografica di pubblicazione aggiuntiva che corrisponde alle regole di rete avanzate passerà attraverso l’area geografica primaria. Al fine di sfruttare la maggiore disponibilità, si consiglia di abilitare la rete avanzata nelle aree geografiche aggiuntive.

Consulta la sezione [Configurazione di rete avanzata per aree geografiche di pubblicazione aggiuntive](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions) nella documentazione sulla rete avanzata per ottenere ulteriori informazioni, tra cui come aggiungere configurazioni di rete avanzate alle aree geografiche aggiuntive senza causare la perdita di connettività.

## Limitazioni {#limitations}

Tieni presenti le seguenti limitazioni quando consideri di utilizzare aree di pubblicazione aggiuntive.

* È possibile aggiungere aree geografiche di pubblicazione aggiuntiva solo ad AEM Sites. Le aree geografiche di pubblicazione aggiuntiva non si estendono ad altre soluzioni AEM o a funzionalità correlate implementate nello stesso programma (ad esempio, AEM Forms o Adobe Learning Manager).
* È possibile aggiungere altre aree solo se i diritti associati sono disponibili e non utilizzati nel tenant.
* È possibile aggiungere fino a tre aree geografiche di pubblicazione aggiuntiva a ogni singolo ambiente.
* Ulteriori aree geografiche sono disponibili solo nei programmi di produzione. Questa funzione non è disponibile nei programmi sandbox.
* Le aree geografiche di pubblicazione aggiuntiva vengono applicate solo agli ambienti di staging e di produzione, non agli ambienti RDE o di sviluppo.
* Le aree geografiche di pubblicazione aggiuntiva richiedono l’aggiornamento del programma alla versione AEM 12142 o successiva.
