---
title: Introduzione ai programmi sandbox
description: Scopri che cosa sono i programmi sandbox e in cosa differiscono dai programmi di produzione.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 18c5d2ba77a97413d0d83235ad2baec9fe4b0238
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 88%

---


# Introduzione ai programmi sandbox {#sandbox-programs}

Scopri che cosa sono i programmi sandbox e in cosa differiscono dai programmi di produzione.

## Introduzione {#introduction}

Un programma sandbox viene tipicamente creato per scopi di formazione, esecuzione di demo, attivazione o modelli di verifica (POC) e non è quindi destinato a contenere traffico in tempo reale.

Un programma sandbox è uno dei due tipi di programmi disponibili in AEM Cloud Service; l’altro è il [programma di produzione.](introduction-production-programs.md) Per ulteriori informazioni sui tipi di programmi, consulta il documento [Informazioni su programmi e tipi di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

## Creazione automatica {#auto-creation}

I programmi sandbox dispongono della funzionalità di creazione automatica. Ogni volta che crei un nuovo programma sandbox, Cloud Manager automaticamente:

* Aggiunge al programma le soluzioni AEM Sites e AEM Assets.
* Imposta un archivio Git del progetto con un progetto di esempio basato sull’[archetipo del progetto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it)
* Crea un ambiente di sviluppo.
* Crea una pipeline non di produzione da distribuire nell’ambiente di sviluppo.

Un programma sandbox presenta un solo ambiente di sviluppo.

## Limitazioni e condizioni {#limitations}

Poiché non sono destinati al traffico in tempo reale, i programmi sandbox presentano alcune limitazioni e condizioni sull’utilizzo che li differenziano dai programmi di produzione.

### Traffico in tempo reale non disponibile {#live-traffic}

I programmi sandbox non sono destinati a contenere traffico in tempo reale e non sono pertanto soggetti agli [impegni di AEM as a Cloud Service.](https://www.adobe.com/it/legal/service-commitments.html)

### Ridimensionamento automatico non disponibile {#auto-scaling}

Gli ambienti creati in un programma sandbox non sono configurati per il ridimensionamento automatico. Pertanto, questi ambienti non sono adatti per il test delle prestazioni o del carico.

### Domini personalizzati o elenchi IP consentiti non disponibili {#ip-allow}

I domini personalizzati e gli elenchi IP consentiti non sono disponibili nei programmi sandbox.

### Funzionalità di rete avanzate non disponibili {#advanced-networking}

[Le funzionalità di rete avanzate](/help/security/configuring-advanced-networking.md) (ad esempio il provisioning self-service di VPN, porte non standard, indirizzi IP in uscita dedicati e così via) non sono disponibili nei programmi sandbox.

### Aggiornamenti di AEM manuali {#updates}

Gli aggiornamenti di AEM non vengono eseguiti automaticamente per i programmi sandbox, ma possono essere applicati manualmente agli ambienti nel programma sandbox.

* È possibile eseguire un aggiornamento manuale solo se nell’ambiente di destinazione è presente una pipeline configurata correttamente.
* Apportando un aggiornamento manuale a un ambiente di produzione o di staging si aggiorna automaticamente anche l’altro. Il set di ambienti Produzione + Staging deve avere la stessa versione di AEM.

Per ulteriori informazioni, consulta il documento [Aggiornamenti della versione di AEM](/help/implementing/deploying/aem-version-updates.md).

Per ulteriori informazioni su come aggiornare un ambiente, consulta il documento [Aggiornamento dell’ambiente](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment).

### Sospensione ed eliminazione {#hibernation}

Gli ambienti in un programma sandbox vengono automaticamente sospesi dopo 8 ore di inattività. Una volta sospesi, possono essere riattivati manualmente.

I programmi sandbox vengono eliminati dopo 6 mesi di sospensione continua. Al termine di questo periodo, possono essere ricreati.

Per ulteriori informazioni, consulta [Sospensione e riattivazione degli ambienti sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md).

### Nessun supporto tecnico {#no-support}

Poiché in genere viene creato un programma sandbox per scopi di formazione, demo in esecuzione, abilitazione o prova di concetti (POC), il supporto tecnico non è disponibile per problemi riscontrati in un programma sandbox.

In caso di problemi durante la creazione e la gestione dei programmi sandbox, l’ambito del supporto tecnico rimane invariato.
