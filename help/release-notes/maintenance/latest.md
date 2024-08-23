---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1eeb15c16581c945beb90495801c525697a46710
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 17465 {#release-17465}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 17465, rilasciata al pubblico il 14 agosto 2024. La precedente versione di manutenzione era la 17258.

Con la versione di attivazione della funzione 2024.8.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-17465}

* FORMS-15436 - Gestisci con cura l’eccezione nel modulo di pianificazione di Adobe Sign Status.
* FORMS-15362 - Aggiungi la configurazione per forms-foundation in aemds per abilitare l’accesso.
* FORMS-15261 - SPA non esegue il rendering nell’editor di Forms.
* FORMS-15138 - Gestione della compatibilità con le versioni precedenti di dati doppi a causa dell’aggiornamento Sling Commons JSON.
* FORMS-15113 - Modifica del nome della chiave in sid da visitorId per il tracciamento RUM.
* FORMS-15103 - Risorse allegate in un modulo non vengono pubblicate in Edge Delivery.
* FORMS-15082 - Schema JSON da mappare ai componenti del modulo adattivo personalizzato.
* FORMS-15002 - Registrazione del tipo di modello dei frammenti v1.
* FORMS-14845 - Supporto per xdpRef nel modulo delle basi dei componenti core tramite Forms Manager.
* FORMS-14840 - Errori del servizio di precompilazione dei moduli.
* FORMS-14836 - Migliora l’interfaccia utente di Forms Manager per elencare i modelli dei frammenti AF1.
* FORMS-14834 - Supporto dei modelli per i frammenti in AF1.
* FORMS-14275 - Sovrascrittura della pagina di ringraziamento e del messaggio di ringraziamento nel contenitore Incorpora.
* FORMS-13623 - Abilita la funzionalità basata sul tempo di salvataggio automatico per V2.
* FORMS-8651 - Finestra di dialogo di avviso sulla modifica della configurazione del modello dati nella pagina delle proprietà del modulo.
* SITES-23310 - API REST per frammenti di contenuto: impedisce dipendenze circolari nei riferimenti nidificati per frammenti di contenuto.
* SITES-23285 - API REST per frammenti di contenuto: crea un endpoint per elencare tutte le lingue disponibili.
* SITES-22857 - API REST per frammenti di contenuto: i campi di enumerazione della casella di controllo non devono consentire l’impostazione di più proprietà su false.
* SITES-22813 - API REST per frammenti di contenuto: definisci le proprietà min/max per i campi di enumerazione.
* SITES-22031 - API REST per frammenti di contenuto: ottieni i modelli di frammenti di contenuto consentiti per la cartella di un frammento.
* SITES-17640 - API REST per frammenti di contenuto: convalida dell’operazione di pubblicazione del frammento di contenuto.
* SITES-22677 - API REST per frammenti di contenuto: recupera un elenco semplice di riferimenti discendenti.
* SITES-22207 - Modello duplicato nella creazione di frammenti di contenuto.
* SITES-23093 - Eventi: aggiungi tag ai payload per gli eventi del modello per frammenti di contenuto.
* SITES-23092 - Eventi: aggiungi tag ai payload per gli eventi dei frammenti di contenuto.
* SITES-22447 - Aggiungi il supporto per l’ereditarietà delle proprietà dei frammenti di esperienza alla scheda Proprietà di base.
* SITES-12209 - Migliora le prestazioni dell’Editor criteri aggiungendo cq:policy all’indice.

### Problemi risolti {#fixed-issues-17465}

