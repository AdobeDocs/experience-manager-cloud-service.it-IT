---
title: Pubblicazione
description: Scopri come eseguire la migrazione una volta che il codice e il contenuto sono pronti per il cloud
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 3%

---

# Pubblicazione {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Preparazione alla pubblicazione"
>abstract="Per garantire che la pubblicazione su AEM as a Cloud Service avvenga correttamente, devi pianificare i periodi di blocco del codice e dei contenuti, le iterazioni dei test, le integrazioni dei contenuti, i test delle prestazioni e di sicurezza e altro ancora."

In questa sezione del percorso imparerai a pianificare ed eseguire la migrazione una volta che il codice e il contenuto saranno pronti per essere trasferiti ad AEM as a Cloud Service. Inoltre, scopri quali sono le best practice e le limitazioni note durante l’esecuzione della migrazione.

## Percorso affrontato finora {#story-so-far}

Nelle fasi precedenti del percorso:

* Hai imparato a passare ad AEM as a Cloud Service nella pagina [Guida introduttiva](/help/journey-migration/getting-started.md).
* Determinato se la distribuzione è pronta per essere spostata nel cloud leggendo la [fase di preparazione](/help/journey-migration/readiness.md)
* Acquisisci familiarità con gli strumenti e i processi attraverso i quali puoi preparare il codice e il cloud di contenuti con la [fase di implementazione](/help/journey-migration/implementation.md).

## Obiettivo {#objective}

Questo documento spiega come eseguire la migrazione ad AEM as a Cloud Service una volta acquisite familiarità con i passaggi precedenti del percorso. Scopri come eseguire la migrazione di produzione iniziale e le best practice da seguire per la migrazione ad AEM as a Cloud Service.

## Migrazione iniziale alla produzione {#initial-migration}

