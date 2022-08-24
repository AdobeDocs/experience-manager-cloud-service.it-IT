---
title: Console Frammenti di contenuto
description: Scopri come gestire i frammenti di contenuto dalla console Frammenti di contenuto.
landing-page-description: Scopri come gestire i frammenti di contenuto dalla console Frammenti di contenuto. La console è incentrata sull’utilizzo di volumi elevati di frammenti di contenuto per casi d’uso headless, ma viene utilizzata anche per l’authoring delle pagine.
exl-id: 0e6e3b61-a0ca-44b8-914d-336e29761579
source-git-commit: 99e3c07f8376859692db41c633bfaa602ed65358
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Console Frammenti di contenuto  {#content-fragments-console}

Scopri in che modo la console Frammenti di contenuto può ottimizzare l’accesso ai frammenti di contenuto, consentendoti di creare, cercare e gestire i frammenti eseguendo azioni amministrative quali pubblicare, annullare le pubblicazioni e copiare.

La console Frammenti di contenuto è dedicata a gestione, ricerca e creazione di frammenti di contenuto. È stata ottimizzata per l’utilizzo in un contesto headless, ma anche durante la creazione di frammenti di contenuto da usare nell’authoring delle pagine.

>[!NOTE]
>
>In questa console vengono visualizzati solo i frammenti di contenuto. Non visualizza altri tipi di risorse, come immagini e video.

>[!NOTE]
>
>L’accesso ai frammenti di contenuto attualmente è possibile tramite:
>
>* la presente console di **Frammenti di contenuto**;
>* la console **Assets** - vedi [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md).


>[!NOTE]
>
>Selezione di [in questa console sono disponibili scelte rapide da tastiera](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md).

È possibile accedere direttamente alla console Frammenti di contenuto dal livello superiore della navigazione globale:

![Navigazione globale - Console Frammenti di contenuto](assets/cfc-global-navigation.png)

Selezionando **Frammenti di contenuto** verrà aperta la console in una nuova scheda.

![Console Frammenti di contenuto - Panoramica](assets/cfc-console-overview.png)

Nella console puoi osservare tre aree principali:

* Barra degli strumenti superiore
   * Fornisce le funzionalità standard di AEM
   * Mostra anche la tua organizzazione IMS
* Pannello a sinistra
   * Qui puoi nascondere o visualizzare la struttura delle cartelle
   * Puoi selezionare un ramo specifico della struttura
* Pannello principale/destro; da qui puoi:
   * Visualizzare l’elenco di tutti i frammenti di contenuto nel ramo selezionato della struttura
      * La posizione è indicata dalle breadcrumb; puoi utilizzarle anche per modificare la posizione
      * Verranno visualizzati i frammenti di contenuto della cartella selezionata e tutte le cartelle secondarie
         * Vari campi di informazioni su un frammento di contenuto includono collegamenti che possono aprire il frammento appropriato nell’editor
      * Puoi selezionare un’intestazione di colonna per ordinare la tabella in base a tale colonna; selezionala ancora per passare da ordine crescente a decrescente
   * **[Creare](#creating-new-content-fragment)** un nuovo frammento di contenuto
   * [Filtrare](#filtering-fragments) i frammenti di contenuto in base a una selezione di predicati e salvare il filtro per utilizzi futuri
   * [Ricercare](#searching-fragments) i frammenti di contenuto
   * Personalizzare la vista tabella per mostrare le colonne di informazioni selezionate
   * Utilizzare **Apri in Assets** per aprire direttamente la posizione corrente nella console **Assets**.

      >[!NOTE]
      >
      >La console **Assets** viene utilizzata per accedere alle risorse, ad esempio immagini, video e così via.  È possibile accedere a questa console:
      >
      >* utilizzando il collegamento **Apri in Assets** (nella console Frammenti di contenuto);
      >* direttamente dal riquadro di navigazione globale.


Quando si seleziona un frammento specifico, viene aperta una barra degli strumenti incentrata sulle azioni disponibili per tale frammento. Puoi inoltre selezionare più frammenti; la selezione delle azioni verrà regolata di conseguenza.

![Console Frammenti di contenuto; barra degli strumenti per un frammento selezionato](assets/cfc-fragment-toolbar.png)

## Creazione di un nuovo frammento di contenuto {#creating-new-content-fragment}

Selezionando **Crea** consente di aprire la compatta finestra di dialogo **Nuovo frammento di contenuto**:

![Console Frammenti di contenuto - Creazione di un nuovo frammento](assets/cfc-console-create.png)

## Filtrare i frammenti {#filtering-fragments}

Il pannello Filtro offre:

* una selezione di predicati che possono essere selezionati e combinati;
* l’opportunità di salvare la configurazione mediante il comando **Salva**.
* l’opzione di recuperare un filtro di ricerca salvato per il riutilizzo.

![Console Frammenti di contenuto - Filtro](assets/cfc-console-filter.png)

## Ricerca di frammenti {#searching-fragments}

La casella di ricerca supporta la ricerca full-text. Immetti i termini di ricerca nella casella di ricerca:

![Console Frammenti di contenuto - Ricerca](assets/cfc-console-search-01.png)

Fornirà i risultati selezionati:

![Console Frammenti di contenuto - Risultati della ricerca](assets/cfc-console-search-02.png)

La casella di ricerca consente inoltre di accedere rapidamente a **Frammenti di contenuto recenti** e **Ricerche salvate**:

![Console Frammenti di contenuto - Recenti e salvati](assets/cfc-console-search-03.png)
