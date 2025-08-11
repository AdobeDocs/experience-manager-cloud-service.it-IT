---
title: Editor di regole per Dynamic Forms nell’editor universale
description: Creare moduli dinamici e intelligenti tramite l’Editor di regole nell’Editor universale. Aggiungi logica condizionale, calcoli e comportamenti interattivi senza codifica.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '2598'
ht-degree: 1%

---


# Editor di regole per Dynamic Forms nell’editor universale

L’editor di regole consente agli autori di trasformare i moduli statici in esperienze intelligenti e reattive, senza scrivere codice. È possibile visualizzare i campi in modo condizionale, eseguire calcoli, convalidare dati, guidare gli utenti attraverso i flussi e integrare una logica di business che si adatta al tipo di persona.

## Cosa imparerai

Al termine di questa guida, sarai in grado di:

- Comprendere il funzionamento delle regole e quando utilizzare tipi di regole diversi
- Abilitare e accedere all’editor di regole nell’editor universale
- Creare una logica condizionale per visualizzare o nascondere i campi in modo dinamico
- Implementazione di calcoli automatizzati e convalida dei dati
- Creare funzioni personalizzate per regole aziendali complesse
- Applicare best practice per prestazioni, manutenibilità e UX

## Perché utilizzare l’editor di regole?

- **Logica condizionale**: mostra i campi rilevanti solo quando necessario per ridurre il rumore e il carico cognitivo.
- **Calcoli dinamici**: calcola automaticamente i valori (totali, aliquote, imposte) durante la digitazione da parte degli utenti.
- **Convalida dei dati**: consente di evitare gli errori in anticipo con controlli in tempo reale e messaggi di cancellazione.
- **Esperienze guidate**: guida gli utenti attraverso passaggi logici (procedure guidate, ramificazioni).
- **Authoring senza codice**: configura un comportamento efficace tramite un&#39;interfaccia visiva.

Gli scenari comuni includono calcolatori fiscali, calcolatori di prestiti e premi, flussi di idoneità, applicazioni in più fasi e indagini con domande condizionali.

## Funzionamento delle regole

Una regola definisce cosa dovrebbe accadere quando viene soddisfatta una condizione. Concettualmente, una regola è composta da due parti:

- **Condizione**: istruzione che restituisce true o false.
   - Esempi: &quot;Entrate > 50.000,&quot; &quot;Copertura = &#39;Sì&#39;,&quot; &quot;Il campo è vuoto&quot;
- **Azione**: cosa accade quando la condizione è vera (e facoltativamente quando è falsa).
   - Esempi: mostrare/nascondere un campo, impostare/cancellare un valore, convalidare l’input, abilitare/disabilitare un pulsante

+++ Modelli logici delle regole

- **Condizione → Azione (When/Then)**

  ```text
  WHEN Gross Salary > 50000
  THEN Show "Additional Deduction"
  ```

  Ideale per la visibilità condizionale e la divulgazione progressiva.

- **Condizione ← azione (Imposta se/solo se)**

  ```text
  SET Taxable Income = Gross Salary - Deductions
  IF Deductions are applicable
  ```

  Consigliato per calcoli e trasformazioni di dati.

- **Se → Allora → Altro (Azione Alternativa)**

  ```text
  IF Income > 50000
  THEN Show "High Income" fields
  ELSE Show "Standard Income" fields
  ```

  Consigliato per logica di ramificazione e flussi reciprocamente esclusivi.

+++

+++ Esempio reale

- **Condizione**: &quot;Lo stipendio lordo supera i 50.000 dollari&quot;
- **Azione primaria**: mostra &quot;detrazione aggiuntiva&quot;
- **Azione alternativa**: nascondi &quot;detrazione aggiuntiva&quot;
- **Risultato**: gli utenti visualizzano solo i campi ad essi applicabili

+++

## Prerequisiti


+++ Requisiti di accesso

**Autorizzazioni essenziali e configurazione**:

- **AEM as a Cloud Service**: autorizzazione alla modifica di accessi tramite modulo
- **Editor universale**: installato e configurato nel tuo ambiente
- **Estensione editor regole**: abilitato tramite [Extension Manager](/help/implementing/developing/extending/extension-manager.md)
- **Autorizzazioni di modifica dei moduli**: possibilità di creare e modificare i componenti del modulo in Universal Editor

**Passaggi di verifica**:

1. Conferma di poter accedere a Universal Editor dalla console AEM Sites.
2. Verificare di poter creare e modificare i componenti del modulo
3. Controlla che venga visualizzata l&#39;icona dell&#39;editor di regole ![edit-rules](/help/forms/assets/edit-rules-icon.svg) durante la selezione dei componenti del modulo

+++

+++ Requisiti tecnici

**Conoscenze e competenze richieste**:

- **Competenza editor universale**: esperienza nella creazione di moduli con input di testo, elenchi a discesa e proprietà di campo di base
- **Informazioni sulla logica di business**: possibilità di definire requisiti condizionali e regole di convalida per il caso d&#39;uso specifico
- **Familiarità del componente Modulo**: conoscenza dei tipi di campo (testo, numero, elenco a discesa), delle proprietà (obbligatorie, visibili, di sola lettura) e della struttura del modulo

**Facoltativo per utilizzo avanzato**:

- **Nozioni di base di JavaScript**: necessario solo per la creazione di funzioni personalizzate (tipi di dati, funzioni, sintassi di base)
- **Comprensione JSON**: utile per la manipolazione di dati complessi e le integrazioni API

**Domande di valutazione**:

- È possibile creare un modulo di base con input di testo e un pulsante di invio in Universal Editor?
- Sapete quando i campi devono essere obbligatori o facoltativi nel vostro contesto aziendale?
- È possibile identificare gli elementi del modulo che richiedono visibilità condizionale nel caso d’uso?

+++

+++ Abilitare l’estensione Editor regole

**Importante**: l&#39;estensione dell&#39;editor di regole non è abilitata per impostazione predefinita negli ambienti dell&#39;editor universale.

**Passaggi di attivazione**:

1. Passa a [Extension Manager](/help/implementing/developing/extending/extension-manager.md) nel tuo ambiente AEM
2. Individua l’estensione &quot;Rule Editor&quot; nell’elenco delle estensioni disponibili.
3. Fai clic su **Abilita** e conferma l&#39;attivazione
4. Attendere l&#39;aggiornamento del sistema (potrebbero essere necessari 1-2 minuti)

**Verifica**:

- Dopo l&#39;abilitazione, l&#39;icona Editor regole viene visualizzata quando si seleziona un componente del modulo: ![edit-rules](/help/forms/assets/edit-rules-icon.svg)

