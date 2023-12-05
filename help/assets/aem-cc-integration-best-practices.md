---
title: Best practice da integrare con [!DNL Adobe Creative Cloud]
description: Le best practice integrano un’implementazione di Experience Manager con Adobe Creative Cloud per semplificare i flussi di lavoro di trasferimento delle risorse e ottenere la massima efficienza.
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration,Adobe Asset Link,Desktop App
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '3431'
ht-degree: 14%

---

# Best practice per l’integrazione di Adobe Experience Manager e Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/aem-cc-integration-best-practices.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Adobe Experience Manager Assets è una soluzione di gestione delle risorse digitali (DAM) che può essere integrata con Adobe Creative Cloud per aiutare gli utenti DAM a collaborare con i team creativi, semplificando la collaborazione nel processo di creazione dei contenuti.

Adobe Creative Cloud fornisce ai team creativi un ecosistema di soluzioni e servizi per aiutarli a creare risorse digitali. Include applicazioni desktop e mobili, servizi cloud come l’archiviazione con sincronizzazione desktop o esperienza web e marketplace come Adobe Stock.

Continua a leggere per scoprire quali integrazioni scegliere tra desktop e DAM di livello Enterprise in base al tuo caso d’uso e quali sono le best practice associate per i flussi di lavoro di connessione.

>[!NOTE]
>
>L’Experience Manager sulla condivisione di cartelle Creative Cloud è ora obsoleto e non è più incluso in questo articolo. Adobe consiglia funzionalità più recenti, come Adobe Asset Link o l’app desktop Experience Manager, per consentire ai creativi di accedere alle risorse gestite in Experience Manager.

## Necessità di collaborazione per creativi, addetti al marketing e utenti DAM {#collaboration-need-of-creatives-marketers-and-dam-users}

| Requisiti | Caso d’uso | Superfici interessate |
|---|---|---|
| Esperienza semplificata per i creativi sul desktop | Accesso semplificato alle risorse da un DAM ([!DNL Assets]) per i creativi o, più in generale, per gli utenti che lavorano in applicazioni per la creazione di risorse native dal desktop. Hanno bisogno di un modo semplice per scoprire, utilizzare (aprire), modificare e salvare le modifiche in Experience Manager e caricare nuovi file. | Windows o Mac desktop; Creative Cloud app |
| Risorse pronte all&#39;uso di alta qualità da [!DNL Adobe Stock] | Gli addetti al marketing contribuiscono ad accelerare il processo di creazione dei contenuti fornendo assistenza per l’origine e il rilevamento delle risorse. I creativi utilizzano le risorse approvate direttamente nei loro strumenti creativi. | [!DNL Assets]; [!DNL Adobe Stock] marketplace; campi metadati |
| Distribuire e condividere le risorse per organizzazioni | Reparti interni/filiali locali e partner esterni, distributori e agenzie utilizzano le risorse approvate condivise dall’organizzazione principale. L’organizzazione desidera condividere in modo sicuro e fluido le risorse create per un riutilizzo più ampio. | [!DNL Brand Portal], [!DNL Asset Share Commons] |
| Genera automaticamente varianti predefinite di risorse caricate | Elabora automaticamente le risorse utilizzando l’esclusiva tecnologia di gestione dei supporti e trasformazione di Adobe per le azioni predefinite. Crea una logica personalizzata per definire le tue azioni utilizzando API e microservizi per le risorse. | [!DNL Assets] interfaccia utente |

## Adobi di offerte per supportare le esigenze di collaborazione {#adobe-offerings-to-support-the-collaboration-need}

