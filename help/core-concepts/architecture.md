---
title: Introduzione all’architettura di Adobe Experience Manager as a Cloud Service
description: 'Introduzione all’architettura di Adobe Experience Manager as a Cloud Service. '
translation-type: tm+mt
source-git-commit: 5a846d34ee094e7d2f7fc71dbeef65f3fa58e86c
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 100%

---


# Introduzione all’architettura di Adobe Experience Manager as a Cloud Service {#an-introduction-to-the-architecture-adobe-experience-manager-as-a-cloud-service}

Adobe Experience Manager (AEM) as a Cloud Service ha apportato delle modifiche all’architettura.

## Ridimensionamento {#scaling}

AEM as a Cloud Service adesso include:

* Architettura dinamica con un numero variabile di immagini AEM

![Architettura dinamica](assets/concepts-01.png "Architettura dinamica")

Tale architettura:

* viene ridimensionata in base al *traffico* e all’*attività* effettiva;

* presenta istanze singole che vengono eseguite solo quando necessario;

* utilizza applicazioni modulari;

* per impostazione predefinita dispone di un cluster di authoring, per garantire la disponibilità continua anche durante le attività di manutenzione.

Questo approccio consente la scalabilità automatica in base alle esigenze di diversi schemi di utilizzo:

![Scalabilità automatica per diversi schemi di utilizzo](assets/concepts-02.png "Scalabilità automatica per diversi schemi di utilizzo")

A tal fine, tutte le istanze di AEM as a Cloud Service vengono create uguali, ciascuna con le medesime caratteristiche predefinite in termini di numero di nodi, di memoria e di capacità di elaborazione allocate.

AEM as a Cloud Service si basa sull’utilizzo di un motore di orchestrazione che:

* controlla costantemente lo stato del servizio;

* ridimensiona in modo dinamico ciascuna istanza del servizio in base alle esigenze effettive, potenziandola o riducendola a seconda delle necessità.

Tale comportamento:

* è applicabile al numero di nodi, alla quantità di memoria e alla capacità della CPU allocata su ciascun nodo;

* consente ad AEM as a Cloud Service di adattarsi agli schemi di traffico mano a mano che cambiano.

La scalabilità delle istanze per tenant del servizio può avvenire in modo automatico o manuale sui due assi:

* Verticale: la memoria e la capacità di CPU allocate possono essere potenziate o ridotte per un numero fisso di nodi.

* Orizzontale: il numero di nodi di un determinato servizio può essere incrementato o ridotto.

## Ambienti {#environments}

