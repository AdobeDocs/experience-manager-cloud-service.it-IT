---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 080a79cdc0e48a54570ea53618b1f0be164d5156
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 99%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 21331 {#21331}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 21331, rilasciata pubblicamente il 24 giugno 2025. La versione di manutenzione precedente era la 21193.

Con la versione di attivazione funzioni 2025.7.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-21331}

* CQ-4356522: ottimizzazione di `WorkflowResourceStatusProvider`.
* FORMS-16458: interfaccia utente per la scelta delle proprietà dei font (caratteri).
* FORMS-17707: il connettore AEP non funziona per le fasi della piattaforma AEP.
* FORMS-19125: supporto alla mappatura automatica dei frammenti nell’editor dei moduli adattivi (AF).
* FORMS-19336: ricerca aggiunta nella struttura di origine dei dati nell’editor dei moduli adattivi (AF).
* FORMS-19417: supporto di pulsanti di scelta nella vista Gerarchia.
* FORMS-19603: supporto alla pagina mastro e a quella di progettazione nell’editor di regole.
* SITES-5358: API REST per frammenti di contenuto: copia di frammenti di contenuto (CF) con elementi figlio.
* SITES-10575: “MSM: caricatore di filtri Bloom nella Blueprint” (Blueprint Bloomfilter Loader) tenta di caricare più di 100.000 righe.
* SITES-14542: la ridenominazione o lo spostamento di una pagina di origine Live Copy deve attivare la pubblicazione della pagina Live Copy rinominata/spostata nel caso in cui sia stata precedentemente pubblicata.
* SITES-19754: Edge Delivery con l’editor universale: aggiungi un messaggio di errore leggibile quando l’integrazione presenta problemi.
* SITES-23499: Edge Delivery con l’editor universale: aggiungi l’utilizzo di un supporto per più campi per le opzioni di blocco.
* SITES-23518: Edge Delivery con l’editor universale: aggiungi supporto a rappresentazioni di risorse specifiche Edge Delivery.
* SITES-24436: API REST per frammenti di contenuto: è stata introdotta la cache locale per velocizzare il recupero di riferimenti duplicati.
* SITES-25155: API REST per frammenti di contenuto: rimozione del parametro di query “enabledForFolder” obsoleto dall’elenco Modelli.
* SITES-25913: API REST di frammenti di contenuto: convalida delle risorse in base al tempo prima di avviare il flusso di lavoro di pubblicazione.
* SITES-25976: i collegamenti all’interno dei frammenti esperienza non si adattano dopo il rollout di MSM.
* SITES-26271: API REST di frammenti di contenuto: passa a BFS Traversal per l’endpoint di variante GET.
* SITES-27486: editor universale - Integrazione di AEM.
* SITES-27775: ricerca di riferimento ottimizzata durante la pubblicazione (caricamento lento dei metadati).
* SITES-27782: Edge Delivery con l’editor universale: aggiungi un’implementazione specifica dell’editore abbonato per pubblicare contenuti su Edge Delivery (accesso anticipato).
* SITES-27792: Edge Delivery con l’editor universale: aggiungi un modello di configurazione di Edge Delivery Services dedicato.
* SITES-28557: API REST per frammenti di contenuto: consente l’utilizzo di ETag recuperati chiamando `/cf/fragments/{fragmentId}` con `references=direct` per applicare una patch a un frammento di contenuto.
* SITES-28683: ricerche MSM LiveRelationship con possibilità di ignorare lo stato avanzato.
* SITES-29601: API REST per frammenti di contenuto: convalida dei riferimenti ai frammenti di contenuto dei campi di testo lunghi.
* SITES-29614: API REST per frammenti di contenuto: recupera un flusso di lavoro utilizzando l’endpoint `/cf/workflows/{workflowInstanceId}`, dove workflowInstanceIda è l’ID restituito dalla richiesta di pubblicazione.
* SITES-29615: API REST per frammenti di contenuto: elenca tutte le richieste batch create tramite POST `/cf/batch` utilizzando `GET /cf/batch`.
* SITES-29874: API REST per frammenti di contenuto: i riferimenti da campi di testo lunghi di frammenti di contenuto ora vengono recuperati e idratati.
* SITES-29930: API REST di frammenti di contenuto: aggiungi metriche per il flusso di lavoro Pubblicazione dei frammenti di contenuto.
* SITES-29986: API REST di frammenti di contenuto: supporto alla denominazione tecnica del modello CF.
* SITES-30088: API REST di frammenti di contenuto: Pubblicazione CF: ignora il recupero di riferimenti quando filterReferencesByStatus è vuoto.
* SITES-30126: API REST per frammenti di contenuto: miglioramento delle prestazioni per la pubblicazione dei frammenti di contenuto: è stato sostituito il controllo se una risorsa è un frammento con un controllo minimo.
* SITES-30328: Edge Delivery con l’editor universale: aggiungi supporto all’anteprima dalla barra laterale.
* SITES-30445: API REST di frammenti di contenuto: schema dell’interfaccia utente del modello CF: aggiungi un’opzione per controllare lo stato iniziale del file comprimibile.
* SITES-30604: API REST di frammenti di contenuto: supporto all’adozione dello schema metadati del modello nella nuova interfaccia utente.
* SITES-30885: elaborazione JSON ottimizzata nelle query persistenti.
* SITES-30886: API REST di frammenti di contenuto: flussi di lavoro GET per l’endpoint dei frammenti di contenuto basati sugli UID dei frammenti memorizzati nei metadati del flusso di lavoro.
* SITES-31005: l’interfaccia utente del processo di rollout è stata migliorata per mostrarne l’avanzamento.
* SITES-31020: l’interfaccia utente del processo Crea Live Copy è stata migliorata per mostrarne l’avanzamento.
* SITES-31111: API REST per frammenti di contenuto: consente all’API della patch di variante di accettare riferimenti ai frammenti di contenuto all’interno dei lanci di frammenti di contenuto.
* SITES-31343: API REST per frammenti di contenuto: sono stati aggiunti filtro e impaginazione per data all’endpoint che elenca le richieste batch.
* SITES-31472: l’utilizzo di Elimina lancio per un lancio di grandi dimensioni può causare la sospensione dell’archivio.
* SITES-31641: API REST per frammenti di contenuto: è stata aggiunta una proprietà ai campi modello per memorizzare le mappe dinamiche relative alle estensioni.
* SITES-31677: l’area di lavoro personalizzata supporta l’esportazione dei frammenti di contenuto di AEM in Target.
* SITES-31770: API REST per frammenti di contenuto: miglioramenti delle prestazioni di PATCH.
* SITES-31782: API REST di frammenti di contenuto: aggiungi una descrizione per le risorse locali.
* SITES-32175: consenti impegni intermediari sia per la creazione di Live Copy che per il rollout di pagine MSM.

