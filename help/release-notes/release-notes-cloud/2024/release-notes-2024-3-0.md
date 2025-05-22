---
title: Note sulla versione 2024.3.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2024.3.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: b3816929-2c0a-4d6a-b583-c928d2182ecd
feature: Release Information
role: Admin
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: tm+mt
source-wordcount: '2283'
ht-degree: 93%

---

# Note sulla versione 2024.3.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2024.3.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente della funzione di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.3.0) è l’11 aprile 2024. La prossima versione funzionale (2024.4.0) è pianificata per il 25 aprile 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video che mostra una panoramica sulla versione di marzo 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.3.0:

>[!VIDEO](https://video.tv.adobe.com/v/3450367?quality=12&captions=ita)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] {#sites-features}

**Authoring di AEM per Edge Delivery Services**

AEM Sites può ora essere utilizzato come origine di contenuto per Edge Delivery Services. Gli autori gestiscono i propri siti web in AEM utilizzando il nuovo editor universale con authoring wysiwyg contestuale. Questo consente alle aziende di creare pagine web veloci e ad alte prestazioni con Edge Delivery Services sfruttando al contempo le potenti funzionalità AEM per la gestione dei contenuti.

![Authoring di AEM](/help/edge/assets/universal_editor_edge_delivery_services.png)

Per ulteriori informazioni, consulta la [documentazione](/help/edge/overview.md) e guarda [AEM Gems: guida introduttiva all’authoring di AEM e Edge Delivery Services](https://experienceleaguecommunities.adobe.com/it/t5/adobe-experience-manager/aem-gems-getting-started-with-aem-authoring-and-edge-delivery/m-p/652694#M43905)

**Editor universale per implementazioni headless**

L’editor universale consente inoltre alle applicazioni web separate di sfruttare lo stesso authoring WYSIWYG contestuale intuitivo precedentemente esclusivo per i siti tradizionali. I creatori di contenuti ora possono comporre visivamente layout utilizzando frammenti di contenuto con la stessa facilità con cui compongono i componenti all’interno delle pagine.

Ciò che contraddistingue l’editor universale è la sua adattabilità a diverse architetture web, supportando sia il rendering lato client che quello lato server, rimanendo indipendente dal framework ed eliminando la necessità di hosting AEM. L’integrazione delle applicazioni web esistenti con l’editor universale per la modifica dei contenuti è semplice e richiede principalmente agli sviluppatori di incorporare attributi di dati specifici nel markup.

In questo modo, l’editor universale garantisce un’esperienza di modifica coerente, indipendentemente dalla struttura del contenuto o dallo stack tecnologico sottostante. Per ulteriori informazioni, consulta l’[Introduzione all’editor universale](/help/implementing/universal-editor/introduction.md).

**OpenAPI per la gestione dei contenuti per modelli e frammenti di contenuto**

Gli sviluppatori possono ora interagire a livello di programmazione con i frammenti di contenuto e i modelli di frammenti di contenuto ed eseguire operazioni CruD su di essi utilizzando le OpenAPI per la gestione dei contenuti. Per ulteriori informazioni, consulta la [documentazione dell’API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)

**Supporto alla gestione multisito per frammenti di esperienza**

Il supporto per la gestione multisito è stato esteso alle strutture di cartelle in cui sono memorizzati i frammenti di esperienza, consentendo agli utenti di eseguire il rollout di una struttura di contenuto completa di frammenti di esperienza.

**Confrontare le versioni dei frammenti di contenuto**

Il nuovo Editor frammento di contenuto ora consente agli autori di contenuti di confrontare e visualizzare le differenze tra la versione corrente di un frammento di contenuto e una versione precedente.

### Programma per i primi utilizzatori {#sites-early-adopter}

**Generare varianti**

Sfruttare l’intelligenza artificiale generativa tramite la nuova funzione di AEM, [genera varianti](/help/generative-ai/generate-variations.md), ora accessibile in Cloud Service. Genera varianti consente di generare e ridimensionare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al tuo team Adobe Account per prendere in considerazione il programma.

**Esplorazione delle risorse nella console Frammenti di contenuto**

Gli autori dei contenuti ora possono esplorare, visualizzare e intervenire sulle immagini e su altre risorse senza dover uscire dalla console Frammenti di contenuto.

![Esplorazione delle risorse](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Per ulteriori informazioni sul programma per i primi utilizzatori, invia un’e-mail all’indirizzo aemcs-headless-adopter@adobe.com dal tuo ID e-mail ufficiale.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella vista Amministratore {#admin-view}

**Integrazione nativa con Adobe Express**

AEM Assets si integra in modo nativo con Adobe Express, che dalla sua interfaccia utente ti consente di accedere direttamente alle risorse memorizzate in AEM Assets. Il contenuto gestito in AEM Assets può essere inserito nell’area di lavoro di Express e il contenuto nuovo o modificato salvato in un archivio AEM Assets.

![Inclusione delle risorse dal componente aggiuntivo di Assets](/help/assets/assets/adobe-express-native-integration.png)

**Anteprima rappresentazioni per tutti i tipi di video supportati**

Experience Manager Assets ora genera le rappresentazioni in anteprima di tutti i tipi di video supportati per impostazione predefinita senza richiedere una configurazione del profilo di elaborazione.

### Nuove funzioni nella Vista risorse {#assets-view}

**Gestione delle autorizzazioni per le raccolte**

Assets Essentials consente agli amministratori di gestire i livelli di accesso per le raccolte private disponibili nell’archivio. In qualità di amministratore, puoi creare gruppi di utenti e assegnare autorizzazioni a tali gruppi per gestire i livelli di accesso. Puoi anche delegare i privilegi di gestione delle autorizzazioni ai gruppi di utenti.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nuove funzioni di AEM Forms {#forms-new-features}

* **[Adobe Experience Manager Forms Edge Delivery Services](/help/edge/docs/forms/overview.md)**: Edge Delivery Services per AEM Forms è un insieme componibile di servizi che consente un ambiente di sviluppo rapido in cui gli autori possono aggiornare, pubblicare e avviare rapidamente nuovi moduli. Questi servizi forniscono esperienze di moduli di eccezionale e forte impatto che determinano coinvolgimento e conversioni. Queste esperienze di moduli sono facili da creare e sviluppare.

  ![Funzioni di EDS Forms](/help/edge/assets/eds-forms-features.png)

Questi servizi consentono di:

* Utilizza più origini di contenuto nello stesso sito moduli con i tuoi strumenti di authoring preferiti, ad esempio Microsoft Excel, Fogli Google o Editor di moduli adattivi.
* Fornisci esperienze di registrazione digitale che consentono di caricare ed eseguire il rendering in modo rapido e continuo monitorando le prestazioni dei moduli tramite la telemetria operativa.
* Utilizza il semplice HTML, CSS moderno e JavaScript vanilla per creare esperienze eccezionali, evitando la difficile curva di apprendimento di un framework specifico.


### Nuove funzioni nella versione prerelease di AEM Forms {#forms-pre-release}

* **Editor di regole visive ottimizzato per Forms adattivo basato su componenti core**: questa versione apporta un aggiornamento significativo all’editor di regole visive per i moduli adattivi basati su componenti core. Questa versione apporta un aggiornamento significativo all’editor di regole visive per i moduli adattivi basati su componenti core. Questo aggiornamento si concentra sulla semplificazione delle interazioni con le funzioni personalizzate, consentendo di creare moduli più solidi ed efficienti.

  Ora puoi semplificare le interazioni delle funzioni personalizzate:

   * Sfruttando le nuove annotazioni per fornire definizioni più chiare delle funzioni.
   * Utilizzando meccanismi di caching per le funzioni personalizzate, per prestazioni di modulo più veloci.
   * Lavorando in modo semplice con gli oggetti globali nelle funzioni personalizzate.
   * Definendo e utilizzando parametri facoltativi nelle funzioni personalizzate.

  Questo aggiornamento apporta anche i seguenti miglioramenti alla funzionalità dell’editor di regole. Operazioni disponibili:

   * Implementazione di una potente logica &quot;when-then-else&quot; per l’esecuzione condizionale.
   * Sfruttamento delle moderne funzioni JavaScript come let e arrow (supporto ES10).
   * Convalida o reimpostazione non solo di campi, ma anche di interi pannelli e moduli, espandendo il controllo sulle interazioni degli utenti.

  Questi miglioramenti forniscono un’esperienza più intuitiva e potente per la creazione di regole e funzioni personalizzate all’interno dell’editor di regole visive.

* **Crea più versioni di un modulo adattivo**: ora è possibile gestire facilmente le varianti dei moduli esistenti. Questo semplifica il controllo delle versioni e facilita il confronto per l’ottimizzazione dei moduli, il tutto all’interno di un unico flusso di lavoro semplificato.

* **Confronta moduli adattivi**: ora è possibile confrontare facilmente due moduli e identificarne le differenze. Questo semplifica la collaborazione consentendo ai membri del gruppo di confrontare le revisioni e discutere le modifiche in modo efficiente.

* **Miglioramenti di accessibilità per il componente Firma scarabocchio**: questo aggiornamento apporta significativi miglioramenti di accessibilità al componente Firma scarabocchio:

  **Miglioramento della navigazione tramite tastiera:**
   * Premendo il tasto TAB, gli utenti possono spostarsi tra tutti gli elementi interattivi all’interno della finestra di dialogo della firma.
   * La firma con un pennello o da tastiera e la pressione di Invio chiudono la finestra di dialogo.
   * Lo stato attivo rimane sul controllo della firma dopo aver firmato e fatto clic su “OK”.

  **Funzionalità Cancellazione firma:**

   * Un’icona a forma di croce deselezionata per cancellare la firma è accessibile tramite il tasto TAB.
   * La finestra di dialogo “Conferma cancellazione firma” è accessibile anche tramite la navigazione tramite TAB.

  **Etichette e controlli migliorati:**
   * L’etichetta per il pulsante di firma della tastiera è ora più chiara, utilizzando “aria-label” per annunciare le funzionalità (come “aria-label=&#39;Sign using Keyboard&#39;”).
   * Il contrasto migliorato garantisce che tutti i controlli all’interno della firma scarabocchio siano facilmente distinguibili.
   * Il pulsante OK/segno di spunta ora indica visivamente quando è inattivo.

  **Feedback sulla firma per assistenti vocali:**
   * Quando viene digitata una firma, gli utenti che utilizzano un assistente vocale possono ascoltare il testo utilizzato per creare la firma.

Questo aggiornamento garantisce un’esperienza più inclusiva per gli utenti con disabilità, migliorando la navigazione, la chiarezza e il feedback per il componente Firma scarabocchio.

### Programma per i primi utilizzatori {#forms-early-adopter}

* **[Invia un modulo adattivo ad Adobe Workfront Fusion Scenario](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service offre un’opzione pronta all’uso per collegare facilmente un modulo adattivo ad Adobe Workfront. Questo semplifica il processo di invio di un modulo adattivo a uno scenario di Adobe Workfront, consentendoti di attivare uno scenario Workfront Fusion all’invio di un modulo adattivo.

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> Utilizzando il connettore Adobe Workfront Fusion, puoi progettare flussi di lavoro che vengono attivati automaticamente al momento dell’invio di un modulo adattivo. Ad esempio, immagina uno scenario in cui viene avviato un flusso di lavoro per assegnare a un individuo specifico il compito di rivedere i dati inviati, consentendo l’approvazione o il rifiuto di una richiesta in base alle informazioni acquisite tramite il modulo adattivo. Questa integrazione semplificata migliora l’efficienza e introduce un nuovo livello di automazione nei processi del flusso di lavoro.|

* **Servizio di estensione Reader**: le API di comunicazione di AEM Forms fanno in modo che il servizio di estensione Reader consenta di aggiungere funzionalità come la compilazione di moduli e commenti ai PDF standard, rendendoli interattivi per gli utenti con Adobe Reader gratuito.

* [Supporto lingue da destra a sinistra](/help/forms/supporting-new-language-localization-core-components.md): i moduli adattivi basati sui Componenti core ora possono essere presentati in una lingua da destra a sinistra (RTL) come l’arabo, il persiano e l’urdu. Le lingue RTL sono parlate da oltre 2 miliardi di persone in tutto il mondo. L’utilizzo di un modulo in linguaggio RTL consente di estendere la portata dei moduli adattivi in modo da soddisfare questi diversi tipi di pubblico e selezionarli in mercati RTL. In alcune aree geografiche, fornire moduli nella lingua locale, è anche obbligatorio dal punto di vista legale. Adattandosi alle lingue locali, non solo si aprono le porte a un pubblico più ampio, ma si garantisce anche la conformità con le leggi e i regolamenti pertinenti.

* **[Proteggere i documenti con le API DocAssurance (parte di API Communication)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Per partecipare al programma per i primi utilizzatori e richiedere l’accesso alla funzionalità, è possibile inviare una e-mail all’indirizzo `aem-forms-ea@adobe.com` dal proprio ID e-mail ufficiale.

* **[Puoi sfruttare il servizio di telemetria operativa](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** per abilitare la raccolta lato client per AEM as a Cloud Service.
Il servizio di telemetria operativa offre una riflessione più precisa delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web. Rappresenta un’ottima opportunità per ottenere informazioni avanzate sulle prestazioni della pagina. Questa funzione è utile per chi utilizza una rete CDN gestita o non gestita da Adobe. Inoltre, per chi utilizza una rete CDN non gestita da Adobe, ora è possibile abilitare il reporting automatico del traffico, eliminando in tal modo la necessità di condividere eventuali rapporti sul traffico con Adobe.

  Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un&#39;e-mail a `aemcs-rum-adopter@adobe.com` insieme al tuo nome di dominio per ciascuno degli ambienti per i quali vuoi abilitare la telemetria operativa dal tuo indirizzo e-mail associato al tuo Adobe ID. Il team di prodotto di Adobe abiliterà quindi il servizio di telemetria operativa.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Programma per i primi utilizzatori {#foundation-early-adopter}

#### Avvisi sulle regole del filtro del traffico (programma per i primi utilizzatori) {#traffic-filter-rules-alerts-early-adopter}

Le [Regole del filtro del traffico](/help/security/traffic-filter-rules-including-waf.md) rilasciate di recente, che includono le regole WAF (Web Application Firewall) con licenza facoltativa a parte, permettono di configurare il traffico da consentire o bloccare.

Ora puoi inviare un’e-mail **<aemcs-cdn-config-adopter@adobe.com>** per partecipare al programma per i primi utilizzatori in modo da poter ricevere un avviso ogni volta che vengono attivate le tue regole del filtro del traffico. Le notifiche e-mail del Centro azioni ti informeranno quando si verificano determinate condizioni di traffico, in modo che tu possa adottare le misure appropriate.

#### Mappatura del dominio (programma Early Adopter) {#cdn-config-early-adopter}

Oltre alle [Regole del filtro del traffico](/help/security/traffic-filter-rules-including-waf.md) rilasciate di recente, che includono le regole WAF (Web Application Firewall) con licenza facoltativa, esiste l’opportunità di utilizzare la pipeline di configurazione per specificare e distribuire altri tipi di configurazione CDN. Consulta [ulteriori informazioni](/help/implementing/dispatcher/cdn-configuring-traffic.md) e partecipa al programma per i primi utilizzatori inviando un’e-mail a **<aemcs-cdn-config-adopter@adobe.com>** per ottenere l’accesso a:

* Reindirizzamenti lato server 301/302
* proxy di richieste al server Edge di origini arbitrarie (ad esempio applicazioni non AEM)
* trasformazioni URL
* impostazione o modifica delle intestazioni di risposta o richiesta
* pagine di errore personalizzate quando la rete CDN non può raggiungere AEM

#### Acquisizione runtime Apache/Dispatcher di mappe di riscrittura (programma per i primi utilizzatori) {#apache-rewritemaps-early-adopter}

In modo simile ad AEM 6.5, Apache/dispatcher acquisisce le mappe di riscrittura che si trovano in una posizione specifica nell’archivio di pubblicazione e le carica, senza richiedere l’esecuzione di una pipeline a livello web. Questo offre a un utente aziendale l’opportunità di dichiarare i reindirizzamenti utilizzando un’interfaccia utente, come quella offerta da ACS Commons Redirect Map Manager. Rivolgiti a **<aemcs-cdn-config-adopter@adobe.com>** per ulteriori informazioni.

#### Edge Side Includes (ESI) per il caricamento di contenuti dinamici (programma per i primi utilizzatori) {#esi-early-adopter}

Adobe Managed CDN ora supporta Edge Side Includes (ESI), un linguaggio di markup per l’assemblaggio di contenuti web dinamici a livello di edge. Includendo snippet ESI, è possibile memorizzare nella cache la pagina HTML generale sulla rete CDN con valori TTL più elevati e recuperare con maggiore frequenza dall’origine le sezioni più piccole che richiedono aggiornamenti più frequenti (TTL più bassi). Per ulteriori informazioni, invia un’email all’indirizzo **<aemcs-cdn-config-adopter@adobe.com>**.

#### Supporto RDE per il codice front-end tramite i temi e i modelli del sito: programma per i primi utilizzatori (Early Adopter Program) {#rde-frontend-early-adopter}

Gli [ambienti di sviluppo rapido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) ora supportano il codice front-end basato su [temi del sito](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelli di sito](/help/sites-cloud/administering/site-creation/site-templates.md), per i primi utilizzatori. Con gli RDE, questa operazione viene eseguita utilizzando una direttiva della riga di comando, anziché una [pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Invia un’email all’indirizzo **<aemcs-rde-support@adobe.com>** per provarlo e fornire un feedback.

#### Registrazione avanzata per gli RDE (Ambienti di sviluppo rapidi) {#rde-logging-early-adopter}

Durante il debug del codice in un’[Ambiente di sviluppo rapido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md), gli sviluppatori possono ora configurare e inviare i registri in modo più efficiente, utilizzando la riga di comando e senza modificare le proprietà OSGI nel controllo della versione. Le funzioni includono:

* dichiarazione dei livelli di registro a livello di pacchetto o classe
* personalizzazione del formato di output del registro
* esecuzione dello streaming di più registri in parallelo

Invia un’email all’indirizzo **<aemcs-rde-support@adobe.com>** per provarlo e fornire un feedback.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
