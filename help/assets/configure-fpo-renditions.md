---
title: Genera solo rappresentazioni per posizionamento per Adobe InDesign
description: Genera rappresentazioni FPO di risorse nuove ed esistenti utilizzando il flusso di lavoro Experience Manager Assets e ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 7%

---

# Genera solo rappresentazioni per posizionamento per Adobe InDesign {#fpo-renditions}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/configure-fpo-renditions.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Quando si inseriscono risorse di grandi dimensioni da Experience Manager nei documenti di Adobe InDesign, un creativo professionista deve attendere per un tempo considerevole dopo che [inserire una risorsa](https://helpx.adobe.com/indesign/using/placing-graphics.html). Nel frattempo, l’utente non può utilizzare l’InDesign. Questo interrompe il flusso creativo e influisce negativamente sull’esperienza utente. Adobe consente di inserire temporaneamente copie trasformate di piccole dimensioni nei documenti InDesign. Quando è necessario l’output finale, ad esempio per i flussi di lavoro di stampa e pubblicazione, le risorse originali a risoluzione completa sostituiscono la rappresentazione temporanea in background. Questo aggiornamento asincrono in background accelera il processo di progettazione per aumentare la produttività e non ostacola il processo creativo.

Assets fornisce rappresentazioni utilizzate solo per il posizionamento (FPO). Queste copie trasformate FPO hanno dimensioni di file ridotte ma hanno le stesse proporzioni. Se per una risorsa non è disponibile una rappresentazione FPO, Adobe InDesign utilizza la risorsa originale. Questo meccanismo di fallback assicura che il flusso di lavoro creativo proceda senza interruzioni.

Experience Manager as a Cloud Service offre funzionalità di elaborazione delle risorse native per il cloud per generare le rappresentazioni FPO. Utilizza i microservizi per le risorse per la generazione di rappresentazioni. Puoi configurare la generazione del rendering delle risorse appena caricate e delle risorse esistenti in Experience Manager.

Di seguito sono riportati i passaggi per generare rappresentazioni FPO:

1. [Creare un profilo di elaborazione](#create-processing-profile).

1. Configura l’Experience Manager per utilizzare questo profilo in [elabora nuove risorse](#generate-renditions-of-new-assets).
1. Utilizzare i profili per [elabora risorse esistenti](#generate-renditions-of-existing-assets).

## Creare un profilo di elaborazione {#create-processing-profile}

Per generare le rappresentazioni dell&#39;oggetto Criteri di gruppo, creare un **[!UICONTROL Profilo di elaborazione]**. I profili utilizzano i microservizi delle risorse native per il cloud per l’elaborazione. Per istruzioni, consulta [creare profili di elaborazione per i microservizi per le risorse](asset-microservices-configure-and-use.md).

Seleziona **[!UICONTROL Crea rappresentazione FPO]** per generare la rappresentazione FPO. Se necessario, fai clic su **[!UICONTROL Aggiungi nuovo]** per aggiungere altre impostazioni di rendering allo stesso profilo.

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## Genera rappresentazioni di nuove risorse {#generate-renditions-of-new-assets}

Per generare rappresentazioni FPO di nuove risorse, applica la **[!UICONTROL Profilo di elaborazione]** nella cartella in proprietà cartella. Nella pagina Proprietà di una cartella, fai clic su **[!UICONTROL Elaborazione risorse]** , seleziona la scheda **[!UICONTROL Profilo FPO]** as a **[!UICONTROL Profilo di elaborazione]** e salva le modifiche. Tutte le nuove risorse caricate nella cartella vengono elaborate utilizzando questo profilo.

![add-fpo-rendition](assets/add-fpo-rendition.png)


## Genera rappresentazioni di risorse esistenti {#generate-renditions-of-existing-assets}

Per generare le rappresentazioni, seleziona le risorse e segui questi passaggi.

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## Visualizza rappresentazioni FPO {#view-fpo-renditions}

Al termine del flusso di lavoro, è possibile controllare le rappresentazioni dell&#39;oggetto Criteri di gruppo generate. Nell’interfaccia utente di Experience Manager Assets, fai clic sulla risorsa per aprire un’anteprima di grandi dimensioni. Apri la barra a sinistra e seleziona **[!UICONTROL Rappresentazioni]**. In alternativa, utilizza la scelta rapida da tastiera `Alt + 3` quando l’anteprima è aperta.

Clic **[!UICONTROL Rendering FPO]** per caricarne l’anteprima. Se necessario, è possibile fare clic con il pulsante destro del mouse sulla copia trasformata e salvarla nel file system. Controlla le rappresentazioni disponibili nella barra a sinistra.

![rendition_list](assets/list-renditions.png)

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
