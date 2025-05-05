---
title: Come applicare una filigrana alle risorse in AEM?
description: Scopri come aggiungere una filigrana digitale alle risorse in AEM. Le filigrane consentono agli utenti di verificare l’autenticità e la proprietà del copyright delle risorse.
contentOwner: AG
feature: Asset Management,Publishing
role: User, Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 19%

---

# Applicare una filigrana alle risorse {#watermark-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/watermarking.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale a immagini e video. [!DNL Assets] supporta l&#39;applicazione di un&#39;immagine come filigrana ad altri file di immagine. Le filigrane consentono agli utenti di verificare l’autenticità e la proprietà del copyright delle risorse. Inoltre, è possibile utilizzare una filigrana per indicare lo stato di un documento, ad esempio riservato, bozza, validità e così via.

Per configurare [!DNL Experience Manager] per la filigrana delle risorse:

1. Un file PNG viene applicato come filigrana. Carica questo file nel tuo archivio DAM.

1. Passa a **[!UICONTROL Strumenti > Assets > Configurazioni Assets]**.

1. Fare clic su **[!UICONTROL Profilo filigrana di sistema]**.

1. Nella pagina [!UICONTROL Profilo filigrana di sistema], specifica il percorso dell&#39;immagine caricato nell&#39;archivio DAM nel passaggio 1.

1. Nel campo **[!UICONTROL Scala]** specificare la scala della filigrana, compresa tra 0,0 e 1,0, relativa alla larghezza della rappresentazione.

1. Fai clic su **[!UICONTROL Salva]**.

   ![Rilevamento duplicazione risorse](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >Se è stato configurato il profilo di filigrana del sistema utilizzando il file di configurazione `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` (configurazione OSGi), è possibile continuare a utilizzarlo, tuttavia Adobe consiglia di utilizzare il nuovo metodo.


1. [Crea un profilo di elaborazione](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) per utilizzare i microservizi delle risorse per applicare la filigrana.

   ![Profilo di elaborazione risorsa per creare la filigrana](assets/watermark-processing-profile.png)

   Assicurati di abilitare l&#39;interruttore **[!UICONTROL Filigrana]** durante la creazione del profilo di elaborazione.

1. [Applica i profili di elaborazione a una cartella](/help/assets/asset-microservices-configure-and-use.md#use-profiles) per creare risorse con filigrana.

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
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Panoramica dei microservizi per le risorse](/help/assets/asset-microservices-overview.md).
>* [Utilizzare i microservizi per le risorse con i profili di elaborazione](/help/assets/asset-microservices-configure-and-use.md).
