---
title: Introduzione all'architettura di Adobe Experience Manager come servizio cloud
description: 'Introduzione all''architettura di Adobe Experience Manager come servizio cloud. '
translation-type: tm+mt
source-git-commit: 5a846d34ee094e7d2f7fc71dbeef65f3fa58e86c

---


# Introduzione all&#39;architettura di Adobe Experience Manager come servizio cloud {#an-introduction-to-the-architecture-adobe-experience-manager-as-a-cloud-service}

Adobe Experience Manager (AEM) come servizio Cloud ha apportato delle modifiche all&#39;architettura.

## Ridimensionamento {#scaling}

AEM come servizio cloud ora include:

* Architettura dinamica con un numero variabile di immagini AEM.

![Architettura](assets/concepts-01.png "dinamicaArchitettura dinamica")

Questa architettura:

* Viene ridimensionata in base al traffico *effettivo* e all&#39;attività *effettiva* .

* Presenta istanze singole che vengono eseguite solo quando necessario.

* Utilizza applicazioni modulari.

* dispone di un cluster di autori come predefinito; in questo modo si evita il tempo di inattività per le attività di manutenzione.

Questo consente di ridimensionare automaticamente i diversi pattern di utilizzo:

![Ridimensionamento automatico per diversi](assets/concepts-02.png "pattern di utilizzoRidimensionamento automatico per diversi pattern di utilizzo")

A tal fine, tutte le istanze di AEM come servizio cloud vengono create uguali, ciascuna con le stesse caratteristiche di ridimensionamento predefinite in termini di numero di nodi, memoria allocata e capacità di elaborazione allocata.

AEM come servizio cloud si basa sull’utilizzo di un motore di orchestrazione che:

* Controlla costantemente lo stato del servizio.

* ridimensiona dinamicamente ciascuna istanza del servizio in base alle esigenze effettive; ingrandire o ridurre, a seconda delle necessità.

Questo:

* È applicabile al numero di nodi, alla quantità di memoria e alla capacità della CPU allocata su ciascun nodo.

* Consente ad AEM come servizio Cloud di adattarsi ai pattern di traffico mano a mano che cambiano.

Il ridimensionamento delle istanze per tenant del servizio può essere automatico o manuale, sui due assi:

* Verticale: la memoria e la capacità della CPU allocata possono essere ridimensionate per un numero fisso di nodi.

* Orizzontale: il numero di nodi per un determinato servizio può essere aumentato o diminuito.

## Ambienti {#environments}

