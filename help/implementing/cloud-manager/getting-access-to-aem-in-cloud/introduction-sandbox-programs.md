---
title: 'Introduzione ai programmi sandbox '
description: Introduzione ai programmi sandbox
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 1892900ea3f365e1b5f7d31ffae64d45256d2a3a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Introduzione ai programmi sandbox {#sandbox-programs}

## Introduzione {#introduction}

Un programma sandbox è uno dei due tipi di programmi disponibili in AEM Cloud Service, l’altro è un programma di produzione.

Una sandbox viene generalmente creata per scopi di formazione, demo in esecuzione, abilitazione o prova di concetto (POC). Non sono fatte per trasportare traffico dal vivo. Non sono soggetti al [AEM impegni as a Cloud Service](https://www.adobe.com/legal/service-commitments.html).

Gli ambienti creati in una sandbox non sono configurati per il ridimensionamento automatico. Pertanto, questi ambienti non sono adatti per il test delle prestazioni o del carico.

I programmi sandbox includono [!DNL Sites] e [!DNL Assets] e vengono compilati automaticamente con un archivio Git, un ambiente di sviluppo e una pipeline non di produzione.  L’archivio Git viene compilato con un progetto di esempio basato sull’archetipo di progetto AEM.

>[!IMPORTANT]
>Un programma sandbox avrà un solo ambiente di sviluppo.

>[!NOTE]
>I domini personalizzati e gli Elenchi consentiti IP non sono disponibili nei programmi sandbox.

Fai riferimento a [Informazioni su programmi e tipi di programmi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html?lang=en) per ulteriori informazioni sui tipi di programma.

### Attributi dei programmi sandbox {#attributes-sandbox}

I programmi sandbox hanno i seguenti attributi:

1. **Creazione di programmi:** La creazione del programma sandbox include automaticamente:
   * configurazione del progetto con codice di esempio e contenuto
   * creazione di un ambiente di sviluppo
   * creazione di una pipeline non di produzione da distribuire nell’ambiente di sviluppo (distribuzione del ramo principale nell’ambiente di sviluppo)

1. **Soluzioni:** I programmi sandbox includono AEM [!DNL Sites] e [!DNL Assets].

1. **Aggiornamenti AEM:** Gli aggiornamenti AEM possono essere applicati manualmente agli ambienti in un programma sandbox e non vengono inviati automaticamente.
Fai riferimento a [Aggiornamenti AEM agli ambienti Sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox) per ulteriori dettagli.

1. **Sospensione:** Gli ambienti in un programma sandbox vengono ibernati automaticamente se non viene rilevata alcuna attività per un determinato periodo di tempo. Le sandbox vengono messe nel nodo di ibernazione dopo 8 ore di inattività, dopo di che, possono essere deibernate. Gli ambienti sospesi possono essere disattivati manualmente.
Fai riferimento a [Ambienti Sandbox sospensione e disattivazione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md) per ulteriori dettagli.

1. **Eliminazione**: Le sandbox vengono cancellate dopo 6 mesi di essere in modalità di sospensione continua, dopo di che, possono essere ricreati.
