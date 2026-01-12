---
title: Panoramica delle API di comunicazione di AEM Forms
description: Panoramica delle API di comunicazione di AEM Forms, inclusi i metodi di autenticazione e i riferimenti API completi
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
source-git-commit: d9eb9a93aba71a5ef5940c9d1d75cfd4e738c26b
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 4%

---


# Panoramica delle API di comunicazione di AEM Forms

Le API di AEM Forms forniscono una suite completa di API native per il cloud progettate per aiutare le aziende ad automatizzare i flussi di lavoro dei documenti.

Le API di AEM Forms sono strutturate e accessibili tramite due console primarie:

* [Adobe Developer Console (ADC)](https://developer.adobe.com/developer-console/) - Adobe Developer Console è il gateway per API, eventi, runtime e App Builder di Adobe.

* [AEM Developer Console](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console) - AEM Developer Console fornisce accesso a dettagli a livello di ambiente, configurazioni, account tecnici e credenziali di servizio per supportare attività operative e di integrazione.

Diverse API supportano [metodi di autenticazione](#authentication-methods) diversi.

## Metodi di autenticazione

Diverse API di Forms utilizzano metodi di autenticazione diversi in base alla timeline della loro versione:

* [Da server a server OAuth](/help/forms/oauth-api-authetication.md)
* Server-to-Server [JWT (token web JSON)](/help/forms/jwt-api-authentication.md)

Le API precedenti supportano l’autenticazione da server a server basata su JWT, configurata e gestita tramite AEM Developer Console. Le API più recenti utilizzano l’autenticazione server-to-server di OAuth e sono configurate tramite Adobe Developer Console.

<!--
>[!NOTE]
>
> Adobe is standardizing authentication method across all APIs and is gradually onboarding APIs to the Adobe Developer Console, which supports the OAuth Server-to-Server authentication method.-->

## Panoramica sulla classificazione API

Tutte le API di AEM Forms sono suddivise in due parti principali:

* [API di runtime e consegna moduli adattivi](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [API di comunicazione di AEM Forms](#aem-forms-communications-apis)

| Dettagli | Consegna di moduli adattivi e API runtime | API di comunicazione |
|--------------|----------------------------|--------------------------|
| Scopo | Gestire le operazioni di consegna e runtime dei moduli adattivi | Generazione e manipolazione di documenti |
| Casi d’uso | - Rendering modulo<br>- Precompilazione dati<br>- Invii modulo<br>- Gestione bozze | - Generazione PDF<br>- Unione documenti<br>- Elaborazione batch<br>- Operazioni di stampa |
| Metodo di autorizzazione | Supporta i metodi di autenticazione server-to-server/utente di OAuth. | Supporta l’autenticazione da server a server, JWT o OAuth a seconda dell’API. Un’API non può supportare entrambi i metodi di autenticazione. |

### API di comunicazione di AEM Forms

Le API di comunicazione sono l’obiettivo principale per le operazioni incentrate sui documenti.

La tabella seguente elenca tutte le [API di AEM Forms Communications](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/) insieme ai relativi metodi di autenticazione e modelli di esecuzione supportati:

#### API per la generazione di documenti


| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
| ----- | ------ |------- | ------ |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | Crea una nuova configurazione batch per i processi di generazione dei documenti. | Asincrono/Batch | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | Recupera i dettagli di una configurazione batch specifica. | Asincrono/Batch | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/configs](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | Restituisce un elenco di tutte le configurazioni batch disponibili. | Asincrono/Batch | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | Avvia l&#39;esecuzione di una generazione di output batch utilizzando una configurazione. | Asincrono/Batch | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | Recupera lo stato di esecuzione di un processo batch. | Asincrono/Batch | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Elenca tutte le istanze in esecuzione per una configurazione batch specifica. | Asincrono/Batch | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | Genera l’output di PDF in modo sincrono in base a modelli e dati. | Sincrono | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Genera formati di output pronti per la stampa (ad esempio, PCL, PostScript). | Sincrono | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | Genera output AFP per la stampa di volumi elevati. | Sincrono | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/document/generate/pdfform](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | Esegue il rendering di un PDF Form (XFA/XDP) con dati uniti. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/status](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | Recupera lo stato di un processo di generazione di moduli di PDF. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | Recupera l’output/risultato di un processo modulo di PDF completato. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |


#### API per la manipolazione dei documenti

| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
| ------------------ | ---------------- | ----------| ---------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | Esegue le istruzioni DDX per combinare, dividere o manipolare i PDF. | Sincrono | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | Converte un documento PDF in formato PDF/A. | Sincrono | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | Convalida se un PDF è conforme allo standard PDF/A | Sincrono | [JWT](/help/forms/jwt-api-authentication.md) |

#### API di conversione dei documenti

| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
|--------- | -------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | Converte un modulo PDF in formato XDP. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |

#### API di estrazione documenti

| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
|---------| -------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | Estrae proprietà e informazioni strutturali da un PDF. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | Estrae i diritti di utilizzo incorporati in un PDF. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | Estrae metadati come titolo, autore e parole chiave. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/data](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | Estrae dati modulo (XML/JSON) da PDF forms. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | Estrae le impostazioni di protezione, ad esempio autorizzazioni e crittografia. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |

#### API di trasformazione dei documenti


| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
|--------|---------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | Aggiorna o aggiunge metadati in un documento PDF. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | Aggiunge un campo di firma digitale a un PDF. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | Cancella il contenuto di un campo firma. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | Rimuove un campo firma da un PDF. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |

#### Documentare le API di Assurance

| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
|---------|-------|---------|----------------------|
| [/adobe/document/sure/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | Applica i diritti di utilizzo a un PDF (ad esempio, commento, riempimento, segno). | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/sure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | Crittografa un PDF con protezione tramite password o certificato. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/sure/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | Decritta un documento PDF protetto. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/sure/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | Firma digitalmente un documento PDF. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/sure/certify](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | Certifica un PDF con un certificato digitale. | Sincrono | [OAuth](/help/forms/oauth-api-authetication.md) |


## Passaggi correlati

Scopri come impostare l’ambiente per le API di comunicazione Forms sincrone (su richiesta) e asincrone (in batch):

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="API sincrone" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="API sincrone"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="API di comunicazione AEM Forms - Sincrono">API di comunicazione AEM Forms - Sincrono</a>
                    </p>
                    <p class="is-size-6">Scopri come impostare l’ambiente per le API di comunicazione Forms sincrone (on-demand) che generano o elaborano documenti all’istante. </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="API di comunicazione AEM Forms - Asincrono" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="API asincrone"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="API asincrone">API di comunicazione AEM Forms - Asincrono (batch)</a>
                    </p>
                    <p class="is-size-6">Scopri come impostare l’ambiente per le API di comunicazione Forms asincrone (in batch) che generano o elaborano più documenti in modo pianificato.</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


>[!MORELIKETHIS]
>
>* [Introduzione ad AEM Forms as a Cloud Service Communications](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Architettura AEM Forms as a Cloud Service per API Forms adattivi e di comunicazione](/help/forms/aem-forms-cloud-service-architecture.md)
>* [Elaborazione comunicazione - API sincrone](/help/forms/aem-forms-cloud-service-communications.md)
>* [Elaborazione comunicazione - API batch](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Elaborazione comunicazione - API on-demand](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)
