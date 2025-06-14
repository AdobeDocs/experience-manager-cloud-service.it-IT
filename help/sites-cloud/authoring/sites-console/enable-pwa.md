---
title: Abilitazione delle funzioni progressive delle web app
description: AEM Sites consente all’autore dei contenuti di abilitare le funzionalità progressive delle app web a qualsiasi sito tramite una configurazione semplice invece che tramite la codifica.
exl-id: 1552a4ce-137a-4208-b7f6-2fc06db8dc39
solution: Experience Manager Sites
feature: Authoring
role: User
index: false
source-git-commit: 19a16bbfc23806f8bc655c0d19713df500e3b12b
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 61%

---

# Abilitazione delle funzioni progressive delle web app {#enabling-pwa}

Grazie a una configurazione semplice, un autore di contenuti può ora abilitare le funzioni dell’app web progressiva (progressive web app, PWA) per le esperienze create in AEM Sites.

>[!CAUTION]
>
>Questa è una funzione avanzata che richiede:
>
>* Conoscenza delle PWA
>* Conoscenza del sito e della struttura dei contenuti
>* Informazioni sulle strategie di caching
>* Supporto dal team di sviluppo
>
>Prima di utilizzare questa funzione, Adobe consiglia di discuterne con il team di sviluppo per definire il modo migliore per utilizzarla per il progetto.

{{pwa-deprecation}}

## Introduzione {#introduction}

