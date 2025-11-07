---
title: Fase di implementazione
description: Assicurarsi che il codice e il contenuto siano pronti per la migrazione al cloud
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
feature: Migration
role: Admin
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '2288'
ht-degree: 9%

---

# Fase di implementazione {#implementation-phase}

Nella fase di implementazione del percorso, esplorerai gli strumenti attraverso i quali puoi rendere il codice e il contenuto pronti per essere spostati su AEM as a Cloud Service.

## Percorso affrontato finora {#story-so-far}

Nelle parti precedenti del percorso, sei passato attraverso [la conoscenza delle modifiche in AEM as a Cloud Service](/help/journey-migration/getting-started.md) e hai stabilito se la tua distribuzione è pronta per essere spostata nel cloud con la [fase di preparazione](/help/journey-migration/readiness.md).

Questo articolo continua con consigli su come utilizzare gli strumenti forniti da Adobe per assicurarsi che il codice e il contenuto siano pronti per essere spostati sul cloud.

## Obiettivo {#objective}

Il presente documento si prefigge di:

* Presenta Cloud Manager, il framework di integrazione e consegna continua di AEM utilizzato per distribuire il codice in AEM as a Cloud Service
* Scopri come usare lo strumento per il trasferimento dei contenuti
* Descrivi gli strumenti di refactoring del codice da utilizzare per modernizzare il codice per AEM as a Cloud Service

## Utilizzo di Cloud Manager {#using-cloud-manager}

Prima di iniziare, devi acquisire familiarità con Cloud Manager, in quanto è l’unico meccanismo per distribuire il codice in AEM as a Cloud Service.

Cloud Manager consente alle organizzazioni di gestire autonomamente AEM nel cloud. Include un framework di integrazione continua e distribuzione continua (CI/CD, Continuous Integration/Continuous Delivery) che consente ai team IT e ai partner dell’implementazione di accelerare la distribuzione di personalizzazioni o aggiornamenti senza compromettere prestazioni o sicurezza.

Per acquisire familiarità con l’utilizzo di Cloud Manager, consulta le risorse seguenti:

* [Percorso di onboarding](/help/journey-onboarding/overview.md) per informazioni sulle risorse di supporto autonomo relative all&#39;onboarding per Experience Manager as a Cloud Service.

* [Integrazione di Git con Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) per informazioni sull’utilizzo di un archivio Git singolo per implementare il codice.

