---
title: Profili metadati
description: Informazioni sui profili di metadati per le risorse. Scopri come creare un profilo di metadati e applicarlo alle risorse delle cartelle.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 19%

---

# Profili metadati {#metadata-profiles}

Un profilo metadati consente di applicare metadati predefiniti alle risorse all’interno di una cartella. Crea un profilo metadati e applicalo a una cartella. Qualsiasi risorsa da caricare successivamente nella cartella eredita i metadati predefiniti configurati nel profilo metadati.

Un concetto importante relativo all’utilizzo dei profili in Experience Manager Assets è che vengono assegnati alle cartelle. All’interno di un profilo, le impostazioni sono sotto forma di profili di metadati, insieme a profili video o di immagini. Queste impostazioni elaborano il contenuto di una cartella insieme a una delle relative sottocartelle. Pertanto, la modalità di denominazione di file e cartelle, la modalità di organizzazione delle sottocartelle e la gestione dei file all’interno di tali cartelle hanno un impatto significativo sul modo in cui tali risorse vengono elaborate da un profilo.
Utilizzando strategie di denominazione dei file e delle cartelle coerenti e appropriate e buone pratiche in materia di metadati, puoi sfruttare al massimo la tua raccolta di risorse digitali e accertarti che i file giusti siano elaborati dal profilo giusto.

## Aggiungere un profilo di metadati {#adding-a-metadata-profile}

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili metadati]**, quindi fai clic su **[!UICONTROL Crea]**.
1. Inserisci un titolo per il profilo metadati, ad esempio Metadati campione, e tocca **[!UICONTROL Invia]**. Viene visualizzato il modulo di modifica per il profilo metadati.
1. Fai clic su un componente e configurane le proprietà nel **[!UICONTROL Impostazioni]** scheda . Ad esempio, fai clic su **[!UICONTROL Descrizione]** e modificane le proprietà.
Modifica le seguenti proprietà per **[!UICONTROL Descrizione]** componente:

   * **[!UICONTROL Etichetta campo]** - Nome visualizzato della proprietà metadati. È solo per il riferimento utente.
   * **[!UICONTROL Mappa su proprietà]** - Il valore di questa proprietà fornisce il percorso/nome relativo al nodo della risorsa in cui viene salvata nell&#39;archivio. Il valore deve sempre iniziare con `./` perché indica che il percorso si trova sotto il nodo della risorsa.

      Il valore specificato per **[!UICONTROL Mappa su proprietà]** è memorizzato come proprietà sotto il nodo di metadati della risorsa. Ad esempio, se specifichi: `/jcr:content/metadata/dc:desc` come nome **[!UICONTROL Mappa su proprietà]**, [!DNL Adobe Experience Manager Assets] memorizza il valore `dc:desc` nel nodo di metadati della risorsa.

   * **[!UICONTROL Valore predefinito]** - Utilizzare questa proprietà per aggiungere un valore predefinito per il componente metadati. Ad esempio, se specifichi &quot;Descrizione personale&quot;, questo valore viene assegnato alla proprietà `dc:desc` nel nodo di metadati della risorsa.

      >[!NOTE]
      >
      >Aggiunta di un valore predefinito a una nuova proprietà di metadati (che non esiste in `/jcr:content/metadata` node) non visualizza la proprietà e il relativo valore nella pagina Proprietà della risorsa per impostazione predefinita. Per visualizzare la nuova proprietà nel [!UICONTROL Proprietà] modificare il modulo schema corrispondente.

1. (Facoltativo) Aggiungi altri componenti alla scheda Modifica modulo dalla scheda **[!UICONTROL Genera modulo]** e configurane le proprietà nella scheda **[!UICONTROL Impostazioni]**. Le seguenti proprietà sono disponibili dalla scheda **[!UICONTROL Genera modulo]**:

| Componente | Proprietà |
|------------------|----------------------------------------------------|
| Intestazione sezione | Etichetta campo, descrizione |
| Testo su riga singola | Etichetta campo, mappa su proprietà, valore predefinito |
| Testo con più valori | Etichetta campo, mappa su proprietà, valore predefinito |
| Numero | Etichetta campo, mappa su proprietà, valore predefinito |
| Data | Etichetta campo, mappa su proprietà, valore predefinito |
| Tag standard | Etichetta campo, mappa su proprietà, valore predefinito, descrizione |

1. Fai clic su **[!UICONTROL Fine]**. Il profilo metadati viene aggiunto all’elenco dei profili nel **[!UICONTROL Profili metadati]** pagina.

## Copiare un profilo di metadati {#copying-a-metadata-profile}

1. Da **[!UICONTROL Profili metadati]** , seleziona un profilo metadati per crearne una copia.
1. Fai clic su **[!UICONTROL Copia]** dalla barra degli strumenti.
1. In **[!UICONTROL Copia profilo metadati]** immetti un titolo per la nuova copia del profilo metadati.
1. Fai clic su **[!UICONTROL Copia]**. La copia del profilo metadati viene visualizzata nell’elenco apposito della pagina **[!UICONTROL Profili metadati]**.

## Eliminare un profilo di metadati {#deleting-a-metadata-profile}

