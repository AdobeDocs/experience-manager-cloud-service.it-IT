---
title: Dynatrace OneAgent
description: Scopri come utilizzare OneAgent di Dynatrace con AEM as a Cloud Service
source-git-commit: 2e70c8be73915bea860b98e02c08772bb4f5dcd2
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Dynatrace OneAgent {#dynatrace-oneagent}

Adobe offre la possibilità di utilizzare l&#39;agente OneAgent di Dynatrace per monitorare l&#39;AEM as a Cloud Service come parte di un&#39;implementazione aziendale, identificare la causa di eventuali problemi e intervenire per risolverli in base alle esigenze. <!-- When GA, add: Read this [Dynatrace article](https://www.dynatrace.com/hub/detail/adobe-experience-manager/) about AEM monitoring to learn more. -->

## Integrazione di OneAgent con AEM as a Cloud Service {#integrating-oneagent-with-aem-as-a-cloud-service}

I clienti Dynatrace OneAgent possono monitorare il proprio utilizzo di AEM richiedendo la connettività tramite un ticket di assistenza clienti.

Di seguito sono descritti i dettagli necessari per le richieste di connettività:

| **Campo** | **Descrizione** |
|---|---|
| URL ambiente Dynatrace | URL dell’ambiente Dynatrace.<br><br>Per i clienti Dynatrace SaaS, il formato è `https://<environment>.live.dynatrace.com`.<br><br>Per i clienti Dynamic Managed, il formato è `https://<your-managed-url>/e/<environmentId>` |
| ID ambiente Dynatrace | L’ID dell’ambiente Dynatrace, disponibile nell’URL dell’ambiente |
| Token ambiente Dynatrace | Token di ambiente OneAgent. Consulta la documentazione di Dynatrace per informazioni su come creare questo elemento.<br><br>Questo deve essere considerato un segreto, quindi utilizza le pratiche di sicurezza appropriate. Ad esempio, proteggerlo con password in un sito Web come **zerobin.net**, a cui può fare riferimento il ticket di assistenza clienti, insieme alla password. |
| Token di accesso all’API Dynatrace | Il token di accesso API dell’ambiente Dynatrace. Consulta la documentazione di Dynatrace per informazioni su come creare questo elemento.<br><br>Questo deve essere considerato un segreto, quindi utilizza le pratiche di sicurezza appropriate. Ad esempio, proteggerlo con password in un sito Web come **zerobin.net**, a cui può fare riferimento il ticket di assistenza clienti, insieme alla password.<br><br>Nota: questo è richiesto solo per Dynatrace Managed. |
| Porta di destinazione Dynatrace | Il porto di destinazione di Dynatrace.<br><br>Nota: questo è richiesto solo per Dynatrace Managed. |
| ID ambiente AEM | ID dell’ambiente AEM che Dynatrace deve monitorare. |


