---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: b7e8fd902bb2fe98e183b7d987b87fee69e48337
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 24%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note specifiche sulla versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente della funzione di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.5.0) è il venerdì 30 maggio 2024. La prossima versione funzionale (2024.6.0) è pianificata per il venerdì 27 giugno 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica della versione di maggio 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni di Sites {#sites-new-features}

**Authoring di AEM per Edge Delivery Services**

Maggiore stabilità e vari miglioramenti per una migliore esperienza di authoring.

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
* MP4 è ora supportato nell&#39;integrazione nativa di AEM in Express (importazione ed esportazione).

### Nuove funzioni nella Vista risorse {#assets-view-new-features}

**Pubblicare risorse su AEM e Dynamic Medie**

Experience Manager Assets ora consente di [pubblicare risorse su Experience Manager e Dynamic Medie](/help/assets/publish-assets-to-aem-and-dm.md) utilizzare la vista Risorse senza passare alla vista Amministratore. Puoi pubblicare le risorse durante il caricamento, la navigazione e la ricerca.

![controllare lo stato di pubblicazione1](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nuove funzioni pre-release in AEM Forms {#forms-new-prerelease-features}

#### Editor di regole visive ottimizzato per Forms adattivo basato su componenti core

Questa versione apporta un aggiornamento significativo all’editor di regole visive per i moduli adattivi basati su componenti core. Ora puoi:

* Creare regole nell’editor di regole visive per [sostituire i messaggi di esito positivo/negativo predefiniti per l’invio del modulo](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* Nell’editor di regole di Forms adattivo, è stata aggiunta la possibilità di [selezionare diversi tipi di campi per l&#39;operazione WHEN](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* Un autore di moduli può ora applicare funzioni personalizzate a [pre-elabora dati prima dell’invio](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Utilizza il [**Salva come bozza**](/help/forms/save-core-component-based-form-as-draft.md) funzionalità per salvare moduli parzialmente completati da inviare successivamente. Ciò è utile negli scenari in cui gli utenti devono interrompere la compilazione di un modulo e ritornare in seguito.



### Funzioni introduttive di AEM Forms {#forms-new-early-adopter-features}

Il programma AEM Forms Early Adopter Program offre un’opportunità unica per ottenere l’accesso esclusivo alle innovazioni all’avanguardia prima di chiunque altro e contribuire a modellarne lo sviluppo.
Il programma offre l’accesso a molteplici innovazioni.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma Early Adopter, vedi [Documentazione del programma AEM Forms Early Adopter](/help/forms/early-adopter-ea-features.md).

#### Metodi di protezione bot migliorati

AEM Forms ha migliorato le sue funzioni di sicurezza aggiungendo il supporto per due soluzioni CAPTCHA popolari: Cloudflare Turnstile e hCaptcha. Questo si aggiunge al già disponibile Google reCAPTCHA, fornendo agli utenti una maggiore scelta e flessibilità nel proteggere i loro moduli da bot e invii di spam.

* **Tornello Cloudflare**: questo CAPTCHA senza attriti verifica gli utenti attraverso una semplice sfida che non richiede un’interazione esplicita. Si integra perfettamente nei moduli, migliorando l’esperienza utente.
* **hCaptcha**: CAPTCHA incentrato sulla privacy offre un’alternativa di facile utilizzo incentrata sulla privacy dei dati. Mira a trovare un equilibrio tra sicurezza ed esperienza dell’utente.
* **Google reCAPTCHA**: AEM Forms continua a supportare sia reCAPTCHA v2 che reCAPTCHA Enterprise, offrendo una soluzione affidabile e consolidata.

Offrendo più opzioni CAPTCHA, AEM Forms ti ha consentito di selezionare la soluzione più adatta alle tue esigenze specifiche.

Sei pronto a integrare una di queste soluzioni CAPTCHA con il tuo Forms adattivo? La nostra documentazione fornisce istruzioni dettagliate per ciascuno di essi: [Tornello Cloudflare](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components), e [Google reCAPTCHA](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Servizio Forms

Il servizio Forms genera PDF forms interattivi per l’acquisizione dei dati. Può essere utilizzato anche per importare o esportare dati da e verso un modulo interattivo di PDF esistente e convalidare i dati inviati. Ecco una suddivisione delle sue funzionalità:

* **Rendering di Forms**: genera un modulo PDF interattivo da un modello creato con AEM Forms Designer e, facoltativamente, da dati XML. In sostanza, questo produce un modulo compilabile di PDF, facoltativamente precompilato con i dati.
* **Estrazione e importazione dei dati**: importa i dati in un modulo PDF esistente ed estrae i dati da un modulo PDF compilato. Sono supportati sia i formati di dati XDP che XML e l’importazione in PDF forms non XFA (noti anche come AcroForms) supporta anche i dati FDF e XFDF.
* **Convalida dei dati**: convalida dei dati inviati, in formato XDP o XML, in base a un modello creato utilizzando AEM Forms Designer.

>[!IMPORTANT]
>
> Se sei interessato a partecipare al nostro programma Early Adopter per qualsiasi innovazione iniziale, è sufficiente inviare un’e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) per richiedere l&#39;accesso. Puoi richiedere l’accesso a tutte le innovazioni o a quelle specifiche.


## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Supporto delle credenziali server-to-server OAuth per le integrazioni AEM con altre soluzioni Adobe {#S2S-OAuth-credentials}

La console Adobe Developer viene utilizzata per generare le credenziali di accesso a varie API. Uno di questi tipi di credenziali, le credenziali dell’account di servizio (JWT), è stato dichiarato obsoleto a favore delle credenziali server-to-server OAuth, che AEM Cloud Service ora supporta per le integrazioni con altre soluzioni di Adobe come Adobe Analytics e Adobe Target.

[Leggi informazioni sull’elemento obsoleto](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md) e [scopri come utilizzare l’interfaccia utente di creazione dell’AEM](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) per configurare le integrazioni con altre soluzioni Adobe.

### Picco di traffico negli avvisi di origine {#traffic-spike-origin}

[Ricevere notifiche proattive](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert) tramite il Centro operativo quando i pattern di traffico all’origine sono indicativi di un attacco DDoS, che consente di indagare e configurare le regole del filtro del traffico.

### Nuove funzioni per gli RDE {#RDE-new-features}

[Ambienti di sviluppo rapido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) consente agli sviluppatori di implementare, rivedere e testare rapidamente le modifiche in Cloud. Molte nuove funzioni saranno introdotte nel mese di giugno. Ti invitiamo inoltre a interagire direttamente con l’ingegneria Adobe presso [Canale discordia RDE](https://discord.com/channels/1131492224371277874/1245304281184079872).


#### Supporto RDE per il codice front-end tramite Temi del sito e Modelli del sito {#rde-frontend}

[Gli RDE ora supportano il codice front-end](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) in base a [temi del sito](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelli di sito](/help/sites-cloud/administering/site-creation/site-templates.md), per i primi utilizzatori. Con gli RDE, questa operazione viene eseguita utilizzando una direttiva della riga di comando, anziché una [pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

#### Registrazione avanzata per gli RDE {#rde-logging}

Durante il debug del codice in un RDE, gli sviluppatori possono ora [configurazione e streaming dei registri in modo più produttivo](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging), utilizzando la riga di comando e senza modificare le proprietà OSGI nel controllo della versione. Le funzioni includono:

* dichiarazione dei livelli di registro per pacchetto o livello di classe
* personalizzazione del formato di output del registro
* streaming di più registri in parallelo

#### Miglioramenti di RDE CLI {#rde-cli-enhancements}

L’interfaccia della riga di comando RDE dispone di alcune nuove funzioni che migliorano l’esperienza di sviluppo:

* [il comando di installazione è interattivo](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive), semplificando la scelta tra organizzazioni, programmi e ambienti. Ora è anche possibile ignorare questi valori nella riga di comando.
* [modalità non interattiva](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) per un output meno dettagliato.
* [modalità json](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) per ottenere un output utile quando viene richiamato a livello di programmazione.

### Nuove notifiche del Centro azioni {#actions-center-notifications}

[Centro azioni](/help/operations/actions-center.md) invia notifiche e-mail quando si verificano incidenti importanti, o se notiamo qualcosa sul tuo codice o sulla tua configurazione in cui dovresti intervenire in modo proattivo. Esistono tre nuovi tipi di notifica:

* troppe connessioni in uscita tramite l&#39;infrastruttura di rete avanzata
* utilizzo di un formato di mappatura utenti del servizio obsoleto
* è in corso un potenziale attacco DDoS

### Programma per i primi utilizzatori {#foundation-early-adopter}

E-mail **<aemcs-cdn-config-adopter@adobe.com>**, che indica a quali dei primi programmi di adozione in basso sei interessato.

#### Elimina i contenuti dalla rete CDN con una chiave API self-service (Early Adopter Program) {#purge-cdn}

Registra una chiave API di eliminazione CDN in modo self-service e utilizzala per annullare la validità del contenuto sulla CDN, a livello globale o per una o più risorse. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Creazione self-service di X-AEM-Edge-Key per rete CDN gestita dal cliente (BYOCDN) (programma Early Adopter) {#byocdn-keys}

In precedenza, era necessario un ticket di supporto per generare la chiave X-AEM-Edge-Key necessaria per la configurazione di una rete CDN gestita dal cliente. Ora è possibile eseguire questa operazione in modo autonomo tramite un file di configurazione distribuito utilizzando la pipeline di configurazione, rimuovendo eventuali ritardi nell’onboarding di un nuovo ambiente. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Reindirizzamento lato client (programma per i primi utilizzatori) {#client-side-redirects-early-adopter}

Configura i reindirizzamenti lato client 301/302 nel controllo del codice sorgente e distribuiscili alla rete CDN. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Sono già disponibili diverse altre funzioni correlate a [Configurazione CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), comprese le trasformazioni di richiesta e risposta e il traffico di indirizzamento verso siti esterni all’AEM.

#### Avvisi sulle regole del filtro del traffico (programma per i primi utilizzatori) {#traffic-filter-rules-alerts-early-adopter}

Le [Regole del filtro del traffico](/help/security/traffic-filter-rules-including-waf.md) rilasciate di recente, che includono le regole WAF (Web Application Firewall) con licenza facoltativa a parte, permettono di configurare il traffico da consentire o bloccare.

Partecipa al programma di adozione anticipata per ricevere un avviso ogni volta che vengono attivate le regole del filtro del traffico. Le notifiche e-mail del Centro azioni ti informeranno quando si verificano determinate condizioni di traffico, in modo che tu possa adottare le misure appropriate.

#### Gli utenti aziendali possono dichiarare i reindirizzamenti al di fuori di Git (Early Adopter Program) {#apache-rewritemaps-early-adopter}

In modo simile ad AEM 6.5, Apache/dispatcher acquisisce le mappe di riscrittura che si trovano in una posizione specifica nell’archivio di pubblicazione e le carica, senza richiedere l’esecuzione di una pipeline a livello web. Questo offre a un utente aziendale l’opportunità di dichiarare i reindirizzamenti utilizzando un foglio di calcolo o un’interfaccia utente, come quella offerta da ACS Commons Redirect Map Manager o creata come parte di un’applicazione del cliente. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) per il caricamento di contenuti dinamici (programma per i primi utilizzatori) {#esi-early-adopter}

Adobe Managed CDN ora supporta [Inclusioni lato bordo (ESI)](/help/implementing/dispatcher/edge-side-includes.md): linguaggio di markup per l&#39;assembly di contenuti web dinamici a livello di edge. Includendo snippet ESI, è possibile memorizzare nella cache la pagina HTML complessiva sulla rete CDN con valori TTL più elevati, recuperando con maggiore frequenza dall’origine le sezioni più piccole che richiedono aggiornamenti con maggiore frequenza (TTL più bassi). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

#### Servizio dati di Real User Monitoring (RUM) (programma Early Adopter)

* **[Il servizio dati Real Use Monitoring (RUM) è ora GA](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** consentire la raccolta di dati lato client per AEM as a Cloud Service.
Il servizio Real Use Monitoring, la raccolta lato client, offre un riflesso più preciso delle interazioni, garantendo una misura affidabile del coinvolgimento del sito web. Consente ai clienti di ottenere informazioni avanzate sul traffico e sulle prestazioni delle pagine. È un’ottima opportunità per saperne di più sulle prestazioni della pagina e ottenere informazioni per migliorarle.

## Guide di [!DNL Experience Manager] {#guides}

* **Pubblicare un argomento o i relativi elementi in un frammento di esperienza**
Ora, Experience Manager Guides consente di pubblicare un argomento o i relativi elementi in un frammento di esperienza. Un frammento di esperienza è un’unità di contenuto modulare che integra sia il contenuto che il layout.  I frammenti di esperienza sono fondamentali e possono aiutarti a creare esperienze coerenti e coinvolgenti.
* **Possibilità di passare i metadati della risorsa dell’argomento all’output di PDF nativo**
Puoi aggiungere i metadati della risorsa dell’argomento durante la generazione dell’output di PDF nativo. Questa funzione consente di aggiungere metadati specifici per argomenti diversi, come il titolo e l&#39;autore dell&#39;argomento, alle intestazioni e ai piè di pagina dell&#39;argomento.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, vedi [Roadmap sulla versione di Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
