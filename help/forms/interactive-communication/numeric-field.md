---
title: Componente Campo numerico nell’editor di comunicazione interattiva
description: Componente Campo numerico nell’editor di comunicazioni interattive in AEM Forms per consentire agli autori di raccogliere input numerici dagli utenti in un formato controllato.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 7%

---


# Componente Campo numerico nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Il componente Campo numerico nell’editor di comunicazione interattiva (IC) consente agli autori di raccogliere input numerici dagli utenti in un formato controllato. Che si tratti di numeri di telefono, codici PIN, ID policy o dati finanziari, questo campo assicura che vengano accettati solo i valori numerici. Il componente supporta anche lo stile, la formattazione, la convalida e l’associazione dati, rendendolo essenziale per le comunicazioni strutturate.

![Trova documento IC](/help/forms/interactive-communication/assets/numericfield.png)

## &#x200B;2. Proprietà

2.1 Campo di base

- **Nome:** Definisci un identificatore univoco per il campo, utilizzato in modelli di dati, regole e script.

- **Didascalia:** Visualizza l&#39;etichetta visualizzata sullo schermo (ad esempio, &quot;Numero di contatto&quot; o &quot;ID dipendente&quot;).

- **Valore:** Consente agli utenti di immettere valori numerici quali numeri di telefono, ID, quantità o valori monetari.

- **Riserva:** Impostare l&#39;allineamento del valore numerico (a sinistra, a destra, in alto o in basso) oppure specificare una posizione personalizzata utilizzando unità di misura come i millimetri (ad esempio, 20 mm).

- **Aspetto:** Impostare l&#39;aspetto della casella dei valori su Nessuno, Casella continua o Sottolineato in base al layout visivo desiderato.

2.2 Tipografia

Controlla lo stile visivo dei caratteri numerici immessi dall&#39;utente:

- **Convalida font:** Applica vincoli per garantire che venga accettato solo un input numerico valido, ad esempio numeri interi, decimali o intervalli di numeri, in base al tipo di dati previsto.

- **Dimensione carattere:** Regolare la dimensione del testo numerico utilizzando valori come 10 pt, 12 pt o 20 pt per mantenere coerenza e leggibilità nel modulo.

2.3 Posizione

Controlla la posizione spaziale del campo numerico nell&#39;area di lavoro.

- **Coordinate X e Y:** Definire il posizionamento esatto del campo.

- **Larghezza e altezza (in mm):** determina le dimensioni della casella di input.

2.4 Margine

Definisce la spaziatura attorno al limite del campo numerico per un allineamento pulito.

- Superiore (Su)

- Inferiore (giù)

- Sinistra

- Destra

2.5 Aspetto

Personalizza lo stile del contenitore del campo di input numerico in modo che corrisponda al layout visivo desiderato:

- **Riempimento:** Imposta il colore di sfondo del campo numerico. Questo lo aiuta a separarlo visivamente da altri elementi o a combaciarlo con il tema generale.

- **Tratto:** Aggiungi bordi attorno al campo numerico con le seguenti opzioni personalizzabili:

- **Larghezza:** Definire lo spessore del bordo in base all&#39;enfasi visiva.

- **Stile:** Scegliere un motivo di bordo, solido, tratteggiato o punteggiato.

- **Edge:** Seleziona gli angoli arrotondati o vivi del bordo.

- **Raggio:** Regola la rotondità degli angoli utilizzando valori di raggio specifici (ad esempio, 4 px, 10 px) per attenuare o rendere più nitido l&#39;aspetto del campo.

2.6 Presenza

Controlla la visibilità del campo numerico durante il runtime.

- **Visibile:** stato predefinito; il campo viene visualizzato normalmente.

- **Campo nascosto (mantiene spazio):** Campo invisibile, ma lo spazio viene mantenuto nel layout.

2.7 Associazione dei dati

**Tipo di associazione dati:** collega il campo numerico a un&#39;origine dati (XML o JSON) per l&#39;integrazione in tempo reale.

**Usa nome:** associa il campo al relativo nome univoco per l&#39;acquisizione di valori semplici.

**Usa dati globali:** Collega il campo a un nodo di dati condiviso tra moduli o frammenti.

**Nessuna associazione dati:** mantiene il campo statico per l&#39;utilizzo solo visivo o per l&#39;input temporaneo.

## &#x200B;3. Utilizzo

I campi numerici sono ideali negli scenari in cui solo le cifre sono input validi. I casi d’uso comuni includono:

- Acquisizione di **numeri di cellulare, OTP e PIN**

- Inserimento di **numeri dei criteri o ID dei dipendenti**

- Raccolta di **quantità numeriche o valori monetari**

- Abilitazione di **campi numerici basati su passaggi** (ad esempio, contatori o voci di punteggio)

Gli autori possono inserire campi numerici all’interno di contenitori o sottomaschere di layout e applicare la convalida (come vincoli di lunghezza, valore minimo o massimo) per migliorare la qualità dei dati.

## &#x200B;4. Best practice

- Etichetta chiaramente i campi numerici con le unità, se necessario (ad esempio, &quot;Quantità in ₹&quot;).

- Applica la convalida del formato (come i limiti di 10 cifre per i numeri di telefono) per una maggiore precisione.

- Utilizza i valori di riserva quando i campi sono obbligatori, ma potrebbero mancare dati dinamici.

- Associa accuratamente i campi numerici ai percorsi dello schema per supportare l’elaborazione back-end.

- Mantieni l’aspetto coerente e la tipografia per rispettare le linee guida del brand.

Il componente **Campo numerico** nell&#39;editor di comunicazioni interattive è uno strumento preciso e affidabile per la raccolta dati basata sulle cifre. Grazie alla formattazione affidabile, ai controlli di visibilità e alle opzioni di associazione dei dati, gli input numerici vengono acquisiti in modo chiaro e integrati perfettamente nei moduli digitali. Se formattato e configurato correttamente, migliora notevolmente l’usabilità dei moduli e la precisione complessiva dei dati.


