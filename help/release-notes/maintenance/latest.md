---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: fa2da21ef6424bce0830d503eba650e1c1bf3dc2
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 98%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 17964 {#release-17964}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 17964, rilasciata al pubblico il 25 settembre 2024. La versione di manutenzione precedente era 17689. Le 17882 sulla versione sono state rese private a causa di un problema.

Con la versione di attivazione funzioni 2024.10.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-17964}

* ASSETS - 37750: [Priorità 4] [GraphQL] Supporto per gli URL di DM Scene7: ritagli avanzati delle immagini.
* CQ - 4354583: [AEMaaCS] Invio di eventi del processo di traduzione tramite la pipeline Adobe.
* CQ - 4357642: aggiornamento delle credenziali MSFT nel connettore OOTB.
* CQ - 4358217: deserializzazione del corpo delle richieste dall’entità delle richieste.
* CQ - 4358342: registrazione RequestProcessors su un solo metodo HTTP.
* FORMS - 10781: miglioramento dell’editor di regole per creare regole per l’elemento successivo/precedente in un pannello.
* FORMS - 14595: [Funzione senza browser] Valori mancanti nel DoR quando vengono utilizzati dati precompilati per calcolare il DoR per il rendering senza browser.
* FORMS - 15619: kit di traduzione aggiornato per AEM Forms.
* FORMS - 16113: [Adobe Sign] Impossibile aggiornare lo stato dell’accordo da parte di un altro utente.
* FORMS - 16155: [Editor di regole] Implementazione della funzione asincrona.
* GRANITE - 53872: sono state aggiunte nuove variabili env per l’ID client IMS.
* SITES - 23738: versione componenti core 2.27.0.
* SITES - 16610: Frammenti di contenuto: endpoint GET per i dettagli del lancio.
* SITES - 16614: Frammenti di contenuto: rebasing degli endpoint dei lanci.
* SITES - 16615: Frammenti di contenuto: promozione degli endpoint dei lanci.
* SITES - 24215: Frammenti di contenuto: implementazione dell’endpoint GET per origini dei lanci.
* SITES - 20336: Frammenti di contenuto: miglioramento della convalida quando si elimina un modello per frammenti di contenuto.
* SITES - 21090: Frammenti di contenuto: supporto di valori minimi/massimi frazionari per i campi numerici
* SITES - 21658: Frammenti di contenuto: aggiornamento per l’utilizzo di riferimenti UUID.
* SITES - 23054: Frammenti di contenuto: possibilità di copiare i modelli per frammenti di contenuto.
* SITES - 23264: Frammenti di contenuto: possibilità di creare uno schema statico di un modello.
* SITES - 23265: Frammenti di contenuto: esposizione dello schema statico di un modello tramite l’endpoint GET dello schema dell’interfaccia utente.
* SITES - 23266: Frammenti di contenuto: possibilità di aggiungere vincoli ai modelli per frammenti di contenuto.
* SITES - 23778: Frammenti di contenuto: la ricerca di modelli per frammenti di contenuto dovrebbe consentire la ricerca di modelli che non sono mai stati pubblicati.
* SITES - 23335: Frammenti di contenuto: supporto di riferimenti a risorse esterne.
* SITES - 24626: Frammenti di contenuto: RTC: autorizzazioni per la migrazione UUID: 2.
* SITES - 24786: Frammenti di contenuto: miglioramenti per l’endpoint `referencesTree`.
* SITES - 24833: Frammenti di contenuto: rimozione della convalida dell’input HTML rispetto a un elenco di tag HTML consentiti.
* SITES - 23380: GraphQL: utilizzo dell’API corretta per leggere i metadati delle risorse.
* SITES - 22864: [Edge Delivery] Editor universale con nuova integrazione della struttura di contenuto AEM H2 2024.
* SITES - 23583: Test di componenti di base non riusciti su Java 17.
* SITES - 23662: Eventi: l’utente che attiva una richiesta di pubblicazione non può essere estratto dalle istruzioni del registro JCR nei registri del server.
* SITES - 23301: Supporto per l’avvio di un nuovo flusso di lavoro per creare strutture di cartelle quando si creano traduzioni di frammenti di contenuto.
* SITES - 23336: Frammenti di contenuto: supporto di riferimenti a risorse esterne
* SITES - 24091: Pacchetto di contenuti MSM suddiviso: master.
* SITES - 2411 - isSourceRenderCondition: riduce il messaggio del registro degli errori in DEBUG.
* SITES - 24166: mitigazione delle risorse remote per l’editor dell’interfaccia utente touch.
* SITES - 24409: registra tutti i processori di richiesta su un solo metodo HTTP.
* SITES - 25008: migliora la gestione di PersistenceExceptions e dei problemi di autorizzazioni.
* SITES - 24821: [Xwalk] imposta aem.page / aem.live come predefinito.

