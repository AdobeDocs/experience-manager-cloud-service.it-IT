---
title: Panoramica di Edge Delivery Services
description: Scopri in che modo AEM as a Cloud Service può trarre vantaggio dalle prestazioni e dai punteggi impeccabili di Lighthouse offerti da Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 6c7e704dff97e8549664618f879863c3ca0f8f86
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 55%

---


# Panoramica di Edge Delivery Services {#edge-delivery-services}

Con Edge Delivery Services, AEM offre esperienze eccezionali che stimolano coinvolgimento e conversioni. AEM lo fa offrendo esperienze ad alto impatto veloci da creare e sviluppare. Scopri Edge Delivery Services, un set di servizi componibili per un ambiente di sviluppo rapido in cui i contenuti possano essere aggiornati e pubblicati rapidamente dagli autori e che consente il lancio rapido di nuovi siti. Di conseguenza, con Edge Delivery Services è possibile migliorare la conversione, ridurre i costi e velocizzare le attività relative ai contenuti.

Utilizzando Edge Delivery Services, è possibile:

* Creare siti veloci con un punteggio Lighthouse perfetto e monitorare continuamente le prestazioni del sito tramite il monitoraggio dell’utilizzo reale (RUM, Real Use Monitoring).
* Aumentare l’efficienza di authoring separando le origini dei contenuti. È possibile utilizzare sia la modalità WYSIWYG che l’authoring basato su documenti. Di conseguenza, puoi lavorare con più origini di contenuto sullo stesso sito Web.
* Utilizza un framework di sperimentazione integrato che consente di creare e di eseguire rapidamente i test senza alcun impatto sulle prestazioni e di rilasciare rapidamente in produzione un vincitore di test.

## Reazione agile alle esigenze aziendali {#agile-reaction}

Adobe, da sempre leader del settore, sa quanto sia importante poter creare e pubblicare rapidamente nuovi contenuti significativi per i clienti. Il mercato ha messo in evidenza le sfide comuni in materia di scalabilità della creazione dei contenuti, tra cui:

1. **La domanda di contenuto continua a crescere.**
   * È necessario sbloccare nuovi autori di contenuti per soddisfare questa domanda.
   * Il processo di creazione dei contenuti deve essere scalabile in modo efficace a livello aziendale.
   * Gli autori devono essere in grado di reagire rapidamente ai cambiamenti di tendenza.
1. **È necessario il contenuto omni-channel.**
   * Il controllo del layout è necessario indipendentemente dalla distribuzione dei contenuti.
   * Gli autori devono avere la possibilità di modificare direttamente il layout dei contenuti.
1. **La pressione aumenta per incrementare il ROI sui contenuti.**
   * Gli stessi autori devono poter ottimizzare i contenuti creati.

Queste tendenze si sono dimostrate coerenti in tutto il settore. Tuttavia, i requisiti individuali variano inevitabilmente da progetto a progetto. L’obiettivo di qualsiasi progetto di Edge Delivery Services è quello di trovare la soluzione che funzioni per i tuoi utenti.

1. **Concentrati sul valore invece che sulle funzionalità.** - Determina il flusso di lavoro più ottimizzato per gli autori anziché perderti nel set di funzioni espansive dell&#39;AEM.
1. **Sfruttare la flessibilità dell&#39;AEM.** - Non è necessario utilizzare le funzionalità AEM nel vuoto. Utilizza le funzioni necessarie per ogni caso d’uso.
1. **Sfrutta l&#39;esperienza dell&#39;autore.** - Coinvolgi gli autori di contenuti reali nel progetto fin dall&#39;inizio per assicurarti di fornire il valore di cui hanno bisogno implementando le funzionalità più appropriate.

Concentrandosi sul valore per gli autori, il progetto di Edge Delivery Services può soddisfare le esigenze del settore moderno che i creatori di contenuti devono affrontare e fornire contenuti rapidamente per deliziare i clienti.

## Strumenti di authoring flessibili per i creatori di contenuti {#overview}

