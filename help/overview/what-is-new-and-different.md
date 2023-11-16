---
title: Differenze e novità - Adobe Experience Manager as a Cloud Service
description: Differenze e novità - Adobe Experience Manager (AEM) as a Cloud Service.
exl-id: d1ce126e-960c-4367-b741-af709dd81010
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 98%

---

# Novità e differenze {#what-is-new-and-what-is-different}

Da molti anni AEM è disponibile sia

* Locale

* as a Managed Service

Esistono differenze intrinseche tra gli approcci precedenti e AEM as a Cloud Service:

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
>Queste panoramiche non sono esaustive, sono concepite per fornire un’introduzione.

>[!NOTE]
>
>Per ulteriori dettagli sulle versioni On-Premise e Managed Service, consulta la documentazione di [AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it).

## Architettura {#architecture}

>[!NOTE]
>
>Per maggiori dettagli, consulta [Architettura](/help/overview/architecture.md).

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

AEM as a Cloud Service ora utilizza un approccio CI/CD (Continuous Integration/Continuous Delivery, integrazione continua e distribuzione continua), affinché tu possa lavorare sempre sui tuoi progetti con la versione più recente di AEM. Ciò significa che le istanze di produzione e staging vengono aggiornate alla versione più recente di AEM senza alcuna interruzione del servizio per gli utenti.

>[!NOTE]
>
>Se l’aggiornamento dell’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di staging. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, entrambi gli ambienti di staging e di produzione utilizzino la stessa versione di AEM.

Esistono due tipi di aggiornamenti delle versioni di AEM:

* **Aggiornamenti di manutenzione di AEM**

   * Possono essere rilasciati su base giornaliera.
   * Vengono utilizzati principalmente a scopo di manutenzione, e possono contenere le correzioni di bug e gli aggiornamenti di sicurezza più recenti.
   * Dal momento che le modifiche vengono applicate su base regolare, hanno un impatto minimo.

* **Aggiornamenti con nuove funzioni**

   * Vengono rilasciati in base a una pianificazione mensile prevedibile.

>[!TIP]
>
>Per maggiori dettagli, consulta [Aggiornamenti della versione di AEM](/help/implementing/deploying/aem-version-updates.md).

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager è parte integrante dell’approccio di aggiornamento continuo di AEM as a Cloud Service, in quanto controlla tutti gli aggiornamenti alle istanze - questo è obbligatorio.

Gli aggiornamenti possono essere attivati da Adobe quando è disponibile una nuova versione del servizio cloud. In alternativa, puoi attivare gli aggiornamenti dell’applicazione utilizzando le pipeline fornite da Cloud Manager.

Cloud Manager è:

* utilizzato per gestire programmi e ambienti AEM,

* un componente essenziale di AEM as a Cloud Service; per ogni nuovo tenant viene prima eseguito il provisioning per l’accesso a Cloud Manager,

* il punto di ingresso unico per il personale addetto alle operazioni e allo sviluppo.

In particolare, il numero e il tipo di programmi AEM che possono essere creati da Cloud Manager derivano da:

* contratto di licenza con il cliente,

* attori interni quando AEM as a Cloud Service è utilizzato per l’abilitazione o la formazione,

* processi guidati dall’esterno, ad esempio le prove avviate da Adobe.com.

Cloud Manager si è evoluto come portale self-service in cui è possibile creare e configurare i componenti principali di AEM as a Cloud Service:

* Creazione e gestione di nuovi programmi. Consulta [Informazioni su programmi e tipi di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) per ulteriori dettagli.

* Creazione e gestione degli ambienti AEM all’interno di questi programmi. Consulta [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md) per ulteriori dettagli.

* Creazione e gestione delle pipeline per la distribuzione del codice cliente e della relativa configurazione in un ambiente specifico. Consulta [Configurazione della pipeline CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) per ulteriori dettagli.

* Ricevere notifiche su importanti eventi del ciclo di vita per questi componenti (ad esempio, aggiornamenti dei prodotti).

Cloud Manager crea ambienti nei centri dati in molte aree geografiche, offrendo una copertura globale. I POP (Point of Presence) CDN garantiscono una distribuzione dei contenuti a bassa latenza per i clienti di tutto il mondo.


## Onboarding {#onboarding}

L’avvio e la gestione di un progetto AEM è semplice quando si utilizza AEM as a Cloud Service poiché Adobe è responsabile di molti aspetti:

* Le immagini AEM della linea di base sono ottimizzate per casi d’uso specifici.

* Molte delle attività di configurazione manuale sono state rese ridondanti.

È anche molto diverso in quanto ora esiste:

* Una fase di valutazione per garantire il rispetto di tutti i requisiti preliminari, compresi, ad esempio:

   * Requisiti legali

   * Accordi contrattuali

   * Requisiti tecnici per qualsiasi contenuto e/o codice esistente personalizzato dal cliente

