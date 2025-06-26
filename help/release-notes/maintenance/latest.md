---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 467e21aff1c2164be729598d03f30f6a9e90c8aa
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 16%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 21331 {#21331}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 21331, rilasciata pubblicamente il mercoledì 24 giugno 2025. La versione di manutenzione precedente era la 21193.

Con la versione di attivazione funzioni 2025.7.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-21331}

* CQ-4356522: ottimizzazione di `WorkflowResourceStatusProvider`.
* FORMS-16458: interfaccia utente per la scelta delle proprietà dei caratteri (font).
* FORMS-17707: il connettore AEP non funziona per AEP Platform Stage.
* FORMS-19125: supporta la mappatura automatica dei frammenti nell’editor AF.
* FORMS-19336: ricerca aggiunta nella struttura Data Source nell’editor AF.
* FORMS-19417: supporto dei pulsanti di scelta nella vista Gerarchia.
* FORMS-19603: supporta la pagina master e la pagina di progettazione nell’editor di regole.
* SITES-5358: API Rest dei frammenti di contenuto: copia i file CF con elementi figlio.
* SITES-10575: &quot;MSM Blueprint Bloomfilter Loader&quot; tenta di caricare più di 100000 righe.
* SITES-14542: se si rinomina o si sposta una pagina Live Copy di origine, dovrebbe essere attivata la pubblicazione della pagina Live Copy rinominata/spostata nel caso in cui sia stata precedentemente pubblicata.
* SITES-19754: Edge Delivery con Universal Editor: aggiungi un messaggio di errore leggibile quando l’integrazione presenta problemi.
* SITES-23499: Edge Delivery con Universal Editor: aggiunta del supporto per più campi da utilizzare per le opzioni di blocco.
* SITES-23518: Edge Delivery con Universal Editor: aggiunta del supporto per rappresentazioni di risorse specifiche per Edge Delivery.
* SITES-24436: API REST per frammenti di contenuto: è stata introdotta la cache locale per velocizzare il recupero dei riferimenti duplicati.
* SITES-25155: API Rest dei frammenti di contenuto: rimuovi il parametro di query &quot;enabledForFolder&quot; obsoleto nell’elenco Modelli.
* SITES-25913: API REST per frammenti di contenuto: convalida delle risorse in base al tempo prima di avviare il flusso di lavoro di pubblicazione.
* SITES-25976: i collegamenti all’interno dei frammenti esperienza non si adattano dopo il rollout di MSM.
* SITES-26271: Frammenti di contenuto Rest API: passa a BFS Traversal per l’endpoint di variante GET.
* SITES-27486: Editor universale - Integrazione con AEM.
* SITES-27775: Ricerca di riferimento ottimizzata durante la pubblicazione (caricamento lento dei metadati).
* SITES-27782: Edge Delivery con Universal Editor: aggiungi un’implementazione specifica dell’editore-abbonato per pubblicare contenuti su Edge Delivery (accesso anticipato).
* SITES-27792: Edge Delivery con Universal Editor: aggiungi un modello di configurazione del servizio Edge Delivery dedicato.
* SITES-28557: API REST per frammenti di contenuto: consenti l&#39;utilizzo di ETag recuperati chiamando `/cf/fragments/{fragmentId}` con `references=direct` per applicare una patch a un frammento di contenuto.
* SITES-28683: consenti alle ricerche MSM LiveRelationship di saltare lo stato avanzato.
* SITES-29601: API REST per frammenti di contenuto: convalida dei riferimenti ai frammenti di contenuto dei campi di testo lunghi.
* SITES-29614: API REST per frammenti di contenuto: recupera un flusso di lavoro utilizzando l&#39;endpoint `/cf/workflows/{workflowInstanceId}`, dove workflowInstanceIda è l&#39;ID restituito dalla richiesta di pubblicazione.
* SITES-29615: API REST dei frammenti di contenuto: elenca tutte le richieste batch create tramite POST `/cf/batch` utilizzando `GET /cf/batch`.
* SITES-29874: API Rest per frammenti di contenuto: i riferimenti da campi di testo lunghi di frammenti di contenuto ora vengono recuperati e identificati.
* SITES-29930: API Rest dei frammenti di contenuto: aggiungi metriche per il flusso di lavoro Pubblicazione dei frammenti di contenuto.
* SITES-29986: API Rest dei frammenti di contenuto: supporta la denominazione tecnica del modello CF.
* SITES-30088: Frammenti di contenuto Rest API: Pubblicazione CF - Ignora il recupero dei riferimenti quando filterReferencesByStatus è vuoto.
* SITES-30126: Frammenti di contenuto Rest API: CF Miglioramento delle prestazioni di pubblicazione: ha sostituito il controllo se una risorsa è un frammento con un controllo minimo.
* SITES-30328: Edge Delivery con Universal Editor: aggiunta del supporto per l’anteprima da Sidekick.
* SITES-30445: API REST per frammenti di contenuto: Schema dell’interfaccia utente del modello CF: aggiungi un’opzione per controllare lo stato iniziale del file comprimibile.
* SITES-30604: API Rest dei frammenti di contenuto: supporta l’adozione dello schema metadati del modello nella nuova interfaccia utente.
* SITES-30885: elaborazione JSON ottimizzata nelle query persistenti.
* SITES-30886: API Rest dei frammenti di contenuto: flussi di lavoro GET per l’endpoint dei frammenti di contenuto basati sugli UUID dei frammenti memorizzati nei metadati del flusso di lavoro.
* SITES-31005: migliora l’interfaccia utente del processo di rollout per mostrare l’avanzamento.
* SITES-31020: migliora l’interfaccia utente di Crea processo Live Copy per mostrare l’avanzamento.
* SITES-31111: API Rest dei frammenti di contenuto: consenti all’API della patch di variante di accettare riferimenti ai frammenti di contenuto all’interno dei lanci di frammenti di contenuto.
* SITES-31343: API Rest dei frammenti di contenuto: aggiungi filtro e impaginazione per data all’endpoint che elenca le richieste batch.
* SITES-31472: l’eliminazione di Launch può causare la sospensione dell’archivio se il lancio è massiccio.
* SITES-31641: API REST per frammenti di contenuto: aggiungi una proprietà ai campi modello per memorizzare le mappe dinamiche relative alle estensioni.
* SITES-31677: l’area di lavoro personalizzata supporta l’esportazione dei frammenti di contenuto di AEM in Target.
* SITES-31770: API Rest dei frammenti di contenuto: miglioramenti delle prestazioni di PATCH.
* SITES-31782: API REST per frammenti di contenuto: aggiungi una descrizione per le risorse locali.
* SITES-32175: consenti commit intermediari sia per la creazione di Live Copy che per il rollout di pagine MSM.

