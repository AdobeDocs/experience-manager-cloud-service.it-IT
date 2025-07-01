---
title: Distribuzione di frammenti di contenuto di AEM con OpenAPI
description: Scopri la distribuzione di frammenti di contenuto AEM con OpenAPI
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 28d0d6bdfd9e6f1c1483bed7c5e65df340e8b559
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 2%

---


# Distribuzione di frammenti di contenuto di AEM con OpenAPI {#aem-content-fragment-delivery-with-openapi}

In Adobe Experience Manager (AEM) as a Cloud Service, AEM OpenAPI per la distribuzione dei frammenti di contenuto:

* è un’API OpenAPI ottimizzata per la distribuzione live di frammenti di contenuto AEM in formato JSON
* offre una moderna integrazione CDN che consente l’annullamento della validità del contenuto attivo
* si concentra sulla distribuzione dei contenuti (prestazioni, scalabilità, integrazione CDN, controllo e output JSON ottimizzati)
* include la possibilità di idratare JSON per i frammenti e le risorse di riferimento

Questa API:

* è il successore di [Supporto per frammenti di contenuto nell&#39;API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)

* integra le [API OpenAPIs](/help/headless/content-fragment-openapis.md) per frammenti di contenuto e modelli per frammenti di contenuto, che consentono di gestire i frammenti di contenuto e i modelli per frammenti di contenuto (CRUD)

* è un&#39;alternativa HTTP REST all&#39;API GraphQL di [AEM da utilizzare con i frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)

Per la documentazione completa consulta [Distribuzione di frammenti di contenuto di AEM con OpenAPI](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/contentfragments/delivery/).

>[!NOTE]
>
>Consulta [API di AEM per la distribuzione e la gestione strutturata dei contenuti](/help/headless/apis-headless-and-content-fragments.md) per una panoramica delle varie API disponibili e un confronto di alcuni dei concetti coinvolti.

>[!IMPORTANT]
>
>Per abilitare Content Fragment Delivery con OpenAPI su AEM as a Cloud Service, accertati che non sia già abilitato, quindi invia un ticket di supporto Adobe con il titolo **Enable Content Fragment Delivery with OpenAPI** e specifica:
>
>* ID del programma Cloud Service e dell&#39;ambiente
>* dettagli del caso d’uso che desideri risolvere con Content Fragment Delivery OpenAPI
>* i dettagli di tutti i contatti a cui Adobe deve rispondere e rimanere informato sulla richiesta e sul progetto (se necessario)

## Memorizzazione in cache {#caching}

AEM si integra con AEM CDN Fastly. Ciò significa che le risposte JSON distribuite sul livello di pubblicazione sono memorizzate nella cache al livello Fastly.

Le risposte vengono quindi memorizzate nella cache, in base alle intestazioni di memorizzazione in cache predefinite (non può essere configurato):

* Le risposte vengono memorizzate nella cache del browser/client per 5 minuti
   * `max-age`=`300`
* Le risposte vengono memorizzate nella cache della rete CDN per 1 ora
   * `s-maxage`=`3600`
* È possibile distribuire contenuto non aggiornato durante la riconvalida di nuove richieste per un massimo di 1 ora
   * `stale-while-revalidate`=`3600`
* I contenuti non aggiornati possono essere presentati, per errore, per un massimo di 1 giorno
   * `stale-on-error`=`86400`

La distribuzione dei frammenti di contenuto con OpenAPI supporta l’annullamento della validità della cache CDN attiva. Ciò significa che ogni volta che il contenuto viene aggiornato o pubblicato, le corrispondenti risposte JSON OpenAPI vengono automaticamente invalidate tramite una richiesta di eliminazione temporanea a Fastly. Questo consente di visualizzare le modifiche riportate nell&#39;output JSON prima che venga raggiunta l&#39;età effettiva della cache CDN (`s-maxage`).

## Disponibilità {#availability}

La Distribuzione dei frammenti di contenuto con OpenAPI è disponibile sui livelli di anteprima e pubblicazione. OpenAPI distribuisce frammenti di contenuto in formato JSON, sia per l’anteprima che per la distribuzione live.

Per visualizzare in anteprima la distribuzione dei frammenti di contenuto con OpenAPI puoi:

* pubblica in anteprima
* abilita l’accesso all’anteprima con elenco consentiti IP
* ottenere l’URL di anteprima

## CORS {#cors}

[Origini consentite CORS](/help/headless/deployment/cross-origin-resource-sharing.md) definiscono le origini che possono chiamare l&#39;API.

Questa API non prende in considerazione le origini consentite CORS definite sul lato della configurazione del dispatcher, in particolare per GraphQL.

## API Rate Limits {#api-rate-limits}

L’API consente nuove richieste a una velocità massima di 200 richieste al secondo, per ambiente.

Una volta superato questo limite, l’API inizia a inviare 429 errori. Questi errori devono essere gestiti da qualsiasi applicazione client e le richieste non riuscite vengono ritentate dopo un nuovo tentativo di backoff esponenziale.

<!-- 
## Limitations {#limitations}
-->
