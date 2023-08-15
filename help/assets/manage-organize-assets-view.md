---
title: Gestire le risorse digitali
description: Sposta, elimina, copia, rinomina, aggiorna e crea versioni delle risorse in [!DNL Assets view].
role: User,Leader
contentOwner: AG
exl-id: b01e98b9-0cc2-47c5-9f5b-79b8e6bef39f
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 92%

---

# Gestire le risorse {#manage-assets}

Puoi eseguire facilmente diverse attività di gestione delle risorse digitali (DAM) mediante l’interfaccia intuitiva di [!DNL Assets view]. Dopo aver aggiunto le risorse, puoi cercare, scaricare, spostare, copiare, rinominare, eliminare, aggiornare e modificare le risorse.

Utilizza [!DNL Assets view] per eseguire le seguenti attività di gestione risorse. Quando selezioni una risorsa, nella barra degli strumenti in alto vengono visualizzate le seguenti opzioni.

![Opzioni nella barra degli strumenti quando si seleziona una risorsa](assets/toolbar-image-selected.png)

*Figura: Opzioni disponibili nella barra degli strumenti per un’immagine selezionata.*

* ![icona Deseleziona](assets/do-not-localize/close-icon.png) Deseleziona la selezione.
* ![icona Dettagli](assets/do-not-localize/edit-in-icon.png) Fai clic sull’icona per visualizzare l’anteprima di una risorsa e i metadati dettagliati. In anteprima, puoi visualizzare le versioni e modificare un’immagine.
* ![icona di download](assets/do-not-localize/download-icon.png) Scarica nel file system locale la risorsa selezionata.
* ![icona Elimina](assets/do-not-localize/delete-icon.png) Elimina la risorsa o la cartella selezionata.
* ![icona Ritira](assets/do-not-localize/checkout-icon.png) Ritira la risorsa selezionata.
* ![icona Copia](assets/do-not-localize/copy-icon.png) Copia il file o la cartella selezionati.
* ![icona Sposta](assets/do-not-localize/move-icon.png) Sposta la risorsa o la cartella selezionata in una posizione diversa nella gerarchia dell’archivio.
* ![icona Rinomina](assets/do-not-localize/rename-icon.png) Rinomina la risorsa o la cartella selezionata. Utilizza un nome univoco; in caso contrario la ridenominazione non riesce e viene visualizzato un’avvertenza. Riprova con un nuovo nome.
* ![icona Assegna attività](assets/do-not-localize/review-delegate-icon.png) Assegna attività ad altri utenti per collaborare a una risorsa.

Le stesse opzioni sono disponibili anche sulle miniature delle risorse.

![Opzioni sulla miniatura per gestire una risorsa](assets/options-on-thumbnail.png)

[!DNL Assets view] mostra nella barra degli strumenti solo le opzioni pertinenti in base al tipo di risorsa selezionata.

![Opzioni nella barra degli strumenti quando si seleziona una risorsa](assets/toolbar-folder-selected.png)

*Figura: Opzioni disponibili nella barra degli strumenti per una cartella selezionata.*

![Opzioni nella barra degli strumenti quando si seleziona una risorsa](assets/toolbar-pdf-selected.png)

*Figura: Opzioni disponibili nella barra degli strumenti per un file PDF selezionato.*

## Scaricare e distribuire le risorse {#download}

