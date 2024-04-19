---
title: Dynamic Medie con funzionalità OpenAPI
description: Scopri i concetti chiave, ad esempio perché utilizzare Dynamic Medie con funzionalità OpenAPI e come abilitarlo.
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---

# Dynamic Medie con funzionalità OpenAPI {#new-dynaminc-media-apis-overview}

In un mondo digitale in rapida evoluzione, è fondamentale sfruttare appieno il potenziale delle risorse digitali del tuo marchio per battere la concorrenza. Una soluzione DAM (Digital Assets Management) olistica facilita la governance delle risorse, promuove la coerenza del brand e accelera la distribuzione dei contenuti, garantendo al contempo l’integrità del brand e esperienze cliente eccezionali.

Dynamic Medie con funzionalità OpenAPI pone DAM al centro di un ecosistema agile ed efficiente della catena di fornitura dei contenuti per garantire la governance e la distribuzione delle risorse.

## Perché utilizzare Dynamic Medie con funzionalità OpenAPI? {#new-dynamic-media-api-features}

Dynamic Medie con funzionalità OpenAPI offre i seguenti vantaggi chiave:

* **Integrazioni senza soluzione di continuità**: Dynamic Medie con funzionalità OpenAPI offre un set completo di API di ricerca e consegna. Consente agli sviluppatori di [integrare la distribuzione delle risorse con le loro applicazioni](/help/assets/integrate-new-dynamic-media-apis.md). Le applicazioni includono applicazioni Adobe e di terze parti. Inoltre, offre [Interfaccia utente del selettore delle risorse micro-front-end](/help/assets/asset-selector.md) per cercare e selezionare le risorse approvate. Il selettore può essere integrato facilmente con qualsiasi applicazione basata su framework JavaScript come React JS, Angular JS e Vanilla JS.

* **Gestione centralizzata delle risorse digitali**: DAM è l’unica fonte di verità per tutte le risorse digitali. Le risorse digitali vengono gestite centralmente in AEM Assets e distribuite alle applicazioni di consumo mediante riferimento utilizzando gli URL di consegna, senza copiare i file binari delle risorse.

* **Aggiornamenti in tempo reale**: qualsiasi modifica apportata alle risorse approvate in DAM, inclusi gli aggiornamenti della versione e le modifiche ai metadati, viene riflessa automaticamente negli URL di consegna. Con un valore TTL (Time-to-Live) breve di 10 minuti configurato per Dynamic Medie con funzionalità OpenAPI tramite CDN, gli aggiornamenti diventano visibili in meno di 10 minuti su tutte le interfacce di authoring e pubblicazione.

* **Coerenza del brand**: Solo [risorse approvate dal marchio](/help/assets/approved-assets.md) sono esposti ad applicazioni a valle. [I Brand Manager e gli addetti al marketing mantengono uno stretto controllo sulle risorse del brand](/help/assets/restrict-assets-delivery.md). È disponibile per l’uso solo la versione approvata e più recente della risorsa, che garantisce la coerenza del brand su tutti i canali e le applicazioni.

* **Consegna ottimizzata per il web**: le risorse digitali vengono distribuite in formati ottimizzati per il web per migliorare i valori web vitali principali delle esperienze digitali. Ciò include il supporto per le rappresentazioni WebP per le immagini, lo streaming adattivo tramite protocolli HLS o DASH per i video e le rappresentazioni originali per i documenti.

* **Trasformazione dinamica delle risorse**: il nostro sistema consente la trasformazione immediata delle immagini utilizzando parametri URL noti come modificatori di immagini. [Ad esempio, larghezza, altezza, rotazione, capovolgimento, qualità, ritaglio e formato](/help/assets/deliver-assets-apis.md). Dynamic Medie con funzionalità OpenAPI supporta anche le funzionalità di ritaglio avanzato delle immagini. Le rappresentazioni trasformate vengono generate dinamicamente e distribuite senza problemi tramite la rete CDN.

* **Consegna sicura delle risorse**: Dynamic Medie con funzionalità OpenAPI fornisce un meccanismo per controllare l’accesso alle risorse digitali. Puoi specificare ruoli o gruppi di utenti come metadati per le risorse da proteggere e impostare un arco temporale predefinito durante il quale [solo gli utenti autorizzati possono accedere a queste risorse](/help/assets/restrict-assets-delivery.md). Gli URL di consegna per le risorse protette non vengono risolti per gli utenti non autorizzati durante il periodo limitato.

