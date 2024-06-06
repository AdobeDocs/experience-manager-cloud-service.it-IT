---
title: Carica opzioni elenco a discesa da un URL o da un altro foglio per Edge Delivery Services per AEM Forms as a Cloud Service
description: Le opzioni dell’elenco a discesa sono incluse in un foglio di calcolo distinto e quindi importate nel foglio di calcolo principale tramite l’URL fornito.
feature: Edge Delivery Services
exl-id: 5b0bc1b6-6e33-41f3-b7c1-4d997787b6cd
source-git-commit: 8730383d26c6f4fbe31a25a43d33bf314251d267
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 91%

---


# Opzioni da un URL o da un altro foglio per Edge Delivery Services per AEM Forms as a Cloud Service

I moduli spesso includono menu a discesa che gli utenti possono selezionare dalle opzioni predefinite. Queste opzioni vengono in genere definite all’interno del modulo stesso, ma la gestione di elenchi lunghi può risultare complicata. Questa guida illustra come migliorare l’authoring dei moduli caricando le opzioni a discesa da un foglio di calcolo separato tramite un URL.


I vantaggi del caricamento delle opzioni a discesa da un foglio di calcolo separato sono:

* Gestione semplificata: mantiene le opzioni a discesa in una posizione centralizzata per semplificare gli aggiornamenti e le aggiunte.
* Maggiore efficienza: elimina la necessità di aggiungere manualmente lunghi elenchi di opzioni all’interno della definizione del modulo.




![Opzioni a discesa](/help/forms/assets/drop-down-options.png)


Alla fine di questo articolo imparerai a:

* [Definire le opzioni in un foglio di calcolo separato](#define-options)
* [Aggiungere un URL per caricare le opzioni dell’elenco a discesa](#add-url)

## Definire le opzioni in un foglio separato {#define-options}

Definizione delle opzioni in un foglio di calcolo separato

1. Crea un foglio di calcolo:
   1. Individua la cartella del progetto AEM in Microsoft® SharePoint o Google Drive.
   1. Aggiungi un nuovo foglio. Ad esempio, “paese-condiviso”.
1. Definisci le colonne delle opzioni:
Aggiungi due colonne: “Opzione” e “Valore”.
   * “Opzione” definisce il testo visualizzato nel menu a discesa.
   * “Valore” definisce il valore inviato quando un utente seleziona l’opzione.

   >[!NOTE]
   >
   >Se l’opzione e il valore sono identici, è necessaria solo la colonna “Opzione”.

1. Compila il foglio di calcolo:
Immetti le opzioni relative al paese nella colonna “Opzione” (e nella colonna “Valore”, se necessario).

   Per la struttura, consulta l’esempio seguente.

   ![Elenco a discesa per paese](/help/forms/assets/drop-down-country-options.png)

1. Visualizzare in anteprima e pubblicare il foglio `shared-country` utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   Fai riferimento all’URL che mostra il foglio `shared-country`:
https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country` è un parametro di query aggiunto all’URL. Questo parametro indica il JSON filtrato in base al foglio `shared-country`. Viene reindirizzato al file JSON contenente informazioni relative a paesi diversi.

## Aggiungere un URL per caricare le opzioni dell’elenco a discesa{#add-url}

La proprietà `Options` di un campo `select` accetta un URL. L’URL restituisce un array JSON utilizzato come opzioni per l’elenco a discesa `Destination`. Per aggiungere l’URL per caricare le opzioni dell’elenco a discesa:

1. Passa alla cartella del progetto AEM in Microsoft® SharePoint o Google Drive e apri il foglio di calcolo. È inoltre possibile creare un nuovo foglio di calcolo per un modulo.
1. Copia l’URL del foglio `shared-country` e incollalo nella colonna `Options` per il campo `Destination`.

   ![Foglio di calcolo “enquiry”](/help/forms/assets/drop-down-enquiry.png)

1. Visualizzare in anteprima e pubblicare il foglio utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![Menu a discesa per paese](/help/forms/assets/load-dropdown-options-form.png)

Puoi fare riferimento al [foglio di calcolo “enquiry”](/help/forms/assets/enquiry-options.xlsx) per aggiungere l’URL per caricare le opzioni dell’elenco a discesa.

Dopo aver integrato l’URL nella definizione del modulo per caricare le opzioni dell’elenco a discesa, tali opzioni per l’elenco a discesa `Destination` iniziano a comparire dall’URL.

Consulta l’URL seguente, che mostra il modulo `enquiry` che visualizza le opzioni salvate nel foglio separato:

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## Consulta anche

{{see-more-forms-eds}}