Prima di poter eseguire la migrazione di produzione, segui i passaggi di installazione e verifica della migrazione descritti nella sezione [Strategia di migrazione dei contenuti e timeline](/help/journey-migration/implementation.md##strategy-timeline) della [Fase di implementazione](/help/journey-migration/implementation.md).

* Avvia la migrazione dalla produzione in base all’esperienza acquisita durante la migrazione della fase AEM as a Cloud Service eseguita sui cloni:
   * Autore-Autore
   * Publish-Publish

* Convalida i contenuti acquisiti sia nel livello di authoring che in quello di pubblicazione di AEM as a Cloud Service.
* Chiedi al team di authoring dei contenuti di evitare di spostare i contenuti sia sull’origine che sulla destinazione fino al completamento dell’acquisizione
* È possibile aggiungere, modificare o eliminare nuovi contenuti, ma non spostarli. Questo vale sia per l’origine che per la destinazione.
* Registra il [tempo impiegato](/help/journey-migration/implementation.md#gathering-data) per l&#39;estrazione e l&#39;acquisizione complete in modo da avere una stima delle tempistiche di migrazione di integrazione future.
* Crea un [pianificazione della migrazione](/help/journey-migration/implementation.md#migration-plan) sia per l&#39;authoring che per la pubblicazione.

## Top-up incrementali {#top-up}

Dopo la migrazione iniziale dalla produzione, è necessario eseguire integrazioni incrementali per assicurarsi che i contenuti vengano aggiornati nell’istanza cloud. Per questo motivo, si consiglia di seguire le seguenti best practice:

* Raccogliere dati sulla quantità di contenuto. Ad esempio: una settimana, due settimane o un mese.
* Assicurati di pianificare le integrazioni in modo da evitare più di 48 ore di estrazione e acquisizione dei contenuti. Questa opzione è consigliata in modo che i contenuti aggiuntivi rientrino in un intervallo di tempo del fine settimana.
* Pianifica il numero di integrazioni necessarie e utilizza tali stime per pianificare la data di lancio.

## Identificare i tempi di blocco del codice e del contenuto per la migrazione {#code-content-freeze}

Come accennato in precedenza, dovrai pianificare un periodo di blocco del codice e dei contenuti. Utilizza le seguenti domande per pianificare il periodo di blocco:

* Quanto tempo è necessario per bloccare le attività di authoring dei contenuti?
* Per quanto tempo devo chiedere al mio team di consegna di interrompere l’aggiunta di nuove funzioni?

Per rispondere alla prima domanda, è necessario considerare il tempo necessario per eseguire le esecuzioni di prova in ambienti non di produzione. Per rispondere alla seconda domanda, è necessaria una stretta collaborazione tra il team che aggiunge nuove funzionalità e il team che refactoring del codice. L’obiettivo è garantire che tutto il codice aggiunto alla distribuzione esistente venga aggiunto, testato e distribuito anche nel ramo dei servizi cloud. In genere, ciò significa che la quantità di codice bloccato è inferiore.

Inoltre, è necessario pianificare un blocco dei contenuti quando è pianificato l’aggiornamento finale dei contenuti.

## Best practice {#best-practices}

Quando pianifichi o esegui la migrazione, prendi in considerazione le seguenti linee guida:

* Migrazione da Author a Author e Publish a Publish
* Richiedi un clone di produzione che può essere utilizzato per:
   * Acquisire le statistiche dell’archivio
   * Prova delle attività di migrazione
   * Preparare il piano di migrazione
   * Identificazione dei requisiti di blocco dei contenuti
   * Identifica eventuali esigenze di upsize sulla produzione durante la migrazione dalla produzione

**Best practice per lo strumento Content Transfer**

Assicurati di eseguire la migrazione dei contenuti in produzione invece di clonare quando vai live. È consigliabile utilizzare [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) per la migrazione iniziale e quindi eseguire frequentemente estrazioni di ricarica (anche quotidiane) per estrarre blocchi più piccoli ed evitare un carico a lungo termine sull&#39;AEM di origine.

Durante l’esecuzione della migrazione di produzione, è necessario evitare di eseguire lo strumento Content Transfer (Trasferimento contenuti) da un clone perché:

* Se un cliente richiede la migrazione delle versioni dei contenuti durante le migrazioni integrative, l’esecuzione dello strumento Content Transfer (Trasferimento contenuti) da un clone non esegue la migrazione delle versioni. Anche se il clone viene ricreato frequentemente dall’autore live, ogni volta che viene creato un clone vengono ripristinati i punti di controllo utilizzati dallo strumento Content Transfer (Trasferimento contenuti) per calcolare i delta.
* Poiché un clone non può essere aggiornato nel suo insieme, il pacchetto di query ACL deve essere utilizzato per creare un pacchetto e installare il contenuto aggiunto o modificato dalla produzione al clone. Il problema di questo approccio è che qualsiasi contenuto eliminato nell’istanza sorgente non arriverà mai al clone a meno che non venga eliminato manualmente sia dall’origine che dal clone. Questo introduce la possibilità che il contenuto eliminato in produzione non venga eliminato sul clone e su AEM as a Cloud Service.

**Ottimizzazione del carico sull&#39;origine AEM durante l&#39;esecuzione della migrazione dei contenuti**

Ricorda che il carico sulla sorgente dell’AEM è maggiore durante la fase di estrazione. Tieni presente quanto segue:

* Lo strumento Content Transfer (Trasferimento contenuti) è un processo Java esterno che utilizza un heap JVM di 4 GB
* La versione non AzCopy scarica i file binari, li memorizza in uno spazio temporaneo nell’autore AEM di origine, consumando I/O del disco, quindi carica nel contenitore Azure che consuma la larghezza di banda della rete
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) trasferisce i BLOB direttamente dall&#39;archivio BLOB al contenitore Azure che consente di salvare l&#39;I/O del disco e la larghezza di banda della rete. La versione di AzCopy utilizza ancora la larghezza di banda del disco e della rete per estrarre e caricare i dati dall’archivio segmenti nel contenitore di Azure
* Il processo dello strumento Content Transfer (Trasferimento contenuti) è più leggero per le risorse di sistema durante la fase di acquisizione, in quanto esegue lo streaming dei registri di acquisizione e l’istanza sorgente non ha un carico elevato per quanto riguarda l’I/O del disco o la larghezza di banda della rete.

## Limitazioni note {#known-limitations}

Considera che l’intera acquisizione non riesce se una qualsiasi delle seguenti limitazioni viene trovata come parte del set di migrazione estratto:

* Un nodo JCR con un nome che supera i 150 caratteri
* Un nodo JCR di dimensioni superiori a 16 MB
* Qualsiasi utente/gruppo con `rep:AuthorizableID` acquisito già presente in AEM as a Cloud Service
* Se una risorsa estratta e acquisita viene spostata in un percorso diverso nell’origine o nella destinazione prima della successiva iterazione della migrazione.

## Integrità risorsa {#asset-health}

Rispetto alla sezione precedente, l&#39;acquisizione **non ha esito negativo** a causa dei seguenti problemi relativi alle risorse. Tuttavia, si consiglia vivamente di adottare le misure appropriate in questi scenari:

* Qualsiasi risorsa con la rappresentazione originale mancante
* Qualsiasi cartella con un nodo `jcr:content` mancante.

Entrambi gli elementi sopra indicati sono identificati e segnalati nel report [Best Practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

## Elenco di controllo per la pubblicazione {#Go-Live-Checklist}

Per ulteriori informazioni, consulta la documentazione dell&#39;[Elenco di controllo pubblicazione](/help/journey-onboarding/go-live-checklist.md).

## Passaggio successivo {#what-is-next}

Una volta compreso come eseguire la migrazione ad AEM as a Cloud Service, puoi controllare la pagina [Post-Go-Live](/help/journey-migration/post-go-live.md) per mantenere l&#39;istanza in esecuzione senza problemi.
