---
title: Introduzione ad AEM Screens as a Cloud Service
description: Questa pagina funge da introduzione ad AEM Screens as a Cloud Service.
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 100%

---

# Introduzione ad AEM Screens as a Cloud Service {#introduction-screens-cloud}

Con AEM Screens as a Cloud Service, puoi creare esperienze di segnaletica digitale coinvolgenti e dinamiche destinate a essere utilizzate negli spazi pubblici. È la prossima evoluzione del prodotto AEM Screens e rappresenta un importante passo avanti in termini di usabilità e scalabilità.

AEM Screens as a Cloud Service è una soluzione di segnaletica digitale che consente ai professionisti del marketing di creare e gestire esperienze digitali dinamiche su larga scala. Inoltre, prevede diversi tipi di Screens fisici nell&#39;ambito di una strategia di marketing digitale completa. Estende l’offerta multicanale di Adobe oltre i consueti canali web e mobili per includere anche i canali di segnaletica digitale che ci circondano. AEM Screens as a Cloud Service consente esperienze utente più rilevanti, contestuali, produttive e anticipatrici attraverso una profonda comprensione della creazione dei contenuti, del loro assemblaggio, della gestione degli eventi attivati e della riproduzione dei contenuti multimediali per tutti i consumatori e i visitatori in qualsiasi spazio pubblico.

## Informazioni sui componenti in Screens as a Cloud Service {#understanding-components}

Screens as a Cloud Service ha due componenti principali, ovvero:

* **[Fornitore di contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=it)**, componente aggiuntivo Screens in esecuzione su AEM Cloud Service o su Adobe Managed Services (AMS). Il fornitore di contenuti Screens consente all’autore dei contenuti di creare e gestire i canali. Gli autori dei contenuti possono aggiungere nuovi contenuti, modificarli senza preoccuparsi dei dettagli relativi alla creazione di visualizzazioni o alla registrazione del lettore. Il fornitore di contenuti fornisce un’astrazione dai dettagli sottostanti dello sviluppo di contenuti, visualizzazioni o registrazione del lettore.

* **[Fornitore di servizi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=it)**, che è il servizio di gestione della segnaletica digitale in esecuzione in Adobe I/O Runtime. Fornitore di servizi Screens consente all’autore, agli sviluppatori e agli amministratori di contenuti di gestire display e lettori per la riproduzione di contenuti una volta che il contenuto viene aggiunto ai canali. Inoltre, il fornitore di servizi Screens informa l’orchestratore dove e quando il contenuto verrà riprodotto a un livello elevato.


## Panoramica dell’architettura {#architectural-overview}

In qualità di utente AEM Screens as a Cloud Service, puoi aggiungere e gestire contenuti nei canali, registrare e gestire display e lettori dalle interfacce progettate appositamente per Screens as a Cloud Service, ovvero: **Fornitore di servizi Screens** e **Fornitore di contenuti Screens**.

![immagine](/help/screens-cloud/assets/architecture-screenscloud.png)
