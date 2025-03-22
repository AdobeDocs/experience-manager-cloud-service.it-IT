---
title: Integrare i visualizzatori Dynamic Media con i tag di Adobe Analytics e Experience Platform
description: Scopri l’estensione Dynamic Media Viewers per tag Experience Platform e visualizzatori Dynamic Media 5.13. Consente ai clienti di Adobe Analytics e Platform Tags di utilizzare eventi e dati specifici per i visualizzatori Dynamic Media nella propria configurazione di tag Experience Platform.
contentOwner: Rick Brough
feature: Asset Reports
role: Admin,User
exl-id: a71fef45-c9a4-4091-8af1-c3c173324b7a
source-git-commit: 05c6c8bcd8140bed9a30179c5a12d3a3fa8cb37d
workflow-type: tm+mt
source-wordcount: '6667'
ht-degree: 6%

---

# Integrare i visualizzatori Dynamic Media con i tag di Adobe Analytics e Experience Platform {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## Cos’è l’integrazione dei visualizzatori Dynamic Media con i tag di Adobe Analytics e Experience Platform? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch 

name used to be Experience Platform Launch. Changed to Experience Platform Data Collection-->

L&#39;estensione *Dynamic Media Viewers* per i tag Experience Platform funziona con Dynamic Media Viewers 5.13. Consente ai clienti dei tag di Adobe Analytics e Experience Platform di utilizzare gli eventi e i dati dei visualizzatori Dynamic Media nelle loro configurazioni di tag.

Grazie a questa integrazione è possibile monitorare l’utilizzo dei visualizzatori Dynamic Media sul sito web con Adobe Analytics. Allo stesso tempo, puoi utilizzare gli eventi e i dati esposti dai visualizzatori con qualsiasi altra estensione Tag di Experience Platform proveniente da Adobe o da terze parti.

Per ulteriori informazioni sulle estensioni Adobe o di terze parti, consulta [Estensioni Adobe](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/overview) nella Guida utente dei tag di Experience Platform.

**Questo argomento è destinato ai seguenti utenti:** amministratori di siti, sviluppatori nel programma Adobe Experience Manager e utenti nelle operazioni.

### Limitazioni dell’integrazione {#limitations-of-the-integration}

