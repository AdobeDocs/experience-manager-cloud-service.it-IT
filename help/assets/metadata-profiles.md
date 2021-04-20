---
title: Profili metadati
description: Informazioni sui profili di metadati per le risorse. Scopri come creare un profilo di metadati e applicarlo alle risorse delle cartelle.
contentOwner: AG
feature: Metadata
role: Business Practitioner,Administrator
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 20%

---


# Profili metadati {#metadata-profiles}

Un profilo metadati consente di applicare metadati predefiniti alle risorse all’interno di una cartella. Crea un profilo metadati e applicalo a una cartella. Qualsiasi risorsa da caricare successivamente nella cartella eredita i metadati predefiniti configurati nel profilo metadati.

## Aggiungere un profilo di metadati {#adding-a-metadata-profile}

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili metadati]**, quindi fai clic su **[!UICONTROL Crea]**.
1. Inserisci un titolo per il profilo metadati, ad esempio Metadati campione, e tocca **[!UICONTROL Invia]**. Viene visualizzato il modulo di modifica per il profilo metadati.
1. Fai clic su un componente e configurane le proprietà nella scheda **[!UICONTROL Impostazioni]** . Ad esempio, fai clic sul componente **[!UICONTROL Descrizione]** e modificane le proprietà.
Modifica le seguenti proprietà per il componente **[!UICONTROL Descrizione]** :

   * **[!UICONTROL Etichetta campo]** : il nome visualizzato della proprietà metadati. È solo per il riferimento utente.
   * **[!UICONTROL Mappa su proprietà]** : il valore di questa proprietà fornisce il percorso/nome relativo al nodo della risorsa in cui viene salvata nell’archivio. Il valore deve sempre iniziare con `./` perché indica che il percorso si trova sotto il nodo della risorsa.

      Il valore specificato per **[!UICONTROL Mappa su proprietà]** viene memorizzato come proprietà sotto il nodo di metadati della risorsa. Ad esempio, se specifichi: `/jcr:content/metadata/dc:desc` come nome di  **[!UICONTROL Mappa su proprietà]**,  [!DNL Adobe Experience Manager Assets] memorizza il valore  `dc:desc` nel nodo di metadati della risorsa.

   * **[!UICONTROL Valore predefinito]** : utilizza questa proprietà per aggiungere un valore predefinito per il componente metadati. Ad esempio, se specifichi &quot;La mia descrizione&quot;, questo valore viene assegnato alla proprietà `dc:desc` nel nodo di metadati della risorsa.

      >[!NOTE]
      >
      >Per impostazione predefinita, l’aggiunta di un valore predefinito a una nuova proprietà di metadati (che non esiste nel nodo `/jcr:content/metadata` ) non visualizza la proprietà e il relativo valore nella pagina Proprietà della risorsa. Per visualizzare la nuova proprietà nella pagina [!UICONTROL Proprietà], modificare il modulo schema corrispondente.

1. (Facoltativo) Aggiungi altri componenti alla scheda Modifica modulo dalla scheda **[!UICONTROL Genera modulo]** e configurane le proprietà nella scheda **[!UICONTROL Impostazioni]**. Le seguenti proprietà sono disponibili dalla scheda **[!UICONTROL Genera modulo]**:

| Componente | Proprietà |
|------------------|----------------------------------------------------|
| Intestazione sezione | Etichetta campo, descrizione |
| Testo su riga singola | Etichetta campo, mappa su proprietà, valore predefinito |
| Testo con più valori | Etichetta campo, mappa su proprietà, valore predefinito |
| Numero | Etichetta campo, mappa su proprietà, valore predefinito |
| Data | Etichetta campo, mappa su proprietà, valore predefinito |
| Tag standard | Etichetta campo, mappa su proprietà, valore predefinito, descrizione |

1. Fare clic su **[!UICONTROL Fine]**. Il profilo metadati viene aggiunto all’elenco dei profili nella pagina **[!UICONTROL Profili metadati]** .

## Copiare un profilo di metadati {#copying-a-metadata-profile}

1. Dalla pagina **[!UICONTROL Profili metadati]** , seleziona un profilo metadati per crearne una copia.
1. Fai clic su **[!UICONTROL Copia]** nella barra degli strumenti.
1. Nella finestra di dialogo **[!UICONTROL Copia profilo metadati]**, immetti un titolo per la nuova copia del profilo metadati.
1. Fate clic su **[!UICONTROL Copia]**. La copia del profilo metadati viene visualizzata nell’elenco apposito della pagina **[!UICONTROL Profili metadati]**.

## Eliminare un profilo di metadati {#deleting-a-metadata-profile}

1. Dalla pagina **[!UICONTROL Profili metadati]** , seleziona un profilo da eliminare.
1. Fai clic su **[!UICONTROL Elimina profili metadati]** nella barra degli strumenti.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Elimina]** per confermare l’operazione di eliminazione. Il profilo metadati viene eliminato dall’elenco.

