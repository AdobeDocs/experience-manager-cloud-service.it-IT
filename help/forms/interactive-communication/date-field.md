---
title: Oggetto campo data nell’editor di comunicazione interattiva
description: L’oggetto campo data nell’Editor di comunicazione interattiva in AEM Forms consente agli autori di inserire in un documento un campo di selezione data basato su calendario.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 8%

---


# Oggetto campo data nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Il componente **Campo data** nell&#39;editor di comunicazione interattiva (IC) consente agli autori di inserire in un documento un campo di selezione data basato sul calendario. Questo consente agli utenti di scegliere facilmente una data da un selettore di date o di immetterla manualmente in un formato predefinito.

Ideale per acquisire date di nascita, pianificazioni di appuntamenti, date di applicazione o date di inizio/fine dei criteri, il campo Data migliora la precisione e riduce gli errori di input. Supporta la formattazione, lo stile e il binding dei dati per un’integrazione perfetta con i modelli di dati e i sistemi back-end.

![Trova documento IC](/help/forms/interactive-communication/assets/date.png)

## &#x200B;2. Proprietà

L&#39;oggetto Date Field include diverse proprietà configurabili:

2.1. Campo di base

- **Nome:** Identificatore univoco utilizzato per fare riferimento al campo all&#39;interno di regole, script e modelli dati.

- **Didascalia:** etichetta visualizzata dall&#39;utente (ad esempio, &quot;Data di nascita&quot;).

- **Data:** il valore effettivo della data, che può essere vuoto per impostazione predefinita o prepopolato utilizzando dati dinamici.

- **Riserva:** Data di fallback facoltativa (visualizzata se non è selezionata alcuna data o se i dati non sono disponibili).

- **Aspetto:** un predefinito di stile rapido (ad esempio sottolineato, piatto, con bordi) per coerenza visiva.

2.2. Tipografia

Controlla l’aspetto della data all’interno del campo:

- **Variante carattere:** Scegliere la famiglia di caratteri, lo spessore (ad esempio Normale, Grassetto) e lo stile (ad esempio Corsivo).

- **Dimensione:** In genere è impostata su 10 pt per impostazione predefinita, ma personalizzabile per coerenza con il contenuto circostante.

2.3. Posizione

Definisce il posizionamento spaziale all&#39;interno del layout del documento:

- **Coordinate X e Y:** Determina il posizionamento orizzontale e verticale.

- **Larghezza e altezza:** Impostare in millimetri o percentuali per l&#39;allineamento con altri elementi del modulo.

2.4. Margine

Specifica la spaziatura attorno ai limiti del campo:

- Superiore (Su)

- Inferiore (giù)

- Sinistra

- Destra

Questi valori facilitano l’allineamento preciso all’interno di sottomaschere o griglie di layout.

2.5. Aspetto

Definisce lo stile visivo del contenitore di campi:

- **Riempimento:** Colore di sfondo del campo (ad esempio bianco, grigio chiaro).

- **Tratto:** Colore o contorno del bordo.

- **Larghezza:** spessore del bordo del campo.

- **Stile:** opzioni linea continua, tratteggiata o tratteggiata.

- **Spigoli:** Personalizza gli angoli come arrotondati o netti per le diverse preferenze di progettazione.

2.6. Presenza

Determina come e quando viene visualizzato il campo:

- **Visibile:** impostazione predefinita in cui il campo viene visualizzato in fase di esecuzione.

- **Campo nascosto (mantiene spazio):** Il campo rimane invisibile, ma lo spazio di layout viene mantenuto.

Questa funzione è utile quando si attiva o si attiva la visibilità in modo dinamico in base alle regole o agli input dell’utente.

2.7. Associazione dei dati

Collega il campo Data alle strutture di dati per la memorizzazione o la precompilazione dei valori.

**Tipo di associazione dati:**

- **Nome utente:** associa il campo allo schema utilizzando il relativo attributo name.

- **Usa dati globali:** Associa tramite un elemento schema o modello dati predefinito.

- **Nessuna associazione dati:** Il campo rimane statico e non è connesso ad alcuna origine dati.

Questo consente di recuperare, visualizzare o archiviare i valori di data dinamici in base alla logica dell’applicazione.

## &#x200B;3. Utilizzo

Il campo Data è particolarmente utile nei seguenti scenari:

- Acquisizione della data di nascita o di iscrizione nei moduli di onboarding.

- Selezionare le date di inizio e di fine per servizi, abbonamenti o eventi.

- Inserimento di scadenze di applicazione, slot di appuntamento o date di verifica.

Gli autori possono inserire il campo data all’interno di contenitori di layout o sottomaschere e configurare la convalida (ad esempio, formato della data, limiti di intervallo) per migliorare la qualità dei dati.

## &#x200B;4. Best practice

- Utilizza sottotitoli chiari come &quot;Start Date&quot; (Data di inizio) o &quot;Select Appointment Date&quot; (Seleziona data appuntamento) per una migliore esperienza utente.

- Imposta intervalli di date minimi e massimi per evitare input non validi (ad esempio, DOB futuri).

- Applicare stili di carattere coerenti (10 pt consigliati) per migliorarne la leggibilità.

- Associa i campi allo schema quando è necessaria l’integrazione dei dati di back-end.

- Nascondi dinamicamente campi data non rilevanti utilizzando le regole di visibilità.

L&#39;oggetto **Date Field** nell&#39;editor di comunicazioni interattive è uno strumento potente per acquisire dati sensibili al tempo con precisione e facilità. Se formattato in modo accurato e connesso a percorsi di dati significativi, supporta un’esperienza utente fluida ed efficiente nell’elaborazione delle voci basate sul tempo.


