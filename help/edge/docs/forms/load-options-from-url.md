---
title: Carica opzioni elenco a discesa dall’URL
description: Le opzioni dell’elenco a discesa sono incluse in un foglio di calcolo distinto e quindi importate nel foglio di calcolo principale tramite l’URL fornito.
feature: Edge Delivery Services
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 3%

---


# Carica opzioni elenco a discesa dall’URL

Forms spesso include menu a discesa che gli utenti possono selezionare tra le opzioni predefinite. Queste opzioni vengono in genere definite all’interno del modulo stesso, ma la gestione di elenchi lunghi può essere complicata. Questa guida illustra come migliorare l’authoring dei moduli caricando le opzioni a discesa da un foglio di calcolo separato tramite un URL.


I vantaggi del caricamento di un elenco a discesa da un foglio di calcolo separato sono:

* Gestione semplificata: gestisci le opzioni a discesa in una posizione centralizzata per semplificare gli aggiornamenti e le aggiunte.
* Maggiore efficienza: elimina la necessità di aggiungere manualmente elenchi di opzioni lunghi all’interno della definizione del modulo.




![Opzioni a discesa](/help/forms/assets/drop-down-options.png)


Alla fine di questo articolo imparerai a:

* [Definire le opzioni in un foglio di calcolo separato](#define-options)
* [Aggiungi URL per caricare le opzioni dell’elenco a discesa](#add-url)

## Definire le opzioni in un foglio separato {#define-options}

Definizione delle opzioni in un foglio di calcolo separato

1. Creare un foglio di calcolo:
   1. Individuare la cartella dei progetti AEM in Microsoft® SharePoint o Google Drive.
   1. Aggiungi un nuovo foglio. Ad esempio, &quot;shared-country&quot;.
1. Definisci colonne opzione: aggiungi due colonne: &quot;Opzione&quot; e &quot;Valore&quot;.
   * &quot;Option&quot; definisce il testo visualizzato nel menu a discesa.
   * &quot;Value&quot; definisce il valore inviato quando un utente seleziona l’opzione.

   >[!NOTE]
   >
   >Se sia l&#39;opzione che il valore sono identici, è necessaria solo la colonna &quot;Opzione&quot;.

1. Compilare il foglio di calcolo: immettere le opzioni relative al paese nella colonna &quot;Opzione&quot; (e nella colonna &quot;Valore&quot;, se necessario).

   Per la struttura, consulta l’esempio seguente.

   ![Elenco a discesa per paese](/help/forms/assets/drop-down-country-options.png)

1. Visualizzare in anteprima e pubblicare `shared-country` foglio utilizzo [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

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


