---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 0ef1e1915f2fdbe44cff209851eb43cc9d69958e
workflow-type: tm+mt
source-wordcount: '2261'
ht-degree: 31%

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

La data di rilascio della versione corrente della funzione di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.3.0) è il venerdì 11 aprile 2024. La prossima versione funzionale (2024.4.0) è pianificata per l’venerdì 25 aprile 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- ## Release Video {#release-video}

Have a look at the March 2024 Release Overview video for a summary of the features added in the 2024.3.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] {#sites-features}

**Authoring AEM per Edge Delivery Services**

AEM Sites può ora essere utilizzato come origine di contenuto per i Edge Delivery Services. Gli autori gestiscono i loro siti web in AEM utilizzando il nuovo Editor universale con creazione wysiwyg nel contesto. Questo consente alle aziende di creare pagine web veloci e ad alte prestazioni con Edge Delivery Services sfruttando al contempo le potenti funzionalità AEM per la gestione dei contenuti.

![Authoring di AEM](/help/edge/assets/universal_editor_edge_delivery_services.png)

Per ulteriori informazioni, vedere [documentazione](/help/edge/overview.md) e guarda la [AEM Gems: guida introduttiva all’authoring e ai Edge Delivery Services per l’AEM](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-gems-getting-started-with-aem-authoring-and-edge-delivery/m-p/652694#M43905)

**Editor universale per implementazioni headless**

Universal Editor consente inoltre alle applicazioni web scollegate di sfruttare lo stesso authoring WYSIWYG contestuale intuitivo precedentemente esclusivo per i siti tradizionali. I creatori di contenuti ora possono comporre visivamente layout utilizzando frammenti di contenuto con la stessa facilità con cui compongono i componenti all’interno delle pagine.

Ciò che distingue Universal Editor è la sua adattabilità a diverse architetture web, che supporta sia il rendering lato server che quello lato client, rimanendo indipendente dal framework ed eliminando la necessità di hosting AEM. L’integrazione delle applicazioni web esistenti con Universal Editor per la modifica dei contenuti è semplice e richiede principalmente agli sviluppatori di incorporare attributi di dati specifici nel markup.

In questo modo, Universal Editor garantisce un&#39;esperienza di modifica coerente, indipendentemente dalla struttura del contenuto o dallo stack di tecnologia sottostante. Per ulteriori informazioni, vedere [Introduzione all’editor universale](/help/implementing/universal-editor/introduction.md).

**OpenAPI per la gestione dei contenuti per frammenti di contenuto e modelli**

Gli sviluppatori possono ora interagire a livello di programmazione con i frammenti di contenuto e i modelli di frammenti di contenuto ed eseguire operazioni CruD su di essi utilizzando le API OpenAPI per la gestione dei contenuti. Per ulteriori informazioni, consulta [Documentazione API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)

**Supporto della gestione multisito per frammenti di esperienza**

Il supporto per la gestione multisito è stato esteso alle strutture di cartelle in cui sono memorizzati i frammenti di esperienza, consentendo agli utenti di eseguire il rollout di una struttura di contenuto completa con i frammenti di esperienza.

**Confrontare le versioni dei frammenti di contenuto**

Il nuovo Editor frammento di contenuto ora consente agli autori di contenuto di confrontare e visualizzare le differenze tra la versione corrente di un frammento di contenuto e una versione precedente.

### Programma per i primi utilizzatori {#sites-early-adopter}

**Genera varianti**

Sfruttare GenAI tramite la nuova funzione AEM, [genera varianti](/help/generative-ai/generate-variations.md), accessibile ora nel Cloud Service. Genera varianti consente di generare e scalare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al team del tuo account Adobe per prendere in considerazione il programma.

**Esplorazione delle risorse nella console Frammenti di contenuto**

Gli autori dei contenuti ora possono sfogliare, visualizzare e intervenire sulle immagini e su altre risorse senza dover uscire dalla console Frammenti di contenuto.

![Esplorazione risorse](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Invia un’e-mail a aemcs-headless-adopter@adobe.com dal tuo ID e-mail ufficiale per saperne di più sul programma early adopter.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella vista Amministratore {#admin-view}

**Integrazione nativa con Adobi Express**

AEM Assets si integra in modo nativo con Adobi Express, che consente di accedere direttamente alle risorse memorizzate in AEM Assets dall’interfaccia utente di Adobi Express. Puoi inserire il contenuto gestito in AEM Assets nell’area di lavoro di Express e quindi salvare il contenuto nuovo o modificato in un archivio AEM Assets.

![inclusione delle risorse dal componente aggiuntivo di Assets](/help/assets/assets/adobe-express-native-integration.png)

**Anteprima rappresentazioni per tutti i tipi di video supportati**

Experience Manager Assets ora genera le rappresentazioni in anteprima di tutti i tipi di video supportati per impostazione predefinita senza richiedere una configurazione del profilo di elaborazione.

### Nuove funzioni nella Vista risorse {#assets-view}

**Gestire le autorizzazioni per le raccolte**

Gli Assets Essentials consentono agli amministratori di gestire i livelli di accesso per le raccolte private disponibili nell’archivio. In qualità di amministratore, puoi creare gruppi di utenti e assegnare autorizzazioni a tali gruppi per gestire i livelli di accesso. Puoi anche delegare i privilegi di gestione delle autorizzazioni ai gruppi di utenti.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nuove funzioni di AEM Forms {#forms-new-features}

* **[Edge Delivery Services Adobe Experience Manager Forms](/help/edge/docs/forms/overview.md)**: AEM Forms Edge Delivery Services è un insieme componibile di servizi che consente un ambiente di sviluppo rapido in cui gli autori possono aggiornare, pubblicare e avviare rapidamente nuovi moduli. Questi servizi forniscono esperienze di moduli di eccezionale e forte impatto che determinano coinvolgimento e conversioni. Queste esperienze di moduli sono facili da creare e sviluppare.

  ![Funzioni di EDS Forms](/help/edge/assets/eds-forms-features.png)

Questi servizi consentono di:

* Utilizzare più origini di contenuto nello stesso sito moduli e utilizzare gli strumenti di authoring preferiti, ad esempio Microsoft Excel, Google Sheets o Adaptive Forms Editor.
* Fornisci esperienze di registrazione digitale che consentono di caricare ed eseguire il rendering in modo rapido e continuo monitorando le prestazioni dei moduli tramite il monitoraggio degli utenti reali (RUM, Real User Monitoring).
* Utilizza plain HTML, CSS moderno e JavaScript vanilla per creare esperienze eccezionali, evitando la curva di apprendimento ripida di un framework specifico.


### Nuove funzioni nella versione prerelease di AEM Forms {#forms-pre-release}

* **Editor di regole visive ottimizzato per Forms adattivo basato su componenti core**: questa versione apporta un aggiornamento significativo all’editor di regole visive per i moduli adattivi basati su componenti core. Questa versione apporta un aggiornamento significativo all’editor di regole visive per i moduli adattivi basati su componenti core. Questo aggiornamento si concentra sulla semplificazione delle interazioni con le funzioni personalizzate, consentendo di creare moduli più solidi ed efficienti.

  Ora puoi semplificare le interazioni delle funzioni personalizzate:

   * Utilizzo di nuove annotazioni per fornire definizioni più chiare delle funzioni.
   * Utilizzo di meccanismi di caching per le funzioni personalizzate, per prestazioni di modulo più veloci.
   * Lavora senza problemi con gli oggetti globali nelle funzioni personalizzate.
   * Definizione e utilizzo di parametri facoltativi nelle funzioni personalizzate.

  Questo aggiornamento apporta anche i seguenti miglioramenti alla funzionalità dell’editor di regole. Operazioni disponibili:

   * Implementa una potente logica &quot;when-then-else&quot; per l’esecuzione condizionale.
   * Sfrutta le moderne funzioni JavaScript come le funzioni let e arrow (supporto ES10).
   * Convalida o reimposta non solo i campi, ma anche interi pannelli e moduli, espandendo il controllo sulle interazioni degli utenti.

  Questi miglioramenti forniscono un’esperienza più intuitiva e potente per la creazione di regole e funzioni personalizzate all’interno dell’editor di regole visive.

* **Creare più versioni di un modulo adattivo**: ora è possibile gestire facilmente le varianti dei moduli esistenti. Questo semplifica il controllo delle versioni e facilita il confronto per l’ottimizzazione dei moduli, il tutto all’interno di un unico flusso di lavoro semplificato.

* **Confronta modulo adattivo**: ora è possibile confrontare facilmente due moduli per identificare le differenze tra due moduli. Semplifica la collaborazione consentendo ai membri del gruppo di confrontare le revisioni e discutere le modifiche in modo efficiente.

* **Miglioramenti all’accessibilità per il componente Firma a mano**: questo aggiornamento apporta significativi miglioramenti di accessibilità al componente Firma a mano:

  **Miglioramento della navigazione tramite tastiera:**
   * Premendo il tasto TAB, gli utenti possono spostarsi tra tutti gli elementi interattivi all&#39;interno della finestra di dialogo della firma.
   * La firma con un pennello o una tastiera e la pressione di Invio chiudono la finestra di dialogo.
   * Lo stato attivo rimane sul controllo della firma dopo aver firmato e fatto clic su &quot;OK&quot;.

  **Funzionalità Clear Signature:**

   * Un&#39;icona a forma di croce deselezionata per cancellare la firma è accessibile tramite il tasto TAB.
   * La finestra di dialogo &quot;Clear Signature Confirmation&quot; (Cancella conferma firma) è accessibile anche tramite la navigazione tramite scheda.

  **Etichette e controlli migliorati:**
   * L’etichetta per il pulsante di firma della tastiera è ora più chiara, utilizzando &quot;aria-label&quot; per annunciare le funzionalità (come &quot;aria-label=’Sign using Keyboard’&quot;).
   * Il contrasto migliorato garantisce che tutti i controlli all&#39;interno della firma a mano siano facilmente distinguibili.
   * Il pulsante OK/segno di spunta ora indica visivamente quando è inattivo.

  **Feedback sulla firma per Reader di schermate:**
   * Quando viene digitata una firma, gli utenti che utilizzano un assistente vocale possono ascoltare il testo utilizzato per creare la firma.

Questo aggiornamento garantisce un’esperienza più inclusiva per gli utenti con disabilità, migliorando la navigazione, la chiarezza e il feedback per il componente Firma scarabocchio.

### Programma per i primi utilizzatori {#forms-early-adopter}

* **[Inviare un modulo adattivo allo scenario Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service offre un’opzione preconfigurata per collegare facilmente un modulo adattivo ad Adobe Workfront. Questo semplifica il processo di invio di un modulo adattivo a uno scenario di Adobe Workfront, consentendoti di attivare uno scenario Workfront Fusion all’invio di un modulo adattivo.

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> Utilizzando il connettore Adobe Workfront Fusion, puoi progettare flussi di lavoro che vengono attivati automaticamente al momento dell’invio di un modulo adattivo. Ad esempio, immagina uno scenario in cui viene avviato un flusso di lavoro per assegnare a un individuo specifico il compito di rivedere i dati inviati, consentendo l’approvazione o il rifiuto di una domanda in base alle informazioni acquisite tramite il modulo adattivo. Questa integrazione semplificata migliora l&#39;efficienza e introduce un nuovo livello di automazione nei processi del flusso di lavoro.|

* **Servizio di estensione Reader**: le API di comunicazione di AEM Forms hanno introdotto il servizio di estensione di Reader per consentire di aggiungere funzionalità come la compilazione di moduli e commenti ai PDF standard, rendendoli interattivi per gli utenti con l’Adobe Reader gratuito.

* [Supporto lingue da destra a sinistra](/help/forms/supporting-new-language-localization-core-components.md): i moduli adattivi basati sui Componenti core ora possono essere presentati in una lingua da destra a sinistra (RTL) come l’arabo, il persiano e l’urdu. Le lingue RTL sono parlate da oltre 2 miliardi di persone in tutto il mondo. L’utilizzo di un modulo in linguaggio RTL consente di estendere la portata dei moduli adattivi in modo da soddisfare questi diversi tipi di pubblico e selezionarli in mercati RTL. In alcune aree geografiche, fornire moduli nella lingua locale, è anche obbligatorio dal punto di vista legale. Adattandosi alle lingue locali, non solo si aprono le porte a un pubblico più ampio, ma si garantisce anche la conformità con le leggi e i regolamenti pertinenti.

* **[Proteggere i documenti con le API DocAssurance (parte di API Communication)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Per partecipare al programma per i primi utilizzatori e richiedere l’accesso alla funzionalità, è possibile inviare una e-mail all’indirizzo `aem-forms-ea@adobe.com` dal proprio ID e-mail ufficiale.

* **[Puoi sfruttare il Servizio dati del Monitoraggio degli utenti reali (RUM)](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** per abilitare la raccolta lato client per AEM as a Cloud Service.
Il servizio dati del monitoraggio utenti reali (RUM) offre una panoramica più precisa delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web. Rappresenta un’ottima opportunità per ottenere informazioni avanzate sulle prestazioni della pagina. Questa funzione è utile per chi utilizza una rete CDN gestita o non gestita da Adobe. Inoltre, per chi utilizza una rete CDN non gestita da Adobe, ora è possibile abilitare il reporting automatico del traffico, eliminando in tal modo la necessità di condividere eventuali rapporti sul traffico con Adobe.

  Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un’e-mail a `aemcs-rum-adopter@adobe.com`, insieme al nome di dominio per ciascuno degli ambienti per i quali desideri abilitare il monitoraggio degli utenti reali (RUM) dall’indirizzo e-mail associato al tuo Adobe ID. Il team di prodotto di Adobe abiliterà quindi il servizio dati del Monitoraggio degli utenti reali (RUM).

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Programmi di adozione anticipata {#foundation-early-adopter}

#### Avvisi sulle regole del filtro del traffico (programma di adozione anticipata) {#traffic-filter-rules-alerts-early-adopter}

Il rilasciato di recente [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md), che includono le regole WAF (Web Application Firewall) facoltativamente consentite, consente di configurare il traffico da consentire o negare.

Ora puoi inviare un’e-mail **<aemcs-cdn-config-adopter@adobe.com>** per partecipare al programma early adopter in modo da poter essere avvisati ogni volta che vengono attivate le regole del filtro del traffico. Le notifiche e-mail del Centro operativo ti terranno informato quando si verificano determinate condizioni di traffico, in modo da poter adottare le misure appropriate.

#### Configurazione CDN (Early Adopter Program) {#cdn-config-early-adopter}

Oltre agli ultimi [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md), che includono le regole WAF (Web Application Firewall) facoltative, è possibile utilizzare la pipeline di configurazione per dichiarare e distribuire altri tipi di configurazione CDN. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-configuring-traffic.md) e partecipa al programma early adopter inviando un&#39;e-mail **<aemcs-cdn-config-adopter@adobe.com>** per accedere a:

* 301/302 reindirizzamenti lato client
* proxy delle richieste edge a origini arbitrarie (ad esempio applicazioni non AEM)
* trasformazioni URL
* impostazione o modifica delle intestazioni di risposta o richiesta
* pagine di errore personalizzate quando la rete CDN non può raggiungere AEM

#### Acquisizione runtime Apache/Dispatcher di mappe di riscrittura (programma Early Adopter) {#apache-rewritemaps-early-adopter}

Simile a AEM 6.5, Apache/dispatcher acquisisce le mappe di riscrittura posizionate in una posizione specifica nell’archivio di pubblicazione e le carica, senza richiedere l’esecuzione di una pipeline a livello web. Questo offre a un utente aziendale l’opportunità di dichiarare i reindirizzamenti utilizzando un’interfaccia utente, come quella offerta da ACS Commons Redirect Map Manager. Rivolgiti a **<aemcs-cdn-config-adopter@adobe.com>** per ulteriori informazioni.

#### Edge Side include (ESI) per il caricamento di contenuti dinamici (Early Adopter Program) {#esi-early-adopter}

Adobe Managed CDN ora supporta Edge Side Includes (ESI), un linguaggio di markup per l’assembly di contenuti web dinamici a livello di edge. Includendo snippet ESI, è possibile memorizzare nella cache la pagina HTML complessiva sulla rete CDN con valori TTL più elevati, recuperando con maggiore frequenza dall’origine le sezioni più piccole che richiedono aggiornamenti con maggiore frequenza (TTL più bassi). Rivolgiti a **<aemcs-cdn-config-adopter@adobe.com>** per ulteriori informazioni.

#### Supporto RDE per codice front-end tramite temi del sito e modelli del sito (programma Early Adopter) {#rde-frontend-early-adopter}

Gli [ambienti di sviluppo rapido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) ora supportano il codice front-end basato su [temi del sito](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelli di sito](/help/sites-cloud/administering/site-creation/site-templates.md), per i primi utilizzatori. Con gli RDE, questa operazione viene eseguita utilizzando una direttiva della riga di comando, anziché una [pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Rivolgiti a **<aemcs-rde-support@adobe.com>** per provarlo e fornire feedback.

#### Registrazione avanzata per gli RDE (Early Adopter Program) {#rde-logging-early-adopter}

Durante il debug del codice in una [Ambiente di sviluppo rapido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md), gli sviluppatori possono ora configurare e inviare i registri in modo più efficiente, utilizzando la riga di comando e senza modificare le proprietà OSGI nel controllo della versione. Le caratteristiche includono:

* dichiarare i livelli di registro a livello di pacchetto o classe
* personalizzare il formato di output del registro
* eseguire lo streaming di più registri in parallelo

Rivolgiti a **<aemcs-rde-support@adobe.com>** per provarlo e fornire feedback.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
