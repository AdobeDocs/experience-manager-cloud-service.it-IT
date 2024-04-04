---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d07fc976fe9c8e7872468048f80e525fe8484339
workflow-type: tm+mt
source-wordcount: '2584'
ht-degree: 8%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 15787 {#release-15787}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 15787, rilasciata al pubblico il venerdì 4 aprile 2024. La versione di manutenzione precedente era 15575.

Con l’attivazione delle funzioni 2024.3.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-15787}

* SITES-19059 - Frammenti di contenuto - OpenAPI - Consenti valore predefinito per campi enum
* SITES-20013 - Frammenti di contenuto - OpenAPI - WCMScriptHelper deve interrompere il rendering quando non è presente ServletResolver
* SITES-19926 - Frammenti di contenuto - OpenAPI - Miglioramenti a OnOffTriggerProcessor
* SITES-17945 - Frammenti di contenuto - OpenAPI - Ottieni gli ultimi metadati modificati per ogni versione
* SITES-17298 - Frammenti di contenuto - OpenAPI - Autorizzazioni per i modelli di frammenti di contenuto
* SITES-14255 - Frammenti di contenuto - OpenAPI - Convalida l’univocità del campo di testo se nel modello per frammenti è impostato un flag univoco
* SITES-15557 - Frammenti di contenuto - OpenAPI - Consenti valore predefinito per campi enum
* SITES-1559 - Frammenti di contenuto - OpenAPI - Aggiorna l’API dell’elenco CF per consentire il recupero solo dei frammenti di contenuto secondari diretti (BE)
* SITES-16052 - Frammenti di contenuto - OpenAPI - Aggiungi l’URL per l’istanza in cui può essere utilizzata una risorsa
* SITES-17944 - Frammenti di contenuto - OpenAPI - Mappatura appropriata degli ACL JCR all’endpoint CF Permissions
* SITES-17513 - Piano di controllo per frammenti di contenuto - Annullare la pubblicazione dei frammenti di contenuto
* SITES-8831 - Piano di controllo per frammenti di contenuto - PUT - Aggiornare un frammento con informazioni complete
* SITES-8836 - Frammenti di contenuto - OpenAPI - Piano di controllo - Riferimenti a GET - Ottieni riferimenti principali di un frammento (tramite UUID)
* SITES-8986 - Frammenti di contenuto - OpenAPI - Pubblica modello per frammenti di contenuto
* SITES-18073 - Frammenti di contenuto - OpenAPI - Pattern PreviewURL per un CFM
* SITES-15242 - Frammenti di contenuto - OpenAPI - Estende gli eventi di pubblicazione per fornire informazioni sul livello
* SITES-18702 - Frammenti di contenuto - OpenAPI - [Back-end] Possibilità di pubblicare a livello di cartella
* SITES-20020 - Frammenti di contenuto - OpenAPI - Rimuovi `X-Adobe-Accept-Unsupported-API` prima di GA
* SITES-16066 - Frammenti di contenuto - Editor frammento - Cambia l’URL JS del selettore risorse
* SITES-19326 - Frammenti di contenuto - Editor frammento - Aggiorna i collegamenti nell’interfaccia utente Assets per aprire il file CF nel nuovo editor CF
* SITES-10515 - Frammenti di contenuto - API GraphQL - GraphQL - Problema di prestazioni AbstractFetcher caricamento frammenti di contenuto di riferimento
* SITES-17364 - Frammenti di contenuto - API GraphQL - Restituisce il nome completo per le proprietà Modificato da e Pubblicato da
* SITES-19165 - Frammenti di contenuto - API GraphQL - Consente di utilizzare modelli globali, a cui fare riferimento e su cui eseguire query in tutti gli endpoint GraphQL
* SITES-17768 - Frammenti di contenuto - API GraphQL - URL esposizione Dynamic Medie per le immagini tramite _dmS7Url
* SITES-11057 - Backend core - Evita di caricare tutte le versioni quando apri Timeline > Versioni
* SKYOPS-63033 - HTTPD - Ritaglia gli spazi vuoti delle variabili di ambiente del dispatcher
* SKYOPS-65518 - HTTPD - Errore di convalida se nella cartella del dispatcher sono presenti nomi di file non validi
* SITES-19626 - Lanci - Unisci i campi DAM-CFM lastUpdate in main
* SITES-19251 - Sito rapido - Creazione guidata - Barra laterale dell’interfaccia utente di amministrazione dei siti di supporto quando il riferimento al tema non è uguale al nome del sito
* SITES-15430 - Editor universale - Editor universale sotto dominio AEM
* CQ-4344966 - WCM - Traduzione - Crea un framework di base per l’aggiornamento strutturale dei siti e aggiorna quello esistente per le risorse
* CQ-4347312 - WCM - Traduzione - Crea un flusso di lavoro per associare &quot;cq:translationsourcejcruuid&quot; nelle copie di origine e lingua esistenti
* CQ-4354509 - WCM - Traduzione - Pubblica eventi processo di traduzione [OSGi EventAdmin]
* SITES-16318 - Crosswalk - Authoring basato su AEM con Edge Delivery Services
* FORMS-9889: l’utente può aggiungere la configurazione URL POST e Cloud durante la configurazione dell’azione Invia per l’endpoint REST
* Nell’editor delle regole, gli utenti possono:
   * FORMS-12160: convalidare un campo, un pannello o un modulo nella sezione Then della condizione When.
   * FORMS-12570: reimpostare un campo, un pannello o un modulo nella sezione Then della condizione When.
   * FORMS-11541: utilizza oggetti campo e oggetti globali nell’editor di regole tramite le funzioni personalizzate.
   * FORMS-11714: definisci i parametri come facoltativi nella funzione personalizzata. Per impostazione predefinita, i parametri dichiarati nelle funzioni personalizzate sono obbligatori.
   * FORMS-11756: utilizza il caching per le funzioni personalizzate per migliorare il tempo di risposta durante il recupero dell’elenco delle funzioni personalizzate nell’editor di regole.
   * FORMS-12053: aggiungi un’istruzione &quot;else&quot; nella condizione &quot;When&quot; per implementare le condizioni nidificate.
   * FORMS-11269: utilizza funzioni JavaScript moderne ES10 come le funzioni let e arrow nella funzione personalizzata per i moduli basati su componenti core.

