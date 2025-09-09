---
title: Editor regole per Edge Delivery Services Forms
description: Crea moduli dinamici e avanzati utilizzando l’editor di regole nell’editor universale. Aggiungi logica condizionale, calcoli e comportamenti interattivi senza codifica.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: e2bc958104bd9b75845ad2c213eec18d2560a3a4
workflow-type: tm+mt
source-wordcount: '2780'
ht-degree: 92%

---


# Editor regole per Edge Delivery Services Forms

L’editor di regole consente agli autori di trasformare i moduli statici in esperienze intelligenti e reattive senza scrivere codice. Puoi visualizzare i campi in modo condizionale, eseguire calcoli, convalidare dati, guidare gli utenti attraverso specifici flussi e integrare una logica di business che si adatta in base a ciò che viene digitato dall&#39;utente.

## Che cosa imparerai

Al termine di questa guida, sarai in grado di:

- Comprendere il funzionamento delle regole e quando utilizzare tipi di regole diversi
- Abilitare e accedere all’editor di regole nell’editor universale
- Creare una logica condizionale per visualizzare o nascondere i campi in modo dinamico
- Implementare calcoli automatizzati e convalidare dati
- Creare funzioni personalizzate per regole di business complesse
- Applicare best practice per prestazioni, facilità di manutenzione e UX

## Perché utilizzare l’editor di regole?

- **Logica condizionale**: mostra i campi rilevanti solo quando necessario per un modulo più snello e per ridurre il carico cognitivo.
- **Calcoli dinamici**: calcola automaticamente i valori (totali, aliquote, imposte) durante la digitazione da parte degli utenti.
- **Convalida dei dati**: evita gli errori prima che si verifichino, con controlli in tempo reale e messaggi chiari.
- **Esperienze guidate**: guida gli utenti attraverso passaggi logici (procedure guidate, ramificazioni).
- **Authoring senza codice**: configura un comportamento efficace tramite un’interfaccia visiva.

Alcuni scenari comuni sono calcolatori fiscali, calcolatori di prestiti e premi, flussi di idoneità, compilazione in più fasi e sondaggi con domande condizionali.

## Come funzionano le regole

Una regola definisce cosa dovrebbe accadere quando viene soddisfatta una condizione. Concettualmente, una regola è composta da due parti:

- **Condizione**: istruzione che valori vero o falso.
   - Esempi: “Entrate > 50.000,” “Copertura = “Sì”,” “Il campo è vuoto”
- **Azione**: cosa si verifica quando la condizione risulta soddisfatta (vera), e facoltativamente quando non lo è, ossia falsa).
   - Esempi: mostrare/nascondere un campo, impostare/cancellare un valore, convalidare l’input, abilitare/disabilitare un pulsante

+++ Pattern logici delle regole

- **Condizione → Azione (Se/Allora)**

  ```text
  WHEN Gross Salary > 50000
  THEN Show "Additional Deduction"
  ```

  Ideale per la visibilità condizionale e la divulgazione progressiva.

- **Azione ← Condizione (Imposta se/Solo se)**

  ```text
  SET Taxable Income = Gross Salary - Deductions
  IF Deductions are applicable
  ```

  Ideale per calcoli e trasformazioni di dati.

- **Se → Allora → Altro (Azione alternativa)**

  ```text
  IF Income > 50000
  THEN Show "High Income" fields
  ELSE Show "Standard Income" fields
  ```

  Ideale per logica di ramificazione e flussi reciprocamente esclusivi.

+++

+++ Esempio reale

- **Condizione**: “lo stipendio lordo supera i 50.000 dollari”
- **Azione primaria**: mostra “detrazione aggiuntiva”
- **Azione alternativa**: nascondi “detrazione aggiuntiva”
- **Risultato**: gli utenti visualizzano solo i campi a essi applicabili

+++

## Prerequisiti


+++ Requisiti di accesso

**Autorizzazioni essenziali e configurazione**:

- **AEM as a Cloud Service**: accesso di authoring con autorizzazioni alla modifica del modulo
- **Editor universale**: installato e configurato nel tuo ambiente
- **Estensione editor di regole**: abilitato tramite [Extension Manager](/help/implementing/developing/extending/extension-manager.md)
- **Autorizzazioni di modifica del modulo**: possibilità di creare e modificare i componenti del modulo nell’editor universale

