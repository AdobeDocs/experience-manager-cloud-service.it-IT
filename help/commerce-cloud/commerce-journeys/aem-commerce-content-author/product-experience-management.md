---
title: Creazione di esperienze di prodotto
description: Scopri come creare esperienze di prodotto.
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 4%

---

# Creazione di esperienze di prodotto {#building-experiences}

Scopri come gestire le esperienze di prodotto.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso sui contenuti e il commercio dell&#39;AEM, [Gestire le esperienze del catalogo dei prodotti in staging](staged-catalog.md), hai imparato a gestire le esperienze del catalogo dei prodotti in staging.

## Obiettivo {#objective}

Questo documento spiega come creare contenuti ed esperienze di prodotto.

## Gestione dell’esperienza del prodotto {#management}

La gestione dell’esperienza del prodotto è la disciplina adottata per decorare i dati di un prodotto (di proprietà di una soluzione PIM o commerce) con contenuti di marketing in AEM. Questi dati di prodotto arricchiti con i contenuti possono quindi essere utilizzati in vari canali per creare un’esperienza di acquisto coinvolgente.

In AEM puoi creare vari tipi di contenuti e collegarli al catalogo dei prodotti. I contenuti associati possono essere individuati e utilizzati facilmente, con conseguente aumento della produttività.

### Risorse {#assets}

Ad alto livello, esistono due tipi di risorse correlate ai prodotti: prodotto e marketing. Le risorse di prodotto sono solitamente gestite dai commercianti e si concentrano sulla visualizzazione del prodotto (per lo più davanti a uno sfondo neutro). Le risorse vengono gestite nella soluzione commerce o in AEM Assets (con un’integrazione di Assets alla soluzione commerce/pim).

Le risorse di marketing sono correlate alla promozione e all’utilizzo del prodotto, che di solito è di proprietà del marketing. Ad esempio, vengono mostrati più prodotti (&quot;shop the look&quot;), in un contesto specifico (&quot;outdoor fall collection&quot;) o come utilizzare i pdf. CIF permette di collegare facilmente qualunque risorsa AEM con un oggetto del catalogo dei prodotti.

Apri le proprietà della risorsa e passa alla **Commerce** scheda. Questa scheda ti consente di gestire l’associazione con i prodotti. La tabella sotto il selettore fornisce informazioni aggiuntive per gli oggetti collegati (visibili solo con una selezione). Fai clic sull’icona dei dettagli per ottenere una visualizzazione completa nella cabina di pilotaggio del prodotto. Per associare un nuovo oggetto, fai clic sull’icona del selettore prodotti (icona della cartella), seleziona un oggetto e chiudi il selettore.

![pem assets](assets/pem-assets.png)

### Frammenti di esperienza {#experience-fragments}

I frammenti di esperienza sono un ottimo modo per creare contenuti riutilizzabili o singoli prodotti su larga scala. L’associazione funziona in modo simile a una risorsa. Apri le proprietà e passa a **Commerce** scheda. Questa scheda ti consente di gestire l’associazione con prodotti e categorie. Le tabelle sotto i selettori forniscono informazioni aggiuntive per gli oggetti collegati (visibili solo con una selezione). Fai clic sull’icona dei dettagli per ottenere una visualizzazione completa nella cabina di pilotaggio del prodotto. Per associare un nuovo oggetto, fai clic sull’icona del selettore prodotti (icona della cartella), seleziona un oggetto e chiudi il selettore.

![pem xf](assets/pem-xf.png)

### Frammenti di contenuto {#content-fragments}

I frammenti di contenuto sono il tipo di contenuto migliore per qualsiasi contenuto strutturato. Può essere utilizzato per incrementare i dati di prodotto esterni con dati di marketing aggiuntivi o per creare contenuti in modo headless. L’associazione di un frammento di contenuto a un oggetto del catalogo dei prodotti si verifica tramite i tipi di riferimento di prodotto o categoria nell’Editor modello per frammenti di contenuto. Trascina e rilascia il tipo di riferimento corretto sul modello e configura il campo. Questi tipi supportano la selezione singola o multipla.

![pem cf model](assets/pem-cf-model.png)

Se crei un nuovo Frammento di contenuto basato su questo modello, questi tipi di riferimento ti consentono di selezionare facilmente l’oggetto giusto utilizzando il rispettivo selettore.

![pem cf](assets/pem-cf.png)

### Cockpit prodotto {#product-cockpit}

Abbiamo introdotto la cabina di comando del prodotto (o console) in uno dei moduli precedenti. Il cockpit è un modo semplice non solo per sfogliare il catalogo dei prodotti, ma anche per visualizzare tutti i contenuti AEM associati in un’unica posizione. Vai alla console del prodotto e apri le proprietà di un prodotto a cui è associato del contenuto. Passa alla rispettiva scheda per visualizzare il contenuto associato.

