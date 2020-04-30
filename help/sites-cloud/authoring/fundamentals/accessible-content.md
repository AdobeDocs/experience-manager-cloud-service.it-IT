---
title: Creazione di contenuti accessibili per Adobe Experience Manager come servizio cloud (conformità WCAG 2.1)
description: Crea contenuti web accessibili e utilizzabili da utenti disabili
translation-type: tm+mt
source-git-commit: 6d905c5a29b71c9d05dba910a20ffef21a4eceec

---


# Creazione di contenuto accessibile (conformità WCAG 2.1) {#creating-accessible-content-wcag-conformance}

Le linee guida per l&#39;accessibilità dei contenuti [Web (WCAG) 2.1](https://www.w3.org/TR/WCAG/), elaborate da [un gruppo di lavoro del World Wide Wec Consortium](https://www.w3.org/consorzio/attività#Accessibility_Guidelines_Working_Group), sono costituite da una serie di linee guida tecnologiche indipendenti e da criteri di successo che contribuiscono a rendere i contenuti Web accessibili e utilizzabili da persone con disabilità.

Come introduzione, il consorzio fornisce una serie di sezioni e documenti giustificativi:

* [Nuove funzioni in WCAG 2.1](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [Come soddisfare le linee guida WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Informazioni sulle linee guida WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Tecniche per WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)
* [Documenti WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

Inoltre, vedete:
* Our [Quick Guide to WCAG 2.1](/help/onboarding/accessibility/quick-guide-wcag.md) for further details

<!-- 
>* [Configuring the Rich Text Editor for producing accessible conten](/help/sites-administering/rte-accessible-content.md)
-->

Le linee guida sono classificate in base a tre livelli di conformità: Livello A (più basso), livello AA e livello AAA (più alto). Brevemente, i livelli sono definiti come segue:

* **Livello A**: il sito ha raggiunto un livello minimo di accessibilità di base. Per arrivare a questo livello sono stati soddisfatti tutti i criteri di successo di livello A.
* **Livello AA**: si tratta di un livello di accessibilità ideale, in cui il sito presenta un livello massimo di accessibilità che lo rende fruibile dal maggior numero di persone nella maggioranza delle situazioni utilizzando la maggior parte delle tecnologie. Per ottenere questo livello, devono essere soddisfatti tutti i criteri di successo dei livelli A e AA.
* **Livello AAA**: il sito ha raggiunto un livello molto alto di accessibilità. Per arrivare a questo livello sono stati soddisfatti tutti i criteri di successo di livello A, AA e AAA.

Quando si crea un sito, è necessario determinare il livello complessivo che si desidera ottenere.

Nella sezione seguente sono incluse le [linee guida WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) e i criteri di successo per i [livelli di conformità](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1) A e AA.

>[!NOTE]
>
>Poiché non è possibile soddisfare tutti i criteri di successo di livello AAA per alcuni tipi di contenuti, non è consigliabile prevedere questo livello di conformità come politica generale.

>[!NOTE]
>
>In questo documento stiamo utilizzando:
>
>* The short names for the [WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance).
>* The numbering used in the [WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) to aid cross-referencing with the WCAG website.
>



## Principio 1: Percepibilità  {#principle-perceivable}

[Principio 1: Percepibilità - Informazioni e componenti dell’interfaccia utente devono essere presentati agli utenti con modalità da loro percepibili.](https://www.w3.org/TR/WCAG/#perceivable)

### Alternative testuali (1.1)  {#text-alternatives}

[Linea guida 1.1 - Alternative testuali: fornire alternative testuali per qualsiasi contenuto non testuale in modo che possa essere convertito in altri formati richiesti, come la stampa a caratteri grandi, il Braille, la sintesi vocale, i simboli o un linguaggio più semplice.](https://www.w3.org/TR/WCAG/#text-alternatives)

### Contenuto non testuale (1.1.1)  {#non-text-content}

* Criterio di successo 1.1.1
* Livello A
* Contenuto non testuale: tutto il contenuto non testuale presentato all’utente dispone di un’alternativa testuale che svolge la finalità equivalente, fatta eccezione per le situazioni elencate di seguito.

#### Finalità - Contenuto non testuale (1.1.1) {#purpose-non-text-content}

Le informazioni su una pagina web possono essere fornite in diversi formati non testuali, ad esempio immagini, video, animazioni, tabelle e grafici. Le persone non vedenti o con gravi problemi visivi non sono in grado di vedere il contenuto non testuale, ma possono accedere ai contenuti testuali letti mediante un’utilità per la lettura dello schermo o presentati in forma tattile da un dispositivo Braille. Così, grazie alla disponibilità di alternative testuali al contenuto in formato grafico, i non vedenti possono accedere a una versione equivalente delle informazioni veicolate.

Un ulteriore vantaggio è rappresentato dal fatto che le alternative testuali consentono l’indicizzazione dei contenuti non testuali da parte dei motori di ricerca.

#### Come soddisfare il criterio - Contenuto non testuale (1.1.1)  {#how-to-meet-non-text-content}

Per gli elementi grafici statici, il requisito fondamentale consiste nel fornire un’alternativa testuale equivalente. Questo può essere fatto nel campo **Testo Alt**:

>[!NOTE]
>
>Alcuni componenti pronti per l’uso, come **Carosello** e **Presentazione**, non consentono di aggiungere descrizioni di testo alternativo alle immagini. Quando implementi le versioni di questi componenti per l’istanza AEM, il team di sviluppo dovrà configurarli per supportare l’attributo `alt`, affinché gli autori possano aggiungerlo al contenuto (consulta Aggiunta di supporto per elementi e attributi HTML aggiuntivi).

<!--
>Some out-of-the-box components, such as **Carousel** and **Slideshow** do not provide a means for adding alternate text descriptions to images. When implementing versions of these for your AEM instance, your development team will need to configure such components to support the `alt` attribute so that authors can add it to the content (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).
-->

In AEM il campo **Testo alternativo** deve essere compilato per impostazione predefinita. Se l’immagine è solamente decorativa e il testo alternativo non sarebbe appropriato, seleziona l’opzione **L’immagine è decorativa**.

#### Creazione di buone alternative testuali  {#creating-good-text-alternatives}

Esistono varie forme di contenuti non testuali, di conseguenza il valore del testo alternativo dipende dal ruolo dell’elemento grafico all’interno della pagina web. Alcune regole generali da seguire:

* Le alternative testuali dovrebbero essere sintetiche ma veicolare chiaramente le informazioni essenziali fornite dal contenuto non testuale.
* È bene evitare descrizioni eccessivamente lunghe (oltre 100 caratteri). Se un testo alternativo richiede una descrizione più dettagliata:
   * fornisci una breve descrizione nel testo alternativo
   * e includi una descrizione più lunga in un altro elemento di testo, nella stessa pagina o in una pagina web separata. Inserisci un collegamento a questa descrizione separata rendendo l’immagine un collegamento o inserendo un collegamento di testo accanto all’immagine.
* Il testo alternativo non dovrebbe replicare il contenuto fornito sotto forma di testo nella stessa pagina. Ricorda che molte immagini sono illustrazioni di punti già trattati nel testo di una pagina, di conseguenza un’alternativa testuale dettagliata potrebbe già esistere.
* Se il contenuto non testuale è un collegamento a un’altra pagina o un altro documento e non esiste altro testo che faccia parte dello stesso collegamento, il testo alternativo per l’immagine non dovrà descrivere l’immagine ma dovrà invece indicare la destinazione del collegamento.
* Se il contenuto non testuale è incluso in un elemento pulsante e non esiste testo che faccia parte dello stesso pulsante, il testo alternativo per l’immagine non dovrà descrivere l’immagine, ma piuttosto indicare la funzionalità del pulsante.
* È perfettamente accettabile associare a un’immagine un testo alternativo vuoto (null), ma solo se l’immagine non prevede testo alternativo (ad esempio, se si tratta di un elemento grafico puramente decorativo) o se il testo equivalente è già incluso nel testo della pagina.

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

Tipi specifici di contenuto non testuale che richiedono alternative testuali potrebbero includere:

* Foto illustrative: queste sono immagini di persone, oggetti o luoghi. Pensa al ruolo della foto nella pagina: un equivalente testuale adeguato sarà probabilmente `Photo of [object]`, ma potrebbe dipendere dal testo circostante.
* Icone: Si tratta di piccoli pittogrammi (immagini) che veicolano informazioni specifiche. Devono essere utilizzati in modo coerente all’interno di una pagina e del sito. Tutte le istanze dell’icona in una pagina o in un sito devono avere lo stesso testo alternativo, breve e sintetico, a meno che questo determini inutili duplicazioni di testo adiacente.
* Grafici e diagrammi: solitamente rappresentano dati numerici. Di conseguenza, un possibile testo alternativo potrebbe consistere in una breve sintesi delle principali tendenze indicate nel diagramma o grafico. Se necessario, fornisci anche una descrizione più dettagliata nel testo utilizzando il campo **Descrizione** nella scheda **Avanzate** delle proprietà dell’immagine. In aggiunta, è possibile fornire i dati di origine in formato tabellare altrove nella pagina o nel sito.
* Mappe, diagrammi, diagrammi di flusso: per gli elementi grafici che forniscono dati spaziali (ad esempio, per la descrizione di relazioni tra oggetti o un processo), assicurati che il messaggio principale venga comunicato in formato testuale. Per le mappe, sarà probabilmente poco pratico fornire un testo equivalente completo. Tuttavia, se la mappa ha lo scopo di indicare il percorso verso una particolare destinazione, il testo alternativo dell’immagine della mappa potrà brevemente indicare *Mappa di X*, e quindi fornire indicazioni nel testo altrove sulla pagina o mediante il campo **Descrizione** nella scheda **Avanzate** del componente **Immagine**.
* CAPTCHA: è l’acronimo di “*Completely Automated Public Turing test to tell Computers and Humans Apart*” (test di Turing completamente automatizzato per distinguere macchine e persone). Viene utilizzato come controllo di sicurezza nelle pagine web per distinguere esseri umani da software dannosi, ma che può rappresentare un ostacolo all’accessibilità. Si tratta di immagini che richiedono agli utenti di descrivere ciò che vedono, al fine di superare un test di sicurezza. Fornire un testo alternativo per l’immagine non è ovviamente possibile, quindi sarà necessario prendere in considerazione soluzioni alternative non grafiche. Il W3C fornisce una serie di suggerimenti (ciascuno dei quali presenta vantaggi e svantaggi), ad esempio:
   * Puzzle logici
   * L’impiego di output audio anziché di immagini
   * Account a utilizzo limitato e filtri anti-spam.
* Immagini di sfondo: sono ottenute utilizzando i CSS (Cascading Style Sheets, fogli di stile a cascata) anziché in HTML, e non è quindi possibile specificare un valore di testo alternativo. Pertanto le immagini di sfondo non dovrebbero includere informazioni testuali importanti, a meno che non siano incluse anche nel testo della pagina. Tuttavia, è importante utilizzare uno sfondo alternativo per i casi in cui l’immagine non possa essere visualizzata.

>[!NOTE]
>
>Dovrebbe essere previsto un livello adeguato di contrasto tra lo sfondo e il testo in primo piano; questo elemento viene discusso più dettagliatamente in [Contrasto (minimo) (1.4.3)](#contrast-minimum).

#### Ulteriori informazioni - Contenuto non testuale (1.1.1)  {#more-information-non-text-content}

* [Comprendere i criteri di successo 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [Come soddisfare i criteri di successo 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [Spiegazione W3C dei CAPTCHA e relative alternative](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### Elementi multimediali temporizzati (1.2)  {#time-based-media}

[Linea guida 1.2; elementi multimediali temporizzati: fornire alternative per gli elementi multimediali temporizzati.](https://www.w3.org/TR/WCAG/#time-based-media)

L’argomento riguarda i contenuti web *temporizzati*. Questi comprendono i contenuti che l’utente può riprodurre (come video, audio e contenuti animati) e che possono essere preregistrati o in streaming.

### Audio-only and Video-only (Prerecorded) (1.2.1) {#audio-only-and-video-only-prerecorded}

* Criterio di successo 1.2.1
* Livello A
* Solo audio e solo video (preregistrato): per gli elementi solo video e solo audio preregistrati vale quanto segue, tranne quando l’audio o il video sia un elemento alternativo per il testo, chiaramente indicato come tale:
   * Solo audio preregistrato: viene fornita un’alternativa per gli elementi multimediali temporizzati che presenti le informazioni equivalenti ai contenuti solo audio preregistrati.
   * Solo video preregistrato: viene fornita un’alternativa per gli elementi multimediali temporizzati o una traccia audio che presenti le informazioni equivalenti ai contenuti solo video preregistrati.

#### Purpose - Audio-only and Video-only (Prerecorded) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

Problemi di accessibilità per video e audio possono essere riscontrati da:

* Persone con problemi visivi in assenza di audio o quando l’audio non è sufficiente a informarli di ciò che sta accadendo nel video o nell’animazione;
* Persone con disabilità uditive o non udenti, non in grado di sentire l’audio;
* Persone che possono sentire l’audio, ma non comprendono i dialoghi (ad esempio, perché si svolgono in una lingua che non conoscono).

Video o audio possono anche essere non disponibili per chi utilizza browser o dispositivi che non supportano la riproduzione di contenuti in formati multimediali specifici, come Adobe Flash.

Fornire queste informazioni in un formato diverso, ad esempio testo (o audio per i video senza audio) può renderle accessibili alle persone impossibilitate ad accedere al contenuto originale.

#### How to Meet - Audio-only and Video-only (Prerecorded) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* Se il contenuto è una traccia audio preregistrata senza video (come un podcast):
   * Fornisci un collegamento immediatamente prima o dopo il contenuto, che rimandi a una trascrizione in formato testo del contenuto audio. La trascrizione dovrebbe essere una pagina HTML con un equivalente testuale di tutti i contenuti parlati e non parlati rilevanti, oltre all’indicazione di chi sta parlando, una descrizione dell’ambientazione, le espressioni vocali e una descrizione di qualsiasi altro elemento sonoro significativo.
* Se il contenuto è un’animazione o un video preregistrato senza audio:
   * Fornisci un collegamento immediatamente prima o dopo il contenuto, che rimandi a una descrizione testuale equivalente delle informazioni fornite nel video.
   * Oppure fornisci una descrizione audio equivalente in un formato audio comunemente utilizzato, come MP3.

>[!NOTE]
>
>Se il contenuto audio o video è fornito come alternativa a contenuto già esistente in un altro formato in una pagina web, non è necessario soddisfare i requisiti di cui sopra. Ad esempio, se un video illustra un elenco di istruzioni testuali, non richiede un’alternativa in quanto le istruzioni testuali già fungono da alternativa al video.

L’inserimento di elementi multimediali nelle pagine web AEM, in particolare contenuti Flash, è simile a quello di un’immagine. Tuttavia, dato che i contenuti multimediali sono molto più di un fermo immagine, esistono differenti impostazioni e opzioni per controllarne la riproduzione.

>[!NOTE]
>
>Quando si utilizzano elementi multimediali con contenuti informativi, è necessario creare anche collegamenti a contenuti alternativi. Ad esempio, per includere una trascrizione testuale, crea una pagina HTML per visualizzare la trascrizione e quindi aggiungi un collegamento accanto o sotto al contenuto audio.

#### More Information - Audio-only and Video-only (Prerecorded) (1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [Comprendere i criteri di successo 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [Come soddisfare i criteri di successo 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### Sottotitoli (preregistrati) (1.2.2) {#captions-prerecorded}

* Criterio di successo 1.2.2
* Livello A
* Sottotitoli (preregistrati): i sottotitoli vengono forniti per tutti i contenuti audio preregistrati negli elementi multimediali sincronizzati, fatta eccezione per il caso in cui l’elemento multimediale sia alternativo al testo e chiaramente indicato come tale.

#### Finalità - Sottotitoli (preregistrati) (1.2.2) {#purpose-captions-prerecorded}

Le persone non udenti o ipoudenti non saranno in grado di accedere ai contenuti audio, o avranno gravi difficoltà di accesso. I sottotitoli sono equivalenti testuali dell’audio, parlato e non, visualizzati sullo schermo al momento opportuno nel corso del video. Consentono a chi non può udire l’audio di comprendere cosa sta succedendo.

>[!NOTE]
>
>I sottotitoli non sono richiesti quando testo o equivalenti non testuali adeguati (che forniscano informazioni direttamente equivalenti) sono disponibili sulla stessa pagina del video o delle animazioni.

#### How to Meet - Captions (Prerecorded) (1.2.2) {#how-to-meet-captions-prerecorded}

I sottotitoli possono essere:

* Apri: sempre visibile quando il video viene riprodotto
* Sottotitoli codificati: possono essere attivati o disattivati dall’utente

Se possibile, utilizza i sottotitoli codificati allo scopo di consentire agli utenti di scegliere se visualizzarli o meno.

Per i sottotitoli codificati è necessario creare e fornire, unitamente al file video, un file di sottotitoli sincronizzati in un formato appropriato, ad esempio [SMIL](https://www.w3.org/AudioVideo/) (i dettagli su come effettuare questa operazione vanno oltre lo scopo di questa guida, ma abbiamo incluso collegamenti ad alcune esercitazioni nella sezione [Ulteriori informazioni: sottotitoli (preregistrati) (1.2.2)](#more-information-captions-pre-recorded)). Assicurati di includere una nota per indicare agli utenti che per il video sono disponibili sottotitoli.

Se è necessario utilizzare sottotitoli non codificati, inserisci il testo nella traccia video. A questo scopo è possibile utilizzare applicazioni di editing video che consentono di sovrapporre i sottotitoli al video.

#### More Information - Captions (PreRecorded) (1.2.2) {#more-information-captions-prerecorded}

* [Comprendere i criteri di successo 1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html):
* [Come soddisfare i criteri di successo 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### Audio Description or Media Alternative (Prerecorded) (1.2.3) {#audio-description-or-media-alternative-prerecorded}

* Criterio di successo 1.2.3
* Livello A
* Descrizione audio o elemento multimediale alternativo (preregistrato): viene fornita un’alternativa per gli elementi multimediali temporizzati o una descrizione audio del contenuto video preregistrato per gli elementi multimediali sincronizzati, fatta eccezione per il caso in cui l’elemento multimediale sia alternativo al testo, e chiaramente indicato come tale.

#### Purpose - Audio Description or Media Alternative (Prerecorded) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

Le persone non vedenti o ipovedenti avranno problemi di accessibilità se le informazioni in un video o in un’animazione vengono fornite solo visivamente, o se l’audio non fornisce informazioni sufficienti per consentire la comprensione di ciò che sta accadendo.

#### How to Meet - Audio Description or Media Alternative (Prerecorded) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

Gli approcci che è possibile adottare per soddisfare questo criterio di successo sono due. È possibile:

1. Includere una descrizione audio aggiuntiva per il contenuto video. Questo può essere ottenuto in tre modi:
   * In corrispondenza delle pause nella finestra di dialogo, fornisci informazioni sui cambiamenti della scena che non sono inclusi nella traccia audio esistente;
   * Includi una nuova traccia audio, aggiuntiva e facoltativa, contenente l’audio originale, ma anche informazioni audio ulteriori sui cambiamenti della scena.
      * Questo consente agli utenti di passare dalla traccia audio esistente (che *non* contiene una descrizione audio) alla nuova traccia audio (che *contiene* una descrizione audio), e viceversa.
      * In questo modo si evitano interruzioni per gli utenti che non necessitano della descrizione aggiuntiva.
   * Crea una seconda versione del contenuto video per consentire descrizioni audio estese. Questo riduce le difficoltà connesse con la fornitura di descrizioni audio dettagliate all’interno delle pause nella finestra di dialogo esistente, interrompendo temporaneamente audio e video nei momenti adeguati. Come risultato, è possibile fornire una descrizione audio molto più lunga prima che l’azione riprenda. Come nell’esempio precedente, l’ideale, in questo caso, è includere una traccia audio facoltativa per evitare interruzioni agli utenti che non necessitano della descrizione aggiuntiva.
1. Fornisci una trascrizione testuale che rappresenti un equivalente testuale adatto degli elementi sonori e visivi del video o animazione. Questi dovrebbero includere, a seconda del caso, l’indicazione di chi sta parlando, una descrizione dell’ambientazione, espressioni vocali. A seconda della lunghezza, è possibile inserire la trascrizione nella stessa pagina del video o dell’animazione oppure in una pagina separata. Se scegli la seconda opzione, includi un collegamento alla trascrizione accanto al video o all’animazione.

I dettagli precisi sulle modalità di creazione di video con descrizione audio vanno oltre lo scopo di questa guida. La creazione di video e descrizioni audio può richiedere parecchio tempo, ma puoi ricorrere ad altri prodotti Adobe per facilitare l’esecuzione di tali attività. Se crei contenuto in Adobe Flash Professional, devi anche creare uno script per richiedere all’utente di scaricare il plug-in appropriato e fornire un testo alternativo attraverso l’elemento `<noscript>`.

#### More Information - Audio Description or Media Alternative (Prerecorded) (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [Comprendere i criteri di successo 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html):
* [Come soddisfare i criteri di successo 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)
* [Adobe Encore](https://www.adobe.com/products/encore.html)

### Sottotitoli (dal vivo) (1.2.4)    {#captions-live}

* Criterio di successo 1.2.4
* Livello AA
* Sottotitoli (dal vivo): i sottotitoli vengono forniti per tutti i contenuti audio dal vivo negli elementi multimediali sincronizzati.

#### Finalità - Sottotitoli (dal vivo) (1.2.4)  {#purpose-captions-live}

Questo criterio di successo è identico a [Sottotitoli (preregistrati)](#captions-pre-recorded), in quanto riguarda la rimozione degli ostacoli di accessibilità per persone non udenti o ipoudenti, tranne per il fatto che questo criterio di successo è relativo a presentazioni in tempo reale, come i webcast.

#### Come soddisfare il criterio - Sottotitoli (dal vivo) (1.2.4) {#how-to-meet-captions-live}

Follow the guidance provided for [Captions (Prerecorded)](#captions-prerecorded) above. However, due to the live nature of the media, caption provision has to be created as quickly as possible and in response to what is happening. Therefore, you should consider using real time captioning or speech-to-text tools.

Istruzioni dettagliate al riguardo vanno oltre lo scopo di questo documento, ma informazioni utili sono reperibili tramite le risorse seguenti:

* [WebAIM: aggiunta di sottotitoli in tempo reale](https://www.webaim.org/techniques/captions/realtime.php)

<!--
* [AccessIT (University of Washington): Can captions be generated automatically using speech recognition?](https://www.washington.edu/accessit/articles?1209)
-->

#### Ulteriori informazioni - Sottotitoli (dal vivo) (1.2.4)  {#more-information-captions-live}

* [Comprendere i criteri di successo 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [Come soddisfare i criteri di successo 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### Descrizione audio (preregistrato) (1.2.5) {#audio-description-prerecorded}

* Criterio di successo 1.2.5
* Livello AA
* Descrizione audio (preregistrato): una descrizione audio viene fornita per tutti i contenuti video preregistrati negli elementi multimediali sincronizzati.

#### Purpose - Audio Description (Prerecorded) (1.2.5) {#purpose-audio-description-prerecorded}

This success criterion is identical to [Audio Description or Media Alternative (Prerecorded)](#audio-description-or-media-alternative-prerecorded), except that authors must provide a much more detailed audio description to conform to Level AA.

#### How to Meet - Audio Description (Prerecorded) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Follow the guidance provided for [Audio Description or Media Alternative (Prerecorded)](#audio-description-or-media-alternative-prerecorded).

#### More Information - Audio Description (Prerecorded) (1.2.5) {#more-information-audio-description-prerecorded}

* [Comprendere i criteri di successo 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [Come soddisfare i criteri di successo 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### Adattabilità (1.3)  {#adaptable}

[Linea guida 1.3 - Adattabilità: creare contenuti che possano essere rappresentati in modalità differenti (ad esempio con un layout più semplice), senza perdere informazioni o struttura.](https://www.w3.org/TR/WCAG/#adaptable)

Questa linea guida riguarda i requisiti necessari per supportare le persone che:

* potrebbero non essere in grado di accedere alle informazioni come presentate da un autore in un layout *standard* di pagina web colorato, bidimensionale, a più colonne;

* potrebbero utilizzare una visualizzazione solo audio o una alternativa, ad esempio testo di grandi dimensioni e a contrasto elevato.

### Informazioni e correlazioni (1.3.1)    {#info-and-relationships}

* Criterio di successo 1.3.1
* Livello A
* Informazioni e correlazioni: informazioni, struttura e relazioni veicolate attraverso la presentazione possono essere determinate a livello di programmazione o sono disponibili in formato testo.

#### Finalità - Informazioni e correlazioni (1.3.1)  {#purpose-info-and-relationships}

Molte tecnologie per l’accessibilità utilizzate da persone con disabilità si basano su informazioni strutturali per visualizzare o rappresentare i contenuti in modo efficace. Queste possono assumere la forma di titoli, intestazioni di righe e colonne di tabella, e tipi di elenchi. Ad esempio, un’utilità di lettura dello schermo potrebbe consentire a un utente di spostarsi all’interno di una pagina passando da un’intestazione a un’altra. Tuttavia, quando la struttura del contenuto della pagina dipende esclusivamente da uno stile visivo, anziché dal codice HTML sottostante, non sono presenti informazioni strutturali utilizzabili dalle tecnologie per l’accessibilità, il che ne limita la capacità di supportare la navigazione facilitata.

Questo criterio di successo esiste per fare in modo che tali informazioni strutturali vengano fornite tramite HTML, in modo che i browser e le tecnologie per l’accessibilità possano accedere e sfruttare le informazioni.

#### Come soddisfare il criterio - Informazioni e correlazioni (1.3.1)  {#how-to-meet-info-and-relationships}

AEM consente di creare in modo semplice pagine web utilizzando gli elementi HTML appropriati. Apri i contenuti della pagina nell’editor Rich Text (un componente testo) e usa il menu **Formato paragrafo** (simbolo di paragrafo) per specificare l’elemento strutturale appropriato (ad esempio paragrafo, intestazione e così via).

È possibile assicurarsi che alle pagine web sia associata la struttura corretta:

* **Utilizzo dei titoli:** fintanto che le funzioni di accessibilità di RTE sono abilitate, AEM offre 3 livelli di intestazione di pagina. Puoi utilizzarli per identificare sezioni e sottosezioni di contenuto. Titolo 1 rappresenta il livello di intestazione più alto, Titolo 3 quello più basso. L’amministratore di sistema può configurare il sistema per consentire l’utilizzo di più livelli di intestazione.
* **Testo con enfasi**: utilizza l’elemento `<strong>` o `<em>` per indicare l’enfasi. Non utilizzare le intestazioni per evidenziare il testo all’interno dei paragrafi.
   * Evidenzia il testo che desideri mettere in evidenza.
   * Fai clic sull’icona **B** (per `<strong>`) oppure **I** (per `<em>`) nel pannello **Proprietà**, assicurandoti che sia selezionato HTML.

      >[!NOTE]
      >
      >L’editor Rich Text in un’installazione standard di AEM è configurato per utilizzare:
      >
      >* `<b>` per `<strong>`
      >* `<i>` per `<em>`
      >
      >L’efficacia è la medesima, ma `<strong>` e `<em>` sono preferibili in quanto rappresentano un html corretto dal punto di vista semantico. Il tuo team di sviluppo può configurare l’editor Rich Text in modo che utilizzi `<strong>` e `<em>` (anziché `<b>` e `<i>`) durante lo sviluppo dell’istanza di progetto.


* **Utilizzare gli elenchi**: è possibile utilizzare l’HTML per specificare tre diversi tipi di elenchi:
   * L’elemento `<ul>` viene utilizzato per gli elenchi *non ordinati* (puntati). Le singole voci di elenco sono identificate dall’elemento `<li>`. Nell’editor Rich Text, utilizza l’icona **Elenco puntato**.
   * L’elemento `<ol>`viene utilizzato per gli elenchi *numerati*. Le singole voci dell’elenco sono identificate dall’elemento `<li>`. Nell’editor Rich Text, utilizza l’icona **Elenco numerato**.
   Se desideri convertire contenuti esistenti in un determinato tipo di elenco, evidenzia il testo desiderato e seleziona il tipo di elenco. Come nel precedente esempio, che mostra come inserire un testo di paragrafo, gli elementi elenco adeguati verranno aggiunti automaticamente al codice HTML.

   In modalità a tutto schermo, sono visibili le singole icone **Elenco puntato** ed **Elenco numerato**. Se non è attiva la modalità a tutto schermo, le due opzioni sono disponibili dietro la singola icona **Elenchi**.
* **Utilizzare le tabelle:** le tabelle di dati devono essere identificate utilizzando gli elementi di tabella HTML:
   * un elemento `<table>`
   * un elemento `<tr>` per ogni riga della tabella
   * un elemento `<th>` per ogni intestazione di riga e colonna
   * un elemento `<td>` per ogni cella di dati
   In aggiunta, le tabelle accessibili fanno uso dei seguenti elementi e attributi:

   * L’elemento `<caption>` viene utilizzato per fornire una didascalia visibile per la tabella. Per impostazione predefinita, le didascalie vengono visualizzate centrate sopra la tabella, ma possono essere posizionate in modo appropriato utilizzando gli stili CSS. La didascalia è associata alla tabella a livello di programmazione, pertanto è un metodo utile per fornire un’introduzione al contenuto.
   * L’elemento `<summary>` aiuta gli utenti non vedenti a comprendere più facilmente le informazioni presentate all’interno di una tabella, fornendo una sintesi di ciò che un utente vedente può vedere. Risulta particolarmente utile quando si utilizzano layout di tabella complessi o non convenzionali (l’attributo non viene visualizzato nel browser, ma viene letto solo alle tecnologie per l’accessibilità).
   * L’attributo `scope` dell’elemento `<th>` viene utilizzato per indicare se una cella rappresenta un’intestazione per una particolare riga o colonna. Un approccio simile consiste nell’utilizzare gli attributi header e id in tabelle complesse, dove le celle di dati possono essere associate a una o più intestazioni.
   >[!NOTE]
   >
   >Per impostazione predefinita questi elementi e attributi non sono direttamente disponibili, anche se l’amministratore di sistema può aggiungere supporto per questi valori nella finestra di dialogo **Proprietà tabella** (consulta Aggiunta di supporto per elementi e attributi HTML aggiuntivi).

<!-- removed link syntax for ExL - Bob Bringhurst
>By default, these elements and attributes are not directly available, though it is possible for the system administrator to add support for these values in the **Table properties** dialog box (see Adding Support for Additional HTML Elements and Attributes /help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes).
-->

Per aprire la finestra di dialogo **Tabella** in cui puoi selezionare le **Proprietà tabella**:

* Definisci una **Didascalia** appropriata.
* È consigliabile rimuovere eventuali valori predefiniti per **Larghezza**, **Altezza**, **Bordo**, **Margine celle**, **Spaziatura celle**. dato che queste proprietà possono essere impostate in un foglio di stile globale.

Puoi quindi utilizzare le **Proprietà cella** per scegliere se la cella contiene dati o intestazione:

* **Tabelle dati complesse**: in alcuni casi, in presenza di tabelle complesse con due o più livelli di intestazioni, le proprietà della tabella di base potrebbero non essere sufficienti a fornire tutte le informazioni strutturali necessarie. Per questo tipo di tabelle complesse, è necessario creare relazioni dirette tra le intestazioni e le celle correlate mediante gli attributi **header** e **id**. Ad esempio, nella tabella seguente le intestazioni e gli ID vengono abbinati per creare un’associazione programmatica per gli utenti di tecnologie per l’accessibilità.

   >[!NOTE]
   >
   >L’attributo id non è disponibile in un’installazione standard. Può essere attivato configurando regole HTML e il serializzatore nell’editor Rich Text.

```xml
 <table>
    <tr>
      <th rowspan="2" id="h">Homework</th>
      <th colspan="3" id="e">Exams</th>
      <th colspan="3" id="p">Projects</th>
    </tr>
    <tr>
      <th id="e1" headers="e">1</th>
      <th id="e2" headers="e">2</th>
      <th id="ef" headers="e">Final</th>
      <th id="p1" headers="p">1</th>
      <th id="p2" headers="p">2</th>
      <th id="pf" headers="p">Final</th>
    </tr>
    <tr>
     <td headers="h">15%</td>
     <td headers="e e1">15%</td>
     <td headers="e e2">15%</td>
     <td headers="e ef">20%</td>
     <td headers="p p1">10%</td>
     <td headers="p p2">10%</td>
     <td headers="p pf">15%</td>
    </tr>
   </table>
```

A questo scopo, in AEM è necessario aggiungere il codice utilizzando direttamente la modalità di modifica sorgente.

>[!NOTE]
>
>Questa funzionalità non è immediatamente disponibile in un’installazione standard. Richiede la configurazione dell’editor Rich Text, di regole HTML e del serializzatore.

#### Ulteriori informazioni - Informazioni e correlazioni (1.3.1)  {#more-information-info-and-relationships}

* [Comprendere i criteri di successo 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [Come soddisfare i criteri di successo 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### Sequenza significativa (1.3.2) {#meaningful-sequence}

* Criterio di successo 1.3.2
* Livello A
* Sequenza Significativa: Quando la sequenza in cui viene presentato il contenuto ne influenza il significato, è possibile determinare a livello di programmazione una sequenza di lettura corretta.

#### Finalità - Sequenza significativa (1.3.2) {#purpose-meaningful-sequence}

Lo scopo di questo criterio di successo è quello di consentire a un agente utente di fornire una presentazione alternativa del contenuto, preservando l&#39;ordine di lettura necessario per comprendere il significato. È importante che sia possibile determinare a livello di programmazione almeno una sequenza del contenuto che abbia senso. I contenuti che non soddisfano questo criterio di successo possono confondere o disorientare gli utenti quando la tecnologia di supporto legge il contenuto in ordine errato o quando vengono applicati fogli di stile alternativi o altre modifiche di formattazione.

#### Come soddisfare il criterio - Sequenza significativa (1.3.2) {#how-to-meet-meaningful-sequence}

Seguite le linee guida in [Come soddisfare i criteri di successo 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### Ulteriori informazioni - Sequenza significativa (1.3.2) {#more-information-meaningful-sequence}

* [Comprendere i criteri di successo 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [Come soddisfare i criteri di successo 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### Caratteristiche sensoriali (1.3.3)    {#sensory-characteristics}

* Criterio di successo 1.3.3
* Livello A
* Caratteristiche sensoriali: le istruzioni fornite per comprendere e intervenire sui contenuti non si basano unicamente su caratteristiche sensoriali dei componenti quali forma, dimensione, ubicazione visiva, orientamento o audio.

#### Finalità - Caratteristiche sensoriali (1.3.3)  {#purpose-sensory-characteristics}

Nel presentare le informazioni, i designer spesso si concentrano sulle caratteristiche di progettazione visiva come il colore, la forma, lo stile del testo o la posizione assoluta o relativa di un elemento di contenuto. Anche se queste possono essere tecniche di progettazione molto potenti per veicolare le informazioni, le persone non vedenti o ipovedenti potrebbero non essere in grado di accedere alle informazioni che richiedono l’identificazione visiva di attributi come la posizione, il colore o la forma.

Allo stesso modo, le informazioni che richiedono di distinguere tra suoni diversi (ad esempio, contenuti parlati da voci di sesso maschile o femminile) presenteranno problemi di accessibilità per le persone con disabilità uditive, se non vengono incluse in un testo alternativo per il contenuto audio.

>[!NOTE]
>
>Per i requisiti collegati alle alternative ai colori, consulta [Utilizzo del colore](#use-of-color).

#### Come soddisfare il criterio - Caratteristiche sensoriali (1.3.3)  {#how-to-meet-sensory-characteristics}

Assicurati che tutte le informazioni che si basano su caratteristiche visive del contenuto di pagina siano presentate anche in un formato alternativo.

* Non fare affidamento sulla posizione visiva per fornire informazioni. Ad esempio, se desideri indirizzare gli utenti a un menu sul lato destro della pagina per l’accesso alle informazioni, non fare riferimento al *menu a destra*, ma denomina il menu (ad esempio attraverso un’intestazione) e fai riferimento al nome nel testo.
* Non fare affidamento sullo stile del testo (ad esempio, testo in grassetto o in corsivo) come unico modo per trasmettere le informazioni.

>[!NOTE]
>
>L’utilizzo di termini descrittivi sarà accettabile se questi hanno un significato in un contesto non visivo. Ad esempio, l’utilizzo dei termini *sopra* e *sotto* sarà generalmente accettabile, in quanto si riferiscono rispettivamente al contenuto prima e dopo un particolare elemento di contenuto; questa indicazione continuerà ad avere senso quando il contenuto è parlato.

#### Ulteriori informazioni - Caratteristiche sensoriali (1.3.3)  {#more-information-sensory-characteristics}

* [Comprendere i criteri di successo 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [Come soddisfare i criteri di successo 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### Distinguibilità (1.4)  {#distinguishable}

[Linea guida 1.4 - Distinguibilità: facilitare agli utenti la visione e l’ascolto dei contenuti, separando gli elementi in primo piano dallo sfondo.](https://www.w3.org/TR/WCAG/#distinguishable)

### Utilizzo del colore (1.4.1)    {#use-of-color}

* Criterio di successo 1.4.1
* Livello A
* Utilizzo del colore: il colore non è utilizzato come unica modalità visiva per rappresentare le informazioni, indicare un’azione, richiedere una risposta o distinguere un elemento visivo.

>[!NOTE]
>
>Questo criterio di successo riguarda in particolare la percezione del colore. Altre forme di percezione sono illustrate in [Adattabilità (1.3)](#adaptable); compreso l’accesso programmatico al colore e ad altre codifiche presentazione visiva.

#### Finalità - Utilizzo del colore (1.4.1)  {#purpose-use-of-color}

Il colore è un modo efficace per valorizzare l’estetica delle pagine web ed è anche utile per trasmettere informazioni. Tuttavia, esistono una serie di problemi visivi, dalla cecità al daltonismo, che rendono alcune persone incapaci di distinguere tra alcuni colori. Questo rende la codifica tramite colori un modo inaffidabile per fornire informazioni.

Ad esempio, un soggetto con un deficit della visione dei colori rosso-verde non sarà in grado di distinguere tra sfumature di verde e di rosso. Potrà percepire entrambi i colori come un terzo (ad esempio, marrone), nel qual caso non sarà in grado di distinguere tra rosso, verde e marrone.

Inoltre, il colore non può essere percepito da persone che utilizzano browser di solo testo, dispositivi di visualizzazione in bianco e nero o una stampa in bianco e nero della pagina.

#### Come soddisfare il criterio - Utilizzo del colore (1.4.1)  {#how-to-meet-use-of-color}

Qualunque colore sia utilizzato per trasmettere le informazioni, accertati che queste siano disponibili senza che sia necessario vedere il colore stesso.

Ad esempio, accertati che le informazioni fornite dal colore siano presenti in modo esplicito anche nel testo.

Se il colore viene usato come spunto per fornire informazioni, è necessario dare un ulteriore segnale visivo, ad esempio la modifica dello stile (grassetto, corsivo) o del font. Tutto questo favorisce l’identificazione delle informazioni da parte delle persone con problemi di vista o affette da daltonismo. Tuttavia, non vi si può fare completo affidamento, in quanto non aiuterà le persone che non possono vedere affatto la pagina.

#### Ulteriori informazioni - Utilizzo del colore (1.4.1) {#more-information-use-of-color}

* [Comprendere i criteri di successo 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [Come soddisfare i criteri di successo 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

<!-- [Guidance on meeting a 3:1 contrast ratio, containing a list of “web safe” colors](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
-->

### Controllo audio (1.4.2) {#audio-control}

* Criterio di successo 1.4.2
* Livello A
* Controllo audio: Se l&#39;audio di una pagina Web viene riprodotto automaticamente per più di 3 secondi, è disponibile un meccanismo per mettere in pausa o arrestare l&#39;audio, oppure un meccanismo per controllare il volume audio indipendentemente dal livello globale del volume del sistema.

#### Finalità - Controllo audio (1.4.2) {#purpose-audio-control}

Gli utenti che utilizzano il software per la lettura dello schermo possono difficilmente sentire l&#39;uscita audio se è in corso la riproduzione audio. Questa difficoltà è aggravata quando l&#39;uscita vocale dell&#39;assistente vocale è basata su software (come la maggior parte di oggi) ed è controllata attraverso lo stesso controllo del volume del suono. Pertanto, è importante che l&#39;utente sia in grado di disattivare l&#39;audio sullo sfondo. Nota: Il controllo del volume include la possibilità di ridurre il volume a zero.

#### Come soddisfare il criterio - Controllo audio (1.4.2) {#how-to-meet-audio-control}

Seguite le linee guida in [Come soddisfare i criteri di successo 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### Ulteriori informazioni - Controllo audio (1.4.2) {#more-information-audio-control}

* [Comprendere i criteri di successo 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [Come soddisfare i criteri di successo 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### Contrasto (minimo) (1.4.3)  {#contrast-minimum}

* Criterio di successo 1.4.3
* Livello AA
* Contrasto (minimo): la rappresentazione visiva di testo e immagini di testo ha un rapporto di contrasto pari ad almeno 4,5:1, fatta eccezione per i seguenti elementi:
   * Testo di grandi dimensioni: testo di grandi dimensioni e immagini di testo di grandi dimensioni hanno un rapporto di contrasto di almeno 3:1.
   * Incidentale: per il testo o per le immagini di testo che fanno parte di un componente dell’interfaccia inattivo, che sono puramente decorative, non visibili o che fanno parte di un’immagine che contiene altri contenuti visuali significativi, non è previsto alcun requisito di contrasto.
   * Logotipi: per il testo che fa parte di un logo o di un marchio non è previsto alcun requisito minimo di contrasto.

#### Finalità - Contrasto (minimo) (1.4.3)  {#purpose-contrast-minimum}

Le persone con determinate disabilità visive possono non essere in grado di distinguere tra alcune coppie di colori a basso contrasto. Queste persone possono riscontrare problemi di accessibilità se:

* Il testo contrasta poco con il relativo colore di sfondo.
* La codifica di colore del testo (come testo di collegamento e testo non di collegamento) è importante per distinguere le informazioni.

>[!NOTE]
>
>Il testo utilizzato esclusivamente per scopi decorativi è escluso da questo criterio di successo.

#### Come soddisfare il criterio - Contrasto (minimo) (1.4.3)  {#how-to-meet-contrast-minimum}

Assicurati che il testo contrasti a sufficienza con il relativo sfondo. I rapporti di contrasto dipendono dalle dimensioni e dallo stile del testo:

* Per testi con dimensioni inferiori a 18 punti (o 14 se in grassetto), il rapporto di contrasto tra testo/immagini di testo e sfondo deve essere pari ad almeno 4,5:1.
* Per testi con dimensioni almeno pari a 18 punti (o 14 se in grassetto), il rapporto di contrasto deve essere pari ad almeno 3:1.
* Se lo sfondo include un motivo, lo sfondo intorno al testo dovrà essere ombreggiato in modo da mantenere il rapporto di 4,5:1 o 3:1.

Per controllare i rapporti di contrasto, utilizza uno strumento di contrasto del colore, come ad esempio [Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) o [l’utilità di controllo del contrasto di colore di WebAIM](https://www.webaim.org/resources/contrastchecker/). Questi strumenti consentono di controllare le coppie di colori ed evidenziano eventuali problemi di contrasto.

In alternativa, se la specificazione dell’aspetto della pagina non è un problema, è possibile scegliere di non specificare colori di sfondo e del testo in primo piano. In questo caso non sarà necessario alcun controllo del contrasto, in quanto sarà il browser dell’utente a determinare i colori del testo e dello sfondo.

Se non è possibile rispettare i livelli di contrasto raccomandati, sarà necessario fornire un collegamento a una versione alternativa ed equivalente della pagina (senza problemi di contrasto di colore) o consentire all’utente di regolare il contrasto dello schema di colore della pagina in base alle proprie esigenze.

#### Ulteriori informazioni - Contrasto (minimo) (1.4.3)  {#more-information-contrast-minimum}

* [Comprendere i criteri di successo 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [Come soddisfare i criteri di successo 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### Ridimensiona testo (1.4.4) {#resize-text}

* Criterio di successo 1.4.4
* Livello A
* Ridimensiona testo: Eccetto per le didascalie e le immagini di testo, il testo può essere ridimensionato senza tecnologia di supporto fino al 200% senza perdita di contenuti o funzionalità.

#### Finalità - Ridimensiona testo (1.4.4) {#purpose-resize-text}

Lo scopo di questo criterio di successo è garantire che il testo di cui è stato effettuato il rendering visivo, compresi i controlli basati sul testo (caratteri di testo visualizzati in modo che possano essere visualizzati [rispetto ai caratteri di testo che sono ancora nella forma dei dati, come ASCII]), possa essere ridimensionato in modo che possa essere letto direttamente da persone con lievi disabilità visive, senza richiedere l&#39;uso di tecnologie di supporto come una lente di ingrandimento dello schermo. Gli utenti possono trarre vantaggio dal ridimensionamento di tutto il contenuto della pagina Web, ma il testo è molto critico.

#### Come soddisfare il criterio - Ridimensionare il testo (1.4.4) {#how-to-meet-resize-text}

Seguite le linee guida in [Come soddisfare i criteri di successo 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text).

#### Ulteriori informazioni - Ridimensionare il testo (1.4.4) {#more-information-resize-text}

* [Comprendere i criteri di successo 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [Come soddisfare i criteri di successo 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Immagini di testo (1.4.5)  {#images-of-text}

* Criterio di successo 1.4.5
* Livello AA
* Immagini di testo: se le tecnologie utilizzate consentono la presentazione visiva, per trasmettere informazioni viene utilizzato il testo, anziché le immagini di testo, con le seguenti eccezioni:
   * Personalizzabile: l’immagine di testo può essere personalizzata visivamente in base alle esigenze dell’utente;
   * Essenziale: una particolare presentazione del testo è essenziale per il tipo di informazioni veicolate.

>[!NOTE]
>
>I logotipi (testo che fa parte di un logo o di un marchio) sono considerati essenziali.

#### Finalità - Immagini di testo (1.4.5)  {#purpose-images-of-text}

Le immagini di testo vengono spesso utilizzate quando un particolare stile di testo è quello preferenziale (ad esempio un logo) o se il testo è stato generato da un’altra sorgente (ad esempio la scansione di un documento cartaceo). Tuttavia, rispetto al testo presentato in HTML e formattato mediante i CSS, le immagini di testo non hanno la flessibilità necessaria per modificarsi in dimensioni o aspetto nel modo che potrebbe essere necessario per le persone con disabilità visive o difficoltà di lettura.

#### Come soddisfare il criterio - Immagini di testo (1.4.5)  {#how-to-meet-images-of-text}

Se è necessario utilizzare le immagini di testo, utilizza CSS per sostituirle con testo equivalente in HTML, in modo che sia possibile personalizzare il testo. Per visualizzare un esempio di come ottenere questo risultato, consulta [C30: Utilizzare CSS per sostituire il testo con immagini di testo e fornire i comandi dell’interfaccia utente per effettuare il passaggio](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Ulteriori informazioni - Immagini di testo (1.4.5) {#more-information-images-of-text}

* [Comprendere i criteri di successo 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [Come soddisfare i criteri di successo 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## Principio 2: Operabilità  {#principle-operable}

[Principio 2: Operabilità - I componenti dell’interfaccia e la navigazione devono essere operabili.](https://www.w3.org/TR/WCAG/#operable)

### Tastiera accessibile (2.1) {#keyboard-accessible}

[Linea guida 2.1 Tastiera accessibile: Rendere tutte le funzionalità disponibili da una tastiera.](https://www.w3.org/TR/WCAG/#keyboard-accessible)

In questo modo gli utenti possono accedere a tutte le funzionalità utilizzando una tastiera.

### Tastiera (2.1.1) {#keyboard}

* Criterio di successo 2.1.1
* Livello A
* Tastiera: Tutte le funzionalità del contenuto sono utilizzabili attraverso un&#39;interfaccia da tastiera senza che sia necessario un tempo specifico per i singoli tasti, a meno che la funzione sottostante non richieda un input che dipende dal percorso del movimento dell&#39;utente e non solo dai punti finali.

#### Finalità - Tastiera (2.1.1) {#purpose-keyboard}

Lo scopo di questo criterio di successo è garantire che, laddove possibile, il contenuto possa essere gestito tramite una tastiera o un&#39;interfaccia (in modo da poter utilizzare una tastiera alternativa). Quando il contenuto può essere gestito tramite una tastiera o una tastiera alternativa, può essere gestito da persone prive di visione (che non possono utilizzare dispositivi come i topi che richiedono un coordinamento a mano), nonché da persone che devono utilizzare tastiere alternative o dispositivi di input che fungono da emulatori di tastiera. Gli emulatori di tastiera includono software di ingresso vocale, software per sip-and-puff, tastiere su schermo, software di scansione e una varietà di tecnologie di assistenza e tastiere alternative. Gli individui con problemi di vista possono anche avere problemi a tracciare un puntatore e trovare l&#39;uso del software molto più semplice (o solo possibile) se possono controllarlo dalla tastiera.

#### Come soddisfare il criterio - Tastiera (2.1.1) {#how-to-meet-keyboard}

Seguire le linee guida in [Come soddisfare i criteri di successo 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard).

#### Ulteriori informazioni - Tastiera (2.1.1) {#more-information-keyboard}

* [Comprendere i criteri di successo 2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Come soddisfare i criteri di successo 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### Nessuna traccia da tastiera (2.1.2) {#no-keyboard-trap}

* Criterio di successo 2.1.2
* Livello A
* Nessuna traccia da tastiera: Se è possibile spostare lo stato attivo su un componente della pagina utilizzando un&#39;interfaccia di tastiera, è possibile spostare lo stato attivo da tale componente utilizzando solo un&#39;interfaccia di tastiera e, se richiede più di un metodo di uscita standard o freccia non modificata, l&#39;utente è informato del metodo di spostamento dello stato attivo.

#### Finalità - Nessuna traccia da tastiera (2.1.2) {#purpose-no-keyboard-trap}

Lo scopo di questo criterio di successo è garantire che il contenuto non *intercetti* lo stato attivo all&#39;interno delle sottosezioni di contenuto di una pagina Web. Si tratta di un problema comune se all’interno di una pagina vengono combinati più formati e sottoposti a rendering tramite plug-in o applicazioni incorporate.

In alcuni casi, la funzionalità della pagina Web limita lo stato attivo a una sottosezione del contenuto, purché l&#39;utente sia in grado di lasciare tale stato e di *rimuovere il trap* .

#### Come soddisfare il criterio - Nessuna traccia da tastiera (2.1.2) {#how-to-meet-no-keyboard-trap}

Seguire le linee guida in [Come soddisfare i criteri di successo 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap).

#### Ulteriori informazioni - Nessuna traccia da tastiera (2.1.2) {#more-information-no-keyboard-trap}

* [Comprendere i criteri di successo 2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Come soddisfare i criteri di successo 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### Tempo sufficiente (2.2) {#enough-time}

[Linea guida 2.2 Tempo sufficiente: Dare agli utenti tempo sufficiente per leggere e utilizzare il contenuto.](https://www.w3.org/TR/WCAG/#enough-time)

In questo modo si garantisce agli utenti tempo sufficiente per leggere e agire.

### Tempo regolabile (2.2.1) {#timing-adjustable}

* Criterio di successo 2.2.1
* Livello A
* Tastiera: Dare agli utenti tempo sufficiente per leggere e utilizzare il contenuto.

#### Finalità - Tempo regolabile (2.2.1) {#purpose-timing-adjustable}

Lo scopo di questo criterio di successo è garantire che agli utenti disabili sia concesso il tempo necessario per interagire con i contenuti Web quando possibile. Le persone con disabilità come cecità, visibilità ridotta, difficoltà motorie e limitazioni cognitive potrebbero richiedere più tempo per leggere il contenuto o per eseguire funzioni come la compilazione di moduli online. Se le funzioni Web dipendono dal tempo, sarà difficile per alcuni utenti eseguire l&#39;azione richiesta prima che venga eseguito un limite di tempo. Ciò potrebbe rendere il servizio inaccessibile. La progettazione di funzioni che non dipendono dal tempo aiuterà le persone con disabilità a completare queste funzioni. Le opzioni per disabilitare i limiti di tempo, personalizzare i limiti di tempo o richiedere più tempo prima che venga eseguito un limite di tempo consentono agli utenti che richiedono più tempo del previsto di completare con successo le attività. Queste opzioni sono elencate nell&#39;ordine che sarà più utile per l&#39;utente. La disattivazione dei limiti di tempo è migliore rispetto alla personalizzazione dei limiti di tempo, il che è meglio che richiedere più tempo prima che si verifichi un limite di tempo.

#### Come soddisfare il criterio - Tempo regolabile (2.2.1) {#how-to-meet-timing-adjustable}

Seguire le linee guida in [Come soddisfare i criteri di successo 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### Ulteriori informazioni - Tempo regolabile (2.2.1) {#more-information-timing-adjustable}

* [Comprendere i criteri di successo 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [Come soddisfare i criteri di successo 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### Sospendi, Arresta, Nascondi (2.2.2)    {#pause-stop-hide}

* Criterio di successo 2.2.2
* Livello A
* Sospendi, Arresta, Nascondi: per le informazioni in movimento, lampeggianti, scorrevoli o con aggiornamento automatico, vale quanto segue:
   * Spostamento, lampeggiamento, scorrimento: per qualsiasi informazione in movimento, lampeggiante o scorrevole che (a) parta automaticamente, (b) duri più di cinque secondi, e (c) sia rappresentata in parallelo con altro contenuto, esiste un meccanismo che consente all’utente di mettere in pausa, interrompere o nascondere l’effetto, a meno che questo non sia parte di un’attività per la quale è essenziale;
   * Aggiornamento automatico: per qualsiasi informazione con aggiornamento automatico che (a) parta automaticamente e (b) sia rappresentata in parallelo con altro contenuto, esiste un meccanismo che consente all’utente di mettere in pausa, interrompere o nascondere il contenuto, oppure controllare la frequenza dell’aggiornamento, a meno che questo non sia parte di un’attività per la quale è essenziale;

Elementi da sottolineare:

1. Per i requisiti relativi a contenuti che sfarfallano o lampeggiano, consulta Non progettare contenuti con modalità che possano causare attacchi epilettici (2.3).
1. Dal momento che qualsiasi contenuto che non soddisfi questo criterio di successo può interferire con la capacità di un utente di utilizzare l’intera pagina, tutto il contenuto della pagina web (utilizzato per soddisfare altri criteri di successo o meno) deve rispondere a questo criterio. Consulta [Requisito di conformità 5: Non interferenza](https://www.w3.org/TR/WCAG20/#cc5).
1. I contenuti aggiornati periodicamente dal software o trasmessi in streaming all’agente dell’utente non sono tenuti a conservare o presentare le informazioni generate o ricevute tra l’inizio della pausa e la ripresa della presentazione, in quanto questo potrebbe non essere tecnicamente possibile e, in molte situazioni, potrebbe essere fuorviante.
1. Un’animazione che si verifica come parte di una fase di precaricamento, o situazione similare, può essere considerata essenziale se l’interazione non può verificarsi durante quella fase per tutti gli utenti e se la mancata indicazione dell’avanzamento potrebbe confondere gli utenti o far loro pensare che il contenuto sia bloccato o guasto.

#### Finalità - Sospendi, Arresta, Nascondi (2.2.2)  {#purpose-pause-stop-hide}

Per alcuni utenti i contenuti in movimento potrebbero essere fonte di distrazione e impedire di concentrarsi su altre parti della pagina. Inoltre, tali contenuti possono risultare di difficile lettura per chi abbia difficoltà a tenere il passo con il testo in movimento.

#### Come soddisfare il criterio - Sospendi, Arresta, Nascondi (2.2.2)  {#how-to-meet-pause-stop-hide}

In base alla natura del contenuto, è possibile applicare uno o più dei seguenti suggerimenti durante la creazione di pagine web che includono contenuti in movimento, con effetti di sfarfallio o lampeggiamento:

* Fornisci un mezzo per mettere in pausa lo scorrimento dei contenuti, in modo che gli utenti abbiano il tempo di leggerli. Ad esempio, un componente tipo telescrivente o un testo con aggiornamento automatico.
* Assicurati che il contenuto smetta di lampeggiare dopo cinque secondi.
* Utilizza tecnologie appropriate per visualizzare contenuto lampeggiante che possa essere disabilitato dal browser. Ad esempio, file Graphics Interchange Format (GIF) o Animated Portable Network Graphics (APNG).
* Includi un controllo di modulo nella pagina web per consentire all’utente di disattivare tutti i contenuti lampeggianti nella pagina.
* Se nessuno degli accorgimenti di cui sopra è praticabile, fornisci un collegamento a una pagina contenente tutti i contenuti, ma senza effetti di lampeggiamento.

#### Ulteriori informazioni - Sospendi, Arresta, Nascondi (2.2.2)  {#more-information-pause-stop-hide}

* [Comprendere il criterio di successo 2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [Come soddisfare il criterio di successo 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### Attacchi epilettici e reazioni fisiche (2.3) {#seizures-and-physcial-reactions}

[Linea guida 2.3 Attacchi epilettici: Non progettare contenuti in modo che possano causare attacchi epilettici o reazioni fisiche.](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### Tre lampeggiamenti o inferiore alla soglia (2.3.1)  {#three-flashes-or-below-threshold}

* Criterio di successo 2.3.1
* Livello A
* Tre lampeggiamenti o inferiore alla soglia: le pagine web non devono contenere alcun elemento che lampeggi per più di tre volte al secondo, oppure il lampeggiamento deve essere inferiore alle soglie di lampeggiamento generale e rosso.

>[!NOTE]
>
>Dal momento che qualsiasi contenuto che non soddisfi questo criterio di successo può interferire con la capacità di un utente di utilizzare l’intera pagina, tutto il contenuto della pagina web (utilizzato per soddisfare altri criteri di successo o meno) deve rispondere a questo criterio. Consulta [Requisito di conformità 5: Non interferenza](https://www.w3.org/TR/WCAG/#cc5).

#### Finalità - Tre lampeggiamenti o inferiore alla soglia (2.3.1) {#purpose-three-flashes-or-below-threshold}

In alcuni casi i contenuti lampeggianti possono causare crisi epilettiche dovute a fotosensibilità. Questo criterio di successo consente agli utenti a rischio di accedere e utilizzare tutti i contenuti, senza preoccuparsi di eventuali contenuti lampeggianti.

#### Come soddisfare il criterio - Tre lampeggiamenti o inferiore alla soglia (2.3.1)  {#how-to-meet-three-flashes-or-below-threshold}

È consigliabile adottare misure per assicurare che siano applicate le seguenti tecniche:

* Assicurati che i componenti non lampeggino per più di tre volte al secondo;
* Se la condizione di cui sopra non può essere soddisfatta, visualizza il contenuto lampeggiante all’interno di *una piccola area di sicurezza* in pixel sullo schermo. Quest’area è calcolata utilizzando una formula complessa, illustrata in [G176: Mantenere l’area lampeggiante sufficientemente piccola](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), di conseguenza questa tecnica dovrebbe essere applicata solo se il contenuto lampeggiante è *assolutamente* necessario.

#### Ulteriori informazioni - Tre lampeggiamenti o inferiore alla soglia (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Comprendere il criterio di successo 2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [Come soddisfare il criterio di successo 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### Navigabile (2.4) {#navigable}

[Linea guida 2.4 Navigabile: Fornire agli utenti i modi per navigare, trovare il contenuto e determinare dove si trovano.](https://www.w3.org/TR/WCAG/#navigable)

In questo modo si garantisce che il contenuto sia semplice e intuitivo per la navigazione degli utenti.

### Bypass Blocks (2.4.1) {#bypass-blocks}

* Criterio di successo 2.4.1
* Livello A
* Ignora blocchi: È disponibile un meccanismo per bypassare blocchi di contenuto ripetuti su più pagine Web.

#### Finalità - Bypass Blocks (2.4.1) {#purpose-bypass-blocks}

Lo scopo di questo criterio di successo è consentire agli utenti che navigano in sequenza attraverso il contenuto di accedere più direttamente al contenuto principale della pagina Web. Le pagine Web e le applicazioni presentano spesso contenuti che vengono visualizzati su altre pagine o schermate. Esempi di blocchi ripetuti di contenuto includono, tra l’altro, collegamenti di navigazione, elementi grafici di intestazione e cornici pubblicitarie. Ai fini della presente disposizione, le sezioni ripetute di piccole dimensioni, quali singole parole, frasi o singoli collegamenti, non sono considerate blocchi.

#### Come soddisfare il criterio - Bypass Blocks (2.4.1) {#how-to-meet-bypass-blocks}

Seguite le linee guida riportate in [Come soddisfare i criteri di successo 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### Ulteriori informazioni - Bypass Blocks (2.4.1) {#more-information-bypass-blocks}

* [Comprendere i criteri di successo 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [Come soddisfare i criteri di successo 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### Pagina con titolo (2.4.2)    {#page-titled}

* Criterio di successo 2.4.2
* Livello A
* Pagina con titolo: alle pagine web sono associati titoli che ne descrivono argomento o finalità.

#### Finalità - Pagina con titolo (2.4.2)  {#purpose-page-titled}

Questo criterio di successo consente a tutti gli utenti, indipendentemente da eventuali particolari disabilità, di identificare rapidamente il contenuto di una pagina web senza leggere la pagina completa. Questo è particolarmente utile quando più pagine web vengono aperte in altrettante schede del browser, in quanto il titolo della pagina è indicato nella scheda e quindi può essere individuato rapidamente.

#### Come soddisfare il criterio - Pagina con titolo (2.4.2)  {#how-to-meet-page-titled}

Quando si crea una nuova pagina HTML in AEM, è possibile specificare il titolo della pagina. Assicurati che il titolo descriva adeguatamente il contenuto della pagina, in modo che i visitatori possano verificare velocemente se è effettivamente pertinente alle loro esigenze.

È inoltre possibile modificare il titolo della pagina quando la si modifica, attraverso: **Informazioni pagina** > **Proprietà.**

#### Ulteriori informazioni - Pagina con titolo (2.4.2) {#more-information-page-titled}

* [Comprendere il criterio di successo 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [Come soddisfare il criterio di successo 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### Ordine di messa a fuoco (2.4.3) {#focus-order}

* Criterio di successo 2.4.3
* Livello A
* Ordine di messa a fuoco: Se è possibile navigare in sequenza in una pagina Web e le sequenze di navigazione influiscono sul significato o sul funzionamento, i componenti attivabili vengono attivati in un ordine che mantiene il significato e l&#39;operabilità.

#### Finalità - Ordine di messa a fuoco (2.4.3) {#purpose-focus-order}

L&#39;obiettivo di questo criterio di successo è garantire che quando gli utenti si spostano in sequenza nel contenuto, le informazioni vengano visualizzate in un ordine coerente con il significato del contenuto e che possano essere utilizzate dalla tastiera. Questo riduce la confusione consentendo agli utenti di creare un modello mentale coerente del contenuto. Possono essere presenti ordini diversi che riflettono relazioni logiche nel contenuto. Ad esempio, lo spostamento tra i componenti di una tabella in una riga alla volta o in una colonna alla volta riflette le relazioni logiche nel contenuto. Entrambi gli ordini possono soddisfare questo criterio di successo.

#### Come soddisfare il criterio - Ordine di messa a fuoco (2.4.3) {#how-to-meet-focus-order}

Seguite le linee guida riportate in [Come soddisfare i criteri di successo 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### Ulteriori informazioni - Ordine di messa a fuoco (2.4.3) {#more-information-focus-order}

* [Comprendere i criteri di successo 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [Come soddisfare i criteri di successo 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### Scopo del collegamento (nel contesto) (2.4.4)    {#link-purpose-in-context}

* Criterio di successo 2.4.4
* Livello A
* Scopo del collegamento (nel contesto): lo scopo di ogni collegamento può essere determinato esclusivamente dal testo di collegamento, oppure dal testo di collegamento insieme al suo contesto, determinato a livello di programmazione, a meno che lo scopo del collegamento possa risultare ambiguo per gli utenti in generale.

#### Finalità - Scopo del collegamento (nel contesto) (2.4.4)  {#purpose-link-purpose-in-context}

Per tutti gli utenti, indipendentemente da un’eventuale disabilità, indicare chiaramente la direzione di un collegamento tramite apposito testo è di vitale importanza. Questo aiuta gli utenti a decidere se vogliono effettivamente seguire un collegamento. Per i normovedenti, un testo di collegamento significativo è estremamente utile laddove in una pagina siano presenti più collegamenti (in particolare se la pagina è molto ricca di testo), in quanto fornisce un’indicazione più chiara delle funzionalità della pagina di destinazione. Gli utenti di tecnologie per l’accessibilità, in grado di generare un elenco di tutti i collegamenti su una sola pagina, dal canto loro potranno comprendere più facilmente il testo di collegamento fuori dal contesto.

#### Come soddisfare il criterio - Scopo del collegamento (nel contesto) (2.4.4)  {#how-to-meet-link-purpose-in-context}

Soprattutto, fai in modo che lo scopo di un collegamento sia chiaramente descritto all’interno del testo di collegamento.

* Esempio di utilizzo non corretto:
   * Testo: per i dettagli sui nostri corsi serali per l’autunno 2010, fai clic qui.
   * Motivo: non indica in modo chiaro e senza ambiguità la destinazione.
* Esempio di utilizzo corretto:
   * Testo: I nostri corsi serali per l’autunno 2010 - Dettagli.
   * Motivo: modificando leggermente il testo e la posizione dell’elemento di collegamento è possibile migliorare il testo di collegamento:

I collegamenti dovrebbero essere formulati in modo coerente tra le pagine, in particolare per le barre di navigazione. Ad esempio, se un collegamento a una pagina specifica è denominato **Pubblicazioni** in una pagina, utilizza lo stesso testo anche nelle altre pagine per garantire la coerenza.

Al momento in cui scriviamo, tuttavia, l’uso dei titoli pone alcuni problemi:

* Il testo contenuto all’interno dell’attributo title è generalmente disponibile solo a chi utilizza un mouse, sotto forma di pop-up con la descrizione comando, e non è accessibile utilizzando la tastiera.
* Le utilità di lettura dello schermo possono leggere gli attributi title, ma questa funzionalità potrebbe non essere abilitata per impostazione predefinita; è quindi possibile che gli utenti non siano a conoscenza dell’esistenza di un attributo title.
* È difficile modificare l’aspetto del testo del titolo, il che significa che leggerlo può risultare difficile o impossibile per alcuni utenti.

Così, mentre l’attributo title può essere utilizzato per fornire contesto aggiuntivo per un collegamento, è importante essere consapevoli dei suoi limiti e non utilizzarlo come alternativa a un testo collegamento adeguato.

Se il collegamento è costituito da un’immagine, accertati che il testo alternativo per l’immagine descriva la destinazione del collegamento. Ad esempio, se come collegamento alle pubblicazioni di un autore è impostata l’immagine di una libreria, il testo alternativo dovrebbe riportare **Pubblicazioni di John Smith** e non **Libreria**.

In alternativa, se nell’ancoraggio del collegamento è incluso testo che descrive lo scopo del collegamento in aggiunta all’elemento immagine (e, quindi, il testo viene visualizzato a fianco dell’immagine), utilizza un attributo alt vuoto per l’immagine:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>Il frammento di codice sopra ha esclusivamente scopo illustrativo; si consiglia di utilizzare il componente **Immagine**.

Mentre è opportuno fornire un testo di collegamento che identifichi lo scopo del collegamento senza necessità di ulteriore contesto, questo effettivamente non è sempre possibile. I collegamenti senza contesto possono essere utilizzati nei casi seguenti, esempi HTML dei quali sono reperibili in [Come soddisfare il criterio di successo 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* Qualora il testo di collegamento sia parte di un elenco di collegamenti strettamente correlati, e la voce di elenco che racchiude il collegamento fornisca contesto sufficiente.
* Laddove lo scopo di un collegamento possa essere chiaramente identificato dal testo di paragrafo *che lo precede* (non che lo segue).
* Se il collegamento è contenuto all’interno di una tabella di dati, e quindi la finalità può essere chiaramente identificata a partire dalle intestazioni associate.
* Se un elenco di collegamenti è contenuto all’interno di un insieme di intestazioni e l’intestazione fornisce il contesto adatto.
* Se un elenco di collegamenti è contenuto all’interno di un collegamento nidificato e la voce dell’elenco principale rispetto al collegamento nidificato fornisce il contesto adatto.

In alcuni casi, laddove in una pagina siano presenti diversi collegamenti (ciascuno dei quali fornisca la direzione di un collegamento con dettagli complessi ma necessari), può essere opportuno prevedere una versione alternativa della pagina web che mostri lo stesso contenuto, ma in cui il testo dei collegamenti non sia così dettagliato.

In alternativa, puoi utilizzare script in modo da fornire una quantità minima di testo nel collegamento, ma consentendo, all’attivazione di un controllo adeguato posizionato nella parte superiore della pagina, *l’espansione* del testo di collegamento per specificare maggiori dettagli. Un approccio simile consiste nell’utilizzare i CSS per *nascondere* il collegamento completo agli utenti normovedenti, ma mostrarlo agli utenti di utilità di lettura dello schermo. Questo esula dallo scopo di questo documento, ma ulteriori informazioni su come ottenere questo risultato sono reperibili nella sezione [Ulteriori informazioni - Scopo del collegamento (nel contesto) (2.4.4)](#more-information-link-purpose-in-context).

#### Ulteriori informazioni - Scopo del collegamento (nel contesto) (2.4.4) {#more-information-link-purpose-in-context}

* [Comprendere il criterio di successo 2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [Come soddisfare il criterio di successo 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### Varie modalità (2.4.5) {#multiple-ways}

* Criterio di successo 2.4.5
* Livello AA
* Vari modi: Sono disponibili più metodi per individuare una pagina Web all&#39;interno di un set di pagine Web, ad eccezione dei casi in cui la pagina Web è il risultato di un processo o un passaggio in esso.

#### Finalità - Vari modi (2.4.5) {#purpose-multiple-ways}

L’obiettivo di questo criterio di successo è di consentire agli utenti di individuare il contenuto nel modo più adatto alle loro esigenze. Gli utenti possono utilizzare una tecnica più semplice o comprensibile di un&#39;altra.

Anche i siti di piccole dimensioni dovrebbero fornire agli utenti alcuni strumenti di orientamento. Per un sito di tre o quattro pagine, con tutte le pagine collegate dalla home page, può essere sufficiente fornire semplicemente i collegamenti da e verso la home page, dove i collegamenti nella home page possono fungere anche da mappa del sito.

#### Come soddisfare il criterio - Vari modi (2.4.5) {#how-to-meet-multiple-ways}

Seguite le linee guida in [Come soddisfare i criteri di successo 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways).

#### Ulteriori informazioni - Vari modi (2.4.5) {#more-information-multiple-ways}

* [Comprendere i criteri di successo 2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [Come soddisfare i criteri di successo 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### Titoli ed etichette (2.4.6) {#headings-and-labels}

* Criterio di successo 2.4.6
* Livello AA
* Intestazioni ed etichette: Le intestazioni e le etichette descrivono argomento o finalità.

#### Finalità - Titoli ed etichette (2.4.6) {#purpose-headings-and-labels}

Lo scopo di questo criterio di successo è aiutare gli utenti a comprendere quali informazioni sono contenute nelle pagine Web e come tali informazioni sono organizzate. Quando le intestazioni sono chiare e descrittive, gli utenti possono trovare le informazioni che cercano più facilmente, e possono comprendere più facilmente i rapporti tra diverse parti del contenuto. Le etichette descrittive consentono agli utenti di identificare componenti specifici all&#39;interno del contenuto.

#### Come soddisfare il criterio - Titoli ed etichette (2.4.6) {#how-to-meet-headings-and-labels}

Seguite le linee guida in [Come soddisfare i criteri di successo 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels).

#### Ulteriori informazioni - Titoli ed etichette (2.4.6) {#more-information-headings-and-labels}

* [Comprendere i criteri di successo 2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [Come soddisfare i criteri di successo 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### Messa a fuoco visibile (2.4.7) {#focus-visible}

* Criterio di successo 2.4.7
* Livello AA
* Attiva visibile: Qualsiasi interfaccia utente utilizzabile da tastiera ha una modalità operativa in cui l&#39;indicatore di messa a fuoco è visibile.

#### Finalità - Visibile messa a fuoco (2.4.7) {#purpose-focus-visible}

Lo scopo di questo criterio di successo è aiutare una persona a sapere quale elemento è attivo.

Deve essere possibile per una persona sapere quale elemento tra più elementi è attivo. Se sullo schermo è presente un solo controllo utilizzabile da tastiera, il criterio di successo sarà soddisfatto perché il progetto visivo presenta un solo elemento utilizzabile dalla tastiera.

Se il criterio di successo dice &quot;modalità di funzionamento&quot;, questo è dovuto alle piattaforme che potrebbero non sempre mostrare un indicatore di messa a fuoco. Nella maggior parte dei casi esiste una sola modalità di funzionamento, pertanto questo criterio di successo si applica.

#### Come soddisfare il criterio - Visibile messa a fuoco (2.4.7) {#how-to-meet-focus-visible}

Seguite le linee guida in [Come soddisfare i criteri di successo 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### Ulteriori informazioni - Visibile messa a fuoco (2.4.7) {#more-information-focus-visible}

* [Comprendere i criteri di successo 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [Come soddisfare i criteri di successo 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## Principio 3: Comprensibilità  {#principle-understandable}

[Principio 3: Comprensibilità - Le informazioni e le operazioni dell’interfaccia devono essere comprensibili.](https://www.w3.org/TR/WCAG/#understandable)

### Rendere il testo leggibile e comprensibile (3.1)  {#make-text-content-readable-and-understandable}

[Linea guida 3.1 - Leggibilità: rendere il testo leggibile e comprensibile.](https://www.w3.org/TR/WCAG/#readable)

### Lingua della pagina (3.1.1)  {#language-of-page}

* Criterio di successo 3.1.1
* Livello A
* Lingua della pagina: la lingua predefinita di ogni pagina web può essere determinata a livello di programmazione.

#### Finalità - Lingua della pagina (3.1.1)  {#purpose-language-of-page}

Lo scopo di questo criterio è fare in modo che il testo e gli altri contenuti linguistici siano resi correttamente. Per gli utenti di utilità di lettura dello schermo, questo garantisce che la pronuncia sia corretta, mentre i browser visivi saranno più propensi a visualizzare certi set di caratteri correttamente.

#### Come soddisfare il criterio - Lingua della pagina (3.1.1)  {#how-to-meet-language-of-page}

Per soddisfare questo criterio di successo, la lingua predefinita di una pagina web può essere identificata mediante l’attributo `lang` all’interno dell’elemento `<html>` nella parte superiore della pagina. Esempio:

* Se una pagina è scritta in inglese britannico, l’elemento `<html>` dovrebbe riportare:
   `<html lang = “en-gb”>`

* Una pagina che deve essere resa in inglese americano dovrebbe invece adottare il seguente standard:
   `<html lang = “en-us”>`

In AEM, la lingua predefinita della pagina è impostata durante la creazione, ma può anche essere modificata quando apporti cambiamenti alla pagina. Questa funzione è accessibile dal percorso **barra laterale** > scheda **Pagina** > **Proprietà pagina** > scheda **Avanzate**.

#### Ulteriori informazioni - Lingua della pagina (3.1.1) {#more-information-language-of-page}

* [Comprendere il criterio di successo 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [Come soddisfare il criterio di successo 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* I codici sono basati su ISO 639-1. Un elenco più completo dei codici per ogni lingua è reperibile sul [sito W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Lingua delle parti (3.1.2)    {#language-of-parts}

* Criterio di successo 3.1.2
* Livello AA
* Lingua delle parti: la lingua di ogni passaggio o frase nel contenuto può essere determinata a livello di programmazione, fatta eccezione per nomi propri, termini tecnici, parole in lingue indeterminate e parole o frasi che sono diventate parte del gergo del testo immediatamente circostante.

#### Finalità - Lingua delle parti (3.1.2)  {#purpose-language-of-parts}

Lo scopo di questo criterio di successo è simile a quello del criterio [Lingua della pagina](#language-of-page), ma si applica a pagine web con contenuti multilingue all’interno di una singola pagina (ad esempio, a causa di citazioni o prestiti lessicali non comuni).

Le pagine che applicano questo criterio di successo consentono:

* Inserimento di caratteri accentati da parte di software di transizione Braille.
* Pronuncia corretta da parte dell’utilità di lettura dello schermo di quelle parole che non siano nella lingua predefinita.
* Traduzione corretta del contenuto da una lingua all’altra da parte di strumenti di traduzione come Google Translate.

#### Come soddisfare il criterio - Lingua delle parti (3.1.2)  {#how-to-meet-language-of-parts}

L’attributo `lang` può essere utilizzato per identificare le modifiche nella lingua del contenuto. Ad esempio, una citazione in tedesco (codice ISO 639-1 “de”) può essere mostrata come segue:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>Gli elementi blockquote non sono supportati in un’istanza standard. Un componente personalizzato può essere sviluppato per supportare la funzione.

Analogamente, il browser può rappresentare correttamente un prestito lessicale non comune o una frase se l’elemento `span` viene utilizzato come segue:

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>Non è necessario seguire questo criterio di successo per nomi o città in lingue diverse, o quando si utilizzano prestiti lessicali o frasi diventati comuni nella lingua predefinita (come *schadenfreude* in inglese).

Per aggiungere l’elemento span con una lingua appropriata, è possibile modificare manualmente il codice HTML nella modalità di modifica sorgente dell’editor Rich Text, affinché venga letto come sopra indicato. In alternativa, l’attributo `lang` può essere incluso nell’editor Rich Text da un amministratore di sistema (consulta Aggiunta di supporto per elementi e attributi HTML aggiuntivi).
<!--
To add the span element, with an appropriate language, you can manually edit your HTML markup in the source edit mode of the RTE so that it reads as above. Alternatively the `lang` attribute can be included in the RTE by a system administrator (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).
-->

#### Ulteriori informazioni - Lingua delle parti (3.1.2) {#more-information-language-of-parts}

* [Comprendere il criterio di successo 3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [Come soddisfare il criterio di successo 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### Prevedibile (3.2) {#predictable}

[Linea guida 3.2 Prevedibile: Le pagine Web vengono visualizzate e funzionano in modo prevedibile.](https://www.w3.org/TR/WCAG/#predictable)

In questo modo si garantisce che le pagine Web siano coerenti nell’aspetto e nel funzionamento.

### Attiva (3.2.1) {#on-focus}

* Criterio di successo 3.2.1
* Livello A
* Attiva: Quando un componente dell’interfaccia utente viene attivato, non viene attivato alcun cambiamento di contesto.

#### Finalità - Attiva (3.2.1) {#purpose-on-focus}

L’obiettivo di questo criterio di successo è garantire che le funzionalità siano prevedibili man mano che i visitatori si spostano all’interno di un documento. Qualsiasi componente in grado di attivare un evento quando riceve lo stato attivo non deve modificare il contesto. Esempi di modifica del contesto in cui un componente riceve lo stato attivo includono, tra l’altro:

* i moduli inviati automaticamente quando un componente viene messo a fuoco;
* nuove finestre avviate quando un componente riceve lo stato attivo;
* lo stato attivo è cambiato in un altro componente quando il componente viene messo a fuoco;

Lo stato attivo può essere spostato su un controllo tramite la tastiera (ad esempio, il tasto di tabulazione su un controllo) o il mouse (ad esempio, il clic su un campo di testo). Lo spostamento del mouse su un controllo non determina lo spostamento dello stato attivo, a meno che questo comportamento non venga implementato mediante script. Per alcuni tipi di controlli, fare clic su un controllo può anche attivare il controllo (ad es. pulsante), che a sua volta può avviare una modifica nel contesto.

#### Come soddisfare il criterio - Attiva (3.2.1) {#how-to-meet-on-focus}

Seguite le linee guida in [Come soddisfare i criteri di successo 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus).

#### Ulteriori informazioni - Attiva (3.2.1) {#more-information-on-focus}

* [Comprendere i criteri di successo 3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [Come soddisfare i criteri di successo 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### On Input (3.2.2) {#on-input}

* Criterio di successo 3.2.2
* Livello A
* In ingresso: La modifica dell’impostazione di un componente dell’interfaccia utente non causa automaticamente un cambiamento di contesto, a meno che l’utente non sia stato informato del comportamento prima di usare il componente.

#### Finalità - On Input (3.2.2) {#purpose-on-input}

L&#39;obiettivo di questo criterio di successo è garantire che l&#39;immissione dei dati o la selezione di un controllo modulo producano effetti prevedibili. La modifica dell&#39;impostazione di un componente dell&#39;interfaccia utente comporta la modifica di alcuni aspetti del controllo che persisteranno quando l&#39;utente non interagisce più con esso. Selezionando una casella di controllo, immettendo del testo in un campo di testo o modificando l&#39;opzione selezionata in un controllo elenco si modifica l&#39;impostazione, ma non attivando un collegamento o un pulsante. Le modifiche nel contesto possono confondere gli utenti che non percepiscono facilmente il cambiamento o che sono facilmente distratti dai cambiamenti. Le modifiche del contesto sono appropriate solo quando è chiaro che tale modifica verrà eseguita in risposta all&#39;azione dell&#39;utente.

#### Come soddisfare il criterio - On Input (3.2.2) {#how-to-meet-on-input}

Seguite le linee guida in [Come soddisfare i criteri di successo 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input).

#### Ulteriori informazioni - In ingresso (3.2.2) {#more-information-on-input}

* [Comprendere i criteri di successo 3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [Come soddisfare i criteri di successo 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### Navigazione coerente (3.2.3) {#consistent-navigation}

* Criterio di successo 3.2.3
* Livello AA
* Navigazione coerente: I meccanismi di navigazione ripetuti su più pagine Web all&#39;interno di un set di pagine Web vengono eseguiti nello stesso ordine relativo ogni volta che vengono ripetuti, a meno che l&#39;utente non avvii una modifica.

#### Finalità - Navigazione coerente (3.2.3) {#purpose-consistent-navigation}

L’obiettivo di questo criterio di successo è incoraggiare l’uso di presentazioni e layout coerenti per gli utenti che interagiscono con contenuti ripetuti all’interno di una serie di pagine Web e che devono individuare informazioni o funzionalità specifiche più volte. Gli individui con problemi di vista che utilizzano l&#39;ingrandimento dello schermo per visualizzare una piccola parte dello schermo alla volta spesso utilizzano riferimenti visivi e bordi delle pagine per individuare rapidamente contenuti ripetuti. Presentare contenuti ripetuti nello stesso ordine è importante anche per gli utenti visivi che utilizzano la memoria spaziale o segnali visivi all&#39;interno della progettazione per individuare contenuti ripetuti.

È importante notare che l&#39;uso della frase &quot;stesso ordine&quot; in questa sezione non implica l&#39;impossibilità di utilizzare i menu di navigazione secondaria o l&#39;impossibilità di utilizzare i blocchi di navigazione secondaria o la struttura della pagina. Questo criterio di successo è invece destinato ad aiutare gli utenti che interagiscono con contenuti ripetuti su più pagine Web a prevedere la posizione del contenuto che stanno cercando e a trovarlo più rapidamente quando lo incontrano di nuovo.

Gli utenti possono avviare una modifica nell’ordine utilizzando agenti utente adattivi o impostando le preferenze in modo che le informazioni vengano presentate nel modo più utile per loro.

#### Come soddisfare il criterio - Navigazione coerente (3.2.3) {#how-to-meet-consistent-navigation}

Seguite le linee guida in [Come soddisfare i criteri di successo 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation).

#### Ulteriori informazioni - Navigazione coerente (3.2.3) {#more-information-consistent-navigation}

* [Comprendere i criteri di successo 3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [Come soddisfare i criteri di successo 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### Identificazione coerente (3.2.4) {#consistent-identification}

* Criterio di successo 3.2.4
* Livello A
* Identificazione coerente: I componenti con la stessa funzionalità all&#39;interno di un set di pagine Web vengono identificati in modo coerente.

#### Finalità - Identificazione coerente (3.2.4) {#purpose-consistent-identification}

L&#39;obiettivo di questo criterio di successo è garantire un&#39;identificazione coerente dei componenti funzionali che vengono visualizzati ripetutamente all&#39;interno di un set di pagine Web. Una strategia che gli utenti che utilizzano gli assistenti vocali utilizzano quando gestiscono un sito Web consiste nel fare molta affidamento sulla loro familiarità con le funzioni che possono essere visualizzate su diverse pagine Web. Se funzioni identiche hanno etichette diverse (o, più in generale, un nome accessibile diverso) su pagine Web diverse, il sito sarà molto più difficile da usare. Può anche confondere e aumentare il carico cognitivo per le persone con limitazioni cognitive. Di conseguenza, un&#39;etichettatura coerente sarà di aiuto.

Questa coerenza si estende alle alternative testuali. Se le icone o altri elementi non testuali hanno la stessa funzionalità, anche le alternative testuali devono essere coerenti.

Se in una pagina Web sono presenti due componenti che hanno entrambe le stesse funzionalità di un componente in un’altra pagina di un set di pagine Web, tutti e tre devono essere coerenti. Pertanto, i due elementi sulla stessa pagina saranno coerenti.

Anche se è consigliabile e si consiglia sempre di essere coerenti all&#39;interno di una singola pagina Web, 3.2.4 risolve solo la coerenza all&#39;interno di un set di pagine Web in cui un elemento viene ripetuto su più pagine del set.

#### Come soddisfare il criterio - Identificazione coerente (3.2.4) {#how-to-meet-consistent-identification}

Seguite le linee guida in [Come soddisfare i criteri di successo 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification).

#### Ulteriori informazioni - Identificazione coerente (3.2.4) {#more-information-consistent-identification}

* [Comprendere i criteri di successo 3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [Come soddisfare i criteri di successo 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### Assistenza in ingresso (3.3) {#input-assistance}

[Linea guida 3.3 - Assistenza nell’inserimento: aiutare gli utenti a evitare e correggere gli errori.](https://www.w3.org/TR/WCAG/#input-assistance)

### Identificazione errore (3.3.1) {#error-identification}

* Criterio di successo 3.3.1
* Livello A
* Identificazione errore: Se viene rilevato automaticamente un errore di input, l&#39;elemento in errore viene identificato e l&#39;errore viene descritto all&#39;utente nel testo.

#### Finalità - Identificazione degli errori (3.3.1) {#purpose-error-identification}

L&#39;intento di questo criterio di successo è garantire che gli utenti siano consapevoli che si è verificato un errore e possano determinare cosa sia sbagliato. Il messaggio di errore deve essere il più specifico possibile. In caso di invio non riuscito del modulo, la visualizzazione del modulo e l&#39;indicazione dei campi in errore non sono sufficienti per consentire ad alcuni utenti di rilevare che si è verificato un errore. Gli utenti di utilità di lettura dello schermo, ad esempio, non saranno a conoscenza dell&#39;esistenza di un errore finché non incontreranno uno degli indicatori. È possibile che abbandonino completamente il modulo prima di incontrare l&#39;indicatore di errore, ritenendo che la pagina semplicemente non funzioni. Per definizione in WCAG 2.0, un &quot;errore di input&quot; è costituito dalle informazioni fornite dall&#39;utente che non sono accettate. Ciò include:

le informazioni richieste dalla pagina Web ma omesse dall&#39;utente, o quelle fornite dall&#39;utente ma che non rientrano nel formato dati richiesto o nei valori consentiti.
Ad esempio:

* l&#39;utente non inserisce l&#39;abbreviazione corretta in stato, provincia, regione, ecc. field;
* l&#39;utente immette un&#39;abbreviazione di stato non valida;
* l&#39;utente immette un codice postale o postale inesistente;
* l&#39;utente immette una data di nascita 2 anni in futuro;
* l&#39;utente immette caratteri alfabetici o parentesi nel campo relativo al numero di telefono che accetta solo numeri;
* l&#39;utente inserisce un&#39;offerta inferiore all&#39;offerta precedente o all&#39;incremento dell&#39;offerta minima.

#### Come soddisfare il criterio - Identificazione degli errori (3.3.1) {#how-to-meet-error-identification}

Seguite le linee guida in [Come soddisfare i criteri di successo 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification).

#### Ulteriori informazioni - Identificazione degli errori (3.3.1) {#more-information-error-identification}

* [Comprendere i criteri di successo 3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [Come soddisfare i criteri di successo 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### Etichette o istruzioni (3.3.2)  {#labels-or-instructions}

* Criterio di successo 3.3.2
* Livello A
* Etichette o istruzioni: etichette o istruzioni vengono fornite quando il contenuto richiede l’input dell’utente.

#### Finalità - Etichette o istruzioni (3.3.2)  {#purpose-labels-or-instructions}

Fornire istruzioni per facilitare la compilazione dei moduli è una parte fondamentale delle buone pratiche nell’ambito dell’usabilità dell’interfaccia. Questo è particolarmente utile per le persone con disabilità visive o cognitive, che altrimenti potrebbero avere difficoltà nel comprendere il layout di un modulo e il tipo di dati da fornire in un particolare campo.

In AEM un’etichetta predefinita viene aggiunta quando si aggiunge alla pagina un componente di modulo, come ad esempio un **Campo testo**. Questo titolo predefinito dipende dal tipo di componente; è possibile aggiungere un titolo personalizzato nella scheda **Titolo e testo** della finestra di dialogo di modifica per quel campo. È importante fare in modo che le etichette consentano agli utenti di comprendere i dati associati a ciascun componente del modulo.

Il campo **Titolo** deve essere utilizzato per gli elementi di campo in quanto fornisce un’etichetta che è disponibile per la tecnologia per l’accessibilità. Scrivere semplicemente un’etichetta di testo accanto al campo non è sufficiente.

Per alcuni componenti di modulo è anche possibile nascondere visivamente le etichette utilizzando la casella di selezione **Nascondi titolo**. Le etichette nascoste in questo modo sono ancora disponibili per le tecnologie per l’accessibilità, ma non vengono visualizzate sullo schermo. Questo può essere un buon approccio in alcune situazioni, ma solitamente è meglio includere un’etichetta visiva ove possibile, in quanto alcuni utenti potrebbero stare guardando una sezione molto piccola dello schermo (un campo alla volta) e necessitare delle etichette per identificare il campo in modo corretto.

#### Pulsanti immagine {#image-buttons}

Se utilizzi i pulsanti immagine (ad esempio, il componente **Pulsante immagine**), il campo **Titolo** nella scheda **Titolo e testo** della finestra di dialogo di modifica fornisce effettivamente il testo alt per l’immagine, anziché l’etichetta. Nell’esempio seguente, l’immagine con il testo `Submit` presenta il testo alt `Submit`, aggiunto dal campo **Titolo** della finestra di dialogo di modifica.

#### Gruppi di campi modulo {#groups-of-form-fields}

Dove è presente un gruppo di controlli correlati, come un **Gruppo pulsanti di scelta**, per il gruppo così come per i singoli controlli può essere necessario un titolo. Quando si aggiunge una serie di pulsanti di scelta in AEM, il campo **Titolo** fornisce questo titolo per il gruppo, mentre i singoli titoli sono specificati alla creazione dei pulsanti di scelta (**Elementi**).

Tuttavia, non esiste alcuna associazione programmatica tra il titolo del gruppo e i pulsanti di scelta. Per creare tale associazione, gli editor di modelli dovranno eseguire il wrapping del titolo tra i tag necessari `fieldset` e `legend`, semplicemente modificando il codice sorgente della pagina. In alternativa, un amministratore di sistema può aggiungere il supporto di questi elementi affinché vengano visualizzati nella finestra di dialogo **Proprietà campo** (consulta Aggiunta di supporto per elementi e attributi HTML aggiuntivi).

<!--
However, there is no programmatic association between the group title and the radio buttons themselves. Template editors would need to wrap the title in the necessary `fieldset` and `legend` tags to create this association and this can only be done by editing the page source code. Alternatively, a system administrator can add support for these elements so that they appear in the **Field Properties** dialog (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).
-->

#### Considerazioni aggiuntive relative ai moduli {#additional-considerations-for-forms}

Se i dati devono essere immessi in un formato specifico, specificalo chiaramente nel testo dell’etichetta. Ad esempio, se una data deve essere inserita nel formato `DD-MM-YYYY`, indicala chiaramente come parte dell’etichetta. Ciò significa che, quando chi usa un’utilità di lettura dello schermo arriva al campo, l’etichetta viene annunciata automaticamente, insieme alle informazioni aggiuntive relative al formato.

Se l’input di un campo modulo è obbligatorio, specificalo integrando la parola “obbligatorio” nell’etichetta. AEM aggiunge un asterisco quando un campo è obbligatorio, ma sarebbe ideale includere la parola `required` nell’etichetta stessa (nel campo **Titolo** della finestra di dialogo di modifica).

Il posizionamento delle etichette è importante anche in quanto aiuta a individuare campi appropriati. Questo è di particolare importanza quando l’utente si trova di fronte a un modulo complesso. Segui la convenzione qui di seguito:

* Caselle di selezione o pulsanti di scelta:
Le etichette sono posizionate immediatamente a destra del campo.
* Tutti gli altri componenti del modulo (ad esempio caselle di testo, caselle combinate):
Le etichette sono posizionate immediatamente sopra o a sinistra del campo.

Nei moduli semplici con funzionalità molto limitata, l’etichettatura appropriata di un pulsante `Submit` può fungere da etichetta per il campo adiacente (ad esempio `Search`). Ciò è utile in situazioni in cui potrebbe risultare difficile trovare spazio per il testo dell’etichetta.

#### Ulteriori informazioni - Etichette o istruzioni (3.3.2) {#more-information-labels-or-instructions}

* [Comprendere il criterio di successo 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [Come soddisfare il criterio di successo 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### Suggerimento errori (3.3.3) {#error-suggestion}

* Criterio di successo 3.3.3
* Livello AA
* Tastiera: Se viene rilevato automaticamente un errore di input e i suggerimenti per la correzione sono noti, i suggerimenti vengono forniti all&#39;utente, a meno che ciò non comprometta la sicurezza o lo scopo del contenuto.

#### Finalità - Suggerimento errori (3.3.3) {#purpose-error-suggestion}

L&#39;obiettivo di questo criterio di successo è garantire che gli utenti ricevano suggerimenti appropriati per la correzione di un errore di input, se possibile. La definizione WCAG 2.0 di &quot;errore di input&quot; indica che si tratta di &quot;informazioni fornite dall&#39;utente che non sono accettate&quot; dal sistema. Alcuni esempi di informazioni non accettate includono informazioni obbligatorie ma omesse dall&#39;utente e informazioni fornite dall&#39;utente ma che non rientrano nel formato dati richiesto o nei valori consentiti.

Il criterio di successo 3.3.1 prevede la notifica degli errori. Tuttavia, le persone con limitazioni cognitive possono trovare difficile capire come correggere gli errori. Le persone con disabilità visive potrebbero non essere in grado di capire esattamente come correggere l&#39;errore. In caso di invio non riuscito del modulo, gli utenti possono abbandonare il modulo perché potrebbero non essere sicuri di come correggere l&#39;errore, anche se sono consapevoli che si è verificato.

L&#39;autore del contenuto può fornire la descrizione dell&#39;errore, oppure l&#39;agente utente può fornire la descrizione dell&#39;errore in base a informazioni specifiche per la tecnologia e determinate a livello di programmazione.

#### Come soddisfare il criterio - Suggerimento errori (3.3.3) {#how-to-meet-error-suggestion}

Seguite le linee guida in [Come soddisfare i criteri di successo 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion).

#### Ulteriori informazioni - Suggerimento errori (3.3.3) {#more-information-error-suggestion}

* [Comprendere i criteri di successo 3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [Come soddisfare i criteri di successo 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### Prevenzione degli errori (legale, finanziario, dati) (3.3.4) {#error-prevention-legal-financial-data}

* Criterio di successo 3.3.4
* Livello AA
* Prevenzione degli errori (legale, finanziario, dati): Per le pagine Web che causano impegni legali o transazioni finanziarie per l&#39;utente, che modificano o eliminano dati controllabili dall&#39;utente nei sistemi di memorizzazione dei dati, o che inviano risposte di test agli utenti, almeno una delle seguenti affermazioni è vera:

   * ReversibleSubmission è reversibile.
   * CheckedData immesso dall&#39;utente viene controllato per verificare la presenza di errori di input e l&#39;utente ha l&#39;opportunità di correggerli.
   * È disponibile un meccanismo di revisione, conferma e correzione delle informazioni prima di finalizzare l’invio.

#### Finalità - Prevenzione degli errori (legale, finanziario, dati) (3.3.4) {#purpose-error-prevention-legal-financial-data}

L&#39;obiettivo di questo criterio di successo è aiutare gli utenti con disabilità ad evitare gravi conseguenze a seguito di un errore durante l&#39;esecuzione di un&#39;azione che non può essere annullata. Ad esempio, l&#39;acquisto di biglietti aerei non rimborsabili o l&#39;invio di un ordine di acquisto in un conto di intermediazione sono transazioni finanziarie con gravi conseguenze. Se un utente ha commesso un errore alla data del viaggio aereo, potrebbe finire con un biglietto per la giornata sbagliata che non può essere scambiato. Se l&#39;utente ha commesso un errore sul numero di azioni da acquistare, potrebbe finire per acquistare più azioni del previsto. Entrambi questi tipi di errori implicano transazioni che avvengono immediatamente e che non possono essere successivamente alterate, e possono essere molto costose. Allo stesso modo, potrebbe essere un errore irreversibile se gli utenti modificano o eliminano involontariamente i dati memorizzati in un database a cui successivamente hanno bisogno di accedere, ad esempio l&#39;intero profilo di viaggio in un sito Web dei servizi di viaggio. Quando si fa riferimento alla modifica o eliminazione di dati &#39;controllabili dall&#39;utente&#39;, l&#39;intento è quello di impedire la perdita di massa di dati come l&#39;eliminazione di un file o di un record. Non è intenzione richiedere una conferma per ogni comando Salva o la semplice creazione o modifica di documenti, record o altri dati.

Gli utenti con disabilità possono avere più probabilità di commettere errori. Le persone con disabilità di lettura possono trasporre numeri e lettere, e le persone con disabilità motorie possono colpire le chiavi per errore. La possibilità di annullare le azioni consente agli utenti di correggere un errore che potrebbe causare gravi conseguenze. La possibilità di rivedere e correggere le informazioni offre all&#39;utente l&#39;opportunità di rilevare un errore prima di intraprendere un&#39;azione che ha gravi conseguenze.

I dati controllabili dall’utente sono dati visualizzabili dall’utente che l’utente può modificare e/o eliminare mediante un’azione intenzionale. Esempi di come l&#39;utente che controlla tali dati sono l&#39;aggiornamento del numero di telefono e dell&#39;indirizzo del conto dell&#39;utente, o l&#39;eliminazione di un record di fatture passate da un sito Web. Non fa riferimento ad argomenti quali i log di internet e i dati di monitoraggio dei motori di ricerca che l&#39;utente non può visualizzare o con cui interagire direttamente.

#### Come soddisfare il criterio - Prevenzione degli errori (legale, finanziario, dati) (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

Seguite le linee guida in [Come soddisfare i criteri di successo 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### Ulteriori informazioni - Prevenzione degli errori (legale, finanziario, dati) (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [Comprendere i criteri di successo 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [Come soddisfare i criteri di successo 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## Principio 4: Robusto {#principle-robust}

[Principio 4: Robusto: i contenuti devono essere sufficientemente solidi da poter essere interpretati da un&#39;ampia gamma di agenti utente, comprese tecnologie di assistenza.](https://www.w3.org/TR/WCAG/#robust)

### Compatible (4.1) {#compatible}

[Linea guida 4.1 Compatibile: Massimizza la compatibilità con gli agenti utente attuali e futuri, comprese le tecnologie di assistenza.](https://www.w3.org/TR/WCAG/#compatible)

Massimizza la compatibilità con gli agenti utente attuali e futuri, comprese le tecnologie di assistenza.

### Analisi (4.1.1) {#parsing}

* Criterio di successo 4.1.1
* Livello A
* Analisi: Nel contenuto implementato utilizzando i linguaggi di marcatura, gli elementi dispongono di tag iniziali e finali completi, gli elementi sono nidificati in base alle proprie specifiche, gli elementi non contengono attributi duplicati ed eventuali ID sono univoci, a meno che le specifiche consentano tali funzioni.

#### Finalità - Analisi (4.1.1) {#purpose-parsing}

Lo scopo di questo criterio di successo è garantire che gli agenti utente, comprese le tecnologie di assistenza, possano interpretare e analizzare accuratamente il contenuto. Se il contenuto non può essere analizzato in una struttura di dati, diversi agenti utente potrebbero presentarlo in modo diverso o non essere in grado di analizzarlo completamente. Alcuni agenti dell&#39;utente utilizzano &quot;tecniche di riparazione&quot; per eseguire il rendering di contenuto scarsamente codificato.

Poiché le tecniche di riparazione variano tra gli agenti utente, gli autori non possono presumere che il contenuto verrà analizzato accuratamente in una struttura di dati o che verrà rappresentato correttamente da agenti utente specializzati, comprese le tecnologie di assistenza, a meno che il contenuto non venga creato in base alle regole definite nella grammatica formale per tale tecnologia. Nei linguaggi di marcatura, gli errori nella sintassi di elementi e attributi e la mancata fornitura dei tag start/end nidificati in modo corretto generano errori che impediscono agli agenti utente di analizzare il contenuto in modo affidabile. Pertanto, il criterio di successo richiede che il contenuto possa essere analizzato utilizzando solo le regole della grammatica formale.

#### Come soddisfare il criterio - Analisi (4.1.1) {#how-to-meet-parsing}

Seguire le linee guida riportate in [Come soddisfare i criteri di successo 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### Ulteriori informazioni - Analisi (4.1.1) {#more-information-parsing}

* [Comprendere i criteri di successo 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [Come soddisfare i criteri di successo 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### Nome, Ruolo, Valore (4.1.2) {#name-role-value}

* Criterio di successo 4.1.2
* Livello A
* Nome, Ruolo, Valore: Per tutti i componenti dell’interfaccia utente (compresi, tra l’altro: elementi del modulo, collegamenti e componenti generati da script), il nome e il ruolo possono essere determinati a livello di programmazione; stati, proprietà e valori che possono essere impostati dall&#39;utente a livello di programmazione; e la notifica delle modifiche apportate a questi elementi è disponibile per gli agenti utente, comprese le tecnologie di assistenza.

#### Finalità - Nome, Ruolo, Valore (4.1.2) {#purpose-ame-role-value}

Lo scopo di questo criterio di successo è garantire che Assistive Technologies (AT) possa raccogliere informazioni su, attivare (o impostare) e tenere aggiornato lo stato dei controlli dell&#39;interfaccia utente nel contenuto.

Quando si utilizzano controlli standard da tecnologie accessibili, questo processo è semplice. Se gli elementi dell&#39;interfaccia utente vengono utilizzati in base alle specifiche, le condizioni di questa disposizione saranno soddisfatte. (Cfr. esempi di criteri di successo 4.1.2 di seguito)

Tuttavia, se i controlli personalizzati vengono creati o se gli elementi dell&#39;interfaccia sono programmati (in codice o script) in modo da avere un ruolo e/o una funzione diversi rispetto al normale, è necessario adottare ulteriori misure per garantire che i controlli forniscano informazioni importanti alle tecnologie di assistenza e si permettano di essere controllati dalle tecnologie di assistenza.

Uno stato particolarmente importante di un controllo dell&#39;interfaccia utente è se è attivo o meno. Lo stato attivo di un controllo può essere determinato a livello di programmazione e le notifiche sul cambiamento di fuoco vengono inviate agli agenti utente e alla tecnologia di supporto. Altri esempi di stato del controllo dell&#39;interfaccia utente sono se è stata selezionata o meno una casella di controllo o un pulsante di scelta, oppure se un nodo di struttura o elenco comprimibile è espanso o compresso.

#### Come soddisfare il criterio - Nome, Ruolo, Valore (4.1.2) {#how-to-meet-ame-role-value}

Seguire le linee guida riportate in [Come soddisfare i criteri di successo 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### Ulteriori informazioni - Nome, Ruolo, Valore (4.1.2 {#more-information-ame-role-value}

* [Comprendere i criteri di successo 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [Come soddisfare i criteri di successo 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