* Requisiti di distribuzione:

   * Aggiornamenti del codice; tutte le applicazioni per clienti sviluppate per una versione precedente di AEM devono essere riviste ed eventualmente aggiornate.

   * Migrazione dei contenuti

>[!TIP]
>
>Per una panoramica completa del processo di onboarding, consulta [percorso di onboarding](/help/journey-onboarding/overview.md).

## Sviluppo {#developing}

>[!NOTE]
>
>Per ulteriori dettagli puoi iniziare con le [linee guida per lo sviluppo](/help/implementing/developing/introduction/development-guidelines.md) e [l’esercitazione WKND sullo sviluppo](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

La nuova architettura che supporta AEM as a Cloud Service comporta alcuni cambiamenti fondamentali nell’esperienza complessiva di sviluppo. Uno degli obiettivi principali per AEM as a Cloud Service è consentire ai clienti esperti (che hanno utilizzato AEM on-premise o nel contesto di Adobe Managed Services) di migrare ad AEM as a Cloud Service il più rapidamente possibile, senza dover riscrivere la maggior parte del codice personalizzato. Tuttavia, potrebbero essere ancora necessari alcuni adeguamenti.

### Sviluppo cloud {#aem-as-a-cloud-service-developing-cloud-development}

Per l’esecuzione delle applicazioni AEM esistenti su AEM as a Cloud Service, sono previsti i seguenti passaggi:

* Il codice e la configurazione dell’applicazione devono essere memorizzati nell’archivio del codice Git del programma Cloud Manager associato.
* Il codice e la configurazione dell’applicazione devono essere compatibili con la versione più recente dell’immagine AEM della linea di base (che potrebbe cambiare quotidianamente).
   * L’applicazione del cliente deve essere generata e distribuita utilizzando la pipeline di Cloud Manager associata all’ambiente Cloud Manager.
* L’applicazione del cliente deve superare tutti i gate di qualità del codice, sicurezza e prestazioni applicati nella pipeline.
* Le immagini create per l’applicazione del cliente devono essere distribuite dalla pipeline di Cloud Manager.

Questo processo è comunemente denominato sviluppo cloud-first. Poiché la durata end-to-end dovrebbe richiedere alcuni minuti (da 20 a 50 a seconda della complessità dell’applicazione), è necessario adottare metodologie di sviluppo rapido prima che le modifiche al codice e alla configurazione in sospeso vengano tentate nel cloud.

La console web, in cui vengono gestiti i bundle OSGi e la relativa configurazione associata, e in precedenza parte di AEM QuickStart, non è più disponibile in AEM as a Cloud Service. La nuova console per sviluppatori fornisce un’interfaccia di sola lettura per la maggior parte delle informazioni di runtime. Con questa console, gli sviluppatori possono selezionare e accedere direttamente a qualsiasi nodo particolare di un servizio di authoring o pubblicazione e visualizzare le informazioni pertinenti.

>[!NOTE]
>
>Consulta anche [Configurazione OSGi](/help/implementing/deploying/overview.md#osgi-configuration)

Un altro requisito comune per gli sviluppatori è l’accesso rapido ai file di registro dei vari ambienti. Con AEM as a Cloud Service, i file di registro dei diversi nodi di authoring e pubblicazione sono resi disponibili tramite Cloud Manager, sotto forma di file che possono essere scaricati o tramite API.

A causa della netta separazione di codice e contenuto, gli sviluppatori possono utilizzare un particolare processo per aggiornare il contenuto come parte di una distribuzione. I casi d’uso tipici per i contenuti modificabili sono:

* Contenuto standard *predefinito* che fa parte del progetto del cliente (ad esempio cartelle, modelli, flussi di lavoro, ecc.)

* Definizioni degli indici di ricerca

* ACL e autorizzazioni

* Utenti e gruppi di utenti del servizio

### Sviluppo locale {#aem-as-a-cloud-service-developing-local-development}

Per supportare le iterazioni e lo sviluppo rapidi, è anche possibile sviluppare applicazioni AEM al di fuori del contesto di AEM as a Cloud Service. A questo scopo, gli sviluppatori possono accedere ai seguenti artefatti:

* QuickStart AEM as a Cloud Service: un’installazione indipendente basata su `.jar` della base di codice AEM più recente, con la stessa superficie funzionale e API.

* SDK del Dispatcher AEM as a Cloud Service: un processo basato su immagini per testare e convalidare localmente le configurazioni di Dispatcher

>[!NOTE]
>
>È opportuno notare che Cloud QuickStart non consente tutte le funzionalità di AEM Sites e AEM Assets. È costituito da un semplice ambiente di authoring in cui è possibile sviluppare e testare la maggior parte delle estensioni.

## Operazioni e prestazioni {#operations-and-performance}

>[!NOTE]
>
>Per maggiori dettagli, inizia con [ripristino dei contenuti](/help/operations/backup.md), [Indicizzazione](/help/operations/indexing.md), e [altre attività di manutenzione](/help/operations/maintenance.md).

Con AEM as a Cloud Service, tali operazioni sono automatizzate in modo che qualsiasi interruzione del servizio non sia più necessaria.

In questi settori:

* Molte attività sono state automatizzate.

* Le topologie sono ottimizzate per la massima resilienza ed efficienza. Ad esempio, la replica senza binari è l’impostazione predefinita.

* Le attività a carico pesante, come le code, i lavori e le attività di elaborazione in blocco, sono state spostate fuori dall’istanza di AEM principale per essere gestite da microservizi condivisi e dedicati.

Le operazioni per AEM as a Cloud Service sono inoltre supportate da una nuova infrastruttura di monitoraggio, reporting e avvisi. Questo consente agli SRE (Site Reliability Engineers) di Adobe di mantenere il servizio in modo proattivo. I vari elementi dell’architettura sono dotati di una varietà di controlli sanitari. Se, per qualche motivo, un particolare nodo dell’architettura è considerato non sano, allora viene rimosso dal servizio e sostituito senza avviso con un nuovo, sano.

## Gestione identità {#identity-management}

>[!NOTE]
>
>Per maggiori dettagli, consulta [Sicurezza - Supporto IMS](/help/security/ims-support.md).

Una modifica importante per AEM as a Cloud Service è l’utilizzo completamente integrato degli Adobe ID per accedere al livello di authoring.

A tal fine è necessario utilizzare [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Gli account utente consentono agli utenti di accedere ai prodotti e ai servizi di Adobe, in quanto le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS) per essere condivise in tutti i servizi cloud. Una volta assegnato l’accesso a AEM, gli account utente possono essere referenziati in AEM as a Cloud Service (come prima), ad esempio per la definizione di ruoli e autorizzazioni dalle interfacce utente di AEM Security.

Questo combina i vantaggi dell’

* Utilizzo di Adobe Identity Management System (IMS) per fornire l’accesso singolo per tutte le applicazioni cloud di Adobe.

* Preferenze utente che rimangono locali per ogni particolare istanza di AEM as a Cloud Service.

## Interfaccia utente di authoring {#authoring-user-interface}

>[!NOTE]
>
>Per maggiori dettagli, [Operazioni di base](/help/sites-cloud/authoring/getting-started/basic-handling.md) è un buon punto di partenza.

I principi di base dell’interfaccia utente di authoring, sia per Sites che per Assets, saranno familiari per tutti coloro che hanno utilizzato AEM in passato.

La differenza principale consiste nel fatto che l’interfaccia utente è puramente touch, l’interfaccia classica non è più disponibile. In caso contrario, le nozioni di base rimangono invariate, con solo piccole modifiche apparenti.

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites as a Cloud Service consente di offrire ai clienti esperienze personalizzate basate su contenuti, combinando la potenza del sistema di gestione dei contenuti AEM con la gestione delle risorse digitali AEM.

Per ulteriori informazioni, consulta la panoramica di [Modifiche a Sites](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Cloud Service offre una soluzione PaaS nativa per il cloud, che consente alle aziende di eseguire le operazioni di gestione delle risorse digitali e Dynamic Media in modo rapido ed efficace, ma anche di utilizzare funzionalità avanzate di nuova generazione, come AI/ML, dall’interno di un sistema sempre attuale, disponibile e in grado di apprendere.

L’offerta Assets include l’elaborazione delle risorse di nuova generazione nel cloud e l’acquisizione e la ricerca di risorse ad alte prestazioni.

Per maggiori dettagli, consulta [Panoramica e introduzione di Assets as a Cloud Service](/help/assets/overview.md).

## Documentazione su Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

Per ulteriori informazioni, consulta:

* [Introduzione ad Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* [Architettura](/help/overview/architecture.md) di Adobe Experience Manager as a Cloud Service
* [Modifiche di rilievo apportate ad AEM as a Cloud Service (Note sulla versione)](/help/release-notes/aem-cloud-changes.md)
* [Modifiche di rilievo apportate ad AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
* [Modifiche di rilievo apportate ad AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Introduzione a AEM Assets as a Cloud Service](/help/assets/overview.md)
* [Tutorial su Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=it)

>[!TIP]
>
>Una volta acquisite le nozioni generali su AEM as a Cloud Service, per iniziare in breve tempo a utilizzarlo segui il [Percorso di onboarding](/help/journey-onboarding/overview.md).
>
>Hai già iniziato a utilizzarlo, oppure vuoi iniziare a testare le funzionalità di AEM? Installa [AEM Reference Demos Add-On](/help/journey-sites/demos-add-on/overview.md) per esplorare le potenti funzioni di AEM utilizzando esempi articolati.
