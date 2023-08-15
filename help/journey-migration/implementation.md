---
title: Fase di implementazione
description: Assicurarsi che il codice e il contenuto siano pronti per la migrazione al cloud
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 10%

---

# Fase di implementazione {#implementation-phase}

Nella fase di implementazione del percorso, esplorerai gli strumenti attraverso i quali puoi rendere il codice e il contenuto pronti per essere trasferiti all’AEM as a Cloud Service.

## Percorso affrontato finora {#story-so-far}

Nelle parti precedenti del percorso, hai superato [familiarità con i cambiamenti dell’AEM as a Cloud Service](/help/journey-migration/getting-started.md)e determina se la distribuzione è pronta per essere spostata nel cloud con il [fase di preparazione](/help/journey-migration/readiness.md).

Questo articolo continua con consigli su come utilizzare gli strumenti forniti da Adobe per assicurarsi che il codice e il contenuto siano pronti per essere spostati nel cloud.

## Obiettivo {#objective}

Il presente documento si prefigge di:

* Scopri Cloud Manager, il framework di integrazione e consegna continue dell’AEM utilizzato per distribuire il codice su AEM as a Cloud Service
* Scopri come usare lo strumento per il trasferimento dei contenuti
* Descrivi gli strumenti di refactoring del codice da utilizzare per modernizzare il codice per gli as a Cloud Service AEM

## Utilizzo di Cloud Manager {#using-cloud-manager}

Prima di iniziare, è necessario acquisire familiarità con Cloud Manager, in quanto è l’unico meccanismo per distribuire il codice in AEM as a Cloud Service.

Cloud Manager consente alle organizzazioni di gestire autonomamente AEM nel cloud. Include un framework di integrazione continua e distribuzione continua (CI/CD, Continuous Integration/Continuous Delivery) che consente ai team IT e ai partner dell’implementazione di accelerare la distribuzione di personalizzazioni o aggiornamenti senza compromettere prestazioni o sicurezza.

Per acquisire familiarità con l’utilizzo di Cloud Manager, consulta le risorse seguenti:

* [Percorso di onboarding](/help/journey-onboarding/overview.md) per comprendere le risorse di supporto autonomo sull’onboarding, ad Experience Manager as a Cloud Service.

* [Integrazione di Git con Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) per informazioni sull’utilizzo di un archivio Git singolo per implementare il codice.

