---
title: Fase di implementazione
description: Assicurati che il codice e il contenuto siano pronti per la migrazione al cloud
source-git-commit: b6667e19ae111685ab4832a1859a62164b4e31c5
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 9%

---

# Fase di implementazione {#implementation-phase}

Nella fase di implementazione del percorso, esplorerai gli strumenti attraverso i quali puoi rendere il codice e il contenuto pronto per essere spostato in AEM as a Cloud Service.

## La storia finora {#story-so-far}

Nelle parti precedenti del percorso, avete attraversato [acquisire familiarità con le modifiche in AEM as a Cloud Service](/help/journey-migration/getting-started.md), nonché determinare se la distribuzione è pronta per essere spostata nel cloud con l’ [fase di preparazione](/help/journey-migration/readiness.md).

Questo articolo continua con consigli su come utilizzare gli strumenti forniti da Adobe per assicurarsi che il codice e il contenuto siano pronti per essere spostati nel cloud.

## Obiettivo {#objective}

Il presente documento mira a:

* Ti presento Cloud Manager, AEM integrazione continua e framework di consegna utilizzati per distribuire il codice a AEM as a Cloud Service
* Massima rapidità con lo strumento di trasferimento dei contenuti
* Descrivi gli strumenti di refactoring del codice da utilizzare per modernizzare il codice per AEM as a Cloud Service

## Utilizzo di Cloud Manager {#using-cloud-manager}

Prima di iniziare, devi acquisire familiarità con Cloud Manager, in quanto è l’unico meccanismo per distribuire il codice AEM as a Cloud Service.

Cloud Manager consente alle organizzazioni di gestire autonomamente AEM nel cloud. Include un framework di integrazione continua e distribuzione continua (CI/CD, Continuous Integration/Continuous Delivery) che consente ai team IT e ai partner dell’implementazione di accelerare la distribuzione di personalizzazioni o aggiornamenti senza compromettere prestazioni o sicurezza.

Per acquisire familiarità con l’utilizzo di Cloud Manager, consulta le risorse seguenti:

* [Onboarding per Experience Manager as a Cloud Service](/help/onboarding/home.md) per comprendere le risorse disponibili sull’onboarding per Experience Manager as a Cloud Service.

* [Integrazione di Git con Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) per informazioni sull’utilizzo di un archivio Git singolo per implementare il codice.

