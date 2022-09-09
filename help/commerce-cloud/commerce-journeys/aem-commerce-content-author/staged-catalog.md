---
title: Gestire le esperienze catalogo prodotti in fase di staging
description: Scopri come gestire le esperienze di catalogo di prodotti in staging.
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 8%

---

# Creazione di esperienze nel catalogo dei prodotti in fase di sviluppo {#building-experiences}

Scopri come gestire le esperienze di catalogo di prodotti in staging.

## La storia finora {#story-so-far}

Nel documento precedente del percorso Contenuto AEM e Commercio, [Gestione delle pagine e dei modelli del catalogo dei prodotti](catalog-templates.md), hai imparato a gestire e creare esperienze catalogo di prodotti basate su modelli.

Questo articolo si basa su questi fondamentali.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come gestire l’esperienza di catalogo dei prodotti in base ai dati di prodotto e ai AEM lanci. Molte volte gli autori devono preparare in parallelo un prossimo lancio di prodotto (come una nuova collezione di abbigliamento). Ciò richiede l’accesso ai dati di prodotto in fase di staging (non ancora in tempo reale) e la capacità di preparare il contenuto. Questo nuovo contenuto verrà pubblicato con l’avvio del prodotto.

    >[!NOTE]
    >
    >Questa funzione è disponibile solo con i connettori Adobe Commerce o Cloud Edition e di terze parti che supportano l’autenticazione basata sui token. Per ulteriori informazioni, consulta [Guida introduttiva](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html) .

In primo luogo, vediamo come gli autori possono accedere ai dati di prodotto in staging con CIF.

## Utilizzo dei dati di prodotto in fase di sviluppo {#staged-product-data}

Un modo per accedere ai dati di prodotto in fase di staging è l’utilizzo del cockpit di prodotto. Apri il catalogo dei prodotti facendo clic sull’icona Commerce nel menu principale AEM. In questo modo potrai accedere ai dati dei prodotti live. Apri la scheda del filtro a sinistra ed espandi **CATALOGO A PIANO**. Utilizzando i dati di anteprima, ora puoi accedere ai dati di prodotto in staging per qualsiasi momento. I dati di staging includono nuove categorie, prodotti o campi aggiornati come prezzo.

![cabina armadio](assets/staged-cockpit.png)

È possibile visualizzare in anteprima una vetrina con dati in staging utilizzando la visualizzazione timewarp. Apri l’editor e passa la modalità a timewarp. Seleziona una data futura. Osserva le informazioni in cima all’editor che stai visualizzando la pagina per una data specifica.

![timewarp](assets/staged-timewarp.png)

Ora è possibile sfogliare il catalogo con i dati in staging. Se apri una pagina di prodotti o una categoria di staging, l’editor mostrerà un indicatore visivo.

![palco](assets/staged-plp.png)

    >[!NOTE]
    >
    >Omnisearch non ha un contesto e pertanto restituirà solo i dati del catalogo dei prodotti live

## Lanci AEM {#launches}

AEM Lanci consente di creare contenuti per i dati di prodotto in staging. Se non hai familiarità con i lanci, segui il collegamento alla documentazione nella sezione [Sezione Risorse aggiuntive](#additional-resources). La Data lancio viene quindi utilizzata per accedere ai dati di prodotto in fase di staging.

![lancio](assets/staged-launch.png)

Tieni presente che i selettori rispettano la data di lancio con l’indicatore di staging sul lato destro.

![picker](assets/staged-picker.png)

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso devi:

* comprendere i concetti di catalogo e contenuto di prodotti in staging con Lanci
* essere in grado di accedere ai dati di catalogo dei prodotti in fase di sviluppo tramite product cockpit e editor

Ora puoi gestire [esperienze prodotto](product-experience-management.md). Tuttavia, AEM Contenuto e Commerce dispongono di molte opzioni aggiuntive. Consulta alcune delle risorse aggiuntive disponibili nella [sezione Risorse aggiuntive](#additional-resources) per ulteriori informazioni sulle funzioni visualizzate in questo percorso.

## Risorse aggiuntive {#additional-resources}

* [Cockpit prodotto](/help/commerce-cloud/authoring/product-cockpit.md)
* [Guida introduttiva](/help/commerce-cloud/getting-started.md)
* [Lanci](/help/sites-cloud/authoring/launches/overview.md)
