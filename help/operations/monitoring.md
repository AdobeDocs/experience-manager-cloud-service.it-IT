---
title: Monitoraggio dell’infrastruttura e dei servizi in AEM as a Cloud Service
description: Monitoraggio dell’infrastruttura e dei servizi in AEM as a Cloud Service
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
feature: Operations
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 5%

---

# Monitoraggio dell’infrastruttura e dei servizi in AEM as a Cloud Service {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service offre funzionalità di osservazione e monitoraggio di: infrastruttura, servizi ed esperienza utente. Poiché vengono utilizzate diverse soluzioni e sono presenti diversi livelli di monitoraggio, questa pagina è organizzata in tre sezioni:

* [Disponibilità esterna](#external-availability)
* [Monitoraggio dei moduli interni](#module-monitoring)
* [Osservabilità del cliente](#customer-observability)

AEM as a Cloud Service utilizza centinaia di monitor nativi per il cloud per segnalare in modo continuo lo stato di ciascun ambiente (24 ore su 24, 7 giorni su 7) per 365 giorni all’anno. Le definizioni dei monitor non sono statiche, ma vengono continuamente riviste per migliorare la capacità di rilevamento precoce. Inoltre, Adobe dispone di procedure di chiamata configurate per rispondere agli avvisi.

Se hai bisogno di informazioni su altri tipi di monitoraggio, ad esempio la registrazione o il monitoraggio tramite Cloud Manager, consulta [Risorse aggiuntive](#resources).

## Disponibilità esterna {#external-availability}

La disponibilità esterna è composta da due parti: Service Edge e Custom Monitoring.

### Edge del servizio {#service-edge}

Tutti gli ambienti AEM as a Cloud Service vengono monitorati per verificarne la disponibilità. Tuttavia, il monitoraggio di Service Edge è configurato solo per gli ambienti di produzione e le metriche vengono utilizzate per calcolare il SLA del cliente. Prende in considerazione la fase di esecuzione dell’ambiente e la rete CDN di AEM as a Cloud Service. Service Edge Monitoring utilizza cinque posizioni distinte vicine all’area geografica scelta e verifica periodicamente la disponibilità. L’indisponibilità di un sito attiva un avviso e coinvolge i team e i processi di supporto Adobe on-call.

### Monitoraggio personalizzato {#custom-monitoring}

Con il monitoraggio personalizzato, i clienti possono facoltativamente fornire fino a cinque URL di proprietà Web distinti prima di [andare in diretta](/help/journey-migration/go-live.md). Questi URL devono essere validi e restituire un codice di risposta HTTP 200. Questi monitor supportano i clienti che [portano la propria rete CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) davanti all&#39;Adobe CDN e a qualsiasi routing del traffico esterno utilizzato davanti ad AEM as a Cloud Service che non è sotto il controllo di Adobe. Gli avvisi risultanti dai controlli di monitoraggio personalizzati coinvolgono i team e i processi di supporto di Adobe.

>[!NOTE]
>
> Questa funzionalità è disponibile solo per ambienti di produzione e clienti con [Supporto cloud avanzato](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html?lang=it#support-add-ons). In caso di domande, contatta il team del tuo account di Adobe.

## Monitoraggio di moduli interni {#module-monitoring}

Mentre la disponibilità esterna si concentra sul monitoraggio degli utenti finali, il monitoraggio interno dei moduli osserva se i sottosistemi dell&#39;architettura funzionano nominalmente senza deterioramento delle funzioni o delle prestazioni. In caso di problemi, vengono attivati avvisi che consentono di eseguire le riparazioni automaticamente o tramite il coinvolgimento del team operativo, con l&#39;obiettivo di evitare problemi di disponibilità. Esistono varie categorie di monitor. Di seguito sono riportati alcuni esempi di controlli:

* La percentuale di iowait di CPU non supera una determinata soglia.
* Le ridistribuzioni delle istanze non superano una determinata frequenza.
* L&#39;utilizzo del disco è inferiore a una determinata soglia.
* La dimensione dell’archivio di authoring rientra in alcuni limiti.
* Operazioni di backup completate.
* Lo stato e le prestazioni del database vengono monitorati.
* I servizi cloud di AEM si comportano come previsto, senza code di replica bloccate, dati coerenti e query performanti.

Vengono aggiunti controlli aggiuntivi agli ambienti per i quali è stato eseguito il provisioning per Forms. Le definizioni di controllo non sono statiche e sono soggette a modifiche e aggiornamenti.

## Osservabilità del cliente {#customer-observability}

I clienti possono utilizzare la suite [Monitoraggio delle prestazioni delle applicazioni di New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=it) che fornisce dati sulle prestazioni in tempo reale raccolti e tracciati per l&#39;analisi e la risoluzione dei problemi. Utilizzando la suite di monitoraggio, i clienti possono osservare direttamente varie metriche, quali: metriche delle prestazioni JVM, tempo di transazione per Java™, chiamate esterne in background e chiamate al database.

## Risorse aggiuntive {#resources}

* [Monitoraggio delle prestazioni delle applicazioni New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=it)
* [Registrazione per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html?lang=it)
* [Ambienti di monitoraggio](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html?lang=it)
