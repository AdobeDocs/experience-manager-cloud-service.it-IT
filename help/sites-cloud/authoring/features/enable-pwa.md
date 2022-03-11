---
title: Abilitazione delle funzioni progressive delle web app
description: AEM Sites consente all’autore dei contenuti di abilitare le funzionalità progressive delle app web a qualsiasi sito tramite una configurazione semplice invece che tramite la codifica.
exl-id: 1552a4ce-137a-4208-b7f6-2fc06db8dc39
source-git-commit: 3910b47c5d25679d03409380d91afaa6ff5ab265
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 1%

---

# Abilitazione delle funzioni progressive delle web app {#enabling-pwa}

Grazie a una configurazione semplice, un autore di contenuti può ora abilitare le funzioni dell’app web progressiva (PWA) per le esperienze create in AEM Sites.

>[!CAUTION]
>
>Questa è una funzione avanzata che richiede:
>
>* Conoscenza dei PWA
>* Conoscenza del sito e della struttura dei contenuti
>* Informazioni sulle strategie di caching
>* Supporto dal team di sviluppo
>
>Prima di utilizzare questa funzione è consigliabile parlarne con il team di sviluppo per definire il modo migliore per sfruttarla al meglio per il progetto.

## Introduzione {#introduction}

[App web progressive (PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) abilita esperienze app-like immersive per AEM siti, consentendo loro di memorizzarle localmente sul computer di un utente e di essere accessibili offline. Un utente può navigare su un sito mentre è in movimento anche se perde una connessione a Internet. I PWA consentono esperienze senza soluzione di continuità anche in caso di perdita o instabilità della rete.

Invece di richiedere una nuova codifica del sito, un autore di contenuti può configurare le proprietà di PWA come scheda aggiuntiva nella sezione [proprietà pagina](/help/sites-cloud/authoring/fundamentals/page-properties.md) di un sito.

* Quando viene salvata o pubblicata, questa configurazione attiva un gestore eventi che scrive il [file manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest) e [addetto ai servizi](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) che abilitano le funzionalità di PWA sul sito.
* Vengono inoltre mantenute le mappature Sling per garantire che service worker sia servito dalla radice dell’applicazione per abilitare il proxy del contenuto che consente funzionalità offline all’interno dell’app.

Con PWA, l’utente dispone di una copia locale del sito, che offre un’esperienza simile alle app anche senza una connessione Internet.

>[!NOTE]
>
>Le app web progressive sono una tecnologia in evoluzione e supportano l&#39;installazione di app locali e altre funzioni [dipende dal browser utilizzato.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## Prerequisiti {#prerequisites}

Per poter utilizzare le funzioni di PWA per il sito, sono necessari due requisiti per l’ambiente di progetto:

1. [Usa componenti core](#adjust-components) per sfruttare questa funzione
1. [Regolare il dispatcher](#adjust-dispatcher) regole per esporre i file richiesti

Questi sono i passaggi tecnici che l’autore dovrà coordinare con il team di sviluppo. Questi passaggi sono necessari solo una volta per sito.

### Utilizza componenti core {#adjust-components}

La versione 2.15.0 e successive dei componenti core supporta completamente le funzioni PWA dei siti AEM. Poiché AEMaaCS include sempre la versione più recente dei componenti core, puoi sfruttare le funzionalità di PWA predefinite. Il progetto AEMaaCS soddisfa automaticamente questo requisito.

>[!NOTE]
>
>Adobe sconsiglia di utilizzare le funzioni di PWA su componenti personalizzati o non su componenti personalizzati [estesi dai componenti core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
<!--
Your components need to include the [manifest files](https://developer.mozilla.org/en-US/docs/Web/Manifest) and [service worker,](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) which supports the PWA features.

 To do this, the developer will need to add the following link to the `customheaderlibs.html` file of your page component.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

The developer will also need to add the following link to the `customfooterlibs.html` file of your page component.

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

La funzione PWA genera e utilizza `/content/<sitename>/manifest.webmanifest` file. Per impostazione predefinita, [dispatcher](/help/implementing/dispatcher/overview.md) non espone tali file. Per esporre questi file, lo sviluppatore deve aggiungere la seguente configurazione al progetto del sito.

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

A seconda del progetto, potrebbe essere utile includere diversi tipi di estensioni alle regole di riscrittura. La `webmanifest` L&#39;estensione può essere utile da includere nelle condizioni di riscrittura quando hai introdotto una regola che nasconde e reindirizzerà le richieste a `/content/<projectName>`.

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## Abilitazione di PWA per il sito {#enabling-pwa-for-your-site}

Con [i prerequisiti](#prerequisites) tuttavia, per un autore di contenuti è molto semplice abilitare le funzioni di PWA a un sito. Di seguito è riportato un profilo di base su come eseguire questa operazione. Le singole opzioni sono descritte in dettaglio nella sezione . [Opzioni dettagliate.](#detailed-options)

1. Accedi a AEM.
1. Dal menu principale, tocca o fai clic su **Navigazione** -> **Sites**.
1. Seleziona il progetto Sites e tocca o fai clic su [**Proprietà**](/help/sites-cloud/authoring/fundamentals/page-properties.md) o utilizza il tasto di scelta rapida `p`.
1. Seleziona la **App web progressiva** e configura le proprietà applicabili. Come minimo è necessario:
   1. Seleziona l’opzione **Abilita PWA**.
   1. Definisci la **URL di avvio**.

      ![Abilita PWA](../assets/pwa-enable.png)

   1. Carica un&#39;icona png 512x512 nel DAM e fai riferimento a essa come icona per l&#39;app.

      ![Icona Definisci PWA](../assets/pwa-icon.png)

   1. Configura i percorsi che desideri che il service worker metta offline. I percorsi tipici sono:
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * Qualsiasi riferimento a font di terze parti
      * `/etc/clientlibs/<sitename>`

      ![Definire i percorsi offline di PWA](../assets/pwa-offline.png)


1. Tocca o fai clic su **Salva e chiudi**.

Il tuo sito è ora configurato e puoi [installalo come app locale.](#using-pwa-enabled-site)

## Utilizzo del sito abilitato per PWA {#using-pwa-enabled-site}

Ora che hai [configurato il sito per supportare PWA,](#enabling-pwa-for-your-site) puoi sperimentarlo da solo.

1. Accedere al sito in un [browser supportato.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. Nella barra degli indirizzi del browser viene visualizzata una nuova icona che indica che il sito può essere installato come app locale.
   * A seconda del browser, l’icona può variare e il browser può anche visualizzare una notifica (ad esempio un banner o una finestra di dialogo) che indica che è possibile installare come app locale.
1. Installa l&#39;app.
1. L’app verrà installata nella schermata iniziale del dispositivo.
1. Apri l’app, sfoglia un po’ e osserva che le pagine sono disponibili offline.

## Opzioni dettagliate {#detailed-options}

La sezione seguente fornisce ulteriori dettagli sulle opzioni disponibili quando [configurazione del sito per PWA.](#enabling-pwa-for-your-site)

### Configurare l’esperienza installabile {#configure-installable-experience}

Queste impostazioni consentono al tuo sito di comportarsi come un&#39;app nativa, rendendola installabile nella schermata iniziale del visitatore e disponibile offline.

* **Abilita PWA** - Questa è l’opzione principale per abilitare PWA per il sito.
* **URL di avvio** - Questa è la [URL iniziale preferito](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) che l’app si aprirà quando l’utente carica l’app installata localmente.
   * Può essere un qualsiasi percorso nella struttura del contenuto.
   * Questa non deve essere la radice ed è spesso una pagina di benvenuto dedicata per l’app.
   * Se questo URL è relativo, l&#39;URL manifesto viene utilizzato come URL di base per risolverlo.
   * Se lasciata vuota, la funzione utilizza l’indirizzo della pagina web da cui è stata installata l’app.
   * È consigliabile impostare un valore.
* **Modalità di visualizzazione** - Un’app abilitata per PWA è ancora un sito AEM distribuito tramite un browser. [Queste opzioni di visualizzazione](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) definisci come il browser deve essere nascosto o altrimenti presentato all’utente sul dispositivo locale.
   * **Standalone** - Il browser è completamente nascosto all’utente e viene visualizzato come un’app nativa. Questo è il valore predefinito.
      * Con questa opzione, la navigazione nelle app deve essere possibile interamente tramite il contenuto mediante collegamenti e componenti nelle pagine del sito senza utilizzare i controlli di navigazione del browser.
   * **Browser** - Il browser viene visualizzato come di consueto quando si visita il sito.
   * **Interfaccia utente minima** - Il browser è principalmente nascosto, come un’app nativa, ma sono esposti i controlli di navigazione di base.
   * **Schermo intero** - Il browser è completamente nascosto, come un’app nativa, ma viene riprodotto in modalità a schermo intero.
      * Con questa opzione, la navigazione nelle app deve essere possibile interamente tramite il contenuto mediante collegamenti e componenti nelle pagine del sito senza utilizzare i controlli di navigazione del browser.
* **Orientamento dello schermo** - Come app locale, PWA deve sapere come gestire [orientamenti del dispositivo.](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **Qualsiasi** - L’app si adatta all’orientamento del dispositivo dell’utente. Questo è il valore predefinito.
   * **Verticale** - Questo costringe l’app ad aprirsi in layout verticale indipendentemente dall’orientamento del dispositivo dell’utente.
   * **Orizzontale** - Questo costringe l’app ad aprirsi in layout orizzontale indipendentemente dall’orientamento del dispositivo dell’utente.
* **Colore tema** - Definisce il [colore dell’app](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) che influisce sul modo in cui il sistema operativo dell’utente locale visualizza la barra degli strumenti dell’interfaccia utente nativa e i controlli di navigazione. A seconda del browser, può influenzare altri elementi di presentazione dell’app.
   * Utilizzare la finestra a comparsa del pozzetto del colore per selezionare un colore.
   * Il colore può essere definito anche in base al valore esadecimale o RGB.
* **Colore di sfondo** - Definisce il [colore di sfondo dell’app,](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) che viene visualizzato durante il caricamento dell’app.
   * Utilizzare la finestra a comparsa del pozzetto del colore per selezionare un colore.
   * Il colore può essere definito anche in base al valore esadecimale o RGB.
   * Alcuni browser [creazione automatica di una schermata iniziale](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) dal nome dell’app, dal colore di sfondo e dall’icona.
* **Icona** - Definisce [l’icona](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) che rappresenta l’app sul dispositivo dell’utente.
   * L&#39;icona deve essere un file png di dimensioni 512x512 pixel.
   * L’icona deve essere [memorizzato in DAM.](/help/assets/overview.md)

### Gestione cache (avanzata) {#offline-configuration}

Queste impostazioni rendono alcune parti del sito disponibili offline e disponibili localmente sul dispositivo del visitatore. Questo consente di controllare la cache dell’app web per ottimizzare le richieste di rete e supportare le esperienze offline.

* **Strategia di memorizzazione in cache e frequenza di aggiornamento dei contenuti** - Questa impostazione definisce il modello di memorizzazione in cache per PWA.
   * **Moderatamente** - [Questa impostazione](https://web.dev/stale-while-revalidate/) è il caso della maggior parte dei siti ed è il valore predefinito.
      * Con questa impostazione, il contenuto visualizzato per la prima volta dall’utente viene caricato dalla cache e mentre l’utente sta consumando quel contenuto, il resto del contenuto nella cache verrà riconvalidato.
   * **Frequentemente** - Questo è il caso dei siti che necessitano di aggiornamenti per essere molto veloci come le case d&#39;asta.
      * Con questa impostazione, l’app cercherà prima il contenuto più recente tramite la rete e, se non è disponibile, tornerà alla cache locale.
   * **Raramente** - Questo è il caso dei siti quasi statici, come le pagine di riferimento.
      * Con questa impostazione, l’app cercherà prima il contenuto nella cache e, se non disponibile, tornerà sulla rete per recuperarlo.
* **Pre-memorizzazione in cache dei file** - Questi file in hosting su AEM verranno salvati nella cache del browser locale quando il service worker sta installando e prima di utilizzarli. Questo garantisce che l’app web sia completamente funzionante quando è offline.
* **inclusioni dei percorsi** - Le richieste di rete per i percorsi definiti vengono intercettate e il contenuto nella cache viene restituito in conformità alla configurazione **Strategia di memorizzazione in cache e frequenza di aggiornamento dei contenuti**.
* **Esclusioni di cache** - Questi file non verranno mai memorizzati nella cache indipendentemente dalle impostazioni in **Pre-memorizzazione in cache dei file** e **inclusioni di percorso**.

>[!TIP]
>
>È probabile che il team di sviluppatori disponga di informazioni utili sulla configurazione offline.

## Limitazioni e Recommendations {#limitations-recommendations}

Non tutte le funzionalità di PWA sono disponibili per AEM Sites. Questi sono alcuni limiti importanti.

* Le pagine non vengono sincronizzate o aggiornate automaticamente se l’utente non utilizza l’app.

Adobe formula anche le seguenti raccomandazioni quando implementi PWA.

### Riduci al minimo il numero di risorse da pre-memorizzare in cache. {#minimize-precache}

Adobe consiglia di limitare il numero di pagine da prenotare in cache.

* Incorpora le librerie per ridurre il numero di voci da gestire durante la pre-memorizzazione in cache.
* Limita il numero di varianti di immagine a pre-cache.

### Abilita PWA dopo che gli script e i fogli di stile del progetto sono stati stabilizzati. {#pwa-stabilized}

Le librerie client vengono distribuite con l’aggiunta di un selettore di cache che osserva il seguente pattern `lc-<checksumHash>-lc`. Ogni volta che uno dei file (e delle dipendenze) che compongono una modifica della libreria, questo selettore cambia. Se hai elencato una libreria-client che deve essere pre-memorizzata nella cache da service-worker e desideri fare riferimento a una nuova versione, recupera e aggiorna manualmente la voce. Di conseguenza, consigliamo di configurare il sito come PWA dopo la stabilizzazione degli script di progetto e dei fogli di stile.

### Riduci al minimo il numero di varianti di immagine. {#minimize-variations}

Il componente Immagine dei componenti core AEM determina uno dei front-end il rendering migliore da recuperare. Questo meccanismo include anche una marca temporale corrispondente all’ora dell’ultima modifica apportata alla risorsa. Questo meccanismo complica la configurazione del pre-cache di PWA.

Durante la configurazione della pre-cache, l’utente deve elencare tutte le varianti di percorso che possono essere recuperate. Queste varianti sono composte da parametri come la qualità e la larghezza. Si consiglia vivamente di ridurre il numero di queste variazioni ad un massimo di tre - piccolo, medio, grande. Puoi farlo tramite la finestra di dialogo dei criteri per i contenuti della [Componente immagine.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html)

Se non viene configurata con attenzione, il consumo di memoria e rete può influire notevolmente sulle prestazioni di PWA. Inoltre, se si intende prememorizzare in cache, ad esempio, 50 immagini e avere 3 larghezze per immagine, l’utente che gestisce il sito dovrà mantenere un elenco di fino a 150 voci nella sezione pre-cache di PWA delle proprietà della pagina.

Adobe consiglia inoltre di configurare il sito come PWA dopo la stabilizzazione dell’utilizzo delle immagini nel progetto.
