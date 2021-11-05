---
title: AEM Percorso di creazione di siti rapidi
description: Iniziate qui per un percorso guidato attraverso il facile da usare AEM strumento di creazione di siti rapidi per semplificare lo sviluppo front-end del sito AEM e personalizzare rapidamente il sito senza AEM conoscenza back-end.
source-git-commit: efeb97d4bd7e7c11ec2c0ba1244a32b8b9affdab
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 1%

---


# AEM Percorso di creazione di siti rapidi {#quick-site-creation-journey}

Iniziate qui per un percorso guidato attraverso il facile da usare AEM strumento di creazione di siti rapidi per semplificare lo sviluppo front-end del sito AEM e personalizzare rapidamente il sito senza AEM conoscenza back-end.

>[!CAUTION]
>
>Lo strumento di creazione rapida del sito è attualmente un&#39;anteprima tecnica. Esso è messo a disposizione a fini di prova e valutazione e non è destinato all&#39;uso della produzione se non concordato con il sostegno Adobe.

## Introduzione {#introduction}

AEM Sites è un potente set di strumenti per la creazione e la gestione di esperienze digitali. Gli autori dei contenuti possono creare esperienze digitali facilmente tramite l’editor dei siti e organizzare i contenuti mediante la console Sites , visualizzando al contempo i contenuti live così come verranno consegnati dalle AEM ai tipi di pubblico attraverso i canali.

Lo strumento AEM Creazione rapida siti consente agli sviluppatori di creare rapidamente un nuovo sito da zero utilizzando i modelli di sito. Una volta creato, lo strumento di creazione rapida del sito consente inoltre di personalizzare rapidamente il tema e lo stile del sito AEM (risorse JavaScript, CSS e statiche). In questo modo lo sviluppatore front-end, che necessita di una conoscenza di AEM pari a zero, può lavorare separatamente rispetto ai creatori di contenuti e in parallelo ad essi. L’amministratore AEM semplicemente scarica il tema del sito e lo fornisce allo sviluppatore front-end che lo personalizzerà utilizzando i propri strumenti preferiti e quindi commette le modifiche all’archivio del codice AEM, che viene quindi distribuito.

Eliminando le conoscenze per gli sviluppatori per la creazione di siti, eliminando AEM requisiti di conoscenza per lo sviluppo front-end e consentendo lo sviluppo di temi in parallelo con la creazione di contenuti, lo strumento di creazione rapida dei siti AEM accelera notevolmente il time-to-value del sito e aumenta l&#39;agilità di personalizzazione e distribuzione del sito.

## percorsi di documentazione AEM {#documentation-journeys}

[Un Percorso di documentazione](/help/journey-documentation/home.md) unisce molti argomenti e caratteristiche diversi e forse complicati fornendo una narrazione che aiuta il lettore, che può essere nuovo a AEM, capire e risolvere un problema di business dall&#39;inizio alla fine, assumendo al contempo un argomento preliminare minimo o AEM conoscenza.

I Percorsi di documentazione sono progettati in base ai principi delle best practice, alla luce delle ultime ricerche condotte da Adobe, della comprovata esperienza nell’implementazione da parte di consulenti di Adobe e del feedback dai progetti dei clienti.

Se desideri sapere come Adobe consiglia di risolvere i casi aziendali relativi ai siti con AEM, dove iniziare è possibile utilizzare gli Percorsi AEM Sites.

## Pubblico {#audience}

Questo percorso descrive i requisiti, i passaggi e l’approccio per personalizzare i temi AEM Sites. Il suo pubblico principale è lo sviluppatore front-end, che non ha bisogno di alcuna conoscenza di AEM. Tuttavia, per illustrare l’intero processo, il percorso coinvolge gli amministratori, che si presume abbiano conoscenze di base su AEM Sites e Cloud Manager. In pratica, più persone possono gestire più ruoli e questo percorso supporta le prospettive degli amministratori e degli sviluppatori front-end.

