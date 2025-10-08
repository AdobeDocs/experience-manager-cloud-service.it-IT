---
title: Campo data/ora nell’editor di comunicazione interattiva
description: Il componente Campo data/ora nell’Editor comunicazioni interattive di AEM Forms consente agli autori di inserire campi in cui gli utenti possono selezionare o immettere valori di data e/o ora.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 8%

---


# Componente Campo data/ora nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Il componente **Campo data/ora** nell&#39;editor di comunicazione interattiva (IC) consente agli autori di inserire campi in cui gli utenti possono selezionare o immettere valori di data e/o ora. Questo componente viene comunemente utilizzato per acquisire informazioni come data di nascita, pianificazioni di appuntamenti, slot di prenotazione o date di rilascio/scadenza dei documenti.

Il campo supporta varie opzioni di formattazione (ad esempio GG/MM/AAAA, formati a 24 ore o a 12 ore), vincoli di convalida e personalizzazione dell’aspetto in base al design della comunicazione. Migliora l’esperienza utente riducendo gli errori di inserimento manuali e promuovendo la coerenza nella raccolta dei dati.

![Trova documento IC](/help/forms/interactive-communication/assets/datetime.png)

## &#x200B;2. Proprietà

Il componente Campo data/ora include diverse proprietà configurabili:

2.1. Campo di base

- **Nome:** Identificatore univoco del campo. Utilizzato per fare riferimento a regole, espressioni e associazioni di dati.

- **Didascalia:** etichetta visualizzata accanto al campo per indicarne lo scopo (ad esempio, &quot;Data di nascita&quot;).

- **Data:** consente agli utenti di scegliere o inserire una data calendario.

- **Ora:** abilita l&#39;immissione o la selezione di valori di ora specifici, se configurati.

- **Riserva:** Se non viene fornito alcun input, viene visualizzato un valore di fallback utile per gli scenari di sola lettura o di stampa.

- **Aspetto:** Selezionare uno stile di visualizzazione, ad esempio sottolineato, con bordi o piatto, per un rendering dell&#39;interfaccia utente coerente.

2.2. Tipografia

Controlla lo stile del testo all&#39;interno del campo data/ora:

- **Variante font:** Le opzioni includono Regolare, Grassetto, Corsivo a seconda dei requisiti del tema.

- **Dimensione carattere:** Impostazione predefinita impostata su 10 pt per mantenere la coerenza con il layout del modulo.

2.3. Posizione

- **Descrizione:** definisce la posizione del campo data/ora nel layout del modulo.

- **Impostazioni:**

   - **coordinate X e Y**

   - **Altezza e larghezza** (misurate in mm o pixel) per ridimensionare con precisione il campo.

2.4. Margine

Definisce la spaziatura intorno al campo per un allineamento pulito e la flessibilità del layout:

- Superiore (Su)

- Inferiore (giù)

- Sinistra

- Destra

2.5. Aspetto

Definisce lo stile del contenitore per mantenere coerenza e chiarezza visiva:

- **Riempimento:** Colore di sfondo del campo.

- **Tratto:** Colore del bordo intorno al campo.

- **Larghezza:** Spessore del bordo.

- **Stile:** Tipi di bordo come solido, tratteggiato o nessuno.

- **Spigoli:** Scegli tra angoli vivi o arrotondati a seconda del tema del modulo.

2.6. Presenza

Determina il comportamento del campo in fase di esecuzione:

- **Visibile:** Il campo viene visualizzato agli utenti e occupa lo spazio di layout.

- **Nascosto (mantiene spazio):** Il campo non è visibile ma lo spazio è ancora riservato nel layout.

2.7. Associazione dei dati

Collega il campo a un&#39;origine dati per memorizzare o recuperare i valori.

- **Tipo di associazione dati:** Specifica la connessione del campo ai dati.

- **Nome utente:** associa il campo utilizzando il nome di campo definito nello schema.

- **Usa dati globali:** collega il campo ai dati a livello globale condivisi nella comunicazione.

- **Nessuna associazione dati:** Il campo non è connesso ad alcun dato di back-end (utilizzato solo per valori calcolati o di tipo visivo).

## &#x200B;3. Utilizzo

Il campo data/ora è ideale negli scenari in cui sono necessari dati temporali coerenti. I casi d’uso comuni includono:

- Acquisizione della data di nascita, della data di appuntamento o dell’ora dell’evento

- Registrazione delle date di rilascio/scadenza del documento

- Selezione degli slot di consegna o di ritiro

- Registrazione marche temporali transazione

Gli autori possono combinare il campo con contenitori di layout, convalide o regole condizionali per controllare il formato, i campi obbligatori e la visibilità sensibile al contesto.

## &#x200B;4. Best practice

- Utilizza sottotitoli chiari come &quot;Seleziona una data&quot; o &quot;Ora appuntamento&quot; per guidare gli utenti.

- Abilita il selettore data/ora per una migliore interfaccia utente e meno errori di input.

- Applica restrizioni di formato (ad esempio, solo date future) quando necessario.

- Specifica un valore di riserva per l&#39;accessibilità o il fallback di stampa.

- Mantenere la composizione tipografica e l&#39;aspetto coerenti con la struttura generale del modulo.

- Associa il campo a un percorso di schema valido per garantire l’acquisizione e l’elaborazione corretta dei dati.

Il componente Campo data/ora nell’editor di comunicazione interattiva è un componente potente e intuitivo che semplifica l’input basato sul tempo. Con la giusta configurazione di stile, gestione dei dati e controlli di layout, consente esperienze di modulo pulite, affidabili e intuitive sia per gli utenti che per i sistemi back-end.

