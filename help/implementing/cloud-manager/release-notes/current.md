---
title: Note sulla versione 2025.5.0 di Cloud Manager
description: Ulteriori informazioni sulla versione 2025.5.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 6b18623cc940856383009cd6b4ba011515c12ab5
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 21%

---

# Note sulla versione 2025.5.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Ulteriori informazioni sulla versione 2025.5.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione della versione 2025.5.0 di Cloud Manager in AEM as a Cloud Service è il venerdì 8 maggio 2025.

La prossima versione è pianificata per l’venerdì 5 giugno 2025.

## Novità {#what-is-new}

### Come modificare l’origine di contenuto con un clic per Edge Delivery Services

Adobe Experience Manager (AEM) Edge Delivery Services consente la distribuzione dei contenuti da più origini, come Google Drive, SharePoint o AEM stesso, utilizzando una rete Edge veloce e distribuita a livello globale.

La configurazione dell&#39;origine di contenuto differisce tra Helix 4 e Helix 5 nel modo seguente:

| Versione | Metodo di configurazione |
| --- | --- |
| Elica 4 | File YAML (`fstab.yaml`) |
| Elica 5 | API del servizio di configurazione (*no`fstab.yaml`*) |

Questo articolo fornisce passaggi di configurazione completi, esempi e istruzioni di convalida per entrambe le versioni.

**Prima di iniziare**

Se in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site) utilizzi [un clic su Edge Delivery, il tuo sito è Helix 5 con un singolo archivio. Seguire le istruzioni Helix 5 e utilizzare la versione Helix 4 YAML fornita come fallback.

**Determinare la versione Helix**

* Helix 4 - Il progetto include un file `fstab.yaml`.
* Helix 5 - Il progetto *non* utilizza `fstab.yaml` ed è stato configurato tramite l&#39;interfaccia utente o l&#39;API di Edge Delivery Services.

Conferma tramite i metadati dell’archivio o consulta l’amministratore se non sei ancora sicuro.

#### Configurare l’origine di contenuto (Helix 4)

In Helix 4, l&#39;origine di contenuto è definita in un file di configurazione YAML denominato `fstab.yaml` che si trova nella radice dell&#39;archivio GitHub.

##### Formato file YAML

Il file `fstab.yaml` definisce punti di montaggio (prefissi di percorso URL mappati su URL di origine contenuto) simili all&#39;esempio seguente (solo a scopo illustrativo):

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

##### Modificare l’origine di contenuto

I passaggi variano a seconda del sistema di origine utilizzato.

* **Unità Google**

   1. Creare una cartella di Google Drive.
   1. Condividi la cartella con `helix@adobe.com`.
   1. Ottieni il collegamento alla cartella condivisibile.
   1. Aggiorna `fstab.yaml` come mostrato di seguito:

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. Apporta le modifiche a GitHub.

* **SharePoint**

   1. Creare una cartella SharePoint o una raccolta documenti.
   1. Condividi l&#39;accesso con `helix@adobe.com`.
   1. Ottieni l’URL della cartella.
   1. Aggiorna `fstab.yaml` come mostrato di seguito:

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. Apporta le modifiche a GitHub.

* **AEM**

   1. Identifica il percorso del contenuto AEM.
   1. Utilizza l’URL di esportazione del contenuto di AEM come mostrato di seguito:

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. Apporta le modifiche a GitHub.

##### Convalida

* Utilizzando l&#39;estensione AEM Sidekick Chrome, fai clic su **Anteprima** > **Pubblica** > **Verifica il sito attivo**.
* Convalida URL: `https://main--<repo>--<org>.hlx.page/`

#### Configurare l’origine di contenuto (Helix 5)

Helix 5 è repoless, non utilizza `fstab.yaml` e supporta più siti che condividono la stessa directory. La configurazione viene gestita tramite l’API del servizio di configurazione o l’interfaccia utente di Edge Delivery Services. La configurazione è a livello di sito (non a livello di archivio).

##### Differenze concettuali

| Formato | Elica 4 | Elica 5 |
| --- | --- | --- |
| File di configurazione | `fstab.yaml` | Configurazione API o interfaccia utente |
| Punti di montaggio | Definito da YAML | Non obbligatorio (radice implicita) |

##### Modificare l’origine di contenuto

Utilizza l’API del servizio di configurazione.

1. Esegui l’autenticazione tramite una chiave API o un token di accesso.
1. Effettua la seguente chiamata API `PUT`:

   ```bash {.line-numbering}
   PUT /api/{program}/{programId}/site/{siteId}
   Content-Type: application/json
   
   {
     "sitename": "my-site",
     "branchName": "main",
     "version": "v5",
     "repo": "my-content-repo-link"
   }
   ```

1. Convalida la risposta (prevista: HTTP 200 OK).

##### Convalida

* Utilizzando l&#39;estensione AEM Sidekick Chrome, fai clic su **Anteprima** > **Pubblica** > **Verifica il sito attivo**.
* Convalida URL: `https://main--<repo>--<org>.aem.page/`
* (Facoltativo) Controllare la configurazione corrente tramite la seguente chiamata API `GET`:

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```

<!--
* **AI-powered build summaries now available for internal use**

    Internal users can now use AI-powered build summaries to simplify build log analysis. The feature provides actionable recommendations and helps identify the root causes of build failures.

    ![Build Summary dialog box](/help/implementing/cloud-manager/release-notes/assets/build-summary.png)
-->


## Programma per i primi utilizzatori {#early-adoption}

Partecipa al programma Early Adopter di Cloud Manager per ottenere accesso esclusivo alle prossime funzionalità prima del rilascio generale.

Sono attualmente disponibili le seguenti opportunità di adozione anticipata:

### Aggiungi pipeline Edge Delivery {#add-eds-pipeline}

**Le pipeline** sono ora supportate per i siti generati con Edge Delivery Services, espandendo questa funzionalità oltre gli ambienti Cloud Service. È possibile utilizzare **Pipeline** per gestire impostazioni quali le regole di filtro del traffico e le configurazioni di Web Application Firewall (WAF), se applicabile. Vedi [Configurazioni supportate](/help/operations/config-pipeline.md#configurations).

<!-- ![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png) -->

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

<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

