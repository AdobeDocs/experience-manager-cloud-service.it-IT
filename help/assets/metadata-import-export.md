---
title: Importare ed esportare in blocco i metadati delle risorse
description: Questo articolo descrive come importare ed esportare in blocco i metadati.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fb70a068-3ba3-4459-952d-79155d286c42
source-git-commit: ce7ba090a97c2f265af8ed21f11a5a45880e010a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 11%

---

# Importare ed esportare in blocco i metadati delle risorse {#import-and-export-asset-metadata-in-bulk}

Adobe Experience Manager Assets consente di importare in blocco i metadati delle risorse utilizzando un file CSV. Per eseguire aggiornamenti in blocco delle risorse caricate di recente o di quelle esistenti, importa un file CSV. Puoi anche inserire in blocco i metadati delle risorse da un sistema di terze parti in formato CSV.

## Importare metadati {#import-metadata}

L’importazione dei metadati è asincrona e non impedisce le prestazioni del sistema. L’aggiornamento simultaneo dei metadati per più risorse può richiedere molte risorse, a causa dell’attività di writeback dei metadati che utilizza i microservizi per le risorse. L’Adobe consiglia di pianificare eventuali operazioni in blocco durante l’utilizzo snello del server, in modo da non influire sulle prestazioni per gli altri utenti.

>[!NOTE]
>
>Per importare metadati su spazi dei nomi personalizzati, registra innanzitutto gli spazi dei nomi.

1. Accedi a [!DNL Assets] interfaccia utente, selezionare **[!UICONTROL Crea]** dalla barra degli strumenti e seleziona **[!UICONTROL Metadati]** dal menu.
1. In **[!UICONTROL Importazione metadati]** pagina, fai clic su **[!UICONTROL Seleziona file]**. Scegli il file CSV con i metadati.
1. Fornisci i seguenti parametri:

   | Parametro | Descrizione |
   | ---------------------- | ------- |
   | Dimensione batch | Numero di risorse in un batch per le quali devono essere importati i metadati. Il valore predefinito è 50. Il valore massimo è 100. |
   | Separatore di campi | Il valore predefinito è `,` (una virgola). È possibile specificare qualsiasi altro carattere. |
   | Delimitatore multivalore | Separatore per i valori dei metadati. Il valore predefinito è `|`. |
   | Avvia flussi di lavoro | False per impostazione predefinita. Se impostato su `true` e le impostazioni predefinite sono attive per il flusso di lavoro Writeback di metadati DAM (che scrive i metadati nei dati binari XMP). L’abilitazione dei flussi di lavoro rallenta il sistema. |
   | Nome colonna percorso risorsa | Definisce il nome della colonna per il file CSV con le risorse. |

1. Seleziona **[!UICONTROL Importa]** dalla barra degli strumenti. Dopo l’importazione dei metadati, viene inviata una notifica alla casella in entrata delle notifiche. Passa alla pagina delle proprietà della risorsa e verifica che i valori dei metadati siano importati correttamente per le risorse.

1. Per aggiungere data e marca temporale per importare i metadati, utilizza `YYYY-MM-DDThh:mm:ss.fff-00:00` formato per data e ora. Data e ora sono separate da `T`, `hh` è il numero di ore nel formato 24 ore, `fff` è nanosecondi, e `-00:00` è lo scostamento del fuso orario. Ad esempio: `2020-03-26T11:26:00.000-07:00` è il 26 marzo 2020 alle 11:26:00.000 PST.

   * Il formato della data dipende dall’intestazione della colonna e dal formato in essa contenuto. Ad esempio, se la data è in formato reclamo `yyyy-MM-dd'T'HH:mm:ssXXX` quindi la rispettiva intestazione di colonna deve essere `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`.
   * Il formato di data predefinito è `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`.

<!-- Hidden via cqdoc-17869>

>[!CAUTION]
>
>If the date format does not match `YYYY-MM-DDThh:mm:ss.fff-00:00`, the date values are not set. The date formats of exported metadata CSV file is in the format `YYYY-MM-DDThh:mm:ss-00:00`. If you want to import it, convert it to the acceptable format by adding the nanoseconds value denoted by `fff`.
-->

## Esporta metadati {#export-metadata}

Puoi esportare i metadati per più risorse in formato CSV. I metadati vengono esportati in modo asincrono e non influiscono sulle prestazioni del sistema. Per esportare i metadati, Experience Manager scorre le proprietà del nodo della risorsa `jcr:content/metadata` e i relativi nodi secondari ed esporta le proprietà dei metadati in un file CSV.

Alcuni casi d’uso per l’esportazione in blocco di metadati sono:

* Importa i metadati in un sistema di terze parti durante la migrazione delle risorse.
* Condividere i metadati delle risorse con un team di progetto più ampio.
* Verifica o controlla la conformità dei metadati.
* Esternalizzare i metadati per la localizzazione separata.

1. Seleziona la cartella delle risorse contenente le risorse di cui desideri esportare i metadati. Dalla barra degli strumenti, seleziona **[!UICONTROL Esportare i metadati]**.
1. Nella finestra di dialogo Esportazione metadati, specifica un nome per il file CSV. Per esportare i metadati per le risorse nelle sottocartelle, seleziona **[!UICONTROL Includere le risorse nelle sottocartelle]**.

   ![Interfaccia e opzioni per esportare i metadati di tutte le risorse in una cartella](assets/export_metadata_page.png "Interfaccia e opzioni per esportare i metadati di tutte le risorse in una cartella")

1. Seleziona le opzioni desiderate. Fornisci un nome file e, se necessario, una data.

1. In **[!UICONTROL Proprietà da esportare]** , specificare se si desidera esportare tutte le proprietà o proprietà specifiche. Se selezioni Proprietà selettive da esportare, aggiungi le proprietà desiderate.

1. Dalla barra degli strumenti, tocca o fai clic su **[!UICONTROL Esporta]**. Un messaggio conferma che i metadati vengono esportati. Chiudi il messaggio.
1. Apri la notifica della casella in entrata del processo di esportazione. Seleziona il processo e fai clic su **[!UICONTROL Apri]** nella barra degli strumenti. Per scaricare il file CSV con i metadati, tocca o fai clic su **[!UICONTROL Scarica CSV]** nella barra degli strumenti. Fai clic su **[!UICONTROL Chiudi]**.

   ![Finestra di dialogo per scaricare il file CSV contenente i metadati esportati in blocco](assets/csv_download.png)

   *Figura: Finestra di dialogo per scaricare il file CSV contenente i metadati esportati in blocco.*

>[!MORELIKETHIS]
>
>* [Importare metadati durante l’importazione di risorse in blocco](/help/assets/add-assets.md#asset-bulk-ingestor)

