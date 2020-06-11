---
title: Best practice per l'integrazione con Adobe Experience Manager e Adobe Creative Cloud
description: Procedure ottimali per l’integrazione di un’istanza AEM con Adobe Creative Cloud per semplificare i flussi di lavoro di trasferimento delle risorse e ottenere la massima efficienza.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 496ad0831d20eb7653a3c5727999a2abc5728ec7
workflow-type: tm+mt
source-wordcount: '3302'
ht-degree: 18%

---


# Best practice per l&#39;integrazione con AEM e Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

Risorse Adobe Experience Manager (AEM) è una soluzione di gestione delle risorse digitali (DAM) che può essere integrata con Adobe Creative Cloud per aiutare gli utenti DAM a collaborare con i team creativi, semplificando la collaborazione nel processo di creazione dei contenuti.

Adobe Creative Cloud offre ai team creativi un ecosistema di soluzioni e servizi per aiutarli a creare risorse digitali. Include applicazioni desktop e mobili, servizi cloud come l’archiviazione con sincronizzazione desktop o esperienza Web, nonché marketplace come Adobe Stock.

Continua a leggere per scoprire quali integrazioni scegliere tra desktop e DAM di livello Enterprise in base al tuo caso di utilizzo e quali sono le best practice associate ai flussi di lavoro di collegamento.

>[!NOTE]
>
>La condivisione delle cartelle da AEM a Creative Cloud ora è obsoleta e non è più inclusa nella sezione sottostante. Adobe consiglia di utilizzare nuove funzionalità come Adobe Asset Link o l’app desktop AEM per fornire agli utenti creativi l’accesso alle risorse gestite in AEM.

## Necessità di collaborazione tra creativi, esperti di marketing e utenti DAM {#collaboration-need-of-creatives-marketers-and-dam-users}


| Requisiti | Caso di utilizzo | Superfici interessate |
|---|---|---|
| Esperienza semplificata per i creativi su desktop | Semplificate l&#39;accesso alle risorse da DAM (AEM Assets) per i creativi professionisti o, più in generale, per gli utenti desktop che lavorano nelle applicazioni native per la creazione di risorse. Hanno bisogno di un modo semplice e semplice per scoprire, usare (aprire), modificare e salvare le modifiche in AEM, nonché caricare nuovi file. | desktop Win o Mac; App Creative Cloud |
| Fornire risorse pronte all’uso di alta qualità da Adobe Stock | Gli esperti di marketing contribuiscono ad accelerare il processo di creazione dei contenuti fornendo assistenza per l&#39;origine e l&#39;individuazione delle risorse. I creativi professionisti usano le risorse approvate direttamente dai loro strumenti creativi. | Risorse AEM; mercato Adobe Stock; campi di metadati |
| Distribuire e condividere le risorse per organizzazioni | I dipartimenti interni/le filiali locali e i partner esterni, i distributori e le agenzie utilizzano le risorse approvate condivise dall&#39;organizzazione madre. L’organizzazione intende condividere in modo sicuro e senza soluzione di continuità le risorse create per un riutilizzo più ampio. | Portale del marchio, Contenuti di condivisione delle risorse |

## Offerte Adobe a supporto delle esigenze di collaborazione {#adobe-offerings-to-support-the-collaboration-need}