* [Configurazione di Adobe Experience as a Cloud Service](/help/security/ims-support.md#aem-configuration) per informazioni sulla gestione dei prodotti e dell’accesso degli utenti in Admin Console.

## Utilizza gli strumenti forniti dall’Adobe per rendere i contenuti e il codice Cloud pronti {#use-tools-to-make-code-and-content-cloud-ready}

I passaggi esatti della transizione al Cloud Service dipendono dai sistemi acquistati e dalle procedure di sviluppo software seguite.

La figura seguente mostra i passaggi principali della fase che comporta la conversione del codice e del contenuto da utilizzare con AEM as a Cloud Service:

![immagine](/help/journey-migration/assets/exec-image1.png)

Inizieremo a fornire dettagli sugli strumenti necessari per ottenere questo risultato nei capitoli seguenti.

## Migrazione dei contenuti {#content-migration}

Per migrare il contenuto dall’istanza AEM corrente all’istanza di Cloud Service, puoi utilizzare lo strumento Content Transfer (Trasferimento contenuti) di Adobe.

Con questo strumento, puoi specificare il sottoinsieme di contenuti che desideri trasferire dall’istanza AEM sorgente all’istanza AEM Cloud Service.

La migrazione dei contenuti è un processo in più fasi che richiede pianificazione, tracciamento e collaborazione tra team diversi.

Per informazioni complete sul funzionamento dello strumento e su come consigliamo di utilizzarlo, consulta la sezione [Documentazione dello strumento Content Transfer (Trasferimento contenuti)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## Refactoring del codice {#code-refactor}

### Configurazione per lo sviluppo {#set-up-for-development}

È il momento di iniziare a ripristinare le funzionalità esistenti in modo che siano compatibili con i Cloud Services.

Per eseguire questa operazione, è necessario consultare la documentazione che descrive in dettaglio gli strumenti di base necessari per iniziare a eseguire il refactoring del codice:


* Durante la pianificazione, è opportuno disporre di un elenco di aree da ristrutturare per essere compatibili con AEM as a Cloud Service. Puoi rivedere [Linee guida per lo sviluppo](/help/implementing/developing/introduction/development-guidelines.md) per ulteriori dettagli su come eseguire il refactoring e ottimizzare il codice per Cloud Service.
* Scopri come [Gestire le configurazioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) in AEM as a Cloud Service.
* Scopri come configurare un ambiente di sviluppo locale scaricando il [AEM SDK as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* Infine, familiarizza con il [API Java as a Cloud Service AEM](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Inoltre, puoi anche:

* Guarda questo video per scoprire come installare localmente l’SDK di Dispatcher:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Guarda questo video per scoprire come configurare l’SDK di Dispatcher:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

### Un cambiamento di mentalità {#a-change-in-mindset}

Lo sviluppo e l&#39;esecuzione del codice in AEM as a Cloud Service richiede una modifica nella mentalità. Il codice deve essere resiliente, soprattutto poiché un’istanza potrebbe essere arrestata in qualsiasi momento. Il codice in esecuzione in Cloud Service deve tener conto di essere sempre in esecuzione in un cluster. Ciò significa che ci sono sempre in esecuzione più di un’istanza.

Alcune modifiche sono necessarie affinché i progetti Maven AEM siano compatibili con il cloud. AEM as a Cloud Service richiede una separazione *content* e *codice* in pacchetti distinti per la distribuzione in AEM:

* `/apps` e `/libs` sono considerate aree immutabili di AEM in quanto non possono essere modificate dopo l’inizio di AEM (cioè in fase di runtime). Ciò include le operazioni di creazione, aggiornamento o eliminazione. Eventuali tentativi di modifica di un’area immutabile in fase di runtime avranno esito negativo.

* Tutto il resto nell’archivio (ad esempio, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`) sono tutte aree mutabili, il che significa che possono essere modificate in fase di runtime.

Per saperne di più, consulta la [Struttura del pacchetto consigliata](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) documentazione.


### Strumenti di migrazione cloud {#cloud-migration-tools}

Adobe fornisce diversi strumenti per accelerare alcune delle attività di refactoring del codice. Comprendere questi strumenti e i problemi che risolvono ridurrà la complessità e il tempo della migrazione.

* [Migrazione dei flussi di lavoro delle risorse](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md), uno strumento utilizzato per migrare automaticamente i flussi di lavoro di elaborazione delle risorse
* [Dispatcher Converter](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md), uno strumento che converte le configurazioni esistenti di Dispatcher in un formato pronto per AEM as a Cloud Service.
* [Modernizzatore dell&#39;archivio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en), uno strumento che prende un progetto Multimode AEM come input e lo converte in uno as a Cloud Service AEM
* [Convertitore indice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en), uno strumento che converte gli indici in un modulo compatibile con AEM as a Cloud Service
* [Strumenti di modernizzazione](/help/journey-migration/refactoring-tools/aem-modernization-tools.md), una suite di utilità che può essere utilizzata per convertire le funzionalità AEM legacy alle funzionalità moderne e supportate di AEM as a Cloud Service.

Dopo aver configurato l’ambiente di sviluppo locale, acquisisci familiarità con l’SDK as a Cloud Service AEM consultando il [documentazione](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### Pianificare un blocco del codice {#schedule-a-code-freeze}

Per gestire lo sviluppo del codice in corso sul tuo AEM attivo insieme alle attività di refactoring del codice come parte del percorso di transizione, ti consigliamo di pianificare un periodo di blocco del codice fino a quando non avrai completato la ristrutturazione del progetto Maven per renderlo compatibile con AEM as a Cloud Service.

Al termine della ristrutturazione del progetto, puoi riprendere lo sviluppo del nuovo codice in base a questa nuova struttura. Questo riduce gli errori della pipeline di Cloud Manager durante l’implementazione e il test del codice.

>[!NOTE]
>Le attività di trasferimento dei contenuti e refactoring del codice non devono necessariamente essere eseguite in sequenza. Queste attività possono essere svolte l’una indipendentemente dall’altra. Tuttavia, è necessaria la giusta struttura di progetto per garantire il corretto rendering del contenuto nell’ambiente Cloud Service.

## Best practice per l’implementazione e il test del codice {#best-practices}

La pipeline di Cloud Manager supporta l’esecuzione di test eseguiti sull’ambiente stage.

Segui le best practice riportate nei documenti seguenti per quanto riguarda il test della qualità del codice:

* [Test della qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md), un documento che descrive il processo di scrittura degli script di test e spiega il concetto di copertura consigliata di almeno il 50%.
* [Regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md) che ha lo scopo di descrivere le regole di qualità del codice personalizzato eseguite da Cloud Manager create in base alle best practice di AEM Engineering.

## Preparazione per il lancio {#preparing-for-go-live}

La preparazione del sistema di origine per la migrazione comporta l’esecuzione di attività a livello di sistema e AEM amministratore. Puoi iniziare verificando che l’archivio dei contenuti sia in buono stato controllando la [pulizia revisioni](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) e [raccolta oggetti inattivi dell&#39;archivio dati](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html) stato dell&#39;attività. Se esegui AEM versione 6.3 (in quanto lo strumento Content Transfer (Trasferimento contenuti) è compatibile a partire dalla versione 6.3), si consiglia di eseguire la compattazione offline, seguita dalla raccolta degli oggetti inattivi nell’archivio dati.

[Controllo della coerenza dei dati](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) è consigliato in tutte le versioni di AEM per garantire che l’archivio dei contenuti sia in buono stato per avviare le attività di migrazione.

L&#39;accesso a livello di amministratore di sistema è necessario per installare e configurare [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

È inoltre consigliabile esaminare tutte le risorse, le pagine, i progetti AEM, gli utenti e i gruppi non utilizzati per risparmiare tempo sulla migrazione. Consulta la sezione [Stato dell’archivio dei contenuti](#repository-health) sezione .

### Stato dell’archivio dei contenuti {#repository-health}

Una volta effettuato l’accesso a un [clone di produzione](#proof-of-migration) è stabilito procedere per controllare lo stato di salute dell&#39;archivio. Come indicato nella sezione precedente, l’obiettivo è quello di pulire e compattare l’archivio sulla sorgente prima di avviare la migrazione. Questo passaggio potrebbe potenzialmente risparmiare molto tempo altrimenti si spenderà per la risoluzione dei problemi una volta avviata la migrazione.

| Elemento azione | Aree principali |
|---------|----------|
| Utenti, gruppi e autorizzazioni | È necessario comprendere il volume di utenti, gruppi e la complessità intorno alle appartenenze. Cerca le opportunità per ripulire gli utenti e i gruppi inutilizzati nella sorgente prima della migrazione. |
| Elaborazione delle risorse incompleta | Prova a completare l’elaborazione delle risorse nel sistema di origine prima di avviare la migrazione per evitare potenziali problemi AEM migrazione as a Cloud Service dopo la migrazione. |
| Salute dei contenuti | È consigliabile eseguire una query per individuare il contenuto non valido ed eliminarlo prima di avviare la migrazione. Ad esempio, cerca le risorse o le pagine prive di rendering originali o bloccate nell’elaborazione del flusso di lavoro. Vedi anche [Salute risorse](#asset-health). |

## Raccolta dati {#gathering-data}

>[!NOTE]
> La [Strategia e cronologia di migrazione dei contenuti](#content-strategy-and-timeline) sezione ulteriori dettagli su come estrapolare i dati raccolti e creare un piano di migrazione.

La raccolta dei dati può essere utile per pianificare le attività di migrazione e le attività associate. I tempi di estrazione e acquisizione sono particolarmente utili perché i punti dati possono essere associati a una dimensione specifica del set di migrazione. Come tale, questi punti dati possono essere estrapolati per elaborare un piano:

* Quantità totale di tempo impiegato [estrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* Quantità totale di tempo impiegato [ingestione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* Quantità totale di tempo impiegato per l&#39;integrazione [estrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* Quantità totale di tempo impiegato per l&#39;integrazione [ingestione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)

Un altro punto dati importante è il tempo necessario per completare il [mappatura utente](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), se questa è associata alla migrazione dei contenuti. Puoi prendere in considerazione questo punto dati per stime più realistiche, in quanto verrà aggiunto alla timeline di estrazione complessiva e potrebbe non essere necessario eseguirlo durante le operazioni integrative.

Questi punti dati possono anche essere utili [Stabilire i KPI](/help/journey-migration/readiness.md#establish-kpis) e altre attività relative alla migrazione.

### Piano di migrazione {#migration-plan}

In base ai punti dati raccolti (vedi sopra), è possibile creare un piano di migrazione che può essere integrato in un piano di progetto macro. Questo passaggio consentirà a tutte le principali parti interessate di visualizzare e pianificare le attività di migrazione.

La tabella seguente illustra un tipico piano di migrazione:

| Iterazione di migrazione | Data iniziale | Data di fine stimata | Dipendenze | Durata stimata (in giorni) | Dettagli aggiuntivi / Elementi azione |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |  |  |  |  |  |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |  |  |  |  |  |

Come puoi vedere nella tabella precedente, è utile seguire un formato di denominazione specifico per identificare le iterazioni di migrazione, ad esempio: **PRDCLONE** per l&#39;ambiente AEM sorgente , **AUTORE/PUBBLICA** per l&#39;ambiente AEM as a Cloud Service, **CSSTAGE-AUTHOR** per l&#39;istanza AEM as a Cloud Service e così via.

Alcuni importanti dettagli che influenzano il piano di migrazione:

**Numero totale di estrazioni richieste**

* Le estrazioni di authoring e pubblicazione in ambienti specifici sono considerate come due estrazioni parallele indipendenti l’una dall’altra.
* Numero di estrazioni Top Up basate sulla crescita dell&#39;archivio in specifici periodi di tempo.

**Numero totale di gestioni richieste**

* È importante acquisire questo elemento nel piano, in quanto un set estratto può essere acquisito in ambienti con più Cloud Service.
* Numero di acquisizioni principali.
* La migrazione del contenuto dall’istanza di authoring sorgente all’istanza di authoring del servizio Cloud e da Pubblicazione sorgente al Cloud Service Pubblicazione è la best practice per evitare di acquisire tutti i contenuti di authoring nel Cloud Service Pubblicazione.

### Tracker migrazione {#migration-tracker}

Puoi utilizzare il tracciamento della migrazione per annotare i tempi per le esecuzioni iniziali e superiori. Questi punti dati ti aiuteranno a formulare requisiti realistici di blocco dei contenuti prima dell’integrazione finale.

Il tracker ti aiuterà anche a:

* Identificare eventuali deviazioni dal planner che richiedono adeguamenti nel piano o nelle timeline go-live
* Fornire uno stato realistico che possa essere utilizzato in tutte le comunicazioni necessarie
* Pianificare migrazioni integrative iniziali o future

La tabella seguente illustra un tracker funzionale di migrazione:

| Origine (Ambiente/Istanza/URL) | Destinazione (Ambiente/Istanza/URL) | Nome set di migrazione, tipo (iniziale o superiore) | Dimensioni set di migrazione (MB) | Mappatura utente (Sì / No) | Durata estrazione (inizio, fine, ora) | Durata dell’acquisizione (inizio, fine, ora presa) | Problemi / Risoluzioni / Dettagli |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

## Strategia e cronologia di migrazione dei contenuti {#content-strategyand-timeline}

La sezione seguente illustra i passaggi importanti e le attività associate che possono essere utilizzati per formulare una strategia e una cronologia di migrazione dei contenuti.

![immagine](/help/journey-migration/assets/content-migration2.png)

### Fusto {#fitment}

* Esegui il cleanup delle revisioni, la raccolta degli oggetti inattivi nell’archivio dati e i controlli di coerenza dei dati. Vedi anche [Preparazione per il lancio](#preparing-for-go-live)
* [Raccogliere statistiche](#gathering-data) informazioni sull&#39;archivio di origine AEM:
   * Dimensione dell’archivio segmenti
   * Dimensione dell&#39;archivio indici
   * Numero di pagine
   * Numero di attività
   * Numero di utenti e gruppi
* Verifica se le seguenti funzioni sono abilitate nell’origine AEM (richiesta anche in AEM as a Cloud Service):
   * Assegnazione tag avanzati
   * Ricerca per similarità
   * Ricerca di testo contenuto in documenti Word e pdf
* Raccolta di Best Practice Analyzer [rapporto](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* Importa in [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * Rivedi la raccomandazione di analisi automatica per assicurarti che AEM as a Cloud Service possa gestire i requisiti di storage.
* Crea un ticket di Adobe per eventuali chiarimenti prima di continuare con il piano di migrazione.

### Prova della migrazione {#proof-of-migration}

* Richiedi un clone di produzione che:
   * Si trova nella stessa zona di rete
   * Fornirà contenuti di produzione come utenti e gruppi
   * Duplica l’authoring e la pubblicazione: un nodo ciascuno in caso di cluster o pubblicazione di farm
* Scegli un sottoinsieme del contenuto da migrare in modo che:
   * È una combinazione di tutti i tipi di contenuto disponibili
   * Contiene tutti gli utenti e i gruppi nel caso [mappatura utente](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md) obbligatorio
* Include il 25% del contenuto o fino a 1 TB di contenuto, a seconda di quale valore è minore.
* Esegui almeno un ciclo completo e [integrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) migrazione, dal clone di produzione all’ambiente non di produzione as a Cloud Service AEM
* Risolvi eventuali problemi potenziali come:
   * Spazio su disco nella sorgente AEM
   * Connettività tra la sorgente AEM e AEM as a Cloud Service
   * Qualsiasi [limitazioni relative all’acquisizione](go-live.md#known-limitations).
* Registrare il tempo necessario [estrazione e acquisizione](#gathering-data):
   * Scopri quanti contenuti vengono aggiunti alla settimana
   * Estrapolare i tempi misurati dalla prova della migrazione per creare un [piano di migrazione](#migration-plan).

## Novità {#what-is-next}

Una volta compreso come valutare se l&#39;installazione AEM è pronta per essere spostata nel cloud, mentre impariamo come utilizzare gli strumenti necessari per renderla pronta, è il momento di passare al [fase di go-live](/help/journey-migration/go-live.md).
