---
title: 'Differenze tra pagine '
description: È possibile confrontare in modalità affiancata i contenuti di due pagine, evidenziandone le differenze rilevate.
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 97%

---

# Differenze tra pagine  {#page-diff}

## Introduzione {#introduction}

La creazione di contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. La visualizzazione separata di due versioni di una pagina è inefficiente e soggetta a errori. L’autore desidera poter confrontare facilmente la pagina corrente affiancata a un’altra sua versione.

È possibile confrontare in modalità affiancata i contenuti di due pagine, evidenziandone le differenze rilevate.

>[!NOTE]
>
>Per utilizzare questa funzione, l’utente deve disporre dell’autorizzazione **Modifica/Crea/Elimina** sul nodo `/content/versionhistory`.
>
>Per ulteriori informazioni tecniche su questa funzione, consulta [Sviluppo e differenze tra pagine](/help/implementing/developing/introduction/page-diff.md#operation-details).

## Utilizzo {#use}

La visualizzazione affiancata delle differenze permette di confrontare:

* [Versioni](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page) - Versione precedente di una pagina con il relativo stato corrente
* [](/help/sites-cloud/administering/msm/creating-live-copies.md#comparing-a-live-copy-page-with-a-blueprint-page)Live Copy - Live Copy con la relativa blueprint
* [Lanci](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page) - Lancio con la rispettiva origine
* [](/help/sites-cloud/administering/translation/managing-projects.md#comparing-language-copies)Copie per lingua - Una pagina prima e dopo la traduzione o la ritraduzione

Consulta i rispettivi argomenti su come avviare la funzione per il rilevamento delle differenze in questi contesti.

### Presentazione delle differenze   {#presentation-of-differences}

A prescindere dal contenuto, la presentazione delle differenze rimane la stessa.

* Il contenuto selezionato viene visualizzato a sinistra (punto di ingresso per il rilevamento delle differenze).
* Il contenuto con cui viene confrontato è visualizzato a destra.

Ad esempio, se si confrontano due versioni, la versione corrente è a sinistra e quella precedente a destra.

L’origine di entrambe le pagine è indicata chiaramente nella barra dell’intestazione, nella parte superiore della finestra del browser.

![Versioni affiancate](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

Vengono rilevate le modifiche apportate a livello di componente e di codice HTML. Gli elementi che sono stati modificati sono evidenziati con colori diversi.

**Modifica componenti**

* Verde chiaro - Componente aggiunto
* Rosa - Componente rimosso

**Modifiche HTML**

* Verde scuro - HTML aggiunto
* Rosso - HTML rimosso

>[!NOTE]
>
>Quando si confrontano le copie per lingua, l’evidenziazione è disattivata poiché in una traduzione tutto cambia.

### Modalità a schermo intero e Uscita   {#fullscreen-and-exiting}

Per concentrarti su un contenuto particolare, fai clic sull’icona schermo intero di entrambi i “lati” a confronto, per ingrandire il contenuto nella finestra del browser a schermo intero.

![Pulsante Schermo intero](/help/sites-cloud/authoring/assets/versions-full-screen.png)

Il lato selezionato occupa l’intera finestra, ma nella parte superiore rimane visualizzata la barra che consente di alternare tra le due pagine.

![Modalità a tutto schermo](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>Se la finestra del browser è sufficientemente ampia da contenere entrambi i nomi di pagina nella visualizzazione a schermo intero, verrà visualizzato solo il nome della pagina visualizzata. Per visualizzare il nome dell’altra pagina, basta fare clic sui puntini di sospensione.

Per chiudere la visualizzazione a schermo intero, fai clic sull’icona per uscire dalla modalità a tutto schermo.

![Esci da modalità a schermo intero](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

Puoi uscire dalla modalità di confronto affiancato delle differenze in qualsiasi momento facendo clic sul pulsante Chiudi, nell’intestazione.

## Limiti   {#limitations}

Esistono alcune situazioni in cui il confronto delle differenze della pagina non è in grado di rilevare una differenza nel modo previsto.

* Nel confronto di versioni e lanci, la funzione non prende in considerazione le differenze dinamiche, come i componenti breadcrumb, i menu, gli elenchi di prodotti o i loghi (componenti che si basano sulla struttura del sito per eseguire il rendering del contenuto).
* Per le versioni, la differenza non ricrea i criteri di controllo accessi e le relazioni Live Copy.
* Se una pagina viene spostata, non ti sarà più possibile eseguire una rilevazione delle differenze con qualsiasi versione creata prima dello spostamento.
   * Se rilevi dei problemi con una differenza, controlla la [Timeline](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) per verificare se la pagina è stata spostata.

>[!NOTE]
>
>Le versioni non possono essere confrontate tra di loro. Solo la versione corrente può essere confrontata con altre versioni della pagina. La versione corrente è sempre la versione con le modifiche evidenziate.

>[!NOTE]
>
>Per ulteriori informazioni sull’operazione del meccanismo di differenze tra pagine e sui limiti che possono influenzare tale meccanismo, consulta la [documentazione per gli sviluppatori](/help/implementing/developing/introduction/page-diff.md) per questa funzione.
