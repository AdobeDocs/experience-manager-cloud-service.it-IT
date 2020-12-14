---
title: Design reattivo
description: Con un design reattivo, le stesse esperienze possono essere visualizzate in modo efficace su più dispositivi con orientamenti multipli
translation-type: tm+mt
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Design reattivo {#responsive-design}

Progettate le esperienze in modo che si adattino alla vista client in cui vengono visualizzate. Con la progettazione reattiva, le stesse pagine possono essere visualizzate su più dispositivi in entrambi gli orientamenti. L&#39;immagine seguente illustra alcuni modi in cui una pagina può rispondere alle modifiche nelle dimensioni della finestra:

* Layout: Utilizzate i layout a colonna singola per le finestre più piccole e i layout a più colonne per le finestre più grandi.
* Dimensione testo: Utilizzate dimensioni di testo maggiori (se appropriato, come le intestazioni) nelle finestre più grandi.
* Contenuto: Includete solo il contenuto più importante per la visualizzazione su dispositivi più piccoli.
* Navigazione: Sono disponibili strumenti specifici per dispositivi per accedere ad altre pagine.
* Immagini: Trasmissione di rappresentazioni di immagini adatte alla visualizzazione client in base alle dimensioni della finestra.

![Esempi di design reattivo](assets/responsive-example.png)

Sviluppare applicazioni Adobe Experience Manager (AEM) che generano HTML5 adattabili a diverse dimensioni e orientamenti delle finestre. Ad esempio, i seguenti intervalli di larghezze di visualizzazione corrispondono a vari tipi di dispositivi e orientamenti

* Larghezza massima di 480 pixel (telefono, verticale)
* Larghezza massima di 767 pixel (telefono, orizzontale)
* Larghezza tra 768 pixel e 979 pixel (tablet, verticale)
* Larghezza tra 980 pixel e 1199 pixel (tablet, orizzontale)
* Larghezza uguale o superiore a 1200 px (desktop)

Per informazioni sull’implementazione di comportamenti di progettazione reattivi, consultate i seguenti argomenti:

* [Media query](#using-media-queries)
* [Griglie fluide](#developing-a-fluid-grid)
* [Immagini adattive](#using-adaptive-images)

Durante la progettazione, utilizzate la barra degli strumenti **Emulatore** per visualizzare in anteprima le pagine per diverse dimensioni di schermo.

## Prima di sviluppare {#before-you-develop}

Prima di sviluppare l’applicazione AEM che supporta le pagine Web, è necessario adottare diverse decisioni di progettazione. Ad esempio, è necessario disporre delle informazioni seguenti:

* I dispositivi di destinazione
* Dimensioni delle finestre di destinazione
* Layout di pagina per ciascuna dimensione di visualizzazione di destinazione

### Struttura dell&#39;applicazione {#application-structure}

La struttura tipica AEM applicazione supporta tutte le implementazioni di design reattivo:

* I componenti della pagina risiedono sotto `/apps/<application_name>/components`
* I modelli risiedono sotto `/apps/<application_name>/templates`

## Utilizzo di Media Query {#using-media-queries}

Le media query consentono l&#39;uso selettivo di stili CSS per il rendering della pagina. AEM strumenti e funzionalità di sviluppo consentono di implementare in modo efficace ed efficiente le media query nelle applicazioni.

Il gruppo W3C fornisce la raccomandazione [Media Query](https://www.w3.org/TR/css3-mediaqueries/) che descrive questa funzione CSS3 e la sintassi.

### Creazione del file CSS {#creating-the-css-file}

Nel file CSS, definite le query multimediali in base alle proprietà dei dispositivi di destinazione. La seguente strategia di implementazione è efficace per la gestione degli stili per ogni media query:

* Utilizzate una [cartella Libreria client](clientlibs.md) per definire il CSS assemblato quando viene eseguito il rendering della pagina.
* Definite ogni media query e gli stili associati in file CSS separati. È utile utilizzare nomi di file che rappresentano le caratteristiche del dispositivo della query multimediale.
* Definire stili comuni a tutti i dispositivi in un file CSS separato.
* Nel file css.txt della cartella Libreria client, ordinate i file CSS dell&#39;elenco come richiesto nel file CSS assemblato.

L&#39; [esercitazione WKND](develop-wknd-tutorial.md) utilizza questa strategia per definire gli stili nella progettazione del sito. Il file CSS utilizzato da WKND si trova in `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.
