---
title: Configurazione del team di sviluppo Enterprise
description: Scopri come configurare e scalare il team di sviluppo Enterprise e come supportare il processo di sviluppo con AEM as a Cloud Service.
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 40%

---

# Configurazione del team di sviluppo Enterprise per AEM as a Cloud Service {#enterprise-setup}

Scopri come configurare e scalare il team di sviluppo Enterprise e come AEM (Adobe Experience Manager) as a Cloud Service può supportare il processo di sviluppo.

## Introduzione {#introduction}

Per supportare i clienti con configurazioni di sviluppo di livello Enterprise, AEM as a Cloud Service si integra completamente con Cloud Manager e le relative [pipeline CI/CD &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) appositamente progettate. Queste pipeline e servizi sono progettati in base alle best practice e garantiscono [test accurati e la qualità più elevata del codice](/help/implementing/cloud-manager/code-quality-testing.md).

## Supporto di Cloud Manager per la configurazione del team di sviluppo aziendale {#cloud-manager}

Per garantire un onboarding rapido, Cloud Manager fornisce tutto il necessario per iniziare a sviluppare esperienze digitali fin da subito, incluso un archivio Git per archiviare personalizzazioni, che vengono quindi generate, verificate e distribuite da Cloud Manager.

Con Cloud Manager i team di sviluppo possono apportare modifiche frequenti senza dipendere dal personale Adobe.

In Cloud Manager sono disponibili tre tipi di ambienti.

* Ambiente di sviluppo
* Ambiente di staging
* Produzione

Il codice può essere distribuito negli ambienti di sviluppo con una pipeline non di produzione. Per gli ambienti di staging e produzione, che sono sempre forniti in combinazione e quindi garantiscono la convalida prima della distribuzione nell’ambiente di produzione come best practice, una pipeline di produzione utilizza [gate di qualità](/help/implementing/cloud-manager/custom-code-quality-rules.md) per convalidare il codice dell’applicazione e le modifiche alla configurazione.

La pipeline di produzione distribuisce il codice e la configurazione nell’ambiente di staging, esegue il test dell’applicazione e infine la distribuisce nell’ambiente di produzione.

Un SDK Cloud Service sempre aggiornato con i più recenti miglioramenti di AEM as a Cloud Service consente lo sviluppo locale utilizzando direttamente l’hardware locale dello sviluppatore. Questo approccio consente uno sviluppo rapido con tempi di risposta molto ridotti. Di conseguenza, il team di sviluppo può lavorare dal proprio ambiente locale conosciuto e scegliere tra un’ampia gamma di strumenti di sviluppo, eseguendo il push negli ambienti di sviluppo o produzione quando ritenuto opportuno.

Cloud Manager supporta configurazioni flessibili di più team che possono essere regolate in base alle esigenze di un&#39;azienda. Per garantire distribuzioni stabili tra più team, la pipeline categorica di Cloud Manager convalida e verifica il codice da tutti i team insieme. Questo approccio aiuta a evitare situazioni in cui le modifiche di un team influiscono sulla produzione di tutti i team.

## Esempio reale {#real-world-example}

Ogni azienda ha requisiti diversi, che riguardano configurazione del team, processi e flussi di lavoro per lo sviluppo. Adobe utilizza la configurazione descritta di seguito per diversi progetti che forniscono esperienze per AEM as a Cloud Service.

