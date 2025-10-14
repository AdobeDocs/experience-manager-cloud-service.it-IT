---
title: Dynatrace
description: Scopri come utilizzare Dynatrace con AEM as a Cloud Service
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: 498a58c89910f41e6b86c5429629ec9282028987
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

Adobe consente di utilizzare Dynatrace per monitorare AEM as a Cloud Service come parte dell’implementazione aziendale, identificare la causa di eventuali problemi e intervenire per risolverli in base alle esigenze.

Con Dynatrace, puoi ottenere un&#39;osservabilità perfetta per tutte le applicazioni AEM. Dynatrace rileva le app AEM e ne mostra i percorsi, da sito Web a contenitore fino al servizio cloud, per mostrare l’esperienza utente. In combinazione con le analisi end-to-end su ogni livello e con il monitoraggio Real Use, puoi portare le esperienze basate sui contenuti AEM a un livello successivo senza spazi vuoti o punti ciechi. Se sorgono anomalie, Dynatrace le diagnostica in tempo reale, con il motore di intelligenza artificiale Davis. Individua la causa principale nel codice danneggiato prima che i clienti ne siano colpiti, riducendo al minimo il tempo medio di riparazione.

Per ulteriori informazioni su Dynatrace, consulta l&#39;[Integrazione di Adobe AEM Cloud Service](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![Metriche delle prestazioni per l&#39;autore e l&#39;editore di AEM](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Integrazione di Dynatrace con AEM as a Cloud Service {#integrating-dynatrace-with-aem-as-a-cloud-service}

I clienti Dynatrace possono monitorare i propri ambienti AEM richiedendo la connettività tramite un ticket di assistenza clienti.

Di seguito sono descritti i dettagli necessari per le richieste di connettività:

| **Campo** | **Descrizione** |
|---|---|
| [!DNL Dynatrace Environment URL] | URL dell&#39;ambiente Dynatrace.<br><br>Per i clienti SaaS di Dynatrace, il formato è `https://<your-environment-id>.live.dynatrace.com`.<br><br>Per i clienti gestiti da Dynatrace, il formato è `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | ID dell&#39;ambiente Dynatrace. Vedi [Come ottengo i miei dettagli di connessione Dynatrace?](#how-do-i-get-my-dynatrace-connection-details) su come ottenerlo. |
| [!DNL Dynatrace Environment Token] | Token di ambiente Dynatrace. Vedi [Come ottengo i miei dettagli di connessione Dynatrace?](#how-do-i-get-my-dynatrace-connection-details) su come ottenerlo.<br><br>Questo token deve essere considerato un segreto, quindi utilizza le procedure di sicurezza appropriate. Ad esempio, proteggerlo tramite password in un sito Web come **zerobin.net**, a cui il ticket di assistenza clienti può fare riferimento, insieme alla password. |
| [!DNL Dynatrace API access token] | Il token di accesso API dell’ambiente Dynatrace. Consulta [Creare un token di accesso API Dynatrace](#create-dynatrace-access-token) per informazioni su come crearlo.<br><br>Questo token deve essere considerato un segreto, quindi utilizza le procedure di sicurezza appropriate. Ad esempio, proteggerlo tramite password in un sito Web come **zerobin.net**, a cui il ticket di assistenza clienti può fare riferimento, insieme alla password.<br> |
| [!DNL Dynatrace ActiveGate Port] | La porta Dynatrace ActiveGate a cui deve connettersi l’integrazione AEM.<br><br>Questa porta è necessaria solo per Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Network Zone] | L&#39;[area di rete Dynatrace ActiveGate](https://docs.dynatrace.com/docs/manage/network-zones) consente di instradare i dati di monitoraggio di AEM in modo efficiente tra centri dati e aree di rete.<br><br>Nota: un&#39;area di rete Dynatrace ActiveGate è facoltativa. |
| [!DNL AEM Environment IDs] | L’ID o gli ID dell’ambiente AEM che Dynatrace deve monitorare. |

>[!NOTE]
>
>Una volta integrato Dynatrace, i dati non passano più ad altri strumenti APM come New Relic, se precedentemente abilitati.

## Domande frequenti {#faq}

### Quale licenza è necessaria per il monitoraggio di Dynatrace AEM? {#which-license-do-i-need-for-AEM-monitoring}

Il monitoraggio di Dynatrace AEM richiede una licenza Dynatrace. Le licenze di Dynatrace AEM si basano su [monitoraggio full stack per i contenitori Kubernetes](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring). Vengono rilevate automaticamente le dimensioni della memoria dei contenitori AEM monitorati (servizi di authoring e pubblicazione).

Le specifiche di implementazione di Adobe per l’ambiente AEM sono:

* Produzione: in media 4 contenitori, 16 GB di memoria ciascuno
* Non produzione: in media 4 contenitori, 8 GB di memoria ciascuno

Per ulteriori informazioni sulle licenze di Dynatrace, vedere [abbonamento alla piattaforma Dynatrace](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription).

### Come è possibile ottenere i dettagli di connessione a Dynatrace? {#how-do-i-get-my-dynatrace-connection-details}

1. Esegui la seguente richiesta API all’ambiente Dynatrace:

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   Sostituisci `<environmentUrl>` con l&#39;URL dell&#39;ambiente Dynatrace e `<accessToken>` con il token di accesso API creato.

1. Copia `<environmentId>` e `<environmentToken>` dal payload di risposta e archiviali in un luogo protetto.

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### Creare un token di accesso API Dynatrace {#create-dynatrace-access-token}

1. Accedi all’ambiente Dynatrace.
1. Passare a **[!DNL Access tokens]**, quindi fare clic sull&#39;opzione **[!DNL Generate new token]**.
1. Definisci [!DNL token name].
1. Imposta l&#39;ambito del token su **[!DNL PaaS integration - Installer download]**.
1. Selezionare **[!DNL Generate token]**.
1. Copia il token di accesso generato e archivialo in un luogo sicuro.





