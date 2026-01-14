---
title: Introduzione all’architettura di Adobe Experience Manager as a Cloud Service
description: Introduzione all’architettura di Adobe Experience Manager as a Cloud Service.
exl-id: 3fe856b7-a0fc-48fd-9c03-d64c31a51c5d
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '2710'
ht-degree: 98%

---

# Introduzione all’architettura di Adobe Experience Manager as a Cloud Service {#an-introduction-to-the-architecture-adobe-experience-manager-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="intro_aem_cloudservice_architecture"
>title="Introduzione all’architettura di AEM as a Cloud Service"
>abstract="In questa scheda puoi visualizzare la nuova architettura di AEM as a Cloud Service e comprendere le modifiche apportate. Per AEM è stata creata un’architettura dinamica con un numero variabile di immagini, pertanto è importante prendere il tempo necessario per comprenderne l’architettura cloud."
>additional-url="https://video.tv.adobe.com/v/346182?captions=ita" text="Panoramica dell’architettura"

Adobe Experience Manager (AEM) as a Cloud Service offre una serie di servizi componibili per la creazione e la gestione di esperienze ad alto impatto.

Questa pagina fornisce un’introduzione all’architettura logica, all’architettura dei servizi, all’architettura dei sistemi e all’architettura di sviluppo per AEM as a Cloud Service.

## Architettura logica {#logical-architecture}

AEM as a Cloud Service è costituito da soluzioni di alto livello come AEM Sites, AEM Assets e AEM Forms. Questi servizi sono concessi in licenza singolarmente, ma possono essere utilizzati in collaborazione. Ogni soluzione utilizza una combinazione di servizi componibili forniti da AEM as a Cloud Service, a seconda dei rispettivi casi d’uso.

### Programmi {#programs}

Le applicazioni AEM sono materializzate sotto forma di [Programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) che vengono creati nell’applicazione Cloud Manager, in base ai diritti di licenza. Questi programmi consentono di controllare completamente il nome, la configurazione e l’allocazione delle autorizzazioni dell’applicazione AEM associata nel contesto di un determinato progetto.

La clientela viene identificata da Adobe come **tenant**, noto anche come *Organizzazione IMS* (Identity Management System). Un tenant può disporre di tutti i programmi necessari e di una licenza. Ad esempio, è abbastanza comune vedere un programma centrale per AEM Assets, mentre AEM Sites potrebbe essere utilizzato in più programmi corrispondenti a più esperienze online.

>[!NOTE]
>
>Gli Edge Delivery Services di AEM sono esposti come soluzione di livello superiore in Cloud Manager, pur facendo parte delle altre soluzioni principali dal punto di vista delle licenze. Ad esempio, AEM Sites con Edge Delivery Services.

Un programma può essere configurato con qualsiasi combinazione delle soluzioni di alto livello e ogni soluzione può supportare da uno a più componenti aggiuntivi. Ad esempio, Commerce o Screens per AEM Sites, Dynamic Media o Brand Portal per AEM Assets.

![AEM as a Cloud Service: Programmi](assets/architecture-aem-edge-programs.png "AEM as a Cloud Service - Architettura di distribuzione")

### Ambienti {#environments}

Una volta creato un programma con le soluzioni AEM Sites, AEM Assets o AEM Forms, in tale programma le istanze AEM associate verranno rappresentate sotto forma di ambienti AEM.

Con AEM as a Cloud Service sono disponibili quattro tipi di [ambienti](/help/implementing/cloud-manager/manage-environments.md):

* Ambiente di produzione:

   * Un ambiente di produzione ospita le applicazioni per i professionisti aziendali ed esegue le esperienze live.

* Ambiente di staging:

   * Un ambiente di staging è generalmente associato a un ambiente di produzione con una relazione 1:1.
   * L’ambiente di staging è progettato principalmente per test automatizzati prima che le modifiche all’applicazione vengano inviate all’ambiente di produzione,
      * indipendentemente dalle modifiche avviate da Adobe come parte di un aggiornamento di manutenzione o dalle distribuzioni del codice.
      * In caso di distribuzione del codice, è possibile anche eseguire test manuali.
   * Il contenuto dell’ambiente di staging è generalmente sincronizzato con il contenuto di produzione tramite la funzione di copia self-service dei contenuti.
   * Esecuzione di test di prestazioni e sicurezza nell’ambiente di staging.  Ha le stesse dimensioni della produzione.
