---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 4b05f571904384521b79dbaf0fa5f4a3a75fef2b
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 13%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 24678 {#release-24678}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 24678, rilasciata al pubblico il giovedì 4 marzo 2026. La versione di manutenzione precedente era la 24464.

Con la versione di attivazione funzioni 2026.3.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-24678}

* FORMS-18927: è stato aggiunto il supporto per tipi MIME personalizzati ed estensioni di file nel componente AEM Forms File Attachment, consentendo agli utenti di allegare una più ampia varietà di tipi di documenti.
* FORMS-18211, FORMS-22936: gli utenti hanno riscontrato un problema di accessibilità a causa del quale le caselle di controllo non sono state raggruppate correttamente in un elemento `<fieldset>` e l&#39;etichetta del gruppo non è nidificata in un elemento `<legend>` come primo elemento secondario. Ciò ha interessato gli utenti con disabilità che si basano su assistenti vocali per la navigazione. Adaptive Forms, basato su Componenti core, ha ora introdotto il supporto per set di campi e legende per fornire un migliore supporto per l’accessibilità.
È stata aggiunta l’opzione Set di campi nel pannello, che consente agli utenti di organizzare e raggruppare in modo più efficace i campi correlati all’interno dei moduli.
* FORMS-23880: è stato aggiunto il supporto dell’Editor tema nei componenti core. Questo miglioramento consente agli utenti di personalizzare e gestire i temi in modo più efficiente all’interno dei componenti core, migliorando la flessibilità di progettazione e il flusso di lavoro.
* FORMS-21772: è stato aggiunto il supporto per il controllo delle versioni all’interfaccia utente di gestione Forms. Questo miglioramento consente agli utenti di creare e recuperare le versioni per Forms adattivo, frammenti di modulo, temi e Assets binari basati su Componenti core e Componenti di base, migliorando la gestione delle risorse e il controllo delle versioni.
* FORMS-23094: aggiunta dell’analisi lato client per Forms adattivo basato su Componenti di base, per consentire ai clienti aziendali di migrare i moduli al cloud. Questo miglioramento supporta le funzioni EcmaScript nelle regole dell’editor di codice, in precedenza non supportate, facilitando un processo di migrazione più fluido.
* FORMS-23853: è stato aggiunto il supporto per l’override di reCAPTCHA nel componente sling. Questo miglioramento consente agli utenti di personalizzare le impostazioni reCAPTCHA, migliorando la flessibilità e la sicurezza per i clienti aziendali.
* SITES-34936: Edge Delivery con Universal Editor: aggiungi filtri per frammenti di contenuto per modello per la pubblicazione.
* SITES-36203: Edge Delivery con Universal Editor: consente di aggiungere codice per abilitare il supporto per più campi e per più campi compositi.
* SITES-37037: Edge Delivery con Universal Editor: migliora l’importazione del foglio di calcolo per rilevare automaticamente il delimitatore.
* SITES-37804: Edge Delivery con Universal Editor: aggiunta del supporto per la creazione di gruppi di utenti chiusi (accesso anticipato).
* SITES-38990: Edge Delivery con Universal Editor: aggiunta del supporto per le esclusioni nelle mappature dei percorsi.
* SITES-39171: Edge Delivery con Universal Editor: aggiunta del supporto per `cq:tags` in blocchi ed elementi di blocco.
* SITES-40042: Edge Delivery con Universal Editor: impostare il servizio di configurazione come predefinito per i nuovi siti.
* SITES-37649: GraphQL: supporta il filtro dei campi di testo su più righe a livello JCR.
* SITES-37843: GraphQL: il filtro per i campi multivalore (raccolte) non è supportato a livello JCR.
* SITES-37540: Operazioni Replace e replaceAll per i valori dei campi CF (ricerca e sostituzione per un determinato nome di campo).
* SITES-37741: aggiungi la proprietà &quot;card&quot; nella risposta ottieni variante di frammento (vista a schede nell’interfaccia di amministrazione).
* SITES-37754: Pubblica cartella tramite API: convalida della struttura su richiesta quando `validateReferences` è impostato su true.
* SITES-37756: visualizza le informazioni sullo stato di archiviazione/estrazione di un frammento di contenuto.
* SITES-37805: Aggiornamento schema: i frammenti MODIFICATI non possono essere rinominati o spostati (documentazione).
* SITES-37847: sono state migliorate le prestazioni per la query SQL-2 del provider di riferimento per i contenuti prestati (recupero di LentContent).
* SITES-39255: aggiorna l’implementazione OpenAPI alle recenti modifiche API Java per il campo Composito.
* SITES-37096: rimuovi la lentezza della console Launches quando sono presenti nodi orfani.
* SITES-38117: trova un modo per eseguire query sugli avvii secondari senza impatto sulle prestazioni.
* SITES-38317: aggiunge ai metadati l’utente che ha avviato il flusso di lavoro (utente effettivo anziché generico se eseguito dall’utente del servizio).
* SITES-39203: visualizza l’utente che ha avviato il flusso di lavoro (anziché l’utente generico quando viene eseguito dall’utente del servizio).
* SITES-13083: Localizza le stringhe di errore nella finestra di dialogo Sites > Creazione Live Copy.
* SITES-13389: Localizza la stringa &quot;Creato versione di ... prima di promuovere il lancio&quot; in Sites > Timeline.
* SITES-16176: Localizza le stringhe in Editor pagina > Finestra di dialogo per configurazione del componente Image v3.
* SITES-35702: stringa &quot;Live Copy aggiornata con ereditarietà limitata&quot; non localizzata nella scheda &quot;Panoramica Live Copy&quot;.
* SITES-35748: etichetta della casella di controllo &quot;Abilita selezione variante prodotto&quot; non localizzata in &quot;Editor modello per frammenti di contenuto&quot;.
* SITES-35750: segnaposto &quot;SKU prodotto separati da `#` carattere&quot; non localizzato nel campo di input in &quot;Editor modello per frammenti di contenuto&quot;.
* SITES-37113: Finestra di dialogo &quot;Annulla ereditarietà&quot; non localizzata nella scheda &quot;Configurazioni CIF&quot;.
* SITES-25240: Correzione di accessibilità per il modale teaser di call to action.
* SITES-25531: Correzione di accessibilità per il contrasto dei colori nel modale di ricerca.
* SITES-37115: Icone troncate nel demo store di Vienia.

