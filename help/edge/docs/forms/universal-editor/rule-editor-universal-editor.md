---
title: Editor di regole per Dynamic Forms nell’editor universale
description: Creare moduli dinamici e intelligenti tramite l’Editor di regole nell’Editor universale. Aggiungi logica condizionale, calcoli e comportamenti interattivi senza codifica.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: ccfb85da187e828b5f7e8b1a8bae3f483209368d
workflow-type: tm+mt
source-wordcount: '3597'
ht-degree: 23%

---


# Editor di regole per Dynamic Forms nell’editor universale

L&#39;Editor di regole di Universal Editor consente di creare moduli intelligenti e dinamici che rispondono in tempo reale agli input dell&#39;utente. Puoi trasformare i moduli statici in esperienze interattive con visibilità dei campi condizionale, calcoli automatizzati e logica di business complessa, il tutto senza scrivere codice.


## Che cosa imparerai

Al termine di questa guida:

- Comprendere il funzionamento delle regole e quando utilizzare tipi di regole diversi
- Abilitare e accedere all’editor di regole nell’editor universale
- Creare una logica condizionale per visualizzare o nascondere i campi modulo in modo dinamico
- Implementazione di calcoli automatizzati e convalida dei dati
- Creare funzioni personalizzate per regole aziendali complesse
- Applicare le best practice per ottenere prestazioni ottimali dei moduli

## Perché utilizzare l’editor di regole?

**Trasforma Forms statico in esperienze avanzate:**

- **Logica condizionale**: mostra i campi rilevanti in base alle selezioni effettuate dall&#39;utente
- **Calcoli dinamici**: calcola automaticamente i valori come tipi di utenti
- **Convalida dati**: fornire feedback in tempo reale ed evitare errori
- **UX migliorata**: riduzione della complessità dei moduli e guida gli utenti attraverso i flussi logici
- **Non è richiesta alcuna codifica**: interfaccia visiva accessibile ai non sviluppatori

**Casi d&#39;uso comuni:**

- Moduli di calcolo delle imposte con detrazioni condizionali
- Procedure guidate in più passaggi con percorsi di diramazione
- Moduli assicurativi con calcoli dei tassi
- Moduli di sondaggio con domande condizionali
- Moduli e-commerce con prezzi dinamici

## Funzionamento delle regole

Le regole sono istruzioni automatizzate che rendono i moduli intelligenti e reattivi. Esse specificano cosa dovrebbe accadere quando vengono soddisfatte determinate condizioni.

### **Componenti regola**

**Condizione**: un test logico che restituisce true o false.

- &quot;Il reddito dell&#39;utente è superiore a 50.000 dollari?&quot;
- &quot;L&#39;utente ha selezionato &#39;Sì&#39; per la copertura assicurativa?&quot;
- &quot;Il campo modulo è vuoto?&quot;

**Azione**: risultato che si verifica quando viene soddisfatta la condizione.

- Mostrare o nascondere i campi modulo
- Calcola automaticamente i valori
- Visualizza messaggi di convalida
- Abilitare o disabilitare i componenti

### **Modelli logici regola**

**1. Condizione-Azione (When-Then)**

```
WHEN gross salary > 50000
THEN show "Additional Deduction" field
```

*Ideale per:* Visibilità campo condizionale, contenuto dinamico

**2. Condizione-Azione (Set-If)**

```
SET taxable income = gross salary - deductions
IF deductions are applicable
```

*Ottimo per:* Calcoli, trasformazioni dati

**3. Azione-Condizione-Alternativa (If-Then-Else)**

```
IF income > 50000
THEN show "High Income" fields
ELSE show "Standard Income" fields
```

*Ideale per:* logica di diramazione, opzioni reciprocamente esclusive

### **Esempio reale**

**Scenario**: modulo di calcolo delle imposte

- **Condizione**: &quot;Lo stipendio lordo supera i 50.000 dollari&quot;
- **Azione primaria**: mostra campo &quot;Detrazione aggiuntiva&quot;
- **Azione alternativa**: nasconde il campo &quot;Detrazione aggiuntiva&quot;
- **Risultato**: gli utenti visualizzano solo i campi pertinenti in base al loro livello di reddito

## Prerequisiti

Prima di iniziare a utilizzare l’editor di regole, assicurati di disporre dei seguenti elementi:

### **Requisiti di accesso**

- Accesso di authoring a **AEM as a Cloud Service**
- **Universal Editor** con estensione editor di regole abilitata
- Autorizzazioni di modifica dei moduli nell’ambiente AEM

### **Requisiti tecnici**

- **Conoscenza di base sulla progettazione dei moduli**: familiarità con i componenti del modulo e le relative proprietà
- **Familiarità con la logica di business**: possibilità di definire i requisiti condizionali
- **Conoscenza di base di JavaScript** (richiesta solo per le funzioni personalizzate)

### **Abilita estensione editor regole**

Per impostazione predefinita, l’estensione dell’editor di regole non è abilitata nell’editor universale. È possibile abilitarlo da [Extension Manager](/help/implementing/developing/extending/extension-manager.md).

