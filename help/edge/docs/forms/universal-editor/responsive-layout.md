---
title: Creare moduli adattivi con l’editor universale
description: Scopri come progettare, testare e ottimizzare i moduli dinamici per tutti i dispositivi utilizzando l’editor universale. Impara a testare i dispositivi e a usare modelli di layout e tecniche di ottimizzazione per dispositivi mobili per moduli AEM con Edge Delivery Services.
keywords: moduli dinamici, moduli per dispositivi mobili, test dei dispositivi, editor universale, layout adattivo, ottimizzazione dei moduli, progettazione per dispositivi mobili, progettazione reattiva, layout dei moduli, emulatore di dispositivi
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: ht
source-wordcount: '2443'
ht-degree: 100%

---


# Creazione di moduli dinamici con l’editor universale - Guida completa

Il panorama web moderno richiede moduli che funzionino perfettamente in uno spettro sempre più ampio di dispositivi e dimensioni dello schermo. Che sia su un grande monitor desktop o sul piccolo display dello smartphone, gli utenti si aspettano esperienze coerenti e intuitive a prescindere dal dispositivo utilizzato. La creazione di moduli dinamici non è più un optional: è un requisito fondamentale per offrire esperienze digitali professionali, accessibili e ottimizzate per la conversione.

L’editor universale fornisce strumenti e metodologie completi per lo sviluppo di moduli dinamici che si adattano in modo intelligente a schermi di varie dimensioni, a diversi metodi di input e al contesto dell&#39;utente. Questa guida illustra le basi tecniche, le strategie di implementazione e le tecniche di ottimizzazione necessarie per creare moduli che offrono prestazioni eccezionali su tutti i dispositivi, mantenendo al contempo l’usabilità, l’accessibilità e l’impatto visivo.

La creazione di moduli reattivi prevede due attività principali:

- **Test del comportamento responsive:** visualizza in anteprima e testa i moduli su schermi di varie dimensioni utilizzando emulatori di dispositivi.
- **Progettazione responsive:** seleziona e implementa modelli di layout che si adattano perfettamente a dispositivi diversi.

**In questa guida, impererai a:**

- Testare moduli su desktop, tablet e dispositivi mobili
- Selezionare i modelli di layout appropriati per il contenuto
- Applicare le best practice per la progettazione reattiva
- Risolvere i problemi comuni relativi ai moduli reattivi
- Ottimizzare i moduli per le prestazioni dei dispositivi mobili

<!--
## Why Responsive Forms Are Important

**User Experience Impact:**

- Over 60% of users access forms on mobile devices
- Poor mobile experiences result in a 67% higher abandonment rate
- Responsive forms can increase completion rates by up to 25%

**Business Benefits:**

- Higher form completion rates
- Improved user satisfaction
- Enhanced accessibility compliance
- Lower development and maintenance costs-->

>[!TIP]
>
> **Approccio mobile-first:** inizia con la progettazione per dispositivi mobili, poi ottimizza per schermi più grandi. Questo garantische che le funzionalità di base funzionino negli ambienti più limitati.

## Parte 1: test dei moduli su più dispositivi

Il test dei moduli su dispositivi diversi consente di identificare e risolvere i problemi reattivi prima che gli utenti li riscontrino. L’editor universale fornisce una modalità emulatore per simulare varie dimensioni e orientamenti dello schermo.

### Come testare i moduli

**Passaggio 1: aprire l’emulatore del dispositivo**

1. Apri il modulo nell’editor universale
2. Fai clic sull’![icona Emulatore](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} **Emulatore** nella barra degli strumenti.
3. Viene visualizzato il menu del selettore del dispositivo.

