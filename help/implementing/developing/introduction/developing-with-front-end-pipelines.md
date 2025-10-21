---
title: Sviluppare siti con la pipeline front-end
description: La pipeline front-end migliora l’indipendenza degli sviluppatori e accelera il processo di sviluppo. Questo articolo illustra le considerazioni chiave per il processo di sviluppo front-end per garantire prestazioni ed efficienza ottimali.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
recommendations: display, noCatalog
source-git-commit: 0a458616afad836efae27e67dbe145fc44bee968
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 3%

---


# Sviluppare Sites con la pipeline front-end {#developing-site-with-front-end-pipeline}

{{traditional-aem}}

La [pipeline front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) offre agli sviluppatori front-end maggiore indipendenza e accelera notevolmente lo sviluppo. Questo articolo spiega come funziona il processo ed evidenzia le considerazioni chiave per trarre il massimo da esso.

>[!TIP]
>
>Se non sai ancora come utilizzare la pipeline front-end e i relativi vantaggi, consulta la [guida del Percorso Creazione rapida siti](/help/journey-sites/quick-site/overview.md). Fornisce un esempio di come distribuire rapidamente un nuovo sito e personalizzarne il tema indipendentemente dallo sviluppo back-end.

## Comprendere la configurazione e il processo di generazione della pipeline front-end in AEM Cloud Manager {#front-end-build-contract}

Analogamente all&#39;[ambiente di build full stack](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md), la pipeline front-end dispone di un proprio ambiente. Gli sviluppatori hanno una certa flessibilità con questa pipeline, purché seguano il contratto di sviluppo front-end.

La pipeline front-end richiede che il progetto front-end `Node.js` utilizzi la direttiva script `build` per generare la build distribuita. Questo requisito esiste perché Cloud Manager utilizza il comando `npm run build` per generare il progetto distribuibile per la build front-end.

Il contenuto risultante della cartella `dist` è ciò che Cloud Manager distribuisce, fungendo da file statici. Questi file sono ospitati esternamente in AEM, ma sono resi disponibili tramite un URL `/content/...` nell&#39;ambiente distribuito.

## Versioni supportate di Node.js {#node-versions}

L&#39;ambiente di sviluppo front-end supporta le seguenti `Node.js` versioni:

* 23
* 22
* 20
* 18
* 16
* 14 (predefinito)
* 12

È possibile utilizzare la `NODE_VERSION` [variabile di ambiente](/help/implementing/cloud-manager/environment-variables.md) per impostare la versione desiderata.

## Best practice per la denominazione e la gestione delle pipeline front-end in AEM {#single-source-of-truth}

Una best practice per le distribuzioni di AEM consiste nel mantenere un’unica, chiara fonte di verità. Cloud Manager è stata progettata per rafforzare questo principio. Tuttavia, poiché la pipeline front-end consente di disaccoppiare parti del codice, è essenziale una configurazione corretta. Per evitare conflitti, assicurati che più pipeline front-end non vengano distribuite allo stesso sito all’interno dello stesso ambiente.

Per questo motivo, e in particolare quando vengono create diverse pipeline front-end, Adobe consiglia di mantenere una convenzione di denominazione sistematica. Puoi utilizzare i seguenti consigli:

* Il nome del modulo front-end, definito dalla proprietà `name` del file `package.json`, deve contenere il nome del sito a cui si applica. Ad esempio, per un sito situato in `/content/wknd`, il nome del modulo front-end sarà simile a `wknd-theme`.
* Quando un modulo front-end condivide lo stesso archivio Git con altri moduli, il nome della relativa cartella deve essere uguale o contenere lo stesso nome del modulo front-end. Ad esempio, se il modulo front-end è denominato `wknd-theme`, il nome della cartella di inclusione sarà simile a `wknd-theme-sources`.
* Il nome della pipeline front-end di Cloud Manager deve contenere anche il nome del modulo front-end e aggiungere l’ambiente in cui viene distribuito (produzione o sviluppo). Ad esempio, per il modulo front-end denominato `wknd-theme`, la pipeline potrebbe essere denominata ad esempio `wknd-theme-prod`.

Tale convenzione consente di evitare i seguenti errori di distribuzione:

* Applicazione di un modulo front-end al sito errato.
* Creazione di più moduli front-end che applicano lo stesso sito e si sovrascriverebbero a vicenda.
* Creazione di più pipeline front-end per le stesse origini, che potrebbero causare race condition e non garantire l’ordine di distribuzione.

