---
title: Note sulla versione 2026.1.0 di Cloud Manager
description: Scopri la versione 2026.1.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 54566e3ea99c4ac03e266eab52163a516701b611
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 66%

---

# Note sulla versione 2026.1.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Scopri la versione 2026.1.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La versione 2026.1.0 di Cloud Manager in AEM as a Cloud Service è stata rilasciata venerdì 22 gennaio 2026.

La prossima pubblicazione è pianificata per il venerdì 5 febbraio 2026.

## Novità - Cloud Manager {#cloud-manager-whats-new}

* **Le pipeline di configurazione ora supportano i segreti gestiti**

  Ora gli utenti possono aggiungere e gestire i segreti direttamente nelle pipeline di configurazione di Cloud Manager. Questi segreti sostituiscono in modo sicuro i valori nelle specifiche di configurazione della pipeline e supportano distribuzioni flessibili e specifiche per l’ambiente.

  ![Opzione Visualizza/Modifica variabili nel menu a discesa per una pipeline selezionata](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-option.png)
  *Opzione Visualizza/Modifica variabili nel menu a discesa per una pipeline selezionata.*

  ![Finestra di dialogo Configurazione variabili &#x200B;](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-variablesconfig-dialogbox.png)*Finestra di dialogo Configurazione variabili.*

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

### Estensibilità e personalizzazione di Experience Hub {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) funge da punto di accesso ad AEM, personalizzato in base alle esigenze della tua organizzazione. Comunica ad Adobe le tue estensioni dell’interfaccia utente di AEM esistenti, in modo che possano aiutarti ad abilitarle in Experience Hub con il minimo sforzo.

![Diagramma del workflow di estensibilità e personalizzazione di Experience Hub](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Incorpora esperienze personalizzate in Experience Hub per estendere e personalizzare il dashboard della tua organizzazione. Oltre ai widget incorporati di Adobe, aggiungi quelli personalizzati utilizzando il framework [Estensibilità dell’interfaccia utente](https://developer.adobe.com/uix/docs/). Crea app dell’interfaccia utente basate su JavaScript e mostrale agli utenti per soddisfare requisiti e flussi di lavoro specifici per l’azienda.

Ti interessa la versione beta? Invia un’e-mail a [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) con il tuo OrgID Adobe e una breve descrizione della personalizzazione che intendi creare.

### Build più veloci con il caching dei moduli {#quick-build-cm-pipelines}

Un nuovo modello di build compila solo i moduli modificati (anziché l’intero archivio) utilizzando il caching a livello di modulo per ridurre i tempi della build. Si applica alle pipeline di qualità del codice, full stack e di solo staging.

![Finestra di dialogo Modifica pipeline non di produzione con le due opzioni Strategia di compilazione Full Build e Smart Build](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*Finestra di dialogo Modifica pipeline non di produzione che mostra le due opzioni Strategia di compilazione, Build completa e Build avanzata.*

Nella finestra di dialogo **Aggiungi/Modifica pipeline**, nella scheda **Codice Source**, una nuova sezione **Strategia di compilazione** consente di scegliere una delle seguenti opzioni di compilazione:

* **Build completa**: crea tutti i moduli nell&#39;archivio a ogni esecuzione.
* **Smart Build**: crea solo i moduli che sono cambiati dall&#39;ultimo commit, riducendo così il tempo di compilazione complessivo.

Puoi controllare quali pipeline utilizzano **Smart build**. Durante la versione beta, questa opzione viene visualizzata solo per le pipeline **Qualità codice** e **Distribuzione sviluppatore**.

Ti interessa? Invia un’e-mail a [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) indicando il tuo OrgID Adobe e l’ID programma.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

### Integra il tuo Git personale (BYOG) {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Ora è possibile portare in Cloud Manager i propri archivi Git Azure DevOps, con supporto per i nuovi archivi Azure DevOps e gli archivi legacy VSTS (Visual Studio Team Services).

* Per chi usa Edge Delivery Services, l’archivio di cui è stato eseguito l’onboarding può essere utilizzato per sincronizzare e distribuire il codice del sito.
* Per chi usa AEM as a Cloud Service e Adobe Managed Services (AMS), l’archivio può essere collegato sia a pipeline full stack che front-end.

Verranno presto introdotti anche il supporto di ulteriori tipi di pipeline e la convalida di richieste pull tramite pipeline per la qualità del codice.

Consulta [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->

**Domande frequenti su BYOG**

| Domanda | Risposta |
|---|---|
| *Come può un progetto tornare all’archivio Git gestito da Adobe, se necessario?* | Tornare indietro è semplice. [Aggiorna le pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) in modo che puntino all’archivio Adobe e rimuovi l’archivio esterno se non è più necessario. |
| *È possibile configurare archivi diversi per ambienti diversi (ad esempio, non di produzione o di produzione) per consentire prima il test in ambienti non di produzione?* | Sì, è possibile configurare archivi diversi per ambienti separati. Ad esempio, la pipeline di sviluppo o di qualità del codice può puntare a un archivio esterno mentre la pipeline di produzione rimane connessa all’archivio Adobe. Assicurati che il processo di sincronizzazione tra i due archivi rimanga attivo durante questa configurazione. |
| *Le impostazioni esistenti come gli elenchi `IP Allow` continuano a funzionare?* | Sì, gli elenchi `IP Allow` esistenti continuano a funzionare come di consueto. Tuttavia, se l’archivio Git esterno è protetto da un firewall, gli [Indirizzi IP Adobe necessari devono essere aggiunti all’elenco consentiti](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Funzionano tutti gli URL dell’archivio GitLab? L’URL dell’archivio in uso segue il formato `https://gitlab_dedicated_url.com/path/repo-name.git`, che differisce dall’esempio riportato nella documentazione.* | Sì, è supportato qualsiasi archivio GitLab che supporta API V3 o V4, inclusi gli URL GitLab con hosting autonomo come quelli descritto in [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Gestisci token di accesso{#manage-access-tokens}

Utilizza **Gestisci token di accesso** in Cloud Manager per visualizzare, rinominare ed eliminare i token di accesso associati agli archivi BYOG esterni, ad esempio GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Consulta [Gestisci token di accesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


## Correzioni di bug {#bug-fixes}

Non vi sono correzioni di bug significativi nella versione di dicembre 2025 di Cloud Manager.


<!-- ## Known issues {#known-issues} -->

