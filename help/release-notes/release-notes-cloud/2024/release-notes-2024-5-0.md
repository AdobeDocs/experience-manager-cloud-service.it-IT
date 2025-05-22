---
title: Note sulla versione 2024.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2024.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 7b7a27f9-ba57-4eb2-9fcb-653b5213af04
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: tm+mt
source-wordcount: '1943'
ht-degree: 98%

---

# Note sulla versione 2024.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2024.5.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2022 o 2023.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente della funzione di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.5.0) è il 30 maggio 2024. La prossima versione funzionale (2024.6.0) è pianificata per il 27 giugno 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica della versione di maggio 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in Sites {#sites-new-features}

#### Integrazione della traduzione AEM {#translation-integration}

Le azioni e i flussi di lavoro per la traduzione dei contenuti ora attivano gli eventi per consentire il tracciamento dei passaggi e degli stati del processo pertinenti da applicazioni esterne. I seguenti eventi sono in fase di generazione. Gli utenti potranno iscriversi agli eventi utilizzando Adobe Developer Console.

* `TRANSLATION_JOB_CREATED`
* `TRANSLATION_JOB_CONTENT_ADDITION_STARTED`
* `TRANSLATION_JOB_CONTENT_ADDITION_COMPLETED`
* `TRANSLATION_JOB_CONTENT_DELETION_STARTED`
* `TRANSLATION_JOB_CONTENT_DELETION_COMPLETED`
* `TRANSLATION_JOB_COMMITTED_FOR_TRANSLATION`
* `TRANSLATION_JOB_READY_FOR_REVIEW`
* `TRANSLATION_JOB_APPROVED`
* `TRANSLATION_JOB_COMPLETED`
* `TRANSLATION_JOB_CANCELLED`
* `TRANSLATION_JOB_ERROR`

#### Servizio di telemetria operativa {#real-use-monitoring}