* CQ-4358028 - Impossibile creare il progetto se viene caricata la miniatura.
* CQ-4357891 - Problema di sequenza di XLIFF esportato.
* CQ-4357059 - Il completamento del processo di traduzione impiega ore causando il timeout 503 in AEMaaCS.
* FORMS-15320 - L’invio di e-mail non funziona nel modulo basato su componenti core.
* FORMS-15272 - AEM Forms: il gruppo di caselle di controllo invia solo un valore.
* FORMS-15269 - Problemi relativi al prodotto dopo la versione di manutenzione 16461.
* FORMS-15174 - Problema JsonSchemaParser isValid.
* FORMS-15095: la casella di testo su più righe può essere estesa oltre i pannelli contenitori in AEM Forms.
* FORMS-15057: l’elenco FDM Sharepoint genera un errore negli allegati per l’invio > 999.
* FORMS-15011: l’editor core causa un errore della console durante l’apertura di un modulo nell’editor.
* FORMS-14809: la cartella SDK non viene creata automaticamente all’interno della directory temporanea condivisa.
* FORMS-14327: API del servizio Forms: estrazione dati: fornisce un codice di risposta 500 quando viene fornito un pdf non interattivo nell’input.
* FORMS-7475: l’ordinamento non funziona sulla pagina di creazione dei moduli adattivi.
* FORMS-3309: se durante l’invio di un modulo sono selezionate più opzioni, viene visualizzata una sola opzione in un DoR generato.
* SITES-23646: l’endpoint dei modelli GraphQL non riesce per i modelli creati con OpenAPI se i campi contengono valori univoci.
* SITES-23637: API REST per frammenti di contenuto: OpenAPI non utilizza il tipo di valore corretto per le enumerazioni.
* SITES-23573: API REST per frammenti di contenuto: le relazioni live non vengono rispettate nei frammenti di contenuto GET da uuid.
* SITES-23535: API REST per frammenti di contenuto: i campi multipli dell’enumerazione del modello per frammenti di contenuto hanno valori vuoti.
* SITES-23534: API REST per frammenti di contenuto: ClassCastException nella convalida dei frammenti di contenuto.
* SITES-23524: adatta l’endpoint dei modelli BFF di GraphQL per supportare campi di enumerazione nei campi multipli.
* SITES-23467: API REST per frammenti di contenuto: i modelli di ricerca non riescono a causa di un problema del cursore.
* SITES-23327: ArrayIndexOutOfBoundsException in AuditLogTimelineEventProvider durante la descrizione dell’elaborazione dell’evento della timeline.
* SITES-23277: API REST per frammenti di contenuto: la verifica della relazione live del campo per frammenti di contenuto deve essere eseguita solo per le Live Copy.
* SITES-23232: la convalida personalizzata non funziona nella nuova interfaccia utente dell’editor CF.
* SITES-23090: API REST per frammenti di contenuto: impossibile aggiornare il titolo di un frammento di contenuto bloccato.
* SITES-22981: la promozione di un lancio nidificato non profondo non è una pubblicazione.
* SITES-22870: PathAttributesHandler.processSrcAttr ArrayIndexOutOfBoundsException.
* SITES-22814: API REST per frammenti di contenuto: i valori dei campi dei frammenti di enumerazione delle caselle di controllo devono essere ordinati in base alle chiavi definite nel modello.
* SITES-22716: problema con l’elenco di utilizzo live dei componenti OOTB.
* SITES-22457: la promozione di un lancio non profondo non comporta l’aggiornamento del contenuto sorgente.
* SITES-22449: impossibile salvare le modifiche nei frammenti di contenuto dopo l’aggiornamento AEM P20.
* SITES-22279: API REST per frammenti di contenuto: nel frammento di contenuto manca l’attributo univoco per i tipi di enumerazione.
* SITES-22203: API REST per frammenti di contenuto: allinea le API di gestione in modo che rispondano allo stesso modo per la stessa situazione.
* SITES-21973: API REST per frammenti di contenuto: nel modello manca l’attributo univoco per i tipi di enumerazione.
* SITES-20364: reindirizzamenti 302 non funzionanti con il selettore nell’URL.
* SITES-21198: VersionPreviewServlet: la pulizia viene eseguita contemporaneamente in tutti i nodi del cluster, causando conflitti di unione e commit di blocchi.

### Problemi noti {#known-issues-17465}

* ASSETS-40875: La classe AssetDeleteHandler ascolta gli eventi di eliminazione delle risorse ed esegue azioni specifiche in base al tipo di evento di eliminazione (PRE_DELETE o POST_DELETE). In alcuni scenari, il tipo di evento POST_DELETE causa un’eccezione NullPointerException.
* FORMS-14340: Errore nella creazione di un’istanza di FormsAndDocumentOmniSearchHandler e CloudStorageSubmitActionInserter. Queste sono innocue istruzioni di registro.
* FORMS-15818: Voce del descrittore del componente “OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml” istruzioni non trovate nei registri del server. Queste sono innocue istruzioni di registro.
* SITES-23662: L’utente che attiva una pubblicazione non può essere estratto dalle istruzioni di registro JCR nei registri del server. Questo è per una funzione in fase di sviluppo che potrebbe causare errori intermittenti e innocui di tipo “Impossibile trovare un ID utente valido nel batch di eventi OSGI” nel registro.

### Notifica di modifica {#change-notice-17465}

* A partire da settembre 2024, AEM as a Cloud Service disabiliterà la serializzazione dei Risolutori risorse tramite il framework Sling Model Exporter. Per ulteriori dettagli, consulta la [documentazione](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Funzioni e API obsolete {#deprecated-17465}

Si noti che è in corso l’aggiornamento di `com.day.cq.wcm.api` e con la versione corrente sono stati contrassegnati come `@Deprecated` alcuni dei relativi metodi e classi. Questi verranno rimossi nelle versioni future, quindi se utilizzi uno di questi, valuta di passare alle alternative suggerite.

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-17465}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 7 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-17465}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.66.0 | [API Oak API 1.66.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| API SLING AEM | 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.25.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
