---
title: Gestione dei rapporti in vista Risorse
description: Accedi ai dati nella sezione dei rapporti di vista Risorse per valutare l’utilizzo di prodotti e funzionalità e ottenere informazioni approfondite sulle metriche di successo chiave.
exl-id: 26d0289e-445a-4b8e-a5a1-b02beedbc3f1
feature: Asset Insights, Asset Reports
role: User, Admin, Developer
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 89%

---

# Gestire i rapporti {#manage-reports}

Il reporting delle risorse offre agli amministratori visibilità sulle attività dell’ambiente Adobe Experience Manager Assets View. Questi dati forniscono informazioni utili su come gli utenti interagiscono con i contenuti e il prodotto. Tutti gli utenti possono accedere alla dashboard Insight e quelli assegnati al profilo di prodotto Amministratori possono creare rapporti definiti dall’utente.

## Accedere ai rapporti {#access-reports}

Tutti gli utenti assegnati al profilo di prodotto per amministratori di vista Risorse possono accedere alla dashboard Insight e creare rapporti definiti dagli utenti in vista Risorse.

Per accedere ai rapporti, passa a **[!UICONTROL Rapporti]** in **[!UICONTROL Impostazioni]**.

![Rapporti](assets/reports.png)
<!--
In the **[!UICONTROL Reports]** screen, various components are shown in the tabular format which includes the following:

* **Title**: Title of the report
* **Type**: Determines whether the report is uploaded or downloaded to the repository
* **Description**: Provide details of the report that was given during uploading/downloading the report
* **Status**: Determines whether the report is completed, under progress, or deleted.
* **Author**: Provides email of the author who has uploaded/downloaded the report.
* **Created**: Gives information of the date when the report was generated.
-->

## Visualizzare gli insight {#view-live-statistics}

Vista Risorse consente di visualizzare in tempo reale i dati del tuo ambiente vista Risorse, con la dashboard Insight. Puoi visualizzare le metriche degli eventi in tempo reale negli ultimi 30 giorni o negli ultimi 12 mesi.

<!--![Toolbar options when you select an asset](assets/assets-essentials-live-statistics.png)-->

Fai clic su **[!UICONTROL Insight]** nel riquadro di navigazione a sinistra per visualizzare i seguenti grafici generati automaticamente:

* **Download**: numero di risorse scaricate dall’ambiente di visualizzazione Risorse negli ultimi 30 giorni o 12 mesi rappresentato da un grafico a linee.
  ![approfondimenti-download](/help/assets/assets/insights-downloads2341.svg)

* **Caricamenti**: numero di risorse caricate nell’ambiente di visualizzazione Risorse negli ultimi 30 giorni o 12 mesi rappresentato da un grafico a linee.
  ![insights-uploads](/help/assets/assets/insights-uplods2.svg)
  <!--* **Asset Count by Size**: The division of count of assets based on their range of various sizes from 0 MB to 100 GB.-->

* **Utilizzo archiviazione**: utilizzo dell’archiviazione, in byte, per l’ambiente di visualizzazione delle risorse rappresentato da un grafico a barre.
  ![insights-uploads](/help/assets/assets/insights-storage-usage1.svg)
  <!--* **Delivery**: The graph depicts the count of assets as the delivery dates.-->

<!--* **Asset Count by Asset Type**: Represents count of various MIME types of the available assets. For example, application/zip, image/png, video/mp4, application/postscripte.-->

* **Ricerche principali**: visualizza i termini più cercati e il numero di volte in cui tali termini sono stati cercati nell’ambiente vista Risorse negli ultimi 30 giorni o 12 mesi rappresentato in formato tabulare.
  ![insights-uploads](/help/assets/assets/insights-top-search.svg)
  <!--
   ![Insights](assets/insights1.png)
   ![Insights](assets/insights2.png)
   -->

## Creare un rapporto sui download {#create-download-report}

Per creare un rapporto sui download:

1. Passa a **[!UICONTROL Impostazioni]** > **[!UICONTROL Rapporti]** e fai clic su **[!UICONTROL Crea rapporto]**.

1. Nella scheda [!UICONTROL Configurazione], specifica il tipo di rapporto **[!UICONTROL Download]**.

1. Specifica un titolo e una descrizione facoltativa per il rapporto.

1. Seleziona il percorso della cartella, che comprende le risorse su cui eseguire il rapporto, utilizzando il campo **[!UICONTROL Seleziona il percorso della cartella]**.

1. Seleziona l’intervallo di date per il rapporto.

   >[!NOTE]
   >
   > Vista Risorse converte tutti i fusi orari locali nel Tempo coordinato universale (UTC).

1. Nella scheda [!UICONTROL Colonne] seleziona i nomi delle colonne da visualizzare nel rapporto.

1. Fai clic su **[!UICONTROL Crea]**.

   ![Scaricare il rapporto](assets/download-reports-config.png)

La tabella seguente descrive tutte le colonne che è possibile aggiungere al rapporto:

<table>
    <tbody>
     <tr>
      <th><strong>Nome colonna</strong></th>
      <th><strong>Descrizione</strong></th>
     </tr>
     <tr>
      <td>Titolo</td>
      <td>Titolo della risorsa.</td>
     </tr>
     <tr>
      <td>Percorso </td>
      <td>Percorso della cartella in cui la risorsa è disponibile in vista Risorse.</td>
     </tr>
     <tr>
      <td>Tipo MIME</td>
      <td>Tipo MIME della risorsa.</td>
     </tr>
     <tr>
      <td>Dimensione</td>
      <td>Dimensione della risorsa in byte.</td>
     </tr>
     <tr>
      <td>Scaricato da</td>
      <td>ID e-mail dell’utente che ha scaricato la risorsa.</td>
     </tr>
     <tr>
      <td>Data di download</td>
      <td>Data in cui è stata eseguita l’azione di download della risorsa.</td>
     </tr>
     <tr>
      <td>Autore</td>
      <td>Autore della risorsa.</td>
     </tr>
     <tr>
      <td>Data creazione</td>
      <td>La data in cui la risorsa è stata caricata in vista Risorse.</td>
     </tr>
     <tr>
      <td>Data di modifica</td>
      <td>Data dell’ultima modifica apportata alla risorsa.</td>
     </tr>
     <tr>
      <td>Scaduta</td>
      <td>Stato di scadenza della risorsa.</td>
     </tr>
     <tr>
      <td>Scaricato da nome utente</td>
      <td>Nome dell’utente che ha scaricato la risorsa.</td>
     </tr>           
    </tbody>
   </table>

## Creare un rapporto sui caricamenti {#create-upload-report}

Per creare un rapporto sui caricamenti:

1. Passa a **[!UICONTROL Impostazioni]** > **[!UICONTROL Rapporti]** e fai clic su **[!UICONTROL Crea rapporto]**.

1. Nella scheda [!UICONTROL Configurazione], specifica il tipo di rapporto **[!UICONTROL Caricamento]**.

1. Specifica un titolo e una descrizione facoltativa per il rapporto.

1. Seleziona il percorso della cartella, che comprende le risorse su cui eseguire il rapporto, utilizzando il campo **[!UICONTROL Seleziona il percorso della cartella]**.

1. Seleziona l’intervallo di date per il rapporto.

1. Nella scheda [!UICONTROL Colonne] seleziona i nomi delle colonne da visualizzare nel rapporto.

1. Fai clic su **[!UICONTROL Crea]**.

   ![Rapporto sui caricamenti](assets/upload-reports-config.png)

La tabella seguente descrive tutte le colonne che è possibile aggiungere al rapporto:

<table>
    <tbody>
     <tr>
      <th><strong>Nome colonna</strong></th>
      <th><strong>Descrizione</strong></th>
     </tr>
     <tr>
      <td>Titolo</td>
      <td>Titolo della risorsa.</td>
     </tr>
     <tr>
      <td>Percorso </td>
      <td>Percorso della cartella in cui la risorsa è disponibile in vista Risorse.</td>
     </tr>
     <tr>
      <td>Tipo MIME</td>
      <td>Tipo MIME della risorsa.</td>
     </tr>
     <tr>
      <td>Dimensione</td>
      <td>Dimensione della risorsa.</td>
     </tr>
     <tr>
      <td>Autore</td>
      <td>Autore della risorsa.</td>
     </tr>
     <tr>
      <td>Data creazione</td>
      <td>La data in cui la risorsa è stata caricata in vista Risorse.</td>
     </tr>
     <tr>
      <td>Data di modifica</td>
      <td>Data dell’ultima modifica apportata alla risorsa.</td>
     </tr>
     <tr>
      <td>Scaduta</td>
      <td>Stato di scadenza della risorsa.</td>
     </tr>              
    </tbody>
   </table>

## Visualizzare i rapporti esistenti {#view-report-list}

Dopo la [creazione di un rapporto](#create-download-report), puoi visualizzare l’elenco dei rapporti esistenti e scegliere se scaricarli in formato CSV o eliminarli.

Per visualizzare l’elenco dei rapporti, passa a **[!UICONTROL Impostazioni]** > **[!UICONTROL Rapporti]**.

Per ogni rapporto puoi visualizzare il titolo, il tipo di rapporto, la descrizione specificata durante la creazione, lo stato del rapporto, l’ID e-mail dell’autore che ha creato il rapporto e la data di creazione del rapporto.

Lo stato `Completed ` indica che il rapporto è pronto per il download.

![Elenco dei rapporti](assets/list-of-reports.png)


## Scaricare un rapporto CSV {#download-csv-report}

Per scaricare un rapporto in formato CSV:

1. Passa a **[!UICONTROL Impostazioni]** > **[!UICONTROL Rapporti]**.

1. Seleziona un rapporto e fai clic su **[!UICONTROL Scarica come CSV]**.

Il rapporto selezionato viene scaricato in formato CSV. Le colonne visualizzate nel rapporto CSV dipendono da quellle selezionate quando [si crea il rapporto](#create-download-report).

## Eliminare un rapporto {#delete-report}

Per eliminare un rapporto:

1. Passa a **[!UICONTROL Impostazioni]** > **[!UICONTROL Rapporti]**.

1. Seleziona un rapporto e fai clic su **[!UICONTROL Elimina]**.

1. Fai clic di nuovo su **[!UICONTROL Elimina]** per confermare.