* L’integrazione dei tag di Experience Platform per i visualizzatori Dynamic Media non funziona nel nodo di authoring di Experience Manager. Non puoi visualizzare alcun tracciamento da una pagina WCM finché non viene pubblicata.
* L’integrazione dei tag di Experience Platform per i visualizzatori Dynamic Media non è supportata per la modalità operativa pop-up, in cui l’URL del visualizzatore viene ottenuto utilizzando il pulsante &quot;URL&quot; nella pagina Dettagli risorsa.
* L&#39;integrazione dei tag di Experience Platform non può essere utilizzata contemporaneamente all&#39;integrazione dei visualizzatori legacy di Analytics (tramite il parametro `config2=`).
* Il supporto per il tracciamento video è limitato solo al tracciamento della riproduzione di base, come descritto in [Panoramica sul tracciamento](https://experienceleague.adobe.com/en/docs/media-analytics/using/tracking/track-core-overview#player-events). In particolare, QoS, annunci, capitoli/segmenti o tracciamento degli errori non sono supportati.
* La configurazione della durata di archiviazione per gli elementi dati non è supportata per gli elementi dati che utilizzano l&#39;estensione *Dynamic Media Viewers*. La durata dell&#39;archiviazione deve essere impostata su **[!UICONTROL Nessuno]**.

### Casi d’uso per l’integrazione {#use-cases-for-the-integration}

Il caso d’uso principale per l’integrazione con i tag di Experience Platform sono i clienti che utilizzano sia Experience Manager Assets che Experience Manager Sites. In questi scenari, puoi impostare un’integrazione standard tra il nodo di authoring di Experience Manager e i tag di Experience Platform, quindi associare l’istanza Sites alla proprietà Tag di Experience Platform. Successivamente, qualsiasi componente WCM Dynamic Media aggiunto a una pagina Sites tiene traccia dei dati e degli eventi provenienti dai visualizzatori.

Vedi [Tracciare i visualizzatori Dynamic Media in Experience Manager Sites](#tracking-dynamic-media-viewers-in-aem-sites).

Un caso d’uso secondario supportato dall’integrazione è quello dei clienti che utilizzano solo Experience Manager Assets o Dynamic Media Classic. In questi casi, ottieni il codice di incorporamento per il visualizzatore e lo aggiungi alla pagina del sito web. Quindi, ottieni l’URL di produzione della libreria di tag Experience Platform da Tag Experience Platform e aggiungilo manualmente al codice della pagina web.

Vedi [Tracciare i visualizzatori Dynamic Media utilizzando il codice incorporato](#tracking-dynamic-media-viewers-using-embed-code).

## Funzionamento del tracciamento di dati ed eventi nell’integrazione {#how-data-and-event-tracking-works-in-the-integration}

L&#39;integrazione sfrutta due tipi distinti e indipendenti di tracciamento dei visualizzatori Dynamic Media: *Adobe Analytics* e *Adobe Analytics for Audio and Video*.

### Informazioni sul tracciamento con Adobe Analytics {#about-tracking-using-adobe-analytics}

Adobe Analytics consente di tenere traccia delle azioni eseguite da un utente durante l’interazione con i visualizzatori Dynamic Media sul sito web. Adobe Analytics consente inoltre di tenere traccia dei dati specifici del visualizzatore. Ad esempio, puoi tenere traccia e registrare gli eventi di caricamento della visualizzazione insieme al nome della risorsa, alle azioni di zoom che si sono verificate e alle azioni di riproduzione video.

Nei tag di Experience Platform, i concetti di *Elementi dati* e *Regole* funzionano insieme per abilitare il tracciamento di Adobe Analytics.

#### Informazioni sugli elementi dati nei tag di Experience Platform {#about-data-elements-in-adobe-launch}

Un elemento dati nei tag di Experience Platform è una proprietà denominata il cui valore è definito in modo statico o calcolato in modo dinamico in base allo stato di una pagina web o dei dati dei visualizzatori Dynamic Media.

Le opzioni disponibili per la definizione di un elemento dati dipendono dall’elenco delle estensioni installate nella proprietà Tag di Experience Platform. L’estensione &quot;Core&quot; è preinstallata ed è disponibile come strumento predefinito in qualsiasi configurazione. Questa estensione &quot;Core&quot; consente di definire un elemento dati il cui valore proviene da cookie, codice JavaScript, stringa di query e molte altre origini.

Per il tracciamento di Adobe Analytics è necessario installare diverse altre estensioni, come descritto in [Installazione e configurazione di estensioni](#installing-and-setup-of-extensions). L’estensione Dynamic Media Viewers consente di definire un elemento dati; tale valore è un argomento dell’evento Dynamic Viewer. Ad esempio, è possibile fare riferimento al tipo di visualizzatore o al nome della risorsa indicato dal visualizzatore al momento del caricamento, al livello di zoom indicato quando l’utente finale esegue lo zoom e molto altro.

L’estensione Dynamic Media Viewer mantiene automaticamente aggiornati i valori degli elementi dati.

Dopo averlo definito, un elemento dati può essere utilizzato in altre posizioni dell’interfaccia utente Tag di Experience Platform, utilizzando il widget del selettore Elemento dati. L&#39;**azione Imposta variabili** dell&#39;estensione Adobe Analytics in una regola fa riferimento agli elementi dati definiti per il tracciamento dei visualizzatori Dynamic Media (vedi di seguito).

Vedi [Data elements](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements) nella Guida utente di Experience Platform Tags.

#### Informazioni sulle regole nei tag di Experience Platform {#about-rules-in-adobe-launch}

Una regola nei tag di Experience Platform è una configurazione agnostica che definisce tre aree che compongono una regola: *Eventi*, *Condizioni* e *Azioni*:

* *Eventi* (if) indica ai tag di Experience Platform quando attivare una regola.
* *Condizioni* (if) indica ad Experience Platform Tags le altre restrizioni da consentire o non consentire quando si attiva una regola.
* *Azioni* (quindi) indica ai tag di Experience Platform cosa fare quando viene attivata una regola.

Le opzioni disponibili nella sezione Eventi, Condizioni e Azioni dipendono dalle estensioni installate nella proprietà Tag di Experience Platform. L&#39;estensione *Core* è preinstallata ed è disponibile come strumento predefinito in qualsiasi configurazione. L’estensione fornisce diverse opzioni per Eventi, come azioni di base a livello di browser che includono modifiche dello stato attivo, pressioni di tasti e invio di moduli. Include inoltre opzioni per le Condizioni, come valore del cookie, tipo di browser e altro ancora. Per Azioni, è disponibile solo l’opzione Codice personalizzato.

Per il tracciamento di Adobe Analytics, è necessario installare diverse altre estensioni, come descritto in [Installazione e configurazione di estensioni](#installing-and-setup-of-extensions). In particolare:

* L’estensione Dynamic Media Viewers estende l’elenco degli eventi supportati agli eventi specifici dei visualizzatori Dynamic Media, come caricamento del visualizzatore, scambio di risorse, zoom in e riproduzione video.
* L&#39;estensione Adobe Analytics estende l&#39;elenco delle azioni supportate con due azioni necessarie per inviare dati ai server di tracciamento: *Imposta variabili* e *Invia beacon*.

Per tenere traccia dei visualizzatori Dynamic Media, è possibile utilizzare uno dei seguenti tipi:

* Eventi dall’estensione Dynamic Media Viewers, dall’estensione Core o da qualsiasi altra estensione.
* Condizioni nella definizione della regola. In alternativa, è possibile lasciare vuota l&#39;area delle condizioni.

Nella sezione Azioni è necessario disporre di un&#39;azione *Imposta variabili*. Questa azione spiega ad Adobe Analytics come popolare le variabili di tracciamento con i dati. Allo stesso tempo, l&#39;azione *Imposta variabili* non invia nulla al server di tracciamento.

L&#39;azione **Invia beacon** deve seguire l&#39;azione **Imposta variabili**. L&#39;azione *Invia beacon* invia effettivamente i dati al server di tracciamento di Analytics. Entrambe le azioni, *Imposta variabili* e *Invia beacon*, provengono dall&#39;estensione Adobe Analytics.

Consulta le [Regole](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules) nella Guida utente dei tag di Experience Platform.

#### Configurazione di esempio {#sample-configuration}

La seguente configurazione di esempio all’interno dei tag di Experience Platform illustra come tenere traccia del nome di una risorsa al caricamento del visualizzatore.

1. Dalla scheda **[!UICONTROL Elementi dati]**, definisci un elemento dati `AssetName` che faccia riferimento al parametro `asset` dell&#39;evento `LOAD` dall&#39;estensione Dynamic Media Viewers.

   ![immagine2019-11](assets/image2019-11.png)

1. Dalla scheda **[!UICONTROL Regole]**, definisci una regola *TrackAssetOnLoad*.

   In questa regola, il campo **[!UICONTROL Event]** utilizza l&#39;evento **[!UICONTROL LOAD]** dell&#39;estensione Dynamic Media Viewers.

   ![immagine2019-22](assets/image2019-22.png)

1. La configurazione dell&#39;azione dispone di due tipi di azione dell&#39;estensione Adobe Analytics:

   *Imposta variabili*, che mappano una variabile di analisi scelta al valore di `AssetName` elemento dati.

   *Invia beacon*, che invia informazioni di tracciamento ad Adobe Analytics.

   ![immagine2019-3](assets/image2019-3.png)

1. La configurazione della regola risultante viene visualizzata come segue:

   ![immagine2019-4](assets/image2019-4.png)

### Informazioni su Adobe Analytics per audio e video {#about-adobe-analytics-for-audio-and-video}

Quando un account Experience Cloud è abbonato per utilizzare Adobe Analytics for Audio and Video, è sufficiente abilitare il tracciamento video nelle impostazioni dell&#39;estensione *Dynamic Media Viewers*. Le metriche video diventano disponibili in Adobe Analytics. Il tracciamento video dipende dalla presenza dell’estensione Adobe Media Analytics for Audio and Video.

Consulta [Installazione e configurazione delle estensioni](#installing-and-setup-of-extensions).

Attualmente, il supporto per il tracciamento dei video è limitato solo al tracciamento della &quot;riproduzione di base&quot;, come descritto in [Panoramica sul tracciamento](https://experienceleague.adobe.com/en/docs/media-analytics/using/tracking/track-core-overview#player-events). In particolare, QoS, annunci, capitoli/segmenti o tracciamento degli errori non sono supportati.

## Utilizzare l’estensione Dynamic Media Viewers {#using-the-dynamic-media-viewers-extension}

Come indicato in [Casi d&#39;uso per l&#39;integrazione](#use-cases-for-the-integration), è possibile tenere traccia dei visualizzatori Dynamic Media con la nuova integrazione dei tag Experience Platform in Experience Manager Sites e utilizzando il codice di incorporamento.

### Tracciare i visualizzatori Dynamic Media in Experience Manager Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Per tenere traccia dei visualizzatori Dynamic Media in Experience Manager Sites, è necessario eseguire tutti i passaggi elencati nella sezione [Configurare tutte le parti dell&#39;integrazione](#configuring-all-the-integration-pieces). In particolare, devi creare la configurazione IMS e la configurazione cloud dei tag di Experience Platform.

Dopo la configurazione corretta, qualsiasi visualizzatore Dynamic Media aggiunto a una pagina Sites, utilizzando un componente WCM supportato da Dynamic Media, tiene traccia automaticamente dei dati in Adobe Analytics, Adobe Analytics for Video o in entrambi.

Consulta [Aggiungere Dynamic Media Assets alle pagine tramite Adobe Sites](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

### Tracciare i visualizzatori Dynamic Media utilizzando il codice di incorporamento {#tracking-dynamic-media-viewers-using-embed-code}

I clienti che non utilizzano Experience Manager Sites o che incorporano visualizzatori Dynamic Media in pagine web al di fuori di Experience Manager Sites, o in entrambi, possono comunque utilizzare l’integrazione Experience Platform Tags.

Completa i passaggi di configurazione dalle sezioni [Configura Adobe Analytics](#configuring-adobe-analytics-for-the-integration) e [Configura tag Experience Platform](#configuring-adobe-launch-for-the-integration). Tuttavia, i passaggi di configurazione relativi ad Experience Manager non sono necessari.

Dopo aver configurato correttamente il sistema, puoi aggiungere il supporto per tag Experience Platform a una pagina web con un visualizzatore Dynamic Media.

Consulta [Aggiungere il codice di incorporamento dei tag di Experience Platform](https://experienceleague.adobe.com/en/docs/platform-learn/implement-in-websites/configure-tags/add-embed-code) per ulteriori informazioni su come utilizzare il codice di incorporamento della libreria di tag di Experience Platform.

Per ulteriori informazioni sull&#39;utilizzo della funzionalità del codice incorporato di Experience Manager Dynamic Media, consulta [Incorporazione di un visualizzatore di video o immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).

**Traccia i visualizzatori Dynamic Media utilizzando il codice incorporato:**

1. Prepara una pagina web per incorporare un visualizzatore Dynamic Media.
1. Ottieni il codice di incorporamento per la libreria di tag Experience Platform effettuando prima l&#39;accesso a Tag Experience Platform (consulta [Configurare i tag Experience Platform](#configuring-adobe-launch-for-the-integration)).
1. Seleziona **[!UICONTROL Proprietà]**, quindi fai clic sulla scheda **[!UICONTROL Ambienti]**.
1. Scegli il livello di ambiente pertinente all’ambiente della pagina web. Quindi, nella colonna **[!UICONTROL Installa]**, fare clic sull&#39;icona della casella.
1. **[!UICONTROL Nella finestra di dialogo Istruzioni per l&#39;installazione Web]**, copia il codice di incorporamento completo della libreria Experience Platform Tags, insieme ai tag `<script/>` circostanti.

## Guida di riferimento per l’estensione Dynamic Media Viewers {#reference-guide-for-the-dynamic-media-viewers-extension}

### Informazioni sulla configurazione dei visualizzatori Dynamic Media {#about-the-dynamic-media-viewers-configuration}

L’estensione Dynamic Media Viewer si integra automaticamente con la libreria di tag di Experience Platform se sono soddisfatte le seguenti condizioni:

* L&#39;oggetto globale della libreria Tag di Experience Platform ( `_satellite`) è presente nella pagina.
* La funzione di estensione dei visualizzatori Dynamic Media `_dmviewers_v001()` è definita su `_satellite`.

* Il parametro del visualizzatore `config2=` non è specificato, pertanto il visualizzatore non utilizza l&#39;integrazione legacy di Analytics.

È inoltre disponibile un&#39;opzione per disabilitare esplicitamente l&#39;integrazione dei tag di Experience Platform nel visualizzatore specificando il parametro `launch=0` nella configurazione del visualizzatore. Il valore predefinito di questo parametro è `1`.

### Configurare l’estensione Dynamic Media Viewers {#configuring-the-dynamic-media-viewers-extension}

L&#39;unica opzione di configurazione per l&#39;estensione Dynamic Media Viewers è **[!UICONTROL Enable Adobe Media Analytics for Audio and Video]**.

Quando selezioni (abilita) questa opzione e l’estensione Adobe Media Analytics for Audio and Video viene installata e configurata, le metriche di riproduzione video vengono inviate alla soluzione Adobe Analytics for Audio and Video. La disattivazione di questa opzione disattiva il tracciamento video.

Se abiliti questa opzione *senza* aver installato l&#39;estensione Adobe Media Analytics for Audio and Video, l&#39;opzione non ha alcun effetto.

![immagine2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Informazioni sugli elementi dati nell’estensione Dynamic Media Viewers {#about-data-elements-in-the-dynamic-media-viewers-extension}

L’unico tipo di elemento di dati fornito dall’estensione Dynamic Media Viewers è **[!UICONTROL Evento visualizzatore]**, proveniente dall’elenco a discesa **[!UICONTROL Data Element Type (Tipo di elemento dati)]**.

Quando è selezionato, l’editor elementi dati esegue il rendering di un modulo con due campi:

* **[!UICONTROL Tipo di dati evento visualizzatori DM]**: in un elenco a discesa vengono visualizzati tutti gli eventi visualizzatore con argomenti supportati dall&#39;estensione Dynamic Media Viewers, insieme a un elemento speciale **[!UICONTROL COMMON]**. Un elemento **[!UICONTROL COMMON]** rappresenta un elenco di parametri evento che sono comuni a tutti i tipi di eventi inviati dai visualizzatori.
* **[!UICONTROL Parametro di tracciamento]**: argomento dell&#39;evento visualizzatore Dynamic Media selezionato.

![immagine2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

Per l&#39;elenco degli eventi supportati per ciascun tipo di visualizzatore, consulta la [guida di riferimento per visualizzatori Dynamic Media](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers). Vai alla sezione del visualizzatore specifico, quindi seleziona la sottosezione Supporto per il tracciamento di Adobe Analytics. Attualmente, la guida di riferimento per i visualizzatori Dynamic Media non documenta gli argomenti dell’evento.

Consideriamo ora il ciclo di vita dei visualizzatori Dynamic Media *Elemento dati*. Il valore di tale elemento dati viene popolato dopo che l’evento visualizzatore Dynamic Media corrispondente si verifica sulla pagina. Si supponga ad esempio che l&#39;elemento dati punti all&#39;evento **[!UICONTROL LOAD]** e al relativo argomento &quot;asset&quot;. Il valore di tale elemento dati riceve dati validi dopo che il visualizzatore ha eseguito l&#39;evento LOAD per la prima volta. Se l&#39;elemento dati punta all&#39;evento **[!UICONTROL ZOOM]** e al relativo argomento &quot;scale&quot;, il valore di tale elemento dati rimane vuoto finché il visualizzatore non invia un evento **[!UICONTROL ZOOM]** per la prima volta.

Allo stesso modo, i valori di Elementi dati vengono aggiornati automaticamente quando il visualizzatore invia un evento corrispondente sulla pagina. L’aggiornamento del valore si verifica anche se l’evento specifico non è indicato nella configurazione Regola. Si supponga ad esempio che l&#39;elemento dati **[!UICONTROL ZoomScale]** sia definito per il parametro &quot;scale&quot; dell&#39;evento ZOOM. Tuttavia, l&#39;evento **[!UICONTROL LOAD]** è l&#39;unico trigger nella configurazione della regola. Il valore di **[!UICONTROL ZoomScale]** viene comunque aggiornato ogni volta che un utente esegue lo zoom all&#39;interno del visualizzatore.

Qualsiasi visualizzatore Dynamic Media è dotato di un identificatore univoco sulla pagina web. L’elemento dati tiene traccia del valore stesso e del visualizzatore che lo ha popolato. Si supponga, ad esempio, che nella stessa pagina siano presenti più visualizzatori e un elemento dati **[!UICONTROL AssetName]** che punta all&#39;evento **[!UICONTROL LOAD]** e al relativo argomento &quot;asset&quot;. L&#39;elemento dati **[!UICONTROL AssetName]** mantiene una raccolta di nomi di risorse associati a ciascun visualizzatore caricato sulla pagina.

Il valore esatto restituito dall’elemento dati dipende dal contesto. Se una regola attivata da un evento visualizzatore Dynamic Media richiede l’elemento dati, il valore viene restituito per il visualizzatore che ha avviato la regola. Se una regola attivata da un evento di un’altra estensione Experience Platform Tags richiede l’elemento dati, segue il contesto dell’evento corrispondente. A quel punto, il valore dell’elemento dati proviene dal visualizzatore che è stato l’ultimo ad aggiornare questo elemento dati.

**Considerare la seguente configurazione di esempio:**

* Pagina Web con due visualizzatori zoom di Dynamic Media: *visualizzatore1* e *visualizzatore2*.

* L&#39;elemento dati **[!UICONTROL ZoomScale]** punta all&#39;evento **[!UICONTROL ZOOM]** e al relativo argomento &quot;scale&quot;.
* **[!UICONTROL Regola TrackPan]** con quanto segue:

   * Utilizza l&#39;evento **[!UICONTROL PAN]** del visualizzatore Dynamic Media come attivatore.
   * Invia il valore dell&#39;elemento dati **[!UICONTROL ZoomScale]** ad Adobe Analytics.

* Regola **[!UICONTROL TrackKey]** con:

   * Utilizza l’evento di pressione chiave dall’estensione Core Experience Platform Tags come attivatore.
   * Invia il valore dell&#39;elemento dati **[!UICONTROL ZoomScale]** ad Adobe Analytics.

Ora, supponiamo che l’utente carichi la pagina web con i due visualizzatori. In *visualizzatore1* viene eseguito lo zoom avanti del 50%, quindi in *visualizzatore2* viene eseguito lo zoom avanti del 25%. In *viewer1*, viene eseguita la panoramica dell&#39;immagine e infine viene premuto un tasto sulla tastiera.

L’attività dell’utente comporta l’esecuzione delle seguenti due chiamate di tracciamento ad Adobe Analytics:

* La prima chiamata si verifica perché la regola **[!UICONTROL TrackPan]** viene attivata quando l&#39;utente effettua la panoramica in *visualizzatore1*. La chiamata invia **50%** come valore dell&#39;elemento dati **[!UICONTROL ZoomScale]** perché riconosce che *viewer1* ha attivato la regola e recupera il valore di scala corrispondente;
* La seconda chiamata si verifica perché la regola **[!UICONTROL TrackKey]** viene attivata quando l&#39;utente ha premuto un tasto sulla tastiera. La chiamata invia il 25% come valore dell&#39;elemento dati **[!UICONTROL ZoomScale]** perché il visualizzatore non ha attivato la regola. Di conseguenza, l’elemento dati restituisce il valore più aggiornato.

Il campione impostato sopra influisce anche sulla durata del valore dell’elemento dati. Il valore dell’elemento dati gestito dal visualizzatore Dynamic Media viene memorizzato nel codice della libreria di tag di Experience Platform anche dopo che il visualizzatore stesso è stato eliminato sulla pagina web. Questa funzionalità significa che se una regola attivata da un’estensione non Dynamic Media Viewer fa riferimento all’elemento dati, restituisce l’ultimo valore noto. Anche se il visualizzatore non è più presente nella pagina web.

In ogni caso, i valori degli elementi dati guidati dai visualizzatori Dynamic Media non vengono memorizzati nell’archiviazione locale o sul server, ma vengono conservati solo nella libreria di tag Experience Platform lato client. I valori di tale elemento dati scompaiono quando la pagina web viene ricaricata.

In genere, l&#39;editor degli elementi dati supporta la selezione della durata di archiviazione [](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements#create-a-data-element). Tuttavia, gli elementi dati che utilizzano l&#39;estensione Dynamic Media Viewers supportano solo l&#39;opzione di durata di archiviazione **[!UICONTROL None]**. Nell’interfaccia utente è possibile impostare qualsiasi altro valore, ma in questo caso il comportamento dell’elemento dati non è definito. L’estensione gestisce il valore dell’elemento dati singolarmente: l’elemento dati che mantiene il valore dell’argomento evento visualizzatore durante l’intero ciclo di vita del visualizzatore.

### Informazioni sulle regole nell’estensione Dynamic Media Viewers {#about-rules-in-the-dynamic-media-viewers-extension}

Nell’editor delle regole, l’estensione aggiunge nuove opzioni di configurazione per l’editor degli eventi. Inoltre, l’editor fornisce un’opzione per fare riferimento manualmente ai parametri dell’evento nell’editor azioni come opzione a breve termine, invece di utilizzare elementi dati preconfigurati.

#### Informazioni sull’editor eventi {#about-the-events-editor}

Nell&#39;editor eventi, l&#39;estensione Dynamic Media Viewers aggiunge un **[!UICONTROL Tipo evento]** denominato **[!UICONTROL Evento visualizzatore]**.

Quando è selezionato, l&#39;editor eventi visualizza il menu a discesa **[!UICONTROL Eventi visualizzatore Dynamic Media]**, in cui sono elencati tutti gli eventi supportati dai visualizzatori Dynamic Media.

![immagine2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Informazioni sull’editor delle azioni {#about-the-actions-editor}

L’estensione Dynamic Media Viewers consente di utilizzare i parametri evento dei visualizzatori Dynamic Media per la mappatura sulle variabili di analisi nell’editor di variabili Set dell’estensione Adobe Analytics.

Il metodo più semplice per farlo consiste nel completare il seguente processo in due fasi:

* Innanzitutto, definisci uno o più elementi dati, in cui ogni elemento dati rappresenta un parametro di un evento Dynamic Media Viewer.
* Infine, nell&#39;editor Set Variables dell&#39;estensione Adobe Analytics, fai clic sull&#39;icona ![Dati, selettore elemento dati](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Selettore elemento dati** per aprire la finestra di dialogo Seleziona elemento dati, quindi fai clic su un elemento dati da essa.

![immagine2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

È tuttavia possibile adottare un approccio alternativo e ignorare la creazione di elementi dati. È possibile fare riferimento diretto a un argomento da un evento Dynamic Media Viewer. Immetti il nome completo dell&#39;argomento evento nel campo di input **[!UICONTROL value]** dell&#39;assegnazione della variabile Analytics. Assicurarsi che i segni di percentuale (%) siano circondati. Ad esempio,

`%event.detail.dm.LOAD.asset%`

![immagine2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Esiste una differenza importante tra l’utilizzo degli elementi dati e il riferimento diretto agli argomenti dell’evento. Per l’elemento dati, non importa quale evento attiva l’azione Imposta variabili. L’evento che attiva la Regola può non essere correlato al Visualizzatore dinamico (come la selezione della pagina web dall’estensione Core). Tuttavia, quando si utilizza un riferimento diretto all’argomento, è importante assicurarsi che l’evento che attiva la regola corrisponda all’argomento dell’evento a cui fa riferimento.

Ad esempio, se l&#39;evento **[!UICONTROL LOAD]** dall&#39;estensione Dynamic Media Viewer attiva la regola, il riferimento a `%event.detail.dm.LOAD.asset%` restituisce il nome corretto della risorsa.

Tuttavia, restituisce un valore vuoto per qualsiasi altro evento.

Nella tabella seguente sono elencati gli eventi di Dynamic Media Viewer e i relativi argomenti supportati:

<table>
 <tbody>
  <tr>
   <td>Nome evento visualizzatore</td>
   <td>Riferimento argomento</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code><br /> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## Configurare tutte le parti dell’integrazione {#configuring-all-the-integration-pieces}

**PRIMA DI INIZIARE**

Adobe consiglia di consultare attentamente tutta la documentazione che precede questa sezione per comprendere appieno l’integrazione completa.

Questa sezione descrive i passaggi di configurazione necessari per integrare i visualizzatori Dynamic Media con Adobe Analytics e Adobe Analytics for Audio and Video. Anche se è possibile utilizzare l’estensione Dynamic Media Viewers per altri scopi nei tag di Experience Platform, tali scenari non sono trattati in questa documentazione.

Stai per utilizzare i seguenti prodotti Adobe per configurare la tua integrazione:

* Adobe Analytics: utilizzato per configurare variabili e rapporti di tracciamento.
* Tag di Experience Platform: utilizzati per definire una proprietà, una o più regole e uno o più elementi dati per abilitare il tracciamento del visualizzatore.

Inoltre, se questa soluzione di integrazione viene utilizzata con Experience Manager Sites, è necessario eseguire la configurazione seguente:

* [Adobe Developer Console](https://developer.adobe.com/console/home) - integrazione creata per i tag Experience Platform.
* Nodo di authoring di Experience Manager: configurazione IMS e configurazione cloud di tag Experience Platform.

Come parte della configurazione, accertati di avere accesso a una società in Adobe Experience Cloud per la quale sono già abilitati i tag di Adobe Analytics e Experience Platform.

## Configurare Adobe Analytics per l’integrazione {#configuring-adobe-analytics-for-the-integration}

Dopo aver configurato Adobe Analytics, l’integrazione è impostata per:

* È presente una suite di rapporti selezionata.
* Le variabili di Analytics sono disponibili per ricevere i dati di tracciamento.
* I rapporti sono disponibili per visualizzare i dati raccolti all’interno di Adobe Analytics.

Vedi anche [Guida all&#39;implementazione di Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/home).

**Per configurare Adobe Analytics per l&#39;integrazione:**

1. Per iniziare, accedi ad Adobe Analytics dalla [home page](https://experience.adobe.com/#/home) di Experience Cloud. Sulla barra dei menu, fai clic sull&#39;icona ![App, soluzioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) **Soluzioni** nell&#39;angolo superiore destro della pagina, quindi seleziona **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Ora, seleziona una suite di rapporti.

### Seleziona una suite di rapporti {#selecting-a-report-suite}

1. Nell’angolo in alto a destra della pagina Adobe Analytics, alla destra del campo **[!UICONTROL Search Reports (Cerca rapporti)]**, seleziona la report suite corretta dall’elenco a discesa. Se sono disponibili più suite di rapporti e non sai quale utilizzare, chiedi assistenza. L’amministratore di Adobe Analytics può guidarti nella selezione della suite di rapporti appropriata.

   Nell&#39;esempio seguente, un utente ha creato una suite di rapporti denominata *DynamicMediaViewersExtensionDoc* e l&#39;ha selezionata dall&#39;elenco a discesa. Il nome della suite di rapporti è solo un esempio. Spetta a te scegliere il nome della suite di rapporti da selezionare.

   Adobe Analytics Se non è disponibile alcuna suite di rapporti, è necessario crearne una prima di poter procedere con la configurazione.

   Consulta [Report e suite di rapporti](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin) e [Crea una suite di rapporti](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

   In Adobe Analytics, le suite di rapporti sono gestite in **[!UICONTROL Admin]** > **[!UICONTROL Suite di rapporti]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   Ora, imposta le variabili Adobe Analytics.

### Configurare le variabili Adobe Analytics {#setting-up-adobe-analytics-variables}

1. Designa una o più variabili Adobe Analytics da utilizzare per monitorare il comportamento dei visualizzatori Dynamic Media sulla pagina web.

   Puoi utilizzare qualsiasi tipo di variabile supportato da Adobe Analytics. L&#39;implementazione di Analytics deve determinare il tipo di variabile appropriato, ad esempio Traffico personalizzato (`props`) o Conversione (`eVar`).

   Vedi [Panoramica di proprietà ed eVar](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/evar#vars).

   Ai fini di questa documentazione, viene utilizzata solo una variabile Traffico personalizzato (prop) perché diventano disponibili in un rapporto di Analytics entro pochi minuti dopo che si è verificata un’azione su una pagina web.

   Per abilitare una nuova variabile di traffico personalizzata, vai a **[!UICONTROL Amministratore]** > **[!UICONTROL Suite per report]** in Adobe Analytics sulla barra degli strumenti.

1. Nella pagina **[!UICONTROL Gestione suite di rapporti]**, seleziona il rapporto corretto.
1. Sulla barra degli strumenti fare clic su **[!UICONTROL Modifica impostazioni]** > **[!UICONTROL Traffico]** > **[!UICONTROL Variabili di traffico]**.
1. Selezionare una variabile inutilizzata, assegnarle un nome descrittivo (**[!UICONTROL Risorsa visualizzatore (prop 30)]**), quindi modificare la casella combinata in &quot;Abilitato&quot; nella colonna Abilitato.

   La schermata seguente è un esempio di variabile di traffico personalizzata (**[!UICONTROL prop30]**) per il tracciamento di un nome di risorsa utilizzato dal visualizzatore:

   ![immagine2019-6-26_23-6-59](/help/assets/dynamic-media/assets/image2019-6-26_23-6-59.png)

1. Nella parte inferiore dell&#39;elenco delle variabili fare clic su **[!UICONTROL Salva]**.

### Configurare un rapporto {#setting-up-a-report}

In genere, un progetto specifico richiede come impostare un rapporto in Adobe Analytics. Pertanto, la configurazione di un rapporto dettagliato va oltre lo scopo di questa integrazione.

È tuttavia sufficiente sapere che i report Traffico personalizzato diventano automaticamente disponibili in Adobe Analytics dopo la configurazione delle variabili Traffico personalizzato in **[Imposta variabili Adobe Analytics](#setting-up-adobe-analytics-variables)**.

Ad esempio, il rapporto per la variabile **[!UICONTROL Viewer asset (Risorsa visualizzatore) (prop 30)]** è disponibile dal menu Rapporti in **[!UICONTROL Traffico personalizzato]** > **[!UICONTROL Traffico personalizzato 21-30]** > **[!UICONTROL Viewer asset (Risorsa visualizzatore) (prop 30)]**.

Se accedi a questo rapporto subito dopo la creazione di **[!UICONTROL Viewer asset (Risorsa visualizzatore) (prop 30)]** non troverai alcun dato, il che è piuttosto normale a questo punto dell’integrazione.

![immagine2019-6-26_23-12-49](/help/assets/dynamic-media/assets/image2019-6-26_23-12-49.png)

## Configurare i tag di Experience Platform per l’integrazione {#configuring-adobe-launch-for-the-integration}

Dopo aver configurato i tag di Experience Platform, per l’integrazione vengono impostati i seguenti elementi:

* La creazione di una nuova Proprietà per mantenere unite tutte le configurazioni.
* Installazione e configurazione delle estensioni. Il codice lato client di tutte le estensioni installate nella proprietà viene compilato insieme in una libreria. Questa libreria viene utilizzata dalla pagina web in un secondo momento.
* Configurazione di elementi dati e regole. Questa configurazione definisce quali dati acquisire dai visualizzatori Dynamic Media, quando attivare la logica di tracciamento e dove inviare i dati del visualizzatore in Adobe Analytics.
* Pubblicazione della libreria.

**Per configurare i tag Experience Platform per l&#39;integrazione:**

1. Per iniziare, accedi ai tag di Experience Platform dalla [home page](https://experience.adobe.com/#/home) di Experience Cloud. Sulla barra dei menu, fai clic sull&#39;icona ![App, soluzioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) **Soluzioni** nell&#39;angolo superiore destro della pagina, quindi fai clic su **[!UICONTROL Tag]**.

   ![immagine2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Creare una proprietà nei tag di Experience Platform {#creating-a-property-in-adobe-launch}

Una proprietà in Experience Platform Tags è una configurazione denominata che mantiene tutte le impostazioni unite. Viene generata e pubblicata una libreria delle impostazioni di configurazione a diversi livelli di ambiente (sviluppo, staging e produzione).

Vedere anche [Configurare una proprietà di selezione](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/configure-tags).

**Per creare una proprietà in Experience Platform Tags:**

1. In Tag Experience Platform, fai clic su **[!UICONTROL Nuova proprietà]**.
1. Nella finestra di dialogo **[!UICONTROL Crea proprietà]**, digita un nome descrittivo nel campo **[!UICONTROL Nome]**, ad esempio il titolo del tuo sito web. Ad esempio `DynamicMediaViewersProp.`
1. Nel campo **[!UICONTROL Domini]**, immetti il dominio del tuo sito Web.
1. Nel menu a discesa **[!UICONTROL Opzioni avanzate]**, abilita **[!UICONTROL Configura per lo sviluppo dell&#39;estensione (non potrà essere modificata in seguito)]** nel caso in cui l&#39;estensione che desideri utilizzare - in questo caso, *Visualizzatori Dynamic Media* - non sia ancora stata rilasciata.

   ![immagine2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Seleziona **[!UICONTROL Salva]**.

   Selezionare la proprietà creata, quindi passare a *Installazione e configurazione delle estensioni*.

### Installazione e configurazione delle estensioni {#installing-and-setup-of-extensions}

Tutte le estensioni disponibili nei tag di Experience Platform sono elencate in **[!UICONTROL Estensioni]** > **[!UICONTROL Catalogo]**.

Per installare un&#39;estensione, fare clic su **[!UICONTROL Installa]**. Se necessario, eseguire una configurazione di estensione una tantum, quindi fare clic su **[!UICONTROL Salva]**.

Se necessario, è necessario installare e configurare le seguenti estensioni:

* (Obbligatorio) *Estensione del servizio Experience Cloud ID*

Non è necessaria alcuna configurazione aggiuntiva, ad eccezione di eventuali valori proposti. Al termine, fai clic su **[!UICONTROL Salva]**.

Consulta [Estensione del servizio Experience Cloud Identity](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/id-service/overview).

* (Obbligatorio) Estensione *Adobe Analytics*

Per configurare questa estensione, è necessario disporre dell&#39;ID Report Suite trovato in Adobe Analytics, in **[!UICONTROL Admin]** > **[!UICONTROL Report Suite]**, nell&#39;intestazione della colonna **[!UICONTROL Report Suite ID]**.

(Solo a scopo dimostrativo, l&#39;ID suite di rapporti della suite di rapporti **[!UICONTROL DynamicMediaViewersExtensionDoc]** viene utilizzato nelle schermate seguenti. Questo ID è stato creato e utilizzato nella precedente sezione [Selezione di una report suite](#selecting-a-report-suite).

![immagine2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

Nella pagina Installa estensione, immetti l’ID Report Suite nel campo **[!UICONTROL Development Report Suites]** (Report Suite di sviluppo), nel campo **[!UICONTROL Staging Report Suites]** (Report Suite di staging) e nel campo **[!UICONTROL Production Report Suites]** (Report Suite di produzione).

![immagine2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Configurare l&#39;elemento seguente solo se si intende utilizzare il tracciamento video:*

Nella pagina **[!UICONTROL Installa estensione]**, espandi **[!UICONTROL Generale]**, quindi specifica il server di tracciamento. Il server di tracciamento segue il modello `<trackingNamespace>.sc.omtrdc.net`, dove `<trackingNamespace>` è l&#39;informazione ottenuta nell&#39;e-mail di provisioning.

Seleziona **[!UICONTROL Salva]**.

Consulta [Estensione Adobe Analytics](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/analytics/overview).

* (Facoltativo. Richiesto solo se è necessario il tracciamento video) *Estensione Adobe Media Analytics for Audio and Video*

Compila il campo del server di tracciamento. Il server di tracciamento per l&#39;estensione *Adobe Media Analytics for Audio and Video* è diverso dal server di tracciamento utilizzato per Adobe Analytics. Segue il modello `<trackingNamespace>.hb.omtrdc.net`, dove `<trackingNamespace>` è l&#39;informazione dell&#39;e-mail di provisioning.

Tutti gli altri campi sono facoltativi.

Consulta [Estensione Adobe Media Analytics for Audio and Video](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/media-analytics/overview).

* (Obbligatorio) *Estensione Dynamic Media Viewers*

Per attivare il tracking Video Heartbeat, seleziona **[!UICONTROL enable Adobe Analytics for Video (Abilita Adobe Analytics per video)]**.

Al momento della scrittura, l&#39;estensione *Dynamic Media Viewers* è disponibile solo se è stata creata la proprietà Experience Platform Tags per lo sviluppo.

Consulta [Creare una proprietà in Experience Platform Tags](#creating-a-property-in-adobe-launch).

Dopo l’installazione e la configurazione delle estensioni, almeno le cinque estensioni seguenti (quattro se non stai tracciando il video) sono elencate nell’area Estensioni > Installate.

![immagine2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Impostare elementi dati e regole {#setting-up-data-elements-and-rules}

In Tag di Experience Platform, crea elementi dati e regole necessari per il tracciamento dei visualizzatori Dynamic Media.

Per una panoramica del tracciamento con i tag Experience Platform, consulta [Funzionamento del tracciamento di dati ed eventi nell&#39;integrazione](#how-data-and-event-tracking-works-in-the-integration).

Vedi [Configurazione di esempio](#sample-configuration) per una configurazione di esempio in Tag di Experience Platform che illustra come tenere traccia del nome di una risorsa al caricamento del visualizzatore.

Consulta [Configurare l&#39;estensione Dynamic Media Viewers](#configuring-the-dynamic-media-viewers-extension) per informazioni approfondite sulle funzionalità dell&#39;estensione.

### Pubblicare una libreria {#publishing-a-library}

Per modificare la configurazione dei tag di Experience Platform (incluse le impostazioni di Proprietà, Estensioni, Regole ed Elementi dati), devi *pubblicare* tali modifiche. La pubblicazione nei tag di Experience Platform viene eseguita dalla scheda Pubblicazione nella configurazione di Proprietà.

I tag Experience Platform possono potenzialmente avere più ambienti di sviluppo, un ambiente di staging e un ambiente di produzione. Per impostazione predefinita, la configurazione cloud dei tag di Experience Platform in Experience Manager punta il nodo di authoring di Experience Manager all’ambiente di staging dei tag della piattaforma. Il nodo Publish di Experience Manager punta all’ambiente di produzione dei tag di Experience Platform. Ciò significa che con le impostazioni predefinite di Experience Manager, è necessario pubblicare la libreria Tag di Experience Platform nell’ambiente di staging. In questo modo puoi utilizzarlo in modalità di authoring in Experience Manager. Puoi quindi pubblicarlo nell’ambiente di produzione in modo che possa essere utilizzato in Experience Manager Publish.

Per ulteriori informazioni sugli ambienti di tag Experience Platform, consulta [Ambienti](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/environments/environments).

La pubblicazione di una libreria prevede i due passaggi seguenti:

* Aggiunta e creazione di una nuova libreria includendo tutte le modifiche necessarie (nuove e aggiornamenti) nella libreria.
* Spostarsi verso l’alto nella libreria attraverso i diversi livelli di ambiente (da Sviluppo a Staging e Produzione).

#### Aggiungere e creare una nuova libreria {#adding-and-building-a-new-library}

1. La prima volta che apri la scheda Pubblicazione in Tag di Experience Platform, l’elenco delle librerie è vuoto.

   Nella colonna sinistra, fare clic su **[!UICONTROL Aggiungi nuova libreria]**.

   ![immagine2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. Nella pagina Crea nuova libreria, immetti il nome descrittivo della nuova libreria nel campo **[!UICONTROL Nome]**. Ad esempio,

   *LibreriaVisualizzatoriDynamicMedia*

   Dall’elenco a discesa Ambiente, scegli il livello Ambiente. Inizialmente, solo il livello Sviluppo è disponibile per la selezione. Nella parte inferiore sinistra della pagina fare clic su **[!UICONTROL Aggiungi tutte le risorse modificate]**.

   ![immagine2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Fai clic su **[!UICONTROL Salva e genera per sviluppo]** nell&#39;angolo superiore destro della pagina.

   In pochi minuti, la libreria viene creata ed è pronta per l’uso.

   ![immagine2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >Alla prossima modifica della configurazione dei tag Experience Platform, vai alla scheda **[!UICONTROL Pubblicazione]** nella configurazione **[!UICONTROL Proprietà]**, quindi seleziona la libreria creata in precedenza.
   >
   >
   >Dalla schermata di pubblicazione della libreria, fai clic su **[!UICONTROL Aggiungi tutte le risorse modificate]**, quindi fai clic su **[!UICONTROL Salva e genera per sviluppo]**.

#### Spostarsi verso l’alto in una libreria attraverso i livelli di ambiente {#moving-a-library-up-through-environment-levels}

1. Dopo l’aggiunta di una nuova libreria, questa si trova nell’ambiente di sviluppo. Per spostarlo nel livello dell&#39;ambiente di staging (che corrisponde alla colonna Inviato), dal menu a discesa della libreria, fare clic su **[!UICONTROL Invia per approvazione]**.

   ![immagine2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. Nella finestra di dialogo di conferma, fai clic su **[!UICONTROL Invia]**.

   Dopo aver spostato la libreria nella colonna Inviata, dal menu a discesa della libreria, fare clic su **[!UICONTROL Genera per staging]**.

   ![immagine2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Per spostare la libreria dall’ambiente di staging all’ambiente di produzione (che è la colonna Pubblicato), segui un processo simile.

   Innanzitutto, dal menu a discesa, fai clic su **[!UICONTROL Approva per la pubblicazione]**.

   ![immagine2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. Dal menu a discesa, fai clic su **[!UICONTROL Genera e pubblica in produzione]**.

   ![immagine2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Consulta [Pubblicazione](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview) per ulteriori informazioni sul processo di pubblicazione nei tag di Experience Platform.

## Configurare Adobe Experience Manager per l’integrazione {#configuring-adobe-experience-manager-for-the-integration}

<!-- Prerequisites list below should be verified by Sasha -->

Prerequisiti:

* Experience Manager esegue sia le istanze in modalità di authoring che quelle in modalità di pubblicazione.
* Il nodo di authoring di Experience Manager è configurato in Dynamic Media. <!-- Scene7 run mode (dynamicmedia_s7) -->
* I componenti WCM Dynamic Media sono abilitati in Experience Manager Sites.

La configurazione di Experience Manager prevede i due passaggi principali seguenti:

* Configurazione di Experience Manager IMS.
* Configurazione di Experience Platform Tags Cloud.

### Configurare Experience Manager IMS {#configuring-aem-ims}

1. In Experience Manager Author, fai clic sull&#39;icona ![Martello, strumenti](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Strumenti**, quindi vai a **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. Nella pagina Configurazione Adobe IMC, nell&#39;angolo superiore sinistro, fare clic su **[!UICONTROL Crea]**.
1. Nella pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]**, nell&#39;elenco a discesa **[!UICONTROL Soluzione cloud]**, fare clic su **[!UICONTROL Raccolta dati Experience Platform]**.
1. Abilita **[!UICONTROL Crea nuovo certificato]**, quindi immetti un valore significativo per il certificato nel campo di testo. Ad esempio, *AdobeLaunchIMSCert*. Fai clic su **[!UICONTROL Crea certificato]**.

   Viene visualizzato il seguente messaggio informativo:

   *Per recuperare un token di accesso valido, è necessario aggiungere la nuova chiave pubblica del certificato all&#39;account tecnico in Adobe Developer!*

   Per chiudere la finestra di dialogo Info, fare clic su **[!UICONTROL OK]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Selezionare **[!UICONTROL Scarica chiave pubblica]** per scaricare un file di chiave pubblica (`*.crt`) nel sistema locale.

   >[!NOTE]
   >
   >A questo punto, ***lascia aperta*** la **[!UICONTROL pagina Configurazione account tecnico Adobe IMS]**; ***non*** chiude la pagina e ***non*** fai clic su **[!UICONTROL Avanti]**. Tornerai a questa pagina più avanti nei passaggi.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. In una nuova scheda del browser, passa a [Adobe Developer Console](https://developer.adobe.com/console/integrations).

1. Dalla pagina **[!UICONTROL Integrazioni Adobe Developer Console]**, nell&#39;angolo superiore destro, fare clic su **[!UICONTROL Nuova integrazione]**.
1. Nella finestra di dialogo **[!UICONTROL Create a new integration (Crea una nuova integrazione)]**, accertati che sia selezionato il pulsante di scelta **[!UICONTROL Access an API (Accesso a un API)]**, quindi fai clic su **[!UICONTROL Continua]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. Nella seconda pagina **[!UICONTROL Crea una nuova integrazione]**, abilita (attiva) il pulsante di scelta **[!UICONTROL API tag Experience Platform]**. Nell’angolo inferiore destro della pagina, fai clic su **[!UICONTROL Continua]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. Nella terza pagina **[!UICONTROL Crea una nuova integrazione]** eseguire le operazioni seguenti:

   * Nel campo **[!UICONTROL Nome]** immettere un nome descrittivo. Ad esempio, *DynamicMediaViewersIO*.

   * Nel campo **[!UICONTROL Descrizione]** immettere una descrizione per l&#39;integrazione.

   * Nell&#39;area **[!UICONTROL Certificati a chiave pubblica]**, carica il file a chiave pubblica (`*.crt`) scaricato in precedenza in questi passaggi.

   * Nell&#39;intestazione **[!UICONTROL Seleziona un ruolo per l&#39;API dei tag di Experience Platform]**, fare clic su **[!UICONTROL Amministratore]**.

   * Nell&#39;intestazione **[!UICONTROL Seleziona uno o più profili di prodotto per l&#39;API dei tag di Experience Platform]**, seleziona il profilo di prodotto denominato **[!UICONTROL Tag - &lt;nome_società>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Seleziona **[!UICONTROL Crea integrazione]**.
1. Nella pagina **[!UICONTROL Integrazione creata]**, fare clic su **[!UICONTROL Continua con i dettagli di integrazione]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. Viene visualizzata una pagina dei dettagli delle integrazioni simile alla seguente:

   >[!NOTE]
   >
   >***Lascia aperta la pagina dei dettagli di integrazione***. Tra poco ti occorreranno varie informazioni provenienti dalle schede **[!UICONTROL Panoramica]** e **[!UICONTROL JWT]**.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)
   *Pagina dettagli integrazione*

1. Torna alla pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]** che hai lasciato aperta in precedenza. Nell’angolo superiore destro della pagina, fai clic su **[!UICONTROL Avanti]** per aprire la pagina **[!UICONTROL Account]** alla finestra **[!UICONTROL Configurazione account tecnico Adobe IMS]**.

   (Se la pagina è stata chiusa in precedenza, torna ad Experience Manager Author, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**. Seleziona **[!UICONTROL Crea]**. Nell&#39;elenco a discesa **[!UICONTROL Soluzione cloud]**, fare clic su **[!UICONTROL Tag Experience Platform]**. Nell&#39;elenco a discesa **[!UICONTROL Certificato]** fare clic sul nome del certificato creato in precedenza.

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)
   *Configurazione account tecnico Adobe IMS - Pagina certificato*

1. La pagina **[!UICONTROL Account]** contiene cinque campi che è necessario compilare utilizzando le informazioni della pagina Dettagli integrazione del passaggio precedente.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)
   *Configurazione account tecnico Adobe IMS - Pagina account*

1. Nella pagina **[!UICONTROL Account]**, compila i campi seguenti:

   * **[!UICONTROL Titolo]** - Inserisci un titolo account descrittivo.
   * **[!UICONTROL Server autorizzazioni]** - Tornare alla pagina dei dettagli di integrazione aperta in precedenza. Seleziona la scheda **[!UICONTROL JWT]**. Copia il nome del server, senza il percorso, come evidenziato di seguito.

   Torna alla pagina **[!UICONTROL Account]**, quindi incolla il nome nel rispettivo campo.
Ad esempio, `https://ims-na1.adobelogin.com/`
(il nome del server di esempio è solo a scopo illustrativo)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)
   *Pagina dettagli integrazione - Scheda JWT*

1. **[!UICONTROL Chiave API]**: torna alla pagina dei dettagli di integrazione. Seleziona la scheda **[!UICONTROL Panoramica]**, quindi fai clic su **[!UICONTROL Copia]** a destra del campo **[!UICONTROL Chiave API (ID client)]**.

   Torna alla pagina **[!UICONTROL Account]**, quindi incolla la chiave nel rispettivo campo.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)
   *Pagina dettagli integrazione*

1. **[!UICONTROL Segreto client]**: torna alla pagina dei dettagli di integrazione. Nella scheda **[!UICONTROL Panoramica]**, fai clic su **[!UICONTROL Retrieve Client Secret (Recupera segreto client)]**. A destra del campo **[!UICONTROL Segreto client]**, fai clic su **[!UICONTROL Copia]**.

   Torna alla pagina **[!UICONTROL Account]**, quindi incolla la chiave nel rispettivo campo.

1. **[!UICONTROL Payload]** - Torna alla pagina dei dettagli di integrazione. Nella scheda **[!UICONTROL JWT]**, copia l&#39;intero codice oggetto JSON nel campo Payload JWT.

   Torna alla pagina **[!UICONTROL Account]**, quindi incolla il codice nel rispettivo campo.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)
   *Pagina dettagli integrazione - Scheda JWT*

   La pagina Account, con tutti i campi compilati, è simile alla seguente:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Fai clic su **[!UICONTROL Crea]** nell&#39;angolo superiore destro della pagina **[!UICONTROL Account]**.

   Con Experience Manager IMS configurato, ora hai un nuovo IMSAccount elencato in **[!UICONTROL Configurazioni Adobe IMS]**.

   ![immagine2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Configurare Experience Platform Tags Cloud per l’integrazione {#configuring-adobe-launch-cloud-for-the-integration}

1. In modalità Autore Experience Manager, nell&#39;angolo superiore sinistro, fai clic sull&#39;icona ![Martello, strumenti](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Strumenti**, quindi vai a **[!UICONTROL Servizi cloud]** > **[!UICONTROL Configurazioni tag Experience Platform]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. Nella pagina **[!UICONTROL Configurazioni tag Experience Platform]**, seleziona nel pannello a sinistra un sito Experience Manager per il quale desideri applicare la configurazione tag Experience Platform.

   Solo a scopo di esempio, il sito **`We.Retail`** è selezionato nella schermata seguente.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. Fai clic su **[!UICONTROL Crea]** nell’angolo superiore sinistro della pagina.
1. Nella pagina **[!UICONTROL Generale]** (1/3 pagine) della finestra **[!UICONTROL Crea configurazione tag di Experience Platform]**, compila i campi seguenti:

   * **[!UICONTROL Titolo]** - Inserisci un titolo di configurazione descrittivo. Esempio: `We.Retail Tags cloud configuration`.

   * **[!UICONTROL Configurazione Adobe IMS associata]** - Seleziona la configurazione IMS creata in precedenza in [Configura Experience Manager IMS](#configuring-aem-ims).

   * **[!UICONTROL Società]** - Dall&#39;elenco a discesa **[!UICONTROL Società]**, seleziona la tua società Experience Cloud. L’elenco viene compilato automaticamente.

   * **[!UICONTROL Proprietà]** - Dall&#39;elenco a discesa Proprietà, seleziona la proprietà Experience Platform Tags creata in precedenza. L’elenco viene compilato automaticamente.

   Dopo aver completato tutti i campi, la pagina **[!UICONTROL Generale]** sarà simile alla seguente:

   ![immagine2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Fai clic su **[!UICONTROL Avanti]** nell&#39;angolo superiore sinistro.
1. Nella pagina **[!UICONTROL Gestione temporanea]** (2/3 pagine) della finestra **[!UICONTROL Crea configurazione tag di Experience Platform]**, compila il seguente campo:

   Nel campo **[!UICONTROL URI libreria]** (Uniform Resource Identifier), controlla il percorso della versione di staging della libreria Experience Platform Tags. Experience Manager compila automaticamente questo campo.

   Solo a scopo illustrativo, questo passaggio utilizza le librerie di tag Experience Platform distribuite in Adobe CDN.

   >[!NOTE]
   >
   >Verifica che l’URI della libreria con compilazione automatica (Uniform Resource Identifier) sia formato correttamente. Se necessario, correggerlo in modo che l’URI rappresenti un URI relativo al protocollo. In altre parole, inizia da una doppia barra in avanti.
   >
   >
   >Ad esempio: `//assets.adobetm.com/launch-xxxx`.

   È probabile che la pagina **[!UICONTROL Gestione temporanea]** sia simile alla seguente. Le opzioni **[!UICONTROL Archivia]** e **[!UICONTROL Carica libreria in modo asincrono]** sono ***non*** impostate:

   ![immagine2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Fai clic su **[!UICONTROL Avanti]** nell&#39;angolo superiore destro.
1. Se necessario, nella pagina **[!UICONTROL Produzione]** (3/3 pagine) della finestra **[!UICONTROL Crea configurazione tag di Experience Platform]**, correggi l&#39;URI di produzione con compilazione automatica con una procedura simile a quella della pagina **[!UICONTROL Staging]** precedente.
1. Fai clic su **[!UICONTROL Crea]** nell&#39;angolo superiore destro.

   La nuova configurazione cloud di tag di Experience Platform viene ora creata ed elencata accanto al sito web.

1. Seleziona la nuova configurazione cloud di tag Experience Platform (quando è selezionata, a sinistra del titolo della configurazione compare un segno di spunta). Sulla barra degli strumenti fare clic su **[!UICONTROL Pubblica]**.

   ![immagine2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

Attualmente, Experience Manager Author non supporta l’integrazione dei visualizzatori Dynamic Media con i tag di Experience Platform.

È, tuttavia, supportato nel nodo di pubblicazione di Experience Manager. Utilizzando le impostazioni predefinite di Configurazione cloud dei tag di Experience Platform, Experience Manager Publish utilizza l’ambiente di produzione dei tag di Experience Platform. Di conseguenza, ogni volta durante il test è necessario inviare gli aggiornamenti della libreria di tag di Experience Platform dallo Sviluppo all’ambiente di produzione.

È possibile aggirare questo limite. Specifica l’URL di sviluppo o staging della libreria di tag di Experience Platform nella configurazione cloud di tag di Experience Platform per la pubblicazione di Experience Manager di cui sopra. In questo modo, il nodo di pubblicazione di Experience Manager utilizza la versione di sviluppo o staging della libreria di tag di Experience Platform.

Per ulteriori informazioni sulla configurazione cloud dei tag di Experience Platform, vedere [Integrate Experience Platform Tags and Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview#integrations).
