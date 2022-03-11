---
title: AEM Screens as a Cloud Service
description: Questa pagina funge da introduzione ad AEM Screens as a Cloud Service.
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---

# Introduzione ad AEM Screens as a Cloud Service {#introduction-screens-cloud}

Con AEM Screens as a Cloud Service, puoi creare esperienze di digital signage coinvolgenti e dinamiche destinate a essere utilizzate in spazi pubblici. È la prossima evoluzione del prodotto AEM Screens e rappresenta un importante passo avanti in termini di usabilità e scalabilità.

AEM Screens as a Cloud Service è una soluzione di digital signage che consente agli esperti di marketing di creare e gestire esperienze digitali dinamiche su larga scala. Inoltre, prevede diversi tipi di schermi fisici nell&#39;ambito di una strategia di marketing digitale completa. Estende l&#39;offerta omni-channel di Adobe oltre i consueti canali web e mobili per includere anche i canali di digital signage che ci circondano. AEM Screens as a Cloud Service consente esperienze utente più rilevanti, contestuali, produttive e anticipatrici attraverso una profonda comprensione della creazione dei contenuti, dell’assemblaggio dei contenuti, della gestione degli eventi attivati e della riproduzione dei contenuti multimediali per tutti i consumatori e i visitatori in qualsiasi spazio pubblico.

## Informazioni sui componenti in Screens as a Cloud Service {#understanding-components}

Screens as a Cloud Service ha due componenti principali, ovvero:

* **[Content Provider](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en)**, componente aggiuntivo Screens in esecuzione su AEM Cloud Service o su Adobe Managed Services (AMS). Il Content Provider Screens consente all’autore dei contenuti di creare e gestire i canali. Gli autori dei contenuti possono aggiungere nuovi contenuti, modificarli senza preoccuparsi dei dettagli relativi alla creazione di visualizzazioni o alla registrazione del lettore. Il Content Provider fornisce un&#39;astrazione dai dettagli sottostanti dello sviluppo di contenuti, visualizzazioni o registrazione del lettore.

* **[Provider di servizi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=en)**, che è il servizio di gestione del digital signage in esecuzione in Adobe I/O Runtime. Screens Services Provider consente all’autore, agli sviluppatori e agli amministratori di contenuti di gestire display e lettori per la riproduzione di contenuti una volta che il contenuto viene aggiunto ai canali. Inoltre, Screens Services Provider informa l&#39;orchestratore in cui e quando il contenuto verrà riprodotto a un livello elevato.


## Panoramica dell&#39;architettura {#architectural-overview}

In qualità di utente as a Cloud Service di AEM Screens, puoi aggiungere e gestire contenuti nei canali, registrare e gestire display e lettori dalle interfacce progettate appositamente per Screens as a Cloud Service, ovvero: **Provider servizi Screens** e **Provider di contenuti Screens**.

![immagine](/help/screens-cloud/assets/architecture-screenscloud.png)
