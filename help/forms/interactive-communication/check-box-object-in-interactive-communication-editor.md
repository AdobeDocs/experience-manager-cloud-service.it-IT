---
title: Oggetto CheckBox nell’editor di comunicazione interattiva
description: L’oggetto CheckBox nell’editor di comunicazione interattiva di AEM Forms consente agli utenti di effettuare selezioni binarie singole o multiple (sì/no, true/false).
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 8%

---


# Oggetto CheckBox nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Il componente Casella di controllo nell’editor di comunicazione interattiva (IC) consente agli utenti di effettuare selezioni binarie singole o multiple (sì/no, true/false). Utilizzato comunemente per termini e condizioni, preferenze, campi di consenso e opt-in, fornisce un modo rapido per acquisire l’input booleano all’interno di un modulo di comunicazione.

La casella di controllo supporta stili flessibili, opzioni di associazione dati e regole di visibilità, rendendola uno strumento leggero ma potente nella progettazione di moduli interattivi e facili da usare.

![Trova documento IC](/help/forms/interactive-communication/assets/checkbox.png)

## &#x200B;2. Proprietà

2.1 Campo di base

- **Nome:** Identificatore univoco utilizzato per fare riferimento alla casella di controllo nei modelli di dati, nelle regole o negli script.

- **Attiva/Disattiva:** consente di attivare/disattivare la casella di controllo quando si fa clic su di essa. Può essere utilizzato in modalità singola o raggruppata.

- **Didascalia:** etichetta descrittiva visualizzata accanto alla casella di controllo, che indica agli utenti cosa accettano o selezionano.

- **Riserva:** Testo o simbolo segnaposto facoltativo visualizzato in modalità di sola lettura o di fallback quando non viene effettuata alcuna interazione.

2.2 Posizione

Definisce la posizione della casella di controllo nel layout:

- **Coordinate X e Y:** Impostare la posizione della casella di controllo all&#39;interno della griglia di layout.

- **Altezza e larghezza:** Definisce le dimensioni della casella di controllo (in mm o px), particolarmente importanti quando si utilizzano stili visivi o icone personalizzati.

2.3 Margine

Consente la spaziatura intorno alla casella di controllo per le regolazioni del layout:

- Superiore (Su)

- Inferiore (giù)

- Sinistra

- Destra

2.4 Aspetto

Controlla lo stile visivo della casella di controllo e del relativo frame:

- **Riempimento:** Colore di sfondo della casella di controllo (se selezionata o deselezionata).

- **Tratto:** colore del contorno della casella di controllo.

- **Larghezza tratto:** Spessore della linea del bordo.

- **Stile:** pattern di struttura solido, tratteggiato o personalizzato.

- **Spigoli:** Definisce lo stile degli angoli della casella di controllo: spigoli arrotondati o vivi a seconda delle preferenze di progettazione.

2.5 Presenza

Determina come e quando viene visualizzata la casella di controllo in fase di runtime:

- **Visibile:** visualizzato normalmente e occupa spazio.

- **Nascosto (mantiene spazio):** Nascosto dall&#39;interfaccia utente, ma lo spazio di layout viene mantenuto. Utile per la visibilità condizionale senza interruzione del layout.

2.6 Associazione dei dati

Consente alla casella di controllo di interagire con origini dati esterne o interne:

**Tipo di associazione dati:**

**Nome utente:** associa il valore utilizzando il nome del campo del componente.

**Usa dati globali:** si connette a un modello dati globale condiviso nella comunicazione.

**Nessuna associazione dati:** La casella di controllo rimane autonoma e non viene memorizzata nel modello dati.

&#x200B;3. Utilizzo

Le caselle di controllo sono comunemente utilizzate in scenari come:

- **Campi di consenso:** ad esempio, &quot;Accetto i termini e le condizioni&quot;

- **Preferenze utente:** ad esempio, &quot;Iscriviti alla newsletter&quot;

- **Selezioni multiple:** ad esempio, &quot;Seleziona tutte le opzioni applicabili&quot;

- **Riconoscimenti modulo:** ad esempio, &quot;Confermo che i dettagli di cui sopra sono corretti&quot;

Le caselle di controllo possono essere posizionate all&#39;interno di griglie o pannelli layout e raggruppate insieme per una migliore organizzazione nei moduli.

&#x200B;4. Best practice

- Utilizza sottotitoli chiari e concisi per aiutare gli utenti a comprendere cosa stanno selezionando.

- Evita l&#39;ingombro utilizzando le caselle di controllo solo per gli input binari; utilizza i pulsanti di scelta per le opzioni esclusive.

- Assicurati che la spaziatura sia corretta utilizzando le impostazioni di margine e layout per un’interfaccia utente pulita.

- Associa le caselle di controllo a un riferimento significativo al modello di dati quando la scelta acquisita deve essere memorizzata o elaborata.

- Utilizza le regole di visibilità quando le caselle di controllo dipendono da input o condizioni precedenti.

L’oggetto Check Box nell’editor di comunicazioni interattive è un componente semplice ma essenziale per gli input binari. Grazie al supporto per lo stile, la presenza condizionale e l’associazione flessibile dei dati, riveste un ruolo chiave nel miglioramento dell’interattività e del controllo degli utenti nei moduli digitali intelligenti. Se implementate con etichette ponderate, stili coerenti e un’integrazione significativa dei dati, le caselle di controllo contribuiscono in modo significativo a creare un’esperienza di modulo fluida e intuitiva.