Ad esempio, le applicazioni Adobe Creative Cloud, come Adobe Photoshop o Adobe Illustrator, mettono a disposizione degli utenti risorse di contenuti quali tutorial, esempi e guide. Le applicazioni client utilizzano i contenuti di AEM as a Cloud Service in modo headless. Effettuano chiamate API al livello di pubblicazione di AEM Cloud per recuperare contenuti strutturati come flussi JSON. Inoltre, la [rete per la distribuzione dei contenuti (CDN) in AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#content-delivery) viene utilizzata per fornire contenuti strutturati e non strutturati con prestazioni ottimali.

I team che contribuiscono a questo progetto si attengono al processo indicato di seguito.

Ogni team utilizza il proprio flusso di lavoro di sviluppo e dispone di un archivio Git separato. Per i progetti di onboarding viene utilizzato un ulteriore archivio Git condiviso. Questo archivio Git contiene la struttura radice dell’archivio Git di Cloud Manager, inclusa la configurazione Dispatcher condivisa.

L’onboarding di un nuovo progetto richiede l’inserimento nel file di progetto Maven del reattore nella directory principale dell’archivio Git condiviso. Per la configurazione di Dispatcher, viene creato un nuovo file di configurazione all’interno del progetto Dispatcher. La configurazione principale di Dispatcher quindi include questo file. Ogni team è responsabile del proprio file di configurazione di Dispatcher. Le modifiche all’archivio Git condiviso sono rare e di solito sono necessarie solo quando viene effettuato l’onboarding di un nuovo progetto. Il lavoro principale viene svolto da ogni team di progetto all’interno del proprio archivio Git.

![Diagramma del flusso di lavoro](/help/implementing/cloud-manager/assets/team-setup1.png)

Ogni archivio Git viene configurato utilizzando [Archetipo progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview) e segue pertanto le best practice per la configurazione dei progetti AEM. L’unica eccezione è la configurazione di Dispatcher, che viene eseguita nell’archivio Git condiviso come descritto sopra.

Ogni team utilizza un flusso di lavoro Git semplificato con due rami + N, seguendo il modello di flusso Git:

* Un ramo della versione stabile contiene il codice di produzione.

* Un ramo di sviluppo contiene il codice di sviluppo più aggiornato.

* Per ogni funzione viene creato un nuovo ramo.

Lo sviluppo viene eseguito in un ramo della funzione. Quando la funzione matura, viene unita al ramo di sviluppo. Le funzioni completate e convalidate vengono prelevate dal ramo di sviluppo e unite al ramo stabile.

Tutte le modifiche vengono effettuate tramite PR (Richieste pull). I gate di qualità convalidano automaticamente ogni PR. Per il controllo di qualità del codice si utilizza Sonar e si eseguono una serie di suite di test per garantire che il nuovo codice non introduca alcuna regressione.

La configurazione nell’archivio Git di Cloud Manager ha due rami.

* Un ramo della versione stabile contiene il codice di produzione di tutti i team.
* Un ramo di sviluppo contiene il codice di sviluppo di tutti i team.

Ogni push all&#39;archivio Git di un team nel ramo di sviluppo o nel ramo stabile attiva un&#39;azione [GitHub](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code).

Tutti i progetti presentano la stessa configurazione per il ramo stabile. Un push al ramo stabile di un progetto viene inviato automaticamente al ramo stabile nell’archivio Git di Cloud Manager. Un push al ramo stabile attiva la pipeline di produzione in Cloud Manager. Ogni push da parte di un team in un ramo stabile attiva la pipeline di produzione. La distribuzione di produzione viene aggiornata se tutti i gate di qualità superano il test.

![Diagramma push](/help/implementing/cloud-manager/assets/team-setup2.png)

I push al ramo di sviluppo vengono gestiti in modo diverso. Anche il push a un ramo di sviluppo nell’archivio Git di un team attiva un’azione GitHub. Questa azione invia automaticamente il codice nel ramo di sviluppo nell’archivio Git di Cloud Manager. Tuttavia, questo push di codice non attiva automaticamente la pipeline non di produzione. Una chiamata all’API di Cloud Manager la attiva.

L’esecuzione della pipeline di produzione include il controllo del codice di tutti i team tramite i gate di qualità forniti. Dopo aver distribuito il codice nell’ambiente di staging, vengono eseguiti i test e i controlli in modo che tutto funzioni come previsto. Quando tutti i gate vengono superati, le modifiche vengono implementate nell’ambiente di produzione senza interruzioni o tempi di inattività.

Per lo sviluppo locale, si utilizza l’[SDK di AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing). Il SDK consente di configurare un’istanza di Author, Publish e Dispatcher locale. Questo flusso di lavoro consente lo sviluppo offline e tempi di risposta rapidi. A volte per lo sviluppo viene utilizzato solo l’ambiente di authoring, ma configurare rapidamente gli ambienti Dispatcher e di pubblicazione consente di eseguire test locali prima di eseguire il push nell’archivio Git.

In genere, i membri di ogni team estraggono il codice dal Git condiviso per il proprio codice di progetto. Non è necessario estrarre altri progetti perché i progetti sono indipendenti.

![Ritiro locale e SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

Questa configurazione reale può essere utilizzata come blueprint e personalizzata in base alle specifiche esigenze aziendali. Il concetto di ramificazione e unione flessibile di Git consente di utilizzare varianti dei flussi di lavoro di cui sopra, personalizzate in base alle esigenze di ogni team. AEM as a Cloud Service supporta tutte queste varianti senza dover rinunciare al valore di base della pipeline categorica di Cloud Manager.

>[!TIP]
>
>Per ulteriori informazioni su questa configurazione, consulta [Utilizzare più archivi Git di Source](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/managing-code/multiple-git-repos#managing-code).

### Considerazioni per una configurazione con più team {#considerations}

Con l’archivio Git di Cloud Manager e la pipeline di produzione, l’intero codice di produzione passa sempre attraverso tutti i gate di qualità, considerandolo come un’unica unità di distribuzione. In questo modo il sistema di produzione è sempre attivo, senza interruzioni o tempi di inattività.

Al contrario, in assenza di un tale sistema, poiché ogni team può distribuire separatamente, esiste il rischio che un aggiornamento effettuato da un singolo team possa causare problemi di stabilità della produzione. Inoltre, per distribuire gli aggiornamenti è necessario essere coordinati e pianificare i tempi di inattività. Con il costante aumento del numero dei team, coordinarsi diventa molto più complesso e rapidamente ingestibile.

Se viene rilevato un problema al livello dei gate di qualità, la produzione non viene influenzata e il problema può essere rilevato e risolto senza necessità di intervento del personale Adobe. Se non si integra Cloud Service e non si eseguono test continui dell’intera implementazione, le implementazioni parziali possono causare interruzioni che richiedono il ripristino dello stato precedente di una richiesta o persino un ripristino completo da un backup. I test parziali possono anche causare problemi aggiuntivi che devono essere risolti in un secondo momento, che richiedono ancora una volta il coordinamento e il supporto del personale Adobe.

>[!TIP]
>
>Per qualsiasi configurazione con più team, è fondamentale definire un modello di governance e una serie di standard a cui devono attenersi tutti i team. Il blueprint precedente per una configurazione con più team è scalabile per un numero maggiore di team e può essere utilizzato come punto di partenza.
