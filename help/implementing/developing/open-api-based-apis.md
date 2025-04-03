---
title: API basate su OpenAPI
description: Scopri il supporto di AEM as a Cloud Service per le API basate su OpenAPI
feature: Developing
role: Admin, Architect, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: e735f7d2a39e3165907969d2e27565639499a636
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# API basate su OpenAPI {#openapi-based-apis}

>[!NOTE]
>
>OpenAPI sono disponibili come parte di un programma di accesso anticipato. Se ti interessa accedervi, ti invitiamo a inviare un&#39;e-mail a [aem-apis@adobe.com](mailto:aem-apis@adobe.com) con una descrizione del tuo caso d&#39;uso.

Le API di AEM as a Cloud Service più recenti seguono le specifiche OpenAPI e producono quindi API coerenti, ben documentate e di facile utilizzo. Informazioni approfondite sono disponibili nelle pagine seguenti:

* Un [tutorial end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) su come configurare e richiamare le API AEM basate su OpenAPI utilizzando l&#39;autenticazione server-to-server.
* [Guide](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/) informative, inclusi [concetti e sintassi API](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/).
* Endpoint API [documentazione di riferimento](https://developer.adobe.com/experience-cloud/experience-manager-apis/), in cui alcune API sono basate su OpenAPI, ad esempio [questa API Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/). La documentazione di riferimento include anche un ambiente playground API, che semplifica la prova di un endpoint utilizzando un token bearer generato con Adobe Developer Console.

Un caso d’uso API comune prevede integrazioni con sistemi come un CRM o un PIM, in cui le API AEM vengono richiamate per recuperare o mantenere i dati. Come parte dell&#39;implementazione dell&#39;integrazione, le applicazioni possono sottoscrivere [eventi emessi da AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview), che possono attivare la logica di business in Adobe App Builder o in altre infrastrutture.

I tipi di autenticazione API supportati variano a seconda dell’endpoint, ma possono essere server-to-server OAuth, app Web OAuth e app a pagina singola OAuth (SPA).

>[!NOTE]
>
> Il [tutorial end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) è una risorsa consigliata per scoprire come configurare e richiamare le API AEM basate su OpenAPI.


## Configurazione dell’accesso API {#configuring-api-access}

Molte API AEM basate su OpenAPI richiedono l&#39;autenticazione, che richiede la generazione di credenziali tramite [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/). La configurazione prevede i seguenti passaggi:

1. Assicurati che i profili di prodotto [ del tuo programma AEM siano aggiornati](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles) e che sia abilitato un servizio appropriato per accedere all&#39;API desiderata.
1. Crea un nuovo progetto in Adobe Developer Console e aggiungi le API desiderate al progetto, selezionando anche il tipo di autenticazione appropriato.
1. Genera le credenziali, che verranno successivamente utilizzate per scambiarle con un token Bearer quando si richiama l’API.
1. Registra l’ID client con l’ambiente configurando un file YAML, distribuito utilizzando la pipeline di configurazione (o riga di comando per gli RDE).

Per istruzioni dettagliate, consulta l&#39;esercitazione [Configurare API basate su OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/setup).

## Registrazione di un ID client {#registering-a-client-id}

Gli ID client hanno come ambito le API di un progetto Adobe Developer Console per ambienti AEM specifici. Ciò si ottiene come segue:

1. Creare un file denominato `api.yaml` o simile con una configurazione come lo snippet sottostante, inclusi i livelli desiderati (authoring, pubblicazione, anteprima). I valori `Client_id` devono provenire dai progetti API di Adobe Developer Console.

   Le proprietà `kind`, `version` e `metadata` sono descritte nell&#39;articolo [Pipeline di configurazione](/help/operations/config-pipeline.md#common-syntax). Il valore della proprietà `kind` deve essere impostato su *API* e la proprietà `version` su *1*.

   ```
   kind: "API"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     allowedClientIDs:
       author:
         - "<client_id>"
       publish:
         - "<client_id>"
       preview:
         - "<client_id>"
   ```

1. Posizionare il file in una cartella di primo livello denominata `config` o simile, come descritto in [Pipeline di configurazione](/help/operations/config-pipeline.md#folder-structure).
1. Per tipi di ambiente diversi da RDE (che utilizza strumenti della riga di comando), crea una pipeline di configurazione della distribuzione di destinazione in Cloud Manager, come indicato da [questa sezione](/help/operations/config-pipeline.md#creating-and-managing) nell&#39;articolo Pipeline di configurazione. Tieni presente che le pipeline full stack e le pipeline a livello web non distribuiscono il file di configurazione.
1. Distribuisci la configurazione.
