---
title: Comprendere Cloud Manager e il flusso di lavoro per la creazione di siti rapidi
description: Scopri Cloud Manager e come unisce il nuovo processo di creazione rapida dei siti.
source-git-commit: efeb97d4bd7e7c11ec2c0ba1244a32b8b9affdab
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 1%

---


# Comprendere Cloud Manager e il flusso di lavoro per la creazione di siti rapidi {#understand-cloud-manager}

Scopri Cloud Manager e come unisce il nuovo processo di creazione rapida dei siti.

>[!CAUTION]
>
>Lo strumento di creazione rapida del sito è attualmente un&#39;anteprima tecnica. Esso è messo a disposizione a fini di prova e valutazione e non è destinato all&#39;uso della produzione se non concordato con il sostegno Adobe.

>[!TIP]
>
>Se il tuo ruolo è esclusivamente sviluppo front-end, puoi passare all’articolo [Recuperare le informazioni di accesso all’archivio Git](retrieve-access.md) in questo percorso.
>
>Se sei un amministratore AEM, un amministratore di Cloud Manager, sei responsabile sia delle attività di sviluppo front-end che di quelle di amministrazione, oppure desideri semplicemente comprendere il processo end-to-end in AEM per lo sviluppo front-end, continua a leggere il documento corrente e continua su questo percorso.

## Obiettivo {#objective}

Questo documento consente di comprendere il funzionamento dello strumento AEM Creazione rapida siti e offre una panoramica del flusso end-to-end. Dopo la lettura è necessario:

* Scopri in che modo AEM Sites e Cloud Manager collaborano per facilitare lo sviluppo front-end
* Scopri come il passaggio di personalizzazione front-end è completamente scollegato dalla AEM e non richiede alcuna conoscenza AEM.

Questo documento si concentra sulla comprensione di questi elementi fondamentali della soluzione di creazione di siti rapidi prima di passare al passaggio successivo del percorso in cui si inizia la configurazione.

Anche se è consigliabile procedere in questo percorso passo dopo passo, se hai già capito che AEM Sites e Cloud Manager lavorano insieme e desiderano iniziare direttamente con la configurazione, puoi [passa al passaggio successivo del percorso.](create-site.md)

## Ruolo responsabile {#responsible-role}

Questa parte del percorso si applica sia all’amministratore di AEM che all’amministratore di Cloud Manager.

## Requisiti e prerequisiti {#requirements-prerequisites}

Sono necessari diversi requisiti prima di iniziare a creare e personalizzare siti utilizzando lo strumento Creazione rapida siti .

Poiché questo percorso è destinato sia agli sviluppatori front-end che agli amministratori e alle combinazioni di tutti i ruoli, i requisiti per entrambi sono elencati qui.

È importante comprendere che per lo sviluppatore front-end non è necessario alcun accesso o conoscenza AEM.

### Conoscenza {#knowledge}

| Conoscenza | Ruolo |
|---|---|
| Comprensione degli strumenti e dei processi standard di sviluppo front-end | Sviluppatore front-end |
| Conoscenza di base su come creare e gestire i siti in AEM | Amministratore AEM |
| Conoscenza di base di Cloud Manager | Amministratore di Cloud Manager |

Per lo sviluppatore front-end, non è necessaria alcuna conoscenza AEM.

### Strumenti {#tools}

| Strumento | Ruolo |
|---|---|
| Ambiente di sviluppo front-end preferito | Sviluppatore front-end |
| npm | Sviluppatore front-end |
| webpack | Sviluppatore front-end |
| Accesso a Cloud Manager | Amministratore di Cloud Manager |
| Essere membro di **Proprietario business** ruolo in Cloud Manager | Amministratore di Cloud Manager |
| Diventa amministratore di sistema in Cloud Manager | Amministratore di Cloud Manager |
| Accesso all&#39;Admin Console | Amministratore di Cloud Manager |
| Essere membro del **Gestione distribuzione** ruolo in Cloud Manager | Amministratore di Cloud Manager |
| Essere membro del **Gestione distribuzione** ruolo in Cloud Manager | Sviluppatore front-end |

Per lo sviluppatore front-end, non è necessario utilizzare AEM.

