---
title: potrai gestire esperienze del catalogo prodotti in fase di sviluppo
description: Scopri come gestire le esperienze del catalogo dei prodotti in staging.
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
feature: Commerce Integration Framework
role: Admin
source-git-commit: f172f514eaa8f1337359f00fad964f5781fba769
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 10%

---

# Creazione di esperienze nel catalogo dei prodotti in fase di sviluppo {#building-experiences}

Scopri come gestire le esperienze del catalogo dei prodotti in staging.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso di contenuti e Commerce dell&#39;AEM, [Gestire pagine e modelli del catalogo dei prodotti](catalog-templates.md), hai imparato a gestire e creare esperienze del catalogo dei prodotti basate sui modelli.

Questo articolo si basa su questi principi fondamentali.

## Obiettivo {#objective}

Questo documento spiega come gestire l’esperienza del catalogo dei prodotti in base ai dati di prodotto raccolti in staging e ai lanci AEM. Molte volte, gli autori devono preparare in parallelo un prossimo lancio di prodotto (come una nuova collezione di abbigliamento). Questo richiede l’accesso ai dati di prodotto in staging (non ancora live) e la possibilità di preparare il contenuto. I nuovi contenuti verranno pubblicati con il lancio del prodotto.

>[!NOTE]
>
>Questa funzione è disponibile solo con Adobe Commerce o Cloud Edition e connettori di terze parti che supportano l’autenticazione basata su token. Per ulteriori informazioni, vedere [Guida introduttiva](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html?lang=it).

Per prima cosa, vediamo come gli autori possono accedere ai dati di prodotti in staging con l’CIF.

## Utilizzo dei dati di prodotto in staging {#staged-product-data}

Un modo per accedere ai dati di prodotto in staging è utilizzare la cabina di comando del prodotto. Per aprire il catalogo dei prodotti, fai clic sull’icona Commerce nel menu principale dell’AEM. In questo modo potrai accedere ai dati di prodotto live. Apri la scheda del filtro a sinistra ed espandi **CATALOGO STAGNATO**. Utilizzando i dati di anteprima, ora puoi accedere ai dati di prodotto in staging per qualsiasi momento. I dati in staging includono nuove categorie, prodotti o campi aggiornati come prezzo.

![cabina di pilotaggio area di visualizzazione](assets/staged-cockpit.png)

L’anteprima di una vetrina con dati di staging è possibile utilizzando la vista timewarp. Apri l’editor e passa alla modalità timewarp. Seleziona una data futura. Osserva le informazioni nella parte superiore dell’editor che stai visualizzando la pagina per una certa data.

![timewarp fase](assets/staged-timewarp.png)

Ora puoi sfogliare il catalogo con i dati dell’area intermedia. Se apri una categoria o una pagina di prodotto in staging, l’editor visualizza un indicatore visivo.

![stage plp](assets/staged-plp.png)

>[!NOTE]
>
>Omnisearch non ha un contesto e pertanto restituirà solo i dati del catalogo dei prodotti live

## Lanci AEM {#launches}

AEM Launches consente di creare contenuti per dati di prodotti in staging. Se non conosci Launches, segui il collegamento alla documentazione nella [sezione Risorse aggiuntive](#additional-resources). La Data lancio viene quindi utilizzata per accedere ai dati dei prodotti in staging.

![avvio area di visualizzazione](assets/staged-launch.png)

Tieni presente che i selettori rispettano la data di lancio con l’indicatore staging sul lato destro.

![selettore area di visualizzazione](assets/staged-picker.png)

## Passaggio successivo {#what-is-next}

Ora che hai completato questa parte del percorso dovresti:

* comprendere i concetti di catalogo di prodotti in staging e contenuto con Launches
* essere in grado di accedere ai dati del catalogo dei prodotti in staging tramite la cabina di comando e l’editor dei prodotti

Ora puoi gestire [esperienze prodotto](product-experience-management.md). Tuttavia, AEM Content e Commerce hanno molte opzioni aggiuntive disponibili. Consulta alcune delle risorse aggiuntive disponibili nella [sezione Risorse aggiuntive](#additional-resources) per ulteriori informazioni sulle funzioni visualizzate in questo percorso.

## Risorse aggiuntive {#additional-resources}

* [Cockpit prodotto](/help/commerce-cloud/authoring/product-cockpit.md)
* [Guida introduttiva](/help/commerce-cloud/getting-started.md)
* [Lanci](/help/sites-cloud/authoring/launches/overview.md)
