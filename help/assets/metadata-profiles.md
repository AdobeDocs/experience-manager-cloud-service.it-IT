---
title: Profili metadati
description: Scopri i profili di metadati delle risorse. Scopri come creare un profilo di metadati e applicarlo alle risorse delle cartelle.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 21%

---

# Profili metadati {#metadata-profiles}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-config.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Un profilo metadati consente di applicare metadati predefiniti alle risorse all’interno di una cartella. Crea un profilo metadati e applicalo a una cartella. Qualsiasi risorsa caricata successivamente nella cartella eredita i metadati predefiniti configurati nel profilo metadati.

Un concetto importante relativo all’utilizzo dei profili in Experience Manager Assets è che vengono assegnati alle cartelle. All’interno di un profilo sono presenti impostazioni sotto forma di profili di metadati, insieme a profili video o profili immagine. Queste impostazioni elaborano il contenuto di una cartella insieme alle relative sottocartelle. Pertanto, il modo in cui si denominano file e cartelle, si organizzano le sottocartelle e si gestiscono i file all’interno di queste cartelle ha un impatto significativo sul modo in cui tali risorse vengono elaborate da un profilo.
Utilizzando strategie di denominazione dei file e delle cartelle coerenti e appropriate, nonché una buona prassi in materia di metadati, puoi sfruttare al massimo la raccolta di risorse digitali e garantire che i file giusti vengano elaborati dal profilo corretto.

## Aggiungere un profilo di metadati {#adding-a-metadata-profile}

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili metadati]** e quindi fare clic su **[!UICONTROL Crea]**.
1. Immetti un titolo per il profilo metadati, ad esempio Metadati di esempio, e seleziona **[!UICONTROL Invia]**. Viene visualizzato il modulo Modifica per il profilo metadati.
1. Fai clic su un componente e configurane le proprietà nella sezione **[!UICONTROL Impostazioni]** scheda. Ad esempio, fai clic su **[!UICONTROL Descrizione]** e modificarne le proprietà.
Modifica le seguenti proprietà per **[!UICONTROL Descrizione]** componente:

   * **[!UICONTROL Etichetta campo]** : nome visualizzato della proprietà dei metadati. È solo per riferimento utente.
   * **[!UICONTROL Mappa su proprietà]** : il valore di questa proprietà fornisce il percorso/nome relativo del nodo della risorsa in cui viene salvato nell’archivio. Il valore deve sempre iniziare con `./` perché indica che il percorso si trova sotto il nodo della risorsa.

     Il valore specificato per **[!UICONTROL Mappa su proprietà]** viene memorizzato come proprietà sotto il nodo di metadati della risorsa. Ad esempio, se specifichi: `/jcr:content/metadata/dc:desc` come nome di **[!UICONTROL Mappa su proprietà]**, [!DNL Adobe Experience Manager Assets] memorizza il valore `dc:desc` nel nodo dei metadati della risorsa.

   * **[!UICONTROL Valore predefinito]** : utilizza questa proprietà per aggiungere un valore predefinito per il componente metadati. Ad esempio, se specifichi &quot;Descrizione&quot; questo valore viene assegnato alla proprietà `dc:desc` nel nodo dei metadati della risorsa.

     >[!NOTE]
     >
     >Aggiunta di un valore predefinito a una nuova proprietà di metadati (che non esiste in `/jcr:content/metadata` node) non mostra la proprietà e il relativo valore nella pagina Proprietà della risorsa per impostazione predefinita. Per visualizzare la nuova proprietà in [!UICONTROL Proprietà] , modificare il modulo schema corrispondente.

1. (Facoltativo) Aggiungi altri componenti alla scheda Modifica modulo dalla scheda **[!UICONTROL Genera modulo]** e configurane le proprietà nella scheda **[!UICONTROL Impostazioni]**. Le seguenti proprietà sono disponibili dalla scheda **[!UICONTROL Genera modulo]**:

| Componente | Proprietà |
|------------------|----------------------------------------------------|
| Intestazione sezione | Etichetta campo, descrizione |
| Testo su riga singola | Etichetta campo, Mappa su proprietà, Valore predefinito |
| Testo con più valori | Etichetta campo, Mappa su proprietà, Valore predefinito |
| Numero | Etichetta campo, Mappa su proprietà, Valore predefinito |
| Data | Etichetta campo, Mappa su proprietà, Valore predefinito |
| Tag standard | Etichetta campo, Mappa su proprietà, Valore predefinito, Descrizione |

1. Clic **[!UICONTROL Fine]**. Il profilo metadati viene aggiunto all’elenco dei profili nel **[!UICONTROL Profili metadati]** pagina.

## Copiare un profilo di metadati {#copying-a-metadata-profile}

1. Dalla sezione **[!UICONTROL Profili metadati]** , selezionare un profilo metadati per crearne una copia.
1. Clic **[!UICONTROL Copia]** dalla barra degli strumenti.
1. In **[!UICONTROL Copia profilo metadati]** immetti un titolo per la nuova copia del profilo metadati.
1. Clic **[!UICONTROL Copia]**. La copia del profilo metadati viene visualizzata nell’elenco apposito della pagina **[!UICONTROL Profili metadati]**.

## Eliminare un profilo di metadati {#deleting-a-metadata-profile}

