---
title: 'AEM: Domande frequenti sull’integrazione con Commerce tramite Commerce Integration Framework'
description: 'AEM: Domande frequenti sull’integrazione con Commerce tramite Commerce Integration Framework'
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
feature: Commerce Integration Framework
role: Admin, Developer, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 97%

---


# AEM: Domande frequenti sull’integrazione con Commerce tramite Commerce Integration Framework

## &#x200B;1. CIF GraphQL è utilizzato solo per Commerce o sarà disponibile per eseguire query sui contenuti creati con JCR di AEM? {#faq-1}

Adobe ha adottato le API GraphQL di Adobe Commerce come API Commerce ufficiali per tutti i dati relativi all’e-commerce. Quindi, AEM utilizza GraphQL per scambiare dati di e-commerce con Adobe Commerce e con qualsiasi motore di e-commerce tramite I/O Runtime. Questa API GraphQL è indipendente dall’API GraphQL di AEM per accedere ai frammenti di contenuto.

## &#x200B;2. È possibile memorizzare le risorse dei prodotti (immagini) e farvi riferimento da AEM tramite le funzioni di amministrazione di Adobe Commerce? Come possono essere utilizzate le risorse da Dynamic Media? {#faq-2}

Non è disponibile alcuna integrazione ufficiale tra AEM Assets - Adobe Commerce. Connettore partner disponibile nel [marketplace.](https://commercemarketplace.adobe.com)

Come soluzione alternativa, è possibile archiviare le risorse dei prodotti (immagini) in AEM Assets, ma occorre memorizzare manualmente gli URL delle risorse in Adobe Commerce. Dynamic Media fa ora parte di AEM Assets e funziona nello stesso modo.

## &#x200B;3. Ha importanza dove viene implementata la soluzione per l’e-commerce? (on-premise o nel cloud) {#faq-3}

No, non ha importanza dove viene implementata la soluzione per l’e-commerce. CIF e il progetto di vetrina digitale di AEM funzionano indipendentemente dal modello di implementazione. Tuttavia, se la soluzione viene implementata con l’architettura di riferimento E2E consigliata, i test E2E possono essere eseguiti in base ai KPI delle prestazioni che rappresentano un tipico profilo cliente di un’azienda. Questo metodo fornisce informazioni aggiuntive che possono essere utilizzate come benchmark.

## &#x200B;4. In che modo vengono create le pagine di catalogo o di prodotto in AEM? Come persistono in AEM? {#faq-4}

Le pagine di catalogo e di prodotto vengono create e memorizzate nella cache in AEM in base a modelli generici per pagine di catalogo e di prodotto. Nessun dato di prodotto o catalogo viene importato e memorizzato in AEM.

## &#x200B;5. Quando si aggiornano i dati di prodotti nella soluzione per l’e-commerce, questi vengono trasmessi in tempo reale ad AEM? Oppure si tratta di un’elaborazione in batch? {#faq-5}

Grazie al componente aggiuntivo CIF utilizzato con AEM Cloud Service, il flusso di dati dalla soluzione per l’e-commerce ad AEM avviene on-demand. Di conseguenza, un aggiornamento nella soluzione per l’e-commerce non comporta alcun processo push in tempo reale o batch.

## &#x200B;6. Quali sono le dimensioni del catalogo supportate da AEM con CIF? {#faq-6}

Questo dipende da alcuni aspetti aggiuntivi che devono essere presi in considerazione. Qual è il rapporto di cache dei dati e delle pagine del catalogo? Quante richieste simultanee prevedi durante le ore di punta? Quanto sono scalabili le API delle soluzioni per l’e-commerce?

## &#x200B;7. Che ruolo svolge un sistema PIM in questo framework? {#faq-7}

I dati di un sistema PIM (Product Information Management, gestione delle informazioni dei prodotti) vengono esposti ad AEM e ai client tramite le richieste GraphQL. Consigliamo di integrare il PIM con il motore di e-commerce (Adobe Commerce o altri) in modo che i dati PIM possano essere recuperati dal motore di e-commerce.

## &#x200B;8. È possibile memorizzare nella cache anche i prezzi e altri dati tramite Dispatcher? Questo potrebbe comportare problemi di invalidazione frequente della cache? {#faq-8}

I dati dinamici come prezzo o inventario non vengono memorizzati nella cache di Dispatcher. I dati dinamici vengono recuperati lato client con i componenti Web direttamente tramite le API GraphQL. Nella cache di Dispatcher vengono memorizzati solo i dati statici (come i dati di prodotto o categoria). Se i dati di prodotto cambiano, è necessario invalidare la cache.

## &#x200B;9. Come funziona l’annullamento della validità della cache per il Dispatcher AEM con AEM e Commerce? {#faq-9}

Adobe consiglia di impostare l’annullamento della validità della cache basata su TTL per le pagine memorizzate nella cache di Dispatcher. Per informazioni dinamiche come prezzo o inventario, Adobe consiglia di eseguire il rendering dei dati lato client. Per ulteriori informazioni sull’annullamento della validità della cache basata su TTL, consulta [Ottimizzazione della cache di Dispatcher.](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=it)

## &#x200B;10. Vi sono consigli sulla ricerca unificata nei contenuti AEM con Commerce? {#faq-10}

Viene fornita un’implementazione di riferimento per la ricerca di prodotti, ma non viene eseguita alcuna ricerca unificata con i contenuti. Questa funzione è specifica per il cliente e può essere risolta meglio a livello di progetto.

## &#x200B;11. Come funziona la ricerca con AEM e Commerce utilizzando CIF? {#faq-11}

CIF fornisce i componenti Barra di ricerca e Risultati di ricerca. Il componente Barra di ricerca invia una richiesta GraphQL con il termine di ricerca alla soluzione per l’e-commerce, che restituisce un elenco di prodotti che include nome del prodotto, prezzo, SLUG e così via. Il componente Risultato di ricerca visualizza quindi i risultati della ricerca in una visualizzazione a galleria su una pagina di risultati di ricerca creata su AEM. Il componente Ricerca supporta la ricerca full-text. Utilizziamo la chiave SLUG/url per creare un riferimento al PDP.

## &#x200B;12. Come possono essere utilizzati i dati di prodotto in MSM o nelle traduzioni? {#faq-12}

I dati del prodotto sono generalmente già tradotti in PIM o in Adobe Commerce. L’integrazione AEM - Adobe Commerce supporta la connessione a più store e viste store di Adobe Commerce. In genere, in una configurazione MSM un sito AEM è collegato a una vista store di Adobe Commerce.

## &#x200B;13. Esiste un modo per migliorare i dati di prodotto con testo commerciale? Dove si effettua questa procedura? In AEM o nella soluzione per l’e-commerce? {#faq-13}

Adobe consiglia di gestire i dati e i contenuti di marketing in AEM. Arricchisci i dati di prodotto dalla soluzione per l’e-commerce con attributi aggiuntivi utilizzando Frammenti di contenuto oppure crea e collega Frammenti di esperienza per contenuti non strutturati con i tuoi prodotti.

## &#x200B;14. Come è possibile garantire la conformità PCI quando si utilizza AEM per l’intero livello di presentazione? {#faq-14}

Adobe consiglia di utilizzare metodi di pagamento astratti. In tal modo il client browser comunica direttamente con il provider del gateway dei pagamenti e i dati sensibili dei titolari della carta non vengono trasmessi né memorizzati in Adobe né nelle soluzioni per l’e-commerce. Questo approccio richiede solo una conformità PCI di livello 3. Tuttavia, vi sono altri elementi da considerare per assicurare la piena conformità allo standard PCI, come il modo in cui i dipendenti interagiscono con il sistema e i dati. Per ulteriori informazioni sulla conformità PCI di Adobe Commerce, vedere [Requisiti di conformità PCI.](https://business.adobe.com/it/products/magento/pci-compliance.html)

## &#x200B;15. Se vengono utilizzate le versioni AEM e Adobe Commerce Cloud, questa soluzione congiunta è conforme allo standard PCI? {#faq-15}

Sì, il questionario di autovalutazione D e l’attestato di conformità sono disponibili su richiesta.

## &#x200B;16. Come è possibile richiedere una licenza di prova di I/O Runtime? {#faq-16}

Per informazioni dettagliate sulla richiesta di una licenza di prova per l’utilizzo di I/O Runtime, consulta [Ottenere l’accesso](https://developer.adobe.com/runtime/docs/guides/overview/getting_access/).
