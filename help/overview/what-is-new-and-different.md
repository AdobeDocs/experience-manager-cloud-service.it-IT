---
title: Cosa è diverso e cosa è nuovo - Adobe Experience Manager come Cloud Service
description: 'Che cosa è diverso e che cosa è nuovo - Adobe Experience Manager (AEM) come Cloud Service. '
translation-type: tm+mt
source-git-commit: 338f4b8d291bd0dca1c2f0de7bd6f721156d8df9
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 9%

---


# Novità e differenze {#what-is-new-and-what-is-different}

Per molti anni AEM sono disponibili entrambi:

* Locale

* come servizio gestito

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
>Tali panorami non sono esaustivi, ma mirano a fornire un&#39;introduzione.

>[!NOTE]
>
>Per ulteriori dettagli sulle versioni locale e del servizio gestito, consultate la documentazione impostata per [AEM 6.5](https://helpx.adobe.com/it/support/experience-manager/6-5.html).

## Architettura {#architecture}

>[!NOTE]
>
>Per ulteriori dettagli vedere [Architettura](/help/core-concepts/architecture.md).

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


## Aggiornamenti {#upgrades}

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Introduzione](/help/implementing/deploying/overview.md)alla distribuzione.

AEM come Cloud Service utilizza ora l&#39;integrazione continua e la fornitura continua (CI/CD) per garantire che i progetti siano nella versione AEM più recente. Ciò significa che tutte le operazioni di aggiornamento sono completamente automatizzate, pertanto non è necessaria alcuna interruzione del servizio per gli utenti.

>[!NOTE]
>Se l&#39;aggiornamento all&#39;ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l&#39;ambiente dell&#39;area di visualizzazione. Questa operazione viene eseguita automaticamente per essere certi che, al termine di un aggiornamento, sia gli ambienti di fase che quelli di produzione siano sulla stessa versione AEM.

AEM aggiornamenti delle versioni sono di due tipi:

* **Aggiornamenti push**

   * Può essere rilasciato su base giornaliera.
   * La maggior parte delle attività di manutenzione, incluse le correzioni di bug più recenti e gli aggiornamenti della sicurezza.

   Poiché le modifiche vengono applicate regolarmente, l&#39;impatto è incrementale, riducendo l&#39;impatto sul servizio.

>[!NOTE]
>Per ulteriori informazioni AEM aggiornamenti push, consulta il white paper su [Adobe Experience Manager come modello di distribuzione continua Cloud Service](https://fieldreadiness-adobe.highspot.com/items/5ea322e1c714336c23b32599#2)

* **Aggiornamenti delle nuove funzioni**

   * Rilasciato tramite un programma mensile prevedibile.

AEM aggiornamenti passano attraverso un ciclo di convalida del prodotto intenso e completamente automatizzato, che prevede più passaggi per garantire l&#39;assenza di interruzioni del servizio per i sistemi in produzione. I controlli sanitari sono utilizzati per monitorare lo stato della domanda. Se questi controlli non vengono eseguiti durante un AEM come aggiornamento del Cloud Service, il rilascio non verrà completato e  Adobe verificherà perché l&#39;aggiornamento ha causato questo comportamento imprevisto.

[I test di prodotto e i test](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) funzionali dei clienti che impediscono agli aggiornamenti di prodotto e ai suggerimenti sul codice cliente di interrompere la produzione vengono convalidati anche durante un aggiornamento AEM versione.

>[NOTA]
>Se il codice personalizzato è stato messo in staging e successivamente rifiutato dall&#39;utente, il successivo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag git dell&#39;ultima release cliente riuscita alla produzione.


### Archivio nodi composito {#composite-node-structure}

Come già detto, gli aggiornamenti nella maggior parte dei casi non generano tempi di inattività, anche per l&#39;autore, che è un cluster di nodi.

Gli aggiornamenti Rolling sono possibili a causa della funzione *composito archivio* nodi in Oak. Questa funzione consente AEM fare riferimento a più repository contemporaneamente. In una distribuzione continuativa, la nuova versione di AEM verde contiene il proprio `/libs`, ovvero il repository immutabile basato su TarMK), distinto dalla versione precedente di AEM Blu, anche se entrambi fanno riferimento a un repository mutabile basato su DocumentMK condiviso che contiene aree come `/content` , `/conf` , `/etc` e altri. Poiché sia il blu che il verde hanno versioni proprie di `/libs`, possono essere entrambi attivi durante l&#39;aggiornamento continuo, assumendo entrambi il traffico fino a quando il blu non viene completamente sostituito dal verde.

