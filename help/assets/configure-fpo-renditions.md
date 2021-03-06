---
title: Genera solo rappresentazioni per posizionamento per Adobe InDesign
description: Genera rappresentazioni FPO di risorse nuove ed esistenti utilizzando il flusso di lavoro Experience Manager Assets e ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: 7cc0bd5bbd51edb6f3bc2cfcccfa0a35a0d7a790
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Genera solo rappresentazioni per posizionamento per Adobe InDesign {#fpo-renditions}

Quando si inseriscono risorse di grandi dimensioni dall’Experience Manager ai documenti Adobe InDesign, un professionista deve aspettare per un periodo di tempo considerevole dopo che hanno [inserire una risorsa](https://helpx.adobe.com/indesign/using/placing-graphics.html). Nel frattempo, all’utente è impedito di utilizzare InDesign. Questo interrompe il flusso creativo e influisce negativamente sull’esperienza utente. L’Adobe consente di iniziare temporaneamente il posizionamento di rappresentazioni di piccole dimensioni nei documenti InDesign. Quando l’output finale è necessario, ad esempio per i flussi di lavoro di stampa e pubblicazione, le risorse originali a risoluzione completa sostituiscono il rendering temporaneo in background. Questo aggiornamento asincrono in background velocizza il processo di progettazione per aumentare la produttività e non ostacola il processo creativo.

Assets fornisce rappresentazioni utilizzate solo per il posizionamento (FPO). Queste rappresentazioni FPO hanno dimensioni file ridotte ma hanno le stesse proporzioni. Se per una risorsa non è disponibile un rendering FPO, Adobe InDesign utilizza invece la risorsa originale. Questo meccanismo di fallback assicura che il flusso di lavoro creativo proceda senza interruzioni.

Experience Manager as a Cloud Service offre funzionalità di elaborazione delle risorse native per il cloud per generare le rappresentazioni FPO. Utilizza i microservizi per le risorse per la generazione del rendering. Puoi configurare la generazione di rendering delle risorse appena caricate e delle risorse esistenti in Experience Manager.

Di seguito sono riportati i passaggi per generare rappresentazioni FPO:

1. [Creare un profilo di elaborazione](#create-processing-profile).

1. Configura l’Experience Manager per utilizzare questo profilo in [elaborare nuove risorse](#generate-renditions-of-new-assets).
1. Utilizza i profili per [elaborare le risorse esistenti](#generate-renditions-of-existing-assets).

## Creare un profilo di elaborazione {#create-processing-profile}

Per generare rappresentazioni FPO, crea un **[!UICONTROL Profilo di elaborazione]**. I profili utilizzano i microservizi per le risorse native per il cloud per l’elaborazione. Per istruzioni, consulta [creare profili di elaborazione per i microservizi per le risorse](asset-microservices-configure-and-use.md).

Seleziona **[!UICONTROL Crea rappresentazione FPO]** per generare il rendering FPO. Facoltativamente, fai clic su **[!UICONTROL Aggiungi nuovo]** per aggiungere altre impostazioni di rendering allo stesso profilo.

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## Generare rappresentazioni di nuove risorse {#generate-renditions-of-new-assets}

Per generare rappresentazioni FPO di nuove risorse, applica le **[!UICONTROL Profilo di elaborazione]** nella cartella delle proprietà della cartella. Nella pagina Proprietà di una cartella fare clic su **[!UICONTROL Elaborazione delle risorse]** seleziona la scheda **[!UICONTROL Profilo FPO]** come **[!UICONTROL Profilo di elaborazione]** e salva le modifiche. Tutte le nuove risorse caricate nella cartella vengono elaborate utilizzando questo profilo.

![add-fpo-rendition](assets/add-fpo-rendition.png)


## Genera rendering delle risorse esistenti {#generate-renditions-of-existing-assets}

Per generare rappresentazioni, seleziona le risorse e segui questi passaggi.

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## Visualizzare le rappresentazioni FPO {#view-fpo-renditions}

Puoi controllare le rappresentazioni FPO generate al termine del flusso di lavoro. Nell’interfaccia utente di Experience Manager Assets, fai clic sulla risorsa per aprire un’anteprima di grandi dimensioni. Apri la barra a sinistra e seleziona **[!UICONTROL Rendering]**. In alternativa, utilizza la scelta rapida da tastiera `Alt + 3` quando l&#39;anteprima è aperta.

Fai clic su **[!UICONTROL Rendering FPO]** per caricare la relativa anteprima. Facoltativamente, puoi fare clic con il pulsante destro del mouse sul rendering e salvarlo nel file system. Verifica i rendering disponibili nella barra a sinistra.

![rendition_list](assets/list-renditions.png)