1. Dalla sezione **[!UICONTROL Profili metadati]** , selezionare un profilo da eliminare.
1. Clic **[!UICONTROL Elimina profili metadati]** nella barra degli strumenti.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Elimina]** per confermare l&#39;operazione di eliminazione. Il profilo metadati viene eliminato dall’elenco.

## Applicare un profilo di metadati alle cartelle {#applying-a-metadata-profile-to-folders}

Quando si assegna un profilo di metadati a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla relativa cartella principale. L’ereditarietà si interrompe quando un profilo diverso viene applicato a una sottocartella. Puoi assegnare un solo profilo di metadati a una cartella. Pertanto, considera attentamente la struttura di cartelle in cui caricare, archiviare, utilizzare e archiviare le risorse.

Se hai assegnato un profilo di metadati diverso a una cartella, il nuovo profilo sostituisce quello precedente. Le risorse della cartella esistenti in precedenza rimangono invariate. Il nuovo profilo viene applicato alle risorse aggiunte alla cartella dopo la modifica. Puoi applicare profili di metadati a cartelle specifiche o a livello globale a tutte le risorse.

Le cartelle a cui è assegnato un profilo sono indicate nell’interfaccia utente dal nome del profilo che appare nel nome della scheda.

È possibile rielaborare le risorse in una cartella che dispone già di un profilo di metadati esistente che è stato successivamente modificato. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Applicare profili di metadati a cartelle specifiche {#applying-metadata-profiles-to-specific-folders}

Puoi applicare un profilo di metadati a una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come applicare i profili di metadati alle cartelle con entrambe le soluzioni.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo video modificato in seguito. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Applicare profili metadati alle cartelle dall’interfaccia utente Profili {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Accedi a **[!UICONTROL Strumenti > Risorse > Profili metadati]**.
1. Seleziona il profilo di metadati da applicare a una o più cartelle.
1. Clic **[!UICONTROL Applicare il profilo metadati alle cartelle]** e seleziona la cartella o le cartelle in cui desideri ricevere le risorse appena caricate, quindi fai clic su **[!UICONTROL Fine]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

#### Applicare profili di metadati alle cartelle da Proprietà {#applying-metadata-profiles-to-folders-from-properties}

1. Nella barra a sinistra, fai clic su **[!UICONTROL Risorse]** quindi passa alla cartella a cui desideri applicare un profilo di metadati.
1. Sulla cartella, seleziona il segno di spunta per selezionarla, quindi seleziona **Proprietà**.
1. Seleziona la **[!UICONTROL Profili metadati]** e selezionare il profilo dal menu a discesa e fare clic su **[!UICONTROL Salva]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

### Applicare un profilo di metadati a livello globale {#applying-a-metadata-profile-globally}

Oltre ad applicare un profilo a una cartella, puoi anche applicarne uno a livello globale, in modo che qualsiasi contenuto caricato in [!DNL Experience Manager Assets] in qualsiasi cartella è applicato il profilo selezionato.

È possibile rielaborare le risorse in una cartella che dispone già di un profilo di metadati esistente che è stato successivamente modificato. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Per applicare un profilo di metadati a livello globale, effettua una delle seguenti operazioni**

* Accedi a `https://[aem_server]/mnt/overlay/dam/gui/content/assets/v2/foldersharewizard.html/content/dam` e applica il profilo appropriato e fai clic su **[!UICONTROL Salva]**.

* Passa a CRXDE Liti al seguente nodo: `/content/dam/jcr:content`. Aggiungi la proprietà `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`. Clic **Salva tutto**.

## Rimozione di un profilo di metadati dalle cartelle {#removing-a-metadata-profile-from-folders}

Quando rimuovi un profilo di metadati da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla relativa cartella principale. Tuttavia, qualsiasi elaborazione dei file che si è verificata all’interno delle cartelle rimane intatta.

Puoi rimuovere un profilo di metadati da una cartella direttamente dal menu **Strumenti** oppure, se ti trovi nella cartella, da **Proprietà**. Questa sezione descrive come rimuovere i profili di metadati dalle cartelle con entrambe le soluzioni.

### Rimozione dei profili di metadati dalle cartelle tramite l’interfaccia utente Profili {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Fai clic sul logo dell’Experience Manager e passa a **[!UICONTROL Strumenti > Risorse > Profili metadati]**.
1. Seleziona il profilo di metadati da rimuovere da una o più cartelle.
1. Clic **[!UICONTROL Rimuovi profilo metadati dalle cartelle]** e seleziona la cartella o le cartelle da cui vuoi rimuovere un profilo e fai clic su **[!UICONTROL Fine]**.

   Puoi confermare che il profilo di metadati non è più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimozione dei profili di metadati dalle cartelle tramite Proprietà {#removing-metadata-profiles-from-folders-via-properties}

1. Fai clic sul logo dell’Experience Manager e naviga **[!UICONTROL Risorse]** e quindi alla cartella da cui desideri rimuovere un profilo di metadati.
1. Nella cartella fare clic sul segno di spunta per selezionarla e quindi fare clic su **[!UICONTROL Proprietà]**.
1. Seleziona la scheda **[!UICONTROL Profili metadati]**, fai clic su **[!UICONTROL Nessuno]** dal menu a discesa e infine tocca **[!UICONTROL Salva]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
