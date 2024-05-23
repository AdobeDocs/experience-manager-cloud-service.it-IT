---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d107f40c4bc43837db9d8fab3d06627d9e930620
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 10%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 16357 {#release-16357}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 16357, rilasciata pubblicamente il giovedì 22 maggio 2024. La versione di manutenzione precedente era 16145.

Con l’attivazione delle funzioni 2024.5.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-16357}

* SITES-19579: API Java per migrare i frammenti di contenuto da un modello all’altro.
* SITES-19698: [Apri API] Crea un’operazione di lettura per la gestione di uno schema di interfaccia utente per modello nella definizione OpenAPI.
* SITES-19834: ID mancanti nell’evento di Adobe I/O per la pubblicazione o l’annullamento della pubblicazione.
* SITES-20146: Abilita versione anteprima / Confronta per le pagine spostate.
* SITES-19973: Implementazione API di ricerca CFM.
* SITES-20333: migliora la convalida durante la creazione di frammenti di contenuto.
* SITES-20334: migliora la convalida durante la modifica dei modelli per frammenti di contenuto.
* SITES-20585: migliora l’API di ricerca dei frammenti di contenuto per filtrare in base alla lingua.
* SITES-20594: restituisce il nome completo dell’utente che crea, modifica o replica una risorsa.
* SITES-20601: [OpenAPI] Aggiorna l’API di ricerca CF per consentire il recupero solo dei frammenti di contenuto secondari diretti.
* SITES-20656: [BE] Fornisci l’opzione che fa corrispondere le maiuscole/minuscole durante la sostituzione di una stringa.
* SITES-20405: [Xwalk] Supporta mimeType per la compressione del campo.
* SITES-17854: Supporto UUID per riferimenti a CF e risorse (Pfizer MVP).
* SITES-19555: API modello semplice per lo schema dell’interfaccia utente.
* SITES-19611: [Apri API] Crea un’operazione di scrittura/aggiornamento per la gestione di uno schema di interfaccia utente per modello nella definizione OpenAPI.
* SITES-19614: [Xwalk] Paginazione del foglio di calcolo/scorrimento infinito.
* SITES-20005: la pipeline di authoring deve presentare un ritardo dell’evento configurabile.
* SITES-20121: Consenti defaultValue per i campi enum.
* SITES-20342: [Back-end] Pubblica a livello di cartella: aggiungi il filtro per pubblicare solo i CF.
* SITES-20355: rimuovi i modelli per frammenti di contenuto e i servlet API per le autorizzazioni.
* SITES-20387: quando si passa a tagadmin, viene sempre calcolato l’utilizzo dei tag.
* SITES-20495: [BE] Possibilità di ottenere l’autorizzazione per la pubblicazione a livello di cartella.
* SITES-20653: [Xwalk] aggiungi experiment-start-date e -end-date.
* SITES-20666: [Xwalk] l’dell’esperimento deve essere disattivato per impostazione predefinita durante l’authoring.
* SITES-20752: [cq-wcm-core] Apple Launches per FC.
* SITES-20946: aggiungi l’etag come proprietà nell’endpoint dei modelli LIST.
* SITES-20947: [persistenza] recupera l’attività secondaria per id frammento di contenuto.
* SITES-21012: Unisci schema metadati modello a prodotto.
* SITES-21769: utilizza il prefisso del percorso /jcr:id/ per il recupero risorsa per ID.
* ASSETS-30379: il controllo della licenza DRM esamina l’intera struttura delle risorse scaricate.
* ASSETS-35535: [Errore adattatore dati] I download di risorse vuoti devono essere ignorati per gli eventi v1.
* SITES-21550: [Xwalk] Metadati personalizzati: campi numero, data, dataora e ora.
* SITES-20149: RTC: [cq-wcm-launches-core] Esporta nuova API per Launches per FC.
* SITES-20150: RTC: [cq-command] Aggiungi nuovi metodi all’API esistente.
* SITES-20451: Aggiungi il plug-in sidecar a wcm-commons.
* SITES-20499: [MSM][Async] Estrarre il codice da AsyncOperationServlet a una classe di utilità.
* SITES-20763: aggiorna gli endpoint API di consegna nell’integrazione di Sites.
* SITES-20583: Aggiungi etag come proprietà in `LIST`/search frammenti.
* CQ-4356445: Event Producer &amp; Schema Implementation (Generazione eventi e implementazione schema).
* CQ-4356625: migliorare il controllo delle autorizzazioni in languagecopyrendercondition.jsp.
* CQ-4356629: migliorare il check-in dell’autorizzazione in isWorkflowUser rendercondition.
* CQ-4356934: semplifica l’API RequestProcessor quando si lavora con ResponseEntities.
* CQ-4357214: i processori di richiesta non devono dipendere dalla logica del servlet.
* SITES-16392: la creazione di un lancio non riuscita non deve lasciare contenuto indesiderato.
* SITES-20238: [RTC] Pfizer MVP - Aggiungi API CF per risolvere i percorsi CF in ID e viceversa.
* SITES-21043: [CF][launches] Miglioramenti delle prestazioni delle porte laterali al Cloud Service.
* SITES-21044: [CF][launches] Implementazione del payload di modifica asincrona porta laterale al Cloud Service.
* FORMS-7483: il parser dello schema JSON di AEM Forms ora supporta lo schema JSON (2020-12).
* FORMS-13209: è incluso un gestore per ignorare i gestori predefiniti di invio e esito negativo di Adobe Adaptive Forms. Puoi configurare questi gestori tramite l’Editor di regole di Forms adattivo.
* FORMS-13612: gli assistenti vocali ora leggono messaggi di errore, descrizioni brevi e descrizioni lunghe per i campi nel Forms adattivo basato su componenti core. Inoltre, è stato aggiunto il supporto per annullare la validità degli input dei moduli adattivi quando il modulo contiene errori e non è valido per l’invio.
* FORMS-12052: un autore di moduli può ora applicare funzioni personalizzate alla preelaborazione dei dati prima dell’invio.
* FORMS-11295: è stato aggiunto il supporto per SHA256 con l’algoritmo ECDSA per la firma digitale AEM Forms.
* FORMS-9432: è stato aggiunto un ulteriore tipo di contenuto (endpoint REST) alla configurazione cloud dell’origine dati. Consente l’invio di dati in coppie chiave-valore a un endpoint autenticato.

