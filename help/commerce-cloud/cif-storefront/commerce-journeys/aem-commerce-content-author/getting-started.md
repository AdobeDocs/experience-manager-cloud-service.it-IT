---
title: Guida introduttiva all’authoring CIF
description: Guida introduttiva all’authoring di CIF.
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 2%

---


# Guida introduttiva all’authoring di AEM CIF {#getting-started}

Scopri di più sull’authoring CIF di Adobe Experience Manager (AEM).

## Percorso affrontato finora {#story-so-far}

Nel documento precedente di questo percorso AEM Content and Commerce, [Scopri AEM Content and Commerce,](/help/commerce-cloud/cif-storefront/introduction.md), hai imparato la teoria e i concetti di base di CMS headless, AEM Content e Commerce.

Questo articolo si basa su questi principi fondamentali.

## Obiettivo {#objective}

Questo documento spiega come utilizzare CIF per l’authoring specifico di contenuti e Commerce. La lettura di questo articolo ti consente di:

* Comprendere i concetti dell’authoring di CIF utilizzando l’Editor pagina in AEM
* Come accedere ai dati del catalogo dei prodotti in AEM utilizzando i selettori di prodotti e categorie
* Come accedere a contenuti e dati di e-commerce utilizzando il pannello di comando del prodotto e AEM Omnisearch

## Authoring di CIF nell’Editor pagina di AEM {#cif-authoring}

CIF estende l’Editor pagina in AEM con funzionalità che consentono di accedere ai dati di prodotto in tempo reale senza uscire dal contesto:

Apri il pannello laterale e seleziona Prodotti dall’elenco a discesa.

![Seleziona tipo di prodotto](assets/asset-finder-overview.png)

Puoi sfogliare il catalogo dei prodotti o utilizzare il campo di ricerca full-text per trovare i prodotti.

![tipo di prodotto](assets/asset-finder-search.png)

I prodotti possono essere rilasciati su componenti che supportano i rilasci di prodotto (ad esempio, teaser di prodotto, carosello di prodotto) direttamente sulla pagina, creando così automaticamente un componente teaser di prodotto.

## Selettori di prodotti e categorie {#pickers}

Se i dati di prodotti e categorie sono necessari nei componenti commerce o nelle finestre di dialogo di back-office di AEM, gli autori di AEM possono utilizzare selettori che sono elementi dell’interfaccia utente per cercare e selezionare comodamente i dati del catalogo dei prodotti.

### Selettore prodotti {#product-picker}

Fai clic sull’icona della cartella per aprire l’interfaccia utente modale del selettore (ad esempio, teaser di prodotto).

![selettore prodotti](assets/product-picker-open.png)

Puoi trovare i prodotti sfogliando la struttura del catalogo a sinistra o effettuando una ricerca. La ricerca full-text rispetta la categoria selezionata e limita i risultati a questa categoria.

![cartella selettore prodotti](assets/product-picker-folders.png)

I prodotti con varianti sono contrassegnati con un’icona a forma di cartella su cui è possibile fare clic per visualizzare tutte le varianti.

![varianti del selettore prodotti](assets/product-picker-variants.png)

![varianti selettore prodotti aperte](assets/product-picker-variants-open.png)

### Selettore categorie {#category-picker}

Funziona come un selettore di prodotti. Fai clic sull’icona della cartella per aprire l’interfaccia utente modale del selettore (ad esempio, carosello categorie).

![selettore categorie](assets/category-picker-open.png)

Sfoglia la struttura del catalogo a sinistra e seleziona la categoria.

![selettore categorie](assets/category-picker-folders.png)

## Cockpit prodotto {#cockpit}

Il pannello di comando del prodotto è una posizione centrale per accedere rapidamente al catalogo dei prodotti con tutti i relativi contenuti arricchiti. In uno dei moduli successivi scopri come arricchire i dati di prodotto con i contenuti. Per il momento, concentriamoci sull’accesso ai dati dei prodotti.

Dal menu principale, fai clic su commerce per visualizzare un elenco di tutti i cataloghi di prodotti allegati.

![voce di menu commerce](assets/commerce-menu-item.png)

Viene visualizzato un elenco di tutti i cataloghi di prodotti connessi.

![cataloghi integrati del pannello di comando](assets/cockpit-Integrated-catalogs.png)

Il catalogo prodotti mostra per impostazione predefinita tutte le categorie di primo livello con tutti i prodotti. Facendo clic su una categoria si apre tale categoria con tutti i prodotti e le sottocategorie correlati, inclusi i relativi prodotti.

![catalogo prodotti cabina di comando](assets/cockpit-product-catalog.png)

Per aprire le proprietà del prodotto, fai clic sull’icona della proprietà. L’icona viene visualizzata passando il puntatore del mouse su una sezione del prodotto.

![proprietà prodotto cabina di comando](assets/cockpit-properties.png)

Tutte le proprietà del prodotto sono di sola lettura perché i dati vengono caricati in tempo reale dal backend connesso. La modifica delle proprietà del prodotto deve essere eseguita nel sistema back-end, ovvero nel sistema di registrazione. La scheda **Varianti** viene visualizzata solo se il prodotto contiene varianti. Facendo clic sulla scheda vengono visualizzate tutte le varianti con i relativi attributi.

![varianti prodotto cabina di comando](assets/cockpit-properties-variants.png)

Le schede rimanenti mostrano tutto il contenuto AEM associato al prodotto. Queste schede vengono discusse in uno dei moduli successivi.

## AEM Omnisearch {#omnisearch}

Omnisearch consente di trovare facilmente i contenuti AEM mediante la ricerca full-text. CIF estende Omnisearch con la ricerca full-text di cataloghi di prodotti e dei relativi contenuti AEM associati.

![voce di menu commerce](assets/omnisearch.png)

Omnisearch esegue una ricerca full-text nel backend di Commerce per trovare tutti i prodotti correlati. Il risultato è elencato in **Visualizza tutti i prodotti**. Omnisearch cerca inoltre in AEM il contenuto associato al prodotto cercato. I risultati sono elencati nelle rispettive categorie di AEM. In questo esempio, un frammento di contenuto è correlato al prodotto.

## Passaggio successivo {#what-is-next}

Ora che hai completato questa parte del percorso dovresti:

* Comprendere i concetti dell’authoring di CIF utilizzando l’Editor pagina
* Come accedere al catalogo dei prodotti in AEM utilizzando i selettori di prodotti e categorie
* Come accedere a contenuti e dati di e-commerce utilizzando il pannello di comando del prodotto e AEM Omnisearch

Approfondisci l&#39;argomento e continua il tuo percorso consultando il documento [Gestire le pagine e i modelli del catalogo dei prodotti,](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/catalog-templates.md) dove imparerai a creare e personalizzare la tua prima esperienza nel catalogo dei prodotti.

## Risorse aggiuntive {#additional-resources}

Sebbene sia consigliabile passare alla parte successiva del percorso, [Gestione pagine e modelli del catalogo prodotti](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/catalog-templates.md), di seguito sono riportate alcune risorse opzionali che approfondiscono alcuni concetti menzionati. Tuttavia, queste risorse facoltative non sono necessarie per continuare il percorso.

* [Configurazione di store e cataloghi](/help/commerce-cloud/cif-storefront/getting-started.md#catalog)