| Proposta di valore per gli utenti tipo interessati | offerta Adobe | Superfici interessate |
|---|---|---|
| Gli utenti creativi scoprono le risorse da [!DNL Experience Manager], aprirle e utilizzarle, modificarle e caricarle [!DNL Experience Manager], e caricare nuovi file in [!DNL Experience Manager], senza lasciare il loro [!DNL Creative Cloud] app. | [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator e InDesign. |
| Gli utenti aziendali semplificano l’apertura e l’utilizzo delle risorse, la modifica e il caricamento delle modifiche in [!DNL Experience Manager], e caricamento di nuovi file in [!DNL Experience Manager] dall&#39;ambiente desktop. Utilizzano un’integrazione generica per aprire qualsiasi tipo di risorsa nell’applicazione desktop nativa, incluse quelle non di Adobe. | [[!DNL Experience Manager] App desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | App desktop Experience Manager su desktop Win e Mac |
| Gli addetti al marketing e gli utenti aziendali possono scoprire, visualizzare in anteprima, concedere in licenza e salvare le risorse di Adobe Stock, nonché gestirle direttamente da Experience Manager. Le risorse concesse in licenza e salvate forniscono metadati Adobe Stock selezionati per una migliore governance. | [Integrazione di Experience Manager e Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interfaccia web |
| Migliorare la collaborazione tra designer di prodotti digitali e addetti al marketing. Consenti ai designer di utilizzare le risorse digitali nei modelli di progettazione e wireframe nell’area di lavoro di Adobe XD. | [[!DNL Adobe Asset Link] per [!DNL Adobe XD]](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| Gli addetti al marketing possono creare automaticamente varianti e derivati in base alle risorse caricate e alle azioni predefinite create utilizzando la personalizzazione. Utilizza questa automazione per velocizzare le attività relative ai contenuti e ridurre il lavoro manuale. | [Automazione dei contenuti](/help/assets/cc-api-integration.md) | [!DNL Experience Manager Assets] interfaccia web |

Questo articolo si concentra principalmente sui primi due aspetti delle esigenze di collaborazione. La distribuzione e l’approvvigionamento delle risorse su scala viene brevemente citata come caso d’uso. Per tali esigenze, valuta prodotti come Adobe Brand Portal o Asset Share Commons. Soluzioni alternative come [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), soluzioni che possono essere create in base [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) componenti, [Condivisione collegamenti](share-assets.md), utilizzando [Interfaccia web di Experience Manager Assets](/help/assets/manage-digital-assets.md) devono essere riesaminati in base a requisiti specifici.

![Creative Cloud connessioni per Experience Manager: decidere quale funzionalità utilizzare](assets/creative-connections-aem.png)

Scelta della funzionalità da utilizzare

### Mappatura dei casi d’uso e soluzioni di Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso d’uso | Adobe collegamento risorsa | app desktop Experience Manager | Osservazioni o metodi alternativi |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Esplorare le cartelle | Sì | Interfaccia utente web e azioni desktop di Experience Manager | Durante la navigazione nella condivisione di rete, disattiva le miniature per evitare di scaricare file binari di risorse. |
| Individuare - accedere alle raccolte | Sì | Interfaccia utente web e azioni desktop di Experience Manager |  |
| Scoprire: cercare le risorse | Sì | Interfaccia utente web e azioni desktop di Experience Manager |  |
| Usa: apri risorsa | Sì | Sì, per qualsiasi app | [Apri da interfaccia Web](/help/assets/manage-digital-assets.md#previewing-assets) o dal Finder |
| Utilizzo: inserire la risorsa da Experience Manager in un documento | Sì - incorporamento | Sì - Collegamento o incorporamento | L’app desktop Experience Manager consente di accedere alle risorse come file sul file system locale. Questi collegamenti nelle app native sono rappresentati da percorsi locali. |
| Modifica: apri per la modifica | Sì - Estrai | Sì - Azione aperta nella condivisione di rete | [Check-out in AAL](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) salva la risorsa nell’account di archiviazione di creative cloud dell’utente (sincronizzato dall’app Creative Cloud) per impostazione predefinita. |
| Modifica - lavoro in corso al di fuori dell’Experience Manager | Sì - Risorsa disponibile nell’account di archiviazione Creative Cloud dell’utente sincronizzato con il desktop. | Sì |  |
| Modifica - Carica modifiche | Sì - [Azione di archiviazione](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) con commento facoltativo | Sì |  |
| Caricamento - file singolo | Sì - carica il documento attivo corrente | Sì | [Carica tramite interfaccia web](/help/assets/manage-digital-assets.md#uploading-assets) |
| Caricamento: più file/strutture di cartelle gerarchiche | No | Sì | [Carica tramite interfaccia web](/help/assets/manage-digital-assets.md#uploading-assets); Strumento o script personalizzato |
| Varie - utente e accesso | Riconoscimento SSO (Creative Cloud User logged in Creative Cloud Desktop app) | Experience Manager utente/accesso | Gli utenti di entrambe le soluzioni vengono conteggiati rispetto alla quota di utenti Experienci Manager. |
| Varie - Rete e accesso | Richiede l&#39;accesso dal desktop dell&#39;utente per l&#39;Experience Manager dell&#39;installazione in rete | Richiede l&#39;accesso dal desktop dell&#39;utente per l&#39;Experience Manager dell&#39;installazione in rete | Adobe Asset Link non condivide l’ambiente proxy di rete. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

Per supportare i casi di utilizzo della distribuzione delle risorse, considera le seguenti opzioni:

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) per un componente aggiuntivo configurabile per Assets per la pubblicazione delle risorse.

* Le soluzioni personalizzate vengono create in base a [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) base di codice.
* Experience Manager [condivisione collegamenti](/help/assets/share-assets.md) per condividere le risorse su richiesta tramite collegamenti.
* [Interfaccia web di Assets](/help/assets/manage-digital-assets.md) con aree per soggetti esterni protette dalla configurazione del controllo di accesso degli Experienci Manager e con le necessarie regolazioni di configurazione IT/di rete, che consentono a tali utenti esterni di accedere agli Experienci Manager.

## Concetti chiave e casi d’uso {#key-concepts-and-use-cases}

### Glossario dei termini più comuni {#glossary-of-common-terms}

* **Work-in-progress o creative work-in-progress (WIP):** una fase del ciclo di vita delle risorse in cui una risorsa subisce più modifiche e, in genere, non è ancora pronta per essere condivisa con team più grandi.
* **Creative-ready assets (Risorse pronte per i creativi):** risorse pronte per essere condivise con un team più ampio oppure che sono state selezionate o approvate dal team creativo per la condivisione con i team di marketing o LOB.

* **Asset approvals (Approvazioni risorse):** il processo di approvazione che viene eseguito per le risorse già caricate in DAM, che, in genere, include approvazioni del marchio, approvazioni legali e così via.
* **Final asset (Risorsa finale):** una risorsa che ha superato tutte le approvazioni/assegnazione tag dei metadati ed è pronta per essere utilizzata dal team più ampio. Tale risorsa viene memorizzata in DAM, per poi essere resa disponibile a tutti gli utenti (o a tutti gli interessati). Può essere utilizzata nei canali di marketing o dai team creativi per la creazione di design.

* **Minor asset update/change (Aggiornamento/modifica risorsa secondaria):** una modifica rapida e piccola a una risorsa digitale. Spesso viene effettuata in risposta a una richiesta di ritocco o di modifica minore, a una revisione delle risorse o all’approvazione (ad esempio: riposizionamento, modifica dimensioni del testo, regolazione di saturazione/luminosità, colore e così via).
* **Major asset update/change (Aggiornamento/modifica risorsa principale):** un passaggio a una risorsa digitale che richiede un lavoro considerevole e che a volte deve essere effettuato in un periodo di tempo più lungo. Generalmente include più modifiche. La risorsa deve essere salvata più volte durante l’aggiornamento. In genere, gli aggiornamenti principali delle risorse fanno sì che la risorsa entri in una fase WIP.
* **DAM:** gestione delle risorse digitali. In questo documento, è sinonimo di Experience Manager Assets, a meno che non venga espressamente indicato altrimenti.
* **Creative user (Utente creativo):** un professionista che crea risorse digitali utilizzando le app e i servizi Creative Cloud. In alcuni casi, è possibile che un utente creativo sia membro di un team creativo che utilizza Creative Cloud, ma che non crea risorse digitali, ad esempio un direttore creativo o un manager del team creativo.
* **DAM user (Utente DAM)**: utente tipico di un sistema DAM. A seconda dell’organizzazione, un utente DAM può essere di marketing o non, ad esempio un utente Line-of-Business (LOB), un bibliotecario, un venditore e così via.

### Considerazioni durante l’utilizzo dell’integrazione di Experience Manager e Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Questo è un breve riepilogo delle best practice per l’integrazione di Experience Manager e Creative Cloud. Leggi il resto del documento per informazioni dettagliate su questi.

* **Per gli utenti creativi che lavorano in Photoshop, InDesign o Illustrator:** Adobe Asset Link offre la migliore esperienza utente possibile, inclusa la gestione del Work-in-progress sulle risorse estratte da Experience Manager
* **Per semplificare l’accesso alle risorse dal desktop per qualsiasi formato di file o applicazione generica:** usa l’app desktop Experience Manager
* **Understand why and when to store assets in DAM (Scopri perché e quando archiviare le risorse in DAM)**: aggiornamenti da rendere disponibili al team più ampio della tua organizzazione
* **Mind the volume of assets shared (Considera il volume di risorse condivise):** se il caso d’uso è la distribuzione delle risorse, la governance e la sicurezza potrebbero diventare gli aspetti più importanti. Valuta l’utilizzo di strumenti creati per il lavoro in scala, come Brand Portal.
* **Understand asset lifecycle (Informazioni sul ciclo di vita delle risorse):** scopri come le risorse vengono gestite dai diversi team all’interno dell’organizzazione
* **Handle frequent saves to assets with care (Gestisci con attenzione i salvataggi frequenti nelle risorse):** Adobe Asset Link si occupa di questo aspetto con PS, AI, ID. Per altre applicazioni, non eseguire le attività WIP in una cartella condivisa/mappata a meno che non siano necessarie tutte le modifiche in DAM

### Accesso alle risorse di Adobe Stock da Experience Manager Assets {#access-to-adobe-stock-assets-from-aem-assets}

[Integrazione di Experience Manager e Adobe Stock](/help/assets/aem-assets-adobe-stock.md) consente agli utenti Experienci Manager di cercare, visualizzare in anteprima, concedere in licenza e salvare le risorse da Adobe Stock in Experience Manager. Le risorse Adobe Stock concesse in licenza e salvate hanno selezionato metadati Stock che possono essere utilizzati per cercarli con filtri aggiuntivi.

Alcuni punti importanti su questa integrazione:

* Quando le risorse vengono salvate in Experience Manager, diventano un normale Experience Manager Assets Experience Manager, con file binari salvati nell’archivio Adobe. Alcuni metadati relativi ad Adobe Stock vengono salvati per la risorsa in Experience Manager, altrimenti il processo di acquisizione ha lo stesso aspetto di qualsiasi altro file. Ad esempio, se sono attivi i tag avanzati, questi vengono aggiunti a queste risorse al momento del salvataggio.
* La risorsa salvata in Experience Manager è una copia, non un collegamento in Adobe Stock.

**Utilizzo delle risorse salvate da Adobe Stock in Experience Manager in Creative Cloud**. Questa integrazione è indipendente da Adobe Asset Link, ma Adobe Asset Link riconosce queste risorse salvate da Stock in questo modo e visualizza metadati aggiuntivi e l’icona Stock su queste risorse nell’interfaccia utente dell’estensione Adobe Asset Link in Photoshop, Illustrator o InDesign. I file sono disponibili per la navigazione, l’apertura e così via, perché sono normali risorse di Experience Manager quando vengono salvati in Experience Manager.
Gli utenti creativi che lavorano nelle app Creative Cloud con estensione Adobe Asset Link, oltre ad avere accesso alle risorse con licenza di Adobe Stock in Experience Manager, possono anche utilizzare il pannello Librerie Creative Cloud per cercare, visualizzare in anteprima e concedere in licenza le risorse Adobe Stock.
Le risorse Adobe Stock concesse in licenza e salvate in Experience Manager diventano disponibili ai team più ampi che accedono all’implementazione di Experience Manager Assets, mentre le risorse Adobe Stock create in licenza tramite il pannello Librerie Creative Cloud le rendono disponibili a se stesse solo per impostazione predefinita nel proprio account Creative Cloud.

## Informazioni sulla memorizzazione delle risorse in un DAM {#about-storing-assets-in-a-dam}

Per progettare un flusso di lavoro efficiente tra i team creativi e di marketing/line-of-business (LOB) e scegliere le migliori funzionalità di supporto, è importante capire quando e perché le risorse vengono memorizzate in DAM.

### Perché le risorse vengono memorizzate in DAM {#why-assets-are-stored-in-dam}

L’archiviazione delle risorse in DAM ne semplifica l’accesso e la ricerca. In questo modo le risorse possono essere utilizzate da numerosi utenti nell’organizzazione o nell’ecosistema, inclusi partner, clienti e così via.

La maggior parte delle organizzazioni sceglie di memorizzare solo le risorse rilevanti per i processi di marketing/LOB a valle (pubblicazione su canali come il canale web tramite Experience Manager Sites o altri canali gestiti da Adobe Experience Cloud, come Marketing Cloud, Advertising Cloud e misurati da Analytics Cloud, fornitura a utenti/partner e così via). Inoltre, le organizzazioni memorizzano in DAM le risorse che possono essere soggette a un processo di revisione/approvazione. In questo modo, DAM archivia principalmente le risorse che hanno elevate probabilità di essere utilizzate ed evita di archiviare le risorse inattive.

L’archiviazione delle risorse è inoltre soggetta a considerazioni tecniche e sull’utilizzo delle risorse. DAM offre servizi aggiuntivi sulle risorse memorizzate, tra cui estrazione di metadati, controllo delle versioni, generazione di anteprime/transcodifica, gestione dei riferimenti e aggiunta di informazioni di controllo degli accessi. Questi servizi richiedono più tempo e risorse infrastrutturali.

Spesso non è consigliabile archiviare tutte le risorse e gli aggiornamenti. Ad esempio, se gli aggiornamenti a risorse specifiche sono di qualità scadente e consumano risorse eccessive, le risorse potrebbero non essere memorizzate in DAM.

#### Quando le risorse vengono memorizzate in DAM {#when-assets-are-stored-in-dam}

I team creativi (e le organizzazioni) solitamente non sono interessati a memorizzare le risorse in ogni fase del loro ciclo di vita. Ad esempio, evitano di memorizzare le risorse nei seguenti casi:

* Risorse non ancora finalizzate o soggette a sperimentazione
* Risorse che non superano il ciclo di revisione del team creativo/interno
* Rispetto alla risorsa in questione, il team ha candidati migliori per rappresentare il proprio lavoro in team esterni

In genere, le risorse delle classi seguenti sono memorizzate in DAM:

* Risorse che hanno raggiunto una certa maturità e che sono considerate pronte per essere condivise
* Risorse preselezionate dal team creativo
* Formati di risorse specifici utilizzabili o richiesti dal marketing, a seconda di un contratto o accordo specifico (ad esempio, file JPG convertiti da file RAW, TIFF/immagini da originali PSD)

#### Quando gli aggiornamenti alle risorse vengono memorizzati in DAM {#when-updates-to-assets-are-stored-in-dam}

Di regola, in DAM devono essere memorizzati solo gli aggiornamenti delle risorse rilevanti per il set più ampio di utenti DAM. In questo modo gli utenti (funzioni di marketing e simili) potranno visualizzare solo le versioni rilevanti nella timeline delle risorse DAM.

In genere, le modifiche sono correlate alle principali attività cardine del ciclo di vita delle risorse. Ad esempio, la risorsa pronta per il marketing iniziale o un aggiornamento ufficiale basato su richiesta/revisione fornito dal team creativo deve essere archiviato e la versione deve essere in DAM.

L’aggiornamento del team creativo, che dovrà essere rivisto dal team marketing dopo una richiesta di modifica della risorsa esistente in DAM, è un esempio di aggiornamento rilevante. Deve essere archiviato e sottoposto a controllo delle versioni in DAM per ulteriore riferimento o per il ripristino della versione precedente.

Di seguito sono riportati alcuni esempi di aggiornamenti che in genere non sono rilevanti:

* Versioni precedenti delle risorse caricate prima che sia pronto per la revisione marketing
* Frequenti modifiche creative alla risorsa nella fase work-in-progress prima che i team creativi e di marketing decidano che la risorsa è pronta

### Accesso utente a DAM {#user-access-to-dam}

Experience Manager Assets supporta due tipi di utenti in base al loro accesso all’implementazione di Experience Manager Assets. In genere, gli utenti all’interno della rete aziendale (firewall) hanno accesso diretto a DAM. Gli altri utenti esterni alla rete aziendale non avrebbero accesso diretto. Il tipo di utente determina quali integrazioni possono essere utilizzate dal punto di vista tecnico.

#### Utenti creativi con accesso diretto a DAM {#creative-users-with-direct-access-to-dam}

In genere, i team creativi interni o le agenzie/i professionisti creativi integrati nella rete interna hanno accesso all’istanza DAM, incluso l’accesso degli Experienci Manager. È possibile configurare un’infrastruttura di Experience Manager e di rete per consentire l’accesso diretto a soggetti esterni, solitamente organizzazioni affidabili come le agenzie che lavorano per un cliente, per accedere agli Experienci Manager in rete, ad esempio tramite elenchi Consentiti VPN o IP.

In questi casi, Adobe Asset Link o l’app desktop Experience Manager consentono di accedere facilmente alle risorse finali/approvate e di salvare in DAM le risorse pronte per la creazione.

#### Utenti creativi senza accesso a DAM {#creative-users-without-access-to-dam}

Le agenzie esterne e i freelance che non hanno accesso diretto all’istanza DAM possono richiedere l’accesso alle risorse approvate o desiderano aggiungere le nuove progettazioni al DAM.

Utilizza le seguenti strategie per fornire accesso alle risorse finali/approvate:

* Se Asset Link non funziona, utilizza l’app desktop.
* Utilizzare [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) per la distribuzione sicura delle risorse ai partner esterni
* Utilizza un’implementazione personalizzata di un portale di distribuzione e sourcing basato su [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilizza il controllo degli accessi configurato in Experience Manager e l’infrastruttura di rete necessaria (ad esempio, l’inserimento di VPN e IP nell’elenco Consentiti) per consentire alle parti esterne di accedere a un’area dedicata di contenuto nel DAM. Possono utilizzare l’interfaccia utente web di Experience Manager per ottenere risorse e caricare nuovi contenuti in DAM.

#### Lavori in corso sulle risorse da Experience Manager {#work-in-progress-on-assets-from-aem}

Come descritto in questo documento, si consiglia di eseguire importanti aggiornamenti sulle risorse, talvolta denominati work in progress, senza dover caricare tutte le modifiche nel file locale anche in Experience Manager come modifiche. Ciò consente di velocizzare il lavoro di un utente desktop, limitare la larghezza di banda della rete utilizzata, mantenere pulita la timeline delle risorse e concentrarsi su aggiornamenti controllati e importanti.

Adobe Asset Link offre un buon supporto per questo caso d’uso:

* Quando gli utenti di Photoshop, InDesign o Illustrator intendono modificare un file, eseguono un’operazione di Check-Out sulla risorsa in questione
* La risorsa viene scaricata in background, inserita nell&#39;account di Creative Cloud degli utenti sincronizzato su disco dall&#39;app desktop Creative Cloud e il contrassegno di estrazione viene attivato nell&#39;Experience Manager della risorsa per ridurre al minimo i conflitti di modifica
* Da lì in poi, l’utente lavora in un file memorizzato localmente nella posizione sincronizzata e può continuare a lavorare e salvare le modifiche necessarie a qualsiasi frequenza richiesta
* Inoltre, poiché la risorsa si trova nell’account di Creative Cloud, è disponibile anche su altri dispositivi di cui l’utente potrebbe disporre (ad esempio, può essere aperta o modificata in un’app mobile Creative Cloud dedicata) e può essere condivisa con altri utenti Creative Cloud a scopo di collaborazione.
* Una volta apportate le modifiche, l&#39;utente creativo può eseguire un&#39;operazione di check-in su tale file nell&#39;applicazione Creative Cloud, con un commento facoltativo. La risorsa corrispondente in Experience Manager viene sottoposta a controllo delle versioni e aggiornata con il nuovo binario. Gli utenti di Experience Manager, come gli addetti al marketing o gli utenti LOB, hanno accesso alle principali modifiche alle risorse o ai milestone tramite l’interfaccia utente della timeline delle risorse di Experience Manager.

L’app desktop Experience Manager fornisce una condivisione di rete per le risorse aperte nell’app nativa. Per impostazione predefinita, tutte le modifiche apportate localmente vengono caricate in Experience Manager automaticamente dopo un breve periodo di tempo. Con una tale configurazione, i salvataggi frequenti durante la fase di work-in-progress verrebbero tutti caricati in Experience Manager e ne verserebbero le versioni, creando una grande quantità di traffico di rete e potenziali problemi di scalabilità - per non parlare delle versioni non necessarie in Experience Manager.

L’approccio consigliato è quello di utilizzare un’opzione nell’app desktop Experience Manager per disattivare gli aggiornamenti automatici e caricare manualmente le modifiche apportate alle risorse da Experience Manager, utilizzando l’azione carica modifiche nell’interfaccia utente Stato risorse dell’app.

#### Caricamento in blocco in DAM {#bulk-upload-to-dam}

In alcuni casi potrebbe essere necessario caricare simultaneamente un numero maggiore di file in DAM, ad esempio:

* Caricamento dei risultati del servizio fotografico o di progetti più grandi
* Caricamento delle risorse fornite dalle agenzie creative
* Caricamento delle risorse selezionate da un set più grande se la selezione viene eseguita al di fuori di DAM

Questa descrizione si riferisce al caricamento operativo dei file (ad esempio, ogni settimana o con ogni servizio fotografico ), come parte normale del flusso di lavoro dell’utente desktop. Le migrazioni di risorse di grandi dimensioni non sono trattate qui.

Puoi utilizzare le seguenti funzionalità di caricamento:

* Per caricare in blocco cartelle di grandi dimensioni o gerarchiche, utilizza l’app desktop Experience Manager che fornisce [caricamento cartella](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets) funzionalità. Puoi anche caricare strutture di cartelle gerarchiche. Le risorse vengono caricate in background e, pertanto, non sono collegate a una sessione del browser web
* Per caricare alcuni file da una singola cartella, trascina i file direttamente sull’interfaccia web o utilizza l’opzione Crea nell’interfaccia web di Experience Manager Assets.
* A seconda dei requisiti aziendali, puoi anche utilizzare un caricatore personalizzato.

#### Gestione delle risorse digitali direttamente dal desktop {#managing-digital-assets-directly-from-desktop}

Se utilizzi Condivisioni file di rete per gestire le risorse digitali, il semplice utilizzo della condivisione di rete mappata dall’app desktop Experience Manager potrebbe essere considerato un comodo sostituto. Durante la transizione da condivisioni di file di rete, Experience Manager Web Interface fornisce un set completo di funzionalità di gestione delle risorse digitali che vanno ben oltre quanto possibile su una condivisione di rete (ricerche, raccolte, metadati, collaborazione, anteprime e così via) e Experience Manager Desktop App fornisce un comodo collegamento per collegare l’archivio DAM lato server con il lavoro sul desktop.

Evita di utilizzare l’app desktop Experience Manager per gestire le risorse direttamente nella condivisione di rete di Experience Manager Assets. Ad esempio, evita di utilizzare l’app desktop Experience Manager per spostare/copiare più file. È invece possibile utilizzare l&#39;interfaccia utente Web di Experience Manager Assets per trascinare le cartelle da Finder/Explorer alla condivisione di rete o utilizzare la funzione Caricamento cartelle di Experience Manager Assets.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