* Ambiente di sviluppo:
   * Un ambiente di sviluppo consente ai tuoi sviluppatori di implementare e testare le applicazioni AEM nelle medesime condizioni di esecuzione degli ambienti di staging e di produzione.
   * Le modifiche passano attraverso una pipeline di distribuzione che consente gli stessi gate di qualità del codice e sicurezza delle pipeline di distribuzione in produzione.
   * Gli ambienti di sviluppo non hanno le stesse dimensioni di quelli di staging e produzione e non devono essere utilizzati per eseguire test di prestazioni e sicurezza.
* Ambiente di sviluppo rapido (RDE):
   * Un ambiente RDE consente di eseguire rapidamente le iterazioni di sviluppo durante la distribuzione di codice nuovo o esistente nelle istanze RDE, senza passare attraverso una pipeline di distribuzione formale come quella presente negli ambienti di sviluppo regolari.

### Edge Delivery Services {#logical-architecture-edge-delivery-services}

Un programma AEM può essere configurato anche con [Edge Delivery Services](/help/edge/overview.md).

Una volta configurato, AEM può fare riferimento agli archivi di codice GitHub utilizzati per creare le esperienze con gli Edge Delivery Services. Di conseguenza, diventano disponibili nuove opzioni di configurazione per le esperienze associate. Ad esempio, è possibile configurare la rete CDN gestita da Adobe e accedere alle metriche delle licenze o ai rapporti SLA.

## Architettura di servizio {#service-architecture}

L’elenco dei servizi componibili di alto livello in AEM as a Cloud Service può essere rappresentato con due segmenti: Gestione dei contenuti e Distribuzione delle esperienze:

![Panoramica di AEM as a Cloud Service con Edge Delivery Services](assets/architecture-aem-edge.png "Panoramica di AEM as a Cloud Service con Edge Delivery Services")

Per la gestione dei contenuti, esistono due set principali di servizi per l’authoring dei contenuti, entrambi rappresentati da *origini di contenuto*:

* Livello di authoring AEM:
fornisce un’interfaccia basata su web (con API associate) per la gestione dei contenuti web. Funziona per entrambi gli approcci:
   * Headful: tramite l’editor di pagine e l’editor universale
   * Headless: tramite l’editor di frammenti di contenuto
* Livello di authoring basato su documenti:
consente di creare contenuti utilizzando applicazioni standard. Ad esempio:
   * Microsoft Word ed Excel, tramite SharePoint
   * Documenti e Fogli Google, tramite Google Drive

Per la distribuzione delle esperienze, utilizzando AEM Sites o AEM Forms, sono disponibili anche due set principali di servizi, non reciprocamente esclusivi e che funzionano in una rete per la consegna dei contenuti (CDN) gestita da Adobe e condivisa, come origini diverse:

* Livello di pubblicazione di AEM:
   * Esegue una farm di editori e dispatcher AEM standard che consente il rendering dinamico di pagine web e contenuti API (ad esempio, GraphQL) assemblati con contenuti pubblicati.
   * Si basa principalmente sulla logica dell’applicazione lato server.
* Livello di pubblicazione di Edge Delivery:
   * Consente il rendering dinamico di pagine web e contenuti API da varie origini di contenuto, come il livello di authoring AEM o il livello di authoring basato su documenti.
   * Si basa sulla logica dell’applicazione lato client ed è progettato per garantire le massime prestazioni.

Ci sono anche i principali servizi adiacenti:

* Livello delle risorse di Edge Delivery:
   * Consente la consegna di elementi multimediali approvati e pubblicati da AEM Assets. Ad esempio, immagini e video.
   * Di solito si fa riferimento agli elementi multimediali dalle esperienze in esecuzione sul livello di pubblicazione AEM, sul livello di pubblicazione Edge Delivery o da qualsiasi altra applicazione Adobe Experience Cloud integrata con AEM Assets.
* Livello di anteprima AEM e livello di anteprima di Edge Delivery Services:
   * Sono disponibili anche per le esperienze create rispettivamente con il livello di pubblicazione AEM o il livello di pubblicazione Edge Delivery.
   * Consente agli autori di contenuti di visualizzare in anteprima il contenuto nel contesto prima delle operazioni di pubblicazione.

