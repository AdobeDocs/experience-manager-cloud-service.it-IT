---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d3a935a061831befaebd2ce25c00f8bf10522f6c
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 14%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 20783 {#20783}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 20783, rilasciata pubblicamente il mercoledì 13 maggio 2025. La versione di manutenzione precedente era la 20626.

Con la versione di attivazione funzioni 2025.5.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-20783}

* FORMS-18455: l’editor di moduli adattivi per i componenti core di AEM Forms è stato migliorato per visualizzare indicatori visivi (punti) per gli oggetti dati già utilizzati o mappati nel modulo all’interno della struttura dell’origine dati, una funzione che consente agli autori di identificare facilmente gli elementi dati utilizzati.
* FORMS-18450: il prodotto viene migliorato eseguendo la migrazione della logica del dominio reCaptcha V2 in `AdaptiveFormConfigurationServiceImpl`. Questa modifica ha lo scopo di centralizzare la configurazione e può essere allineata con l’aggiunta del supporto per reCaptcha V2 invisibile nei Componenti core.
* FORMS-19630: AEM 6.5 quickstart uber-jar è stato aggiornato per includere il pacchetto più recente dei componenti core Adaptive Forms, in modo che l’ambiente quickstart rifletta le funzionalità più recenti di Adaptive Forms e sostituisca il codice legacy.
* FORMS-19125: l’editor di moduli adattivi dei componenti core è stato migliorato per supportare la mappatura automatica dei frammenti di moduli adattivi disponibili quando una sezione corrispondente dalla struttura dell’origine dati viene rilasciata nell’area di lavoro del modulo. Questa funzione porta una caratteristica chiave di produttività dall’editor di base ai componenti core.
* FORMS-17887: AEM Forms ora fornisce la funzionalità di generare documenti in formato AFP (Advanced Function Presentation) tramite il servizio di output. Questo miglioramento soddisfa le esigenze dei clienti per ambienti di stampa ad alta velocità e volumi elevati che utilizzano solitamente AFP.
* FORMS-15089: AEM Forms ha introdotto la possibilità di creare una versione di un modulo al momento della pubblicazione in modo tale che tutti i frammenti che lo compongono siano allineati (incorporati) in quella specifica versione pubblicata. Ciò garantisce una rappresentazione esatta e indipendente del modulo così come appariva al momento della pubblicazione, che può essere fondamentale per scopi di archiviazione, legali o di conformità.
* SITES-27775: Ricerca di riferimento ottimizzata durante la pubblicazione.
* SITES-30885: elaborazione JSON ottimizzata nelle query persistenti.
* SITES-25433: Edge Delivery con Universal Editor: supportano il rendering di pagine intere quando si confrontano versioni precedenti.
* SITES-27792: Edge Delivery con Universal Editor: aggiungi un modello specifico per le configurazioni del servizio Edge Delivery
* SITES-19754: Edge Delivery con Universal Editor: messaggio di errore convincente quando la configurazione non viene eseguita correttamente.
* SITES-30328: Edge Delivery con Universal Editor: anteprima dal supporto Sidekick.
* SITES-23499: Edge Delivery con Universal Editor: consente di utilizzare più campi per le opzioni di blocco.
* SITES-29987: aggiungi la funzionalità per impostare `previewUrlPattern` durante la creazione di modelli per frammenti di contenuto.
* SITES-29874: è stato aggiunto il supporto per i riferimenti LongTextField nell’API per frammenti di contenuto.
* SITES-29601: aggiungi la convalida per i frammenti di contenuto a cui si fa riferimento tramite campi LongText.
* SITES-24623: rendi utilizzabili per la patch i tag ET restituiti da GET e l’API dei frammenti DI RICERCA.
* SITES-28557: Consenti il parametro URL `references` nel frammento di contenuto di PATCH.
* SITES-5358: [OpenAPI] copia frammenti di contenuto con elementi secondari.
* SITES-29614: endpoint del flusso di lavoro di GET.
* SITES-29615: elenca l’endpoint API per richieste batch.
* SITES-25130: Aggiornamento dei Componenti core alla versione 2.28.0
* SITES-10575: &quot;MSM Blueprint Bloomfilter Loader&quot; tenta di caricare più di 100.000 righe.
* SITES-26711: i collegamenti per i campi di testo dell’Editor Rich Text non vengono aggiornati per puntare alla Live Copy durante il rollout di MSM.
* SITES-25976: i collegamenti all’interno dei frammenti esperienza non si adattano dopo il rollout di MSM.