Puoi selezionare una o più risorse o cartelle o una combinazione di entrambe, e scaricare la selezione nel file system locale. Puoi modificare le risorse e caricarle nuovamente o distribuirle all’esterno di [!DNL Assets view]. Inoltre, puoi [scaricare le rappresentazioni](/help/assets/add-delete-assets-view.md#renditions) di una risorsa.

## Controllo delle versioni di una risorsa {#versions-of-assets}

<!-- 
TBD: query for engineering: How many versions are maintained. What happens when we reach that limit? Are old versions automatically removed? -->

[!DNL Assets view] crea versioni delle risorse quando queste vengono caricate di nuovo dopo essere state aggiornate o modificate. Puoi visualizzare la cronologia delle versioni precedenti e, se necessario, ripristinare una di queste come versione più recente. Le versioni delle risorse vengono create nei seguenti scenari:

* Quando si carica una nuova risorsa con lo stesso nome file e nella stessa cartella della risorsa esistente. [!DNL Assets view] richiede di sovrascrivere la risorsa precedente o di salvare la nuova risorsa come versione. Consulta [Caricare risorse duplicate](/help/assets/add-delete-assets-view.md).

  ![Creare versioni durante il caricamento](assets/uploads-manage-duplicates.png)

  *Figura: Quando carichi una risorsa con lo stesso nome di una risorsa esistente, puoi crearne una versione.*

* Quando modifichi un’immagine e fai clic su **[!UICONTROL Salva come versione]**. Consulta [Modificare le immagini](/help/assets/edit-images-assets-view.md).

  ![Salvare l’immagine modificata come versione](assets/edit-image2.png)

  *Figura: Salvare un’immagine modificata come versione.*

* Quando apri le versioni di una risorsa esistente. Fai clic su **[!UICONTROL Nuova versione]** e carica una versione più recente della risorsa nell’archivio.

  ![Opzione per caricare una nuova versione di una risorsa dalla cronologia delle versioni](assets/view-asset-versions2.png)

### Visualizzare le versioni di una risorsa {#view-versions}

Quando carichi una copia duplicata o modificata di una risorsa, puoi crearne le versioni. Il controllo delle versioni consente di rivedere le risorse storiche e, se necessario, ripristinare una versione precedente.

Per visualizzare le versioni, apri l’anteprima di una risorsa e fai clic su **[!UICONTROL Versioni]** ![icona Versioni](assets/do-not-localize/versions-clock-icon.png) nella barra laterale a destra. Per visualizzare in anteprima una versione specifica, selezionala. Per ripristinarla, fai clic su **[!UICONTROL Rendi più recente]**.

Puoi anche creare versioni dalla timeline delle versioni. Seleziona la versione più recente e fai clic su **[!UICONTROL Nuova versione]**, quindi carica una nuova copia della risorsa dal file system locale.

![Visualizzare le versioni di una risorsa](assets/view-asset-versions1.png)

*Figura: Visualizzare le versioni di una risorsa, ripristinare una versione precedente o caricare un’altra nuova versione.*

## Gestire lo stato delle risorse {#manage-asset-status}

**Autorizzazioni richieste:** `Can Edit`, `Owner` o le autorizzazioni di amministratore per una risorsa.

La vista Risorse consente di impostare lo stato delle risorse disponibili nell’archivio. Imposta lo stato di una risorsa per gestire meglio il consumo a valle di risorse digitali.

Puoi assegnare alle risorse i seguenti stati:

* Approvato

* Rifiutato

* Nessuno stato

### Impostare lo stato di una risorsa {#set-asset-status}

Per impostare lo stato di una risorsa:

1. Seleziona la risorsa e fai clic su **[!UICONTROL Dettagli]** nella barra degli strumenti.

1. Nella scheda **[!UICONTROL Base]** seleziona lo stato della risorsa dall’elenco a discesa **[!UICONTROL Stato]**. I valori possibili sono Approvato, Rifiutato e Nessuno stato (impostazione predefinita).

   >[!VIDEO](https://video.tv.adobe.com/v/342495)


### Impostare la data di scadenza di una risorsa {#set-asset-expiration-date}

La vista Risorse consente inoltre di impostare la data di scadenza delle risorse disponibili nell’archivio. È quindi possibile [filtrare i risultati della ricerca](search-assets-view.md#refine-search-results) in base allo stato `Expired` delle risorse. Inoltre, è possibile specificare un intervallo di date di scadenza per le risorse per filtrare ulteriormente i risultati della ricerca.

Per impostare la data di scadenza di una risorsa:

1. Seleziona la risorsa e fai clic su **[!UICONTROL Dettagli]** nella barra degli strumenti.

1. Nella scheda **[!UICONTROL Base]**, imposta la data di scadenza della risorsa utilizzando il campo **[!UICONTROL Data di scadenza]**.

L’indicatore `Expired` nella scheda delle risorse sostituisce l’indicatore `Approved` o `Rejected` impostato per una risorsa.

Per ulteriori informazioni, consulta la sezione su come filtrare le risorse in base allo stato [Cercare le risorse nella vista Risorse](search-assets-view.md).

## Personalizzare i moduli di metadati per includere il campo dello stato delle risorse {#customize-asset-status-metadata-form}

**Autorizzazioni richieste:** Amministratore

La vista Risorse fornisce molti campi di metadati standard per impostazione predefinita. Spesso le organizzazioni hanno l’esigenza di aggiungere altri metadati, specifici per l’azienda. I moduli di metadati consentono alle aziende di aggiungere campi di metadati personalizzati alla pagina [!UICONTROL Dettagli] di una risorsa. I metadati specifici per l’azienda migliorano la governance e l’individuazione delle risorse.

Per ulteriori informazioni su come aggiungere ulteriori campi di metadati al modulo, consulta [Moduli di metadati](metadata-assets-view.md#metadata-forms).

**Aggiungere al modulo il campo di metadati Stato risorsa**

Per aggiungere al modulo il campo di metadati Stato risorsa, trascina al suo interno il componente **[!UICONTROL Stato risorsa]** dalla barra a sinistra. La proprietà di mappatura viene precompilata automaticamente. Salva il modulo per confermare le modifiche.

**Aggiungere al modulo il campo di metadati Data di scadenza**

Per aggiungere al modulo il campo di metadati Data di scadenza, trascina nel modulo il componente **[!UICONTROL Data]** dalla barra di sinistra. Specifica **Data di scadenza** come etichetta e `pur:expirationDate` come proprietà di mappatura. Salva il modulo per confermare le modifiche.

## Passaggi successivi {#next-steps}

* [Guarda un video per gestire le risorse nella vista Risorse](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/managing.html?lang=it)

* Fornire feedback sul prodotto utilizzando [!UICONTROL Feedback] opzione disponibile nell’interfaccia utente di visualizzazione delle risorse

* Fornisci feedback alla documentazione utilizzando [!UICONTROL Modifica questa pagina] ![modifica la pagina](assets/do-not-localize/edit-page.png) o [!UICONTROL Segnala un problema] ![crea un problema GitHub](assets/do-not-localize/github-issue.png) disponibile sulla barra laterale destra

* Contatta il [Servizio clienti](https://experienceleague.adobe.com/?support-solution=General&amp;lang=it#support)
