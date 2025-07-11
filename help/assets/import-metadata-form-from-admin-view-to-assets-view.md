---
title: Importa moduli metadati da [!DNL Admin View] a [!DNL Assets View]
description: Questo articolo descrive come importare il modulo metadati da [!DNL Admin View] a [!DNL Assets View]
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 5fb4fe97-486a-4a91-af60-a7182efcc2f9
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# Importa moduli metadati da [!DNL Admin View] a [!DNL Assets View] {#import-metadata-forms-from-admin-view-to-assets-view}

[!DNL Adobe Experience Manager Assets] consente di importare i moduli di metadati e le relative associazioni di cartelle da [!DNL Admin View] a [!DNL Assets View].

## Prima di iniziare{#prerequisites-for-importing-metadata-forms-to-assets-view}

Assicurati di disporre dei diritti di amministratore per importare i moduli di metadati e le relative associazioni di cartelle da [!DNL Admin View] a [!DNL Assets View].

## Importa moduli metadati in [!DNL Assets View]{#import-metadata-forms-to-assets-view}

In qualità di amministratore, eseguire la procedura seguente per importare i moduli di metadati disponibili in [!DNL Admin View] in [!DNL Assets View]:

1. Passare alla home page di [!DNL Assets View] e fare clic su **[!UICONTROL Metadata Forms]** in **[!UICONTROL Impostazioni]** per aprire la pagina **[!UICONTROL Metadata Forms]** contenente l&#39;elenco dei moduli di metadati disponibili in [!DNL Assets View].

   ![pagina moduli metadati](/help/assets/assets/metadata-forms-page.png)

1. Seleziona **[!UICONTROL Importa]**, viene visualizzato un messaggio di elaborazione (ad esempio, *Elaborazione di 2 moduli di metadati in corso... Per piacere, aspetta.*) durante l&#39;importazione. Al termine dell&#39;elaborazione verrà visualizzata la tabella **[!UICONTROL Moduli metadati importazione]**, che include un elenco di moduli metadati disponibili in [!DNL Admin View]. La riga della tabella include, il nome del modulo metadati (in **[!UICONTROL Name]**), le cartelle associate a tale modulo (in **[!UICONTROL Folder Association]**) e un&#39;opzione per visualizzare in anteprima ![preview](/help/assets/assets/Preview.svg) il modulo prima di importarlo.

   ![Importa metadati nella pagina Forms](/help/assets/assets/import-metadata-forms-page.png)

   >[!NOTE]
   > 
   > Nella **[!UICONTROL Importa metadati Forms]**, la tabella con un&#39;etichetta **[!UICONTROL Duplicate]** accanto al nome di un modulo indica che il modulo è già applicato a una cartella in [!DNL Assets View]. L’importazione del modulo duplicato ha la precedenza su quello esistente applicato alla cartella. Per evitare questa sostituzione, rinominare il modulo prima di importarlo. Fare clic sul nome del modulo per rinominarlo.

1. Fai clic su ![seleziona cartella](/help/assets/assets/x.svg) accanto al nome di una cartella (in [!UICONTROL Associazione cartella]) per rimuovere l&#39;associazione della cartella al modulo.
1. Fai clic su ![seleziona cartella](/help/assets/assets/add-to-folder.svg) per selezionare una cartella a cui assegnare il modulo di metadati corrispondente.
1. Fai clic sul cerchio rosso per visualizzare i dettagli dei componenti di metadati o dei mapping nel modulo non supportati e esclusi dall’importazione.

   ![Importa metadati nella pagina Forms](/help/assets/assets/unsupported-import-elements.png)

1. Seleziona uno o più moduli nella tabella e fai clic su **[!UICONTROL Avvia importazione]** per importare i moduli di metadati e le cartelle associate in [!DNL Assets View]. Viene visualizzato un messaggio di elaborazione (ad esempio, *Importazione di 3 moduli di metadati. Per favore, aspetta!*). Una volta completata l&#39;importazione, un messaggio di operazione riuscita conferma che i moduli sono stati importati correttamente e la pagina **[!UICONTROL Metadati Forms]** (di [!DNL Assets View]) visualizza sia i moduli importati di recente che quelli esistenti disponibili in [!DNL Assets View]. In questa pagina è possibile effettuare le seguenti operazioni:

   * Fai clic sull&#39;intestazione della colonna per ordinare la tabella in base a [!UICONTROL Nome], [!UICONTROL Modificato] o [!UICONTROL Autore].
   * Seleziona il modulo importato e fai clic su **[!UICONTROL Rimuovi da cartelle]**, quindi verifica il nome della cartella nel percorso della cartella per verificare che la cartella sia stata trasferita correttamente.

     ![verifica pagina moduli metadati](/help/assets/assets/confirm-ported-folder.png)
   * Seleziona il modulo importato e fai clic su **[!UICONTROL Modifica]** per visualizzare tutte le configurazioni supportate del modulo metadati. Per ulteriori informazioni sui moduli di metadati, sui relativi componenti e sui campi, vedere [Configurazione dei metadati Forms](https://experienceleague.adobe.com/it/docs/experience-manager-assets-essentials/help/metadata#metadata-forms).

   ![verifica pagina moduli metadati](/help/assets/assets/verify-metadata-forms-page.png)

## Verificare i moduli di metadati importati{#Verify-the-imported-metadata-forms}

Dopo aver importato i moduli di metadati da [!DNL Admin View] a [!DNL Assets View], eseguire la procedura seguente per verificare l&#39;importazione:

1. Passa a una delle cartelle associate al modulo di metadati importato.
1. Passa alla pagina dei dettagli di una [risorsa](/help/assets/navigate-assets-view.md#preview-assets) e verifica che i componenti di metadati, i campi dei componenti e i valori dei campi supportati siano sincronizzati da [!DNL Admin View]. Consulta l&#39;articolo [Metadati in Assets Essentials](https://experienceleague.adobe.com/it/docs/experience-manager-assets-essentials/help/metadata) per ulteriori informazioni sui componenti metadati, i campi dei componenti e i valori dei campi.

   >[!NOTE]
   >
   > Nella [[!DNL Assets View] pagina dei dettagli](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/assets-view/metadata-assets-view#metadata-forms) o nella [[!DNL Admin View] pagina delle proprietà](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/assets/administer/metadata-schemas), le modifiche ai valori delle proprietà dei metadati vengono sincronizzate automaticamente tra le due interfacce. Tuttavia, le modifiche strutturali del modulo, ad esempio l’aggiunta o la rimozione di campi o altre modifiche, non vengono sincronizzate.
