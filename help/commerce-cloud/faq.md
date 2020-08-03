---
title: AEM - Integrazione dei Magenti tramite Commerce Integration Framework Domande frequenti
description: AEM - Integrazione dei Magenti tramite Commerce Integration Framework Domande frequenti
translation-type: tm+mt
source-git-commit: cafe8825fe34f158c74b94b95b7252394de26e4d
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# AEM - Integrazione dei Magenti tramite Commerce Integration Framework Domande frequenti


## 1. GraphQL è utilizzato solo per l&#39;Magento o sarà disponibile per la query di contenuto creato AEM JCR?

 Adobe ha adottato le API GraphQL del Magento come API di commercio ufficiale per tutti i dati relativi al commercio. Quindi, AEM utilizza GraphQL per scambiare dati di commercio con il Magento e con qualsiasi motore di e-commerce tramite I/O Runtime.

## 2. Come vengono  I/O Adobe? AEM direttamente con il Magento?

AEM collegarsi direttamente al Magento senza un livello I/O Runtime. Se è necessario integrare un back-end di e-commerce non di Magento (soluzione di terze parti) con AEM, la piattaforma Runtime I/O può essere utilizzata per ospitare il livello di mappatura per collegare le API GraphQL Magento a qualsiasi API di soluzioni di terze parti. Per maggiori dettagli su questo punto, consulta questa implementazione [di](https://github.com/adobe/commerce-cif-graphql-integration-reference)riferimento. Per le soluzioni non di Magento, AEM sarebbe configurato per puntare all&#39;endpoint I/O Runtime.

La piattaforma I/O Runtime può essere utilizzata anche per estendere o personalizzare i servizi di e-commerce. Per questi casi d’uso si chiama l’endpoint I/O Runtime che ospiterà un’implementazione personalizzata del rispettivo servizio. I casi di utilizzo di integrazione e estensione possono essere combinati.

## 3. È possibile memorizzare le risorse di prodotto (immagini) e farvi riferimento da AEM tramite l&#39;amministratore di Magento? Come possono essere utilizzate le risorse di Dynamic Media?

Attualmente non esiste un&#39;integrazione AEM Assets - Magento. Come soluzione alternativa, potete memorizzare le risorse di prodotto (immagini) in AEM Assets, ma dovrete memorizzare manualmente gli URL delle risorse nel Magento. Dynamic Media ora fa parte dei AEM Assets e funzionerà allo stesso modo.

## 4. È importante dove viene distribuito il Magento? (Premuto o nel cloud)

Non importa dove viene distribuito il Magento. L&#39;integrazione e la nuova facciata AEM Venia Store funzioneranno indipendentemente dal modello di implementazione. Tuttavia, se viene distribuito in base all&#39;architettura di riferimento E2E approvata, i test E2E verranno eseguiti in base ai KPI delle prestazioni raccolti che rappresentano il profilo di un cliente aziendale. Questo vi fornirà informazioni aggiuntive che potete usare come benchmark.

## 5. In che modo vengono create le pagine di catalogo o di prodotto in AEM? Come persistono in AEM?

Le pagine di catalogo e di prodotto vengono create e memorizzate nella cache in AEM in base a modelli di catalogo e di pagina di prodotto generici. Nessun dato prodotto o catalogo viene importato e memorizzato in AEM.

## 6. È inoltre possibile memorizzare nella cache i prezzi e altri dati tramite Dispatcher. Ciò solleva un problema frequente di annullamento della validità della cache?

I dati dinamici come prezzo o scorte non vengono memorizzati nella cache dell&#39;Dispatcher. I dati dinamici vengono recuperati lato client con i componenti Web direttamente tramite le API GraphQL. Solo i dati statici (come i dati di prodotto o categoria) vengono memorizzati nella cache sull&#39;Dispatcher. Se i dati del prodotto cambiano, sarà necessario annullare la validità della cache.

## 7. Come funziona l&#39;annullamento della validità cache per AEM Dispatcher con AEM-Magento?

È consigliabile impostare l&#39;annullamento della validità della cache basata su TTL per le pagine memorizzate nella cache dell&#39;Dispatcher. Per informazioni dinamiche come prezzo o stock, si consiglia di eseguire il rendering della data lato client. Per ulteriori informazioni sull&#39;annullamento della validità della cache basata su TTL, fare riferimento a [AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 8. Perché non utilizzi We.Retail?

Il tema Venia (sviluppato dal Magento) viene utilizzato, che è mobile prima e allineato con il PWA Magento. Il tema Venia rappresenta l&#39;ultima versione in termini di stile CSS e componenti AEM core.

## 9. Quando aggiornate i dati del prodotto nel Magento, è un push in tempo reale a AEM? O è un processo batch?

Il componente aggiuntivo CIF utilizzato con AEM Cloud Service consente il flusso dei dati da Magenti a AEM on-demand. Di conseguenza, non si tratta di un processo push o batch in tempo reale quando è presente un aggiornamento nel Magento.

## 10. Esiste una raccomandazione sulla ricerca unificata tra AEM contenuto con Commerce?

Viene fornita un’implementazione di riferimento per la ricerca di prodotti, ma non viene eseguita alcuna ricerca unificata con il contenuto. Questa funzione è in genere molto specifica per i clienti e meglio risolta a livello di progetto.

## 11. Come funziona la ricerca con AEM-Magento utilizzando CIF?

CIF fornisce la barra di ricerca e i componenti Risultati ricerca. Il componente Barra di ricerca invia una richiesta GraphQL con il termine di ricerca al Magento. Magento restituisce un elenco di prodotti che include nome prodotto, prezzo, SLUG, ecc. Il componente Risultato della ricerca visualizza quindi i risultati della ricerca in una visualizzazione galleria su una pagina di risultati della ricerca creata in AEM. La ricerca supporta la ricerca di base full-text. Utilizziamo la chiave SLUG/url per creare un riferimento al PDP.

## 11. Come possono essere utilizzati i dati del prodotto in MSM o nelle traduzioni?

I dati del prodotto sono generalmente già tradotti in PIM o in Magento. L&#39;integrazione AEM - Magento supporta la connessione a più store Magenti e viste store. In una configurazione MSM, in genere, un sito AEM è collegato a una visualizzazione dell&#39;archivio di Magenti.

## 13. Come funziona CIF con altre piattaforme commerciali?

L&#39;integrazione con soluzioni di terze parti, come altre soluzioni di commercio (non di Magento) viene realizzata tramite la piattaforma I/O Runtime.  Abbiamo creato un&#39;implementazione [di](https://github.com/adobe/commerce-cif-graphql-integration-reference) riferimento per dimostrare come ciò avviene. Questo consente di riutilizzare il connettore [CIF](https://github.com/adobe/commerce-cif-connector) AEM cloud e i componenti [core](https://github.com/adobe/aem-core-cif-components) AEM CIF esponendo l&#39;API GraphQL Magento su qualsiasi piattaforma di e-commerce di terze parti. Per offrire la massima flessibilità e scalabilità, questo livello di integrazione è implementato sulla piattaforma [](https://www.adobe.io/apis/experienceplatform/runtime.html)Adobe I/O Runtime senza server.

## 14. Esiste un modo per migliorare i dati del prodotto con testo commerciale? Dove fai questo? In AEM o in Magento?

Ci sono diversi modi per ottenere questo e dipenderà dal caso d&#39;uso. Un modo potrebbe essere quello di lavorare con gli attributi personalizzati. Consentire AEM autori di modificare questi campi nell&#39;editor di prodotti di AEM e sincronizzare nuovamente i dati al PIM. Un&#39;altra opzione consiste nell&#39;utilizzare AEM frammenti esperienza che vengono inseriti nelle pagine del prodotto.

## 15. L&#39;integrazione tra AEM-Magento cambia quando si utilizza la piattaforma Adobe I/O Runtime?

I clienti che desiderano estendere i servizi di commercio possono utilizzare le stesse sequenze di azioni di integrazione e scrittura ospitate sulla piattaforma Runtime I/O per inserire logica di business e arricchire i servizi di commercio.

## 16. Poiché AEM creare in modo dinamico pagine di prodotti e cataloghi basate su un modello generico in AEM, cosa posso vedere se devo aprire CRXDE Lite e controllare sotto contenuto? Vedrei un intero albero di prodotti basato sui prodotti in Magento? In caso negativo, in che modo un autore potrebbe migliorare tali pagine?

Non esistono più pagine di catalogo JCR o di prodotti. Cfr. domanda 12.

## 17. Il front store SPA lavorerà con AEM editor SPA?

AEM può essere utilizzato come strumento di authoring per qualsiasi tipo di negozio anteriore. Attualmente, il rendering ibrido viene utilizzato per il nuovo negozio anteriore. In futuro, AEM sarà utilizzato per l’authoring con SPA e PWA.

## 18. In che modo il PIM gioca in questa struttura?

I dati PIM vengono esposti a AEM e client tramite le richieste GraphQL. La nostra raccomandazione è di integrare PIM con il motore di commercio (Magento o altro) in modo che i dati PIM possano essere recuperati dal motore di commercio.

## 19. Come possiamo garantire la conformità PCI quando si utilizzano AEM per l&#39;intero livello di presentazione?

Quando si utilizzano AEM sulla distribuzione di AMS e cloud di Magenti, è obbligatorio utilizzare metodi di pagamento astratti. In questo modo, il client del browser viene messo in comunicazione diretta con il provider del gateway di pagamento, in modo che né  Adobe né i cloud di Magento contengano o trasmettano i dati del titolare della carta. Questo approccio fornisce una copertura per la conformità PCI per gli stack tecnologici e i centri dati. Tuttavia, vi sono altri elementi da considerare pienamente conformi allo standard PCI, come il modo in cui i dipendenti interagiscono con il sistema e i dati. Per ulteriori informazioni sulla conformità Magento PCI, fare riferimento a https://magento.com/pci-compliance

## 20. Come posso richiedere una licenza di prova I/O Runtime?

È possibile richiedere una licenza di prova per utilizzare I/O Runtime [qui](https://github.com/AdobeDocs/adobeio-runtime/blob/master/overview/request_a_trial.md).