>[!NOTE]
>
> Per ulteriori informazioni, vedi [Distribuzione - Modalità di esecuzione](/help/implementing/deploying/overview.md#runmodes)

AEM as a Cloud Service è disponibile come istanza singola, dove ogni istanza rappresenta un ambiente AEM completo. Con AEM as a Cloud Service sono disponibili quattro tipi di ambienti:

* **Ambiente di produzione**: ospita le applicazioni utilizzate dagli utenti business.

* **Ambiente stage**: è sempre associato a un unico ambiente di produzione con una relazione 1:1. L’ambiente stage viene utilizzato per vari test di prestazioni e qualità, prima che eventuali modifiche all’applicazione vengano inviate all’ambiente di produzione.

* **Ambiente di sviluppo**: consente agli sviluppatori di implementare le applicazioni AEM nelle medesime condizioni di esecuzione degli ambienti di stage e produzione.

* **Ambiente dimostrativo**: può essere utilizzato a scopo di valutazione, dimostrazione, prototipazione e formazione.

Gli ambienti di sviluppo e dimostrazione sono spesso definiti ambienti *non di produzione*.

## Programmi {#programs}

Qualsiasi nuovo progetto AEM è sempre associato a una singola base di codice specifica, in cui puoi memorizzare sia la configurazione che il codice personalizzato per il progetto. Queste informazioni sono memorizzate in un archivio di codice, accessibile tramite i consueti client Git, messi a disposizione al momento della creazione di nuovi programmi.

Un programma AEM è il contenitore che include:

|  Elemento del programma |  Numero |
|--- |--- |
| Archivio del codice (Git) |  1 |
| Immagine linea di base (Sites o Assets) |  1 |
| Set di ambienti di stage e produzione (1:1) | 0 o 1 |
| Ambienti non di produzione (sviluppo o dimostrazione) | Da 0 a N |
| Pipeline per ogni ambiente | 0 o 1 |

Per AEM as a Cloud Service, inizialmente sono disponibili due tipi di programmi:

* AEM Cloud Sites Service

* AEM Cloud Assets Service

Entrambi consentono l’accesso a una serie di funzioni e funzionalità. Il livello di authoring contiene tutte le funzionalità di Sites e Assets per tutti i programmi, ma i programmi Assets non avranno un livello di pubblicazione per impostazione predefinita.

## Architettura runtime {#runtime-architecture}

Questa nuova architettura presenta diversi componenti principali:

<!--- needs reworking -->

![AEM as a Cloud Service: architettura runtime](assets/concepts-03.png "AEM as a Cloud Service - Architettura runtime")

* Per AEM Sites as a Cloud Service:

   * Per ogni ambiente ad alto livello permane il concetto di livello di authoring e livello di pubblicazione.

   * Il livello di authoring è composto da due o più nodi all’interno di un singolo cluster di authoring e viene ridimensionato automaticamente in base all’attività di authoring.

      * Gli autori o i creatori dei contenuti accedono al livello di authoring di AEM per creare, modificare e gestire i contenuti.

      * L’accesso al livello di authoring è gestito da Adobe Identity Management Services (IMS).

      * L’integrazione e l’elaborazione di Assets utilizza un servizio dedicato di elaborazione Assets.
   * Il livello di pubblicazione è composto da due o più nodi all’interno di una singola farm di pubblicazione, che possono operare indipendentemente l’uno dall’altro. Ogni nodo è costituito da un editore AEM e da un server web dotato del modulo AEM Dispatcher. Il nodo viene ridimensionato automaticamente in base alle esigenze di traffico del sito.

      * Gli utenti finali o i visitatori del sito visitano il sito web tramite AEM Publish Service.


* Per AEM Assets as a Cloud Service:

   * L’architettura include solo un ambiente di authoring.

* Sia il livello di authoring che quello di pubblicazione leggono e rendono persistente i contenuti da/a un servizio Content Repository.

   * Il livello di pubblicazione legge i contenuti solo dal livello di persistenza.

   * Il livello di authoring legge e scrive i contenuti da e verso il livello di persistenza.

   * L’archiviazione BLOB è condivisa tra il livello di pubblicazione e di authoring; i file non vengono *spostati*.

   * Quando il contenuto viene approvato dal livello di authoring, ciò indica che può essere attivato, e quindi inviato al livello di persistenza del livello di pubblicazione. Ciò avviene tramite il servizio di replica, una pipeline middleware. Questa pipeline riceve il nuovo contenuto: i singoli nodi del servizio di pubblicazione si abbonano al contenuto inviato alla pipeline.

      >[!NOTE]
      >
      >Per ulteriori dettagli, consulta [Replica](/help/operations/replication.md).

   * Sviluppatori e amministratori gestiscono l’applicazione AEM as a Cloud Service mediante Continuous Integration/Continuous Delivery (CI/CD), tramite [Cloud Manager](/help/overview/what-is-new-and-different.md#cloud-manager). Il servizio include distribuzioni di codice e configurazione tramite la pipeline CI/CD di Cloud Manager. I clienti di Cloud Manager visualizzano tutto ciò che riguarda il monitoraggio, la manutenzione e la risoluzione dei problemi, ad esempio, i file di registro.

   * L’accesso ai livelli di authoring e pubblicazione avviene sempre tramite un load balancer, che è sempre aggiornato con i nodi attivi in ciascuno dei livelli.

   * Per il livello di pubblicazione, come primo punto di ingresso è disponibile anche un servizio CDN (Continuous Delivery Network).

* Per le istanze dimostrative di AEM as a Cloud Service, l’architettura viene semplificata a un singolo nodo di authoring. Pertanto non presenta tutte le caratteristiche dell’ambiente di sviluppo, stage o produzione standard. In altre parole, possono anche verificarsi tempi di inattività e non è incluso il supporto di operazioni di backup e ripristino.

## Architettura di distribuzione {#deployment-architecture}

Cloud Manager gestisce tutti gli aggiornamenti alle istanze di AEM as a Cloud Service. È una scelta obbligatoria, essendo l’unica soluzione per creare, testare e distribuire l’applicazione del cliente, sia per il livello di authoring che per quello di pubblicazione. Questi aggiornamenti possono essere attivati da Adobe quando è pronta una nuova versione di AEM Cloud Service oppure dal cliente stesso, quando è pronta una nuova versione della sua applicazione.

Tecnicamente, l’implementazione avviene grazie al concetto di pipeline di distribuzione, associata a ogni ambiente presente all’interno di un programma. Quando una pipeline di Cloud Manager è in esecuzione, crea una nuova versione dell’applicazione del cliente, sia per il livello di authoring che per quello di pubblicazione. Tale risultato si ottiene combinando gli ultimi pacchetti cliente con la più recente immagine linea di base di Adobe. Quando le nuove immagini vengono create e testate correttamente, Cloud Manager automatizza completamente il cutover alla versione più recente dell’immagine tramite l’aggiornamento di tutti i nodi del servizio, secondo uno schema di aggiornamento in sequenza. Ciò non comporta tempi di inattività né per il servizio di authoring né per quello di pubblicazione.

<!--- needs reworking -->

![AEM as a Cloud Service: architettura di distribuzione](assets/concepts-04.png "AEM as a Cloud Service - Architettura di distribuzione")

## Distribuzione dei contenuti {#content-distribution}

Con Adobe Experience Manager as a Cloud Service cambia il funzionamento della pubblicazione dei contenuti. Con AEM as a Cloud Service, il framework di replica delle versioni precedenti di AEM non viene più utilizzato per pubblicare le pagine (le modifiche vengono spostate dall’istanza di authoring a quelle di pubblicazione).

AEM as a Cloud Service adesso utilizza la [funzionalità di distribuzione dei contenuti Sling](https://sling.apache.org/documentation/bundles/content-distribution.html) per spostare il contenuto appropriato. Tale funzionalità si basa su un servizio pipeline eseguito su Adobe I/O, che si trova al di fuori del runtime AEM.

La configurazione è automatizzata, con autoconfigurazione automatica quando i nodi di pubblicazione vengono aggiunti, rimossi o riciclati durante il runtime.

Una singola richiesta di pubblicazione o di annullamento della pubblicazione può includere più risorse, ma restituirà un unico stato applicato a tutte, e avrà esito positivo o negativo per tutte le risorse di AEM Publish Service. In questo modo le risorse di AEM Publish Service non presenteranno mai uno stato incoerente.

**Diagramma dell’architettura di distribuzione dei contenuti di alto livello**

![Diagramma dell’architettura di distribuzione dei contenuti di alto livello](assets/architecture-diagram.png "Diagramma dell’architettura di distribuzione dei contenuti di alto livello")

## Evoluzioni fondamentali {#key-evolutions}

La nuova architettura di AEM as a Cloud Service introduce alcune modifiche e innovazioni fondamentali rispetto alle generazioni precedenti:

* Tutti i file (BLOB) vengono caricati e serviti direttamente da un archivio dati cloud. Il flusso di bit associato non passa mai attraverso la JVM dei servizi AEM Author e Publish. Di conseguenza, i nodi dei servizi di authoring e pubblicazione di AEM possono avere dimensioni più ridotte e risultare maggiormente compatibili con l’aspettativa di una rapida scalabilità automatica. Per i professionisti del settore, questo consente un’esperienza più rapida durante il caricamento e il download di immagini, video ecc.

* Tutte le operazioni che consistono nella pubblicazione di contenuto adesso includono una pipeline che segue uno schema di sottoscrizione. Il contenuto pubblicato viene inviato a varie code della pipeline, alle quali sono abbonati tutti i nodi del servizio di pubblicazione. Di conseguenza, il livello di authoring non deve essere a conoscenza del numero di nodi presenti nel servizio di pubblicazione, il che consente un rapido ridimensionamento automatico del livello di pubblicazione.

* Il concetto di Golden Master è stato introdotto per automatizzare il ciclo di vita dei nodi di pubblicazione. Il Golden Master è un nodo di pubblicazione specializzato, a cui nessun utente finale accede e da cui vengono creati tutti i nodi del servizio di pubblicazione. Le operazioni di manutenzione, come la compattazione, vengono eseguite nell’archivio dei contenuti collegato al Golden Master. I nodi di pubblicazione vengono riciclati ogni giorno e non richiedono alcun tipo di manutenzione ordinaria. In passato, tale manutenzione comportava tempi di inattività, in particolare per l’istanza di authoring.

* L’architettura separa completamente il contenuto dell’applicazione dal codice e dalla configurazione dell’applicazione. Tutto il codice e la configurazione diventano praticamente immutabili e vengono inseriti nell’immagine linea di base utilizzata per creare i vari nodi dei servizi di authoring e pubblicazione. Di conseguenza, esiste una garanzia assoluta che ogni nodo sia identico e che le modifiche al codice e alla configurazione possano essere apportate solo a livello globale, eseguendo una pipeline di Cloud Manager.
