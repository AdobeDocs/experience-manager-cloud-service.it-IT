---
title: AEM - Domande frequenti sull’integrazione con Magento tramite Commerce Integration Framework
description: AEM - Domande frequenti sull’integrazione con Magento tramite Commerce Integration Framework
translation-type: ht
source-git-commit: cafe8825fe34f158c74b94b95b7252394de26e4d
workflow-type: ht
source-wordcount: '1321'
ht-degree: 100%

---


# AEM - Domande frequenti sull’integrazione con Magento tramite Commerce Integration Framework


## 1. GraphQL è utilizzato solo per Magento o sarà disponibile per eseguire query sui contenuti creati con AEM JCR?

 Adobe ha adottato le API GraphQL di Magento come API Commerce ufficiali per tutti i dati relativi all’e-commerce. Quindi, AEM utilizza GraphQL per scambiare dati di e-commerce con Magento e con qualsiasi motore di e-commerce tramite I/O Runtime.

## 2. Qual è il ruolo di Adobe I/O? AEM dialoga direttamente con Magento?

AEM può collegarsi direttamente a Magento senza un livello I/O Runtime. Se è necessario integrare con AEM un back-end di e-commerce non Magento (soluzione di terze parti), la piattaforma I/O Runtime può essere utilizzata per ospitare il livello di mappatura che consente di collegare le API GraphQL di Magento a qualsiasi API di soluzioni di terze parti. Per maggiori dettagli su questo punto, consulta questa [implementazione di riferimento](https://github.com/adobe/commerce-cif-graphql-integration-reference). Per le soluzioni non di Magento, AEM dovrebbe essere configurato per puntare all’endpoint I/O Runtime.

La piattaforma I/O Runtime può essere utilizzata anche per estendere o personalizzare i servizi di e-commerce. Per questi casi d’uso, si richiama l’endpoint I/O Runtime che ospiterà un’implementazione personalizzata del rispettivo servizio. È possibile combinare insieme casi di utilizzo di integrazione e di estensione.

## 3. È possibile memorizzare le risorse dei prodotti (immagini) e farvi riferimento da AEM tramite le funzioni di amministrazione di Magento? Come possono essere utilizzate le risorse da Dynamic Media?

Attualmente non esiste un’integrazione AEM Assets-Magento. Come soluzione alternativa, è possibile archiviare le risorse dei prodotti (immagini) in AEM Assets, ma occorre memorizzare manualmente gli URL delle risorse in Magento. Dynamic Media fa ora parte di AEM Assets e funziona allo stesso modo.

## 4. Ha importanza se Magento viene implementato on-premise o nel cloud?

Non importa dove viene implementato Magento. L’integrazione e la nuova vetrina AEM Venia Store funzioneranno indipendentemente dal modello di implementazione. Tuttavia, se viene implementato in base all’architettura di riferimento E2E approvata, verranno eseguiti test E2E in base ai KPI delle prestazioni raccolti che rappresentano il profilo di un cliente aziendale. Questo vi fornirà informazioni aggiuntive che possono essere usate come benchmark.

## 5. In che modo vengono create le pagine di catalogo o di prodotto in AEM? Come persistono in AEM?

Le pagine di catalogo e di prodotto vengono create e memorizzate nella cache in AEM in base a modelli generici per pagine di catalogo e di prodotto. Nessun dato di prodotto o catalogo viene importato e memorizzato in AEM.

## 6. È possibile memorizzare nella cache anche i prezzi e altri dati tramite Dispatcher? Questo potrebbe comportare problemi di invalidazione frequente della cache?

I dati dinamici come prezzo o inventario non vengono memorizzati nella cache di Dispatcher. I dati dinamici vengono recuperati lato client con i componenti Web direttamente tramite le API GraphQL. Nella cache di Dispatcher vengono memorizzati solo i dati statici (come i dati di prodotto o categoria). Se i dati di prodotto cambiano, sarà necessario invalidare la cache.

## 7. Come funziona l’invalidazione della cache per AEM Dispatcher con AEM-Magento?

È consigliabile impostare l’invalidazione della cache basata su TTL per le pagine memorizzate nella cache di Dispatcher. Per informazioni dinamiche come prezzo o inventario, si consiglia di eseguire il rendering dei dati lato client. Per ulteriori informazioni sull’invalidazione della cache basata su TTL, consulta [AEM Dispatcher](https://helpx.adobe.com/it/experience-manager/kb/optimizing-the-dispatcher-cache.html).

## 8. Perché non si utilizza We.Retail?

Viene utilizzato il tema Venia (sviluppato da Magento), che è mobile e allineato con il PWA di Magento. Il tema Venia rappresenta l’ultima versione in termini di stile CSS e componenti core di AEM.

## 9. Quando si aggiornano i dati di prodotto in Magento, questi vengono trasmessi in tempo reale ad AEM oppure si tratta di un processo batch?

Grazie al componente aggiuntivo CIF utilizzato con AEM Cloud Service, il flusso di dati da Magento ad AEM avviene on-demand. Di conseguenza, un aggiornamento in Magento non comporta alcun processo push in tempo reale o batch.

## 10. Vi sono consigli sulla ricerca unificata nei contenuti AEM con Commerce?

Viene fornita un’implementazione di riferimento per la ricerca di prodotti, ma non viene eseguita alcuna ricerca unificata con i contenuti. In genere questa funzione dipende molto dalle specifiche esigenze dei clienti, ed è quindi preferibile gestirla a livello di progetto.

## 11. Come funziona la ricerca con AEM-Magento utilizzando CIF?

CIF fornisce i componenti Barra di ricerca e Risultati di ricerca. Il componente Barra di ricerca invia una richiesta GraphQL con il termine di ricerca a Magento. Magento restituisce un elenco di prodotti che include nome del prodotto, prezzo, descrizione abbreviata (SLUG), ecc. Il componente Risultato di ricerca visualizza quindi i risultati della ricerca in una visualizzazione a galleria su una pagina di risultati di ricerca creata su AEM. Il componente Ricerca supporta la ricerca full-text. Utilizziamo la chiave SLUG/url per creare un riferimento al PDP.

## 11. Come possono essere utilizzati i dati di prodotto in MSM o nelle traduzioni?

I dati del prodotto sono generalmente già tradotti in PIM o in Magento. L’integrazione AEM - Magento supporta la connessione a più store e viste store di Magento. In genere, in una configurazione MSM un sito AEM è collegato a una vista store di Magento.

## 13. Come funziona CIF con altre piattaforme commerce?

L’integrazione con soluzioni di terze parti, come altre soluzioni commerce (non Magento) viene realizzata tramite la piattaforma I/O Runtime. Abbiamo creato un’[implementazione di riferimento](https://github.com/adobe/commerce-cif-graphql-integration-reference) per dimostrare come ciò avviene. Questo consente di riutilizzare [AEM CIF Cloud Connector](https://github.com/adobe/commerce-cif-connector) e i [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) esponendo l’API GraphQL di Magento su qualsiasi piattaforma di e-commerce di terze parti. Per offrire la massima flessibilità e scalabilità, questo livello di integrazione è implementato sulla piattaforma [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) senza server.

## 14. Esiste un modo per migliorare i dati di prodotto con testo commerciale? Dove si effettua questa procedura? In AEM o in Magento?

Ci sono diversi modi per farlo, a seconda del caso d’uso. Ad esempio, si possono usare attributi personalizzati. Consenti agli autori AEM di modificare questi campi nell’editor di prodotti di AEM e sincronizzarli nuovamente con la soluzione PIM. Un’altra opzione consiste nell’utilizzare Frammenti di esperienza AEM da inserire nelle pagine dei prodotti.

## 15. L’integrazione AEM-Magento cambia quando si utilizza la piattaforma Adobe I/O Runtime?

I clienti che desiderano estendere i servizi di e-commerce possono utilizzare le stesse sequenze di azioni di integrazione e scrittura ospitate sulla piattaforma I/O Runtime per inserire una logica di business e arricchire i servizi commerce.

## 16. Dal momento che AEM crea in modo dinamico pagine di prodotti e cataloghi basate su un modello generico in AEM, cosa si vede quando si controlla in contenuto in CRXDE Lite? Un’intera struttura ad albero di prodotti in base ai prodotti in Magento? In caso negativo, in che modo un autore può migliorare le pagine?

Non esistono più pagine JCR di catalogo o di prodotti. Consulta la risposta alla domanda 12.

## 17. Una vetrina di tipo applicazione a pagina singola funziona con l’editor di AEM per applicazioni a pagina singola?

AEM può essere utilizzato come strumento di creazione di contenuti per qualsiasi tipo di vetrina. Attualmente, per la nuova vetrina viene utilizzato un rendering ibrido. In futuro, AEM sarà utilizzato per la creazione di contenuti di tipo SPA (applicazione a pagina singola) e PWA (app Web progressiva).

## 18. Che ruolo svolge un sistema PIM in questo framework?

I dati di un sistema PIM (Product Information Management, gestione delle informazioni dei prodotti) vengono esposti ad AEM e ai client tramite le richieste GraphQL. Consigliamo di integrare un sistema PIM con il motore di e-commerce (Magento o altro) in modo che i dati PIM possano essere recuperati dal motore di e-commerce.

## 19. Come possiamo garantire la conformità PCI quando si utilizza AEM per l’intero livello di presentazione?

Quando si utilizzano AEM su AMS e l’implementazione cloud di Magento, è obbligatorio utilizzare metodi di pagamento astratti. In tal modo il client browser comunica direttamente con il provider del gateway dei pagamenti e i dati sensibili dei titolari della carta non vengono trasmessi né memorizzati nel cloud di Adobe né di Magento. Questo approccio permette di rispettare i requisiti PCI per gli stack tecnologici e i data center. Tuttavia, vi sono altri elementi da considerare per assicurare la piena conformità allo standard PCI, come il modo in cui i dipendenti interagiscono con il sistema e i dati. Per ulteriori informazioni sulla conformità PCI di Magento, consulta https://magento.com/pci-compliance

## 20. Come posso richiedere una licenza di prova di I/O Runtime?

Per richiedere una licenza di prova per utilizzare I/O Runtime, visita [questa pagina](https://github.com/AdobeDocs/adobeio-runtime/blob/master/overview/request_a_trial.md).