## Applicare un profilo di metadati alle cartelle {#applying-a-metadata-profile-to-folders}

Quando assegni un profilo di metadati a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla relativa cartella padre. Ciò significa che puoi assegnare un solo profilo di metadati a una cartella. Considera attentamente la struttura delle cartelle in cui caricare, archiviare, utilizzare e archiviare le risorse.

Se hai assegnato un profilo di metadati diverso a una cartella, il nuovo profilo sostituisce il profilo precedente. Le risorse della cartella esistenti in precedenza rimangono invariate. Il nuovo profilo viene applicato alle risorse aggiunte successivamente alla cartella.

Le cartelle a cui è assegnato un profilo sono indicate nell&#39;interfaccia utente in base al nome del profilo visualizzato nel nome della scheda.

Puoi applicare i profili di metadati a cartelle specifiche o globalmente a tutte le risorse.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo di metadati esistente che hai successivamente modificato. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Applicare profili di metadati a cartelle specifiche {#applying-metadata-profiles-to-specific-folders}

Puoi applicare un profilo di metadati a una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come applicare i profili di metadati alle cartelle con entrambe le soluzioni.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo video esistente che hai successivamente modificato. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Applicare profili di metadati alle cartelle dall&#39;interfaccia utente Profili {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Passa a **[!UICONTROL Strumenti > Risorse > Profili metadati]**.
1. Seleziona il profilo di metadati da applicare a una o più cartelle.
1. Fai clic su **[!UICONTROL Applica profilo metadati a cartelle]** e seleziona la cartella o le cartelle multiple da utilizzare per ricevere le risorse appena caricate, quindi fai clic su **[!UICONTROL Fine]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

#### Applicare profili di metadati alle cartelle da Proprietà {#applying-metadata-profiles-to-folders-from-properties}

1. Nella barra a sinistra, fai clic su **[!UICONTROL Risorse]**, quindi individua la cartella a cui desideri applicare un profilo di metadati.
1. Nella cartella, fai clic sul segno di spunta o fai clic sul segno di spunta per selezionarlo, quindi fai clic su **Proprietà**.
1. Seleziona la scheda **[!UICONTROL Profili metadati]** e seleziona il profilo dal menu a discesa, quindi fai clic su **[!UICONTROL Salva]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

### Applicare un profilo di metadati a livello globale {#applying-a-metadata-profile-globally}

Oltre ad applicare un profilo a una cartella, puoi anche applicarne uno a livello globale in modo che a qualsiasi contenuto caricato in [!DNL Experience Manager Assets] in una cartella sia applicato il profilo selezionato.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo di metadati esistente che hai successivamente modificato. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Per applicare un profilo di metadati a livello globale, effettua una delle seguenti operazioni**

* Passa a `https://<AEM server>/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e applica il profilo appropriato, quindi fai clic su **Salva**.

* Passa a CRXDE Lite al seguente nodo: `/content/dam/jcr:content`. Aggiungi la proprietà `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`. Fare clic su **Salva tutto**.

## Rimozione di un profilo di metadati dalle cartelle {#removing-a-metadata-profile-from-folders}

Quando rimuovi un profilo di metadati da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla relativa cartella principale. Tuttavia, l’elaborazione dei file che si è verificata all’interno delle cartelle rimane intatta.

Puoi rimuovere un profilo di metadati da una cartella direttamente dal menu **Strumenti** oppure, se ti trovi nella cartella, da **Proprietà**. Questa sezione descrive come rimuovere i profili di metadati dalle cartelle con entrambe le soluzioni.

### Rimozione dei profili di metadati dalle cartelle tramite l’interfaccia utente Profiles {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Fai clic sul logo AEM e passa a **[!UICONTROL Strumenti > Risorse > Profili metadati]**.
1. Seleziona il profilo di metadati da rimuovere da una o più cartelle.
1. Fai clic su **[!UICONTROL Rimuovi profilo metadati da cartelle]**, seleziona la cartella o le cartelle multiple da cui vuoi rimuovere un profilo e fai clic su **[!UICONTROL Fine]**.

   Puoi confermare che il profilo di metadati non viene più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimozione dei profili di metadati dalle cartelle tramite Proprietà {#removing-metadata-profiles-from-folders-via-properties}

1. Fai clic sul logo AEM e passa a **[!UICONTROL Risorse]**, quindi alla cartella da cui vuoi rimuovere un profilo di metadati.
1. Nella cartella, fai clic sul segno di spunta per selezionarlo, quindi fai clic su **[!UICONTROL Proprietà]**.
1. Seleziona la scheda **[!UICONTROL Profili metadati]**, fai clic su **[!UICONTROL Nessuno]** dal menu a discesa e infine tocca **[!UICONTROL Salva]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.
