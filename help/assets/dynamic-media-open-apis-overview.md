---
title: Dynamic Media con funzionalità OpenAPI
description: Scopri i concetti chiave, ad esempio perché utilizzare Dynamic Media con funzionalità OpenAPI e come abilitarlo.
role: User
exl-id: 658b6eff-9f5a-4166-9ff6-5dc8eb92ada3
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 2%

---

# Dynamic Media con funzionalità OpenAPI {#new-dynaminc-media-apis-overview}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|-----|

>[!AVAILABILITY]
>
>La guida alle funzionalità di Dynamic Media con OpenAPI è ora disponibile in formato PDF. Scarica l’intera guida e utilizza Adobe Acrobat AI Assistant per rispondere alle tue domande.
>
>[!BADGE Guida di Dynamic Media con funzionalità OpenAPI PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

In un mondo digitale in rapida evoluzione, è fondamentale sfruttare appieno il potenziale delle risorse digitali del tuo marchio per battere la concorrenza. Una soluzione DAM (Digital Assets Management) olistica facilita la governance delle risorse, promuove la coerenza del brand e accelera la distribuzione dei contenuti, garantendo al contempo l’integrità del brand e esperienze cliente eccezionali.

Dynamic Media con funzionalità OpenAPI pone DAM al centro di un ecosistema agile ed efficiente della catena di fornitura dei contenuti per garantire la governance e la distribuzione delle risorse.

## Perché utilizzare Dynamic Media con funzionalità OpenAPI? {#dynamic-media-open-api-features}

Dynamic Media con funzionalità OpenAPI offre i seguenti vantaggi chiave:

* **Integrazioni senza soluzione di continuità**: Dynamic Media con funzionalità OpenAPI offre un set completo di API di ricerca e consegna. Consente agli sviluppatori di [integrare facilmente la distribuzione delle risorse con le applicazioni](/help/assets/integrate-dynamic-media-open-apis.md). Le applicazioni includono applicazioni di Adobe e di terze parti. Fornisce un [interfaccia utente del selettore delle risorse di Microsoft Frontend](/help/assets/overview-asset-selector.md) per cercare e selezionare le risorse approvate. Il selettore può essere integrato facilmente con qualsiasi applicazione basata su framework JavaScript come React JS, Angular JS e Vanilla JS.

* **Gestione centralizzata delle risorse digitali**: DAM è l&#39;unica fonte di verità per tutte le risorse digitali. Le risorse digitali vengono gestite centralmente in AEM Assets e distribuite alle applicazioni di consumo mediante riferimento utilizzando gli URL di consegna, senza copiare i file binari delle risorse.

* **Aggiornamenti in tempo reale**: qualsiasi modifica apportata alle risorse approvate in DAM, inclusi gli aggiornamenti della versione e le modifiche ai metadati, viene automaticamente riportata negli URL di consegna. Con un valore TTL (Time-to-Live) breve di 10 minuti configurato per Dynamic Media con funzionalità OpenAPI tramite CDN, gli aggiornamenti diventano visibili in meno di 10 minuti su tutte le interfacce di authoring e pubblicazione.

* **Coerenza marchio**: solo [risorse approvate dal marchio](/help/assets/approve-assets.md) sono esposte alle applicazioni a valle. [I Brand Manager e gli addetti al marketing mantengono uno stretto controllo sulle risorse del brand](/help/assets/restrict-assets-delivery.md). È disponibile per l’uso solo la versione approvata e più recente della risorsa, che garantisce la coerenza del brand su tutti i canali e le applicazioni.

* **Consegna ottimizzata per il web**: le risorse digitali vengono distribuite in formati ottimizzati per il web in modo da migliorare i valori web fondamentali delle esperienze digitali. Ciò include il supporto per le rappresentazioni WebP per le immagini, lo streaming adattivo tramite protocolli HLS o DASH per i video e le rappresentazioni originali per i documenti.

* **Trasformazione dinamica delle risorse**: il nostro sistema consente la trasformazione immediata delle immagini utilizzando i parametri URL noti come modificatori di immagini. [Ad esempio, larghezza, altezza, rotazione, capovolgimento, qualità, ritaglio, formato e ritaglio avanzato](/help/assets/deliver-assets-apis.md). Le rappresentazioni trasformate vengono generate dinamicamente e distribuite senza problemi tramite la rete CDN.

* **Consegna sicura delle risorse**: Dynamic Media con funzionalità OpenAPI offre un meccanismo per controllare l&#39;accesso alle risorse digitali. È possibile specificare ruoli o gruppi di utenti come metadati per le risorse da proteggere e impostare un intervallo di tempo predefinito durante il quale [solo gli utenti autorizzati possono accedere a queste risorse](/help/assets/restrict-assets-delivery.md). Gli URL di consegna per le risorse protette non vengono risolti per gli utenti non autorizzati durante il periodo limitato.

* **Informazioni sui dati per prendere decisioni informate (in arrivo)**: oltre alla gestione e alla consegna delle risorse, acquisisce informazioni sulla consegna dei dati nelle consegne di risorse in CDN, consentendo ai Brand Manager di tenere traccia delle metriche di consegna tra i canali. Consente loro di prendere decisioni basate sui dati per ottimizzare continuamente la governance delle risorse e le strategie di distribuzione.

![Diagramma del flusso di dati API aperto di Dynamic Media](assets/dm-openapi-dfd.png)

## Prerequisiti per accedere a Dynamic Media con funzionalità OpenAPI {#prerequisites-dynaminc-media-open-apis}

Per accedere a Dynamic Media con funzionalità OpenAPI, è necessario disporre di licenze per:

* AEM Assets as a Cloud Service

* Dynamic Media AEM

## Come abilitare Dynamic Media con le funzionalità OpenAPI? {#enable-dynamic-media-open-apis}

Prima di inviare una richiesta per abilitare Dynamic Media con funzionalità OpenAPI su AEM as a Cloud Service, accertati che non sia già abilitato.

Una volta soddisfatti i [prerequisiti](#prerequisites-dynaminc-media-open-apis) e se Dynamic Media con funzionalità OpenAPI è abilitato nell&#39;istanza AEM as a Cloud Service, è disponibile un URL di consegna per ogni risorsa approvata nell&#39;archivio. Per informazioni su come copiare l&#39;URL di consegna, consulta [Copiare l&#39;URL di consegna per le risorse approvate](approve-assets.md#copy-delivery-url-approved-assets) . Adobe consiglia di utilizzare questo metodo per verificare che Dynamic Media con funzionalità OpenAPI sia abilitato su AEM as a Cloud Service prima di inviare un ticket di supporto per abilitarlo.

Per abilitare Dynamic Media con funzionalità OpenAPI su AEM as a Cloud Service, invia un ticket di supporto Adobe con i seguenti dettagli:

* Programma Cloud Service e ID ambiente

* Dettagli del caso d’uso da risolvere con Dynamic Media con l’integrazione delle funzionalità OpenAPI.

* Dettagli delle applicazioni a valle da integrare con Dynamic Media con funzionalità OpenAPI.

  >[!NOTE]
  >
  Per l’integrazione con un’applicazione non Adobe, fornisci i nomi di dominio per indicare l’elenco consentiti in cui è ospitata l’applicazione.

* Dettagli dei contatti chiave dei clienti coinvolti nel progetto di integrazione.

* Elenco dei membri chiave del team dell’account di Adobe (e-mail).

Dopo aver inviato il ticket di supporto, Adobe abilita Dynamic Media con funzionalità OpenAPI nell’ambiente dei Cloud Service e condiviso i dettagli, come l’ID client IMS, per consentire all’utente di procedere con l’integrazione.

>[!NOTE]
>
Escludi `/conf/global/settings/dam/assets-configurations/assetdelivery` da qualsiasi pacchetto di contenuti, per evitare la disattivazione di Dynamic Media con funzionalità OpenAPI.

## Approfondisci le funzionalità chiave {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approve-assets.md">
   <img alt="Approvare le risorse in Experience Manager Assets" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approve-assets.md">
      <strong>Approva risorse in Experience Manager Assets</strong>
      </a>
   </div>
   <p>
      <em>Approva le risorse in AEM Assets per semplificare la gestione delle risorse, garantendo un processo controllato ed efficiente per la gestione delle risorse.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-dynamic-media-open-apis.md">
   <img alt="Integrare AEM Assets con le applicazioni a valle" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-dynamic-media-open-apis.md">
      <strong>Integrare AEM Assets con le applicazioni downstream</strong>
      </a>
   </div>
   <p>
      <em>Integra la tua interfaccia utente personalizzata con l'archivio di Experience Manager Assets utilizzando le API di ricerca e consegna oppure utilizza il selettore delle risorse micro-front-end di Adobe.</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="Selettore risorse di Adobe" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>Selettore risorse micro-front-end di Adobe</strong>
      </a>
   </div>
   <p>
      <em>Interfaccia utente che interagisce con l'archivio di AEM Assets per cercare le risorse e utilizzarle nell'esperienza di creazione dell'applicazione.</em>
   </p>
</td>
</table>
<table>



<table>
<td>
   <a href="/help/assets/search-assets-api.md">
   <img alt="Cercare risorse nell’archivio Experience Manager Assets" src="./assets/search-assets-api-overview.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-api.md">
      <strong>Cercare risorse nell'archivio di Experience Manager Assets</strong>
      </a>
   </div>
   <p>
      <em>Cerca le risorse nell'archivio di AEM Assets in modo che possano essere distribuite alle applicazioni a valle.</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="Distribuzione di risorse alle applicazioni a valle" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>Distribuisci risorse alle applicazioni a valle</strong>
      </a>
   </div>
   <p>
      <em>Distribuisci risorse alle applicazioni downstream integrate utilizzando un URL di consegna.</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Limitare l’accesso alle risorse in Experience Manager" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Limita l'accesso alle risorse in Experience Manager</strong>
      </a>
   </div>
   <p>
      L'amministratore DAM <em> o i Brand Manager limitano l'accesso configurando i ruoli per le risorse approvate nell'istanza di authoring di AEM as a Cloud Service.</em>
   </p>
</td>

</table>
<table>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="Integrare AEM Assets remoto con AEM Sites" src="./assets/connected-assets-rdam.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong>Integrare AEM Assets remoto con AEM Sites</strong>
      </a>
   </div>
   <p>
      <em>Scopri come integrare AEM Assets remoto con l’ambiente AEM Sites. </em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media-open-apis-faqs.md">
   <img alt="Domande frequenti su Dynamic Media con funzionalità OpenAPI" src="./assets/dynamic-media-faqs.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-faqs.md">
      <strong>Domande frequenti su Dynamic Media con funzionalità OpenAPI</strong>
      </a>
   </div>
   <p>
      <em>Ottieni una risposta alle domande più frequenti su Dynamic Media con funzionalità OpenAPI.</em>
   </p>
</td>
<td>
   <a href="/help/assets/configure-custom-domain.md">
   <img alt="Configurare domini personalizzati" src="./assets/configure-custom-domain.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-custom-domain.md">
      <strong>Configura dominio personalizzato</strong>
      </a>
   </div>
   <p>
      <em>Se AEM as a Cloud Service viene fornito con un dominio predefinito, puoi personalizzarlo in base alle tue esigenze.</em>
   </p>
</td>

</table>
