---
title: Introduzione ad AEM Screens as a Cloud Service
description: Cos’è AEM Screens as a Cloud Service.
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: 53086e2ec6d9d962a8f1cb1cc40f0601da74ac63
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 59%

---


# Introduzione ad AEM Screens as a Cloud Service {#introduction-screens-cloud}

Con Adobe Experience Manager (AEM) Screens as a Cloud Service, puoi creare esperienze di segnaletica digitale coinvolgenti e dinamiche destinate a essere utilizzate negli spazi pubblici. È la prossima evoluzione del prodotto AEM Screens e rappresenta un importante passo avanti in termini di usabilità e scalabilità.

AEM Screens as a Cloud Service è una soluzione di segnaletica digitale che consente ai professionisti del marketing di creare e gestire esperienze digitali dinamiche su larga scala. Inoltre, prevede diversi tipi di schermi fisici come parte di una strategia di marketing digitale completa. Estende l’offerta multicanale di Adobe oltre i consueti canali web e mobili per includere anche i canali di segnaletica digitale che ci circondano. AEM Screens as a Cloud Service consente esperienze utente più rilevanti, contestuali, produttive e anticipatrici attraverso una profonda comprensione della creazione dei contenuti, del loro assemblaggio, della gestione degli eventi attivati e della riproduzione dei contenuti multimediali per tutti i consumatori e i visitatori in qualsiasi spazio pubblico.

## Informazioni sui componenti in Screens as a Cloud Service {#understanding-components}

Screens as a Cloud Service ha due componenti principali, ovvero:

* **[Fornitore di contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html)**, componente aggiuntivo Screens in esecuzione su AEM Cloud Service o su Adobe Managed Services (AMS). Il fornitore di contenuti Screens consente all’autore dei contenuti di creare e gestire i canali. Gli autori dei contenuti possono aggiungere nuovi contenuti, modificarli senza preoccuparsi dei dettagli relativi alla creazione di visualizzazioni o alla registrazione del lettore. Il fornitore di contenuti fornisce un’astrazione dai dettagli sottostanti dello sviluppo di contenuti, visualizzazioni o registrazione del lettore.

* **[Provider di servizi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html)**, che è il servizio di gestione del digital signage in esecuzione su Adobe I/O Runtime. Screens Services Provider consente ad autori, sviluppatori e amministratori di contenuti di gestire visualizzazioni e lettori per la riproduzione dei contenuti una volta aggiunti ai canali. Inoltre, Screens Services Provider informa l&#39;orchestratore su dove e quando il contenuto verrà riprodotto ad alto livello.


## Panoramica dell’architettura {#architectural-overview}

In qualità di utente di AEM Screens as a Cloud Service, puoi aggiungere e gestire contenuti nei canali. È possibile registrare e gestire visualizzazioni e lettori dalle interfacce progettate appositamente per Screens as a Cloud Service, ovvero **Screens Services Provider** e **Screens Content Provider**.

![Panoramica dell&#39;architettura](/help/screens-cloud/assets/architecture-screenscloud.png)
