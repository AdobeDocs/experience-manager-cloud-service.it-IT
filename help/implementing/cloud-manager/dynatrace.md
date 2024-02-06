---
title: Dynatrace
description: Scopri come usare Dynatrace con AEM as a Cloud Service
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
source-git-commit: fec3aa6debec49014406ab241c3ce0338ec5a1d2
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

Adobe consente di utilizzare Dynatrace per monitorare l&#39;AEM as a Cloud Service come parte dell&#39;implementazione aziendale, identificare la causa di eventuali problemi e intervenire per risolverli in base alle esigenze.

Con Dynatrace è possibile osservare direttamente tutte le applicazioni AEM. Dynatrace fornisce una visibilità completa sull’esperienza dell’utente finale rilevando automaticamente le applicazioni AEM e visualizzando le loro dipendenze dal sito web al contenitore al servizio cloud. Abbinate a tracce end-to-end su tutti i livelli e al monitoraggio degli utenti reali, migliorate le vostre esperienze AEM basate sui contenuti, senza intervalli o blind spot. Se si verificano anomalie, Dynatrace le diagnostica in tempo reale, con il motore di intelligenza artificiale Davis, e individua la causa principale fino al codice danneggiato prima che i clienti siano colpiti, riducendo in tal modo il tempo medio di riparazione.

Per ulteriori informazioni su Dynatrace, vedere [Integrazione di Adobe AEM Cloud Service](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![Metriche delle prestazioni di authoring e pubblicazione AEM](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Integrazione di Dynatrace con AEM as a Cloud Service {#integrating-dynatrace-with-aem-as-a-cloud-service}

I clienti Dynatrace possono monitorare i propri ambienti AEM richiedendo la connettività tramite un ticket di assistenza clienti.

Di seguito sono descritti i dettagli necessari per le richieste di connettività:

| **Campo** | **Descrizione** |
|---|---|
| [!DNL Dynatrace Environment URL] | URL dell’ambiente Dynatrace.<br><br>Per i clienti Dynatrace SaaS, il formato è `https://<your-environment-id>.live.dynatrace.com`.<br><br>Per i clienti Dynamic Managed, il formato è `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | ID dell&#39;ambiente Dynatrace. Consulta [Ottenere informazioni sull&#39;ambiente Dynatrace](#get-dynatrace-env-info) per come ottenere questo. |
| [!DNL Dynatrace Environment Token] | Token di ambiente Dynatrace. Consulta [Ottenere informazioni sull&#39;ambiente Dynatrace](#get-dynatrace-env-info) per come ottenere questo.<br><br>Questo deve essere considerato un segreto, quindi utilizza le pratiche di sicurezza appropriate. Ad esempio, proteggerlo con password in un sito Web come **zerobin.net**, a cui può fare riferimento il ticket di assistenza clienti, insieme alla password. |
| [!DNL Dynatrace API access token] | Il token di accesso API dell’ambiente Dynatrace.  Consulta [Creare un token di accesso API Dynatrace](#create-dynatrace-access-token) per informazioni su come crearlo.<br><br>Questo deve essere considerato un segreto, quindi utilizza le pratiche di sicurezza appropriate. Ad esempio, proteggerlo con password in un sito Web come **zerobin.net**, a cui può fare riferimento il ticket di assistenza clienti, insieme alla password.<br><br>Nota: questo è richiesto solo per Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Port] | La porta ActiveGate Dynatrace a cui deve connettersi l’integrazione AEM.<br><br>Nota: questo è richiesto solo per Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Network Zone] | Il tuo [Zona di rete ActiveGate Dynatrace](https://docs.dynatrace.com/docs/manage/network-zones) indirizzare i dati di monitoraggio AEM in modo efficiente tra centri dati e regioni di rete.<br><br>Nota: l&#39;area di rete Dynatrace ActiveGate è facoltativa. |
| [!DNL AEM Environment ID(s)] | ID dell’ambiente AEM che Dynatrace deve monitorare. |

>[!NOTE]
>
>Una volta integrato Dynatrace, i dati non passeranno più ad altri strumenti APM come New Relic, se precedentemente abilitati.


## Creare un token di accesso API Dynatrace {#create-dynatrace-access-token}

1. Accedi all’ambiente Dynatrace.
1. In [!DNL Dynatrace] menu, vai a [!DNL Manage] > [!DNL Access tokens].
1. Seleziona [!DNL Generate new token].
1. Definisci un [!DNL token name].

1. Facoltativo: impostare un valore [!DNL expiration date]. Assicurati di generare un nuovo token prima della scadenza.
1. Imposta il [!DNL token scope] a [!DNL PaaS integration - Installer download]
1. Seleziona [!DNL Generate token].
1. Copia il token di accesso generato e archivialo in un luogo sicuro.


## Ottenere informazioni sull&#39;ambiente Dynatrace {#get-dynatrace-env-info}

1. Esegui la seguente richiesta API all’ambiente Dynatrace:

`curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"`

Sostituisci \&lt;environmenturl> con l’URL dell’ambiente Dynatrace e \&lt;accesstoken> con il token di accesso API creato.

1. Copia il \&lt;environmentid> e \&lt;environmenttoken> dal payload di risposta e memorizzale in un luogo sicuro.

```
{
   "tenantUUID": "<environmentId>",
   "tenantToken": "<environmentToken>",
   "communicationEndpoints": [
   ... 
   ],
   "formattedCommunicationEndpoints": "<endpoints>" 
}
```


