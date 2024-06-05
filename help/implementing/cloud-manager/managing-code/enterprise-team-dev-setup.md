---
title: Configurazione del team di sviluppo Enterprise
description: Scopri come configurare e scalare il team di sviluppo Enterprise e come supportare il processo di sviluppo con AEM as a Cloud Service.
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 95%

---

# Configurazione del team di sviluppo Enterprise per AEM as a Cloud Service {#enterprise-setup}

Scopri come configurare e scalare il team di sviluppo Enterprise e come supportare il processo di sviluppo con AEM as a Cloud Service.

## Introduzione {#introduction}

Per supportare i clienti con configurazioni di sviluppo di livello Enterprise, AEM as a Cloud Service si integra completamente con Cloud Manager e le relative [pipeline CI/CD ](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) appositamente progettate. Queste pipeline e servizi sono progettati in base alle best practice e garantiscono [test accurati e la qualità più elevata del codice](/help/implementing/cloud-manager/code-quality-testing.md).

## Supporto di Cloud Manager per la configurazione del team di sviluppo Enterprise {#cloud-manager}

Per garantire un processo di onboarding rapido, Cloud Manager offre tutto il necessario per iniziare a sviluppare esperienze digitali fin da subito, incluso un archivio Git per archiviare personalizzazioni che vengono poi generate, verificate e distribuite da Cloud Manager.

Con Cloud Manager i team di sviluppo possono apportare modifiche frequenti senza dipendere dal personale Adobe.

In Cloud Manager sono disponibili tre tipi di ambienti.

* Ambiente di sviluppo
* Ambiente di staging
* Produzione

Il codice può essere distribuito negli ambienti di sviluppo con una pipeline non di produzione. Per gli ambienti di staging e produzione, che sono sempre forniti in combinazione e quindi garantiscono la convalida prima della distribuzione nell’ambiente di produzione come best practice, una pipeline di produzione utilizza [gate di qualità](/help/implementing/cloud-manager/custom-code-quality-rules.md) per convalidare il codice dell’applicazione e le modifiche alla configurazione.

La pipeline di produzione distribuisce il codice e la configurazione nell’ambiente di staging, esegue il test dell’applicazione e infine la distribuisce nell’ambiente di produzione.

Grazie all’SDK di Cloud Service, sempre aggiornato con i più recenti miglioramenti per AEM as a Cloud Service, è possibile sviluppare a livello locale utilizzando direttamente l’hardware locale dello sviluppatore o della sviluppatrice. In questo modo lo sviluppo è rapido e i tempi di risposta molto ridotti. Di conseguenza, il team di sviluppo può lavorare dal proprio ambiente locale conosciuto e scegliere tra un’ampia gamma di strumenti di sviluppo, eseguendo il push negli ambienti di sviluppo o produzione quando ritenuto opportuno.

Cloud Manager supporta configurazioni flessibili di più team che possono essere regolate in base alle esigenze dell’azienda. Per garantire distribuzioni stabili con più team ed evitare situazioni in cui un solo team influisce sulla produzione di tutti gli altri, la pipeline categorica di Cloud Manager convalida e verifica sempre il codice da tutti i team.

## Esempio reale {#real-world-example}

Ogni azienda ha requisiti diversi, che riguardano configurazione del team, processi e flussi di lavoro per lo sviluppo. Adobe utilizza la configurazione descritta di seguito per diversi progetti che forniscono esperienze per AEM as a Cloud Service.

