---
title: Guida introduttiva all’authoring CIF
description: Guida introduttiva all’authoring CIF
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 2%

---

# Guida introduttiva all’authoring CIF AEM {#getting-started}

Scopri AEM authoring CIF.

## La storia finora {#story-so-far}

Nel documento precedente di questo percorso Contenuto e Commercio AEM, [Informazioni su AEM contenuti e commercio](/help/commerce-cloud/introduction.md), hai imparato la teoria di base su cosa sia un CMS headless e ora dovresti capire i concetti di base di AEM Content and Commerce .

Questo articolo si basa su questi fondamentali.

## Obiettivo {#objective}

Questo documento spiega come utilizzare CIF per l’authoring specifico per contenuti e contenuti commerciali. Dopo la lettura, è necessario:

* Comprendere i concetti di authoring CIF utilizzando l’editor universale
* Come accedere ai dati del catalogo dei prodotti in AEM utilizzando i selettori di prodotti e categorie
* Come accedere ai contenuti e ai dati di e-commerce utilizzando il cockpit di prodotto e AEM Omnisearch

## Authoring CIF nell’editor universale {#cif-authoring}

CIF estende l’editor universale con le funzionalità di accesso ai dati dei prodotti in tempo reale senza lasciare il contesto:

Apri il pannello laterale e seleziona &quot;Prodotti&quot; dal menu a discesa.
![Seleziona tipo di prodotto](assets/asset-finder-overview.png)

Puoi sfogliare il catalogo dei prodotti o utilizzare il campo di ricerca full-text per trovare i prodotti.
![tipo di prodotto](assets/asset-finder-search.png)

I prodotti possono essere omessi sui componenti che supportano le gocce di prodotto (ad esempio il product teaser, product carousel) direttamente sulla pagina, creando automaticamente un componente product teaser.

## Pickers per prodotti e categorie {#pickers}

Se i dati di prodotto e categoria sono necessari nei componenti di e-commerce o nelle finestre di dialogo AEM back-office, AEM gli autori possono utilizzare selettori che sono elementi dell’interfaccia utente per cercare e selezionare agevolmente i dati del catalogo di prodotti.

### Selettore prodotti

Facendo clic sull’icona della cartella si aprirà l’interfaccia utente modale del selettore (ad esempio il product teaser)
![selettore prodotti](assets/product-picker-open.png)

I prodotti possono essere trovati sfogliando la struttura del catalogo a sinistra o ricercando. La ricerca full-text rispetta la categoria selezionata e limita i risultati della ricerca a questa categoria.
![cartella del selettore prodotti](assets/product-picker-folders.png)

I prodotti con varianti sono contrassegnati da un’icona di cartella che può essere selezionata per mostrare tutte le varianti.
![varianti del selettore prodotti](assets/product-picker-variants.png)
![varianti del selettore prodotti aperte](assets/product-picker-variants-open.png)

### Selettore categoria

Funziona come un selettore di prodotti. Fai clic sull’icona della cartella per aprire l’interfaccia utente modale del selettore (ad esempio il carosello di categorie)
![selettore categoria](assets/category-picker-open.png)

Sfoglia la struttura del catalogo a sinistra e seleziona la categoria.
![selettore categoria](assets/category-picker-folders.png)

## Cockpit prodotto {#cockpit}

Il cockpit prodotto è un luogo centrale per accedere rapidamente al catalogo dei prodotti con tutti i suoi contenuti arricchiti. In uno dei prossimi moduli imparerai come arricchire i dati dei prodotti con i contenuti. Per il momento, concentriamoci sull&#39;accesso ai dati dei prodotti.

Dal menu principale, fai clic su e-commerce per visualizzare un elenco di tutti i cataloghi di prodotti allegati.
![voce di menu commercio](assets/commerce-menu-item.png)

Viene visualizzato un elenco di tutti i cataloghi di prodotti per la connessione.
![cataloghi integrati di cockpit](assets/cockpit-Integrated-catalogs.png)

Il catalogo dei prodotti mostra per impostazione predefinita tutte le categorie di primo livello con tutti i prodotti. Facendo clic su una categoria si aprirà quella categoria con tutti i prodotti e le sottocategorie correlate, compresi i relativi prodotti.
![catalogo dei prodotti in cabina](assets/cockpit-product-catalog.png)

Per aprire le proprietà del prodotto, fai clic sull’icona della proprietà . L’icona viene visualizzata passando il puntatore del mouse su un riquadro del prodotto.
![proprietà del prodotto cockpit](assets/cockpit-properties.png)

Tutte le proprietà del prodotto sono di sola lettura perché i dati vengono caricati in tempo reale dal backend connesso. La modifica delle proprietà del prodotto deve essere eseguita nel sistema di back-end che è il sistema di registrazione. Scheda **Varianti** apparirà solo se il prodotto presenta varianti. Facendo clic sulla scheda vengono visualizzate tutte le varianti con i relativi attributi.
![varianti di prodotti in cabina di pilotaggio](assets/cockpit-properties-variants.png)

Le schede rimanenti mostrano tutto AEM contenuto associato al prodotto. Discuteremo queste schede in uno dei prossimi moduli.

## Omnisearch AEM {#omnisearch}

L’utilizzo di Omnisearch è un modo semplice per trovare AEM contenuto utilizzando la ricerca full-text. CIF estende Omnisearch con la ricerca full-text di cataloghi di prodotti con il relativo contenuto AEM associato.
![voce di menu commercio](assets/omnisearch.png)

Omnisearch eseguirà una ricerca full-text nel backend commerce per trovare tutti i prodotti correlati. Il risultato è elencato in **Visualizza tutti i prodotti**. Omnisearch eseguirà anche la ricerca AEM contenuti associati al prodotto ricercato. I risultati saranno elencati nelle rispettive categorie AEM. In questo esempio, un frammento di contenuto è correlato al prodotto .

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso devi:

* Comprendere i concetti di authoring CIF utilizzando l’editor universale
* Come accedere al catalogo dei prodotti in AEM utilizzando i selettori di prodotti e categorie
* Come accedere ai contenuti e ai dati di e-commerce utilizzando il cockpit di prodotto e AEM Omnisearch

Sviluppa questa conoscenza e continua il tuo percorso rivedendo il documento successivo [Gestione delle pagine e dei modelli del catalogo dei prodotti](catalog-templates.md), dove imparerai a creare e personalizzare la tua prima esperienza di catalogo dei prodotti.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso rivedendo il documento [Gestione delle pagine e dei modelli del catalogo dei prodotti](catalog-templates.md)Di seguito sono riportate alcune risorse aggiuntive facoltative che consentono di approfondire alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso.

* [Configurazione di store e cataloghi](/help/commerce-cloud/getting-started.md#catalog)
