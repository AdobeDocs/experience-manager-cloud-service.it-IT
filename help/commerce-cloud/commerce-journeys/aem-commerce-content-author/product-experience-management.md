---
title: Creazione di esperienze di prodotto
description: Scopri come creare esperienze di prodotto.
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 1%

---

# Creazione di esperienze di prodotto {#building-experiences}

Scopri come gestire le esperienze dei prodotti.

## La storia finora {#story-so-far}

Nel documento precedente del percorso Contenuto AEM e Commercio, [Gestire le esperienze catalogo prodotti in fase di staging](staged-catalog.md), hai imparato a gestire le esperienze di catalogo dei prodotti in staging.

## Obiettivo {#objective}

Questo documento spiega come creare contenuti ed esperienze dei prodotti.

## Gestione dell&#39;esperienza del prodotto {#management}

Product Experience Management è la disciplina per decorare i dati di prodotto (di proprietà di una soluzione PIM o commerce) con i contenuti di marketing in AEM. Questi dati di prodotto arricchiti con contenuti possono quindi essere utilizzati in vari canali per creare un&#39;esperienza di acquisto coinvolgente.

In AEM puoi creare vari tipi di contenuti e collegarli al catalogo dei prodotti. I contenuti associati possono essere facilmente scoperti e utilizzati, il che porta a un&#39;elevata produttività.

### Assets {#assets}

Ad alto livello, esistono due tipi di attività correlate ai prodotti: prodotto e marketing. Le risorse dei prodotti sono solitamente gestite dai commercianti e si concentrano sulla visualizzazione del prodotto (principalmente davanti a uno sfondo neutro). Le risorse sono gestite nella soluzione commerce o in AEM Assets (con un’integrazione di Assets nella soluzione commerce/pim).

Le risorse di marketing sono correlate alla promozione e all’utilizzo del prodotto di solito di proprietà di marketing. Esempi sono la visualizzazione di più prodotti (&quot;shop the look&quot;), in un contesto specifico (&quot;outdoor fall collection&quot;), o come-to pdfs. CIF consente di collegare facilmente qualsiasi risorsa AEM con un oggetto catalogo di prodotto.

Apri le proprietà della risorsa e passa alla **Commerce** scheda . Questa scheda ti consente di gestire l’associazione con i prodotti. La tabella sotto il selettore fornisce informazioni aggiuntive per gli oggetti collegati (visibili solo con una selezione). Fai clic sull’icona dei dettagli per ottenere una visualizzazione completa nella cabina di pilotaggio del prodotto. Per associare un nuovo oggetto, fai clic sull’icona del selettore prodotto (icona della cartella), seleziona un oggetto e chiudi il selettore.

![risorse pem](assets/pem-assets.png)

### Frammenti di esperienza {#experience-fragments}

I frammenti esperienza sono un ottimo modo per creare contenuti di prodotto riutilizzabili o individuali su larga scala. L’associazione funziona in modo simile a una risorsa. Apri le proprietà e passa alla **Commerce** scheda . Questa scheda ti consente di gestire l’associazione con prodotti e categorie. Le tabelle sotto i selettori forniscono informazioni aggiuntive per gli oggetti collegati (visibili solo con una selezione). Fai clic sull’icona dei dettagli per ottenere una visualizzazione completa nella cabina di pilotaggio del prodotto. Per associare un nuovo oggetto, fai clic sull’icona del selettore prodotto (icona della cartella), seleziona un oggetto e chiudi il selettore.

![pem xf](assets/pem-xf.png)

### Frammenti di contenuto {#content-fragments}

I frammenti di contenuto sono il tipo di contenuto migliore per qualsiasi contenuto strutturato. Può essere utilizzato per migliorare i dati dei prodotti esterni con dati di marketing aggiuntivi o per creare contenuti in modo headless. L’associazione di un frammento di contenuto a un oggetto catalogo di prodotto avviene tramite i tipi di riferimento di prodotto o categoria nell’Editor modello frammento di contenuto. Trascina e rilascia il tipo di riferimento destro sul modello e configura il campo . Questi tipi supportano selezioni singole o multiple.

![modello pem cf](assets/pem-cf-model.png)

Se crei un nuovo frammento di contenuto basato su questo modello, questi tipi di riferimento consentono di selezionare facilmente l’oggetto corretto utilizzando il rispettivo selettore.

![pem cf](assets/pem-cf.png)

### Cockpit prodotto {#product-cockpit}

Abbiamo introdotto il cockpit (o console) del prodotto in uno dei moduli precedenti. L&#39;abitacolo è un modo semplice non solo per navigare nel catalogo dei prodotti, ma anche per vedere tutti i contenuti AEM associati in un&#39;unica posizione. Vai alla console del prodotto e apri le proprietà di un prodotto a cui è associato del contenuto. Passa alla relativa scheda per visualizzare il contenuto associato.

