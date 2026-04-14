---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d2c26a122bd2a0a970af7578932d88e6f93487d5
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 13%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 25194 {#25194}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 25194, rilasciata al pubblico il giovedì 1 aprile 2026. La versione di manutenzione precedente era la 24678.

Con la versione di attivazione delle funzioni 2026.4.0 viene fornito il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

>[!NOTE]
>
>Il 24893 sulla versione è stato reso privato.

### Miglioramenti {#enhancements-25194}

* ASSETS-65127: metadati personalizzati di eventi: è stata migliorata la gestione dei nomi dei metadati.
* ASSETS-63313: creazione automatica di collegamenti correlati per risorse esportate e elementi principali basati su manifesti C2PA.
* ASSETS-10995: limita il numero di risorse in uno zip di download.
* FORMS-24388: è stato aggiunto un ambiente di sviluppo locale per l’editor di comunicazione interattiva (IC) che consente agli sviluppatori di creare e testare configurazioni senza affidarsi a server condivisi. Questo miglioramento consente ai clienti aziendali di eseguire più rapidamente l’iterazione, ridurre le dipendenze dell’ambiente e migliorare la produttività complessiva dello sviluppo.
* FORMS-24014: è stato migliorato l’editor di regole per i componenti di file allegato in modo da supportare la combinazione di condizioni utilizzando la logica &quot;AND&quot;, ad esempio per consentire regole come &quot;Se l’allegato del file viene modificato e il pannello è valido, effettua questa operazione.&quot; In precedenza, non era possibile utilizzare condizioni aggiuntive con i file allegati; questo aggiornamento abilita definizioni di regole più complesse per supportare flussi di lavoro avanzati.
* FORMS-23571: è stata migliorata la visualizzazione grammaticale semplificata esistente per le regole dell’evento trigger aggiungendo, oltre agli eventi personalizzati, il supporto per gli eventi predefiniti (OOTB). In precedenza, gli utenti potevano utilizzare solo la grammatica semplificata per gli eventi personalizzati e dovevano passare tra le regole &quot;WHEN&quot; e &quot;ON TRIGGER EVENT&quot; per configurare gli eventi OOTB e personalizzati separatamente. Con questo aggiornamento, sia gli eventi OOTB che quelli personalizzati possono essere utilizzati nella stessa grammatica semplificata, semplificando la configurazione delle regole e riducendo la necessità di cambiare contesto.
* FORMS-24462: è stato aggiunto il supporto per il componente Scribble Signature nei componenti React Vanilla per Headless Adaptive Forms (AF). Questo miglioramento consente agli utenti di acquisire firme scritte a mano direttamente nei moduli basati su React, supportando i flussi di lavoro di firma digitale e le tempistiche di pubblicazione pianificate per i clienti aziendali.
* FORMS-24343: è stata aggiunta la gestione ottimizzata per `custom:setProperty` nel modello di modulo Notazione oggetto JavaScript (JSON), consentendo un&#39;elaborazione più rapida degli aggiornamenti delle proprietà dinamiche. Questo miglioramento migliora le prestazioni per Forms adattivo (AF) complessi che si basano su frequenti modifiche di runtime, garantendo interazioni utente più fluide e tempi di caricamento ridotti.
* FORMS-24358: è stato aggiunto il supporto per l&#39;utilizzo della proprietà `items` nella struttura JSON (JavaScript Object Notation) del modello invece di `:items` e `:itemsOrder`. Questo miglioramento consente agli sviluppatori di lavorare con un modello di dati più pulito e intuitivo che si allinea meglio alle convenzioni JSON comuni e semplifica l’integrazione con i sistemi esterni.
* FORMS-24087: è stato aggiunto il supporto per la definizione di regole ed eventi direttamente sui contenitori di frammenti in Adaptive Forms (AF). Questo miglioramento consente agli autori di applicare logica condizionale e interazioni a livello di contenitore, migliorando il riutilizzo e riducendo la necessità di duplicare le regole tra i singoli campi del frammento.
* FORMS-24440: aggiunta una nuova azione &quot;Rimuovi campo&quot; nel menu a discesa THEN dell’editor di regole per l’editor di comunicazioni interattive che consente agli utenti di rimuovere completamente un componente selezionato dal modulo quando viene soddisfatta una condizione della regola. Questo miglioramento supporta i flussi di lavoro che richiedono una ristrutturazione dinamica dei moduli invece di nascondere solo i campi, attivando comunque lo script `forms_ready` appropriato per un comportamento coerente.
* FORMS-23898: è stato aggiunto il supporto per la definizione delle variabili utilizzando la notazione `@` nell&#39;editor di comunicazione interattiva (IC), consentendo agli utenti di configurare le tabelle dinamiche in modo più intuitivo. Questo miglioramento semplifica la configurazione del contenuto delle tabelle basate su variabili e migliora la chiarezza durante la gestione dei dati dinamici nell’esperienza di authoring.
* FORMS-23702: aggiunta dell&#39;autenticazione basata su certificato per le connessioni SPL (SharePoint List) che consente un accesso più sicuro e basato su certificati ai dati SharePoint. Questo miglioramento consente alle aziende di soddisfare requisiti di sicurezza e conformità più severi, riducendo al contempo il ricorso all&#39;autenticazione basata su password.
* FORMS-23800: è stato aggiunto il supporto per l’override delle chiavi segrete reCAPTCHA nelle configurazioni sling, consentendo ai clienti aziendali di allinearsi ai propri requisiti di sicurezza e conformità. Questo miglioramento consente la gestione segreta delle chiavi specifica per l’ambiente, in modo che gli amministratori possano integrare reCAPTCHA in modo sicuro senza modifiche al codice.

### Problemi risolti {#fixed-issues-25194}

* ASSETS-62882: visualizzazione Amministratore: la descrizione comando info si interrompe quando vengono caricati più nomi di file non validi.
* ASSETS-63642: il collegamento di condivisione non riesce a eseguire il rendering della risorsa in alcuni ambienti di sviluppo (SLA3).
* ASSETS-59267: NPE durante il caricamento dei metadati dell’applicazione per il payload di consegna.
* ASSETS-59227: esportazione metadati: le proprietà non selezionate non sono più incluse a causa della corrispondenza regex.
* ASSETS-65187: anteprima CSV in Cloud quando i dati della colonna contengono virgole di escape.
* ASSETS-63441: assicurati che tutti gli utenti abbiano le autorizzazioni per leggere la configurazione di Assets Omnisearch.
* SITES-40095: Editor metadati: i riferimenti dei frammenti di contenuto locali superano le 10 voci.
* FORMS-24811: gli utenti hanno riscontrato problemi durante la gestione delle regole della logica dei moduli. Quando tentavano di modificare le regole create in precedenza, l’editor di regole non consentiva modifiche, obbligando gli utenti a ricreare le regole da zero e rallentando la manutenzione dei moduli.
* FORMS-24720: gli utenti hanno riscontrato problemi durante la configurazione delle variabili appena create in Adaptive Forms (AF). Quando aggiungevano regole a variabili con o senza associazione di dati, le regole non venivano salvate come previsto, obbligando gli utenti a ricreare la logica e rallentando i flussi di lavoro di creazione dei moduli.
* FORMS-24195: gli utenti hanno riscontrato un comportamento incoerente durante la reimpostazione dei campi a discesa in Adaptive Forms (AF). Quando in un elenco a discesa era configurato un segnaposto e il modulo o il componente veniva reimpostato, il campo diventava vuoto invece di tornare al valore del segnaposto, creando confusione circa le selezioni necessarie.
* FORMS-24718: gli utenti hanno riscontrato problemi di navigazione nell’editor di comunicazione interattiva (IC) quando si seleziona il pulsante Home. Invece di tornare all’interfaccia principale di Adobe Experience Manager (AEM), il pulsante non veniva reindirizzato come previsto, interrompendo il flusso di lavoro degli utenti che si spostavano tra l’editing IC e la schermata iniziale di AEM.
* FORMS-24810: al primo tentativo gli utenti hanno riscontrato errori intermittenti durante il caricamento dell’interfaccia utente adattiva (AUI) per i moduli. In alcune sessioni, il rendering della pagina iniziale non veniva eseguito correttamente, costringendo gli utenti ad aggiornare o riprovare prima di poter iniziare a compilare i moduli.
* FORMS-24520: nell’interfaccia utente dell’agente, gli utenti hanno riscontrato la mancanza di numeri di pagina nell’anteprima di stampa dei moduli tramite l’interfaccia utente adattiva (AUI). Quando gli agenti aprono l&#39;anteprima di stampa, a volte il campo del numero di pagina appariva vuoto, rendendo più difficile fare riferimento a pagine specifiche durante la revisione o la condivisione di copie stampate.
* FORMS-24532: gli utenti hanno riscontrato errori durante l’utilizzo della precompilazione del modello dati del modulo (FDM) con le configurazioni dell’elenco SharePoint `/teams`. Le organizzazioni governative che si basano su questi elenchi hanno visto i moduli caricarsi senza dati precompilati previsti, interrompendo i flussi di lavoro di raccolta dei dati e aumentando lo sforzo di immissione manuale.
* FORMS-24516: dopo un aggiornamento SDK in AEM Forms as a Cloud Service, nel documento record (DoR) degli utenti risultavano mancanti i dati della firma a mano. Quando i moduli sono stati firmati utilizzando l’opzione Scribble, il DoR generato non mostrava la firma acquisita, causando confusione e record incompleti per i clienti aziendali.
* FORMS-18631: gli utenti hanno riscontrato problemi di accessibilità con i layout a griglia nelle visualizzazioni desktop, tablet Responsive Web Design (RWD) e dispositivi mobili RWD. Quando si utilizza Chrome su Windows 11 con l’utilità di lettura dello schermo NVDA (NonVisual Desktop Access), nelle griglie mancavano ruoli e attributi appropriati, rendendo difficile per le tecnologie per l’accessibilità interpretare e navigare correttamente nel contenuto.
* FORMS-24798: gli utenti hanno riscontrato un comportamento incoerente durante l&#39;utilizzo delle condizioni `else` nelle regole di Adaptive Forms (AF) nell&#39;interfaccia utente di AEM Forms. Quando la condizione della regola primaria non è stata soddisfatta, le azioni `else` associate non sono state eseguite, determinando un comportamento diverso della logica del modulo e della visibilità del campo rispetto a quello configurato dagli autori.
* FORMS-24334: si sono verificati errori di precompilazione e problemi di unione JSON (JavaScript Object Notation) durante l’utilizzo di un modulo adattivo (AF) incorporato in Adobe Experience Manager (AEM) Forms as a Cloud Service. Durante il caricamento dei moduli migrati, i dati precompilati previsti non venivano visualizzati e il contenuto JSON unito era incompleto o errato. Questa operazione bloccava la migrazione da AEM 6.5 on-premise ad AEM Forms as a Cloud Service per gli ambienti interessati.
* FORMS-24441: gli utenti hanno riscontrato problemi con la configurazione del modello del documento di record (DoR) in Adobe Experience Manager (AEM) Forms as a Cloud Service. Quando si salvava un modello DoR personalizzato nell&#39;ambiente di sviluppo rapido, il modello tornava alla versione predefinita, impedendo loro di mantenere il layout e le impostazioni desiderate.
* FORMS-24393: gli utenti hanno avuto confusione quando i modelli precedenti continuavano a essere visualizzati come &quot;Senza titolo&quot; invece di mostrare nomi significativi. Questo rendeva difficile distinguere e riutilizzare i modelli esistenti durante il lavoro di authoring giornaliero.
* FORMS-24163: gli utenti hanno riscontrato dei problemi durante l’anteprima dei moduli versione 2 contenenti frammenti. In modalità anteprima, il contenuto del modulo non veniva riprodotto come previsto, impedendo agli utenti di convalidare il layout e il comportamento prima della pubblicazione.
* FORMS-24328: gli utenti hanno riscontrato che l’invio dei moduli non veniva completato quando utilizzavano reCAPTCHA v2 invisibile con l’opzione &quot;Convalida CAPTCHA per un’azione dell’utente&quot;. I clienti aziendali hanno notato che i moduli negli ambienti interessati non venivano inviati come previsto, interrompendo i flussi di lavoro di contatti e richieste di proposte.

#### AEM Guides {#guides-25194}

* GUIDES-38412 : Quando si modifica un file Schematron `(*.sch)` e si utilizza la funzione Trova e sostituisci, il pannello Trova e sostituisci appare parzialmente fuori schermo nella parte inferiore, impedendo l&#39;accesso ai relativi campi e controlli di input.
* GUIDE-37806: quando lo stesso argomento viene riutilizzato in più mappe con diversi predefiniti condizionali, la pubblicazione della mappa più recente in Salesforce sovrascrive il contenuto dell’argomento, causando la visualizzazione di dati errati agli utenti delle mappe pubblicate in precedenza.
* GUIDE-39394: quando un&#39;immagine inizialmente gestita come risorsa specifica per una lingua con una versione specifica (ad esempio, in `/en/`) viene spostata in una cartella globale con una versione aggiornata e viene eseguita un&#39;esportazione della linea di base, la nuova linea di base continua a fare riferimento a versioni obsolete specifiche per la lingua dell&#39;immagine, causando un&#39;esportazione della linea di base non riuscita.
* GUIDES-39054: durante la creazione di una linea di base dinamica, a volte l’editor non risponde a causa di più richieste API simultanee, causando l’arresto di tutte le altre operazioni.
* GUIDES-37781: quando si assegna un utente a un’attività di revisione, il menu a discesa elenca tutti gli utenti anziché solo quelli associati ai progetti selezionati, generando opzioni utente non valide.
* GUIDES-39385: quando si apre un rapporto per una mappa, si verifica un ritardo nel caricamento del pannello Filtri.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-25194}

Nessuna.

### Funzioni e API obsolete {#deprecated-25194}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-25194}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 9 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-25194}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,90,0 | [API Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache HTTPD 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.30.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