| Persona | Descrizione | Ruolo nel Percorso |
|---|---|---|
| Sviluppatore front-end | Personalizza il tema del sito | Tema fornito dall’amministratore AEM e lo personalizza in modo che possa essere distribuito sul sito AEM. |
| Autore del contenuto | Crea e gestisce i contenuti consegnati come siti | Gli autori di contenuti creano contenuti su AEM di cui viene eseguito il rendering con il tema personalizzato dallo sviluppatore front-end. |
| Amministratore AEM | Crea un nuovo sito AEM | L’amministratore AEM crea un nuovo sito basato su un modello e quindi fornisce allo sviluppatore front-end un tema da personalizzare. |
| Amministratore di Cloud Manager | Crea pipeline e concede l’accesso | L’amministratore di Cloud Manager crea la pipeline front-end e concede l’accesso allo sviluppatore front-end per poter eseguire il commit delle personalizzazioni nell’archivio Git AEM. |

## Il Percorso di creazione rapida AEM sito {#the-journey}

Esplorerai molti argomenti in questo percorso. I seguenti articoli forniscono informazioni fondamentali sulla creazione e la personalizzazione di siti AEM mediante lo strumento Creazione rapida di siti e collegano a una documentazione tecnica dettagliata.

|#|Articolo|Descrizione|Ruolo responsabile| |—|—|—|—| |0|AEM Percorso di creazione di siti rapidi|Questo documento|Amministratori di AEM e Cloud Manager| |1[Comprendere Cloud Manager e il flusso di lavoro per la creazione di siti rapidi](cloud-manager.md)|Scopri Cloud Manager e come unisce il nuovo processo di creazione rapida dei siti.|Amministratore AEM| |2[Crea sito da modello](create-site.md)|Scopri come creare rapidamente un nuovo sito AEM utilizzando un modello di sito.|Amministratore AEM| |3[Configurare la pipeline](pipeline-setup.md)|Crea una pipeline front-end per gestire la personalizzazione del tema del sito.Amministratore di Cloud Manager| |4[Concedere l’accesso allo sviluppatore front-end](grant-access.md)|Onboarding degli sviluppatori front-end in Cloud Manager in modo che possano accedere all’archivio Git del sito AEM e alla pipeline.Amministratore di Cloud Manager| |5[Recuperare le informazioni di accesso all’archivio Git](retrieve-access.md)|Scopri in che modo lo sviluppatore front-end utilizza Cloud Manager per accedere alle informazioni dell’archivio Git.|Sviluppatore front-end| |6[Personalizzare il tema del sito](customize-theme.md)|Scopri come viene creato un tema del sito, come personalizzarlo e come testarlo utilizzando AEM contenuto live.|Sviluppatore front-end| |7[Distribuisci il tema personalizzato](deploy-theme.md)|Scopri come distribuire il tema del sito utilizzando la pipeline.|Sviluppatore front-end|

## Novità {#what-is-next}

È ora possibile iniziare il percorso di creazione rapida dei siti di Adobe.

* Se sei un amministratore di AEM o di Cloud Manager, o se utilizzi entrambi i ruoli di sviluppatore front-end e amministratore, o se desideri semplicemente comprendere il processo end-to-end in AEM, inizia all’inizio del percorso con [Comprendere Cloud Manager](cloud-manager.md) come illustrato di seguito.
* Se sei solo responsabile dello sviluppo front-end e interagirai con gli amministratori di AEM e Cloud Manager, puoi passare direttamente a [Recuperare le informazioni di accesso all’archivio Git](retrieve-access.md) per accedere all’archivio Git AEM e iniziare a personalizzarlo.
* Se sai già che AEM Sites e Cloud Manager lavorano insieme e desiderano iniziare direttamente con la configurazione, puoi [passa direttamente alla creazione di un nuovo sito da un modello.](create-site.md)

## Risorse aggiuntive {#additional-resources}

Consulta queste risorse aggiuntive per ulteriori informazioni su come AEM funzioni potenti funzionano insieme.

* [AEM documentazione tecnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=it) - Se hai già una conoscenza approfondita di AEM, potresti voler consultare direttamente i documenti tecnici approfonditi.
* [Documentazione sull’amministrazione del sito](/help/sites-cloud/administering/site-creation/create-site.md) - Per ulteriori informazioni sulle funzioni dello strumento Creazione rapida di siti, consultare i documenti tecnici sulla creazione del sito.
