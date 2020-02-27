---
title: Differenze e novità - Adobe Experience Manager come servizio cloud
description: 'Differenze e novità - Adobe Experience Manager (AEM) come servizio cloud. '
translation-type: tm+mt
source-git-commit: 160db0dabc99eccdef5bd579f8ccc26a861b1380

---


# Novità e differenze {#what-is-new-and-what-is-different}

Per molti anni AEM è disponibile:

* Locale

* come servizio gestito

Esistono differenze intrinseche tra questi approcci precedenti e AEM come servizio cloud:

* [Architettura](#architecture)
* [Aggiornamenti](#upgrades)
* [Cloud Manager](#cloud-manager)
* [Onboarding](#onboarding)
* [Sviluppo](#developing)
* [Operazioni e prestazioni](#operations-and-performance)
* [Gestione identità](#identity-management)
* [Interfaccia utente di authoring](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>Tali panorami non sono esaustivi, ma mirano a fornire un&#39;introduzione.

>[!NOTE]
>
>Per ulteriori informazioni sulle versioni locale e del servizio gestito, consultate la documentazione fornita con [AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html).

## Architettura {#architecture}

>[!NOTE]
>
>Per ulteriori dettagli vedere [Architettura](/help/core-concepts/architecture.md).

AEM come servizio cloud ora include:

* Architettura dinamica con un numero variabile di immagini AEM.

![Architettura](assets/introduction-03.png "dinamicaArchitettura dinamica")

Questa architettura:

* Viene ridimensionata in base al traffico *effettivo* e all&#39;attività *effettiva* .

* Presenta istanze singole che vengono eseguite solo quando necessario.

* Utilizza applicazioni modulari.

* dispone di un cluster di autori come predefinito; in questo modo si evita il tempo di inattività per le attività di manutenzione.

Questo consente di ridimensionare automaticamente i diversi pattern di utilizzo:

![Ridimensionamento automatico per diversi](assets/introduction-04.png "pattern di utilizzoRidimensionamento automatico per diversi pattern di utilizzo")


## Aggiornamenti {#upgrades}

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Introduzione](/help/implementing/deploying/overview.md)alla distribuzione.

AEM come servizio cloud ora utilizza l’integrazione continua e la fornitura continua (CI/CD) per garantire che i progetti siano completamente aggiornati. Ciò significa che tutte le operazioni di aggiornamento sono completamente automatizzate, pertanto non è necessaria alcuna interruzione del servizio per gli utenti.

Adobe si occupa in modo proattivo di aggiornare tutte le istanze operative del servizio all’ultima versione della base di codici AEM:

* Correzioni di bug:

   * Può essere rilasciato su base giornaliera.

   * Le istanze vengono spesso aggiornate con le correzioni di bug più recenti. Poiché le modifiche vengono applicate regolarmente, l&#39;impatto è incrementale, riducendo l&#39;impatto sul servizio.

   * La maggior parte degli aggiornamenti sono per motivi di manutenzione e sicurezza.

* Nuove funzioni:

   * Verrà rilasciato tramite un programma mensile prevedibile.

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Architettura](/help/core-concepts/architecture.md#deployment-architecture)di distribuzione.

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager è integrato nell&#39;approccio di aggiornamento continuo di AEM come servizio cloud, in quanto controlla tutti gli aggiornamenti delle tue istanze - questo è obbligatorio.

Gli aggiornamenti possono essere attivati da Adobe quando è disponibile una nuova versione del servizio cloud. In alternativa, puoi attivare gli aggiornamenti dell&#39;applicazione utilizzando le pipeline fornite da Cloud Manager.

Cloud Manager è:

* utilizzati per gestire i programmi e gli ambienti AEM,

* un componente essenziale di AEM come servizio cloud; per ogni nuovo tenant viene eseguito il primo provisioning per l&#39;accesso a Cloud Manager,

* il punto di ingresso unico per il personale operativo e di sviluppo.

Nello specifico, il numero e il tipo di programmi AEM che è possibile creare da Cloud Manager deriva da:

* dal contratto di licenza con il cliente,

* da attori interni quando AEM come servizio cloud viene utilizzato per l’abilitazione, o per la formazione,

* da processi basati su esterni, ad esempio quelli avviati da Adobe.com.

Cloud Manager si è evoluto come portale self-service in cui è possibile creare e configurare i componenti principali di AEM come servizio Cloud:

* Creazione e gestione di nuovi programmi.

* Creazione e gestione degli ambienti AEM all’interno di questi programmi.

* Creazione e gestione delle tubazioni per distribuire il codice cliente e la configurazione correlata a un ambiente specifico.

* Essere informati di importanti eventi del ciclo di vita per questi componenti (ad esempio, aggiornamenti dei prodotti).

Attualmente Cloud Manager è in grado di creare ambienti in 3 aree geografiche (con più aree geografiche):

* Stati Uniti (est)

* EMEA (Paesi Bassi)

* APAC (Australia)

## Onboarding {#onboarding}

>[!NOTE]
>
>Per ulteriori dettagli, consultate [Onboarding](/help/onboarding/home.md).

L’avvio e la gestione di un progetto AEM è semplice quando si utilizza AEM come servizio Cloud, in quanto Adobe è responsabile per molti aspetti:

* Le immagini AEM di base sono ottimizzate per casi di utilizzo specifici.

* Molte delle attività di configurazione manuale sono state ridondanti.

È anche molto diverso in quanto esiste ora:

* una fase di valutazione per garantire che tutti i prerequisiti siano stati soddisfatti; , ad esempio:

   * Requisiti legali

   * Accordi contrattuali

   * Requisiti tecnici per qualsiasi contenuto e/o codice esistente personalizzato dal cliente

* Requisiti di distribuzione:

   * Aggiornamenti del codice; tutte le applicazioni sviluppate dai clienti per una versione precedente di AEM dovranno essere riviste ed eventualmente aggiornate.

   * Migrazione dei contenuti

## Sviluppo {#developing}

>[!NOTE]
>
>Per ulteriori dettagli è possibile iniziare con [Linee guida](/help/implementing/developing/introduction/development-guidelines.md) per lo sviluppo e [lo sviluppo - Esercitazione](/help/implementing/developing/introduction/develop-wknd-tutorial.md)WKND.

La nuova architettura che supporta AEM come servizio cloud include alcune modifiche fondamentali all&#39;esperienza di sviluppo complessiva. Uno degli obiettivi principali di AEM come servizio cloud è consentire ai clienti esperti (che hanno utilizzato AEM sia in sede sia nel contesto dei servizi gestiti Adobe) di migrare il più rapidamente possibile ad AEM come servizio cloud, senza dover riscrivere la maggior parte del codice personalizzato. Tuttavia, potrebbero essere ancora necessari alcuni adeguamenti.

### Sviluppo cloud {#aem-as-a-cloud-service-developing-cloud-development}

Per l&#39;esecuzione delle applicazioni AEM esistenti su AEM come servizio cloud, sono previsti i seguenti passaggi:

* Il codice e la configurazione dell&#39;applicazione devono essere memorizzati nell&#39;archivio del codice Git del programma Cloud Manager associato.
* Il codice e la configurazione dell’applicazione devono essere compatibili con l’ultima versione dell’immagine AEM della linea di base (che potrebbe essere modificata ogni giorno).
   * L&#39;applicazione del cliente deve essere creata e distribuita utilizzando la pipeline di Cloud Manager associata all&#39;ambiente Cloud Manager.
* L&#39;applicazione del cliente deve superare tutti i cancelli di qualità del codice, sicurezza e prestazioni applicati nella pipeline.
* Le immagini create per l&#39;applicazione cliente devono essere distribuite dalla pipeline di Cloud Manager.

Questo processo viene comunemente definito sviluppo per il cloud. Poiché la durata end-to-end dovrebbe richiedere alcuni minuti (da 20 a 50 a seconda della complessità dell&#39;applicazione), è necessario adottare metodologie di sviluppo rapido prima che le modifiche al codice in sospeso e alla configurazione siano tentate nel cloud.

La console Web, in cui vengono gestiti i bundle OSGI e la relativa configurazione, e in precedenza parte di AEM QuickStart, non è più direttamente accessibile agli utenti di AEM come ambiente di servizio cloud. Questa interfaccia è ancora accessibile in modalità di sola lettura tramite una nuova console per sviluppatori. Con questa console, gli sviluppatori possono selezionare e accedere direttamente a qualsiasi nodo particolare di un servizio di creazione o pubblicazione, quindi accedere alle aree bloccate per impostazione predefinita.

>[!NOTE]
>
>Vedere anche Configurazione [OSGi](/help/implementing/deploying/overview.md#osgi-configuration)

Un altro requisito comune per gli sviluppatori è l&#39;accesso rapido ai file di registro dei vari ambienti. Con AEM come servizio cloud, i file di registro dei diversi nodi nei nodi di creazione e pubblicazione sono disponibili tramite Cloud Manager, sia sotto forma di file che possono essere scaricati, sia tramite API.

A causa della netta separazione tra codice e contenuto, gli sviluppatori possono utilizzare un particolare processo per aggiornare il contenuto come parte di una distribuzione. I casi di utilizzo tipici per i contenuti modificabili sono:

* Contenuto standard *predefinito* che fa parte del progetto del cliente (ad esempio, cartelle, modelli, flussi di lavoro ecc.)

* Cerca definizioni indice

* ACL e autorizzazioni

* Utenti e gruppi di utenti del servizio

### Sviluppo locale {#aem-as-a-cloud-service-developing-local-development}

Al fine di supportare sessioni e sviluppo rapidi, è anche possibile sviluppare applicazioni AEM al di fuori di AEM come contesto di servizio cloud. A tal fine, gli sviluppatori possono accedere ai seguenti artifact:

* Guida rapida di AEM come servizio cloud: un programma di installazione autonomo `.jar` basato sulla più recente base di codice AEM, con la stessa superficie funzionale e API.

* AEM come SDK del dispatcher di servizi cloud: un processo basato su immagini per verificare e convalidare localmente le configurazioni del dispatcher

>[!NOTE]
>
>È opportuno notare che la Guida rapida di Cloud non consente tutte le funzionalità di AEM Sites e AEM Assets. È costituito da un semplice ambiente di authoring in cui la maggior parte delle estensioni può essere sviluppata e testata.

## Operazioni e prestazioni {#operations-and-performance}

>[!NOTE]
>
>Per ulteriori dettagli, inizia da [Backup](/help/operations/backup.md), [Indicizzazione](/help/operations/indexing.md) e [altre attività di manutenzione](/help/operations/maintenance.md).

Con AEM come servizio cloud, tali operazioni sono automatizzate e non è più necessario interrompere il servizio.

In questi settori:

* Molte attività sono state automatizzate.

* Le topologie sono ottimizzate per la massima resilienza ed efficienza; ad esempio, la replica binaryless è l&#39;impostazione predefinita.

* Le attività a carico elevato, come code, processi e attività di elaborazione in blocco, sono state spostate dall’istanza principale di AEM per essere gestite tramite micro-servizi condivisi e dedicati.

Le operazioni per AEM come servizio Cloud sono inoltre supportate da una nuova infrastruttura di monitoraggio, reporting e avvisi. Questo consente agli SRE di Adobe (Site Reliability Engineers) di mantenere il servizio in modo proattivo. I vari elementi dell&#39;architettura sono dotati di una varietà di controlli sanitari. Se, per qualche motivo, un particolare nodo dell&#39;architettura è considerato malsano, allora viene rimosso dal servizio e sostituito silenziosamente con uno nuovo, sano.

## Gestione identità {#identity-management}

>[!NOTE]
>
>Per ulteriori dettagli, consultate [Sicurezza - Supporto](/help/security/ims-support.md)IMS.

Una modifica importante ad AEM come servizio Cloud è l&#39;utilizzo completamente integrato degli Adobe ID per accedere al livello di authoring.

Questo richiede l’utilizzo di [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Gli account utente consentono agli utenti di accedere ai prodotti e ai servizi Adobe, poiché le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS) da condividere tra tutti i servizi cloud. Una volta assegnato l&#39;accesso ad AEM, gli account utente possono essere citati in AEM come servizio cloud (come prima); ad esempio, per definire ruoli e autorizzazioni dalle interfacce utente di AEM Security.

Questo combina i vantaggi di:

* Utilizzo di Adobe Identity Management System (IMS) per fornire single sign-on in tutte le applicazioni cloud Adobe.

* Preferenze utente che rimangono locali per ogni particolare istanza di AEM come servizio cloud.

## Interfaccia utente di authoring {#authoring-user-interface}

>[!NOTE]
>
>Per ulteriori dettagli, la [gestione](/help/sites-cloud/authoring/getting-started/basic-handling.md) di base è un buon punto di partenza.

I principi di base dell’interfaccia utente di authoring, sia per Siti che per Risorse, saranno molto familiari per chiunque abbia già utilizzato AEM in passato.

La differenza principale sta nel fatto che l’interfaccia è completamente touch; l’interfaccia classica non è più disponibile. In caso contrario, le nozioni di base rimangono invariate, con solo piccole modifiche apparenti.

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites as a Cloud Service consente di fornire ai clienti esperienze personalizzate basate su contenuti, combinando le potenzialità di AEM Content Management System con AEM Digital Asset Management.

Per informazioni dettagliate, consultate la panoramica delle [modifiche ai siti](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Cloud Service offre alle aziende una soluzione SaaS nativa per il cloud, che consente non solo di eseguire le operazioni di gestione delle risorse digitali e di contenuti multimediali dinamici con velocità ed impatto, ma anche di utilizzare funzionalità intelligenti di nuova generazione, come l&#39;AI/ML, direttamente da un sistema sempre attuale, sempre disponibile e sempre in grado di apprendere.

L’offerta di risorse include l’elaborazione di risorse di nuova generazione nel cloud e l’acquisizione e la ricerca di risorse ad alte prestazioni.

Per informazioni dettagliate, consultate [panoramica e introduzione alle risorse come servizio](/help/assets/overview.md)cloud.
