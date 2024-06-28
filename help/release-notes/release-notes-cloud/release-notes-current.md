---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 19b52f733a592c7e84ba2e9d83d37e5e181f21ab
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 60%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note specifiche sulla versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2022 o 2023.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.6.0) è il venerdì 27 giugno 2024. La successiva versione funzionale (2024.7.0) è pianificata per il venerdì 25 luglio 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!--  ## Release Video {#release-video}

Have a look at the June 2024 Release Overview video for a summary of the features added in the 2024.6.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programma per i primi utilizzatori {#sites-early-adopter}

**Generare varianti**

Sfruttare l’intelligenza artificiale generativa tramite la nuova funzione di AEM, [genera varianti](/help/generative-ai/generate-variations.md), ora accessibile in Cloud Service. Genera varianti consente di generare e ridimensionare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al tuo team Adobe Account per prendere in considerazione il programma.

**Esplorazione delle risorse nella console Frammenti di contenuto**

Gli autori dei contenuti ora possono esplorare, visualizzare e intervenire sulle immagini e su altre risorse senza dover uscire dalla console Frammenti di contenuto.

![Esplorazione delle risorse](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Per ulteriori informazioni sul programma per i primi utilizzatori, invia un’e-mail all’indirizzo aemcs-headless-adopter@adobe.com dal tuo ID e-mail ufficiale.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni di Experience Manager Assets {#new-features-assets}

**Content Hub**

Content Hub è disponibile come parte di Experience Manager Assets as a Cloud Service per la democratizzazione dell’accesso ai contenuti sul marchio per le organizzazioni e i loro partner commerciali. Con Content Hub, puoi trovare e distribuire facilmente le risorse, riutilizzare e creare nuove varianti di marchio e accelerare l’attivazione su larga scala.

![Interfaccia utente di Content Hub](/help/release-notes/assets/content-hub-ui.png)

**Dynamic Medie con funzionalità OpenAPI**

Dynamic Medie con funzionalità OpenAPI estende il DAM a più applicazioni di Adobe e terze parti, consentendo l’accesso alle risorse digitali approvate dal marchio, in qualsiasi canale, tramite Asset Selector o stack OpenAPI. Principi chiave: nessuna copia binaria, le risorse vengono ottimizzate e trasformate al limite per prestazioni veloci, fornire risorse pubbliche o sicure.

![Nuovo diagramma di flusso dei dati di Dynamic Medie](/help/assets/assets/dm-openapi-dfd.png)


### Nuove funzioni nella Vista risorse {#assets-view-new-features}

**Altre opzioni disponibili nella dashboard di Assets Insights**

Il conteggio delle risorse per tipo e dimensione di risorsa è ora disponibile nella dashboard di Assets Insights. Queste opzioni forniscono dati in tempo reale nell’ambiente di visualizzazione Assets sul conteggio e la percentuale delle risorse per intervallo di dimensioni e tipo di risorsa.

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

#### Editor di regole visive ottimizzato per moduli adattivi basati su componenti core

Questa versione apporta un aggiornamento significativo all’editor di regole visive per i moduli adattivi basati su componenti core. Ora puoi:

* Creare regole nell’editor di regole visive per [ignora i messaggi di esito positivo/negativo predefiniti per l’invio del modulo](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* Nell’editor di regole dei moduli adattivi, è stata aggiunta la possibilità di [selezionare diversi tipi di campi per l’operazione WHEN](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* Un autore di moduli ora può applicare funzioni personalizzate alla [preelaborazione dei dati prima dell’invio](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Utilizza la funzionalità [**Salva come bozza**](/help/forms/save-core-component-based-form-as-draft.md) per salvare moduli parzialmente completati da inviare successivamente. Ciò è utile negli scenari in cui gli utenti devono interrompere la compilazione di un modulo e completarlo in seguito.

### Funzioni di accesso anticipato in AEM Forms {#forms-new-early-access-features}

Il programma AEM Forms Early Access Program offre l’opportunità unica di accedere in esclusiva alle innovazioni all’avanguardia prima di chiunque altro, e di aiutarti a modellarne lo sviluppo. Il programma offre l’accesso a molteplici innovazioni.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma di accesso anticipato, consulta [Documentazione del programma di accesso anticipato AEM Forms](/help/forms/early-access-ea-features.md).

#### Metodi di protezione bot migliorati

AEM Forms ha migliorato le sue funzioni di sicurezza aggiungendo il supporto per due soluzioni CAPTCHA popolari: Cloudflare Turnstile e hCaptcha. Queste si aggiungono al già disponibile Google reCAPTCHA, fornendo agli utenti una maggiore scelta e flessibilità nel proteggere i loro moduli da bot e invii di spam.

* **Cloudflare Turnstile**: questo intuitivo CAPTCHA verifica gli utenti attraverso una semplice sfida che non richiede un’interazione esplicita. Si integra perfettamente nei moduli, migliorando l’esperienza utente.
* **hCaptcha**: CAPTCHA incentrato sulla privacy che offre un’alternativa di facile utilizzo con particolare attenzione alla privacy dei dati. Mira a trovare un equilibrio tra sicurezza ed esperienza dell’utente.
* **Google reCAPTCHA**: AEM Forms continua a supportare sia reCAPTCHA v2 che reCAPTCHA Enterprise, offrendo una soluzione affidabile e consolidata.

Offrendo più opzioni CAPTCHA, AEM Forms ti consente di selezionare la soluzione più adatta alle tue esigenze specifiche.

Sei pronto a integrare una di queste soluzioni CAPTCHA con il tuo modulo adattivo? La nostra documentazione fornisce istruzioni dettagliate per ciascuno di essi: [Cloudflare Turnstile](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) e [Google reCAPTCHA](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Servizio Forms

Il servizio Forms genera moduli PDF interattivi per l’acquisizione dei dati. Può essere utilizzato anche per importare o esportare dati da e verso un modulo interattivo di PDF esistente e convalidare i dati inviati. Ecco una suddivisione delle sue funzionalità:

* **Rendering di moduli**: genera un modulo PDF interattivo da un modello creato con AEM Forms Designer e, facoltativamente, da dati XML. In sostanza, questo produce un modulo PDF compilabile, facoltativamente precompilato con i dati.
* **Estrazione e importazione dei dati**: importa i dati in un modulo PDF esistente ed estrae i dati da un modulo PDF compilato. Sono supportati sia i formati di dati XDP che XML e l’importazione in moduli PDF non XFA (noti anche come AcroForms); supporta anche i dati FDF e XFDF.
* **Convalida dei dati**: convalida dei dati inviati, in formato XDP o XML, in base a un modello creato utilizzando AEM Forms Designer.

>[!IMPORTANT]
>
> Se sei interessato a partecipare al nostro programma di accesso anticipato per qualsiasi innovazione di accesso anticipato, è sufficiente inviare un’e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) per richiedere l&#39;accesso. Puoi richiedere l’accesso a tutte le innovazioni o solo a qualcuna.


## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Notifiche del Centro per le azioni relative allo stato dei contenuti - Programma di adozione anticipata {#actions-center-notifications}

Il [Centro azioni](/help/operations/actions-center.md) invia notifiche e-mail quando si verificano problemi importanti, o se viene notato qualcosa in merito al tuo codice o alla tua configurazione in cui dovresti intervenire in modo proattivo. Sono stati introdotti diversi nuovi tipi di notifiche associate allo stato dei contenuti. Questa funzione è disponibile tramite un programma per i primi utenti. Per partecipare, contatta l’Assistenza clienti Adobe.

#### Le pagine contengono un numero elevato di nodi {#page-nodes}

Un numero elevato di nodi può ridurre le prestazioni di rendering e i tempi di caricamento delle pagine. Ricevi una notifica proattiva tramite il Centro azioni quando viene rilevato un numero elevato di nodi in una pagina, consentendo di adottare le misure necessarie per ridurre il numero totale di nodi all’interno di una pagina.

#### Numero elevato di istanze del flusso di lavoro in esecuzione {#running-workflows}

Le prestazioni del motore del flusso di lavoro sono interessate quando nell’ambiente di authoring è presente un numero elevato di flussi di lavoro in esecuzione. Ricevi una notifica proattiva tramite il Centro azioni quando viene rilevato un numero elevato di istanze di flussi di lavoro in esecuzione, che ti consente di configurare un processo di eliminazione per terminare flussi di lavoro in esecuzione che non sono necessari.

#### Utenti aggiunti direttamente ai gruppi personalizzati {#users-customgroups}

Ricevi una notifica proattiva tramite il Centro azioni quando gli utenti vengono aggiunti direttamente ai gruppi personalizzati, consentendoti di seguire le best practice IMS per aggiungere utenti ai gruppi IMS pertinenti e quindi aggiungere i gruppi IMS come membri dei gruppi AEM.

#### Contenuto JCR mancante {#jcr-content}

Ricevi una notifica proattiva tramite il Centro azioni quando viene rilevato un contenuto JCR mancante, che ti consente di aggiungere il contenuto JCR mancante ed evitare errori in alcune funzioni di AEM Assets.

#### Flussi di lavoro completati non eliminati {#workflows}

Ricevi una notifica proattiva tramite il Centro azioni quando i flussi di lavoro completati nell’arco di 90 giorni non sono stati eliminati, consentendoti di migliorare le prestazioni del motore del flusso di lavoro riducendo al minimo il numero di istanze.

#### Risorsa Sling mancante {#sling-resource}

Ricevi una notifica proattiva tramite il Centro azioni quando viene rilevata una risorsa Sling mancante, che ti consente di aggiungere la risorsa Sling mancante ed evitare errori in alcune funzioni di AEM Assets.

### Programmi di adozione anticipata relativi alla distribuzione dei contenuti {#foundation-early-adopter}

Invia un’e-mail all’indirizzo **<aemcs-cdn-config-adopter@adobe.com>**, indicando quali dei programmi per i primi utilizzatori seguenti ti interessa.

#### Autenticazione di base alla rete CDN (Early Adopter Program) {#basicauth-cdn}

Protect alcune risorse di contenuto visualizzando una finestra di dialogo di autenticazione di base che richiede un nome utente e una password. Questa funzione è destinata principalmente a casi di utilizzo di autenticazione leggera, come la revisione dei contenuti da parte delle parti interessate del business, anziché essere una soluzione completa per i diritti di accesso degli utenti finali. L’elenco di nome utente e password in gestito tramite un file di configurazione in Git distribuito tramite la pipeline di configurazione, con riferimento alle variabili di ambiente Cloud Manager di tipo segreto. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Eliminare i contenuti dalla rete CDN con una chiave API self-service (programma di adozione anticipata) {#purge-cdn}

Registrare una chiave API di eliminazione CDN in modo self-service e utilizzarla per annullare la validità del contenuto sulla CDN, a livello globale o per una o più risorse. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Creazione self-service di X-AEM-Edge-Key per rete CDN gestita dal cliente (BYOCDN) (programma di adozione anticipata) {#byocdn-keys}

In precedenza, era necessario un ticket di supporto per generare la chiave X-AEM-Edge-Key necessaria per la configurazione di una rete CDN gestita dalla clientela. Ora è possibile eseguire questa operazione in modo autonomo tramite un file di configurazione distribuito utilizzando la pipeline di configurazione, rimuovendo eventuali ritardi nell’onboarding di un nuovo ambiente. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Reindirizzamenti Lato Client (Programma Early Adopter) {#client-side-redirects-early-adopter}

Configura i reindirizzamenti lato client 301/302 nel controllo del codice sorgente e distribuiscili alla rete CDN. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Attenzione: sono già disponibili diverse altre funzioni correlate a [Configurazione CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), comprese le trasformazioni di richiesta e risposta e il routing del traffico verso siti esterni ad AEM.

#### Avvisi sulle regole del filtro del traffico (programma per i primi utilizzatori) {#traffic-filter-rules-alerts-early-adopter}

Le [Regole del filtro del traffico](/help/security/traffic-filter-rules-including-waf.md) rilasciate di recente, che includono le regole WAF (Web Application Firewall) con licenza facoltativa a parte, permettono di configurare il traffico da consentire o bloccare.

Ora puoi inviare un’e-mail per partecipare al programma per i primi utilizzatori in modo da poter ricevere un avviso ogni volta che vengono attivate le tue regole del filtro del traffico. Le notifiche e-mail del Centro azioni ti informeranno quando si verificano determinate condizioni di traffico, in modo che tu possa adottare le misure appropriate.

#### Gli utenti aziendali possono dichiarare i reindirizzamenti al di fuori di Git (Early Adopter Program) {#apache-rewritemaps-early-adopter}

In modo simile ad AEM 6.5, Apache/dispatcher acquisisce le mappe di riscrittura che si trovano in una posizione specifica nell’archivio di pubblicazione e le carica, senza richiedere l’esecuzione di una pipeline a livello web. Questo offre a un utente aziendale l’opportunità di dichiarare i reindirizzamenti utilizzando un foglio di calcolo o un’interfaccia utente, come quella offerta da ACS Commons Redirect Map Manager o creata come parte di un’applicazione della clientela. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) per il caricamento di contenuti dinamici (programma per i primi utilizzatori) {#esi-early-adopter}

Adobe Managed CDN ora supporta [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un linguaggio di markup per l’assemblaggio di contenuti web dinamici a livello di edge. Includendo snippet ESI, è possibile memorizzare nella cache la pagina HTML generale sulla rete CDN con valori TTL più elevati e recuperare con maggiore frequenza dall’origine le sezioni più piccole che richiedono aggiornamenti più frequenti (TTL più bassi). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## Guide di [!DNL Experience Manager] {#guides}

L’elenco completo delle funzioni nuove e migliorate dell’ultima versione delle Guide di Adobe Experience Manager è disponibile [qui](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Note sulla versione di Experience Cloud {#experience-cloud}

Informazioni sulle versioni di altre applicazioni Experience Cloud sono disponibili [qui](https://experienceleague.adobe.com/it/docs/release-notes/experience-cloud/current).
Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).
