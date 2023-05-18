---
title: Monitoraggio dell’infrastruttura e dei servizi in AEM as a Cloud Service
description: Monitoraggio dell’infrastruttura e dei servizi in AEM as a Cloud Service
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
source-git-commit: 34fed4e64b49ab32e7025c9654d930e3fa362a52
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 5%

---

# Monitoraggio dell’infrastruttura e dei servizi in AEM as a Cloud Service {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service fornisce osservabilità e monitoraggio di: infrastruttura, servizi ed esperienza utente. Poiché vengono utilizzate diverse soluzioni e sono disponibili diversi livelli di monitoraggio, questa pagina è organizzata in tre sezioni:

* [Disponibilità esterna](#external-availability)
* [Monitoraggio del modulo interno](#module-monitoring)
* [Osservabilità del cliente](#customer-observability)

AEM as a Cloud Service utilizza centinaia di monitor nativi per il cloud per segnalare continuamente lo stato di ogni ambiente (24/7) per 365 giorni all&#39;anno. Le definizioni dei monitor non sono statiche, vengono continuamente riviste per migliorare la capacità di rilevamento rapido. Inoltre, Adobe dispone di procedure di chiamata configurate per rispondere agli avvisi.

Se hai bisogno di informazioni su altri tipi di monitoraggio come la registrazione o il monitoraggio tramite Cloud Manager, consulta la [Risorse aggiuntive](#resources) sezione .

## Disponibilità esterna {#external-availability}

La disponibilità esterna è composta da due parti: Monitoraggio Edge di servizio e personalizzato.

### Service Edge {#service-edge}

Tutti gli ambienti as a Cloud Service AEM vengono monitorati per verificare la disponibilità. Tuttavia, Service Edge Monitoring è configurato solo per gli ambienti di produzione e le metriche vengono utilizzate per calcolare lo SLA del cliente. Prende in considerazione il runtime dell’ambiente e il CDN AEM as a Cloud Service. Service Edge Monitoring utilizza cinque posizioni distinte nelle vicinanze dell’area geografica selezionata e verifica periodicamente la disponibilità. L’indisponibilità di un sito attiverà un avviso e coinvolgerà i team e i processi di supporto on-call di Adobe.

### Monitoraggio personalizzato {#custom-monitoring}

Con il monitoraggio personalizzato, i clienti possono fornire fino a cinque URL di proprietà web distinti prima di [andare in diretta](/help/journey-migration/go-live.md). Questi URL devono essere validi e restituire un codice di risposta HTTP 200. Questi monitor supportano i clienti che [portare la propria CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) davanti alla rete CDN di Adobe e a qualsiasi indirizzamento del traffico esterno utilizzato davanti a AEM as a Cloud Service che non è sotto il controllo dell’Adobe. Gli avvisi derivanti dai controlli di monitoraggio personalizzati coinvolgeranno i team e i processi di supporto di Adobe.

>[!NOTE]
>
> Questa funzionalità è disponibile solo per i clienti che dispongono del supporto avanzato Cloud. In caso di domande, solleva un caso di assistenza tramite Admin Console.

## Monitoraggio del modulo interno {#module-monitoring}

Mentre la disponibilità esterna si concentra sul monitoraggio degli utenti finali, il monitoraggio interno dei moduli osserva se i sottosistemi architettonici funzionano in modo nominale senza deterioramento delle caratteristiche o delle prestazioni. In caso di problemi, gli avvisi vengono attivati in modo che le riparazioni possano essere eseguite automaticamente o attraverso il coinvolgimento del team operativo, con l&#39;obiettivo di evitare la disponibilità compromessa. Ci sono varie categorie di monitor, presentati di seguito sono alcuni esempi di controlli:

* La percentuale di utilizzo della CPU non supera una determinata soglia.
* Le ridistribuzioni delle istanze non superano una determinata frequenza.
* L&#39;utilizzo del disco è inferiore a una certa soglia.
* La dimensione dell’archivio dell’autore si trova entro certi limiti.
* Le operazioni di backup sono state completate.
* Monitoraggio dello stato e delle prestazioni del database.
* I servizi AEM Cloud si comportano come previsto, incluse nessuna coda di replica bloccata, dati coerenti e query performanti.

Sono stati aggiunti ulteriori controlli agli ambienti per i quali è stato eseguito il provisioning per Forms. Tieni presente che le definizioni di controllo non sono statiche e sono soggette a modifiche e aggiornamenti.

## Osservabilità del cliente {#customer-observability}

I clienti possono utilizzare [Monitoraggio delle prestazioni delle applicazioni New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) suite che fornisce dati sulle prestazioni in tempo reale raccolti e mappati per analisi e risoluzione dei problemi. Utilizzando la suite di monitoraggio, i clienti possono osservare direttamente varie metriche quali: Metriche delle prestazioni JVM, tempo delle transazioni per Java, chiamate esterne in background e chiamate al database.

## Risorse aggiuntive {#resources}

* [Monitoraggio delle prestazioni delle applicazioni New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [Registrazione per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [Ambienti di monitoraggio](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
