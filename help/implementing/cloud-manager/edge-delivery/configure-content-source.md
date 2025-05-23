---
title: Configurare il Source dei contenuti
description: Scopri come configurare l’origine di contenuto per il sito Edge Delivery. Utilizza "fstab.yaml" con l’architettura Helix 4, oppure utilizza la procedura guidata in Cloud Manager (o l’API del servizio di configurazione) con l’architettura Helix 5.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: f82eafc0-03d0-4c69-9b28-e769a012531b
source-git-commit: 71618a5603328990603db2ee7554048c9020a883
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 59%

---

# Configurare l’origine di contenuto con un clic per Edge Delivery Services {#config-content-source}

>[!IMPORTANT]
>
>*Helix* è il nome interno dell&#39;architettura sottostante che alimenta AEM Sites con l&#39;authoring basato su documenti. Non è una funzione o un nome di prodotto. In questo articolo, *Helix* fa riferimento alla versione dell&#39;architettura utilizzata dai siti Edge Delivery. Helix 5 è la versione corrente dell&#39;architettura sottostante; Helix 4 è la versione precedente.

Edge Delivery Services di Adobe Experience Manager (AEM) consente la distribuzione dei contenuti da più origini, come Google Drive, SharePoint o AEM stesso, utilizzando una rete Edge veloce e distribuita a livello globale.

La configurazione dell’origine di contenuto differisce tra le due versioni dell’architettura nel modo seguente:

| Versione | Metodo di configurazione dell’origine contenuto |
| --- | --- |
| Helix 4 | File YAML (`fstab.yaml`) |
| Helix 5 | API del servizio di configurazione (*no`fstab.yaml`*) |

Questo articolo fornisce passaggi di configurazione completi, esempi e istruzioni di convalida per entrambe le versioni.

**Prima di iniziare**

Se in Cloud Manager[&#128279;](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site) utilizzi un clic su Edge Delivery, il tuo sito utilizza Helix 5 con un singolo archivio. [Seguire le istruzioni Helix 5](#config-helix5) e utilizzare la versione Helix 4 YAML delle istruzioni come fallback.

**Determinare la versione Helix**

* Helix 4: il progetto include un file `fstab.yaml`.
* Helix 5 - Il progetto *non* utilizza `fstab.yaml` ed è stato configurato tramite [Cloud Manager tramite la procedura guidata](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) o l&#39;API.

Se non hai la certezza, conferma tramite i metadati dell’archivio o consulta l’amministratore.

## Configurare l’origine di contenuto per Helix 4

In Helix 4, il file `fstab.yaml` definisce l&#39;origine di contenuto per il sito. Situato nella directory principale dell’archivio GitHub, questo file mappa i prefissi del percorso URL (denominati punti di montaggio) alle origini di contenuto esterne. Un esempio tipico è simile al seguente:

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

L’esempio precedente è solo a scopo illustrativo. L’URL effettivo deve puntare all’origine di contenuto, ad esempio una cartella Google Drive, una directory SharePoint o un percorso AEM.

**Per configurare l’origine di contenuto per Helix 4:**

I passaggi variano a seconda del sistema di origine utilizzato.

* **Google Drive**

   1. Crea una cartella di Google Drive.
   1. Condividi la cartella con `helix@adobe.com`.
   1. Ottieni il collegamento alla cartella condivisibile.
   1. Aggiorna `fstab.yaml` come mostrato di seguito:

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. Conferma e invia le modifiche su GitHub.

* **SharePoint**

   1. Crea una cartella SharePoint o una libreria documenti.
   1. Condividi l’accesso con `helix@adobe.com`.
   1. Ottieni l’URL della cartella.
   1. Aggiorna `fstab.yaml` come mostrato di seguito:

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. Conferma e invia le modifiche su GitHub.

* **AEM**

   1. Identifica il percorso del contenuto AEM.
   1. Utilizza l’URL di esportazione del contenuto di AEM come mostrato di seguito:

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. Conferma e invia le modifiche su GitHub.

### Convalida

* Utilizzando l’estensione AEM Sidekick per Chrome, fai clic su **Anteprima** > **Pubblica** > **Verifica il sito live**.
* Convalida URL: `https://main--<repo>--<org>.hlx.page/`

## Configurare l’origine dei contenuti per Helix 5 {#config-helix5}

Helix 5 è privo di archivio, non utilizza `fstab.yaml` e supporta più siti che condividono la stessa directory. La configurazione viene gestita tramite l’API del servizio di configurazione o l’interfaccia utente di Edge Delivery Sites. La configurazione è a livello di sito (non a livello di archivio).

Le differenze concettuali sono le seguenti:

| Aspetto | Helix 4 | Helix 5 |
| --- | --- | --- |
| Configurazione | Eseguita tramite `fstab.yaml` | Eseguita tramite l’API o l’interfaccia utente anziché tramite YAML. |
| Punti di montaggio | Definiti in `fstab.yaml`. | Non obbligatori. La directory principale è implicita. |

**Per configurare l’origine dei contenuti per Helix 5:**

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

* Utilizzando l’estensione AEM Sidekick per Chrome, fai clic su **Anteprima** > **Pubblica** > **Verifica il sito live**.
* Convalida URL: `https://main--<repo>--<org>.aem.page/`
* (Facoltativo) Ispeziona la configurazione corrente tramite la seguente chiamata API `GET`:

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```
