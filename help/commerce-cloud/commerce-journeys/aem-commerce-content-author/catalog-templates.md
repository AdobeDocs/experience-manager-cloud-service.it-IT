---
title: Gestione delle pagine e dei modelli del catalogo dei prodotti
description: Scopri come gestire pagine e modelli di catalogo dei prodotti
exl-id: 0d795d85-c865-40d5-941e-e02ee96fdd11
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---

# Gestione delle pagine e dei modelli del catalogo dei prodotti {#product-catalog}

Scopri come gestire le pagine e i modelli del catalogo dei prodotti.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di authoring Contenuto e Commercio AEM, [Guida introduttiva alle nozioni di base sull’authoring CIF AEM](getting-started.md), hai appreso le nozioni di base sull’authoring CIF.

Questo articolo si basa su questi fondamentali.

## Obiettivo {#objective}

Questo documento spiega come gestire le pagine e i modelli del catalogo dei prodotti. Dopo la lettura dovresti:

* comprendere i concetti dei modelli di catalogo
* funzionamento dei modelli generici
* hanno creato un singolo modello

## Concetto di base {#basic-concept}

Venia vetrina è dotata di una tipica esperienza di catalogo dei prodotti con navigazione, e destinazione, categorie (PLP) e pagine di dettaglio dei prodotti (PDP).

Le pagine di catalogo vengono create in modo dinamico utilizzando un modello di catalogo CIF AEM e i dati di prodotto in tempo reale recuperati dall’endpoint di e-commerce quando necessario. Ogni catalogo dispone di un modello generico per le pagine di prodotti e categorie.
![struttura del catalogo](assets/catalog-structure.png)

Il componente di navigazione mostra il contenuto e le pagine del catalogo. È possibile visualizzare la pagina di destinazione del catalogo o le categorie di primo livello nella navigazione. Passando il puntatore del mouse su una categoria verranno visualizzate categorie di secondo livello come seconda riga.
![navigazione nel catalogo](assets/catalog-navigation.png)

Facendo clic su una categoria si aprirà la pagina della categoria (o la pagina dell’elenco dei prodotti).

![PLP](assets/catalog-plp.png)

Facendo clic su un prodotto si aprirà la pagina dei dettagli del prodotto.

![PLP](assets/catalog-pdp.png)

## I Modelli {#templates}

### Modelli generici {#generic}

Il modello di catalogo Venia generico utilizza il componente di base Elenco prodotti . Questo componente visualizza l’immagine della categoria, se disponibile, e i prodotti della categoria .
![modello di categoria](assets/category-template.png)

Il modello di prodotto Venia generico utilizza il componente core Product Detail. Questo componente visualizza le informazioni sui prodotti per vari tipi di prodotti e azioni add-to-cart.
![modello di prodotto](assets/product-template.png)

### Modifica modelli {#edit-templates}

È possibile modificare i modelli aprendo direttamente la pagina del modello o passando alla modalità di modifica durante la navigazione in una pagina del catalogo dei prodotti. Tieni presente che la modifica della pagina modificherà il modello e non solo la pagina specifica del prodotto o della categoria.

### Modelli specifici per categorie o prodotti {#specific}

CIF supporta più modelli in pochi clic. Per creare un altro modello, seleziona il modello generico dalla rispettiva categoria e crea una nuova pagina utilizzando il **Crea** azione.

![crea pagina modello](assets/create-template-page.png)

Selezionare il rispettivo modello di prodotto o categoria.

![crea selezione modello](assets/create-template-select.png)

Inserisci il titolo e crea la pagina.

![crea inserimento modelli](assets/create-template-enter.png)

Ora disponi di un modello specifico sotto quello generico.

![creazione gerarchia dei modelli](assets/create-template-hierachry.png)

Apri il modello. Assomiglia esattamente al modello di categoria generico.

![crea nuovo modello](assets/create-template-new.png)

Aggiungi un’immagine nella parte superiore della pagina.

![crea aggiornamento modello](assets/create-template-update.png)

Il modello può essere visualizzato in anteprima con qualsiasi categoria/prodotto. Apri **Informazioni pagina** quindi seleziona **Visualizza con categoria/prodotto**. Seleziona il prodotto/categoria dal selettore per ottenere un’anteprima con questo prodotto/categoria. Seleziona **Acquista il look** per ottenere un’anteprima del modello aggiornato.

![crea modello ](assets/create-template-picker.png)

Ora dobbiamo assegnare questo modello alla categoria specifica. Apri le proprietà in **Informazioni pagina** e passa alla scheda commercio. Fai clic sull’icona della cartella per selezionare il **Acquista il look** categoria dal selettore categoria. È possibile assegnare più categorie a un modello e includere anche le sottocategorie abilitando la casella di controllo.

![creare un&#39;associazione di modelli](assets/create-template-associate.png)

Torna alla home page principale e fai clic su **Acquista il look** per visualizzare il modello specifico. Tutte le altre categorie utilizzano ancora il modello generico.

![crea risultato modello](assets/create-template-result.png)

Lo stesso flusso di lavoro può essere applicato per creare singoli modelli di prodotto.

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso devi:

* comprendere i concetti dei modelli di catalogo
* funzionamento dei modelli generici
* hanno creato un singolo modello

Sviluppa questa conoscenza e continua il tuo percorso rivedendo il documento successivo [Gestire le esperienze catalogo prodotti in fase di staging](staged-catalog.md), dove imparerai a lavorare con i dati di prodotto e i lanci di AEM.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso rivedendo il documento [Gestire le esperienze catalogo prodotti in fase di staging](staged-catalog.md)Di seguito sono riportate alcune risorse aggiuntive facoltative che consentono di approfondire alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso headless:

* [Creazione di più pagine per categorie e prodotti](/help/commerce-cloud/authoring/multi-template-usage.md)
* [Guida alla migrazione per l’Experience Manager Cloud Service](/help/commerce-cloud/migration.md) - Come migrare al componente aggiuntivo CIF di AEM Commerce Integration Framework (CIF) da una versione precedente