![Editor regole dell&#39;editor universale](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
Figura: L’icona Editor regole viene visualizzata quando si selezionano i componenti del modulo

Per aprire l’editor di regole:

1. Seleziona un componente modulo nell’Editor universale.
2. Fai clic sull’icona Editor di regole.
3. L’Editor regole si apre in un pannello laterale.

![Interfaccia utente dell&#39;editor di regole](/help/edge/docs/forms/assets/rule-editor-for-field.png)
Figura: Interfaccia dell’editor delle regole per la modifica delle regole dei componenti

>[!NOTE]
>
> In questo articolo, &quot;componente modulo&quot; e &quot;oggetto modulo&quot; si riferiscono agli stessi elementi (ad esempio, ingressi, pulsanti, pannelli).

## Panoramica dell’interfaccia dell’editor di regole

![Interfaccia utente editor regole](/help/edge/docs/forms/assets/rule-editor-interface.png)
Figura: Interfaccia completa dell’Editor regole con componenti numerati

- **Titolo componente e tipo di regola**: conferma il componente selezionato e il tipo di regola attivo.
- **Pannello Funzioni e oggetti modulo**:
   - Oggetti modulo: visualizzazione gerarchica di campi e contenitori a cui fare riferimento nelle regole
   - Funzioni: helper incorporati di matematica, stringhe, data e convalida
- **Selettore pannello**: mostra/nascondi il pannello oggetti e funzioni per aumentare l&#39;area di lavoro
- **Generatore di regole visive**: Compositore di regole a discesa con trascinamento della selezione
- **Controlli**: Operazione completata (salvataggio), Annulla (eliminazione). Prima di salvare, verifica sempre le regole.

+++

+++ Gestione delle regole esistenti

Quando un componente ha già delle regole, puoi:

- **Visualizza**: vedere i riepiloghi e la logica delle regole
- **Modifica**: modifica condizioni e azioni
- **Riordina**: cambia ordine di esecuzione (dall&#39;alto in basso)
- **Attiva/Disattiva**: attiva/disattiva le regole per il test
- **Elimina**: rimuovi le regole in modo sicuro

>[!TIP]
>
> Metti regole specifiche prima di quelle generali. L’esecuzione è dall’alto verso il basso.

+++

## Tipi di regole disponibili

Scegli il tipo di regola che corrisponde meglio all’intento.

+++ Logica condizionale

- **Quando**: regola primaria per un comportamento condizionale complesso (condizione → azione ± altro)
- **Nascondi/Mostra**: controlla la visibilità in base a una condizione (divulgazione progressiva)
- **Abilita/Disabilita**: controlla se un campo è interattivo (ad esempio, disabilita Invia finché i campi obbligatori non sono validi)

+++

+++ Manipolazione dei dati

- **Imposta valore di**: compila automaticamente i valori (ad esempio, date, totali, copie)
- **Cancella valore di**: rimuovi dati quando cambiano le condizioni
- **Formato**: trasforma la formattazione di visualizzazione (valuta, telefono, data) senza modificare i valori memorizzati

+++

+++ Convalida

- **Convalida**: logica di convalida personalizzata, inclusi controlli tra campi diversi e regole business

+++

+++ Calcolo

- **Espressione matematica**: calcolo dei valori in tempo reale (totali, imposte, rapporti)

+++

+++ Interfaccia utente

- **Imposta stato attivo**: sposta lo stato attivo su un campo specifico (usa con moderazione)
- **Imposta proprietà**: modifica dinamicamente le proprietà del componente (segnaposto, opzioni, ecc.)

+++

+++ Controllo modulo

- **Invia modulo**: invia il modulo a livello di programmazione (solo dopo il superamento delle convalide)
- **Ripristina modulo**: cancella e ripristina lo stato iniziale (conferma prima dell&#39;uso)
- **Salva modulo**: salva come bozza per un momento successivo (moduli lunghi, sessioni multiple)

+++

+++ Avanzato

- **Richiama servizio**: chiama API/servizi esterni (caricamento handle ed errori)
- **Aggiungi/Rimuovi istanza**: gestisci sezioni ripetibili (ad esempio, dipendenti, indirizzi)
- **Accedi a**: Inoltra ad altri moduli/pagine (mantieni i dati prima della navigazione)
- **Naviga tra i pannelli**: navigazione e salto del passaggio della procedura guidata di controllo
- **Evento di invio**: attiva eventi personalizzati per integrazioni o analisi

+++

## Tutorial dettagliato: creare un calcolatore fiscale intelligente

+++ Panoramica del tutorial

In questo esempio vengono illustrati la visibilità condizionale e i calcoli automatici.

![Schermata dell&#39;interfaccia dell&#39;editor di regole che mostra la creazione di una regola condizionale con logica When-Then per la visibilità dei campi modulo](/help/edge/docs/forms/assets/rule-editor-1.png)
Figura: Modulo di calcolo delle imposte con campi condizionali intelligenti

Verrà creato un modulo che:

1. Si adatta all’input dell’utente mostrando i campi rilevanti
2. Calcola i valori in tempo reale
3. Convalida i dati per migliorare la precisione

+++

+++ Struttura del modulo

| Nome campo | Tipo | Scopo | Comportamento |
|-------------------------|---------------|--------------------------------|-----------------------------------------|
| Stipendio lordo | Inserimento numero | Reddito annuale dell&#39;utente | Attiva la logica condizionale |
| Detrazione aggiuntiva | Inserimento numero | Detrazioni supplementari (se ammissibili) | Visibile solo quando lo stipendio è > $50.000 |
| Reddito Imponibile | Inserimento numero | Valore calcolato | Sola lettura, aggiornamenti in caso di modifica |
| Imposta da pagare | Inserimento numero | Valore calcolato | Sola lettura, calcolato su base forfettaria |

+++

+++ Logica di business

- **Regola 1: visualizzazione condizionale**

  ```text
  WHEN Gross Salary > 50,000
  THEN Show "Additional Deduction"
  ELSE Hide "Additional Deduction"
  ```

- **Regola 2: calcolo reddito imponibile**

  ```text
  SET Taxable Income = Gross Salary - Additional Deduction
  (Only when Additional Deduction applies)
  ```

- **Regola 3: calcolo imposta a debito**

  ```text
  SET Tax Payable = Taxable Income × 10%
  (Simplified flat rate)
  ```

+++

+++ Passaggio 1: creare il modulo di base

**Obiettivo**: creare il modulo di base con tutti i campi e le impostazioni iniziali.

1. **Apri editor universale**:
   - Passa alla console AEM Sites, seleziona la pagina e fai clic su **Modifica**
   - Verifica che [Universal Editor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html) sia configurato correttamente

2. **Aggiungi componenti modulo in questo ordine**:
   - Titolo (H2): &quot;Modulo di calcolo delle imposte&quot;
   - Numero Input: &quot;Stipendio lordo&quot; (obbligatorio: Sì, segnaposto: &quot;Inserisci stipendio annuale&quot;)
   - Input numero: &quot;Detrazione aggiuntiva&quot; (obbligatorio: No, segnaposto: &quot;Inserire detrazioni aggiuntive&quot;)
   - Input numero: &quot;Reddito imponibile&quot; (sola lettura: sì)
   - Input numero: &quot;Imposta dovuta&quot; (sola lettura: sì)
   - Pulsante Invia: &quot;Calcola imposta&quot;

3. **Configurare le proprietà del campo iniziale**:
   - Nascondi &quot;Detrazione aggiuntiva&quot; (set Visibile: no nel pannello Proprietà)
   - Impostare &quot;Reddito imponibile&quot; e &quot;Imposta pagabile&quot; su Sola lettura: Sì

![Schermata di un modulo di calcolo delle imposte con campi di input per lo stipendio lordo, lo stato civile e i figli dipendenti, che illustra la struttura del modulo prima dell&#39;applicazione delle regole](/help/edge/docs/forms/assets/rule-editor2.png)
Figura: Struttura del modulo iniziale con componenti di base configurati

**Checkpoint**: è necessario disporre di un modulo con tutti i campi obbligatori in cui &quot;Detrazione aggiuntiva&quot; è nascosto e i campi calcolati sono di sola lettura.

+++

+++ Passaggio 2: aggiungere la regola di visibilità condizionale

**Obiettivo**: mostra il campo &quot;Detrazione aggiuntiva&quot; solo quando lo stipendio lordo supera i 50.000 dollari.

1. **Selezionare il campo Stipendio lordo** e fare clic sull&#39;icona Editor regole ![edit-rules](/help/forms/assets/edit-rules-icon.svg)
2. **Crea una nuova regola**:
   - Fai clic su **Crea**.
   - Cambia il tipo di regola da &quot;Imposta valore di&quot; a **&quot;Quando&quot;**
3. **Configura la condizione**:
   - Seleziona **&quot;è maggiore di&quot;** dal menu a discesa
   - Immetti `50000` nel campo numerico
4. **Imposta l&#39;azione Then**:
   - Scegli **&quot;Show&quot;** dal menu a discesa Seleziona azione
   - Trascina o seleziona il campo **&quot;Detrazione aggiuntiva&quot;** dagli oggetti modulo
5. **Aggiungi l&#39;azione Else**:
   - Fare clic su **&quot;Aggiungi sezione Else&quot;**
   - Scegli **&quot;Nascondi&quot;** dal menu a discesa Seleziona azione
   - Seleziona campo **&quot;Detrazione aggiuntiva&quot;**
6. **Salva la regola**: fai clic su **Fine**

>[!NOTE]
>
> Approccio alternativo: è possibile ottenere lo stesso risultato creando una regola Mostra/Nascondi direttamente nel campo &quot;Detrazione aggiuntiva&quot; invece di una regola Quando su &quot;Stipendio lordo&quot;.

+++

+++ Passaggio 3: aggiungere regole di calcolo

**Obiettivo**: calcolare automaticamente &quot;Reddito imponibile&quot; e &quot;Imposta pagabile&quot; in base all&#39;input dell&#39;utente.

**Configura calcolo reddito imponibile**:

1. **Selezionare il campo &quot;Reddito imponibile&quot;** e aprire l&#39;editor di regole
2. **Crea espressione matematica**:
   - Fai clic su **Crea** → Seleziona **&quot;Espressione matematica&quot;**
   - Espressione di compilazione: **Stipendio lordo − detrazione aggiuntiva**
   - Trascinare &quot;Stipendio lordo&quot; nel primo campo
   - Seleziona operatore **&quot;Meno&quot;**
   - Trascina &quot;Detrazione aggiuntiva&quot; nel secondo campo
3. **Salva**: fai clic su **Fine**

**Configura calcolo imposta a debito**:

1. **Selezionare il campo &quot;Imposta dovuta&quot;** e aprire l&#39;editor di regole
2. **Crea espressione matematica**:
   - Fai clic su **Crea** → Seleziona **&quot;Espressione matematica&quot;**
   - Espressione di compilazione: **Reddito imponibile × 10 ÷ 100**
   - Trascinare &quot;Reddito imponibile&quot; nel primo campo
   - Seleziona **&quot;Moltiplicato per&quot;** operatore
   - Immetti `10` come numero
   - Fare clic su **&quot;Estendi espressione&quot;**
   - Seleziona **&quot;diviso per&quot;** operatore
   - Immetti `100` come numero
3. **Salva**: fai clic su **Fine**

+++

+++ Passaggio 4: verifica del modulo

**Verifica l&#39;implementazione sottoponendo a test il flusso completo**:

1. **Anteprima modulo**: fare clic sulla modalità di anteprima in Universal Editor
2. **Verifica la logica condizionale**:
   - Immettere lo stipendio lordo = `30000` → &quot;Detrazione aggiuntiva&quot; deve rimanere nascosta
   - Immettere lo stipendio lordo = `60000` → dovrebbe essere visualizzata la &quot;detrazione aggiuntiva&quot;
3. **Calcoli del test**:
   - Con Stipendio lordo = `60000`, immettere Detrazione aggiuntiva = `5000`
   - Verifica reddito imponibile = `55000` (60000 - 5000)
   - Verifica imposta a debito = `5500` (55000 × 10%)

![Anteprima modulo](/help/edge/docs/forms/assets/rule-editor-form.png)
Figura: Calcolatore imposte completato con campi condizionali e calcoli automatici

**Criteri di successo**: il modulo deve mostrare/nascondere dinamicamente i campi e calcolare i valori in tempo reale durante la digitazione da parte degli utenti.


+++

## Avanzate: funzioni personalizzate

Per una logica di business complessa oltre le funzionalità incorporate, puoi creare funzioni JavaScript personalizzate che si integrano perfettamente con l’Editor di regole.

+++ Quando utilizzare funzioni personalizzate

**Scenari ideali per le funzioni personalizzate**:

- **Calcoli complessi**: i calcoli a più passaggi non sono facilmente espressi nella regola Espressione matematica
- **Convalide specifiche per l&#39;azienda**: logica di convalida personalizzata specifica per l&#39;organizzazione o il settore
- **Trasformazioni dati**: conversioni di formati, manipolazioni di stringhe o analisi dei dati
- **Integrazioni esterne**: chiamate alle API interne o a servizi di terze parti (con limitazioni)

**Vantaggi delle funzioni personalizzate**:

- **Riutilizzabilità**: scrittura singola, utilizzo in più moduli e regole
- **Manutenzione**: logica centralizzata più semplice da aggiornare ed eseguire il debug
- **Prestazioni**: esecuzione di JavaScript ottimizzata rispetto a catene di regole complesse
- **Flessibilità**: gestisci casi edge e scenari complessi non gestiti da regole standard

+++

+++ Creazione e implementazione di funzioni personalizzate

**Percorso file**: tutte le funzioni personalizzate devono essere definite in `/blocks/form/functions.js` nel progetto Edge Delivery Services.

**Flusso di lavoro di sviluppo**:

1. **Progettazione funzione**
   - Utilizzare nomi di funzione descrittivi e orientati alle azioni
   - Definisci i tipi di parametri e i valori restituiti
   - Gestione corretta dei casi edge e degli input non validi

2. **Implementazione**
   - Scrivi JavaScript pulito e ben commentato
   - Includi convalida input e gestione degli errori
   - Verifica delle funzioni in modo indipendente prima dell’integrazione

3. **documentazione**
   - Aggiungere commenti JSDoc completi
   - Includi esempi di utilizzo e descrizioni dei parametri
   - Documentare eventuali limitazioni o dipendenze

4. **Distribuzione**
   - Esportare funzioni utilizzando esportazioni denominate
   - Implementare nell’archivio del progetto
   - Verifica il completamento della build prima del test

**Implementazione di esempio**:

```javascript
/**
 * Concatenates first and last name with proper formatting
 * @name getFullName
 * @description Combines first and last name, handles edge cases like missing values
 * @param {string} firstName - The person's first name
 * @param {string} lastName - The person's last name  
 * @returns {string} Formatted full name or empty string if both inputs are invalid
 */
function getFullName(firstName, lastName) {
  // Handle null, undefined, or empty string inputs
  const first = (firstName || '').toString().trim();
  const last = (lastName || '').toString().trim();
  
  return `${first} ${last}`.trim();
}

/**
 * Calculates the number of days between two dates
 * @name days
 * @description Computes absolute difference in days, handles various date input formats
 * @param {Date|string} endDate - End date (Date object or ISO string)
 * @param {Date|string} startDate - Start date (Date object or ISO string)
 * @returns {number} Number of days between dates, 0 if inputs are invalid
 */
function days(endDate, startDate) {
  // Convert string inputs to Date objects
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // Validate date objects
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  // Calculate absolute difference in milliseconds, then convert to days
  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// Export functions for use in Rule Editor
export { getFullName, days };
```

![Aggiunta funzione personalizzata](/help/edge/docs/forms/assets/create-custom-function.png)
Figura: Aggiunta di funzioni personalizzate al file functions.js

+++

+++ Utilizzo di funzioni personalizzate nell’editor delle regole

**Passaggi dell&#39;integrazione**:

1. **Aggiungi funzione al progetto**
   - Crea o modifica `/blocks/form/functions.js` nel progetto
   - Includi la funzione nell’istruzione di esportazione

2. **Distribuisci e genera**
   - Eseguire il commit delle modifiche nell&#39;archivio
   - Verifica del completamento del processo di compilazione
   - Consenti aggiornamenti cache CDN

3. **Accesso nell&#39;editor di regole**
   - Apri l’editor di regole per qualsiasi componente del modulo
   - Seleziona **&quot;Output funzione&quot;** nel menu a discesa **Seleziona azione**
   - Scegliere la funzione personalizzata dall&#39;elenco delle funzioni disponibili
   - Configurare i parametri della funzione utilizzando campi modulo o valori statici

4. **Verifica completa**
   - Visualizza l&#39;anteprima del modulo per verificare il comportamento della funzione
   - Test con varie combinazioni di input, inclusi casi limite
   - Verificare l’impatto delle prestazioni sul caricamento e sull’interazione dei moduli

![Funzione personalizzata nell&#39;editor di regole](/help/edge/docs/forms/assets/custom-function-rule-editor.png)
Figura: Selezione e configurazione di funzioni personalizzate nell’interfaccia dell’editor di regole

**Best practice per l&#39;utilizzo delle funzioni**:

- **Gestione degli errori**: includi sempre il comportamento di fallback per gli errori di funzione
- **Prestazioni**: funzioni di profilo con volumi di dati realistici
- **Sicurezza**: convalida di tutti gli input per evitare vulnerabilità di sicurezza
- **Test**: crea test case che coprono casi normali e edge

+++

## Best practice per lo sviluppo di regole


+++ Ottimizzazione delle prestazioni

- Ridurre al minimo la complessità delle regole; suddividere la logica di grandi dimensioni in regole piccole e mirate
- Ordina le regole in base alla frequenza (prima le più comuni)
- Mantieni gestibili i set di regole per componente
- Preferisci funzioni personalizzate riutilizzabili rispetto alla logica di duplicazione

+++

+++ Esperienza utente

- Fornire una convalida chiara e un feedback in linea
- Evita di alterare le modifiche visive; usa mostra/nascondi attentamente
- Test tra dispositivi e layout

+++

+++ Igiene dello sviluppo

- Test con casi limite e valori noti
- Verifica tra browser
- Intento del documento alla base di regole complesse, non solo meccanica
- Gestisci un inventario di regole per i moduli di grandi dimensioni
- Utilizza nomi coerenti per componenti e regole
- Funzioni personalizzate della versione e test in ambienti non di produzione

+++

## Risoluzione dei problemi comuni


+++ Le regole non vengono attivate

- Verifica dei nomi e dei riferimenti dei componenti
- Controlla ordine di esecuzione (dall’alto verso il basso)
- Convalida condizioni con valori noti
- Controlla la console del browser per individuare eventuali errori di blocco

+++

+++ Comportamento errato

- Verifica operatori e raggruppamenti (AND/OR)
- Test dei singoli frammenti di espressione
- Conferma tipi di dati (numeri e stringhe)

+++

+++ Problemi relativi alle prestazioni

- Semplificare le condizioni profondamente nidificate
- Funzioni personalizzate del profilo
- Riduci a icona le chiamate esterne all&#39;interno delle regole
- Utilizzare selettori e riferimenti specifici

+++

+++ Problemi relativi alla funzione personalizzata

- Conferma percorso file: `/blocks/form/functions.js`
- Verificare che le esportazioni denominate siano corrette
- Conferma che la build includa le modifiche
- Cancella cache del browser dopo la distribuzione
- Convalidare i tipi di parametri e la gestione degli errori

+++

+++ Integrazione con Universal Editor

- Conferma che l’estensione Editor regole sia abilitata
- Seleziona un componente supportato
- Utilizza un browser supportato (Chrome, Firefox, Safari)
- Verifica di disporre delle autorizzazioni necessarie

## Limitazioni importanti

>[!IMPORTANT]
>
> Vincoli di funzione personalizzati:
>
> - Importazioni statiche/dinamiche non supportate
> - Tutta la logica deve risiedere in `/blocks/form/functions.js`
> - Le funzioni devono essere sincrone (no async/await or Promises)
> - L’accesso all’API del browser è limitato

>[!WARNING]
>
> Considerazioni sulla produzione:
>
> - Esegui il test completo nella gestione temporanea
> - Monitorare le prestazioni dopo l’implementazione
> - Disponi di un piano di ripristino per i problemi relativi alle regole
> - Considerare reti lente e dispositivi a basse specifiche

## Riepilogo

L’editor di regole di Universal Editor trasforma i moduli statici in esperienze intelligenti e reattive che si adattano all’input dell’utente in tempo reale. Sfruttando la logica condizionale, i calcoli automatizzati e le regole aziendali personalizzate, è possibile creare flussi di lavoro di moduli sofisticati senza scrivere il codice dell’applicazione.

**Funzionalità chiave acquisite**:

- **Logica condizionale**: mostra e nascondi i campi in base all&#39;input dell&#39;utente per creare esperienze mirate e rilevanti
- **Calcoli dinamici**: calcola automaticamente i valori (imposte, totali, tassi) durante l&#39;interazione degli utenti con il modulo
- **Convalida dei dati**: implementa la convalida in tempo reale con messaggi di feedback chiari e actionable
- **Funzioni personalizzate**: estendere le funzionalità con JavaScript per logiche di business e integrazioni complesse
- **Ottimizzazione delle prestazioni**: applica le best practice per uno sviluppo delle regole gestibile ed efficiente

**Valore consegnato**:

- **Esperienza utente migliorata**: riduci il carico cognitivo con la divulgazione progressiva e i flussi di moduli intelligenti
- **Errori ridotti**: impedisci invii non validi tramite convalida in tempo reale e input guidato
- **Maggiore efficienza**: automazione dei calcoli e dell&#39;immissione dei dati per ridurre al minimo il lavoro dell&#39;utente
- **Soluzioni gestibili**: crea regole riutilizzabili e ben documentate su larga scala nell&#39;organizzazione

**Impatto aziendale**:

Forms diventa uno strumento potente per la raccolta di dati, la qualifica dei lead e il coinvolgimento degli utenti. L’editor di regole consente agli autori non tecnici di implementare una logica di business sofisticata, riducendo i costi di sviluppo e migliorando al contempo i tassi di completamento dei moduli e la qualità dei dati.

+++

## Passaggi successivi

**Percorso consigliato**:

1. **Inizia con le nozioni di base**: crea semplici regole di visualizzazione per comprendere i concetti di base
2. **Esercitazione con i tutorial**: utilizza l&#39;esempio del calcolatore delle imposte come base per i moduli
3. **Espandi gradualmente**: aggiungi espressioni matematiche e regole di convalida man mano che la tua affidabilità cresce
4. **Implementazione di funzioni personalizzate**: sviluppo di funzioni JavaScript per esigenze aziendali specifiche
5. **Ottimizza e ridimensiona**: applica le best practice per le prestazioni e mantieni la documentazione sulle regole

**Risorse aggiuntive**:

- [Documentazione di Universal Editor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html) per un contesto più ampio
- [Guida di Extension Manager](/help/implementing/developing/extending/extension-manager.md) per abilitare funzionalità aggiuntive
- [Edge Delivery Services forms](/help/edge/docs/forms/overview.md) per informazioni complete sullo sviluppo di moduli

