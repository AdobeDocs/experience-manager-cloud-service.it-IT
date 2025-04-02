---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 7d93af706d8b0556e9e26282d339794447eb0a41
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 21%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 20133 {#20133}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 20133, rilasciata al pubblico il mercoledì 1 aprile 2025. La versione di manutenzione precedente era la 19823.

Con la versione di attivazione funzioni 2025.4.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-20133}

* ASSETS-47850: limita l’aggiunta di configurazioni Scene7 se AEM CS è abilitato per ES.
* CQ-4359547: rimozione completa di Guava dall’archivio https://git.corp.adobe.com/target-sdk/tsdk-core.
* FORMS-17551: aggiunto supporto per documenti di record (DoR) per le integrazioni di elenchi SharePoint.
* FORMS-18432: è stata implementata la configurazione della precompilazione lato client specifica per il modulo (basata su regex) per abilitare la funzionalità di precompilazione selettiva senza modifiche a livello OSGI.
* FORMS-18513: è stato implementato il supporto per la trasformazione della struttura dati nel connettore AEP per migliorare le funzionalità della procedura guidata e la gestione dei dati.
* FORMS-19068: è stato aggiunto il supporto per le azioni di invio del connettore AEP nelle API di Forms Manager per migliorare le funzionalità di integrazione dei dati dei moduli.
* GRANITE-57717: aggiorna il bundle client in AEM.
* SITES-10469: AdapterFactory deve restituire sempre la stessa istanza PageManager.
* SITES-25130: versione dei Componenti core 2.28.0.
* SITES-25433: supporta il rendering a pagina intera quando si confrontano versioni precedenti.
* SITES-25923: LinkInfoStorageImpl può bloccarsi se non vengono più archiviati URL.
* SITES-26208: L’eliminazione di un frammento di contenuto tramite un flusso di lavoro ora consente di aggiornare le risorse di riferimento rimuovendo il frammento appena eliminato.
* SITES-26500: aggiunta dell&#39;opzione per spostare i frammenti di contenuto tramite il flusso di lavoro - `move-fragments`.
* SITES-26711: Attivatore rollout - I collegamenti non vengono aggiornati.
* SITES-27583: i frammenti di esperienza perdono la cronologia delle versioni dopo essere stati spostati.
* SITES-27618: la ricerca dei riferimenti di un frammento nelle pagine non restituisce tutti i risultati.
* SITES-27781: è stata implementata la convalida a livello di modello per i riferimenti ai frammenti di contenuto, che consente di convalidare i frammenti di riferimento in base ai vincoli di modello e al tag richiesto.
* SITES-27784: Aggiornare la generazione di query SQL per utilizzare la funzione PATH anziché `jcr:path`.
* SITES-28040: Adobe Target ExperienceFragmentsReplicationListener è danneggiato.
* SITES-28051: ottiene le autorizzazioni dell&#39;utente corrente per un frammento di contenuto: GET /cf/fragments/{fragmentId}/permissions.
* SITES-28190: Configurazione per il test di integrazione dell’anteprima.
* SITES-28227: quando si aggiungono risorse come riferimenti a un frammento, viene verificata l’esistenza della risorsa.
* SITES-28248: attiva/disattiva eventi Sites in base alla configurazione OSGI.
* SITES-28255: nome completo mancante in tutte e 3 le proprietà di controllo: creato, modificato, pubblicato.
* SITES-28390: PageImpl: Optimize hasContent().
* SITES-28404: L’eliminazione delle pagine sull’istanza di authoring dovrebbe comportare l’annullamento della pubblicazione da Anteprima servizio.
* SITES-28446: aggiunti 2 nuovi campi non visibili nella risposta, ovvero il segnaposto in NumberModelField e i modelli consentiti da LongTextModelField.
* SITES-28536: crea `RENAME` endpoint per frammenti di contenuto.
* SITES-28537: aggiunta dell&#39;opzione per rinominare i frammenti di contenuto tramite il flusso di lavoro - `rename-fragments`.
* SITES-28538: i riferimenti devono essere ripubblicati per mantenere contenuti validi per l’authoring e la pubblicazione.
* SITES-28549: crea `/cf/domains` per restituire l&#39;ID dominio basato sul livello AEM.
* SITES-29026: aggiunto un parametro facoltativo che specifica le impostazioni locali del frammento di contenuto, utilizzando una lingua e un codice paese.
* SITES-29031: è stata migliorata la logica per i frammenti PATCH-ing, fornendo così prestazioni migliori.
* SITES-29169: tutte le risorse pubblicate (indipendentemente dallo stato PUBBLICATO o MODIFICATO) verranno ripubblicate se fanno riferimento a una risorsa che è stata spostata, rinominata o eliminata.
* SITES-29376: Aggiungi codice per attivare o disattivare la convalida dell’eliminazione delle risorse pubblicate.
* SITES-29417: aggiorna /libs/cq/Page/proxy.jsp per inoltrare la richiesta a jcr:content, nodo invece di includere.
* SITES-2947: crea/modifica la visualizzazione kibana per confrontare i rasp di pubblicazione.
* SITES-29733: sono state migliorate le prestazioni della ricerca di modelli tramite tag di Frammenti di contenuto.
* SITES-8316: Criteri contenuto: memorizzare in cache ContentPolicyManager.
* SITES-24906: Edge Delivery con Universal Editor: supporta fogli di calcolo creati dall’autore senza una mappatura (accesso anticipato)
* SITES-24907: Edge Delivery con Universal Editor: supporto per la pubblicazione di Assets su più siti per casi di utilizzo MSM (accesso anticipato)
* SITES-27956: Edge Delivery con Universal Editor: migliorare la velocità effettiva di pubblicazione (accesso anticipato)
* SITES-27956: Edge Delivery con Universal Editor: migliorare la gestione degli errori per la pubblicazione su Edge Delivery Services (accesso anticipato)