* **[Il servizio di telemetria operativa è ora GA](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** e abilita la raccolta di dati lato client per AEM as a Cloud Service.
Il servizio dati del Monitoraggio degli utenti reali (RUM) per la raccolta lato client rispecchia in modo più preciso le interazioni, per una misurazione affidabile del coinvolgimento nel sito web. Consente ai clienti di ottenere insight avanzati sul traffico e sulle prestazioni delle pagine. Permette di saperne di più sulle prestazioni delle pagine e di ottenere insight utili a migliorarle.

#### Authoring di AEM per Edge Delivery Services {#edge-enhancements}

Maggiore stabilità e vari miglioramenti per un’ottimale esperienza di authoring.

### Programma per i primi utilizzatori {#sites-early-adopter}

**Generare varianti**

Sfruttare l’intelligenza artificiale generativa tramite la nuova funzione di AEM, [genera varianti](/help/generative-ai/generate-variations.md), ora accessibile in Cloud Service. Genera varianti consente di generare e ridimensionare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al tuo team Adobe Account per prendere in considerazione il programma.

**Esplorazione delle risorse nella console Frammenti di contenuto**

Gli autori dei contenuti ora possono esplorare, visualizzare e intervenire sulle immagini e su altre risorse senza dover uscire dalla console Frammenti di contenuto.

![Esplorazione delle risorse](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Per ulteriori informazioni sul programma per i primi utilizzatori, invia un’e-mail all’indirizzo aemcs-headless-adopter@adobe.com dal tuo ID e-mail ufficiale.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella vista Amministratore {#admin-view-new-features}

* WebM è ora un file di output supportato nel profilo di elaborazione per video.
* MP4 è ora supportato nell’integrazione nativa di AEM in Express (importazione ed esportazione).

### Nuove funzioni nella Vista risorse {#assets-view-new-features}

**Pubblicare risorse in AEM e Dynamic Media**

Experience Manager Assets ora consente di [pubblicare risorse su Experience Manager e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md) in modo rapido, utilizzando la vista Risorse senza passare alla vista Amministratore. Puoi pubblicare le risorse durante il caricamento, la navigazione e la ricerca.

![controllare lo stato di pubblicazione1](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nuove funzioni pre-release in AEM Forms {#forms-new-prerelease-features}

#### Editor di regole visive ottimizzato per moduli adattivi basati su componenti core

Questa versione apporta un aggiornamento significativo all’editor di regole visive per i moduli adattivi basati su componenti core. Ora puoi:

* Crea regole nell’editor di regole visivo per [sovrascrivere i messaggi di esito positivo/negativo predefiniti per l’invio del modulo](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* Nell’editor di regole dei moduli adattivi, è stata aggiunta la possibilità di [selezionare diversi tipi di campi per l’operazione WHEN](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* Un autore di moduli ora può applicare funzioni personalizzate alla [preelaborazione dei dati prima dell’invio](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Utilizza la funzionalità [**Salva come bozza**](/help/forms/save-core-component-based-form-as-draft.md) per salvare moduli parzialmente completati da inviare successivamente. Ciò è utile negli scenari in cui gli utenti devono interrompere la compilazione di un modulo e completarlo in seguito.



### Funzionalità per Accesso anticipato ad AEM Forms {#forms-new-early-access-features}

Il programma di accesso anticipato per AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia prima di chiunque altro e contribuire a definirne lo sviluppo. Il programma offre l’accesso a molteplici innovazioni.

In queste note sulla versione sono elencate le nuove funzioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [Documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Metodi di protezione bot migliorati

AEM Forms ha migliorato le sue funzioni di sicurezza aggiungendo il supporto per due soluzioni CAPTCHA popolari: Cloudflare Turnstile e hCaptcha. Queste si aggiungono al già disponibile Google reCAPTCHA, fornendo agli utenti una maggiore scelta e flessibilità nel proteggere i loro moduli da bot e invii di spam.

* **Cloudflare Turnstile**: questo intuitivo CAPTCHA verifica gli utenti attraverso una semplice sfida che non richiede un’interazione esplicita. Si integra perfettamente nei moduli, migliorando l’esperienza utente.
* **hCaptcha**: CAPTCHA incentrato sulla privacy che offre un’alternativa di facile utilizzo con particolare attenzione alla privacy dei dati. Mira a trovare un equilibrio tra sicurezza ed esperienza dell’utente.
* **Google reCAPTCHA**: AEM Forms continua a supportare sia reCAPTCHA v2 che reCAPTCHA Enterprise, offrendo una soluzione affidabile e consolidata.

Offrendo più opzioni CAPTCHA, AEM Forms ti consente di selezionare la soluzione più adatta alle tue esigenze specifiche.

Sei pronto a integrare una di queste soluzioni CAPTCHA con il tuo modulo adattivo? La nostra documentazione fornisce istruzioni dettagliate per ciascuno di essi: [Cloudflare Turnstile](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) e [Google reCAPTCHA](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Servizio Forms

Il servizio Forms genera moduli PDF interattivi per l’acquisizione dei dati. Può essere utilizzato anche per importare o esportare dati da e verso un modulo interattivo PDF esistente e convalidare i dati inviati. Ecco una suddivisione delle sue funzionalità:

* **Rendering di moduli**: genera un modulo PDF interattivo da un modello creato con AEM Forms Designer e, facoltativamente, da dati XML. In sostanza, questo produce un modulo PDF compilabile, facoltativamente precompilato con i dati.
* **Estrazione e importazione dei dati**: importa i dati in un modulo PDF esistente ed estrae i dati da un modulo PDF compilato. Sono supportati sia i formati di dati XDP che XML e l’importazione in moduli PDF non XFA (noti anche come AcroForms); supporta anche i dati FDF e XFDF.
* **Convalida dei dati**: convalida dei dati inviati, in formato XDP o XML, in base a un modello creato utilizzando AEM Forms Designer.

>[!IMPORTANT]
>
> Se ti interessa partecipare al nostro programma per l’accesso anticipato per qualsiasi innovazione iniziale, per richiedere l’accesso, è sufficiente inviare un’e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com). Puoi richiedere l’accesso a tutte le innovazioni o solo a qualcuna.


## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Supporto delle credenziali server-to-server OAuth per le integrazioni AEM con altre soluzioni Adobe {#S2S-OAuth-credentials}

Adobe Developer Console viene utilizzata per generare le credenziali di accesso a varie API. Uno di questi tipi di credenziali, le credenziali dell’account di servizio (JWT), è stato dichiarato obsoleto a favore delle credenziali OAuth server-to-server, che AEM Cloud Service ora supporta per le integrazioni con altre soluzioni di Adobe come Adobe Analytics e Adobe Target.

[Leggi informazioni sull’elemento obsoleto](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md) e [scopri come utilizzare l’interfaccia utente di creazione AEM](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) per configurare le integrazioni con altre soluzioni Adobe.

### Avviso predefinito di picco nel traffico all’origine {#traffic-spike-origin}

[Ricevezione di notifiche proattive](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert) tramite il Centro operativo quando i pattern di traffico all’origine sono indicativi di un attacco DDoS: questo ti consente di indagare e configurare le regole del filtro del traffico.

### Nuove funzioni per RDE (ambienti di sviluppo rapido) {#RDE-new-features}

[Ambienti di sviluppo rapido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) consente agli sviluppatori di implementare, rivedere e testare rapidamente le modifiche in Cloud. Molte nuove funzioni saranno introdotte nel mese di giugno. Ti invitiamo inoltre a interagire direttamente coni tecnici Adobe sul [canale Discord RDE](https://discord.com/channels/1131492224371277874/1245304281184079872).


#### Supporto RDE per il codice front-end tramite i temi e i modelli del sito {#rde-frontend}

Gli [ambienti di sviluppo rapido (RDE) ora supportano il codice front-end](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) basato su [temi del sito](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelli di sito](/help/sites-cloud/administering/site-creation/site-templates.md), per i primi utilizzatori. Con gli RDE, questa operazione viene eseguita utilizzando una direttiva della riga di comando, anziché una [pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

#### Registrazione avanzata per gli RDE {#rde-logging}

Durante il debug del codice in un’ambiente di sviluppo rapido (RDE), gli sviluppatori possono ora [configurare e inviare i registri in modo più efficiente](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging), utilizzando la riga di comando e senza modificare le proprietà OSGI nel controllo della versione. Le funzioni includono:

* dichiarazione dei livelli di registro a livello di pacchetto o classe
* personalizzazione del formato di output del registro
* esecuzione dello streaming di più registri in parallelo

#### Miglioramenti di RDE CLI {#rde-cli-enhancements}

L’interfaccia della riga di comando RDE dispone di alcune nuove funzioni che migliorano l’esperienza dello sviluppatore:

* [il comando di configurazione è interattivo](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive), questo semplifica la scelta tra organizzazioni, programmi e ambienti. Ora è anche possibile ignorare questi valori nella riga di comando.
* [modalità silenziosa](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) per un output meno dettagliato.
* [modalità json](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) per ottenere un output utile quando viene richiamato a livello di programmazione.

### Nuove notifiche del Centro azioni {#actions-center-notifications}

Il [Centro azioni](/help/operations/actions-center.md) invia notifiche e-mail quando si verificano problemi importanti, o se viene notato qualcosa in merito al tuo codice o alla tua configurazione in cui dovresti intervenire in modo proattivo. Esistono tre nuovi tipi di notifica:

* troppe connessioni in uscita tramite l’infrastruttura di rete avanzata
* utilizzo di un formato di mappatura utenti del servizio obsoleto
* è in corso un potenziale attacco DDoS

### Programma per i primi utilizzatori {#foundation-early-adopter}

Invia un’e-mail all’indirizzo **<aemcs-cdn-config-adopter@adobe.com>**, indicando quali dei programmi per i primi utilizzatori seguenti ti interessa.

#### Eliminare i contenuti dalla rete CDN con una chiave API self-service (Programma per i primi utilizzatori) {#purge-cdn}

Registrare una chiave API di eliminazione CDN in modo self-service e utilizzarla per annullare la validità del contenuto sulla CDN, a livello globale o per una o più risorse. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Creazione self-service di X-AEM-Edge-Key per rete CDN gestita dalla clientela (BYOCDN) (Programma per i primi utilizzatori) {#byocdn-keys}

In precedenza, era necessario un ticket di supporto per generare la chiave X-AEM-Edge-Key necessaria per la configurazione di una rete CDN gestita dalla clientela. Ora è possibile eseguire questa operazione in modo autonomo tramite un file di configurazione distribuito utilizzando la pipeline di configurazione, rimuovendo eventuali ritardi nell’onboarding di un nuovo ambiente. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Reindirizzamenti lato server (programma Early Adopter) {#server-side-redirects-early-adopter}

Configura i reindirizzamenti lato server 301/302 nel controllo del codice sorgente e distribuiscili alla rete CDN. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Attenzione: sono già disponibili diverse altre funzioni correlate a [Configurazione CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), comprese le trasformazioni di richiesta e risposta e il routing del traffico verso siti esterni ad AEM.

#### Avvisi sulle regole del filtro del traffico (programma per i primi utilizzatori) {#traffic-filter-rules-alerts-early-adopter}

Le [Regole del filtro del traffico](/help/security/traffic-filter-rules-including-waf.md) rilasciate di recente, che includono le regole WAF (Web Application Firewall) con licenza facoltativa a parte, permettono di configurare il traffico da consentire o bloccare.

Ora puoi inviare un’e-mail per partecipare al programma per i primi utilizzatori in modo da poter ricevere un avviso ogni volta che vengono attivate le tue regole del filtro del traffico. Le notifiche e-mail del Centro azioni ti informeranno quando si verificano determinate condizioni di traffico, in modo che tu possa adottare le misure appropriate.

#### Gli utenti aziendali possono dichiarare i reindirizzamenti al di fuori di Git (programma per i primi utilizzatori) {#apache-rewritemaps-early-adopter}

In modo simile ad AEM 6.5, Apache/dispatcher acquisisce le mappe di riscrittura che si trovano in una posizione specifica nell’archivio di pubblicazione e le carica, senza richiedere l’esecuzione di una pipeline a livello web. Questo offre a un utente aziendale l’opportunità di dichiarare i reindirizzamenti utilizzando un foglio di calcolo o un’interfaccia utente, come quella offerta da ACS Commons Redirect Map Manager o creata come parte di un’applicazione della clientela. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) per il caricamento di contenuti dinamici (programma per i primi utilizzatori) {#esi-early-adopter}

Adobe Managed CDN ora supporta [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un linguaggio di markup per l’assemblaggio di contenuti web dinamici a livello di edge. Includendo snippet ESI, è possibile memorizzare nella cache la pagina HTML generale sulla rete CDN con valori TTL più elevati e recuperare con maggiore frequenza dall’origine le sezioni più piccole che richiedono aggiornamenti più frequenti (TTL più bassi). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] Guides {#guides}

* **Pubblicare un argomento o i relativi elementi in un frammento di esperienza**
Ora, Experience Manager Guides consente di pubblicare un argomento o i relativi elementi in un frammento di esperienza. Un frammento di esperienza è un’unità di contenuto modulare che integra sia il contenuto che il layout.  I frammenti di esperienza sono fondamentali e possono aiutarti a creare esperienze coerenti e coinvolgenti.
* **Possibilità di passare i metadati delle risorse degli argomenti all’output PDF nativo**
Puoi aggiungere i metadati delle risorse degli argomento durante la generazione dell’output PDF nativo. Questa funzione consente di aggiungere metadati specifici per argomenti diversi, come titolo e autore di ogni argomento, alle intestazioni e ai piè di pagina dello stesso.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, vedi [Roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Note sulla versione di Experience Cloud {#experience-cloud}

Informazioni sulle versioni di altre applicazioni Experience Cloud sono disponibili [qui](https://experienceleague.adobe.com/it/docs/release-notes/experience-cloud/current).
Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).
