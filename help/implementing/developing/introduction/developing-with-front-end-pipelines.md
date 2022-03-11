---
title: Sviluppo di siti con la pipeline front-end
description: Con la pipeline front-end, viene data maggiore indipendenza agli sviluppatori front-end e il processo di sviluppo può ottenere una notevole velocità.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# Sviluppo di siti con la pipeline front-end {#developing-site-with-front-end-pipeline}

[con la conduttura front-end,](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) maggiore indipendenza è data agli sviluppatori front-end e il processo di sviluppo può ottenere una velocità notevole. Questo documento descrive come questo processo funziona insieme ad alcune considerazioni di cui tenere conto per sfruttare appieno il potenziale di questo processo.

>[!TIP]
>
>Se non hai ancora familiarità con l’utilizzo della pipeline front-end e con i vantaggi che può apportare, consulta la sezione [Percorso di creazione di siti rapidi](/help/journey-sites/quick-site/overview.md) per un esempio su come distribuire rapidamente un nuovo sito e personalizzare il tema in modo completamente indipendente dallo sviluppo back-end.

## Singola fonte di verità {#single-source-of-truth}

Una buona pratica generale è quella di mantenere un&#39;unica fonte di verità per ciò che è distribuito a AEM. L&#39;obiettivo di Cloud Manager è quello di rendere ovvia l&#39;unica fonte di verità. Tuttavia, poiché la pipeline front-end consente di disaccoppiare la posizione per parti del codice, una parte di responsabilità aggiuntiva risiede nella corretta configurazione delle pipeline front-end. È necessario prestare attenzione a non creare più pipeline front-end da distribuire sullo stesso sito nello stesso ambiente.

Per questo motivo, e specialmente quando vengono create più pipeline front-end, si consiglia di mantenere una convenzione di denominazione sistematica come quella riportata di seguito:

* Nome del modulo front-end definito dalla `name` proprietà `package.json` deve contenere il nome del sito a cui si applica. Ad esempio, per un sito che si trova in `/content/wknd`, il nome del modulo front-end è simile a `wknd-theme`.
* Quando un modulo front-end condivide lo stesso archivio Git con altri moduli, il nome della cartella deve essere uguale o contenere lo stesso nome del modulo front-end. Ad esempio, se il modulo front-end è denominato `wknd-theme`, il nome della cartella che lo contiene è simile a `wknd-theme-sources`.
* Il nome della pipeline front-end di Cloud Manager deve contenere anche il nome del modulo front-end e deve anche aggiungere l’ambiente a cui distribuisce (produzione o sviluppo). Ad esempio, per il modulo front-end denominato `wknd-theme`, la pipeline potrebbe essere denominata come `wknd-theme-prod`.

Tale convenzione dovrebbe prevenire efficacemente i seguenti errori di distribuzione:

* Applicazione di un modulo front-end al sito errato
* Creazione di più moduli front-end che applicano lo stesso sito e che si sovrascrivono a vicenda
* Creazione di più pipeline front-end per le stesse sorgenti, il che potrebbe causare condizioni di concorrenza, senza garantire l’ordine delle distribuzioni

## Separazione tra logica e markup {#separation-of-concerns}

Un&#39;altra buona pratica che si applica a qualsiasi separazione delle preoccupazioni è quella di porre particolare attenzione nel modo in cui il contratto che separa le preoccupazioni è progettato e gestito. Nel caso della pipeline front-end, il contratto che separa tale codice dal resto è il HTML e il JSON sottoposti a rendering dal sito. Se HTML e JSON rimangono stabili, la pipeline front-end offre il suo valore massimo rendendo il team front-end completamente indipendente.

Attualmente non esiste una funzionalità specifica per eseguire la pipeline a stack intero in modo sincrono con le pipeline front-end. Per questo motivo, quando si disaccoppiano lo sviluppo front-end dalla pipeline full-stack, occorre prestare maggiore attenzione al contratto che separa queste due aree di preoccupazione. Generalmente, tale contratto è il HTML e/o il JSON di cui Experience Manager esegue il rendering. Le modifiche a tale contratto devono pertanto essere ben pianificate tra i team che gestiscono le diverse condotte in modo che concordino su come sequenziare le modifiche corrispondenti.

I passaggi seguenti sono generalmente consigliati quando è necessario apportare modifiche all’output HTML e/o JSON che influiscono su entrambe le aree problematiche.

1. Il team back-end imposta innanzitutto un ambiente di sviluppo con il nuovo output HTML e/o JSON.
   1. Tramite la pipeline a stack completo, distribuiscono il codice necessario per eseguire il rendering del nuovo output HTML e/o JSON desiderato.
   1. Se si tratta di un ambiente a cui il team front-end non aveva accesso in precedenza, è necessario eseguire i seguenti passaggi.
      1. URL: Il team front-end deve conoscere l’URL di tale ambiente di sviluppo.
      1. ACL: Al team front-end deve essere assegnato un utente AEM locale con qualcosa di simile ai diritti di &quot;Collaboratori&quot;.
      1. Git: Il team front-end deve disporre di una posizione Git separata per il modulo front-end specifico per l’ambiente di sviluppo.
         * Una pratica comune consiste nel creare un `dev` , in modo che le modifiche apportate per l’ambiente di sviluppo possano essere facilmente unite nuovamente nel `main` ramo da distribuire nell’ambiente di produzione.
      1. Pipeline: Il team front-end deve disporre di una pipeline front-end da distribuire nell’ambiente di sviluppo. Tale pipeline distribuirebbe il modulo front-end tipicamente situato nella `dev` come descritto nel punto precedente.
1. Il team front-end quindi fa funzionare il codice CSS e JS sia con il vecchio che con il nuovo output.
   1. Come al solito, per sviluppare localmente:
      1. La `npx aem-site-theme-builder proxy` Il comando eseguito all’interno del modulo front-end avvia un server proxy che richiede il contenuto da un ambiente AEM, sostituendo i file CSS e JS del modulo front-end con quelli del locale `dist` cartella.
      1. Configurazione della `AEM_URL` nella variabile nascosta `.env` file consente di controllare da quale ambiente AEM server proxy locale utilizza il contenuto.
      1. Modifica del valore di questo `AEM_URL` consente quindi di passare dagli ambienti di produzione a quelli di sviluppo per regolare i CSS e JS in modo che si adattino a entrambi gli ambienti.
      1. Deve funzionare con l’ambiente di sviluppo che esegue il rendering del nuovo output e con l’ambiente di produzione che esegue il rendering del vecchio output.
   1. Il lavoro front-end viene completato quando il modulo front-end aggiornato funziona per entrambi gli ambienti e viene distribuito a entrambi.
1. Il team back-end può quindi aggiornare l’ambiente di produzione distribuendo il codice che esegue il rendering del nuovo output HTML e/o JSON tramite la pipeline a stack completo.
1. Il team front-end può quindi ripulire i CSS e JS e rimuovere ciò che era necessario solo per il vecchio output, implementando l’ultimo aggiornamento alla produzione tramite la pipeline front-end.

## Risorse aggiuntive {#additional-resources}

* [Temi del sito](/help/sites-cloud/administering/site-creation/site-themes.md) - Scopri come utilizzare AEM temi del sito per personalizzare lo stile e la progettazione del sito.
* [Generatore di temi del sito AEM](https://github.com/adobe/aem-site-theme-builder) - Adobe fornisce un Generatore di temi del sito AEM come set di script per la creazione di nuovi temi del sito.
