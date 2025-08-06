---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 0f16c31a5fea1fc538fbeabe6db182ad3a30560d
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 13%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 21772 {#21772}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 21772, rilasciata al pubblico il giovedì 6 agosto 2025. La versione di manutenzione precedente era la 21706.

Con la versione di attivazione funzioni 2025.8.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Nuove funzioni  {#new-features-21772}

* SITES-30049: è stato aggiunto un nuovo endpoint per il recupero delle copie per lingua di un frammento di contenuto tramite il relativo UUID.

### Miglioramenti {#enhancements-21772}

* CQ-4358722 : sono stati risolti i problemi di localizzazione causati da codici di localizzazione diversi tra Java 11 e Java 17.
* FORMS-19624: comunicazioni interattive (IC) abilitate. Consente alle organizzazioni di fornire comunicazioni personalizzate su richiesta, ad esempio rendiconti, fatture e corrispondenza, combinando modelli strutturati con dati dinamici. Grazie a funzioni quali la progettazione di modelli basati sul web, frammenti di contenuto riutilizzabili, varianti basate su regole e integrazione perfetta dei dati, IC consente comunicazioni con i clienti coerenti e scalabili tra i canali.
* FORMS-19587, FORMS-17107, FORMS-19591, FORMS-19582, FORMS-20129, FORMS-20002, FORMS-19593, FORMS-20655, FORMS-19583, FORMS-18024, FORMS-19581: Sono stati apportati i seguenti miglioramenti all’editor di regole per Forms adattivo:
   * Il metodo `validate` nell&#39;elenco delle funzioni ora può convalidare pannelli, campi e moduli.
   * È stata migliorata l’analisi delle funzioni personalizzate lato client per supportare le funzioni ES10+ e le importazioni statiche.
   * Nell’editor delle regole è stato aggiunto il pulsante &quot;Scarica documento di record (DoR)&quot; pronto all’uso.
   * È stato aggiunto il supporto per le variabili dinamiche all’interno delle regole.
   * Abilitazione della creazione di regole basate su eventi personalizzati.
   * Le regole per i pannelli ripetibili ora vengono eseguite nel contesto corretto, anziché solo sull’ultima istanza del pannello.
   * Le regole possono ora essere attivate in base a parametri di query, parametri UTM e parametri del browser.
   * È stato aggiunto il supporto per script di funzioni personalizzati specifici dei moduli in EDS (Experience Data Store).
   * È stato aggiunto il supporto per l&#39;utilizzo di `EVENT_PAYLOAD` nell&#39;azione &quot;Accedi a&quot; nel gestore operazioni riuscite dell&#39;editor di regole.
   * Le chiamate di funzione supportate all’interno dei parametri di input nell’editor di regole e le regole garantite non vengono salvate se nella chiamata di funzione mancano i parametri richiesti.
   * Sono state evidenziate le regole interrotte nell’interfaccia utente dell’editor di regole.
* FORMS-18450: reCAPTCHA V2 (incluso reCAPTCHA invisibile) è ora più semplice da configurare e utilizzare in Adaptive Forms. La configurazione viene ora gestita in un’unica posizione, semplificando l’abilitazione della protezione da posta indesiderata nei moduli.
* FORMS-18385: è stato aggiunto il supporto per la generazione AFP da XDP e per i dati in AEM Forms tramite il servizio di output.
* FORMS-17789: è stato aggiunto un pulsante predefinito nell’editor delle regole per scaricare un documento di record (DoR).
* FORMS-20313, FORMS-2896: è stato aggiunto il supporto per la proprietà `dorExclude` per disabilitare funzionalità specifiche nei moduli basati su componenti di base.
* FORMS-20262: gestiva allegati di file non validi (0 byte) sul lato client.
* FORMS-18347: è stata migliorata la registrazione dell’editor di Forms adattivo per i componenti proxy del contenitore di moduli mancanti.
* FORMS-16205: sono stati esclusi i componenti disabilitati dal documento di record (DoR) nei moduli basati su componenti di base.
* FORMS-10836: modifica dell&#39;orientamento delle proprietà della pagina master nel documento di record (DoR) per le lingue da destra a sinistra.
* SITES-33025: Apri un nuovo editor CF tramite ID invece del percorso.
* SITES-32741: attiva l’aggiornamento dei riferimenti di pagina dei frammenti di contenuto in modo asincrono.
* SITES-32087: GraphQL: aggiunta del supporto per `_ignoreCase` in StringArray.
* SITES-12211: Prestazioni migliorate nell’editor modelli
* SITES-32861: miglioramento delle prestazioni per la creazione di Live Copy tramite elaborazione a blocchi.
* SITES-21383: Ottimizzazione delle prestazioni per le operazioni di eliminazione dell’avvio dei frammenti di contenuto.
* SITES-31165: miglioramento delle prestazioni grazie alla suddivisione delle operazioni di rollout in blocchi gestibili.
* SITES-21353: Miglioramento delle prestazioni delle query per gli avvii di frammenti di contenuto tramite l’indicizzazione del database.
* SITES-30495: è stato migliorato il supporto dei riferimenti ai frammenti basati su UUID negli avvii di frammenti di contenuto.
* SITES-32151: il miglioramento dell’API espone la funzionalità della proprietà del contenitore.
* SITES-26849: regola i riferimenti retroversi quando una variante di frammento di contenuto viene spostata o eliminata.
* SITES-31846: Aggiungi l’opzione per copiare/incollare il frammento principale e i riferimenti nella stessa cartella per l’operazione di copia della struttura.
* SITES-30241: regola i riferimenti che si trovano all’interno di un campo di testo lungo durante lo spostamento, la ridenominazione o l’eliminazione di un frammento.
* SITES-32684: migliora il meccanismo di sincronizzazione delle modifiche alle schede nello schema dell’interfaccia utente.
* SITES-33308: aggiungi un meccanismo di esecuzione di nuovi tentativi per sincronizzare le modifiche allo schema dell’interfaccia utente durante la modifica dei modelli.
* SITES-32247: Dialogo mancante, Disallineamento di Personalization e interfaccia utente nel componente &quot;Testo e Personalization&quot;.
* SITES-32261: Frammento di esperienza i18n non applicato al campo.
* SITES-32666: il predicato del modello contiene `\n` e la ricerca di HTML non riesce.
* SITES-32674: il selettore immagini per campi immagine in primo piano non funziona per la creazione guidata pagine nonostante `cq:showOnCreate`.
* SITES-32014: Edge Delivery con Universal Editor: aggiunta della configurazione automatica dei criteri CORS per localhost, aem.page e aem.live
* SITES-26532: Edge Delivery con Universal Editor: aggiunta del supporto per URL localizzati (accesso anticipato).
* SITES-30887: aggiungi gli UUID dei frammenti di contenuto memorizzati nei metadati del flusso di lavoro.

### Problemi risolti {#fixed-issues-21772}

* CQ-4360190: è stato corretto `UnsupportedOperationException` che si verificava durante il tentativo di utilizzare add su un keySet che non supporta l&#39;operazione.
* CQ-4360421: è stato risolto un problema con la crittografia della chiave di abbonamento a Microsoft Translator per migliorare la sicurezza e la compatibilità.
* FORMS-20980: sono stati risolti dei problemi di accessibilità della tastiera in Selezione data con formato di visualizzazione personalizzato in Adaptive Forms.
* FORMS-20498: è stata aggiunta una verifica delle eccezioni del puntatore null in OdataResponse per evitare errori di runtime.
* FORMS-20947: sono stati risolti diversi problemi di accessibilità, tra cui violazioni degli assistenti vocali e problemi di troncamento/sovrapposizione di testo.
* FORMS-21030, FORMS-20630: sono stati risolti dei problemi relativi ai campi a discesa configurati per selezioni multiple nei moduli adattivi. Il PDF generato ora include correttamente tutti i valori selezionati.
* FORMS-19579: è stato risolto il problema che impediva la correzione automatica della regola del servizio Invoke al salvataggio successivo.
* FORMS-20734: è stata corretta la duplicazione dei campi di firma nei documenti PDF generati dal servizio di output per i modelli di input PDF basati su XFAF.
* FORMS-20934: il menu a discesa Attributo riempimento automatico nell’interfaccia utente di authoring di AEM Forms è stato corretto per rimuovere le voci duplicate e includere tutti i token di completamento automatico standard di HTML.
* FORMS-20700: risolto lo sfarfallio del testo della guida a discesa al caricamento iniziale in AEM Forms.
* FORMS-20307: risolto il problema che impediva la traduzione dei moduli incorporati in una pagina del sito con lingue di 4 caratteri.
* FORMS-20493: risolto il problema relativo all’aggiornamento automatico dei moduli quando i dati venivano recuperati, causando inconvenienti all’utente.
* FORMS-18455: è stato migliorato l’editor di Forms adattivo per i componenti core in modo da visualizzare i punti per gli oggetti dati utilizzati nella struttura dell’origine dati.
* FORMS-19373: sono stati evitati gli errori di replica per gli ambienti di pubblicazione in cui non è configurato alcun agente di replica.
* FORMS-20042: è stata corretta la visualizzazione delle proprietà danneggiate causata dalla configurazione Apache Sling GET Servlet con la configurazione HTML abilitata.
* FORMS-20036, FORMS-19978: sono stati risolti i problemi di conformità e convalida di PDF/A-1b.
* FORMS-19166: spostamento di pagedatasource.jsp nel servlet per migliorare la chiarezza della traccia dello stack degli errori e aggiunta di ulteriori guardrail e registri.
* FORMS-16466: sono stati risolti dei problemi che impedivano il corretto popolamento dei pannelli ripetibili in AEM Forms.
* FORMS-19629: sono stati risolti dei problemi con l’analisi dello schema JSON del cliente che fornivano risultati non validi.
* LC-3923083: è stato risolto l’errore &quot;oggetto percorso non taggato&quot; per gli elementi con bordi nei modelli XDP.
* SITES-33177: Edge Delivery con Universal Editor: correggi gli stili di sezione interrotta se memorizzata come stringhe separate da virgola.
* SITES-33262: Edge Delivery con Universal Editor: correggi i blocchi senza proprietà name per interrompere il rendering e la pubblicazione della pagina.
* SITES-33309: Edge Delivery con Universal Editor: correggi `IllegalArgumentException` durante la scrittura su un foglio di calcolo con una barra nelle colonne.
* SITES-33408: Edge Delivery con Universal Editor: correggi I fogli di calcolo non vengono visualizzati come modificati dopo aver apportato modifiche.
* SITES-31992: GraphQL: correggi gli errori sporadici nella scansione del modello durante l’avvio dei bundle.
* SITES-29967: GraphiQL: i nomi di query lunghi sono tagliati.
* SITES-26266: i riferimenti ai contenuti che non iniziano con `/` non vengono restituiti dalla risposta BE (API Java).
* SITES-17874: query persistenti di GraphQL: correggi la codifica per il tipo di contenuto application/graphql-response+json.
* SITES-24506: gli assistenti vocali vengono informati sui risultati della ricerca.
* SITES-25268: miglioramenti agli assistenti vocali per le annotazioni.
* SITES-32366: i risultati del controllo ortografico sono nascosti dietro la finestra di dialogo dell’editor Rich Text.
* SITES-32829: miglioramenti all’emulatore MediaQuery per analizzare le query multimediali di livello 3 e 4.
* SITES-32278: assegna tag ai campi impostati per utilizzare correttamente l’etichetta del campo.
* SITES-25244: la barra orizzontale non viene più visualizzata nella finestra modale dell’immagine.
* SITES-33395: è stata corretta la funzionalità del pulsante di rollout per la sincronizzazione Live Copy dei frammenti di contenuto.
* SITES-33147: è stato corretto un problema di associazione del servizio che influiva sulla funzionalità delle relazioni live.
* SITES-33528: è stato risolto un problema di conservazione della marca temporale durante la promozione del lancio.
* SITES-33014: è stata corretta la generazione eccessiva di registri di avviso da LaunchesAdapterFactory.
* SITES-32305: è stata corretta la funzionalità di interruzione dell’ereditarietà della Live Copy dopo le modifiche al layout.
* SITES-32268: disabilita la codifica URL per la ricerca di frammenti di contenuto.
* SITES-32772: la proprietà bloccata nei campi della variante era sempre false quando si abilitavano i miglioramenti di SITES-31455 relativi all’unificazione del valore etag.
* SITES-32696: è stato corretto un problema a causa del quale non era più possibile modificare un campo Live Copy di un frammento di contenuto con ereditarietà interrotta.
* SITES-31712: query lente da Omni-search su prod Author.
* SITES-33039: gli eventi di pagina non si attivano correttamente.
* SITES-31192: i frammenti di esperienza perdono la cronologia della versione dopo essere stati spostati.
* SITES-33529: errore durante il collegamento dei modelli ACS Campaign con le pagine AEM.
* SITES-33678: Aggiungi/nascondi per SITES-33529.
* SITES-33468: AEMaaCS non è in grado di connettersi ad ACS.

### Funzionalità modificate {#altered-functionality-21772}

* SITES-26344: Unifica la convalida di `fragmentId`/`modelId` tra endpoint. Questi ID vengono ora convalidati e, se non sono validi, viene restituito un codice di stato 400.
* SITES-29598: Convalida i riferimenti ai frammenti di contenuto aggiunti nei campi di riferimento dei frammenti durante l’aggiornamento di un modello per frammenti di contenuto.

### Problemi noti {#known-issues-21772}

* SITES-31791: GraphQL dei frammenti di contenuto - Query non riuscita con &quot;Numero massimo di campi superato&quot;. Vedi [Articolo della Knowledge Base](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27231).

### Funzioni e API obsolete {#deprecated-21772}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-21772}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 35 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.


### Tecnologie incorporate {#embedded-tech-21772}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni supportate di Node.js](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

