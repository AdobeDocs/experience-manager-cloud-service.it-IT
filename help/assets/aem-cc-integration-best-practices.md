---
title: Best practice per l’integrazione con [!DNL Adobe Creative Cloud]
description: Le best practice integrano un’implementazione Experience Manager con Adobe Creative Cloud per semplificare i flussi di lavoro di trasferimento delle risorse e ottenere la massima efficienza.
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration,Adobe Asset Link,Desktop App
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '3443'
ht-degree: 15%

---

# Best practice per l’integrazione di Adobe Experience Manager e Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

Adobe Experience Manager Assets è una soluzione di gestione delle risorse digitali (DAM) che può essere integrata con Adobe Creative Cloud per aiutare gli utenti DAM a collaborare con i team creativi, semplificando la collaborazione nel processo di creazione dei contenuti.

Adobe Creative Cloud fornisce ai team creativi un ecosistema di soluzioni e servizi per aiutarli a creare risorse digitali. Include applicazioni desktop e mobili, servizi cloud come l’archiviazione con sincronizzazione desktop o esperienza web, nonché marketplace come Adobe Stock.

Continua a leggere per scoprire quali integrazioni scegliere tra desktop e DAM di livello enterprise in base al tuo caso d’uso e quali sono le best practice associate per i flussi di lavoro di connessione.

>[!NOTE]
>
>L’Experience Manager su Creative Cloud condivisione cartelle è ora obsoleto e non viene più trattato di seguito. Adobe consiglia funzionalità più recenti, come Adobe Asset Link o l’app desktop Experience Manager, per fornire agli utenti creativi l’accesso alle risorse gestite in Experience Manager.

## Necessità di collaborazione tra creativi, esperti di marketing e utenti DAM {#collaboration-need-of-creatives-marketers-and-dam-users}

| Requisiti  | Caso d’uso | Superfici interessate |
|---|---|---|
| Semplificare l&#39;esperienza per i creativi sul desktop | Semplificare l’accesso alle risorse da un DAM ([!DNL Assets]) per i creativi o, più in generale, per gli utenti desktop che lavorano in applicazioni native per la creazione di risorse. Hanno bisogno di un modo semplice e semplice per scoprire, utilizzare (aprire), modificare e salvare le modifiche all&#39;Experience Manager, nonché caricare nuovi file. | desktop Win o Mac; Creative Cloud app |
| Fornire risorse pronte all’uso di alta qualità da [!DNL Adobe Stock] | Gli addetti al marketing contribuiscono ad accelerare il processo di creazione dei contenuti fornendo assistenza per l’origine e l’individuazione delle risorse. I professionisti creativi utilizzano le risorse approvate direttamente dai propri strumenti creativi. | [!DNL Assets]; [!DNL Adobe Stock] mercato; campi metadati |
| Distribuire e condividere le risorse per organizzazioni | I dipartimenti interni/le filiali locali e i partner esterni, i distributori e le agenzie utilizzano le risorse approvate condivise dall&#39;organizzazione madre. L&#39;organizzazione desidera condividere in modo sicuro e senza soluzione di continuità le risorse create per un riutilizzo più ampio. | [!DNL Brand Portal], [!DNL Asset Share Commons] |
| Genera automaticamente varianti predefinite delle risorse caricate | Elabora automaticamente le risorse sfruttando l’esclusiva tecnologia di gestione e trasformazione dei contenuti multimediali di Adobe per azioni predefinite. Crea una logica personalizzata per definire le tue azioni tramite API e microservizi per le risorse. | [!DNL Assets] - Interfaccia utente |

## Offerte di Adobe per supportare le esigenze di collaborazione {#adobe-offerings-to-support-the-collaboration-need}

