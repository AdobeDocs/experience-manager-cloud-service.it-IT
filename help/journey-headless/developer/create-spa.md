---
title: Facoltativo - Come creare applicazioni a pagina singola (SPA) con Adobe Experience Manager (AEM)
description: In questa continuazione facoltativa del Percorso per sviluppatori AEM headless, scoprirai come AEM riesce a unire la distribuzione headless con le tradizionali funzioni di un CMS full-stack e come tu puoi creare SPA modificabili utilizzando il framework editor di SPA di AEM.
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 48%

---

# Come creare applicazioni a pagina singola (SPA) con AEM {#create-spa}

In questa continuazione facoltativa del [Percorso di sviluppatori AEM headless](overview.md), scopri come l’AEM può combinare la distribuzione headless con le funzioni CMS full stack tradizionali. Scopri anche come creare SPA modificabile utilizzando il framework dell’Editor SPA dell’AEM e integrare l’SPA esterno, abilitando le funzionalità di modifica in base alle esigenze.

## Percorso affrontato finora {#story-so-far}

A questo punto, avresti dovuto completare l’intero [Percorso per sviluppatori headless AEM](overview.md) e dovresti aver appreso le nozioni di base sulla distribuzione headless in AEM, oltre ad aver compreso:

* La differenza tra distribuzione headless e headful dei contenuti.
* Le funzionalità headless di AEM.
* Come organizzare un progetto AEM headless.
* Come creare contenuti headless in AEM.
* Come recuperare e aggiornare il contenuto headless in AEM.
* Come pubblicare con un progetto AEM headless.

Fino ad ora, o sei andato in diretta con il tuo primo progetto AEM Headless o hai le conoscenze per farlo. Congratulazioni. 

