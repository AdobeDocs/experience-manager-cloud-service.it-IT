---
title: Carica opzioni elenco a discesa dall’URL
description: Le opzioni dell’elenco a discesa sono incluse in un foglio di calcolo distinto e quindi importate nel foglio di calcolo principale tramite l’URL fornito.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 2%

---


# Carica opzioni elenco a discesa dall’URL

Nei moduli Edge Delivery Services, gli utenti possono selezionare un valore da un insieme predefinito di opzioni. Gli autori dei moduli utilizzano `select` , che fornisce un elenco di scelte.
Ad esempio, il `enquiry` il modulo include un menu a discesa per selezionare i paesi, che offre agli utenti una serie di paesi predefiniti tra cui scegliere. Puoi vedere che questo elenco comprende un lungo elenco di paesi separati da virgole.

![Opzioni a discesa](/help/forms/assets/drop-down-options.png)

La gestione di lunghi elenchi di opzioni per i menu a discesa può risultare complessa quando si aggiungono direttamente tali opzioni nel foglio contenente la definizione del modulo. La creazione di un foglio separato per memorizzare queste opzioni a discesa può semplificare e semplificare il processo. Questo foglio funge da archivio centralizzato per tutte le opzioni a discesa, organizzate in un formato strutturato. Ogni opzione è elencata nella propria riga, facilitando la gestione e gli aggiornamenti.

Esaminiamo come migliorare il processo di authoring dei moduli caricando l’elenco delle opzioni da un altro foglio di calcolo tramite un URL.

Alla fine di questo articolo imparerai a:

* [Definire le opzioni in un foglio di calcolo separato](#define-options)
* [Aggiungi URL per caricare le opzioni dell’elenco a discesa](#add-url)

## Definire le opzioni in un foglio separato {#define-options}

Creare un foglio con due colonne:`Option` e `Value`, per definire le opzioni:

1. Vai alla cartella dei progetti AEM in Microsoft® SharePoint o Google Drive.
2. Aggiungi un foglio denominato `shared-country` nel sito Microsoft® SharePoint o nella cartella Google Drive e aggiungi quanto segue:

   * **Opzione**: rappresenta i valori di visualizzazione delle opzioni nel menu a discesa.
   * **Valore**: rappresenta il valore inviato quando un utente seleziona l’opzione.

   >[!NOTE]
   >
   > Se il valore e l’opzione di un elenco a discesa sono uguali, il foglio di calcolo può contenere solo **Opzione** colonna.

   Aggiungiamo un nuovo foglio, [paese condiviso](/help/forms/assets/enquiry-options.xlsx) per le opzioni visualizzate nella `Destination` elenco a discesa nella `enquiry` modulo.

   Fai riferimento all’illustrazione seguente, che illustra `shared-country` foglio di calcolo:

   ![Elenco a discesa per paese](/help/forms/assets/drop-down-country-options.png)
3. Visualizzare in anteprima e pubblicare `shared-country` foglio utilizzo [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   Fai riferimento all’URL che mostra `shared-country` foglio: https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country` è un parametro di query aggiunto all’URL. Questo parametro indica il JSON filtrato in base al `shared-country` foglio. Viene reindirizzato al file JSON contenente informazioni relative a paesi diversi.

## Aggiungi URL per caricare le opzioni dell’elenco a discesa{#add-url}

Il `Options` proprietà di un `select` accetta un URL. L’URL restituisce un array JSON utilizzato come opzioni per `Destination` elenco a discesa. Per aggiungere l’URL per caricare le opzioni dell’elenco a discesa:

1. Vai alla cartella dei progetti AEM su Microsoft® SharePoint o Google Drive e apri il foglio di calcolo. È inoltre possibile creare un nuovo foglio di calcolo per un modulo.
1. Copia l’URL di `shared-country` e incollarlo nel `Options` colonna per `Destination` campo.

   ![Foglio di calcolo di interrogazione](/help/forms/assets/drop-down-enquiry.png)

1. Visualizzare in anteprima e pubblicare il foglio utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![Elenco a discesa per paese](/help/forms/assets/load-dropdown-options-form.png)

È possibile fare riferimento a [foglio di calcolo interrogazione](/help/forms/assets/enquiry-options.xlsx) per aggiungere l’URL per caricare le opzioni dell’elenco a discesa.

Dopo aver integrato l’URL nella definizione del modulo per caricare le opzioni dell’elenco a discesa, le opzioni `Destination` dall&#39;URL.

Consulta l’URL seguente, che mostra `enquiry` maschera che visualizza le opzioni salvate nel foglio separato:

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## Consulta anche

{{see-more-forms-eds}}


