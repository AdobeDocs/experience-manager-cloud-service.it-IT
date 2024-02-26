---
title: Pannello laterale della console Sites
description: Scopri come utilizzare il pannello laterale nella console dei siti AEM per comprendere e navigare meglio nel contenuto.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 23%

---


# Pannello laterale della console Sites {#side-panel}

Scopri come utilizzare il pannello laterale nell’AEM **Sites** per comprendere e navigare meglio nel contenuto.

## Orientamento {#orientation}

Per impostazione predefinita, il pannello laterale viene chiuso quando si immette **Sites** console. In questo modo lo schermo è interamente dedicato al tuo contenuto.

Tocca o fai clic su **Pannello laterale** icona in **Sites** barra degli strumenti della console per attivare il pannello laterale e scegliere la visualizzazione del contenuto.

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
>Utilizza l’accento grave/contrassegno `´` scelta rapida da tastiera per passare alla visualizzazione solo contenuto del pannello laterale.

## Struttura contenuto {#content-tree}

Questa vista del pannello laterale mostra il contenuto in una gerarchia ad albero. La struttura del contenuto può essere utilizzata per spostarsi rapidamente nella gerarchia del sito all’interno del pannello laterale e visualizzare molte informazioni sulle pagine nella cartella corrente.

![Visualizzazione struttura contenuto del pannello laterale](assets/console-side-panel-content-tree.png)

Una freccia rivolta a destra accanto a un elemento nella struttura indica un nodo che può essere espanso per rivelarne gli elementi secondari. Tocca o fai clic sulla freccia per visualizzare gli elementi secondari.

Nella console viene visualizzato il contenuto dell’elemento attualmente selezionato nella struttura del contenuto.

Utilizzando il pannello laterale della struttura del contenuto insieme a una vista a elenco o a schede, è possibile visualizzare facilmente la struttura gerarchica del progetto, spostarsi facilmente nella struttura del contenuto con il pannello laterale della struttura del contenuto e visualizzare informazioni di pagina dettagliate nella vista a elenco.

>[!TIP]
>
>* Utilizza il `Alt+1` scelta rapida da tastiera per passare alla visualizzazione struttura contenuto del pannello laterale.
>* Una volta selezionata una voce nella visualizzazione gerarchica, puoi spostarti rapidamente nella gerarchia attraverso i tasti freccia.
>* Per ulteriori informazioni, consulta [scelte rapide da tastiera](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md).

## Timeline {#timeline}

La timeline può essere utilizzata per visualizzare gli eventi che hanno interessato la risorsa selezionata. Puoi utilizzarlo anche per avviare determinati eventi, ad esempio flussi di lavoro o versioni.

![Dettagli Timeline](/help/sites-cloud/authoring/assets/timeline-detail.png)

Il **Timeline** il pannello laterale consente di visualizzare vari eventi relativi a un elemento selezionato selezionabili come tipi da un elenco a discesa:

* Commenti
* [Annotazioni](/help/sites-cloud/authoring/page-editor/annotations.md)
* [Attività](/help/sites-cloud/authoring/personalization/activities.md)
* [Lanci](/help/sites-cloud/authoring/launches/overview.md)
* [Versioni](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md)
   * Tieni presente che non verranno visualizzate informazioni per i flussi di lavoro transitori, in quanto per tali flussi non vengono salvate informazioni sulla cronologia.<!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
* Mostra tutto

È inoltre possibile aggiungere o visualizzare commenti sull&#39;elemento selezionato utilizzando **Commento** nella parte inferiore dell’elenco degli eventi. Digita un commento seguito da `Return` registrerà il commento. Per visualizzarlo, basta selezionare **Commenti** o **Mostra tutti**.

In **Sites** console è inoltre possibile accedere a funzioni aggiuntive tramite il pulsante con i puntini di sospensione accanto al **Commento** campo.

* [Salvare una versione](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Avviare un flusso di lavoro](/help/sites-cloud/authoring/workflows/applying.md)

![Campo commento della console Sites](assets/sites-console-comment-ellipsis.png)

>[!TIP]
>
>* Utilizza il `Alt+2` scelta rapida da tastiera per passare alla vista timeline del pannello laterale.
>* Per ulteriori informazioni, consulta [scelte rapide da tastiera](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md).

## Riferimenti {#references}

Il **Riferimenti** visualizza mostra un elenco di tipi di riferimenti alla risorsa selezionata nella console o da essa.

![Dettagli riferimenti](assets/console-side-panel-references-detail.png)

Seleziona il tipo di riferimento adeguato per ulteriori informazioni. In determinate situazioni sono disponibili azioni ulteriori quando viene selezionato un riferimento specifico, inclusi:

* **Collegamenti in ingresso**, fornisce un elenco di pagine che fanno riferimento alla pagina e accesso diretto a **Modifica** una di queste pagine quando selezioni un collegamento specifico.
   * Questo può mostrare solo collegamenti statici, non collegamenti generati dinamicamente come dal componente Elenco.
* [Lanci](/help/sites-cloud/authoring/launches/overview.md): fornisce accesso ai lanci correlati.
* [Live Copy](/help/sites-cloud/administering/msm/overview.md) visualizza i percorsi di tutte le Live Copy basate sulla risorsa selezionata.
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md) fornisce dettagli e varie azioni
* [Copie per lingua](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel): fornisce dettagli e varie azioni

## Sito {#site}

Il **Sito** la visualizzazione del pannello laterale mostra i dettagli dei siti [creato utilizzando un modello di sito.](/help/sites-cloud/administering/site-creation/create-site.md)

![Pannello Sito](assets/console-side-panel-site-paenl.png)

Consulta il documento [Utilizzo del pannello Sito per gestire il tema del sito](/help/sites-cloud/administering/site-creation/site-rail.md) per ulteriori dettagli su come utilizzare il pannello per gestire [tema del sito.](/help/sites-cloud/administering/site-creation/site-themes.md).

Se non hai ancora configurato la pipeline front-end per abilitare la creazione di siti basati su temi, il pannello laterale offrirà tale opzione.

![Opzione per abilitare la pipeline front-end nel pannello laterale](assets/sites-console-side-panel-site.png)

>[!TIP]
>
>Per una descrizione end-to-end del processo di creazione di un sito da un modello e personalizzazione del relativo tema, vedi [Percorso di Creazione Rapida dei Siti.](/help/journey-sites/quick-site/overview.md)

## Filtro {#filter}

Il **Filtro** è simile al pannello [funzione di ricerca](/help/sites-cloud/authoring/search.md) con i filtri di posizione appropriati già impostati, che consentono di filtrare ulteriormente il contenuto da visualizzare.

![Esempio di filtro](assets/console-side-panel-filter.png)

A differenza di altre viste del pannello laterale, per passare a un’altra vista tocca o fai clic sul pulsante `X` nel campo di ricerca.

## Configurazione di Analytics {#setup-analytics}

Questa vista consente di configurare rapidamente Adobe Analytics per un sito selezionato.

![Configurazione analisi](assets/sites-console-side-panel-setup-analytics.png)
