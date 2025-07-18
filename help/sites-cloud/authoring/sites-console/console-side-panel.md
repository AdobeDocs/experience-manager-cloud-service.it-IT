---
title: Pannello laterale della console Sites
description: Scopri come utilizzare il pannello laterale nella console AEM Sites per comprendere e navigare meglio nel contenuto.
exl-id: 7f2571d6-b847-4cce-8e94-94ba0d2e04a5
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 45805d4baa8b93df2225b44152fee1457b421150
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 23%

---

# Pannello laterale della console Sites {#side-panel}

Scopri come utilizzare il pannello laterale nella console **Sites** di AEM per comprendere e navigare meglio nel contenuto.

## Orientamento {#orientation}

Per impostazione predefinita, il pannello laterale viene chiuso quando si accede alla console **Sites**. In questo modo lo schermo è interamente dedicato al tuo contenuto.

Tocca o fai clic sull&#39;icona **Pannello laterale** nella barra degli strumenti della console **Sites** per attivare il pannello laterale e scegliere la tua visualizzazione del contenuto.

* [Solo contenuto](#content-only)
* [Struttura contenuto](#content-tree)
* [Timeline](#timeline)
* [Riferimenti](#references)
* [Sito](#site)
* [Filtro](#filter)
* [Configurazione di Analytics](#setup-analytics)

![Visualizzazioni del pannello laterale della console Sites](assets/sites-console-side-panel-views.png)

La vista corrente selezionata è indicata da un segno di spunta blu nel menu a discesa e l’icona del pannello laterale nella barra degli strumenti viene aggiornata con il nome della vista selezionata.

## Solo contenuto {#content-only}

Questa visualizzazione del pannello laterale si disattiva in modo efficace, ovvero mostra solo il contenuto del sito.

>[!TIP]
>
>Utilizza la scelta rapida da tastiera `´` per evidenziare o mostrare il contenuto del pannello laterale.

## Struttura contenuto {#content-tree}

Questa vista del pannello laterale mostra il contenuto in una gerarchia ad albero. La struttura del contenuto può essere utilizzata per spostarsi rapidamente nella gerarchia del sito all’interno del pannello laterale e visualizzare molte informazioni sulle pagine nella cartella corrente.

![Visualizzazione struttura contenuto del pannello laterale](assets/console-side-panel-content-tree.png)

Una freccia rivolta a destra accanto a un elemento nella struttura indica un nodo che può essere espanso per rivelarne gli elementi secondari. Tocca o fai clic sulla freccia per visualizzare gli elementi secondari.

Nella console viene visualizzato il contenuto dell’elemento attualmente selezionato nella struttura del contenuto.

Utilizzando il pannello laterale della struttura del contenuto insieme a una vista a elenco o a schede, è possibile visualizzare facilmente la struttura gerarchica del progetto, spostarsi facilmente nella struttura del contenuto con il pannello laterale della struttura del contenuto e visualizzare informazioni di pagina dettagliate nella vista a elenco.

>[!TIP]
>
>* Utilizza la scelta rapida da tastiera `Alt+1` per passare alla visualizzazione struttura contenuto del pannello laterale.
>* Una volta selezionata una voce nella visualizzazione gerarchica, puoi spostarti rapidamente nella gerarchia attraverso i tasti freccia.
>* Per ulteriori informazioni, consulta [scelte rapide da tastiera](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md).

## Timeline {#timeline}

La timeline può essere utilizzata per visualizzare gli eventi che hanno interessato la risorsa selezionata. Puoi utilizzarlo anche per avviare determinati eventi, ad esempio flussi di lavoro o versioni.

![Dettagli Timeline](/help/sites-cloud/authoring/assets/timeline-detail.png)

Il pannello laterale **Timeline** consente di visualizzare vari eventi relativi a un elemento selezionato selezionabili come tipi da un elenco a discesa:

* Commenti
* [Annotazioni](/help/sites-cloud/authoring/page-editor/annotations.md)
* [Attività](/help/sites-cloud/authoring/personalization/activities.md)
* [Lanci](/help/sites-cloud/authoring/launches/overview.md)
* [Versioni](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md)
   * Non verranno visualizzate informazioni per i flussi di lavoro transitori poiché per tali flussi non vengono salvate informazioni sulla cronologia.<!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
* Mostra tutto

È inoltre possibile aggiungere o visualizzare commenti sull&#39;elemento selezionato utilizzando la casella **Commento** visualizzata in fondo all&#39;elenco degli eventi. Per registrare un commento, digitalo e premi `Return`. Per visualizzarlo, basta selezionare **Commenti** o **Mostra tutti**.

Nella console **Sites** puoi anche accedere a funzioni aggiuntive tramite il pulsante con i puntini di sospensione accanto al campo **Commento**.

* [Salvare una versione](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Avviare un flusso di lavoro](/help/sites-cloud/authoring/workflows/applying.md)

![Campo commento console Sites](assets/sites-console-comment-ellipsis.png)

>[!TIP]
>
>* Utilizza la scelta rapida da tastiera `Alt+2` per passare alla visualizzazione della timeline del pannello laterale.
>* Per ulteriori informazioni, consulta [scelte rapide da tastiera](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md).

## Riferimenti {#references}

La visualizzazione **Riferimenti** mostra un elenco di tipi di riferimenti a o da alla risorsa selezionata nella console.

![Dettagli riferimenti](assets/console-side-panel-references-detail.png)

Seleziona il tipo di riferimento adeguato per ulteriori informazioni. In determinate situazioni sono disponibili azioni ulteriori quando viene selezionato un riferimento specifico, inclusi:

* **Collegamenti in ingresso**, fornisce un elenco di pagine che fanno direttamente riferimento alla pagina selezionata, insieme all&#39;accesso diretto a **Modifica** una di queste pagine quando selezioni un collegamento specifico.
   * In questo modo vengono visualizzati solo i collegamenti statici, non quelli generati in modo dinamico, ad esempio dal componente Elenco.
* [Lanci](/help/sites-cloud/authoring/launches/overview.md): fornisce accesso ai lanci correlati.
* [Live Copy](/help/sites-cloud/administering/msm/overview.md) visualizza i percorsi di tutte le Live Copy basate sulla risorsa selezionata.
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md) fornisce dettagli e varie azioni
* [Copie per lingua](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel): fornisce dettagli e varie azioni

## Sito {#site}

La visualizzazione **Sito** del pannello laterale mostra i dettagli dei siti [creati utilizzando un modello di sito](/help/sites-cloud/administering/site-creation/create-site.md).

![Pannello del sito](assets/console-side-panel-site-paenl.png)

Per ulteriori informazioni su come utilizzare il pannello per gestire il [tema del sito](/help/sites-cloud/administering/site-creation/site-rail.md), consulta il documento [Utilizzo del pannello del sito per gestire il tema del sito](/help/sites-cloud/administering/site-creation/site-themes.md).

Se non hai ancora configurato la pipeline front-end per abilitare la creazione di siti basati su temi, il pannello laterale offrirà tale opzione.

![Opzione per abilitare la pipeline front-end nel pannello laterale](assets/sites-console-side-panel-site.png)

>[!TIP]
>
>Per una descrizione end-to-end del processo di creazione di un sito da un modello e personalizzazione del relativo tema, consulta [Percorso di creazione rapida dei siti](/help/journey-sites/quick-site/overview.md).

## Filtro {#filter}

Il pannello **Filtro** è simile alla [funzionalità di ricerca](/help/sites-cloud/authoring/search.md) con i filtri di posizione già impostati, che consentono di filtrare ulteriormente il contenuto da visualizzare.

![Esempio di filtro](assets/console-side-panel-filter.png)

A differenza di altre visualizzazioni del pannello laterale, per passare a un&#39;altra visualizzazione tocca o fai clic su `X` nel campo di ricerca.

## Configurazione di Analytics {#setup-analytics}

Questa vista consente di configurare rapidamente Adobe Analytics per un sito selezionato.

![Imposta analisi](assets/sites-console-side-panel-setup-analytics.png)