Allora, perché leggete questa ulteriore, facoltativa continuazione del percorso? Se ne ricorda nel [Guida introduttiva](getting-started.md#integration-levels)Inoltre, è stato discusso come l’AEM non solo supporti la distribuzione headless e i modelli tradizionali full-stack, ma supporti modelli ibridi che combinano i vantaggi di entrambi. Anche se non può farlo il modello tradizionale headless, questi modelli ibridi possono offrire una grandissima flessibilità per determinati progetti.

Questo articolo sviluppa la tua conoscenza di AEM Headless esplorando in modo approfondito come creare le tue applicazioni a pagina singola (SPA) modificabili in AEM. In questo modo, puoi creare contenuti e distribuirli direttamente a un SPA, ma l’SPA rimane modificabile nell’AEM.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come vengono sviluppate le applicazioni a pagina singola utilizzando il framework editor di SPA di AEM. Dopo aver letto questo documento, dovresti:

* Avere compreso le funzioni di base dell’Editor di SPA.
* Conoscere i requisiti per creare una SPA completamente modificabile per AEM.
* Avere compreso come integrare SPA esterne in AEM.
* Scopri come implementare o meno il rendering lato server.

## Requisiti e prerequisiti {#requirements-prerequisites}

Ci sono diversi requisiti prima di iniziare a lavorare con SPA nell’AEM.

### Conoscenza {#knowledge}

* Esperienza di sviluppo nella creazione di SPA con i framework React o Angular
* Competenze di base in AEM per la creazione di frammenti di contenuto e l’utilizzo dell’editor
* Assicurati di rivedere il documento [Headful e Headless nell&#39;AEM](/help/implementing/developing/headful-headless.md) in modo da comprendere i vari livelli di integrazione dell&#39;SPA possibili.

### Strumenti {#tools}

* Accesso alla sandbox per testare la distribuzione del progetto
* Istanza di sviluppo locale per la modellazione dei dati e il testing
* SPA esterna esistente (facoltativa, a seconda del modello di integrazione scelto)
* Archetipo progetto AEM

## Cos’è una SPA? {#what-is-a-spa}

Un’applicazione a pagina singola (SPA) differisce da una pagina convenzionale in quanto viene sottoposta a rendering lato client ed è principalmente basata su JavaScript, poiché si basa sulle chiamate Ajax per caricare i dati e aggiornare dinamicamente la pagina. La maggior parte o tutti i contenuti vengono recuperati una volta in un singolo caricamento di pagina, con risorse aggiuntive caricate in modo asincrono in base alle esigenze, in base all’interazione dell’utente con la pagina.

Questa funzionalità riduce la necessità di aggiornamenti delle pagine e offre all’utente un’esperienza fluida, veloce e simile a un’esperienza nativa per l’app.

L’editor AEM di SPA consente agli sviluppatori front-end di creare SPA che possono essere integrate in un sito AEM, permettendo agli autori dei contenuti di modificare il contenuto delle SPA con la stessa facilità con cui sono modificati altri contenuti AEM.

## Perché una SPA? {#why-spa}

Essendo più veloce, fluido e simile a un&#39;applicazione nativa, un SPA diventa un&#39;esperienza attraente. È utile non solo per il visitatore della pagina web, ma anche per gli esperti di marketing e gli sviluppatori a causa della natura del modo in cui funziona l’SPA.

Per una descrizione completa delle SPA e del motivo per cui utilizzarle, consulta la sezione [risorse aggiuntive](#additional-resources): troverai i collegamenti a una documentazione più dettagliata.

## Come AEM gestisce le SPA

Lo sviluppo di applicazioni a pagina singola in AEM presuppone che lo sviluppatore front-end osservi le best practice standard durante la creazione di una SPA. In qualità di sviluppatore front-end, se segui queste best practice generali e alcuni principi specifici dell’AEM, il tuo SPA diventa funzionale con l’AEM e le sue funzionalità di authoring dei contenuti.

* **Portabilità** - Come per qualunque componente, i componenti SPA devono essere costruiti in modo da essere il più possibile portatili. La SPA deve essere realizzata con componenti portabili e riutilizzabili.
* **Struttura del sito di guida AEM** - Lo sviluppatore front-end crea i componenti e possiede la propria struttura interna, ma si affida all’AEM per definire la struttura del contenuto del sito.
* **Rendering dinamico** - Tutto il rendering deve essere dinamico.
* **Routing dinamico** - La SPA è responsabile del routing e AEM lo ascolta ed esegue il recupero in base ad esso. Anche altri routing devono essere dinamici.

Per una descrizione completa di come AEM gestisce le SPA, consulta la sezione [risorse aggiuntive](#additional-resources) per i collegamenti a una documentazione più dettagliata.

## Editor SPA di AEM  {#aem-spa-editor}

I siti generati utilizzando framework SPA comuni, come React e Angular, caricano i contenuti tramite JSON dinamico. Non forniscono la struttura HTML necessaria affinché l’Editor pagina AEM possa inserire i controlli di modifica.

Per consentire la modifica dell’SPA all’interno dell’AEM, è necessario mappare l’output JSON dell’SPA e il modello di contenuto nell’archivio AEM per poter salvare le modifiche al contenuto.

Il supporto SPA nell&#39;AEM introduce un sottile livello JavaScript che interagisce con il codice JavaScript dell&#39;SPA quando viene caricato nell&#39;Editor pagina con cui è possibile inviare gli eventi. È possibile attivare la posizione dei controlli di modifica per consentire la modifica contestuale. Questa funzione si basa sul concetto di endpoint API di Content Services, in quanto il contenuto dell’SPA deve essere caricato tramite Content Services.

Per una descrizione completa dell’editor di SPA AEM, consulta la sezione [risorse aggiuntive](#additional-resources) per i collegamenti a una documentazione più dettagliata.

## Alloggio SPA esistenti {#existing-spas}

Se disponi già di un SPA, l’AEM supporta la sua incorporazione nell’AEM in modo che sia visibile agli autori di contenuti nell’editor AEM. Questa funzionalità può essere utile per visualizzare il contenuto che stanno creando tramite Frammenti di contenuto nel contesto dell’applicazione finale in cui viene utilizzato.

Inoltre, con solo piccole modifiche, è possibile abilitare una certa capacità di modifica per l&#39;SPA esterno all&#39;interno dell&#39;Editor AEM.

Il componente RemotePage consente il rendering di un SPA esterno in AEM.

Per una descrizione completa di come rendere modificabile un SPA esterno in AEM, consulta la sezione [risorse aggiuntive](#additional-resources) per i collegamenti a una documentazione più dettagliata.

## Passaggio successivo {#what-is-next}

Per iniziare a sviluppare un proprio SPA per AEM, controlla i seguenti documenti:

* [Tutorial WKND per SPA](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Guida introduttiva all’utilizzo di React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Guida introduttiva all’utilizzo di Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Se devi adattare un SPA esistente per usarlo nell’AEM, consulta i seguenti documenti:

* [Componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)
* [Modifica di uno SPA esterno in AEM](/help/implementing/developing/hybrid/editing-external-spa.md)

Vedi sotto le [risorse aggiuntive](#additional-resources) che possono farti approfondire argomenti SPA in AEM.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate alcune risorse aggiuntive che approfondiscono alcuni concetti menzionati in questo documento.

* [Headful e headless in AEM](/help/implementing/developing/headful-headless.md): descrizione dei diversi modelli di distribuzione disponibili in AEM
* [Introduzione e procedura dettagliata per l’SPA](/help/implementing/developing/hybrid/introduction.md) - una buona introduzione dell’SPA nell’AEM.
* [Sviluppo di SPA per AEM](/help/implementing/developing/hybrid/developing.md): linee guida su come sviluppare SPA per AEM
* [Panoramica dell’editor di SPA](/help/implementing/developing/hybrid/editor-overview.md): dettagli sul funzionamento dell&#39;editor SPA
* [Rendering lato server](/help/implementing/developing/hybrid/ssr.md) - Come configurare SSR per AEM SPA
* [Documenti di riferimento SPA](/help/implementing/developing/hybrid/reference-materials.md) AEM - Riferimenti e collegamenti API JavaScript ai progetti open-source SPA GitHub
* [Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments.md): come creare frammenti di contenuto
* [L’Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) è un modello Maven che crea un progetto AEM minimo basato sulle best practice di Adobe Experience Manager (AEM) come punto di partenza per il tuo sito web