![cabina di pilotaggio pem](assets/pem-cockpit.png)

Facendo clic sull’icona dell’azione, questo contenuto verrà aperto in una nuova scheda del browser.

## Arricchimento di singole pagine di prodotti e categorie {#enrich}

Nei moduli precedenti hai imparato a utilizzare più modelli di catalogo prodotti. La presenza di più modelli rappresenta un ottimo modo per creare modelli diversi, ma in molti casi non è necessaria. In molti casi, lo stesso modello può essere utilizzato in combinazione con segnaposto per singoli contenuti. CIF supporta i segnaposto per Frammenti di contenuto e Frammenti di esperienza.

Iniziamo con il segnaposto Frammento esperienza. Apri un modello di prodotto nell’editor AEM. Trascina la **Frammento di esperienza Commerce** sul modello, quindi apri la finestra di dialogo config.

![segnaposto pem](assets/pem-placeholder.png)

Apri la finestra di dialogo del componente e immetti un nome per questo segnaposto. Il nome del segnaposto è obbligatorio e consente di aggiungere tutti i segnaposto necessari.

![finestra di dialogo pem XF](assets/pem-dialog-xf.png)

Apri il frammento di esperienza associato a un prodotto nel passaggio precedente. Apri le proprietà e passa alla scheda Commerce. Inserisci lo stesso nome segnaposto in **Posizione segnaposto catalogo**.

![pem xf](assets/pem-xf.png)

Ora trascina e rilascia la **Frammento di contenuto Commerce** sul modello e apri la finestra di dialogo config.

![finestra di dialogo pem CF](assets/pem-dialog-cf.png)

Questa finestra di dialogo riutilizza la finestra di dialogo Frammento di contenuto del componente core. Per ulteriori informazioni, consulta Risorse aggiuntive. L&#39;unica differenza è **Elemento collegamento** proprietà che configura il campo dell’identificatore (SKU prodotto o UID categoria) nel modello Frammento di contenuto.

Visualizza l’anteprima di una pagina di prodotto a cui sono associati un frammento di contenuto e/o un frammento di esperienza. Quando AEM esegue il rendering di una pagina, esegue una ricerca per ogni segnaposto in base al tipo (Contenuto o Frammento esperienza), all’identificatore e al nome del segnaposto per Frammenti esperienza. L’AEM utilizza un risolutore URL per ottenere l’identificatore (SKU per prodotti, UID per categorie). Se viene restituito un’esperienza o un frammento di contenuto, questo verrà rappresentato nella posizione del segnaposto, altrimenti il segnaposto viene ignorato.

![risultato pem](assets/pem-result.png)

## Rendere i contenuti acquistabili {#making-shoppable}

È inoltre possibile rendere acquistabile una pagina AEM regolare aggiungendo componenti commerce. Crea una nuova pagina di contenuti in AEM e apri la pagina vuota nell’editor.

![pagina vuota pem](assets/pem-page-empty.png)

Innanzitutto, trascina e rilascia un componente di dettaglio prodotto sulla pagina. Quindi passa alla barra laterale Risorse, passa ai prodotti e seleziona un prodotto. Trascina e rilascia il prodotto sul componente del prodotto. Questo mostrerà un componente prodotto normale su una pagina di contenuto.

![pagina prodotto pem](assets/pem-page-product.png)

Se hai creato contenuti associati per quel prodotto, passa nella barra laterale di Assets a **Contenuto Commerce associato**. Questa scheda mostra tutti i contenuti AEM associati a questo prodotto. Questo consente ora di abbellire rapidamente le pagine con qualsiasi contenuto associato.

![pagina arricchita pem](assets/pem-page-enriched.png)

## Fine del percorso? {#end-of-journey}

Congratulazioni. Hai completato il percorso per sviluppatori di contenuti e commercio dell’AEM. Ora dovresti:

* come associare qualsiasi contenuto AEM agli oggetti del catalogo dei prodotti
* utilizzare i segnaposto per arricchire singolarmente le pagine di prodotti e categorie
* sapere come rendere il contenuto acquistabile e utilizzare la scheda contenuto associata

Ora puoi gestire le esperienze dei prodotti utilizzando AEM Content and Commerce. Tuttavia, AEM Content and Commerce dispone di molte opzioni aggiuntive. Consulta alcune delle risorse aggiuntive disponibili nella [sezione Risorse aggiuntive](#additional-resources) per ulteriori informazioni sulle funzioni visualizzate in questo percorso.

## Risorse aggiuntive {#additional-resources}

* [Authoring di esperienze Commerce](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [Cockpit prodotto](/help/commerce-cloud/authoring/product-cockpit.md)
* [Componente Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=en)
