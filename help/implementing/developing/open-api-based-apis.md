---
title: API basate su OpenAPI
description: Scopri il supporto di AEM as a Cloud Service per le API basate su OpenAPI
feature: Developing
role: Admin, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 1%

---

# API basate su OpenAPI {#openapi-based-apis}

Le API di AEM as a Cloud Service più recenti seguono le specifiche OpenAPI e offrono quindi un set di API coerente e ben documentato.

>[!NOTE]
>
> Un [tutorial end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) è una risorsa consigliata per scoprire come configurare e richiamare le API AEM basate su OpenAPI.

Per gli endpoint che richiedono l’autenticazione, l’approccio all’autenticazione varia in base all’endpoint, ma può utilizzare OAuth Server-to-Server, OAuth Web App o OAuth Single Page App (SPA). Le credenziali sono configurate tramite progetti in [Adobe Developer Console](https://developer.adobe.com/developer-console/).

Casi d’uso comuni dell’API includono integrazioni con sistemi come un CRM o un PIM, in cui le API AEM vengono richiamate per recuperare o mantenere i dati. Come parte dell&#39;implementazione dell&#39;integrazione, le applicazioni possono sottoscrivere [eventi emessi da AEM](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-eventing/overview), che possono attivare la logica di business in Adobe App Builder o in altre infrastrutture.

Questo documento funge da panoramica, ma la documentazione più dettagliata è disponibile nelle pagine seguenti:

* I collegamenti dalla sezione API basata su OpenAPI di [documentazione di riferimento](https://developer.adobe.com/experience-cloud/experience-manager-apis/). Ogni documentazione di riferimento dell’API include anche un ambiente playground API, che consente di provare facilmente un endpoint utilizzando un token bearer generato con Adobe Developer Console.

* [Guide](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/) informative, inclusi [concetti e sintassi API](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/).

* Un tutorial di primo livello che descrive [approcci all&#39;autenticazione](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/openapis/overview#authentication-support) e altri concetti.

* Un tutorial con video incentrato su [come configurare le API basate su OpenAPI](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup).

* [Un&#39;esercitazione end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) sulla configurazione e la chiamata di OpenAPI con la strategia di autenticazione server-to-server. Esercitazioni simili sono disponibili anche per gli approcci di autenticazione tramite app web e applicazioni a pagina singola.

## Configurazione dell’accesso API {#configuring-api-access}

Alcune API AEM basate su OpenAPI richiedono l&#39;autenticazione, che richiede la generazione di credenziali tramite [Adobe Developer Console](https://developer.adobe.com/developer-console/). La configurazione prevede i seguenti passaggi:

1. Modernizzazione dell’ambiente AEM as a Cloud Service. Per ulteriori informazioni, consulta il passaggio dell&#39;esercitazione [Modernizzazione dell&#39;ambiente AEM as a Cloud Service](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup?#modernization-of-aem-as-a-cloud-service-environment).
1. Abilita l’accesso alle API di AEM utilizzando i profili di prodotto. I profili di prodotto sono associati ai servizi che rappresentano i gruppi di utenti di AEM con elenchi di controllo di accesso (ACL, Access Control List) predefiniti. Mentre alcuni servizi sono associati a profili di prodotto specifici per impostazione predefinita, altri devono essere associati in modo esplicito; ad esempio, il servizio Utenti API di AEM Assets non è associato ad alcun [profilo di prodotto](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles), pertanto devi abilitarlo per utilizzare l&#39;API di AEM Assets. Per ulteriori informazioni, consulta il passaggio tutorial [Abilita accesso alle API di AEM](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access).
1. Per aggiungere l’autenticazione server-to-server, l’utente che configura l’integrazione deve essere l’amministratore di sistema dell’organizzazione in Adobe Admin Console oppure deve essere aggiunto come sviluppatore al profilo di prodotto a cui è associato il servizio. Per ulteriori informazioni, consulta il passaggio tutorial [Abilita accesso alle API di AEM](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access).
1. Creazione di un progetto Adobe Developer Console (ADC).
1. Configura il progetto ADC. Questo genera credenziali che verranno utilizzate successivamente per scambiarle con un token Bearer quando si richiama l’API.
1. Configura l’istanza di AEM per abilitare la comunicazione al progetto ADC. Ciò comporta la registrazione dell&#39;ID client con l&#39;ambiente configurando e distribuendo un file YAML, come descritto nella sezione [Registrazione di un ID client](#registering-a-client-id) di seguito.

Per istruzioni dettagliate, consulta l&#39;esercitazione [Configurare API basate su OpenAPI](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup).

### Registrazione di un ID client {#registering-a-client-id}

Gli ID client eseguono l’ambito delle API in un progetto Adobe Developer Console in ambienti AEM specifici. Ciò si ottiene come segue:

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
