---
title: Profili metadati
description: Informazioni sui profili di metadati per le risorse. Scoprite come creare un profilo di metadati e applicarlo alle risorse delle cartelle.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 68cf71054b1cd7dfb2790122ba4c29854ffdf703
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 23%

---


# Profili metadati {#metadata-profiles}

Un profilo di metadati consente di applicare i metadati predefiniti alle risorse all’interno di una cartella. Create un profilo di metadati e applicatelo a una cartella. Le risorse che successivamente caricate nella cartella ereditano i metadati predefiniti configurati nel profilo di metadati.

## Aggiunta di un profilo di metadati {#adding-a-metadata-profile}

1. Toccate il logo AEM e selezionate **[!UICONTROL Strumenti > Risorse > Profili]** metadati, quindi toccate **[!UICONTROL Crea]**.
1. Immettete un titolo per il profilo di metadati, ad esempio Metadati di esempio, e toccate **[!UICONTROL Invia]**. Viene visualizzato il modulo di modifica per il profilo metadati.
1. Fate clic su un componente e configuratene le proprietà nella scheda **[!UICONTROL Impostazioni]** . Ad esempio, fare clic sul componente **[!UICONTROL Descrizione]** e modificarne le proprietà.
Modificate le seguenti proprietà per il componente **[!UICONTROL Descrizione]** :

   * **[!UICONTROL Etichetta]** campo - Il nome visualizzato della proprietà metadata. È solo per il riferimento utente.
   * **[!UICONTROL Mappa su proprietà]** - Il valore di questa proprietà fornisce il percorso/nome relativo al nodo della risorsa in cui viene salvata nella directory archivio. Il valore deve sempre iniziare con `./` perché indica che il percorso si trova sotto il nodo della risorsa.

      The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. Ad esempio, se specifichi: `/jcr:content/metadata/dc:desc` come nome della proprietà **** Mappa, i AEM Assets memorizzano il valore `dc:desc` nel nodo di metadati della risorsa.

   * **[!UICONTROL Valore]** predefinito - Utilizzate questa proprietà per aggiungere un valore predefinito per il componente metadati. Ad esempio, se specificate &quot;Descrizione personale&quot;, questo valore viene assegnato alla proprietà `dc:desc` nel nodo di metadati della risorsa.

      >[!NOTE]
      >
      >Aggiunta di un valore predefinito a una nuova proprietà di metadati (che non esiste già in . `/jcr:content/metadata` node) per impostazione predefinita, la proprietà e il relativo valore non vengono visualizzati nella pagina Proprietà della risorsa. Per visualizzare la nuova proprietà nella pagina Proprietà delle risorse, modificare il modulo dello schema corrispondente.

1. (Facoltativo) Aggiungi altri componenti alla scheda Modifica modulo dalla scheda **[!UICONTROL Genera modulo]** e configurane le proprietà nella scheda **[!UICONTROL Impostazioni]**. Le seguenti proprietà sono disponibili dalla scheda **[!UICONTROL Genera modulo]**:

| Componente | Proprietà |
|------------------|----------------------------------------------------|
| Intestazione sezione | Etichetta campo, Descrizione |
| Testo su riga singola | Etichetta campo, Mappa sulla proprietà, Valore predefinito |
| Testo con più valori | Etichetta campo, Mappa sulla proprietà, Valore predefinito |
| Numero | Etichetta campo, Mappa sulla proprietà, Valore predefinito |
| Data | Etichetta campo, Mappa sulla proprietà, Valore predefinito |
| Tag standard | Etichetta campo, Mappa sulla proprietà, Valore predefinito, Descrizione |

1. Toccate **[!UICONTROL Chiudi]**. Il profilo metadati viene aggiunto all’elenco dei profili nella pagina **[!UICONTROL Profili]** metadati.

## Copiare un profilo di metadati {#copying-a-metadata-profile}

1. Dalla pagina **[!UICONTROL Profili]** metadati, selezionate un profilo metadati per crearne una copia.
1. Toccate **[!UICONTROL Copia]** dalla barra degli strumenti.
1. Nella finestra di dialogo **[!UICONTROL Copia profilo]** metadati, inserite un titolo per la nuova copia del profilo metadati.
1. Tocca **[!UICONTROL Copia]**. La copia del profilo metadati viene visualizzata nell’elenco apposito della pagina **[!UICONTROL Profili metadati]**.

## Eliminare un profilo di metadati {#deleting-a-metadata-profile}

