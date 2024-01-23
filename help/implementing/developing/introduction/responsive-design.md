---
title: Design reattivo
description: Con il design reattivo, le stesse esperienze possono essere visualizzate in modo efficace su più dispositivi in più orientamenti.
source-git-commit: c9ee24e7b9f10ebbf9425dff66103e097701c8e4
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 0%

---


# Design reattivo {#responsive-design}

Progetta le esperienze in modo che si adattino al riquadro di visualizzazione client in cui vengono visualizzate. Con il design reattivo, le stesse pagine possono essere visualizzate in modo efficace su più dispositivi in entrambi gli orientamenti. L&#39;immagine seguente illustra alcuni modi in cui una pagina può rispondere alle modifiche apportate alle dimensioni del riquadro di visualizzazione:

* Layout: utilizza layout a colonna singola per riquadri di visualizzazione più piccoli e layout a più colonne per riquadri di visualizzazione più grandi.
* Dimensione testo: utilizza dimensioni maggiori del testo (se appropriato, ad esempio le intestazioni) nelle finestre di visualizzazione più grandi.
* Contenuto: include solo il contenuto più importante quando viene visualizzato su dispositivi più piccoli.
* Navigazione: sono disponibili strumenti specifici per i dispositivi per accedere ad altre pagine.
* Immagini: distribuiscono rappresentazioni di immagini appropriate per il riquadro di visualizzazione client in base alle dimensioni della finestra.

![Esempi di progettazione reattiva](assets/responsive-example.png)

Sviluppa applicazioni Adobe Experience Manager (AEM) che generano HTML5 adattabili a più dimensioni e orientamenti di finestre. Ad esempio, i seguenti intervalli di larghezze dei riquadri di visualizzazione corrispondono a vari tipi di dispositivi e orientamenti

* Larghezza massima di 480 pixel (telefono, verticale)
* Larghezza massima di 767 pixel (telefono, orizzontale)
* Larghezza compresa tra 768 e 979 pixel (tablet, verticale)
* Larghezza compresa tra 980 e 1199 pixel (tablet, orizzontale)
* Larghezza uguale o superiore a 1200 px (desktop)

Per informazioni sull’implementazione del comportamento di progettazione reattiva, consulta i seguenti argomenti:

* [Query multimediali](#using-media-queries)
* [Griglie fluide](#developing-a-fluid-grid)
* [Immagini adattive](#using-adaptive-images)

Durante la progettazione, utilizzare **Emulatore** per visualizzare in anteprima le pagine per schermi di varie dimensioni.

## Prima di sviluppare {#before-you-develop}

Prima di sviluppare l’applicazione AEM che supporta le pagine web, è necessario prendere diverse decisioni di progettazione. Ad esempio, è necessario disporre delle seguenti informazioni:

* Dispositivi di destinazione
* Le dimensioni del riquadro di visualizzazione di destinazione
* I layout di pagina per ciascuna dimensione del riquadro di visualizzazione di destinazione

### Struttura dell&#39;applicazione {#application-structure}

La tipica struttura di applicazioni AEM supporta tutte le implementazioni di progettazione reattiva:

* I componenti della pagina risiedono di seguito `/apps/<application_name>/components`
* I modelli si trovano sotto `/apps/<application_name>/templates`

## Utilizzo delle query multimediali {#using-media-queries}

Le query multimediali consentono l’utilizzo selettivo degli stili CSS per il rendering delle pagine. Gli strumenti e le funzioni di sviluppo AEM consentono di implementare in modo efficace ed efficiente le query multimediali nelle applicazioni.

Il gruppo W3C fornisce [Query multimediali](https://www.w3.org/TR/css3-mediaqueries/) consiglio che descrive questa funzione CSS3 e la sintassi.

### Creazione del file CSS {#creating-the-css-file}

Nel file CSS, definisci le query multimediali in base alle proprietà dei dispositivi di destinazione. La seguente strategia di implementazione è efficace per la gestione degli stili per ogni query multimediale:

* Utilizza un [Cartella libreria client](clientlibs.md) per definire il CSS che viene assemblato al momento del rendering della pagina.
* Definisci ogni query multimediale e gli stili associati in file CSS separati. È utile utilizzare nomi di file che rappresentino le funzioni dispositivo della query multimediale.
* Definisci gli stili comuni a tutti i dispositivi in un file CSS separato.
* Nel file css.txt della cartella Libreria client, ordinare i file CSS di elenco come richiesto nel file CSS assemblato.

Il [Esercitazione WKND](develop-wknd-tutorial.md) utilizza questa strategia per definire gli stili nella progettazione del sito. Il file CSS utilizzato da WKND si trova in `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.

### Utilizzo delle query multimediali con le pagine AEM {#using-media-queries-with-aem-pages}

[Progetto di esempio WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) e [Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) utilizzare il [Componente core pagina,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/page.html) che include clientlibs tramite il criterio di pagina.

Se il tuo componente pagina non è basato sul componente core pagina, puoi anche includere la cartella della libreria client nello script HTL o JSP. In questo modo si genera e si fa riferimento al file CSS con le query multimediali necessarie per il funzionamento della griglia reattiva.

#### HTL {#htl}

```html
<sly data-sly-use.clientlib="${'/libs/granite/sightly/templates/clientlib.html'}">
<sly data-sly-call="${clientlib.all @ categories='apps.weretail.all'}"/>
```

#### JSP {#jsp}

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

Lo script JSP genera il seguente codice HTML che fa riferimento ai fogli di stile:

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Anteprima per dispositivi specifici {#previewing-for-specific-devices}

L’emulatore ti consente di visualizzare in anteprima le pagine in diverse dimensioni di riquadri di visualizzazione, in modo da poter testare il comportamento del design reattivo. Quando modifichi una pagina nella console Sites, puoi toccare o fare clic sul pulsante **Emulatore** per visualizzare l’emulatore.

![Icona dell’emulatore nella barra degli strumenti](assets/emulator-icon.png)

Nella barra degli strumenti dell’emulatore puoi toccare o fare clic sul pulsante **Dispositivi** per visualizzare un menu a discesa in cui selezionare un dispositivo. Quando selezioni un dispositivo, la pagina cambia in base alle dimensioni del riquadro di visualizzazione.

![Barra degli strumenti dell’emulatore](assets/emulator.png)

### Specifica dei gruppi di dispositivi {#specifying-device-groups}

Per specificare i gruppi di dispositivi visualizzati nel **Dispositivi** elenco, aggiungi `cq:deviceGroups` proprietà per il `jcr:content` della pagina del modello del sito. Il valore della proprietà è un array di percorsi ai nodi del gruppo di dispositivi.

Ad esempio, la pagina modello del sito WKND è `/conf/wknd/settings/wcm/template-types/empty-page/structure`. E il `jcr:content` il nodo sotto di esso include la seguente proprietà:

* Nome: `cq:deviceGroups`
* Tipo: `String[]`
* Valore: `mobile/groups/responsive`

I nodi del gruppo di dispositivi si trovano in `/etc/mobile/groups` cartella.

## Immagini reattive {#responsive-images}

Le pagine reattive si adattano dinamicamente al dispositivo su cui vengono riprodotte, offrendo un’esperienza migliore per l’utente. Tuttavia, è anche importante che le risorse siano ottimizzate per il punto di interruzione e il dispositivo per ridurre al minimo il tempo di caricamento delle pagine.

[Componente core Immagine](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=it) funzioni come la selezione adattiva delle immagini.

* Per impostazione predefinita, il componente Immagine utilizza [Adaptive Image Servlet](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/adaptive-image-servlet.html) per consegnare la rappresentazione corretta.
* [Consegna di immagini ottimizzate per il web](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html?lang=it) è disponibile anche tramite una semplice casella di controllo nella sua policy, che fornisce risorse di immagini da DAM in formato WebP e può ridurre la dimensione di download di un’immagine di circa il 25% in media.

## Contenitore di layout {#layout-container}

Contenitore di layout AEM consente di implementare in modo efficiente ed efficace il layout dinamico per adattare le dimensioni della pagina al riquadro di visualizzazione client.

Consulta il documento [Configurazione del contenitore di layout e della modalità layout](/help/sites-cloud/administering/responsive-layout.md) per ulteriori informazioni su come funziona il Contenitore di layout e come abilitare i layout reattivi per i contenuti.
