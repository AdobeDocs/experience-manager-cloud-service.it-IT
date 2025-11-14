---
title: Panoramica delle API di comunicazione di AEM Forms
description: Panoramica delle API di comunicazione di AEM Forms, inclusi i metodi di autenticazione e i riferimenti API completi
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: cba0a8a0a0b346fc89cca146519cc5843f244d23
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 7%

---


# Panoramica delle API di comunicazione di AEM Forms

Le API di comunicazione di AEM Forms forniscono una suite completa di API native per il cloud progettate per aiutare le aziende ad automatizzare i flussi di lavoro dei documenti.

Le API di AEM Forms sono strutturate e accessibili tramite due console primarie:

* [Adobe Developer Console (ADC)](https://developer.adobe.com/developer-console/) - Adobe Developer Console è il gateway per API, eventi, runtime e App Builder di Adobe.

* [AEM Developer Console](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console) - AEM Developer Console fornisce gli strumenti per il debug e l&#39;analisi degli ambienti AEM as a Cloud Service.

Ogni console consente di accedere a API e servizi diversi per l&#39;elaborazione, la generazione, la conversione, la crittografia e le attività di comunicazione dei documenti. Le API supportano [metodi di autenticazione](#authentication-methods) diversi.

## Metodi di autenticazione

Le API supportano più metodi di autenticazione per un’integrazione sicura tra le applicazioni e i servizi Adobe:

| Aspetto | OAuth Server-to-Server (consigliato) | JWT (token web JSON) |
|-------------|------------------------------------------|---------------------------|
| Descrizione | Metodo moderno e sicuro per l’accesso API senza interazione dell’utente. | Metodo precedente che utilizza token firmati per l’accesso. |
| Percorso di configurazione | ADOBE DEVELOPER CONSOLE e AEM DEVELOPER CONSOLE | Solo AEM Developer Console |
| Protezione | Alta: usa le credenziali e gli ambiti client | Moderato: dipende dalla gestione delle chiavi |
| Scalabilità | Estremamente scalabile per le integrazioni back-end | Limitato, adatto per l&#39;utilizzo legacy |
| Gestione token | Generazione e rinnovo automatici | Firma e rotazione manuale dei token |
| Stato | Consigliato | Non approvato |


>[!NOTE]
>
> Fai clic sui collegamenti seguenti per ulteriori informazioni su:-
> 
> * [Server-to-Server OAuth (consigliato)](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)
> * [JWT (token Web JSON)](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/)

<!--### Execution Models

The following table highlights the key differences between Synchronous (On-Demand) and Asynchronous (Batch) execution models supported in AEM Forms Communications APIs:

| Feature | Synchronous (On-Demand) | Batch (Asynchronous) |
|---------|-------------------------|----------------------|
| **Execution Model** | Real-time, immediate | Queued, scheduled |
| **Response Time** | Seconds | Minutes to hours |
| **Volume** | Single or few documents | Hundreds to thousands |
| **Testing Environment** | Author & Publish | Author Only |
| **Use Case** | User-triggered actions | Scheduled bulk operations |
| **Console Access** | ADC & AEM Developer Console | AEM Developer Console Only |-->

## Panoramica sulla classificazione API

Tutte le API di AEM Forms sono suddivise in due parti principali:

* [API di runtime e consegna moduli adattivi](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [API di comunicazione di AEM Forms](#aem-forms-communications-apis)

| Dettagli | Consegna di moduli adattivi e API runtime | API di comunicazione |
|--------------|----------------------------|--------------------------|
| Scopo | Gestire le operazioni di consegna e runtime dei moduli adattivi | Generazione e manipolazione di documenti |
| Casi d’uso | - Rendering modulo<br>- Precompilazione dati<br>- Invii modulo<br>- Gestione bozze | - Generazione PDF<br>- Unione documenti<br>- Elaborazione batch<br>- Operazioni di stampa |
| Metodo di autorizzazione | Supporta i metodi di autenticazione server-to-server/utente di OAuth. | Supporta solo l&#39;autenticazione server-to-server OAuth. |

### API di comunicazione di AEM Forms

Le API di comunicazione sono l’obiettivo principale per le operazioni incentrate sui documenti.

La tabella seguente elenca tutte le [API di AEM Forms Communications](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/) insieme ai relativi metodi di autenticazione e modelli di esecuzione supportati:

#### API per la generazione di documenti


| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
| ----- | ------ |------- | ------ |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | Crea una nuova configurazione batch per i processi di generazione dei documenti. | Asincrono/Batch | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | Recupera i dettagli di una configurazione batch specifica. | Asincrono/Batch | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/configs](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | Restituisce un elenco di tutte le configurazioni batch disponibili. | Asincrono/Batch | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | Avvia l&#39;esecuzione di una generazione di output batch utilizzando una configurazione. | Asincrono/Batch | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | Recupera lo stato di esecuzione di un processo batch. | Asincrono/Batch | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Elenca tutte le istanze in esecuzione per una configurazione batch specifica. | Asincrono/Batch | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | Genera l’output di PDF in modo sincrono in base a modelli e dati. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Genera formati di output pronti per la stampa (ad esempio, PCL, PostScript). | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | Genera output AFP per la stampa di volumi elevati. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/document/generate/pdfform](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | Esegue il rendering di un PDF Form (XFA/XDP) con dati uniti. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/generate/pdfform/jobs/{id}/status](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | Recupera lo stato di un processo di generazione di moduli di PDF. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/generate/pdfform/jobs/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | Recupera l’output/risultato di un processo modulo di PDF completato. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |


#### API per la manipolazione dei documenti

| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
| ------------------ | ---------------- | ----------| ---------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | Esegue le istruzioni DDX per combinare, dividere o manipolare i PDF. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | Converte un documento PDF in formato PDF/A. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | Convalida se un PDF è conforme allo standard PDF/A | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |

#### API di conversione dei documenti

| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
|--------- | -------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | Converte un modulo PDF in formato XDP. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### API di estrazione documenti

| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
|---------| -------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | Estrae proprietà e informazioni strutturali da un PDF. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | Estrae i diritti di utilizzo incorporati in un PDF. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | Estrae metadati come titolo, autore e parole chiave. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/data](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | Estrae dati modulo (XML/JSON) da PDF forms. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | Estrae le impostazioni di protezione, ad esempio autorizzazioni e crittografia. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### API di trasformazione dei documenti


| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
|--------|---------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | Aggiorna o aggiunge metadati in un documento PDF. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | Aggiunge un campo di firma digitale a un PDF. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | Cancella il contenuto di un campo firma. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | Rimuove un campo firma da un PDF. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### Documentare le API di Assurance

| Endpoint API | Descrizione | Modello di esecuzione | Metodo di autenticazione |
|---------|-------|---------|----------------------|
| [/adobe/document/sure/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | Applica i diritti di utilizzo a un PDF (ad esempio, commento, riempimento, segno). | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/sure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | Crittografa un PDF con protezione tramite password o certificato. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/sure/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | Decritta un documento PDF protetto. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/sure/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | Firma digitalmente un documento PDF. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/sure/certify](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | Certifica un PDF con un certificato digitale. | Sincrono | [Server OAuth al server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |


## Passaggi successivi

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