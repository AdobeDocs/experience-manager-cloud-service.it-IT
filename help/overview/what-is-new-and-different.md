---
title: Quali sono le differenze e le novità - Adobe Experience Manager as a Cloud Service
description: Novità e differenze - Adobe Experience Manager (AEM) come Cloud Service.
exl-id: d1ce126e-960c-4367-b741-af709dd81010
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 10%

---

# Novità e differenze {#what-is-new-and-what-is-different}

Da molti anni AEM sono disponibili entrambi:

* Locale

* as a Managed Service

Esistono differenze intrinseche tra questi approcci precedenti e AEM come Cloud Service:

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
>Tali panorami non sono esaustivi, ma mirano a fornire un’introduzione.

>[!NOTE]
>
>Per ulteriori dettagli sulle versioni On-Premise e Managed Service, consulta la documentazione impostata per [AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it).

## Architettura {#architecture}

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Architettura](/help/core-concepts/architecture.md).

AEM as a Cloud Service adesso include:

* Architettura dinamica con un numero variabile di immagini AEM

![Architettura dinamica](assets/introduction-03.png "Architettura dinamica")

Tale architettura:

* viene ridimensionata in base al *traffico* e all’*attività* effettiva;

* presenta istanze singole che vengono eseguite solo quando necessario;

* utilizza applicazioni modulari;

* per impostazione predefinita dispone di un cluster di authoring, per garantire la disponibilità continua anche durante le attività di manutenzione.

Questo approccio consente la scalabilità automatica in base alle esigenze di diversi schemi di utilizzo:

![Scalabilità automatica per diversi schemi di utilizzo](assets/introduction-04.png "Scalabilità automatica per diversi schemi di utilizzo")


## Aggiornamenti AEM {#aem-updates}

>[!NOTE]
>Per ulteriori dettagli, consulta [Aggiornamenti AEM versione](/help/implementing/deploying/aem-version-updates.md).

AEM come Cloud Service ora utilizza l’integrazione continua e la distribuzione continua (CI/CD) per garantire che i progetti siano nella versione di AEM più recente. Ciò significa che le istanze Production e Stage vengono aggiornate alla versione più recente AEM senza alcuna interruzione del servizio per gli utenti.

>[!NOTE]
> Se l’aggiornamento dell’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di stage. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, sia gli ambienti di stage che di produzione si trovino nella stessa versione AEM.

Gli aggiornamenti delle versioni AEM sono di due tipi:

* **Aggiornamenti push AEM**

   * Può essere rilasciato su base giornaliera.
   * La maggior parte della manutenzione, incluse le ultime correzioni di bug e gli aggiornamenti di sicurezza.

      Con l’applicazione regolare delle modifiche, l’impatto è incrementale, riducendo l’impatto sul servizio.

* **Nuovi aggiornamenti delle funzioni**

   * Rilasciato tramite un programma mensile prevedibile.

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager è parte integrante dell’approccio di aggiornamento continuo di AEM come Cloud Service, in quanto controlla tutti gli aggiornamenti alle istanze - questo è obbligatorio.

Gli aggiornamenti possono essere attivati da Adobe quando è disponibile una nuova versione del servizio cloud. In alternativa, puoi attivare gli aggiornamenti dell’applicazione utilizzando le pipeline fornite da Cloud Manager.

Cloud Manager è:

* utilizzati per gestire programmi e ambienti AEM,

* un componente essenziale di AEM come Cloud Service; per ogni nuovo tenant viene eseguito il primo provisioning per l’accesso a Cloud Manager,

* il punto di ingresso unico per il personale addetto alle operazioni e allo sviluppo.

In particolare, viene derivato il numero e il tipo di programmi AEM che possono essere creati da Cloud Manager:

* dal contratto di licenza con il cliente,

* da attori interni quando AEM come Cloud Service è utilizzato per l&#39;abilitazione, o la formazione,

* da processi guidati dall&#39;esterno, come le prove, avviati da Adobe.com.

Cloud Manager si è evoluto come portale self-service in cui è possibile creare e configurare i componenti principali di AEM come Cloud Service:

* Creazione e gestione di nuovi programmi. Per ulteriori informazioni, consulta [Informazioni su programmi e tipi di programmi](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) .

* Creazione e gestione degli ambienti di AEM all&#39;interno di questi programmi. Per ulteriori informazioni, consulta [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md) .

* Creazione e gestione delle pipeline per la distribuzione del codice cliente e della relativa configurazione in un ambiente specifico. Per ulteriori informazioni, consulta [Configurazione della pipeline CI-CD](/help/implementing/cloud-manager/configure-pipeline.md) .

* Ricevere notifiche su importanti eventi del ciclo di vita per questi componenti (ad esempio, aggiornamenti dei prodotti).

Cloud Manager crea ambienti nei centri dati in molte aree geografiche, fornendo una copertura globale. I punti di presenza CDN (PoPs) garantiscono una distribuzione dei contenuti a bassa latenza per i clienti di tutto il mondo.

