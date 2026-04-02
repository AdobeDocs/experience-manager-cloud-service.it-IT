---
title: Note sulla versione 2026.4.0 di Cloud Manager
description: Ulteriori informazioni sulla versione 2026.4.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 6c98a27889257a6d8befa04a2b2c4e5a7e6e49f2
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 23%

---

# Note sulla versione 2026.4.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Ulteriori informazioni sulla versione 2026.4.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione della versione 2026.4.0 di Cloud Manager in AEM as a Cloud Service è il venerdì 2 aprile 2026.

La prossima versione è pianificata per l’venerdì 7 maggio 2026.


## Novità - Cloud Manager {#cloud-manager-whats-new}

* **Server MCP Cloud Manager per IDE basati su IA**

  È ora possibile utilizzare un server MCP (Model Context Protocol) che espone le API pubbliche di Cloud Manager come strumenti per IDE abilitati per l’intelligenza artificiale (come Cursore). Dopo averlo connesso, puoi utilizzare le richieste di conversazione per elencare e gestire programmi, pipeline, ambienti e archivi, in modo da velocizzare l’operazione senza uscire dall’editor.

  Consulta la documentazione [Utilizzare MCP con AEM as a Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

  Vedere l&#39;esercitazione [Cloud Manager MCP Server](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-servers/cloud-manager#).

* **Build più veloci con memorizzazione nella cache dei moduli**

  Un nuovo modello di build compila solo i moduli modificati (anziché l’intero archivio) utilizzando il caching a livello di modulo per ridurre i tempi della build. Si applica alle pipeline non di produzione di qualità del codice e alle pipeline non di produzione di sviluppo full stack.

  Consulta [Informazioni sull&#39;utilizzo di Smart Build in una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build) e [Aggiungi una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

* **Verifica connettività host self-service**

  Cloud Manager ora consente di eseguire controlli self-service dall’ambiente. Questi controlli verificano la raggiungibilità dell’host e della porta e confermano la risoluzione DNS utilizzando il percorso di rete configurato del programma, inclusa l’uscita. Questa funzionalità consente di convalidare la rete avanzata e risolvere più rapidamente i problemi di integrazione senza aprire casi di supporto o accedere ai pod. <!-- SKYOPS-23640 -->

  Vedere [Test connettività di rete](/help/security/network-connectivity-test.md)

* **Stabilità, prestazioni e affidabilità migliorate**

  Questa versione include aggiornamenti di ottimizzazione e manutenzione che migliorano la stabilità, le prestazioni e l’affidabilità di Cloud Manager.


## Programmi Beta {#private-beta-program}

Partecipa al programma Beta privato di Cloud Manager per ottenere un accesso esclusivo alle funzioni in arrivo prima del rilascio generale.

>[!IMPORTANT]
>
>I rilasci di Beta possono contenere difetti e vengono forniti &quot;COSÌ COME SONO&quot; senza alcuna garanzia. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare o altrimenti supportare (tramite i servizi di supporto Adobe o in altro modo) le versioni beta. Adobe consiglia ai clienti di prestare attenzione e di non affidarsi al corretto funzionamento o alle prestazioni delle versioni beta o a qualsiasi documentazione o materiale di accompagnamento. Le funzioni e le API in versione beta sono soggette a modifiche senza preavviso. Di conseguenza, qualsiasi utilizzo delle versioni beta è interamente a rischio del cliente.

Vedi anche [Programmi AEM Beta](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

Sono attualmente disponibili le seguenti opportunità:

### Edge Delivery Services con AEM Authoring e configurazione flessibile del livello di pubblicazione {#eds-with-aem-authoring}

Cloud Manager introduce due funzionalità progettate per supportare architetture di consegna moderne.

* **Edge Delivery Services con AEM Authoring**
Ora puoi distribuire siti utilizzando Edge Delivery Services mentre continui a creare contenuti in modalità Autore AEM. A seconda delle preferenze del flusso di lavoro, puoi scegliere tra i seguenti approcci di authoring:

   * Authoring basato su documenti
   * Authoring basato su AEM Author

Per ulteriori informazioni, vedere [Creare un sito Edge Delivery in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site).

* **Configurazione flessibile livello di pubblicazione**
Cloud Manager ora consente di configurare se è necessario un livello di pubblicazione per il programma. Questa flessibilità consente di configurare ambienti che si adattano meglio all’architettura di consegna scelta.

Per ulteriori informazioni, vedere [Livello di pubblicazione flessibile (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).

Per partecipare a Beta, invia un&#39;e-mail a [grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com) con il tuo ID organizzazione Adobe e l&#39;ID programma.

### Build più veloci con il caching dei moduli {#quick-build-cm-pipelines}

Un nuovo modello di build compila solo i moduli modificati (anziché l’intero archivio) utilizzando la memorizzazione nella cache a livello di modulo per ridurre i tempi di build. Si applica alle pipeline di produzione. Puoi controllare quali pipeline di produzione utilizzano **Smart Build**.

Per ulteriori informazioni, consulta:

* [Utilizzo di Smart Build in una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build).
* [Aggiungi una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

Per partecipare a Beta, invia un&#39;e-mail a [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) con il tuo OrgID Adobe e il tuo ID programma.

<!-- OLD
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

<!-- OLD
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.
-->



## Correzioni di bug {#bug-fixes}

Non vi sono correzioni di bug significativi nella versione di Cloud Manager di aprile 2026.

<!-- ## Known issues {#known-issues} -->

