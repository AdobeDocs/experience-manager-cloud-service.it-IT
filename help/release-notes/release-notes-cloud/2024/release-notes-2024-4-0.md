---
title: Note sulla versione 2024.4.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2024.4.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 153a3172-676f-4434-94d4-12fab8e17734
feature: Release Information
role: Admin
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '2689'
ht-degree: 95%

---

# Note sulla versione 2024.4.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2024.4.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente della funzione di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.4.0) è il 25 aprile 2024. La prossima versione funzionale (2024.5.0) è pianificata per il 30 maggio 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di aprile 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3446317?quality=12&captions=ita)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programma per i primi utilizzatori {#sites-early-adopter}

**Generare varianti**

Sfruttare l’intelligenza artificiale generativa tramite la nuova funzione di AEM, [genera varianti](/help/generative-ai/generate-variations.md), ora accessibile in Cloud Service. Genera varianti consente di generare e ridimensionare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al tuo team Adobe Account per prendere in considerazione il programma.

**Esplorazione delle risorse nella console Frammenti di contenuto**

Gli autori dei contenuti ora possono esplorare, visualizzare e intervenire sulle immagini e su altre risorse senza dover uscire dalla console Frammenti di contenuto.

![Esplorazione delle risorse](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Per ulteriori informazioni sul programma per i primi utilizzatori, invia un’e-mail all’indirizzo aemcs-headless-adopter@adobe.com dal tuo ID e-mail ufficiale.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella Vista risorse {#assets-view-new-features}


**Ricerca contestuale**

Ora puoi anche [cercare le risorse disponibili nell’archivio definendo i prompt di testo](/help/assets/search-assets-view.md#contextual-search). Experience Manager Assets trasforma automaticamente i prompt di testo in filtri di ricerca e visualizza i risultati della ricerca. È possibile visualizzare e modificare i filtri automatici utilizzando il riquadro Filtri per limitare ulteriormente i risultati della ricerca.

![Ricerca contestuale](/help/assets/assets/contextual-search-text-prompt1.png)

**Azioni rapide per video Express**

Experience Manager Assets ora include [strumenti di editing video semplici e intuitivi basati su Adobe Express](/help/assets/edit-videos-assets-view.md) per aumentare il riutilizzo dei contenuti e accelerarne la velocità. Le opzioni di modifica includono il taglio, il ritaglio, il ridimensionamento di un video e anche la conversione di un file MP4 in GIF.

![ritagliare video con Adobe Express](/help/assets/assets/adobe-express-crop-video.png)

**Rappresentazioni dinamiche**

Ora puoi [visualizzare e scaricare le rappresentazioni dinamiche (inclusi i ritagli avanzati)](/help/assets/renditions.md) in Experience Manager Assets. Le rappresentazioni dinamiche sono versioni personalizzate delle risorse di immagini create in tempo reale per soddisfare esigenze specifiche, ad esempio per ridimensionare le immagini in base alla risoluzione del dispositivo o per adattarle a proporzioni diverse. Queste rappresentazioni consentono alle organizzazioni di fornire esperienze personalizzate e ottimizzate per soddisfare le diverse esigenze del pubblico.

![Rappresentazioni dinamiche](/help/assets/assets/preset_smart_crop.png)

**Ridenominazione diretta di risorse e cartelle**

Experience Manager Assets ora offre un’esperienza utente semplificata grazie alla [possibilità di rinominare una risorsa o una cartella tramite un singolo clic](/help/assets/manage-organize-assets-view.md).

**Assegnare o rimuovere il modulo metadati in più cartelle**

Ora puoi [assegnare o rimuovere il modulo metadati in più cartelle](/help/assets/metadata-assets-view.md#assign-metadata-form-to-a-folder).

### Nuove funzioni nella vista Amministratore {#admin-view-new-features}

**Configurazione della condivisione di collegamenti**

Una nuova esperienza utente migliorata per [creare condivisioni di collegamenti](/help/assets/share-assets.md) e un nuovo set di configurazioni consentono agli amministratori di personalizzare il comportamento predefinito di questa funzionalità per gli utenti.

![Configurazione condivisione collegamenti](/help/assets/assets/config-email-service.png)



## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nuove funzioni in AEM Forms {#forms-new-features}

* **Editor di regole visive ottimizzato per Forms adattivo basato su componenti core**: questa versione apporta un aggiornamento significativo all’editor di regole visive per i moduli adattivi basati su componenti core. Questa versione apporta un aggiornamento significativo all’editor di regole visive per i moduli adattivi basati su componenti core. Questo aggiornamento si concentra sulla semplificazione delle interazioni con le funzioni personalizzate, consentendo di creare moduli più solidi ed efficienti.

  Ora puoi semplificare le interazioni delle funzioni personalizzate:

   * [Sfruttando le nuove annotazioni per fornire definizioni più chiare delle funzioni](/help/forms/create-and-use-custom-functions.md#supported-javascript-annotations-for-custom-function).
   * [Utilizzando meccanismi di caching per le funzioni personalizzate, per prestazioni dei moduli più veloci](/help/forms/create-and-use-custom-functions.md#caching-support-for-custom-function).
   * [Lavorando in modo semplice con oggetti globali nelle funzioni personalizzate.](/help/forms/create-and-use-custom-functions.md#field-and-global-scope-objects-in-custom-functions)
   * [Definendo e utilizzando parametri facoltativi nelle funzioni personalizzate](/help/forms/create-and-use-custom-functions.md#parameter).

  Questo aggiornamento apporta anche i seguenti miglioramenti alla funzionalità dell’editor di regole. Operazioni disponibili:

   * Implementazione di una potente logica [“when-then-else”](/help/forms/rule-editor-core-components.md#when) per l’esecuzione condizionale.
   * Sfruttamento delle moderne funzioni JavaScript come let e arrow (supporto ES10).
   * Convalida o reimpostazione non solo di campi, ma anche di interi pannelli e moduli, espandendo il controllo sulle interazioni degli utenti.

  Questi miglioramenti forniscono un’esperienza più intuitiva e potente per la creazione di regole e funzioni personalizzate all’interno dell’editor di regole visive.

* **[Crea più versioni di un modulo adattivo](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)**: ora è possibile gestire facilmente le varianti dei moduli esistenti. Questo semplifica il controllo delle versioni e facilita il confronto per l’ottimizzazione dei moduli, il tutto all’interno di un unico flusso di lavoro semplificato.

* **[Confronta moduli adattivi](/help/forms/compare-forms.md)**: ora è possibile confrontare facilmente due moduli e identificarne le differenze. Questo semplifica la collaborazione consentendo ai membri del gruppo di confrontare le revisioni e discutere le modifiche in modo efficiente.

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

* **[Servizio di estensione Reader](/help/forms/aem-forms-cloud-service-communications-introduction.md#reader-extension-service)**: le API di comunicazione di AEM Forms fanno in modo che il servizio di estensione Reader consenta di aggiungere funzionalità come la compilazione di moduli e commenti ai PDF standard, rendendoli interattivi per gli utenti con Adobe Reader gratuito.

* [Supporto lingue da destra a sinistra](/help/forms/supporting-new-language-localization-core-components.md): i moduli adattivi basati sui Componenti core ora possono essere presentati in una lingua da destra a sinistra (RTL) come l’arabo, il persiano e l’urdu. Le lingue RTL sono parlate da oltre 2 miliardi di persone in tutto il mondo. L’utilizzo di un modulo in linguaggio RTL consente di estendere la portata dei moduli adattivi in modo da soddisfare questi diversi tipi di pubblico e selezionarli in mercati RTL. In alcune aree geografiche, fornire moduli nella lingua locale, è anche obbligatorio dal punto di vista legale. Adattandosi alle lingue locali, non solo si aprono le porte a un pubblico più ampio, ma si garantisce anche la conformità con le leggi e i regolamenti pertinenti.

* **[Proteggere i documenti con le API DocAssurance (parte di API Communication)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Per partecipare al programma per i primi utilizzatori e richiedere l’accesso alla funzionalità, è possibile inviare una e-mail all’indirizzo `aem-forms-ea@adobe.com` dal proprio ID e-mail ufficiale.

* **[Puoi sfruttare il servizio di telemetria operativa](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** per abilitare la raccolta lato client per AEM as a Cloud Service.
Il servizio di telemetria operativa offre una riflessione più precisa delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web. Rappresenta un’ottima opportunità per ottenere informazioni avanzate sulle prestazioni della pagina. Questa funzione è utile per chi utilizza una rete CDN gestita o non gestita da Adobe. Inoltre, per chi utilizza una rete CDN non gestita da Adobe, ora è possibile abilitare il reporting automatico del traffico, eliminando in tal modo la necessità di condividere eventuali rapporti sul traffico con Adobe.

  Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un&#39;e-mail a `aemcs-rum-adopter@adobe.com` insieme al tuo nome di dominio per ciascuno degli ambienti per i quali vuoi abilitare la telemetria operativa dal tuo indirizzo e-mail associato al tuo Adobe ID. Il team di prodotto di Adobe abiliterà quindi il servizio di telemetria operativa.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Mappatura del dominio {#cdn-config}

Configura il traffico nella rete CDN di Adobe nei seguenti modi:

* [Trasformazioni delle richieste](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations): modifica gli aspetti delle richieste in arrivo, inclusi percorsi, parametri di query e intestazioni HTTP, prima che vengano instradate in AEM.
* [Trasformazioni delle risposte](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations): modifica le intestazioni HTTP delle risposte in uscita prima che vengano inviate al browser.
* [Selettori di origine](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations#origin-selectors): instradano il traffico attraverso la rete CDN verso siti e applicazioni esterni ad AEM.

Una volta dichiarate queste regole nel controllo del codice sorgente (Git), puoi distribuirle nella rete CDN utilizzando la pipeline di configurazione di Cloud Manager. Consulta anche la funzione di reindirizzamento lato client nella sezione dei primi utilizzatori, qui di seguito.

### Pagine di errore della rete CDN personalizzate {#cdn-error-pages}

Nell’improbabile eventualità in cui la rete CDN non riesca a indirizzare il traffico all’origine AEM, può essere indicata una pagina di errore personalizzata, che sostituisce la versione generica. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-error-pages.md) su come distribuire pagine di errore con il brand.

### Programma per i primi utilizzatori {#foundation-early-adopter}

#### Reindirizzamenti lato server (programma Early Adopter) {#server-side-redirects-early-adopter}

Configura i reindirizzamenti lato server 301/302 nel controllo del codice sorgente e distribuiscili alla rete CDN. Consulta [ulteriori informazioni](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) e partecipa al programma per i primi utilizzatori inviando un’e-mail a **<aemcs-cdn-config-adopter@adobe.com>**.

#### Avvisi sulle regole del filtro del traffico (programma per i primi utilizzatori) {#traffic-filter-rules-alerts-early-adopter}

Le [Regole del filtro del traffico](/help/security/traffic-filter-rules-including-waf.md) rilasciate di recente, che includono le regole WAF (Web Application Firewall) con licenza facoltativa a parte, permettono di configurare il traffico da consentire o bloccare.

Ora puoi inviare un’e-mail **<aemcs-cdn-config-adopter@adobe.com>** per partecipare al programma per i primi utilizzatori in modo da poter ricevere un avviso ogni volta che vengono attivate le tue regole del filtro del traffico. Le notifiche e-mail del Centro azioni ti informeranno quando si verificano determinate condizioni di traffico, in modo che tu possa adottare le misure appropriate.

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

## Guide di [!DNL Experience Manager] {#guides}

### Possibilità di tradurre i contenuti in più lingue utilizzando gruppi di lingue preconfigurati

Experience Manager Guides ora consente di creare gruppi di lingue e tradurre facilmente il contenuto in più lingue. Questa funzione consente di organizzare e gestire le traduzioni in base alle esigenze della tua organizzazione.

Ad esempio, se devi tradurre il contenuto per alcuni paesi in Europa, puoi creare un gruppo contenente le lingue europee come inglese (EN), francese (FR), tedesco (DE), spagnolo (ES) e italiano (IT).

![pannello di traduzione](/help/release-notes/assets/guides/translation-languages-2404.png)

*Seleziona i gruppi di lingue o le lingue in cui tradurre i documenti.*

>[!NOTE]
>
>Se manca la cartella di destinazione di una lingua o la lingua di destinazione è la stessa della lingua di origine, la cartella di destinazione è disattivata e mostra un segnale di avviso.

In qualità di amministratore, puoi creare gruppi di lingue e configurarli in più profili di cartelle. In qualità di autore, puoi visualizzare i gruppi di lingue configurati nel tuo profilo di cartella.


Nel complesso, la creazione di gruppi linguistici migliora l’efficienza e la produttività dei progetti di traduzione, migliorando in ultima analisi il processo di localizzazione in più lingue.

### Esperienza rinnovata per cercare e filtrare i file nella vista Archivio

Ora disponi di un’esperienza avanzata per filtrare i file. La funzionalità rinnovata di filtro dei file consente di cercare e navigare tra i file in modo più semplice.

![cerca i file nella vista archivio](/help/release-notes/assets/guides/repository-filter-search-2404.png)

*Cerca i file contenenti il testo`general purpose.`*

Sfrutta vantaggi quali un accesso più rapido ai file rilevanti e un’interfaccia utente più intuitiva, che rende l’esperienza di ricerca più fluida ed efficiente.

![filtro di ricerca rapida &#x200B;](/help/release-notes/assets/guides/repository-filter-search-quick.png)

*Utilizza i filtri rapidi per cercare file DITA e non DITA.*

Ulteriori informazioni sulla funzionalità **Ricerca con filtro** nella sezione [Pannello sinistro](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/user-guide/author-content/create-preview-topics/author-content-aem-guides/work-with-web-editor/web-editor-features#id2051EA0M0HS).

### Miglioramenti nei connettori delle origini dati

I seguenti miglioramenti sono stati apportati ai connettori delle origini dati per la versione 2024.4.0:

#### Connessione a origini dati Salsify, Akeneo e bacheche DevOps di Microsoft Azure (ADO)

Oltre ai connettori predefiniti esistenti, Experience Manager Guides fornisce anche connettori per origini dati Salsify, Akeneo e bacheche DevOps di Microsoft Azure (ADO). In qualità di amministratore, puoi scaricare e installare questi connettori. Quindi, configura i connettori installati.

#### Copiare e incollare la query di esempio per creare un frammento di contenuto o un argomento

Puoi copiare e incollare facilmente una query di dati di esempio nel generatore per creare uno snippet di contenuto o un argomento. Con questa funzione, non è necessario ricordare la sintassi o creare una query manualmente. Invece di digitare manualmente la query, puoi copiare e incollare una query di esempio, modificarla e utilizzarla per recuperare i dati in base alle tue esigenze.

![finestra di dialogo inserisci frammento di contenuto](/help/release-notes/assets/guides/insert-content-snippet.png)

*Copia e modifica una query di esempio per creare lo snippet di contenuto.*

#### Connettersi a file di dati JSON utilizzando un connettore file


Ora, in qualità di amministratore, puoi configurare un connettore per file JSON per utilizzare i file di dati JSON come origine di dati. Utilizza il connettore per importare i file JSON dal computer o da Adobe Experience Manager Assets. In qualità di autore, puoi quindi creare snippet di contenuti o argomenti utilizzando i generatori.

Questa funzione consente di utilizzare i dati memorizzati nei file JSON e di riutilizzarli in vari snippet. Il contenuto viene inoltre aggiornato dinamicamente ogni volta che si aggiornano i file JSON.

#### Configurare più URL di risorse per un connettore per creare snippet di contenuto o argomenti

In qualità di amministratore, puoi configurare più URL di risorse per alcuni connettori come Generic REST Client, Salsify, Akeneo e bacheche Microsoft Azure DevOps (ADO).
Quindi, in qualità di autore, puoi connetterti alle origini dati per creare snippet o argomenti utilizzando i generatori. Questa funzione è utile in quanto non è necessario creare un’origine dati per ogni URL. Consente di recuperare rapidamente i dati da una qualsiasi delle risorse per una particolare origine dati in un singolo snippet di contenuto o argomento. Visualizza ulteriori dettagli sui connettori delle origini dati e su come [configurare un connettore di origine dati dall’interfaccia utente](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/install-guide/cs-ig/web-editor-configs-cs/conf-data-source-connector-tools). Scopri come [utilizzare dati dall’origine dati](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/user-guide/author-content/create-preview-topics/author-content-aem-guides/work-with-web-editor/web-editor-content-snippet).

Per ulteriori informazioni sulle nuove funzionalità e sui miglioramenti, visualizzare [Informazioni sulle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