**Passaggi di verifica**:

1. Confermare di poter accedere all’editor universale dalla console AEM Sites
2. Verificare di poter creare e modificare i componenti del modulo
3. Controllare che venga visualizzata l’icona dell’editor di regole ![Modifica regole](/help/forms/assets/edit-rules-icon.svg) durante la selezione dei componenti del modulo

+++

+++ Requisiti tecnici

**Conoscenze e competenze richieste**:

- **Competenza editor universale**: esperienza nella creazione di moduli con input di testo, elenchi a discesa e proprietà di campo di base
- **Informazioni sulla logica di business**: possibilità di definire requisiti condizionali e regole di convalida per il caso d’uso specifico
- **Familiarità del componente del modulo**: conoscenza dei tipi di campo (testo, numero, elenco a discesa), delle proprietà (obbligatorie, visibili, di sola lettura) e della struttura del modulo

**Facoltativo per utilizzo avanzato**:

- **Nozioni di base di JavaScript**: richieste solo per la creazione di funzioni personalizzate (tipi di dati, funzioni, sintassi di base)
- **Informazioni su JSON**: utile per la manipolazione di dati complessi e le integrazioni API

**Domande di valutazione**:

- Sei in grado di creare un modulo di base con input di testo e un pulsante di invio nell’editor universale?
- Sei a conoscenza di quando i campi devono essere obbligatori o facoltativi nel tuo contesto aziendale?
- Sei in grado di identificare gli elementi del modulo che richiedono visibilità condizionale nel caso d’uso?

+++

+++ Abilitare l’estensione editor di regole

**Importante**: per impostazione predefinita, l’estensione dell’editor di regole non è abilitata negli ambienti dell’editor universale.

**Passaggi di attivazione**:

1. Passa a [Extension Manager](/help/implementing/developing/extending/extension-manager.md) nel tuo ambiente AEM
2. Individua l’estensione “editor di regole” nell’elenco delle estensioni disponibili
3. Fai clic su **Abilita** e conferma l’attivazione
4. Attendi l’aggiornamento del sistema (potrebbero essere necessari 1-2 minuti)

**Verifica**:

- Dopo l’abilitazione, l’icona editor di regole viene visualizzata quando selezioni un componente del modulo: ![modifica regole](/help/forms/assets/edit-rules-icon.svg)

