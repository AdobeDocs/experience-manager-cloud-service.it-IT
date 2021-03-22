---
title: Domande frequenti sull'integrazione di AEM e commerce tramite Commerce Integration Framework
description: Domande frequenti sull'integrazione di AEM e commerce tramite Commerce Integration Framework
translation-type: tm+mt
source-git-commit: 903a78d98082b937128073d5edce23dc70b01a1d
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 68%

---


# Domande frequenti sull&#39;integrazione di AEM e commerce tramite Commerce Integration Framework


## 1. CIF GraphQL è utilizzato solo per l’e-commerce o sarà disponibile per eseguire query sui contenuti creati su AEM JCR?

 Adobe ha adottato le API GraphQL di Magento come API Commerce ufficiali per tutti i dati relativi all’e-commerce. Quindi, AEM utilizza GraphQL per scambiare dati di e-commerce con Magento e con qualsiasi motore di e-commerce tramite I/O Runtime. Questa API GraphQL è indipendente AEM API GraphQL per accedere ai frammenti di contenuto.

## 2. Qual è il ruolo di Adobe I/O? AEM dialoga direttamente con Magento?

AEM può collegarsi direttamente a Magento senza un livello I/O Runtime. Se è necessario integrare con AEM un back-end di e-commerce non Magento (soluzione di terze parti), la piattaforma I/O Runtime può essere utilizzata per ospitare il livello di mappatura che consente di collegare le API GraphQL di Magento a qualsiasi API di soluzioni di terze parti. Per maggiori dettagli su questo punto, consulta questa [implementazione di riferimento](https://github.com/adobe/commerce-cif-graphql-integration-reference). Per le soluzioni non di Magento, AEM dovrebbe essere configurato per puntare all’endpoint I/O Runtime.

La piattaforma I/O Runtime può essere utilizzata anche per estendere o personalizzare i servizi di e-commerce. Per questi casi d’uso, si richiama l’endpoint I/O Runtime che ospiterà un’implementazione personalizzata del rispettivo servizio. È possibile combinare insieme casi di utilizzo di integrazione e di estensione.

## 3. È possibile memorizzare le risorse dei prodotti (immagini) e farvi riferimento da AEM tramite le funzioni di amministrazione di Magento? Come possono essere utilizzate le risorse da Dynamic Media?

Attualmente non esiste un’integrazione AEM Assets-Magento. Come soluzione alternativa, è possibile archiviare le risorse dei prodotti (immagini) in AEM Assets, ma occorre memorizzare manualmente gli URL delle risorse in Magento. Dynamic Media fa ora parte di AEM Assets e funziona allo stesso modo.

## 4. È importante dove viene implementata la soluzione commerce? on-premise o nel cloud?

Non importa dove viene distribuita la soluzione commerce. L’integrazione e la nuova vetrina AEM Venia Store funzioneranno indipendentemente dal modello di implementazione. Tuttavia, se viene implementato in base all’architettura di riferimento E2E approvata, verranno eseguiti test E2E in base ai KPI delle prestazioni raccolti che rappresentano il profilo di un cliente aziendale. Questo vi fornirà informazioni aggiuntive che possono essere usate come benchmark.

## 5. In che modo vengono create le pagine di catalogo o di prodotto in AEM? Come persistono in AEM?

Le pagine di catalogo e di prodotto vengono create e memorizzate nella cache in AEM in base a modelli generici per pagine di catalogo e di prodotto. Nessun dato di prodotto o catalogo viene importato e memorizzato in AEM.

## 6. Quando aggiorni i dati di prodotto nella tua soluzione commerce, è un push in tempo reale a AEM? oppure si tratta di un processo batch?

Il componente aggiuntivo CIF utilizzato con AEM Cloud Service consente il flusso dei dati dalla soluzione commerce a AEM on-demand. Pertanto, non si tratta di un processo push in tempo reale o batch quando è presente un aggiornamento nella soluzione commerce.

## 7. Qual è la dimensione del catalogo AEM con il supporto CIF?

Poiché i dati di prodotto e le pagine di catalogo vengono creati e memorizzati nella cache in modo dinamico, non vi è alcun limite di dimensione per la correzione. La dimensione del catalogo è, tuttavia, solo un aspetto che è necessario considerare. Rapporto di cache, richieste di dati simultanee e creazione di pagine possono avere un impatto sulla scalabilità e sulle prestazioni.

## 8. Che ruolo svolge un sistema PIM in questo framework?

I dati di un sistema PIM (Product Information Management, gestione delle informazioni dei prodotti) vengono esposti ad AEM e ai client tramite le richieste GraphQL. Si consiglia di integrare PIM con il motore di e-commerce (Magento o altri) in modo che i dati PIM possano essere recuperati dal motore di e-commerce.

## 9. È possibile memorizzare nella cache anche i prezzi e altri dati tramite Dispatcher? Questo potrebbe comportare problemi di invalidazione frequente della cache?

I dati dinamici come prezzo o inventario non vengono memorizzati nella cache di Dispatcher. I dati dinamici vengono recuperati lato client con i componenti Web direttamente tramite le API GraphQL. Nella cache di Dispatcher vengono memorizzati solo i dati statici (come i dati di prodotto o categoria). Se i dati di prodotto cambiano, sarà necessario invalidare la cache.

## 10. Come funziona l’invalidazione della cache per AEM Dispatcher con AEM e commerce?

È consigliabile impostare l’invalidazione della cache basata su TTL per le pagine memorizzate nella cache di Dispatcher. Per informazioni dinamiche come prezzo o inventario, si consiglia di eseguire il rendering dei dati lato client. Per ulteriori informazioni sull’invalidazione della cache basata su TTL, consulta [AEM Dispatcher](https://helpx.adobe.com/it/experience-manager/kb/optimizing-the-dispatcher-cache.html).

## 11. Vi sono consigli sulla ricerca unificata nei contenuti AEM con Commerce?

Viene fornita un’implementazione di riferimento per la ricerca di prodotti, ma non viene eseguita alcuna ricerca unificata con i contenuti. In genere questa funzione dipende molto dalle specifiche esigenze dei clienti, ed è quindi preferibile gestirla a livello di progetto.

## 12. Come funziona la ricerca con AEM e commercio utilizzando CIF?

CIF fornisce i componenti Barra di ricerca e Risultati di ricerca. Il componente Barra di ricerca invia una richiesta GraphQL con il termine di ricerca alla soluzione di e-commerce che restituisce un elenco di prodotti che include nome prodotto, prezzo, SLUG, ecc. Il componente Risultato di ricerca visualizza quindi i risultati della ricerca in una visualizzazione a galleria su una pagina di risultati di ricerca creata su AEM. Il componente Ricerca supporta la ricerca full-text. Utilizziamo la chiave SLUG/url per creare un riferimento al PDP.

## 13. Come possono essere utilizzati i dati di prodotto in MSM o nelle traduzioni?

I dati del prodotto sono generalmente già tradotti in PIM o in Magento. L’integrazione AEM - Magento supporta la connessione a più store e viste store di Magento. In genere, in una configurazione MSM un sito AEM è collegato a una vista store di Magento.

## 14. Come funziona CIF con le piattaforme di e-commerce non di Magento?

L’integrazione con soluzioni di terze parti, come altre soluzioni commerce (non Magento) viene realizzata tramite la piattaforma I/O Runtime. Abbiamo creato un’[implementazione di riferimento](https://github.com/adobe/commerce-cif-graphql-integration-reference) per dimostrare come ciò avviene. Questo consente di riutilizzare [AEM CIF Cloud Connector](https://github.com/adobe/commerce-cif-connector) e i [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) esponendo l’API GraphQL di Magento su qualsiasi piattaforma di e-commerce di terze parti. Per offrire la massima flessibilità e scalabilità, questo livello di integrazione è implementato sulla piattaforma [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) senza server.

## 15. Esiste un modo per migliorare i dati di prodotto con testo commerciale? Dove si effettua questa procedura? In AEM o nella soluzione commerce?

È consigliabile gestire i dati e i contenuti relativi al marketing in AEM. Decorare i dati di prodotto dalla soluzione commerce con attributi aggiuntivi utilizzando Frammenti di contenuto o creare e collegare Frammenti di esperienza per contenuti non strutturati con i tuoi prodotti.

## 16. L’integrazione AEM-Magento cambia quando si utilizza la piattaforma Adobe I/O Runtime?

I clienti che desiderano estendere i servizi di e-commerce possono utilizzare le stesse sequenze di azioni di integrazione e scrittura ospitate sulla piattaforma I/O Runtime per inserire una logica di business e arricchire i servizi commerce.

## 17. Una vetrina di tipo applicazione a pagina singola funziona con l’editor di AEM per applicazioni a pagina singola?

AEM può essere utilizzato come strumento di creazione di contenuti per qualsiasi tipo di vetrina. Attualmente, il rendering lato server e client (ibrido) viene utilizzato in AEM vetrina. In seguito verrà introdotto il supporto PWA per l’authoring di contenuti headless e headful.


## 18. Come possiamo garantire la conformità PCI quando si utilizza AEM per l’intero livello di presentazione?

Si consiglia di utilizzare metodi di pagamento astratti. In questo modo il client browser comunica direttamente con il provider del gateway dei pagamenti in modo che né l&#39;Adobe né le soluzioni commerce detengano o trasmettano i dati del titolare della carta. Questo approccio richiede solo una conformità PCI di livello 3. Tuttavia, vi sono altri elementi da considerare per assicurare la piena conformità allo standard PCI, come il modo in cui i dipendenti interagiscono con il sistema e i dati. Per ulteriori informazioni sulla conformità PCI di Magento, consulta https://magento.com/pci-compliance

## 19. Se uso versioni cloud AEM e di Magento, questa soluzione comune è compatibile con PCI?

Sì, il Questionario di autovalutazione D e la Certificazione di conformità sono disponibili su richiesta.


## 20. Come posso richiedere una licenza di prova di I/O Runtime?

Per richiedere una licenza di prova per utilizzare I/O Runtime, visita [questa pagina](https://adobeio.typeform.com/to/obqgRm).