### Problemi risolti {#fixed-issues-20133}

* CQ-4358378: Gestione degli errori di licenza nell’esecuzione della traduzione.
* CQ-4359263: nessun messaggio visualizzato nella finestra di dialogo al completamento del processo.
* CQ-4359386: impossibile aggiungere il dizionario i18n al progetto di traduzione in AEMaaCS.
* FORMS-18068: problemi di rendering del testo in grassetto nel documento record (DoR) per i gruppi di pulsanti di scelta e caselle di controllo che utilizzano campi in formato Rich Text.
* FORMS-18189: è stata modificata la gestione delle funzioni personalizzate per impedire la registrazione degli errori per le librerie client vuote e migliorare la visualizzazione degli errori nell’interfaccia utente.
* FORMS-18213: è stata implementata la funzionalità di nascondere/escludere i campi disabilitati dal documento record (DoR) per migliorare la chiarezza del documento e l’esperienza utente.
* FORMS-18271: l’Editor tema di Forms visualizza messaggi di errore non localizzati che influiscono sull’esperienza utente nella configurazione dei moduli e nella personalizzazione del tema.
* FORMS-18304: i documenti PDF/A-1b che passano la convalida in Acrobat e LiveCycle ES4 vengono erroneamente contrassegnati come non conformi in AEM 6.5 Forms a causa di errori di colore dipendenti dal dispositivo.
* FORMS-18325: aggiunta configurazione cloud di Adobe Experience Platform (AEP) per migliorare l’integrazione e le funzionalità di elaborazione dei dati dei moduli.
* FORMS-18360: gestione avanzata dell’ambito dell’elenco SharePoint per i team e i siti in Forms Document Management per migliorare l’organizzazione dei dati e il controllo degli accessi.
* FORMS-18375: i moduli basati su Componenti Foundation selezionano erroneamente le configurazioni recaptcha dalla cartella `conf/global` quando non è selezionato alcun contenitore di configurazione specifico.
* FORMS-18426: la funzionalità di ricerca elenco di SharePoint non riesce se i nomi degli elenchi contengono caratteri speciali (ad esempio, &quot;-&quot;), influendo sull’integrazione dei moduli con gli elenchi di SharePoint.
* FORMS-19028: la funzionalità di precompilazione lato client interrompe la gestione degli eventi dei moduli, impedendo la corretta attivazione degli eventi Value commit e DOMContentLoaded al caricamento del modulo.
* FORMS-6950: sono stati aggiunti i ruoli e gli attributi ARIA richiesti ai componenti treeview del navigatore del file system per migliorare l’accessibilità degli assistenti vocali e per conformarsi allo standard WCAG 4.1.2 per nome, ruolo e valore (livello A).
* FORMS-7016: l&#39;ordine di attivazione della tastiera nell&#39;editor moduli non segue la navigazione logica.
* SITES-1960: sono state migliorate le prestazioni dell’anteprima JSON dell’Editor frammento di contenuto.
* SITES-24308: la barra di scorrimento orizzontale viene visualizzata quando il contenuto viene ridimensionato al 400%.
* SITES-24493: l’elemento interattivo non ha il ruolo richiesto.
* SITES-24669: la barra di divisione della finestra della barra laterale dei riferimenti non è accessibile da tastiera.
* SITES-26881: bug nell’accessibilità di AEMaaCS: viene fornito un ruolo non corretto per l’icona &quot;Tre punti&quot; accanto al campo di input del commento.
* SITES-26956: Completare su SITES-24920 Impossibile spostare la pagina nell’ambiente di produzione.
* SITES-27707: L’elenco delle risorse di Content Finder non riesce a causa di problemi con i nomi delle risorse (regressione di 6.5 SP22).
* SITES-27757: Edge Delivery con Universal Editor: riscrivere le icone in base alla semantica helix-html-pipeline.
* SITES-27780: Il tag &lt;br> imprevisto viene visualizzato nell’editor Rich Text con Plaintext DefaultPasteMode in SP22.
* SITES-27958: Linkchecker genera errori &quot;Questa sessione è stata chiusa&quot;.
* SITES-28149: ExperienceFragmentLinkRewriterProvider personalizzato non attivato durante l’esportazione XF in Target.
* SITES-28449: bug dell’interfaccia utente del widget del flusso di lavoro - Includi elementi figlio che non visualizzano tutte le pagine figlie in AEM.
* SITES-28456: Notifica mancante nell’interfaccia utente in caso di salvataggio di una query persistente errata in GraphiQL Explorer (Follow up-SITES-28313).
* SITES-28464: aggiorna la query del frammento per utilizzare date formattate con millisecondi.
* SITES-28486: la modifica diretta nel nuovo Editor frammento di contenuto non viene reindirizzata al vecchio editor.
* SITES-28570: i metadati delle risorse mancanti vengono gestiti correttamente dal GraphQL dei frammenti di contenuto.
* SITES-28580: Interruzione di Classic Image Asset Finder dopo l&#39;aggiornamento a SP22.
* SITES-28600: Launches - Contenuto duplicato.
* SITES-28668: impossibile promuovere Launch con LaunchPromotionParameters.
* SITES-28820: il prefisso di lancio è stato aggiunto due volte all’interno della nuova variante creata al momento del rebase.
* SITES-28877: il servizio URL dell’UE genera un’eccezione quando l’endpoint dell’esternalizzatore locale non è definito.
* SITES-28956: l’operazione di eliminazione dei tag visualizza un avviso se ai tag fanno riferimento frammenti di contenuto.
* SITES-29208: i riferimenti e le varianti vengono restituiti correttamente nelle situazioni in cui un campo di riferimento contiene un percorso non valido.
* SITES-29363: il pulsante Reimposta Live Copy non funziona per la gerarchia dei contenuti della Live Copy nidificata.
* SITES-29369: Problema dell&#39;evento Assets all&#39;AIO | Attivazione Errata Degli Eventi Pubblicati/Non Pubblicati Della Pagina.
* SITES-29972: Le azioni Elimina e Rinomina a volte producono commenti non veri nei flussi di lavoro.

