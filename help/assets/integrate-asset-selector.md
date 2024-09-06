---
title: Selettore risorse per [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service]
description: Integra il selettore delle risorse con varie applicazioni di Adobe, non di Adobe e di terze parti.
role: Admin, User
exl-id: 1c0051a3-549c-4783-9fc1-594f424a70c3
source-git-commit: f9f5b2a25933e059cceacf2ba69e23d528858d4b
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 47%

---

# Integra il Selettore risorse utilizzando Vanilla JS {#integration-using-vanilla-js}

È possibile integrare qualsiasi applicazione [!DNL Adobe] o non Adobe con l&#39;archivio [!DNL Experience Manager Assets] e selezionare le risorse dall&#39;interno dell&#39;applicazione. Consulta [Integrazione di Asset Selector con varie applicazioni](#asset-selector-integration-with-apps).

L’integrazione viene eseguita importando il pacchetto Selettore risorse e connettendolo ad Assets as a Cloud Service tramite la libreria JavaScript Vanilla. Modificare un file `index.html` o qualsiasi file appropriato all&#39;interno dell&#39;applicazione in:

* Definire i dettagli di autenticazione
* Accedere all’archivio Assets as a Cloud Service
* Configurare le proprietà di visualizzazione del Selettore risorse

Puoi eseguire l’autenticazione senza definire alcune delle proprietà IMS se:

* Stai integrando un’applicazione [!DNL Adobe] su [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=it).
* Hai già generato un token IMS per l’autenticazione.

## Integrare Asset Selector con varie applicazioni {#asset-selector-integration-with-apps}

È possibile integrare Asset Selector (Selettore risorse) con diverse applicazioni, tra cui:

* [Integrare Asset Selector con un&#39;applicazione  [!DNL Adobe] ](#integrate-asset-selector.md)
* [Integrare Asset Selector con un’applicazione non basata su Adobi](#integrate-asset-selector-non-adobe.md)
* [Integrazione per Dynamic Medie con funzionalità OpenAPI](#integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [Personalizzazione del selettore risorse](/help/assets/asset-selector-customization.md)
>* [Proprietà selettore risorse](/help/assets/asset-selector-properties.md)
>* [Integrare le API di Dynamic Media Open di Asset Selector](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