| Proposta di valore per i soggetti coinvolti | offerta Adobe | Superfici interessate |
|---|---|---|
| Gli utenti creativi scoprono le risorse da [!DNL Experience Manager], aprilo e utilizzali, modifica e carica le modifiche in [!DNL Experience Manager], nonché carica nuovi file in [!DNL Experience Manager]senza lasciare il loro [!DNL Creative Cloud] app. | [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator e InDesign. |
| Gli utenti aziendali semplificano l’apertura e l’utilizzo delle risorse, la modifica e il caricamento delle modifiche a [!DNL Experience Manager]e il caricamento di nuovi file in [!DNL Experience Manager] dall’ambiente desktop. Utilizzano un’integrazione generica per aprire qualsiasi tipo di risorsa nell’applicazione desktop nativa, inclusi quelli non Adobi. | App desktop [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | App desktop Experience Manager su desktop Win e Mac |
| Gli addetti al marketing e gli utenti aziendali possono individuare, visualizzare in anteprima, concedere in licenza e salvare le risorse Adobe Stock e gestirle dall’interno di Experience Manager. Le risorse concesse in licenza e salvate forniscono metadati selezionati di Adobe Stock per una migliore governance. | [Integrazione di Experience Manager e Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interfaccia web |
| Migliorare la collaborazione tra designer di prodotti digitali e addetti al marketing. Consentono ai designer di utilizzare le risorse digitali nei modelli di progettazione e wireframe su Adobe XD canvas. | [[!DNL Adobe Asset Link] per [!DNL Adobe XD]](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| Gli addetti al marketing possono creare automaticamente varianti e derivati in base alle risorse caricate e alle azioni predefinite create utilizzando la personalizzazione. Utilizza questa automazione per migliorare la velocità dei contenuti e ridurre lo sforzo manuale. | [Automazione dei contenuti](/help/assets/cc-api-integration.md) | [!DNL Experience Manager Assets] interfaccia web |

Questo articolo si concentra principalmente sui primi due aspetti delle esigenze di collaborazione. La distribuzione e l’approvvigionamento delle risorse su scala viene brevemente citata come caso d’uso. Per tali esigenze, valuta prodotti come Adobe Brand Portal o Asset Share Commons. Soluzioni alternative come [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), soluzioni che possono essere create in base a [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) componenti, [Condivisione collegamenti](share-assets.md), utilizzando [Interfaccia web Experience Manager Assets](/help/assets/manage-digital-assets.md) devono essere riesaminati sulla base di requisiti specifici.

![Creative Cloud connessioni, ad Experience Manager: Decidere quale funzionalità utilizzare](assets/creative-connections-aem.png)

Decidere su quale funzionalità utilizzare

### Mappatura dei casi d’uso e delle soluzioni di Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso d’uso | Adobe Asset Link | App desktop Experience Manager | Osservazioni o metodi alternativi |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Scopri - sfogliare le cartelle | Sì | Experience Manager Interfaccia web + azioni desktop | Quando esplori la condivisione di rete, disattiva le miniature per evitare di scaricare file binari di risorse. |
| Scopri - accedere alle raccolte | Sì | Experience Manager Interfaccia web + azioni desktop |  |
| Scopri - Cercare risorse | Sì | Experience Manager Interfaccia web + azioni desktop |  |
| Utilizzo - Apri risorsa | Sì | Sì - per qualsiasi app | [Apri da interfaccia Web](/help/assets/manage-digital-assets.md#previewing-assets) o dal Finder |
| Utilizzo: posizionamento di una risorsa dall’Experience Manager in un documento | Sì - incorporazione | Sì: collegamento o incorporamento | L’app desktop Experience Manager consente di accedere alle risorse come file nel file system locale. Questi collegamenti nelle app native sono rappresentati da percorsi locali. |
| Modifica : aperto per la modifica | Sì - Azione di ritiro | Sì - Azione aperta (nella condivisione di rete) | [Check-out in AAL](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) salva la risorsa nell’account di archiviazione creative cloud dell’utente (sincronizzato da app Creative Cloud) per impostazione predefinita. |
| Modifica : lavoro in corso al di fuori dell’Experience Manager | Sì: risorsa disponibile nell’account di archiviazione Creative Cloud dell’utente sincronizzato con il desktop. | Sì |  |
| Modifica - Carica modifiche | Sì - [Azione di archiviazione](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) con commento opzionale | Sì |  |
| Carica - file singolo | Sì - carica il documento attivo corrente | Sì | [Caricare tramite interfaccia web](/help/assets/manage-digital-assets.md#uploading-assets) |
| Caricamento: più file / strutture di cartelle gerarchiche | No | Sì | [Caricare tramite interfaccia web](/help/assets/manage-digital-assets.md#uploading-assets); Strumento o script personalizzato |
| Varie - utente e accesso | Viene riconosciuto l’accesso dell’utente Creative Cloud all’app desktop Creative Cloud (SSO) | Experience Manager utente/accesso | Gli utenti di entrambe le soluzioni contano sulla quota utente Experience Manager. |
| Varie - rete e accesso | Richiede l&#39;accesso dal desktop dell&#39;utente all&#39;implementazione di Experience Manager tramite rete | Richiede l&#39;accesso dal desktop dell&#39;utente all&#39;implementazione di Experience Manager tramite rete | Adobe Asset Link non condivide l’ambiente proxy di rete. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

Per supportare i casi di utilizzo della distribuzione delle risorse, considera le seguenti opzioni:

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) per un componente aggiuntivo configurabile per Assets per pubblicare le risorse.

* Le soluzioni personalizzate vengono create in base a [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) base di codice.
* Experience Manager [condivisione di collegamenti](/help/assets/share-assets.md) per condividere risorse ad hoc utilizzando i collegamenti.
* [Interfaccia web di Assets](/help/assets/manage-digital-assets.md) con aree per soggetti esterni protette dalla configurazione di Experience Manager Access Control e con le necessarie regolazioni di configurazione IT/rete, consentendo a questi utenti esterni di accedere all&#39;Experience Manager.

## Concetti chiave e casi d’uso {#key-concepts-and-use-cases}

### Glossario dei termini comuni {#glossary-of-common-terms}

* **Work-in-progress o creative work-in-progress (WIP):** una fase del ciclo di vita delle risorse in cui una risorsa subisce più modifiche e, in genere, non è ancora pronta per essere condivisa con team più grandi.
* **Creative-ready assets (Risorse pronte per i creativi):** risorse pronte per essere condivise con un team più ampio oppure che sono state selezionate o approvate dal team creativo per la condivisione con i team di marketing o LOB.

* **Asset approvals (Approvazioni risorse):** il processo di approvazione che viene eseguito per le risorse già caricate in DAM, che, in genere, include approvazioni del marchio, approvazioni legali e così via.
* **Final asset (Risorsa finale):** una risorsa che ha superato tutte le approvazioni/assegnazione tag dei metadati ed è pronta per essere utilizzata dal team più ampio. Tale risorsa viene memorizzata in DAM, per poi essere resa disponibile a tutti gli utenti (o a tutti gli interessati). Può essere utilizzata nei canali di marketing o dai team creativi per la creazione di design.

* **Minor asset update/change (Aggiornamento/modifica risorsa secondaria):** una modifica rapida e piccola a una risorsa digitale. Spesso viene effettuata in risposta a una richiesta di ritocco o di modifica minore, a una revisione delle risorse o all’approvazione (ad esempio: riposizionamento, modifica dimensioni del testo, regolazione di saturazione/luminosità, colore e così via).
* **Major asset update/change (Aggiornamento/modifica risorsa principale):** un passaggio a una risorsa digitale che richiede un lavoro considerevole e che a volte deve essere effettuato in un periodo di tempo più lungo. Generalmente include più modifiche. La risorsa deve essere salvata più volte durante l’aggiornamento. In genere, gli aggiornamenti principali delle risorse fanno sì che la risorsa entri in una fase WIP.
* **DAM:** gestione delle risorse digitali. In questo documento, è sinonimo di Experience Manager Assets, a meno che non venga espressamente indicato altrimenti.
* **Creative user (Utente creativo):** un professionista che crea risorse digitali utilizzando le app e i servizi Creative Cloud. In alcuni casi, è possibile che un utente creativo sia membro di un team creativo che utilizza Creative Cloud, ma che non crea risorse digitali, ad esempio un direttore creativo o un manager del team creativo.
* **DAM user (Utente DAM)**: utente tipico di un sistema DAM. A seconda dell’organizzazione, un utente DAM può essere di marketing o non, come un utente Line-of-Business (LOB), un bibliotecario, un venditore e così via.

### Considerazioni sull’utilizzo dell’integrazione di Experience Manager e Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Questo è un breve riepilogo delle best practice per l’integrazione di Experienci Manager e Creative Cloud. Leggi il resto di questo documento per ottenere la comprensione dettagliata di questi.

* **Per gli utenti creativi che lavorano in Photoshop, InDesign o Illustrator:** Adobe Asset Link offre la migliore esperienza utente possibile, inclusa la gestione del Work-in-progress sulle risorse estratte da Experience Manager
* **Per semplificare l’accesso alle risorse dal desktop per qualsiasi formato di file o applicazione generico:** utilizzare l’app desktop Experience Manager
* **Understand why and when to store assets in DAM (Scopri perché e quando archiviare le risorse in DAM)**: aggiornamenti da rendere disponibili al team più ampio della tua organizzazione
* **Mind the volume of assets shared (Considera il volume di risorse condivise):** se il caso d’uso è la distribuzione delle risorse, la governance e la sicurezza potrebbero diventare gli aspetti più importanti. Valuta l’utilizzo di strumenti creati per il lavoro in scala, come Brand Portal.
* **Understand asset lifecycle (Informazioni sul ciclo di vita delle risorse):** scopri come le risorse vengono gestite dai diversi team all’interno dell’organizzazione
* **Handle frequent saves to assets with care (Gestisci con attenzione i salvataggi frequenti nelle risorse):** Adobe Asset Link si occupa di questo aspetto con PS, AI, ID. Per altre applicazioni, non eseguire le attività WIP in cartelle condivise o mappate, a meno che non ti servano tutte le modifiche all’interno di DAM

### Accesso alle risorse Adobe Stock da Experience Manager Assets {#access-to-adobe-stock-assets-from-aem-assets}

[Integrazione di Experience Manager e Adobe Stock](/help/assets/aem-assets-adobe-stock.md) consente agli utenti di Experience Manager di cercare, visualizzare in anteprima, concedere in licenza e salvare le risorse da Adobe Stock in Experience Manager. Le risorse Adobe Stock concesse in licenza e salvate hanno selezionato i metadati Stock, che possono essere utilizzati per cercarli con filtri aggiuntivi.

Alcuni punti importanti su questa integrazione:

* Quando le risorse da stock di Adobe vengono salvate in Experience Manager, diventano un normale Experience Manager Assets, con file binario salvato nell’archivio Experience Manager. Alcuni metadati relativi ad Adobe Stock vengono salvati per la risorsa in Experience Manager, altrimenti il processo di acquisizione sarà lo stesso di qualsiasi altro file. Ad esempio, se Tag avanzati sono attivi, al momento del salvataggio questi tag vengono aggiunti a tali risorse.
* La risorsa salvata in Experience Manager è una copia, non un collegamento in Adobe Stock.

**Utilizzo delle risorse salvate da Adobe Stock in Experience Manager in Creative Cloud**. Questa integrazione è indipendente da Adobe Asset Link, ma Adobe Asset Link riconosce le risorse salvate da Stock in questo modo e visualizza metadati aggiuntivi e l’icona Stock su queste risorse nell’interfaccia utente dell’estensione Asset Link di Adobe in Photoshop, Illustrator o InDesign. I file sono disponibili per la navigazione, l’apertura e così via, perché sono normali risorse di Experience Manager quando vengono salvate in Experience Manager.
I creativi che lavorano nelle app Creative Cloud con estensione Adobe Asset Link presente, oltre ad avere accesso alle risorse già concesse in licenza da Adobe Stock in Experience Manager, possono anche utilizzare il pannello Creative Cloud librerie per cercare, visualizzare in anteprima e concedere in licenza le risorse Adobe Stock.
Le risorse di Adobe Stock concesse in licenza e salvate in Experience Manager diventano disponibili per i team più grandi che accedono all’implementazione Experience Manager Assets, mentre i creativi che concedono in licenza le risorse da Adobe Stock tramite il pannello Librerie Creative Cloud le rendono disponibili solo per impostazione predefinita nel loro account Creative Cloud.

## Informazioni sull’archiviazione delle risorse in un DAM {#about-storing-assets-in-a-dam}

Per progettare un flusso di lavoro efficiente tra team creativi e di marketing/line-of-business (LOB) e scegliere le migliori funzionalità di supporto, è importante comprendere quando e perché le risorse vengono memorizzate in DAM.

### Perché le risorse vengono memorizzate in DAM {#why-assets-are-stored-in-dam}

L’archiviazione delle risorse in DAM le rende facilmente accessibili e accessibili. Garantisce che le risorse possano essere sfruttate da numerosi utenti nell’organizzazione o nell’ecosistema, inclusi partner, clienti e così via.

La maggior parte delle organizzazioni sceglie di archiviare solo le risorse rilevanti per i processi di marketing/LOB a valle (pubblicazione su canali web come Experience Manager Sites o altri canali serviti da Adobe Experience Cloud - Marketing Cloud, Advertising Cloud e misurati da Analytics Cloud, fornitura a utenti/partner e così via). Inoltre, le organizzazioni memorizzano risorse che possono essere soggette a un processo di revisione/approvazione in DAM. In questo modo, DAM memorizza principalmente risorse che hanno alte probabilità di essere sfruttate ed evita di archiviare le risorse inattive.

La memorizzazione delle risorse è inoltre soggetta a considerazioni tecniche e relative all’utilizzo delle risorse. DAM fornisce servizi aggiuntivi sulle risorse memorizzate, tra cui l’estrazione dei metadati, il controllo delle versioni, la generazione di anteprime/transcodifica, la gestione dei riferimenti e l’aggiunta di informazioni sul controllo degli accessi. Questi servizi richiedono tempo e risorse aggiuntive per l&#39;infrastruttura.

Spesso, l’archiviazione di tutte le risorse e gli aggiornamenti non è auspicabile. Ad esempio, se gli aggiornamenti a risorse specifiche sono di scarsa qualità e consumano risorse eccessive, le risorse potrebbero non essere memorizzate in DAM.

#### Quando le risorse vengono memorizzate in DAM {#when-assets-are-stored-in-dam}

I team creativi (e le organizzazioni) solitamente non sono interessati a memorizzare le risorse in ogni fase del ciclo di vita delle risorse. Ad esempio, evitano di memorizzare le risorse nei seguenti casi:

* Risorse ancora da completare o oggetto di sperimentazione
* Risorse che non superano il ciclo di revisione creativo/interno del team
* Rispetto alla risorsa in questione, il team ha candidati migliori per rappresentare il proprio lavoro a team esterni

Di solito, le risorse delle classi seguenti vengono memorizzate in DAM:

* Attività che hanno raggiunto una certa scadenza e sono considerate pronte per essere condivise
* Risorse preselezionate dal team creativo
* Formati di risorse specifici utilizzabili o richiesti dal marketing, a seconda di un contratto o di un contratto specifico (ad esempio, file JPG convertiti da file RAW, TIFF/immagini da originali PSD)

#### Quando gli aggiornamenti alle risorse vengono memorizzati in DAM {#when-updates-to-assets-are-stored-in-dam}

Di regola, solo gli aggiornamenti alle risorse rilevanti per il set più ampio di utenti DAM devono essere archiviati in DAM. Assicura che gli utenti (marketing e funzioni simili) vedano solo le versioni rilevanti nella timeline delle risorse DAM.

In genere, le modifiche sono correlate alle fasi principali del ciclo di vita delle risorse. Ad esempio, la risorsa iniziale pronta per il marketing o un aggiornamento ufficiale basato su richiesta/revisione fornita dal team creativo devono essere memorizzati e controllati in versione in DAM.

L’aggiornamento del team creativo per la revisione da parte del team marketing dopo una richiesta di modifica della risorsa esistente in DAM è un esempio di aggiornamento rilevante. Deve essere memorizzato e modificato in DAM per ulteriori riferimenti o per ripristinare la versione precedente.

Di seguito sono riportati alcuni esempi di aggiornamenti che in genere non sono rilevanti:

* Versioni precedenti delle risorse caricate prima che sia pronto per la revisione del marketing
* Frequenti modifiche creative alla risorsa nella fase in corso di lavorazione prima che i team creativi e di marketing decidano che la risorsa è pronta

### Accesso utente a DAM {#user-access-to-dam}

Experience Manager Assets supporta due tipi di utenti in base al loro accesso alla distribuzione Experience Manager Assets. In genere, gli utenti all’interno della rete aziendale (firewall) hanno accesso diretto a DAM. Altri utenti esterni alla rete aziendale non avrebbero accesso diretto. Il tipo di utente determina quali integrazioni possono essere utilizzate dal punto di vista tecnico.

#### Utenti creativi con accesso diretto a DAM {#creative-users-with-direct-access-to-dam}

In genere, i team creativi interni o le agenzie/professionisti creativi caricati nella rete interna hanno accesso all’istanza DAM, incluso l’accesso Experience Manager. L&#39;infrastruttura di Experience Manager e di rete può essere impostata per consentire l&#39;accesso diretto a soggetti esterni - solitamente organizzazioni fidate come agenzie che lavorano per un cliente - per avere accesso ad Experienci Manager in rete, ad esempio tramite VPN o elenco Consentiti IP.

In questi casi, Adobe Asset Link o l’app desktop Experience Manager consente di accedere facilmente alle risorse finali/approvate e di salvare le risorse pronte per la creazione in DAM.

#### Utenti creativi senza accesso a DAM {#creative-users-without-access-to-dam}

Le agenzie esterne e i freelance senza accesso diretto all’istanza DAM possono richiedere l’accesso alle risorse approvate o desiderano aggiungere le loro nuove progettazioni al DAM.

Utilizza le seguenti strategie per fornire accesso alle risorse finali/approvate:

* Utilizza l’app desktop se Asset Link non funziona.
* Utilizzo [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) per la distribuzione sicura delle risorse ai partner esterni
* Utilizzare un&#39;implementazione personalizzata di un portale di distribuzione e determinazione origine basata su [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilizza il Controllo accessi configurato in Experience Manager e l&#39;infrastruttura di rete necessaria (ad esempio, l&#39;inserimento di VPN e IP nell&#39;elenco Consentiti) per consentire a parti esterne di accedere a un&#39;area dedicata di contenuto nel tuo DAM. Possono utilizzare l’interfaccia utente Web di Experience Manager per ottenere risorse e caricare nuovi contenuti nel DAM.

#### Lavori in corso sulle risorse dell’Experience Manager {#work-in-progress-on-assets-from-aem}

Come descritto in questo documento, si consiglia di eseguire aggiornamenti importanti sulle risorse, talvolta denominati work in progress, senza che tutte le modifiche salvate nel file locale vengano caricate in Experience Manager come modifiche. Questo consente di velocizzare il lavoro dell’utente desktop, limitare l’ampiezza di banda utilizzata e mantenere pulita la timeline delle risorse e concentrarsi su aggiornamenti principali controllati.

Adobe Asset Link offre un buon supporto per questo caso d’uso:

* Quando gli utenti di Photoshop, InDesign o Illustrator intendono modificare un file, eseguono un’operazione di estrazione sulla risorsa specificata
* La risorsa viene scaricata in background, inserita nell’account di Creative Cloud degli utenti sincronizzato su disco dall’app desktop Creative Cloud e il flag di estrazione viene attivato in Experience Manager sulla risorsa per ridurre al minimo i conflitti di modifica
* Da lì in poi, l&#39;utente lavora in un file memorizzato localmente nella posizione sincronizzata, e può continuare a lavorare e salvare le modifiche necessarie a qualsiasi frequenza richiesta
* Inoltre, poiché la risorsa si trova nell’account Creative Cloud, è disponibile anche su altri dispositivi di cui l’utente potrebbe disporre (ad esempio, possono essere aperti o modificati in un’app mobile Creative Cloud dedicata) e può essere condivisa con altri utenti di Creative Cloud a scopo di collaborazione.
* Al termine delle modifiche, l’utente creativo può eseguire un’operazione di Check-in sul file nella propria applicazione Creative Cloud, con un commento facoltativo. Le versioni della risorsa corrispondente in Experience Manager vengono impostate e aggiornate con il nuovo binario. Gli utenti di Experienci Manager come gli addetti al marketing o gli utenti LOB possono accedere a modifiche importanti delle risorse o a fasi cardine tramite l’interfaccia utente della timeline delle risorse di Experience Manager.

L’app desktop Experience Manager fornisce una condivisione di rete per le risorse aperte nell’app nativa. Per impostazione predefinita, tutte le modifiche eseguite localmente vengono caricate in Experience Manager automaticamente dopo un breve periodo di tempo. Con questa configurazione, i frequenti salvataggi durante la fase in corso di lavorazione verranno caricati in Experience Manager e versioni, creando un sacco di traffico di rete e potenziali problemi di scalabilità - per non parlare di versioni non necessarie in Experience Manager.

L’approccio consigliato consiste nell’utilizzare un’opzione nell’app desktop Experience Manager per disattivare gli aggiornamenti automatizzati e caricare manualmente le modifiche alle risorse da Experience Manager, sfruttando l’azione di caricamento delle modifiche nell’interfaccia utente dell’app Stato risorsa.

#### Caricamento in serie in DAM {#bulk-upload-to-dam}

Potrebbe essere necessario caricare contemporaneamente un numero maggiore di file in DAM in alcuni scenari, ad esempio:

* Caricamento dei risultati di fotografie o progetti di grandi dimensioni
* Caricamento delle risorse fornite dalle agenzie creative
* Caricamento di risorse selezionate da un set più grande se la selezione viene eseguita all’esterno di DAM

Questa descrizione fa riferimento al caricamento dei file operazionale (ad esempio, ogni settimana o con ogni servizio fotografico ), come parte normale del flusso di lavoro dell’utente desktop. Le migrazioni di risorse di grandi dimensioni non sono coperte qui.

Puoi sfruttare le seguenti funzionalità di caricamento:

* Per caricare in massa cartelle grandi/gerarchiche, utilizza l’app desktop Experience Manager che fornisce [caricamento di cartelle](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets) funzionalità. Puoi anche caricare strutture di cartelle gerarchiche. Le risorse vengono caricate in background, quindi non sono collegate a una sessione del browser web
* Per caricare alcuni file da una singola cartella, trascinali direttamente nell’interfaccia Web o utilizza l’opzione Crea nell’interfaccia Web di Experience Manager Assets.
* A seconda delle esigenze aziendali, puoi anche utilizzare caricatori personalizzati.

#### Gestione delle risorse digitali direttamente dal desktop {#managing-digital-assets-directly-from-desktop}

Se utilizzi Condivisione file di rete per gestire le risorse digitali, l’utilizzo della condivisione di rete mappata dall’app desktop Experience Manager potrebbe essere considerato un comodo sostituto. Durante la transizione dalle condivisioni di file di rete, l’interfaccia web di Experience Manager fornisce un set completo di funzionalità di Gestione delle risorse digitali che vanno ben oltre quanto possibile su una condivisione di rete (ricerca, raccolte, metadati, collaborazione, anteprime e così via), e l’app desktop Experience Manager fornisce un comodo collegamento per collegare l’archivio DAM lato server al lavoro sul desktop.

Evita di utilizzare l’app desktop Experience Manager per gestire le risorse direttamente nella condivisione di rete di Experience Manager Assets. Ad esempio, evita di utilizzare l’app desktop Experience Manager per spostare/copiare più file. Utilizza invece l&#39;interfaccia utente Web di Experience Manager Assets per trascinare le cartelle da Finder/Explorer alla condivisione di rete o utilizza la funzione Caricamento cartelle di Experience Manager Assets.