### Problemi noti {#known-issues-20133}

Nessuna.

### Funzioni e API obsolete {#deprecated-20133}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

#### Modifiche alla sincronizzazione di gruppi di utenti e profili di prodotto {#changes-user-groups}

Quando si utilizza Adobe Admin Console per la gestione delle autorizzazioni, i seguenti gruppi NON DEVONO essere utilizzati in quanto non saranno più sincronizzati con AEM:
* Gruppi AEM che terminano con _GROUP_NAME_SUFFIX.
* Profili di prodotto da altri ambienti, programmi o prodotti.

Per ulteriori dettagli, controlla [Modifiche alla sincronizzazione di gruppi di utenti e profili di prodotto](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).

#### Obsolescenza dell’editor SPA {#deprecate-spa-editor}

[L’editor SPA](/help/implementing/developing/hybrid/introduction.md) è stato dichiarato obsoleto per i nuovi progetti a partire dalla versione 2025.4.0. L’editor SPA rimane supportato per i progetti esistenti, ma non deve essere utilizzato per i nuovi progetti.

Gli editor preferiti per la gestione dei contenuti headless in AEM sono:

* [Editor universale](/help/edge/wysiwyg-authoring/authoring.md) per la modifica visiva.
* [Editor frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) per la modifica basata su modulo.

Ulteriori dettagli su questa rimozione sono disponibili nel documento [Deprecazione dell&#39;editor SPA.](/help/implementing/developing/hybrid/spa-editor-deprecation.md)

### Correzioni di sicurezza {#security-20133}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 34 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-20133}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.76.0 | [API Oak API 1.76.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2,28,0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