>[!TIP]
>
>Se non conosci i ruoli e la gestione dei ruoli di Cloud Manager, consulta il documento sulle autorizzazioni basate sul ruolo nella sezione [Risorse aggiuntive](#additional-resources) sezione .

## Cloud Manager {#cloud-manager}

Cloud Manager è un componente essenziale di AEM as a Cloud Service e funge da punto di ingresso singolo per la piattaforma.

Per supportare i clienti con configurazioni di sviluppo aziendali, AEM as a Cloud Service si integra completamente con Cloud Manager e le sue pipeline CI/CD appositamente progettate. Lo strumento di creazione rapida del sito estende queste funzioni per supportare pipeline di sviluppo front-end dedicate.

Ai fini del presente percorso, non è necessaria una comprensione completa di Cloud Manager. Ad alto livello, Cloud Manager è costituito da diversi livelli di struttura.

![Struttura di Cloud Manager](assets/cloud-manager-structure.png)

* **TENDA** - Per ogni cliente viene eseguito il provisioning con un tenant. **WKND Travel and Adventure Enterprises** potrebbe essere un tenant.
* **PROGRAMMI** - Ogni tenant dispone di uno o più programmi. La **WKND Travel and Adventure Enterprises** tenant potrebbe avere un **Vita notturna WKND** e **Progetti pomeridiani WKND** programma.
* **AMBIENTI** - Ogni programma dispone di più ambienti, ad esempio la produzione di contenuti live, la gestione temporanea e lo sviluppo a scopo di sviluppo. **Vita notturna WKND** e **Progetti pomeridiani WKND** i programmi avrebbero ambienti di sviluppo, stage e produzione.
* **ARCHIVIO** - Gli ambienti dispongono di archivi git in cui viene mantenuto l’applicazione e il codice front-end.
* **STRUMENTI E FLUSSI DI LAVORO** - Le pipeline gestiscono la distribuzione del codice dagli archivi agli ambienti.

## Flusso di sviluppo front-end per la creazione rapida di siti {#flow}

Il flusso complessivo è semplice e intuitivo anche se non disponi ancora di un’esperienza completa con Cloud Manager.

1. L’amministratore AEM effettua l’accesso a un ambiente AEM e crea un nuovo sito utilizzando un modello di sito.
1. L’amministratore di Cloud Manager crea una pipeline front-end in Cloud Manager. La pipeline orchestra la distribuzione del codice da un archivio Git a un ambiente AEM.
1. L’amministratore AEM esporta il tema del sito dall’istanza AEM del programma e lo fornisce allo sviluppatore front-end.
1. L’amministratore di Cloud Manager concede agli sviluppatori front-end l’accesso all’archivio Git AEM dove è possibile eseguire il commit delle personalizzazioni.
1. Lo sviluppatore front-end recupera le credenziali di accesso per accedere a Git e alla pipeline.
1. Lo sviluppatore front-end personalizza il tema, lo sottopone a test utilizzando il contenuto effettivo dal sito utilizzando un proxy e quindi invia le modifiche all’archivio git.
1. Lo sviluppatore front-end esegue la pipeline per distribuire le personalizzazioni dei temi nell’ambiente di produzione del programma.

![Flusso di creazione rapida del sito](assets/qsc-flow.png)

Il vantaggio principale dell&#39;utilizzo dello strumento Creazione rapida siti è che lo sviluppatore front-end puro è responsabile solo della personalizzazione effettiva. Lo sviluppatore front-end non ha alcuna interazione con AEM o ha bisogno di alcuna conoscenza di AEM.

## Novità {#what-is-next}

Dopo aver completato questa parte del percorso di creazione siti rapidi AEM, è necessario:

* Scopri in che modo AEM Sites e Cloud Manager collaborano per facilitare lo sviluppo front-end
* Scopri come il passaggio di personalizzazione front-end è completamente scollegato dalla AEM e non richiede alcuna conoscenza AEM.

Sviluppare questa conoscenza e continuare il percorso di creazione siti rapida AEM revisione successiva del documento [Crea sito da modello,](create-site.md) dove verrà illustrato come creare rapidamente un nuovo sito AEM utilizzando un modello.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso Creazione rapida siti esaminando il documento [Crea sito da modello,](create-site.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso.

* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
* [Autorizzazioni basate sul ruolo](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - Cloud Manager dispone di ruoli preconfigurati con le autorizzazioni appropriate. Per informazioni dettagliate su questi ruoli e su come amministrarli, consulta questo documento.
* [npm](https://www.npmjs.com) - AEM temi utilizzati per costruire rapidamente i siti sono basati su npm.
* [webpack](https://webpack.js.org) - AEM temi utilizzati per costruire rapidamente i siti si basano su webpack.
