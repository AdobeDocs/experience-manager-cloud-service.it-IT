---
title: Archivia ed estrai file in [!DNL Assets]
description: Scopri come estrarre le risorse per la modifica e archiviarle di nuovo al termine delle modifiche.
contentOwner: AG
feature: Asset Management
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 11%

---

# Archivia ed estrai file in [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Medie con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione per gli sviluppatori di AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/check-out-and-submit-assets.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di estrarre le risorse per la modifica e archiviarle nuovamente dopo aver completato le modifiche. Dopo aver estratto una risorsa, solo tu puoi modificarla, annotarla, pubblicarla, spostarla o eliminarla. Il Check-Out di una risorsa blocca la risorsa. Gli altri utenti non possono eseguire nessuna di queste operazioni sulla risorsa finché non la sottoponi nuovamente a check-in in [!DNL Assets]. Tuttavia, possono comunque modificare i metadati della risorsa bloccata.

Per poter estrarre/archiviare le risorse, è necessario disporre dell&#39;accesso in scrittura.

Questa funzione impedisce ad altri utenti di ignorare le modifiche apportate da un autore, qualora più utenti collaborino alla modifica dei flussi di lavoro tra i team.

## Estrarre le risorse {#checking-out-assets}

1. Dall&#39;interfaccia utente [!DNL Assets], selezionare la risorsa da estrarre. È inoltre possibile selezionare più risorse da estrarre.

1. Dalla barra degli strumenti, fare clic su **[!UICONTROL Estrai]**. L&#39;opzione **[!UICONTROL Estrai]** attiva **[!UICONTROL Archivia]**.
Per verificare se altri utenti possono modificare la risorsa estratta, accedere come un altro utente. L&#39;icona ![icona blocco estrazione](assets/do-not-localize/checkout_lock.png) viene visualizzata nella miniatura della risorsa estratta.

   ![icona di estrazione nella vista a schede](assets/checkout-icon-card-view.png)

   Seleziona la risorsa. Nella barra degli strumenti non sono visualizzate opzioni che consentono di modificare, annotare, pubblicare o eliminare la risorsa.

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   Per modificare i metadati della risorsa bloccata, fai clic su **[!UICONTROL Visualizza proprietà]**.

1. Fai clic su **[!UICONTROL Modifica]** per aprire la risorsa in modalità di modifica.

1. Modifica la risorsa e salva le modifiche. Ad esempio, ritaglia l’immagine e salva. Puoi anche scegliere di annotare o pubblicare la risorsa.

1. Seleziona la risorsa modificata dall&#39;interfaccia [!DNL Assets] e fai clic su **[!UICONTROL Archivia]** nella barra degli strumenti. La risorsa modificata è archiviata in [!DNL Assets] ed è disponibile per la modifica per altri utenti.

## Check-in forzato {#forced-check-in}

Gli amministratori possono archiviare le risorse estratte da altri utenti.

1. Accedere a [!DNL Assets] come amministratore.
1. Dall&#39;interfaccia utente di [!DNL Assets], selezionare una o più risorse estratte da altri utenti.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Dalla barra degli strumenti, fare clic su **[!UICONTROL Blocco versione]**. La risorsa viene archiviata nuovamente e può essere modificata da altri utenti.

## Best practice e limitazioni {#tips-limitations}

* È possibile eliminare una *cartella* contenente file di risorse estratti. Prima di eliminare una cartella, accertati che gli utenti non estraggano risorse digitali.

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

>[!MORELIKETHIS]
>
>* [Informazioni su archiviazione ed estrazione nell&#39;app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2) [!DNL Experience Manager] 
>* [Esercitazione video per comprendere l&#39;archiviazione e l&#39;estrazione in [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)
