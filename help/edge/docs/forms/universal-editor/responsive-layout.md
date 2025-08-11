---
title: Creare un Forms reattivo con Universal Editor
description: Scopri come progettare, testare e ottimizzare i moduli reattivi per tutti i dispositivi utilizzando Universal Editor. Test del dispositivo principale, modelli di layout e tecniche di ottimizzazione mobile per AEM Forms con Edge Delivery Services.
keywords: moduli reattivi, moduli mobili, test dei dispositivi, editor universale, layout adattivo, ottimizzazione dei moduli, progettazione mobile, progettazione reattiva, layout dei moduli, emulatore di dispositivi
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '2382'
ht-degree: 1%

---


# Creare un Forms reattivo con Universal Editor

Il panorama web moderno richiede forme che funzionino perfettamente in uno spettro sempre più ampio di dispositivi e dimensioni dello schermo. Dai monitor desktop di grandi dimensioni agli schermi compatti degli smartphone, gli utenti si aspettano esperienze coerenti e intuitive indipendentemente dal dispositivo scelto. La creazione di moduli reattivi non è più facoltativa, ma è un requisito fondamentale per offrire esperienze digitali professionali, accessibili e ottimizzate per la conversione.

Universal Editor fornisce strumenti e metodologie completi per lo sviluppo di moduli reattivi che si adattano in modo intelligente a varie dimensioni dello schermo, metodi di input e contesti utente. Questa guida illustra le basi tecniche, le strategie di implementazione e le tecniche di ottimizzazione necessarie per creare moduli che offrono prestazioni eccezionali su tutti i dispositivi, mantenendo al contempo l’usabilità, l’accessibilità e l’impatto visivo.

La creazione di moduli reattivi prevede due attività principali:

- **Test reattivi:** Visualizza in anteprima e verifica i moduli su schermi di dimensioni diverse utilizzando emulatori di dispositivi.
- **Progettazione reattiva:** Seleziona e implementa modelli di layout che si adattano perfettamente a dispositivi diversi.

**In questa guida verrà illustrato come:**

- Test dei moduli su desktop, tablet e dispositivi mobili
- Seleziona i modelli di layout appropriati per il contenuto
- Applicare le best practice per la progettazione reattiva
- Risoluzione dei problemi comuni dei moduli reattivi
- Ottimizzare i moduli per le prestazioni mobili

## Importanza dei Forms reattivi

**Impatto sull&#39;esperienza utente:**

- Oltre il 60% degli utenti accede ai moduli su dispositivi mobili
- Le esperienze mobili scadenti causano un tasso di abbandono superiore del 67%
- I moduli reattivi possono aumentare le percentuali di completamento fino al 25%

**Vantaggi aziendali:**

- Percentuali più elevate di completamento dei moduli
- Maggiore soddisfazione degli utenti
- Migliore conformità in materia di accessibilità
- Riduzione dei costi di sviluppo e manutenzione

>[!TIP]
>
> **Primo approccio mobile:** inizia la progettazione per dispositivi mobili, quindi migliora per schermi più grandi. In questo modo le funzionalità di base funzionano nell’ambiente più vincolato.

## Parte 1: Test di Forms tra dispositivi

Il test dei moduli su dispositivi diversi consente di identificare e risolvere i problemi dinamici prima che gli utenti li incontrino. Universal Editor fornisce una modalità emulatore per simulare varie dimensioni e orientamenti dello schermo.

### Come testare il Forms

**Passaggio 1: aprire l&#39;emulatore di dispositivo**

1. Aprire il modulo nell&#39;Editor universale.
2. Fai clic sull&#39;icona ![Emulatore](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} **Emulatore** nella barra degli strumenti.
3. Viene visualizzato il menu del selettore del dispositivo.

