---
title: Oggetto Campo di testo nell’editor di comunicazione interattiva
description: Oggetto Campo di testo nell’Editor di comunicazione interattiva in AEM Forms per consentire agli autori di visualizzare informazioni quali nomi, indirizzi, commenti o ID numerici.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 7%

---


# Oggetto Campo di testo nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Il componente Campo di testo nell’editor di comunicazione interattiva (IC) consente agli autori di visualizzare informazioni quali nomi, indirizzi, commenti o ID numerici. Il valore visualizzato nel campo di testo è predefinito (statico) o viene compilato dinamicamente utilizzando l&#39;associazione dati. Supporta le voci a riga singola, le regole di convalida e la formattazione flessibile, rendendola uno degli elementi più utilizzati e versatili nelle comunicazioni personalizzate.

![Trova documento IC](/help/forms/interactive-communication/assets/textfield.png)

## &#x200B;2. Proprietà

2.1 Campo di base

- **Nome:** Definisci un identificatore univoco per il campo, utilizzato in modelli di dati, regole e script.

- **Didascalia:** Visualizza l&#39;etichetta visualizzata sullo schermo (ad esempio, &quot;Nome&quot;).

- **Valore:** Visualizza testo come nomi, indirizzi, note o altri dettagli. Il valore è statico o derivato dall&#39;associazione dati.

- **Riserva:** Impostare l&#39;allineamento del valore, a sinistra, a destra, in alto o in basso oppure specificare una posizione personalizzata utilizzando unità di misura come i millimetri (ad esempio, 20 mm).

- **Aspetto:** Impostare l&#39;aspetto della casella dei valori su Nessuno, Casella continua o Sottolineato in base al layout visivo desiderato.

2.2 Tipografia

Controlla lo stile visivo dei caratteri digitati:

- **Convalida carattere:** Applica vincoli facoltativi per convalidare il formato del valore visualizzato, ad esempio consentendo solo alfabeti, numeri o pattern personalizzati specifici.

- **Dimensione carattere:** Regolare la dimensione del testo all&#39;interno del campo utilizzando valori di punto come 10 pt, 12 pt, 20 pt, ecc., per garantire leggibilità e allineamento con gli standard di progettazione.

2.3 Posizione

Definisce il posizionamento del campo all’interno del layout:

- **coordinate X / Y**

- **Larghezza e altezza** (mm, px o %)

2.4 Margine

Specifica la spaziatura attorno al contenitore di campi:

- Superiore (Su)

- Inferiore (giù)

- Sinistra

- Destra

2.5 Aspetto

Personalizza lo stile del contenitore di campi:

- **Riempimento:** Impostare il colore di sfondo della casella di testo. In questo modo è possibile distinguere le aree di input o allinearle ai colori del marchio.

- **Tratto:** Aggiungere bordi attorno alla casella di testo con le seguenti proprietà personalizzabili:

- **Larghezza:** Definire lo spessore del bordo.

- **Stile:** Scegliere uno degli stili di bordo a tinta unita, tratteggiato o punteggiato.

- **Edge:** Selezionare la forma degli angoli, arrotondata o tagliente.

- **Raggio:** regola la curvatura d&#39;angolo utilizzando i valori di raggio (ad esempio, 4 px, 10 px) per ottenere un aspetto più morbido o angolare.

2.6 Presenza

Determina la visibilità in fase di runtime:

- **Visibile:** mostrato e occupa spazio

- **Nascosto (mantiene spazio):** invisibile ma lo spazio di layout è riservato

2.7 Associazione dei dati

Collega il campo di testo a un&#39;origine dati per visualizzare i valori in modo dinamico o statico all&#39;interno della comunicazione.

- **Tipo di associazione dati:** Specifica la modalità di connessione del campo a un&#39;origine dati o a uno schema.

- **Nome utilizzo:** associa il campo di testo utilizzando il nome del campo definito nel modello di dati o nello schema, consentendo la visualizzazione di testo dinamico in base a dati esterni.

- **Usa dati globali:** collega il campo ai dati globali condivisi nell&#39;intera comunicazione per una visualizzazione coerente delle informazioni.

- **Nessuna associazione dati:** mantiene il campo scollegato da qualsiasi origine back-end. Viene utilizzato per visualizzare valori statici o testo destinato solo al contesto visivo.

## &#x200B;3. Utilizzo

Gli scenari comuni includono:

- Acquisizione dei dati personali (nomi, indirizzi, numeri di telefono)

- Accettazione di commenti o feedback (multilinea)

- Inserimento di numeri di criteri o ID account

- Raccolta di valori numerici brevi come codici PIN o OTP

Gli autori possono inserire il campo in sottomaschere o griglie layout per l’allineamento e allegare regole di convalida (limiti di lunghezza, pattern regex) per garantire un input ordinato.

## &#x200B;4. Best practice

- Applica la convalida (flag obbligatori, controlli pattern) per un feedback immediato.

- Specificare un testo di riserva significativo per le visualizzazioni stampate o di sola lettura.

- Tipografia coerente con le linee guida del marchio.

- Riduci la larghezza del campo sui layout mobili per adattarla a schermi più piccoli.

- Se possibile, associa direttamente al modello dati per semplificare la manutenzione.

L&#39;oggetto Campo di testo nell&#39;editor IC è un blocco predefinito versatile che semplifica l&#39;acquisizione dei dati. Se configurato in modo accurato, con tipografia ben scelta, etichette chiare, convalida corretta e associazione dati solida, offre un’esperienza fluida e intuitiva e dati affidabili per l’elaborazione a valle.


