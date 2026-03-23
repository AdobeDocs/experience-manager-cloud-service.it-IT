---
title: Note sulla versione 2026.3.0 di Cloud Manager
description: Ulteriori informazioni sulla versione 2026.3.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 2556f606db8b74bce25cd504a183abdc43e31227
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 22%

---

# Note sulla versione 2026.3.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Ulteriori informazioni sulla versione 2026.3.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione della versione 2026.3.0 di Cloud Manager in AEM as a Cloud Service è il venerdì 5 marzo 2026.

La prossima pubblicazione è pianificata per il venerdì 2 aprile 2026.


## Novità - Cloud Manager {#cloud-manager-whats-new}

* **Cloud Manager ora supporta l&#39;opzione** Cancella **per** Importazioni copia contenuto ****

  Quando abiliti **Cancella**, Cloud Manager elimina il contenuto esistente nella destinazione prima di avviare l&#39;importazione, in modo da poter iniziare da una nuova lavagna ed evitare conflitti con il contenuto preesistente. Se lasci disabilitato **Cancella**, Cloud Manager importa il nuovo contenuto sopra il contenuto di destinazione esistente. Viene visualizzata una richiesta di conferma prima dell’inizio della cancellazione e Cloud Manager registra l’azione di cancellazione e i dettagli di importazione per la tracciabilità.

  Vedi anche [Copia contenuto](/help/implementing/developing/tools/content-copy.md#copy-content).

* **Supporto per l&#39;estensibilità dell&#39;interfaccia utente in AEM Experience Hub**
Il supporto per le estensioni dell&#39;interfaccia utente in [AEM Experience Hub](https://experience.adobe.com/experiencemanager) è ora abilitato e consente agli sviluppatori di estendere l&#39;interfaccia con funzionalità personalizzate e widget generati con Adobe App Builder.

  Per ulteriori informazioni, consulta [AEM Experience Hub](https://developer.adobe.com/uix/docs/services/aem-experience-hub/).

* **Stabilità, prestazioni e affidabilità migliorate**

  Questa versione include aggiornamenti di ottimizzazione e manutenzione che migliorano la stabilità, le prestazioni e l’affidabilità di Cloud Manager.


## Programmi Beta {#private-beta-program}

Partecipa al programma Beta privato di Cloud Manager per ottenere un accesso esclusivo alle funzioni in arrivo prima del rilascio generale.

>[!IMPORTANT]
>
>I rilasci di Beta possono contenere difetti e vengono forniti &quot;COSÌ COME SONO&quot; senza alcuna garanzia. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare o altrimenti supportare (tramite i servizi di supporto Adobe o in altro modo) le versioni beta. Adobe consiglia ai clienti di prestare attenzione e di non affidarsi al corretto funzionamento o alle prestazioni delle versioni beta o a qualsiasi documentazione o materiale di accompagnamento. Le funzioni e le API in versione beta sono soggette a modifiche senza preavviso. Di conseguenza, qualsiasi utilizzo delle versioni beta è interamente a rischio del cliente.

Vedi anche [Programmi AEM Beta](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

Sono attualmente disponibili le seguenti opportunità:
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### Server MCP Cloud Manager per IDE basati su intelligenza artificiale{#mcp-server-for-cm}

È ora possibile provare un server MCP (Model Context Protocol) che espone le API pubbliche di Cloud Manager come strumenti per IDE abilitati per l’intelligenza artificiale (come Cursore). Dopo averlo connesso, puoi utilizzare le richieste di conversazione per elencare e gestire programmi, pipeline, ambienti e archivi, in modo da velocizzare l’operazione senza uscire dall’editor.

Consulta la documentazione [Utilizzare MCP con AEM as a Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

Vedere l&#39;esercitazione [Cloud Manager MCP Server](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-server/cloud-manager#).

Ti interessa la versione beta? Invia un&#39;e-mail a [GRP-AEM-CM-MCP-FEEDBACK@adobe.com](mailto:GRP-AEM-CM-MCP-FEEDBACK@adobe.com) con il tuo ID organizzazione e l&#39;ID programma di Adobe.


<!--
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

### Build più veloci con il caching dei moduli {#quick-build-cm-pipelines}

Un nuovo modello di build compila solo i moduli modificati (anziché l’intero archivio) utilizzando il caching a livello di modulo per ridurre i tempi della build. Si applica alle pipeline di qualità del codice, full stack e di solo staging.

![Finestra di dialogo Modifica pipeline non di produzione con le due opzioni Strategia di compilazione Full Build e Smart Build](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*Finestra di dialogo Modifica pipeline non di produzione che mostra le due opzioni Strategia di compilazione, Build completa e Build avanzata.*

Nella finestra di dialogo **Aggiungi/Modifica pipeline**, nella scheda **Codice Source**, una nuova sezione **Strategia di compilazione** consente di scegliere una delle seguenti opzioni di compilazione:

* **Build completa**: crea tutti i moduli nell&#39;archivio a ogni esecuzione.
* **Smart Build**: crea solo i moduli che sono cambiati dall&#39;ultimo commit, riducendo così il tempo di compilazione complessivo.

Puoi controllare quali pipeline utilizzano **Smart build**. Durante la versione beta, questa opzione viene visualizzata solo per le pipeline **Qualità codice** e **Distribuzione full stack sviluppo**.

Consulta [Informazioni sull&#39;utilizzo di Smart Build in una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build) e [Aggiungi una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)

Ti interessa? Invia un’e-mail a [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) indicando il tuo OrgID Adobe e l’ID programma.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

## Correzioni di bug {#bug-fixes}

* È stato risolto un problema a causa del quale l’API Restore Points (Punti di ripristino) poteva restituire un errore 500 durante il recupero dei punti di ripristino. L’endpoint ora gestisce correttamente i valori nulli, garantendo risposte coerenti e affidabili. (CMGR-72963)
* Cloud Manager ora accetta gli URL dell’archivio GitHub con o senza il suffisso `.git`, allineando il comportamento API all’interfaccia utente e rendendo più flessibile l’onboarding dell’archivio. (CMGR-73296)
* La convalida del nome del profilo di prodotto ora non distingue tra maiuscole e minuscole, evitando errori durante la creazione di profili con nomi che differiscono solo per l’iniziale maiuscola. (CMGR-74075)
* Ora è possibile eseguire più operazioni di ripristino dalla stessa esecuzione della pipeline, abilitando i ripristini sequenziali per ambienti quali Stage e Produzione senza richiedere una nuova esecuzione della pipeline. (CMGR-73538)


<!-- ## Known issues {#known-issues} -->