* [Configurazione di Adobe Experience as a Cloud Service](/help/security/ims-support.md#aem-configuration) per informazioni sulla gestione dei prodotti e dell’accesso degli utenti in Admin Console.

## Utilizza gli strumenti forniti da Adobe per rendere pronti i contenuti e Code Cloud {#use-tools-to-make-code-and-content-cloud-ready}

I passaggi esatti della transizione verso Cloud Service dipendono dai sistemi acquistati e dalle procedure di sviluppo software seguite.

La figura seguente mostra i passaggi principali della fase che comporta la conversione del codice e del contenuto per l’utilizzo con AEM as a Cloud Service:

![Passaggi di conversione](/help/journey-migration/assets/exec-image1.png)

Inizieremo a specificare gli strumenti da utilizzare per ottenere questo risultato nei capitoli seguenti.

## Migrazione dei contenuti {#content-migration}

Per migrare il contenuto dall’istanza AEM corrente all’istanza Cloud Service, puoi utilizzare lo strumento Content Transfer (Trasferimento contenuti) di Adobe.

Con questo strumento, puoi specificare il sottoinsieme di contenuti che desideri trasferire dall’istanza AEM sorgente all’istanza AEM Cloud Service.

La migrazione dei contenuti è un processo in più fasi che richiede pianificazione, tracciamento e collaborazione tra team diversi.

Per informazioni dettagliate su come funziona lo strumento e su come Adobe consiglia di utilizzarlo, consulta la [documentazione dello strumento Content Transfer](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## Refactoring del codice {#code-refactor}

### Configurazione per lo sviluppo {#set-up-for-development}

È ora di iniziare a eseguire il refactoring delle funzioni esistenti per renderle compatibili con Cloud Services.

Per prima cosa, consulta la documentazione che descrive gli strumenti di base e inizia a rieseguire il factoring del codice:


* Durante la pianificazione, è consigliabile disporre di un elenco di aree che devono essere reimpostate per essere compatibili con AEM as a Cloud Service. Puoi consultare le [Linee guida per lo sviluppo](/help/implementing/developing/introduction/development-guidelines.md) per ulteriori dettagli su come effettuare il refactoring del codice e ottimizzarlo per Cloud Service.
* Scopri come [gestire le configurazioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html#what-is-a-configuration) in AEM as a Cloud Service.
* Scopri come impostare un ambiente di sviluppo locale scaricando [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=it)
* Infine, acquisisci familiarità con [API Java di AEM as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Inoltre, puoi anche:

* Guarda questo video per comprendere come installare Dispatcher SDK a livello locale:

  >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Guarda questo video per comprendere come configurare Dispatcher SDK:

  >[!VIDEO](https://video.tv.adobe.com/v/30602)

### Un cambio di mentalità {#a-change-in-mindset}

Lo sviluppo e l’esecuzione del codice in AEM as a Cloud Service richiedono un cambiamento di mentalità. Il codice deve essere resiliente, soprattutto poiché un’istanza potrebbe essere interrotta in qualsiasi momento. Il codice in esecuzione in Cloud Service deve tener conto di essere sempre in esecuzione in un cluster. Ciò significa che ci sono sempre in esecuzione più di un’istanza.

Per rendere i progetti AEM Maven compatibili con il cloud, sono necessarie alcune modifiche. AEM as a Cloud Service richiede una separazione di *content* e *code* in pacchetti distinti per la distribuzione in AEM:

* `/apps` e `/libs` sono considerate aree immutabili di AEM in quanto non possono essere modificate dopo l&#39;avvio di AEM (ovvero in fase di runtime). Ciò include le operazioni di creazione, aggiornamento o eliminazione. Eventuali tentativi di modifica di un’area immutabile in fase di runtime avranno esito negativo.

* Tutte le altre aree del repository (ad esempio, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`) sono mutabili, il che significa che possono essere modificate in fase di esecuzione.

Per ulteriori informazioni, consulta la [documentazione sulla struttura consigliata dei pacchetti](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure).


### Strumenti di migrazione per cloud {#cloud-migration-tools}

Adobe fornisce diversi strumenti per accelerare alcune delle attività di refactoring del codice. Comprendere questi strumenti e i problemi che risolvono ridurrà la complessità e i tempi della migrazione.

* [Migrazione dei flussi di lavoro delle risorse](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md), uno strumento utilizzato per migrare automaticamente i flussi di lavoro di elaborazione delle risorse
* [Dispatcher Converter](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md), uno strumento che converte le configurazioni esistenti di Dispatcher in un formato pronto per AEM as a Cloud Service.
* [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html), uno strumento che accetta un progetto AEM Multimode come input e lo converte in un progetto AEM as a Cloud Service
* [Convertitore indice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html), uno strumento che converte gli indici in un modulo compatibile con AEM as a Cloud Service
* [Strumenti di modernizzazione](/help/journey-migration/refactoring-tools/aem-modernization-tools.md), una suite di utilità che può essere utilizzata per convertire le funzionalità legacy di AEM nelle funzionalità moderne e supportate di AEM as a Cloud Service.

Dopo aver configurato l&#39;ambiente di sviluppo locale, acquisisci familiarità con AEM as a Cloud Service SDK consultando la [documentazione](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### Pianificare un blocco del codice {#schedule-a-code-freeze}

Per gestire lo sviluppo del codice in corso sul tuo AEM attivo insieme alle attività di refactoring del codice come parte del percorso di transizione, Adobe consiglia di pianificare un periodo di blocco del codice fino a quando non avrai completato la ristrutturazione del progetto Maven per renderlo compatibile con AEM as a Cloud Service.

Al termine della ristrutturazione del progetto, puoi riprendere lo sviluppo del nuovo codice in base a questa nuova struttura. Questo riduce gli errori della pipeline Cloud Manager durante la distribuzione e il test del codice.

>[!NOTE]
>Le attività di trasferimento dei contenuti e refactoring del codice non devono necessariamente essere eseguite in sequenza. Queste attività possono essere svolte l’una indipendentemente dall’altra. Tuttavia, è necessaria la giusta struttura di progetto per garantire il corretto rendering del contenuto nell’ambiente Cloud Service.

## Best practice per l’implementazione e il test del codice {#best-practices}

La pipeline di Cloud Manager supporta l’esecuzione di test nell’ambiente di staging.

Segui le best practice riportate nei documenti seguenti relativi al test della qualità del codice:

* [Test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md), un documento che descrive il processo di scrittura degli script di test e spiega il concetto di copertura consigliata di almeno il 50%.
* [Regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md) che descrive le regole per la qualità del codice personalizzato eseguite da Cloud Manager e create in base alle best practice di AEM Engineering.

## Preparazione per il lancio {#preparing-for-go-live}

La preparazione del sistema di origine per la migrazione prevede attività a livello di amministratore di sistema e AEM. Puoi iniziare verificando che l&#39;archivio dei contenuti sia in uno stato di manutenzione corretto controllando lo stato dell&#39;attività [pulizia revisioni](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=it) e [raccolta di oggetti inattivi dell&#39;archivio dati](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html?lang=it). Se esegui AEM versione 6.3 (poiché lo strumento Content Transfer è compatibile a partire dalla versione 6.3), si consiglia di eseguire la compattazione offline, seguita dalla raccolta di oggetti inattivi dell’archivio dati.

[La verifica di coerenza dei dati](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) è consigliata in tutte le versioni di AEM per garantire che l&#39;archivio dei contenuti sia in buono stato per avviare le attività di migrazione.

Per installare e configurare [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) è necessario disporre dell&#39;accesso a livello di amministratore di sistema

È inoltre consigliabile rivedere eventuali Assets, pagine, progetti AEM, utenti e gruppi inutilizzati per risparmiare tempo durante la migrazione. Consulta la sezione [Integrità dell&#39;archivio dei contenuti](#repository-health).

### Integrità archivio contenuti {#repository-health}

Una volta stabilito l&#39;accesso a un [clone di produzione](#proof-of-migration), procedere con la verifica dello stato dell&#39;archivio. Come indicato nella sezione precedente, l’obiettivo è pulire e compattare l’archivio sull’origine prima di avviare la migrazione. Questo passaggio potrebbe risparmiare molto tempo altrimenti, una volta avviata la migrazione, si occuperà della risoluzione dei problemi.

| Oggetto Azione | Elementi principali da ricordare |
|---------|----------|
| Utenti, gruppi e autorizzazioni | È necessario comprendere il volume di utenti, gruppi e la complessità delle appartenenze. Cerca le opportunità per eliminare eventuali utenti inutilizzati, gruppi nell’origine prima della migrazione. |
| Elaborazione risorsa incompleta | Prova a completare l’elaborazione delle risorse nel sistema di origine prima di iniziare la migrazione per evitare potenziali problemi in AEM as a Cloud Service dopo la migrazione. |
| Integrità dei contenuti | Si consiglia di eseguire una query per individuare eventuali contenuti errati ed eliminarli prima di avviare la migrazione. Ad esempio, cerca le risorse o le pagine che non hanno rappresentazioni originali o che sono bloccate nell’elaborazione del flusso di lavoro. Vedi anche [Integrità risorsa](#asset-health). |

## Raccolta dei dati {#gathering-data}

>[!NOTE]
> Nella sezione [Strategia e tempistica di migrazione dei contenuti](#content-strategy-and-timeline) sono disponibili ulteriori dettagli su come estrapolare i dati raccolti e creare un piano di migrazione.

La raccolta dei dati può essere utile per pianificare le attività di migrazione e le attività associate. I tempi di estrazione e di acquisizione sono particolarmente utili perché i punti dati possono essere associati a una dimensione specifica del set di migrazione. Di conseguenza, questi punti di dati possono essere estrapolati per ottenere un piano:

* Tempo totale impiegato per [estrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* Tempo totale impiegato per [l&#39;acquisizione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* Tempo totale impiegato per [estrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) integrativa
* Tempo totale impiegato per l&#39;acquisizione integrativa di [&#128279;](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)


<!-- Alexandru: hiding this for now

One more important datapoint is the amount of time it takes to complete the [user mapping](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), if this is coupled with the content migration. You can take this data point into consideration for more realistic estimates, because it is added to the overall extraction timeline and it may not be required to run it during top-ups.

-->

Questi punti dati possono inoltre essere utili per [stabilire i KPI](/help/journey-migration/readiness.md#establish-kpis) e altre attività correlate alla migrazione.

### Piano di migrazione {#migration-plan}

In base ai punti dati raccolti (vedere sopra), è possibile creare un piano di migrazione che può essere integrato in un piano di progetto macro. Questo passaggio consentirà a tutte le principali parti interessate di visualizzare e pianificare le attività di migrazione.

Nella tabella seguente viene illustrato un tipico piano di migrazione:

| Iterazione di migrazione | Data di inizio | Data di fine stimata | Dipendenze | Durata stimata (in giorni) | Dettagli aggiuntivi/Azioni |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |   |   |   |   |   |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |   |   |   |   |   |

Come illustrato nella tabella precedente, è utile seguire un formato di denominazione specifico per identificare le iterazioni di migrazione, ad esempio: **PRDCLONE** per l&#39;ambiente AEM di origine, **AUTHOR/PUBLISH** per l&#39;ambiente AEM as a Cloud Service, **CSSTAGE-AUTHOR** per l&#39;istanza AEM as a Cloud Service e così via.

Alcuni dettagli importanti che influenzano il piano di migrazione:

**Numero totale di estrazioni richieste**

* Le estrazioni di authoring e pubblicazione in ambienti specifici sono considerate due estrazioni parallele in quanto sono indipendenti l’una dall’altra.
* Numero di estrazioni integrative basate sulla crescita dell’archivio in periodi di tempo specifici.

**Numero totale di acquisizioni richieste**

* È importante acquisire questo elemento nel piano, poiché un set estratto può essere acquisito in più ambienti Cloud Service.
* Numero di acquisizioni integrative.
* La migrazione del contenuto da Source Author all’istanza Cloud Service Author e da Source Publish a Cloud Service Publish è la best practice per evitare di acquisire tutti i contenuti di Author in Cloud Service Publish.

### Tracciamento migrazione {#migration-tracker}

Puoi utilizzare il tracciatore della migrazione per annotare i tempi sia per le esecuzioni iniziali che per quelle integrative. Questi punti dati ti aiuteranno a formulare requisiti realistici di blocco dei contenuti prima dell’integrazione finale.

Il tracker ti aiuterà anche a:

* Identifica eventuali deviazioni dal planner che richiedono adeguamenti nei timeline del piano o del lancio
* Fornire uno stato realistico che possa essere utilizzato in tutte le comunicazioni necessarie
* Pianificare migrazioni di backup iniziali o future

La tabella seguente illustra un tracker di migrazione funzionale:

| Source (Ambiente/Istanza/URL) | Destinazione (ambiente/istanza/URL) | Nome e tipo del set di migrazione (iniziale o superiore) | Dimensioni set di migrazione (MB) | Mappatura utenti (sì/no) | Durata estrazione (inizio, fine, tempo impiegato) | Durata acquisizione (inizio, fine, tempo impiegato) | Problemi / Risoluzioni / Dettagli |
|---|---|---|---|---|---|---|---|
|   |   |   |   |   |   |   |   |

## Strategia e tempistica di migrazione dei contenuti {#content-strategyand-timeline}

Nella sezione seguente sono illustrati i passaggi importanti e le attività associate che è possibile utilizzare per formulare una strategia e una tempistica di migrazione dei contenuti.

![Passaggi per formulare una strategia di migrazione](/help/journey-migration/assets/content-migration2.png)

### Filtraggio {#fitment}

* Eseguire la pulizia delle revisioni, la raccolta di oggetti inattivi dell’archivio dati e i controlli di coerenza dei dati. Vedi anche [Preparazione per il lancio](#preparing-for-go-live)
* [Raccogli statistiche](#gathering-data) sull&#39;archivio di origine di AEM:
   * Dimensione archivio segmenti
   * Dimensione archivio indice
   * Numero di pagine
   * Numero di risorse
   * Numero di utenti e gruppi
* Scopri se le seguenti funzioni sono abilitate nell’origine di AEM (necessaria anche in AEM as a Cloud Service):
   * Applicazione di tag avanzati
   * Ricerca per affinità
   * Cerca il testo che contiene nei documenti Word e Pdf
* Raccogli il report [Best Practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* Importa in [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * Rivedi i consigli di analisi automatica per assicurarti che AEM as a Cloud Service possa gestire i requisiti di storage.
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
* Esegui almeno una migrazione completa e [integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) dal clone di produzione all&#39;ambiente non di produzione AEM as a Cloud Service
* Risolvi eventuali problemi come:
   * Spazio su disco nell’origine AEM
   * Connettività tra l’origine di AEM e AEM as a Cloud Service
   * Qualsiasi [limitazione relativa all&#39;acquisizione](go-live.md#known-limitations).
* Registra il tempo impiegato per [l&#39;estrazione e l&#39;acquisizione](#gathering-data):
   * Conoscere la quantità di contenuti aggiunti alla settimana
   * Estrapolare i tempi misurati dalla bozza di migrazione per creare un [piano di migrazione](#migration-plan).

## Passaggio successivo {#what-is-next}

Dopo aver compreso a fondo come valutare se l&#39;installazione di AEM è pronta per essere spostata sul cloud, mentre impariamo a utilizzare gli strumenti necessari per prepararla, è ora di passare alla [fase di pubblicazione](/help/journey-migration/go-live.md).