Le [app web progressive (PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) abilitano esperienze simili alle applicazioni immersive per siti di AEM Sites, che possono essere memorizzate localmente sul computer di un utente ed essere accessibili offline. Un utente può navigare su un sito mentre è in movimento anche se perde una connessione a Internet. Le PWA consentono un’esperienza fluida anche in caso di perdita o instabilità della rete.

Anziché richiedere una nuova codifica del sito, un autore di contenuti può configurare le proprietà di PWA come scheda aggiuntiva nelle [proprietà pagina](/help/sites-cloud/authoring/sites-console/page-properties.md) di un sito.

* Quando viene salvata o pubblicata, questa configurazione attiva un gestore eventi che scrive i [file manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest) e un [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) che abilita le funzionalità di PWA nel sito.
* Vengono inoltre mantenute le mappature Sling per garantire che service worker sia servito dalla radice dell’applicazione per abilitare il proxy del contenuto che consente funzionalità offline all’interno dell’app.

Con PWA, l’utente dispone di una copia locale del sito, che offre un’esperienza simile alle app anche senza una connessione Internet.

>[!NOTE]
>
>Le app web progressive sono una tecnologia in evoluzione e supportano l&#39;installazione di app locali e altre funzionalità [a seconda del browser utilizzato](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Tutorials/js13kGames/Installable_PWAs#summary).

## Prerequisiti {#prerequisites}

Per poter utilizzare le funzioni di PWA per il sito, sono necessari due requisiti per l’ambiente di progetto:

1. [Usare componenti core](#adjust-components) per sfruttare questa funzione
1. [Regola le regole di Dispatcher](#adjust-dispatcher) per esporre i file richiesti

Si tratta di passaggi tecnici che l’autore deve coordinare con il team di sviluppo. Questi passaggi sono necessari solo una volta per sito.

### Utilizzare componenti core {#adjust-components}

La versione 2.15.0 o successiva dei componenti core supporta completamente le funzioni PWA di AEM Sites. Poiché AEMaaCS include sempre la versione più recente dei componenti core, puoi usare le funzionalità di PWA predefinite. Il progetto AEMaaCS soddisfa automaticamente questo requisito.

>[!NOTE]
>
>Adobe sconsiglia di utilizzare le funzionalità di PWA su componenti personalizzati o non su [componenti personalizzati estesi dai Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=it).
<!--
Your components need to include the [manifest files](https://developer.mozilla.org/en-US/docs/Web/Manifest) and [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API), which supports the PWA features.

 To do this, the developer adds the following link to the `customheaderlibs.html` file of your page component.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

The developer also adds the following link to the `customfooterlibs.html` file of your page component.

```xml
<script>
        // Check that service workers are supported
        if ('serviceWorker' in navigator) {
            // Use the window load event to make sure the page load performs well
            window.addEventListener('load', () => {
                let serviceWorker = '/<projectName>sw.js';
                navigator.serviceWorker.register(serviceWorker);
            });
        }
</script>
```
-->

### Regolare il Dispatcher {#adjust-dispatcher}

La funzione PWA genera e utilizza file `/content/<sitename>/manifest.webmanifest`. Per impostazione predefinita, [Dispatcher](/help/implementing/dispatcher/overview.md) non espone tali file. Per esporre questi file, lo sviluppatore deve aggiungere la seguente configurazione al progetto del sito.

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

A seconda del progetto, potrebbe essere utile includere diversi tipi di estensioni alle regole di riscrittura. L’estensione `webmanifest` può essere utile da includere nelle condizioni di riscrittura quando hai introdotto una regola che nasconde e reindirizza le richieste a `/content/<projectName>`.

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## Abilitazione di PWA per il sito {#enabling-pwa-for-your-site}

Rispettando [i prerequisiti](#prerequisites), per un autore di contenuti è semplice abilitare le funzionalità di PWA a un sito. Di seguito è riportato uno schema di base su come eseguire questa operazione. Le singole opzioni sono descritte in dettaglio nella sezione [Opzioni dettagliate](#detailed-options).

1. Accedi ad AEM.
1. Dal menu principale, seleziona **Navigazione** > **Siti**.
1. Selezionare il progetto Sites e selezionare [**Proprietà**](/help/sites-cloud/authoring/sites-console/page-properties.md) oppure utilizzare il tasto di scelta rapida `p`.
1. Seleziona la scheda **App web progressiva** e configura le proprietà applicabili. Come minimo, desideri:
   1. Selezionare l’opzione **Abilita PWA**.
   1. Definire l’**URL di avvio**.

      ![Abilita PWA](../assets/pwa-enable.png)

   1. Caricare un’icona png 512x512 nel DAM e fare riferimento a essa come icona per l’app.

      ![Definisci icona PWA](../assets/pwa-icon.png)

   1. Configurare i percorsi che si desidera vengano disconnessi dal service worker. I percorsi tipici sono:
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * Qualsiasi riferimento a font di terze parti
      * `/etc/clientlibs/<sitename>`

      ![Definire i percorsi offline di PWA](../assets/pwa-offline.png)

1. Seleziona **Salva e chiudi**.

Il tuo sito è ora configurato e puoi [installarlo come app locale](#using-pwa-enabled-site).

## Utilizzo del sito abilitato per PWA {#using-pwa-enabled-site}

Ora che hai [configurato il tuo sito per supportare PWA](#enabling-pwa-for-your-site), puoi provarlo per conto tuo.

1. Accedi al sito in un [browser supportato](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Tutorials/js13kGames/Installable_PWAs#summary).
1. Nella barra degli indirizzi del browser viene visualizzata una nuova icona che indica che il sito può essere installato come app locale.
   * A seconda del browser, l’icona può variare e il browser può anche visualizzare una notifica (ad esempio un banner o una finestra di dialogo) che indica che è possibile installare come app locale.
1. Installa l’app.
1. L’app viene installata nella schermata iniziale del dispositivo.
1. Apri l’app, sfoglia un po’ e osserva che le pagine sono disponibili offline.

## Opzioni dettagliate {#detailed-options}

La sezione seguente fornisce ulteriori dettagli sulle opzioni disponibili durante la [configurazione del sito per PWA](#enabling-pwa-for-your-site).

### Configurare esperienza installabile {#configure-installable-experience}

Queste impostazioni consentono al sito di comportarsi come un’app nativa rendendolo installabile nella schermata iniziale del visitatore e disponibile offline.

* **Abilita PWA** - Questa è l&#39;opzione principale per abilitare PWA per il sito.
* **URL di avvio** - Questo è l&#39;[URL iniziale preferito](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) che l&#39;app apre quando l&#39;utente carica l&#39;app installata localmente.
   * Può essere un qualsiasi percorso nella struttura del contenuto.
   * Non deve essere la radice ed è spesso una pagina di benvenuto dedicata per l’app.
   * Se questo URL è relativo, l’URL manifesto viene utilizzato come URL di base per risolverlo.
   * Se lasciata vuota, la funzione utilizza l’indirizzo della pagina web da cui è stata installata l’app.
   * È consigliabile impostare un valore.
* **Modalità di visualizzazione** - Un’app abilitata per PWA è ancora un sito AEM distribuito tramite un browser. [Queste opzioni di visualizzazione](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) definiscono come il browser deve essere nascosto o altrimenti presentato all’utente sul dispositivo locale.
   * **Standalone** - Il browser è nascosto all&#39;utente e viene visualizzato come un&#39;app nativa. Questo è il valore predefinito.
      * Con questa opzione, la navigazione nelle app deve essere possibile interamente tramite il contenuto mediante collegamenti e componenti nelle pagine del sito senza utilizzare i controlli di navigazione del browser.
   * **Browser** - Il browser viene visualizzato come di consueto quando si visita il sito.
   * **Interfaccia utente minima** - Il browser è principalmente nascosto, come un’app nativa, ma sono esposti i controlli di navigazione di base.
   * **Schermo intero** - Il browser è nascosto, come un&#39;app nativa, ma viene riprodotto in modalità a schermo intero.
      * Con questa opzione, la navigazione nelle app deve essere possibile interamente tramite il contenuto mediante collegamenti e componenti nelle pagine del sito senza utilizzare i controlli di navigazione del browser.
* **Orientamento schermo** - Come app locale, PWA deve sapere come gestire [gli orientamenti del dispositivo](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation).
   * **Qualsiasi** - L’app si adatta all’orientamento del dispositivo dell’utente. Questo è il valore predefinito.
   * **Verticale** - Questo costringe l’app ad aprirsi in layout verticale indipendentemente dall’orientamento del dispositivo dell’utente.
   * **Orizzontale** - Questo costringe l’app ad aprirsi in layout orizzontale indipendentemente dall’orientamento del dispositivo dell’utente.
* **Colore tema** - Definisce il [colore dell’app](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) che influisce sul modo in cui il sistema operativo dell’utente locale visualizza la barra degli strumenti dell’interfaccia utente nativa e i controlli di navigazione. A seconda del browser, può influenzare altri elementi di presentazione dell’app.
   * Utilizzare la finestra a comparsa del pozzetto di colore per selezionare un colore.
   * Il colore può essere definito anche in base al valore esadecimale o RGB.
* **Colore di sfondo** - Definisce il [colore di sfondo dell’app](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color), che viene visualizzato durante il caricamento dell’app.
   * Utilizzare la finestra a comparsa del pozzetto di colore per selezionare un colore.
   * Il colore può essere definito anche in base al valore esadecimale o RGB.
   * Alcuni browser [creano automaticamente una schermata iniziale](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) dal nome dell’app, dal colore di sfondo e dall’icona.
* **Icona** - Definisce [l’icona](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) che rappresenta l’app sul dispositivo dell’utente.
   * L’icona deve essere un file png di dimensioni pari a 512x512 pixel.
   * L’icona deve essere [memorizzata in DAM](/help/assets/overview.md).

### Gestione della cache (avanzate) {#offline-configuration}

Queste impostazioni rendono alcune parti del sito disponibili offline e localmente sul dispositivo del visitatore. Ciò consente di controllare la cache dell’app web per ottimizzare le richieste di rete e supportare le esperienze offline.

* **Strategia di memorizzazione in cache e frequenza di aggiornamento dei contenuti** - Questa impostazione definisce il modello di memorizzazione in cache per PWA.
   * **Moderatamente** - [Questa impostazione](https://web.dev/stale-while-revalidate/) è il caso della maggior parte dei siti ed è il valore predefinito.
      * Con questa impostazione, il contenuto visualizzato per la prima volta dall’utente viene caricato dalla cache e mentre l’utente sta utilizzando quel contenuto, il resto del contenuto nella cache viene riconvalidato.
   * **Frequentemente** - Questo è il caso dei siti che necessitano di aggiornamenti per essere veloci come le case d&#39;asta.
      * Con questa impostazione, l’app cerca prima il contenuto più recente tramite la rete e, se non è disponibile, torna alla cache locale.
   * **Raramente** - Questo è il caso dei siti quasi statici, come le pagine di riferimento.
      * Con questa impostazione, l’app cerca prima il contenuto nella cache e, se non disponibile, torna alla rete per recuperarlo.
* **Pre-memorizzazione in cache dei file** - Questi file in hosting su AEM vengono salvati nella cache del browser locale quando il service worker si sta installando e prima di essere utilizzato. Questo garantisce che l’app web sia completamente funzionante quando è offline.
* **Inclusioni dei percorsi** - Le richieste di rete per i percorsi definiti vengono intercettate e il contenuto nella cache viene restituito in conformità alla configurazione della **Strategia di memorizzazione in cache e frequenza di aggiornamento dei contenuti**.
* **Esclusioni di cache** - Questi file non vengono mai memorizzati nella cache indipendentemente dalle impostazioni in **Pre-memorizzazione in cache dei file** e **Inclusioni dei percorsi**.

>[!TIP]
>
>È probabile che il team di sviluppatori disponga di informazioni utili sulla configurazione offline.

## Limitazioni e consigli {#limitations-recommendations}

Non tutte le funzionalità di PWA sono disponibili per AEM Sites. Questi sono alcuni limiti importanti.

* Le pagine non vengono sincronizzate o aggiornate automaticamente se l’utente non sta utilizzando l’app.

Quando si implementa PWA, Adobe consiglia anche quanto segue.

### Riduci al minimo il numero di risorse da pre-memorizzare in cache. {#minimize-precache}

Adobe consiglia di limitare il numero di pagine da pre-memorizzare in cache.

* Incorpora le librerie in modo da ridurre il numero di voci da gestire durante la pre-memorizzazione in cache.
* Limita il numero di varianti di immagine da pre-memorizzare in cache.

### Abilita PWA dopo la stabilizzazione degli script di progetto e dei fogli di stile. {#pwa-stabilized}

Le librerie client vengono distribuite con l’aggiunta di un selettore di cache che osserva il seguente pattern `lc-<checksumHash>-lc`. Questo selettore cambia ogni volta che cambia uno dei file (e delle dipendenze) che compongono una libreria. Se hai elencato una libreria client che deve essere pre-memorizzata nella cache dal service-worker e desideri fare riferimento a una nuova versione, recupera e aggiorna manualmente la voce. Di conseguenza, Adobe consiglia di configurare il sito come PWA dopo la stabilizzazione degli script del progetto e dei fogli di stile.

### Riduci al minimo il numero di varianti di immagine. {#minimize-variations}

Il componente Immagine dei componenti core AEM determina il front-end della migliore resa da recuperare. Questo meccanismo include anche una marca temporale corrispondente all’ora dell’ultima modifica apportata alla risorsa. Questo meccanismo complica la configurazione della pre-memorizzazione della cache di PWA.

Durante la configurazione della pre-cache, l’utente deve elencare tutte le varianti di percorso che possono essere recuperate. Queste varianti sono composte da parametri come la qualità e la larghezza. Si consiglia di ridurre il numero di queste varianti a un massimo di tre: piccolo, medio, grande. Puoi eseguire questa operazione tramite la finestra di dialogo dei criteri per i contenuti del [componente Immagine](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=it).

Se non viene configurato con attenzione, il consumo di memoria e rete può influire notevolmente sulle prestazioni di PWA. Inoltre, se intendi prememorizzare in cache, ad esempio, 50 immagini e avere tre larghezze per immagine, l’utente che gestisce il sito deve mantenere un elenco di fino a 150 voci nella sezione di pre-memorizzazione della cache di PWA delle proprietà di pagina.

Adobe consiglia inoltre di configurare il sito come PWA dopo la stabilizzazione dell’utilizzo delle immagini nel progetto.