![Editor di regole dell’editor universale](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
Figura: l’icona editor di regole viene visualizzata quando selezioni i componenti del modulo

Per aprire l’editor di regole:

1. seleziona un componente del modulo nell’editor universale.
2. Fai clic sull’icona editor di regole.
3. L’editor di regole si apre in un pannello laterale.

![Interfaccia utente dell’editor di regole](/help/edge/docs/forms/assets/rule-editor-for-field.png)
Figura: interfaccia dell’editor di regole per la modifica delle regole del componente

>[!NOTE]
>
> In questo articolo, “componente del modulo” e “oggetto del modulo” si riferiscono agli stessi elementi (ad esempio, input, pulsanti, pannelli).

## Panoramica sull’interfaccia dell’editor di regole

![Interfaccia utente dell’editor di regole](/help/edge/docs/forms/assets/rule-editor-interface.png)
Figura: interfaccia dell’editor di regole completa con componenti numerati

- **Titolo del componente e tipo di regola**: conferma il componente selezionato e il tipo di regola attivo.
- **Pannello Funzioni e oggetti del modulo**:
   - Oggetti del modulo: vista gerarchica di campi e contenitori a cui fare riferimento nelle regole
   - Funzioni: helper incorporati di matematica, stringhe, data e convalida
- **Pulsante di attivazione/disattivazione del pannello**: mostra/nascondi il pannello oggetti e funzioni per aumentare l’area di lavoro
- **Generatore di regole visive**: compositore di regole a discesa con trascinamento
- **Controlli**: Fine (salva), Annulla (elimina). Prima di salvare, testa sempre le regole.

+++

+++ Gestione delle regole esistenti

Quando un componente dispone già delle regole, puoi:

- **Visualizzare**: visualizzare i riepiloghi e la logica della regola
- **Modificare**: modificare condizioni e azioni
- **Riordinare**: cambiare l’ordine di esecuzione (dall’alto verso il basso)
- **Abilitare/Disabilitare**: attivare/disattivare le regole per il test
- **Eliminare**: rimuovere le regole in modo sicuro

>[!TIP]
>
> Inserisci regole specifiche prima di quelle generali. L’esecuzione avviene dall’alto verso il basso.

+++

## Tipi di regole disponibili

Scegli il tipo di regola che corrisponde meglio all’intento.

+++ Logica condizionale

- **Quando**: regola primaria per un comportamento condizionale complesso (Condizione → Azione ± Altro)
- **Nascondi/Mostra**: controlla la visibilità in base a una condizione (divulgazione progressiva)
- **Abilita/Disabilita**: controlla se un campo è interattivo (ad esempio, disabilita Invia finché i campi obbligatori non sono validi)

+++

+++ Manipolazione dei dati

- **Imposta valore di**: compila automaticamente i valori (ad esempio, date, totali, copie)
- **Cancella valore di**: rimuovi dati quando cambiano le condizioni
- **Formato**: trasforma la formattazione di visualizzazione (valuta, telefono, data) senza modificare i valori memorizzati

+++

+++ Convalida

- **Convalida**: logica di convalida personalizzata, inclusi controlli tra campi diversi e regole aziendali

+++

+++ Calcolo

- **Espressione matematica**: calcolo dei valori in tempo reale (totali, imposte, rapporti)

+++

+++ Interfaccia utente

- **Imposta punto di interesse**: sposta il punto di interesse su un campo specifico (utilizza con moderazione)
- **Imposta proprietà**: modifica dinamicamente le proprietà del componente (segnaposto, opzioni, ecc.)

+++

+++ Controllo del modulo

- **Invia modulo**: invia il modulo a livello di programmazione (solo dopo il superamento delle convalide)
- **Ripristina modulo**: cancella e ripristina lo stato iniziale (conferma prima dell’utilizzo)
- **Salva modulo**: salva come bozza per un momento successivo (moduli lunghi, sessioni multiple)

+++

+++ Avanzate

- **Richiama servizio**: chiama servizi/API esterni (gestisci caricamento ed errori)
- **Aggiungi/Rimuovi istanza**: gestisci sezioni ripetibili (ad esempio, dipendenti, indirizzi)
- **Passa a**: inoltra ad altri moduli/pagine (mantieni i dati prima della navigazione)
- **Naviga tra i pannelli**: controlla la navigazione e il salto del passaggio della procedura guidata
- **Invia evento**: attiva eventi personalizzati per integrazioni o analisi

+++

## Tutorial dettagliato: creare un calcolatore fiscale avanzato

+++ Panoramica sul tutorial

Questo esempio illustra la visibilità condizionale e i calcoli automatici.

![Schermata dell’interfaccia dell’editor di regole che mostra la creazione di una regola condizionale con logica When-Then (Quando-Allora) per la visibilità dei campi modulo](/help/edge/docs/forms/assets/rule-editor-1.png)
Figura: modulo del calcolo fiscale con campi condizionali avanzati

Creerai un modulo che:

1. si adatta all’inserimento dell’utente mostrando i campi rilevanti
2. Calcola i valori in tempo reale
3. Convalida i dati per migliorare la precisione

+++

+++ Struttura del modulo

| Nome campo | Tipo | Scopo | Comportamento |
|-------------------------|---------------|--------------------------------|-----------------------------------------|
| Stipendio lordo | Inserimento numero | Reddito annuale dell’utente | Attivatori di logica condizionale |
| Detrazione aggiuntiva | Inserimento numero | Detrazioni supplementari (se ammissibili) | Visibile solo quando lo stipendio è > 50.000 dollari |
| Reddito Imponibile | Inserimento numero | Valore calcolato | Sola lettura, aggiornamenti in caso di modifica |
| Imposta a debito | Inserimento numero | Valore calcolato | Sola lettura, calcolato su base forfettaria |

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

1. **Aprire l’editor universale**:
   - Passa alla console AEM Sites, seleziona la pagina e fai clic su **Modifica**
   - Verifica che l’[editor universale](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=it) sia configurato correttamente

2. **Aggiungi componenti del modulo in questo ordine**:
   - Titolo (H2): “Modulo di calcolo delle imposte”
   - Inserimento numero: “stipendio lordo” (obbligatorio: Sì, segnaposto: “Inserisci stipendio annuale”)
   - Inserimento numero: “detrazione aggiuntiva” (obbligatorio: No, segnaposto: “Inserisci detrazioni aggiuntive”)
   - Inserimento numero: “reddito imponibile” (sola lettura: sì)
   - Inserimento numero: “Imposta a debito” (sola lettura: sì)
   - Pulsante Invia: “calcola imposta”

3. **Configurare le proprietà del campo iniziale**:
   - Nascondi “detrazione aggiuntiva” (set Visibile: no nel pannello Proprietà)
   - Imposta “reddito imponibile” e “imposta a debito” su Sola lettura: Sì

![Schermata di un modulo di calcolo delle imposte con campi di inserimento per stipendio lordo, stato civile e figli a carico, che illustra la struttura del modulo prima dell’applicazione delle regole](/help/edge/docs/forms/assets/rule-editor2.png)
Figura: struttura del modulo iniziale con componenti di base configurati

**Punti di controllo**: devi disporre di un modulo con tutti i campi obbligatori in cui “detrazione aggiuntiva” è nascosto e i campi calcolati sono di sola lettura.

+++

+++ Passaggio 2: aggiungere la regola di visibilità condizionale

**Obiettivo**: mostra il campo “detrazione aggiuntiva” solo quando lo stipendio lordo supera i 50.000 dollari.

1. **Seleziona il campo stipendio lordo** e fai clic sull’icona dell’editor delle regole ![Modifica regola](/help/forms/assets/edit-rules-icon.svg)
2. **Crea un nuovo ruolo**:
   - Fai clic su **Crea**.
   - Cambia il tipo di regola da “Imposta valore di” a **“Quando”**
3. **Configura la condizione**:
   - Seleziona **“è maggiore di”** dal menu a discesa
   - Immetti `50000` nel campo numerico
4. **Imposta l’azione Allora**:
   - Scegli **“Mostra”** dal menu a discesa Seleziona azione
   - Trascina o seleziona il campo **“detrazione aggiuntiva”** dagli oggetti del modulo
5. **Aggiungi l’azione Altro**:
   - Fai clic su **“Aggiungi la sezione Altro”**
   - Scegli **“Nascondi”** dal menu a discesa Seleziona azione
   - Seleziona campo **“detrazione aggiuntiva”**
6. **Salva la regola**: fai clic su **Fine**

>[!NOTE]
>
> Approccio alternativo: puoi ottenere lo stesso risultato creando una regola Mostra/Nascondi direttamente nel campo “detrazione aggiuntiva” invece di una regola Quando su “stipendio lordo”.

+++

+++ Passaggio 3: aggiungere regole di calcolo

**Obiettivo**: calcolare automaticamente “Reddito imponibile” e “Imposta a debito” in base all’inserimento dell’utente.

**Configura il calcolo del reddito imponibile**:

1. **Seleziona il campo “reddito imponibile”** e apri l’editor di regole
2. **Crea l’espressione matematica**:
   - “Fai clic su **Crea** 	 Seleziona **“Espressione matematica”**
   - Crea l’espressione: **stipendio lordo − detrazione aggiuntiva**
   - Trascina “Stipendio lordo” nel primo campo
   - Seleziona l’operatore **“meno”**
   - Trascina “Detrazione aggiuntiva” nel secondo campo
3. **Salva**: fai clic su **Fine**

**Configura il calcolo dell’imposta a debito**:

1. **Seleziona il campo “imposta a debito”** e apri l’editor di regole
2. **Crea l’espressione matematica**:
   - Fai clic su **Crea** → Seleziona **“Espressione matematica”**
   - Crea l’espressione: **Reddito imponibile × 10 ÷ 100**
   - Trascina “reddito imponibile” nel primo campo
   - Seleziona l’operatore **“Moltiplicato per”**
   - Inserisci `10` come numero
   - Fai clic su **“Estendi espressione”**
   - Seleziona l’operatore **“diviso per”**
   - Inserisci `100` come numero
3. **Salva**: fai clic su **Fine**

+++

+++ Passaggio 4: testare ill modulo

**Verifica l’implementazione sottoponendo a test il flusso completo**:

1. **Anteprima del modulo**: fai clic sulla modalità di anteprima nell’editor universale
2. **Testa la logica condizionale**:
   - Inserisci lo stipendio lordo = `30000` → “Detrazione aggiuntiva” deve rimanere nascosta
   - Inserisci lo stipendio lordo = `60000` → “detrazione aggiuntiva” deve essere visualizzata
3. **Calcoli del test**:
   - Con Stipendio lordo = `60000`, inserisci Detrazione aggiuntiva = `5000`
   - Verifica reddito imponibile = `55000` (60000 - 5000)
   - Verifica imposta a debito = `5500` (55000 × 10%)

![Anteprima del modulo](/help/edge/docs/forms/assets/rule-editor-form.png)
Figura: calcolatore di imposte completo di campi condizionali e calcoli automatici

**Criteri di successo**: il modulo deve mostrare/nascondere dinamicamente i campi e calcolare i valori in tempo reale durante la digitazione da parte degli utenti.


+++

## Avanzato: funzioni personalizzate

Per una logica di business complessa oltre le funzionalità incorporate, puoi creare funzioni JavaScript personalizzate che si integrano perfettamente con l’editor di regole.

+++ Quando utilizzare le funzioni personalizzate

**Scenari ideali per le funzioni personalizzate**:

- **Calcoli complessi**: i calcoli a più passaggi non sono facilmente espressi nella regola Espressione matematica
- **Convalide specifiche per l’azienda**: logica di convalida personalizzata specifica per l’organizzazione o il settore
- **Trasformazioni dati**: conversioni di formati, manipolazioni di stringhe o analisi dei dati
- **Integrazioni esterne**: chiamate alle API interne o a servizi di terze parti (con limitazioni)

**Vantaggi delle funzioni personalizzate**:

- **Riutilizzabilità**: scrittura singola, utilizzo in più moduli e regole
- **Manutenzione**: logica centralizzata più semplice da aggiornare ed eseguire il debug
- **Prestazioni**: esecuzione di JavaScript ottimizzata rispetto a catene di regole complesse
- **Flessibilità**: gestisci casi edge e scenari complessi non gestiti da regole standard

+++

+++ Creazione e implementazione di funzioni personalizzate

**Posizione dei file**: tutte le funzioni personalizzate devono essere definite in `/blocks/form/functions.js` nel progetto Edge Delivery Services.

**Flusso di lavoro di sviluppo**:

1. **Progettazione funzione**
   - Utilizza nomi di funzione descrittivi e orientati alle azioni
   - Definisci tipi di parametri chiari e valori restituiti
   - Gestisci casi edge e inserimenti non validi con criterio

2. **Implementazione**
   - Scrivi JavaScript pulito e ben commentato
   - Includi convalida dell’input e la gestione degli errori
   - Testa le funzioni in modo indipendente prima dell’integrazione

3. **Documentazione**
   - Aggiungi commenti JSDoc completi
   - Includi esempi di utilizzo e descrizioni dei parametri
   - Documenta eventuali limitazioni o dipendenze

4. **Distribuzione**
   - Esporta funzioni utilizzando esportazioni denominate
   - Distribuisci nell’archivio del progetto
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
Immagine: aggiunta di funzioni personalizzate al file functions.js

+++

+++ Utilizzo di funzioni personalizzate nell’editor di regole

**Passaggi dell’integrazione**:

1. **Aggiungere una funzione al progetto**
   - Crea o modifica `/blocks/form/functions.js` nel progetto
   - Includi la funzione nell’istruzione di esportazione

2. **Distribuisci e genera**
   - Eseguire il commit delle modifiche nell’archivio
   - Verifica il completamento del processo di compilazione
   - Concedi tempo per gli aggiornamenti alla cache CDN

3. **Accesso all’editor di regole**
   - Apri l’editor di regole per qualsiasi componente del modulo
   - Seleziona **&quot;Output funzione&quot;** nel menu a discesa **Seleziona azione**
   - Scegli la funzione personalizzata dall&#39;elenco delle funzioni disponibili
   - Configura i parametri della funzione utilizzando campi modulo o valori statici

4. **Test completo**
   - Visualizza l&#39;anteprima del modulo per verificare il comportamento della funzione
   - Test con varie combinazioni di input, inclusi casi limite
   - Verifica l’impatto delle prestazioni sul caricamento e sull’interazione dei moduli

![Funzione personalizzata nell&#39;editor di regole](/help/edge/docs/forms/assets/custom-function-rule-editor.png)
Figura: selezione e configurazione di funzioni personalizzate nell’interfaccia dell’editor di regole


**Best practice per l&#39;uso della funzione**

- **Gestione degli errori**: includi sempre il comportamento di fallback per gli errori di funzione
- **Prestazioni**: funzioni di profilo con volumi di dati realistici
- **Sicurezza**: convalida di tutti gli input per evitare vulnerabilità della sicurezza
- **Test**: crea test case che coprono casi normali ed edge

+++


### Importazioni statiche per funzioni personalizzate

L&#39;editor di regole dell&#39;editor universale supporta le importazioni statiche, consentendo di organizzare la logica riutilizzabile in più file e moduli. Invece di mantenere tutte le funzioni personalizzate in un unico file (/blocks/form/functions.js), puoi importare funzioni da altri moduli.
Esempio: importazione di funzioni da un file esterno
Considera la seguente struttura di cartelle:

```
      form
      ┣ commonLib
      ┃ ┗ functions.js
      ┣ rules
      ┃ ┗ _form.json
      ┣ form.js
      ┗ functions.js
```

È possibile importare le funzioni da `commonLib/functions.js` nel file `functions.js` principale come illustrato di seguito:

```
`import {days} from './commonLib/functions';
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in String format
 * @param {string} lastname in String format
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

// Export multiple functions for use in Rule Editor
export { getFullName, days};
```

### Organizzazione Di Funzioni Personalizzate In Diversi Forms

È possibile creare diversi set di funzioni in file o cartelle separati ed esportarli come richiesto:

- Se si desidera rendere disponibili determinate funzioni solo in moduli specifici, è possibile specificare il percorso del file delle funzioni nella configurazione del modulo.

- Se la casella di testo per il percorso viene lasciata vuota, per impostazione predefinita nell&#39;Editor regole vengono caricate le funzioni da `/blocks/form/functions.js`

![Funzione personalizzata in UE](/help/forms/assets/custom-function-in-ue.png){width=50%}

Nella schermata precedente, il percorso della funzione personalizzata viene aggiunto nella casella di testo Percorso funzione personalizzato. Le funzioni personalizzate per questo modulo sono caricate dal file specificato (`cc_function.js`).

Ciò consente flessibilità condividendo funzioni su più moduli o mantenendoli isolati per modulo.

## Best practice per lo sviluppo delle regole


+++ Ottimizzazione delle prestazioni

- Ridurre al minimo la complessità delle regole; suddividere la logica di grandi dimensioni in regole piccole e mirate
- Ordina le regole in base alla frequenza (prima le più comuni)
- Mantieni gestibili i set di regole per componente
- Preferisci funzioni personalizzate riutilizzabili rispetto alla logica di duplicazione

+++

+++ Esperienza utente

- Fornisci una convalida chiara e un feedback in linea
- Evita di alterare le modifiche visive; usa mostra/nascondi attentamente
- Test tra dispositivi e layout

+++

+++ Igiene dello sviluppo

- Test con casi limite e valori noti
- Verificare su più browser
- Intento del documento alla base di regole complesse, non solo di procedura
- Gestire un inventario di regole per i moduli di grandi dimensioni
- Utilizzare nomi coerenti per componenti e regole
- Funzioni personalizzate della versione e test in ambienti non di produzione

+++

## Risoluzione dei problemi comuni


+++ Le regole non vengono attivate

- Verificare i nomi e i riferimenti dei componenti
- Controllare l’ordine di esecuzione (dall’alto verso il basso)
- Convalidare condizioni con valori noti
- Ispezionare la console del browser per individuare eventuali errori di blocco

+++

+++ Comportamento non corretto

- Rivedere operatori e raggruppamenti (AND/OR)
- Testare i singoli frammenti di espressione
- Confermare tipi di dati (numeri e stringhe)

+++

+++ Problemi relativi alle prestazioni

- Semplificare le condizioni profondamente nidificate
- Funzioni personalizzate del profilo
- Ridurre a icona le chiamate esterne all’interno delle regole
- Utilizzare selettori e riferimenti specifici

+++

+++ Problemi relativi alla funzione personalizzata

- Confermare il percorso file: `/blocks/form/functions.js`
- Assicurarsi che le esportazioni denominate siano corrette
- Confermare che la build includa le modifiche
- Cancellare la cache del browser dopo l’implementazione
- Convalidare i tipi di parametri e la gestione degli errori

+++

+++ Integrazione editor universale

- Confermare che l’estensione editor di regole sia abilitata
- Selezionare un componente supportato
- Utilizzare un browser supportato (Chrome, Firefox, Safari)
- Verificare di disporre delle autorizzazioni necessarie

## Limitazioni importanti

>[!IMPORTANT]
>
> Vincoli di funzione personalizzata:
>
> - Importazioni statiche/dinamiche non supportate
> - Tutta la logica deve risiedere in `/blocks/form/functions.js`
> - Le funzioni devono essere sincrone (non asincrone/in attesa or promesse)
> - L’accesso all’API del browser è limitato

>[!WARNING]
>
> Considerazioni sulla produzione:
>
> - Eseguire il test completo in fase di staging
> - Monitorare le prestazioni dopo l’implementazione
> - Disporre di una pianificazione di rollback per i problemi relativi alle regole
> - Prendere in considerazione le reti lente e i dispositivi a basse specifiche

## Riepilogo

L’editor di regole dell’editor universale trasforma i moduli statici in esperienze intelligenti e reattive che si adattano all’input dell’utente in tempo reale. Sfruttando la logica condizionale, i calcoli automatizzati e le regole aziendali personalizzate, puoi creare flussi di lavoro di moduli sofisticati senza scrivere il codice dell’applicazione.

**Funzionalità chiave acquisite**:

- **Logica condizionale**: mostra e nascondi i campi in base all’input dell’utente per creare esperienze mirate e rilevanti
- **Calcoli dinamici**: calcola automaticamente i valori (imposte, totali, tassi) durante l’interazione degli utenti con il modulo
- **Convalida dei dati**: implementa la convalida in tempo reale con messaggi di feedback chiari e attuabili
- **Funzioni personalizzate**: estendi le funzionalità con JavaScript per logiche di business e integrazioni complesse
- **Ottimizzazione delle prestazioni**: applica le best practice per uno sviluppo delle regole gestibile ed efficiente

**Valore consegnato**:

- **Esperienza utente migliorata**: riduci il carico cognitivo con la divulgazione progressiva e i flussi di moduli intelligenti
- **Errori ridotti**: impedisci invii non validi tramite convalida in tempo reale e input guidato
- **Maggiore efficienza**: automatizza i calcoli e l’immissione dei dati per ridurre al minimo il lavoro dell’utente
- **Soluzioni gestibili**: crea regole riutilizzabili e ben documentate che siano scalabili all’interno della tua organizzazione

**Impatto aziendale**:

I Moduli diventano uno strumento potente per la raccolta di dati, la qualificazione dei lead e il coinvolgimento degli utenti. L’editor di regole consente agli autori non tecnici di implementare una logica di business sofisticata, riducendo i costi di sviluppo e migliorando al contempo i tassi di completamento dei moduli e la qualità dei dati.

+++

## Passaggi successivi

**Percorso di apprendimento consigliato**:

1. **Inizia con le nozioni di base**: crea semplici regole mostra/nascondi per comprendere i concetti di base
2. **Esercitati con i tutorial**: utilizza l’esempio del calcolatore delle imposte come base per i moduli
3. **Espandi gradualmente**: aggiungi espressioni matematiche e regole di convalida man mano che la tua sicurezza cresce
4. **Implementa funzioni personalizzate**: sviluppa funzioni JavaScript per esigenze aziendali specifiche
5. **Ottimizza e scala**: applica le best practice per le prestazioni e mantieni la documentazione sulle regole

**Risorse aggiuntive**:

- [Documentazione dell’editor universale](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=it) per un contesto più ampio
- [Guida di Extension Manager](/help/implementing/developing/extending/extension-manager.md) per abilitare funzionalità aggiuntive
- [Moduli Edge Delivery Services](/help/edge/docs/forms/overview.md) per indicazioni complete sullo sviluppo di moduli