### Problemi risolti {#fixed-issues-20783}

* ASSETS-50994: traffico in ingresso bloccato in AemRequestEventFilter.
* CQ-4358591: progetti mancanti per alcune lingue quando vengono create copie per lingua dal pannello di riferimento dei siti con l’opzione &quot;Crea progetti di traduzione&quot;.
* CQ-4359108: errore nel formato XLIFF 2.0 durante l’utilizzo di Importazione/Esportazione traduzione umana.
* CQ-4358722: la localizzazione non funziona per i codici ISO legacy a causa di codici internazionali diversi in Java 11 e Java 17.
* FORMS-19808: quando si salva un modulo di grandi dimensioni contenente frammenti abilitati per il caricamento lento, l’utente non può estrarre le bozze.
* FORMS-19887: un campo a discesa in un modulo XFA, inizialmente impostato per l’accesso in sola lettura, non passa a uno stato aperto/modificabile quando si esegue il rendering del modulo in HTML5. Il campo rimane di sola lettura e impedisce l’interazione dell’utente, a differenza del rendering PDF in cui funziona come previsto.
* FORMS-19651: nell’editor delle regole, una regola non funziona correttamente quando si utilizza un clic su un pulsante in una condizione binaria e lo stesso pulsante viene utilizzato anche nell’istruzione &quot;then&quot; di tale regola.
* FORMS-19628: nel documento di record generato automaticamente (DoR) per il Forms adattivo basato su Componente core, escludendo il titolo di un pannello nidificato dal DoR, si nasconde erroneamente anche il titolo del pannello principale, se nel pannello principale è abilitata l’opzione &quot;Consenti testo formattato per titolo&quot;.
* FORMS-18977: nei PDF generati dal servizio Document of Record (DoR) manca il titolo del documento. Questo può causare la non conformità agli standard di accessibilità PDF/UA e WCAG 2.1, in quanto il titolo del documento è un attributo obbligatorio per i PDF accessibili.
* FORMS-18526: quando una regola contenente più campi nelle relative condizioni viene copiata da un campo all’altro, un riferimento a un campo fisso all’interno di queste condizioni mantiene erroneamente il proprio riferimento al campo di origine originale invece di eseguire l’aggiornamento al nuovo campo in cui la regola viene copiata.
* FORMS-19047: dopo la modifica e la ripubblicazione di un modulo adattivo in AEM Forms (in particolare 6.5.22.0), potrebbero mancare le traduzioni per alcuni elementi del modulo, in particolare le caselle di testo.
* FORMS-19234: la funzione timeline per PDF in AEM Forms, che consente agli utenti di visualizzare i dettagli sulla creazione e sul controllo delle versioni di un PDF, non funziona più dopo il caricamento di qualsiasi PDF nella sezione &quot;Forms e documenti&quot;.
* FORMS-19373: gli errori di replica non vengono segnalati correttamente durante un processo di &quot;pubblicazione dorata&quot; in ambienti in cui non sono configurati agenti di replica.
* FORMS-18196: l&#39;API HTTP per la sincronizzazione di `generatePrintedOutput` (o `generatePdfOutput`) restituisce erroneamente un codice di risposta 200 (riuscito) invece del codice di errore 400 (richiesta non valida) previsto quando i dati dei campi facoltativi richiesti dal modello XDP vengono lasciati vuoti nella richiesta.
* FORMS-19336: nell’editor di moduli adattivi dei componenti core (editor AF2), la funzionalità di ricerca nella struttura del Source dati non funziona correttamente o come previsto, impedendo agli utenti di trovare facilmente elementi di dati specifici.
* FORMS-19629: il parser dello schema JSON genera risultati non validi o interpreta in modo errato alcuni schemi JSON forniti dal cliente. Questo problema può influire negativamente sulle funzionalità che si basano su un’analisi corretta dello schema, come la mappatura automatica dei frammenti.
* FORMS-19380: l’introduzione del supporto del controllo delle versioni per i Componenti core di Adaptive Forms ha involontariamente abilitato le funzionalità di controllo delle versioni per vari altri tipi di risorse (ad esempio, Foundation Forms, file PDF, Temi, FDM) senza una progettazione o un test specifici per tali tipi di risorse. Questo effetto collaterale non voluto è sotto esame.
* FORMS-17707: il connettore AEP (Adobe Experience Platform) non funziona correttamente se configurato per la connessione agli ambienti di stage della piattaforma AEP.
* GRANITE-58276: i cicli di dipendenza OSGi impediscono il corretto funzionamento del factory del motore di script HTL.
* OAK-11673: aumento di Oak-segment-azure v12 CPU causato da refreshLease.
* SITES-30752: non utilizzare le intestazioni `If-modified-since`/`last-modified` durante la generazione della risposta di query persistente.
* SITES-30353: GraphQL DataFetchingExceptions per il campo &quot;src&quot; nei frammenti di contenuto di AEM.
* SITES-30333: leggi i metadati delle risorse da jcr per evitare problemi di analisi xmp.
* SITES-30140: problema relativo alla finestra doppia durante la creazione del riferimento a un frammento di contenuto.
* SITES-29748: correggi le condizioni di rendering per visualizzare le azioni Gestisci pubblicazione/pubblicazione rapida all’interno dell’editor CF.
* SITES-15452: gli elementi CF univoci non devono essere verificati rispetto alle relative copie nel lancio.
* SITES-30386: Edge Delivery con Universal Editor: la duplicazione di UE cors.js fa sì che UE duplichi le sezioni durante l’aggiunta di contenuto.
* SITES-29745: risolto un raro problema a causa del quale le varianti dei riferimenti non venivano idratate.
* SITES-30585: impossibile impostare &#39;previewUrlPattern&#39; durante la creazione di modelli con riferimenti.
* SITES-30327: la pubblicazione di frammenti di contenuto senza autorizzazioni crea flussi di lavoro separati per ogni risorsa del payload.
* SITES-29528: ETag non può essere utilizzato per il caching nell’istanza Publish.
* SITES-30583: strumento Find &amp; Replace (Trova e sostituisci), che consente di convertire tutti i caratteri in minuscolo.
* SITES-31157: la patch non riesce a causa di ETag incoerente.
* SITES-31327: [OpenAPI] La richiesta di recupero del frammento di contenuto nell&#39;istanza di authoring può rispondere con 304.
* SITES-29691: NullPointerException durante il tentativo di spostamento della pagina.
* SITES-30728: OnTime/OffTime non pubblica/Annulla pubblicazione come previsto se configurato nelle proprietà della risorsa.
* SITES-29789: Modifica del collegamento dei componenti nelle pagine principali copiate in AEM.
* SITES-29191: impossibile aggiungere più di 20 SKU al componente Elenco prodotti.
* SITES-30372: Ritaglio avanzato non funziona sul componente core Immagine (V2) di AEM.
* SITES-28693: il componente Teaser esegue il rendering del HTML danneggiato quando il titolo è vuoto.
* SITES-28668: impossibile promuovere il lancio con LaunchPromotionParameters.
* SITES-31005: migliora l’interfaccia utente del processo di rollout per mostrare al cliente l’avanzamento.
* SITES-31020: migliora l’interfaccia utente Crea processo Live Copy per mostrare al cliente l’avanzamento.
* SITES-29816: Errore &quot;Risorsa non trovata&quot; durante la creazione di Live Copy del frammento di esperienza.
* SITES-29363: il pulsante Ripristina la Live Copy non funziona per la gerarchia dei contenuti della live copy nidificata.
* SKYOPS-106509: aggiungi altri flag di apertura dei componenti aggiuntivi per supportare l’accesso riflettente GSON su Java 21.

### Problemi noti {#known-issues-20783}

Nessuna.

### Funzioni e API obsolete {#deprecated-20783}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-20783}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 19 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-20783}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.78.1-T20250429061757 | [API Oak API 1.78.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