* FORMS-9014: vari miglioramenti relativi all’accessibilità del componente Firma scarabocchio


### Problemi risolti {#fixed-issues-15787}

* Vari problemi di accessibilità e internazionalizzazione risolti
* SITES-16966 - AEM: &quot;Not Versioned!&quot; non localizzato stringa in Sites > Ripristina > Ripristina struttura
* SITES-16208 - ContentFragmentModelIdentifier espone una proprietà del titolo fuorviante
* SITES-18024 - Quando l’intestazione If-Match non è presente, la risposta deve essere 428
* SITES-18003 - L’utente che ha creato una versione non viene restituito correttamente
* SITES-17937 - L’evento di creazione del frammento di contenuto viene emesso prima della sincronizzazione dei pod di authoring
* SITES-18029 - La pipeline di elaborazione dell’evento si blocca se notificata contemporaneamente dall’osservazione JCR
* SITES-17882 - Rimuovi dallo schema il limite massimo del campo di testo del frammento
* SITES-19252 - Correzione delle incoerenze relative ai codici di stato HTTP 406 e 415
* SITES-16964 - [Back-end] L’ordinamento in base a &quot;Modificato da&quot; non funziona correttamente
* SITES-17519 - Editor proprietà pagina Sites - Il nome lungo della pagina rende i pulsanti non cliccabili
* SITES-16852 - L’API Publish sta pubblicando riferimenti con NUOVO stato
* SITES-18833 - Vincolo di unicità non visibile negli endpoint OpenAPI
* SITES-15553 - Impossibile caricare il pannello laterale di XF se l’URL del file XF contiene un selettore
* SITES-14340 - NPE in VersioningTimelineEventProvider.accept
* SITES-1605 - [Sites] DeletePageCommand genera un valore NPE in caso di percorso di origine nullo
* SITES-16308 - [GB18030]: viene visualizzato un messaggio di avviso quando si crea una nuova cartella Sites denominata con caratteri GB18030
* SITES-16304 - [GB18030]: viene visualizzato un messaggio di avviso quando crei una nuova cartella Frammenti esperienza denominata con caratteri GB18030
* SITES-8769 - Miglioramento delle prestazioni StyleImpl
* CQ-4343815 - Campagna - Targeting - La variante predefinita di un teaser ha un URL vuoto
* CQ-4355889 - Campaign - Targeting - Crea richiesta pubblico non riuscita con configurazione IMS.
* SITES-12460 - Integrazione di Campaign - Integrazione di Campaign/AEM Cloud Service interrotta
* SITES-11571 - Frammenti di contenuto - API GraphQL - PersistedQueryServlet deve inviare 400 su URL non validi
* SITES-19946 - Frammenti di contenuto - API GraphQL - I modelli non vengono più analizzati all’avvio
* SITES-1605 - Back-end core - DeletePageCommand genera un’eccezione NPE in caso di percorso di origine nullo
* SITES-5429 - Back-end core - ChildrenListServlet itemResourceType consente l’esecuzione diretta del codice
* SITES-15553 - Frammenti esperienza - Impossibile caricare il pannello laterale di XF se l’URL del file XF contiene un selettore
* SITES-13666 - Headless - Admin - Error Log False Positive &quot;com.adobe.cq.dam.cfm.headless.ui.impl.models.CFHomeCardModelImpl L’ID di configurazione non può essere nullo&quot;
* SITES-17164 - Editor pagina - [Cloud, 6.5 Forms] L’anteprima dell’Editor temi AF è interrotta
* SITES-14340 - Interfaccia utente amministratore Sites - NPE in VersioningTimelineEventProvider.accept
* SKYOPS-68611 - Sling - repoinit - Port sling repoinit crea correzione percorso nel ramo manutenzione
* CQ-4354678 - WCM - Traduzione - I processi di traduzione esportano il contenuto tradotto
* CQ-4355167 - WCM - Traduzione - Impossibile ottenere la finestra a comparsa mentre si contrassegna un processo di traduzione come Completo o Archivio
* CQ-4355913 - WCM - Traduzione - Errori nelle schede delle lingue del progetto di traduzione
* GRANITE-47694 - Flusso di lavoro - Impossibile ottenere sottoattività in un flusso di lavoro sul cloud per un utente non amministratore
* ASSETS-31097 - Assets Cloud - Registri compilati con gli avvisi di attraversamento dell’indice per /bin/numberofentitiesinfolders.json
* ASSETS-35860 - Assets Cloud - Conversione errata del fuso orario nella vista a colonne di AEM Assets
* SITES-15260 - Interfaccia classica (legacy) - Bulkedit aggiunge proprietà VUOTE alla pagina se si utilizza l’importazione del foglio
* SITES-16834 - Interfaccia classica (legacy) - Testo mancante dopo la modifica del testo utilizzando l’editor in blocco quando il testo contiene la virgola
* SITES-17767 - Frammenti di contenuto - Amministratore - Supporto consentito di cf-model anche per cartelle senza un nodo jcr:content
* SITES-17683 - Frammenti di contenuto - Back-end core - I frammenti di contenuto non sono serializzabili con l’esportatore Jackson
* SITES-18797 - Frammenti di contenuto - Back-end core - Risultati GraphQL duplicati dopo la personalizzazione dell’indice
* SITES-18076 - Frammenti di contenuto - Back-end core - Il testo con più valori presenta @TypeHint errati
* SITES-17856 - Frammenti di contenuto - Models &amp; Model Editor - Modelli CF non visualizzati se la configurazione non è una cartella
* SITES-17071 - Back-end di base - Una pagina specifica non visualizza la versione nella timeline
* SITES-17285 - Componenti core - Il ritaglio dell’immagine in linea è diverso nelle funzioni Author e Publish in AEMaCS
* SITES-19187 - Componenti core - Due metodi di posizionamento delle risorse nel componente Immagine forniscono risultati diversi nella finestra di dialogo
* SITES-20077 - Componenti core - Ritaglio immagine in linea - ritaglio errato e immagini sfocate
* SITES-17211 - Frammenti esperienza - Finestra di dialogo del selettore del percorso del componente Frammenti esperienza che mostra i frammenti esperienza eliminati
* SITES-17894 - Lanci - La promozione di lanci nidificati ripristina il contenuto del lancio a una versione precedente
* SITES-16042 - MSM - Live Copy - Le annotazioni non vengono visualizzate correttamente nella Livecopy dopo i rollout
* SITES-16691 - MSM - Live Copy - Quando il cliente seleziona &quot;rollout&quot; o &quot;rollout a&quot; dall’icona &quot;rollout&quot; su un componente, il pulsante &quot;continua&quot; è disattivato.
* SITES-16733 - MSM - Live Copy - Non è possibile eseguire il rollout della pagina dell’indice blueprint quando rep:policy è applicato al nodo
* SITES-17155 - MSM - Live Copy - Le intestazioni e i piè di pagina vengono tradotti nuovamente in inglese quando LiveCopy viene rinominata
* SITES-17492 - MSM - Live Copy - Incongruenze nel layout della pagina Live Copy dell’AEM
* SITES-19316 - MSM - Live Copy - Il collegamento di riferimento al frammento di esperienza non viene aggiornato nella copia per lingua
* SITES-19347 - MSM - Live Copy - Messaggi di rallentamento dell’authoring del prodotto e interruzione del servizio - Riavvio frequente dei pod - Avvisi di stato
* SITES-19790 - MSM - Live Copy - Informazioni di anteprima errate dopo la creazione della Live Copy
* SITES-20086 - MSM - Live Copy - Il rollout MSM per CF in Assets eseguirà il rollout di tutte le Live Copy anche se è selezionata una Live Copy per cui effettuare il rollout
* SITES-20088 - MSM - Live Copy - Pagina vuota Problema dopo il rollout XF in Proprietà - AEM as a Cloud Service
* SITES-16854 - Editor pagina - La sovrapposizione del target di rilascio riguarda i componenti con la funzione &quot;Seleziona pannello&quot;
* CQ-4355563 - Progetti - Il parametro del percorso è errato. Compilazione di &quot;?appId=aemshell&quot; per lo script di ricerca della casella in entrata del progetto
* SITES-16876 - Sito rapido - Distribuzione del tema - CSS e JS mancanti nelle pagine di anteprima 2
* SITES-18418 - Interfaccia utente amministratore Sites - La funzionalità Mostra/Nascondi per il widget del percorso non funziona correttamente quando il campo è obbligatorio
* SITES-19534 - Interfaccia utente amministratore Sites - Impossibile aprire la finestra di dialogo Autorizzazioni effettive dopo l’aggiornamento a AEM 6.5.19
* SITES-19203 - Editor modelli - Criterio modello modificabile Testo non allineato e pulsante di eliminazione sovrapposizione stili
* CQ-4354881 - WCM - Traduzione - Il percorso dei frammenti di contenuto è impostato sull’origine (en-us) quando i frammenti di contenuto sono tradotti come parte di una pagina
* CQ-4355289 - WCM - Traduzione - Nei Cloud Service di traduzione vengono visualizzati solo i primi 40 elementi
* CQ-4355866 - WCM - Traduzione - Errore di generazione del flusso di lavoro di traduzione per le pagine esistenti
* CQ-4355797 - Flusso di lavoro - Impossibile utilizzare il passaggio del flusso di lavoro OOTB
* GRANITE-48938 - Flusso di lavoro - L’autore presenta uno stato di &quot;pubblicazione in sospeso&quot; per le risorse. Problema nella nuova cache della mappa del payload persistente.
* GRANITE-49036 - Flusso di lavoro - Richiesta funzionalità | Possibilità di pianificare e configurare l’eliminazione dei pacchetti del flusso di lavoro
* SITES-17393 - Estensioni del flusso di lavoro - La pubblicazione della struttura del contenuto non riesce quando si utilizzano i moduli di avvio del flusso di lavoro per cq:Tag
* SITES-17759 - Estensioni del flusso di lavoro - Tree-Activation-Workflow per i tag non funzionanti in AEMaaCS
* FORMS-12411: sui dispositivi Android, la `Maximum Number of Characters Validation` non funziona per il componente Textbox del modulo adattivo.
* FORMS-13377: quando un utente tenta di aggiungere il font personalizzato e di eseguire la pipeline per configurarlo, l’operazione non riesce e viene visualizzato l’errore &quot;ContainersNotReady&quot;
* FORMS-13267: quando un utente aggiunge un componente Elenco a discesa Modulo adattivo, l’ID del menu a discesa non viene generato
* FORMS-13544: quando un utente aggiunge un componente Contenitore modulo adattivo con un layout della procedura guidata, questo non funziona correttamente durante la creazione del modulo
* FORMS-13091, FORMS-13414: se l’utente tenta di configurare un URL di dominio personalizzato nell’archiviazione BLOB di Azure, l’operazione non riesce
* FORMS-13595: quando un utente tenta di salvare il modulo in una posizione diversa, non è possibile visualizzare i pulsanti &quot;Seleziona cartella&quot; e &quot;Annulla&quot; se la risoluzione del browser è impostata su 100%. Tuttavia, l&#39;opzione è visibile quando la risoluzione è impostata su 75%
* FORMS-10952: quando un utente aggiunge un componente Elenco a discesa Modulo adattivo a un Modulo adattivo e utilizza la proprietà &quot;Imposta opzioni&quot; basata su varie regole personalizzate, la proprietà &quot;Imposta opzioni&quot; funziona solo per l’ultima regola
* FORMS-11471: il caricamento lento di un frammento non riesce quando la chiamata &quot;emitter.json&quot; non riesce a causa di un’interruzione della rete.
* FORMS-11786: quando un utente passa da un mese all’altro nel widget del calendario, il componente del selettore data mostra una riga in più.
* FORMS-12093, FORMS-12093: quando un utente seleziona la casella di controllo Modulo adattivo per inviare un modulo, il valore errato con un’opzione  `\` viene memorizzato nella casella di testo
* FORMS-11993: quando un utente fa clic su un’immagine utilizzando &quot;Scatta una foto&quot; nel componente Allegato su un dispositivo iOS, tutte le immagini vengono aggiunte alla cartella con lo stesso nome
* FORMS-12555: quando un utente tenta di integrare AEM Forms in una piattaforma di posta con un URL pubblicato dell’AEM, AEM Forms non aggiunge method=post durante il rendering della pagina. Questo problema si verifica anche se POST è impostato nell’azione di invio con l’URL. In questo modo la piattaforma di posta non lo riconosce come modulo
* FORMS-12938: i moduli HTML5 non funzionano o non vengono caricati correttamente nel browser Microsoft Edge con modalità di compatibilità IE
* FORMS-12032: quando un utente invia un modulo, il percorso dell’azione di invio non punta correttamente
* FORMS-12445: i valori errati vengono acquisiti nel modello dati del modulo dopo la modifica dell’ordine delle opzioni del pulsante di opzione e la pubblicazione del modulo.
* FORMS-12947: quando un utente aggiunge una nuova lingua a un dizionario esistente, l’operazione di unione o aggiunta non riesce
* FORMS-11363: quando un utente invia un modulo tramite Workspace, si verifica un problema di visualizzazione nelle tabelle durante il rendering
* FORMS-11756: quando un utente aggiunge le funzioni JavaScript di ES6 come `let` e `const` nelle funzioni personalizzate, l’editor di regole non si apre. Questa versione di manutenzione supporta ES10
* FORMS-13164: se l’utente genera un PDF, dopo l’invio vengono aggiunte righe vuote impreviste
* FORMS-13789: quando l’utente tenta di generare più PDF, l’API batch di output non riesce
* FORMS-11483: quando un utente converte PDF in PDF/A-2B o PDF/A-3B, la conversione non riesce e viene visualizzato un errore di convalida
* FORMS-10501: quando un utente richiama HSM, i documenti vengono certificati ma non abilita LTV
* FORMS-11546: quando un autore di moduli utilizza pannelli ripetuti in un modulo adattivo, l’attributo ARIA non è presente nei tag HTML. Ciò migliora l’accessibilità dei pannelli ripetuti dei moduli adattivi
* FORMS-11826: a causa delle etichette corrispondenti Arial® etichettate da e Arial®, gli assistenti vocali non sono in grado di distinguere tra queste due. Per risolvere il problema: l’etichetta &quot;aria-labelledby&quot; è sostituita da &quot;aria-descripedby&quot; per i campi modulo. F). Questo migliora l’accessibilità di Adaptive Forms
* FORMS-12626, FORMS-13094: gli utenti non possono accedere alla barra degli strumenti utilizzando la tastiera per salvare o modificare il contenuto nella pagina dell’editor di moduli. Questo problema di accessibilità è stato risolto
* FORMS-13102: durante il processo di authoring dei moduli, le icone disponibili nella pagina Forms e Documenti non dispongono di funzioni descrittive per utenti con caratteristiche diverse. Questo problema di accessibilità è stato risolto

### Problemi noti {#known-issues-15787}

* SITES-17934 - Frammenti di contenuto - Anteprima non riuscita a causa della protezione DoS per una grande struttura ad albero di frammenti. Consulta [KB](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945)

### Funzioni e API obsolete {#deprecated-15787}

* [Credenziali JWT nella console Adobe Developer obsolete](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Dai un&#39;occhiata a [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md) per sapere cosa è stato dichiarato obsoleto o rimosso in AEM as a Cloud Service.

### Notifica di modifica {#change-notice-15787}

**Azioni richieste**

#### Impostare la versione Java CM su 11 {#set-java-version-11}

La nuova versione di aem-sdk-api contiene classi compilate con una destinazione Java 11, che non è compatibile con l’ambiente di build predefinito di Cloud Manager versione 1.8 di JDK. Questo aggiornamento richiede l’esecuzione di Maven con JDK 11.

Si consiglia di aggiungere un file `.cloudmanager/java-version` nella directory principale del relativo archivio Git con il contenuto: `11`. Consulta [Ambiente di build/Impostazione della versione JDK di Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).


### Tecnologie incorporate {#embedded-tech-15787}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak API 1.60.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html?lang=it) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.24.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
