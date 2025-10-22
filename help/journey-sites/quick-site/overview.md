---
title: Percorso di creazione di siti rapidi AEM
description: Inizia qui per un percorso guidato attraverso lo strumento Creazione rapida sito di AEM facile da usare che permette di semplificare lo sviluppo front-end del sito AEM e personalizzare rapidamente il sito senza alcuna conoscenza del back-end di AEM.
exl-id: b8218232-0298-4b16-9dab-fa59be592a24
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: noDisplay, noCatalog
source-git-commit: 8c4b34a77ef85869048fae254728c58cf0d99b66
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 100%

---


# Percorso di creazione di siti rapidi AEM {#quick-site-creation-journey}

{{traditional-aem}}

Inizia qui per un percorso guidato attraverso lo strumento Creazione rapida sito di AEM facile da usare che permette di semplificare lo sviluppo front-end del sito AEM e personalizzare rapidamente il sito senza alcuna conoscenza del back-end di AEM.

## Introduzione {#introduction}

AEM Sites è un potente set di strumenti per la creazione e la gestione di esperienze digitali. Gli autori dei contenuti possono creare facilmente esperienze digitali tramite l’editor dei siti e organizzare i contenuti mediante la console Sites, visualizzando allo stesso tempo i contenuti live così come saranno distribuiti da AEM ai vari tipi di pubblico su tutti i canali.

Lo strumento Creazione rapida siti AEM consente agli sviluppatori di creare rapidamente un sito da zero utilizzando dei modelli. Una volta creato, lo strumento Creazione rapida sito consente inoltre di personalizzare velocemente il tema e lo stile del sito AEM (risorse JavaScript, CSS e statiche). In questo modo lo sviluppatore front-end, che non ha bisogno di conoscere AEM, può lavorare in maniera autonoma e in parallelo ai creatori di contenuti. L’amministratore AEM scarica semplicemente il tema del sito e lo fornisce allo sviluppatore front-end. Quest&#39;ultimo lo personalizza utilizzando i propri strumenti preferiti e successivamente conferma le modifiche nell’archivio del codice AEM, che viene quindi distribuito.

Eliminando le conoscenze per gli sviluppatori per la creazione di siti, eliminando i requisiti di conoscenza AEM per lo sviluppo front-end e consentendo lo sviluppo di temi in parallelo con la creazione di contenuti, lo strumento di Creazione rapida siti AEM accelera notevolmente il time-to-value del sito e aumenta l’agilità di personalizzazione e distribuzione del sito.

## Panoramica video {#video-overview}