### Problemi risolti {#fixed-issues-21331}

* CQ-4359756: le regole di traduzione ora includono le proprietà del filtro a livello di componente.
* CQ-4359826: è stato risolto uno stato incoerente nel pannello dei riferimenti dei frammenti di contenuto.
* CQ-4359866: la classe LanguageUtils ora supporta test unitari senza aggiungere ulteriori dipendenze.
* FORMS-13990: API servizio Forms: generazione documenti: il campo dati, se lasciato vuoto dopo la selezione, restituisce 200 quando è previsto un 400.
* FORMS-14309: API servizio Forms: rettifica del codice di risposta per l’estrazione dei dati.
* FORMS-18526: quando viene copiata una regola con più campi nelle condizioni, il campo fisso non cambia.
* FORMS-18977: il servizio DOR non trasmette il titolo del documento.
* FORMS-19047: traduzioni mancanti dopo la pubblicazione di un modulo adattivo su AEM Forms su SP22.
* FORMS-19234: impossibile utilizzare la funzione timeline dei PDF in AM Forms.
* FORMS-19628: nel DOR generato automaticamente, escludendo il titolo del pannello nidificato viene nascosto anche il titolo del pannello principale.
* FORMS-19651: correzione della regola per cui un pulsante su cui si fa clic viene utilizzato in condizioni binarie e questo stesso viene utilizzato nell’istruzione then.
* FORMS-19808: FormsPortal: non è possibile estrarre le bozze quando è abilitato il caricamento lento.
* FORMS-19887: la proprietà Access non funziona nell’anteprima di HTML5.
* SITES-15452: gli elementi di frammenti di contenuto univoci non devono essere verificati rispetto alle relative copie nel lancio.
* SITES-24492: ARIA tablist non ha un nome accessibile.
* SITES-24623: API REST di frammenti di contenuto: correzione della mancata corrispondenza ETag tra gli endpoint per lo stesso frammento di contenuto.
* SITES-24668: la funzionalità della barra dei riferimenti viene interrotta aumentando lo zoom al 400%.
* SITES-24678: il messaggio di stato della barra dei riferimenti non viene annunciato dall’assistente vocale.
* SITES-24697: lo stato di caricamento del modello di immagine non viene annunciato dall’assistente vocale.
* SITES-24708: la funzionalità della barra dei filtri viene interrotta aumentando lo zoom al 400%.
* SITES-25235: il messaggio di caricamento del contenuto della barra dei filtri non viene annunciato dall’assistente vocale.
* SITES-25254: la barra di scorrimento orizzontale viene visualizzata nel modale Carosello quando il contenuto viene visualizzato a 320 px.
* SITES-25433: Edge Delivery con Editor universale: correzione del rendering delle versioni di pagina per strutture di siti multilingue.
* SITES-26064: API REST per frammenti di contenuto: è stato corretto il codice di stato restituito durante la creazione di un frammento e la ricezione di un `AccessDeniedException` nel backend.
* SITES-26890: quando viene utilizzata la tastiera, il focus tastiera dell’ambito “Intestazioni tabella” non è visibile nella pagina Gestione Pubblicazione.
* SITES-29075: la panoramica della Live Copy non funziona per i siti web con volumi elevati.
* SITES-29514: Edge Delivery con Editor universale: rende obbligatorio l’URL di GitHub/progetto durante la creazione di un nuovo sito.
* SITES-29691: impossibile spostare la pagina in un caso specifico relativo ai lanci.
* SITES-29745: API REST di frammenti di contenuto: implementazione dell’idratazione delle varianti di riferimento in BFS Traversal.
* SITES-29748: correzione delle condizioni di rendering per visualizzare le azioni Gestisci pubblicazione e Pubblicazione rapida nell’editor dei frammenti di contenuto.
* SITES-29789: problema di modifica del collegamento del componente nelle pagine principali copiate.
* SITES-29987: API REST di frammenti di contenuto: Crea e modifica modello per frammenti di contenuto non supporta `previewUrlPattern`.
* SITES-30140: problema relativo alla finestra doppia durante la creazione del riferimento a un frammento di contenuto.
* SITES-30327: API REST di frammenti di contenuto: la pubblicazione di frammenti di contenuto senza autorizzazioni crea flussi di lavoro separati per ogni risorsa del payload.
* SITES-30333: lettura dei metadati delle risorse da JCR per evitare problemi di analisi XMP.
* SITES-30353: GraphQL DataFetchingExceptions per il campo “src” nei frammenti di contenuto di AEM.
* SITES-30377: Edge Delivery con Editor universale: pulizia dei nomi di sito e organizzazione.
* SITES-30386: Edge Delivery con Editor universale: rimuovere duplicato, UE legacy `cors.js`.
* SITES-30583: API REST di frammenti di contenuto: lo strumento Trova e sostituisci cambia tutti i caratteri in minuscolo.
* SITES-30585: API REST di frammenti di contenuto: `previewUrlPattern` non impostata durante la creazione di CFM con riferimenti.
* SITES-30634: Testo e allineamento alternativo immagine nell’Editor Rich Text non funzionano in modo coerente.
* SITES-30660: problema di conformità ADA con il componente AEM personalizzato.
* SITES-30695: Edge Delivery con Editor universale: aumento della classificazione della pipeline di riscrittura per non interferire con il codice personalizzato.
* SITES-30727: impossibile trascinare componenti nell’editor di authoring di produzione.
* SITES-30752: non vengono utilizzate le intestazioni `If-modified-since`/`last-modified` durante la generazione della risposta a una query persistente.
* SITES-30871: il DOM viene aggiornato dopo l’attivazione del listener afteredit.
* SITES-30877: stato di rollout della pagina secondaria non corretto.
* SITES-30899: l’opzione di rollout “Più tardi” consente di continuare senza selezionare alcuna data.
* SITES-30947: eccezione Null Pointer a causa di una proprietà “behavior” mancante sulla blueprint durante il rollout.
* SITES-31157: API REST di frammenti di contenuto: la patch Non riesce è un caso specifico.
* SITES-31162: API REST per frammenti di contenuto: è stato risolto un problema di casting per il campo `DateTimeField` in `ModelFieldMapper`.
* SITES-31174: API REST per frammenti di contenuto: i tag non sono stati pubblicati insieme alla richiesta di pubblicazione.
* SITES-31272: impossibile creare la copia per lingua di Assets tramite PageManager.copy.
* SITES-31327: API REST di frammenti di contenuto: rimuovi la convalida ETag nella richiesta del frammento GET.
* SITES-31387: errore di JavaScript “ns.ui.alert non è una funzione” durante la riattivazione dell’ereditarietà del componente fantasma.
* SITES-31454: API REST per frammenti di contenuto: allenta i pattern per i campi di riferimento dei frammenti per accettare anche gli UUID.
* SITES-31455: API REST di frammenti di contenuto: correggi la mancata corrispondenza di ETag tra gli endpoint per lo stesso modello per frammenti di contenuto.
* SITES-31459: API REST di frammenti di contenuto: non è possibile modificare la Live Copy dei frammenti di contenuto (CF) quando è presente un campo di riferimento al contenuto.
* SITES-31467: js-errors da contexthub.authoring-hook.js nell’editor pagina.
* SITES-31487: API REST per frammenti di contenuto: consente la chiamata dell’endpoint delle autorizzazioni per la cartella principale.
* SITES-31621: Edge Delivery con l’editor universale: rimuovi una riga vuota dai fogli di calcolo che sono Live Copy.
* SITES-31676: quando si creano o si eliminano componenti, nella parte inferiore della pagina rimane uno spazio vuoto.
* SITES-31822: etichetta della casella di controllo ClassicUI mancante e HTML codificato.
* SITES-31857: la creazione di frammenti di contenuto (CF) non riesce nelle cartelle con apici.
* SITES-31888: l’eliminazione dei frammenti di contenuto non si propaga all’anteprima.
* SITES-31922: API REST di frammenti di contenuto: i riferimenti di pagina non vengono restituiti dall’endpoint referencedBy.
* SITES-31987: non mostrare gli URL di anteprima per i frammenti di contenuto durante la pubblicazione in anteprima.
* SITES-32095: l’aggiornamento automatico non riesce nel listener di evento afterchilddelete in Live Copy.
* SITES-32237: Edge Delivery con l’editor universale: corregge il rendering di componenti di testo vuoti/non corretti.

### Problemi noti {#known-issues-21331}

* SITES-33177: Gli stili di sezione memorizzati come stringhe separate da virgola sono interrotti.

### Funzioni e API obsolete {#deprecated-21331}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-21331}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 21 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-21331}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