* [Configurazione di Adobe Experience as a Cloud Service](/help/security/ims-support.md#aem-configuration) per informazioni sulla gestione dei prodotti e dell’accesso degli utenti in Admin Console.

## Utilizza l’Adobe fornito di strumenti per rendere pronti i contenuti e Code Cloud {#use-tools-to-make-code-and-content-cloud-ready}

I passaggi esatti della transizione al Cloud Service dipendono dai sistemi acquistati e dalle procedure di sviluppo software seguite.

La figura seguente mostra i passaggi principali della fase che comporta la conversione del codice e del contenuto per l’utilizzo con AEM as a Cloud Service:

![immagine](/help/journey-migration/assets/exec-image1.png)

Inizieremo a specificare gli strumenti da utilizzare per ottenere questo risultato nei capitoli seguenti.

## Migrazione dei contenuti {#content-migration}

Per migrare il contenuto dall’istanza AEM corrente all’istanza di Cloud Service, puoi utilizzare lo strumento Content Transfer (Trasferimento contenuti) di Adobe.

Con questo strumento, puoi specificare il sottoinsieme di contenuti che desideri trasferire dall’istanza AEM sorgente all’istanza AEM Cloud Service.

La migrazione dei contenuti è un processo in più fasi che richiede pianificazione, tracciamento e collaborazione tra team diversi.

Per informazioni dettagliate su come funziona lo strumento e su come Adobe consiglia di utilizzarlo, vedere [Documentazione dello strumento Content Transfer (Trasferimento contenuti)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## Refactoring del codice {#code-refactor}

### Configurazione per lo sviluppo {#set-up-for-development}

È ora di iniziare a rieseguire il factoring delle funzioni esistenti per renderle compatibili con i Cloud Service.

Per prima cosa, consulta la documentazione che descrive gli strumenti di base e inizia a rieseguire il factoring del codice:


* Durante la pianificazione, è consigliabile disporre di un elenco di aree che devono essere riadattate per essere compatibili con gli as a Cloud Service AEM. Puoi rivedere [Linee guida per lo sviluppo](/help/implementing/developing/introduction/development-guidelines.md) per ulteriori dettagli su come effettuare il refactoring del codice per il Cloud Service e ottimizzarlo.
* Scopri come [Gestione configurazioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) nell’AEM as a Cloud Service.
* Scopri come impostare un ambiente di sviluppo locale scaricando il [SDK AS A CLOUD SERVICE AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* Infine, impara a conoscere [API Java as a Cloud Service AEM](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Inoltre, puoi anche:

* Guarda questo video per comprendere come installare localmente l’SDK di Dispatcher:

  >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Guarda questo video per comprendere come configurare l’SDK di Dispatcher:

  >[!VIDEO](https://video.tv.adobe.com/v/30602)

### Un cambio di mentalità {#a-change-in-mindset}

Lo sviluppo e l’esecuzione del codice in AEM as a Cloud Service richiedono un cambiamento di mentalità. Il codice deve essere resiliente, soprattutto poiché un’istanza potrebbe essere arrestata in qualsiasi momento. Il codice in esecuzione in Cloud Service deve tener conto di essere sempre in esecuzione in un cluster. Ciò significa che ci sono sempre in esecuzione più di un’istanza.

Per rendere i progetti AEM Maven compatibili con il cloud sono necessarie alcune modifiche. AEM as a Cloud Service richiede una separazione di *contenuto* e *codice* in pacchetti distinti da distribuire nell’AEM:

* `/apps` e `/libs` sono considerate aree immutabili dell’AEM in quanto non possono essere modificate dopo l’inizio dell’AEM (vale a dire in fase di runtime). Ciò include le operazioni di creazione, aggiornamento o eliminazione. Eventuali tentativi di modifica di un’area immutabile in fase di runtime avranno esito negativo.

* Tutto il resto nell’archivio (ad esempio, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`) sono tutte aree mutabili, ovvero possono essere modificate in fase di runtime.

Per saperne di più, consulta [Struttura consigliata dei pacchetti](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) documentazione.


### Strumenti di migrazione per cloud {#cloud-migration-tools}

Adobe fornisce diversi strumenti per accelerare alcune delle attività di refactoring del codice. Comprendere questi strumenti e i problemi che risolvono ridurrà la complessità e i tempi della migrazione.

* [Migrazione flusso di lavoro risorse](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md), strumento utilizzato per migrare automaticamente i flussi di lavoro di elaborazione delle risorse
* [Dispatcher Converter](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md), strumento che converte le configurazioni esistenti di Dispatcher in un formato pronto per l’AEM as a Cloud Service.
* [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en), uno strumento che prende come input un progetto multimodo AEM e lo converte in un progetto as a Cloud Service AEM
* [Convertitore indice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en), strumento che converte gli indici in una forma compatibile con AEM as a Cloud Service
* [Strumenti di modernizzazione](/help/journey-migration/refactoring-tools/aem-modernization-tools.md), una suite di utility che può essere utilizzata per convertire le funzioni legacy dell’AEM nelle funzionalità moderne e supportate di AEM as a Cloud Service.

Dopo aver configurato l’ambiente di sviluppo locale, acquisisci familiarità con l’SDK as a Cloud Service dell’AEM consultando il [documentazione](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### Pianificare un blocco del codice {#schedule-a-code-freeze}

Per gestire lo sviluppo del codice in corso sull’AEM attivo insieme alle attività di refactoring del codice come parte del percorso di transizione, Adobe consiglia di pianificare un periodo di blocco del codice fino a quando non avrai completato la ristrutturazione del progetto Maven per renderlo compatibile con AEM as a Cloud Service.

Al termine della ristrutturazione del progetto, puoi riprendere lo sviluppo del nuovo codice in base a questa nuova struttura. Questo riduce gli errori della pipeline di Cloud Manager durante la distribuzione e il test del codice.

>[!NOTE]
>Le attività di trasferimento dei contenuti e refactoring del codice non devono necessariamente essere eseguite in sequenza. Queste attività possono essere svolte l’una indipendentemente dall’altra. Tuttavia, è necessaria la giusta struttura di progetto per garantire il corretto rendering del contenuto nell’ambiente Cloud Service.

## Best practice per l’implementazione e il test del codice {#best-practices}

La pipeline di Cloud Manager supporta l’esecuzione di test nell’ambiente di staging.

Segui le best practice riportate nei documenti seguenti relativi al test della qualità del codice:

* [Test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md): documento che descrive il processo di scrittura degli script di test e spiega il concetto di copertura consigliata di almeno il 50%.
* [Regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md) che ha lo scopo di descrivere le regole per la qualità del codice personalizzato eseguite da Cloud Manager e create in base alle best practice di AEM Engineering.

## Preparazione per il lancio {#preparing-for-go-live}

La preparazione del sistema di origine per la migrazione prevede attività a livello di sistema e di amministratore AEM. Puoi iniziare verificando che l’archivio dei contenuti sia in uno stato di manutenzione corretto controllando [pulizia revisioni](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=it) e [raccolta di oggetti inattivi dell’archivio dati](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html?lang=it) stato attività. Se esegui la versione 6.3 dell’AEM (poiché lo strumento Content Transfer (Trasferimento contenuti) è compatibile dalla versione 6.3 in poi), si consiglia di eseguire la compattazione offline, seguita dalla raccolta di oggetti inattivi dell’archivio dati.

[Verifica coerenza dati](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) è consigliato in tutte le versioni AEM per garantire che l’archivio dei contenuti in buono stato avvii le attività di migrazione.

Per installare e configurare è necessario disporre dell&#39;accesso a livello di amministratore di sistema [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

È inoltre consigliabile rivedere eventuali risorse, pagine, progetti AEM, utenti e gruppi inutilizzati per risparmiare tempo durante la migrazione. Consulta la [Integrità archivio contenuti](#repository-health) sezione.

### Integrità archivio contenuti {#repository-health}

Dopo l’accesso a [clone di produzione](#proof-of-migration) viene stabilito procedere alla verifica dello stato dell’archivio. Come indicato nella sezione precedente, l’obiettivo è pulire e compattare l’archivio sull’origine prima di avviare la migrazione. Questo passaggio potrebbe risparmiare molto tempo altrimenti, una volta avviata la migrazione, si occuperà della risoluzione dei problemi.

| Oggetto Azione | Takeaway chiave |
|---------|----------|
| Utenti, gruppi e autorizzazioni | È necessario comprendere il volume di utenti, gruppi e la complessità delle appartenenze. Cerca le opportunità per eliminare eventuali utenti inutilizzati, gruppi nell’origine prima della migrazione. |
| Elaborazione risorsa incompleta | Prova a completare l’elaborazione delle risorse nel sistema di origine prima di iniziare la migrazione per evitare potenziali problemi nell’AEM as a Cloud Service dopo la migrazione. |
| Integrità dei contenuti | Si consiglia di eseguire una query per individuare eventuali contenuti errati ed eliminarli prima di avviare la migrazione. Ad esempio, cerca le risorse o le pagine che non hanno rappresentazioni originali o che sono bloccate nell’elaborazione del flusso di lavoro. Vedi anche [Integrità risorsa](#asset-health). |

## Raccolta dei dati {#gathering-data}

>[!NOTE]
> Il [Strategia e tempistica di migrazione dei contenuti](#content-strategy-and-timeline) Questa sezione descrive come estrapolare i dati raccolti e creare un piano di migrazione.

La raccolta dei dati può essere utile per pianificare le attività di migrazione e le attività associate. I tempi di estrazione e di acquisizione sono particolarmente utili perché i punti dati possono essere associati a una dimensione specifica del set di migrazione. Di conseguenza, questi punti di dati possono essere estrapolati per ottenere un piano:

* Quantità totale di tempo impiegato per [estrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* Quantità totale di tempo impiegato per [acquisizione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* Tempo totale impiegato per l&#39;integrazione [estrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* Tempo totale impiegato per l&#39;integrazione [acquisizione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)


<!-- Alexandru: hiding this for now

One more important datapoint is the amount of time it takes to complete the [user mapping](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), if this is coupled with the content migration. You can take this data point into consideration for more realistic estimates, because it is added to the overall extraction timeline and it may not be required to run it during top-ups.

-->

Questi punti dati possono anche aiutarti [Stabilire i KPI](/help/journey-migration/readiness.md#establish-kpis) e altre attività relative alla migrazione.

### Piano di migrazione {#migration-plan}

In base ai punti dati raccolti (vedere sopra), è possibile creare un piano di migrazione che può essere integrato in un piano di progetto macro. Questo passaggio consentirà a tutte le principali parti interessate di visualizzare e pianificare le attività di migrazione.

Nella tabella seguente viene illustrato un tipico piano di migrazione:

| Iterazione di migrazione | Data iniziale | Data di fine stimata | Dipendenze | Durata stimata (in giorni) | Dettagli aggiuntivi/Azioni |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |   |   |   |   |   |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |   |   |   |   |   |

Come puoi vedere nella tabella precedente, è utile seguire un formato di denominazione specifico per identificare le iterazioni di migrazione, ad esempio: **PRDCLONE** per l&#39;ambiente AEM di origine , **AUTORE/PUBBLICAZIONE** per l&#39;ambiente as a Cloud Service dell&#39;AEM, **CSSTAGE-AUTHOR** per l&#39;istanza AEM as a Cloud Service e così via.

Alcuni dettagli importanti che influenzano il piano di migrazione:

**Numero totale di estrazioni richieste**

* Le estrazioni di authoring e pubblicazione in ambienti specifici sono considerate due estrazioni parallele in quanto sono indipendenti l’una dall’altra.
* Numero di estrazioni integrative basate sulla crescita dell’archivio in periodi di tempo specifici.

**Numero totale di acquisizioni richieste**

* È importante acquisire questo elemento nel piano, poiché un set estratto può essere acquisito in più ambienti di Cloud Service.
* Numero di acquisizioni integrative.
* La migrazione del contenuto dall’istanza di authoring dell’origine a quella di authoring del servizio Cloud e dalla pubblicazione dell’origine a quella del Cloud Service è la best practice per evitare di acquisire tutti i contenuti di authoring nella pubblicazione del Cloud Service.

### Tracciamento migrazione {#migration-tracker}

Puoi utilizzare il tracciatore della migrazione per annotare i tempi sia per le esecuzioni iniziali che per quelle integrative. Questi punti dati ti aiuteranno a formulare requisiti realistici di blocco dei contenuti prima dell’integrazione finale.

Il tracker ti aiuterà anche a:

* Identifica eventuali deviazioni dal planner che richiedono adeguamenti nei timeline del piano o del lancio
* Fornire uno stato realistico che possa essere utilizzato in tutte le comunicazioni necessarie
* Pianificare migrazioni di backup iniziali o future

La tabella seguente illustra un tracker di migrazione funzionale:

| Origine (ambiente/istanza/URL) | Destinazione (ambiente/istanza/URL) | Nome e tipo del set di migrazione (iniziale o superiore) | Dimensioni set di migrazione (MB) | Mappatura utenti (sì/no) | Durata estrazione (inizio, fine, tempo impiegato) | Durata acquisizione (inizio, fine, tempo impiegato) | Problemi / Risoluzioni / Dettagli |
|---|---|---|---|---|---|---|---|
|   |   |   |   |   |   |   |   |

## Strategia e tempistica di migrazione dei contenuti {#content-strategyand-timeline}

Nella sezione seguente sono illustrati i passaggi importanti e le attività associate che è possibile utilizzare per formulare una strategia e una tempistica di migrazione dei contenuti.

![immagine](/help/journey-migration/assets/content-migration2.png)

### Filtraggio {#fitment}

* Eseguire la pulizia delle revisioni, la raccolta di oggetti inattivi dell’archivio dati e i controlli di coerenza dei dati. Vedi anche [Preparazione per il lancio](#preparing-for-go-live)
* [Raccogliere statistiche](#gathering-data) informazioni sull’archivio di origine dell’AEM:
   * Dimensione archivio segmenti
   * Dimensione archivio indice
   * Numero di pagine
   * Numero di risorse
   * Numero di utenti e gruppi
* Scopri se le seguenti funzioni sono abilitate nella sorgente dell’AEM (necessaria anche in AEM as a Cloud Service):
   * Applicazione di tag avanzati
   * Ricerca per affinità
   * Cerca il testo che contiene nei documenti Word e Pdf
* Raccogli Best Practice Analyzer [rapporto](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* Importa in [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * Rivedi le raccomandazioni di auto-analisi per assicurarti che gli as a Cloud Service AEM possano gestire i requisiti di storage.
* Crea un ticket di supporto Adobe per eventuali chiarimenti prima di continuare con il piano di migrazione.

### Prova della migrazione {#proof-of-migration}

* Richiedi un clone di produzione che:
   * Si trova nella stessa area di rete
   * Fornirà contenuti di produzione come utenti e gruppi
   * Cloni authoring e pubblicazione: un nodo ciascuno in caso di cluster o farm di pubblicazione
* Scegli un sottoinsieme del contenuto di cui eseguire la migrazione in modo che:
   * È una combinazione di tutti i tipi di contenuto disponibili
   * Contiene tutti gli utenti e i gruppi
* Include il 25% del contenuto o fino a 1 TB, a seconda di quale dei due valori è minore.
* Esegui almeno un&#39;esecuzione completa e [integrativo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) migrazione, dal clone di produzione all’ambiente non di produzione as a Cloud Service AEM
* Risolvi eventuali problemi come:
   * Spazio su disco nell&#39;origine AEM
   * Connettività tra la fonte dell’AEM e l’AEM as a Cloud Service
   * Qualsiasi [limitazioni relative all’acquisizione](go-live.md#known-limitations).
* Registra il tempo impiegato per [estrazione e acquisizione](#gathering-data):
   * Conoscere la quantità di contenuti aggiunti alla settimana
   * Estrapolare i tempi misurati dalla bozza di migrazione per creare un [piano di migrazione](#migration-plan).

## Passaggio successivo {#what-is-next}

Dopo aver compreso appieno come valutare se l’installazione dell’AEM è pronta per essere spostata sul cloud, mentre impariamo a utilizzare gli strumenti necessari per prepararla, è ora di passare al [fase di pubblicazione](/help/journey-migration/go-live.md).