Per una rapida panoramica pratica di questa funzione, [è disponibile un’introduzione della durata di cinque minuti.](https://www.youtube.com/watch?v=NQeQ1jZ7ZBw)

Questo percorso di documentazione illustra in un video tutte le funzioni dettagliate per passaggi, consentendoti di comprendere il flusso di lavoro e creare nuovamente il processo nel tuo ambiente.

## Percorsi di documentazione AEM {#documentation-journeys}

[Un percorso di documentazione](/help/journey-documentation/documentation-journeys.md) unisce molti argomenti e caratteristiche diversi e complicati, fornendo un resoconto che aiuta il lettore, che potrebbe essere un nuovo utente di AEM, a capire e risolvere un problema di business dall’inizio alla fine, supponendo una conoscenza minima pregressa dell’argomento o di AEM.

I percorsi di documentazione sono progettati in base ai principi delle best practice, alla luce delle ultime ricerche condotte da Adobe, della comprovata esperienza nell’implementazione da parte di consulenti di Adobe e del feedback raccolto sui progetti della clientela.

Se desideri sapere come Adobe consiglia di risolvere i casi aziendali relativi ai siti con AEM, per iniziare puoi utilizzare i Percorsi AEM Sites.

## Pubblico {#audience}

Questo percorso descrive i requisiti, i passaggi e l’approccio per personalizzare i temi AEM Sites. Il pubblico principale è lo sviluppatore front-end, che non ha bisogno di alcuna conoscenza di AEM. Tuttavia, per illustrare l’intero processo, il percorso coinvolge gli amministratori, che si presume abbiano conoscenze di base di AEM Sites e Cloud Manager. In pratica, più persone possono gestire più ruoli e questo percorso supporta i punti di vista degli amministratori e degli sviluppatori front-end.

| Persona | Descrizione | Ruolo nel percorso |
|---|---|---|
| Sviluppatore front-end | Personalizza il tema del sito | Prende il tema fornito dall’amministratore AEM e lo personalizza in modo che possa essere distribuito sul sito AEM. |
| Autore del contenuto | Crea e gestisce i contenuti distribuiti come siti | Gli autori di contenuti creano su AEM contenuti di cui viene eseguito il rendering con il tema personalizzato dallo sviluppatore front-end. |
| Amministratore AEM | Crea un nuovo sito AEM | L’amministratore AEM crea un nuovo sito basato su un modello e quindi fornisce allo sviluppatore front-end un tema da personalizzare. |
| Amministratore di Cloud Manager | Crea pipeline e concede l’accesso | L’amministratore di Cloud Manager crea la pipeline front-end e concede l’accesso allo sviluppatore front-end per poter eseguire il commit delle personalizzazioni nell’archivio Git AEM. |

## Percorso di Creazione di siti rapidi AEM {#the-journey}

In questo percorso esplorerai molti argomenti. I seguenti articoli forniscono informazioni fondamentali su come creare e personalizzare siti AEM Sites mediante lo strumento Creazione rapida di siti e collegamenti alla documentazione tecnica dettagliata.

| # | Articolo | Descrizione | Ruolo responsabile |
|---|---|---|--|
| 0 | Percorso di creazione di siti rapidi AEM | Questo documento | Amministratori di AEM e Cloud Manager |
| 1 | [Informazioni su Cloud Manager e il flusso di lavoro per la creazione di siti rapidi](cloud-manager.md) | Scopri Cloud Manager e il modo in cui unisce il nuovo processo di creazione di siti rapidi. | Amministratore AEM |
| 2 | [Crea sito da modello](create-site.md) | Scopri come creare rapidamente un sito AEM utilizzando un modello di sito. | Amministratore AEM |
| 3 | [Configurare la pipeline](pipeline-setup.md) | Crea una pipeline front-end per gestire la personalizzazione del tema del sito. | Amministratore di Cloud Manager |
| 4 | [Concedere l’accesso allo sviluppatore front-end](grant-access.md) | Integra gli sviluppatori front-end in Cloud Manager in modo che abbiano accesso all’archivio Git del sito AEM e alla pipeline. | Amministratore di Cloud Manager |
| 5 | [Recuperare le informazioni di accesso all’archivio Git](retrieve-access.md) | Scopri in che modo lo sviluppatore front-end utilizza Cloud Manager per accedere alle informazioni dell’archivio Git. | Sviluppatore front-end |
| 6 | [Personalizzare il tema del sito](customize-theme.md) | Scopri come è fatto un tema del sito, come personalizzarlo e come testarlo utilizzando contenuti live AEM. | Sviluppatore front-end |
| 7 | [Distribuire il tema personalizzato](deploy-theme.md) | Scopri come distribuire il tema del sito utilizzando la pipeline. | Sviluppatore front-end |

## Passaggio successivo {#what-is-next}

Ora puoi iniziare il percorso di Creazione rapida di siti di Adobe.

* Se sei un amministratore di AEM o di Cloud Manager, o se svolgi entrambi i ruoli di sviluppatore front-end e amministratore, oppure se desideri semplicemente comprendere il processo end-to-end in AEM, parti all’inizio del percorso con [Scopri Cloud Manager](cloud-manager.md) come illustrato di seguito.
* Se sei solo responsabile dello sviluppo front-end e interagirai con gli amministratori di AEM e Cloud Manager, puoi passare direttamente a [Recuperare le informazioni di accesso all’archivio Git](retrieve-access.md) per accedere all’archivio Git AEM e iniziare a personalizzarlo.
* Se hai già compreso come AEM Sites e Cloud Manager lavorano insieme e desideri iniziare direttamente con la configurazione, puoi [passare direttamente alla creazione di un sito da un modello](create-site.md).

## Risorse aggiuntive {#additional-resources}

Consulta queste risorse aggiuntive per ulteriori informazioni su come si integrano tra loro le potenti funzionalità di AEM.

* [Documentazione tecnica di AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=it): se hai già una conoscenza approfondita di AEM, potresti voler consultare direttamente i documenti tecnici approfonditi.
* [Documentazione sull’amministrazione del sito](/help/sites-cloud/administering/site-creation/create-site.md): per ulteriori informazioni sulle funzioni dello strumento Creazione rapida di siti, consulta i relativi documenti tecnici.
