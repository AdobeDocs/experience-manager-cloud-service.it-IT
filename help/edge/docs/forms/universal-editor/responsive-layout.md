---
title: Creare un Forms reattivo con Universal Editor
description: Scopri come progettare, testare e ottimizzare i moduli reattivi per tutti i dispositivi utilizzando Universal Editor. Test del dispositivo principale, modelli di layout e tecniche di ottimizzazione mobile per AEM Forms con Edge Delivery Services.
keywords: moduli reattivi, moduli mobili, test dei dispositivi, editor universale, layout adattivo, ottimizzazione dei moduli, progettazione mobile, progettazione reattiva, layout dei moduli, emulatore di dispositivi
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 1%

---


# Creare un Forms reattivo con Universal Editor

Gli utenti accedono ai moduli su una vasta gamma di dispositivi, tra cui desktop, tablet e smartphone. La progettazione di moduli reattivi garantisce un’esperienza ottimale per tutti gli utenti, indipendentemente dal dispositivo. Questa guida spiega come progettare, testare e ottimizzare i moduli per qualsiasi dimensione di schermo utilizzando Universal Editor.

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

**Scopo:** organizza i contenuti correlati in sezioni visivamente distinte che possono essere visualizzate contemporaneamente.

![Esempio di layout pannello](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Comportamento reattivo:**

- **Desktop (1200px+):** pannelli affiancati o in griglia
- **Tablet (768px-1199px):** i pannelli si sovrappongono verticalmente con la spaziatura
- **Mobile (320px-767px):** layout a colonna singola con interruzioni di sezione cancellate

**Passaggi di implementazione:**

1. Utilizza il [componente pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).
2. Raggruppa i campi correlati in ciascun pannello.
3. Aggiungi intestazioni chiare per ogni sezione.
4. Assicurati che vi sia una spaziatura adeguata tra i pannelli.

**Best practice:**

- Limita a 3-4 pannelli sul desktop per evitare di sopraffare gli utenti.
- Utilizza titoli descrittivi per ciascun pannello.
- Raggruppa i campi correlati in modo logico per ridurre il carico cognitivo.
- Test della navigazione del pannello sui dispositivi touch.

**Casi d&#39;uso di esempio:**

- **Domanda di lavoro:** Informazioni personali, Istruzione, Esperienza, Riferimenti
- **Registrazione prodotto:** Dettagli di base, Specifiche tecniche, Informazioni sulla garanzia
- **Forms sondaggio:** Dati demografici, preferenze, feedback, contatto

### Layout procedura guidata

**Finalità:** guida gli utenti attraverso processi complessi passo dopo passo, riducendo il carico cognitivo e migliorando i tassi di completamento.

![Esempio di layout guidato](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Comportamento reattivo:**

- **Tutti i dispositivi:** mantiene lo stato attivo in un unico passaggio per un&#39;esperienza mobile ottimale.
- **Contenuto passaggio:** si adatta all&#39;interno di ogni passaggio (stacking o side-by-side).
- **Navigazione:** pulsanti descrittivi con spaziatura sufficiente.
- **Indicatore di avanzamento:** ridimensiona in modo appropriato le dimensioni dello schermo.

**Passaggi di implementazione:**

1. Utilizzare il [componente procedura guidata](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).
2. Suddividi le forme complesse in fasi logiche (sono ottimali 3-7 fasi).
3. Includi indicatori di progresso per l’orientamento degli utenti.
4. Fornisce chiari controlli di navigazione (Avanti, Indietro, Salva).

**Ottimizzazione mobile:**

- Utilizza destinazioni touch di grandi dimensioni (minimo 44 px) per i pulsanti di navigazione.
- Assicurati che gli indicatori a gradino siano chiari e visibili sui piccoli schermi.
- Limita il numero di campi per passaggio per ridurre lo scorrimento.
- Abilita il salvataggio automatico per evitare la perdita di dati.

**Best practice:**

- Garantire la progressione dei passaggi logici: ogni passaggio deve basarsi sul precedente.
- Utilizza titoli chiari per i passaggi, in modo che gli utenti sappiano cosa aspettarsi.
- Convalida l’input in ogni passaggio per rilevare gli errori in anticipo.
- Consente agli utenti di spostarsi all’indietro per rivedere o modificare le informazioni.

**Casi d&#39;uso di esempio:**

- **Indennizzi assicurativi:** Incidenti → Prove → Revisione → Personali
- **Configurazione account:** Informazioni di base → Preferenze → Sicurezza → Conferma
- **Processo ordine:** Prodotti → Spedizione → Riepilogo → pagamento

### Layout pannello a soffietto

**Scopo:** consente di risparmiare spazio organizzando il contenuto in sezioni comprimibili, ideali per informazioni facoltative o secondarie.

![Esempio di layout pannello a soffietto](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Comportamento reattivo:**

- **Prestazioni mobili eccellenti:** viene visualizzato solo il contenuto pertinente.
- **Intestazioni ottimizzate per il tocco:** Tocca ed espandi le sezioni con facilità.
- **Animazioni smussate:** fornire un feedback visivo per le interazioni.
- **Riduzione dello spazio:** Riduce al minimo lo scorrimento su tutti i dispositivi.

**Passaggi di implementazione:**

1. Utilizza il [componente Pannello a soffietto](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).
2. Raggruppa contenuti facoltativi correlati in ogni sezione.
3. Utilizza le intestazioni di sezione descrittive.
4. Impostare gli stati di apertura/chiusura predefiniti appropriati.

**Vantaggi per dispositivi mobili:**

- Riduce lo scorrimento comprimendo le sezioni inutilizzate.
- Interazione intuitiva con gesti naturali di espansione/compressione.
- Caricamento più rapido: è visibile solo il contenuto attivo.
- Maggiore attenzione: gli utenti possono vedere solo ciò di cui hanno bisogno.

**Best practice:**

- Utilizza intestazioni di sezione chiare in modo che gli utenti sappiano cosa c’è dentro prima di espanderlo.
- Raggruppa in modo logico il contenuto correlato all’interno di ogni sezione.
- Imposta le sezioni importanti per iniziare espanse, se necessario.
- Fornisci brevi anteprime di sezione per aiutare gli utenti a decidere cosa espandere.

**Casi d&#39;uso di esempio:**

- **Configurazione prodotto:** Supporto → per accessori → di base → avanzati
- **Domande frequenti su Forms:** Account → fatturazione → tecnico → Generale
- **Impostazioni Forms:** Privacy → Notifiche → Aspetto → Avanzate

## Parte 3: Best practice per la progettazione reattiva

### Best practice per tipo di dispositivo

+++Ottimizzazione mobile (320px-767px)

**Pratiche Essenziali:**

- Utilizza un layout a colonna singola per tutto il contenuto.
- Tasti touch-screen di grandi dimensioni (altezza minima 44 px).
- Semplifica la navigazione con opzioni chiare &quot;Indietro/Avanti&quot;.
- Riduci al minimo lo scorrimento all&#39;interno di ogni sezione.
- Attiva automaticamente il primo campo per visualizzare la tastiera.

**Linee Guida Specifiche Per Il Campo:**

- **Input di testo:** Larghezza intera con spaziatura ampia.
- **Elenchi a discesa:** Utilizza elementi di selezione nativi per migliorare l&#39;esperienza di contatto.
- **Selettori data:** Utilizza input data nativi per la compatibilità mobile.
- **Caricamenti di file:** Specificare aree di caricamento grandi e chiare.

+++

+++Ottimizzazione tablet (768px-1199px)

**Strategie di layout:**

- Utilizza layout a due colonne per i campi correlati.
- Verifica l&#39;orientamento sia verticale che orizzontale.
- Supporto delle interazioni con il mouse e con il tocco.
- Fornire aree di contenuto più ampie mantenendo al tempo stesso la leggibilità.

+++

+++Ottimizzazione desktop (1200 px+)

**Funzioni avanzate:**

- Utilizzare layout a più colonne per un utilizzo efficiente dello spazio.
- Scelte rapide da tastiera per gli utenti esperti.
- Implementa gli stati al passaggio del mouse per il feedback interattivo.
- Fornisci la convalida avanzata con messaggi di errore dettagliati.

+++

## Risoluzione completa dei problemi

### Problemi di layout

+++Interruzioni layout modulo su dispositivi mobili

**Cause comuni:**

- Elementi a larghezza fissa non scalabili
- CSS progettato per layout desktop
- Immagini o contenuti con overflow dei contenitori

**Soluzioni:**

- Assicurati che le immagini e i contenitori siano scalabili in base alle dimensioni dello schermo.
- Utilizza un design mobile-first con miglioramento progressivo.
- Test con emulatori di dispositivi e dispositivi reali.
- Utilizzare il dimensionamento flessibile invece di dimensioni fisse.

+++

+++Destinazioni Touch troppo piccole

**Cause comuni:**

- Pulsanti inferiori a 44 px × 44 px
- Elementi interattivi troppo vicini tra loro
- CSS personalizzato che sovrascrive i valori predefiniti touch

**Soluzioni:**

- Assicurati che tutti gli elementi interattivi siano almeno 44 px × 44 px.
- Aggiungi spaziatura tra pulsanti e collegamenti.
- Verificare l&#39;interazione con le dita reali, non solo con il mouse.
- Aumenta le aree di destinazione di contatto per toccare più facilmente.

+++

+++Problemi di overflow del contenuto

**Cause comuni:**

- Testo lungo o etichette che non vanno a capo
- Contenitori a larghezza fissa
- Immagini che non vengono ridimensionate correttamente

**Soluzioni:**

- Abilita la disposizione del testo per i contenuti lunghi.
- Utilizza immagini reattive scalabili in modo appropriato.
- Implementare layout flessibili che si adattano ai contenuti.
- Esegui il test con diverse lunghezze di contenuto.

+++

### Problemi relativi alle prestazioni

+++Caricamento lento su dispositivi mobili

**Cause comuni:**

- Immagini di grandi dimensioni non ottimizzate per i dispositivi mobili
- Esecuzione eccessiva di JavaScript
- Troppi campi modulo caricati contemporaneamente

**Soluzioni:**

- Ottimizza le immagini per diverse dimensioni dello schermo.
- Caricare contenuti non critici solo quando necessario.
- Utilizza tecniche per velocizzare il caricamento dei dispositivi mobili.
- Riduci al minimo script e widget di terze parti.

+++

### Problemi di test e convalida

+++Differenze tra emulatore e dispositivo reale

**Cause comuni:**

- Differenze di rendering specifiche per il browser
- Differenze di interazione tra tocco e mouse
- Variazioni della velocità di rete

**Soluzioni:**

- Se possibile, eseguire il test sui dispositivi effettivi.
- Utilizza più browser per testare l’emulatore.
- Simulare diverse velocità di rete durante il test.
- Convalida con utenti reali negli ambienti di destinazione.

+++

## Metriche di successo per Forms reattivo

+++Indicatori prestazioni chiave

**Metriche esperienza utente:**

- **Percentuale di completamento modulo:** Target 85%+ su dispositivi mobili
- **Tempo di completamento:** Il tempo di completamento mobile deve essere entro il 20% del desktop
- **Frequenza errori:** meno del 5% di errori di convalida
- **Punti di abbandono:** Identificare la destinazione degli utenti

**Prestazioni tecniche:**

- **Tempo di caricamento pagina:** In meno di 3 secondi sulle reti 3G
- **Core Web Vitals:** supera tutti i benchmark delle prestazioni Google
- **Punteggio di accessibilità:** conformità WCAG 2.1 AA
- **Compatibilità tra browser diversi:** 98%+ funzionalità tra browser principali

+++

+++Elenco di controllo di prova

**Prima della pubblicazione:**

- Verifica il modulo su dispositivi mobili effettivi.
- Assicurati che tutte le destinazioni di contatto siano almeno 44 px × 44 px.
- Verifica la leggibilità del testo a tutte le dimensioni dello schermo.
- La convalida del modulo di conferma funziona su tutti i dispositivi.
- Assicurati che il tempo di caricamento sia inferiore a 3 secondi su dispositivi mobili.
- Verifica che tutti gli elementi interattivi siano accessibili.
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