>[!NOTE]
>Per iniziare a utilizzare Cloud Manager in AEM come Cloud Service, consulta [Accesso ad Experience Manager as a Cloud Service](/help/onboarding/what-is-required/accessing-aem-instance.md) .

## Onboarding {#onboarding}

>[!NOTE]
>
>Per ulteriori dettagli, consulta [Onboarding](/help/onboarding/home.md).

L’avvio e la gestione di un progetto AEM è semplice quando si utilizza AEM as a Cloud Service come Adobe, ed è responsabile di molti aspetti:

* Le immagini della AEM linea di base sono ottimizzate per casi d’uso specifici.

* Molte delle attività di configurazione manuale sono state ridondanti.

È anche molto diverso in quanto ora esiste:

* una fase di valutazione per garantire il rispetto di tutti i requisiti preliminari; compresi, ad esempio:

   * Requisiti legali

   * Accordi contrattuali

   * Requisiti tecnici per qualsiasi contenuto e/o codice esistente personalizzato dal cliente

* Requisiti di distribuzione:

   * Aggiornamenti del codice; tutte le applicazioni per clienti sviluppate per una versione precedente di AEM dovranno essere riviste ed eventualmente aggiornate.

   * Migrazione dei contenuti

## Sviluppo {#developing}

>[!NOTE]
>
>Per ulteriori dettagli, puoi iniziare con [Linee guida per lo sviluppo](/help/implementing/developing/introduction/development-guidelines.md) e [Sviluppo - Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

La nuova architettura che supporta AEM come Cloud Service comporta alcuni cambiamenti fondamentali nell’esperienza complessiva di sviluppo. Uno degli obiettivi principali per AEM come Cloud Service è quello di consentire ai clienti esperti (che hanno utilizzato AEM on-premise o nel contesto di Adobe Managed Services) di migrare a AEM il più rapidamente possibile, senza dover riscrivere la maggior parte del codice personalizzato. Tuttavia, potrebbero essere ancora necessari alcuni adeguamenti.

### Sviluppo cloud {#aem-as-a-cloud-service-developing-cloud-development}

Per l&#39;esecuzione delle applicazioni AEM esistenti su AEM come Cloud Service, sono previsti i seguenti passaggi:

* Il codice e la configurazione dell’applicazione devono essere memorizzati nell’archivio del codice Git del programma Cloud Manager associato.
* Il codice e la configurazione dell&#39;applicazione devono essere compatibili con la versione più recente dell&#39;immagine della linea di base AEM (che potrebbe cambiare quotidianamente).
   * L’applicazione cliente deve essere generata e distribuita utilizzando la pipeline di Cloud Manager associata all’ambiente Cloud Manager.
* L’applicazione del cliente deve superare tutti i gate di qualità del codice, sicurezza e prestazioni applicati nella pipeline.
* Le immagini create per l’applicazione cliente devono essere distribuite dalla pipeline di Cloud Manager.

Questo processo è comunemente denominato sviluppo Cloud-first. Poiché la durata end-to-end dovrebbe richiedere minuti (da 20 a 50 a seconda della complessità dell&#39;applicazione), è necessario adottare metodologie di sviluppo rapido prima che le modifiche al codice in sospeso e alla configurazione vengano tentate nel cloud.

La console Web, in cui vengono gestiti i bundle OSGI e la relativa configurazione associata, e in precedenza parte del AEM QuickStart, non è più accessibile direttamente agli utenti di un AEM come ambiente di Cloud Service. È comunque possibile accedere a questa interfaccia in modalità di sola lettura utilizzando una nuova console per sviluppatori. Con questa console, gli sviluppatori possono selezionare e accedere direttamente a qualsiasi nodo particolare di un servizio di authoring o pubblicazione, quindi accedere alle aree bloccate per impostazione predefinita.

>[!NOTE]
>
>Vedere anche [Configurazione OSGi](/help/implementing/deploying/overview.md#osgi-configuration)

Un altro requisito comune per gli sviluppatori è l’accesso rapido ai file di registro dei vari ambienti. Con AEM come Cloud Service, i file di registro dei diversi nodi nei nodi di authoring e pubblicazione sono resi disponibili tramite Cloud Manager, sotto forma di file che possono essere scaricati o tramite API.

A causa della netta separazione di codice e contenuto, gli sviluppatori possono utilizzare un particolare processo per aggiornare il contenuto come parte di una distribuzione. I casi d’uso tipici per i contenuti modificabili sono:

* Contenuto standard *predefinito* che fa parte del progetto del cliente (ad esempio cartelle, modelli, flussi di lavoro, ecc.)

* Definizioni degli indici di ricerca

* ACL e autorizzazioni

* Utenti e gruppi di utenti del servizio

### Sviluppo locale {#aem-as-a-cloud-service-developing-local-development}

Al fine di sostenere le iterazioni e lo sviluppo rapidi, è anche possibile sviluppare applicazioni AEM al di fuori del AEM come contesto Cloud Service. A questo scopo, gli sviluppatori possono accedere ai seguenti artefatti:

* Guida rapida AEM come Cloud Service: un programma di installazione autonomo `.jar` basato su  della base di codice AEM più recente, con la stessa superficie funzionale e API.

* L’SDK di Dispatcher AEM come Cloud Service: un processo basato su immagini per testare e convalidare localmente le configurazioni di Dispatcher

>[!NOTE]
>
>È opportuno notare che Cloud QuickStart non consente tutte le funzionalità di AEM Sites e AEM Assets. È costituito da un semplice ambiente di authoring in cui è possibile sviluppare e testare la maggior parte delle estensioni.

## Operazioni e prestazioni {#operations-and-performance}

>[!NOTE]
>
>Per ulteriori dettagli, inizia da [Backup](/help/operations/backup.md), [Indicizzazione](/help/operations/indexing.md) e [altre attività di manutenzione](/help/operations/maintenance.md).

Con AEM come Cloud Service, tali operazioni sono automatizzate in modo che qualsiasi interruzione del servizio non sia più necessaria.

In questi settori:

* Molte attività sono state automatizzate.

* Le topologie sono ottimizzate per la massima resilienza ed efficienza; ad esempio, la replica senza binari è l’impostazione predefinita.

* Le attività a carico pesante, come le code, i lavori e le attività di elaborazione in blocco, sono state spostate fuori dall’istanza di AEM principale per essere gestite da microservizi condivisi e dedicati.

Le operazioni per AEM come Cloud Service sono supportate anche da una nuova infrastruttura di monitoraggio, reporting e avvisi. Questo consente agli SRE di Adobe (Site Reliability Engineers) di mantenere il servizio in modo proattivo. I vari elementi dell&#39;architettura sono dotati di una varietà di controlli sanitari. Se, per qualche motivo, un particolare nodo dell&#39;architettura è considerato non sano, allora viene rimosso dal servizio e sostituito silenziosamente con un nuovo, sano.

## Gestione identità {#identity-management}

>[!NOTE]
>
>Per ulteriori dettagli, consulta [Sicurezza - Supporto IMS](/help/security/ims-support.md).

Un cambiamento importante nell’AEM come Cloud Service è l’utilizzo completamente integrato degli ID Adobe per accedere al livello di authoring.

Questo richiede l&#39;utilizzo di [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Gli account utente consentono agli utenti di accedere ai prodotti e ai servizi di Adobe, in quanto le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS) da condividere in tutti i servizi cloud. Una volta assegnato l&#39;accesso a AEM, gli account utente possono essere referenziati in AEM come Cloud Service (come prima); ad esempio, per la definizione di ruoli e autorizzazioni dalle interfacce utente di AEM Security.

Questo combina i vantaggi di:

* Utilizzo di Adobe Identity Management System (IMS) per fornire il single sign-on in tutte le applicazioni cloud di Adobe.

* Preferenze utente che rimangono locali per ogni particolare istanza di AEM come Cloud Service.

## Interfaccia utente di authoring {#authoring-user-interface}

>[!NOTE]
>
>Per ulteriori dettagli, la [Operazioni di base](/help/sites-cloud/authoring/getting-started/basic-handling.md) è un buon punto di partenza.

I principi di base dell’interfaccia utente di authoring, sia per Sites che per Assets, saranno molto familiari per tutti coloro che hanno utilizzato AEM in passato.

La differenza principale consiste nel fatto che l’interfaccia utente è puramente touch; l’interfaccia classica non è più disponibile. In caso contrario, le nozioni di base rimangono invariate, con solo piccole modifiche apparenti.

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites as a Cloud Service consente di fornire ai clienti esperienze personalizzate basate su contenuti, combinando la potenza del sistema di gestione dei contenuti AEM con AEM gestione delle risorse digitali.

Per informazioni dettagliate, consulta la panoramica delle [Modifiche a Sites](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Cloud Service offre alle aziende una soluzione PaaS nativa per il cloud, che consente loro non solo di eseguire le operazioni di gestione delle risorse digitali e Dynamic Media in modo rapido ed efficace, ma anche di utilizzare funzionalità avanzate di nuova generazione, come AI/ML, dall’interno di un sistema sempre attuale, sempre disponibile e sempre in grado di apprendere.

L’offerta Assets include l’elaborazione delle risorse di nuova generazione nel cloud e l’acquisizione e la ricerca di risorse ad alte prestazioni.

Per informazioni dettagliate, consulta [panoramica e introduzione ad Assets as a Cloud Service](/help/assets/overview.md).

## Documentazione su Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

Per ulteriori informazioni, consulta:

* [Introduzione ad Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* [Architettura](/help/core-concepts/architecture.md) di Adobe Experience Manager as a Cloud Service
* [Modifiche di rilievo apportate ad AEM as a Cloud Service (Note sulla versione)](/help/release-notes/aem-cloud-changes.md)
* [Modifiche di rilievo apportate ad AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
* [Modifiche di rilievo apportate ad AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Introduzione ad AEM Assets as a Cloud Service](/help/assets/overview.md)
* [Tutorial su Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=it)