1. Da **[!UICONTROL Profili metadati]** , seleziona un profilo da eliminare.
1. Fai clic su **[!UICONTROL Elimina profili metadati]** nella barra degli strumenti.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Elimina]** per confermare l’operazione di eliminazione. Il profilo metadati viene eliminato dall’elenco.

## Applicare un profilo di metadati alle cartelle {#applying-a-metadata-profile-to-folders}

Quando assegni un profilo di metadati a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla relativa cartella padre. L’ereditarietà si interrompe quando un profilo diverso viene applicato a una sottocartella. Puoi assegnare un solo profilo di metadati a una cartella. Considera quindi attentamente la struttura delle cartelle in cui caricare, archiviare, utilizzare e archiviare le risorse.

Se hai assegnato un profilo di metadati diverso a una cartella, il nuovo profilo sostituisce il profilo precedente. Le risorse della cartella esistenti in precedenza rimangono invariate. Il nuovo profilo viene applicato alle risorse aggiunte alla cartella dopo la modifica. Puoi applicare i profili di metadati a cartelle specifiche o globalmente a tutte le risorse.

Le cartelle a cui è assegnato un profilo sono indicate nell&#39;interfaccia utente in base al nome del profilo visualizzato nel nome della scheda.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo di metadati esistente che hai successivamente modificato. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Applicare profili di metadati a cartelle specifiche {#applying-metadata-profiles-to-specific-folders}

Puoi applicare un profilo di metadati a una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come applicare i profili di metadati alle cartelle con entrambe le soluzioni.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo video esistente che hai successivamente modificato. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Applicare profili di metadati alle cartelle dall’interfaccia utente Profili {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Passa a **[!UICONTROL Strumenti > Risorse > Profili metadati]**.
1. Seleziona il profilo di metadati da applicare a una o più cartelle.
1. Fai clic su **[!UICONTROL Applica profilo metadati a cartelle]** e seleziona la cartella o più cartelle da utilizzare per ricevere le risorse appena caricate e fai clic su **[!UICONTROL Fine]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

#### Applicare profili di metadati alle cartelle da Proprietà {#applying-metadata-profiles-to-folders-from-properties}

1. Nella barra a sinistra, fai clic su **[!UICONTROL Risorse]** quindi passa alla cartella a cui desideri applicare un profilo di metadati.
1. Nella cartella fare clic o fare clic sul segno di spunta per selezionarlo, quindi fare clic o fare clic su **Proprietà**.
1. Seleziona la **[!UICONTROL Profili metadati]** , quindi seleziona il profilo dal menu a discesa e fai clic su **[!UICONTROL Salva]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

### Applicare un profilo di metadati a livello globale {#applying-a-metadata-profile-globally}

Oltre ad applicare un profilo a una cartella, puoi anche applicarne uno a livello globale in modo che qualsiasi contenuto caricato in [!DNL Experience Manager Assets] in qualsiasi cartella viene applicato il profilo selezionato.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo di metadati esistente che hai successivamente modificato. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Per applicare un profilo di metadati a livello globale, effettua una delle seguenti operazioni**

* Passa a `https://[aem_server]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e applica il profilo appropriato e fai clic su **[!UICONTROL Salva]**.

* Passa a CRXDE Lite al seguente nodo: `/content/dam/jcr:content`. Aggiungi la proprietà `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`. Fai clic su **Salva tutto**.

## Rimozione di un profilo di metadati dalle cartelle {#removing-a-metadata-profile-from-folders}

Quando rimuovi un profilo di metadati da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla relativa cartella principale. Tuttavia, l’elaborazione dei file che si è verificata all’interno delle cartelle rimane intatta.

Puoi rimuovere un profilo di metadati da una cartella direttamente dal menu **Strumenti** oppure, se ti trovi nella cartella, da **Proprietà**. Questa sezione descrive come rimuovere i profili di metadati dalle cartelle con entrambe le soluzioni.

### Rimozione dei profili di metadati dalle cartelle tramite l’interfaccia utente Profiles {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Fai clic sul logo dell’Experience Manager e passa a **[!UICONTROL Strumenti > Risorse > Profili metadati]**.
1. Seleziona il profilo di metadati da rimuovere da una o più cartelle.
1. Fai clic su **[!UICONTROL Rimuovi profilo metadati da cartelle]** e seleziona la cartella o più cartelle da cui vuoi rimuovere un profilo e fai clic su **[!UICONTROL Fine]**.

   Puoi confermare che il profilo di metadati non viene più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimozione dei profili di metadati dalle cartelle tramite Proprietà {#removing-metadata-profiles-from-folders-via-properties}

1. Fai clic sul logo Experience Manager e naviga **[!UICONTROL Risorse]** e quindi alla cartella da cui desideri rimuovere un profilo di metadati.
1. Sulla cartella fare clic sul segno di spunta per selezionarla, quindi fare clic su **[!UICONTROL Proprietà]**.
1. Seleziona la scheda **[!UICONTROL Profili metadati]**, fai clic su **[!UICONTROL Nessuno]** dal menu a discesa e infine tocca **[!UICONTROL Salva]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