## Coordinare lo sviluppo front-end e back-end per la stabilità in AEM {#separation-of-concerns}

Una best practice chiave per ogni separazione delle preoccupazioni è quella di progettare e gestire il contratto con attenzione che definisca i confini tra di loro. Nella pipeline front-end, questo contratto è l’output HTML e JSON renderizzato dal sito. Mantenendo la stabilità dell’output, la pipeline front-end fornisce il massimo valore, consentendo al team front-end di lavorare in modo indipendente.

Al momento non è disponibile alcuna funzionalità incorporata per eseguire la pipeline full stack in modo sincrono con le pipeline front-end. Pertanto, quando si separa lo sviluppo front-end dalla pipeline full stack, è fondamentale gestire con attenzione il contratto che ne definisce i limiti. Questo contratto è in genere costituito dal rendering di HTML o JSON, o entrambi, eseguito da Experience Manager. Qualsiasi modifica a questo contratto deve essere attentamente coordinata tra i team che gestiscono diverse pipeline, in modo da garantire una transizione senza intoppi e la corretta sequenza degli aggiornamenti.

I passaggi seguenti sono generalmente consigliati quando si apportano modifiche all’output HTML o JSON, in particolare quando sono interessate entrambe le aree.

1. Il team back-end configura innanzitutto un ambiente di sviluppo con il nuovo output HTML o JSON.
   1. Tramite la pipeline full stack, distribuiscono il codice necessario per eseguire il rendering del nuovo output HTML o JSON, o di entrambi, a seconda delle esigenze.
   1. Se si tratta di un ambiente a cui il team front-end non aveva precedentemente accesso, è necessario eseguire i passaggi seguenti.
      1. URL: il team front-end deve conoscere l’URL di tale ambiente di sviluppo.
      1. ACL: al team front-end deve essere assegnato un utente AEM locale con autorizzazioni simili a &quot;Collaboratori&quot;.
      1. Git: il team front-end deve disporre di una posizione Git separata per il modulo front-end che esegue il targeting specifico dell’ambiente di sviluppo.

         Una pratica comune consiste nel creare un ramo `dev` per gestire le modifiche apportate nell&#39;ambiente di sviluppo. Questa procedura consente un merge più semplice nel ramo `main`, utilizzato per la distribuzione nell&#39;ambiente di produzione.

      1. Pipeline: il team front-end deve disporre di una pipeline front-end da distribuire nell’ambiente di sviluppo. La pipeline distribuisce il modulo front-end che si trova in genere nel ramo `dev`, come descritto nel punto precedente.
1. Il team front-end fa quindi in modo che il codice CSS e JS funzioni sia con il vecchio che con il nuovo output.
   1. Come di consueto, per sviluppare localmente, effettuare le seguenti operazioni:
      1. Il comando `npx aem-site-theme-builder proxy` avvia un server proxy che recupera il contenuto da un ambiente AEM. Sostituisce i file CSS e JS del modulo front-end con i file della cartella locale `dist`.
      1. La configurazione della variabile `AEM_URL` nel file nascosto `.env` consente di controllare da quale ambiente AEM il server proxy locale utilizza il contenuto.
      1. La modifica del valore di `AEM_URL` consente quindi di passare dagli ambienti di produzione a quelli di sviluppo per adeguare CSS e JS in modo che siano adatti a entrambi gli ambienti.
      1. Deve funzionare con l’ambiente di sviluppo che esegue il rendering del nuovo output e con l’ambiente di produzione che esegue il rendering del vecchio output.
   1. Il lavoro front-end viene completato quando il modulo front-end aggiornato funziona per entrambi gli ambienti e viene distribuito in entrambi.
1. Il team back-end può quindi aggiornare l’ambiente di produzione distribuendo il codice che esegue il rendering del nuovo output HTML o JSON, o di entrambi, tramite la pipeline full stack.
1. Il team front-end può pulire i propri CSS e JS, rimuovere gli elementi necessari solo per l’output precedente e distribuire l’aggiornamento finale alla produzione utilizzando la pipeline front-end.

## Risorse aggiuntive {#additional-resources}

* Scopri come utilizzare i temi del sito AEM per personalizzare lo stile e la progettazione del sito.

  Vedi [Temi del sito](/help/sites-cloud/administering/site-creation/site-themes.md).

* Adobe fornisce un generatore di temi del sito AEM come set di script per la creazione di nuovi temi.

  Vedi [Generatore di temi del sito AEM](https://github.com/adobe/aem-site-theme-builder)