>[!NOTE]
>
>Per impostazione predefinita, i programmi solo Assets non dispongono di un livello di pubblicazione né di un livello di anteprima.

Ci sono altri servizi adiacenti:

* Servizio di replica:
   * Situato tra il livello di gestione dei contenuti e il livello di distribuzione delle esperienze.
   * È responsabile dell’esecuzione delle operazioni di *pubblicazione* emesse dagli autori dei contenuti e di fornitura dei contenuti pubblicati ai livelli di pubblicazione (AEM o Edge Delivery).

  >[!NOTE]
  >Il servizio di replica ha subito una riprogettazione completa rispetto alle versioni 6.x di AEM, in quanto il framework di replica delle versioni precedenti di AEM non viene più utilizzato per pubblicare contenuti.
  >
  >L’architettura più recente si basa su un approccio di *pubblicazione e abbonamento* con code di contenuti basate su cloud. Per il livello di pubblicazione AEM, consente a un numero variabile di editori di abbonarsi al contenuto di pubblicazione ed è una parte essenziale per ottenere una scalabilità automatica vera e rapida di AEM as a Cloud Service

* Servizio di archiviazione dei contenuti:
   * Viene utilizzato dal livello di authoring AEM.
   * È un’istanza basata su cloud di un archivio di contenuti conforme a JCR, implementato con tecnologia Apache Oak.
   * La persistenza dei contenuti si basa principalmente sull’archiviazione cloud basata su BLOB.
* Servizio CI/CD:
   * Rappresenta il sottoinsieme delle funzionalità di Cloud Manager dedicate alla gestione delle pipeline di distribuzione negli ambienti AEM.
* Servizio di testing:
   * Rappresenta l’infrastruttura sottostante utilizzata per eseguire:
      * test funzionali,
      * test dell’interfaccia utente, ad esempio basati su script Selenium o Cypress,
      * test di audit dell’esperienza, ad esempio i punteggi Lighthouse,

     come parte di una pipeline di distribuzione in un ambiente AEM o come parte di una richiesta pull GitHub a un archivio del codice di Edge Delivery.
* Servizio dati:
   * È responsabile dell’esposizione dei dati cliente come le metriche delle licenze (ad esempio, richieste di contenuti, archiviazione, utenti) o i rapporti sull’utilizzo (come il numero di caricamenti e download).
   * I dati cliente possono essere esposti tramite API e all’interno di interfacce utente del prodotto (come Cloud Manager).
* Il servizio di telemetria operativa:
   * È responsabile della raccolta di metriche chiave da un’esperienza del cliente (come visualizzazioni di pagina, web vitals di base, eventi di conversione), nonché della risposta alle query associate (ad esempio, principali visualizzazioni della pagina per un determinato dominio negli ultimi 7 giorni).
* Servizio Assets Compute:
   * È responsabile dell’elaborazione di immagini, video e documenti caricati, ad esempio file PDF e Adobe Photoshop. L’elaborazione può utilizzare l’intelligenza artificiale di Adobe per estrarre metadati di immagini e video (come tag descrittivi o tonalità di colore primarie) e generare rappresentazioni (come dimensioni o formati diversi) con accesso a API come le API di Adobe Photoshop e Adobe Lightroom.
* L’Identity Management Service (IMS):
   * È la posizione centrale responsabile della gestione e dell’autenticazione di utenti e gruppi di utenti per una determinata applicazione di Adobe Experience Cloud (ad esempio, il livello di authoring di Cloud Manager o AEM).
   * È accessibile tramite Adobe Admin Console.

## Architettura di sistema {#system-architecture}

### Livelli di authoring, anteprima e pubblicazione AEM {#aem-author-preview-publish-tiers}

I livelli authoring e pubblicazione di AEM sono implementati come un set di contenitori Docker, gestiti da un servizio standard di orchestrazione dei contenitori. L’architettura containerizzata risultante è un sistema completamente dinamico con un numero variabile di pod che dipende dall’attività effettiva (per la gestione dei contenuti) e dal traffico effettivo (per la distribuzione dell’esperienza). Questo consente ad AEM as a Cloud Service di adattarsi agli schemi di traffico man mano che cambiano.

