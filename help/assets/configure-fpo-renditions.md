---
title: Genera solo rappresentazioni per posizionamento per Adobe InDesign
description: Genera rappresentazioni FPO (solo per posizionamento) di risorse nuove ed esistenti tramite il flusso di lavoro di Experience Manager Assets e ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 12%

---

# Genera solo rappresentazioni per posizionamento per Adobe InDesign {#fpo-renditions}

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
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/assets/administer/configure-fpo-renditions) |
| AEM as a Cloud Service | Questo articolo |

Quando inserisci risorse di grandi dimensioni da Experience Manager nei documenti di Adobe InDesign, un professionista deve attendere molto tempo dopo aver [inserito una risorsa](https://helpx.adobe.com/it/indesign/using/placing-graphics.html). Nel frattempo, l’utente non può utilizzare InDesign. Questo interrompe il flusso creativo e influisce negativamente sull’esperienza utente. Adobe consente di inserire temporaneamente nei documenti di InDesign copie trasformate di piccole dimensioni. Quando è necessario l’output finale, ad esempio per i flussi di lavoro di stampa e pubblicazione, le risorse originali a risoluzione completa sostituiscono la rappresentazione temporanea in background. Questo aggiornamento asincrono in background accelera il processo di progettazione per aumentare la produttività e non ostacola il processo creativo.

Assets fornisce copie trasformate utilizzate solo per il posizionamento (FPO). Queste copie trasformate FPO hanno dimensioni di file ridotte ma hanno le stesse proporzioni. Se per una risorsa non è disponibile una rappresentazione FPO, Adobe InDesign utilizza la risorsa originale. Questo meccanismo di fallback assicura che il flusso di lavoro creativo proceda senza interruzioni.

Experience Manager as a Cloud Service offre funzionalità di elaborazione delle risorse native per il cloud per generare le rappresentazioni FPO. Utilizza i microservizi per le risorse per la generazione di rappresentazioni. Puoi configurare la generazione del rendering delle risorse appena caricate e delle risorse esistenti in Experience Manager.

Di seguito sono riportati i passaggi per generare rappresentazioni FPO:

1. [Crea un profilo di elaborazione](#create-processing-profile).

1. Configura Experience Manager per utilizzare questo profilo per [elaborare nuove risorse](#generate-renditions-of-new-assets).
1. Utilizza i profili per [elaborare le risorse esistenti](#generate-renditions-of-existing-assets).

## Creare un profilo di elaborazione {#create-processing-profile}

Per generare le rappresentazioni dell&#39;oggetto Criteri di gruppo, creare un **[!UICONTROL profilo di elaborazione]**. I profili utilizzano i microservizi delle risorse native per il cloud per l’elaborazione. Per istruzioni, consulta [creare profili di elaborazione per i microservizi per le risorse](asset-microservices-configure-and-use.md).

Selezionare **[!UICONTROL Crea rappresentazione oggetto Criteri di gruppo]** per generare la rappresentazione oggetto Criteri di gruppo. Facoltativamente, fare clic su **[!UICONTROL Aggiungi nuovo]** per aggiungere altre impostazioni di rendering allo stesso profilo.

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## Genera rappresentazioni di nuove risorse {#generate-renditions-of-new-assets}

Per generare le rappresentazioni dell&#39;oggetto Criteri di gruppo delle nuove risorse, applicare il **[!UICONTROL profilo di elaborazione]** alla cartella nelle proprietà della cartella. Nella pagina Proprietà di una cartella, fare clic sulla scheda **[!UICONTROL Elaborazione risorse]**, selezionare il **[!UICONTROL profilo FPO]** come **[!UICONTROL Profilo elaborazione]** e salvare le modifiche. Tutte le nuove risorse caricate nella cartella vengono elaborate utilizzando questo profilo.

![add-fpo-rendition](assets/add-fpo-rendition.png)


## Genera rappresentazioni di risorse esistenti {#generate-renditions-of-existing-assets}

Per generare le rappresentazioni, seleziona le risorse e segui questi passaggi.

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## Visualizza rappresentazioni FPO {#view-fpo-renditions}

È possibile verificare che le copie trasformate dell&#39;oggetto Criteri di gruppo generate vengano eseguite al termine del flusso di lavoro. Nell’interfaccia utente di Experience Manager Assets, fai clic sulla risorsa per aprire un’anteprima di grandi dimensioni. Apri la barra a sinistra e seleziona **[!UICONTROL Rappresentazioni]**. In alternativa, utilizzare la scelta rapida da tastiera `Alt + 3` quando l&#39;anteprima è aperta.

Fare clic su **[!UICONTROL Rendering FPO]** per caricarne l&#39;anteprima. Se necessario, è possibile fare clic con il pulsante destro del mouse sulla copia trasformata e salvarla nel file system. Controlla le rappresentazioni disponibili nella barra a sinistra.

![elenco_rappresentazioni](assets/list-renditions.png)

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