| Proposta di valore per le persone coinvolte | Offerta Adobe | Superfici interessate |
|---|---|---|
| Gli utenti creativi scoprono le risorse da AEM, le aprono e le utilizzano, le modificano e caricano in AEM, nonché caricano nuovi file in AEM, senza uscire dalle app Creative Cloud. | [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator e InDesign |
| Gli utenti aziendali semplificano l’apertura e l’utilizzo delle risorse, la modifica e il caricamento delle modifiche in AEM e il caricamento di nuovi file in AEM dall’ambiente desktop. Utilizzano un&#39;integrazione generica per aprire qualsiasi tipo di risorsa nell&#39;applicazione desktop nativa, inclusi quelli non Adobe. | [App desktop AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | App desktop AEM su Windows e Mac |
| Gli esperti di marketing e gli utenti aziendali possono scoprire, visualizzare in anteprima, concedere in licenza e salvare e gestire le risorse Adobe Stock dall’interno di AEM. Le risorse concesse in licenza e salvate forniscono metadati Adobe Stock selezionati per una migliore governance. | [Integrazione con Experience Manager e Adobe Stock](aem-assets-adobe-stock.md) | Interfaccia Web di AEM |

Questo articolo si concentra principalmente sui primi due aspetti delle esigenze di collaborazione. La distribuzione e l’approvvigionamento delle risorse su scala viene brevemente citata come caso d’uso. Per tali esigenze, valuta prodotti come Adobe Brand Portal o Asset Share Commons. Le soluzioni alternative, come [AEM Assets Brand Portal](https://helpx.adobe.com/it/experience-manager/brand-portal/user-guide.html), che possono essere create in base ai componenti di [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) e [Condivisione collegamenti](share-assets.md) e che sfruttano l’interfaccia [web di AEM Assets](/help/assets/manage-digital-assets.md), devono essere esaminate secondo requisiti specifici.

![Connessioni Creative Cloud per AEM: Definizione di quale funzionalità utilizzare](assets/creative-connections-aem.png)

Decidere su quale funzionalità utilizzare

### Mappatura dei casi di utilizzo e delle soluzioni Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso di utilizzo | Adobe Asset Link | App desktop AEM | Osservazioni o metodi alternativi |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Scopri - Sfoglia cartelle AEM | Sì | AEM Web UI + azioni desktop | Quando sfogliate la condivisione di rete, disattivate le miniature per evitare di scaricare file binari di risorse. |
| Scopri - Accesso alle raccolte AEM | Sì | AEM Web UI + azioni desktop |  |
| Scopri - cercare risorse da AEM | Sì | AEM Web UI + azioni desktop |  |
| Usa - apri risorsa | Sì | Sì - per qualsiasi app | [Apri dall&#39;interfaccia](/help/assets/manage-digital-assets.md#previewing-assets) Web o dal Finder |
| Utilizzo: inserire una risorsa da AEM in un documento | Sì - incorporamento | Sì - collegamento o incorporazione | L’app desktop AEM consente di accedere alle risorse come file nel file system locale. Tali collegamenti nelle app native sono rappresentati da percorsi locali. |
| Modifica - aprire per la modifica | Sì - Azione di check-out | Sì - Azione di apertura (nella condivisione di rete) | [Il check-out in AAL](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) salva la risorsa nell’account di archiviazione Creative Cloud dell’utente (sincronizzato dall’app Creative Cloud) per impostazione predefinita. |
| Modifica - lavoro in corso all’esterno di AEM | Sì - Risorsa disponibile nell’account di archiviazione Creative Cloud dell’utente sincronizzato con il desktop. | Sì |  |
| Modifica - modifiche di caricamento | Sì - [Check-in azione](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) con commento facoltativo | Sì |  |
| Carica - file singolo | Sì - carica il documento attivo corrente | Sì | [Caricamento tramite interfaccia Web](/help/assets/manage-digital-assets.md#uploading-assets) |
| Caricamento: più file/strutture di cartelle gerarchiche | No | Sì | [Caricamento tramite interfaccia](/help/assets/manage-digital-assets.md#uploading-assets)Web; Strumento o script personalizzato |
| Varie - utente e login | L&#39;utente Creative Cloud che ha effettuato l&#39;accesso all&#39;app desktop Creative Cloud viene riconosciuto (SSO) | Utente/login AEM | Gli utenti di entrambe le soluzioni contano sulla quota di utenti di AEM. |
| Varie - rete e accesso | Richiede l&#39;accesso dal desktop dell&#39;utente alla distribuzione AEM in rete | Richiede l&#39;accesso dal desktop dell&#39;utente alla distribuzione AEM in rete | Adobe Asset Link non condivide l’ambiente proxy di rete. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

Per supportare i casi di utilizzo della distribuzione delle risorse, è necessario considerare altre soluzioni:

* [AEM Assets Brand Portal](https://helpx.adobe.com/it/experience-manager/brand-portal/user-guide.html) per un componente aggiuntivo SaaS configurabile per Risorse AEM per pubblicare risorse.

* Le soluzioni personalizzate vengono create in base al codice di base di [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) .
* Condivisione [dei](/help/assets/share-assets.md) collegamenti AEM per condividere risorse ad hoc tramite i collegamenti.
* [Interfaccia](/help/assets/manage-digital-assets.md) Web di AEM Assets con aree per soggetti esterni protetti dalla configurazione di AEM Access Control e con le necessarie regolazioni di configurazione IT/rete, per consentire a questi utenti esterni di accedere ad AEM.

## Concetti chiave e casi di utilizzo {#key-concepts-and-use-cases}

### Glossario dei termini comuni {#glossary-of-common-terms}

* **Work-in-progress o creative work-in-progress (WIP):** una fase del ciclo di vita delle risorse in cui una risorsa subisce più modifiche e, in genere, non è ancora pronta per essere condivisa con team più grandi.
* **Creative-ready assets (Risorse pronte per i creativi):** risorse pronte per essere condivise con un team più ampio oppure che sono state selezionate o approvate dal team creativo per la condivisione con i team di marketing o LOB.

* **Asset approvals (Approvazioni risorse):** il processo di approvazione che viene eseguito per le risorse già caricate in DAM, che, in genere, include approvazioni del marchio, approvazioni legali e così via.
* **Final asset (Risorsa finale):** una risorsa che ha superato tutte le approvazioni/assegnazione tag dei metadati ed è pronta per essere utilizzata dal team più ampio. Tale risorsa viene memorizzata in DAM, per poi essere resa disponibile a tutti gli utenti (o a tutti gli interessati). Può essere utilizzata nei canali di marketing o dai team creativi per la creazione di design.

* **Minor asset update/change (Aggiornamento/modifica risorsa secondaria):** una modifica rapida e piccola a una risorsa digitale. Spesso viene effettuata in risposta a una richiesta di ritocco o di modifica minore, a una revisione delle risorse o all’approvazione (ad esempio: riposizionamento, modifica dimensioni del testo, regolazione di saturazione/luminosità, colore e così via).
* **Major asset update/change (Aggiornamento/modifica risorsa principale):** un passaggio a una risorsa digitale che richiede un lavoro considerevole e che a volte deve essere effettuato in un periodo di tempo più lungo. Generalmente include più modifiche. La risorsa deve essere salvata più volte durante l’aggiornamento. In genere, gli aggiornamenti principali delle risorse fanno sì che la risorsa entri in una fase WIP.
* **DAM:** gestione delle risorse digitali. In questo documento, è sinonimo di AEM Experience Manager Assets, a meno che non venga espressamente indicato altrimenti.
* **Creative user (Utente creativo):** un professionista che crea risorse digitali utilizzando le app e i servizi Creative Cloud. In alcuni casi, è possibile che un utente creativo sia membro di un team creativo che utilizza Creative Cloud, ma che non crea risorse digitali, ad esempio un direttore creativo o un manager del team creativo.
* **DAM user (Utente DAM)**: utente tipico di un sistema DAM. A seconda dell’organizzazione, un utente DAM può essere di marketing o non, come un utente Line-of-Business (LOB), un bibliotecario, un venditore e così via.

### Considerazioni sull’utilizzo dell’integrazione AEM e Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Questo è un breve riepilogo delle best practice per l&#39;integrazione di AEM e Creative Cloud. Leggi il resto del documento per avere una comprensione dettagliata di questi.

* **For creative users, working in Photoshop, InDesign, or Illustrator (Per gli utenti creativi che lavorano in Photoshop, InDesign o Illustrator)**: Adobe Asset Link offre la migliore esperienza utente possibile, inclusa la gestione del Work-in-progress sulle risorse estratte da AEM
* **For simplifying access to assets from desktop for any generic file format or application (Per semplificare l’accesso alle risorse dal desktop per qualsiasi formato di file o applicazione di tipo generico):** utilizza l’app desktop AEM
* **Understand why and when to store assets in DAM (Scopri perché e quando archiviare le risorse in DAM)**: aggiornamenti da rendere disponibili al team più ampio della tua organizzazione
* **Mind the volume of assets shared (Considera il volume di risorse condivise):** se il caso d’uso è la distribuzione delle risorse, la governance e la sicurezza potrebbero diventare gli aspetti più importanti. Valuta l’utilizzo di strumenti creati per il lavoro in scala, come Brand Portal.
* **Understand asset lifecycle (Informazioni sul ciclo di vita delle risorse):** scopri come le risorse vengono gestite dai diversi team all’interno dell’organizzazione
* **Handle frequent saves to assets with care (Gestisci con attenzione i salvataggi frequenti nelle risorse):** Adobe Asset Link si occupa di questo aspetto con PS, AI, ID. Per altre applicazioni, non eseguire le attività WIP in cartelle condivise o mappate, a meno che non ti servano tutte le modifiche all’interno di DAM

### Accesso alle risorse Adobe Stock da Risorse AEM {#access-to-adobe-stock-assets-from-aem-assets}

[L’integrazione](/help/assets/aem-assets-adobe-stock.md) di AEM e Adobe Stock consente agli utenti AEM di cercare, visualizzare in anteprima, concedere in licenza e salvare risorse da Adobe Stock in AEM. Le risorse Adobe Stock concesse in licenza e salvate hanno selezionato i metadati Stock, che possono essere utilizzati per la ricerca con altri filtri.

Alcuni punti importanti su questa integrazione:

* Quando le risorse di Adobe stock vengono salvate in AEM, diventano normali risorse AEM, con file binari salvati nell’archivio AEM. Alcuni metadati relativi ad Adobe Stock vengono salvati per la risorsa in AEM, altrimenti il processo di assimilazione sarà simile a quello di qualsiasi altro file. Ad esempio, se i tag avanzati sono attivi, al momento del salvataggio vengono aggiunti a tali risorse.
* La risorsa salvata in AEM è una copia, non un collegamento in Adobe Stock.

**Utilizzo delle risorse salvate da Adobe Stock in AEM in Creative Cloud**. Questa integrazione è indipendente da Adobe Asset Link, ma Adobe Asset Link riconosce le risorse salvate da Stock in questo modo e visualizza metadati aggiuntivi e l’icona Stock su queste risorse nell’interfaccia utente dell’estensione Adobe Asset Link in Photoshop, Illustrator o InDesign. I file sono disponibili per la navigazione, l’apertura e così via, perché sono normali risorse AEM se salvate in AEM.
Gli utenti Creative Cloud che lavorano nelle app Creative Cloud con l’estensione Adobe Asset Link presente, oltre a poter accedere a risorse già concesse in licenza da Adobe Stock in AEM, possono anche utilizzare il pannello Creative Cloud Libraries per cercare, visualizzare in anteprima e concedere in licenza risorse Adobe Stock.
Le risorse da Adobe Stock con licenza e salvate in AEM diventano disponibili per i team più grandi che accedono alla distribuzione di Risorse AEM, mentre le risorse per la licenza di Adobe Stock mediante il pannello Creative Cloud Libraries le rendono disponibili per se stesse solo per impostazione predefinita nel loro account Creative Cloud.

## Memorizzazione delle risorse in un DAM {#about-storing-assets-in-a-dam}

Per progettare un flusso di lavoro efficiente tra i team creativi e di marketing/line-of-business (LOB) e scegliere le migliori funzionalità di supporto, è importante comprendere quando e perché le risorse vengono memorizzate in DAM.

### Perché le risorse sono memorizzate in DAM {#why-assets-are-stored-in-dam}

La memorizzazione delle risorse in DAM le rende facilmente accessibili e accessibili. Garantisce che le risorse possano essere sfruttate da numerosi utenti in tutta l&#39;organizzazione o l&#39;ecosistema, compresi partner, clienti e così via.

La maggior parte delle organizzazioni sceglie di archiviare solo le risorse rilevanti per i processi di marketing/LOB a valle (la pubblicazione su canali come il canale Web tramite AEM Sites o altri canali serviti da Adobe Experience Cloud - Marketing Cloud, Advertising Cloud e misurati da Analytics Cloud, fornendo a utenti/partner e così via). Inoltre, le organizzazioni memorizzano le risorse che possono essere sottoposte a un processo di revisione/approvazione in DAM. In questo modo, DAM memorizza principalmente le risorse che hanno alte probabilità di essere sfruttate ed evita di archiviare le risorse inutilizzate.

La memorizzazione delle risorse è inoltre soggetta a considerazioni tecniche e di utilizzo delle risorse. DAM offre servizi aggiuntivi sulle risorse memorizzate, come l’estrazione di metadati, il controllo delle versioni, la generazione di anteprime/transcodifica, la gestione dei riferimenti e l’aggiunta di informazioni sul controllo degli accessi. Questi servizi richiedono tempo e risorse aggiuntive per l&#39;infrastruttura.

Spesso, non è consigliabile memorizzare tutte le risorse e gli aggiornamenti. Ad esempio, se gli aggiornamenti a risorse specifiche sono di scarsa qualità e consumano risorse eccessive, le risorse potrebbero non essere memorizzate in DAM.

#### Quando le risorse vengono memorizzate in DAM {#when-assets-are-stored-in-dam}

I team creativi (e le organizzazioni) solitamente non sono interessati a memorizzare le risorse in ogni fase del ciclo di vita delle risorse. Ad esempio, evitano di memorizzare le risorse nei seguenti casi:

* Risorse che devono ancora essere completate o che devono essere sperimentate
* Risorse che non superano il ciclo di revisione del team creativo/interno
* Rispetto alla risorsa in questione, la squadra ha candidati migliori per rappresentare il proprio lavoro a squadre esterne

In genere, le risorse delle classi seguenti vengono memorizzate in DAM:

* Attività che hanno raggiunto una certa scadenza e sono considerate pronte per essere condivise
* Risorse preselezionate dal team creativo
* Formati di risorse specifici utilizzabili o richiesti dal marketing, a seconda di un contratto o contratto specifico (ad esempio, file JPG convertiti da file RAW, TIFF/immagini da originali PSD)

#### Quando vengono memorizzati gli aggiornamenti delle risorse in DAM {#when-updates-to-assets-are-stored-in-dam}

Di regola, solo gli aggiornamenti alle risorse rilevanti per il più ampio set di utenti DAM devono essere memorizzati in DAM. Essa garantisce che gli utenti (funzioni di marketing e simili) vedano solo le versioni rilevanti nella timeline delle risorse DAM.

In genere, le modifiche sono correlate alle tappe principali del ciclo di vita delle risorse. Ad esempio, la risorsa iniziale pronta per il marketing o un aggiornamento ufficiale basato su richiesta/revisione fornita dal team creativo devono essere memorizzati e dotati di versione in DAM.

L&#39;aggiornamento del team creativo per la revisione da parte del team marketing dopo una richiesta di modifica della risorsa esistente in DAM è un esempio di aggiornamento rilevante. Deve essere memorizzato e conservato in DAM per ulteriori riferimenti o per ripristinare la versione precedente.

Di seguito sono riportati alcuni esempi di aggiornamenti generalmente non rilevanti:

* Versioni precedenti delle risorse caricate prima che siano pronte per la revisione del marketing
* Frequenti modifiche creative alla risorsa nella fase di lavoro in corso prima che i team creativi e di marketing decidano che la risorsa è pronta

### Accesso utente a DAM {#user-access-to-dam}

Risorse AEM supporta due tipi di utenti in base al loro accesso alla distribuzione di Risorse AEM. In genere, gli utenti all&#39;interno della rete aziendale (firewall) hanno accesso diretto a DAM. Gli altri utenti esterni alla rete aziendale non avrebbero accesso diretto. Il tipo di utente determina quali integrazioni possono essere utilizzate dal punto di vista tecnico.

#### Utenti creativi con accesso diretto a DAM {#creative-users-with-direct-access-to-dam}

In genere, i team creativi interni o le agenzie/i professionisti creativi caricati sulla rete interna hanno accesso all’istanza DAM, incluso l’accesso AEM. AEM e l’infrastruttura di rete possono essere configurate per consentire l’accesso diretto alle parti esterne, in genere organizzazioni affidabili come le agenzie che lavorano per un cliente, per accedere ad AEM tramite rete, ad esempio tramite VPN o elenco di indirizzi IP consentiti.

In tali casi, Adobe Asset Link o l’app desktop AEM consente di accedere facilmente alle risorse finali/approvate e di salvare le risorse pronte per la creazione in DAM.

#### Utenti creativi senza accesso a DAM {#creative-users-without-access-to-dam}

Le agenzie esterne e i freelance senza accesso diretto all’istanza DAM possono richiedere l’accesso alle risorse approvate o desiderano aggiungere nuove progettazioni al DAM.

Utilizzate le seguenti strategie per fornire l&#39;accesso alle risorse finali/approvate:

* Utilizzate l’app desktop se il collegamento risorsa non funziona.
* Utilizzare [AEM Assets Brand Portal](https://helpx.adobe.com/it/experience-manager/brand-portal/user-guide.html) per distribuire le risorse in modo sicuro ai partner esterni
* Utilizzare un&#39;implementazione personalizzata di un portale di distribuzione e determinazione origine basato su [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilizzate la configurazione del controllo degli accessi in AEM e l&#39;infrastruttura di rete necessaria (ad esempio, l&#39;elenco delle reti VPN e IP consentite) per consentire alle parti esterne di accedere a un&#39;area dedicata di contenuto nel vostro DAM. Possono utilizzare l’interfaccia utente Web di AEM per ottenere risorse e caricare nuovi contenuti in DAM.

#### Lavoro in corso sulle risorse da AEM {#work-in-progress-on-assets-from-aem}

Come discusso in questo documento, si consiglia di eseguire importanti aggiornamenti sulle risorse, talvolta denominati lavoro in corso, senza che tutte le modifiche salvate nel file locale siano caricate anche su AEM come modifiche. Questo consente di velocizzare il lavoro di un utente desktop, limitare la larghezza di banda utilizzata e mantenere la timeline delle risorse pulita e focalizzata sugli aggiornamenti principali e controllati.

Adobe Asset Link offre un buon supporto per questo caso di utilizzo:

* Quando gli utenti in Photoshop, InDesign o Illustrator intendono modificare un file, eseguono un’operazione di estrazione sulla risorsa specificata
* La risorsa viene scaricata in background, inserita nell’account Creative Cloud sincronizzato su disco dall’app desktop Creative Cloud e il flag di estrazione è attivato in AEM sulla risorsa per ridurre al minimo i conflitti di modifica
* Da qui in poi, l&#39;utente lavora in un file memorizzato localmente nella posizione sincronizzata, e può continuare a lavorare e salvare le modifiche necessarie a qualsiasi frequenza richiesta
* Inoltre, poiché la risorsa si trova nell’account Creative Cloud, è disponibile anche su altri dispositivi che l’utente potrebbe avere (ad esempio, può essere aperta o modificata in un’app mobile Creative Cloud dedicata) e può essere condivisa con altri utenti Creative Cloud a scopo di collaborazione.
* Al termine delle modifiche, l’utente creativo può eseguire un’operazione di check-in sul file nell’applicazione Creative Cloud, con un commento facoltativo. La risorsa corrispondente in AEM dispone di una versione e viene aggiornata con il nuovo binario. Gli utenti AEM, come gli esperti di marketing o gli utenti LOB, possono accedere alle modifiche o alle pietre miliari principali delle risorse tramite l’interfaccia utente della timeline delle risorse AEM.

L&#39;app desktop AEM fornisce una condivisione di rete per le risorse aperte nell&#39;app nativa. Per impostazione predefinita, tutte le modifiche effettuate localmente vengono caricate automaticamente in AEM dopo un breve periodo di tempo. Grazie a questa configurazione, i frequenti risparmi durante la fase di lavoro in corso vengono caricati in AEM e versioni, creando un sacco di traffico di rete e potenziali problemi di scalabilità, per non parlare delle versioni non necessarie in AEM.

L’approccio consigliato consiste nell’utilizzare un’opzione nell’app desktop AEM per disattivare gli aggiornamenti automatizzati e caricare manualmente le modifiche alle risorse in AEM, sfruttando l’azione di caricamento delle modifiche nell’interfaccia utente Stato risorsa dell’app.

#### Caricamento in blocco su DAM {#bulk-upload-to-dam}

In alcuni scenari potrebbe essere necessario caricare simultaneamente un numero maggiore di file in DAM, ad esempio:

* Caricamento dei risultati di photoshot o progetti di dimensioni maggiori
* Caricamento delle risorse fornite dalle agenzie creative
* Caricamento delle risorse selezionate da un set più grande se la selezione viene effettuata al di fuori di DAM

Questa descrizione fa riferimento al caricamento di file operativamente (ad esempio, ogni settimana o con ogni scatto), come parte normale del flusso di lavoro dell&#39;utente desktop. Le migrazioni di risorse di grandi dimensioni non sono incluse in questa sezione.

Potete sfruttare le seguenti funzionalità di caricamento:

* Per caricare cartelle grandi o gerarchiche in massa, utilizzate l&#39;app desktop AEM che fornisce funzionalità di caricamento [delle](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) cartelle. Potete anche caricare strutture di cartelle gerarchiche. Le risorse vengono caricate in background e, di conseguenza, non sono collegate a una sessione del browser Web
* Per caricare alcuni file da una singola cartella, trascinateli direttamente nell’interfaccia Web o utilizzate l’opzione Crea nell’interfaccia Web di Risorse AEM.
* A seconda delle esigenze aziendali, potete anche utilizzare il caricatore personalizzato.

#### Gestione delle risorse digitali direttamente dal desktop {#managing-digital-assets-directly-from-desktop}

Se utilizzate Condivisione file di rete per gestire le risorse digitali, l&#39;utilizzo della condivisione di rete mappata dall&#39;app desktop AEM potrebbe essere considerato un comodo sostituto. Quando si passa da condivisioni di file di rete, l’interfaccia Web di AEM fornisce un set completo di funzionalità di gestione delle risorse digitali che vanno ben oltre quanto possibile su una condivisione di rete (ricerca, raccolte, metadati, collaborazione, anteprime e così via), e l’app desktop AEM fornisce un collegamento pratico per connettere l’archivio DAM lato server al lavoro sul desktop.

Evitate di utilizzare l&#39;app desktop AEM per gestire le risorse direttamente nella condivisione di rete di Risorse AEM. Ad esempio, evitate di utilizzare l&#39;app desktop AEM per spostare/copiare più file. Utilizzate, invece, l&#39;interfaccia utente Web di Risorse AEM per trascinare le cartelle dal Finder/Esplora risorse alla condivisione di rete o utilizzate la funzione di caricamento delle cartelle di Risorse AEM.

<!-- 
#### Asset migration {#asset-migration}

To plan and execute asset migrations from existing system to a new system or migration of large volume of assets stored on servers, see the [Migration Guide](/help/assets/assets-migration-guide.md). AEM desktop app and AEM to Creative Cloud integrations do not support such migrations. Due to the large volumes of assets to be ingested, and additional requirements around metadata mapping, transformation, and ingestion, migrations should be handled using different tools and approaches.
-->