## Cloud Manager {#cloud-manager}

 Adobe Cloud Manager è integrato nell&#39;approccio di aggiornamento continuo di AEM come Cloud Service, in quanto controlla tutti gli aggiornamenti delle istanze - questo è obbligatorio.

Gli aggiornamenti possono essere attivati da  Adobe quando è disponibile una nuova versione del servizio cloud. In alternativa, puoi attivare gli aggiornamenti dell&#39;applicazione utilizzando le pipeline fornite da Cloud Manager.

Cloud Manager è:

* utilizzati per gestire programmi e ambienti AEM,

* un componente essenziale di AEM come Cloud Service; per ogni nuovo tenant viene eseguito il primo provisioning per l&#39;accesso a Cloud Manager,

* il punto di ingresso unico per il personale addetto alle operazioni e allo sviluppo.

Nello specifico, il numero e il tipo di programmi AEM che è possibile creare da Cloud Manager è derivato:

* dal contratto di licenza con il cliente,

* da attori interni quando AEM come Cloud Service è utilizzato per l&#39;abilitazione, o

* da processi guidati dall&#39;esterno, come le sperimentazioni avviate da  Adobe.com.

Cloud Manager si è evoluto come portale self-service in cui è possibile creare e configurare i componenti principali di AEM come Cloud Service:

* Creazione e gestione di nuovi programmi. Per ulteriori informazioni, consulta [Informazioni sui programmi e i tipi](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) di programmi.

* Creazione e gestione degli ambienti AEM all&#39;interno di questi programmi. Per ulteriori informazioni, consulta [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md) .

* Creazione e gestione delle tubazioni per distribuire il codice cliente e la configurazione correlata a un ambiente specifico. Per ulteriori informazioni, vedere [Configurazione della tubazione](/help/implementing/cloud-manager/configure-pipeline.md) CI-CD.

* Essere informati di importanti eventi del ciclo di vita per questi componenti (ad esempio, aggiornamenti dei prodotti).

Attualmente Cloud Manager è in grado di creare ambienti in 3 aree geografiche (con più aree geografiche):

* Stati Uniti (est)

* EMEA (Paesi Bassi)

* APAC (Australia)

>[!NOTE]
>Per iniziare a utilizzare Cloud Manager in AEM come Cloud Service, fai riferimento a [Accesso  Experience Manager](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md) .

## Onboarding {#onboarding}

>[!NOTE]
>
>Per ulteriori dettagli, consultate [Onboarding](/help/onboarding/home.md).

L&#39;avvio e la gestione di un progetto AEM è semplice quando si utilizza AEM come servizio Cloud come  Adobe è responsabile di molti aspetti:

* Le immagini della AEM di base sono ottimizzate per casi di utilizzo specifici.

* Molte delle attività di configurazione manuale sono state ridondanti.

È anche molto diverso in quanto esiste ora:

* una fase di valutazione per garantire che tutti i prerequisiti siano stati soddisfatti; , ad esempio:

   * Obblighi legali

   * Accordi contrattuali

   * Requisiti tecnici per qualsiasi contenuto e/o codice esistente personalizzato dal cliente

* Requisiti di distribuzione:

   * Aggiornamenti del codice; tutte le applicazioni dei clienti sviluppate per una versione precedente di AEM dovranno essere riviste ed eventualmente aggiornate.

   * Migrazione dei contenuti

## Sviluppo {#developing}

>[!NOTE]
>
>Per ulteriori dettagli è possibile iniziare con [Linee guida](/help/implementing/developing/introduction/development-guidelines.md) per lo sviluppo e [lo sviluppo - Esercitazione](/help/implementing/developing/introduction/develop-wknd-tutorial.md)WKND.

La nuova architettura che supporta AEM come Cloud Service comporta alcuni cambiamenti fondamentali nell&#39;esperienza di sviluppo complessiva. Uno degli obiettivi principali per AEM come Cloud Service è quello di consentire ai clienti esperti (che hanno utilizzato AEM locale o nel contesto dei servizi gestiti Adobe) di migrare il più rapidamente possibile a AEM, senza dover riscrivere la maggior parte del codice personalizzato. Tuttavia, potrebbero essere ancora necessari alcuni adeguamenti.

