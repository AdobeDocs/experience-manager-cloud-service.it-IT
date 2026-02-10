---
title: Panoramica dell’agente di sviluppo
description: Scopri in che modo l’agente di sviluppo di AEM analizza le pipeline in Cloud Manager non riuscite e genera i registri per suggerire correzioni di codice e velocizzare il debug.
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Architect, Developer
exl-id: 2194556f-aac2-4cdd-8f7f-00c92c8c4424
source-git-commit: eeaa119711b480197b5807b85eb9c566a735f270
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# Panoramica dell’agente di sviluppo {#development-agent-overview}

L’agente di sviluppo consente agli sviluppatori e agli amministratori di AEM di creare, eseguire il debug, distribuire e ottimizzare il codice in modo più efficiente.

Al momento, l’agente può recuperare gli stati della pipeline e aiutarti a risolvere i problemi dei passaggi di build non riusciti suggerendo correzioni, risparmiando tempo durante il debug delle distribuzioni AEM as a Cloud Service negli ambienti di sviluppo, staging e produzione. Esamina i registri di build e il codice correlato per consigliare una correzione da applicare manualmente.

>[!VIDEO](https://video.tv.adobe.com/v/3478015?captions=ita&quality=12&learn=on)

>[!IMPORTANT]
>
>Le risposte generate dall’intelligenza artificiale possono essere imprecise o fuorvianti. Controlla nuovamente le correzioni e le risposte suggerite.
>
>Consulta anche [Linee guida per l&#39;utente di Adobe Experience Cloud Generative AI](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

Per accedere a questo agente, fare riferimento alle [note sulla versione](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs) per istruzioni su come iscriversi al programma beta e assicurarsi di indicare il proprio interesse per l&#39;agente di sviluppo. Puoi anche inviare un feedback specifico all&#39;agente di sviluppo all&#39;indirizzo [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com).

[Segui un&#39;esercitazione](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/ai/development-agent-troubleshoot-ci-cd-pipeline) per scoprire come utilizzare l&#39;agente di sviluppo per risolvere gli errori della pipeline.

## Accedere all’agente di sviluppo tramite Cloud Manager {#how-to-access-the-agent}

Puoi accedere all’agente di sviluppo tramite l’Assistente AI presente nelle interfacce utente, inclusi Cloud Manager o Experience Hub.

**Per accedere all&#39;agente di sviluppo tramite Cloud Manager:**

1. Per iniziare, fare clic su [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) per aprire la relativa home page.

   ![Home page di Adobe Experience Cloud](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. Nella barra a sinistra, sotto l&#39;intestazione **Servizi**, fai clic su **Cloud Manager**.

   ![L&#39;elenco a discesa che mostra il predefinito di authoring dei contenuti è selezionato](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >I widget, gli strumenti e gli artefatti visualizzati dipendono dall’utente tipo, dalle adesioni e dal tipo di distribuzione di AEM (AEM as a Cloud Service o Managed Services 6.5/6.5 LTS).

1. Nella barra a sinistra, in **Programma**, fai clic su **![Icona Panoramica](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) Panoramica**.

1. Nella pagina **Panoramica del programma**, nella scheda **Pipeline**, fai clic su una pipeline.

   ![Pipeline selezionata](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-select.png)

1. Nella pagina **Build e analisi del codice**, annota la pipeline non riuscita.

   ![Errore della pipeline rilevato nella pagina Build and Code Scanning](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-failure.png)

1. Fai clic sull&#39;icona **Assistente AI** nell&#39;angolo superiore destro dell&#39;interfaccia utente di AEM (dalle pagine di Cloud Manager o dall&#39;istanza di authoring degli ambienti AEM).

   ![Icona Assistente IA sulla barra degli strumenti](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   Vedi anche [Assistente AI in AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).

1. Nella casella di testo del pannello **Assistente AI**, nella parte inferiore, digitare la domanda o il prompt, quindi premere `Enter` o fare clic sull&#39;icona ![Invia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   Ad esempio:
   *Nel programma &quot;eda-org-01-no-access&quot;, analizzare l&#39;errore della pipeline &quot;no-access&quot; e risolvere i problemi.*

   Il prompt restituisce la seguente risposta.

   ![Richiesta dell&#39;Assistente AI e risposta risultante](/help/ai-in-aem/agents/development/assets/dev-agent-prompt-response.png)


## Autorizzazioni {#permissions}

Il processo di risoluzione dei problemi della pipeline dell’agente di sviluppo richiede il ruolo Cloud Manager - Sviluppatore o il ruolo Cloud Manager - Responsabile del programma.

## Prompt di esempio {#sample-prompts}

| Prompt | Risultato |
| --- | --- |
| *Risoluzione dei problemi relativi alla pipeline non riuscita* | Esegue un’analisi del motivo per cui una pipeline non è riuscita; se non è chiaro a quale pipeline viene fatto riferimento, verranno poste all’utente ulteriori domande. |
| *Elencare le pipeline non riuscite per il programma principale.* | Anche se i risultati possono variare, questo prompt restituisce una tabella di pipeline non riuscite, con un suggerimento di follow-up per fare riferimento a una pipeline specifica da analizzare. |
| *Analizza la pipeline non riuscita denominata &quot;Pipeline di sviluppo&quot;* | Questo prompt determina un’analisi della pipeline non riuscita con suggerimenti da correggere. In caso di più errori, l’utente dovrà porre ulteriori domande. |
| *Risoluzione dei problemi di esecuzione della pipeline 1234567* | Fornendo un ID di esecuzione della pipeline esatto, viene eseguita un’analisi della pipeline. |

## Funzioni fuori ambito {#out-of-scope-features}

La risoluzione dei problemi della pipeline funziona nella fase di build della pipeline full stack. Per altri tipi e passaggi di pipeline, esegui il debug degli errori scaricando ed esaminando i registri.

Consulta [Registri di accesso e download](/help/implementing/cloud-manager/manage-logs.md).