>[!NOTE]
>
> Per ulteriori informazioni, vedere [Distribuzione - Modalità di esecuzione](/help/implementing/deploying/overview.md#runmodes)

AEM come servizio cloud è disponibile come istanza singola con ogni istanza che rappresenta un ambiente AEM completo. Con AEM come servizio cloud sono disponibili quattro tipi di ambienti:

* **Ambiente** di produzione: ospita le applicazioni per i professionisti.

* **Ambiente** stage: è sempre associato a un unico ambiente di produzione in una relazione 1:1. L&#39;ambiente stage viene utilizzato per vari test di prestazioni e qualità prima che le modifiche all&#39;applicazione vengano inviate all&#39;ambiente di produzione.

* **Ambiente** di sviluppo: consente agli sviluppatori di implementare le applicazioni AEM nelle stesse condizioni di runtime degli ambienti di fase e produzione.

* **Ambiente** dimostrativo: può essere utilizzato a scopo di valutazione, dimostrazione, prototipazione e formazione.

Gli ambienti di sviluppo e dimostrazione sono spesso definiti ambienti *non di produzione* .

## Programmi {#programs}

Qualsiasi nuovo progetto AEM è sempre associato a un&#39;unica base di codice specifica, in cui puoi memorizzare sia la configurazione che il codice personalizzato per il progetto. Queste informazioni sono memorizzate in un archivio di codice, accessibili tramite i consueti client Git, messi a disposizione al momento della creazione di nuovi programmi.

Un programma AEM è il contenitore che include:

|  Elemento del programma |  Numero |
|--- |--- |
| Repository dei codici (Git) |  1 |
| Immagine della linea di base (Siti o Risorse) |  1 |
| Set di ambienti di fase e produzione (1:1) | 0 o 1 |
| Ambienti non di produzione (sviluppo o dimostrazione) | 0 a N |
| Pipeline per ogni ambiente | 0 o 1 |

Per AEM come servizio cloud sono inizialmente disponibili due tipi di programmi:

* Servizio AEM Cloud Sites

* Servizio AEM Cloud Assets

Entrambi consentono l&#39;accesso a una serie di funzioni e funzionalità. Il livello autore conterrà tutte le funzionalità Siti e Risorse per tutti i programmi, ma per impostazione predefinita i programmi Risorse non avranno un livello di pubblicazione.

## Architettura runtime {#runtime-architecture}

Questa nuova architettura presenta diversi componenti principali:

<!--- needs reworking -->

![AEM come servizio cloud -](assets/concepts-03.png "Architettura del runtimeAEM come servizio cloud - Architettura del runtime")

* Per AEM Sites come servizio cloud:

   * Per ogni ambiente (ad alto livello) continua ad esistere il concetto di livello di authoring e di livello di pubblicazione.

   * Il livello di authoring è composto da due o più nodi all’interno di un singolo cluster di autori. Viene ridimensionato automaticamente in base all’attività di authoring.

      * Gli autori o i creatori dei contenuti accedono al livello di creazione di AEM per creare, modificare e gestire i contenuti.

      * L&#39;accesso al livello di authoring è gestito da Adobe Identity Management Services (IMS).

      * L’integrazione e l’elaborazione delle risorse utilizzano un servizio di elaborazione risorse dedicato.
   * Il livello di pubblicazione è composto da due o più nodi all’interno di una singola farm di pubblicazione: possono operare indipendentemente l&#39;uno dall&#39;altro. Ogni nodo è costituito da un editore AEM e da un server Web dotato del modulo AEM Dispatcher. Viene ridimensionato automaticamente in base alle esigenze di traffico del sito.

      * Gli utenti finali o i visitatori del sito visitano il sito Web tramite AEM Publish Service.


* Per Risorse AEM come servizio Cloud:

   * L&#39;architettura include solo un ambiente di authoring.

* Sia il livello di creazione che il livello di pubblicazione leggono e persistono il contenuto da/a un servizio Content Repository.

   * Il livello di pubblicazione legge solo il contenuto dal livello di persistenza.

   * Il livello di authoring legge e scrive il contenuto da e verso il livello di persistenza.

   * L’archiviazione BLOB è condivisa tra il livello di pubblicazione e l’autore; i file non vengono *spostati*.

   * Quando il contenuto viene approvato dal livello di authoring, ciò indica che può essere attivato, quindi inviato al livello di persistenza del livello di pubblicazione. Ciò avviene tramite il servizio di replica, una pipeline middleware. Questa pipeline riceve il nuovo contenuto, con i singoli nodi del servizio di pubblicazione che si iscrivono al contenuto inviato alla pipeline.

      >[!NOTE]
      >
      >For more details see [Replication](/help/operations/replication.md).

   * Sviluppatori e amministratori gestiscono AEM come applicazione di servizio cloud utilizzando un servizio di integrazione continua/consegna continua (CI/CD), reso disponibile tramite [Cloud Manager](/help/overview/what-is-new-and-different.md#cloud-manager). Ciò include distribuzioni di codice e configurazione tramite la pipeline CI/CD di Cloud Manager. Tutto ciò che riguarda il monitoraggio, la manutenzione e la risoluzione dei problemi (ad esempio, i file di registro) è esposto ai clienti in Cloud Manager.

   * L’accesso ai livelli di creazione e pubblicazione avviene sempre tramite un sistema di bilanciamento del carico. Questo è sempre aggiornato con i nodi attivi in ciascuno dei livelli.

   * Per il livello di pubblicazione, come primo punto di ingresso è disponibile anche un servizio CDN (Continuous Delivery Network).

* Per le istanze dimostrative di AEM come servizio cloud, l&#39;architettura viene semplificata a un singolo nodo di authoring. Pertanto non presenta tutte le caratteristiche dello sviluppo, della fase o dell&#39;ambiente di produzione standard. Ciò significa anche che possono verificarsi dei tempi di inattività e che non è possibile supportare le operazioni di backup e ripristino.

## Architettura di distribuzione {#deployment-architecture}

Cloud Manager gestisce tutti gli aggiornamenti alle istanze di AEM come servizio Cloud. È obbligatorio, in quanto unico modo per creare, testare e distribuire l’applicazione del cliente, sia per l’autore che per i livelli di pubblicazione. Questi aggiornamenti possono essere attivati da Adobe, quando è pronta una nuova versione del servizio AEM Cloud o dal Cliente, quando è pronta una nuova versione della loro applicazione.

Tecnicamente, questo è implementato a causa del concetto di una pipeline di distribuzione, accoppiata a ogni ambiente all&#39;interno di un programma. Quando una pipeline di Cloud Manager è in esecuzione, crea una nuova versione dell&#39;applicazione cliente, sia per l&#39;autore che per i livelli di pubblicazione. Questo si ottiene combinando i pacchetti cliente più recenti con l&#39;immagine Adobe di base più recente. Quando le nuove immagini vengono create e testate correttamente, Cloud Manager automatizza completamente il ritaglio alla versione più recente dell&#39;immagine aggiornando tutti i nodi di servizio utilizzando un pattern di aggiornamento continuo. Ciò non comporta tempi di inattività né per l’autore né per il servizio di pubblicazione.

<!--- needs reworking -->

![AEM come servizio cloud -](assets/concepts-04.png "Architettura di distribuzioneAEM come servizio cloud - Architettura di distribuzione")

## Distribuzione dei contenuti {#content-distribution}

Adobe Experience Manager come servizio Cloud ha modificato il funzionamento della pubblicazione dei contenuti. Con AEM come servizio cloud, il framework di replica delle versioni precedenti di AEM non viene più utilizzato per pubblicare le pagine (le modifiche vengono spostate dall’istanza di creazione alle istanze di pubblicazione).

AEM come servizio cloud ora utilizza la funzionalità di distribuzione [dei contenuti](https://sling.apache.org/documentation/bundles/content-distribution.html) Sling per spostare il contenuto appropriato. Questo utilizza un servizio pipeline eseguito su Adobe I/O, che si trova al di fuori del runtime AEM.

La configurazione è automatizzata, inclusa l&#39;autoconfigurazione automatica quando i nodi di pubblicazione vengono aggiunti, rimossi o riciclati durante il runtime.

Una singola richiesta di pubblicazione o di annullamento della pubblicazione può includere più risorse, ma restituirà un singolo stato applicato a tutti; avrà esito positivo per tutte le risorse nel servizio AEM Publish o avrà esito negativo per tutti. In questo modo le risorse all’interno di AEM Publish Service non si troveranno mai in uno stato incoerente.

**Diagramma dell&#39;architettura di distribuzione dei contenuti di alto livello**

![Architettura di distribuzione dei contenuti di alto livello](assets/architecture-diagram.png "Diagramma dell&#39;architettura di distribuzione dei contenuti di alto livello")

## Evoluzioni chiave {#key-evolutions}

La nuova architettura di AEM come servizio cloud introduce alcune modifiche e innovazioni fondamentali rispetto alle generazioni precedenti:

* Tutti i file (BLOB) vengono caricati e serviti direttamente da un archivio dati cloud. Il flusso di bit associato non passa mai attraverso la JVM dei servizi AEM Author e Publish. Di conseguenza, i nodi dei servizi di creazione e pubblicazione di AEM possono avere dimensioni più ridotte e essere più compatibili con l’aspettativa di una rapida scalabilità automatica. Per i professionisti del settore, questo consente un&#39;esperienza più rapida durante il caricamento e il download di immagini, video ecc.

* Tutte le operazioni che consistono nella pubblicazione di contenuto ora includono una pipeline che segue un pattern di sottoscrizione. Il contenuto pubblicato viene inviato a varie code nella pipeline, alle quali tutti i nodi del servizio di pubblicazione sottoscrivono. Di conseguenza, il livello di authoring non deve essere a conoscenza del numero di nodi nel servizio di pubblicazione; questo consente di ridimensionare automaticamente rapidamente il livello di pubblicazione.

* Il concetto di master dorato è stato introdotto per automatizzare il ciclo di vita dei nodi di pubblicazione. Il master golden è un nodo di pubblicazione specializzato, a cui nessun utente finale accede e da cui vengono creati tutti i nodi del servizio di pubblicazione. Le operazioni di manutenzione, come la compattazione, vengono eseguite nell’archivio dei contenuti collegato al master d’oro. I nodi di pubblicazione vengono riciclati ogni giorno e non richiedono alcun tipo di manutenzione ordinaria; in passato tale manutenzione richiedeva alcuni tempi di inattività, in particolare per l’istanza di authoring.

* L&#39;architettura separa completamente il contenuto dell&#39;applicazione dal codice e dalla configurazione dell&#39;applicazione. Tutto il codice e la configurazione sono praticamente immutabili e vengono inseriti nell’immagine di base utilizzata per creare i vari nodi dei servizi di creazione e pubblicazione. Di conseguenza, esiste una garanzia assoluta che ogni nodo sia identico e che le modifiche al codice e alla configurazione possano essere apportate solo a livello globale eseguendo una pipeline di Cloud Manager.