Edge Delivery Services è un set di sevizi componibili che consente un elevato grado di flessibilità per quanto riguarda la creazione di contenuti sul sito web. Puoi utilizzare sia [Gestione dei contenuti AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=it) che l’authoring WYSIWYG utilizzando l’[Editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md) nonché l’[authoring basato su documenti.](https://www.aem.live/docs/authoring)

Il diagramma seguente illustra come modificare il contenuto in Microsoft Word (modifica basata su documento) e pubblicarlo in Edge Delivery Services. Mostra anche la modifica WYSIWYG utilizzando l’editor universale.

![Architettura di Edge Delivery](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services sfrutta GitHub per consentirti di gestire e distribuire il codice direttamente dall’archivio GitHub. I nuovi contenuti vengono aggiunti immediatamente senza un processo di ricostruzione.

### Authoring basato su documenti {#document-based}

Con l’authoring basato su documenti, è possibile utilizzare il contenuto direttamente dai documenti di Microsoft Word o Google in modo che tali origini diventino pagine del sito web. Le intestazioni, gli elenchi, le immagini e gli elementi dei caratteri possono essere trasferiti dalla sorgente iniziale al sito Web.

* Con l’authoring basato su documenti, ogni addetto al marketing è in grado di creare rapidamente contenuti con strumenti di authoring noti (Microsoft Word, Google Docs, ecc.).
* La creazione dei contenuti è semplificata consentendo l&#39;authoring, la revisione e la pubblicazione direttamente all&#39;interno dei documenti sorgente.
* Poiché vengono utilizzati strumenti noti, per gli autori di contenuti non è richiesto alcun onboarding, con conseguente aumento della velocità dei contenuti.
* Le funzionalità del sito possono essere sviluppate utilizzando CSS e JavaScript in GitHub.

![Authoring basato su documenti](assets/document-based-authoring.png)

Ulteriori informazioni sono disponibili nella documentazione relativa all’authoring basato su documenti:

* Per informazioni dettagliate su come iniziare a utilizzare Edge Delivery, consulta la [sezione Creare](https://www.aem.live/docs/#build).
* Per capire come creare e pubblicare contenuti utilizzando Edge Delivery, consulta la [sezione Pubblicare.](https://www.aem.live/docs/authoring)
* Per informazioni su come avviare correttamente il progetto del sito Web, consulta la [sezione Avvio](https://www.aem.live/docs/#launch).

### Authoring WYSIWYG {#wysiwyg-authoring}

L’authoring WYSIWYG (What-you-see-is-what-you-get) sfrutta Universal Editor, uno strumento personalizzabile per la modifica dei contenuti in tempo reale e nel contesto con un’anteprima visiva.

* Con l’authoring WYSIWYG, puoi aumentare l’efficienza dell’authoring sia headless che headful.
* Puoi sfruttare le funzionalità complete di gestione dei contenuti dell&#39;AEM, inclusi il flusso di lavoro e la governance.
* Sfrutta numerosi punti di estensione per supportare i tuoi processi e le tue integrazioni.
* Le funzionalità del sito possono essere sviluppate utilizzando CSS e JavaScript in GitHub.

![Authoring WYSIWYG](assets/wysiwyg-authoring.png)

Ulteriori informazioni sono disponibili nella documentazione sull’authoring WYSIWYG:

* Per una panoramica dell&#39;editor universale e dell&#39;authoring WYSIWYG, vedere il documento [Authoring dei contenuti WYSIWYG per Edge Delivery Services.](/help/edge/wysiwyg-authoring/authoring.md)
* Per una panoramica per gli sviluppatori, vedere il documento [Guida introduttiva per gli sviluppatori per l&#39;authoring WYSIWYG con Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)

### Decidere il metodo di authoring {#authoring-method}

La flessibilità dell’AEM garantisce che le tue esigenze di authoring siano soddisfatte. Adobe può aiutarti a determinare quale metodo o metodi si adattano meglio alle tue esigenze.

* Coinvolgi sempre i tuoi autori di contenuti nella decisione.
* È possibile implementare più metodi di authoring.
* Puoi sempre modificare il tuo metodo di authoring dopo il fatto.
* Non devi decidere prima dell’implementazione, ma piuttosto come parte dell’implementazione.

Per ulteriori informazioni, vedere il documento [Scelta di un metodo di creazione](authoring-methods.md).

## Edge Delivery Services e altri prodotti di Adobe Experience Cloud {#edge-other-products}

Edge Delivery Services fa parte di Adobe Experience Manager e, per questo motivo, i siti di Edge Delivery Services e di AEM possono coesistere sullo stesso dominio, pratica diffusa per quanto riguarda i siti web più grandi. Inoltre, il contenuto di Edge Delivery Services può essere facilmente utilizzato nelle pagine di AEM Sites e viceversa.

Consulta la [Guida introduttiva per sviluppatori di authoring di WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) per scoprire come avviare un proprio progetto per l’authoring con AEM e Edge Delivery Services.

È inoltre possibile utilizzare Edge Delivery Services con [Adobe Target](https://www.aem.live/developer/target-integration), con la funzione di [monitoraggio dell’utilizzo reale](https://www.aem.live/developer/rum) (RUM, Real Use Monitoring) per diagnosticare l’utilizzo e le prestazioni dei siti, e con [Launch.](https://experienceleague.adobe.com/it/docs/experience-platform/tags/home)

## Guida introduttiva a Edge Delivery Service {#getting-started}

È facile iniziare a utilizzare Edge Delivery Services seguendo la [Guida introduttiva: tutorial per sviluppatori.](https://www.aem.live/developer/tutorial)

## Ottenere assistenza da Adobe {#getting-help}

Adobe fornisce tre canali per aiutarti con Edge Delivery Services:

* Interazione con le [risorse della community](#community-resources) per rispondere a domande generali.
* Accesso al [canale di collaborazione sui prodotti](#collaboration-channel) per domande specifiche.
* [Registra un ticket di supporto](#support-ticket) per risolvere i problemi importanti e critici.

### Accesso alle risorse della community {#community-resources}

Adobe si impegna a fornire la migliore community e il miglior supporto per Edge Delivery Services, WYSIWYG e l’authoring basato su documenti.

* Aderisci alla [community Experience League](https://adobe.ly/3Q6kTKl) per rivolgere domande, condividere feedback, avviare discussioni, chiedere assistenza da esperti di Adobe e consulenti ed esperti di AEM e connetterti in tempo reale con altri utenti che condividono i tuoi stessi interessi. 
* Segui il nostro [canale Discord](https://discord.gg/aem-live), una piattaforma più informale per interazioni in tempo reale e rapidi scambi di idee.

### Come accedere al canale di collaborazione sui prodotti {#collaboration-channel}

Dato il valore di un canale di comunicazione diretta con gli utenti, all’avvio di ogni progetto AEM viene stabilito un canale Slack per comunicazioni rapide, aggiornamenti critici e reporting scalabile sulla qualità dell’esperienza. Riceverai un invito da Adobe per partecipare a canale Slack specifico per la tua organizzazione.

Per ulteriori informazioni, consulta [Utilizzo del bot di Slack](https://www.aem.live/docs/slack).

Puoi interagire con i team di prodotto Adobe tramite il canale di collaborazione sui prodotti fornito per domande sull’utilizzo dei prodotti o sulle best practice. Non sono presenti termini di livello di servizio (Service Level Terms, SLT) associati alle conversazioni tramite il canale di collaborazione sui prodotti.

### Registrare un ticket di supporto {#support-ticket}

Se un problema relativo a un prodotto richiede ulteriori indagini e tentativi di risoluzione e deve soddisfare gli SLT di risposta, puoi inviare un ticket di supporto seguendo la Admin Console.

1. Crea un ticket [seguendo la procedura di assistenza standard](https://experienceleague.adobe.com/?support-tab=home?lang=it#support).
1. Aggiungi **Edge Delivery** nel titolo del ticket.
1. Nella descrizione, fornisci i dettagli seguenti oltre alla descrizione del problema:

   * URL del sito web live. Ad esempio: `www.mydomain.com`.
   * URL del sito web di origine (URL `.hlx`).

## Passaggio successivo {#whats-next}

Per iniziare, consulta [Utilizzo di Edge Delivery Services](/help/edge/using.md).
