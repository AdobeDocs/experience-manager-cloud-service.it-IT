---
title: Gestione dei rapporti in vista Risorse
description: Accedi ai dati nella sezione dei rapporti di vista Risorse per valutare l’utilizzo di prodotti e funzionalità e ottenere informazioni approfondite sulle metriche di successo chiave.
exl-id: c7155459-05d9-4a95-a91f-a1fa6ae9d9a4
source-git-commit: df82681338f8ca1a34df6118cbddc6642aa8d4b5
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 100%

---

# Gestire i rapporti {#manage-reports}

>[!CONTEXTUALHELP]
>id="assets_reports"
>title="Rapporti"
>abstract="La funzionalità di reporting sulle risorse offre agli amministratori visibilità sulle attività dell’ambiente delle viste di Adobe Experience Manager Assets. Questi dati forniscono informazioni utili su come gli utenti interagiscono con i contenuti e il prodotto. Tutti gli utenti ai quali viene assegnato il profilo di prodotto per amministratori possono accedere alla dashboard Insight e creare rapporti definiti dagli utenti."

La funzionalità di reporting sulle risorse offre agli amministratori visibilità sulle attività dell’ambiente delle viste di Adobe Experience Manager Assets. Questi dati forniscono informazioni utili su come gli utenti interagiscono con i contenuti e il prodotto.

## Accedere ai rapporti {#access-reports}

Tutti gli utenti assegnati al profilo di prodotto per amministratori di vista Risorse possono accedere alla dashboard Insight e creare rapporti definiti dagli utenti in vista Risorse.

## Visualizzare gli approfondimenti {#view-live-statistics}

Vista Risorse consente di visualizzare in tempo reale i dati del tuo ambiente vista Risorse, con la dashboard Insight. Puoi visualizzare le metriche degli eventi in tempo reale negli ultimi 30 giorni o negli ultimi 12 mesi.

![Opzioni nella barra degli strumenti quando si seleziona una risorsa](assets/assets-essentials-live-statistics.png)

Fai clic su **[!UICONTROL Approfondimenti]** disponibile nel riquadro di navigazione a sinistra per visualizzare i seguenti grafici generati automaticamente:

* **Download**: numero di risorse scaricate dall’ambiente vista Risorse negli ultimi 30 giorni o 12 mesi rappresentato da un grafico a linee.

* **Caricamenti**: numero di risorse caricate nell’ambiente vista Risorse negli ultimi 30 giorni o 12 mesi rappresentato da un grafico a linee.

* **Ricerche principali**: visualizza i termini più cercati e il numero di volte in cui tali termini sono stati cercati nell’ambiente vista Risorse negli ultimi 30 giorni o 12 mesi rappresentato in formato tabulare.

<!--

* **Storage usage**: The storage usage, in gigabytes (GB), for the Assets view environment, for the last 30 days or 12 months represented using a bar chart.

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