### Problemi risolti {#fixed-issues-21331}

* CQ-4359756: le regole di traduzione ora includono le proprietà del filtro a livello di componente.
* CQ-4359826: risolve uno stato incoerente nel pannello dei riferimenti dei frammenti di contenuto.
* CQ-4359866: la classe LanguageUtils ora supporta gli unit test senza aggiungere dipendenza aggiuntiva.
* FORMS-13990: API dei servizi Forms: Generazione documento: il campo dati, se lasciato vuoto dopo la selezione, restituisce 200 quando previsto è 400.
* FORMS-14309: API dei servizi Forms : Estrai la rettifica del codice di risposta dei dati.
* FORMS-18526: quando viene copiata una regola con più campi nelle condizioni, il campo fisso non cambia.
* FORMS-18977: il servizio DOR non trasmette il titolo del documento.
* FORMS-19047: traduzioni mancanti dopo la pubblicazione di un modulo adattivo su AEM Forms su SP22.
* FORMS-19234: impossibile utilizzare la funzione timeline dei PDF in AEM Forms.
* FORMS-19628: in DOR generato automaticamente, escludendo il titolo del pannello nidificato viene nascosto anche il titolo del pannello principale.
* FORMS-19651: correggi la regola quando un pulsante su cui si fa clic viene utilizzato in condizioni binarie e lo stesso pulsante viene utilizzato nell’istruzione then.
* FORMS-19808: FormsPortal - Non è possibile estrarre le bozze quando è abilitato il caricamento lento.
* FORMS-19887: la proprietà Access non funziona in HTML5 Preview.
* SITES-15452: gli elementi di frammenti di contenuto univoci non devono essere verificati rispetto alle relative copie nel lancio.
* SITES-24492: ARIA tablist non ha un nome accessibile.
* SITES-24623: API REST per frammenti di contenuto: correggi la mancata corrispondenza ETag tra gli endpoint per lo stesso CF.
* SITES-24668: la funzionalità della barra dei riferimenti si interrompe quando si aumenta lo zoom al 400%.
* SITES-24678: Il messaggio di stato della barra dei riferimenti non viene annunciato dall’assistente vocale.
* SITES-24697: lo stato di caricamento del modello di immagine non viene annunciato dall’assistente vocale.
* SITES-24708: La funzionalità della barra dei filtri si interrompe quando si aumenta lo zoom al 400%.
* SITES-25235: il messaggio di caricamento del contenuto della barra dei filtri non viene annunciato dall’assistente vocale.
* SITES-25254: la barra di scorrimento orizzontale viene visualizzata nel modale Carosello quando il contenuto viene visualizzato a 320 px.
* SITES-25433: Edge Delivery con Universal Editor: Correggere il rendering delle versioni di pagina per strutture di siti multilingue.
* SITES-26064: API REST per frammenti di contenuto: è stato corretto il codice di stato restituito durante la creazione di un frammento e l’ottenimento di un `AccessDeniedException` nel backend.
* SITES-26890: quando si utilizza la tastiera, lo stato attivo su Tastiera Ambito &quot;Intestazioni tabella&quot; non è visibile nella pagina Gestisci pubblicazione.
* SITES-29075: la panoramica della Live Copy non funziona per i siti web con volumi elevati.
* SITES-29514: Edge Delivery con Universal Editor: rendi obbligatorio l’URL di GitHub/progetto durante la creazione di un nuovo sito.
* SITES-29691: impossibile spostare la pagina in un caso specifico relativo ai lanci.
* SITES-29745: API Rest dei frammenti di contenuto: implementa l’idratazione delle varianti di riferimento nell’attraversamento BFS.
* SITES-29748: correzione delle condizioni di rendering per visualizzare le azioni Gestisci pubblicazione e Pubblicazione rapida nell’editor dei frammenti di contenuto.
* SITES-29789: problema di modifica del collegamento del componente nelle pagine principali copiate.
* SITES-29987: API REST per frammenti di contenuto: Crea e modifica modello per frammenti di contenuto non supporta `previewUrlPattern`.
* SITES-30140: problema relativo alla finestra doppia durante la creazione del riferimento a un frammento di contenuto.
* SITES-30327: API REST per frammenti di contenuto: la pubblicazione di FC senza autorizzazioni crea flussi di lavoro separati per ogni risorsa del payload.
* SITES-30333: lettura dei metadati delle risorse da JCR per evitare problemi di analisi XMP.
* SITES-30353: GraphQL DataFetchingExceptions per il campo &quot;src&quot; nei frammenti di contenuto di AEM.
* SITES-30377: Edge Delivery con Universal Editor: bonifica nomi di organizzazioni e siti.
* SITES-30386: Edge Delivery con Universal Editor: rimuovere duplicato, UE legacy `cors.js`.
* SITES-30583: API REST per i frammenti di contenuto: strumento Trova e sostituisci che modifica tutti i caratteri in minuscolo.
* SITES-30585: API REST dei frammenti di contenuto: `previewUrlPattern` non impostata durante la creazione di CFM con riferimenti.
* SITES-30634: Testo e allineamento alternativo immagine Editor Rich Text non funzionano in modo coerente.
* SITES-30660: Problema di conformità ADA con il componente AEM personalizzato.
* SITES-30695: Edge Delivery con Universal Editor: aumenta la classificazione della pipeline del rewriter per non interferire con il codice personalizzato.
* SITES-30727: impossibile trascinare e rilasciare componenti nell’editor di authoring di produzione.
* SITES-30752: non vengono utilizzate le intestazioni `If-modified-since`/`last-modified` durante la generazione della risposta a una query persistente.
* SITES-30871: DOM viene aggiornato dopo l’attivazione del listener afteredit.
* SITES-30877: Stato di rollout pagina figlio non corretto.
* SITES-30899: il rollout dell’opzione &quot;Più tardi&quot; consente di continuare senza selezionare alcuna data.
* SITES-30947: Eccezione Null Pointer a causa di una proprietà &quot;behavior&quot; mancante sulla blueprint durante il rollout.
* SITES-31157: API Rest dei frammenti di contenuto: la patch non riesce è un caso specifico.
* SITES-31162: API Rest dei frammenti di contenuto: è stato risolto un problema di cast per il campo `DateTimeField` in `ModelFieldMapper`.
* SITES-31174: API REST per frammenti di contenuto: i tag non sono stati pubblicati insieme alla richiesta di pubblicazione.
* SITES-31272: impossibile creare la copia per lingua di Assets tramite PageManager.copy.
* SITES-31327: API REST per frammenti di contenuto: rimuovi la convalida ETag nella richiesta di frammenti di GET.
* SITES-31387: Errore JavaScript &quot;ns.ui.alert non è una funzione&quot; durante la riattivazione dell’ereditarietà del componente fantasma.
* SITES-31454: Frammenti di contenuto Rest API: rilascia il modello per i campi di riferimento dei frammenti per accettare anche gli UUID.
* SITES-31455: API REST per frammenti di contenuto: correggi la mancata corrispondenza ETag tra gli endpoint per lo stesso modello per frammenti di contenuto.
* SITES-31459: API Rest dei frammenti di contenuto: non è possibile modificare la Live Copy CF quando è presente un campo di riferimento al contenuto.
* SITES-31467: js-errors da contexthub.authoring-hook.js nell’editor di pagine.
* SITES-31487: API Rest dei frammenti di contenuto: consenti la chiamata dell’endpoint delle autorizzazioni per la cartella principale.
* SITES-31621: Edge Delivery con Universal Editor: rimuovi una riga vuota dai fogli di calcolo che sono Live Copy.
* SITES-31676: quando si creano o si eliminano componenti, nella parte inferiore della pagina rimane uno spazio vuoto.
* SITES-31822: etichetta della casella di controllo ClassicUI mancante e HTML codificato.
* SITES-31857: la creazione di CF non riesce nelle cartelle con apici.
* SITES-31888: l’eliminazione dei frammenti di contenuto non si propaga all’anteprima.
* SITES-31922: API Rest dei frammenti di contenuto: i riferimenti di pagina non vengono restituiti dall’endpoint referencedBy.
* SITES-31987: non mostrare gli URL di anteprima per i frammenti di contenuto quando li pubblichi in Anteprima.
* SITES-32095: l’aggiornamento automatico non riesce nel listener di eventi afterchild delete in Live Copy.
* SITES-32237: Edge Delivery con Universal Editor: corregge il rendering di componenti di testo vuoti/non corretti.

### Problemi noti {#known-issues-21331}

Nessuna.

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
