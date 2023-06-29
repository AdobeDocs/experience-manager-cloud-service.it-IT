---
title: Domande frequenti sull’integrazione AEM-Commerce tramite Commerce Integration Framework
description: Domande frequenti sull’integrazione AEM-Commerce tramite Commerce Integration Framework
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 29%

---

# Domande frequenti sull’integrazione AEM-Commerce tramite Commerce Integration Framework

## 1. CIF GraphQL è utilizzato solo per il commercio o sarà disponibile per eseguire query sui contenuti creati con AEM JCR?

Adobe ha adottato le API GraphQL di Adobe Commerce come API Commerce ufficiale per tutti i dati relativi al commercio. Pertanto, l’AEM utilizza GraphQL per scambiare dati di e-commerce con Adobe Commerce e con qualsiasi motore di e-commerce tramite I/O Runtime. Questa API GraphQL è indipendente dall’API GraphQL dell’AEM per accedere ai frammenti di contenuto.

## 2. È possibile memorizzare le risorse dei prodotti (immagini) e farvi riferimento dall’AEM tramite l’amministratore Adobe Commerce? Come possono essere utilizzate le risorse da Dynamic Media?

Non è disponibile alcuna integrazione ufficiale AEM Assets - Adobe Commerce. È disponibile un connettore per i partner su [marketplace](https://marketplace.magento.com) <!-- THIS IS THE OLD URL THAT WAS USED. IT WAS 404 (https://marketplace.magento.com/bounteous-dam.html) -->

Oppure, come soluzione alternativa, puoi memorizzare le risorse dei prodotti (immagini) in AEM Assets, ma devi memorizzare manualmente gli URL delle risorse in Adobe Commerce. Dynamic Media ora fa parte di AEM Assets e funziona allo stesso modo.

## 3. Importa dove viene implementata la soluzione commerce? on-premise o nel cloud?

No, non importa dove viene distribuita la soluzione commerce. CIF e la vetrina AEM funzionano indipendentemente dal modello di distribuzione. Tuttavia, se la soluzione viene implementata con l’architettura di riferimento E2E consigliata, i test E2E possono essere eseguiti in base a KPI delle prestazioni che rappresentano un tipico profilo cliente aziendale. Questo metodo fornisce informazioni aggiuntive che possono essere utilizzate come benchmark.

## 4. In che modo vengono create le pagine di catalogo o di prodotto in AEM? Come persistono in AEM?

Le pagine di catalogo e di prodotto vengono create e memorizzate nella cache in AEM in base a modelli generici per pagine di catalogo e di prodotto. Nessun dato di prodotto o catalogo viene importato e memorizzato in AEM.

## 5. Quando aggiorni i dati di prodotto nella tua soluzione commerce, si tratta di un push in tempo reale all’AEM? oppure si tratta di un processo batch?

Il componente aggiuntivo CIF utilizzato con AEM Cloud Service consente il flusso di dati dalla soluzione commerce all’AEM on-demand. Pertanto, non si tratta di un processo push in tempo reale o batch quando è presente un aggiornamento nella soluzione commerce.

## 6. Quali sono le dimensioni del catalogo supportate dall’AEM con CIF?

Questo dipende da alcuni aspetti aggiuntivi che devi considerare. Qual è il rapporto di cache dei dati e delle pagine del catalogo? Quante richieste simultanee prevedi durante le ore di punta? Quanto sono scalabili le API delle soluzioni commerce?

## 7. Che ruolo svolge un sistema PIM in questo framework?

I dati di un sistema PIM (Product Information Management, gestione delle informazioni dei prodotti) vengono esposti ad AEM e ai client tramite le richieste GraphQL. Consigliamo di integrare un sistema PIM con il motore di e-commerce (Adobe Commerce o altri) in modo che i dati PIM possano essere recuperati dal motore di e-commerce.

## 8. È possibile memorizzare nella cache anche i prezzi e altri dati tramite Dispatcher? Questo potrebbe comportare problemi di invalidazione frequente della cache?

I dati dinamici come prezzo o inventario non vengono memorizzati nella cache di Dispatcher. I dati dinamici vengono recuperati lato client con i componenti Web direttamente tramite le API GraphQL. Nella cache di Dispatcher vengono memorizzati solo i dati statici (come i dati di prodotto o categoria). Se i dati del prodotto cambiano, è necessario annullare la validità della cache.

## 9. Come funziona l’invalidazione della cache per il Dispatcher AEM con l’AEM e il Commerce?

È consigliabile impostare l’invalidazione della cache basata su TTL per le pagine memorizzate nella cache di Dispatcher. Per informazioni dinamiche come prezzo o azioni, si consiglia di eseguire il rendering dei dati lato client. Per ulteriori informazioni sull’invalidazione della cache basata su TTL, consulta [Ottimizzazione della cache di Dispatcher](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=it) e [Ottimizzazione delle prestazioni AEM](https://experienceleague.adobe.com/docs/commerce-operations/deliver-commerce-at-scale/performance.html).

## 10. Vi sono consigli sulla ricerca unificata nei contenuti AEM con Commerce?

Viene fornita un’implementazione di riferimento per la ricerca di prodotti, ma non viene eseguita alcuna ricerca unificata con i contenuti. Questa funzione è specifica per il cliente e può essere risolta meglio a livello di progetto.

## 11. Come funziona la ricerca con l’AEM e il commercio utilizzando CIF?

CIF fornisce i componenti Barra di ricerca e Risultati di ricerca. Il componente Barra di ricerca invia una richiesta GraphQL con il termine di ricerca alla soluzione commerce, che restituisce un elenco di prodotti che include nome del prodotto, prezzo, SLUG e così via. Il componente Risultato di ricerca visualizza quindi i risultati della ricerca in una visualizzazione a galleria su una pagina di risultati di ricerca creata su AEM. Il componente Ricerca supporta la ricerca full-text. Utilizziamo la chiave SLUG/url per creare un riferimento al PDP.

## 12. Come possono essere utilizzati i dati di prodotto in MSM o nelle traduzioni?

I dati del prodotto sono già tradotti in PIM o in Adobe Commerce. L’integrazione AEM - Adobe Commerce supporta la connessione a più store e viste store di Adobe Commerce. In una configurazione MSM, in genere un sito AEM è collegato a una vista store di Adobe Commerce.

## 13. Esiste un modo per migliorare i dati di prodotto con testo commerciale? Dove si effettua questa procedura? In AEM o nella soluzione Commerce?

Consigliamo di gestire i dati e i contenuti di marketing in AEM. Decora i dati di prodotto dalla soluzione commerce con attributi aggiuntivi utilizzando Frammenti di contenuto oppure crea e collega frammenti di esperienza per contenuti non strutturati con i tuoi prodotti.

## 14. Come possiamo garantire la conformità PCI quando si utilizza AEM per l’intero livello di presentazione?

Si consiglia di utilizzare metodi di pagamento astratti. Questo mette il client browser in comunicazione diretta con il provider del gateway dei pagamenti in modo che né l&#39;Adobe né le soluzioni commerce conservino o trasmettano i dati del titolare della carta. Questo approccio richiede solo una conformità PCI di livello 3. Tuttavia, ci sono altri aspetti da considerare per essere pienamente conformi allo standard PCI, come il modo in cui i dipendenti interagiscono con il sistema e i dati. Per ulteriori informazioni sulla conformità PCI di Adobe Commerce, consulta [Requisiti di conformità PCI](https://business.adobe.com/products/magento/pci-compliance.html).

## 15. Se utilizzo le versioni cloud AEM e Adobe Commerce, questa soluzione congiunta è compatibile con PCI?

Sì, il questionario di autovalutazione D e l&#39;attestato di conformità sono disponibili su richiesta.

## 16. Come posso richiedere una licenza di prova di I/O Runtime?

Per richiedere una licenza di prova per utilizzare I/O Runtime, visita [questa pagina](https://developer.adobe.com/app-builder/trial/).
