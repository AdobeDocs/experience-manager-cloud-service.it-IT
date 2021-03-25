---
title: Abilitazione delle funzioni progressive delle app web
description: AEM Sites consente all’autore dei contenuti di abilitare le funzionalità progressive delle app web a qualsiasi sito tramite una configurazione semplice invece che tramite la codifica.
translation-type: tm+mt
source-git-commit: f130fe34e5c57b9fc78697374a5a9772da3c4c17
workflow-type: tm+mt
source-wordcount: '2032'
ht-degree: 0%

---


# Abilitazione delle funzioni progressive delle app Web {#enabling-pwa}

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
>
Prima di utilizzare questa funzione è consigliabile parlarne con il team di sviluppo per definire il modo migliore per sfruttarla al meglio per il progetto.

>[!NOTE]
>
>Le funzioni descritte in questo documento sono pianificate per essere rese disponibili con la versione di [marzo 2021 di AEM come Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## Introduzione {#introduction}

[Le app web progressive (PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) consentono esperienze coinvolgenti di tipo app per AEM siti, memorizzandole localmente sul computer di un utente e rendendole accessibili offline. Un utente può navigare su un sito mentre è in movimento anche se perde una connessione a Internet. I PWA consentono esperienze senza soluzione di continuità anche in caso di perdita o instabilità della rete.

Invece di richiedere qualsiasi codifica del sito, un autore di contenuti può configurare le proprietà di PWA come scheda aggiuntiva nelle proprietà di pagina [a1/> di un sito.](/help/sites-cloud/authoring/fundamentals/page-properties.md)

* Quando viene salvata o pubblicata, questa configurazione attiva un gestore eventi che scrive i [file manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest) e [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) che abilitano le funzioni di PWA sul sito.
* Vengono inoltre mantenute le mappature Sling per garantire che service worker sia servito dalla radice dell’applicazione per abilitare il proxy del contenuto che consente funzionalità offline all’interno dell’app.

Con PWA, l’utente dispone di una copia locale del sito, che offre un’esperienza simile alle app anche senza una connessione Internet.

>[!NOTE]
>
>Le app web progressive sono una tecnologia in evoluzione e il supporto per l&#39;installazione di app locali e altre funzionalità [dipende dal browser utilizzato.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## Prerequisiti {#prerequisites}

Per poter utilizzare le funzioni di PWA per il sito, sono necessari due requisiti per l’ambiente di progetto:

1. [Utilizza ](#adjust-components) i componenti core per sfruttare questa funzione
1. [Regola i ](#adjust-dispatcher) dispatcher per esporre i file richiesti

Questi sono i passaggi tecnici che l’autore dovrà coordinare con il team di sviluppo. Questi passaggi sono necessari solo una volta per sito.

### Utilizza componenti core {#adjust-components}

La versione 2.15.0 e successive dei componenti core supporta completamente le funzioni PWA dei siti AEM. Poiché AEMaaCS include sempre la versione più recente dei componenti core, puoi sfruttare le funzionalità di PWA predefinite. Il progetto AEMaaCS soddisfa automaticamente questo requisito.

>[!NOTE]
>
>Adobe sconsiglia di utilizzare le funzioni di PWA su componenti personalizzati o componenti non [estesi dai componenti core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
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

La funzione PWA genera e utilizza file `/content/<sitename>/manifest.webmanifest`. Per impostazione predefinita, [il dispatcher](/help/implementing/dispatcher/overview.md) non espone tali file. Per esporre questi file, lo sviluppatore deve aggiungere la seguente configurazione al progetto del sito.

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

A seconda del progetto, potrebbe essere utile includere diversi tipi di estensioni alle regole di riscrittura. L&#39;estensione `webmanifest` può essere utile da includere nelle condizioni di riscrittura quando hai introdotto una regola che nasconde e reindirizzerà le richieste a `/content/<projectName>`.

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## Abilitazione di PWA per il sito {#enabling-pwa-for-your-site}

Se [i prerequisiti](#prerequisites) sono soddisfatti, per un autore di contenuti è molto semplice abilitare le funzioni di PWA su un sito. Di seguito è riportato un profilo di base su come eseguire questa operazione. Le singole opzioni sono descritte in dettaglio nella sezione [Opzioni dettagliate.](#detailed-options)

1. Accedi a AEM.
1. Dal menu principale, tocca o fai clic su **Navigazione** -> **Siti**.
1. Seleziona il progetto dei siti e tocca o fai clic su [**Proprietà**](/help/sites-cloud/authoring/fundamentals/page-properties.md) oppure utilizza il tasto di scelta rapida `p`.
1. Seleziona la scheda **App web progressiva** e configura le proprietà applicabili. Come minimo è necessario:
   1. Selezionare l&#39;opzione **Abilita PWA**.
   1. Definire l&#39; **URL di avvio**.

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

Il sito è ora configurato e può essere [installato come app locale.](#using-pwa-enabled-site)

## Utilizzo del sito abilitato per PWA {#using-pwa-enabled-site}

Dopo aver [configurato il sito per supportare PWA,](#enabling-pwa-for-your-site) è possibile utilizzarlo autonomamente.

1. Accedi al sito in un [browser supportato.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. Nella barra degli indirizzi del browser viene visualizzata una nuova icona che indica che il sito può essere installato come app locale.
   * A seconda del browser, l’icona può variare e il browser può anche visualizzare una notifica (ad esempio un banner o una finestra di dialogo) che indica che è possibile installare come app locale.
1. Installa l&#39;app.
1. L’app verrà installata nella schermata iniziale del dispositivo.
1. Apri l’app, sfoglia un po’ e osserva che le pagine sono disponibili offline.

## Opzioni dettagliate {#detailed-options}

La sezione seguente fornisce ulteriori dettagli sulle opzioni disponibili durante la [configurazione del sito per PWA.](#enabling-pwa-for-your-site)

### Configurare l’esperienza installabile {#configure-installable-experience}

Queste impostazioni consentono al tuo sito di comportarsi come un&#39;app nativa, rendendola installabile nella schermata iniziale del visitatore e disponibile offline.

* **Abilita PWA** : questa è l’opzione principale per abilitare PWA per il sito.
* **URL di avvio** : questo è l&#39; [URL di avvio ](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) preferito che l&#39;app verrà aperta quando l&#39;utente carica l&#39;app installata localmente.
   * Può essere un qualsiasi percorso nella struttura del contenuto.
   * Questa non deve essere la radice ed è spesso una pagina di benvenuto dedicata per l’app.
   * Se questo URL è relativo, l&#39;URL manifesto viene utilizzato come URL di base per risolverlo.
   * Se lasciata vuota, la funzione utilizza l’indirizzo della pagina web da cui è stata installata l’app.
   * È consigliabile impostare un valore.
* **Modalità di visualizzazione** : un’app abilitata per PWA è ancora un sito AEM distribuito tramite un browser. [Queste ](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) opzioni di visualizzazione definiscono come il browser deve essere nascosto o altrimenti presentato all’utente sul dispositivo locale.
   * **Standalone**  - Il browser è completamente nascosto all’utente e viene visualizzato come un’app nativa. Questo è il valore predefinito.
      * Con questa opzione, la navigazione nelle app deve essere possibile interamente attraverso il contenuto utilizzando collegamenti e componenti sulle pagine del sito senza utilizzare i controlli di navigazione del browser.
   * **Browser**  - Il browser appare come normalmente quando si visita il sito.
   * **Interfaccia utente minima** : il browser è principalmente nascosto, come un’app nativa, ma sono esposti i controlli di navigazione di base.
   * **Schermo intero** : il browser è completamente nascosto, come un’app nativa, ma viene riprodotto in modalità a schermo intero.
      * Con questa opzione, la navigazione nelle app deve essere possibile interamente attraverso il contenuto utilizzando collegamenti e componenti sulle pagine del sito senza utilizzare i controlli di navigazione del browser.
* **Orientamento dello schermo** : in quanto app locale, PWA deve sapere come gestire gli orientamenti  [del dispositivo.](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **Qualsiasi** : l’app si adatta all’orientamento del dispositivo dell’utente. Questo è il valore predefinito.
   * **Verticale** : consente di aprire l’app in layout verticale indipendentemente dall’orientamento del dispositivo dell’utente.
   * **Orizzontale** : consente di aprire l’app in un layout orizzontale indipendentemente dall’orientamento del dispositivo dell’utente.
* **Colore tema** : definisce il  [colore dell’](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) app che influisce sul modo in cui il sistema operativo dell’utente locale visualizza la barra degli strumenti dell’interfaccia utente nativa e i controlli di navigazione. A seconda del browser, può influenzare altri elementi di presentazione dell’app.
   * Utilizzare la finestra a comparsa del pozzetto del colore per selezionare un colore.
   * Il colore può essere definito anche dal valore esadecimale o RGB.
* **Colore di sfondo** : definisce il colore di  [sfondo dell’app, ](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) che viene mostrato durante il caricamento dell’app.
   * Utilizzare la finestra a comparsa del pozzetto del colore per selezionare un colore.
   * Il colore può essere definito anche dal valore esadecimale o RGB.
   * Alcuni browser [generano automaticamente una schermata iniziale](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) dal nome dell&#39;app, dal colore di sfondo e dall&#39;icona.
* **Icona** : definisce  [l’](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) icona che rappresenta l’app sul dispositivo dell’utente.
   * L&#39;icona deve essere un file png di dimensioni 512x512 pixel.
   * L&#39;icona deve essere [memorizzata in DAM.](/help/assets/overview.md)

### Gestione cache (avanzata) {#offline-configuration}

Queste impostazioni rendono alcune parti del sito disponibili offline e disponibili localmente sul dispositivo del visitatore. Questo consente di controllare la cache dell’app web per ottimizzare le richieste di rete e supportare le esperienze offline.

* **Strategia di memorizzazione in cache e frequenza di aggiornamento**  dei contenuti: questa impostazione definisce il modello di memorizzazione in cache per PWA.
   * **Moderatamente**  -  [Questa ](https://web.dev/stale-while-revalidate/) impostazione è valida per la maggior parte dei siti ed è il valore predefinito.
      * Con questa impostazione, il contenuto visualizzato per la prima volta dall’utente viene caricato dalla cache e mentre l’utente sta consumando quel contenuto, il resto del contenuto nella cache verrà riconvalidato.
   * **Frequentemente**  - Questo è il caso per i siti che hanno bisogno di aggiornamenti per essere molto veloci come le case d&#39;asta.
      * Con questa impostazione, l’app cercherà prima il contenuto più recente tramite la rete e, se non è disponibile, tornerà alla cache locale.
   * **Raramente**  - Questo è il caso dei siti quasi statici, come le pagine di riferimento.
      * Con questa impostazione, l’app cercherà prima il contenuto nella cache e, se non disponibile, tornerà sulla rete per recuperarlo.
* **File pre-caching**  - Questi file in hosting su AEM verranno salvati nella cache del browser locale quando il service worker sta installando e prima di essere utilizzati. Questo garantisce che l’app web sia completamente funzionante quando è offline.
* **inclusioni di percorsi** : le richieste di rete per i percorsi definiti vengono intercettate e il contenuto nella cache viene restituito in conformità alla strategia di  **caching configurata e alla frequenza di aggiornamento** del contenuto.
* **Esclusioni di cache**  - Questi file non verranno mai memorizzati nella cache indipendentemente dalle impostazioni in  **File pre-** caching e inclusioni di  **percorso**.

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

Le librerie client vengono distribuite con l’aggiunta di un selettore di cache che osservi il seguente pattern `lc-<checksumHash>-lc`. Ogni volta che uno dei file (e delle dipendenze) che compongono una modifica della libreria, questo selettore cambia. Se hai elencato una libreria-client che deve essere pre-memorizzata nella cache da service-worker e desideri fare riferimento a una nuova versione, recupera e aggiorna manualmente la voce. Di conseguenza, consigliamo di configurare il sito come PWA dopo la stabilizzazione degli script di progetto e dei fogli di stile.

### Riduci al minimo il numero di varianti di immagine. {#minimize-variations}

Il componente Immagine dei componenti core AEM determina uno dei front-end il rendering migliore da recuperare. Questo meccanismo include anche una marca temporale corrispondente all’ora dell’ultima modifica apportata alla risorsa. Questo meccanismo complica la configurazione del pre-cache di PWA.

Durante la configurazione della pre-cache, l’utente deve elencare tutte le varianti di percorso che possono essere recuperate. Queste varianti sono composte da parametri come la qualità e la larghezza. Si consiglia vivamente di ridurre il numero di queste variazioni ad un massimo di tre - piccolo, medio, grande. Puoi farlo tramite la finestra di dialogo content-policy del [componente immagine.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html)

Se non viene configurata con attenzione, il consumo di memoria e rete può influire notevolmente sulle prestazioni di PWA. Inoltre, se si intende prememorizzare in cache, ad esempio, 50 immagini e avere 3 larghezze per immagine, l’utente che gestisce il sito dovrà mantenere un elenco di fino a 150 voci nella sezione pre-cache di PWA delle proprietà della pagina.

Adobe consiglia inoltre di configurare il sito come PWA dopo la stabilizzazione dell’utilizzo delle immagini nel progetto.
