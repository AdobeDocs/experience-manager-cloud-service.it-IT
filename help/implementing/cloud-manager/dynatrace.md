---
title: Dynatrace
description: Scopri come utilizzare Dynatrace con AEM as a Cloud Service
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

Adobe consente di utilizzare Dynatrace per monitorare l’AEM as a Cloud Service come parte dell’implementazione aziendale, identificare la causa di eventuali problemi e intervenire per risolverli in base alle esigenze.

Con Dynatrace, puoi ottenere un&#39;osservabilità perfetta per tutte le applicazioni AEM. Dynatrace fornisce una visibilità completa sull’esperienza dell’utente finale rilevando automaticamente le applicazioni AEM e visualizzandone le dipendenze dal sito web al contenitore al servizio cloud. Abbinate a tracce end-to-end su tutti i livelli e al monitoraggio degli utenti reali, migliorate le vostre esperienze AEM basate sui contenuti, senza intervalli o blind spot. Se si verificano anomalie, Dynatrace le diagnostica in tempo reale con il motore di intelligenza artificiale Davis e individua la causa principale del codice danneggiato prima che i clienti siano interessati, riducendo in tal modo il tempo medio di riparazione.

Per ulteriori informazioni su Dynatrace, consulta [Integrazione di Adobe AEM Cloud Service](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![Metriche delle prestazioni di authoring e pubblicazione AEM](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Integrazione di Dynatrace con AEM as a Cloud Service {#integrating-dynatrace-with-aem-as-a-cloud-service}

I clienti Dynatrace possono monitorare i propri ambienti AEM richiedendo la connettività tramite un ticket di assistenza clienti.

Di seguito sono descritti i dettagli necessari per le richieste di connettività:

| **Campo** | **Descrizione** |
|---|---|
| [!DNL Dynatrace Environment URL] | URL dell&#39;ambiente Dynatrace.<br><br>Per i clienti SaaS di Dynatrace, il formato è `https://<your-environment-id>.live.dynatrace.com`.<br><br>Per i clienti gestiti da Dynatrace, il formato è `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | ID dell&#39;ambiente Dynatrace. Consulta [Come è possibile ottenere i dettagli di connessione a Dynatrace?](#how-do-i-get-my-dynatrace-connection-details) per come ottenere questo. |
| [!DNL Dynatrace Environment Token] | Token di ambiente Dynatrace. Consulta [Come è possibile ottenere i dettagli di connessione a Dynatrace?](#how-do-i-get-my-dynatrace-connection-details) per come ottenere questo.<br><br>Questo deve essere considerato un segreto, quindi utilizza le pratiche di sicurezza appropriate. Ad esempio, proteggerlo con password in un sito Web come **zerobin.net**, a cui può fare riferimento il ticket di assistenza clienti, insieme alla password. |
| [!DNL Dynatrace API access token] | Il token di accesso API dell’ambiente Dynatrace.  Consulta [Creare un token di accesso API Dynatrace](#create-dynatrace-access-token) per informazioni su come crearlo.<br><br>Questo deve essere considerato un segreto, quindi utilizza le pratiche di sicurezza appropriate. Ad esempio, proteggerlo con password in un sito Web come **zerobin.net**, a cui può fare riferimento il ticket di assistenza clienti, insieme alla password.<br><br>Nota: questo è necessario solo per Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Port] | La porta Dynatrace ActiveGate a cui deve connettersi l’integrazione AEM.<br><br>Nota: questo è necessario solo per Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Network Zone] | Il tuo [Area di rete Dynatrace ActiveGate](https://docs.dynatrace.com/docs/manage/network-zones) indirizzare i dati di monitoraggio AEM in modo efficiente tra centri dati e regioni di rete.<br><br>Nota: un&#39;area di rete Dynatrace ActiveGate è facoltativa. |
| [!DNL AEM Environment ID(s)] | ID dell’ambiente AEM da monitorare per Dynatrace. |

>[!NOTE]
>
>Una volta integrato Dynatrace, i dati non passeranno più ad altri strumenti APM come New Relic, se precedentemente abilitato.

## Domande frequenti {#faq}

### Quale licenza è necessaria per il monitoraggio dell&#39;AEM di Dynatrace? {#which-license-do-i-need-for-AEM-monitoring}

Il monitoraggio AEM di Dynatrace richiede una licenza Dynatrace. Le licenze AEM di Dynatrace si basano su [monitoraggio full stack per i contenitori Kubernetes](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring). Le dimensioni della memoria dei contenitori AEM monitorati (servizi di authoring e pubblicazione) vengono rilevate automaticamente.

Adobi di specifiche di implementazione per l’ambiente AEM sono:

* Produzione: in media 4 contenitori, 16 GB di memoria ciascuno
* Non produzione: in media 4 contenitori, 8 GB di memoria ciascuno

Per ulteriori informazioni sulle licenze di Dynatrace, vedere [Iscrizione alla piattaforma Dynatrace](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription).

### Come è possibile ottenere i dettagli di connessione a Dynatrace? {#how-do-i-get-my-dynatrace-connection-details}

1. Esegui la seguente richiesta API all’ambiente Dynatrace:

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   Sostituisci `<environmentUrl>` con l’URL del tuo ambiente Dynatrace e `<accessToken>` con il token di accesso API creato.

1. Copia il `<environmentId>` e `<environmentToken>` dal payload di risposta e memorizzale in un luogo sicuro.

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### Creare un token di accesso API Dynatrace {#create-dynatrace-access-token}

1. Accedi all’ambiente Dynatrace.
1. Vai a **[!DNL Access tokens]** e seleziona **[!DNL Generate new token]**.
1. Definisci un [!DNL token name].
1. Imposta l’ambito del token su **[!DNL PaaS integration - Installer download]**.
1. Seleziona **[!DNL Generate token]**.
1. Copia il token di accesso generato e archivialo in un luogo sicuro.





