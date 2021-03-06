---
title: Design reattivo
description: Con il design reattivo, le stesse esperienze possono essere visualizzate in modo efficace su più dispositivi con più orientamenti
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Design reattivo {#responsive-design}

Progetta le tue esperienze in modo che si adattino al riquadro di visualizzazione client in cui vengono visualizzate. Con il design reattivo, le stesse pagine possono essere visualizzate in modo efficace su più dispositivi in entrambi gli orientamenti. L&#39;immagine seguente illustra alcuni modi in cui una pagina può rispondere ai cambiamenti nelle dimensioni del riquadro di visualizzazione:

* Layout: Utilizza layout a colonne singola per riquadri di visualizzazione più piccoli e layout a più colonne per riquadri di visualizzazione più grandi.
* Dimensioni testo: Utilizzare dimensioni di testo più grandi (se appropriato, ad esempio titoli) nei riquadri di visualizzazione più grandi.
* Contenuto: Includi solo il contenuto più importante quando viene visualizzato su dispositivi più piccoli.
* Navigazione: Sono disponibili strumenti specifici per il dispositivo per accedere ad altre pagine.
* Immagini: Distribuzione di rappresentazioni di immagini appropriate per il riquadro di visualizzazione client in base alle dimensioni della finestra.

![Esempi di design reattivo](assets/responsive-example.png)

Sviluppa applicazioni Adobe Experience Manager (AEM) che generano HTML5 adattabili a diverse dimensioni e orientamenti delle finestre. Ad esempio, i seguenti intervalli di larghezze di visualizzazione corrispondono a vari tipi di dispositivi e orientamenti

* Larghezza massima di 480 pixel (telefono, verticale)
* Larghezza massima di 767 pixel (telefono, orizzontale)
* Larghezza tra 768 pixel e 979 pixel (tablet, ritratto)
* Larghezza tra 980 pixel e 1199 pixel (tablet, orizzontale)
* Larghezza uguale o superiore a 1200 px (desktop)

Per informazioni sull’implementazione di un comportamento di progettazione reattiva, consulta i seguenti argomenti:

* [Query multimediali](#using-media-queries)
* [Griglie fluide](#developing-a-fluid-grid)
* [Immagini adattive](#using-adaptive-images)

Durante la progettazione, utilizza il **Emulatore** per visualizzare in anteprima le pagine per diverse dimensioni dello schermo.

## Prima di sviluppare {#before-you-develop}

Prima di sviluppare l’applicazione AEM che supporta le pagine web, è necessario prendere diverse decisioni di progettazione. Ad esempio, è necessario disporre delle seguenti informazioni:

* I dispositivi di destinazione
* Dimensioni del riquadro di visualizzazione di destinazione
* Layout di pagina per ciascuna dimensione del riquadro di visualizzazione di destinazione

### Struttura dell&#39;applicazione {#application-structure}

La tipica struttura dell&#39;applicazione AEM supporta tutte le implementazioni di progettazione reattiva:

* I componenti della pagina si trovano sotto `/apps/<application_name>/components`
* I modelli si trovano sotto `/apps/<application_name>/templates`

## Utilizzo di query multimediali {#using-media-queries}

Le query multimediali abilitano l’uso selettivo degli stili CSS per il rendering della pagina. Gli strumenti e le funzioni di sviluppo AEM consentono di implementare in modo efficace ed efficiente le query multimediali nelle applicazioni.

Il gruppo W3C fornisce [Query multimediali](https://www.w3.org/TR/css3-mediaqueries/) consiglio che descrive questa funzione CSS3 e la sintassi.

### Creazione del file CSS {#creating-the-css-file}

Nel file CSS, definisci le query multimediali in base alle proprietà dei dispositivi di destinazione. La seguente strategia di implementazione è efficace per gestire gli stili per ogni query multimediale:

* Utilizza un [Cartella Libreria client](clientlibs.md) per definire il CSS che viene assemblato quando viene eseguito il rendering della pagina.
* Definisci ogni query multimediale e gli stili associati in file CSS separati. È utile utilizzare nomi di file che rappresentano le caratteristiche del dispositivo della query multimediale.
* Definisci gli stili comuni a tutti i dispositivi in un file CSS separato.
* Nel file css.txt della cartella Libreria client, ordinate i file CSS dell&#39;elenco come richiesto nel file CSS assemblato.

La [Esercitazione WKND](develop-wknd-tutorial.md) utilizza questa strategia per definire gli stili nella progettazione del sito. Il file CSS utilizzato da WKND si trova in `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.
