---
title: Best practice per l'integrazione con  [!DNL Adobe Creative Cloud]
description: Le best practice integrano un’implementazione di Experience Manager con Adobe Creative Cloud per semplificare i flussi di lavoro di trasferimento delle risorse e ottenere la massima efficienza.
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration, Adobe Asset Link, Desktop App
role: User, Developer, Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3438'
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
>La condivisione cartelle da Experience Manager a Creative Cloud è ora obsoleta e non è più trattata di seguito. Adobe consiglia funzionalità più recenti, come Adobe Asset Link o l’app desktop Experience Manager, per consentire ai creativi di accedere alle risorse gestite in Experience Manager.

## Creatività, addetti al marketing e utenti DAM nella necessità di Collaboration {#collaboration-need-of-creatives-marketers-and-dam-users}

| Requisiti | Caso d’uso | Superfici interessate |
|---|---|---|
| Esperienza semplificata per i creativi sul desktop | Accesso semplificato alle risorse da un DAM ([!DNL Assets]) per i creativi o più in generale per gli utenti desktop che lavorano in applicazioni di creazione di risorse native. Hanno bisogno di un modo semplice per scoprire, utilizzare (aprire), modificare e salvare le modifiche in Experience Manager e caricare nuovi file. | Windows o Mac desktop; app Creative Cloud |
| Fornisci risorse pronte all&#39;uso di alta qualità da [!DNL Adobe Stock] | Gli addetti al marketing contribuiscono ad accelerare il processo di creazione dei contenuti fornendo assistenza per l’origine e il rilevamento delle risorse. I professionisti Creative utilizzano le risorse approvate direttamente nei loro strumenti creativi. | [!DNL Assets]; [!DNL Adobe Stock] marketplace; campi metadati |
| Distribuire e condividere le risorse per organizzazioni | Reparti interni/filiali locali e partner esterni, distributori e agenzie utilizzano le risorse approvate condivise dall’organizzazione principale. L’organizzazione desidera condividere in modo sicuro e fluido le risorse create per un riutilizzo più ampio. | [!DNL Brand Portal], [!DNL Asset Share Commons] |
| Genera automaticamente varianti predefinite di risorse caricate | Elabora automaticamente le risorse utilizzando l&#39;esclusiva tecnologia Adobe di gestione dei supporti e trasformazione per le azioni predefinite. Crea una logica personalizzata per definire le tue azioni utilizzando API e microservizi per le risorse. | Interfaccia utente di [!DNL Assets] |

## Offerte Adobe per supportare le esigenze di collaborazione {#adobe-offerings-to-support-the-collaboration-need}

