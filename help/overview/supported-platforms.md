---
title: Piattaforme client supportate
description: Scopri quali browser sono supportati per la creazione di contenuti con Adobe Experience Manager as a Cloud Service e l’accesso ai siti pubblicati con AEM.
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 7ddd0a75-621a-4499-91d1-7b3408a68269
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 99%

---

# Piattaforme client supportate {#supported-platforms}

Scopri quali browser sono supportati per la creazione di contenuti con Adobe Experience Manager as a Cloud Service e l’accesso ai siti pubblicati con AEM.

>[!TIP]
>
>Questo documento descrive le piattaforme client supportate da AEM as a Cloud Service. Per informazioni dettagliate sull’ambiente di build per lo sviluppo del progetto AEM, consulta il documento [Ambiente di build.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)

## Livelli di supporto {#support-levels}

Adobe definisce i seguenti livelli di supporto per le piattaforme client di AEM.

| Livello di supporto | Descrizione |
|---|---|
| A: supportato | Adobe fornisce supporto e manutenzione completi per questa configurazione. Questa configurazione è coperta dal processo di controllo qualità di Adobe. |
| R: supporto limitato | Il supporto necessita di una richiesta formale ad Adobe per utilizzare la configurazione in un progetto. Una volta confermato, Adobe fornisce il supporto completo all’interno del programma di supporto limitato. Per ulteriori informazioni, contatta l’Assistenza clienti di Adobe. |
| Z: non supportato | La configurazione non è supportata. Adobe non fornisce istruzioni sul funzionamento o meno della configurazione e non la supporta. |

## Browser supportati per l’authoring dei contenuti {#authoring}

L’interfaccia utente di AEM è ottimizzata per schermi più grandi presenti in notebook, computer desktop e dispositivi tablet (come Apple iPad o Microsoft Surface). Il fattore di forma telefono non è supportato per nessun caso d’uso di authoring.

L’interfaccia utente di Adobe Experience Manager funziona con le seguenti piattaforme client a seconda del [metodo di authoring.](/help/edge/overview.md#authoring-method)

* [Editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [Editor pagina](/help/sites-cloud/authoring/page-editor/introduction.md)
* [Authoring basato su documenti](https://www.aem.live/docs/aem-authoring) utilizzando [Sidekick](https://www.aem.live/docs/sidekick)

Tutti i browser vengono testati con il set predefinito di plug-in e componenti aggiuntivi.

| Browser | Livello di supporto dell’editor universale | Livello di supporto dell’Editor pagina | Livello di supporto di Sidekick |
|---|---|---|---|
| Google Chrome (Evergreen) | A: supportato | A: supportato | A: supportato |
| Microsoft Edge (Evergreen) | A: supportato | A: supportato | Z: non supportato |
| Mozilla Firefox (Evergreen) | A: supportato | A: supportato | Z: non supportato |
| Mozilla Firefox ESR [1] più recente | A: supportato | A: supportato | Z: non supportato |
| Safari su macOS (Evergreen) | A: supportato | A: supportato | Z: non supportato |
| Safari su iPadOS (evergreen) | Z: non supportato | A: supportato | Z: non supportato |

1. Supporto esteso per versione di Firefox ([ulteriori informazioni su mozilla.org](https://www.mozilla.org/it-IT/firefox/enterprise/))

>[!NOTE]
>
>**Supporto per browser con cicli di rilascio rapidi:**
>
>Gli aggiornamenti sulle versioni di Firefox, Chrome e Edge sono regolari. Adobe si impegna a mantenere il livello di supporto indicato in precedenza per le prossime versioni di questi browser.

## Browser supportati per i siti Web {#websites}

Il supporto browser per i siti Web sottoposti a rendering da AEM dipende dall’implementazione dei modelli di pagina, dei blocchi, della progettazione e dell’output dei componenti di AEM. Pertanto, gli sviluppatori che implementano il progetto hanno il controllo finale sulla compatibilità del sito.

Il [progetto standard AEM](https://www.aem.live/developer/ue-tutorial#create-github-project), i [componenti core](/help/implementing/developing/components/overview.md#aem-core-components) e il [sito di esempio WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) sono compatibili con tutti i browser moderni.
