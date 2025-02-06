---
title: Sviluppo di Sites con la pipeline front-end
description: Con la pipeline front-end, viene data maggiore indipendenza agli sviluppatori front-end e il processo di sviluppo può guadagnare una notevole velocità. Questo documento descrive alcune considerazioni particolari del processo di sviluppo front-end che devono essere fornite.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 1%

---


# Sviluppo di Sites con la pipeline front-end {#developing-site-with-front-end-pipeline}

[Con la pipeline front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end), viene data maggiore indipendenza agli sviluppatori front-end e il processo di sviluppo può guadagnare una notevole velocità. Questo documento descrive il funzionamento di questo processo e contiene alcune considerazioni di cui tenere conto per sfruttare appieno il potenziale.

>[!TIP]
>
>Se non sai ancora come utilizzare la pipeline front-end e i vantaggi che può offrire, consulta il [Percorso per la creazione rapida di siti](/help/journey-sites/quick-site/overview.md) per vedere come distribuire rapidamente un nuovo sito e personalizzarne il tema in modo completamente indipendente dallo sviluppo back-end.

## Contratto di sviluppo front-end {#front-end-build-contract}

Analogamente all&#39;[ambiente di build full stack](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md), la pipeline front-end dispone di un proprio ambiente. Gli sviluppatori possono utilizzare questa pipeline con una certa flessibilità, purché venga rispettato il seguente contratto di sviluppo front-end.

La pipeline front-end richiede che il progetto Node.js front-end utilizzi la direttiva script `build` per generare la build distribuita. Questo perché Cloud Manager utilizza il comando `npm run build` per generare il progetto distribuibile per la build front-end.

Il contenuto risultante della cartella `dist` è ciò che viene distribuito da Cloud Manager, che funge da file statici. Questi file sono ospitati esternamente all&#39;AEM, ma sono resi disponibili tramite un URL `/content/...` nell&#39;ambiente distribuito.

## Versioni dei nodi {#node-versions}

L’ambiente di sviluppo front-end supporta le seguenti versioni di Node.js.

* 12
* 14 (predefinito)
* 16
* 18

È possibile utilizzare la `NODE_VERSION` [variabile di ambiente](/help/implementing/cloud-manager/environment-variables.md) per impostare la versione desiderata.

## Source unico della verità {#single-source-of-truth}

Una buona pratica generale è quella di mantenere un&#39;unica fonte di verità per ciò che viene implementato nell&#39;AEM. L&#39;obiettivo di Cloud Manager è quello di rendere ovvia quell&#39;unica fonte di verità. Tuttavia, poiché la pipeline front-end consente di disaccoppiare la posizione di parti del codice, una parte di responsabilità aggiuntiva risiede nella corretta configurazione delle pipeline front-end. Fai molta attenzione a non creare più pipeline front-end da distribuire sullo stesso sito nello stesso ambiente.

Per questo motivo, e in particolare quando vengono create diverse pipeline front-end, si consiglia di mantenere una convenzione di denominazione sistematica come la seguente:

* Il nome del modulo front-end, definito dalla proprietà `name` del file `package.json`, deve contenere il nome del sito a cui si applica. Ad esempio, per un sito situato in `/content/wknd`, il nome del modulo front-end sarà simile a `wknd-theme`.
* Quando un modulo front-end condivide lo stesso archivio Git con altri moduli, il nome della relativa cartella deve essere uguale o contenere lo stesso nome del modulo front-end. Ad esempio, se il modulo front-end è denominato `wknd-theme`, il nome della cartella di inclusione sarà simile a `wknd-theme-sources`.
* Il nome della pipeline front-end di Cloud Manager deve contenere anche il nome del modulo front-end e aggiungere l’ambiente in cui viene distribuito (produzione o sviluppo). Ad esempio, per il modulo front-end denominato `wknd-theme`, la pipeline potrebbe essere denominata ad esempio `wknd-theme-prod`.

Tale convenzione dovrebbe prevenire efficacemente i seguenti errori di distribuzione:

* Applicazione di un modulo front-end al sito errato
* Creazione di più moduli front-end che applicano lo stesso sito, che si sovrascriverebbero a vicenda
* Creazione di più pipeline front-end per le stesse origini, che potrebbero causare race condition e non garantire l’ordine di distribuzione

## Separazione tra logica e markup {#separation-of-concerns}

