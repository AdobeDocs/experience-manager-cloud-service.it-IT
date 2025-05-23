---
title: Note sulla versione 2024.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2024.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 4033abf4-7094-4ce4-ba93-c936062667e3
source-git-commit: 0f5fc5469034139a45ec0fe7e30319012af97301
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 97%

---

# Note sulla versione 2024.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2024.6.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2022 o 2023.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.6.0) è il 27 giugno 2024. La prossima versione funzionale (2024.7.0) è pianificata per il 25 luglio 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di giugno 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/3430779?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuova funzione in Experience Manager Sites {#new-feature-sites}

**Servizio dati di telemetria operativa** {#real-use-monitoring}

Il [servizio di telemetria operativa](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) è ora generalmente disponibile e consente la raccolta dati lato client per AEM as a Cloud Service. Il servizio offre una panoramica più precisa delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web. Offre ai clienti informazioni avanzate sul traffico e sulle prestazioni della pagina, presentando un’opportunità preziosa per comprenderne e migliorarne le prestazioni.

### Programma per i primi utilizzatori {#sites-early-adopter}

**Generare varianti**

Sfruttare l’intelligenza artificiale generativa tramite la nuova funzione di AEM, [genera varianti](/help/generative-ai/generate-variations.md), ora accessibile in Cloud Service. Genera varianti consente di generare e ridimensionare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al tuo team Adobe Account per prendere in considerazione il programma.

**Esplorazione delle risorse nella console Frammenti di contenuto**

Gli autori dei contenuti ora possono esplorare, visualizzare e intervenire sulle immagini e su altre risorse senza dover uscire dalla console Frammenti di contenuto.

![Esplorazione delle risorse](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Per ulteriori informazioni sul programma per i primi utilizzatori, invia un’e-mail all’indirizzo aemcs-headless-adopter@adobe.com dal tuo ID e-mail ufficiale.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni di Experience Manager Assets {#new-features-assets}



**Hub di contenuti**

L’hub di contenuti è disponibile come parte di Experience Manager Assets as a Cloud Service per rendere accessibili i contenuti in linea con il marchio alle organizzazioni e ai loro partner commerciali. Con Content Hub, puoi trovare e distribuire facilmente le risorse, riutilizzare e creare nuove varianti in linea con il marchio e accelerare l’attivazione su larga scala.

![Configurare l’interfaccia utente dell’hub di contenuti](/help/release-notes/assets/content-hub-ui.png)

**Dynamic Media con funzionalità OpenAPI**

Dynamic Media con funzionalità OpenAPI estende il DAM a tutte le applicazioni Adobe e di terze parti, consentendo l’accesso alle risorse digitali approvate in linea con il marchio, in qualsiasi canale, tramite il selettore risorse o lo stack OpenAPI. Principi chiave: nessuna copia binaria, le risorse vengono ottimizzate e trasformate al limite per prestazioni veloci, fornire risorse pubbliche o sicure.

![Nuovo diagramma di flusso dei dati di Dynamic Media](/help/assets/assets/dm-openapi-dfd.png)


### Nuove funzioni nella Vista risorse {#assets-view-new-features}

**Sono disponibili altre opzioni nella dashboard di approfondimenti sulle risorse**

Il conteggio delle risorse per tipo e dimensione di risorsa è ora disponibile nella dashboard di approfondimenti sulle risorse. Queste opzioni forniscono dati in tempo reale nell’ambiente di vista Assets. Descrivono in dettaglio il conteggio e la percentuale delle risorse per intervallo di dimensioni e tipo di risorsa.

**Aggiornamenti all’editor di Adobe Express incorporato**

* È stata migliorata l’esperienza dell’utente per salvare come nuova risorsa anziché come nuova versione.

* Esportazione di documenti Express multipagina (in precedenza era supportata solo una pagina singola) in entrambi i formati PDF multipagina e immagine. Selezionando i formati immagine, ogni pagina viene salvata come una risorsa distinta in DAM per la distribuzione a valle.

* Supporto per l’aggiunta di metadati nella finestra di dialogo Salva durante il salvataggio di una risorsa.

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nuove funzioni in AEM Forms {#forms-new-prerelease-features}

#### Editor di regole visivo ottimizzato per moduli adattivi basati su componenti core

Questa versione apporta un aggiornamento significativo all’editor di regole visivo per i moduli adattivi basati su componenti core. Ora puoi:

* Creare regole nell’editor di regole visive per [sovrascrivere i messaggi di esito positivo/negativo predefiniti per l’invio del modulo](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* Nell’editor di regole dei moduli adattivi, è stata aggiunta la possibilità di [selezionare diversi tipi di campi per l’operazione WHEN](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* Un autore di moduli ora può applicare funzioni personalizzate alla [preelaborazione dei dati prima dell’invio](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Utilizza la funzionalità [**Salva come bozza**](/help/forms/save-core-component-based-form-as-draft.md) per salvare moduli parzialmente completati da inviare successivamente. Ciò è utile negli scenari in cui gli utenti devono interrompere la compilazione di un modulo e completarlo in seguito.

### Funzionalità per Accesso anticipato ad AEM Forms {#forms-new-early-access-features}

Il programma di accesso anticipato per AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia prima di chiunque altro e contribuire a definirne lo sviluppo. Il programma offre l’accesso a molteplici innovazioni.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Metodi di protezione bot migliorati

AEM Forms ha migliorato le sue funzioni di sicurezza aggiungendo il supporto per due soluzioni CAPTCHA popolari: Cloudflare Turnstile e hCaptcha. Questa funzionalità integra il Google reCAPTCHA esistente e offre agli utenti opzioni aggiuntive. Migliora la flessibilità nella protezione dei loro moduli da bot e invii di spam.

* **Cloudflare Turnstile**: questo CAPTCHA intuitivo verifica gli utenti attraverso una semplice sfida che non richiede un’interazione esplicita. Si integra perfettamente nei moduli, migliorando l’esperienza utente.
* **hCaptcha**: CAPTCHA incentrato sulla privacy che offre un’alternativa di facile utilizzo con particolare attenzione alla privacy dei dati. Mira a trovare un equilibrio tra sicurezza ed esperienza dell’utente.
* **Google reCAPTCHA**: AEM Forms continua a supportare sia reCAPTCHA v2 che reCAPTCHA Enterprise, offrendo una soluzione affidabile e consolidata.

Offrendo più opzioni CAPTCHA, AEM Forms ti consente di selezionare la soluzione più adatta alle tue esigenze specifiche.

Sei pronto a integrare una di queste soluzioni CAPTCHA con i moduli adattivi? La documentazione Adobe fornisce istruzioni dettagliate per: [Cloudflare Turnstile](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) e [Google reCAPTCHA](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Servizio Forms

Il servizio Forms genera moduli PDF interattivi per l’acquisizione dei dati. Può essere utilizzato anche per importare o esportare dati da e verso un modulo interattivo PDF esistente e convalidare i dati inviati. Ecco una suddivisione delle sue funzionalità:

* **Rendering di moduli**: genera un modulo PDF interattivo da un modello creato con AEM Forms Designer e, facoltativamente, da dati XML. Questa funzionalità produce un modulo PDF compilabile, facoltativamente precompilato con i dati.
* **Estrazione e importazione dei dati**: importa i dati in un modulo PDF esistente ed estrae i dati da un modulo PDF compilato. Sono supportati sia i formati di dati XDP che XML e l’importazione in moduli PDF non XFA (noti anche come AcroForms); supporta anche i dati FDF e XFDF.
* **Convalida dei dati**: convalida dei dati inviati, in formato XDP o XML, in base a un modello creato utilizzando AEM Forms Designer.

>[!IMPORTANT]
>
> Se ti interessa partecipare al programma di accesso anticipato di Adobe per qualsiasi innovazione, invia un’e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com). Puoi richiedere l’accesso a tutte le innovazioni o solo a qualcuna.


## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Programma per i primi utilizzatori per le notifiche del centro per le azioni relative all’integrità dei contenuti {#actions-center-notifications}

Il [Centro azioni](/help/operations/actions-center.md) invia notifiche e-mail quando si verificano problemi importanti, o se viene notato qualcosa in merito al codice o alla configurazione in cui dovresti intervenire in modo proattivo. Adobe ha ora introdotto diversi nuovi tipi di notifiche associate all’integrità dei contenuti. Questa funzione è disponibile tramite un programma per i primi utilizzatori. Per partecipare, contatta l’Assistenza clienti Adobe.

#### Le pagine contengono un numero elevato di nodi {#page-nodes}

Un numero elevato di nodi può ridurre le prestazioni di rendering e i tempi di caricamento delle pagine. Ricevi una notifica proattiva tramite il Centro azioni quando viene rilevato un numero elevato di nodi in una pagina, consentendo di adottare le misure necessarie per ridurre il numero totale di nodi all’interno di una pagina.

#### Numero elevato di istanze di flusso di lavoro in esecuzione {#running-workflows}

Le prestazioni del motore del flusso di lavoro sono interessate quando nell’ambiente di authoring è presente un numero elevato di flussi di lavoro in esecuzione. Ricevi una notifica proattiva tramite il Centro azioni quando viene rilevato un numero elevato di istanze di flusso di lavoro in esecuzione. Questo processo consente di configurare un processo di eliminazione per interrompere flussi di lavoro in esecuzione non necessari.

#### Utenti aggiunti direttamente ai gruppi personalizzati {#users-customgroups}

Ricevi una notifica proattiva tramite il Centro azioni quando gli utenti vengono aggiunti direttamente ai gruppi personalizzati. Questo processo consente di seguire le best practice IMS aggiungendo utenti ai gruppi IMS rilevanti e includendo quindi tali gruppi IMS come membri dei gruppi AEM.

#### Contenuto JCR mancante {#jcr-content}

Il Centro azioni invia una notifica proattiva quando viene rilevato un contenuto JCR mancante. Questo approccio consente di aggiungere i contenuti mancanti e di evitare l’errore di alcune funzioni di AEM Assets.

#### Flussi di lavoro completati non eliminati {#workflows}

Il Centro azioni notifica in modo proattivo quando i flussi di lavoro completati oltre i 90 giorni non sono stati eliminati. Questo approccio consente di migliorare le prestazioni del motore del flusso di lavoro riducendo il numero di istanze del flusso di lavoro.

#### Risorsa Sling mancante {#sling-resource}

Il Centro azioni invia una notifica proattiva quando viene rilevata una risorsa Sling mancante. Questo approccio consente di aggiungere la risorsa mancante e di evitare l’errore di alcune funzioni di AEM Assets.

### Programmi per i primi utilizzatori relativi alla distribuzione dei contenuti {#foundation-early-adopter}

Invia un’e-mail all’indirizzo **<aemcs-cdn-config-adopter@adobe.com>**, indicando quali dei programmi per i primi utilizzatori seguenti ti interessa.

#### Autenticazione di base alla rete CDN (Programma per i primi utilizzatori) {#basicauth-cdn}

Proteggi alcune risorse di contenuto visualizzando una finestra di dialogo di autenticazione di base che richiede un nome utente e una password. Questa funzione è destinata principalmente a casi d’uso di autenticazione leggera, come la revisione dei contenuti da parte delle parti aziendali interessate, anziché fungere da soluzione completa per i diritti di accesso degli utenti finali. L’elenco di nome utente e password in gestito tramite un file di configurazione in Git distribuito tramite la pipeline di configurazione, con riferimento alle variabili di ambiente Cloud Manager di tipo segreto. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Eliminare i contenuti dalla rete CDN con una chiave API self-service (Programma per i primi utilizzatori) {#purge-cdn}

Registrare una chiave API di eliminazione CDN in modo self-service e utilizzarla per annullare la validità del contenuto sulla CDN, a livello globale o per una o più risorse. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Creazione self-service di X-AEM-Edge-Key per rete CDN gestita dalla clientela (BYOCDN) (Programma per i primi utilizzatori) {#byocdn-keys}

In precedenza, era necessario un ticket di supporto per generare la chiave X-AEM-Edge-Key necessaria per la configurazione di una rete CDN gestita dalla clientela. Ora è possibile eseguire questa operazione in modo autonomo tramite un file di configurazione distribuito utilizzando la pipeline di configurazione, rimuovendo eventuali ritardi nell’onboarding di un nuovo ambiente. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Reindirizzamenti Lato Server (Programma Early Adopter) {#server-side-redirects-early-adopter}

Configura i reindirizzamenti lato server 301/302 nel controllo del codice sorgente e distribuiscili alla rete CDN. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Attenzione: sono già disponibili diverse altre funzioni correlate a [Configurazione CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), comprese le trasformazioni di richiesta e risposta e il routing del traffico verso siti esterni ad AEM.

#### Avvisi sulle regole del filtro del traffico (programma per i primi utilizzatori) {#traffic-filter-rules-alerts-early-adopter}

Le [Regole del filtro del traffico](/help/security/traffic-filter-rules-including-waf.md) rilasciate di recente, che includono le regole WAF (Web Application Firewall) con licenza facoltativa a parte, permettono di configurare il traffico da consentire o bloccare.

Ora puoi inviare un’e-mail per partecipare al programma per i primi utilizzatori in modo da poter ricevere un avviso ogni volta che vengono attivate le tue regole del filtro del traffico. Le notifiche e-mail del Centro azioni ti informeranno quando si verificano determinate condizioni di traffico, in modo che tu possa adottare le misure appropriate.

#### Gli utenti aziendali possono dichiarare i reindirizzamenti al di fuori di Git (programma per i primi utilizzatori) {#apache-rewritemaps-early-adopter}

In modo simile ad AEM 6.5, Apache/dispatcher acquisisce le mappe di riscrittura che si trovano in una posizione specifica nell’archivio di pubblicazione e le carica, senza richiedere l’esecuzione di una pipeline a livello web. Questo approccio consente agli utenti aziendali di dichiarare i reindirizzamenti utilizzando un foglio di calcolo o un’interfaccia utente, come ACS Commons Redirect Map Manager o un’applicazione personalizzata. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) per il caricamento di contenuti dinamici (programma per i primi utilizzatori) {#esi-early-adopter}

Adobe Managed CDN ora supporta [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un linguaggio di markup per l’assemblaggio di contenuti web dinamici a livello di edge. Includendo snippet ESI, è possibile memorizzare nella cache la pagina HTML generale sulla rete CDN con valori TTL più elevati e recuperare con maggiore frequenza dall’origine le sezioni più piccole che richiedono aggiornamenti più frequenti (TTL più bassi). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## Guide di [!DNL Experience Manager] {#guides}

L’elenco completo delle funzioni nuove e migliorate dell’ultima versione delle Guide di Adobe Experience Manager è disponibile [qui](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universale {#universal-editor}

L’elenco completo dei rilasci dell’editor universale è disponibile [qui](/help/release-notes/universal-editor/current.md).

## Generare varianti {#generate-variations}

L’elenco completo dei rilasci di generare varianti è disponibile [qui](/help/generative-ai/release-notes-generate-variations.md).

## Note sulla versione di Experience Cloud {#experience-cloud}

Informazioni sulle versioni di altre applicazioni Experience Cloud sono disponibili [qui](https://experienceleague.adobe.com/it/docs/release-notes/experience-cloud/current).