![cockpit](assets/pem-cockpit.png)

Facendo clic sull’icona dell’azione si aprirà tale contenuto in una nuova scheda del browser.

## Arricchimento delle pagine dei singoli prodotti e categorie {#enrich}

Nei moduli precedenti hai imparato a lavorare con più modelli di catalogo dei prodotti. I modelli multipli sono un ottimo modo per creare diversi modelli, ma non sono necessari in molti casi. In molti casi, lo stesso modello può essere utilizzato insieme ai segnaposto per i singoli contenuti. CIF supporta i segnaposto per frammenti di contenuto e frammenti esperienza.

Cominciamo con il segnaposto Frammento esperienza. Apri un modello di prodotto nell’editor AEM. Trascina e rilascia la **Frammento esperienza Commerce** sul modello, quindi apri la finestra di dialogo di configurazione.

![segnaposto pem](assets/pem-placeholder.png)

Apri la finestra di dialogo del componente e immetti un nome per questo segnaposto. Il nome del segnaposto è obbligatorio e consente di aggiungere tutti i segnaposto necessari.

![finestra di dialogo pem XF](assets/pem-dialog-xf.png)

Apri il frammento esperienza associato a un prodotto nel passaggio precedente. Apri le proprietà e passa alla scheda commercio. Immettere lo stesso nome segnaposto sotto **Posizione segnaposto del catalogo**.

![pem xf](assets/pem-xf.png)

Ora trascina e rilascia la **Frammento di contenuto Commerce** sul modello e apri la finestra di dialogo di configurazione.

![finestra di dialogo pem CF](assets/pem-dialog-cf.png)

Questa finestra di dialogo riutilizza la finestra di dialogo Frammento di contenuto del componente core. Per ulteriori informazioni, consulta le risorse aggiuntive. L&#39;unica differenza è la **Elemento di collegamento** che configura il campo identificatore (SKU prodotto o UID categoria) nel modello Frammento di contenuto.

Anteprima una pagina di prodotto a cui sono associati frammenti di contenuto e/o frammenti esperienza. Quando AEM esegue il rendering di una pagina, eseguirà una ricerca per ogni segnaposto in base al tipo (Contenuto o Frammento esperienza), all’identificatore e al nome del segnaposto per Frammenti esperienza. AEM utilizza un risolutore URL per ottenere l’identificatore (SKU per i prodotti, UID per le categorie). Se viene restituita un’esperienza o un frammento di contenuto, questo viene rappresentato nel segnaposto, altrimenti il segnaposto viene ignorato.

![risultato del pem](assets/pem-result.png)

## Come rendere i contenuti acquistabili {#making-shoppable}

È inoltre possibile rendere acquistabile una pagina AEM regolare aggiungendo componenti commerce. Crea una nuova pagina di contenuto in AEM e apri la pagina vuota nell’editor.

![pagina vuota pem](assets/pem-page-empty.png)

Innanzitutto, trascina e rilascia un componente di dettaglio del prodotto sulla pagina. Quindi passa alla barra laterale Risorse, passa ai prodotti e seleziona un prodotto. Trascina e rilascia il prodotto sul componente del prodotto. Questo mostrerà un normale componente di prodotto in una pagina di contenuto.

![pagina di prodotto pem](assets/pem-page-product.png)

Se per quel prodotto è stato creato del contenuto associato, passa alla barra laterale Risorse per **Contenuto commerciale associato**. In questa scheda vengono visualizzati tutti i contenuti AEM associati al prodotto. Ora è possibile incorporare rapidamente le pagine con qualsiasi contenuto associato.

![pagina arricchita da pem](assets/pem-page-enriched.png)

## Fine del Percorso? {#end-of-journey}

Congratulazioni! Hai completato il percorso AEM Content and Commerce Developer! Ora dovresti:

* informazioni su come associare qualsiasi contenuto AEM a oggetti catalogo prodotti
* utilizzare i segnaposto per arricchire singolarmente le pagine di prodotti e categorie
* Scopri come rendere il contenuto acquistabile e utilizzare la scheda contenuto associata

Ora puoi gestire le esperienze dei prodotti utilizzando AEM Contenuto e Commerce. Tuttavia, AEM Contenuto e Commerce dispongono di molte opzioni aggiuntive. Consulta alcune delle risorse aggiuntive disponibili nella sezione [Sezione Risorse aggiuntive](#additional-resources) per ulteriori informazioni sulle funzioni visualizzate in questo percorso.

## Risorse aggiuntive {#additional-resources}

* [Creazione di esperienze Commerce](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [Cockpit prodotto](/help/commerce-cloud/authoring/product-cockpit.md)
* [Componente Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=en)
