---
title: Piattaforme client supportate
description: Scopri quali browser sono supportati per la creazione di contenuti con Adobe Experience Manager as a Cloud Service e l’accesso ai siti pubblicati con AEM.
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 7ddd0a75-621a-4499-91d1-7b3408a68269
source-git-commit: e57610e4c5e498ddfdbaa0ba39c9197ecfb5d177
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 3%

---

# Piattaforme client supportate {#supported-platforms}

Scopri quali browser sono supportati per la creazione di contenuti con Adobe Experience Manager as a Cloud Service e l’accesso ai siti pubblicati con AEM.

>[!TIP]
>
>Questo documento descrive le piattaforme client supportate da AEM as a Cloud Service. Per informazioni dettagliate sull&#39;ambiente di build per lo sviluppo del progetto AEM, consulta il documento [Ambiente di build.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)

## Livelli di supporto {#support-levels}

Adobe definisce i seguenti livelli di supporto per le piattaforme client di AEM.

| Livello di supporto | Descrizione |
|---|---|
| R: Supportato | Adobe fornisce supporto e manutenzione completi per questa configurazione. Questa configurazione è coperta dal processo di controllo qualità di Adobe. |
| R: Supporto limitato | Il supporto richiede una richiesta formale ad Adobe per utilizzare la configurazione in un progetto. Una volta confermato da Adobe, Adobe fornisce il supporto completo all’interno del programma di supporto limitato. Per ulteriori informazioni, contatta l’Assistenza clienti di Adobe. |
| Z: non supportato | Configurazione non supportata. Adobe non fornisce istruzioni sul funzionamento o meno della configurazione e non la supporta. |

## Browser supportati per l’authoring dei contenuti {#authoring}

L’interfaccia utente di AEM è ottimizzata per schermi più grandi presenti in notebook, computer desktop e dispositivi tablet (come Apple iPad o Microsoft Surface). Il fattore di forma telefono non è supportato per nessun caso d’uso di authoring.

L&#39;interfaccia utente di Adobe Experience Manager funziona con le seguenti piattaforme client a seconda del metodo di authoring [.](/help/edge/overview.md#authoring-method)

* [Editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [Editor pagina](/help/sites-cloud/authoring/page-editor/introduction.md)
* [Authoring basato su documenti](/help/edge/docs/authoring.md) con [Sidekick](/help/edge/docs/sidekick.md)

Tutti i browser vengono testati con il set predefinito di plug-in e componenti aggiuntivi.

| Browser | Livello di supporto dell’editor universale | Livello di supporto dell’Editor pagina | Livello di supporto Sidekick |
|---|---|---|---|
| Google Chrome (sempreverde) | R: Supportato | R: Supportato | R: Supportato |
| Microsoft Edge (evergreen) | R: Supportato | R: Supportato | Z: non supportato |
| Mozilla Firefox (sempreverde) | R: Supportato | R: Supportato | Z: non supportato |
| Mozilla Firefox più recente ESR [1] | R: Supportato | R: Supportato | Z: non supportato |
| Safari su macOS (evergreen) | R: Supportato | R: Supportato | Z: non supportato |
| Safari su iOS (sempreverde) [2] | Z: non supportato | R: Supportato | Z: non supportato |

1. Supporto esteso per Firefox ([ulteriori informazioni su mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/))
1. Supporto solo per Apple iPad

>[!NOTE]
>
>**Supporto per browser con cicli di rilascio rapidi:**
>
>Gli aggiornamenti sulle versioni di Firefox, Chrome e Edge sono regolari. Adobe si impegna a mantenere il livello di supporto indicato sopra per le prossime versioni di questi browser.

## Browser supportati per i siti Web {#websites}

Il supporto browser per i siti web sottoposti a rendering da AEM dipende dall’implementazione dei modelli di pagina, dei blocchi, della progettazione e dell’output dei componenti di AEM. Pertanto, gli sviluppatori che implementano il progetto hanno il controllo finale sulla compatibilità del sito.

Il [progetto standard di AEM,](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md#create-github-project) [Componenti core,](/help/implementing/developing/components/overview.md#aem-core-components) e il [sito di esempio WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) sono tutti compatibili con tutti i browser moderni.