### Sviluppo cloud {#aem-as-a-cloud-service-developing-cloud-development}

Per l&#39;esecuzione delle applicazioni AEM esistenti su AEM come Cloud Service, è previsto quanto segue:

* Il codice e la configurazione dell&#39;applicazione devono essere memorizzati nell&#39;archivio del codice Git del programma Cloud Manager associato.
* Il codice e la configurazione dell&#39;applicazione devono essere compatibili con l&#39;ultima versione dell&#39;immagine AEM linea di base (che potrebbe essere modificata ogni giorno).
   * L&#39;applicazione del cliente deve essere creata e distribuita utilizzando la pipeline di Cloud Manager associata all&#39;ambiente Cloud Manager.
* L&#39;applicazione del cliente deve superare tutti i cancelli di qualità del codice, sicurezza e prestazioni applicati nella pipeline.
* Le immagini create per l&#39;applicazione cliente devono essere distribuite dalla pipeline di Cloud Manager.

Questo processo viene comunemente definito sviluppo per il cloud. Poiché la durata end-to-end dovrebbe richiedere alcuni minuti (da 20 a 50 a seconda della complessità dell&#39;applicazione), è necessario adottare metodologie di sviluppo rapido prima che le modifiche al codice in sospeso e alla configurazione siano tentate nel cloud.

La console Web, in cui vengono gestiti i bundle OSGI e la configurazione associata, e in precedenza parte di AEM QuickStart, non è più direttamente accessibile agli utenti di un AEM come ambiente Cloud Service. Questa interfaccia è ancora accessibile in modalità di sola lettura tramite una nuova console per sviluppatori. Con questa console, gli sviluppatori possono selezionare e accedere direttamente a qualsiasi nodo particolare di un servizio di creazione o pubblicazione, quindi accedere alle aree bloccate per impostazione predefinita.

>[!NOTE]
>
>Vedere anche Configurazione [OSGi](/help/implementing/deploying/overview.md#osgi-configuration)

Un altro requisito comune per gli sviluppatori è l&#39;accesso rapido ai file di registro dei vari ambienti. Ad Cloud Service, AEM i file di registro dei diversi nodi dei nodi di creazione e pubblicazione sono disponibili tramite Cloud Manager, sia sotto forma di file che possono essere scaricati, sia tramite API.

A causa della netta separazione tra codice e contenuto, gli sviluppatori possono utilizzare un particolare processo per aggiornare il contenuto come parte di una distribuzione. I casi di utilizzo tipici per i contenuti modificabili sono:

* Contenuto standard *predefinito* che fa parte del progetto del cliente (ad esempio, cartelle, modelli, flussi di lavoro ecc.)

* Cerca definizioni indice

* ACL e autorizzazioni

* Utenti e gruppi di utenti del servizio

### Sviluppo locale {#aem-as-a-cloud-service-developing-local-development}

Al fine di sostenere le fasi e lo sviluppo rapidi, è anche possibile sviluppare applicazioni AEM al di fuori del AEM come contesto Cloud Service. A tal fine, gli sviluppatori possono accedere ai seguenti artifact:

* La AEM come Cloud Service QuickStart: un programma di installazione autonomo `.jar` basato sulla più recente base di codice AEM, con la stessa superficie funzionale e API.

* Il AEM come SDK del dispatcher di Cloud Service: un processo basato su immagini per testare e convalidare localmente le configurazioni del dispatcher

>[!NOTE]
>
>È opportuno notare che la Guida rapida di Cloud non consente tutte  funzionalità AEM Sites e  AEM Assets. È costituito da un semplice ambiente di authoring in cui la maggior parte delle estensioni può essere sviluppata e testata.

## Operazioni e prestazioni {#operations-and-performance}

>[!NOTE]
>
>Per ulteriori dettagli, inizia da [Backup](/help/operations/backup.md), [Indicizzazione](/help/operations/indexing.md) e [altre attività di manutenzione](/help/operations/maintenance.md).

Con AEM come Cloud Service, tali operazioni sono automatizzate in modo che non sia più necessario interrompere il servizio.

In questi settori:

* Molte attività sono state automatizzate.

* Le topologie sono ottimizzate per la massima resilienza ed efficienza; ad esempio, la replica binaryless è l&#39;impostazione predefinita.

* Le attività con un carico elevato, come code, processi e attività di elaborazione in blocco, sono state spostate dall&#39;istanza principale AEM per essere gestite da micro-servizi condivisi e dedicati.

Le operazioni per AEM come Cloud Service sono inoltre supportate da una nuova infrastruttura di monitoraggio, reporting e avvisi. Questo consente agli SRE del Adobe  (Site Reliability Engineers) di mantenere il servizio in modo proattivo. I vari elementi dell&#39;architettura sono dotati di una varietà di controlli sanitari. Se, per qualche motivo, un particolare nodo dell&#39;architettura è considerato malsano, allora viene rimosso dal servizio e sostituito silenziosamente con uno nuovo, sano.

## Gestione identità {#identity-management}

>[!NOTE]
>
>Per ulteriori dettagli, consultate [Sicurezza - Supporto](/help/security/ims-support.md)IMS.

Un cambiamento importante nell’AEM come Cloud Service è l’uso completamente integrato di  ID Adobe per accedere al livello di authoring.

Ciò richiede l&#39;utilizzo della console [di amministrazione del](https://helpx.adobe.com/it/enterprise/using/admin-console.html) Adobe per la gestione di utenti e gruppi di utenti. Gli account utente consentono agli utenti di accedere  prodotti e servizi del Adobe, poiché le informazioni del profilo utente sono centralizzate nel Adobe   Identity Management System (IMS) da condividere tra tutti i servizi cloud. Una volta assegnato l&#39;accesso a AEM, gli account utente possono essere AEM come un Cloud Service (come prima); ad esempio, per definire ruoli e autorizzazioni dalle interfacce utente di AEM Security.

Questo combina i vantaggi di:

* Utilizzo del Adobe   Identity Management System (IMS) per fornire single sign-on in tutte  applicazioni cloud Adobe.

* Preferenze utente che rimangono locali per ogni particolare istanza di AEM come Cloud Service.

## Interfaccia utente di authoring {#authoring-user-interface}

>[!NOTE]
>
>Per ulteriori dettagli, la [gestione](/help/sites-cloud/authoring/getting-started/basic-handling.md) di base è un buon punto di partenza.

I principi di base dell’interfaccia utente di authoring, sia per Siti che per Risorse, saranno molto familiari a chiunque abbia utilizzato AEM in passato.

La differenza principale sta nel fatto che l’interfaccia è completamente touch; l’interfaccia classica non è più disponibile. In caso contrario, le nozioni di base rimangono invariate, con solo piccole modifiche apparenti.

## AEM Sites {#aem-sites}

 Adobe Experience Manager Sites come Cloud Service consente di offrire ai clienti esperienze personalizzate basate su contenuti, combinando la potenza del sistema di gestione dei contenuti AEM con AEM Digital Asset Management.

Per informazioni dettagliate, consultate la panoramica delle [modifiche ai siti](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets come Cloud Service offre una soluzione SaaS nativa per il cloud, che consente alle aziende non solo di eseguire le operazioni Digital Asset Management e Dynamic Media con velocità ed impatto, ma anche di utilizzare funzionalità intelligenti di nuova generazione, come AI/ML, da un sistema sempre attuale, sempre disponibile e sempre in grado di apprendere.

L’offerta di risorse include l’elaborazione di risorse di nuova generazione nel cloud e l’acquisizione e la ricerca di risorse ad alte prestazioni.

Per informazioni dettagliate, consultate [panoramica e introduzione alle risorse come Cloud Service](/help/assets/overview.md).

## Documentazione su Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

Per ulteriori informazioni, consulta:

* [Introduzione ad Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* [Architettura](/help/core-concepts/architecture.md) di Adobe Experience Manager as a Cloud Service
* [Modifiche di rilievo apportate ad AEM as a Cloud Service (Note sulla versione)](/help/release-notes/aem-cloud-changes.md)
* [Modifiche di rilievo apportate ad AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
* [Modifiche di rilievo apportate ad AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Presentazione  AEM Assets come Cloud Service](/help/assets/overview.md)
* [Esercitazioni su Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)