### Problemi risolti {#fixed-issues-16357}

* SITES-20608: i frammenti di esperienza con la personalizzazione abilitata quando sono inclusi in un modello causano un ciclo infinito.
* SITES-19554: [Xwalk] Spreadsheet Editor: impossibile svuotare una cella.
* SITES-19971: L’applicazione di patch a un CFM contenente schede cambia l’ordine dei campi.
* SITES-20168: Modello per frammenti di contenuto `locked` campo non aggiornato correttamente.
* SITES-20522: i frammenti di contenuto danneggiati interrompono l’endpoint /adobe/sites/cf/fragments.
* SITES-20816: CF OpenAPI - Incoerenza di output con modello mancante per il frammento di riferimento.
* SITES-21239: rimuovere la dipendenza circolare ContentFragmentSearchService.
* SITES-20582: la ricerca e l’elenco dei frammenti di contenuto devono consentire la profondità 0.
* SITES-20559: [MSM][XF][Lufthansa] Il rollout dei frammenti di esperienza da master/lingua a paese/lingua non aggiorna i riferimenti.
* SITES-17772: AEM: l’utente con il gruppo di amministrazione non può sbloccare la pagina bloccata da un altro utente.
* SITES-20401: [Xwalk] I metadati di sezione non supportano proprietà con più valori.
* SITES-21391: [OpenAPI, evento] Nessun evento attivato durante la modifica del titolo o dei tag (proprietà) di un modello per frammenti di contenuto.
* SKYOPS-73234: aumento degli errori di registro in seguito all’aggiornamento del programma AEM Assets Global DAM al 15553 sulla versione AEM e al 35362 ID PR.
* SKYOPS-75341: NoThatMethodError nel bundle di distribuzione Crosswalk.
* SCRNS-3945: Skyline: Stringa &quot;Pianificata&quot; non localizzata in Screens.
* SITES-20586: Timestamp del modello &quot;Pubblicato&quot; non aggiornato.
* SITES-16674: la casella di controllo Eredita configurazioni di rollout non funziona sulle proprietà Live Copy.
* SITES-18680: impossibile estrarre le varianti di riferimento nella query graphql (Apple).
* SITES-21233: [CoreCmp] Pannello a soffietto rotto per GS1 US dopo l’aggiornamento a 15860.
* SITES-20367: problema con l’eliminazione dei lanci nell’AEM.
* CQ-4357161: la schermata Payload della casella in entrata AEM restituisce 404.
* SITES-20214: Problema relativo alla sequenza di configurazione del rollout dell’AEM al momento del salvataggio.
* SITES-20364: 302 Reindirizzamenti non funzionanti con il selettore nell’URL.
* SITES-20547: Elenco dei percorsi troncati nelle Live Copy Excluded Paths (percorsi esclusi) su AEM as a Cloud Service.
* SITES-20691: la limitazione del modello di frammento esperienza non rispetta cq:allowedTemplates.
* SITES-21122: Difetto di AEM CS Live Copy con frammenti di contenuto.
* ASSETS-38723: NPE generato da MetadataRulesProviderImpl quando getReadRulesForMetadataChildNodes() viene chiamato prima dell’inizializzazione di this.readRules.
* SITES-11727: [GQL] Mancano dati nella piena idratazione dei riferimenti ai frammenti di contenuto.
* SITES-19462: La ricerca delle risorse non funziona correttamente in AEM Cloud.
* SITES-19994: pulsante Chiudi che si attiva quando gli utenti tentano di chiudere un frammento di contenuto.
* SITES-20029: le versioni dei frammenti di contenuto vengono create subito dopo averlo chiuso senza modificare il contenuto.
* SITES-21316: Anteprima frammento: l’anteprima non riesce a causa di modifiche al codice da SITES-11727.
* SITES-20023: Il caricamento del file non funziona per le risorse Remote (risorse di nuova generazione) in più campi.
* ASSETS-37611: viene attivato il flusso di lavoro &quot;Request to Complete Move Operation&quot; (Richiesta di completamento operazione di spostamento) per la risorsa non pubblicata.
* CQ-4357278: DispatcherServlet restituisce un valore NPE se getRequestBodyType restituisce null.
* CQ-4357279: l’elaborazione della richiesta non riesce se non è presente pathInfo per una richiesta.
* SITES-20496: [Xwalk] Opzione Nessuna proprietà quando si seleziona il foglio di calcolo in Amministrazione sito.
* FORMS-13827: nell’editor di regole di Forms adattivo, l’operazione WHEN non supporta attualmente diversi tipi di campi con selettori di date.
* FORMS-13786: nell’editor di regole di Forms adattivo, la funzionalità di trascinamento della selezione non funziona per le funzioni personalizzate.
* FORMS-13587: nell’editor di Forms adattivo, la funzione di emulatore di dispositivi non funziona correttamente per Forms adattivo basato su componenti core.
* FORMS-14376 Quando un utente preme il pulsante Reimposta, se il testo statico è contrassegnato come non associato si verificano errori nella console.
* FORMS-13801: anche se il componente termini e condizioni è disabilitato, la casella di controllo corrispondente rimane abilitata.
* FORMS-11952: quando un modulo viene inviato, l’URL di invio generato dal modulo inizia con /content/ invece di /portale/, inviando erroneamente la richiesta. Questo impedisce alla richiesta di raggiungere i server previsti.
* FORMS-13616: la selezione della data mostra la data corrente come un giorno indietro, probabilmente a causa di un problema di fuso orario, e c’è difficoltà a impostare il formato corretto della data a causa di questa incoerenza e di un problema aggiuntivo nel modello di visualizzazione.
* FORMS-13829: il menu a discesa, controllato da regole per simulare la funzionalità dei pulsanti di scelta, non viene compilato correttamente dopo che una selezione è stata cancellata e riselezionata. Si desidera che le singole caselle di controllo agiscano come pulsanti di scelta, consentendo una sola selezione alla volta e la deselezione di tutte le opzioni.
* FORMS-14244: in un modulo adattivo basato su un XDP con script incorporati nelle caselle di controllo, gli script non vengono eseguiti per gli elementi che seguono tali caselle di controllo.
* FORMS-14267: gli utenti riscontrano errori di timeout coerenti durante l’invio di richieste API in ambienti di sviluppo, stage e produzione. Queste richieste sono correlate alla generazione di PDF, a volte con dati precompilati utilizzando l’associazione dati. Il problema si traduce in un processo di sospensione che alla fine si interrompe, ma riesce e riprova dopo l’errore.
* FORMS-11589: per gli utenti che dispongono solo della soluzione AEM Forms (senza altre soluzioni), la pipeline front-end non funziona.
* FORMS-13896: nell’output DoR (Document of Record), le date e i numeri vengono visualizzati in arabo indipendentemente dal fatto che i dati di input vengano uniti utilizzando numeri gregoriani.

### Problemi noti {#known-issues-16357}

Nessuno.

### Funzioni e API obsolete {#deprecated-16357}

Per sapere cosa è obsoleto o è stato rimosso in AEM as a Cloud Service, consulta [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Tecnologie incorporate {#embedded-tech-16357}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.62.0 | [API Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| API SLING AEM | 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.25.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