![Interfaccia di test reattivo dell&#39;editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

**Passaggio 2: selezionare un dispositivo per il test**

- **Desktop** (larghezza 1200px+): visualizzazione di modifica predefinita
- **Tablet** (larghezza 768px-1199px): test dello schermo Medium
- **Dispositivi mobili** (larghezza 320px-767px): test con schermo piccolo
- **Personalizzato**: specifica dimensioni esatte per dispositivi specifici

**Passaggio 3: verifica orientamenti dispositivo**

Utilizza l&#39;icona **Rotatore schermo** per verificare entrambi:

- **Modalità verticale**: orientamento mobile standard
- **Modalità orizzontale**: tavoletta o telefono ruotati

### Risultati test dispositivo

Ogni tipo di dispositivo rivela comportamenti reattivi univoci:

| **Tipo di dispositivo** | **Larghezza schermo** | **Cosa verificare** | **Problemi comuni** |
|-----------------|------------------|-------------------|-------------------|
| **Desktop** | 1200px+ | Layout completo, tutte le funzioni visibili | Spazi bianchi eccessivi, layout eccessivamente ampi |
| **Tablet** | 768 px-1199 px | Stacking dei componenti, navigazione e usabilità | Problemi relativi a dimensioni e destinazione touch |
| **Dispositivi mobili** | 320 px-767 px | Layout a colonna singola, navigazione miniature | Testo piccolo, pulsanti con spaziatura stretta |
| **Personalizzati** | Definito dall&#39;utente | Requisiti specifici del dispositivo | Casi spigolo punto di interruzione |

### Esempi visivi per dispositivo

**Visualizzazione desktop (1200px+):**
![Visualizzazione modulo desktop](/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png)
*Layout a larghezza intera con campi modulo affiancati.*

**Visualizzazione Tablet (768px-1199px):**
![Visualizzazione modulo Tablet](/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png)
*Layout con larghezza Medium con spaziatura dei componenti regolata.*

**Visualizzazione mobile (320px-767px):**
![Visualizzazione modulo mobile](/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png)
*Layout a colonna singola con componenti sovrapposti.*

**Visualizzazione dispositivo personalizzata:**
![Visualizzazione dispositivo personalizzata](/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png)
*Dimensioni specificate dall&#39;utente per il test di destinazione.*

### Flusso di lavoro di prova

**Per Il Nuovo Forms:**

1. **Generazione nella visualizzazione desktop:** Iniziare con funzionalità complete.
2. **Test sul tablet:** Controllare gli adattamenti per gli schermi medi.
3. **Convalida sul dispositivo mobile:** Garantire l&#39;usabilità su schermi piccoli.
4. **Correzione dei problemi reattivi:** Regolare i layout in base alle esigenze.
5. **Ripeti il test di tutti i dispositivi:** Conferma le correzioni in tutte le dimensioni.

**Per Forms Esistente:**

1. **Controllo rapido per dispositivi mobili:** il modulo funziona sui telefoni?
2. **Identificare le aree problematiche:** Rilevare problemi di layout e usabilità.
3. **Test sistematici:** Verificare accuratamente le dimensioni di ogni dispositivo.
4. **Problemi del documento:** Tieni traccia di ciò che deve essere risolto.
5. **Correzioni di implementazione:** problemi relativi agli indirizzi in modo metodico.

## Parte 2: Selezione di modelli di layout reattivi

I modelli di layout determinano il modo in cui il contenuto del modulo si adatta alle diverse dimensioni dello schermo. Il modello giusto migliora sia l’esperienza utente che le prestazioni mobili.

### Panoramica del modello di layout

| **Tipo di layout** | **Ideale per** | **Prestazioni mobili** | **Complessità** |
|---------------------|-------------------------------------------|------------------------|----------------|
| **Layout pannello** | Contenuto classificato, moduli in stile dashboard | Buono | Bassa |
| **Layout procedura guidata** | Processi in più fasi, flussi di lavoro complessi | Eccellente | Media |
| **Layout pannello a soffietto** | Contenuto in stile FAQ, sezioni facoltative | Eccellente | Bassa |

### Guida rapida alle decisioni

**Usa layout pannello quando:**

- Il contenuto è diviso in categorie distinte
- Gli utenti devono visualizzare più sezioni contemporaneamente
- Il contenuto è relativamente semplice

**Usa layout procedura guidata quando:**

- Il modulo include più passaggi logici
- Vuoi ridurre il carico cognitivo
- Gli utenti di dispositivi mobili sono un pubblico principale

**Usa layout pannello a soffietto quando:**

- Il modulo contiene contenuto facoltativo o secondario
- La conservazione dello spazio è importante
- Il contenuto può essere raggruppato logicamente

### Layout pannello

Il layout del pannello organizza il contenuto correlato in sezioni visivamente distinte, consentendo agli utenti di visualizzare più sezioni contemporaneamente. Questo layout è ideale per i moduli con informazioni suddivise in categorie e che prevedono una presentazione affiancata su schermi più grandi.

![Esempio di layout pannello](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Comportamento reattivo**

- **Desktop (1200px e versioni successive):** i pannelli vengono visualizzati affiancati o in una griglia per ottenere la massima visibilità.
- **Tablet (768px-1199px):** i pannelli si sovrappongono verticalmente con la spaziatura appropriata per mantenere la chiarezza.
- **Mobile (320px-767px):** i pannelli sono presentati in un layout a colonna singola, con netta separazione tra le sezioni per una facile navigazione.

**Come implementare**

1. Aggiungi il [componente Pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) al modulo.
2. Raggruppa i campi correlati all’interno di ciascun pannello per mantenere un’organizzazione logica.
3. Assegna intestazioni chiare e descrittive a ciascuna sezione del pannello.
4. Assicurati che vi sia una spaziatura sufficiente tra i pannelli per evitare disagi visivi.

**Best practice**

- Limita il numero di pannelli a 3 o 4 sul desktop per evitare di sopraffare gli utenti.
- Utilizza titoli descrittivi e concisi per ciascun pannello, per aiutare l’utente a comprendere.
- Organizza i campi all’interno dei pannelli in modo logico per ridurre al minimo il carico cognitivo.
- Testa la navigazione del pannello sui dispositivi touch per assicurarne l’usabilità su tutte le piattaforme.

**Casi d&#39;uso comuni**

- **Domanda di lavoro:** sezioni per informazioni personali, istruzione, esperienza e riferimenti.
- **Registrazione prodotto:** pannelli per informazioni di base, specifiche tecniche e garanzia.
- **Forms sondaggio:** raggruppamenti per dati demografici, preferenze, feedback e informazioni di contatto.

### Layout procedura guidata

Il layout guidato guida gli utenti attraverso un processo con più passaggi, presentando una sezione alla volta. Questo layout è particolarmente efficace per le forme complesse, in quanto riduce il carico cognitivo e aumenta i tassi di completamento suddividendo il processo in passaggi gestibili.

![Esempio di layout guidato](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Comportamento reattivo**

- **Tutti i dispositivi:** mantiene lo stato attivo in un unico passaggio, il che è ottimale per gli utenti di dispositivi mobili.
- **Contenuto passaggio:** ogni passaggio si adatta in modo dinamico, impilando i campi o disponendoli affiancati in base alle dimensioni dello schermo.
- **Navigazione:** presenta pulsanti touch-screen con spazio adeguato per una facile interazione.
- **Indicatore di avanzamento:** Le barre di avanzamento o gli indicatori di passaggio vengono scalati in modo appropriato per i diversi dispositivi, fornendo un feedback chiaro sullo stato di completamento.

**Come implementare**

1. Inserire il [componente procedura guidata](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) nel modulo.
2. Dividi la forma in passaggi logici, idealmente tra 3 e 7, per mantenere ogni passaggio mirato e gestibile.
3. Aggiungi indicatori di progresso per aiutare gli utenti a comprendere la loro posizione nel processo.
4. Fornisce controlli di navigazione chiari, ad esempio i pulsanti Avanti, Indietro e Salva.

**Suggerimenti per l&#39;ottimizzazione mobile**

- Utilizza destinazioni touch di grandi dimensioni (altezza minima 44 px) per i controlli di navigazione per migliorare l’accessibilità.
- Assicurati che gli indicatori a gradino siano visibili e leggibili su schermi di piccole dimensioni.
- Limita il numero di campi per passaggio per ridurre al minimo lo scorrimento e migliorare lo stato attivo.
- Abilita la funzionalità di salvataggio automatico per evitare la perdita di dati se gli utenti lasciano il modulo.

**Best practice**

- Progetta i passaggi per seguire una progressione logica, con ogni passaggio che si basa sul precedente.
- Utilizza titoli chiari e descrittivi per ogni passaggio per definire le aspettative dell’utente.
- Convalida l’input dell’utente in ogni passaggio per rilevare gli errori in anticipo e ridurre la frustrazione.
- Consente agli utenti di tornare indietro per rivedere o modificare le informazioni precedenti senza perdere dati.

**Casi d&#39;uso comuni**

- **Indennizzi assicurativi:** passaggi per i dettagli sull&#39;incidente, l&#39;invio di prove, le informazioni personali e la revisione.
- **Configurazione account:** fasi per informazioni di base, preferenze, impostazioni di protezione e conferma.
- **Processo ordine:** passaggi per la selezione del prodotto, le informazioni di spedizione, i dettagli del pagamento e il riepilogo dell&#39;ordine.

### Layout pannello a soffietto

Il layout Pannello a soffietto consente di organizzare i contenuti in sezioni comprimibili, rendendoli ideali per le informazioni facoltative o secondarie. Questo layout è particolarmente efficace per i moduli con contenuto che può essere raggruppato logicamente e che non deve essere visualizzato contemporaneamente.

![Esempio di layout pannello a soffietto](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Comportamento reattivo**

- **Prestazioni mobili:** solo la sezione pertinente viene espansa, riducendo la necessità di scorrere e migliorando i tempi di caricamento.
- **Intestazioni ottimizzate per il tocco:** Le intestazioni di sezione sono facili da toccare ed espandere, e supportano i movimenti naturali sui dispositivi mobili.
- **Animazioni smussate:** Le sezioni di espansione e compressione forniscono un feedback visivo per le interazioni dell&#39;utente.
- **Efficienza dello spazio:** Le sezioni compresse riducono al minimo lo spazio verticale, semplificando la navigazione del modulo su tutti i dispositivi.

**Come implementare**

1. Aggiungi il [componente Pannello a soffietto](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) al modulo.
2. Raggruppa contenuti facoltativi o secondari correlati all’interno di ogni sezione del Pannello a soffietto.
3. Utilizza intestazioni chiare e descrittive per ogni sezione per aiutare gli utenti a comprendere quali informazioni sono contenute in.
4. Impostare gli stati di apertura o chiusura predefiniti appropriati per ogni sezione in base alla rilevanza e alle esigenze dell&#39;utente.

**Vantaggi per dispositivi mobili**

- Riduce lo scorrimento comprimendo le sezioni inutilizzate, consentendo agli utenti di concentrarsi su una sezione alla volta.
- L’interazione touch supporta i gesti di espansione/compressione naturali.
- Caricamento più rapido, in quanto è visibile solo il contenuto attivo.
- È stata migliorata la messa a fuoco, poiché gli utenti visualizzano solo le informazioni necessarie in un dato momento.

**Best practice**

- Utilizza intestazioni di sezione chiare in modo che gli utenti sappiano cosa aspettarsi prima di espandere una sezione.
- Raggruppa in modo logico i contenuti correlati all’interno di ogni sezione per facilitarne la comprensione.
- Impostare le sezioni importanti in modo che inizino espanse se è richiesto un intervento immediato.
- Fornisci brevi anteprime di sezioni o riepiloghi per aiutare gli utenti a decidere quali sezioni espandere.

**Casi d&#39;uso comuni**

- **Configurazione prodotto:** sezioni per le opzioni di base, le impostazioni avanzate, gli accessori e il supporto.
- **Domande frequenti su Forms:** raggruppamenti per domande relative a account, fatturazione, tecniche e generali.
- **Impostazioni Forms:** Sezioni per le opzioni Privacy, Notifiche, Aspetto e Avanzate.


## Parte 3: Best practice per la progettazione reattiva

### Best practice per tipo di dispositivo

+++Ottimizzazione mobile (320px-767px)

**Layout e interazione:**

- Utilizza un layout a colonna singola per tutto il contenuto del modulo per massimizzare la leggibilità e la facilità d’uso.
- Assicurati che tutti i pulsanti e gli elementi interattivi abbiano un&#39;altezza di almeno 44 px per un&#39;interazione touch affidabile.
- Navigazione semplice e chiara con pulsanti visibili sul retro e sul successivo.
- Riduci al minimo la necessità di scorrere all’interno di ogni sezione suddividendo le forme lunghe.
- Attiva automaticamente il primo campo di input per richiedere la tastiera mobile.

**Linee guida per i campi:**

- I campi di testo devono coprire l’intera larghezza dello schermo con una spaziatura sufficiente per l’input tocco.
- Utilizza elementi nativi a discesa/selezionati per un’usabilità mobile ottimale.
- Implementa selettori data nativi per un’esperienza mobile coerente.
- Aree di caricamento file grandi e chiaramente etichettate per un facile accesso.

+++

+++Ottimizzazione tablet (768px-1199px)

**Layout e usabilità:**

- Utilizza layout a due colonne per i campi correlati per sfruttare lo spazio disponibile sullo schermo.
- Verificate l&#39;aspetto e l&#39;usabilità del modulo sia in orientamento verticale che orizzontale.
- Progettazione per il tocco e l&#39;input del mouse, garantendo l&#39;accesso facile a tutti i controlli.
- Aumentare le dimensioni dell&#39;area del contenuto mantenendo una chiara gerarchia visiva e la leggibilità.

+++

+++Ottimizzazione desktop (1200 px+)

**Funzioni e layout avanzati:**

- Utilizza layout a più colonne per utilizzare in modo efficiente lo spazio orizzontale e ridurre lo scorrimento verticale.
- Fornire scelte rapide da tastiera per azioni frequenti a supporto degli utenti esperti.
- Implementa stati di passaggio del mouse e feedback visivo per gli elementi interattivi.
- Offri la convalida avanzata con messaggi di errore chiari e dettagliati per i moduli complessi.

+++

## Risoluzione di problemi

### Problemi di layout

+++Interruzioni layout modulo su dispositivi mobili

**Cause possibili:**

- Elementi a larghezza fissa che non si adattano a schermi più piccoli
- CSS per desktop che sostituisce gli stili dei dispositivi mobili
- Immagini o contenuti che traboccano dai loro contenitori

**Come correggere:**

- Assicurati che tutte le immagini e i contenitori utilizzino dimensioni relative o basate su percentuali.
- Inizia con un approccio CSS mobile-first e posiziona i miglioramenti per schermi più grandi.
- Testare i moduli utilizzando sia emulatori di dispositivi che dispositivi reali.
- Evitare quote fisse; utilizzare layout flessibili.

+++

+++Destinazioni Touch troppo piccole

**Cause possibili:**

- Pulsanti o collegamenti di dimensioni inferiori a 44 px per 44 px
- Elementi interattivi troppo vicini tra loro
- CSS personalizzato che riduce le dimensioni predefinite del target di contatto

**Come correggere:**

- Assicurati che ogni elemento interattivo sia di almeno 44 px per 44 px.
- Aggiungere una spaziatura adeguata tra pulsanti, collegamenti e altri controlli.
- Prova con dispositivi touch reali, non solo con un mouse.
- Espandi le aree di destinazione di contatto in base alle esigenze di accessibilità.

+++

+++Problemi di overflow del contenuto

**Cause possibili:**

- Testo lungo o etichette che non vanno a capo
- Contenitori con larghezze fisse
- Immagini che non sono scalabili in modo dinamico

**Come correggere:**

- Attiva la disposizione del testo per tutte le etichette e il contenuto.
- Utilizza immagini reattive scalabili con il contenitore.
- Progetta layout flessibili che si adattano a lunghezze di contenuto diverse.
- Esegui test con contenuti brevi e lunghi per garantire adattabilità.

+++

### Problemi relativi alle prestazioni

+++Caricamento lento su dispositivi mobili

**Cause possibili:**

- Immagini grandi e non ottimizzate
- JavaScript pesanti o eccessivi
- Troppi campi modulo caricati contemporaneamente

**Come correggere:**

- Ottimizza le immagini per dispositivi mobili e utilizza i formati di file appropriati.
- Differire o caricare lentamente contenuti non critici.
- Riduci al minimo l’utilizzo di script e widget di terze parti.
- Semplifica i campi modulo per caricare solo ciò che è necessario.

+++

### Problemi di test e convalida

+++Differenze tra emulatore e dispositivo reale

**Cause possibili:**

- Differenze nei motori di rendering del browser
- Interazione touch non accuratamente simulata con il mouse
- Discrepanze nella velocità della rete

**Come correggere:**

- Eseguire sempre il test su dispositivi reali oltre agli emulatori.
- Utilizza più browser e dispositivi per test completi.
- Simulare varie velocità di rete per identificare i colli di bottiglia delle prestazioni.
- Raccogli feedback da utenti reali nel pubblico di destinazione.

+++

## Metriche di successo per Forms reattivo

+++Indicatori prestazioni chiave

**Esperienza utente:**

- **Percentuale di completamento modulo:** Esegui l&#39;85% o superiore sui dispositivi mobili.
- **Tempo di completamento:** gli utenti mobili devono completare i moduli entro il 20% dei tempi di completamento del desktop.
- **Frequenza errori:** Mantenere gli errori di convalida al di sotto del 5%.
- **Punti di abbandono:** Identificare e indirizzare i passaggi in cui gli utenti si ritirano.

**Prestazioni tecniche:**

- **Tempo di caricamento pagina:** Meno di 3 secondi in una connessione 3G.
- **Core Web Vitals:** soddisfa o supera le soglie consigliate di Google.
- **Accessibilità:** Raggiungere la conformità WCAG 2.1 AA.
- **Compatibilità browser:** Garantire il 98%+ di funzionalità in tutti i principali browser.

+++

+++Elenco di controllo di prova

**Elenco di controllo pre-pubblicazione:**

- Verifica il modulo su dispositivi mobili effettivi (non solo emulatori).
- Assicurati che tutte le destinazioni di contatto siano almeno 44 px × 44 px.
- Verifica la leggibilità del testo a tutte le dimensioni di schermo supportate.
- La convalida del modulo di conferma funziona in modo coerente tra dispositivi e browser.
- Assicurati che il tempo di caricamento mobile sia inferiore a 3 secondi.
- Verifica che tutti gli elementi interattivi siano accessibili tramite la tastiera e gli assistenti vocali.
- Verifica l’invio del modulo su tutti i dispositivi supportati.


+++

## Passaggi successivi

**Azioni immediate:**

1. **Controlla i moduli correnti:** verifica i moduli esistenti utilizzando l&#39;emulatore di dispositivi.
2. **Identifica risultati positivi:** Risolvi prima i problemi di usabilità ovvi relativi ai dispositivi mobili.
3. **Assegna priorità ai moduli a traffico elevato:** Concentrati sui moduli con l&#39;impatto maggiore sugli utenti.
4. **Implementa un approccio mobile-first:** Inizia con la progettazione dello schermo più piccola.

**Ottimizzazione avanzata:**

- **Monitoraggio delle prestazioni:** Configura analisi per tenere traccia delle metriche dei moduli.
- **Test A/B:** esperimento con layout e approcci diversi.
- **Raccolta feedback utenti:** raccogliere informazioni da utenti reali.
- **Miglioramento continuo:** Esamina e ottimizza regolarmente i moduli.