**Dopo aver abilitato l&#39;estensione:**
Quando selezioni i componenti del modulo, nell&#39;angolo superiore destro viene visualizzata l&#39;icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg).

![Editor regole dell&#39;editor universale](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
*Figura: l&#39;icona Editor regole viene visualizzata quando si selezionano i componenti del modulo*

**Per accedere all&#39;editor di regole:**

1. Seleziona un componente modulo nell’Editor universale.
2. Fai clic sull&#39;icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg) visualizzata.
3. L’interfaccia dell’editor delle regole si apre in un nuovo pannello.

![Interfaccia utente dell&#39;editor di regole](/help/edge/docs/forms/assets/rule-editor-for-field.png)
*Figura: interfaccia dell&#39;editor di regole per la modifica delle regole dei componenti*

>[!NOTE]
>
> In questo articolo, &quot;componente modulo&quot; e &quot;oggetto modulo&quot; si riferiscono agli stessi elementi (come campi di input, pulsanti, pannelli, ecc.).

## Panoramica dell’interfaccia dell’editor di regole

L’editor di regole offre un’interfaccia visiva intuitiva per la creazione e la gestione delle regole:

![Interfaccia utente editor regole](/help/edge/docs/forms/assets/rule-editor-interface.png)
*Figura: interfaccia completa dell&#39;editor di regole con componenti numerati*

### **Componenti interfaccia**

**1. Titolo componente e tipo di regola**

- **Scopo**: visualizza il nome del componente selezionato e il tipo di regola corrente.
- **Esempio**: &quot;Inserisci stipendio lordo&quot; (input di testo) con la regola &quot;Quando&quot; selezionata.
- **Suggerimento**: confermare sempre che si sta modificando il componente corretto.

**2. Pannello Funzioni e oggetti modulo**

- **Scheda Oggetti modulo**: fornisce una visualizzazione gerarchica di tutti i componenti del modulo.
   - Utilizza per: riferimento ad altri campi nelle regole.
   - Navigazione: espandi o comprimi per individuare componenti specifici.
- **Scheda Funzioni**: contiene funzioni matematiche e logiche incorporate.
   - Utilizzare per: esecuzione di calcoli complessi e manipolazioni di dati.
   - Categorie: funzioni Matematica, Stringa, Data e Convalida.

**3. Pulsante di attivazione/disattivazione pannello**

- **Scopo**: mostra o nasconde il pannello oggetti e funzioni.
- **Suggerimento**: disattiva il pannello per aumentare l&#39;area di lavoro di modifica delle regole.
- **Scelta rapida da tastiera**: utile quando si lavora con regole complesse.

**4. Generatore di regole visive**

- **Scopo**: area principale per la costruzione della logica delle regole.
- **Funzionalità**: interfaccia di trascinamento e selettori a discesa.
- **Flusso di lavoro**: seleziona il tipo di regola → Definisci condizioni → Imposta azioni.

**5. Pulsanti di controllo**

- **Fine**: salva la regola e chiude l&#39;editor.
- **Annulla**: ignora le modifiche e chiude l&#39;editor senza salvarlo.
- **Suggerimento**: verifica sempre le regole prima di fare clic su Fine.

### **Gestione regole**

Quando apri l’Editor regole per un componente che dispone già di regole:

![mostra le regole disponibili dell&#39;oggetto modulo](/help/edge/docs/forms/assets/rule-editor15.png)
*Figura: Gestione delle regole esistenti per un componente modulo*

**Azioni disponibili:**

- **Visualizza**: rivedi i riepiloghi e la logica delle regole.
- **Modifica**: modifica le condizioni o azioni della regola esistenti.
- **Riordina**: cambia l&#39;ordine di esecuzione delle regole (le regole vengono eseguite dall&#39;alto verso il basso).
- **Attiva/Disattiva**: attiva o disattiva temporaneamente le regole a scopo di test.
- **Elimina**: rimuovere definitivamente le regole.

>[!TIP]
>
> **Importanza ordine di esecuzione regola**: le regole vengono eseguite dall&#39;alto verso il basso. Posizionare condizioni più specifiche prima di quelle generali.

## Tipi di regole disponibili

L’Editor regole offre un set completo di tipi di regole organizzati per funzionalità. Seleziona il tipo appropriato in base al caso d’uso specifico:

### **Regole per la logica condizionale**

**Quando**

- **Scopo**: funge da regola condizionale principale per l&#39;implementazione di logica complessa.
- **Caso d&#39;uso**: ad esempio, &quot;Quando l&#39;utente seleziona &#39;Sposato&#39;, mostra i campi relativi alle informazioni sul coniuge.&quot;
- **Schema logico**: Condizione → Azione (con un&#39;azione alternativa facoltativa)

**Nascondi/Mostra**

- **Scopo**: controlla la visibilità del campo in base alle condizioni specificate.
- **Caso d&#39;uso**: nascondi sezioni irrilevanti o abilita la divulgazione progressiva.
- **Best practice**: utilizza per creare un&#39;esperienza utente pulita e mirata.

**Attiva/Disattiva**

- **Scopo**: controlla se un campo può essere interagito con, in base alle condizioni.
- **Caso d&#39;uso**: disabilitare il pulsante di invio fino al completamento di tutti i campi obbligatori.
- **Best practice**: fornisci agli utenti un feedback visivo chiaro.

### **Regole di manipolazione dei dati**

**Imposta Valore Di**

- **Scopo**: compila automaticamente i valori dei campi.
- **Caso d&#39;uso**: imposta la data odierna, calcola i totali o copia i valori tra i campi.
- **Best practice**: utilizza per ridurre il carico di lavoro degli utenti e garantire precisione.

**Cancella Valore Di**

- **Scopo**: rimuove i dati dai campi quando cambiano le condizioni.
- **Caso d&#39;uso**: cancella i campi dipendenti quando cambia una selezione padre.
- **Best practice**: mantieni l&#39;integrità dei dati e impedisci valori orfani.

**Formato**

- **Scopo**: trasforma la visualizzazione dei valori.
- **Caso d&#39;uso**: formattazione valuta, numeri di telefono o date.
- **Best practice**: migliora la leggibilità senza modificare i dati sottostanti.

### **Regole di convalida**

**Convalida**

- **Scopo**: implementa una logica di convalida personalizzata.
- **Caso d&#39;uso**: applicazione di regole di business complesse o convalida tra campi.
- **Best practice**: fornisci messaggi di errore chiari e actionable.

### **Regole di calcolo**

**Espressione matematica**

- **Scopo**: esegue calcoli automatizzati.
- **Caso d&#39;uso**: calcoli fiscali, totali o percentuali.
- **Best practice**: aggiorna i calcoli in tempo reale durante la digitazione da parte degli utenti.

### **Regole interfaccia utente**

**Imposta stato attivo**

- **Scopo**: indirizza l&#39;attenzione dell&#39;utente a campi specifici.
- **Caso d&#39;uso**: concentrarsi sui campi di errore o guidare gli utenti attraverso i passaggi della procedura guidata.
- **Best practice**: utilizza con moderazione per evitare di interrompere il flusso dell&#39;utente.

**Imposta proprietà**

- **Scopo**: modifica dinamicamente le proprietà del componente.
- **Caso d&#39;uso**: modifica il testo segnaposto o le opzioni di modifica in un elenco a discesa.
- **Best practice**: migliora l&#39;esperienza utente con modifiche contestuali.

### **Regole di controllo modulo**

**Invia modulo**

- **Scopo**: attiva l&#39;invio dei moduli a livello di programmazione.
- **Caso d&#39;uso**: invio automatico dopo che sono state soddisfatte determinate condizioni.
- **Best practice**: convalida sempre il modulo prima dell&#39;invio.

**Reimposta modulo**

- **Scopo**: cancella tutti i dati del modulo e ripristina lo stato iniziale del modulo.
- **Caso d&#39;uso**: funzionalità &quot;Ricomincia&quot;.
- **Best practice**: conferma l&#39;azione con l&#39;utente prima di reimpostare.

**Salva modulo**

- **Scopo**: salva il modulo come bozza per un successivo completamento.
- **Caso d&#39;uso**: utile per moduli lunghi o flussi di lavoro con più sessioni.
- **Best practice**: fornisci un feedback chiaro sullo stato di salvataggio.

### **Regole avanzate**

**Richiama servizio**

- **Scopo**: chiama API o servizi esterni.
- **Caso d&#39;uso**: ricerca di indirizzi, convalida in tempo reale o arricchimento dei dati.
- **Best practice**: gestisci in modo appropriato gli stati di caricamento e gli scenari di errore.

**Aggiungi/Rimuovi istanza**

- **Scopo**: gestione dinamica delle sezioni ripetibili.
- **Caso d&#39;uso**: aggiungere membri della famiglia o più indirizzi.
- **Best practice**: fornisci controlli chiari per l&#39;aggiunta o la rimozione di istanze.

**Accedi A**

- **Scopo**: reindirizza gli utenti ad altri moduli o pagine.
- **Caso d&#39;uso**: flussi di lavoro multimodulo o routing condizionale.
- **Best practice**: mantieni i dati del modulo prima della navigazione.

**Naviga Tra I Pannelli**

- **Scopo**: controlla la navigazione nei moduli in stile procedura guidata.
- **Caso d&#39;uso**: moduli con più passaggi o passaggio condizionale ignorato.
- **Best practice**: visualizza indicatori di avanzamento chiari.

**Evento di invio**

- **Scopo**: attiva eventi personalizzati per integrazioni avanzate.
- **Caso d&#39;uso**: tracciamento di Analytics o integrazioni di terze parti.
- **Best practice**: da utilizzare solo per le azioni non bloccanti.


## Tutorial dettagliato: creazione di un calcolatore di imposta intelligente

In questa sezione viene fornito un esempio pratico per illustrare le funzionalità dell&#39;editor di regole. Nell&#39;esempio viene illustrato come creare un modulo di calcolo delle imposte che utilizza la logica condizionale e i calcoli automatizzati.

![Schermata dell&#39;interfaccia dell&#39;editor di regole che mostra la creazione di una regola condizionale con logica When-Then per la visibilità dei campi modulo](/help/edge/docs/forms/assets/rule-editor-1.png)
*Figura: Modulo di calcolo imposte con campi condizionali intelligenti*

### **Panoramica del tutorial**

In questa esercitazione verrà creato un modulo che:

1. **Si adatta all&#39;input dell&#39;utente**: visualizza i campi pertinenti in base al livello di reddito.
2. **Calcola automaticamente**: calcola la passività fiscale in tempo reale.
3. **Convalida dei dati**: garantisce calcoli accurati e l&#39;immissione dei dati.

### **Struttura modulo**

| Nome campo | Tipo | Scopo | Comportamento |
|------------|------|---------|----------|
| **Stipendio lordo** | Inserimento numero | L&#39;utente immette il reddito annuale | Attiva la logica condizionale |
| **Detrazione aggiuntiva** | Inserimento numero | Detrazioni supplementari (se del caso) | Visualizza quando lo stipendio è > $50.000 |
| **Reddito imponibile** | Inserimento numero | Calcolato automaticamente | Aggiornamenti sulle modifiche di input |
| **Imposta dovuta** | Inserimento numero | Importo imposta finale | Calcola a una percentuale del 10% |

### **Logica aziendale da implementare**

**Regola 1: Visualizzazione Campo Condizionale**

```
WHEN Gross Salary > 50,000
THEN Show "Additional Deduction" field
ELSE Hide "Additional Deduction" field
```

**Regola 2: Calcolo reddito imponibile**

```
SET Taxable Income = Gross Salary - Additional Deduction
(When Additional Deduction is applicable)
```

**Regola 3: Calcolo delle imposte**

```
SET Tax Payable = Taxable Income × 10%
(Simplified flat rate for demonstration)
```

### **Passaggi di implementazione**

Per creare il modulo fiscale intelligente, segui la procedura riportata di seguito.



+++ 1: Creare il modulo Foundation

**Obiettivo**: creare la struttura del modulo di base con tutti i componenti richiesti

Per creare il modulo di calcolo delle imposte in Universal Editor:

1. **Apri editor universale**
   - Passa alla console AEM Sites
   - Selezionare la pagina in cui si desidera aggiungere il modulo
   - Fai clic su **Modifica** per aprire Editor universale

2. **Aggiungi componenti modulo**

   Aggiungi questi componenti nell’ordine:

   | Componente | Tipo | Etichetta | Impostazioni |
   |-----------|------|-------|----------|
   | Titolo | Titolo | &quot;Modulo di calcolo imposte&quot; | Livello di intestazione H2 |
   | Inserimento numero | Inserimento numero | &quot;Stipendio lordo&quot; | Obbligatorio: sì, segnaposto: &quot;Inserire lo stipendio annuale&quot; |
   | Inserimento numero | Inserimento numero | &quot;Detrazione aggiuntiva&quot; | Obbligatorio: no, segnaposto: &quot;Inserire detrazioni aggiuntive&quot; |
   | Inserimento numero | Inserimento numero | &quot;Reddito Imponibile&quot; | Obbligatorio: no, sola lettura: sì |
   | Inserimento numero | Inserimento numero | &quot;Imposta da pagare&quot; | Obbligatorio: no, sola lettura: sì |
   | Pulsante Invia | Invia | &quot;Calcola imposta&quot; | Tipo: invia |

3. **Configura impostazioni iniziali**

   - **Nascondi il campo Detrazione aggiuntiva**:
      - Seleziona il componente &quot;Detrazione aggiuntiva&quot;
      - Nel pannello Proprietà, imposta **Visible** su **No**
      - Questo campo verrà visualizzato in modo condizionale in base alle regole

   - **Rendi i campi calcolati di sola lettura**:
      - Selezionare i campi &quot;Reddito imponibile&quot; e &quot;Imposta da pagare&quot;
      - Imposta **Sola lettura** su **Sì** nelle proprietà

     ![Schermata di un modulo di calcolo delle imposte con campi di input per lo stipendio lordo, lo stato civile e i figli a carico, che illustra la struttura del modulo prima che le regole siano applicate](/help/edge/docs/forms/assets/rule-editor2.png)
     *Figura: struttura del modulo iniziale con componenti di base configurati*

**Checkpoint**: è ora necessario disporre di un modulo con tutti i campi obbligatori, in cui &quot;Detrazione aggiuntiva&quot; è nascosto e i campi calcolati sono di sola lettura.

+++

+++ &#x200B;2. Aggiungere una regola condizionale per un campo modulo

Dopo aver creato il modulo, scrivi la prima regola per visualizzare il campo `Additional Deduction` solo se lo stipendio lordo supera i 50.000 dollari. Per aggiungere una regola condizionale:

1. Apri un modulo nell’editor universale per la modifica e seleziona il campo **[!UICONTROL Stipendio lordo]** nella struttura contenuto, quindi seleziona ![edit-rules](/help/forms/assets/edit-rules-icon.svg). In alternativa, puoi selezionare il campo **[!UICONTROL Stipendio lordo]** direttamente dal riquadro **[!UICONTROL Oggetto Forms]**.
   ![Esempio di editor di regole1](/help/edge/docs/forms/assets/rule-editor3.png)
Viene visualizzata l’interfaccia dell’editor di regole visivo.
1. Fai clic su **[!UICONTROL Crea]** per creare le regole.
   ![Esempio di editor di regole2](/help/edge/docs/forms/assets/rule-editor4.png)
Per impostazione predefinita, è selezionato il tipo di regola `Set Value Of`. Sebbene non sia possibile cambiare o modificare l’oggetto selezionato, è possibile utilizzare l’elenco a discesa delle regole per selezionare un altro tipo di regola.\
   ![Esempio di editor di regole3](/help/edge/docs/forms/assets/rule-editor5.png)
1. Apri l’elenco a discesa Tipo di regola e seleziona il tipo di regola **[!UICONTROL Quando]**.
   ![Esempio di editor di regole4](/help/edge/docs/forms/assets/rule-editor6.png)
1. Seleziona l’elenco a discesa **[!UICONTROL Seleziona stato]** e seleziona **[!UICONTROL è maggiore di]**. Viene visualizzato il campo **[!UICONTROL Immetti un numero]**.
   ![Esempio di editor di regole5](/help/edge/docs/forms/assets/rule-editor7.png)
1. Immetti `50000` nel campo **[!UICONTROL Immetti un numero]** nella regola.
   ![Esempio di editor di regole6](/help/edge/docs/forms/assets/rule-editor8.png)
La condizione è stata definita come `When Gross Salary is greater than 50000`. Definisci quindi l’azione da eseguire se la condizione è `True`.
1. Nell’istruzione `Then`, seleziona **[!UICONTROL Mostra]** dal menu a discesa **[!UICONTROL Seleziona azione]**.
   ![Esempio di editor di regole7](/help/edge/docs/forms/assets/rule-editor9.png)
1. Trascina il campo **[!UICONTROL Detrazione aggiuntiva]** dalla scheda Oggetti modulo del campo **[!UICONTROL Rilascia oggetto o seleziona qui]**. In alternativa, seleziona il campo **[!UICONTROL Rilascia oggetto o seleziona qui]** e seleziona il campo **[!UICONTROL Detrazione aggiuntiva]** dal menu a comparsa, in cui sono elencati tutti gli oggetti modulo nel modulo.
   ![Esempio di editor di regole8](/help/edge/docs/forms/assets/rule-editor10.png)
1. Fai clic su **[!UICONTROL Aggiungi altra sezione]** per aggiungere un’altra condizione per il campo **[!UICONTROL Stipendio lordo]**, nel caso in cui sia immesso uno stipendio inferiore a `50000`.
   ![Esempio di editor di regole9](/help/edge/docs/forms/assets/rule-editor11.png)
1. Seleziona **[!UICONTROL Nascondi]** dal menu a discesa **[!UICONTROL Seleziona azione]** nell’istruzione `Else`.
   ![Esempio di editor di regole10](/help/edge/docs/forms/assets/rule-editor12.png)
1. Trascina il campo **[!UICONTROL Detrazione aggiuntiva]** dalla scheda Oggetti modulo nel campo **[!UICONTROL Rilascia oggetto o seleziona qui]**. In alternativa, seleziona il campo **[!UICONTROL Rilascia oggetto o seleziona qui]** e seleziona il campo **[!UICONTROL Detrazione aggiuntiva]** dal menu a comparsa, in cui sono elencati tutti gli oggetti modulo nel modulo.
   ![Editor di regole, esempio 11](/help/edge/docs/forms/assets/rule-editor13.png)
1. Per salvare la regola, fai clic su **[!UICONTROL Fine]**.
La regola viene visualizzata nell’editor di regole nel modo seguente.
   ![Editor di regole, esempio 12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> In alternativa, per implementare lo stesso comportamento, è possibile scrivere una regola Mostra nel campo Detrazione aggiuntiva, anziché una regola Quando nel campo Stipendio lordo.

+++

+++ &#x200B;3. Aggiungere regole di calcolo per i campi modulo

Scrivi quindi una regola per calcolare il `Taxable Income`, che è la differenza tra `Gross Salary` e `Additional Deduction` (se applicabile). Per aggiungere la regola di calcolo nel campo **[!UICONTROL Reddito imponibile]**, esegui i seguenti passaggi:

1. In modalità di authoring, seleziona il campo **[!UICONTROL Reddito imponibile]** e quindi l’icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg). In alternativa, puoi selezionare il campo **[!UICONTROL Reddito imponibile]** direttamente dal riquadro **[!UICONTROL Oggetto Forms]**.
1. Quindi, seleziona **[!UICONTROL Crea]** per creare la regola.
   ![Editor di regole, esempio 13](/help/edge/docs/forms/assets/rule-editor16.png)
1. Seleziona **[!UICONTROL Seleziona opzione]** e scegli **[!UICONTROL Espressione matematica]**. Si apre un campo in cui scrivere espressioni matematiche.
   ![Editor di regole, esempio 14](/help/edge/docs/forms/assets/rule-editor17.png)

1. Nel campo per le espressioni matematiche:

   - Seleziona o trascina dalla scheda Oggetto modulo il campo **[!UICONTROL Stipendio lordo]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   - Seleziona **[!UICONTROL Meno]** dal campo **[!UICONTROL Seleziona operatore]**.

   - Seleziona o trascina dalla scheda Oggetto modulo il campo **[!UICONTROL Detrazione aggiuntiva]** nell’altro campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.
     ![Editor di regole, esempio 15](/help/edge/docs/forms/assets/rule-editor18.png)

1. Per salvare la regola, fai clic su **[!UICONTROL Fine]**.

   Aggiungi ora una regola per il campo `Tax Payable `, determinata moltiplicando il reddito imponibile per l’aliquota fiscale. Per semplicità, supponiamo un’aliquota fissa di `10%`.

1. In modalità di authoring, seleziona il campo **[!UICONTROL Imposta dovuta]** e seleziona l’icona ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Successivamente, seleziona **[!UICONTROL Crea]** per creare le regole.
   ![Editor di regole, esempio 16](/help/edge/docs/forms/assets/rule-editor19.png)
1. Seleziona **[!UICONTROL Seleziona opzione]** e seleziona **[!UICONTROL Espressione matematica]**. Si apre un campo in cui scrivere espressioni matematiche.
   ![Editor di regole, esempio 17](/help/edge/docs/forms/assets/rule-editor20.png)
1. Nel campo per le espressioni matematiche:

   - Seleziona o trascina dalla scheda Oggetto modulo il campo **[!UICONTROL Reddito imponibile]** nel primo campo **[!UICONTROL Rilascia oggetto o seleziona qui]**.

   - Seleziona **[!UICONTROL Moltiplicato per]** dal campo **[!UICONTROL Seleziona operatore]**.

   - Seleziona **Numero** dal campo **[!UICONTROL Seleziona opzione]** e immetti il valore `10` nel campo **[!UICONTROL Immetti un numero]**.
     ![Editor di regole, esempio 18](/help/edge/docs/forms/assets/rule-editor21.png)
1. Quindi, seleziona nell’area evidenziata intorno al campo espressione e seleziona **[!UICONTROL Estendi espressione]**.
   ![Editor di regole, esempio 19](/help/edge/docs/forms/assets/rule-editor22.png)
1. Nel campo espressione estesa, seleziona **[!UICONTROL diviso per]** dal campo **[!UICONTROL Seleziona operatore]** e **[!UICONTROL Numero]** dal campo **[!UICONTROL Seleziona opzione]**. Quindi, specifica `100` nel campo Numero.
   ![Editor di regole, esempio 20](/help/edge/docs/forms/assets/rule-editor23.png)
1. Per salvare la regola, seleziona **[!UICONTROL Fine]**.

+++

+++ &#x200B;4. Visualizzare l’anteprima di un modulo

Ora, quando visualizzi l’anteprima del modulo e immetti come **Stipendio lordo** `60,000`, viene visualizzato il campo **Detrazione aggiuntiva** e vengono calcolati di conseguenza il **Reddito imponibile** e l’**Imposta dovuta**.

![Visualizzare l’anteprima di un modulo](/help/edge/docs/forms/assets/rule-editor-form.png)

+++

Oltre alle funzioni incorporate come Somma e Media, puoi creare funzioni personalizzate per implementare logiche di business complesse personalizzate in base alle tue esigenze.

## Avanzate: funzioni personalizzate

**Quando utilizzare le funzioni personalizzate:**

- Per calcoli complessi che vanno oltre le funzionalità delle funzioni integrate
- Per implementare regole di convalida specifiche per l&#39;azienda
- Per la trasformazione e la formattazione dei dati
- Per l’integrazione con sistemi o API esterni

**Vantaggi:**

- **Riutilizzabilità**: scrivere la funzione una sola volta e utilizzarla in più moduli e regole
- **Manutenzione**: logica centralizzata facile da aggiornare
- **Prestazioni**: esecuzione JavaScript ottimizzata
- **Flessibilità**: possibilità di gestire scenari complessi non gestiti da regole standard

### **Creazione di funzioni personalizzate**

**Posizione file**: `/blocks/form/functions.js` nel progetto AEM

**Flusso di lavoro di sviluppo:**

1. **Dichiarazione funzione**
   - Definire nomi e parametri di funzioni chiari e descrittivi
   - Utilizzare nomi che indicano lo scopo della funzione
   - Parametri del documento e tipi restituiti

2. **Implementazione logica**
   - Scrittura di codice JavaScript pulito ed efficiente
   - Gestire casi edge e scenari di errore
   - Segui le best practice di codifica

3. **Esportazione funzione**
   - Esporta funzioni per renderle disponibili nell’Editor di regole
   - Utilizzare esportazioni denominate per una migliore organizzazione
   - Test delle funzioni prima della distribuzione

4. **documentazione**
   - Aggiungere commenti JSDoc per la documentazione della funzione
   - Includi esempi di utilizzo
   - Specificare i tipi di parametri e i valori restituiti

L&#39;esempio seguente illustra due funzioni personalizzate: `getFullName` e `days`.

```JavaScript
/**
 - Get Full Name
 - @name getFullName Concats first name and last name
 - @param {string} firstname in Stringformat
 - @param {string} lastname in Stringformat
 - @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 - Calculate the number of days between two dates.
 - @param {*} endDate
 - @param {*} startDate
 - @name days Calculates the numebr of days between two dates
 - @returns {number} returns the number of days between two dates
 */
function days(endDate, startDate) {
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // return zero if dates are valid
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// eslint-disable-next-line import/prefer-default-export
export { getFullName, days };
```

![Aggiunta di una funzione personalizzata](/help/edge/docs/forms/assets/create-custom-function.png)

### Utilizzare una funzione personalizzata nell’editor di regole

Per utilizzare una funzione personalizzata nell’editor di regole:

1. **Aggiungi funzione**: aggiungi la funzione personalizzata al file `../[blocks]/form/functions.js`. Assicurarsi di includerlo nell&#39;istruzione `export` nel file.
2. **Distribuisci il file**: distribuisci il file `functions.js` aggiornato nel progetto GitHub e verifica che la compilazione sia stata completata correttamente.
3. **Utilizzo funzione**: nell&#39;Editor regole del modulo, accedere alla funzione selezionando l&#39;opzione `Function Output` nel campo **[!UICONTROL Seleziona azione]**.

   ![Funzione personalizzata nell’editor di regole](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

4. **Anteprima del modulo**: visualizza l&#39;anteprima del modulo per verificare che la nuova funzione implementata funzioni come previsto.

## Best practice per lo sviluppo delle regole

### **Ottimizzazione delle prestazioni**

**Ridurre Al Minimo La Complessità Delle Regole**

- Mantieni le singole regole semplici e mirate.
- Suddividi la logica complessa in più regole più piccole.
- Se possibile, evita le condizioni annidate in profondità.

**Ottimizza esecuzione regola**

- Inserisci prima le regole attivate più di frequente.
- Utilizza condizioni specifiche per ridurre le valutazioni non necessarie.
- Considera l’impatto delle regole sul tempo di caricamento dei moduli.

**Gestione risorse**

- Limita il numero di regole per componente modulo.
- Utilizza funzioni personalizzate per logica ripetuta invece di duplicare le regole.
- Verifica le prestazioni con volumi di dati realistici.

### **Linee guida per l&#39;esperienza utente**

**Cancella feedback**

- Utilizzare messaggi di convalida che guidano gli utenti verso l&#39;input corretto.
- Mostra gli indicatori di caricamento per le regole che coinvolgono servizi esterni.
- Implementa la divulgazione progressiva per ridurre il carico cognitivo.

**Gestisci reattività modulo**

- Evita le regole che causano improvvisi cambiamenti visivi.
- Implementare transizioni graduali per le operazioni di visualizzazione/nascondere.
- Verifica le regole su dispositivi e dimensioni di schermo diversi.

**Gestione errori**

- Fornisci un comportamento di fallback quando le regole non riescono.
- Visualizzare messaggi di errore intuitivi.
- Registra gli errori per il debug mantenendo un’esperienza utente positiva.

### **Best practice per lo sviluppo**

**Strategia di test**

- Verifica le regole con casi di spigoli e valori limite.
- Verifica il comportamento delle regole tra browser diversi.
- Test della funzionalità dei moduli con e senza JavaScript abilitato.

**documentazione**

- Documentare la logica di business alla base di regole complesse.
- Gestisce un inventario di regole per i moduli di grandi dimensioni.
- Utilizza convenzioni di denominazione coerenti per componenti e regole.

**Controllo versione**

- Tieni traccia delle modifiche alle funzioni personalizzate nel controllo della versione.
- Test delle regole in un ambiente di sviluppo prima della produzione.
- Gestisci copie di backup delle configurazioni delle regole di lavoro.

## Risoluzione dei problemi comuni

### **Problemi di esecuzione delle regole**

**Impossibile attivare le regole**

- **Controllare i nomi dei componenti**: verificare che i componenti a cui si fa riferimento esistano e che i nomi siano corretti.
- **Verifica ordine regole**: le regole vengono eseguite dall&#39;alto verso il basso; riordinarle se necessario.
- **Convalida condizioni**: condizioni di test con valori noti per verificare la logica.
- **Console browser**: verificare la presenza di errori JavaScript che potrebbero bloccare l&#39;esecuzione.

**Comportamento regola non corretto**

- **Operatori logici di revisione**: verificare che le condizioni AND/OR siano strutturate correttamente.
- **Verifica con dati di esempio**: utilizza valori noti per isolare i problemi.
- **Controllare i tipi di dati**: assicurarsi che i confronti numerici utilizzino numeri, non stringhe.
- **Convalida espressioni**: verifica le espressioni matematiche separatamente.

### **Problemi relativi alle prestazioni**

**Risposta modulo lenta**

- **Ridurre la complessità delle regole**: semplificare la logica condizionale complessa.
- **Ottimizzare le funzioni personalizzate**: profilare e ottimizzare il codice JavaScript.
- **Limita chiamate esterne**: riduci al minimo le chiamate al servizio nelle regole.
- **Utilizzare selettori efficienti**: verificare che i riferimenti agli oggetti modulo siano specifici.

**Utilizzo memoria**

- **Pulizia listener di eventi**: rimuovere le associazioni di regole non utilizzate.
- **Ottimizzare le funzioni personalizzate**: evitare perdite di memoria nel codice JavaScript.
- **Limita ambito regola**: utilizza regole di destinazione anziché condizioni globali.

### **Problemi con la funzione personalizzata**

**Funzioni non disponibili**

- **Controllare il percorso del file**: verificare che `functions.js` si trovi nel percorso corretto: `/blocks/form/functions.js`.
- **Verifica esportazioni**: verificare che le funzioni siano esportate correttamente.
- **Processo di compilazione**: verificare che la compilazione del progetto includa il file delle funzioni aggiornato.
- **Cancellazione della cache**: cancella la cache del browser dopo aver distribuito nuove funzioni.

**Errori di funzione**

- **Convalida parametro**: verificare che i parametri della funzione corrispondano ai tipi previsti.
- **Gestione degli errori**: aggiungi blocchi try-catch per gestire le eccezioni in modo corretto.
- **Registrazione console**: utilizzare console.log per l&#39;esecuzione della funzione di debug.
- **Convalida JSDoc**: verifica che la documentazione della funzione corrisponda all&#39;implementazione.

### **Integrazione editor universale**

**Editor Regole Non Visualizzato**

- **Estensione abilitata**: verificare che l&#39;estensione dell&#39;editor di regole sia attivata.
- **Selezione di componenti**: verificare di aver selezionato un componente modulo supportato.
- **Compatibilità browser**: verifica nei browser supportati (Chrome, Firefox, Safari).
- **Autorizzazioni di accesso**: verificare che l&#39;utente disponga delle autorizzazioni AEM necessarie.

**Problemi di interfaccia**

- **Visibilità pannello**: utilizzare il pulsante di attivazione/disattivazione per mostrare o nascondere il pannello oggetti modulo.
- **Salvataggio regola**: assicurati che le regole siano salvate prima di chiudere l&#39;editor.
- **Zoom del browser**: reimposta lo zoom del browser al 100% per una visualizzazione ottimale dell&#39;interfaccia.

## Limitazioni importanti

>[!IMPORTANT]
>
> **Restrizioni funzioni personalizzate**:
>
> - Le importazioni statiche e dinamiche non sono supportate negli script di funzioni personalizzati.
> - Tutto il codice deve essere incluso direttamente nel file `/blocks/form/functions.js`.
> - Le funzioni devono essere sincrone (senza async/await o Promises).
> - L’accesso alle API del browser è limitato per motivi di sicurezza.

>[!WARNING]
>
> **Considerazioni sulla produzione**:
>
> - Verifica a fondo tutte le regole in un ambiente di staging.
> - Monitora le prestazioni dei moduli dopo la distribuzione di regole complesse.
> - Disporre di un piano di ripristino per i problemi correlati alle regole.
> - Considera l’impatto sugli utenti con connessioni di rete lente.

## Riepilogo

L’Editor di regole nell’Editor universale consente di creare moduli intelligenti e dinamici che forniscono esperienze utente eccezionali. Implementando la logica condizionale, i calcoli automatizzati e le regole aziendali personalizzate, è possibile:

**Trasforma Forms statico**:

- Aggiunta della visibilità dei campi condizionali per interfacce più pulite e mirate.
- Implementa calcoli in tempo reale e convalida dei dati.
- Crea una logica di business sofisticata senza codificare.

**Migliora l&#39;esperienza utente**:

- Guida gli utenti attraverso i flussi di moduli logici.
- Riduci gli errori con la convalida intelligente.
- Fornisci feedback e assistenza immediati.

**Maggiore efficienza**:

- Automatizzare i calcoli ripetitivi e l&#39;immissione dei dati.
- Semplifica i flussi di lavoro complessi con il routing intelligente.
- Riduzione del carico di supporto con funzionalità self-service.

### **Passaggi successivi**

Ora che conosci le nozioni di base dell’Editor regole:

1. **Inizia semplice**: inizia con le regole di base per mostrare/nascondere prima di passare a calcoli complessi.
1. **Esercitazione con esempi**: utilizzare l&#39;esercitazione del calcolatore delle imposte come base.
1. **Esplora le funzionalità avanzate**: prova le funzioni personalizzate per i requisiti specifici.
1. **Verifica approfondita**: convalida sempre le regole in scenari e dispositivi diversi.
1. **Monitoraggio delle prestazioni**: assicurarsi che le regole migliorino l&#39;esperienza utente anziché ostacolarla.
