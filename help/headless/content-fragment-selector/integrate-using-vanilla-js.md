---
title: Integrare il selettore dei frammenti di contenuto utilizzando Vanilla JS
description: Integra il selettore Frammento di contenuto con varie applicazioni Adobe, non Adobe e di terze parti.
role: Admin, User, Developer
source-git-commit: 592e443928f2c9c18ac281027026132b1c877ce3
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---

# Integrare il selettore dei frammenti di contenuto utilizzando Vanilla JS {#integrate-content-fragment-selector-using-vanilla-js}

È possibile integrare qualsiasi applicazione Adobe o non Adobe con l’archivio Adobe Experience Manager (AEM) as a Cloud e selezionare Frammenti di contenuto dall’interno di tale applicazione.

L’integrazione viene eseguita importando il pacchetto Selettore frammento di contenuto e collegandosi a AEM as a Cloud Service utilizzando la libreria JavaScript di Vanilla. Modificare un file `index.html` o qualsiasi file appropriato all&#39;interno dell&#39;applicazione in:

* Definire i dettagli di autenticazione
* Accedere all’archivio di AEM as a Cloud Service
* Configurare le proprietà di visualizzazione del selettore dei frammenti di contenuto

Puoi eseguire l’autenticazione senza definire alcune delle proprietà IMS se:

* sta integrando un&#39;applicazione Adobe in [Unified Shell](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell)
* ha già generato un token IMS per l’autenticazione