1. Nella pagina **[!UICONTROL Profili]** metadati, selezionate un profilo da eliminare.
1. Toccate **[!UICONTROL Elimina profili]** metadati nella barra degli strumenti.
1. Nella finestra di dialogo, fare clic su **[!UICONTROL Elimina]** per confermare l’operazione di eliminazione. Il profilo di metadati viene eliminato dall’elenco.

## Applicazione di un profilo di metadati alle cartelle {#applying-a-metadata-profile-to-folders}

Quando assegnate un profilo di metadati a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla cartella principale. Questo significa che potete assegnare un solo profilo di metadati a una cartella. Considerate quindi attentamente la struttura delle cartelle in cui caricare, memorizzare, usare e archiviare le risorse.

Se avete assegnato un profilo di metadati diverso a una cartella, il nuovo profilo sostituisce il profilo precedente. Le risorse di cartella esistenti in precedenza restano invariate. Il nuovo profilo viene applicato alle risorse aggiunte successivamente alla cartella.

Le cartelle a cui è assegnato un profilo sono indicate nell&#39;interfaccia utente in base al nome del profilo visualizzato nel nome della scheda.

Potete applicare i profili di metadati a cartelle specifiche o globalmente a tutte le risorse.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Applicazione di profili di metadati a cartelle specifiche {#applying-metadata-profiles-to-specific-folders}

Puoi applicare un profilo di metadati a una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come applicare i profili di metadati alle cartelle con entrambe le soluzioni.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

You can reprocess assets in a folder that already has an existing video profile that you later changed. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Applicazione dei profili di metadati alle cartelle dall&#39;interfaccia utente Profili {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. Selezionate il profilo di metadati da applicare a una o più cartelle.
1. Tap **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap **[!UICONTROL Done]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

#### Applicazione dei profili di metadati alle cartelle da Proprietà {#applying-metadata-profiles-to-folders-from-properties}

1. Nella barra a sinistra, toccate **[!UICONTROL Risorse]** , quindi individuate la cartella a cui desiderate applicare un profilo di metadati.
1. Sulla cartella, toccate o fate clic sul segno di spunta per selezionarlo, quindi toccate o fate clic su **Proprietà**.
1. Seleziona la scheda **[!UICONTROL Profili metadati]**, fai clic sul profilo dal menu a discesa e infine tocca **Salva]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

### Applicare un profilo di metadati a livello globale {#applying-a-metadata-profile-globally}

Oltre ad applicare un profilo a una cartella, puoi applicarne uno a livello globale in modo che a qualsiasi contenuto caricato in risorse AEM in qualsiasi cartella sia applicato il profilo selezionato.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Per applicare un profilo di metadati a livello globale, effettuate una delle seguenti operazioni**

* Individuate `https://<AEM server>/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e applicate il profilo appropriato e toccate **Salva**.

* Passa a CRXDE Lite al seguente nodo: `/content/dam/jcr:content`. Aggiungete la proprietà `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` e toccate **Salva tutto**.

## Rimozione di un profilo di metadati dalle cartelle {#removing-a-metadata-profile-from-folders}

Quando rimuovete un profilo di metadati da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla cartella principale. Tuttavia, l&#39;elaborazione dei file che si è verificata all&#39;interno delle cartelle rimane intatta.

Puoi rimuovere un profilo di metadati da una cartella direttamente dal menu **Strumenti** oppure, se ti trovi nella cartella, da **Proprietà**. Questa sezione descrive come rimuovere i profili di metadati dalle cartelle con entrambe le soluzioni.

### Rimozione di profili di metadati dalle cartelle tramite l’interfaccia utente Profili {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Toccate o fate clic sul logo AEM e andate a **[!UICONTROL Strumenti > Risorse > Profili]** metadati.
1. Selezionate il profilo di metadati da rimuovere da una o più cartelle.
1. Tocca **[!UICONTROL Rimuovi profilo metadati da cartelle]** e seleziona una o più cartelle da cui vuoi rimuovere il profilo, infine tocca **[!UICONTROL Fine]**.

   Potete confermare che il profilo di metadati non viene più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimozione dei profili di metadati dalle cartelle tramite Proprietà {#removing-metadata-profiles-from-folders-via-properties}

1. Toccate il logo AEM, individuate **[!UICONTROL Risorse]** e quindi la cartella da cui desiderate rimuovere un profilo di metadati.
1. Sulla cartella, toccate il segno di spunta per selezionarlo, quindi toccate **[!UICONTROL Proprietà]**.
1. Seleziona la scheda **[!UICONTROL Profili metadati]**, fai clic su **[!UICONTROL Nessuno]** dal menu a discesa e infine tocca **[!UICONTROL Salva]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.