Un&#39;altra buona pratica che si applica a qualsiasi separazione delle preoccupazioni è di porre particolare attenzione nel modo in cui il contratto che separa le preoccupazioni è progettato e gestito. Nel caso della pipeline front-end, il contratto che separa tale codice dal resto è il HTML e il JSON riprodotto dal sito. Se il HTML e il JSON rimangono stabili, la pipeline front-end fornisce il suo valore massimo rendendo il team front-end completamente indipendente.

Attualmente non esiste una funzionalità specifica per eseguire la pipeline full stack in modo sincrono con le pipeline front-end. Per questo motivo, quando si separa lo sviluppo front-end dalla pipeline full-stack, è necessario prestare maggiore attenzione nel contratto che separa queste due aree di preoccupazione. Tale contratto è generalmente il HTML e/o il JSON che l’Experience Manager esegue. Le modifiche a tale contratto devono quindi essere ben pianificate tra i team che gestiscono le diverse pipeline in modo che concordino su come sequenziare le modifiche corrispondenti.

I passaggi seguenti sono generalmente consigliati quando è necessario apportare modifiche all’output HTML e/o JSON che influiscono su entrambe le aree problematiche.

1. Il team back-end configura innanzitutto un ambiente di sviluppo con il nuovo output HTML e/o JSON.
   1. Tramite la pipeline full stack, distribuiscono il codice necessario per eseguire il rendering del nuovo output HTML e/o JSON desiderato.
   1. Se si tratta di un ambiente a cui il team front-end non aveva precedentemente accesso, è necessario eseguire i passaggi seguenti.
      1. URL: il team front-end deve conoscere l’URL di tale ambiente di sviluppo.
      1. ACL: il team front-end deve disporre di un utente AEM locale con autorizzazioni simili a &quot;Collaboratori&quot;.
      1. Git: il team front-end deve disporre di una posizione Git separata per il modulo front-end che esegue il targeting specifico dell’ambiente di sviluppo.
         * Di solito si crea un ramo `dev`, in modo che le modifiche apportate per l&#39;ambiente di sviluppo possano essere facilmente unite nuovamente al ramo `main` da distribuire nell&#39;ambiente di produzione.
      1. Pipeline: il team front-end deve disporre di una pipeline front-end da distribuire nell’ambiente di sviluppo. La pipeline distribuisce il modulo front-end che si trova in genere nel ramo `dev`, come descritto nel punto precedente.
1. Il team front-end fa quindi in modo che il codice CSS e JS funzioni sia con il vecchio che con il nuovo output.
   1. Come di consueto, per sviluppare localmente:
      1. Il comando `npx aem-site-theme-builder proxy` eseguito nel modulo front-end avvia un server proxy che richiede il contenuto da un ambiente AEM, sostituendo i file CSS e JS del modulo front-end con quelli della cartella locale `dist`.
      1. La configurazione della variabile `AEM_URL` nel file nascosto `.env` consente di controllare da quale ambiente AEM il server proxy locale utilizza il contenuto.
      1. La modifica del valore di `AEM_URL` consente quindi di passare dagli ambienti di produzione a quelli di sviluppo per adeguare CSS e JS in modo che siano adatti a entrambi gli ambienti.
      1. Deve funzionare con l’ambiente di sviluppo che esegue il rendering del nuovo output e con l’ambiente di produzione che esegue il rendering del vecchio output.
   1. Il lavoro front-end viene completato quando il modulo front-end aggiornato funziona per entrambi gli ambienti e viene distribuito in entrambi.
1. Il team back-end può quindi aggiornare l’ambiente di produzione distribuendo il codice che esegue il rendering del nuovo output HTML e/o JSON tramite la pipeline full stack.
1. Il team front-end può quindi ripulire i file CSS e JS e rimuovere ciò che era necessario solo per l’output precedente, distribuendo l’ultimo aggiornamento alla produzione tramite la pipeline front-end.

## Risorse aggiuntive {#additional-resources}

* [Temi del sito](/help/sites-cloud/administering/site-creation/site-themes.md) - Scopri come utilizzare i temi del sito AEM per personalizzare lo stile e la progettazione del sito.
* [Generatore di temi del sito AEM](https://github.com/adobe/aem-site-theme-builder) - Adobe fornisce un generatore di temi del sito AEM come set di script per la creazione di nuovi temi del sito.