Il livello di authoring AEM funziona come un cluster di pod di authoring AEM che condividono un singolo archivio dei contenuti. Un minimo di due pod consente la continuità aziendale durante l’esecuzione delle attività di manutenzione o durante un processo di distribuzione.

Il livello di pubblicazione AEM funziona come una farm di istanze di pubblicazione AEM, ciascuna con il proprio archivio di contenuti pubblicati. Ogni editore è associato a una singola istanza di Apache dotata del modulo dispatcher di AEM per una vista materializzata del contenuto che funge da origine per la rete CDN gestita da Adobe. Un minimo di due pod consente inoltre la continuità aziendale, ma non è insolito vedere questo numero crescere in periodi di traffico elevato.

Il livello di anteprima AEM è composto da un singolo nodo AEM. Utilizzato per il controllo qualità dei contenuti prima della pubblicazione sul livello di pubblicazione. Sul livello di anteprima possono verificarsi tempi di inattività occasionali, in particolare durante le distribuzioni.

### Edge Delivery Services {#system-architecture-edge-delivery-services}

Gli Edge Delivery Services funzionano su una rete CDN e su un’infrastruttura senza server per assemblare le pagine nel modo più performante. Quando viene richiesta una risorsa, l’infrastruttura senza server è responsabile della conversione del contenuto pubblicato in HTML semantico e funge da origine per la rete CDN.

La conversione in HTML semantico avviene dal contenuto pubblicato distribuito dal livello di authoring AEM o dall’ambiente di authoring basato su documenti.

Il diagramma seguente illustra come modificare il contenuto di Sites in Microsoft Word (authoring basato su documento) e pubblicarlo in Edge Delivery. Mostra anche il tradizionale metodo di pubblicazione di AEM utilizzando i vari editor.

![AEM Sites as a Cloud Service con Edge Delivery Services](assets/architecture-aem-edge-author-publish.png "AEM Sites as a Cloud Service con Edge Delivery Services")

Edge Delivery Services fa parte di Adobe Experience Manager e, come tale, Edge Delivery, AEM Sites e AEM Assets possono coesistere sullo stesso dominio. Questo è un caso d’uso comune per i siti Web più grandi. Ad esempio, potrebbe sussistere la necessità di migrare una determinata pagina con traffico elevato in Edge Delivery Services, mentre tutte le altre pagine potrebbero rimanere nel livello di pubblicazione AEM.

## Architettura di sviluppo {#development-architecture}

### Archivi di codice {#code-repositories}

Il codice e la configurazione per i progetti AEM vengono memorizzati in un archivio di codice, da cui vengono rilasciate le pipeline di distribuzione quando vengono apportate modifiche. Esistono diversi tipi di archivi di codice:

* Full stack AEM:
   * Per l’archiviazione del codice Java lato server e le configurazioni OSGI per i livelli di authoring e pubblicazione di AEM.
* Front-end AEM:
   * Per memorizzare codice JS, CSS e HTML lato client per i livelli di authoring e pubblicazione di AEM.
Per ulteriori dettagli su clientlibs, consultare [Utilizzo delle librerie lato client su AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md).
* Livello web AEM:
   * Memorizza i file di configurazione del Dispatcher per il livello di pubblicazione AEM.
* Configurazione AEM:
   * Consente di memorizzare varie opzioni di configurazione (ad esempio impostazioni CDN o impostazioni delle attività di manutenzione) per il livello di pubblicazione AEM e il livello di pubblicazione Edge Delivery Services.
* Edge Delivery AEM:
   * Per memorizzare il codice JS, CSS e HTML lato client per i siti generati con gli Edge Delivery Services

### Pipeline di distribuzione {#deployment-pipelines}

Sviluppatori e amministratori gestiscono l’applicazione AEM as a Cloud Service mediante il servizio Continuous Integration/Continuous Delivery (CI/CD), tramite Cloud Manager. Cloud Manager espone inoltre qualsiasi elemento relativo al monitoraggio, alla manutenzione, alla risoluzione dei problemi (ad esempio, l’accesso ai file di registro) e alle licenze.

![AEM as a Cloud Service: architettura di distribuzione](assets/architecture-aem-edge-deployment-pipelines.png "AEM as a Cloud Service - Architettura di distribuzione")