| Proposta di valore per gli utenti tipo interessati | Offerta Adobe | Superfici interessate |
|---|---|---|
| Gli utenti di Creative individuano le risorse da [!DNL Experience Manager], le aprono e le utilizzano, modificano e caricano le modifiche in [!DNL Experience Manager] e caricano nuovi file in [!DNL Experience Manager], senza uscire dall&#39;app [!DNL Creative Cloud]. | [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator e InDesign. |
| Gli utenti aziendali semplificano l&#39;apertura e l&#39;utilizzo delle risorse, la modifica e il caricamento delle modifiche in [!DNL Experience Manager] e il caricamento di nuovi file in [!DNL Experience Manager] dall&#39;ambiente desktop. Utilizzano un’integrazione generica per aprire qualsiasi tipo di risorsa nell’applicazione desktop nativa, comprese quelle non Adobe. | [[!DNL Experience Manager] App desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | App desktop Experience Manager su desktop Win e Mac |
| Gli addetti al marketing e gli utenti aziendali possono scoprire, visualizzare in anteprima, concedere in licenza e salvare le risorse di Adobe Stock, nonché gestirle direttamente da Experience Manager. Le risorse concesse in licenza e salvate forniscono metadati Adobe Stock selezionati per una migliore governance. | [Integrazione di Experience Manager e Adobe Stock](aem-assets-adobe-stock.md) | Interfaccia Web [!DNL Experience Manager] |
| Migliorare la collaborazione tra designer di prodotti digitali e addetti al marketing. Consenti ai designer di utilizzare le risorse digitali nei modelli di progettazione e wireframe nell’area di lavoro di Adobe XD. | [[!DNL Adobe Asset Link] per [!DNL Adobe XD]](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| Gli addetti al marketing possono creare automaticamente varianti e derivati in base alle risorse caricate e alle azioni predefinite create utilizzando la personalizzazione. Utilizza questa automazione per velocizzare le attività relative ai contenuti e ridurre il lavoro manuale. | [Automazione dei contenuti](/help/assets/cc-api-integration.md) | Interfaccia Web [!DNL Experience Manager Assets] |

Questo articolo si concentra principalmente sui primi due aspetti delle esigenze di collaborazione. La distribuzione e l’approvvigionamento delle risorse su scala viene brevemente citata come caso d’uso. Per tali esigenze, valuta prodotti come Adobe Brand Portal o Asset Share Commons. Le soluzioni alternative, come [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), che possono essere create in base ai componenti [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/), [Link Share](share-assets.md), utilizzando [Experience Manager Assets Web UI](/help/assets/manage-digital-assets.md), devono essere esaminate in base a requisiti specifici.

![Connessioni Creative Cloud per Experience Manager: scelta della funzionalità da utilizzare](assets/creative-connections-aem.png)

Scelta della funzionalità da utilizzare

### Mappatura dei casi d’uso e soluzioni Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso d’uso | Adobe Asset Link | app desktop Experience Manager | Osservazioni o metodi alternativi |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Esplorare le cartelle | Sì | Interfaccia utente web di Experience Manager + azioni desktop | Durante la navigazione nella condivisione di rete, disattiva le miniature per evitare di scaricare file binari di risorse. |
| Individuare - accedere alle raccolte | Sì | Interfaccia utente web di Experience Manager + azioni desktop |  |
| Scoprire: cercare le risorse | Sì | Interfaccia utente web di Experience Manager + azioni desktop |  |
| Usa: apri risorsa | Sì | Sì, per qualsiasi app | [Apri dall&#39;interfaccia Web](/help/assets/manage-digital-assets.md#previewing-assets) o dal Finder |
| Utilizza: inserire una risorsa da Experience Manager in un documento | Sì - incorporamento | Sì - Collegamento o incorporamento | L’app desktop Experience Manager consente di accedere alle risorse come file sul file system locale. Questi collegamenti nelle app native sono rappresentati da percorsi locali. |
| Modifica: apri per la modifica | Sì - Estrai | Sì - Azione aperta nella condivisione di rete | Per impostazione predefinita, il Check-Out in AAL[&#x200B; salva la risorsa nell&#39;account di archiviazione di Creative Cloud dell&#39;utente (sincronizzato dall&#39;app Creative Cloud).](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) |
| Modifica: lavoro in corso al di fuori di Experience Manager | Sì - Risorsa disponibile nell’account di archiviazione Creative Cloud dell’utente sincronizzato con il desktop. | Sì |  |
| Modifica - Carica modifiche | Sì - [Azione di archiviazione](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) con commento facoltativo | Sì |  |
| Caricamento - file singolo | Sì - carica il documento attivo corrente | Sì | [Carica tramite interfaccia Web](/help/assets/manage-digital-assets.md#uploading-assets) |
| Caricamento: più file/strutture di cartelle gerarchiche | No | Sì | [Carica tramite interfaccia Web](/help/assets/manage-digital-assets.md#uploading-assets); script o strumento personalizzato |
| Varie - utente e accesso | L&#39;utente Creative Cloud connesso all&#39;app desktop Creative Cloud viene riconosciuto (SSO) | Utente/accesso Experience Manager | Gli utenti di entrambe le soluzioni vengono conteggiati rispetto alla quota di utenti di Experience Manager. |
| Varie - Rete e accesso | Richiede l’accesso dal desktop dell’utente all’implementazione di Experience Manager tramite rete | Richiede l’accesso dal desktop dell’utente all’implementazione di Experience Manager tramite rete | Adobe Asset Link non condivide l’ambiente proxy di rete. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

Per supportare i casi di utilizzo della distribuzione delle risorse, considera le seguenti opzioni:

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) per un componente aggiuntivo configurabile per Assets per la pubblicazione delle risorse.

* Le soluzioni personalizzate vengono create in base alla base di codice di [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/).
* Experience Manager [condivisione collegamenti](/help/assets/share-assets.md) per condividere risorse su richiesta tramite collegamenti.
* [Interfaccia Web di Assets](/help/assets/manage-digital-assets.md) con aree per le parti esterne protette dal programma di installazione di Experience Manager Access Control e con le necessarie regolazioni della configurazione IT/di rete, che consentono a tali utenti esterni di accedere ad Experience Manager.

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
* **Per semplificare l&#39;accesso alle risorse dal desktop per qualsiasi formato di file o applicazione generica:** utilizza l&#39;app desktop Experience Manager
* **Understand why and when to store assets in DAM (Scopri perché e quando archiviare le risorse in DAM)**: aggiornamenti da rendere disponibili al team più ampio della tua organizzazione
* **Mind the volume of assets shared (Considera il volume di risorse condivise):** se il caso d’uso è la distribuzione delle risorse, la governance e la sicurezza potrebbero diventare gli aspetti più importanti. Valuta l’utilizzo di strumenti creati per il lavoro in scala, come Brand Portal.
* **Understand asset lifecycle (Informazioni sul ciclo di vita delle risorse):** scopri come le risorse vengono gestite dai diversi team all’interno dell’organizzazione
* **Handle frequent saves to assets with care (Gestisci con attenzione i salvataggi frequenti nelle risorse):** Adobe Asset Link si occupa di questo aspetto con PS, AI, ID. Per altre applicazioni, non eseguire le attività WIP in una cartella condivisa/mappata a meno che non siano necessarie tutte le modifiche in DAM

### Accesso alle risorse di Adobe Stock da Experience Manager Assets {#access-to-adobe-stock-assets-from-aem-assets}

L&#39;[integrazione di Experience Manager e Adobe Stock](/help/assets/aem-assets-adobe-stock.md) consente agli utenti di Experience Manager di cercare, visualizzare in anteprima, concedere in licenza e salvare risorse da Adobe Stock in Experience Manager. Le risorse Adobe Stock concesse in licenza e salvate hanno selezionato metadati Stock che possono essere utilizzati per cercarli con filtri aggiuntivi.

Alcuni punti importanti su questa integrazione:

* Quando le risorse da Adobe Stock vengono salvate in Experience Manager, diventano un normale Experience Manager Assets, con file binari salvati nell’archivio Experience Manager. Alcuni metadati relativi ad Adobe Stock vengono salvati per la risorsa in Experience Manager, altrimenti il processo di acquisizione ha lo stesso aspetto di qualsiasi altro file. Ad esempio, se sono attivi i tag avanzati, questi vengono aggiunti a queste risorse al momento del salvataggio.
* La risorsa salvata in Experience Manager è una copia, non un collegamento in Adobe Stock.

**Utilizzo delle risorse salvate da Adobe Stock in Experience Manager in Creative Cloud**. Questa integrazione è indipendente da Adobe Asset Link, ma Adobe Asset Link riconosce queste risorse salvate da Stock in questo modo e visualizza metadati aggiuntivi e l’icona Stock su queste risorse nell’interfaccia utente dell’estensione Adobe Asset Link in Photoshop, Illustrator o InDesign. I file sono disponibili per la navigazione, l’apertura e così via, perché sono normali risorse di Experience Manager quando vengono salvati in Experience Manager.
Gli utenti di Creative che lavorano nelle app Creative Cloud con estensione Adobe Asset Link, oltre ad avere accesso alle risorse già concesse in licenza da Adobe Stock ad Experience Manager, possono utilizzare il pannello Creative Cloud Libraries anche per cercare, visualizzare in anteprima e concedere in licenza le risorse Adobe Stock.
Assets da Adobe Stock concesso in licenza e salvato in Experience Manager diventa disponibile per i team più ampi che accedono all’implementazione di Experience Manager Assets, mentre le risorse per le licenze dei creativi da Adobe Stock tramite il pannello Creative Cloud Libraries le rendono disponibili a se stessi solo per impostazione predefinita nel proprio account Creative Cloud.

## Informazioni sulla memorizzazione delle risorse in un DAM {#about-storing-assets-in-a-dam}

Per progettare un flusso di lavoro efficiente tra i team creativi e di marketing/line-of-business (LOB) e scegliere le migliori funzionalità di supporto, è importante capire quando e perché le risorse vengono memorizzate in DAM.

### Perché le risorse vengono memorizzate in DAM {#why-assets-are-stored-in-dam}

L’archiviazione delle risorse in DAM ne semplifica l’accesso e la ricerca. In questo modo le risorse possono essere utilizzate da numerosi utenti nell’organizzazione o nell’ecosistema, inclusi partner, clienti e così via.

La maggior parte delle organizzazioni sceglie di memorizzare solo le risorse rilevanti per i processi di marketing/LOB a valle (pubblicazione su canali come il canale web tramite Experience Manager Sites o altri canali gestiti da Adobe Experience Cloud, come Marketing Cloud, Advertising Cloud e misurati da Analytics Cloud, fornendo informazioni a utenti/partner e così via). Inoltre, le organizzazioni memorizzano in DAM le risorse che possono essere soggette a un processo di revisione/approvazione. In questo modo, DAM archivia principalmente le risorse che hanno elevate probabilità di essere utilizzate ed evita di archiviare le risorse inattive.

L’archiviazione delle risorse è inoltre soggetta a considerazioni tecniche e sull’utilizzo delle risorse. DAM offre servizi aggiuntivi sulle risorse memorizzate, tra cui estrazione di metadati, controllo delle versioni, generazione di anteprime/transcodifica, gestione dei riferimenti e aggiunta di informazioni di controllo degli accessi. Questi servizi richiedono più tempo e risorse infrastrutturali.

Spesso non è consigliabile archiviare tutte le risorse e gli aggiornamenti. Ad esempio, se gli aggiornamenti a risorse specifiche sono di qualità scadente e consumano risorse eccessive, le risorse potrebbero non essere memorizzate in DAM.

#### Quando le risorse vengono memorizzate in DAM {#when-assets-are-stored-in-dam}

I team Creative (e le organizzazioni) solitamente non sono interessati a memorizzare le risorse in ogni fase del loro ciclo di vita. Ad esempio, evitano di memorizzare le risorse nei seguenti casi:

* Assets non ancora finalizzati o soggetti a sperimentazione
* Assets che non superano il ciclo di revisione del team creativo/interno
* Rispetto alla risorsa in questione, il team ha candidati migliori per rappresentare il proprio lavoro in team esterni

In genere, le risorse delle classi seguenti sono memorizzate in DAM:

* Assets che hanno raggiunto una certa maturità e sono considerati pronti per essere condivisi
* Assets preselezionati dal team creativo
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

#### Utenti Creative con accesso diretto a DAM {#creative-users-with-direct-access-to-dam}

In genere, i team creativi interni o le agenzie/i professionisti creativi integrati nella rete interna hanno accesso all’istanza DAM, incluso l’accesso ad Experience Manager. Experience Manager e l’infrastruttura di rete possono essere configurati per consentire l’accesso diretto a parti esterne, solitamente organizzazioni affidabili come le agenzie che lavorano per un cliente, per accedere ad Experience Manager in rete, ad esempio tramite VPN o elenchi Consentiti IP.

In questi casi, Adobe Asset Link o l’app desktop Experience Manager consentono di accedere facilmente alle risorse finali/approvate e di salvare in DAM le risorse pronte per la creazione.

#### Utenti Creative senza accesso a DAM {#creative-users-without-access-to-dam}

Le agenzie esterne e i freelance che non hanno accesso diretto all’istanza DAM possono richiedere l’accesso alle risorse approvate o desiderano aggiungere le nuove progettazioni al DAM.

Utilizza le seguenti strategie per fornire accesso alle risorse finali/approvate:

* Se Asset Link non funziona, utilizza l’app desktop.
* Utilizza [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) per distribuire le risorse in modo sicuro ai partner esterni
* Utilizza un&#39;implementazione personalizzata di un portale di distribuzione e sourcing basato su [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilizza il controllo degli accessi configurato in Experience Manager e l’infrastruttura di rete necessaria (ad esempio, l’inserimento di VPN e IP nell’elenco Consentiti) per consentire a parti esterne di accedere a un’area dedicata di contenuti nel tuo DAM. Possono utilizzare l’interfaccia utente web di Experience Manager per ottenere risorse e caricare nuovi contenuti in DAM.

#### Lavori in corso sulle risorse da Experience Manager {#work-in-progress-on-assets-from-aem}

Come descritto in questo documento, si consiglia di eseguire aggiornamenti principali sulle risorse, talvolta denominati work in progress, senza dover caricare tutte le modifiche nel file locale anche in Experience Manager come modifiche. Ciò consente di velocizzare il lavoro di un utente desktop, limitare la larghezza di banda della rete utilizzata, mantenere pulita la timeline delle risorse e concentrarsi su aggiornamenti controllati e importanti.

Adobe Asset Link offre un buon supporto per questo caso d’uso:

* Quando gli utenti di Photoshop, InDesign o Illustrator intendono modificare un file, eseguono un’operazione di Check-Out sulla risorsa in questione
* La risorsa viene scaricata in background, inserita nell&#39;account Creative Cloud degli utenti sincronizzato su disco dall&#39;app desktop Creative Cloud e il flag di check-out viene attivato in Experience Manager sulla risorsa per ridurre al minimo i conflitti di modifica
* Da lì in poi, l’utente lavora in un file memorizzato localmente nella posizione sincronizzata e può continuare a lavorare e salvare le modifiche necessarie a qualsiasi frequenza richiesta
* Inoltre, poiché la risorsa si trova nell’account Creative Cloud, è disponibile anche su altri dispositivi di cui l’utente potrebbe disporre (ad esempio, può essere aperta o modificata in un’app mobile Creative Cloud dedicata) e può essere condivisa con altri utenti Creative Cloud a scopo di collaborazione.
* Una volta apportate le modifiche, l&#39;utente creativo può eseguire un&#39;operazione di archiviazione su tale file nell&#39;applicazione Creative Cloud, con un commento facoltativo. In Experience Manager, la risorsa corrispondente viene sottoposta a controllo delle versioni e aggiornata con il nuovo binario. Gli utenti di Experience Manager, come gli addetti al marketing o gli utenti LOB, hanno accesso alle principali modifiche alle risorse o alle milestone tramite l’interfaccia utente della timeline delle risorse di Experience Manager.

L’app desktop Experience Manager fornisce una condivisione di rete per le risorse aperte nell’app nativa. Per impostazione predefinita, tutte le modifiche apportate localmente vengono caricate automaticamente in Experience Manager dopo un breve periodo di tempo. Con una tale configurazione, i salvataggi frequenti durante la fase di work-in-progress verrebbero tutti caricati in Experience Manager e sottoposti a gestione delle versioni, creando una grande quantità di traffico di rete e potenziali problemi di scalabilità - per non parlare delle versioni non necessarie in Experience Manager.

L’approccio consigliato è quello di utilizzare un’opzione nell’app desktop Experience Manager per disattivare gli aggiornamenti automatizzati e caricare manualmente le modifiche apportate alle risorse in Experience Manager, utilizzando l’azione carica modifiche nell’interfaccia utente dello stato delle risorse dell’app.

#### Caricamento in blocco in DAM {#bulk-upload-to-dam}

In alcuni casi potrebbe essere necessario caricare simultaneamente un numero maggiore di file in DAM, ad esempio:

* Caricamento dei risultati del servizio fotografico o di progetti più grandi
* Caricamento delle risorse fornite dalle agenzie creative
* Caricamento delle risorse selezionate da un set più grande se la selezione viene eseguita al di fuori di DAM

Questa descrizione si riferisce al caricamento operativo dei file (ad esempio, ogni settimana o con ogni servizio fotografico ), come parte normale del flusso di lavoro dell’utente desktop. Le migrazioni di risorse di grandi dimensioni non sono trattate qui.

Puoi utilizzare le seguenti funzionalità di caricamento:

* Per caricare in blocco cartelle di grandi dimensioni o gerarchiche, utilizza l&#39;app desktop Experience Manager che fornisce la funzionalità di [caricamento cartelle](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets). Puoi anche caricare strutture di cartelle gerarchiche. Assets viene caricato in background e, pertanto, non è legato a una sessione del browser web
* Per caricare alcuni file da una singola cartella, trascina i file direttamente sull’interfaccia web o utilizza l’opzione Crea nell’interfaccia web di Experience Manager Assets.
* A seconda dei requisiti aziendali, puoi anche utilizzare un caricatore personalizzato.

#### Gestione delle risorse digitali direttamente dal desktop {#managing-digital-assets-directly-from-desktop}

Se utilizzi Condivisioni file di rete per gestire le risorse digitali, l’utilizzo della condivisione di rete mappata dall’app desktop Experience Manager potrebbe essere considerato un comodo sostituto. Durante la transizione da condivisioni di file di rete, l’interfaccia web di Experience Manager offre un set completo di funzionalità di gestione delle risorse digitali che vanno ben oltre quanto possibile su una condivisione di rete (ricerca, raccolte, metadati, collaborazione, anteprime e così via) e l’app desktop Experience Manager fornisce un comodo collegamento per collegare l’archivio DAM lato server con il lavoro sul desktop.

Evita di utilizzare l’app desktop Experience Manager per gestire le risorse direttamente nella condivisione di rete di Experience Manager Assets. Ad esempio, evita di utilizzare l’app desktop Experience Manager per spostare/copiare più file. È invece possibile utilizzare l&#39;interfaccia utente Web di Experience Manager Assets per trascinare le cartelle da Finder/Explorer alla condivisione di rete o utilizzare la funzione Caricamento cartelle di Experience Manager Assets.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
