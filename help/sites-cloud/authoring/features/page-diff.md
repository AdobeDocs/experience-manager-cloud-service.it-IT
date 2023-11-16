---
title: Differenze tra pagine
description: È possibile confrontare in modalità affiancata i contenuti di due pagine, evidenziandone le differenze rilevate.
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 89%

---

# Differenze tra pagine  {#page-diff}

## Introduzione {#introduction}

La creazione dei contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. La visualizzazione separata di due versioni di una pagina è inefficiente e soggetta a errori. L’autore desidera poter confrontare facilmente la pagina corrente affiancata a un’altra sua versione.

È possibile confrontare in modalità affiancata i contenuti di due pagine, evidenziandone le differenze rilevate.

>[!NOTE]
>
>Per utilizzare questa funzione, l’utente deve disporre dell’autorizzazione **Modifica/Crea/Elimina** sul nodo `/content/versionhistory`.
>
>Per ulteriori informazioni tecniche su questa funzione, consulta [Sviluppo e differenze tra pagine](/help/implementing/developing/introduction/page-diff.md#operation-details).

## Utilizzare {#use}

La visualizzazione affiancata delle differenze permette di confrontare:

* [Versioni](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page) - Versione precedente di una pagina con il relativo stato corrente
* [live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md#comparing-a-live-copy-page-with-a-blueprint-page) - Live Copy con la relativa blueprint
* [Lanci](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page) - Lancio con la rispettiva sorgente
* [Copie per lingua](/help/sites-cloud/administering/translation/managing-projects.md#comparing-language-copies) - Una pagina prima e dopo la traduzione o la ritraduzione

Consulta i rispettivi argomenti su come avviare la funzione per il rilevamento delle differenze all’interno di questi contesti.

### Presentazione delle differenze   {#presentation-of-differences}

Indipendentemente dal contenuto confrontato, la presentazione della differenza rimane la stessa.

* Il contenuto selezionato all’avvio della funzione per il rilevamento delle differenze viene visualizzato a sinistra (il punto di ingresso).
* Il contenuto con cui viene confrontato viene visualizzato a destra (rispetto a cosa viene confrontato il contenuto selezionato).

Ad esempio, se si confrontano le versioni, la versione corrente viene visualizzata a sinistra e la versione precedente a destra.

L’origine di entrambe le pagine viene visualizzata in modo chiaro nella barra dell’intestazione nella parte superiore della finestra del browser.

![Versioni affiancate](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

La differenza rileva le modifiche apportate a livello di componente e HTML. Gli elementi che sono stati modificati sono evidenziati con colori diversi.

**Modifiche ai componenti**

* Verde chiaro: componente aggiunto
* Rosa: componente rimosso

**Modifiche HTML**

* Verde scuro: HTML aggiunto
* Rosso - HTML rimosso

>[!NOTE]
>
>Quando si confrontano le copie per lingua, l’evidenziazione viene disattivata in quanto in una traduzione cambia tutto e l’evidenziazione non avrebbe alcun vantaggio.

### Modalità a schermo intero e Uscita   {#fullscreen-and-exiting}

Per concentrarti su un contenuto particolare, puoi fare clic sull’icona a schermo intero di entrambi i &quot;lati&quot; di side-by-side diff (differenze affiancate) per ingrandirla fino alla finestra del browser completa.

![Pulsante Schermo intero](/help/sites-cloud/authoring/assets/versions-full-screen.png)

Il lato selezionato occupa l’intera finestra, ma nella parte superiore rimane visualizzata la barra che consente di alternare tra le due pagine.

![Modalità a tutto schermo](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>Se la larghezza del browser non supporta entrambi i nomi di pagina nella visualizzazione a schermo intero, viene visualizzato solo il nome della pagina visualizzata e dietro i puntini di sospensione viene visualizzato l’altro nome.

Per chiudere la visualizzazione a schermo intero, fai clic sull’icona per uscire dalla modalità a tutto schermo.

![Esci da modalità a schermo intero](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

Puoi uscire dalla modalità di confronto affiancato delle differenze in qualsiasi momento facendo clic sul pulsante Chiudi, nell’intestazione.

## Limiti   {#limitations}

In alcune situazioni, il confronto delle differenze della pagina potrebbe non essere in grado di rilevare una differenza nel modo previsto.

* Quando si confrontano versioni e lanci, la funzione non tiene conto dei componenti dinamici come breadcrumb, menu, elenchi di prodotti o loghi (componenti che si basano sulla struttura del sito per eseguire rendering del contenuto).
* Per le versioni, non viene ricreato il criterio per il controllo degli accessi e le relazioni Live Copy.
* Se una pagina viene spostata, non sarà più possibile eseguire una rilevazione delle differenze con qualsiasi versione creata prima dello spostamento.
   * Se riscontri problemi con un confronto, controlla la [Timeline](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) per la pagina per verificare se la pagina è stata spostata.

>[!NOTE]
>
>Le versioni non possono essere confrontate tra loro. Solo la versione corrente può essere confrontata con altre versioni della pagina. La versione corrente è sempre la versione con le modifiche evidenziate.

>[!NOTE]
>
>Per ulteriori informazioni sul funzionamento del meccanismo di confronto tra pagine e sui limiti che possono influenzare tale meccanismo, consulta la [documentazione per gli sviluppatori](/help/implementing/developing/introduction/page-diff.md) relativa a questa funzione.
