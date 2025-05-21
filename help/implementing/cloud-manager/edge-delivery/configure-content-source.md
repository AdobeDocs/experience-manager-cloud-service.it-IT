---
title: Configurare il Source dei contenuti
description: Scopri come configurare l’origine di contenuto per il sito Edge Delivery utilizzando fstab.yaml in Helix 4 o utilizzando la procedura guidata in Cloud Manager (o l’API del servizio di configurazione) in Helix 5.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: f82eafc0-03d0-4c69-9b28-e769a012531b
source-git-commit: 56ab7a402a2fa7bdcf30bd66045b04e9314bed64
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Configurare l’origine di contenuto con un clic per Edge Delivery Services {#config-content-source}

Adobe Experience Manager (AEM) Edge Delivery Services consente la distribuzione dei contenuti da più origini, come Google Drive, SharePoint o AEM stesso, utilizzando una rete Edge veloce e distribuita a livello globale.

La configurazione dell&#39;origine di contenuto differisce tra Helix 4 e Helix 5 nel modo seguente:

| Versione | Metodo di configurazione origine contenuto |
| --- | --- |
| Elica 4 | File YAML (`fstab.yaml`) |
| Elica 5 | API del servizio di configurazione (*no`fstab.yaml`*) |

Questo articolo fornisce passaggi di configurazione completi, esempi e istruzioni di convalida per entrambe le versioni.

**Prima di iniziare**

Se in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site) utilizzi [un clic su Edge Delivery, il tuo sito è Helix 5 con un singolo archivio. [Seguire le istruzioni Helix 5](#config-helix5) e utilizzare la versione Helix 4 YAML delle istruzioni come fallback.

**Determinare la versione Helix**

* Helix 4 - Il progetto include un file `fstab.yaml`.
* Helix 5 - Il progetto *non* utilizza `fstab.yaml` ed è stato configurato tramite [Cloud Manager tramite la procedura guidata](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) o l&#39;API.

Conferma tramite i metadati dell’archivio o consulta l’amministratore se non sei ancora sicuro.

## Configurare l’origine di contenuto per Helix 4

In Helix 4, il file fstab.yaml definisce l&#39;origine di contenuto per il sito. Situato nella directory principale dell’archivio GitHub, questo file mappa i prefissi del percorso URL (denominati punti di montaggio) alle origini di contenuto esterne. Un esempio tipico è simile al seguente:

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

Questo esempio è solo a scopo illustrativo. L’URL effettivo deve puntare all’origine di contenuto, ad esempio una cartella Google Drive, una directory SharePoint o un percorso AEM.

**Per configurare l&#39;origine di contenuto per Helix 4:**

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

### Convalida

* Utilizzando l&#39;estensione AEM Sidekick Chrome, fai clic su **Anteprima** > **Pubblica** > **Verifica il sito attivo**.
* Convalida URL: `https://main--<repo>--<org>.hlx.page/`

## Configurare l’origine di contenuto per Helix 5 {#config-helix5}

Helix 5 è repoless, non utilizza `fstab.yaml` e supporta più siti che condividono la stessa directory. La configurazione viene gestita tramite l’API del servizio di configurazione o l’interfaccia utente di Edge Delivery Services. La configurazione è a livello di sito (non a livello di archivio).

Le differenze concettuali sono le seguenti:

| Formato | Elica 4 | Elica 5 |
| --- | --- | --- |
| Configurazione | Completato tramite `fstab.yaml` | Eseguito tramite l’API o l’interfaccia utente anziché tramite YAML. |
| Punti di montaggio | Definito in `fstab.yaml`. | Non obbligatorio. La radice è implicitamente compresa. |

**Per configurare l&#39;origine di contenuto per Helix 5:**

1. Utilizzando l’API del servizio di configurazione, esegui l’autenticazione tramite una chiave API o un token di accesso.
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

### Convalida

* Utilizzando l&#39;estensione AEM Sidekick Chrome, fai clic su **Anteprima** > **Pubblica** > **Verifica il sito attivo**.
* Convalida URL: `https://main--<repo>--<org>.aem.page/`
* (Facoltativo) Controllare la configurazione corrente tramite la seguente chiamata API `GET`:

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```
