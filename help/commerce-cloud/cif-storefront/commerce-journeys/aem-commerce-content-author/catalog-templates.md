---
title: Gestire pagine e modelli del catalogo dei prodotti
description: Scopri come gestire pagine e modelli di catalogo dei prodotti
exl-id: 0d795d85-c865-40d5-941e-e02ee96fdd11
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---


# Gestire pagine e modelli del catalogo dei prodotti {#product-catalog}

Scopri come gestire pagine e modelli di catalogo dei prodotti.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso di authoring AEM Content and Commerce, [Guida introduttiva alle nozioni di base sull&#39;authoring AEM CIF](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/getting-started.md) hai imparato le nozioni di base sull&#39;authoring CIF.

Questo articolo si basa su questi principi fondamentali.

## Obiettivo {#objective}

Questo documento spiega come gestire pagine e modelli di catalogo dei prodotti. Dopo la lettura dovresti:

* comprendere i concetti dei modelli di catalogo
* funzionamento dei modelli generici
* hanno creato un singolo modello

## Concetto di base {#basic-concept}

La vetrina Venia offre un’esperienza tipica con il catalogo dei prodotti, con navigazione e pagine di dettaglio dei prodotti (PDP), categorie (PLP) e destinazione.

Le pagine del catalogo vengono create dinamicamente utilizzando un modello di catalogo AEM CIF e dati di prodotto in tempo reale che vengono recuperati dall’endpoint commerce quando necessario. Ogni catalogo dispone di un modello generico per le pagine di prodotti e categorie.

![struttura catalogo](assets/catalog-structure.png)

Il componente Navigazione mostra il contenuto e le pagine del catalogo. È possibile visualizzare la pagina di destinazione del catalogo o le categorie di primo livello nella navigazione. Passando il puntatore del mouse su una categoria, le categorie di secondo livello vengono visualizzate come seconda riga.

![navigazione nel catalogo](assets/catalog-navigation.png)

Facendo clic su una categoria si apre la pagina della categoria (o la pagina dell’elenco dei prodotti).

![PLP](assets/catalog-plp.png)

Facendo clic su un prodotto si apre la pagina dei dettagli del prodotto.

![PLP](assets/catalog-pdp.png)

## I Modelli {#templates}

### Modelli generici {#generic}

Il modello di catalogo Venia generico utilizza il componente core Elenco prodotti. Questo componente visualizza l’immagine della categoria, se disponibile, e i prodotti della categoria.

![modello categoria](assets/category-template.png)

Il modello di prodotto Venia generico utilizza il componente core Dettagli prodotto. Questo componente visualizza le informazioni sul prodotto per vari tipi di prodotto e azioni di aggiunta al carrello.

![modello di prodotto](assets/product-template.png)

### Modifica Modelli {#edit-templates}

I modelli possono essere modificati aprendo direttamente la pagina del modello o passando alla modalità di modifica durante la navigazione in una pagina del catalogo prodotti. Tieni presente che la modifica della pagina modificherà il modello e non solo la pagina specifica del prodotto/categoria.

### Modelli per categorie o prodotti specifici {#specific}

CIF supporta più modelli con pochi clic. Per creare un altro modello, selezionare il modello generico dalla rispettiva categoria e creare una pagina utilizzando l&#39;azione **Crea**.

![crea pagina modello](assets/create-template-page.png)

Seleziona il rispettivo modello di prodotto o categoria.

![crea selezione modello](assets/create-template-select.png)

Inserisci il titolo e crea la pagina.

![crea immissione modello](assets/create-template-enter.png)

Tieni presente che ora disponi di un modello specifico sotto quello generico.

![crea gerarchia modelli](assets/create-template-hierachry.png)

Apri il modello. Assomiglia esattamente al modello di categoria generico.

![crea modello nuovo](assets/create-template-new.png)

Aggiungi un’immagine sopra la pagina.

![crea aggiornamento modello](assets/create-template-update.png)

Il modello può essere visualizzato in anteprima con qualsiasi categoria/prodotto. Apri **Informazioni pagina**, quindi seleziona **Visualizza con categoria/prodotto**. Seleziona il prodotto/categoria dal selettore per ottenere un’anteprima con questo prodotto/categoria. Seleziona **Acquista la categoria Look** per ottenere un&#39;anteprima del modello aggiornato.

![crea modello ](assets/create-template-picker.png)

Ora devi assegnare questo modello alla categoria specifica. Apri proprietà nel menu **Informazioni pagina** e passa alla scheda Commerce. Fai clic sull&#39;icona della cartella per selezionare la categoria **Acquista aspetto** dal selettore delle categorie. È possibile assegnare più categorie a un modello e includere anche le sottocategorie abilitando la casella di controllo.

![crea associazione modello](assets/create-template-associate.png)

Torna alla home page principale e fai clic sulla categoria **Acquista l&#39;aspetto** per visualizzare il modello specifico. Tutte le altre categorie utilizzano ancora il modello generico.

![crea risultato modello](assets/create-template-result.png)

È possibile applicare lo stesso flusso di lavoro per creare singoli modelli di prodotto.

## Passaggio successivo {#what-is-next}

Ora che hai completato questa parte del percorso dovresti:

* comprendere i concetti dei modelli di catalogo
* funzionamento dei modelli generici
* hanno creato un singolo modello

Approfondisci l&#39;argomento e continua il tuo percorso consultando il documento [Gestire le esperienze del catalogo prodotti in staging](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/staged-catalog.md) dove imparerai a utilizzare i dati dei prodotti in staging e AEM Launches.

## Risorse aggiuntive {#additional-resources}

Sebbene sia consigliabile passare alla parte successiva del percorso esaminando il documento [Gestione dell&#39;esperienza del catalogo prodotti in staging](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/staged-catalog.md), di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non sono necessarie per continuare il percorso headless:

* [Creazione di più pagine per categorie e prodotti](/help/commerce-cloud/cif-storefront/authoring/multi-template-usage.md)
* [Guida alla migrazione per Experience Manager Cloud Service](/help/commerce-cloud/cif-storefront/migration.md) - Come effettuare la migrazione al componente aggiuntivo AEM Commerce integration framework (CIF) da una versione precedente
