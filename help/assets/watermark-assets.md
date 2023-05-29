---
title: Applicare una filigrana alle risorse
description: Aggiungi una filigrana alle risorse digitali.
contentOwner: AG
feature: Asset Management,Publishing
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: 5da4be3ec9af6a00cce8d80b8eea7f7520754a1d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 14%

---

# Applicare una filigrana alle risorse {#watermark-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/watermarking.html) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle immagini. [!DNL Assets] supporta l’applicazione di un’immagine come filigrana ad altri file di immagine. Le filigrane consentono agli utenti di verificare l’autenticità e la proprietà del copyright delle risorse. Inoltre, è possibile utilizzare una filigrana per indicare lo stato di un documento, ad esempio riservato, bozza, validità e così via.

Per configurare [!DNL Experience Manager] per applicare una filigrana alle risorse:

1. Un file PNG viene applicato come filigrana. Carica questo file nel tuo archivio DAM.

1. Accedi a **[!UICONTROL Strumenti > Risorse > Configurazioni risorse]**.

1. Clic **[!UICONTROL Profilo filigrana sistema]**.

1. Il giorno [!UICONTROL Pagina Profilo filigrana sistema], specifica il percorso dell’immagine caricata nell’archivio DAM al passaggio 1.

1. Specificare la scala della filigrana, compresa tra 0,0 e 1,0, relativa alla larghezza della rappresentazione, nel **[!UICONTROL Scala]** campo.

1. Fai clic su **[!UICONTROL Salva]**.

   ![Rilevamento duplicazione risorse](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >Se hai configurato il profilo Filigrana di sistema utilizzando `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` file di configurazione di (configurazione OSGi), puoi continuare a utilizzarlo, tuttavia, l’Adobe consiglia di utilizzare il nuovo metodo.


1. [Creare un profilo di elaborazione](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) per applicare la filigrana sfruttando i microservizi per risorse.

   ![Profilo di elaborazione risorsa per la creazione della filigrana](assets/watermark-processing-profile.png)

   Assicurati di abilitare **[!UICONTROL Filigrana]** durante la creazione del profilo di elaborazione.

1. [Applicare i profili di elaborazione a una cartella](/help/assets/asset-microservices-configure-and-use.md#use-profiles) per creare risorse con filigrana.

## Suggerimenti e limitazioni {#tips-limitations-bestpractices}

* Puoi utilizzare un’unica configurazione per applicare una filigrana a tutte le risorse. Per la filigrana viene utilizzata una sola immagine e la sua larghezza è fissa.
* È possibile posizionare la filigrana al centro senza affiancare.
* Le filigrane basate su testo non sono supportate.

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

>[!MORELIKETHIS]
>
>* [Panoramica dei microservizi per le risorse](/help/assets/asset-microservices-overview.md).
>* [Utilizzare i microservizi per le risorse con i profili di elaborazione](/help/assets/asset-microservices-configure-and-use.md).

