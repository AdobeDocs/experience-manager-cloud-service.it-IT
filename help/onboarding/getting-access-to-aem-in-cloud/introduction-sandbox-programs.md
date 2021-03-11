---
title: 'Introduzione ai programmi sandbox '
description: 'Introduzione ai programmi sandbox '
translation-type: tm+mt
source-git-commit: d98e3ba930690627bfbe9b90ce5cb93328c30503
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Introduzione ai programmi sandbox {#sandbox-programs}

## Introduzione {#introduction}

Un programma Sandbox è uno dei due tipi di programmi disponibili AEM Cloud Service, l&#39;altro è un programma di produzione.

Una sandbox viene generalmente creata per scopi di formazione, demo in esecuzione, abilitazione o prova di concetto (POC). Non sono fatte per trasportare traffico dal vivo. Non sono soggetti al [AEM come impegni Cloud Service](https://www.adobe.com/legal/service-commitments.html).

Gli ambienti creati in una sandbox non sono configurati per il ridimensionamento automatico. Pertanto, questi ambienti non sono adatti per il test delle prestazioni o del carico.

I programmi sandbox includono Sites e Assets e vengono compilati automaticamente con un archivio Git, un ambiente di sviluppo e una pipeline non di produzione.  L’archivio Git viene compilato con un progetto di esempio basato sull’archetipo di progetto AEM.

Per ulteriori informazioni sui tipi di programma, consulta [Informazioni su programmi e tipi di programma](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) .

### Attributi dei programmi sandbox {#attributes-sandbox}

I programmi sandbox hanno i seguenti attributi:

1. **Creazione del programma:** la creazione del programma sandbox include automatica:
   * configurazione del progetto con codice di esempio e contenuto
   * creazione di un ambiente di sviluppo
   * creazione di una pipeline non di produzione da distribuire nell’ambiente di sviluppo (distribuzione del ramo principale nell’ambiente di sviluppo)

1. **Soluzioni:** i programmi sandbox includono AEM Sites e Assets.

1. **Aggiornamenti AEM:** AEM gli aggiornamenti possono essere applicati manualmente agli ambienti in un programma sandbox e non vengono inviati automaticamente.
Per ulteriori informazioni, consulta [AEM Aggiornamenti agli ambienti Sandbox](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox) .

1. **Sospensione:** gli ambienti in un programma sandbox vengono ibernati automaticamente se non viene rilevata alcuna attività per un determinato periodo di tempo. Gli ambienti sospesi possono essere disattivati manualmente.
Per ulteriori informazioni, consulta [Sospensione e disattivazione degli ambienti sandbox](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md) .