Cloud Manager gestisce tutti gli aggiornamenti alle istanze di AEM as a Cloud Service. È una scelta obbligatoria, essendo l’unica soluzione per creare, testare e distribuire l’applicazione del cliente, per il livello di authoring, di anteprima e di pubblicazione. Questi aggiornamenti possono essere attivati da Adobe quando è pronta una nuova versione di AEM Cloud Service oppure dal cliente stesso, quando è pronta una nuova versione della sua applicazione.

Questa viene implementata da una pipeline di implementazione, associata a ogni ambiente all’interno di un programma. Quando una pipeline di Cloud Manager è in esecuzione, crea una nuova versione dell’applicazione del cliente, sia per il livello di authoring che per quello di pubblicazione. Tale risultato si ottiene combinando gli ultimi pacchetti cliente con la più recente immagine linea di base di Adobe.

La pipeline di distribuzione viene attivata quando si apportano modifiche al codice o quando Adobe distribuisce una nuova versione di manutenzione.

In entrambi i casi viene eseguito lo stesso insieme di test automatizzati. È costituito da test:

* offerti da Adobe per garantire l’integrità del prodotto
* test forniti dal cliente
   * Test funzionali: tramite richieste http al livello di authoring o pubblicazione di AEM
   * Test dell’interfaccia utente: basati sulla tecnologia Selenium o Cypress

Questi test automatizzati vengono eseguiti nell’ambiente di staging, ed è per questo che è importante mantenere il contenuto di tale ambiente il più vicino possibile al contenuto dell’istanza di produzione.

Una volta superati tutti i test, il nuovo codice viene distribuito all’ambiente di produzione.

### Aggiornamenti continui {#rolling-updates}

Cloud Manager automatizza completamente il cut-over alla versione più recente dell’applicazione AEM aggiornando tutti i nodi di servizio con un pattern di aggiornamento continuo. Questo significa che i servizi di authoring o pubblicazione non subiranno alcun **tempo di inattività**.

## Importanti innovazioni da AEM 6.x {#major-innovations-since-aem-6x}

La più recente architettura di AEM as a Cloud Service introduce alcune modifiche e innovazioni fondamentali rispetto alle generazioni precedenti (AEM 6.x e versioni precedenti):

* Tutti i file vengono caricati e serviti direttamente da un archivio dati cloud. Il flusso di bit associato non passa mai attraverso la JVM dei servizi di authoring e pubblicazione di AEM. Di conseguenza, i nodi dei servizi di authoring e pubblicazione di AEM possono avere dimensioni più ridotte e risultare maggiormente compatibili con l’aspettativa di una rapida scalabilità automatica. Per i professionisti del settore, questo consente un’esperienza più rapida durante il caricamento e il download di immagini, video e altre attività.

* Tutte le operazioni che consistono nella pubblicazione di contenuto adesso includono una pipeline che segue uno schema di sottoscrizione. Il contenuto pubblicato viene inviato a varie code della pipeline, alle quali sono abbonati tutti i nodi del servizio di pubblicazione. Di conseguenza, il livello di authoring non deve essere a conoscenza del numero di nodi presenti nel servizio di pubblicazione, il che consente un rapido ridimensionamento automatico del livello di pubblicazione.

* L’architettura separa completamente il contenuto dell’applicazione dal codice e dalla configurazione dell’applicazione. Tutto il codice e la configurazione diventano praticamente immutabili e vengono inseriti nell’immagine linea di base utilizzata per creare i vari nodi dei servizi di authoring e pubblicazione. Di conseguenza, esiste una garanzia assoluta che ogni nodo sia identico e che le modifiche al codice e alla configurazione possano essere apportate solo a livello globale, eseguendo una pipeline di Cloud Manager.

* L’architettura include più micro-servizi basati su tecnologia senza server, in particolare con Adobe I/O Runtime

## Ulteriori informazioni {#further-information}

* Configurazione del programma
   * [Percorso di onboarding](/help/journey-onboarding/overview.md)
   * [Programmi e tipi di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
* Architettura di sviluppo
   * [Archivi di Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md)
   * [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)
   * [Test della qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md)
* Edge Delivery Services:
   * [Panoramica di AEM as a Cloud Service con Edge Delivery Services](/help/edge/overview.md)
   * [Utilizzo di Edge Delivery Services](/help/edge/overview.md)
   * [Esplora l’architettura sottostante e le parti importanti di AEM as a Cloud Service con Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/introduction/architecture.html?lang=it)