### Problemi risolti {#fixed-issues-17964}

* CQ - 4356887: incoerenza nello stato del progetto di traduzione per Akamai Technologies Inc.
* CQ - 4357878: il framework di traduzione non imposta lo stato di errore in caso di errore di traduzione del fornitore.
* CQ-4358028 - impossibile creare il progetto se viene caricata la miniatura.
* CQ - 4358290: l’impostazione di Target NON funziona sulla pagina pubblicata.
* FORMS - 13173: disallineamento dell’elenco a discesa in Modulo adattivo > Editor regole > Campo Rilascia oggetto.
* FORMS - 13873: AFv2: (“-”) nel nome del componente risulta in un errore delle regole.
* FORMS-14340: errore nella creazione di un’istanza di FormsAndDocumentOmniSearchHandler e CloudStorageSubmitActionInserter.
* FORMS - 15363: nome visualizzato nell’editor di regole.
* FORMS - 15381: miglioramento dell’interfaccia utente per il messaggio Ambito di autorizzazione.
* FORMS - 15595: problema di interruzione di riga per il testo del consenso del componente TnC del modulo AEM.
* FORMS - 15623: AEMaaCS Forms: alternative per aggiornare più tabelle in Dynamics con One POST.
* FORMS - 15682: AEM Forms: impossibile associare DOR a Dynamics FDM.
* FORMS - 15799: la pagina Adobe Sign GovCloud Signature non esegue il rendering in iframe.
* FORMS - 15835: problema di riscrittura URL modulo post-invio.
* FORMS - 16091: consumo del Binary.java ristrutturato.
* FORMS - 16096: l’utente di Forms non ha accesso alla finestra di dialogo restendpoint.
* FORMS - 16139: aggiunta della registrazione richiesta per il DoR nel modulo di componenti core.
* FORMS - 6935: lo stato del componente attivo non dispone di un rapporto di contrasto 3 a 1.
* FORMS - 7018: l’elemento vuoto diventa attivo.
* GRANITE - 53028: NPE in ExternalProcessPollingHandler.
* GRANITE - 53907: impossibile identificare l’utente del servizio come utente con privilegi avanzati del flusso di lavoro.
* SITES - 24405: Frammenti di contenuto: le informazioni estese per le enumerazioni dovrebbero essere più resilienti
* SITES - 23024: Frammenti di contenuto: l’enumerazione non restituisce locked: true nei frammenti GET.
* SITES - 23269: Frammenti di contenuto: la creazione di frammenti di contenuto consente di impostare campi bloccati.
* SITES - 23337: Frammenti di contenuto: l’endpoint batch con `body` non riesce con l’eccezione di cast.
* SITES - 23474: Frammenti di contenuto: la paginazione dovrebbe escludere le risorse interrotte nei frammenti di contenuto di ricerca.
* SITES - 23615: Frammenti di contenuto: AuthoringInfo della copia del frammento di contenuto non aggiornato
* SITES - 23668: Frammenti di contenuto: la patch Live Copy con più campi non riesce con 400
* SITES - 23695: Frammenti di contenuto: la descrizione della scheda non è disponibile in UiSchema
* SITES - 23704: Frammenti di contenuto: enum con più valori non supportati in _extendedInfo
* SITES - 23781: Frammenti di contenuto: valori duplicati non consentiti nei campi di enumerazione
* SITES - 24150: Frammenti di contenuto: mancano i dati di authoring della versione di un frammento di contenuto sulla creazione
* SITES - 24230: Frammenti di contenuto: correggere il filtro dopo lo stato di replica `modified` nei modelli per frammenti di contenuto di ricerca
* SITES - 24233: Frammenti di contenuto: il filtro per `publishedBy` può includere risorse non pubblicate nei modelli per frammenti di contenuto di ricerca
* SITES - 24355: Frammenti di contenuto: la relazione Live non viene rispettata per la cartella creata Frammenti di contenuto
* SITES - 24816: Frammenti di contenuto: l’ordine dei messaggi ValidationStatus non è coerente.
* SITES - 23896: Eventi: più eventi si uniscono con un evento di spostamento di pagina
* SITES - 23899: Eventi: gli eventi di pagina vengono ritardati o non vengono generati
* SITES - 23961: Eventi: la creazione di modelli per frammenti di contenuto con riferimenti non riesce quando è presente la cartella di configurazione
* SITES - 23963: Eventi: a volte gli eventi di pagina eliminata non arrivano
* SITES - 23443: GraphQL: comportamento incoerente della query del cursore GraphQL.
* SITES - 10994: l’ordine di attivazione della tastiera non è logico.
* SITES - 16357: AEM: il pulsante viene troncato nella scheda Configurazione di Analytics dal menu Sites.
* SITES - 19836: il componente ghost nel contenitore viene visualizzato nelle istanze di pubblicazione e anteprima.
* SITES - 22348: la pagina Panoramica Live Copy non viene caricata se ci sono più di 100 Live Copy per un progetto.
* SITES - 22960: risolutore risorse non chiuso in ContentFragmentModelOmniSearchHandler.
* SITES - 23284: la codifica URL genera una finestra di dialogo vuota nel browser del percorso.
* SITES - 23505: i componenti mostrano URL non corretti quando la pagina viene spostata in un’altra posizione.
* SITES - 23574: impossibile visualizzare in anteprima/confrontare con le versioni correnti per molte pagine
* SITES - 23585: problema con il ripristino dell’ereditarietà per i componenti con nodo cq:responsive
* SITES - 23650: discrepanza nel conteggio dei collegamenti in entrata nell’ambiente di authoring AEM
* SITES - 23659: regressione di Content Language Servlet causata dall’attivazione/disattivazione di FT_* SITES - 9757
* SITES - 23759: le risorse aggiunte al frammento di esperienza non vengono pubblicate con i lanci
* SITES - 24025: i reindirizzamenti 302 in AEM restituiscono l’intestazione della posizione utilizzando DNS interno invece di DNS pubblico
* SITES - 24036: indagine necessaria per i caratteri persistenti in formato ASCII dell’editor Rich Text AEM
* SITES - 24317: la configurazione proxy non funziona con l’autenticazione di base
* SITES - 24918: [Xwalk] corregge gli errori 504 restituiti occasionalmente quando si utilizza l&#39;uscita IP dedicata.

### Problemi noti {#known-issues-17964}

* FORMS - 15818: la voce descrittore componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` non ha trovato istruzioni nei registri del server. Queste sono innocue istruzioni di registro.

### Funzioni e API obsolete {#deprecated-17964}

Si noti che è in corso l’aggiornamento di `com.day.cq.wcm.api` e con la versione corrente sono stati contrassegnati come `@Deprecated` alcuni dei relativi metodi e classi. Questi verranno rimossi nelle versioni future, quindi se utilizzi uno di questi, valuta di passare alle alternative suggerite.

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-17964}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 16 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-17964}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.68.0 | [API Oak API 1.68.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
