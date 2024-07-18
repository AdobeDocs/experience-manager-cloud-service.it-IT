---
title: Aree geografiche di pubblicazione aggiuntiva
description: Scopri in che modo AEM as a Cloud Service supporta ulteriori aree geografiche di pubblicazione aggiuntiva per una maggiore disponibilità e una latenza ridotta.
exl-id: b9ac3c6a-eb8b-461d-8f1d-a0356046a3f9
feature: Operations
role: Admin
source-git-commit: c7362a77fd929d812db3cd40bf01763ed3bef02c
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 71%

---


# Aree geografiche di pubblicazione aggiuntiva {#additional-publish-regions}

Nei programmi impostati con AEM Sites è possibile concedere in licenza e abilitare aree geografiche di pubblicazione aggiuntiva. Una volta configurata, il traffico negli ambienti di staging e produzione viene indirizzato a più farm di pubblicazione, offrendo i seguenti vantaggi:

* Latenza ridotta: le richieste che passano dalla rete CDN alle istanze di pubblicazione di AEM vengono indirizzate all’area geografica di pubblicazione più vicina, costituendo un vantaggio per i siti web e le applicazioni visitate da utenti in più aree geografiche.
* Disponibilità più elevata: se un’area geografica non è disponibile, la rete CDN indirizza il traffico sulle altre aree geografiche disponibili.

Le organizzazioni possono concedere licenze fino a tre aree geografiche di pubblicazione aggiuntiva.

>[!NOTE]
>
>* Questa funzione è disponibile per le soluzioni Sites e Forms.
>* Questa funzionalità non può essere applicata a [programmi sandbox.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
>* Questa funzione richiede l’aggiornamento del programma alla versione AEM 12142 o successiva.

## Casi d’uso {#use-cases}

Di seguito sono riportati alcuni casi d’uso in cui le organizzazioni possono usufruire della concessione di licenze per aree geografiche di pubblicazione aggiuntiva.

1. Per le organizzazioni che ricevono traffico significativo o essenziale per l’azienda da utenti lontani dall’area geografica primaria, le aree geografiche di pubblicazione aggiuntiva possono ridurre la latenza rilevata da tali visitatori.
1. Per le organizzazioni che potrebbero subire danni monetari o alla reputazione significativi quando un sito non è disponibile, tali rischi possono essere mitigati utilizzando aree geografiche di pubblicazione aggiuntiva per rendere il livello di pubblicazione di AEM più resiliente rispetto agli errori.
1. Per le organizzazioni i cui autori di contenuti si trovano in una posizione geografica distante dalla maggior parte dei visitatori del livello di pubblicazione, accanto alla posizione degli autori di contenuti è possibile scegliere l’area geografica primaria, mentre accanto al traffico lato pubblicazione è possibile configurare aree di pubblicazione aggiuntiva, con entrambi i tipi di pubblico che usufruiscono di un’esperienza ottimizzata.

## Abilitazione e configurazione {#enabling-and-configuring}

Dopo aver concesso in licenza un’area geografica di pubblicazione aggiuntiva, le aree geografiche vengono configurate utilizzando Cloud Manager. Consulta la [Documentazione di Cloud Manager](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) per istruzioni dettagliate.

Le aree geografiche di pubblicazione aggiuntiva vengono applicate agli ambienti di staging e produzione, ma non agli ambienti RDE o di sviluppo.

Nel caso in cui un’area geografica non sia più disponibile, i clienti non dovranno gestire l’instradamento del traffico verso le aree disponibili, in quanto è gestito dalla rete CDN di Adobe.

Come descritto nella sezione Considerazioni avanzate sulla rete di seguito, si consiglia ai clienti che utilizzano la rete avanzata di configurarla per ogni area di pubblicazione aggiuntiva per mantenere la disponibilità nel caso in cui un’area non sia più disponibile.


## Considerazioni sulle reti avanzate {#advanced-networking-considerations}

Quando un’area geografica di pubblicazione aggiuntiva è abilitata in un programma con rete avanzata già configurata, per impostazione predefinita il traffico nell’area geografica di pubblicazione aggiuntiva che corrisponde alle regole di rete avanzate passerà attraverso l’area geografica primaria. Al fine di sfruttare la maggiore disponibilità, si consiglia di abilitare la rete avanzata nelle aree geografiche aggiuntive.

Consulta la sezione [Configurazione di rete avanzata per aree geografiche di pubblicazione aggiuntive](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions) nella documentazione sulla rete avanzata per ottenere ulteriori informazioni, tra cui come aggiungere configurazioni di rete avanzate alle aree geografiche aggiuntive senza causare la perdita di connettività.

## Registrazione {#logging}

Se sono abilitate altre aree, i registri separati per ciascuna area saranno resi disponibili tramite Cloud Manager. Per ulteriori informazioni, vedere [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md) e [Registri per altre aree geografiche di Publish](/help/implementing/developing/introduction/logging.md#logs-for-additional-publish-regions).

## Limitazioni {#limitations}

Tieni presenti le seguenti limitazioni quando consideri di utilizzare aree di pubblicazione aggiuntive.

* È possibile aggiungere altre aree geografiche di pubblicazione solo ad AEM Sites o AEM Forms.
   * Altre aree geografiche di pubblicazione non si estendono ad altre soluzioni AEM o funzionalità correlate implementate nello stesso programma (ad esempio, AEM Assets o Adobe Learning Manager).
   * Tuttavia, queste soluzioni possono essere aggiunte a un programma a condizione che disponga di almeno una soluzione Sites o Forms applicabile.
* È possibile aggiungere altre aree solo se i diritti associati sono disponibili e non utilizzati nel tenant.
* È possibile aggiungere fino a tre aree geografiche di pubblicazione aggiuntiva a ogni singolo ambiente.
* Ulteriori aree geografiche sono disponibili solo nei programmi di produzione. Questa funzione non è disponibile nei programmi sandbox.
* Le aree geografiche di pubblicazione aggiuntiva vengono applicate solo agli ambienti di staging e di produzione, non agli ambienti RDE o di sviluppo.
* Le aree geografiche di pubblicazione aggiuntiva richiedono l’aggiornamento del programma alla versione AEM 12142 o successiva.
