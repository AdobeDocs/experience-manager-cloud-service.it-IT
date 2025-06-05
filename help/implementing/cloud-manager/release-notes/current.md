---
title: Note sulla versione 2025.6.0 di Cloud Manager
description: Ulteriori informazioni sulla versione 2025.6.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 6365b1c4109c2f2a77fbc332d11e1a8906d2cc6d
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 33%

---

# Note sulla versione 2025.6.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Ulteriori informazioni sulla versione 2025.6.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione della versione 2025.6.0 di Cloud Manager in AEM as a Cloud Service è l’venerdì 5 giugno 2025.

La prossima versione è pianificata per il venerdì 10 luglio 2025.

## Novità {#what-is-new}

* **La dashboard delle licenze ora include la licenza Edge Delivery Services**

  L’utilizzo delle licenze Edge Delivery Services viene ora visualizzato nella dashboard Licenze, fornendo una visibilità più chiara delle adesioni e dello stato. <!-- CMGR-67686 -->

  ![Dashboard delle licenze](/help/implementing/cloud-manager/assets/license-dashboard.png)

  Vedi [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

* **Configurazione del sito Edge Delivery aggiornata**

  Il flusso per l&#39;aggiunta di un sito Edge Delivery è stato semplificato richiedendo l&#39;**origine Edge Delivery** invece dell&#39;**URL archivio**, rendendo l&#39;onboarding e la configurazione più veloci e intuitivi <!-- CMGR-67686 -->

  ![Finestra di dialogo Aggiungi sito Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-site.png)

  Consulta [Aggiungere un sito Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md).

* **Preferiti pipeline**

  In questa versione, Cloud Manager introduce la possibilità di fissare le pipeline preferite, consentendoti di contrassegnare specifiche pipeline come preferite in modo che vengano visualizzate nella parte superiore dell&#39;elenco nella pagina **Pipeline**. Questo miglioramento semplifica la ricerca e l’esecuzione delle pipeline a cui si accede di frequente. <!-- CMGR-68293 -->

  ![Pipeline contrassegnate come preferite](/help/implementing/cloud-manager/release-notes/assets/pipeline-favorites.png) *Due pipeline contrassegnate come preferite.*

  Consulta [Contrassegnare i preferiti della pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipeline-favorites).


## Programma per i primi utilizzatori {#early-adoption}

Partecipa al programma per i primi utilizzatori di Cloud Manager per ottenere l’accesso esclusivo alle prossime funzioni prima che vengano rilasciate al pubblico.

Le seguenti opportunità sono attualmente disponibili per i primi utilizzatori:


### Gestisci token di accesso{#manage-access-tokens}

Utilizza **Gestisci token di accesso** in Cloud Manager per visualizzare, rinominare ed eliminare i token di accesso associati agli archivi Git esterni, quali GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Vedi [Gestione token di accesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)

Se ti interessa testare questa nuova funzione e condividere i tuoi commenti e suggerimenti, invia un’e-mail a dal tuo indirizzo e-mail associato al tuo Adobe ID.


### Ambiente di test specializzato {#specialized-test-environment}

Cloud Manager ora supporta l&#39;aggiunta di un nuovo tipo di ambiente denominato **Ambiente di test specializzato**. L’ambiente è progettato per aiutare i team a convalidare le funzioni in condizioni prossime alla produzione prima della pubblicazione. Questo tipo di ambiente è diverso dagli ambienti *Produzione + Stage*, *Sviluppo* o *Sviluppo rapido* e offre uno spazio mirato per l&#39;esecuzione di scenari di convalida avanzati.

Consulta [Aggiunta di un ambiente di test specializzato](/help/implementing/cloud-manager/specialized-test-environment.md).

![Finestra di dialogo Aggiungi ambiente con il pulsante di opzione Ambiente di test specializzato selezionato](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un&#39;e-mail a [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) dal tuo indirizzo e-mail associato al tuo Adobe ID.


### Bring Your Own Git: ora con supporto per Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Ora è possibile portare in Cloud Manager i propri archivi Git Azure DevOps, con supporto per i nuovi archivi Azure DevOps e gli archivi legacy VSTS (Visual Studio Team Services).

* Per chi usa Edge Delivery Services, l’archivio di cui è stato eseguito l’onboarding può essere utilizzato per sincronizzare e distribuire il codice del sito.
* Per chi usa AEM as a Cloud Service e Adobe Managed Services (AMS), l’archivio può essere collegato sia a pipeline full stack che front-end.

Verranno presto introdotti anche il supporto di ulteriori tipi di pipeline e la convalida di richieste pull tramite pipeline per la qualità del codice.

Consulta [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID. Se ti trovi in una struttura di archivio privata/pubblica o aziendale, assicurati di specificare la piattaforma Git che desideri utilizzare.


#### Domande frequenti su Porta il tuo Git

| Domanda | Risposta |
|---|---|
| *Come può un progetto tornare all&#39;archivio Git gestito da Adobe, se necessario?* | Il passaggio all’indietro è semplice. [Aggiorna le pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) in modo che puntino all&#39;archivio Adobe e rimuovi l&#39;archivio esterno se non è più necessario. |
| *È possibile configurare archivi diversi per ambienti diversi (ad esempio, non di produzione rispetto alla produzione) per consentire prima il test in ambienti non di produzione?* | Sì, è possibile configurare archivi diversi per ambienti separati. Ad esempio, la pipeline di sviluppo o di qualità del codice può puntare a un archivio esterno mentre la pipeline di produzione rimane connessa all’archivio Adobe. Assicurati che il processo di sincronizzazione tra i due archivi rimanga attivo durante questa configurazione. |
| *Le impostazioni esistenti come gli elenchi consentiti IP continuano a funzionare?* | Sì, gli elenchi consentiti IP esistenti continuano a funzionare come al solito. Tuttavia, se l&#39;archivio Git esterno è protetto da un firewall, è necessario aggiungere all&#39;elenco consentiti [&#128279;](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) i indirizzi IP Adobe necessari. |
| *Tutti gli URL dell&#39;archivio GitLab funzionano? L&#39;URL del repository in uso segue il formato `https://gitlab_dedicated_url.com/path/repo-name.git`, che differisce dall&#39;esempio riportato nella documentazione.* | Sì, è supportato qualsiasi archivio GitLab che supporta API V3 o V4, inclusi gli URL GitLab con hosting autonomo come quello descritto in [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


### Aggiungi pipeline di configurazione Edge Delivery {#add-eds-pipeline}

Le pipeline di configurazione sono ora supportate per i siti creati con Edge Delivery Services, espandendo questa funzionalità oltre gli ambienti Cloud Service. È possibile utilizzare **Pipeline di configurazione** per gestire impostazioni quali le regole di filtro del traffico e le configurazioni del Firewall applicazione Web (WAF), se applicabile. Consulta le [configurazioni supportate](/help/operations/config-pipeline.md#configurations).

![Aggiungi pipeline Edge Delivery nell&#39;elenco a discesa Aggiungi pipeline](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Aggiunta di una pipeline Edge Delivery dalla pagina **Panoramica del programma**, scheda **Pipeline**.*

![Finestra di dialogo Aggiungi pipeline di Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Finestra di dialogo Aggiungi pipeline di Edge Delivery.*

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID.


## Correzioni di bug

* Gli ambienti sandbox precedentemente contrassegnati come `HIBERNATED` non rimangono più bloccati in quello stato, consentendo all&#39;esecuzione o alla distribuzione della pipeline di procedere come previsto. <!-- CMGR-67705 -->
* AEM Cloud Manager ora mappa correttamente gli errori di build Maven causati da errori 409 (conflitti) durante il recupero degli artefatti del cliente su un errore causato dal cliente. Questa modifica migliora la messaggistica di errore distinguendo tra errori interni e problemi relativi alla configurazione dell’ambiente del cliente. <!-- CMGR-66673 -->


<!-- ## Known issues {#known-issues} -->

