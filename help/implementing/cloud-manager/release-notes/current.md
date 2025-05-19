---
title: Note sulla versione 2025.5.0 di Cloud Manager
description: Ulteriori informazioni sulla versione 2025.5.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 8696cf8a7e7cfc439450b34fa6fda10b38cd415e
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 24%

---

# Note sulla versione 2025.5.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Ulteriori informazioni sulla versione 2025.5.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione della versione 2025.5.0 di Cloud Manager in AEM as a Cloud Service è il venerdì 8 maggio 2025.

La prossima versione è pianificata per l’venerdì 5 giugno 2025.

## Novità {#what-is-new}

### Configurare l’origine di contenuto con un clic per Edge Delivery Services

Adobe Experience Manager (AEM) Edge Delivery Services consente la distribuzione dei contenuti da più origini, come Google Drive, SharePoint o AEM stesso, utilizzando una rete Edge veloce e distribuita a livello globale.

La configurazione dell&#39;origine di contenuto è diversa tra Helix 4 e Helix 5. Scopri la differenza e segui i passaggi di configurazione completi, gli esempi e le istruzioni di convalida per entrambe le versioni.

Consulta [Configurare l&#39;origine di contenuto](/help/implementing/cloud-manager/edge-delivery/configure-content-source.md).


## Programma per i primi utilizzatori {#early-adoption}

Partecipa al programma Early Adopter di Cloud Manager per ottenere accesso esclusivo alle prossime funzionalità prima del rilascio generale.

Sono attualmente disponibili le seguenti opportunità di adozione anticipata:

### Aggiungi pipeline di configurazione Edge Delivery {#add-eds-pipeline}

Le pipeline di configurazione sono ora supportate per i siti creati con Edge Delivery Services, espandendo questa funzionalità oltre gli ambienti Cloud Service. È possibile utilizzare **Pipeline di configurazione** per gestire impostazioni quali le regole di filtro del traffico e le configurazioni del Firewall applicazione Web (WAF), se applicabile. Vedi [Configurazioni supportate](/help/operations/config-pipeline.md#configurations).

![Aggiungi pipeline Edge Delivery nell&#39;elenco a discesa Aggiungi pipeline](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png)

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un&#39;e-mail a [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) dal tuo indirizzo e-mail associato al tuo Adobe ID.

### Git personalizzato con supporto per Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

È ora possibile integrare gli archivi Git di Azure DevOps in Cloud Manager, con il supporto per gli archivi moderni di Azure DevOps e gli archivi VSTS (Visual Studio Team Services) legacy.

* Per gli utenti di Edge Delivery Services, l’archivio integrato può essere utilizzato per sincronizzare e distribuire il codice del sito.
* Per gli utenti di AEM as a Cloud Service e Adobe Managed Services (AMS), l’archivio può essere collegato sia a pipeline full stack che front-end.

Il supporto per ulteriori tipi di pipeline e la convalida delle richieste di pull tramite pipeline di qualità del codice sarà presto disponibile.

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


<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