### Problemi risolti {#fixed-issues-24678}

* CQ-4361552: il dizionario JSON i18n è stato corretto e mantiene l’unicode con escape HTML nelle traduzioni di importazione.
* CQ-4361634: i frammenti di esperienza fissi non sono selezionabili o vengono aggiunti al progetto di traduzione.
* CQ-4362072: Flusso di lavoro di traduzione AEMaaCS fisso - DE > ES Il passaggio non riesce ad aggiungere la pagina al progetto di traduzione.
* FORMS-23741: gli utenti hanno riscontrato problemi in cui i passaggi di caricamento InvokeDDX e Asset non venivano eseguiti in serie, richiedendo due esecuzioni separate del flusso di lavoro. Questo problema interessava l’ambiente di produzione utilizzando AEM as a Cloud Service con il componente aggiuntivo Sites e Forms.
* FORMS-23877: gli utenti hanno riscontrato problemi con il mancato caricamento delle funzioni personalizzate in fase di runtime durante la creazione di moduli direttamente all’interno delle pagine Sites utilizzando una versione precedente dei Componenti core.
* FORMS-24038: gli utenti hanno riscontrato problemi con il pulsante di navigazione quando sono state aggiunte dinamicamente più schede.
* FORMS-23721: è stato risolto un problema che impediva la persistenza dei pattern di convalida configurati per gli input di testo nella finestra di dialogo Modifica. In precedenza, il valore del pattern veniva salvato ma non mantenuto o visualizzato nell’interfaccia utente, generando confusione per gli autori di moduli.
* FORMS-23456: gli utenti hanno riportato annunci errati da parte di assistenti vocali su dispositivi mobili relativi alle righe di intestazione nascoste in una tabella quando utilizzavano il componente Tabella in Adaptive Forms. Un’intestazione di tabella nascosta è stata annunciata fuori contesto, creando confusione per gli utenti che si affidano ad iOS VoiceOver e Android TalkBack.
* FORMS-23454: gli utenti hanno riscontrato problemi con il Selettore data per Forms adattivo basato su Componenti core. Quando si immettono date non valide, il sistema corregge automaticamente le possibili date chiuse.
* FORMS-23117: gli utenti hanno avuto esperienza con hCaptcha che non veniva tradotto correttamente in Forms adattivo basato su Componenti Foundation.
* FORMS-22634: gli utenti hanno riscontrato un problema a causa del quale gli allegati e-mail non venivano inclusi quando venivano utilizzate insieme le opzioni &quot;Includi allegato&quot; e &quot;Usa modello HTML&quot;.
* FORMS-23288: gli utenti hanno riscontrato problemi con Adaptive Forms incorporato nei moduli Asset Share Commons. Impossibile caricare correttamente il modulo quando l&#39;URL contiene `.html` nel percorso intermedio.
* FORMS-19198: gli utenti hanno riscontrato errori 404 durante l’incorporamento di moduli tramite le regole del dispatcher. Gli errori si sono verificati per URL come /etc.clientlibs/toggles.json, libreria rum e analyticsparserconfigparser.json, perché il rewriter dell’URL non è in grado di riscrivere questi URL.
* SITES-33799: Edge Delivery con Universal Editor: correzione rappresentazione video ottimizzata non pubblicata.
* SITES-35082: Edge Delivery con Editor universale: rimuovi i paragrafi vuoti, le interruzioni di riga iniziali e finali dai testi RTF.
* SITES-35524: Edge Delivery con Universal Editor: corregge gli errori di pubblicazione per i percorsi contenenti caratteri speciali non ASCII.
* SITES-38647: Edge Delivery con Universal Editor: correggere i colli di bottiglia delle prestazioni in ambienti con molti siti.
* SITES-40521: Edge Delivery con Universal Editor: Correggi i nomi di classi duplicati per blocchi ed elementi di blocco.
* SITES-37887: GraphQL: le ricerche UUID per set di risultati più grandi potrebbero causare tempi di risposta più lunghi.
* SITES-38412: impossibile applicare la patch ai frammenti nel lancio quando esiste un campo o una colonna univoca (il vincolo UNIQUE ora esclude i file CF nei lanci).
* SITES-38606: Errore di convalida durante l’aggiunta di una variante al CF con UUID di riferimento al frammento (CF idrati a cui fa riferimento l’UUID nelle varianti).
* SITES-39489: L&#39;interfaccia utente di Assets mostra i frammenti dalle cartelle cq:discarded (i file CF eliminati temporaneamente sono stati rimossi dalle risposte API di gestione).
* SITES-39517: GET CF con campo composito contenente enumerazione non riesce con errore 500.
* SITES-40072: i campi compositi con schede restituiscono valori segnaposto vuoti.
* SITES-39575: il salvataggio della Live Copy rimuove `cq:rolloutConfigs` - configurazione rollout persa.
* SITES-39694: Rollout di produzione non riusciti con NPE.
* SITES-39761: NavigationItem.getLink() restituisce null nel componente Navigazione di CIF v2.
* SITES-40519: il rollout MSM non riesce con NullPointerException quando la risorsa di destinazione Live Copy è null.
* SITES-17531: Stringa hardcoded &quot;Smart crop preview&quot; in Editor pagina > Immagine > Smart Crop.
* SITES-31575: La descrizione comando Info non è completamente visibile in Editor pagina > Componente Carosello > Proprietà.
* SITES-34215: il componente JS di completamento automatico genera un errore di convalida immediato nel campo percorso richiesto nella scheda della finestra di dialogo.
* SITES-35218: alcuni componenti core di AEM non riproducono correttamente il tag alt vuoto.
* SITES-37114: Descrizione comando &quot;Abilita supporto UID per il catalogo&quot; troncata nella scheda &quot;Configurazioni CIF&quot;.
* SITES-36138: Query senza indice rilevato (problema).
* SITES-37682: override del tipo di contenuto in `/libs/cq/Page/Page.css.jsp` e `/libs/cq/Page/Page.js.jsp.`
* SITES-38709: l’editor Rich Text per interfaccia classica mostra il codice HTML non elaborato dopo l’aggiornamento al 6.5.24.
* SITES-39630: gli aggiornamenti dei frammenti di contenuto nidificati non si riflettono nelle offerte Target esportate.
* SITES-39696: l’ora di attivazione/disattivazione per la pianificazione dell’attivazione/disattivazione non funziona.
* SITES-39824: L’esportazione di frammenti di esperienza in Adobe Target restituisce 500 (NPE).
* SITES-40253: errori intermittenti 500 in `/bin/cif/invalidate-cache` - conflitti Oak in `/var/cif/cacheinvalidation`.
* SITES-40341: Correggi le immagini in linea base64 negli stili del tag in `HtmlToJsonConvertorImpl`.

### Problemi noti {#known-issues-24678}

Nessuna.

### Funzioni e API obsolete {#deprecated-24678}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-24678}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 15 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-24678}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,90,0 | [API Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache HTTPD 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.30.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