![Interfaccia di test reattivo dell’editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

**Passaggio 2: selezionare un dispositivo per il test**

- **Desktop** (larghezza 1200px+): visualizzazione predefinita di modifica
- **Tablet** (larghezza 768px-1199px): test su schermo medio
- **Dispositivi mobili** (larghezza 320px-767px): test su schermo piccolo
- **Personalizzato**: specifica dimensioni esatte per dispositivi specifici

**Passaggio 3: testare gli orientamenti del dispositivo**

Utilizza l’icona **Rotatore schermo** per testare entrambe le modalità:

- **Modalità verticale**: orientamento standard per dispositivi mobili
- **Modalità orizzontale**: visualizzazione con tablet o telefono ruotato

### Risultati dei test sui dispositivi

Ogni tipo di dispositivo rivela comportamenti reattivi univoci:

| **Tipo di dispositivo** | **Larghezza dello schermo** | **Cosa verificare** | **Problemi comuni** |
|-----------------|------------------|-------------------|-------------------|
| **Desktop** | 1200px+ | Layout completo, tutte le funzioni visibili | Spazi bianchi eccessivi, layout troppo ampi |
| **Tablet** | 768px-1199px | Sovrapposizione dei componenti, navigazione e usabilità | Problemi relativi a dimensioni inadeguate e destinazione touch |
| **Dispositivi mobili** | 320px-767px | Layout a colonna singola, navigazione con il pollice | Testo piccolo, pulsanti troppo ravvicinati |
| **Personalizzati** | Definito dall’utente | Requisiti specifici del dispositivo | Casi limite del punto di interruzione |

### Esempi visivi per dispositivo

**Vista desktop (1200px+):**
![Vista modulo desktop](/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png)
*Layout a larghezza intera con campi modulo affiancati.*

**Vista tablet (768px-1199px):**
![Vista modulo tablet](/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png)
*Layout a larghezza media con spaziatura dei componenti regolata.*

**Vista mobile (320px-767px):**
![Vista modulo per dispositivi mobili](/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png)
*Layout a colonna singola con componenti sovrapposti.*

**Vista dispositivo personalizzata:**
![Vista dispositivo personalizzata](/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png)
*Dimensioni specificate dall’utente per il test di destinazione.*

### Flusso di lavoro di test

**Per i nuovi moduli:**

1. **Genera nella vista desktop:** inizia con la funzionalità completa.
2. **Test su tablet:** verifica gli adattamenti per gli schermi medi.
3. **Convalida su dispositivi mobili:** garantisci l’usabilità su schermi piccoli.
4. **Correggi i problemi reattivi:** regola i layout in base alle esigenze.
5. **Ripeti il test su tutti i dispositivi:** conferma le correzioni in tutte le dimensioni.

**Per i moduli esistenti:**

1. **Controllo rapido per dispositivi mobili:** il modulo funziona sui telefoni?
2. **Identifica le aree problematiche:** rileva problemi di layout e usabilità.
3. **Test sistematici:** testa accuratamente le dimensioni di ogni dispositivo.
4. **Problemi del documento:** tieni traccia di ciò che deve essere risolto.
5. **Correzioni di implementazione:** affronta i problemi in modo metodico.

## Parte 2: selezione di modelli di layout reattivi

I modelli di layout determinano il modo in cui il contenuto del modulo si adatta alle diverse dimensioni dello schermo. Il modello giusto migliora sia l’esperienza utente che le prestazioni dei dispositivi mobili.

### Panoramica sui modelli di layout

| **Tipo di layout** | **Ideale per** | **Prestazione dei dispositivi mobili** | **Complessità** |
|---------------------|-------------------------------------------|------------------------|----------------|
| **Layout pannello** | Contenuto suddiviso in categorie, moduli in stile dashboard | Buona | Bassa |
| **Layout procedura guidata** | Processi a più passaggi, flussi di lavoro complessi | Eccellente | Media |
| **Layout pannello a soffietto** | Contenuto in stile Domande frequenti, sezioni facoltative | Eccellente | Bassa |

### Guida rapida alle decisioni

**Usa il layout pannello quando:**

- Il contenuto è diviso in categorie distinte
- Gli utenti hanno bisogno visualizzare più sezioni contemporaneamente
- Il contenuto è relativamente semplice

**Usa il layout procedura guidata quando:**

- Il modulo comprende più passaggi logici
- Vuoi ridurre il carico cognitivo
- Il pubblico principale è composto da utenti di dispositivi mobili

**Usa il layout pannello a soffietto quando:**

- Il modulo contiene contenuto facoltativo o secondario
- Il risparmio di spazio è importante
- Il contenuto può essere raggruppato logicamente

### Layout pannello

Il layout pannello organizza il contenuto correlato in sezioni visivamente distinte, consentendo agli utenti di visualizzare più sezioni contemporaneamente. Questo layout è ideale per i moduli con informazioni suddivise in categorie che traggono vantaggio dalla presentazione affiancata su schermi di grandi dimensioni.

![Esempio di layout pannello](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Comportamento dinamico**

- **Desktop (1200 px e oltre):** i pannelli vengono visualizzati affiancati o in una griglia per garantire la massima visibilità.
- **Tablet (768 px - 1199 px):** i pannelli vengono impilati verticalmente con una distanza adeguata per garantire la massima chiarezza.
- **Dispositivi mobili (320 px - 767 px):** i pannelli vengono presentati in un layout a singola colonna, con una netta separazione tra le sezioni per semplificarne l&#39;esplorazione.

**Modalità di implementazione**

1. Aggiungi il [componente Pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) al modulo.
2. Raggruppa i campi correlati all’interno di ogni pannello per mantenere un’organizzazione logica.
3. Assegna intestazioni chiare e descrittive a ogni sezione del pannello.
4. Assicurati che tra i pannelli sia presente spazio sufficiente a impedire disordine visivo.

**Best practice**

- Limita il numero di pannelli a 3 o 4 sul desktop per evitare di confondere gli utenti.
- Utilizza titoli concisi e descrittivi per ogni pannello, in modo da facilitare la comprensione dell&#39;utente.
- Organizza i campi all’interno dei pannelli in modo logico per ridurre al minimo il carico cognitivo.
- Testa l&#39;esplorazione del pannello su dispositivi touch per garantirne l&#39;usabilità su tutte le piattaforme.

**Casi d’uso comuni**

- **Domanda di lavoro:** sezioni per informazioni personali, istruzione, esperienze e referenze.
- **Registrazione prodotto:** pannelli per detagli di base, specifiche tecniche e informazioni sulla garanzia.
- **Moduli sondaggio:** raggruppamenti per dati demografici, preferenze, feedback e informazioni di contatto.

### Layout procedura guidata

Il layout procedura guidata conduce gli utenti attraverso un processo in più fasi, presentando una sezione alla volta. Questo layout è particolarmente efficace per i moduli complessi, in quanto riduce il carico cognitivo e aumenta i tassi di completamento suddividendo il processo in passaggi gestibili.

![Esempio di layout procedura guidata](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Comportamento dinamico**

- **Tutti i dispositivi:** mantiene l&#39;attenzione concentrata su un unico passaggio, ottimale per gli utenti di dispositivi mobili.
- **Contenuto in passaggi:** ogni passaggio si adatta in modo dinamico, impilando i campi o disponendoli affiancati, in base alle dimensioni dello schermo.
- **Esplorazione:** presenta pulsanti touch-screen con spazio adeguato per una facile interazione.
- **Indicatore di avanzamento:** le barre di avanzamento o gli indicatori di passaggio vengono adattati alle dimensioni dei dispositivi, fornendo un feedback chiaro sullo stato di completamento.

**Modalità di implementazione**

1. Inserire il [componente Procedura guidata](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) nel modulo.
2. Dividi il modulo in passaggi logici, idealmente tra 3 e 7, per mantenere ogni passaggio mirato e gestibile.
3. Aggiungi indicatori di progresso per aiutare gli utenti a capire a che punto sono nel processo.
4. Fornisci controlli di navigazione chiari, come i pulsanti Avanti, Indietro e Salva.

**Suggerimenti di ottimizzazione per dispositivi mobili**

- Utilizza campi touch di grandi dimensioni (altezza minima 44 px) per i controlli di navigazione, in modo da migliorarne l’accessibilità.
- Assicurarsi che gli indicatori dei passaggi siano visibili e leggibili su schermi di piccole dimensioni.
- Limita il numero di campi per ogni passaggio, in modo da ridurre al minimo le esigenze di scorrimento e favorire la concentrazione.
- Abilita la funzionalità di salvataggio automatico per evitare la perdita di dati se gli utenti abbandonano il modulo.

**Best practice**

- Progetta i passaggi in modo da seguire una progressione logica, in cui ogni passaggio si basa su quello precedente.
- Utilizza titoli chiari e descrittivi per ogni passaggio, in modo da definire le aspettative dell’utente.
- Convalida l&#39;input dell&#39;utente ad ogni passaggio per individuare tempestivamente eventuali errori e ridurre la frustrazione.
- Consenti agli utenti di tornare indietro per rivedere o modificare le informazioni precedenti senza perdere dati.

**Casi d’uso comuni**

- **Richieste di risarcimento assicurativo:** passaggi per i dettagli dell&#39;incidente, l&#39;invio delle prove, le informazioni personali e la revisione.
- **Configurazione di account:** fasi per l&#39;inserimento di informazioni di base, preferenze, impostazioni di protezione e conferma.
- **Processo di ordinazione:** passaggi per la selezione del prodotto, le informazioni di spedizione, i dettagli del pagamento e il riepilogo dell&#39;ordine.

### Layout pannello a soffietto

Il layout pannello a soffietto fa risparmiare spazio, consentendo di organizzare i contenuti in sezioni comprimibili ed è ideale per le informazioni facoltative o secondarie. Questo layout è particolarmente efficace per i moduli con contenuti che possono essere raggruppati logicamente e che non devono essere visualizzati contemporaneamente.

![Esempio di layout pannello a soffietto](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Comportamento dinamico**

- **Prestazioni su dispositivi mobili:** viene espansa solo la sezione pertinente, riducendo la necessità di scorrere e migliorando i tempi di caricamento.
- **Intestazioni ottimizzate per il tocco:** le intestazioni di sezione sono facili da toccare ed espandere, e supportano i movimenti naturali sui dispositivi mobili.
- **Animazioni fluide:** le sezioni di espansione e compressione forniscono un feedback visivo per le interazioni dell’utente.
- **Efficienza dello spazio:** le sezioni compresse riducono al minimo lo spazio verticale, semplificando la navigazione del modulo su tutti i dispositivi.

**Come implementarlo**

1. Aggiungi il [componente pannello a soffietto](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) al modulo.
2. Raggruppa contenuti facoltativi o secondari correlati all’interno di ogni sezione del pannello a soffietto.
3. Utilizza intestazioni chiare e descrittive per ogni sezione per aiutare gli utenti a comprendere quali informazioni vi sono contenute.
4. Imposta come predefinito lo stato “aperto” o “chiuso” per ogni sezione in base alla rilevanza e alle esigenze dell’utente.

**Vantaggi dei dispositivi mobili**

- Riduce lo scorrimento comprimendo le sezioni inutilizzate, consentendo agli utenti di concentrarsi su una sezione alla volta.
- L’interazione predisposta per il touch supporta i gesti di espansione/compressione naturali.
- Caricamento più rapido, in quanto è visibile solo il contenuto attivo.
- Maggiore attenzione: gli utenti visualizzano solo le informazioni necessarie in un dato momento.

**Best practice**

- Utilizza intestazioni di sezione chiare in modo che gli utenti sappiano cosa aspettarsi prima di espanderla.
- Raggruppa in modo logico i contenuti correlati all’interno di ogni sezione per facilitarne la comprensione.
- Imposta le sezioni importanti in modo che inizino espanse se è richiesto un intervento immediato.
- Fornisci brevi anteprime di sezioni o riepiloghi per aiutare gli utenti a decidere quali sezioni espandere.

**Casi d’uso comuni**

- **Configurazione prodotto:** sezioni per opzioni di base, impostazioni avanzate, accessori e supporto.
- **Domande frequenti sui moduli:** raggruppamenti per domande relative a account, fatturazione, tecniche e generali.
- **Impostazioni moduli:** sezioni per le opzioni privacy, notifiche, aspetto e avanzate.


## Parte 3: best practice per la progettazione reattiva

### Best practice per tipo di dispositivo

+++Ottimizzazione per dispositivi mobili (320 px-767 px)

**Layout e interazione:**

- Utilizza un layout a colonna singola per tutto il contenuto del modulo per massimizzare la leggibilità e la facilità d’uso.
- Assicurati che tutti i pulsanti e gli elementi interattivi abbiano un’altezza di almeno 44 px per un’interazione touch affidabile.
- Fornisci una navigazione semplice e chiara con pulsanti “Indietro” e “Avanti” visibili.
- Riduci al minimo la necessità di scorrere all’interno di ogni sezione suddividendo i moduli lunghi.
- Focalizza automaticamente il primo campo di input per richiedere la tastiera del dispositivo mobile.

**Linee guida per i campi:**

- I campi di testo devono coprire l’intera larghezza dello schermo con una spaziatura sufficiente per l’input touch.
- Utilizza elementi nativi a discesa e selezionali per un’usabilità ottimale del dispositivo mobile.
- Implementa selettori di date nativi per un’esperienza coerente con il dispositivo mobile.
- Applica alle aree di caricamento dei file etichette grandi e chiare per un facile accesso.

+++

+++Ottimizzazione per tablet (768 px-1199 px)

**Layout e usabilità:**

- Utilizza layout a due colonne per i campi correlati per sfruttare il maggior spazio disponibile sullo schermo.
- Verifica l’aspetto e l’usabilità del modulo sia in orientamento verticale che orizzontale.
- Progetta per l’input touch e con il mouse, garantendo un facile accesso a tutti i controlli.
- Aumenta le dimensioni dell’area del contenuto mantenendo una chiara gerarchia visiva e leggibilità.

+++

+++Ottimizzazione per desktop (1200 px+)

**Funzioni e layout avanzati:**

- Utilizza layout a più colonne per utilizzare in modo efficiente lo spazio orizzontale e ridurre lo scorrimento verticale.
- Fornisci scelte rapide da tastiera per azioni frequenti a supporto degli utenti esperti.
- Implementa stati di passaggio del mouse e feedback visivi per gli elementi interattivi.
- Offri la convalida avanzata con messaggi di errore chiari e dettagliati per i moduli complessi.

+++

## Configurare layout personalizzati con punti di interruzione query di file multimediali

Quando crei layout personalizzati per i componenti in Moduli adattivi utilizzando **Editor universale**, devi definire il comportamento dinamico utilizzando **Punti di interruzione per query di file multimediali CSS**. In questo modo il rendering dei moduli è corretto su dispositivi e dimensioni di schermo diversi.

**Punti di interruzione consigliati (In base ai componenti core di AEM)**

| **Tipo di dispositivo** | **Punto di interruzione consigliato** |
|-----------------|---------------------------|
| **Desktop** | `min-width: 1200px` |
| **Tablet** | `min-width: 768px and max-width: 1199px` |
| **Dispositivi mobili** | `max-width: 767px` |

**Punti chiave**

- Utilizza questi punti di interruzione per controllare come i componenti si ridimensionano, sovrappongono o nascondono su dispositivi diversi.
- Segui le linee guida di progettazione dinamica della tua organizzazione per un’esperienza utente coerente.
- Testa i layout su più dispositivi e orientamenti per garantire usabilità e accessibilità.

```css
/* Example: Stack form fields on smaller screens */
@media (max-width: 767px) {
  .custom-form-container {
    display: flex;
    flex-direction: column;
  }
}
```

>[!NOTE]
>
> L’editor universale non fornisce un’interfaccia utente per la definizione del comportamento dinamico. Tutte le personalizzazioni del layout devono essere gestite tramite CSS.



## Risoluzione di problemi

### Problemi di layout

+++Interruzioni del layout del modulo su dispositivi mobili

**Cause possibili:**

- Elementi a larghezza fissa che non si adattano a schermi più piccoli
- CSS per desktop che sostituisce gli stili dei dispositivi mobili
- Immagini o contenuti che fuoriescono dai loro contenitori

**Come risolvere il problema:**

- Assicurati che tutte le immagini e i contenitori utilizzino dimensioni relative o basate su percentuali.
- Inizia con un approccio CSS mobile-first e sovrapponi i miglioramenti per schermi più grandi.
- Testa i moduli utilizzando sia emulatori di dispositivi che dispositivi reali.
- Evita dimensioni fisse; utilizza layout flessibili.

+++

+++Destinazioni touch troppo piccole

**Cause possibili:**

- Pulsanti o collegamenti di dimensioni inferiori a 44px per 44px
- Elementi interattivi troppo vicini tra loro
- CSS personalizzato che riduce le dimensioni predefinite delle destinazioni touch

**Come risolvere il problema:**

- Assicurati che ogni elemento interattivo sia di almeno 44px per 44px.
- Aggiungi una spaziatura adeguata tra pulsanti, collegamenti e altri controlli.
- Testa con dispositivi touch reali, non solo con un mouse.
- Espandi le aree di destinazione touch in base alle esigenze di accessibilità.

+++

+++Problemi di riversamento del contenuto

**Cause possibili:**

- Testo lungo o etichette che non vanno a capo
- Contenitori con larghezze fisse
- Immagini che non sono scalabili in modo dinamico

**Come risolvere il problema:**

- Abilita la disposizione del testo per tutte le etichette e i contenuti.
- Utilizza immagini reattive scalabili con il contenitore.
- Progetta layout flessibili che si adattano alle diverse lunghezze dei contenuti.
- Esegui test con contenuti brevi e lunghi per garantire l’adattabilità.

+++

### Problemi relativi alle prestazioni

+++Caricamento lento su dispositivi mobili

**Cause possibili:**

- Immagini grandi e non ottimizzate
- JavaScript pesanti o eccessivi
- Troppi campi modulo caricati contemporaneamente

**Come risolvere il problema:**

- Ottimizza le immagini per dispositivi mobili e utilizza i formati di file appropriati.
- Differisci o carica lentamente i contenuti non critici.
- Riduci al minimo l’utilizzo di script e widget di terze parti.
- Semplifica i campi modulo per caricare solo ciò che è necessario.

+++

### Problemi di test e convalida

+++Differenze tra emulatore e dispositivo reale

**Cause possibili:**

- Differenze nei motori di rendering del browser
- Interazione touch non accuratamente simulata con il mouse
- Discrepanze nella velocità della rete

**Come risolvere il problema:**

- Esegui sempre il test su dispositivi reali oltre agli emulatori.
- Utilizza più browser e dispositivi per test completi.
- Simula varie velocità di rete per identificare i colli di bottiglia delle prestazioni.
- Raccogli feedback da utenti reali nel pubblico di destinazione.

+++

## Metriche di successo per moduli dinamici

+++Indicatori di prestazioni chiave

**Esperienza utente:**

- **Tasso di completamento del modulo:** esegui l&#39;85% o più sui dispositivi mobili.
- **Tempo di completamento:** gli utenti mobile devono completare i moduli entro il 20% dei tempi di completamento del desktop.
- **Frequenza errori:** mantieni gli errori di convalida al di sotto del 5%.
- **Punti di abbandono:** identifica e indirizza i passaggi in cui gli utenti si ritirano.

**Prestazioni tecniche:**

- **Tempo di caricamento pagina:** meno di 3 secondi con una connessione 3G.
- **Core Web Vitals:** soddisfare o superare le soglie consigliate di Google.
- **Accessibilità:** raggiungere la conformità WCAG 2.1 AA.
- **Compatibilità browser:** garantire oltre il 98% di funzionalità in tutti i principali browser.

+++

+++Elenco di controllo di prova

**Elenco di controllo pre-pubblicazione:**

- Esegui il test del modulo su dispositivi mobili effettivi (non solo emulatori).
- Assicurarti che tutte le destinazioni touch siano almeno 44px x 44px.
- Verifica la leggibilità del testo a tutte le dimensioni di schermo supportate.
- La convalida del modulo di conferma funziona in modo coerente su dispositivi e browser.
- Assicurati che il tempo di caricamento del dispositivo mobile sia inferiore a 3 secondi.
- Verifica che tutti gli elementi interattivi siano accessibili tramite la tastiera e le utilità di lettura.
- Testa l’invio del modulo su tutti i dispositivi supportati.


+++

## Passaggi successivi

**Azioni immediate:**

1. **Controlla i moduli correnti:** testa i moduli esistenti utilizzando l’emulatore di dispositivi.
2. **Identifica risultati positivi:** risolvi prima i problemi evidenti relativi all’usabilità dei dispositivi mobili.
3. **Assegna priorità ai moduli a traffico elevato:** concentrati sui moduli con l’impatto maggiore sugli utenti.
4. **Implementa un approccio mobile-first:** inizia con la progettazione dello schermo più piccolo.

**Ottimizzazione avanzata:**

- **Monitoraggio delle prestazioni:** configura l’analisi per tenere traccia delle metriche dei moduli.
- **Test A/B:** sperimenta layout e approcci diversi.
- **Raccolta feedback degli utenti:** raccogli informazioni dagli utenti reali.
- **Miglioramento continuo:** rivedi e ottimizza regolarmente i moduli.