* **Informazioni sui dati per prendere decisioni informate**: oltre alla gestione e alla distribuzione delle risorse, acquisisce informazioni approfondite sulla consegna dei dati in CDN, consentendo ai Brand Manager di tenere traccia delle metriche di consegna tra i canali. Consente loro di prendere decisioni basate sui dati per ottimizzare continuamente la governance delle risorse e le strategie di distribuzione.

![Nuovo diagramma di flusso dei dati di Dynamic Medie](assets/dm-openapi-dfd.png)

## Prerequisiti per accedere a Dynamic Medie con funzionalità OpenAPI {#prerequisites-new-dynaminc-media-apis}

Per accedere a Dynamic Medie con funzionalità OpenAPI, è necessario disporre di licenze per:

* AEM Assets as a Cloud Service

* Dynamic Medie AEM

## Come abilitare Dynamic Medie con le funzionalità OpenAPI? {#enable-new-dynamic-media-apis}

Prima di inviare una richiesta per abilitare Dynamic Medie con funzionalità OpenAPI su AEM as a Cloud Service, accertati che non sia già abilitato.

Per abilitare Dynamic Medie con funzionalità OpenAPI su AEM as a Cloud Service, invia un ticket di supporto per gli Adobi con i seguenti dettagli:

* Programma Cloud Service e ID ambiente

* Dettagli del caso d’uso da risolvere con Dynamic Medie con l’integrazione delle funzionalità OpenAPI.

* Dettagli delle applicazioni a valle da integrare con Dynamic Medie con funzionalità OpenAPI.

  >[!NOTE]
  >
  > Per l’integrazione con un’applicazione non Adobe, fornisci i nomi di dominio per la whitelist in cui è ospitata l’applicazione.

* Dettagli dei contatti chiave dei clienti coinvolti nel progetto di integrazione.

Dopo aver inviato il ticket di supporto, Adobe abilita Dynamic Medie con funzionalità OpenAPI nell’ambiente dei Cloud Service e condiviso i dettagli, come l’ID client IMS, per consentire all’utente di procedere con l’integrazione.

## Approfondisci le funzionalità chiave {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approved-assets.md">
   <img alt="Approvare le risorse in Experience Manager Assets" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approved-assets.md">
      <strong>Approvare le risorse in Experience Manager Assets</strong>
      </a>
   </div>
   <p>
      <em>Approva le risorse in AEM Assets per semplificare la gestione delle risorse, garantendo un processo controllato ed efficiente.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-new-dynamic-media-apis.md">
   <img alt="Integrare AEM Assets con le applicazioni a valle" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-new-dynamic-media-apis.md">
      <strong>Integrare AEM Assets con le applicazioni a valle</strong>
      </a>
   </div>
   <p>
      <em>Integra la tua interfaccia utente personalizzata con l’archivio di Experience Manager Assets utilizzando le API di ricerca e consegna oppure utilizza il selettore delle risorse micro-front-end di Adobe.</em>
   </p>
</td>
<td>
   <a href="/help/assets/asset-selector.md">
   <img alt="Selettore risorse di Adobe" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/asset-selector.md">
      <strong>Selettore risorse micro-front-end di Adobe</strong>
      </a>
   </div>
   <p>
      <em>Interfaccia utente che interagisce con l’archivio di AEM Assets per cercare le risorse e utilizzarle nell’esperienza di authoring dell’applicazione.</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/search-assets-api.md">
   <img alt="Cercare risorse nell’archivio Experience Manager Assets" src="./assets/search-assets-api-overview.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-api.md">
      <strong>Cercare risorse nell’archivio di Experience Manager Assets</strong>
      </a>
   </div>
   <p>
      <em>Cerca le risorse nell’archivio di AEM Assets in modo che possano essere consegnate alle applicazioni a valle.</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="Distribuzione di risorse alle applicazioni a valle" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>Distribuzione di risorse alle applicazioni a valle</strong>
      </a>
   </div>
   <p>
      <em>Distribuisci risorse alle applicazioni a valle integrate utilizzando un URL di consegna.</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Limitare l’accesso alle risorse in Experience Manager" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Limitare l’accesso alle risorse in Experience Manager</strong>
      </a>
   </div>
   <p>
      <em> L’amministratore DAM o i Brand Manager limitano l’accesso configurando i ruoli per le risorse approvate nell’istanza di authoring as a Cloud Service dell’AEM.</em>
   </p>
</td>
</table>