Ad esempio, le applicazioni Adobe Creative Cloud, come Adobe Photoshop o Adobe Illustrator, mettono a disposizione degli utenti risorse di contenuti quali tutorial, esempi e guide. Questo contenuto viene utilizzato dalle applicazioni client che utilizzano AEM as a Cloud Service in modo headless, effettuando chiamate API al livello di pubblicazione di AEM Cloud per recuperare il contenuto strutturato come flussi JSON e utilizzando [Content Delivery Network (CDN) in AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#content-delivery) per fornire contenuti strutturati e non strutturati con prestazioni ottimali.

I team che contribuiscono a questo progetto si attengono al processo indicato di seguito.

Ogni team utilizza il proprio flusso di lavoro di sviluppo e dispone di un archivio Git separato. Per i progetti di onboarding viene utilizzato un ulteriore archivio Git condiviso. Tale archivio Git contiene la struttura radice dell’archivio Git di Cloud Manager, inclusa la configurazione del Dispatcher condivisa.

L’onboarding di un nuovo progetto richiede l’inserimento nel file di progetto Maven multi-modulo nella radice dell’archivio Git condiviso. Per la configurazione dispatcher viene creato un nuovo file di configurazione all’interno del progetto dispatcher. Questo file viene quindi incluso dalla configurazione dispatcher principale. Ogni team è responsabile del proprio file di configurazione dispatcher. Le modifiche all’archivio Git condiviso sono rare e di solito sono necessarie solo per effettuare l’onboarding di un nuovo progetto. Le operazioni principali vengono svolto da ogni team di progetto all’interno del proprio archivio Git.

![Diagramma del flusso di lavoro](/help/implementing/cloud-manager/assets/team-setup1.png)

Ogni archivio Git viene configurato utilizzando l’[archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) e segue pertanto le best practice per la creazione di progetti AEM. L’unica eccezione è la configurazione dispatcher, che viene eseguita nell’archivio Git condiviso come descritto in precedenza.

Ogni team utilizza un flusso di lavoro Git semplificato con due rami + N, seguendo il modello di flusso Git:

* Un ramo della versione stabile contiene il codice di produzione.

* Un ramo di sviluppo contiene il codice di sviluppo più aggiornato.

* Per ogni funzione viene creato un nuovo ramo.

Lo sviluppo viene eseguito in un ramo della funzione. Quando la funzione è pronta, viene unita al ramo di sviluppo. Le funzioni completate e convalidate vengono prelevate dal ramo di sviluppo e unite al ramo stabile.

Tutte le modifiche vengono effettuate tramite richieste pull (PR). Ogni PR viene convalidato automaticamente dai gate di qualità. Per il controllo di qualità del codice si utilizza Sonar e si eseguono una serie di suite di test per garantire che il nuovo codice non introduca alcuna regressione.

La configurazione nell’archivio Git di Cloud Manager presenta due rami.

* Un ramo della versione stabile contiene il codice di produzione di tutti i team.
* Un ramo di sviluppo contiene il codice di sviluppo di tutti i team.

Ogni push all’archivio Git di un team nel ramo di sviluppo o nel ramo stabile attiva un’[azione GitHub](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code).

Tutti i progetti presentano la stessa configurazione per il ramo stabile. Un push al ramo stabile di un progetto viene inviato automaticamente al ramo stabile nell’archivio Git di Cloud Manager. La pipeline di produzione in Cloud Manager è configurata per essere attivata da un push al ramo stabile. La pipeline di produzione viene quindi eseguita da ogni push in un ramo stabile eseguito dai team, mentre la distribuzione in produzione viene aggiornata se supera tutti i gate di qualità.

![Diagramma push](/help/implementing/cloud-manager/assets/team-setup2.png)

I push al ramo di sviluppo vengono gestiti in modo diverso. Mentre un push a un ramo di sviluppo nell’archivio Git di un team attiva anche un’azione GitHub e il codice viene inviato automaticamente nel ramo di sviluppo dell’archivio Git di Cloud Manager, la pipeline non di produzione non viene attivata automaticamente dal push del codice. Viene attivata da una chiamata all’API di Cloud Manager.

L’esecuzione della pipeline di produzione include il controllo del codice di tutti i team tramite i gate di qualità forniti. Dopo aver distribuito il codice nell’ambiente di staging, vengono eseguiti test e audit per garantire che tutto funzioni come previsto. Se il controllo di tutti i gate viene superato, le modifiche vengono implementate nell’ambiente di produzione senza interruzioni o tempi di inattività.

Per lo sviluppo locale, si utilizza l’[SDK di AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing). L’SDK consente di configurare un’istanza di Author, Publish e Dispatcher locale. In questo modo lo sviluppo può avvenire offline con tempi di risposta rapidi. A volte per lo sviluppo si utilizza solo l’ambiente di Author, ma configurare rapidamente gli ambienti Dispatcher e Publish consente di eseguire test completi a livello locale prima di eseguire il push nell’archivio Git.

In genere, i membri di ogni team estraggono il codice dall’archivio Git condiviso per il codice dei progetti proprietari. Non è necessario estrarre altri progetti, in quanto ognuno è indipendente.

![Ritiro locale e SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

Questa configurazione reale può essere utilizzata come blueprint e personalizzata in base alle specifiche esigenze aziendali. Il concetto di ramificazione e unione flessibile degli archivi Git consente di utilizzare delle varianti dei flussi di lavoro precedenti in base alle esigenze specifiche dei team. AEM as a Cloud Service supporta tutte queste varianti senza dover rinunciare al valore di base della pipeline categorica di Cloud Manager.

>[!TIP]
>
>Per ulteriori informazioni su questa configurazione, consulta [Utilizzo di più archivi Git di origine](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html?lang=it#managing-code).

### Considerazioni per una configurazione con più team {#considerations}

Con l’archivio Git e la pipeline di produzione di Cloud Manager, l’intero codice di produzione viene sempre controllato da tutti i gate di qualità, da cui viene considerato alla stregua di un’unica unità di distribuzione. In questo modo il sistema di produzione è sempre attivo, senza interruzioni o tempi di inattività.

In assenza di un tale sistema, poiché ogni team può eseguire la distribuzione separatamente, c’è il rischio che l’aggiornamento apportato da un singolo team possa portare a problemi di stabilità della produzione. Inoltre, per distribuire gli aggiornamenti è necessario essere coordinati e pianificare i tempi di inattività. Con il costante aumento del numero dei team, coordinarsi diventa molto più complesso e rapidamente ingestibile.

Se viene rilevato un problema al livello dei gate di qualità, la produzione non viene influenzata e il problema può essere rilevato e risolto senza necessità di intervento del personale Adobe. Se non si integra Cloud Service e non si eseguono test continui dell’intera distribuzione, le distribuzioni parziali possono causare interruzioni che richiedono il ripristino dello stato precedente di una richiesta o persino un ripristino completo da un backup. Anche l’esecuzione parziale dei test può far sorgere altri problemi che dovranno essere risolti richiedendo nuovamente il coordinamento e il supporto del personale Adobe.

>[!TIP]
>
>Per qualsiasi configurazione con più team è fondamentale definire un modello di governance e una serie di standard a cui dovranno attenersi tutti i team. Il blueprint precedente per una configurazione con più team è scalabile per un numero maggiore di team e può essere utilizzato come punto di partenza.
