---
title: Ricerca
description: Individua il contenuto più velocemente con funzionalità complete di ricerca
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 83%

---

# Ricerca   {#search-feature}

L’ambiente di authoring di AEM offre vari metodi per la ricerca dei contenuti, a seconda del tipo di risorsa.

## Informazioni di base sulla ricerca {#search-basics}

La funzione Ricerca è disponibile nella barra degli strumenti superiore:

![Icona Ricerca](/help/sites-cloud/authoring/assets/search-icon.png)

La barra di ricerca consente di effettuare le seguenti operazioni:

* Cercare una parola chiave, un percorso o un tag specifico
* Filtra in base a criteri specifici per le risorse, ad esempio date di modifica, stato della pagina, dimensione del file e così via.
* Definire e utilizzare una [ricerca salvata](#saved-searches) in base ai criteri impostati

>[!NOTE]
>
>La ricerca può anche essere avviata mediante il tasto di scelta rapida `/` (barra) ogni volta che la barra di ricerca è visibile.

## Ricerca e filtro {#search-and-filter}

Per cercare e filtrare le risorse:

1. Apri la **Ricerca** (con la lente di ingrandimento nella barra degli strumenti) e immetti il termine da cercare. Vengono forniti suggerimenti che possono essere selezionati:

   ![Ricerca termine](/help/sites-cloud/authoring/assets/search-term.png)

   Per impostazione predefinita, i risultati della ricerca sono limitati alla posizione corrente (ovvero alla console e al tipo di risorsa corrispondente):

   ![Ricerca per posizione](/help/sites-cloud/authoring/assets/search-term-location.png)

1. Se necessario, è possibile rimuovere il filtro località (selezionare **X** sul filtro che si desidera rimuovere) per eseguire ricerche in tutte le console/i tipi di risorse.
1. I risultati visualizzati vengono raggruppati in base alla console e al tipo di risorsa corrispondente.

   È possibile selezionare una risorsa specifica (per ulteriori azioni) oppure eseguire il drill-down selezionando il tipo di risorsa richiesto, ad esempio **Visualizza tutti i siti**:

   ![Risultati di ricerca](/help/sites-cloud/authoring/assets/search-results.png)

1. Per approfondire la ricerca, seleziona il simbolo della barra laterale (in alto a sinistra) per aprire il pannello laterale **Filtri e opzioni**.

   ![Pulsante della barra](/help/sites-cloud/authoring/assets/rail-button.png)

   A seconda del tipo di risorsa, nella finestra di ricerca viene visualizzata una selezione predefinita di criteri di ricerca/filtro.

   Il pannello laterale consente di selezionare:

   * Ricerche salvate
   * Directory di ricerca
   * Tag
   * Criteri di ricerca, ad esempio Date modificate, Stato Publish, Stato LiveCopy

   >[!NOTE]
   >
   >I criteri di ricerca possono variare:
   >
   >* A seconda del tipo di risorsa selezionato; ad esempio, i criteri di Risorse e Community sono chiaramente specifici.
   >* La tua istanza, nonché i moduli di ricerca, possono essere personalizzati (in base alla posizione all’interno di AEM).

<!--
  >* Your instance as the [Search Forms](/help/sites-administering/search-forms.md) can be customized (appropriate to the location within AEM).
  -->

![Pannello laterale di ricerca](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. Puoi anche aggiungere altri termini di ricerca.

1. Per chiudere la **Ricerca**, utilizza la **X** in alto a destra.

>[!NOTE]
>
>I criteri di ricerca vengono mantenuti quando selezioni un elemento nei risultati di ricerca.
>
>Quando selezioni un elemento nella pagina dei risultati, e quindi torni alla pagina di ricerca dopo avere utilizzato il pulsante indietro del browser, i criteri di ricerca rimangono.

## Ricerche salvate {#saved-searches}

Oltre a eseguire ricerche in base a un’ampia gamma di facet, puoi anche salvare una particolare configurazione di ricerca per riutilizzarla in una fase successiva:

1. Definisci i criteri di ricerca e seleziona **Salva**.

   ![Salvataggio di una ricerca](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. Assegna un nome e seleziona **Salva** per confermare:

   ![Salvataggio di una ricerca con un nome](/help/sites-cloud/authoring/assets/search-save-name.png)

1. La ricerca salvata è disponibile nel selettore alla successiva apertura del pannello di ricerca:

   ![Ricerche salvate](/help/sites-cloud/authoring/assets/saved-searches.png)

1. Una volta salvato, è possibile:

   * Utilizza **x** (rispetto al nome della ricerca salvata) per avviare una nuova query (la ricerca salvata stessa non verrà eliminata).
   * **Modifica ricerca salvata**, modifica le condizioni di ricerca, quindi **Salva** di nuovo.

Per modificare le ricerche salvate, seleziona una ricerca e fai clic sull’opzione **Modifica ricerca salvata** nella parte inferiore del pannello di ricerca.

![Modifica di una ricerca salvata](/help/sites-cloud/authoring/assets/saved-searches-modify.png)
