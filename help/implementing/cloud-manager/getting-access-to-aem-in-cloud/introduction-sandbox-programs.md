---
title: Introduzione ai programmi sandbox
description: Scopri quali programmi sandbox differiscono dai programmi di produzione.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 2%

---


# Introduzione ai programmi sandbox {#sandbox-programs}

Scopri quali programmi sandbox differiscono dai programmi di produzione.

## Introduzione {#introduction}

Un programma sandbox viene tipicamente creato per scopi di formazione, demo in esecuzione, abilitazione o prova di concetti (POC) e quindi non è destinato a trasportare traffico live.

Un programma sandbox è uno dei due tipi di programmi disponibili in AEM Cloud Service, mentre l’altro è un [programma di produzione.](introduction-production-programs.md) Fare riferimento al documento [Informazioni su programmi e tipi di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) per ulteriori informazioni sui tipi di programma.

## Creazione automatica {#auto-creation}

I programmi sandbox dispongono di creazione automatica. Ogni volta che crei un nuovo programma sandbox, Cloud Manager automaticamente:

* Aggiunge AEM Sites e AEM Assets come soluzioni nel programma.
* Imposta un archivio Git del progetto con un progetto di esempio basato su [AEM Archetipo di progetto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it)
* Crea un ambiente di sviluppo.
* Crea una pipeline non di produzione da distribuire nell’ambiente di sviluppo.

Un programma sandbox avrà un solo ambiente di sviluppo.

## Limitazioni e condizioni {#limitations}

Poiché non sono destinati al traffico live, i programmi sandbox hanno alcune limitazioni e condizioni sull’utilizzo, che le differenziano dai programmi di produzione.

### Nessun traffico live {#live-traffic}

I programmi sandbox non sono destinati a trasportare traffico in diretta e non sono pertanto soggetti a tali programmi [AEM impegni as a Cloud Service.](https://www.adobe.com/legal/service-commitments.html)

### Nessun ridimensionamento automatico {#auto-scaling}

Gli ambienti creati in un programma sandbox non sono configurati per il ridimensionamento automatico. Pertanto, questi ambienti non sono adatti per il test delle prestazioni o del carico.

### Nessun dominio personalizzato o Elenco consentiti IP {#ip-allow}

I domini personalizzati e gli elenchi consentiti IP non sono disponibili nei programmi sandbox.

### Nessuna rete avanzata {#advanced-networking}

[Funzioni di rete avanzate](/help/security/configuring-advanced-networking.md) (ad esempio, provisioning self-service di VPN, porte non standard, indirizzi IP in uscita dedicati, ecc.) non sono disponibili nei programmi sandbox.

### Aggiornamenti manuali AEM {#updates}

Gli aggiornamenti AEM non vengono inviati automaticamente ai programmi sandbox, ma possono essere applicati manualmente agli ambienti nel programma sandbox.

* È possibile eseguire un aggiornamento manuale solo se l’ambiente di destinazione dispone di una pipeline configurata correttamente.
* Un aggiornamento manuale a un ambiente di produzione o di staging aggiornerà automaticamente l’altro. L’ambiente Production+Stage deve trovarsi nella stessa versione AEM.

Fare riferimento al documento [Aggiornamenti delle versioni AEM](/help/implementing/deploying/aem-version-updates.md) per ulteriori dettagli.

Fare riferimento al documento [Aggiornamento dell’ambiente](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) per scoprire come aggiornare un ambiente.

### Sospensione e cancellazione {#hibernation}

Gli ambienti in un programma sandbox vengono automaticamente ibernati dopo 8 ore di inattività. Una volta ibernati, possono essere disattivati manualmente.

I programmi sandbox vengono eliminati dopo 6 mesi di essere in modalità di sospensione continua, dopo di che, possono essere ricreati.

Fai riferimento a [Ambienti Sandbox sospensione e disattivazione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) per ulteriori dettagli.
